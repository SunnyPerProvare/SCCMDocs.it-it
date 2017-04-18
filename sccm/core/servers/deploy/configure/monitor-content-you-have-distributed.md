---
title: Monitorare il contenuto | Microsoft Docs
description: Informazioni su come monitorare il contenuto distribuito usando la console di Configuration Manager.
ms.custom: na
ms.date: 2/8/2017
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
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: 7496c8bf11d058c94bc36fd28e9557b6470b61f1
ms.lasthandoff: 04/12/2017

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorare il contenuto distribuito con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare la console di System Center Configuration Manager per monitorare il contenuto distribuito, tra cui:  

-   Lo stato di tutti i tipi di pacchetti in relazione ai punti di distribuzione associati.  
-   Lo stato di convalida per il contenuto di un pacchetto.  
-   Lo stato del contenuto assegnato a un gruppo specifico di punti di distribuzione.  
-   Lo stato del contenuto assegnato a un punto di distribuzione.  
-   Lo stato delle funzionalità facoltative per ogni punto di distribuzione (convalida del contenuto, PXE e multicast).  

> [!NOTE]  
>  Configuration Manager monitora solo il contenuto in un punto di distribuzione nella raccolta contenuto. Il contenuto archiviato nel punto di distribuzione in condivisioni pacchetto o personalizzate non è monitorato.  

##  <a name="BKMK_ContentStatus"></a> Monitoraggio dello stato del contenuto  
 Il nodo **Stato componente** dell'area di lavoro **Monitoraggio** fornisce informazioni sui pacchetti contenuto. Nella console di Configuration Manager è possibile esaminare informazioni quali:  

-   Il nome del pacchetto.  
-   Il tipo.  
-   Il numero di punti di distribuzione a cui è stato inviato un pacchetto.  
-   Il tasso di conformità.  
-   La data di creazione del pacchetto.  
-   L'ID del pacchetto.  
-   La versione di origine.  

È anche possibile trovare informazioni dettagliate sullo stato di qualsiasi pacchetto nonché lo stato di distribuzione del pacchetto, tra cui:  

-   Il numero di errori.  
-   Le distribuzioni in sospeso.  
-   Il numero di installazioni.

È anche possibile gestire le distribuzioni di contenuto ancora in corso o non completate correttamente in un punto di distribuzione:  

-   L'opzione per annullare o ridistribuire il contenuto è disponibile quando si visualizza il messaggio di stato di un processo di distribuzione a un punto di distribuzione nel riquadro **Dettagli asset**. Questo riquadro è disponibile nella scheda **In corso** o nella scheda **Errore** del nodo **Stato contenuto**.  
-   Inoltre, nei dettagli di un processo nella scheda **In corso** viene visualizzata la percentuale di completamento del processo, mentre nei dettagli di un processo nella scheda **Errore** vengono visualizzati il numero di tentativi rimanenti per un processo e il tempo di attesa prima che possa essere effettuato un altro tentativo.  

Quando si annulla una distribuzione non ancora completata, il processo di distribuzione per il trasferimento del contenuto viene interrotto:  

-   Lo stato della distribuzione viene aggiornato per indicare che la distribuzione non è riuscita ed è stata annullata da un'azione dell'utente.  
-   Questo nuovo stato viene visualizzato nella scheda **Errore** .  

> [!TIP]  
>  A distribuzione quasi completata, è possibile che l'annullamento della distribuzione non venga effettuato prima del completamento di tale operazione al punto di distribuzione. In tal caso, l'annullamento della distribuzione viene ignorato e lo stato indica che la distribuzione è stata eseguita correttamente.  

> [!NOTE]  
>  Sebbene si possa selezionare l'opzione per annullare una distribuzione a un punto di distribuzione che si trova su un server del sito, tale operazione non ha alcun effetto. Ciò si verifica perché il server del sito e il punto di distribuzione su un server del sito condividono l'archivio di contenuto a istanza singola. Non sono presenti processi di distribuzione da annullare.  

Quando si ridistribuisce il contenuto dopo un trasferimento non riuscito in un punto di distribuzione, Configuration Manager inizia subito a ridistribuire il contenuto nel punto di distribuzione, aggiornandone lo stato in base allo stato attuale di tale ridistribuzione.  

Usare le procedure seguenti per visualizzare lo stato del contenuto e gestire distribuzioni ancora in corso o non riuscite.  

### <a name="to-monitor-content-status"></a>Per monitorare lo stato del contenuto  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto di cui visualizzare informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate informazioni dettagliate sullo stato per il pacchetto.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Per annullare una distribuzione ancora in corso  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto che si desidera gestire, quindi nel riquadro dei dettagli fare clic su **Visualizza stato**.  

4.  Nel riquadro **Dettagli asset** della scheda **In corso** fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione che si vuole annullare e scegliere **Annulla**.  

5.  Fare clic su **Sì** per confermare l'operazione e annullare il processo di distribuzione a un determinato punto di distribuzione.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Per ridistribuire il contenuto dopo una distribuzione non riuscita  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**. Vengono visualizzati i pacchetti.  

3.  Selezionare il pacchetto che si desidera gestire, quindi nel riquadro dei dettagli fare clic su **Visualizza stato**.  

