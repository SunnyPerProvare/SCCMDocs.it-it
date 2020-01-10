---
title: Preparare Intune per la migrazione degli utenti
titleSuffix: Configuration Manager
description: Informazioni su come preparare Intune in Azure per la migrazione degli utenti dalla soluzione MDM ibrida.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 99ba39fd8f5ff65f4d4fdca5dc71fe7b252af56b
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826765"
---
# <a name="prepare-intune-for-user-migration"></a>Preparare Intune per la migrazione degli utenti 

*Si applica a: Configuration Manager (Current Branch)*     
Prima di eseguire la migrazione degli utenti da MDM ibrido a Intune autonomo, seguire questa procedura per preparare Intune. Questi passaggi consentono di verificare che gli utenti migrati e i relativi dispositivi continuino a essere gestiti. Quando si completano questi passaggi e si avvia la migrazione a Intune, non ci sono effetti signifcant sugli utenti.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Correggere i problemi riscontrati durante la raccolta e l'importazione dei dati
Se è stato utilizzato lo strumento Intune Data Importer per [importare Configuration Manager dati Microsoft Intune](migrate-import-data.md), vengono riepilogati gli oggetti che non sono stati importati. Nella tabella seguente sono elencati alcuni dei problemi tipici e i passaggi per correggerli in Intune: 

|Problema  |Correzione  |
|---------|---------|
|Le raccolte basate sull'appartenenza diretta o su un complesso non vengono migrate automaticamente.|Creare gruppi di Azure Active Directory (Azure AD) in Azure per sostituire la raccolta che non è stata importata. Assegnare quindi l'oggetto al gruppo.|
|I criteri non sono importabili |Ricreare i criteri in Intune.|
|La distribuzione di un oggetto non viene importata|Assegnare l'oggetto al gruppo. Il gruppo deve includere gli stessi utenti della raccolta per la distribuzione.|

## <a name="create-intune-objects"></a>Creare oggetti di Intune 
Se sono stati [importati Configuration Manager dati in Microsoft Intune](migrate-import-data.md) e sono stati corretti problemi durante il processo, verificare che gli oggetti importati siano configurati correttamente. Creare anche eventuali oggetti aggiuntivi (criteri, profili e app) in Intune necessari per l'organizzazione. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Assegnare le licenze di Intune agli utenti di cui è stata eseguita la migrazione
In Configuration Manager si aggiunge una raccolta alla sottoscrizione di Intune e i membri della raccolta possono registrare i propri dispositivi. Quando una licenza di Intune è riservata ai dispositivi registrati, queste licenze non sono associate all'utente o al dispositivo. Ad esempio, non è possibile trovare una licenza di Intune in Azure AD per un utente con un dispositivo registrato. 

In Intune autonomo configurare una licenza di Intune per ogni utente. Configurare la licenza *prima* di eseguire la migrazione di un utente a Intune autonomo. Questa azione assicura che l'utente e i relativi dispositivi siano gestiti da Intune dopo la modifica nell'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign) (Assegnare licenze di Intune agli account utente). 

