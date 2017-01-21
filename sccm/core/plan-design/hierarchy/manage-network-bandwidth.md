---
title: Gestire la larghezza di banda di rete per i contenuti | Microsoft Docs
description: Configurare la pianificazione, la limitazione della larghezza di banda e il contenuto pre-installato per System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 14ce376f385ec19d224e8b1a2918eed5379a64e5


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Pianificazione e limitazione della larghezza di banda della rete  
 Per consentire la gestione della larghezza di banda di rete usata per il processo di gestione del contenuto, è possibile usare i controlli predefiniti di Configuration Manager per la pianificazione e la limitazione della larghezza di banda della rete oppure usare contenuto pre-installato.  

 Quando si crea un pacchetto, modificare il percorso di origine per il contenuto oppure aggiornare il contenuto nel punto di distribuzione; i file vengono copiati dal percorso di origine alla raccolta contenuto nel server del sito. Quindi, il contenuto viene copiato dalla raccolta contenuto nel server del sito alla raccolta contenuto nei punti di distribuzione. Quando i file origine di contenuto vengono aggiornati e i file di origine sono già stati distribuiti, Configuration Manager recupera solo i file nuovi o aggiornati e li invia al punto di distribuzione. È possibile configurare la pianificazione e la limitazione di controlli per la comunicazione da sito a sito e per la comunicazione tra un server del sito e un punto di distribuzione remoto. Quando la larghezza di banda di rete tra il server del sito e il punto di distribuzione remoto è limitata anche dopo aver configurato le impostazioni di pianificazione e limitazione, è possibile pre-installare il contenuto nel punto di distribuzione.  

 In Configuration Manager è possibile configurare una pianificazione e impostare specifiche impostazioni di limitazione nei punti di distribuzione remoti che determinano quando e come viene eseguita la distribuzione del contenuto. Ogni punto di distribuzione remoto può avere diverse configurazioni che consentono di limitare la larghezza di banda di rete dell'indirizzo dal server del sito al punto di distribuzione remoto. I controlli usati per la pianificazione e la limitazione al punto di distribuzione remoto sono simili alle impostazioni per un indirizzo mittente standard, ma in questo caso le impostazioni vengono usate da un componente nuovo chiamato Package Transfer Manager. Package Transfer Manager distribuisce il contenuto da un server del sito, come sito primario o secondario, in un punto di distribuzione installato su un sistema del sito. Le impostazioni di limitazione sono configurate nella scheda **Limiti di velocità** , mentre le impostazioni di pianificazione nella scheda **Pianifica** per un punto di distribuzione che non si trova su un server del sito. Le impostazioni di ora sono basate sul fuso orario del sito di invio, non del punto di distribuzione.  

> [!WARNING]  
>  Le schede **Limiti di velocità** e **Pianifica** vengono visualizzate solo nelle proprietà dei punti di distribuzione che non sono installati in un server del sito.  

Per altre informazioni sulla configurazione delle impostazioni di pianificazione e limitazione per un punto di distribuzione remoto, vedere [Install and configure distribution points for System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points) (Installare e configurare i punti di distribuzione per System Center Configuration Manager).  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>Contenuto pre-installato  
 È possibile pre-installare il contenuto per aggiungere i file di contenuto alla raccolta contenuto in un server del sito o in un punto di distribuzione prima di distribuire il contenuto  

-   Poiché i file di contenuto si trovano già nella raccolta contenuto, quando si distribuisce il contenuto questi file non vengono trasferiti in rete  

-   È possibile pre-installare i file di contenuto per applicazioni e pacchetti  

Nella console di Configuration Manager si seleziona il contenuto che si desidera pre-installare, quindi si usa la **Creazione guidata file di contenuto pre-installazione** per creare un file di contenuto pre-installato compresso che contiene i file e i metadati associati per il contenuto. Quindi, è possibile importare manualmente il contenuto in un server del sito o in punto di distribuzione.  

-   Quando si importa il file di contenuti in versione di preproduzione in un server del sito, i file di contenuto vengono aggiunti alla raccolta contenuto nel server del sito e quindi registrati nel database del server del sito  

-   Quando si importa il file di contenuti in versione di preproduzione in un punto di distribuzione, i file di contenuto vengono aggiunti alla raccolta contenuto nel punto di distribuzione e un messaggio di stato viene inviato al server del sito che informa il sito che il contenuto è disponibile nel punto di distribuzione  

