---
title: Introduzione a Long-Term Servicing Branch
titleSuffix: Configuration Manager
description: Informazioni su Long-Term Servicing Branch di System Center Configuration Manager.
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: ad1eac9933a59dd4cf69db468e0fdbe10b5ba619
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introduzione a Long-Term Servicing Branch di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Long-Term Servicing Branch (LTSB) di System Center Configuration Manager è un ramo distinto di Configuration Manager progettato come opzione di installazione disponibile per tutti i clienti. È tuttavia l'unica opzione disponibile per i clienti che hanno lasciato scadere Software Assurance o i diritti di sottoscrizione equivalenti per Configuration Manager.


In base a Configuration Manager versione 1606, LTSB offre funzionalità ridotte rispetto a Current Branch di Configuration Manager.

 > [!TIP]   
 > Se si stanno cercando informazioni sulle opzioni di **Windows Server**, vedere [Windows Server 2016 new Current Branch for Business servicing option]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Nuova opzione di manutenzione Current Branch for Business per Windows Server 2016).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funzionalità non disponibili in LTSB di Configuration Manager
Current Branch di Configuration Manager supporta le funzionalità seguenti, non disponibili quando si usa LTSB:

-   Aggiornamenti nella console che aggiungono nuove funzionalità e miglioramenti.
-   Supporto per sistemi operativi rilasciati di recente da usare come client e server del sito.
-   Usare una sottoscrizione di Microsoft Intune per supportare quanto segue:
    -   Intune in una configurazione ibrida di gestione dei dispositivi mobili (MDM)
    -   Software MDM locale
-   Dashboard di manutenzione di Windows 10 e piani di manutenzione, incluso il supporto per versioni recenti di Windows 10 Current Branch e Current Branch for Business.  
-   Supporto per versioni future di Windows Server e Windows 10 LTSB
-   Asset Intelligence
-   Punti di distribuzione basati su cloud
-   Exchange Online come Exchange Connector    

Il supporto per queste funzionalità non è disponibile con LTSB. Alcune funzionalità, tuttavia, restano visibili nella console di Configuration Manager ma non possono essere selezionate o usate.


## <a name="find-documentation-for-the-ltsb"></a>Trovare la documentazione per LTSB
L'opzione LTSB è basata su Current Branch versione 1606. Come documentazione del prodotto, usare la [documentazione di Current Branch](https://docs.microsoft.com/sccm/), con le avvertenze e le limitazioni specifiche di LTSB. Tali avvertenze e limitazioni sono descritte negli argomenti online seguenti:

-     [Introduzione a Long-Term Servicing Branch](introduction-to-the-ltsb.md): (questo argomento)
-     [Installare Long-Term Servicing Branch](install-the-ltsb.md)
-     [Aggiornare Long-Term Servicing Branch a Current Branch](convert-to-current-branch.md)
-     [Configurazioni supportate per Long-Term Servicing Branch](supported-configurations-for-ltsb.md)
-   [Manage the Long-Term Servicing Branch of Configuration Manager](manage-the-ltsb.md) (Gestire Long-Term Servicing Branch di Configuration Manager)

Quando si fa riferimento alla documentazione di Current Branch per LTSB, i dettagli validi per la versione 1606 sono validi anche per LTSB. Le funzionalità o i dettagli introdotti con la versione 1610 o con versioni successive non sono supportate da LTSB.


## <a name="licensing-overview-for-the-ltsb"></a>Panoramica della gestione delle licenze per LTSB   
I clienti con contratti Software Assurance attivi per le licenze di System Center Configuration Manager, o con diritti di sottoscrizione equivalenti alla data 1 ottobre 2016, hanno diritto a usare la versione 1606 di ottobre 2016 di System Center Configuration Manager. I clienti con diritti per System Center Configuration Manager in data 1 ottobre 2016 o successiva, al momento dell'installazione avranno a disposizione due opzioni con licenza: Current Branch e Long-Term Servicing Branch (LTSB).

I clienti che dispongono di diritti perpetui su System Center Configuration Manager o che dopo il 1° ottobre lasciano scadere la sottoscrizione Software Assurance o equivalente possono installare la versione di System Center Configuration Manager LTSB corrente al momento della scadenza.

[I termini e le condizioni relativi ai prodotti acquistati tramite i programmi multilicenza Microsoft sono disponibili qui](http://go.microsoft.com/fwlink/?LinkId=800052).

Per altre informazioni sulla gestione delle licenze per i rami di Configuration Manager, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Passaggi successivi

Se si decide che Configuration Manager LTSB è il ramo corretto per l'ambiente in uso, [installare un nuovo sito LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) come parte di una nuova gerarchia o [aggiornare un sito e una gerarchia di System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager).

Se non si dispone di un supporto di installazione, vedere la [documentazione di System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) per informazioni su come ottenere System Center 2016, che include il supporto da usare per installare System Center Configuration Manager LTSB.  
