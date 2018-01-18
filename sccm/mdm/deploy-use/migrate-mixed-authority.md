---
title: "Modificare l'autorità MDM per utenti specifici (autorità MDM mista)"
titleSuffix: Configuration Manager
description: "Informazioni su come modificare l'autorità MDM dalla soluzione MDM ibrida alla versione autonoma di Intune per alcuni utenti."
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 59fb06d14002f781e0448a64bb0064b4add2f087
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Modificare l'autorità MDM per utenti specifici (autorità MDM mista) 

*Si applica a: System Center Configuration Manager (Current Branch)*    

È possibile configurare un'autorità MDM mista nello stesso tenant selezionando alcuni utenti da gestire in Intune e altri da gestire con la soluzione MDM ibrida (Intune integrato con Configuration Manager). Questo articolo include informazioni su come iniziare a spostare gli utenti nella versione autonoma di Intune e presuppone che siano stati completati i passaggi seguenti:
- Uso dello strumento di importazione dati per [importare gli oggetti di Configuration Manager in Intune](migrate-import-data.md) (facoltativo).
- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.

> [!Note]    
> Se si decide di eseguire un ripristino completo del tenant, che consente di rimuovere tutti i criteri, le app e le registrazioni dei dispositivi, contattare il supporto tecnico per assistenza.

Gli utenti di cui è stata eseguita la migrazione e i relativi dispositivi vengono gestiti in Intune, mentre gli altri dispositivi continuano a essere gestiti in Configuration Manager. Iniziare con un piccolo gruppo di utenti di test, per verificare che tutto funzioni come previsto. Eseguire quindi gradualmente la migrazione di altri gruppi di utenti, fino a quando non si è pronti a spostare l'autorità MDM a livello di tenant da Configuration Manager alla versione autonoma di Intune. 

