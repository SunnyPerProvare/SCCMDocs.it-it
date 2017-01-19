---
title: Raccolta contenuto | Microsoft Docs
description: Informazioni sulla raccolta contenuto che System Center Configuration Manager usa per ridurre le dimensioni totali del contenuto distribuito.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 8bdb4e4209ea557afa9d8140d54e98637e560944

---
# <a name="the-content-library-in-system-center-configuration-manager"></a>Raccolta contenuto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La raccolta contenuto è un Single Instance Store del contenuto che Configuration Manager usa per ridurre le dimensioni complessive del corpo combinato di contenuto distribuito. La raccolta contenuto memorizza tutti i file di contenuto per la distribuzione di aggiornamenti software, applicazioni, sistemi operativi e così via.

 - Una copia della raccolta contenuto viene creata e gestita automaticamente in ogni **server del sito** e in ogni **punto di distribuzione**
 - Prima di scaricare i file di contenuto nel server del sito o di copiare i file nei punti di distribuzione, Configuration Manager verifica se ogni file di contenuto si trova già nella raccolta contenuto.
 - Se il file di contenuto è disponibile, Configuration Manager non copia il file, ma associa il file di contenuto esistente all'applicazione o al pacchetto

Nei computer in cui si installa un punto di distribuzione è possibile configurare:
- Una o più unità disco in cui creare la raccolta contenuto
- Una priorità per ogni unità usata

Configuration Manager copia i file di contenuto nell'unità disco con la priorità massima fino a quando lo spazio disponibile sul disco è inferiore al valore specificato.
- Le impostazioni dell'unità vengono configurate durante l'installazione del punto di distribuzione
- Al termine dell'installazione non è possibile configurare le impostazioni dell'unità nelle proprietà del punto di distribuzione


Per informazioni su come configurare le impostazioni dell'unità per il punto di distribuzione, vedere [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager).  


>  [!IMPORTANT]  
>  Per spostare la raccolta contenuto in un percorso diverso di un punto di distribuzione dopo l'installazione, usare lo **strumento per il trasferimento di raccolte contenuto** in System Center 2012 R2 Configuration Manager Toolkit. Il toolkit è disponibile per il download dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>Informazioni sulla raccolta contenuto nel sito di amministrazione centrale  
 Per impostazione predefinita, Configuration Manager crea una raccolta contenuto nel sito di amministrazione centrale quando viene installato il sito. La raccolta contenuto viene collocata nell'unità del server del sito che dispone della maggior parte di spazio libero su disco. Poiché non è possibile installare un punto di distribuzione nel sito di amministrazione centrale, è impossibile assegnare la priorità alle unità per l'utilizzo della raccolta contenuto. In modo simile alla raccolta contenuto sugli altri server del sito e sui punti di distribuzione, quando l'unità che contiene la raccolta contenuto esaurisce lo spazio su disco disponibile, la raccolta contenuto si espande automaticamente sull'unità successiva disponibile.  

 Configuration Manager usa la raccolta contenuto nel sito di amministrazione centrale negli scenari seguenti:  

-   Quando si crea contenuto nel sito di amministrazione centrale.  

-   Quando si esegue la migrazione del contenuto da un altro sito di Configuration Manager e si assegna il sito di amministrazione centrale come sito che si occuperà della gestione del contenuto.  

> [!NOTE]  
>  Quando si crea contenuto su un sito primario e lo si distribuisce in un sito primario diverso o in un sito secondario di un sito primario diverso, il sito di amministrazione centrale memorizza temporaneamente quel contenuto nella posta in arrivo dell'Utilità di pianificazione del sito di amministrazione centrale, ma non lo aggiunge alla sua raccolta contenuto.  

 Utilizzare le seguenti opzioni per gestire la raccolta contenuto nel sito di amministrazione centrale:  

-   Per evitare l'installazione della raccolta contenuto su un'unità specifica, creare un file vuoto denominato **no_sms_on_drive.sms** e copiarlo nella cartella radice dell'unità prima che venga creata la raccolta contenuto.  

-   Dopo aver creato la raccolta contenuto, usare lo **strumento per il trasferimento di raccolte contenuto** in System Center 2012 R2 Configuration Manager Toolkit per gestire il percorso della raccolta contenuto. Il toolkit è disponibile per il download dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  



<!--HONumber=Dec16_HO3-->


