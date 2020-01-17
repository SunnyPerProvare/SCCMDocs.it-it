---
title: Domande frequenti sui dati di diagnostica e di utilizzo
titleSuffix: Configuration Manager
description: Sono disponibili le domande frequenti sui dati di diagnostica e di utilizzo per Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8180b1eee08f3e0ba0ef58fdd18138d4e1b7ca6d
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75792179"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-configuration-manager"></a>Domande frequenti sui dati di diagnostica e di utilizzo per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo fornisce le risposte alle domande frequenti sui dati di diagnostica e di utilizzo in Configuration Manager.

## <a name="faqs"></a>Domande frequenti

###  <a name="bkmk_off"></a> Come si può disattivare la telemetria?  
La telemetria non può essere disattivata. È comunque possibile scegliere il livello di dati di telemetria raccolti. Per gestire gli orari di invio dei dati di telemetria, usare il punto di connessione del servizio in modalità offline.

Configuration Manager Current Branch deve essere aggiornato a intervalli regolari per supportare le nuove versioni di Windows 10 e Microsoft Intune. Microsoft richiede almeno il livello base dei dati di diagnostica e di utilizzo. Questi dati vengono usati per mantenere aggiornato il prodotto, migliorare l'esperienza di aggiornamento e aumentare la qualità e la sicurezza del prodotto.

###  <a name="bkmk_retention"></a> Qual è il periodo di conservazione dei dati?  
 I dati di diagnostica e di utilizzo vengono archiviati per un anno.  

###  <a name="bkmk_update"></a> I dati di diagnostica e utilizzo vengono inviati durante l'installazione o l'aggiornamento del prodotto?  
 No. I dati di diagnostica e di utilizzo vengono inviati solo dopo che il sito è installato e funzionante.  

###  <a name="bkmk_frequency"></a> Con quale frequenza vengono inviati i dati?  
 Le stored procedure SQL vengono eseguite ogni sette giorni dalla data di installazione del sito. In modalità online, il punto di connessione del servizio viene configurato in modo da caricare i dati dopo l'esecuzione di query. In modalità offline, l'amministratore usa lo strumento di connessione del servizio per caricare i dati. I dati non sono inizialmente disponibili per l'uso offline fino a sette giorni dopo l'installazione del sito.  

###  <a name="bkmk_network"></a> È possibile usare i dati per formare una mappa di rete?  
 Come illustrato nella descrizione dei livelli dei dati di diagnostica e di utilizzo, i dettagli del sito includono informazioni sul fuso orario provenienti da ciascun sito. Queste informazioni possono fornire indicazioni riguardo la georilevazione generale e la dispersione globale dei siti in una gerarchia. Tali dati non includono dettagli relativi alla rete, ad esempio indirizzi IP o informazioni geografiche più dettagliate. Per altre informazioni, vedere l'elenco degli [articoli sui dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles) e individuare i livelli di raccolta dei dati di diagnostica e di utilizzo per la versione in uso.


###  <a name="bkmk_tables"></a> È possibile visualizzare i dati in tabelle personalizzate?  
 No. Configuration Manager raccoglie i dati di diagnostica e di utilizzo tramite stored procedure SQL che vengono eseguite per tabelle di prodotti predefinite nel database. Tutte queste tabelle SQL sono precedute dal prefisso **TEL_** . Come parte della query di rilevamento dello schema SQL, viene eseguito l'hashing di tutti i nomi di tabella per il confronto con i valori predefiniti noti. Questo comportamento determina l'esistenza di tabelle personalizzate nel database. La presenza di tabelle personalizzate indica che lo schema di database viene esteso dall'impostazione predefinita. Non include i dati archiviati all'interno di tali tabelle.  

###  <a name="bkmk_databases"></a> È possibile visualizzare nomi o dati di altri database? 
 No. Le stored procedure per raccogliere i dati sono limitate al database del sito.  

### <a name="bkmk_gdpr"></a> Configuration Manager è soggetto al Regolamento generale sulla protezione dei dati (GDPR)?
 No. Configuration Manager non è soggetto alla supervisione del GDPR. È un prodotto locale distribuibile, gestibili e utilizzabile direttamente. I dati di diagnostica e di utilizzo che Microsoft raccoglie migliorano l'esperienza, la qualità e la sicurezza di installazione delle versioni future. Questi dati di diagnostica e di utilizzo sono soggetti a supervisione GDPR. Tuttavia, nessuna informazione di identificazione dell'utente finale (EUII) o identificatore di pseudonimo dell'utente finale (EUPI) viene raccolto e trasmesso a Microsoft. Per altre informazioni sul Regolamento generale sulla protezione dei dati, vedere il [Microsoft Trust Center sul GDPR](https://microsoft.com/gdpr). Per altre informazioni sui dati di Configuration Manager, vedere [Dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Vedere anche  
 [Diagnostica e dati di utilizzo](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
