---
title: Concetti di base della gestione dei client | Microsoft Docs
description: "Informazioni sulle attività da eseguire per gestire i client di System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fee4f4ba462e59859ac93c4218b67cb26bdd6f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Nozioni fondamentali sulle attività di gestione client per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver installato i client di System Center Configuration Manager è possibile eseguire diverse attività per la gestione dei client.  Alcune delle attività vengono eseguite dalla console di Configuration Manager, altre dall'applicazione client di Configuration Manager. L'applicazione client di Configuration Manager viene installata con il software client di Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Attività dalla console di Configuration Manager
 Nella console di Configuration Manager è possibile eseguire diverse attività di gestione dei client:  

-   Distribuzione di applicazioni, aggiornamenti software, script di manutenzione e sistemi operativi. Configurare l'installazione in una data e ora specifica oppure rendere disponibile il software per l'installazione da parte dell'utente in base alla necessità o configurare le applicazioni da disinstallare.  

-   Agevolare la protezione dei computer da malware e minacce alla protezione e notificare eventuali problemi rilevati.  

-   Definire le impostazioni di configurazione del client che si vuole monitorare e risolvere eventuali mancate conformità.  

-   Raccogliere informazioni di inventario hardware e software, incluse le informazioni sul monitoraggio e la riconciliazione delle licenze da Microsoft.  

-   Risolvere i problemi dei computer usando il controllo remoto.  

-   Implementare impostazioni di risparmio energia per gestire e monitorare il consumo energetico dei computer.  

La console di Configuration Manager consente di monitorare le attività precedenti in tempo quasi reale. Le informazioni di notifica e di stato per ogni attività sono disponibili nella console di Configuration Manager. Per acquisire dati e tendenze cronologiche, usare le funzionalità per la creazione di report integrate di SQL Reporting Services. I client inviano i dettagli al sito come stato del client.  Le informazioni sullo stato del client offrono dati sull'integrità e sulle attività del client e possono essere visualizzate nella console o usando i report predefiniti per Configuration Manager. Questi dati consentono di identificare i computer che non rispondono e, in alcuni casi, i problemi vengono risolti automaticamente.  

 Per altre informazioni sulle attività di gestione per i client, vedere  [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) (Come gestire i client in System Center Configuration Manager) e [Come gestire i client per i server Linux e UNIX in System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Per informazioni sull'uso dei report, vedere   
            [Introduzione ai report in System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Applicazione client di Configuration Manager  
 Quando si installa il software client di Configuration Manager, viene installata anche l'applicazione client di Configuration Manager. A differenza di Software Center, l'applicazione client di Configuration Manager è progettata per l'help desk piuttosto che per gli utenti finali. Per alcune opzioni di configurazione sono necessarie autorizzazioni amministrative locali e la maggior parte delle opzioni necessita di competenze tecniche relative al funzionamento dell'applicazione client di Configuration Manager. È possibile usare questa applicazione per eseguire le attività seguenti in un client:  

-   Visualizzare le proprietà relative al client, ad esempio numero di build, sito assegnato, punto di gestione con cui comunica e uso di un certificato dell'infrastruttura a chiave pubblica (PKI) o un certificato autofirmato da parte del client.  

-   Verificare che il client abbia scaricato correttamente un criterio client dopo la prima installazione del client. Assicurarsi inoltre che le impostazioni del client vengono abilitate o disabilitate come previsto, in base alle impostazioni client configurate nella console di Configuration Manager.  

-   Avviare azioni del client. Ad esempio il download dei criteri client, nel caso in cui sia stata apportata una modifica recente alla configurazione nella console di Configuration Manager e non si voglia attendere fino al successivo aggiornamento pianificato.  

-   Assegnare un client a un sito di Configuration Manager o tentare di trovare un sito manualmente. Specificare quindi il suffisso DNS (Domain Name System) per i punti di gestione pubblicati in DNS.  

-   Configurare la cache del client per la memorizzazione temporanea dei file. Eliminare quindi i file nella cache, se è necessario più spazio su disco per l'installazione di software.  

-   Configurare le impostazioni per la gestione client basata su Internet.  

-   Visualizzare le linee di base di configurazione distribuite nel client, avviare la valutazione di conformità e visualizzare i report di conformità.  
