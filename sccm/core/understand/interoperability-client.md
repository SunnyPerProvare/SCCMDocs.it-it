---
title: "Usare il client di interoperabilità estesa di Configuration Manager con Current Branch | Microsoft Docs"
description: Informazioni sull'uso del client Long-Term Servicing Branch di Configuration Manager con un sito Current Branch.
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: robstackmsft
ms.author: robstack
ms.openlocfilehash: 6487a7c0eb958c74ca4c6a7233747966110eceb9
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/11/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Usare il software client del supporto di Configuration Manager per l'interoperabilità estesa con le versioni future di un sito Current Branch

*Si applica a: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*  

In alcuni casi, i criteri aziendali potrebbero non consentire di aggiornare regolarmente il client di Configuration Manager in alcuni PC. Ad esempio, potrebbe essere necessario garantire la conformità con criteri di gestione delle modifiche oppure potrebbe trattarsi di un dispositivo strategico per l'azienda.

Sebbene sia consigliabile continuare a usare l'aggiornamento automatico per la maggior parte dei client quando possibile, a partire dall'aggiornamento 1610 di Configuration Manager è possibile soddisfare queste esigenze tramite l'installazione di un nuovo client per l'uso a lungo termine, denominato client di interoperabilità estesa.

Il client di interoperabilità estesa è compatibile con i siti di Configuration Manager che eseguono la versione 1610 o successiva. Il client di interoperabilità estesa deve essere usato solo per PC specifici che non possono essere aggiornati di frequente, come dispositivi POS o chiosco multimediale. Per tutti gli altri PC, usare il client di Configuration Manager più recente.

## <a name="how-this-scenario-works"></a>Funzionamento di questo scenario

In genere, quando si installa un nuovo aggiornamento nella console per Current Branch, il software client dei computer client si aggiorna automaticamente in modo da poter usare le nuove funzionalità.

In questo scenario si usa Current Branch e si ricevono nuove funzionalità e nuovi aggiornamenti. La maggior parte dei client esegue il software client da Current Branch e può aggiornare il software client con ogni versione di aggiornamento installata. Tuttavia, in un subset di sistemi critici per i quali non si vogliono ricevere aggiornamenti del software client si installa il client di interoperabilità estesa. Questi client non installano nuovo software client fino a quando in essi non viene distribuita in modo esplicito una nuova versione del software client.

>[!IMPORTANT]
>Il sito Current Branch deve eseguire la versione 1610 o una versione successiva.

## <a name="how-to-use-the-eic"></a>Come usare il client di interoperabilità estesa

1. Recuperare il client di interoperabilità estesa (versione client 5.00.8412) dalla cartella \SMSSETUP\Client del supporto di installazione della versione 1606 di Configuration Manager. Assicurarsi di copiare l'intero contenuto della cartella.
2. Installare manualmente il client di interoperabilità estesa in tali dispositivi. [Informazioni dettagliate su come installare manualmente il client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Escludere tale raccolta dagli aggiornamenti del client.

>[!TIP]
>Per trovare System Center Configuration Manager versione 1606 in Volume Licensing Service Center (VLSC), passare alla scheda **Downloads and Keys** (Download e codici) di [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), cercare "system center config" e selezionare **System Center Config Mgr (Current Branch e LTSB)**.

## <a name="the-extended-interoperability-client-software"></a>Software client di interoperabilità estesa

Il client di interoperabilità estesa corrente continuerà a essere supportato con le versioni aggiornate di Configuration Manager Current Branch almeno fino al 18 novembre 2018. Dopo questa data, verificare di nuovo questa pagina per informazioni dettagliate su un nuovo client di compatibilità estesa oppure sull'estensione del supporto per il client esistente.

>[!TIP]
>Il client di compatibilità estesa sarà supportato per almeno due anni dopo la data di rilascio (vedere [Supporto per le versioni Current Branch di System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported). Ad esempio, il supporto per il client di compatibilità estesa corrente dura due anni a partire dalla data di rilascio della versione 1610, ovvero fino al 18 novembre 2018.

Pianificare l'aggiornamento del client di interoperabilità estesa nei dispositivi gestiti con Current Branch prima della scadenza del supporto. A tale scopo è necessario scaricare una nuova versione del client da Microsoft e quindi distribuire il software client aggiornato nei dispositivi che usano il client di interoperabilità estesa.

## <a name="limitations-of-the-extended-interoperability-client"></a>Limiti del client di interoperabilità estesa

- Gli aggiornamenti per il software client di interoperabilità estesa non sono disponibili tramite gli aggiornamenti nella console. Dettagli aggiuntivi per la distribuzione di software client aggiornato verranno forniti al momento del rilascio di un aggiornamento del client.
- Il client di compatibilità estesa supporta solo aggiornamenti software, inventario e pacchetti e programmi.

## <a name="next-steps"></a>Passaggi successivi

Usare le informazioni disponibili in [Come monitorare i client](/sccm/core/clients/manage/monitor-clients) per garantire la corretta installazione dei client nei dispositivi.
