---
title: Strumento di registrazione dell'aggiornamento | System Center Configuration Manager
description: Informazioni su quando e come usare lo strumento di registrazione dell'aggiornamento per importare manualmente un aggiornamento nella console di Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 176c1d7055ae8706b92886d59d8a048dd867c18b


---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Usare lo strumento di registrazione dell'aggiornamento per importare hotfix in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Alcuni aggiornamenti per Configuration Manager non sono disponibili dal servizio cloud Microsoft e possono essere ottenuti solo come rilascio fuori programma. Questo si verifica, ad esempio, nel caso di un hotfix a rilascio limitato per la soluzione di un problema specifico.   
Quando è necessario installare un rilascio fuori programma e il nome file dell'aggiornamento o dell'hotfix termina con l'estensione **update.exe**, si usa lo **strumento di registrazione dell'aggiornamento** per importare manualmente l'aggiornamento nella console di Configuration Manager. Lo strumento consente di estrarre e trasferire il pacchetto di aggiornamento nel server del sito e di registrare l'aggiornamento con la console di Configuration Manager.  

 Se il file dell'hotfix ha l'estensione **exe** (non **update.exe**), vedere [Usare il programma di installazione di hotfix per installare gli aggiornamenti per System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Questo argomento fornisce indicazioni generali su come installare gli hotfix che aggiornano System Center Configuration Manager. Per informazioni dettagliate su un aggiornamento o un hotfix specifico, vedere l'articolo corrispondente della Knowledge Base (KB) nel sito del supporto tecnico Microsoft.  

 **Prerequisiti per l'uso dello strumento di registrazione dell'aggiornamento:**  

-   Solo gli aggiornamenti fuori programma che terminano con l'estensione **update.exe** possono essere installati usando questo strumento  

-   Lo strumento gestisce autonomamente i singoli aggiornamenti ottenuti direttamente da Microsoft  

-   Lo strumento non dipende dalla modalità del punto di connessione del servizio  

-   Lo strumento deve essere eseguito nel computer che ospita il punto di connessione del servizio  

-   Nel computer in cui è in esecuzione lo strumento (il computer del punto di connessione del servizio) deve essere installato .NET Framework 4.52  

-   L'account usato per eseguire lo strumento deve avere le autorizzazioni di **amministratore locale** nel computer che ospita il punto di connessione del servizio dove viene eseguito lo strumento  

-   L'account usato per eseguire lo strumento deve avere le autorizzazioni di **scrittura** per la cartella seguente nel computer che ospita il punto di connessione del servizio: **&lt;Directory di installazione di ConfigMgr\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Per usare lo strumento di registrazione dell'aggiornamento  

1.  Nel computer che ospita il punto di connessione del servizio:  

    -   Aprire un prompt dei comandi con privilegi amministrativi e quindi passare alle directory nel percorso che contiene **&lt;Prodotto\>-&lt;versione prodotto\>-&lt;ID articolo KB\>-ConfigMgr.Update.exe**  

2.  Eseguire il comando seguente per avviare lo strumento di registrazione dell'aggiornamento:  

    -   **&lt;Prodotto\>-&lt;versione prodotto\>-&lt;ID articolo KB\>-ConfigMgr.Update.exe**  

    Dopo la registrazione, l'hotfix, viene visualizzato come nuovo aggiornamento nella console entro 24 ore.  È possibile accelerare il processo in uno dei modi seguenti:  

    -   Con la versione 1511: nella console di Configuration Manager passare ad **Amministrazione > Servizi cloud > Aggiornamenti e manutenzione** e quindi selezionare **Avviare immediatamente il processo di individuazione dell'aggiornamento**.  Dopo il completamento del processo di registrazione verrà così avviata immediatamente l'importazione dell'hotfix, rendendolo disponibile nella console.  

    -   Con la versione 1602 e le versioni successive: nella console di Configuration Manager passare ad **Amministrazione > Servizi cloud > Aggiornamenti e manutenzione** e quindi fare clic su **Verifica la disponibilità di aggiornamenti**  

    Lo strumento di registrazione dell'aggiornamento registra le azioni in un file con estensione log nel computer locale. Il file di log ha lo stesso nome del file EXE dell'hotfix e viene scritto nella cartella **%SystemRoot%/Temp**.  

     Dopo la registrazione dell'aggiornamento, è possibile chiudere lo strumento di registrazione.  

3.  Aprire la console di Configuration Manager e passare ad **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**. Gli hotfix importati sono ora disponibili per l'installazione. Per informazioni sull'installazione degli aggiornamenti, vedere [Installare gli aggiornamenti nella console per System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  



<!--HONumber=Nov16_HO1-->

