---

title: Rimuovere un punto di aggiornamento software | Configuration Manager
description: Seguire questa procedura per rimuovere il ruolo di sistema del sito del punto di aggiornamento software in un sito dalla console di Configuration Manager.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e95e3fc2aafde2d947f08d32e2b2130a313e7328


---
#  <a name="a-namebkmkremovesupa-remove-the-software-update-point-site-system-role"></a><a name="BKMK_RemoveSUP"></a> Rimuovere il ruolo del sistema del sito del punto di aggiornamento software  

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



<!--HONumber=Nov16_HO1-->


