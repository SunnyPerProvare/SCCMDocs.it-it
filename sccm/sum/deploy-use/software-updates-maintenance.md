---
title: Manutenzione degli aggiornamenti software
titleSuffix: Configuration Manager
description: "Per gestire gli aggiornamenti in Configuration Manager, è possibile pianificare l'attività di pulizia di WSUS oppure eseguirla manualmente."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
ms.openlocfilehash: 51e103b09ced9916fc76f9c87654379b538248b4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="software-updates-maintenance"></a>Manutenzione degli aggiornamenti software

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile pianificare ed eseguire l'attività di pulizia WSUS dalla console di Configuration Manager oppure eseguirla manualmente nelle proprietà del componente del punto di aggiornamento software. Quando si sceglie di eseguire l'attività di pulizia WSUS, questa verrà eseguita alla successiva sincronizzazione degli aggiornamenti software. Gli aggiornamenti software scaduti verranno impostati su uno stato rifiutato nel server WSUS e l'Agente di Windows Update nei computer non eseguirà più la scansione di questi aggiornamenti software. Per impostazione predefinita, il processo di pulizia WSUS viene eseguito ogni 30 giorni.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Per pianificare ed eseguire il processo di pulizia WSUS  

1.  Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.  

2.  Fare clic su **Configura componenti del sito** nel gruppo **Impostazioni** , quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.  

3.  Fare clic sulla scheda **Regole di sostituzione** , selezionare **Esecuzione guidata pulizia WSUS**, quindi fare clic su **OK**.
