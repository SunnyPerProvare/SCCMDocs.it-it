---
title: Prerequisiti per il risparmio energia | Microsoft Docs
description: Ottenere i prerequisiti per il risparmio energia in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 5247bf1ce5b04264bc0d3e04c5de7f98300905c9
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Prerequisiti per il risparmio energia in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il risparmio energia in System Center Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 La tabella seguente elenca le dipendenze esterne a Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|I computer client devono essere in grado di supportare gli stati necessari relativi al risparmio energia|Per usare tutte le funzionalità di risparmio energia, i computer client devono essere in grado di supportare le azioni sospensione, ibernazione, riattivazione dallo stato di sospensione e riattivazione dallo stato di ibernazione. È possibile usare il report **Funzionalità alimentazione** per determinare se i computer supportano queste azioni. Per altre informazioni, vedere [Report sulla funzionalità alimentazione](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) nell'argomento [Come monitorare e pianificare il risparmio energia in Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  
 La tabella seguente elenca le dipendenze interne di Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Il risparmio energia deve essere abilitato prima di poter creare e monitorare le combinazioni per il risparmio di energia.|Per informazioni su come abilitare e configurare il risparmio energia, vedere [Configurazione del risparmio energia in Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Punto di Reporting Services|Prima di poter visualizzare i report di risparmio energia, è necessario configurare un punto di Reporting Services. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
