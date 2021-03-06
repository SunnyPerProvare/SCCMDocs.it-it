---
title: Prerequisiti per la creazione di report
titleSuffix: Configuration Manager
description: Individuare le diverse dipendenze che influiscono sull'uso della creazione di report in Configuration Manager.
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c5850c19da1cbf33a01a38bcc08052bd94d0f8c
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75794495"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Prerequisiti per la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La creazione di report in Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 Nella seguente tabella vengono elencate le dipendenze esterne per la creazione di report.  

|Prerequisito|Altre informazioni|  
|------------------|----------------------|  
|SQL Server Reporting Services|Prima di poter usare la creazione di report in Configuration Manager, è necessario installare e configurare SQL Server Reporting Services.<br /><br /> Per informazioni sulla pianificazione e la distribuzione di Reporting Services nell'ambiente, vedere la sezione [Reporting Services](https://go.microsoft.com/fwlink/p/?LinkId=212032) nella documentazione online di SQL Server 2008.|  
|Dipendenze del ruolo del sistema del sito per computer che eseguono il punto di Reporting Services.|[Configurazioni supportate per Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dipendenze interne a Configuration Manager  
 La tabella seguente elenca le dipendenze per la creazione di report in Configuration Manager.  

|Prerequisito|Altre informazioni|  
|------------------|----------------------|  
|Punto di Reporting Services|È necessario configurare il ruolo di sistema del sito del punto di Reporting Services prima di usare la creazione di report in Configuration Manager. Per altre informazioni su come installare e configurare un punto di Reporting Services, vedere [Configurazione della creazione di report](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versioni di SQL Server supportate per il punto di Reporting Services  
 È possibile installare il database di Reporting Services sia nell'istanza predefinita che in un'istanza denominata di un'installazione di SQL Server a 64 bit. L'istanza di SQL Server può avere un percorso condiviso con il server del sistema del sito oppure risiedere in un computer remoto.  

 Nella seguente tabella vengono elencate le versioni di SQL Server supportate dal punto di Reporting Services.  

|Versione di SQL Server|Punto di Reporting Services|  
|------------------------|------------------------------|
|SQL Server 2017 con aggiornamento cumulativo 2 o successivo<br /><br /> Standard<br />Enterprise|Sì, a partire da Configuration Manager versione 1710|  
|SQL Server 2016 con SP1<br /><br /> Standard<br />Enterprise|Sì| 
|SQL Server 2016<br /><br /> Standard<br />Enterprise|Sì|
|SQL Server 2014 con SP2<br /><br /> Standard<br />Enterprise|Sì|
|SQL Server 2014 con SP1<br /><br /> Standard<br />Enterprise|Sì|
|SQL Server 2012 con SP4 <br /><br /> Standard<br />Enterprise|Sì|  
|SQL Server 2012 con SP3 <br /><br /> Standard<br />Enterprise|Sì|  
|SQL Server 2008 R2 con SP3<br /><br /> Standard<br />Enterprise<br />Datacenter|Sì, per le versioni supportate di Configuration Manager precedenti alla 1702.|  
|SQL Server Express 2008 R2 con SP3|Non supportato| 




## <a name="next-steps"></a>Passaggi successivi
[Operazioni e manutenzione per la creazione di report](operations-and-maintenance-for-reporting.md)
