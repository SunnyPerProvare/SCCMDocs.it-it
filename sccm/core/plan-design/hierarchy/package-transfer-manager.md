---
title: Package Transfer Manager | Microsoft Docs
description: Informazioni su come Package Transfer Manager in System Center Configuration Manager trasferisce il contenuto da un server del sito ai punti di distribuzione remoti.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 6e61c56b9d1111287bf5a9f22832f6b1ca8146b7

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Package Transfer Manager in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In un sito di System Center Configuration Manager, Package Transfer Manager è un componente di SMS_Executive che gestisce il trasferimento di contenuto da un computer del server di sito ai punti di distribuzione remoti in un sito. (Un punto di distribuzione remoto è un punto che non si trova nel computer del server di sito). Package Transfer Manager non supporta le configurazioni impostate dall'amministratore, ma capire il suo funzionamento aiuta a pianificare l'infrastruttura di gestione del contenuto e a risolvere i problemi relativi alla distribuzione del contenuto.


Quando si distribuisce il contenuto a uno o più punti di distribuzione remoti in un sito, **Distribution Manager** crea un processo di trasferimento del contenuto e quindi comunica a Package Transfer Manager nei server del sito primario e secondario di trasferire il contenuto ai punti di distribuzione remoti.

 Package Transfer Manager registra le sue azioni nel file **pkgxfermgr.log** sul server del sito. Il file di log rappresenta l'unica posizione in cui è possibile visualizzare le attività di Package Transfer Manager.  

> [!NOTE]  
>  Nelle versioni precedenti di Configuration Manager, Distribution Manager gestisce il trasferimento del contenuto a un punto di distribuzione remoto. Distribution Manager gestisce inoltre il trasferimento del contenuto tra i siti. Con System Center Configuration Manager, Distribution Manager continua a gestire il trasferimento del contenuto tra due siti. Package Transfer Manager consente a Configuration Manager di ripartire il carico con Distribution Manager relativo alle operazioni necessarie per trasferire il contenuto a un numero maggiore di punti di distribuzione. Rispetto alle versioni del prodotto precedenti, esso consente di migliorare le prestazioni generali della distribuzione del contenuto tra entrambi i siti e ai punti di distribuzione all'interno di un sito.  

 Per trasferire il contenuto a un punto di distribuzione standard, Package Transfer Manager usa le stesse funzionalità di Distribution Manager delle versioni precedenti di Configuration Manager. Vale a dire gestisce attivamente il trasferimento di file a ogni punto di distribuzione remoto. Tuttavia per distribuire il contenuto a un punto di distribuzione pull, Package Transfer Manager comunica al punto di distribuzione pull che il contenuto è disponibile e quindi trasmette il processo di trasferimento del contenuto al punto di distribuzione pull.  

Le informazioni seguenti descrivono come Package Transfer Manager gestisce il trasferimento del contenuto a punti di distribuzione standard e a punti di distribuzione configurati come punti di distribuzione pull:
1.  **L'utente amministrativo distribuisce il contenuto a uno o più punti di distribuzione in un sito**  

    -   **Punto di distribuzione standard:** Distribution Manager crea un processo di trasferimento per il contenuto.  

    -   **Punto di distribuzione pull:** Distribution Manager crea un processo di trasferimento per il contenuto.  

2.  **Distribution Manager esegue i controlli preliminari**  

    -   **Punto di distribuzione standard:** Distribution Manager esegue un controllo di base per verificare che ogni punto di distribuzione sia pronto per ricevere il contenuto. Dopo questa verifica, Distribution Manager comunica a Package Transfer Manager di iniziare il trasferimento del contenuto al punto di distribuzione.  

    -   **Punto di distribuzione pull:** Distribution Manager avvia Package Transfer Manager, il quale comunica al punto di distribuzione pull che è presente un nuovo processo di trasferimento del contenuto per il punto di distribuzione. Distribution Manager non verifica lo stato dei punti di distribuzione remoti che sono punti di distribuzione pull in quanto ogni punto di distribuzione pull gestisce i propri trasferimenti di contenuto.  

