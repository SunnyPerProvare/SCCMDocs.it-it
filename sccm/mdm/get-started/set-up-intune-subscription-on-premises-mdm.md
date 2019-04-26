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
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62217016"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurare una sottoscrizione di Microsoft Intune per MDM locale in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager in locale la gestione dei dispositivi mobili (MDM) richiede una sottoscrizione di Microsoft Intune per tenere traccia delle licenze. Il servizio Intune non viene usato per gestire i dispositivi o per archiviare le informazioni di gestione. Per MDM locale, tutte le gestione dei dispositivi viene gestita dall'infrastruttura di Configuration Manager.  

Prima di installare i ruoli del sistema del sito necessari per MDM locale, impostare la sottoscrizione di Intune. Questa azione consente di ridurre il tempo necessario per i ruoli del sistema del sito appena installati diventare funzionale.  

> [!Note]  
> A partire dalla versione 1810, una connessione di Intune non è più necessaria per le nuove distribuzioni MDM locale.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>Iscriversi a Microsoft Intune  

Intune è necessario per rendere funzionale MDM locale. [Effettuare l'iscrizione](https://docs.microsoft.com/intune/free-trial-sign-up) per una sottoscrizione di valutazione o a pagamento. Quindi andare al passaggio successivo per aggiungere la sottoscrizione a Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Aggiungere la sottoscrizione di Intune a Configuration Manager  

Per aggiungere la sottoscrizione a Configuration Manager, seguire i passaggi di base come si farebbe quando si aggiunge la sottoscrizione per la gestione ibrida MDM con Intune. Leggere le note riportate di seguito in merito alle differenze specifiche e seguire le istruzioni in [Configurare la sottoscrizione di Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Quando si aggiunge la sottoscrizione di Intune, tenere presente le note seguenti:  
> 
> - La raccolta specificata di Microsoft Intune procedura guidata Aggiungi sottoscrizione non viene usata per la delega a destra di on-premises MDM utente. Viene usato solo per la gestione dei dispositivi mobili con Intune. Tuttavia, ti viene richiesto di specificare una raccolta per la procedura guidata continuare.  
> 
> - Il codice del sito che specifica nella procedura guidata viene ignorato per MDM locale. Usa il codice del sito specificato nell'ambito della registrazione profilo che concede l'autorizzazione per registrare i dispositivi degli utenti.  
> 
> - Non abilitare multi-factor authentication. Non è supportato in MDM locale.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurare la sottoscrizione di Intune per MDM locale  

1. Nella console di Configuration Manager passare ad il **Administration** dell'area di lavoro, espandere **servizi Cloud**e selezionare il **sottoscrizioni a Microsoft Intune** nodo. Selezionare la sottoscrizione e quindi scegliere **proprietà** nella barra multifunzione.   

    1. Nella sezione nella gestione dei dispositivi mobili locale in fondo il **generale** pagina, scegliere una delle opzioni seguenti:

        - Se si prevede di avere solo i dispositivi gestiti in locale, selezionare l'opzione **gestire solo dispositivi in locale**.  

            > [!NOTE]  
            > Quando si abilita questa opzione, si configura la sottoscrizione di Intune per mantenere tutti i management informazioni in locale. Nessun dato di gestione di dispositivi viene replicato nel cloud.  

        - Se si intende disporre i dispositivi gestiti da Intune sia Configuration Manager in locale, non configurare questa opzione.  

    Selezionare **OK** per chiudere le proprietà della sottoscrizione.

2. Se si prevede di gestire i dispositivi Windows 10 Mobile, selezionare la sottoscrizione nell'elenco, selezionare **Configura piattaforme** nella barra multifunzione e quindi selezionare **Windows Phone**.  

    1. Selezionare l'opzione **Windows Phone 8.1 e Windows 10 Mobile**, quindi selezionare **OK**.  

3. Se si prevede di gestire computer desktop Windows 10, selezionare la sottoscrizione nell'elenco, selezionare **Configura piattaforme** nella barra multifunzione e quindi selezionare **Windows**.  

    1. Selezionare l'opzione **registrazione di Windows di abilitare**e quindi selezionare **OK**.  

