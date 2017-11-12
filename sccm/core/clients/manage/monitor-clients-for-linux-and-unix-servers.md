---
title: 'Monitorare i client Linux/UNIX '
titleSuffix: Configuration Manager
description: Monitorare i client su server Linux e UNIX in System Center Configuration Manager.
ms.custom: na
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 777842307b280a4f269d68bcb993f3cec6f2e3e3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Come monitorare i client per i server Linux e UNIX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile visualizzare le informazioni dei server Linux e UNIX nella console di System Center Configuration Manager usando gli stessi metodi usati per visualizzare informazioni dei client basati su Windows.  

 Le informazioni che è possibile visualizzare includono:  

-   Dettagli sullo stato dei client, nei dashboard della console di Configuration Manager  

-   Dettagli sui client nei report di Configuration Manager predefiniti  

-   Dettagli sull'inventario in Esplora inventario risorse  

 Le sezioni seguenti descrivono come ottenere queste informazioni dettagliate da Esplora inventario risorse e dai report.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Usare Esplora inventario risorse per visualizzare l'inventario per i server Linux e UNIX  

 Dopo che un client di Configuration Manager invia l'inventario hardware al sito di Configuration Manager, è possibile usare Esplora inventario risorse per visualizzare queste informazioni. Il client di Configuration Manager per Linux e UNIX non aggiunge nuove classi o visualizzazioni per l'inventario in Esplora inventario risorse. I dati di inventario di Linux e UNIX sono mappati a classi WMI esistenti. È possibile visualizzare i dettagli sull'inventario per i server Linux e UNIX nelle classificazioni basate su Windows usando Esplora inventario risorse.  

 Ad esempio, è possibile raccogliere l'elenco di tutti i programmi installati in modo nativo presenti nei server Linux e UNIX. Esempi di programmi installati in modo nativo includono **.rpms** in Linux o **.pkgs** in Solaris. Dopo che un inventario è stato inviato da un client Linux o UNIX, è possibile visualizzare l'elenco di tutti i programmi Linux o UNIX installati in modo nativo in Esplora inventario risorse nella console di Configuration Manager.  

 Per informazioni su come usare Esplora inventario risorse, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Come usare i report per visualizzare informazioni per i server Linux e UNIX  
 I report per Configuration Manager includono informazioni dei server Linux e UNIX, insieme a informazioni dei computer basati su Windows. Non sono necessarie configurazioni aggiuntive per integrare i dati di Linux e UNIX nei report.  

 Ad esempio, se si esegue il report relativo al numero di versioni del sistema operativo, vengono visualizzati l'elenco dei diversi sistemi operativi e il numero dei client che eseguono ogni sistema operativo. Il report è basato sulle informazioni dell'inventario hardware inviate dai diversi client di Configuration Manager che eseguono sistemi operativi diversi.  

 È anche possibile creare report personalizzati specifici dei dati dei server Linux e UNIX. La proprietà **Didascalia** della classe di inventario hardware **Sistema operativo** è un attributo utile che è possibile usare per identificare sistemi operativi specifici nella query del report.  

 Per informazioni sui report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