## <a name="things-to-know-before-you-migrate-users"></a>Informazioni da sapere prima di eseguire la migrazione degli utenti
- Durante la migrazione in fasi, le app o i criteri MDM esistenti in Configuration Manager continuano a essere applicati ai dispositivi della soluzione MDM ibrida.
- I dispositivi per gli utenti nella raccolta associata alla sottoscrizione di Intune possono essere registrati nella soluzione MDM ibrida. Tutti i dispositivi associati agli utenti non inclusi nella raccolta vengono gestiti in Intune fino a quando l'utente dispone di una licenza di Intune o EMS. 
- Quando si esegue la migrazione di un utente a Intune, l'utente e i dispositivi vengono visualizzati in Intune nel portale di Azure dopo circa 15 minuti.  
- Quando si esegue la migrazione di utenti alla versione autonoma di Intune, continuare a gestire le impostazioni seguenti da Configuration Manager sia per i dispositivi della versione autonoma di Intune che per quelli della soluzione MDM ibrida:
    - [Certificato Apple Push Notification Service (APN)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [DEP (Device Enrollment Program)](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Profili di registrazione
    - [Licenze Volume Purchase Program (VPP)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificatori aziendali 
    - [Certificati di firma del codice](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Categorie di dispositivi](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Manager di registrazione](/sccm/mdm/plan-design/device-enrollment-methods)
    - Terms and conditions
    - File SLK di Windows
    - Personalizzazione del portale aziendale    
      
  > [!Important]    
  > Continuare a modificare i criteri a livello di tenant usando la console di Configuration Manager. Dopo avere [modificato l'autorità MDM a livello di tenant](change-mdm-authority.md) spostandola a Intune, questi criteri vengono gestiti in Intune in Azure. 
-   Se si usano certificati di firma del codice, è consigliabile eseguire la migrazione degli utenti in modo graduale. Dopo la migrazione di un dispositivo mobile, viene richiesto un nuovo certificato all'autorità di certificazione. Eseguendo la migrazione degli utenti, e dei relativi dispositivi, in modo graduale si limita il numero di richieste simultanee all'autorità di certificazione.
- È consigliabile non eseguire la migrazione degli account utente che sono stati aggiunti come manager di registrazione dispositivi in Configuration Manager. In seguito, quando si modifica l'autorità MDM a livello di tenant spostandola a Intune, verrà eseguita correttamente la migrazione di questi account utente. Se si esegue la migrazione dell'account utente manager di registrazione dispositivi prima della modifica dell'autorità MDM a livello di tenant, è necessario aggiungere manualmente l'utente come manager di registrazione dispositivi in Intune in Azure. La migrazione dei dispositivi registrati usando un manager di registrazione dispositivi non verrà tuttavia eseguita correttamente. Per la migrazione di questi dispositivi è necessario chiamare il supporto tecnico. Per informazioni dettagliate, vedere [Aggiungere un manager di registrazione dispositivi](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Per i dispositivi registrati usando un manager di registrazione dispositivi e i dispositivi senza [affinità utente](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) non viene eseguita automaticamente la migrazione alla nuova autorità MDM. Per cambiare l'autorità di gestione per questi dispositivi MDM, vedere [Eseguire la migrazione di dispositivi senza affinità utente](#migrate-devices-without-user-affinity).

## <a name="migrate-users-to-intune"></a>Eseguire la migrazione degli utenti a Intune
Per verificare che le configurazioni di Intune funzionino come previsto, eseguire prima di tutto la migrazione di un piccolo set di utenti con i relativi dispositivi. Dopo aver verificato che tutto funzioni come previsto, è quindi possibile avviare la migrazione di più gruppi di AAD con altri utenti e dispositivi.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Eseguire la migrazione di un gruppo di utenti di test alla versione autonoma di Intune
I dispositivi per gli utenti nella raccolta associata alla sottoscrizione di Intune possono essere registrati nella soluzione MDM ibrida. Quando si rimuove un utente dalla raccolta, se all'utente è assegnata una licenza di Intune, viene eseguita la migrazione dei relativi dispositivi registrati alla versione autonoma di Intune. Se agli utenti di cui si vuole eseguire la migrazione non sono ancora state assegnate le licenze, vedere [Assegnare le licenze di Intune agli account utente](https://docs.microsoft.com/intune/licenses-assign). Nella raccolta per la sottoscrizione di Intune, è possibile escludere raccolte di utenti dalla raccolta principale per eseguire la migrazione degli utenti nella raccolta esclusa. 

Nell'esempio seguente la raccolta di utenti ibridi contiene tutti i membri della raccolta Tutti gli utenti. Ciò consente a qualsiasi utente di registrare un dispositivo nella soluzione MDM ibrida. Per eseguire la migrazione degli utenti alla versione autonoma di Intune, selezionare Escludi raccolte e aggiungere una raccolta con gli utenti di cui eseguire la migrazione. Quando si è pronti per eseguire la migrazione di più utenti, è possibile aggiungere altre raccolte escluse contenenti tali utenti. 

![Escludi raccolte](../media/migrate-excludecollections.png)

> [!Note] 
> Quando è selezionata la raccolta **Tutti gli utenti** per la sottoscrizione di Intune, non è consentito aggiungere una regola per escludere le raccolte. Creare una nuova raccolta basata sulla raccolta **Tutti gli utenti**, verificare che la raccolta contenga gli utenti previsti e quindi modificare la sottoscrizione di Intune per usare la nuova raccolta. È possibile escludere le raccolte di utenti dalla nuova raccolta per la migrazione degli utenti. 

Per eseguire la migrazione di un gruppo di utenti di test a Intune, creare una raccolta di utenti contenente gli utenti di cui eseguire la migrazione e quindi escludere la raccolta di utenti dalla raccolta usata per la sottoscrizione di Intune.   

Il diagramma seguente fornisce una panoramica del funzionamento della migrazione degli utenti.

 ![Panoramica dell'autorità mista](../media/migrate-mixedauthority.svg)

1. Verificare che l'utente abbia una licenza di Intune/EMS. 
2. Creare una raccolta da escludere dalla raccolta per la sottoscrizione di Intune. In questo esempio la raccolta **Tutti gli utenti ibridi** contiene una regola per escludere gli utenti nella raccolta **Pilota migrazione**. **Utente1** è un membro della raccolta **Pilota migrazione** ed è escluso dalla raccolta **Tutti gli utenti ibridi**. 
3. I dispositivi di **Utente1** sono ora gestiti da Intune nel portale di Azure. 
4. Tutti gli altri dispositivi continuano a essere gestiti dalla console di Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Verificare le funzionalità della versione autonoma di Intune
Dopo avere eseguito la migrazione di un piccolo set di utenti, verificare che i dispositivi degli utenti siano elencati in Intune. Passare al pannello **Dispositivi** e selezionare **Tutti i dispositivi**. 

Verificare quindi che criteri, profili, app e così via funzionino come previsto nei dispositivi degli utenti.

## <a name="migrate-additional-users"></a>Eseguire la migrazione di utenti aggiuntivi
Dopo avere verificato che la versione autonoma di Intune funzioni come previsto, è possibile avviare la migrazione di altri utenti. Nello stesso modo in cui è stata creata una raccolta con un set di utenti di test, creare raccolte contenenti gli utenti di cui eseguire la migrazione ed escludere tali raccolte dalla raccolta associata alla sottoscrizione di Intune. Per informazioni dettagliate, vedere [Raccolta associata alla sottoscrizione di Intune](#collection-associated-with-your-intune-subscription).

## <a name="migrate-devices-without-user-affinity"></a>Eseguire la migrazione di dispositivi senza affinità utente
Per i dispositivi registrati usando un manager di registrazione dispositivi e i dispositivi senza [affinità utente](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) non viene eseguita automaticamente la migrazione alla nuova autorità MDM. È possibile usare il cmdlet di PowerShell *Switch-MdmDeviceAuthority* per selezionare l'autorità di gestione Intune o Configuration Manager negli scenari seguenti: 

-   Scenario 1: usare il cmdlet *Switch-MdmDeviceAuthority* per eseguire la migrazione dei dispositivi selezionati e verificare che possano essere gestiti con Intune in Azure. Quindi, quando si è pronti, è possibile [cambiare l'autorità MDM impostando Intune per il tenant](migrate-change-mdm-authority.md) per completare la migrazione per i dispositivi. 
-   Scenario 2: quando si è pronti a impostare Intune come autorità MDM per il tenant, è possibile eseguire le azioni seguenti per completare la migrazione dei dispositivi senza affinità utente:
    - Usare il cmdlet per cambiare l'autorità di gestione dei dispositivi mobili per i dispositivi senza affinità utente prima di [impostare l'autorità MDM su Intune per il tenant](migrate-change-mdm-authority.md).    
    - Contattare il supporto tecnico per cambiare l'autorità di gestione dei dispositivi senza affinità utente dopo aver impostato l'autorità MDM su Intune per il tenant.

Per cambiare l'autorità di gestione per questi dispositivi MDM, è possibile usare il cmdlet di *Switch-MdmDeviceAuthority* per impostare le autorità di gestione Intune e Configuration Manager. 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>RIEPILOGO
Il cmdlet cambia l'autorità di gestione dei dispositivi MDM senza affinità utente (ad esempio, dispositivi registrati in blocco). Il cmdlet cambia l'autorità di gestione impostando Intune o Configuration Manager per i dispositivi specificati in base alle autorità di gestione attive quando si esegue il cmdlet.

### <a name="syntax"></a>SINTASSI
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARAMETRI
``` powershell
-Credential <PSCredential>
Credential for Intune Tenant Admin or Service Admin account to use when switching device management authorities. The user is prompted for credentials if the parameter is not specified.

-DeviceIds <Guid[]>
The ids of the MDM devices that need to have their management authority switched. The device ids are unique identifiers for the devices displayed by the Configuration Manager console.

-Force [<SwitchParameter>]
Specify parameter to disable the Should Continue prompt.<br>
 
-LogFilePath <string>
Path to log file location.
 
-LoggingLevel <SourceLevels>
The log level used to determine the type of logs that need to be written to the log file.
 
The following are the possible values for LoggingLevel:

  - ActivityTracing
  - All
  - Critical
  - Error
  - Information
  - Off
  - Verbose
  - Warning
 
-Confirm [<SwitchParameter>]
Prompts you for confirmation before executing the command.
 
-WhatIf [<SwitchParameter>]
Describes what would happen if you executed the command without actually executing the command.
 
<CommonParameters>
This cmdlet supports the common parameters: Verbose, Debug,
ErrorAction, ErrorVariable, WarningAction, WarningVariable,
OutBuffer, PipelineVariable, and OutVariable. For more information, see
[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).
```

### <a name="example-1"></a>Esempio 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds
 
  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM
 
Description
 
-----------
 
Successfully switched the management authority of the device from Configuration Manager to Intune.
```
### <a name="remarks"></a>OSSERVAZIONI
``` powershell
To see the examples, type: "get-help Switch-MdmDeviceAuthority -examples".
For more information, type: "get-help Switch-MdmDeviceAuthority -detailed".
For technical information, type: "get-help Switch-MdmDeviceAuthority -full".
For online help, type: "get-help Switch-MdmDeviceAuthority -online".
```

## <a name="next-steps"></a>Passaggi successivi
Dopo avere seguito la migrazione degli utenti e avere testato la funzionalità di Intune, stabilire se si è pronti per [modificare l'autorità MDM](migrate-change-mdm-authority.md) del tenant di Intune da Configuration Manager a Intune. 