Facoltativamente, è possibile configurare il punto di distribuzione come **pre-installato** per la gestione della distribuzione del contenuto. Quindi, quando si distribuisce il contenuto è possibile scegliere se:  

-   Pre-installare sempre il contenuto nel punto di distribuzione  

-   Pre-installare il contenuto iniziale per il pacchetto e quindi usare il processo di distribuzione del contenuto standard quando sono disponibili aggiornamenti al contenuto  

-   Usare sempre il processo di distribuzione del contenuto standard per il contenuto nel pacchetto  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Determinare se pre-installare il contenuto  
 Prendere in considerazione la pre-installazione di contenuto per applicazioni e pacchetti nei seguenti scenari:  

-   **Larghezza di banda di rete limitata dal server del sito al punto di distribuzione**: Quando la pianificazione e la limitazione non risolvono eventuali problematiche di distribuzione del contenuto sulla rete in un punto di distribuzione remoto, prendere in considerazione la pre-installazione del contenuto nel punto di distribuzione. Ciascun punto di distribuzione dispone dell'impostazione **Abilita questo punto di distribuzione per il contenuto pre-installato** che è possibile configurare nelle proprietà del punto di distribuzione. Quando si abilita questa opzione, il punto di distribuzione viene individuato come punto di distribuzione pre-installato ed è possibile scegliere come gestire il contenuto in base al pacchetto.  

     Le impostazioni seguenti sono disponibili nelle proprietà di un'applicazione, pacchetto, pacchetto driver, immagine di avvio, programma di installazione del sistema operativo e immagine e consentono all'utente di configurare le modalità in cui viene gestita la distribuzione del contenuto nei punti di distribuzione remoti individuati come pre-installati:  

    -   **Scarica automaticamente il contenuto quando i pacchetti sono assegnati ai punti di distribuzione**: usare questa opzione se si dispongono di pacchetti più piccoli, dove le impostazioni di pianificazione e limitazione forniscono sufficiente controllo per la distribuzione del contenuto.  

    -   **Scarica solo le modifiche di contenuto nel punto di distribuzione**: usare questa opzione se si ha un pacchetto iniziale, anche grande, ma si prevede che i futuri aggiornamenti al contenuto del pacchetto siano generalmente di dimensioni ridotte. Ad esempio, è possibile pre-installare un'applicazione come Microsoft Office, perché la dimensione del pacchetto iniziale è superiore a 700 MB e quindi troppo grande da inviare in rete. Tuttavia, gli aggiornamenti del contenuto di questo pacchetto possono essere inferiori a 10 MB e quindi accettabili per la distribuzione in rete. Un altro esempio potrebbe essere costituito da pacchetti driver in cui la dimensione del pacchetto iniziale è grande, ma le aggiunte driver incrementali per il pacchetto potrebbero essere ridotte.  

    -   **Copia manualmente il contenuto del pacchetto nel punto di distribuzione**: Usare questa opzione quando si dispone di pacchetti di grandi dimensioni, ad esempio un sistema operativo, e non si vuole mai usare la rete per distribuire il contenuto al punto di distribuzione. Quando si seleziona questa opzione, è necessario pre-installare il contenuto nel punto di distribuzione.  

    > [!WARNING]  
    >  Le opzioni precedenti sono applicabili in base al pacchetto e vengono usate solo quando un punto di distribuzione è identificato come pre-installato. I punti di distribuzione che non sono stati identificati come pre-installati ignorano queste impostazioni. In questo caso, il contenuto sempre viene distribuito in rete dal server del sito ai punti di distribuzione.  

-   **Ripristinare la raccolta contenuto in un server del sito**: quando un server del sito restituisce un errore, le informazioni sui pacchetti e le applicazioni contenute nella raccolta contenuto vengono ripristinate nel database del sito come parte del processo di ripristino, ma i file della raccolta contenuto non vengono ripristinati come parte del processo. Se non si dispone di un backup del file system per ripristinare la raccolta contenuto, è possibile creare un file di contenuto pre-installato da un altro sito che contiene i pacchetti e le applicazioni che occorrono e quindi estrarre il file di contenuto pre-installato sul server del sito ripristinato. Per altre informazioni sul backup e il ripristino del server del sito, vedere [Backup e ripristino per System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery)  



<!--HONumber=Dec16_HO3-->


