---
title: Prerequisiti per la creazione di report | Configuration Manager
description: Individuare le diverse dipendenze che influiscono sull'uso della creazione di report in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: 5
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8554221bc3aede86a255b7f0aa45948fe312b43d


---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Prerequisiti per la creazione di report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La creazione di report in System Center Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 Nella seguente tabella vengono elencate le dipendenze esterne per la creazione di report.  

|Prerequisito|Altre informazioni|  
|------------------|----------------------|  
|SQL Server Reporting Services|Prima di poter usare la creazione di report in Configuration Manager, è necessario installare e configurare SQL Server Reporting Services.<br /><br /> Per informazioni sulla pianificazione e la distribuzione di Reporting Services nell'ambiente, vedere la sezione [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) nella documentazione online di SQL Server 2008.|  
|Dipendenze del ruolo del sistema del sito per computer che eseguono il punto di Reporting Services.|[Configurazioni supportate per System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dipendenze interne a Configuration Manager  
 La tabella seguente elenca le dipendenze per la creazione di report in Configuration Manager.  

|Prerequisito|Altre informazioni|  
|------------------|----------------------|  
|Punto di Reporting Services|È necessario configurare il ruolo di sistema del sito del punto di Reporting Services prima di usare la creazione di report in Configuration Manager. Per altre informazioni su come installare e configurare un punto di Reporting Services, vedere [Configurazione della creazione di report in Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versioni di SQL Server supportate per il punto di Reporting Services  
 È possibile installare il database di Reporting Services sia nell'istanza predefinita che in un'istanza denominata di un'installazione di SQL Server a 64 bit. L'istanza di SQL Server può avere un percorso condiviso con il server del sistema del sito oppure risiedere in un computer remoto.  

 Nella seguente tabella vengono elencate le versioni di SQL Server supportate dal punto di Reporting Services.  

|Versione di SQL Server|Punto di Reporting Services|  
|------------------------|------------------------------|  
|SQL Server 2008 SP2 con aggiornamento cumulativo 9 o successivo<br /><br /> Standard<br />Enterprise<br />Datacenter|?|  
|SQL Server 2008 SP3 con aggiornamento cumulativo 4 o successivo<br /><br /> Standard<br />Enterprise<br />Datacenter|?|  
|SQL Server 2008 R2 con SP1 e aggiornamento cumulativo 6 o successivo<br /><br /> Standard<br />Enterprise<br />Datacenter|?|  
|SQL Server 2008 R2 con SP2<br /><br /> Standard<br />Enterprise<br />Datacenter|?|  
|SQL Server Express 2008 R2 con SP1 e aggiornamento cumulativo 4 o successivo|Non supportato|  
|SQL Server Express 2008 R2 con SP2|Non supportato|  
|SQL Server 2012 e con aggiornamento cumulativo 2 o successivo<br /><br /> Standard<br />Enterprise|?|  
|SQL Server 2012 con SP1 e nessun aggiornamento cumulativo<br /><br /> Standard<br />Enterprise|?|  
|SQL Server 2014<br /><br /> Standard<br />Enterprise|?|  

## <a name="next-steps"></a>Passaggi successivi
[Operazioni e manutenzione per la creazione di report](operations-and-maintenance-for-reporting.md)



<!--HONumber=Nov16_HO1-->