4.  Nel riquadro **Dettagli asset** della scheda **Errore** fare clic con il pulsante destro del mouse sulla voce relativa alla distribuzione che si vuole ripetere e scegliere **Ridistribuisci**.  

5.  Fare clic su **Sì** per confermare l'operazione e avviare il processo di ridistribuzione allo specifico punto di distribuzione.  

## <a name="distribution-point-group-status"></a>Stato del gruppo di punti di distribuzione  
Il nodo **Stato gruppo di punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sui gruppi di punti di distribuzione. È possibile esaminare informazioni quali:  

-   Il nome del gruppo di punti di distribuzione.  
-   La descrizione.  
-   Il numero di punti di distribuzione appartenenti al gruppo.  
-   Il numero di pacchetti assegnati al gruppo.  
-   Lo stato del gruppo di punti di distribuzione.  
-   Il tasso di conformità.  

È anche possibile visualizzare informazioni dettagliate sullo stato per gli elementi seguenti:  

-   Gli errori del gruppo di punti di distribuzione.  
-   Il numero di distribuzioni in corso.
-   Il numero di distribuzioni completate.  

### <a name="to-monitor-distribution-point-group-status"></a>Per monitorare lo stato del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato gruppo di punti di distribuzione**. Vengono visualizzati i gruppi di punti di distribuzione.  

3.  Selezionare il gruppo di punti di distribuzione di cui visualizzare le informazioni dettagliate sullo stato.  

4.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate le informazioni dettagliate sullo stato per il gruppo di punti di distribuzione.  

## <a name="distribution-point-configuration-status"></a>Stato di configurazione dei punti di distribuzione  
 Il nodo **Stato di configurazione dei punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sul punto di distribuzione. È possibile verificare gli attributi che sono abilitati per il punto di distribuzione, come PXE, multicast, convalida del contenuto e lo stato della distribuzione per il punto di distribuzione. È inoltre possibile visualizzare informazioni dettagliate sullo stato per il punto di distribuzione.  

> [!WARNING]  
>  Lo stato di configurazione del punto di distribuzione è relativo alle ultime 24 ore. Se il punto di distribuzione ha un errore e viene ripristinato, lo stato dell'errore potrebbe essere visualizzato fino a 24 ore dopo il ripristino del punto di distribuzione.  

Usare la procedura seguente per visualizzare lo stato di configurazione del punto di distribuzione.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Per monitorare lo stato di configurazione del punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**, quindi fare clic su **Stato di configurazione dei punti di distribuzione**. Vengono visualizzati i punti di distribuzione.  

3.  Selezionare il punto di distribuzione di cui visualizzare le informazioni sullo stato.  

4.  Nel riquadro dei risultati fare clic sulla scheda **Dettagli** . Verranno visualizzate le informazioni sullo stato per il punto di distribuzione.  

## <a name="client-data-sources-dashboard"></a>Dashboard Origini dati del client
A partire dalla versione 1610, è possibile usare il dashboard **Origini dati del client** per informazioni sull'uso di [Peer Cache](/sccm/core/plan-design/hierarchy/client-peer-cache) nell'ambiente. Questo dashboard inizierà a visualizzare i dati dopo che il contenuto è stato scaricato dai client e tale informazione viene segnalata al sito. Questa operazione può richiedere al massimo 24 ore.

> [!TIP]  
> Con la versione 1610, la peer cache e il dashboard Origini dati del client sono funzionalità di versioni non definitive. Per abilitarle, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease). Il dashboard **Origini dati del client** diventerà visibile solo dopo averlo abilitato. Per la visualizzazione dei dati possono essere necessarie fino a 24 ore dopo l'abilitazione. 

Nella console passare a **Monitoraggio** > **Stato distribuzione** > **Origini dati del client**. In questa posizione è possibile selezionare un periodo di tempo da applicare al dashboard. Nella visualizzazione è quindi possibile selezionare il gruppo di limiti o il pacchetto per il quale visualizzare le informazioni. Quando si esaminano le informazioni, passare il puntatore sulla superficie per vedere altri dettagli relativi ai diversi contenuti o origini dei criteri.

Sono incluse le seguenti informazioni:  
- **Client Content Sources** (Origini contenuto client): visualizza l'origine da cui i client hanno ottenuto il contenuto.
- **Distribution points** (Punti di distribuzione): visualizza il numero di punti di distribuzione che fanno parte del gruppo di limiti selezionato.
- **Clients that used a distribution point** (Clienti che hanno usato un punto di distribuzione): questo valore indica quanti client, tra quelli presenti nel gruppo di limiti selezionato, hanno usato un punto di distribuzione per ottenere il contenuto.
- **Peer Cache sources** (Origini peer cache): per il gruppo di limiti selezionato indica quanti origini di peer cache hanno segnalato la cronologia di download.
- **Clients that used a peer** (Clienti che hanno usato un peer): questo valore indica quanti client, tra quelli presenti nel gruppo di limiti selezionato, hanno usato un'origine peer cache per ottenere il contenuto.



È anche possibile usare un nuovo report, **Client Data Sources - Summarization** (Origini dati del client - Riepilogo), per visualizzare un riepilogo delle origini dati del client per ogni gruppo di limiti.

