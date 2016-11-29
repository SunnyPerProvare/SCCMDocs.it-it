---
title: Monitorare il contenuto | System Center Configuration Manager
description: Informazioni su come monitorare il contenuto distribuito usando la console di Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 402c06ed92bbfe509206d3e7800e41e90c5d3a38

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorare il contenuto distribuito con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare la console di System Center Configuration Manager per monitorare il contenuto distribuito che include:  

-   Lo stato di tutti i tipi di pacchetti in relazione ai punti di distribuzione associati  

-   Lo stato di convalida del contenuto per il contenuto in un pacchetto  

-   Lo stato del contenuto assegnato a un gruppo di punti di distribuzione specifico  

-   Lo stato del contenuto assegnato a un punto di distribuzione  

-   Lo stato delle funzionalità facoltative per ogni punto di distribuzione (convalida del contenuto, PXE e multicast).  

> [!NOTE]  
>  Configuration Manager monitora solo il contenuto in un punto di distribuzione nella raccolta contenuto. Il contenuto archiviato nel punto di distribuzione in condivisioni pacchetto o personalizzate non è monitorato.  

##  <a name="a-namebkmkcontentstatusa-content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Monitoraggio dello stato del contenuto  
 Il nodo **Stato componente** dell'area di lavoro **Monitoraggio** fornisce informazioni sui pacchetti contenuto. Nella console di Configuration Manager è possibile esaminare informazioni quali:  

-   Nome del pacchetto  

-   Tipo  

-   Numero di punti di distribuzione a cui è stato inviato un pacchetto  

-   Tasso di conformità  

-   Data di creazione del pacchetto  

-   ID del pacchetto  

-   Versione di origine  

È anche possibile trovare informazioni dettagliate sullo stato di qualsiasi pacchetto nonché lo stato di distribuzione del pacchetto, tra cui:  

-   Numero di errori  

-   distribuzioni in sospeso  

-   Numero di installazioni  

È anche possibile gestire le distribuzioni ancora in corso in un punto di distribuzione o che non sono riuscite a distribuire correttamente il contenuto in un punto di distribuzione:  

-   L'opzione applicabile per annullare o ridistribuire il contenuto è disponibile quando si visualizza il messaggio di stato della distribuzione di un processo di distribuzione a un punto di distribuzione nel riquadro **Dettagli asset** della scheda **In corso** o **Errore** del nodo **Stato contenuto** .  

-   Inoltre, viene visualizzata la percentuale relativa al processo completato quando si visualizzano i dettagli di un processo nella scheda **In corso** e il numero di tentativi rimanenti per un processo e il tempo di attesa prima che possa essere effettuato un altro tentativo quando si visualizzano i dettagli di un processo disponibile nella scheda **Errore** .  

Quando si annulla una distribuzione non ancora completata, il processo di distribuzione per il trasferimento del contenuto viene interrotto:  

-   Lo stato della distribuzione si aggiorna per indicare che la distribuzione non è riuscita ed è stata annullata da un'azione dell'utente.  

-   Questo nuovo stato viene visualizzato nella scheda **Errore** .  

> [!TIP]  
>  A distribuzione quasi completata, è possibile che l'annullamento della distribuzione non venga effettuato prima del completamento di tale operazione al punto di distribuzione. In tal caso, l'annullamento della distribuzione viene ignorato e lo stato indica che la distribuzione è stata eseguita correttamente.  

> [!NOTE]  
>  Sebbene si possa selezionare l'opzione per annullare una distribuzione a un punto di distribuzione che si trova su un server del sito, tale operazione non ha alcun effetto. Ciò si verifica perché il server del sito e il punto di distribuzione su un server del sito condividono lo stesso archivio contenuti a istanza singola e non sono presenti processi di distribuzione da annullare.  

