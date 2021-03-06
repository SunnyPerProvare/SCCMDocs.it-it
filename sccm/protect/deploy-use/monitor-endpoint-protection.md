---
title: Monitorare lo stato di Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come monitorare Endpoint Protection nella gerarchia di Configuration Manager.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c1890eb3cb6f201483c21ad4da85b83658d3081f
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75819506"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Come monitorare lo stato di Endpoint Protection

*Si applica a: Configuration Manager (Current Branch)*

È possibile monitorare Endpoint Protection nella gerarchia di Microsoft Configuration Manager usando il nodo **Stato Endpoint Protection** di **Sicurezza** nell'area di lavoro **Monitoraggio**, il nodo **Endpoint Protection** nell'area di lavoro **Asset e conformità** e usando i report.  

##  <a name="BKMK_1"></a> Come monitorare Endpoint Protection usando il nodo Stato Endpoint Protection  

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2. Nell'area di lavoro **Monitoraggio** espandere **Sicurezza** e quindi fare clic su **Stato Endpoint Protection**.  

3. Nel **raccolta** selezionare la raccolta per cui si desidera visualizzare informazioni sullo stato.  

   > [!IMPORTANT]
   >  Gli insiemi sono disponibili per la selezione nei seguenti casi:  
   > 
   > - Quando si seleziona **Visualizza questa raccolta nel dashboard di Endpoint Protection** nella scheda **Avvisi** della finestra di dialogo <em><nome raccolta\></em>**Proprietà**.  
   >   -   Quando si distribuisce un criterio antimalware Endpoint Protection nella raccolta.  
   >   -   Quando si abilitano e si distribuiscono le impostazioni client di Endpoint Protection nella raccolta.  

4. Esaminare le informazioni visualizzate nel **dello stato di protezione** e **stato operativo** sezioni. È possibile fare clic sui collegamenti di stato per creare una raccolta temporanea nel **dispositivi** nodo il **asset e conformità** area di lavoro. La raccolta temporanea contiene i computer con lo stato selezionato.  

   > [!IMPORTANT]  
   >  Le informazioni visualizzate nel nodo **Stato Endpoint Protection** sono basate sugli ultimi dati riepilogati dal database di Configuration Manager e potrebbero non essere aggiornate. Se si vogliono recuperare i dati più recenti, nella scheda **Home** fare clic su **Esegui riepilogo**oppure fare clic su **Pianifica riepilogo** per regolare l'intervallo di esecuzione del riepilogo.  

##  <a name="BKMK_2"></a> Come monitorare Endpoint Protection nell'area di lavoro Asset e conformità  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nel **asset e conformità** area di lavoro, effettuare una delle seguenti operazioni:  

    -   Fare clic su **dispositivi**. Nel **dispositivi** elenco, selezionare un computer e quindi scegliere il **dettaglio Malware** scheda.  

    -   Fare clic su **raccolte dispositivi**. Nell'elenco **Raccolte dispositivi** selezionare la raccolta che contiene il computer che si vuole monitorare e quindi fare clic su **Home** nel gruppo **Raccolta** della scheda **Home**.  

3.  Nell'elenco *<nome raccolta\>* selezionare un computer e quindi fare clic sulla scheda **Dettagli malware**.  

##  <a name="BKMK_3"></a> Come monitorare Endpoint Protection usando i report  
 Usare i report seguenti per visualizzare le informazioni su Endpoint Protection nella gerarchia. È anche possibile usare questi report per risolvere eventuali problemi di Endpoint Protection. Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Creazione di report](../../core/servers/manage/reporting.md) e [File di log](../../core/plan-design/hierarchy/log-files.md). I report di Endpoint Protection sono nella cartella di Endpoint Protection.  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|**Report attività antimalware**|Consente di visualizzare una panoramica delle attività antimalware per una raccolta specificata.|  
|**Computer infetti**|Consente di visualizzare un elenco dei computer in cui viene rilevata una minaccia specificata.|  
|**Principali utenti da minacce**|Visualizza un elenco di utenti con il maggior numero di minacce rilevate.|  
|**Elenco di minacce utente**|Consente di visualizzare un elenco delle minacce che sono stati rilevati per un account utente specificato.|  

## <a name="malware-alert-levels"></a>Livelli di avviso di malware  
 Usare la tabella seguente per identificare i diversi livelli di avviso di Endpoint Protection che potrebbero essere visualizzati nei report o nella console di Configuration Manager.  

|Livello di avviso|Descrizione|  
|-----------------|-----------------|  
|**Operazione non riuscita**|Endpoint Protection non è riuscito a correggere il malware. Controllare i registri per i dettagli dell'errore.<br /><br /> **Nota:** Per un elenco dei file di log Configuration Manager e Endpoint Protection, vedere la sezione "Endpoint Protection" nell'argomento [file di log](../../core/plan-design/hierarchy/log-files.md) .|  
|**Rimosso**|Endpoint Protection ha rimosso il malware.|  
|**In quarantena**|Endpoint Protection ha spostato il malware in una posizione sicura e ne ha impedito l'esecuzione fino a quando l'utente non l'ha rimosso o ne ha consentito l'esecuzione.|  
|**Pulito**|Il malware è stato eliminato dal file infetto.|  
|**È consentito**|Un utente amministratore selezionato per consentire al software che contiene l'esecuzione di malware.|  
|**Nessuna azione**|Endpoint Protection non ha eseguito alcuna azione sul malware. Ciò può verificarsi se il computer viene riavviato dopo che viene rilevato software dannoso e il malware non viene rilevato; ad esempio, se una rete connessa unità in cui malware viene rilevato non è riconnesse al riavvio del computer.|  
|**Bloccato**|Endpoint Protection ha bloccato l'esecuzione del malware. Ciò può verificarsi se viene rilevato un processo nel computer che contengono malware.|
