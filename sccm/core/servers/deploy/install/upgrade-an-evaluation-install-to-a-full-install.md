---
title: Aggiornare le installazioni di valutazione | Microsoft Docs
description: Informazioni su come eseguire l&quot;aggiornamento di un&quot;installazione di valutazione a installazione completa di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 66dc01b7d1eeed5ad8262c60164460b669301aaf

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>Aggiornare un'installazione di valutazione di System Center Configuration Manager a installazione completa

*Si applica a: System Center Configuration Manager (Current Branch)*



 Se System Center Configuration Manager è stato installato come versione di valutazione, dopo 180 giorni la console di Configuration Manager passerà alla modalità di sola lettura fino a quando il prodotto non sarà attivato nella pagina **Manutenzione sito** del programma di installazione. In qualsiasi momento prima o dopo il periodo di 180 giorni, è possibile eseguire l'aggiornamento di un'installazione di valutazione in un'installazione completa.  

> [!NOTE]  
>  Quando una console di Configuration Manager viene connessa a un'installazione di valutazione di Configuration Manager, sulla barra del titolo della console viene visualizzato il numero di giorni restanti prima della scadenza dell'installazione di valutazione. Il numero di giorni non viene aggiornato automaticamente ma solo quando si stabilisce una nuova connessione a un sito.  

 **È possibile aggiornare i siti seguenti che eseguono un'installazione di valutazione:**  

-   Sito di amministrazione centrale  

-   Sito primario  

Poiché i siti secondati non sono trattati come installazioni di valutazione, non è necessario modificare un sito secondario dopo l'aggiornamento del sito padre primario a un'installazione completa.  

**Prerequisiti per aggiornare una versione di valutazione a una versione completa:**  

-   È necessario avere un prodotto valido da usare durante l'aggiornamento  

-   L'account deve avere le autorizzazioni di **amministratore** per il computer in cui è installato il sito  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>Per aggiornare una versione di valutazione di Configuration Manager a una versione con licenza  

1.  Nel server del sito trovare ed eseguire il programma di installazione di Configuration Manager **SETUP.exe** dalla cartella di installazione di Configuration Manager (**%path%\BIN\X64**).  È necessario copiare il programma di installazione che si trova nel server del sito nella cartella Configuration Manager perché le opzioni di manutenzione del sito non sono disponibili quando si esegue il programma di installazione dal supporto di installazione.  

2.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

3.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Manutenzione sito** selezionare **Aggiornare la versione di valutazione a una versione con licenza**, immettere un codice Product Key valido e quindi fare clic su **Avanti**.  

5.  Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza e fare clic su **Avanti**.  

6.  Nella pagina **Configurazione** fare clic su **Chiudi** per completare la procedura guidata.  

    > [!NOTE]  
    >  La barra del titolo delle console di Configuration Manager che rimangono connesse al sito aggiornato indica che è ancora attiva la versione di valutazione finché non si esegue la riconnessione delle console al sito.  



<!--HONumber=Dec16_HO3-->


