---
title: Controllo remoto | Microsoft Docs
description: Introduzione al controllo remoto in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29350919-6a25-446b-a0da-05e8914fbb26
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: 47bfeec5bd5d9b843e9064560d0cd0b14bd7d6a1
ms.contentlocale: it-it
ms.lasthandoff: 12/30/2016


---
# <a name="introduction-to-remote-control-in-system-center-configuration-manager"></a>Introduzione al controllo remoto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare il controllo remoto per amministrare o visualizzare in remoto tutti i computer client nella gerarchia o per fornire assistenza a questi. È possibile usare il controllo remoto per risolvere i problemi di configurazione hardware e software nei computer client e per fornire supporto. Configuration Manager supporta il controllo remoto di computer di gruppi di lavoro e aggiunti a dominio.  

Configuration Manager consente anche di configurare le impostazioni client per l'esecuzione di Desktop remoto di Windows e di Assistenza remota dalla console di Configuration Manager.  

> [!NOTE]  
>  Non è possibile creare una sessione di Assistenza remota dalla console di Configuration Manager a un computer client negli scenari seguenti:  
>   
>  -   Il computer client fa parte di un gruppo di lavoro.  
> -   Il computer che esegue la console di Configuration Manager esegue Windows XP Service Pack 3 ma il computer host non esegue questo sistema operativo. Per altre informazioni, vedere la documentazione di Assistenza remota Windows.  

 È possibile avviare una sessione di controllo remoto da qualsiasi raccolta di dispositivi nella console di Configuration Manager, dalla finestra del prompt dei comandi di Windows o dal menu **Start** di Windows.  

