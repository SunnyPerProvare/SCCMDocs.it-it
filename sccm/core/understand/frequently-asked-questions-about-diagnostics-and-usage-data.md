---
title: Domande frequenti sui dati di diagnostica | Microsoft Docs
description: Sono disponibili le domande frequenti sui dati di diagnostica e di utilizzo per System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4a8d98addcd463eb82d8b7100b44254a10d21992
ms.openlocfilehash: 7d252fbbdc23ff676b87643408caf977f5636b67


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Domande frequenti sui dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Di seguito sono riportate le domande poste più di frequente sui dati di diagnostica e di utilizzo per System Center Configuration Manager:  

###  <a name="a-namebkmkoffa-how-do-i-turn-off-telemetry"></a><a name="bkmk_off"></a> Come si può disattivare la telemetria?  
La disattivazione della telemetria non è supportata. È comunque possibile scegliere il livello di dati di telemetria raccolti e usare un punto di connessione del servizio in modalità offline per gestire quando vengono inviati i dati di telemetria.

Il ramo corrente di Configuration Manager deve essere aggiornato a intervalli regolari per supportare le nuove versioni di Windows 10 e Microsoft Intune. Microsoft richiede come minimo il livello di base per i dati di diagnostica e utilizzo per mantenere aggiornato il prodotto, migliorare l'esperienza di aggiornamento e migliorare qualità e sicurezza del prodotto.

###  <a name="a-namebkmkretentiona-what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Qual è il periodo di conservazione dei dati?  
 I dati di diagnostica e utilizzo vengono conservati per un anno.  

###  <a name="a-namebkmkupdatea-is-diagnostics-and-usage-data-sent-when-installing-or-updating-the-product"></a><a name="bkmk_update"></a> I dati di diagnostica e utilizzo vengono inviati durante l'installazione o l'aggiornamento del prodotto?  
 No. I dati di diagnostica e di utilizzo vengono inviati solo dopo che il sito è installato e funzionante.  

###  <a name="a-namebkmkfrequencya-how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Con quale frequenza vengono inviati i dati?  
 Le stored procedure SQL vengono eseguite ogni sette giorni (dalla data di installazione del sito). In modalità online, il punto di connessione del servizio viene configurato in modo da caricare i dati dopo l'esecuzione di query. In modalità offline, l'amministratore usa lo strumento di connessione del servizio per caricare i dati. Nota: i dati non sono inizialmente disponibili per l'uso offline fino a sette giorni dopo l'installazione del sito.  

###  <a name="a-namebkmknetworka-can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> È possibile usare i dati per formare una mappa di rete?  
 Come illustrato nella descrizione dei livelli di raccolta dati di diagnostica e di utilizzo per System Center Configuration, i dettagli includono informazioni sul fuso orario da ciascun sito. Questo può fornire informazioni approfondite riguardo la georilevazione generale e la dispersione globale dei siti in una gerarchia. Tuttavia, non viene raccolto alcun dettaglio relativo alla rete, ad esempio indirizzi IP o informazioni geografiche più dettagliate.
 - [Dati diagnostici per 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Dati di diagnostica per la versione 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Dati di diagnostica per 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Dati di diagnostica per 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="a-namebkmktablesa-can-you-see-data-in-custom-tables"></a><a name="bkmk_tables"></a> È possibile visualizzare i dati in tabelle personalizzate?  
 No. I dati di diagnostica e di utilizzo vengono raccolti con le stored procedure SQL per le tabelle di prodotti predefinite nel database (tutte precedute da **TEL_**). Come parte della query di rilevamento dello schema SQL, viene eseguito l'hashing di tutti i nomi di tabella per il confronto con i valori predefiniti noti. Questo può determinare l'esistenza di tabelle personalizzate nel database (lo schema di database viene esteso dall'impostazione predefinita), ma non dei dati contenuti all'interno di tali tabelle.  

###  <a name="a-namebkmkdatabasesa-can-you-see-names-of-other-databases-or-data-in-other-databases"></a><a name="bkmk_databases"></a> È possibile visualizzare nomi di altri database o dati in altri database?  
 No. Le stored procedure per raccogliere i dati sono limitate al database del sito.  

## <a name="see-also"></a>Vedere anche  
 [Diagnostica e dati di utilizzo per System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)



<!--HONumber=Dec16_HO5-->


