---

title: Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso | Configuration Manager
description: Seguire le procedure qui riportate per verificare che la sincronizzazione degli aggiornamenti software sia stata completata nei metadati del server di esportazione, degli aggiornamenti di esportazione e degli aggiornamenti di importazione.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f821433d017f2e14f874eca359df0f38e896ab69



---

# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso  

*Si applica a: System Center Configuration Manager (Current Branch)*

 Quando il punto di aggiornamento software nel sito di livello superiore viene disconnesso da Internet, è necessario utilizzare le funzioni di esportazione e importazione dello strumento WSUSUtil per sincronizzare i metadati degli aggiornamenti software. Come origine della sincronizzazione è possibile scegliere un server WSUS esistente che non si trovi nella gerarchia di Configuration Manager. In questo argomento vengono specificate informazioni su come usare le funzioni di esportazione e importazione dello strumento WSUSUtil.  

 Per esportare e importare i metadati degli aggiornamenti software è necessario esportare i metadati degli aggiornamenti software dal database di WAUS in un server di esportazione specifico, quindi copiare i file con le condizioni di licenza archiviate in locale nel punto di aggiornamento software disconnesso e infine importare i metadati degli aggiornamenti software nel database di WSUS nel punto di aggiornamento software disconnesso.  

 Utilizzare la tabella seguente per identificare il server di esportazione in cui esportare i metadati degli aggiornamenti software.  

|Punto di aggiornamento software|Origine aggiornamento upstream per i punti di aggiornamento software connessi|Server di esportazione per un punto di aggiornamento software disconnesso|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Sito di amministrazione centrale|Microsoft Update (Internet)<br /><br /> Server WSUS esistente|Scegliere un server WSUS sincronizzato con Microsoft Update usando le classificazioni di aggiornamento software, i prodotti e le lingue necessari nell'ambiente di Configuration Manager.|  
|Sito primario autonomo|Microsoft Update (Internet)<br /><br /> Server WSUS esistente|Scegliere un server WSUS sincronizzato con Microsoft Update usando le classificazioni di aggiornamento software, i prodotti e le lingue necessari nell'ambiente di Configuration Manager.|  

 Prima di avviare il processo di esportazione, verificare che la sincronizzazione degli aggiornamenti software sia stata completata nel server di esportazione selezionato per verificare che i metadati degli aggiornamenti software più recenti siano sincronizzati. Per verificare che la sincronizzazione degli aggiornamenti software sia stata completata, utilizzare la procedura seguente.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Per verificare che la sincronizzazione degli aggiornamenti software sia stata completata nel server di esportazione  

1.  Aprire la console di amministrazione di WSUS e connettersi al database di WSUS nel server di esportazione.  

2.  Nella console di amministrazione di WSUS fare clic su **Sincronizzazioni**. Un elenco dei tentativi di sincronizzazione degli aggiornamenti software verrà visualizzato nel riquadro dei risultati.  

3.  Nel riquadro dei risultati cercare i tentativi di sincronizzazione degli aggiornamenti software più recenti e verificare che siano stati completati.  

> [!IMPORTANT]  
>  Lo strumento WSUSUtil deve essere eseguito in locale nel server di esportazione per esportare i metadati degli aggiornamenti software e deve inoltre essere eseguito nel server del punto di aggiornamento software disconnesso per importare i metadati degli aggiornamenti software. Inoltre, l'utente che esegue lo strumento WSUSUtil deve essere un membro del gruppo di amministratori locali in ogni server.  

## <a name="export-process-for-software-updates"></a>Processo di esportazione per gli aggiornamenti software  
 Il processo di esportazione degli aggiornamenti software consiste in due passaggi principali: uno per copiare i file con le condizioni di licenza archiviate in locale nel punto di aggiornamento software disconnesso e uno per esportare i metadati degli aggiornamenti software dal database WSUS nel server di esportazione.  

 Utilizzare la procedura seguente per copiare i metadati delle condizioni di licenza in locale nel punto di aggiornamento software disconnesso.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Per copiare i file in locale dal server di esportazione al server del punto di aggiornamento software disconnesso  

