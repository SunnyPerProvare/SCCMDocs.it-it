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
ms.collection: M365-identity-device-management
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62237010"
---
# <a name="prepare-intune-for-user-migration"></a>Preparare Intune per la migrazione degli utenti 

*Si applica a: System Center Configuration Manager (Current Branch)*    
Prima di eseguire la migrazione degli utenti dalla soluzione MDM ibrida a Intune autonomo, eseguire passaggi di preparazione di Intune. Questi passaggi consentono di assicurarsi che gli utenti migrati e i dispositivi continuino a essere gestiti. Quando si completano questi passaggi e avviare la migrazione a Intune, non ha alcun impatto di una notevole quantità agli utenti.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Correggere i problemi riscontrati durante la raccolta e l'importazione dei dati
Se è stato usato lo strumento di importazione dati di Intune per [importare dati di Configuration Manager in Microsoft Intune](migrate-import-data.md), riepilogato gli oggetti che nelze importovat. Nella tabella seguente sono elencati alcuni dei problemi tipici e i passaggi per correggere gli errori in Intune: 

|Problema  |Fix  |
|---------|---------|
|Non vengono migrate automaticamente raccolte basate sull'appartenenza diretta o su un tipo complesso.|Creare gruppi di Azure Active Directory (Azure AD) in Azure per sostituire la raccolta che non è stata importata. Assegnare quindi l'oggetto al gruppo.|
|I criteri non sono stati importable (importabile) |Ricreare i criteri in Intune.|
|La distribuzione di un oggetto non viene importata|Assegnare l'oggetto al gruppo. Il gruppo debba includere gli stessi utenti dalla raccolta per la distribuzione.|

## <a name="create-intune-objects"></a>Creare oggetti di Intune 
Se si [importati i dati di Configuration Manager a Microsoft Intune](migrate-import-data.md) e risolto i problemi durante il processo, verificare gli oggetti importati siano configurati correttamente. Creare anche tutti gli oggetti aggiuntivi (criteri, profili e le App) in Intune che è necessario nell'organizzazione. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Assegnare le licenze di Intune agli utenti di cui è stata eseguita la migrazione
In Configuration Manager, si aggiunge un insieme alla sottoscrizione di Intune e i membri della raccolta possono registrare i dispositivi. Mentre una licenza di Intune è riservata per i dispositivi registrati, queste licenze non sono associate all'utente o dispositivo. È ad esempio, non sarebbe trovare una licenza di Intune in Azure AD per un utente che ha un dispositivo registrato. 

Nella versione autonoma di Intune, configurare una licenza di Intune per ogni utente. Configurare la licenza *prima di* si esegue la migrazione di un utente a Intune autonomo. Questa azione assicura che l'utente e i suoi dispositivi siano gestiti da Intune dopo la modifica nell'autorità MDM. Per altre informazioni, vedere [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign) (Assegnare licenze di Intune agli account utente). 

