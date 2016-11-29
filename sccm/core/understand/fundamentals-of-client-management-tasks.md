---
title: Nozioni fondamentali sulla gestione dei client | System Center Configuration Manager
description: "Informazioni sulle attività che è possibile eseguire per gestire i client di System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b746c051eee42bcea5c01ced359f568c5aae5fd8


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Nozioni fondamentali sulle attività di gestione client per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver installato i client di System Center Configuration Manager è possibile eseguire diverse attività per la gestione dei client.  Alcune vengono avviate dalla console di Configuration Manager mentre altre possono essere avviate o visualizzate in un client dall'app Configuration Manager dei client nel Pannello di controllo di Windows.  

## <a name="the-console"></a>La console  
 Dalla console di Configuration Manager è possibile eseguire diverse attività di gestione dei client, incluse le seguenti:  

-   Distribuzione di applicazioni, aggiornamenti software, script di manutenzione e sistemi operativi. È possibile configurare questi elementi per l'installazione in una data e ora specifica oppure renderli disponibili per l'installazione da parte dell'utente in base alla necessità. Si possono anche configurare le applicazioni da disinstallare.  

-   Agevolare la protezione dei computer da malware e minacce alla protezione e notificare eventuali problemi rilevati.  

-   Definire le impostazioni di configurazione del client che si desidera monitorare e risolvere eventuali mancate conformità.  

-   Raccogliere informazioni di inventario hardware e software, incluse le informazioni sul monitoraggio e la riconciliazione delle licenze da Microsoft.  

-   Risolvere i problemi dei computer usando il controllo remoto.  

-   Implementare impostazioni di risparmio energia per gestire e monitorare il consumo energetico dei computer.  

Per monitorare queste operazioni quasi in tempo reale, usare la console di Configuration Manager per visualizzare avvisi e informazioni sullo stato. Per acquisire dati e tendenze cronologiche, è possibile usare le capacità di reporting integrate di SQL Reporting Services.  I client inviano i dettagli al sito come stato del client.  Le informazioni sullo stato del client offrono dati sull'integrità e sulle attività del client e possono essere visualizzate nella console o usando i report predefiniti per Configuration Manager. Questi dati consentono di identificare i computer che non rispondono e, in alcuni casi, i problemi possono essere risolti automaticamente.  

 Per altre informazioni sulle attività di gestione per i client, vedere  [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) (Come gestire i client in System Center Configuration Manager) e [Come gestire i client per i server Linux e UNIX in System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Per informazioni sull'uso dei report, vedere   
            [Introduzione ai report in System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="the-windows-control-panel-app"></a>App Pannello di controllo di Windows  
 Quando si installa il software client di Configuration Manager, nel Pannello di controllo viene installata l'applicazione client di **Configuration Manager**. A differenza del Software Center, questa applicazione è progettata per l'help desk e non per gli utenti finali. Per alcune opzioni di configurazione sono necessarie autorizzazioni amministrative locali e la maggior parte delle opzioni necessita di competenze tecniche relative al funzionamento di Configuration Manager. È possibile usare questa applicazione per eseguire le attività seguenti in un client:  

-   Visualizzare le proprietà relative al client, ad esempio numero di build, sito assegnato, punto di gestione con cui comunica e utilizzo di un certificato PKI o un certificato autofirmato da parte del client.  

-   Verificare che il client abbia scaricato i criteri client dopo la prima installazione del client e che le impostazioni client siano abilitate o disabilitate come previsto, in base delle impostazioni client configurate nella console di Configuration Manager.  

-   Avviare azioni del client, ad esempio il download dei criteri client, nel caso in cui sia stata apportata una modifica recente ala configurazione nella console di Configuration Manager e non si voglia attendere fino al successivo aggiornamento pianificato.  

-   Assegnare manualmente un client a un sito di Configuration Manager oppure provare a individuare un sito e specificare il suffisso DNS per i punti di gestione pubblicati su DNS.  

-   Configurare la cache del client che memorizza temporaneamente i file ed eliminare i file nella cache se è necessario più spazio su disco per installare il software.  

-   Configurare le impostazioni per la gestione client basata su Internet.  

-   Visualizzare le linee di base di configurazione distribuite nel client, avviare la valutazione di conformità e visualizzare i report di conformità.  



<!--HONumber=Nov16_HO1-->


