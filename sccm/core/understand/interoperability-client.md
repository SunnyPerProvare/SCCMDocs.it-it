---
title: "Usare il client di interoperabilità estesa con Current Branch | Microsoft Docs"
description: Informazioni sull&quot;uso del client di Long-Term Servicing Branch di Configuration Manager con un sito di Current Branch.
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: robstackmsft
ms.author: robstack
Robots: NOINDEX,NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 30d0177dc7fcc7f39d00c48067130d587435bf2d
ms.contentlocale: it-it
ms.lasthandoff: 12/16/2016

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usare il software client del supporto di base della versione 1606 per l'interoperabilità estesa con le versioni future di un sito di Current Branch

*Si applica a: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

È possibile usare il software client di Configuration Manager per computer Windows (client. msi) dal DVD supporto di base della versione 1606 in dotazione con System Center 2016 o da una versione di System Center Configuration Manager (Current Branch e Long-Term Servicing Branch 1606) per gestire i dispositivi che appartengono a un sito di Current Branch. Questo client è detto client di interoperabilità estesa.

## <a name="how-this-scenario-works"></a>Funzionamento di questo scenario:
In genere, quando si installa un nuovo aggiornamento nella console per Current Branch, il software client dei computer client si aggiorna automaticamente in modo da poter usare le nuove funzionalità.

In questo scenario si usa Current Branch e si ricevono nuove funzionalità e nuovi aggiornamenti. La maggior parte dei client esegue il software client da Current Branch e può aggiornare il software client con ogni versione di aggiornamento installata. Tuttavia, in un subset di sistemi critici per i quali non si vogliono ricevere aggiornamenti del software client si installa il client di interoperabilità estesa. Questi client installeranno nuovo software client solo quando riceveranno la distribuzione esplicita di una nuova versione del software client.

Altre informazioni su come impedire l'aggiornamento automatico dei client Current Branch quando si installa una nuova versione di Configuration Manager saranno disponibili con Current Branch versione 1610.

Il sito Current Branch deve eseguire la versione 1606 o una versione successiva.

## <a name="the-extended-interoperability-client-software"></a>Software client di interoperabilità estesa
Quando si usa il client di interoperabilità estesa di System Center 2016 o di System Center Configuration Manager (Current Branch e Long-Term Servicing Branch 1606) con un sito Current Branch, il client è supportato per due anni dalla disponibilità generale della versione, cioè a partire dal 12 ottobre 2016.

Pianificare l'aggiornamento del client di interoperabilità estesa nei dispositivi gestiti con Current Branch prima della scadenza del supporto. A tale scopo è necessario scaricare una nuova versione del client da Microsoft e quindi distribuire il software client aggiornato nei dispositivi che usano il client di interoperabilità estesa.

**Limiti del software client di interoperabilità estesa:**
-     Gli aggiornamenti per il software client di interoperabilità estesa non sono disponibili tramite gli aggiornamenti nella console. Dettagli aggiuntivi per la distribuzione di software client aggiornato verranno forniti al momento del rilascio di un aggiornamento del client.

## <a name="identify-the-client-version-you-use"></a>Identificare la versione del client in uso
Di seguito sono indicate le versioni client principali disponibili per Current Branch e LTSB:

|Versione client|Ramo e versione |  
|----------------|---------------------|
|5.00.8325.xxxx |    - Current Branch 1511|
|5.00.8355.xxxx    |- Current Branch 1602|
|5.00.8412.1307    |- Current Branch 1606 </br> - Current Branch 1606 con hotfix rollup 1606 (KB3186654)</br>- client di interoperabilità estesa dal supporto di base della versione 1606|  

È possibile visualizzare la versione del client nella scheda **Generale** dell'applet Pannello di controllo di Configuration Manager.

Nella scheda **Componenti** dell'applicazione alcuni componenti visualizzano valori diversi. Ad esempio, per la versione 8412.1307 del client alcuni componenti sono elencati con la versione 5.00.8412.**1000** e altri con la versione 5.00.8412.**1006**.  La differenza nelle ultime quattro cifre per alcuni componenti è normale e non indica un errore di aggiornamento alla versione corrente del componente.