## <a name="verify-intune-user-groups"></a>Verificare i gruppi di utenti di Intune
Gli utenti e gruppi sono probabilmente già in Azure AD perché hai configurata la sincronizzazione delle directory. Per assicurarsi che gli utenti facciano parte del gruppo di utenti corretto, è consigliabile esaminare i gruppi di utenti di Intune. Destinazione dei criteri, profili e le app a tali gruppi. Assicurarsi che gli utenti di cui si esegue la migrazione alla versione autonoma di Intune facciano parte dei gruppi corretti. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurare Controllo degli accessi in base al ruolo
Come parte della migrazione, configurare tutti i ruoli Controllo degli accessi in base al ruolo necessari in Intune e assegnare gli utenti a tali ruoli. Esistono differenze tra RBAC in Configuration Manager e Intune, ad esempio di definizione dell'ambito delle risorse. Per altre informazioni, vedere [controllo degli accessi in base al ruolo (RBAC) con Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Assegnare app e criteri ai gruppi di AAD
Se si [importati i dati di Configuration Manager a Microsoft Intune](migrate-import-data.md), molti oggetti potrebbero essere già assegnati a gruppi Azure AD. Verificare che tutti gli oggetti (App, i criteri e profili) siano assegnati correttamente i gruppi Azure AD. Se si assegnano gli oggetti in modo corretto, i dispositivi dell'utente vengono configurati automaticamente dopo che l'utente viene eseguita la migrazione e la migrazione non deve avere alcun impatto di una notevole quantità di utenti. Per altre informazioni sull'assegnazione di oggetti a un gruppo di Azure AD, vedere gli articoli seguenti: 
- [Assegnare criteri](https://docs.microsoft.com/intune/get-started-policies)  
- [Assegnare profili](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Quando Intune distribuisce il nuovo profilo di posta elettronica, gli utenti ricevono la richiesta di immettere nuovamente la password. Questo comportamento determina i messaggi di posta elettronica da scaricare nuovamente gli elementi nei dispositivi degli utenti. Le modifiche personalizzate apportate dall'utente dovrà eseguire di nuovo. 
- [Assegnare app](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Criteri relativi a termini e condizioni
Come per gli altri criteri a livello di tenant, per i criteri relativi a termini e condizioni viene eseguita automaticamente la migrazione a Intune una volta abilitata l'autorità mista per il tenant.  Tuttavia, è necessario assegnare i termini e condizioni a un gruppo che contiene la migrazione degli utenti per report relativi all'accettazione per gli utenti migrati in modo accurato e assicurarsi che i termini e condizioni correttamente come destinazione per future termini e condizioni aggiornamenti o dispositivo registrazioni. Gli utenti non dovranno accettare i termini e condizioni, a meno che non sono disponibili le modifiche apportate ai criteri nella console di Configuration Manager. Per altre informazioni, vedere [assegnare termini e condizioni](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurare Exchange Connector
Se si usa Exchange e si ha un'istanza di Exchange Connector locale in Configuration Manager, è necessario [configurare la versione locale di Exchange Connector in Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considerare inoltre le informazioni nelle sezioni seguenti che consentono di eseguire la migrazione a Intune Exchange Connector e per verificare che l'accesso condizionale funzioni correttamente dopo la migrazione.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Script di PowerShell per facilitare la migrazione a Intune Exchange Connector 
Sono disponibili script di PowerShell per preparare la transizione dei dispositivi di Exchange da Configuration Manager Exchange Connector a Intune Exchange Connector. Anche se l'esecuzione di questi script è facoltativa, si consiglia di eseguirli in modo da rimuovere i dispositivi inattivi da Exchange, che impediscono a Intune di individuare i dispositivi non necessari. L'esecuzione degli script garantisce che i dispositivi individuati mediante Exchange possano essere uniti ai dispositivi registrati in Intune nel modo più lineare possibile. Eseguire questi script prima di configurare Intune Exchange Connector. Gli script di PowerShell fanno parte dell'installazione dello strumento di importazione dati di Intune usato per [importare i dati di Configuration Manager in Microsoft Intune](migrate-import-data.md) nell'articolo successivo. Per informazioni dettagliate e per scaricare gli script, visitare la pagina di GitHub dello [strumento di importazione dati di Microsoft Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Passaggi per rendere in modo corretto funzionamento dell'accesso condizionale che dopo la migrazione degli utenti
Per l'accesso condizionale per funzionare correttamente dopo la migrazione di utenti e per assicurarsi che gli utenti continuino ad avere accesso al server di posta elettronica, assicurarsi che siano impostate le seguenti configurazioni:
- Se l'impostazione del livello di accesso predefinito di Exchange ActiveSync (DefaultAccessLevel) è Blocca o Quarantena, i dispositivi potrebbero perdere l'accesso alla posta elettronica. 
- Se è installato Exchange Connector in Configuration Manager e il **livello di accesso quando un dispositivo mobile non è gestito da una regola** impostazione ha un valore pari **consentire l'accesso**, installare il [ Exchange connector locale](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) in Intune prima della migrazione degli utenti. Configurare l'impostazione del livello di accesso predefinito in Intune nel **Exchange in locale** nella pagina **le impostazioni di accesso Advanced Exchange ActiveSync**. Per altre informazioni, vedere [configurare Exchange in locale l'accesso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Usare la stessa configurazione per entrambi i connettori. L'ultimo connettore configurato sovrascrive le impostazioni dell'organizzazione di ActiveSync scritte in precedenza dall'altro connettore. Se si configurano i connettori in modo diverso, potrebbero verificarsi modifiche impreviste dell'accesso condizionale.
- Rimuovere gli utenti dall'accesso condizionale in Configuration Manager una volta eseguita la migrazione alla versione autonoma di Intune.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurare Connettore di certificati di Microsoft Intune
Se si usa il servizio Registrazione dispositivi di rete (NDES) per l'emissione di certificati tramite SCEP, è necessario configurare Connettore di certificati di Microsoft Intune. Computer che ospita NDES connector in Intune non può essere lo stesso computer che ospita NDES connector in Configuration Manager. Per altre informazioni, vedere [configurare e gestire i certificati SCEP con Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Dopo aver configurato il connettore, modificare i profili SCEP importati per il nuovo URL del server di riferimento.

## <a name="next-step"></a>Passaggio successivo
Dopo avere preparato Intune per la migrazione, si è pronti per eseguire la migrazione di un set di utenti di test alla versione autonoma di Intune. Per altre informazioni, vedere [cambiare l'autorità MDM per utenti specifici (autorità mista)](migrate-mixed-authority.md).


