---
title: Monitorare i client - Configuration Manager| Microsoft Docs
description: Informazioni su come monitorare i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: 23
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3743c80b0c2b5142f3a537ba3855ffd14794d42b
ms.openlocfilehash: 85afe010e734d20ae1f1479b3edd166c54cc8fd2
ms.lasthandoff: 01/24/2017


---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Come monitorare i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Dopo aver installato l'applicazione client di System Center Configuration Manager nei computer e dispositivi Windows nel proprio sito, è possibile monitorarne l'integrità e l'attività nella console di Configuration Manager.  

##  <a name="a-namebkmkabouta-about-client-status"></a><a name="bkmk_about"></a> Informazioni sullo stato del client  
 Configuration Manager offre i seguenti tipi di informazioni come stato del client:  

-   **Stato online del client**: a partire dalla versione 1602 di Configuration Manager questo stato indica se il computer è online. Un computer viene considerato online se è connesso al relativo punto di gestione assegnato.  Per indicare che è online, il client invia i messaggi di tipo ping al punto di gestione. Se il punto di gestione non riceve un messaggio per circa 5 minuti, lo stato del client è considerato offline.  

-   **Attività del client**: questo stato indica se il client è stato usato attivamente con Configuration Manager negli ultimi 7 giorni. Se non ha richiesto un aggiornamento dei criteri, inviato un messaggio di tipo heartbeat o inviato l'inventario hardware in 7 giorni, il client viene considerato inattivo.  