3.  **Package Transfer Manager si prepara al trasferimento del contenuto**  

    -   **Punto di distribuzione standard:** Package Transfer Manager esamina l'archivio di contenuto della singola istanza di ogni punto di distribuzione remoto specificato per identificare eventuali file che sono già presenti in quel punto di distribuzione. Quindi Package Transfer Manager esegue la coda per il trasferimento solo di quei file che non sono già presenti.  

        > [!NOTE]  
        >  Quando si usa l'azione **Ridistribuisci** per il contenuto, Package Transfer Manager copia ogni file nella distribuzione al punto di distribuzione anche se i file sono già presenti nel singolo archivio dell'istanza del punto di distribuzione.  

    -   **Punto di distribuzione pull:** per ogni punto di distribuzione pull nella distribuzione, Package Transfer Manager verifica i punti di distribuzione di origine dei punti di distribuzione pull per confermare la disponibilità del contenuto:  

        -   Se il contenuto è disponibile in almeno un punto di distribuzione di origine, Package Transfer Manager invia una notifica a quel punto di distribuzione pull che indica al punto di distribuzione di iniziare il processo di trasferimento del contenuto. La notifica include i nomi e le dimensioni dei file, gli attributi e i valori hash.  

        -   Quando il contenuto non è ancora disponibile, Package Transfer Manager non invia una notifica al punto di distribuzione. Al contrario, ripete la verifica ogni 20 minuti fino a quando il contenuto non è disponibile. Quindi, quando il contenuto è disponibile, Package Transfer Manager invia la notifica a quel punto di distribuzione pull.  

        > [!NOTE]  
        >  Quando si usa l'azione **Ridistribuisci** per il contenuto, il punto di distribuzione pull copia ogni file nella distribuzione al punto di distribuzione, anche se i file sono già presenti nel singolo archivio dell'istanza del punto di distribuzione pull.  

4.  **Il contenuto inizia a essere trasferito**  

    -   **Punto di distribuzione standard:** Package Transfer Manager copia i file in ogni punto di distribuzione remoto. Durante il trasferimento a un punto di distribuzione standard:  

        -   Per impostazione predefinita, Package Transfer Manager può elaborare contemporaneamente tre pacchetti univoci e distribuirli ai cinque punti di distribuzione in parallelo. Queste vengono chiamate **Impostazioni distribuzione simultanea** e sono configurate nella scheda **Generale** delle **Proprietà componente distribuzione software** per ogni sito.  

        -   Package Transfer Manager usa le configurazioni di larghezza di banda di rete e di pianificazione di ogni punto di distribuzione durante il trasferimento del contenuto al punto di distribuzione. Queste impostazioni vengono configurate nelle schede **Pianifica** e **Limiti di velocità** nelle **Proprietà** di ogni punto di distribuzione remoto. Per altre informazioni, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

    -   **Punto di distribuzione pull:** se un punto di distribuzione pull riceve un file di notifica, viene avviato il processo di trasferimento del contenuto. Il processo di trasferimento viene eseguito in modo indipendente in ogni punto di distribuzione pull:  

        -   La distribuzione pull identifica i file nella distribuzione del contenuto che non presenta già nel suo singolo archivio dell'istanza e si prepara per scaricare il contenuto da uno dei suoi punti di distribuzione di origine.  

        -   Successivamente, il punto di distribuzione pull verifica ognuno dei suoi punti di distribuzione di origine, in ordine, fino a che trova un punto di distribuzione di origine con contenuto disponibile. Quando il punto di distribuzione pull identifica un punto di distribuzione di origine con il contenuto, inizia il download di tale contenuto.  

        > [!NOTE]  
        >  Il processo di download del contenuto eseguito dal punto di distribuzione pull è identico a quello usato dai client di Configuration Manager. Per il trasferimento del contenuto mediante il punto di distribuzione pull, non vengono usate né le impostazioni di trasferimento simultanee, né le opzioni di pianificazione e limitazione configurate per i punti di distribuzione standard.  

5.  **Completamento del trasferimento del contenuto**  

    -   **Punto di distribuzione standard:** al termine del trasferimento dei file a ogni punto di distribuzione remoto designato, Package Transfer Manager verifica l'hash del contenuto nel punto di distribuzione e comunica a Distribution Manager che la distribuzione è completa.  

    -   **Punto di distribuzione pull:** dopo il completamento del download del contenuto, il punto di distribuzione pull verifica l'hash del contenuto e invia un messaggio di stato al punto di gestione dei siti per indicare la corretta esecuzione del download. Se, tuttavia, dopo 60 minuti questo stato non viene ricevuto, viene riattivato Package Transfer Manager e viene eseguita una verifica con il punto di distribuzione pull per confermare se il contenuto è stato scaricato. Se il download del contenuto è in corso, Package Transfer Manager rimane inattivo per 60 minuti prima di eseguire nuovamente una verifica con il punto di distribuzione pull. Questo ciclo continua fino a quando il punto di distribuzione pull non ha completato il trasferimento del contenuto.  



<!--HONumber=Dec16_HO3-->