Se il contenuto viene ridistribuito dopo un trasferimento in un punto di distribuzione non riuscito, Configuration Manager inizia subito a ridistribuire il contenuto nel punto di distribuzione aggiornandone lo stato in modo da riflettere lo stato attuale della ridistribuzione.  

Utilizzare le procedure seguenti per visualizzare lo stato del contenuto e gestire distribuzioni ancora in corso o non riuscite.  

#### <a name="to-monitor-content-status"></a>Per monitorare lo stato del contenuto  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto in cui si desiderano le informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate informazioni dettagliate sullo stato per il pacchetto.  

#### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Per annullare una distribuzione ancora in corso  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto che si desidera gestire, quindi nel riquadro dei dettagli fare clic su **Visualizza stato**.  

4.  Nel riquadro **Dettagli asset** della scheda **In corso** , fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione che si desidera annullare e selezionare **Annulla**.  

5.  Fare clic su **Sì** per confermare l'operazione e annullare il processo di distribuzione a un determinato punto di distribuzione.  

#### <a name="to-redistribute-content-that-failed-to-distribute"></a>Per ridistribuire il contenuto dopo una distribuzione non riuscita  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto che si desidera gestire, quindi nel riquadro dei dettagli fare clic su **Visualizza stato**.  

4.  Nel riquadro **Dettagli asset** della scheda **Errore** , fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione che si desidera ridistribuire e selezionare **Ridistribuisci**.  

5.  Fare clic su **Sì** per confermare l'operazione e avviare il processo di ridistribuzione a un determinato punto di distribuzione.  

## <a name="distribution-point-group-status"></a>Stato del gruppo di punti di distribuzione  
Il nodo **Stato gruppo di punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sui gruppi di punti di distribuzione. È possibile esaminare informazioni quali:  

-   Nome del gruppo di punti di distribuzione  

-   Descrizione  

-   Numero di punti di distribuzione membri del gruppo di punti di distribuzione  

-   Numero di pacchetti assegnati al gruppo  

-   Stato del gruppo di punti di distribuzione  

-   Tasso di conformità  

È anche possibile visualizzare informazioni dettagliate sullo stato per gli elementi seguenti:  

-   Errori del gruppo di punti di distribuzione  

-   Numero di distribuzioni in corso  

-   Numero di distribuzioni completate  

#### <a name="to-monitor-distribution-point-group-status"></a>Per monitorare lo stato del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato gruppo di punti di distribuzione**. Vengono visualizzati i gruppi di punti di distribuzione.  

3.  Selezionare il gruppo di punti di distribuzione in cui si desiderano le informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate le informazioni dettagliate sullo stato per il gruppo di punti di distribuzione.  

## <a name="distribution-point-configuration-status"></a>Stato di configurazione dei punti di distribuzione  
 Il nodo **Stato di configurazione dei punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sul punto di distribuzione. È possibile verificare gli attributi che sono abilitati per il punto di distribuzione, come PXE, multicast, convalida del contenuto e lo stato della distribuzione per il punto di distribuzione. È inoltre possibile visualizzare informazioni dettagliate sullo stato per il punto di distribuzione.  

> [!WARNING]  
>  Lo stato di configurazione del punto di distribuzione è relativo alle ultime 24 ore. Se il punto di distribuzione ha un errore e viene ripristinato, lo stato dell'errore potrebbe essere visualizzato fino a 24 ore dopo il ripristino del punto di distribuzione.  

Usare la procedura seguente per visualizzare lo stato di configurazione del punto di distribuzione.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Per monitorare lo stato di configurazione del punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato di configurazione dei punti di distribuzione**. Vengono visualizzati i punti di distribuzione.  

3.  Selezionare il punto di distribuzione in cui si desiderano le informazioni sullo stato del punto di distribuzione.  

4.  Nel riquadro dei risultati fare clic sulla scheda **Dettagli** . Verranno visualizzate le informazioni sullo stato per il punto di distribuzione.  



<!--HONumber=Nov16_HO1-->