-   **Controllo client**: questo stato indica la riuscita della valutazione periodica eseguita dal client di Configuration Manager nel computer.  La valutazione controlla i computer e può correggere alcuni problemi rilevati. Per altre informazioni, vedere [Controlli e correzioni effettuati dal controllo client](#BKMK_ClientHealth).  

     Nei computer che eseguono Windows 7, il controllo dei client viene eseguito come un'attività pianificata. Nei sistemi operativi successivi, il controllo client viene eseguito automaticamente durante la manutenzione di Windows.  

     È possibile configurare la correzione in modo che venga eseguita su computer specifici, ad esempio, un server di rilevanza critica per l'azienda. Inoltre, se sono presenti voci aggiuntive che si vuole valutare, è possibile usare le impostazioni di conformità di Configuration Manager per offrire una soluzione completa per monitorare l'integrità, il funzionamento e la conformità complessivi dei computer dell'organizzazione. Per altre informazioni sulle impostazioni di conformità, vedere [Pianificazione e configurazione delle impostazioni di conformità in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

##  <a name="a-namebkmkindstatusa-monitor-the-status-of-individual-clients"></a><a name="bkmk_indStatus"></a> Monitorare lo stato dei singoli client  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Dispositivi** oppure scegliere una raccolta in **Raccolte dispositivi**.  

     A partire dalla versione 1602 di Configuration Manager, le icone all'inizio di ogni riga indicano lo stato online del dispositivo:  

    |||  
    |-|-|  
    |![icona di stato online per i client](../../../core/clients/manage/media/online-status-icon.png)|Il dispositivo è online.|  
    |![icona di stato offline per i client](../../../core/clients/manage/media/offline-status-icon.png)|Il dispositivo è offline.|  
    |![icona di stato sconosciuto per i client](../../../core/clients/manage/media/unknown-status-icon.png)|Lo stato online è sconosciuto.|  
    |![client non installato](../../../core/clients/manage/media/client-not-installed.png)|Il client non è installato nel dispositivo.|  

2.  Per ottenere uno stato online più dettagliato, aggiungere le informazioni di stato online del client alla visualizzazione del dispositivo facendo clic con il pulsante destro del mouse sull'intestazione di colonna e scegliendo i campi di stato in linea da aggiungere. Le colonne che è possibile aggiungere sono:  

    -   **Stato online dispositivo** indica se il client è attualmente online o offline. (si tratta delle stesse informazioni fornite dalle icone).  

    -   **Ora ultimo stato online** indica quando lo stato online del client è diventato online.  

    -   **Ora ultimo stato offline** indica quando lo stato è diventato offline.  

3.  Fare clic su un singolo client nel riquadro elenco per visualizzare altre informazioni di stato nel riquadro dei dettagli, incluse informazioni sull'attività del client e controlli client.  

##  <a name="a-namebkmkallstatusa-monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> Monitorare lo stato di tutti i client  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio** > **Stato client**. In questa pagina della console è possibile esaminare le statistiche generali per l'attività client e i controlli client nell'intero sito.  È anche possibile modificare l'ambito delle informazioni scegliendo una raccolta diversa.  

2.  Per visualizzare i dettagli delle statistiche, fare clic sul nome delle informazioni restituite, ad esempio **Client attivi che hanno superato il controllo o con nessun risultato**, ed esaminare le informazioni sui singoli client.  

3.  Fare clic su **Attività client** per visualizzare grafici che descrivono l'attività del client nel sito di Configuration Manager.  

4.  Fare clic su **Controllo client** per visualizzare grafici che descrivono lo stato dei controlli client nel sito di Configuration Manager.  

 È possibile configurare degli avvisi per inviare una notifica all'utente quando i client controllano i risultati oppure quando l'attività client cade al di sotto di una percentuale specificata di client in una raccolta oppure quando la correzione non viene eseguita correttamente su una percentuale specifica di client. Per informazioni su come configurare lo stato del client, vedere [Come configurare lo stato del client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

##  <a name="a-namebkmkclienthealtha-checks-and-remediations-made-by-client-check"></a><a name="BKMK_ClientHealth"></a> Controlli e correzioni effettuati dal controllo client  
 I controlli e le correzioni seguenti possono essere eseguiti dal controllo client.  

|Controllo client|Azione di correzione|Altre informazioni|  
|------------------|------------------------|----------------------|  
|Verificare che il controllo client sia stato eseguito di recente|Esecuzione del controllo client|Verifica che il controllo client sia eseguito almeno una volta negli ultimi tre giorni.|  
|Verificare che siano installati i prerequisiti client|Installazione dei prerequisiti client|Verifica che siano installati i prerequisiti client. Legge il file ccmsetup.xml nella cartella di installazione client per individuare i prerequisiti.|  
|Verifica di integrità del repository WMI|Reinstallare il client di Configuration Manager|Verifica che le voci client di Configuration Manager siano presenti in WMI.|  
|Verificare che sia in esecuzione il servizio client|Avvio del servizio client (host agenti di SMS)|Nessuna informazione aggiuntiva|  
|Verifica del sink di evento WMI.|Riavvio del servizio client|Verificare se il relativo sink di evento WMI di Configuration Manager è stato perso|  
|Verificare che sia presente il servizio Strumentazione gestione Windows (WMI)|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il client sia stato installato correttamente|Reinstallazione del client|Nessuna informazione aggiuntiva|  
|Verifica di lettura e scrittura del repository WMI|Reimpostare il repository WMI e reinstallare il client di Configuration Manager|La correzione di questo controllo client viene eseguita solo su computer con Windows Server 2003, Windows XP (64 bit) o versioni precedenti.|  
|Verificare che il tipo di avvio del servizio antimalware sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che sia in esecuzione il servizio antimalware|Avvio del servizio antimalware|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Windows Update sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio client (host agenti SMS) sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che sia in esecuzione il servizio Strumentazione gestione Windows (WMI).|Avvio del servizio Strumentazione gestione Windows|Nessuna informazione aggiuntiva|  
|Verificare che il database Microsoft SQL CE sia integro|Reinstallare il client di Configuration Manager|Nessuna informazione aggiuntiva|  
|Verifica di integrità di Microsoft Policy Platform WMI|Ripristinare Microsoft Policy Platform|Nessuna informazione aggiuntiva|  
|Verificare che il servizio Microsoft Policy Platform esista|Ripristinare Microsoft Policy Platform|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Microsoft Policy Platform sia manuale|Reimpostare il tipo di avvio del servizio su manuale|Nessuna informazione aggiuntiva|  
|Verificare che sia presente il Servizio trasferimento intelligente in background|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del Servizio trasferimento intelligente in background sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio controllo di rete sia manuale|Reimpostare il tipo di avvio del servizio su manuale se installato|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Strumentazione gestione Windows (WMI) sia automatico|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Windows Update nei computer Windows 8 sia automatico o manuale|Reimpostare il tipo di avvio del servizio su manuale|Nessuna informazione aggiuntiva|  
|Verificare che esista il servizio client (Host agenti di SMS).|Nessuna correzione|Nessuna informazione aggiuntiva|  
|Verificare che il tipo di avvio del servizio Controllo remoto di Configuration Manager sia automatico o manuale|Reimpostare il tipo di avvio del servizio su automatico|Nessuna informazione aggiuntiva|  
|Verificare che il servizio Controllo remoto di Configuration Manager sia in esecuzione|Avviare il servizio di controllo remoto|Nessuna informazione aggiuntiva|  
|Verificare che il provider WMI client sia integro|Avviare il servizio Windows Management Instrumentation|La correzione di questo controllo client viene eseguita solo su computer con Windows Server 2003, Windows XP (64 bit) o versioni precedenti.|  
|Verificare che sia in esecuzione il servizio proxy di riattivazione (Proxy di riattivazione di Configuration Manager)|Avviare il servizio Proxy di riattivazione di Configuration Manager|Questa verifica del client viene eseguita solo se l'impostazione **Risparmio energia**: **Abilitare il proxy di riattivazione** del client è impostata su **Sì** nei sistemi operativi client supportati.|  
|Verificare che il tipo di avvio del servizio proxy di riattivazione (Proxy di riattivazione di Configuration Manager) sia automatico|Reimpostare il tipo di avvio del servizio Proxy di riattivazione di Configuration Manager su automatico|Questa verifica del client viene eseguita solo se l'impostazione **Risparmio energia**: **Abilitare il proxy di riattivazione** del client è impostata su **Sì** nei sistemi operativi client supportati.|  

