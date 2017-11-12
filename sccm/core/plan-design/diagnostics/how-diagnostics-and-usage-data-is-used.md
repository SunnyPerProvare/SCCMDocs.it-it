---
title: Uso dei dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni su come Microsoft usa i dati di diagnostica e di utilizzo raccolti da System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e6395421e88baf822bc0a8971119b6fe360e6680
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Come vengono usati i dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I dati di diagnostica e di utilizzo raccolti da System Center Configuration Manager offrono un feedback quasi immediato a Microsoft sul funzionamento del prodotto e vengono usati per adeguare gli aggiornamenti futuri. Microsoft può inoltre vedere dati di configurazione utili per progettare e testare le configurazioni in produzione. Ad esempio:  

-   Versioni dei server Windows usate dai server del sito  

-   Language Pack installati  

-   Differenziale dello schema SQL rispetto all'impostazione predefinita del prodotto  

Questi dati consentono al team di progettazione di pianificare test futuri per garantire un'esperienza ottimale per le configurazioni più comuni. Poiché gli aggiornamenti per Configuration Manager vengono rilasciati con una frequenza maggiore per supportare meglio le tecnologie in rapida evoluzione come Windows 10 e Microsoft Intune, questi dati sono fondamentali per interventi di adattamento tempestivi.  

Altrettanto importante è comprendere in quali situazioni questi dati non vengono usati. Microsoft non usa questi dati per:  

-   Controlli delle licenze, ad esempio per confrontare l'utilizzo di una licenza da parte dell'utente rispetto al contratto stipulato  

-   Controllo dei prodotti non supportati  

-   Pubblicità basata sui dati disponibili, ad esempio l'utilizzo delle funzionalità o la georilevazione (fuso orario)  

##  <a name="bkmk_improve"></a> Esempi di miglioramenti al prodotto con i dati di diagnostica e di utilizzo  
Microsoft usa i dati disponibili per migliorare il prodotto. Di seguito sono indicati alcuni esempi:  

-   **Revisione del supporto per i sistemi operativi del server:**  

     Il supporto iniziale offerto da System Center Configuration Manager Current Branch limitava la tempistica di supporto per Windows Server 2008 R2. Dopo aver esaminato i dati di utilizzo dei clienti che hanno eseguito l'aggiornamento a Configuration Manager Current Branch, è emersa la necessità di modificare ed estendere i tempi previsti per supportare i clienti che ancora usano questo sistema operativo server per ospitare i server del sito e i ruoli del sistema del sito.  

-   **Controlli dei prerequisiti migliorati:**  

     In base ai dati di utilizzo, sono stati migliorati i controlli dei prerequisiti per l'installazione di un aggiornamento per rimuovere le regole obsolete, tenere conto di altri scenari e, in alcuni casi, per correggere automaticamente alcuni problemi.  
