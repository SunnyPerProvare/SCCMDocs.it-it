---
title: Punto di distribuzione pull
titleSuffix: Configuration Manager
description: Informazioni sulle configurazioni e le limitazioni per l'uso di un punto di distribuzione pull con System Center Configuration Manager.
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f0feba771dcc75d84cd1233fea562472ff6c1158
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Usare un punto di distribuzione pull basato sul cloud con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Un punto di distribuzione pull per System Center Configuration Manager è un punto di distribuzione standard che consente di ottenere il contenuto distribuito scaricandolo da una posizione di origine, ad esempio un client, anziché eseguire il push del contenuto nella posizione dal server del sito.  

 Quando si distribuisce contenuto in un ampio numero di punti di distribuzione in un sito, i punti di distribuzione pull possono ridurre il carico di elaborazione sul server del sito e velocizzare il trasferimento del contenuto a ciascun punto di distribuzione. Questa efficienza viene ottenuta ripartendo il carico del processo di trasferimento del contenuto a ogni punto di distribuzione dal processo di gestione della distribuzione al server del sito.  

-   È possibile configurare singoli punti di distribuzione come punti di distribuzione pull.  

-   Per ogni punto di distribuzione pull è necessario specificare uno o più punti di distribuzione di origine da cui ottenere le distribuzioni (un punto di distribuzione pull può ricevere contenuto solo da un punto di distribuzione specificato come punto di distribuzione di origine).  

-   Quando si distribuisce contenuto in un punto di distribuzione pull, il server del sito invia una notifica al punto di distribuzione pull che quindi avvia il download (trasferimento) del contenuto da un punto di distribuzione di origine. Un punto di distribuzione pull gestisce individualmente il trasferimento del contenuto, scaricandolo da un altro punto di distribuzione che contiene già una copia del contenuto.  

I punti di distribuzione pull supportano le stesse configurazioni e funzionalità dei normali punti di distribuzione di Configuration Manager. Ad esempio, un punto di distribuzione configurato come un punto di distribuzione pull supporta l'utilizzo di configurazioni multicast e PXE, convalida contenuto e distribuzione di contenuto su richiesta. Un punto di distribuzione pull supporta comunicazioni HTTP o HTTPS da client, supporta le stesse opzioni relative ai certificati di altri punti di distribuzione e può essere gestito individualmente o come un membro di un gruppo di punti di distribuzione.  

> [!IMPORTANT]
> Anche se un punto di distribuzione pull supporta le comunicazioni su HTTP e HTTPS, quando si usa Configuration Manager è possibile specificare solo punti di distribuzione di origine configurati per HTTP. È possibile usare Configuration Manager SDK per specificare un punto di distribuzione di origine configurato per HTTPS.  

 **La sequenza di eventi seguente si verifica durante la distribuzione del contenuto a un punto di distribuzione pull:**  

-   Non appena si distribuisce contenuto a un punto di distribuzione pull, sul server del sito, Package Transfer Manager esegue la verifica del database del sito per confermare se il contenuto è disponibile in un punto di distribuzione di origine. Se questa conferma non è possibile, il controllo viene ripetuto ogni 20 minuti finché il contenuto non diventa disponibile.  

-   Quando il Package Transfer Manager conferma la disponibilità del contenuto, viene inviata una notifica al punto di distribuzione pull con la richiesta di scaricare il contenuto. Quando riceve questa notifica, il punto di distribuzione pull tenta di scaricare il contenuto dai relativi punti di distribuzione di origine.  

-   Al termine del download del contenuto, lo stato del punto di distribuzione pull viene inviato a un punto di gestione. Se però dopo 60 minuti questo stato non viene ricevuto, viene riattivato Package Transfer Manager e viene eseguita una verifica sul punto di distribuzione pull per controllare che il contenuto sia stato scaricato. Se il download del contenuto è in corso, Package Transfer Manager rimane inattivo per 60 minuti prima di eseguire nuovamente una verifica con il punto di distribuzione pull. Questo ciclo continua fino a quando il punto di distribuzione pull non ha completato il trasferimento del contenuto.  

**È possibile configurare un punto di distribuzione pull** quando si installa il punto di distribuzione o dopo averlo installato modificando le proprietà del ruolo del sistema del sito del punto di distribuzione.  

**È possibile rimuovere la configurazione come punto di distribuzione pull** modificando le proprietà del punto di distribuzione. Quando si rimuove la configurazione del punto di distribuzione pull, il punto di distribuzione torna al normale funzionamento e i successivi trasferimenti di contenuto al punto di distribuzione vengono gestiti dal server del sito.  

## <a name="limitations-for-pull-distribution-points"></a>Limitazioni per i punti di distribuzione pull  

-   Il punto di distribuzione basato su cloud non può essere configurato come punto di distribuzione pull.  

-   Un punto di distribuzione in un server del sito non può essere configurato come punto di distribuzione pull.  

-   **La configurazione del contenuto di pre-installazione sostituisce la configurazione del punto di distribuzione pull**. Un punto di distribuzione pull configurato per il contenuto pre-installazione rimane in attesa del contenuto. Non abilita il pull di contenuto dal punto di distribuzione di origine e, analogamente a un punto di distribuzione standard con configurazione contenuto pre-installazione, non riceve contenuto dal server del sito.  

