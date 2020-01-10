---
title: Configurare la sottoscrizione di Intune
titleSuffix: Configuration Manager
description: Configurare una sottoscrizione di Intune per tenere traccia delle licenze per la gestione dei dispositivi mobili locale in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1f90b4088f066132e61d7dd60e3fe259eb945f96
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75821614"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurare una sottoscrizione di Microsoft Intune per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager gestione di dispositivi mobili (MDM) locale richiede una sottoscrizione Microsoft Intune per tenere traccia delle licenze. Il servizio Intune non viene usato per gestire i dispositivi o per archiviare le informazioni di gestione. Per la gestione di dispositivi mobili locale, tutta la gestione dei dispositivi viene gestita dall'infrastruttura Configuration Manager.  

Prima di installare i ruoli del sistema del sito richiesti per MDM locale, configurare la sottoscrizione di Intune. Questa azione riduce al minimo il tempo necessario affinché i ruoli del sistema del sito appena installati diventino operativi.  

> [!Note]  
> A partire dalla versione 1810, una connessione a Intune non è più necessaria per le nuove distribuzioni MDM locali.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>Iscriversi a Microsoft Intune  

Intune è necessario per rendere funzionale MDM locale. [Iscriversi](https://docs.microsoft.com/intune/free-trial-sign-up) per una sottoscrizione di valutazione o a pagamento. Quindi, andare al passaggio successivo per aggiungere la sottoscrizione a Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Aggiungere la sottoscrizione di Intune a Configuration Manager  

Per aggiungere la sottoscrizione a Configuration Manager, seguire gli stessi passaggi di base che si otterrebbe quando si aggiunge la sottoscrizione per MDM ibrida con Intune. Leggere le note riportate di seguito in merito alle differenze specifiche e seguire le istruzioni in [Configurare la sottoscrizione di Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Quando si aggiunge la sottoscrizione di Intune, tenere presenti le note seguenti:  
> 
> - La raccolta specificata nella procedura guidata Aggiungi sottoscrizione Microsoft Intune non viene usata per la delega dei diritti utente MDM locale. Viene usato solo per la gestione dei dispositivi mobili con Intune. Tuttavia, è necessario specificare una raccolta per poter continuare la procedura guidata.  
> 
> - Il codice del sito specificato nella procedura guidata viene ignorato per MDM locale. Usa il codice del sito specificato nel profilo di registrazione che concede agli utenti l'autorizzazione per registrare i dispositivi.  
> 
> - Non abilitare l'autenticazione a più fattori. Non è supportato in MDM locale.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurare la sottoscrizione di Intune per MDM locale  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** , espandere **servizi cloud**e selezionare il nodo **sottoscrizioni Microsoft Intune** . Selezionare la sottoscrizione e quindi scegliere **Proprietà** nella barra multifunzione.   

    1. Nella sezione gestione dei dispositivi mobili locale nella parte inferiore della pagina **generale** scegliere una delle opzioni seguenti:

        - Se si prevede di avere solo dispositivi gestiti in locale, selezionare l'opzione per **gestire solo i dispositivi locali**.  

            > [!NOTE]  
            > Quando si abilita questa opzione, si configura la sottoscrizione di Intune in modo che mantenga tutte le informazioni di gestione in locale. Nessun dato di gestione del dispositivo viene replicato nel cloud.  

        - Se si prevede di gestire dispositivi gestiti da Intune e Configuration Manager in locale, non configurare questa opzione.  

    Selezionare **OK** per chiudere le proprietà della sottoscrizione.

2. Se si prevede di gestire i dispositivi Windows 10 Mobile, selezionare la sottoscrizione nell'elenco, selezionare **Configura piattaforme** nella barra multifunzione e quindi selezionare **Windows Phone**.  

    1. Selezionare l'opzione per **Windows Phone 8,1 e Windows 10 Mobile**, quindi fare clic su **OK**.  

3. Se si prevede di gestire computer desktop Windows 10, selezionare la sottoscrizione nell'elenco, selezionare **Configura piattaforme** nella barra multifunzione e quindi selezionare **Windows**.  

    1. Selezionare l'opzione per **abilitare la registrazione di Windows**e quindi fare clic su **OK**.  