1.  Nel server di esportazione individuare la cartella in cui sono archiviati gli aggiornamenti software e le condizioni di licenza per gli aggiornamenti software. Per impostazione predefinita, il server WSUS archivia i file in <*UnitàInstallazioneWSUS*>\WSUS\WSUSContent\\, dove *UnitàInstallazioneWSUS* è l'unità in cui è installato WSUS.  

2.  Copiare tutti i file e le cartelle da questo percorso nella cartella WSUSContent sul server del punto di aggiornamento software disconnesso.  

 Utilizzare la procedura seguente per esportare i metadati degli aggiornamenti software dal database di WSUS nel server di esportazione.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Per esportare i metadati degli aggiornamenti software dal database di WSUS nel server di esportazione  

1.  Nel prompt dei comandi nel server di esportazione andare alla cartella che contiene WSUSutil.exe. Per impostazione predefinita, lo strumento si trova in %*ProgramFiles*%\Update Services\Tools. Ad esempio, se lo strumento si trova nel percorso predefinito, digitare **cd %ProgramFiles%\Update Services\Tools**.  

2.  Digitare quanto segue per esportare i metadati degli aggiornamenti software in un file del pacchetto:  

     **wsusutil.exe export**  *nomepacchetto*  *filelog*  

     Ad esempio:  

     **wsusutil.exe export export.cab export.log**  

     Il formato può essere riepilogato come segue: WSUSutil.exe è seguito dall'opzione di esportazione, dal nome del file CAB di esportazione creato durante l'operazione di esportazione e dal nome di un file di log. WSUSutil.exe esporta i metadati dal server di esportazione e crea un file di log dell'operazione.  

    > [!NOTE]  
    >  Il pacchetto (file CAB) e il nome del file di log devono essere univoci nella cartella corrente.  

3.  Spostare il pacchetto di esportazione nella cartella che contiene WSUSutil.exe nel server di WSUS.  

    > [!NOTE]  
    >  Se il pacchetto viene spostato in questa cartella, l'esperienza di importazione può essere più semplice. È possibile spostare il pacchetto in qualsiasi percorso accessibile al server di importazione e quindi specificare il percorso quando si esegue WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importare i metadati degli aggiornamenti software  
 Utilizzare la procedura seguente per importare i metadati degli aggiornamenti software dal server di esportazione al punto di aggiornamento software disconnesso.  

> [!IMPORTANT]  
>  Non importare i dati esportati da un'origine non attendibile. Se si importano contenuti da un'origine non attendibile, la sicurezza del server WSUS potrebbe essere compromessa.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Per importare i metadati nel database del server di importazione  

1.  Nel prompt dei comandi nel server WSUS di importazione andare alla cartella che contiene WSUSutil.exe. Per impostazione predefinita, lo strumento si trova in %*ProgramFiles*%\Update Services\Tools.  

2.  Digitare quanto segue:  

     **wsusutil.exe import**  *nomepacchetto*  *filelog*  

     Ad esempio:  

     **wsusutil.exe import export.cab import.log**  

     Il formato può essere riepilogato come segue: WSUSutil.exe è seguito dal comando di importazione, dal nome del file CAB del pacchetto creato durante l'operazione di esportazione, dal percorso del file del pacchetto se si trova in un'altra cartella e dal nome di un file di log. WSUSutil.exe importa i metadati dal server di esportazione e crea un file di log dell'operazione.  

## <a name="next-steps"></a>Passaggi successivi
Dopo aver sincronizzato gli aggiornamenti software per la prima volta o dopo che sono stati resi disponibili nuovi prodotti o classificazioni, è necessario [configurare le classificazioni e i prodotti nuovi](configure-classifications-and-products.md) per sincronizzare gli aggiornamenti software con i nuovi criteri.

Dopo aver sincronizzato gli aggiornamenti software con i criteri appropriati, [gestire le impostazioni per gli aggiornamenti software](manage-settings-for-software-updates.md).  



<!--HONumber=Nov16_HO1-->