-   **Un punto di distribuzione pull non usa le configurazioni per i limiti di velocità** durante il trasferimento del contenuto. Se si configura un punto di distribuzione installato in precedenza per farlo diventare un punto di distribuzione pull, le configurazioni per i limiti di velocità vengono salvate ma non usate. Se in un secondo momento si rimuove la configurazione del punto di distribuzione pull, vengono implementate le configurazioni del limite di velocità configurate in precedenza.  

    > [!NOTE]  
    >  Se un punto di distribuzione è configurato come un punto di distribuzione pull, la scheda **Limiti di velocità** non è visibile nelle proprietà del punto di distribuzione.  

-   Un punto di distribuzione pull non usa l'opzione **Impostazioni tentativi** per la distribuzione del contenuto. **Impostazioni tentativi** può essere configurata come parte di **Proprietà componente distribuzione software** per ogni sito. Per visualizzare o configurare queste proprietà, nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito**, quindi selezionare **Siti**. Selezionare un sito nel riquadro dei risultati e quindi selezionare **Configura componenti del sito** nella scheda **Home**. Infine selezionare **Distribuzione software**.  

-   Per trasferire contenuto da un punto di distribuzione di origine in una foresta remota, nel computer che ospita il punto di distribuzione pull deve essere installato un client di Configuration Manager. Un account di accesso alla rete che può accedere al punto di distribuzione di origine deve essere configurato per l'utilizzo.  

-   In un computer configurato come un punto di distribuzione pull e che esegue un client di Configuration Manager la versione del client deve essere identica a quella del sito di Configuration Manager che installa il punto di distribuzione pull. Di conseguenza, è necessario usare il componente CCMFramework comune al punto di distribuzione pull e al client di Configuration Manager.  

## <a name="about-source-distribution-points"></a>Informazioni sui punti di distribuzione di origine  
 Quando si configura il punto di distribuzione pull, è necessario specificare uno o più punti di distribuzione di origine:  

-   Vengono visualizzati solo i punti di distribuzione che sono qualificati come punti di distribuzione di origine.  

-   Un punto di distribuzione pull può essere specificato come un punto di distribuzione di origine per un altro punto di distribuzione pull.  

-   Quando si usa la console di Configuration Manager, solo i punti di distribuzione che supportano HTTP possono essere specificati come punti di distribuzione di origine.  

-   È possibile usare Configuration Manager SDK per specificare un punto di distribuzione di origine configurato per HTTPS. Per usare un punto di distribuzione di origine configurato per HTTPS, il percorso del punto di distribuzione pull deve essere condiviso in un computer che esegue il client di Configuration Manager.  

È possibile assegnare una priorità a ogni punto di distribuzione in un elenco di punti di distribuzione di origine con punti di distribuzione pull:  

-   È possibile assegnare una priorità separata per ogni punto di distribuzione di origine o assegnare la stessa priorità a più punti di distribuzione di origine.  

-   La priorità determina l'ordine secondo cui il punto di distribuzione pull richiede contenuto dai relativi punti di distribuzione di origine.  

-   Inizialmente viene contattato il punto di distribuzione di origine con il valore di priorità più basso.  Se esistono più punti di distribuzione di origine con la stessa priorità, viene selezionato in modo non deterministico uno dei punti di distribuzione di origine che condividono tale priorità.  

-   Se il contenuto non è disponibile nell'origine selezionata, il punto di distribuzione pull prova a scaricare il contenuto da un altro punto di distribuzione con la stessa priorità.  

-   Se nessuno dei punti di distribuzione con una priorità specifica dispone del contenuto, il punto di distribuzione pull tenta di scaricare il contenuto da un punto di distribuzione a cui è stato assegnato il valore di priorità successivo più alto, finché il contenuto non viene individuato o il punto di distribuzione pull passa in modalità di sospensione per 30 minuti prima di iniziare nuovamente il processo.  

Un punto di distribuzione pull che scarica contenuto da un punto di distribuzione di origine viene conteggiato come un client nella colonna **Client a cui è stato effettuato l'accesso (univoco)** del report **Riepilogo di utilizzo dei punti di distribuzione** .  

 Per impostazione predefinita, un punto di distribuzione pull usa l' **account computer** per trasferire il contenuto da un punto di distribuzione di origine. Tuttavia, quando il punto di distribuzione pull trasferisce il contenuto da un punto di distribuzione di origine ubicato in una foresta remota, usa sempre l'account di accesso alla rete. Questo processo richiede che il client di Configuration Manager sia installato nel computer e che un account di accesso alla rete sia configurato per l'uso e possa accedere al punto di distribuzione di origine.  

## <a name="about-content-transfers"></a>Informazioni sui trasferimenti di contenuto  
 Per gestire il trasferimento del contenuto, i punti di distribuzione pull usano il componente **CCMFramework** del software client di Configuration Manager.  

-   Questo framework viene installato da **Pulldp.msi** quando si configura il punto di distribuzione come punto di distribuzione pull. Non richiede l'installazione del client di Configuration Manager.  

-   Al termine dell'installazione del punto di distribuzione pull, il servizio CCMExec nel computer del punto di distribuzione deve essere operativo per il funzionamento del punto di distribuzione pull.  
<!--sms.503672 -Clarified BITS use-->
-   Quando il punto di distribuzione pull trasferisce il contenuto, il trasferimento viene eseguito tramite il **Servizio trasferimento intelligente in background** (BITS) incluso nel sistema operativo Windows. Un punto di distribuzione pull non richiede l'installazione della funzionalità facoltativa di estensione del server IIS BITS.

-  Il punto di distribuzione pull registra le operazioni all'interno di **datatransferservice.log** e **pulldp.log** nel computer del punto di distribuzione.

## <a name="see-also"></a>Vedere anche  
 [Concetti di base per la gestione dei contenuti in System Center Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
