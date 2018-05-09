---
title: Rimuovere un punto di aggiornamento software
titleSuffix: Configuration Manager
description: Seguire questa procedura per rimuovere il ruolo di sistema del sito del punto di aggiornamento software in un sito dalla console di Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 585077c44b13d79da55e8ab140fd93998b8371c1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_RemoveSUP"></a> Rimuovere il ruolo del sistema del sito del punto di aggiornamento software  

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile rimuovere il ruolo di sistema del sito del punto di aggiornamento software in un sito dalla console di Configuration Manager. I criteri client vengono aggiornati per rimuovere il punto di aggiornamento software dall'elenco. Quando si rimuove l'ultimo punto di aggiornamento software nel sito, l'elenco di punti di aggiornamento software non conterrà alcun punto di aggiornamento software e gli aggiornamenti software sono sostanzialmente disabilitati nel sito. Quando sono presenti più punti di aggiornamento software in un sito primario e si rimuove il punto di aggiornamento software configurato come origine della sincronizzazione, è necessario scegliere un altro punto di aggiornamento software nel sito come nuova origine della sincronizzazione.  

> [!NOTE]  
>  Quando si rimuove il ruolo del sito del punto di aggiornamento software da un sistema del sito, attendere almeno 15 minuti prima di reinstallare il ruolo del sito del punto di aggiornamento software.  

 Utilizzare la procedura seguente per rimuovere un punto di aggiornamento software.  

#### <a name="to-remove-the-software-update-point"></a>Per rimuovere il punto di aggiornamento software  

1.  Nella console di **Configuration Manager** fare clic su **Amministrazione**.  

2.  Nell'area di lavoro Amministrazione, espandere **Configurazione del sito**e quindi fare clic su **Server e ruoli del sistema del sito**.  

3.  Selezionare il server di sistema del sito con il punto di aggiornamento software da rimuovere e quindi in **Ruoli sistema del sito**selezionare **Punto di aggiornamento software**.  

4.  Nel gruppo **Ruolo del sito** della scheda **Ruolo del sito** fare clic su **Rimuovi ruolo**. Confermare che si vuole rimuovere il punto di aggiornamento software o selezionare una nuova origine di sincronizzazione per gli altri punti di aggiornamento software nel sito.  
