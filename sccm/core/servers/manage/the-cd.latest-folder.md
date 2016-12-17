---
title: Cartella CD.Latest | System Center Configuration Manager
description: Informazioni sul nuovo processo di aggiornamento che offre aggiornamenti per il prodotto all'interno della console di Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fc63227aa4345fb58e7efc15abd55071fb33e5d5


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>Cartella CD.Latest per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager è disponibile un nuovo processo di aggiornamento che offre aggiornamenti per il prodotto all'interno della console di Configuration Manager. Per supportare questo nuovo metodo di aggiornamento di Configuration Manager viene creata una nuova cartella denominata **CD.Latest** che contiene una copia dei file di installazione di Configuration Manager per la versione aggiornata del sito.  

A partire dall'aggiornamento 1606, la cartella CD.Latest contiene una cartella denominata **Redist** che contiene i file ridistribuibili usati e scaricati dal programma di installazione. Questi file corrispondono alla versione dei file di Configuration Manager della cartella CD.Latest. Quando si esegue l'installazione da una cartella CD.Latest, è necessario usare i file che corrispondono alla versione del programma di installazione. A tale scopo è possibile impostare il programma di installazione in modo che scarichi i file nuovi e aggiornati da Microsoft o usi i file della cartella Redist inclusa nella cartella CD.Latest.

> [!TIP]
> Se non è ancora stata installata la versione 1606, è necessario assicurarsi che i file redist usati siano aggiornati. Se i file redist non sono stati scaricati di recente, consentire al programma di installazione di scaricarli da Microsoft.   

 Di seguito sono riportati alcuni scenari di creazione o aggiornamento della cartella CD.Latest in un sito di amministrazione centrale o in un server del sito primario:  

-   Installare un aggiornamento o un hotfix dalla console di Configuration Manager. La cartella viene creata o aggiornata nella cartella di installazione di Configuration Manager.  

-   Eseguire l'attività di backup predefinita di Configuration Manager. La cartella viene creata o aggiornata nel percorso della cartella di backup specificata.  

I file di origine della cartella CD.Latest sono supportati per le operazioni seguenti:  

1.  **Backup e ripristino:** la cartella CD.Latest contiene file di origine usati per reinstallare il sito come parte di un ripristino del sito. Per ripristinare un sito di Configuration Manager, il backup del sito deve includere la cartella CD.Latest. L'attività di backup del sito predefinita include automaticamente questa cartella come parte del backup del sito.  

    -   **Quando si reinstalla un sito come parte di un ripristino del sito** , è necessario installarlo dalla cartella CD.Latest inclusa nel backup. In questo modo, il sito viene installato usando le versioni dei file che corrispondono al backup del sito e al database del sito.  

        > [!IMPORTANT]  
        >  Se la cartella CD.Latest corretta e il relativo contenuto non sono disponibili, non è possibile ripristinare un sito che deve essere reinstallato.  

    -   Quando una cartella CD.Latest non è disponibile, ma si ha un sito primario figlio o un sito di amministrazione centrale funzionante è possibile usarlo come sito di riferimento per il ripristino.  

2.  **Per installare un sito primario figlio:** quando si vuole installare un nuovo sito primario figlio all'interno di un sito di amministrazione centrale in cui sono stati installati uno o più aggiornamenti nella console, è necessario usare il programma di installazione e i file di origine dalla cartella CD.Latest dal sito di amministrazione centrale. Quando il programma di installazione viene eseguito da una copia della cartella CD.Latest dal sito di amministrazione centrale, usa i file di origine di installazione che corrispondono alla versione del sito di amministrazione centrale. Per altre informazioni, vedere [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Usare l'installazione guidata per installare i siti).  

3.  **Per espandere un sito primario autonomo:** quando si espande un sito primario autonomo installando un nuovo sito di amministrazione centrale, è necessario usare il programma di installazione e i file di origine della cartella CD.Latest dal sito primario per installare il nuovo sito di amministrazione centrale. Quando il programma di installazione viene eseguito da una copia della cartella CD.Latest dal sito primario, usa i file di origine di installazione che corrispondono alla versione del sito primario. Per altre informazioni, vedere [Expand a stand-alone primary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) (Espandere un sito primario autonomo) in [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Usare l'installazione guidata per installare i siti)

> [!IMPORTANT]  
>  I file di origine della cartella CD.Latest aggiornati non sono supportati per le operazioni seguenti:  
>   
>  -   Installazione di un nuovo sito per una nuova gerarchia  
>  -   Aggiornamento dal sito di Microsoft System Center 2012 Configuration Manager a System Center Configuration Manager



<!--HONumber=Nov16_HO1-->

