---
title: 'Configurare la sottoscrizione di Intune '
titleSuffix: Configuration Manager
description: Configurare una sottoscrizione di Intune per tenere traccia delle licenze per la gestione dei dispositivi mobili locale in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 64acd3dbdafaec3dbf49e7939718100897c0976b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422624"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurare una sottoscrizione di Microsoft Intune per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione dei dispositivi mobili locale di System Center Configuration Manager richiede una sottoscrizione di Microsoft Intune per tenere traccia delle licenze. Il servizio Intune non viene usato per gestire i dispositivi o per archiviare le informazioni di gestione. Per la gestione dei dispositivi mobili locale, tutta la gestione dei dispositivi viene gestita dall'infrastruttura di Configuration Manager.  

> [!NOTE]  
> A partire dalla versione 1610, Configuration Manager supporta l'uso di Microsoft Intune e dell'infrastruttura di Configuration Manager locale per gestire simultaneamente i dispositivi mobili.   

> [!TIP]  
>  È consigliabile configurare la sottoscrizione di Intune per la gestione dei dispositivi mobili locale prima di installare i ruoli del sistema del sito necessari, per ridurre al minimo il tempo necessario prima che diventino funzionanti i ruoli del sistema del sito appena installati.  

##  <a name="sign-up-for-microsoft-intune"></a>Iscriversi a Microsoft Intune  
 Intune è obbligatorio per il funzionamento della gestione dei dispositivi mobile locale. È sufficiente [iscriversi](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) per una sottoscrizione di valutazione o a pagamento e andare al passaggio successivo per aggiungere la sottoscrizione a Configuration Manager.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Aggiungere la sottoscrizione di Intune a Configuration Manager  
 Per aggiungere la sottoscrizione a Configuration Manager, la procedura è fondamentalmente la stessa valida per l'aggiunta della sottoscrizione per la gestione dei dispositivi mobili con Intune. Leggere le note riportate di seguito in merito alle differenze specifiche e seguire le istruzioni in [Configurare la sottoscrizione di Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]
>  Quando si aggiunge la sottoscrizione di Intune, tenere presente quanto segue:  
> 
> - La raccolta specificata nella procedura guidata Aggiungi sottoscrizione a Microsoft Intune non viene usata per la delega dei diritti utente della gestione dei dispositivi mobili locale. Viene usata solo per la gestione dei dispositivi mobili con Intune. È comunque necessario specificare una raccolta per poter continuare la procedura guidata.  
>   -   L'impostazione del codice del sito specificata nella procedura guidata viene ignorata per la gestione dei dispositivi mobili locale. Il codice del sito usato è quello che si specifica nel profilo di registrazione che concede agli utenti l'autorizzazione per registrare i dispositivi.  
>   -   Non abilitare l'autenticazione a più fattori. Non è supportata nella gestione dei dispositivi mobili locale.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Configurare la sottoscrizione di Intune per la gestione dei dispositivi mobili (MDM) locale  

1. Nella console di Configuration Manager fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune** e scegliere **Proprietà**.  

2. Nella casella On Premises Mobile Device Management (Gestione dispositivi mobili locale) scegliere una delle soluzioni seguenti:

   - Se si prevede di gestire i dispositivi solo in locale, selezionare la casella di controllo accanto a **Only manage devices on-premises** (Gestire solo dispositivi in locale) e fare clic su **OK**.  

     > [!NOTE]  
     >  Selezionando questa casella di controllo, si configura la sottoscrizione di Intune per mantenere tutte le informazioni di gestione in locale senza replicare i dati nel cloud.  

   - Se si prevede di gestire i dispositivi in locale sia con Intune che con Configuration Manager, non selezionare la casella.

3. Se si prevede di gestire dispositivi Windows 10 Mobile, fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune**, fare clic su **Configura piattaforme**e quindi su  **Windows Phone**.  

4. Fare clic sulla casella di controllo accanto a **Windows Phone 8.1 e Windows 10 Mobile**, quindi fare clic su **OK**.  

5. Se si prevede di gestire computer desktop Windows 10, fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune**, fare clic su **Configura piattaforme**e quindi su **Abilita registrazione Windows**.  

6. Fare clic sulla casella di controllo accanto a **Abilita registrazione Windows**e quindi su **OK**.  
