---
title: Cambiare l'autorità MDM
titleSuffix: Configuration Manager
description: Informazioni su come modificare l'autorità MDM da MDM ibrido a Intune autonomo per utenti specifici (autorità MDM mista).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6ba2ff769ed56b0edf75b7d0d0e63028c71b198
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520423"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Modificare l'autorità MDM per utenti specifici (autorità MDM mista)

*Si applica a: Configuration Manager (Current Branch)*

È possibile configurare un'autorità MDM mista nello stesso tenant. Gestione di alcuni utenti in Microsoft Intune e altri con MDM ibrida. Questo articolo fornisce informazioni su come iniziare a trasferire gli utenti a Intune autonomo. Si presuppone che siano stati completati i passaggi seguenti:  

- Uso dello strumento di importazione dati per [importare gli oggetti di Configuration Manager in Intune](migrate-import-data.md) (facoltativo).  

- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.  

> [!Note]  
> Una reimpostazione completa del tenant rimuove tutti i criteri, le app e le registrazioni dei dispositivi. Se si decide di eseguire questo processo, contattare il supporto tecnico per assistenza.  

Gestire gli utenti migrati e i relativi dispositivi in Intune. Continuare a gestire altri dispositivi in Configuration Manager. Per verificare che tutto funzioni come previsto, iniziare con un piccolo gruppo di utenti di test. Eseguire quindi gradualmente la migrazione di altri gruppi di utenti. Quando si è pronti, impostare l'autorità MDM a livello di tenant da Configuration Manager a Intune autonomo.

> [!Important]  
> A partire dal 13 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>Informazioni da sapere prima di eseguire la migrazione degli utenti

- Durante la migrazione in fasi, le app o i criteri MDM esistenti in Configuration Manager continuano a essere applicati ai dispositivi della soluzione MDM ibrida.  

- I dispositivi per gli utenti nella raccolta associata alla sottoscrizione di Intune possono essere registrati nella soluzione MDM ibrida. Tutti i dispositivi associati agli utenti non inclusi nella raccolta vengono gestiti in Intune fino a quando l'utente dispone di una licenza di Intune o EMS.  

    > [!Note]  
    > Gli utenti possono eseguire la registrazione nella versione di Intune autonoma anche se è stato impedito loro di farlo nella console di Configuration Manager. Per impedire del tutto a un utente di eseguire la registrazione, non concedergli Intune in licenza. Non possono registrarsi senza una licenza.<!--SCCMDocs issue 738-->  

- Quando si esegue la migrazione di un utente a Intune, l'utente e i dispositivi vengono visualizzati in Intune nel portale di Azure dopo circa 15 minuti.  

