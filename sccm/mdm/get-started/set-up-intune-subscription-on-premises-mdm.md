---
title: Configurare una sottoscrizione a Intune | Locale | System Center Configuration Manager
description: Configurare una sottoscrizione di Intune per tenere traccia delle licenze per la gestione dei dispositivi mobili locale in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4daf5d6ea30aa1fb4aa189ef6da9b364fe197805


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurare una sottoscrizione di Microsoft Intune per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione dei dispositivi mobili locale di System Center Configuration Manager richiede una sottoscrizione di Microsoft Intune per tenere traccia delle licenze. Il servizio Intune non viene usato per gestire i dispositivi o per archiviare le informazioni di gestione. Per la gestione dei dispositivi mobili locale, tutta la gestione dei dispositivi viene gestita dall'infrastruttura di Configuration Manager.  

> [!IMPORTANT]  
>  Configuration Manager non supporta l'uso di Microsoft Intune e dell'infrastruttura di Configuration Manager locale come autorità di gestione allo stesso momento. Pertanto, quando si imposta la sottoscrizione di Intune per la gestione locale, in realtà si disabilita la gestione di Intune.  

 Configurazione del servizio di Intune per l'uso con la gestione dei dispositivi locale prevede i passaggi generali seguenti:  

-   [Iscriversi a Microsoft Intune](#bkmk_signup)  

-   [Aggiungere la sottoscrizione di Intune a Configuration Manager](#bkmk_addSub)  

-   [Configurare la sottoscrizione di Intune per la gestione dei dispositivi mobili (MDM) locale](#bkmk_configure)  

> [!TIP]  
>  È consigliabile configurare la sottoscrizione di Intune per la gestione dei dispositivi mobili locale prima di installare i ruoli del sistema del sito necessari, per ridurre al minimo il tempo necessario prima che diventino funzionanti i ruoli del sistema del sito appena installati.  

##  <a name="a-namebkmksignupa-sign-up-for-microsoft-intune"></a><a name="bkmk_signup"></a> Iscriversi a Microsoft Intune  
 Intune è obbligatorio per il funzionamento della gestione dei dispositivi mobile locale. È sufficiente [iscriversi](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) per una sottoscrizione di valutazione o a pagamento e andare al passaggio successivo per aggiungere la sottoscrizione a Configuration Manager.  

##  <a name="a-namebkmkaddsuba-add-the-intune-subscription-to-configuration-manager"></a><a name="bkmk_addSub"></a> Aggiungere la sottoscrizione di Intune a Configuration Manager  
 Per aggiungere la sottoscrizione a Configuration Manager, la procedura è fondamentalmente la stessa valida per l'aggiunta della sottoscrizione per la gestione dei dispositivi mobili con Intune. Leggere le note riportate di seguito per le differenze specifiche e quindi usare le istruzioni in [To create the Microsoft Intune subscription](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_subscription) (Per creare la sottoscrizione di Microsoft Intune) in [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md) (Gestione dei dispositivi mobili (MDM) con System Center Configuration Manager e Microsoft Intune).  

> [!NOTE]  
>  Quando si aggiunge la sottoscrizione di Intune, tenere presente quanto segue:  
>   
>  -   La raccolta specificata nella procedura guidata Aggiungi sottoscrizione a Microsoft Intune non viene usata per la delega dei diritti utente della gestione dei dispositivi mobili locale. Viene usata solo per la gestione dei dispositivi mobili con Intune. È comunque necessario specificare una raccolta per poter continuare la procedura guidata.  
> -   L'impostazione del codice del sito specificata nella procedura guidata viene ignorata per la gestione dei dispositivi mobili locale. Il codice del sito usato è quello che si specifica nel profilo di registrazione che concede agli utenti l'autorizzazione per registrare i dispositivi.  
> -   Non abilitare l'autenticazione a più fattori. Non è supportata nella gestione dei dispositivi mobili locale.  

##  <a name="a-namebkmkconfigurea-configure-the-intune-subscription-for-on-premises-mobile-device-management"></a><a name="bkmk_configure"></a> Configurare la sottoscrizione di Intune per la gestione dei dispositivi mobili (MDM) locale  

1.  Nella console di Configuration Manager fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune** e scegliere **Proprietà**.  

2.  Nella casella Gestione dispositivi mobili locali selezionare la casella di controllo accanto a **Gestire solo dispositivi in locale**e fare clic su **OK**.  

    > [!NOTE]  
    >  Selezionando questa casella di controllo, si configura la sottoscrizione di Intune per mantenere tutte le informazioni di gestione in locale senza replicare i dati nel cloud.  

3.  Se si prevede di gestire dispositivi Windows 10 Mobile, fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune**, fare clic su **Configura piattaforme**e quindi su  **Windows Phone**.  

4.  Fare clic sulla casella di controllo accanto a **Windows Phone 8.1 e Windows 10 Mobile**, quindi fare clic su **OK**.  

5.  Se si prevede di gestire computer desktop Windows 10, fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune**, fare clic su **Configura piattaforme**e quindi su **Abilita registrazione Windows**.  

6.  Fare clic sulla casella di controllo accanto a **Abilita registrazione Windows**e quindi su **OK**.  



<!--HONumber=Nov16_HO1-->


