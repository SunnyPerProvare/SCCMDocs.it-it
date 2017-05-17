---
title: Domande frequenti sui dati di diagnostica | Microsoft Docs
description: Sono disponibili le domande frequenti sui dati di diagnostica e di utilizzo per System Center Configuration Manager.
ms.custom: na
ms.date: 2/8/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 6cf291d79c1c5d9540f809fcb00e7ab48e0c3d3b
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Domande frequenti sui dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Di seguito sono riportate le domande poste più di frequente sui dati di diagnostica e di utilizzo per System Center Configuration Manager:  

###  <a name="bkmk_off"></a> Come si può disattivare la telemetria?  
La telemetria non può essere disattivata. È comunque possibile scegliere il livello di dati di telemetria raccolti. È inoltre possibile usare un punto di connessione del servizio in modalità offline per gestire gli orari di invio dei dati di telemetria.

Configuration Manager Current Branch deve essere aggiornato a intervalli regolari per supportare le nuove versioni di Windows 10 e Microsoft Intune. Microsoft richiede almeno il livello base dei dati di diagnostica e utilizzo per mantenere aggiornato il prodotto, migliorare l'esperienza di aggiornamento e aumentare la qualità e la sicurezza del prodotto.

###  <a name="bkmk_retention"></a> Qual è il periodo di conservazione dei dati?  
 I dati di diagnostica e utilizzo vengono conservati per un anno.  

###  <a name="bkmk_update"></a> I dati di diagnostica e utilizzo vengono inviati durante l'installazione o l'aggiornamento del prodotto?  
 No. I dati di diagnostica e di utilizzo vengono inviati solo dopo che il sito è installato e funzionante.  

###  <a name="bkmk_frequency"></a> Con quale frequenza vengono inviati i dati?  
 Le stored procedure SQL vengono eseguite ogni sette giorni (dalla data di installazione del sito). In modalità online, il punto di connessione del servizio viene configurato in modo da caricare i dati dopo l'esecuzione di query. In modalità offline, l'amministratore usa lo strumento di connessione del servizio per caricare i dati. Si tenga presente che i dati non sono disponibili per l'uso offline fino a sette giorni dopo l'installazione del sito.  

###  <a name="bkmk_network"></a> È possibile usare i dati per formare una mappa di rete?  
 Come illustrato nella descrizione dei livelli di raccolta dei dati di diagnostica e utilizzo per System Center Configuration Manager, i dettagli includono informazioni sul fuso orario provenienti da ciascun sito. Queste informazioni possono fornire indicazioni riguardo la georilevazione generale e la dispersione globale dei siti in una gerarchia. Non viene tuttavia raccolto alcun dettaglio relativo alla rete, ad esempio indirizzi IP o informazioni geografiche più dettagliate.
 - [Dati di diagnostica per la versione 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Dati di diagnostica per la versione 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Dati di diagnostica per 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Dati di diagnostica per 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> È possibile visualizzare i dati in tabelle personalizzate?  
 No. I dati di diagnostica e di utilizzo vengono raccolti con le stored procedure SQL per le tabelle di prodotti predefinite nel database (tutte precedute da **TEL_**). Come parte della query di rilevamento dello schema SQL, viene eseguito l'hashing di tutti i nomi di tabella per il confronto con i valori predefiniti noti. Questo può determinare l'esistenza di tabelle personalizzate nel database (lo schema di database viene esteso dall'impostazione predefinita), ma non dei dati contenuti all'interno di tali tabelle.  

###  <a name="bkmk_databases"></a> È possibile visualizzare nomi o dati di altri database?  
 No. Le stored procedure per raccogliere i dati sono limitate al database del sito.  

## <a name="see-also"></a>Vedere anche  
 [Diagnostica e dati di utilizzo per System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

