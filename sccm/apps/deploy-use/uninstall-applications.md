---
title: Disinstallare le applicazioni | System Center Configuration Manager
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9f654d899a1e3e1603eccb3943ffc4d4c178e143


---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Disinstallare le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Introduzione  
  
-   Specificare la riga di comando per disinstallare il contenuto del tipo di distribuzione nella pagina **Contenuto** della **Creazione guidata tipo di distribuzione**.  

-   Distribuire l'applicazione tramite un'azione di distribuzione di **Disinstalla**.  

> [!IMPORTANT]  
>  Alcuni tipi di applicazioni non supportano la disinstallazione.  

 Nell'elenco di seguito vengono fornite ulteriori informazioni sul comportamento per la disinstallazione di un'applicazione:  

-   Quando si disinstalla un'applicazione di Configuration Manager, eventuali applicazioni dipendenti non vengono disinstallate automaticamente.  

-   Se si distribuisce un'applicazione che utilizza un'azione di **Disinstalla** per un utente e l'applicazione è stata installata per tutti gli utenti del computer, la disinstallazione potrebbe non riuscire se l'account dell'utente non dispone delle autorizzazioni per la disinstallazione dell'applicazione.  

-   Se si rimuove un utente o un dispositivo da una raccolta in cui è stata distribuita l'applicazione, questa non verrà automaticamente rimossa dal dispositivo.  

-   Una distribuzione con lo scopo di distribuzione di **Disinstalla** non controlla le regole relative ai requisiti. Se l'applicazione è installata sul computer su cui viene eseguita la distribuzione, l'applicazione verrà rimossa.  

> [!IMPORTANT]  
>  È necessario eliminare tutte le distribuzioni simulate o esistenti di un'applicazione in una raccolta prima di poter distribuire l'applicazione con un'azione di distribuzione di **Disinstalla**.  
  
 Per altre informazioni su come creare un tipo di distribuzione, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).  
  
 Per altre informazioni su come distribuire un'applicazione, vedere [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Distribuire applicazioni).  
  
## <a name="uninstall-an-application"></a>Disinstallare un'applicazione  

1.  Configurare il tipo di distribuzione di applicazioni con la riga di comando di disinstallazione utilizzando uno dei seguenti metodi:  

    -   Nella pagina **Generale** della **Creazione guidata applicazione**selezionare l'opzione **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione**. Se le informazioni sono disponibili nei file di installazione, la riga del comando di disinstallazione viene aggiunta automaticamente alle proprietà del tipo di distribuzione.  

    -   Nella pagina **Contenuto** della **Creazione guidata tipo di distribuzione**, nel campo **Disinstalla programma** specificare la riga di comando da utilizzare per disinstallare l'applicazione.  

        > [!NOTE]  
        >  La pagina **Contenuto** viene visualizzata solo se si seleziona l'opzione **Specifica manualmente le informazioni sul tipo di distribuzione** nella pagina **Generale** della **Creazione guidata tipo di distribuzione**.  

    -   Nella scheda **Programmi** della finestra di dialogo *Proprietà\> di ***<nome tipo di distribuzione>** specificare la riga di comando da usare per disinstallare l'applicazione nel campo **Disinstalla programma**.  

2.  Distribuire l'applicazione e selezionare l'azione di distribuzione **Disinstalla** dalla pagina **Impostazioni di distribuzione** della **Distribuzione guidata del software**.  

    > [!NOTE]  
    >  Quando si seleziona un'azione di distribuzione di **Disinstalla**, lo scopo della distribuzione viene automaticamente configurato come **Richiesto**.  



<!--HONumber=Nov16_HO1-->


