---
title: Disinstallare applicazioni | Microsoft Docs
description: Disinstallare le applicazioni usando System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2d0c0bc2e4e080e6061d8d3fe6cafd264d95c42a
ms.openlocfilehash: f42fee5974567f667c015a6b0bf34d9a9a7d2dab


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Disinstallare le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Eseguire le azioni seguenti per disinstallare un'applicazione distribuita in precedenza.

-   Specificare la riga di comando per disinstallare il contenuto del tipo di distribuzione nella pagina **Contenuto** della Creazione guidata tipo di distribuzione.  

-   Distribuire l'applicazione tramite un'azione di distribuzione di **Disinstalla**.  

> [!IMPORTANT]  
> Alcuni tipi di applicazioni non supportano la disinstallazione.  

 Questo elenco include altre informazioni sulle modalità di disinstallazione delle applicazioni:  

-   Quando si disinstalla un'applicazione di System Center Configuration Manager (Configuration Manager), le eventuali applicazioni dipendenti non vengono disinstallate automaticamente.  

-   Se si distribuisce un'applicazione che usa un'azione **Disinstalla** per un utente e l'applicazione è stata installata per tutti gli utenti del computer, la disinstallazione potrebbe non riuscire se l'account dell'utente non ha le autorizzazioni per la disinstallazione dell'applicazione.  

-   Se si rimuove un utente o un dispositivo da una raccolta in cui è stata distribuita un'applicazione, questa non verrà automaticamente rimossa dal dispositivo.  

-   Una distribuzione con lo scopo di distribuzione di **Disinstalla** non controlla le regole relative ai requisiti. Se l'applicazione è installata sul computer su cui viene eseguita la distribuzione, l'applicazione verrà rimossa.  

> [!IMPORTANT]  
> È necessario eliminare tutte le distribuzioni simulate o esistenti di un'applicazione in una raccolta prima di poter distribuire l'applicazione con un'azione di distribuzione di **Disinstalla**.  

 Per altre informazioni su come creare un tipo di distribuzione, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).  

 Per altre informazioni su come distribuire un'applicazione, vedere [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Distribuire applicazioni).  

## <a name="uninstall-an-application"></a>Disinstallare un'applicazione  

1.  Configurare il tipo di distribuzione di applicazioni con la riga di comando di disinstallazione utilizzando uno dei seguenti metodi:  

    -   Nella pagina **Generale** della Creazione guidata applicazione selezionare l'opzione **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione**. Se le informazioni sono disponibili nei file di installazione, la riga del comando di disinstallazione viene aggiunta automaticamente alle proprietà del tipo di distribuzione.  

    -   Nella pagina **Contenuto** della Creazione guidata tipo di distribuzione, nel campo **Disinstalla programma** specificare la riga di comando da usare per disinstallare l'applicazione.  

        > [!NOTE]  
        >  La pagina **Contenuto** viene visualizzata solo se si seleziona l'opzione **Specifica manualmente le informazioni sul tipo di distribuzione** nella pagina **Generale** della Creazione guidata tipo di distribuzione.  

    -   Nella scheda **Programmi** della finestra di dialogo **<*nome tipo di distribuzione*> Proprietà** specificare la riga di comando da usare per disinstallare l'applicazione nel campo **Disinstalla programma**.  

2.  Distribuire l'applicazione e selezionare l'azione di distribuzione **Disinstalla** nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software.  

    > [!NOTE]  
    >  Quando si seleziona un'azione di distribuzione di **Disinstalla**, lo scopo della distribuzione viene automaticamente configurato come **Richiesto**.  



<!--HONumber=Dec16_HO3-->


