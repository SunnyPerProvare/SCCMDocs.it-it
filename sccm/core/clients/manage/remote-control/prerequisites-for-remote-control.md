---
title: Prerequisiti per il controllo remoto
titleSuffix: Configuration Manager
description: Ottenere i prerequisiti per il controllo remoto in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e7287ae7df68ebbcb8f251b8d001233a647596ee
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Prerequisiti per il controllo remoto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il controllo remoto in System Center Configuration Manager ha dipendenze esterne e dipendenze nel prodotto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Driver della scheda video del computer|Assicurarsi che nei computer client sia installato il driver della scheda video più aggiornato per garantire prestazioni di controllo remoto ottimali.|  

 I dispositivi che eseguono Windows Embedded, Windows Embedded per punto di servizio e Windows Fundamentals per PC legacy non supportano il visualizzatore controllo remoto, ma supportano il client di controllo remoto.  

 Il controllo remoto di Configuration Manager non può essere usato per amministrare in remoto computer client che eseguono Systems Management Server 2003 o Configuration Manager 2007.  

> [!NOTE]  
>  Non è necessario alcun servizio di Windows come dipendenza esterna per il controllo remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemi operativi supportati per il visualizzatore controllo remoto  
Il visualizzatore controllo remoto è supportato in tutti i sistemi operativi supportati per la console di Configuration Manager. Per altre informazioni, vedere [Configurazioni supportate per le console di System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Il controllo remoto deve essere abilitato per i client|Per impostazione predefinita, il controllo remoto non è abilitato quando si installa Configuration Manager. Per informazioni su come abilitare e configurare il controllo remoto, vedere [Configurazione del controllo remoto in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Punto di Reporting Services|Prima di poter eseguire report per il controllo remoto, è necessario installare il ruolo del sistema del sito del punto di Reporting Services. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Autorizzazioni di sicurezza per la gestione del controllo remoto|Per accedere alle risorse della raccolta e avviare una sessione di controllo remoto dalla console di Configuration Manager: autorizzazioni **Lettura**, **Leggi risorsa** e **Controllo remoto** per l'oggetto **Raccolta**.<br /><br /> Il ruolo di sicurezza **Operatore strumenti remoti** include queste autorizzazioni necessarie per gestire il controllo remoto in Configuration Manager.<br /><br /> Per altre informazioni, vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Inoltre, agli utenti autorizzati alla visualizzazione è necessario concedere l'autorizzazione all'uso del controllo remoto aggiungendo tali utenti all'elenco **Visualizzatori autorizzati di controllo remoto e assistenza remota** nelle impostazioni client **Strumenti remoti**.