## <a name="verify-intune-user-groups"></a>Verificare i gruppi di utenti di Intune
È probabile che utenti e gruppi siano già in Azure AD perché è stata configurata la sincronizzazione della directory. Per assicurarsi che gli utenti facciano parte del gruppo di utenti corretto, è consigliabile esaminare i gruppi di utenti di Intune. I criteri, i profili e le app sono destinati a questi gruppi. Assicurarsi che gli utenti di cui si esegue la migrazione alla versione autonoma di Intune facciano parte dei gruppi corretti. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurare Controllo degli accessi in base al ruolo
Come parte della migrazione, configurare tutti i ruoli Controllo degli accessi in base al ruolo necessari in Intune e assegnare gli utenti a tali ruoli. Esistono differenze tra il controllo degli accessi in base al ruolo in Configuration Manager e Intune, ad esempio l'ambito delle risorse. Per altre informazioni, vedere [Controllo degli accessi in base al ruolo (RBAC) con Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Assegnare app e criteri ai gruppi di AAD
Se sono stati [importati Configuration Manager dati Microsoft Intune](migrate-import-data.md), molti degli oggetti potrebbero essere già stati assegnati ai gruppi di Azure ad. Verificare che tutti gli oggetti (app, criteri e profili) siano assegnati ai gruppi di Azure AD corretti. Se si assegnano correttamente oggetti, i dispositivi dell'utente vengono configurati automaticamente dopo la migrazione dell'utente e la migrazione non dovrebbe avere alcun effetto signifcant per gli utenti. Per ulteriori informazioni sull'assegnazione degli oggetti a un gruppo di Azure AD, vedere gli articoli seguenti: 
- [Assegnare criteri](https://docs.microsoft.com/intune/get-started-policies)  
- [Assegnare profili](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Quando Intune distribuisce il nuovo profilo di posta elettronica, gli utenti ricevono una richiesta di immissione della password. Questo comportamento comporta il download dei messaggi di posta elettronica nei dispositivi degli utenti. Eventuali modifiche personalizzate eseguite dall'utente dovranno essere eseguite di nuovo. 
- [Assegnare app](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Criteri relativi a termini e condizioni
Come per gli altri criteri a livello di tenant, per i criteri relativi a termini e condizioni viene eseguita automaticamente la migrazione a Intune una volta abilitata l'autorità mista per il tenant.  Tuttavia, è necessario assegnare i termini e le condizioni a un gruppo contenente gli utenti migrati per segnalare accuratamente l'accettazione degli utenti migrati e assicurarsi che i termini e le condizioni siano assegnati correttamente per gli aggiornamenti o i dispositivi futuri di termini e condizioni. Iscrizioni. Non è necessario che gli utenti riaccettino i termini e le condizioni a meno che non siano state apportate modifiche ai criteri nella console di Configuration Manager. Per altre informazioni, vedere [assegnare termini e condizioni](https://docs.microsoft.com/intune/enrollment/terms-and-conditions-create#create-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurare Exchange Connector
Se si usa Exchange e si ha un'istanza di Exchange Connector locale in Configuration Manager, è necessario [configurare la versione locale di Exchange Connector in Intune](https://docs.microsoft.com/intune/exchange-connector-install). Prendere in considerazione anche le informazioni nelle sezioni riportate di seguito per eseguire la migrazione a Intune Exchange Connector e assicurarsi che l'accesso condizionale funzioni correttamente dopo la migrazione.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Script di PowerShell per facilitare la migrazione a Intune Exchange Connector 
Sono disponibili script di PowerShell per preparare la transizione dei dispositivi di Exchange da Configuration Manager Exchange Connector a Intune Exchange Connector. Anche se l'esecuzione di questi script è facoltativa, si consiglia di eseguirli in modo da rimuovere i dispositivi inattivi da Exchange, che impediscono a Intune di individuare i dispositivi non necessari. L'esecuzione degli script garantisce che i dispositivi individuati mediante Exchange possano essere uniti ai dispositivi registrati in Intune nel modo più lineare possibile. Eseguire questi script prima di configurare Intune Exchange Connector. Gli script di PowerShell fanno parte dell'installazione dello strumento di importazione dati di Intune usato per [importare i dati di Configuration Manager in Microsoft Intune](migrate-import-data.md) nell'articolo successivo. Per informazioni dettagliate e per scaricare gli script, visitare la pagina di GitHub dello [strumento di importazione dati di Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Passaggi per assicurarsi che l'accesso condizionale funzioni correttamente dopo la migrazione degli utenti
Per il corretto funzionamento dell'accesso condizionale dopo la migrazione degli utenti e per assicurarsi che gli utenti continuino ad accedere al server di posta elettronica, verificare che siano impostate le configurazioni seguenti:
- Se l'impostazione del livello di accesso predefinito di Exchange ActiveSync (DefaultAccessLevel) è Blocca o Quarantena, i dispositivi potrebbero perdere l'accesso alla posta elettronica. 
- Se Exchange Connector viene installato in Configuration Manager e il **livello di accesso quando un dispositivo mobile non è gestito da un'** impostazione della regola ha il valore **Consenti accesso**, installare [on-premises Exchange Connector](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune prima di eseguire la migrazione degli utenti. Configurare l'impostazione del livello di accesso predefinito in Intune nella pagina **Exchange locale** in **Impostazioni avanzate di accesso a Exchange ActiveSync**. Per altre informazioni, vedere [configurare l'accesso locale a Exchange](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Usare la stessa configurazione per entrambi i connettori. L'ultimo connettore configurato sovrascrive le impostazioni dell'organizzazione di ActiveSync scritte in precedenza dall'altro connettore. Se si configurano i connettori in modo diverso, potrebbero verificarsi modifiche impreviste dell'accesso condizionale.
- Rimuovere gli utenti dall'accesso condizionale in Configuration Manager una volta eseguita la migrazione alla versione autonoma di Intune.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurare Connettore di certificati di Microsoft Intune
Se si usa il servizio Registrazione dispositivi di rete (NDES) per l'emissione di certificati tramite SCEP, è necessario configurare Connettore di certificati di Microsoft Intune. Il computer che ospita il connettore Registrazione dispositivi in Intune non può essere lo stesso computer che ospita il connettore Registrazione dispositivi in Configuration Manager. Per altre informazioni, vedere [configurare e gestire i certificati SCEP con Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Dopo aver configurato il connettore, modificare i profili SCEP importati per fare riferimento al nuovo URL del server.

## <a name="next-step"></a>Passaggio successivo
Dopo aver preparato Intune per la migrazione, si è pronti per eseguire la migrazione di un set di utenti di test a Intune autonomo. Per altre informazioni, vedere [modificare l'autorità MDM per utenti specifici (autorità mista)](migrate-mixed-authority.md).


