---
title: Preparare Intune per la migrazione degli utenti
titleSuffix: Configuration Manager
description: Informazioni su come preparare Intune in Azure per la migrazione degli utenti dalla soluzione MDM ibrida.
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 226586f0ee42cdad98b1d74f25421685d85e0dcf
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2017
---
# <a name="prepare-intune-for-user-migration"></a>Preparare Intune per la migrazione degli utenti 

*Si applica a: System Center Configuration Manager (Current Branch)*    

Prima di eseguire la migrazione degli utenti dalla soluzione MDM ibrida (Intune integrato con Configuration Manager) alla versione autonoma di Intune, è necessario eseguire i passaggi di preparazione di Intune. Questi passaggi garantiscono la continuità della gestione degli utenti di cui viene eseguita la migrazione e dei relativi dispositivi. Quando si completano questi passaggi e si avvia la migrazione a Intune, l'operazione dovrebbe essere trasparente per gli utenti.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Correggere i problemi riscontrati durante la raccolta e l'importazione dei dati
Se è stato eseguito il processo di [importazione dei dati di Configuration Manager in Microsoft Intune](migrate-import-data.md), lo strumento di importazione dati di Intune ha fornito un riepilogo di tutti gli oggetti che non è stato possibile importare. Alcuni dei problemi tipici che si potrebbero riscontrare con i passaggi da eseguire per risolvere il problema in Intune sono elencati nella tabella seguente: 

|Problema  |Correzione  |
|---------|---------|
|Non è possibile eseguire automaticamente la migrazione delle raccolte basate sull'appartenenza diretta o su un tipo complesso.|È necessario creare gruppi di Azure Active Directory (AAD) in Azure per sostituire la raccolta che non è stata importata. Assegnare quindi l'oggetto al gruppo.|
|I criteri non possono essere importati |È necessario ricreare i criteri in Intune.|
|La distribuzione di un oggetto non viene importata|È necessario assegnare l'oggetto al gruppo. Il gruppo deve contenere gli stessi utenti dalla raccolta per la distribuzione.|

## <a name="create-intune-objects"></a>Creare oggetti di Intune 
Se è stato eseguito il processo di [importazione dei dati di Configuration Manager in Microsoft Intune](migrate-import-data.md) e sono stati risolti i problemi riscontrati durante il processo di importazione, è necessario verificare che gli oggetti importati siano configurati correttamente. Creare inoltre in Intune gli oggetti aggiuntivi (criteri, profili, app e così via) necessari nell'organizzazione. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Assegnare le licenze di Intune agli utenti di cui è stata eseguita la migrazione
In Configuration Manager aggiungere una raccolta alla sottoscrizione di Intune e i membri della raccolta avranno la possibilità di registrare i propri dispositivi. Mentre la licenza di Intune è riservata ai dispositivi registrati, queste licenze non sono associate in modo specifico all'utente o al dispositivo. Non si troverà, ad esempio, una licenza di Intune in AAD per un utente che ha un dispositivo registrato. Nella versione autonoma di Intune, tuttavia, è necessario configurare una licenza di Intune per ogni utente. Eseguire questa operazione PRIMA di eseguire la migrazione di un utente alla versione autonoma di Intune, per garantire che l'utente e i relativi dispositivi siano gestiti da Intune dopo la modifica all'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign) (Assegnare licenze di Intune agli account utente). 

