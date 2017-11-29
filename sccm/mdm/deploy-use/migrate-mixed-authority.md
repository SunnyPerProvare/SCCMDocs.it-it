---
title: "Modificare l'autorità MDM per utenti specifici (autorità MDM mista)"
titleSuffix: Configuration Manager
description: "Informazioni su come modificare l'autorità MDM dalla soluzione MDM ibrida alla versione autonoma di Intune per alcuni utenti."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Modificare l'autorità MDM per utenti specifici (autorità MDM mista) 

*Si applica a: System Center Configuration Manager (Current Branch)*    

È possibile configurare un'autorità MDM mista nello stesso tenant selezionando alcuni utenti da gestire in Intune e altri da gestire con la soluzione MDM ibrida (Intune integrato con Configuration Manager). Questo argomento fornisce informazioni su come iniziare a spostare gli utenti nella versione autonoma di Intune e presuppone che siano stati completati i passaggi seguenti:
- Uso dello strumento di importazione dati per [importare gli oggetti di Configuration Manager in Intune](migrate-import-data.md) (facoltativo).
- [Preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md) per assicurarsi che gli utenti e i relativi dispositivi continuino a essere gestiti dopo la migrazione.

> [!Note]    
> Se si decide di eseguire un ripristino completo del tenant, che consente di rimuovere tutti i criteri, le app e le registrazioni dei dispositivi, contattare il supporto tecnico per assistenza.

Gli utenti di cui è stata eseguita la migrazione e i relativi dispositivi verranno gestiti in Intune, mentre gli altri dispositivi continueranno a essere gestiti in Configuration Manager. Iniziare con un piccolo gruppo di utenti di test, per verificare che tutto funzioni come previsto. Eseguire quindi gradualmente la migrazione di altri gruppi di utenti, fino a quando non si è pronti a spostare l'autorità MDM a livello di tenant da Configuration Manager alla versione autonoma di Intune. 

## <a name="things-to-know-before-you-migrate-users"></a>Informazioni da sapere prima di eseguire la migrazione degli utenti
- Durante la migrazione in fasi, le app o i criteri MDM esistenti in Configuration Manager continuano a essere applicati ai dispositivi della soluzione MDM ibrida.
- Gli utenti vengono aggiunti a un gruppo di AAD designato come gruppo di migrazione. Tutti i dispositivi associati agli utenti nel gruppo di migrazione vengono gestiti in Intune.
- Se i dispositivi vengono aggiunti al gruppo di AAD, vengono ignorati a meno che non si tratti di un dispositivo senza un utente associato.
- Gli utenti non in un gruppo di AAD contrassegnato per la migrazione ereditano automaticamente l'autorità MDM a livello di tenant (Configuration Manager).
- Quando si esegue la migrazione di un utente a Intune, l'utente e i dispositivi verranno visualizzati in Intune nel portale di Azure dopo circa 15 minuti.  
- Quando si esegue la migrazione di utenti alla versione autonoma di Intune, continuare a gestire le impostazioni seguenti da Configuration Manager sia per i dispositivi della versione autonoma di Intune che per quelli della soluzione MDM ibrida:
    - [Certificato Apple Push Notification Service (APN)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [DEP (Device Enrollment Program)](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Profili di registrazione
    - [Licenze Volume Purchase Program (VPP)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificatori aziendali 
    - [Certificati di firma del codice](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Categorie di dispositivi](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Manager di registrazione](/sccm/mdm/plan-design/device-enrollment-methods)
    - Termini e condizioni
    - File SLK di Windows
    - Personalizzazione del portale aziendale    
      
> [!Important]    
  > Continuare a modificare i criteri a livello di tenant usando la console di Configuration Manager. Dopo avere [modificato l'autorità MDM a livello di tenant](change-mdm-authority.md) spostandola in Intune, si gestiranno questi criteri in Intune in Azure. 
- È consigliabile non eseguire la migrazione degli account utente che sono stati aggiunti come manager di registrazione dispositivi in Configuration Manager. In seguito, quando si modificherà l'autorità MDM a livello di tenant spostandola in Intune, verrà eseguita correttamente la migrazione di questi account utente. Se si esegue la migrazione dell'account utente manager di registrazione dispositivi prima della modifica dell'autorità MDM a livello di tenant, è necessario aggiungere manualmente l'utente come manager di registrazione dispositivi in Intune in Azure. La migrazione dei dispositivi registrati usando un manager di registrazione dispositivi non verrà tuttavia eseguita correttamente. Per la migrazione di questi dispositivi è necessario chiamare il supporto tecnico. Per informazioni dettagliate, vedere [Aggiungere un manager di registrazione dispositivi](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Per i dispositivi registrati usando un manager di registrazione dispositivi e i dispositivi che non hanno utenti associati non viene eseguita la migrazione alla nuova autorità MDM. Per tali dispositivi, è necessario chiamare il supporto tecnico per assistenza per i singoli dispositivi. Non chiedere al supporto tecnico di reimpostare l'autorità MDM, altrimenti i dati in Intune verranno cancellati. È necessario [modificare l'autorità MDM](migrate-change-mdm-authority.md) dalla console di Configuration Manager.

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

## <a name="next-steps"></a>Passaggi successivi
Dopo avere seguito la migrazione degli utenti e avere testato la funzionalità di Intune, stabilire se si è pronti per [modificare l'autorità MDM](migrate-change-mdm-authority.md) del tenant di Intune da Configuration Manager a Intune. 