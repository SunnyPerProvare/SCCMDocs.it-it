---
title: Gestire le query | Microsoft Docs
description: Informazioni su come gestire le query. Include una tabella di riferimento dettagliata.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 738dcf0b52f18b38b732bf8ca5d7a87369b1c468


---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Come gestire le query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni in questo argomento per gestire le query in System Center Configuration Manager.  

 Per informazioni su come creare le query, vedere [Come creare query in Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Come gestire le query  
 Nell'area di lavoro **Monitoraggio** selezionare **Query**, selezionare la query da gestire e quindi selezionare un'attività di gestione.  

 Per altre informazioni sulle attività di gestione che potrebbero richiedere alcune informazioni prima della relativa selezione, usare la seguente tabella.  

|Attività di gestione|Dettagli|Altre informazioni|  
|---------------------|-------------|----------------------|  
|**Esegui**|Esegue la query selezionata e visualizza i risultati nella console di Configuration Manager.|Nessuna informazione aggiuntiva.|  
|**Installa client**|Apre la **procedura guidata di installazione client** che consente di installare il client di Configuration Manager nei computer restituiti dalla query selezionata.<br /><br /> Questa opzione non è disponibile per le query che restituiscono dispositivi mobili, utenti o gruppi di utenti.|Per altre informazioni su come installare i client di Configuration Manager usando push client, vedere [Come distribuire i client nei computer Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Export**|Apre l' **Esportazione guidata oggetti** , che consente di esportare questa query in un file MOF (Managed Object Format) che può quindi essere importato in un altro sito.|Nessuna informazione aggiuntiva.|  
|**Sposta**|Apre la finestra di dialogo **Sposta elementi selezionati** in cui è possibile spostare la query selezionata in una cartella creata in precedenza nel nodo **Query** .|Nessuna informazione aggiuntiva.|  

## <a name="see-also"></a>Vedere anche  
 [Operazioni e manutenzione per le query in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)



<!--HONumber=Dec16_HO3-->


