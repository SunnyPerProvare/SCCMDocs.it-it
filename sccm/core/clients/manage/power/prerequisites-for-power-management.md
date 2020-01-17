---
title: Prerequisiti per il risparmio energia
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per il risparmio energia in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: cbcb56a95f0ad4d876636db311fa8d7d7047292c
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75823926"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Prerequisiti per il risparmio energia in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Il risparmio energia in Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  
 La tabella seguente elenca le dipendenze esterne a Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|I computer client devono essere in grado di supportare gli stati necessari relativi al risparmio energia|Per usare tutte le funzionalità di risparmio energia, i computer client devono essere in grado di supportare le azioni sospensione, ibernazione, riattivazione dallo stato di sospensione e riattivazione dallo stato di ibernazione. È possibile usare il report **Funzionalità alimentazione** per determinare se i computer supportano queste azioni. Per altre informazioni, vedere [Report Funzionalità alimentazione](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) nell'argomento [Come monitorare e pianificare il risparmio energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  
 La tabella seguente elenca le dipendenze interne di Configuration Manager per il risparmio energia.  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Il risparmio energia deve essere abilitato prima di poter creare e monitorare le combinazioni per il risparmio di energia.|Per informazioni su come abilitare e configurare il risparmio energia, vedere [Configurazione del risparmio energia](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Punto di Reporting Services|Prima di poter visualizzare i report di risparmio energia, è necessario configurare un punto di Reporting Services. Per altre informazioni, vedere [Reporting](../../../../core/servers/manage/reporting.md) (Creazione di report).|  