- Quando si esegue la migrazione di utenti alla versione autonoma di Intune, continuare a gestire le impostazioni seguenti da Configuration Manager sia per i dispositivi della versione autonoma di Intune che per quelli della soluzione MDM ibrida:  

    - [Certificato Apple Push Notification Service (APN)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Programma di registrazione dei dispositivi](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > Non è necessario ricreare il token DEP o rimuoverlo dal Configuration Manager. Viene automaticamente eseguita la migrazione a Intune 24 ore dopo la modifica dell'autorità MDM del tenant da Configuration Manager a Intune. Questa modifica è il passaggio finale della migrazione. Se il token DEP non viene migrato entro 24 ore, contattare il supporto tecnico Microsoft per assistenza.  

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
    > Continuare a modificare i criteri a livello di tenant usando la console di Configuration Manager. Dopo aver [modificato l'autorità MDM a livello di tenant](/sccm/mdm/deploy-use/change-mdm-authority) in Intune, i criteri a livello di tenant gestiti in Configuration Manager la migrazione automatica a Intune in Azure. Un esempio di tale criterio è per i certificati del servizio Apple Push Notification (APNs).<!--SCCMDocs issue #971-->  

- Se si usano certificati di firma del codice, è consigliabile eseguire la migrazione degli utenti in modo graduale. Dopo la migrazione di un dispositivo mobile, viene richiesto un nuovo certificato all'autorità di certificazione. Eseguendo la migrazione degli utenti, e dei relativi dispositivi, in modo graduale si limita il numero di richieste simultanee all'autorità di certificazione.  

- Non eseguire la migrazione degli account utente che sono stati aggiunti come manager di registrazione dispositivi in Configuration Manager. In seguito, quando si modifica l'autorità MDM a livello di tenant spostandola a Intune, verrà eseguita correttamente la migrazione di questi account utente. Se si esegue la migrazione dell'account utente DEM prima della modifica dell'autorità MDM a livello di tenant, è necessario aggiungere manualmente l'utente come DEM in Intune in Azure. Tuttavia, i dispositivi registrati tramite un DEM non vengono migrati correttamente. Per la migrazione di questi dispositivi chiamare il supporto tecnico. Per altre informazioni, vedere [Aggiungere un manager di registrazione dispositivi](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > In modalità di autorità mista non spostare questi account in Intune rimuovendoli dalla raccolta cloud ConfigMgr, altrimenti l'utente diventa un utente standard e non può registrare più di 15 dispositivi. Eseguire invece la migrazione di questi utenti e dei relativi dispositivi dopo aver cambiato completamente l'autorità MDM per il tenant.<!--Intune bug 2174210-->  

- I dispositivi registrati usando un DEM e i dispositivi senza [affinità utente](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) non vengono automaticamente migrati alla nuova autorità MDM. Per cambiare l'autorità di gestione per questi dispositivi MDM, vedere [Eseguire la migrazione di dispositivi senza affinità utente](#migrate-devices-without-user-affinity).  



## <a name="migrate-users-to-intune"></a>Eseguire la migrazione degli utenti a Intune

Per verificare che le configurazioni di Intune funzionino come previsto, eseguire prima di tutto la migrazione di un piccolo set di utenti con i relativi dispositivi. Dopo aver verificato che tutto funzioni come previsto, è quindi possibile avviare la migrazione di più gruppi di AAD con altri utenti e dispositivi.



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Eseguire la migrazione di un gruppo di utenti di test alla versione autonoma di Intune

I dispositivi per gli utenti nella raccolta associata alla sottoscrizione di Intune possono essere registrati nella soluzione MDM ibrida. Quando si rimuove un utente dalla raccolta, se all'utente è stata assegnata una licenza di Intune, viene eseguita la migrazione dei dispositivi registrati a Intune autonomo. Se non sono già state assegnate licenze agli utenti di cui si intende eseguire la migrazione, vedere [assegnare le licenze di Intune agli account utente](https://docs.microsoft.com/intune/licenses-assign). Nella raccolta per la sottoscrizione di Intune, è possibile escludere raccolte di utenti dalla raccolta principale per eseguire la migrazione degli utenti nella raccolta esclusa.

Nell'esempio seguente la raccolta di utenti ibridi contiene tutti i membri della raccolta Tutti gli utenti. Questa configurazione consente a qualsiasi utente di registrare un dispositivo nella soluzione MDM ibrida. Per eseguire la migrazione degli utenti alla versione autonoma di Intune, selezionare Escludi raccolte e aggiungere una raccolta con gli utenti di cui eseguire la migrazione. Quando si è pronti per eseguire la migrazione di più utenti, aggiungere altre raccolte escluse contenenti tali utenti.

![Escludi raccolte](../media/migrate-excludecollections.png)

> [!Note]  
>   Quando si seleziona la raccolta **tutti gli utenti** per la sottoscrizione di Intune, non è possibile aggiungere una regola per escludere le raccolte. In alternativa, creare una nuova raccolta basata sulla raccolta **tutti gli utenti** , verificare che la raccolta contenga gli utenti previsti, quindi modificare la sottoscrizione di Intune per usare la nuova raccolta. È possibile escludere le raccolte di utenti dalla nuova raccolta per la migrazione degli utenti. Se si esclude un utente da una raccolta ma si include un gruppo di cui l'utente è membro, l'utente non sarà escluso dalla raccolta.

Per eseguire la migrazione di un gruppo di utenti di test a Intune, creare una raccolta di utenti contenente gli utenti di cui eseguire la migrazione. Quindi escludere la raccolta di utenti dalla raccolta usata per la sottoscrizione di Intune.  

Il diagramma seguente fornisce una panoramica del funzionamento della migrazione degli utenti.

![Panoramica dell'autorità mista](../media/migrate-mixedauthority.svg)

1. Verificare che l'utente abbia una licenza di Intune/EMS.  

2. Creare una raccolta da escludere dalla raccolta per la sottoscrizione di Intune. In questo esempio la raccolta **Tutti gli utenti ibridi** contiene una regola per escludere gli utenti nella raccolta **Pilota migrazione**. **Utente1** è un membro della raccolta **Pilota migrazione** ed è escluso dalla raccolta **Tutti gli utenti ibridi**.  

3. I dispositivi **User1**sono ora gestiti da Intune nel portale di Azure.  

4. Tutti gli altri dispositivi continuano a essere gestiti dalla console di Configuration Manager.  

> [!Important]  
> Quando si sposta un utente da ibrido a autonomo, la rimozione dei criteri viene sospesa per sette giorni.<!-- SCCMDocs issue #1066 -->


## <a name="verify-intune-standalone-functionality"></a>Verificare le funzionalità della versione autonoma di Intune

Dopo avere eseguito la migrazione di un piccolo set di utenti, verificare che i dispositivi degli utenti siano elencati in Intune. Passare a **Dispositivi** e selezionare **Tutti i dispositivi**.

Verificare quindi che criteri, profili e app funzionino come previsto nei dispositivi degli utenti.



## <a name="migrate-additional-users"></a>Eseguire la migrazione di utenti aggiuntivi

Dopo avere verificato che la versione autonoma di Intune funzioni come previsto, avviare la migrazione di altri utenti. Così come è stata creata una raccolta con un set di utenti di test, creare raccolte che includano gli utenti di cui eseguire la migrazione. Escludere le raccolte dalla raccolta associata alla sottoscrizione di Intune. Per informazioni dettagliate, vedere [eseguire la migrazione di un gruppo di utenti di test a Intune autonomo](#migrate-a-test-group-of-users-to-intune-standalone).



## <a name="migrate-devices-without-user-affinity"></a>Eseguire la migrazione di dispositivi senza affinità utente

Per eseguire la migrazione del modulo dei singoli dispositivi Configuration Manager a Intune registrati senza affinità utente, usare il cmdlet di PowerShell switch-MdmDeviceAuthority.  Dopo aver eseguito la migrazione dei dispositivi selezionati usando il cmdlet, convalidare in Intune in Azure che la migrazione si è verificata come previsto per i dispositivi selezionati. Quindi, quando si è pronti, impostare l'autorità MDM su Intune per il tenant per completare la migrazione per tutti i dispositivi rimanenti con Configuration Manager come autorità MDM.

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>RIEPILOGO

Il cmdlet cambia l'autorità di gestione dei dispositivi MDM senza affinità utente (ad esempio, dispositivi registrati in blocco). Il cmdlet passa tra le autorità di gestione di Intune e Configuration Manager. Viene attivato per i dispositivi specificati in base alle rispettive autorità di gestione quando si esegue il cmdlet.

### <a name="syntax"></a>SINTASSI

`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARAMETRI

#### `-Credential <PSCredential>`

Un oggetto credenziali di PowerShell per l'account utente di Azure AD che viene usato quando si cambia l'autorità di gestione dei dispositivi. Se il parametro non è specificato, all'utente vengono richieste le credenziali. Il ruolo della directory per questo account utente deve essere un **amministratore globale** o un **amministratore con limitazioni** con il ruolo amministrativo di **amministrazione di Intune**.

#### `-DeviceIds <Guid[]>`

Gli ID dei dispositivi MDM per cui è necessario cambiare l'autorità di gestione. Gli ID dei dispositivi sono identificatori univoci per i dispositivi visualizzati dalla console di Configuration Manager.

#### `-Force [<SwitchParameter>]`

Specificare un parametro per disabilitare la richiesta di continuazione.

#### `-LogFilePath <string>`

Percorso file di log.

#### `-LoggingLevel <SourceLevels>`

Il livello di log usato per determinare i tipi di log che devono essere scritti nel file di log.

Di seguito sono elencati i valori possibili per LoggingLevel:

- ActivityTracing
- Tutto
- Critico
- Errore di
- Informazioni
- Off
- Dettagliato
- Avviso

#### `-Confirm [<SwitchParameter>]`

Viene chiesta la conferma prima dell'esecuzione del comando.

#### `-WhatIf [<SwitchParameter>]`

Viene descritto ciò che accadrebbe se venisse eseguito il comando senza effettivamente eseguirlo.

#### `<CommonParameters>`

Questo cmdlet supporta i parametri comuni: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable, e OutVariable. Per altre informazioni, vedere [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

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

### <a name="remarks"></a>COMMENTI

- Per visualizzare gli esempi, digitare: `get-help Switch-MdmDeviceAuthority -examples`  
- Per altre informazioni, digitare: `get-help Switch-MdmDeviceAuthority -detailed`  
- Per informazioni tecniche, digitare: `get-help Switch-MdmDeviceAuthority -full`  
- Per la Guida in linea, digitare: `get-help Switch-MdmDeviceAuthority -online`  



## <a name="next-steps"></a>Passaggi successivi

Dopo avere eseguito la migrazione degli utenti e avere testato la funzionalità di Intune, stabilire se si è pronti per [modificare l'autorità MDM](migrate-change-mdm-authority.md) del tenant di Intune da Configuration Manager a Intune.