## <a name="verify-intune-user-groups"></a>Verificare i gruppi di utenti di Intune
Gli utenti e i gruppi sono probabilmente già in AAD, perché è configurata la sincronizzazione delle directory. Per assicurarsi che gli utenti facciano parte del gruppo di utenti corretto, è consigliabile esaminare i gruppi di utenti di Intune. Criteri, profili, app e così via vengono destinati a questi gruppi. Assicurarsi che gli utenti di cui si esegue la migrazione alla versione autonoma di Intune facciano parte dei gruppi corretti. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurare Controllo degli accessi in base al ruolo
Come parte della migrazione, configurare tutti i ruoli Controllo degli accessi in base al ruolo necessari in Intune e assegnare gli utenti a tali ruoli. Si noti che ci sono alcune differenze tra Controllo degli accessi in base al ruolo in Configuration Manager e in Intune, ad esempio per quanto riguarda l'ambito delle risorse. Per informazioni dettagliate, vedere [Controllo degli accessi in base al ruolo (RBAC) con Intune](https://docs.microsoft.com/en-us/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Assegnare app e criteri ai gruppi di AAD
Se è stata eseguita la fase di [importazione dei dati di Configuration Manager in Microsoft Intune](migrate-import-data.md) del processo di migrazione per eseguire la migrazione di diversi oggetti di Configuration Manager a Intune, molti oggetti potrebbero essere già assegnati ai gruppi di AAD. È tuttavia necessario verificare che tutti gli oggetti (app, criteri, profili e così via) siano assegnati ai gruppi di AAD corretti. Se si assegnano gli oggetti in modo corretto, i dispositivi degli utenti vengono configurati automaticamente dopo la migrazione, che deve essere trasparente per gli utenti. Per informazioni dettagliate sull'assegnazione di oggetti a un gruppo di AAD, vedere gli argomenti seguenti: 
- [Assegnare criteri](https://docs.microsoft.com/intune/get-started-policies) 
- [Assegnare profili](https://docs.microsoft.com/intune/device-profile-assign) 
- [Assegnare app](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Criteri relativi a termini e condizioni
Come per gli altri criteri a livello di tenant, per i criteri relativi a termini e condizioni viene eseguita automaticamente la migrazione a Intune una volta abilitata l'autorità mista per il tenant.  È tuttavia necessario assegnare i termini e le condizioni a un gruppo che contiene gli utenti di cui è stata eseguita la migrazione per creare report accurati relativi all'accettazione per gli utenti di cui è stata eseguita la migrazione e per assicurarsi che i termini e le condizioni vengano gestiti correttamente per le registrazioni dei dispositivi o gli aggiornamenti di termini e condizioni futuri. Gli utenti non devono accettare di nuovo le condizioni, a meno che non vengano apportate modifiche ai criteri nella console di Configuration Manager. Per informazioni dettagliate, vedere [Assegnare termini e condizioni](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurare Exchange Connector
Se si usa Exchange e si ha un'istanza di Exchange Connector locale in Configuration Manager, è necessario [configurare la versione locale di Exchange Connector in Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considerare inoltre le informazioni nelle sezioni seguenti per eseguire la migrazione a Intune Exchange Connector e per garantire il corretto funzionamento dell'accesso condizionale dopo la migrazione.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Script di PowerShell per facilitare la migrazione a Intune Exchange Connector 
Sono disponibili script di PowerShell per preparare la transizione dei dispositivi di Exchange da Configuration Manager Exchange Connector a Intune Exchange Connector. Anche se l'esecuzione di questi script è facoltativa, si consiglia di eseguirli in modo da rimuovere i dispositivi inattivi da Exchange, che impediscono a Intune di individuare i dispositivi non necessari. L'esecuzione degli script garantisce che i dispositivi individuati mediante Exchange possano essere uniti ai dispositivi registrati in Intune nel modo più lineare possibile. Eseguire questi script prima di configurare Intune Exchange Connector. Gli script di PowerShell fanno parte dell'installazione dello strumento di importazione dati di Intune usato per [importare i dati di Configuration Manager in Microsoft Intune](migrate-import-data.md) nell'articolo successivo. Per informazioni dettagliate e per scaricare gli script, visitare la pagina di GitHub dello [strumento di importazione dati di Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Passaggi per garantire il corretto funzionamento dell'accesso condizionale dopo la migrazione degli utenti
Per il corretto funzionamento dell'accesso condizionale dopo la migrazione degli utenti e per fare in modo che gli utenti continuino ad avere accesso al server di posta elettronica, verificare quanto segue:
- Se l'impostazione del livello di accesso predefinito di Exchange ActiveSync (DefaultAccessLevel) è Blocca o Quarantena, i dispositivi potrebbero perdere l'accesso alla posta elettronica. 
- Se Exchange Connector è installato in Configuration Manager e il **livello di accesso quando un dispositivo mobile non è gestito da una regola** ha un valore **Consenti accesso**, è necessario installare la [versione locale di Exchange Connector](https://docs.microsoft.com/en-us/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune prima di eseguire la migrazione degli utenti. Configurare l'impostazione del livello di accesso predefinito in Intune nel pannello **Exchange locale** in **Impostazioni avanzate dell'accesso a Exchange ActiveSync**. Per informazioni dettagliate, vedere [Configurare l'accesso locale a Exchange](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Usare la stessa configurazione per entrambi i connettori. L'ultimo connettore configurato sovrascrive le impostazioni dell'organizzazione di ActiveSync scritte in precedenza dall'altro connettore. Se si configurano i connettori in modo diverso, potrebbero verificarsi modifiche impreviste dell'accesso condizionale.
- Rimuovere gli utenti dall'accesso condizionale in Configuration Manager una volta eseguita la migrazione alla versione autonoma di Intune.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurare Connettore di certificati di Microsoft Intune
Se si usa il servizio Registrazione dispositivi di rete (NDES) per l'emissione di certificati tramite SCEP, è necessario configurare Connettore di certificati di Microsoft Intune. Il computer che ospita NDES Connector in Intune non può essere lo stesso computer che ospita NDES Connector in Configuration Manager. Per informazioni dettagliate, vedere [Configurare e gestire i certificati SCEP con Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Dopo avere configurato il connettore, è necessario modificare i profili SCEP importati per fare riferimento al nuovo URL del server.

## <a name="next-step"></a>Passaggio successivo
Dopo avere preparato Intune per la migrazione, si è pronti per eseguire la migrazione di un set di utenti di test alla versione autonoma di Intune. Per informazioni dettagliate, vedere [Modificare l'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md).


