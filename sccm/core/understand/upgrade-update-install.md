---
title: Informazioni su upgrade, aggiornamento e installazione | Documentazione Microsoft
description: Informazioni sulla differenza tra i termini installazione, aggiornamento e upgrade per la gestione dell&quot;infrastruttura di Configuration Manager.
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: 0
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d0735c170820259ac8bb6706aac7cc5569a1628
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.lasthandoff: 01/12/2017

---

# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Informazioni su upgrade, aggiornamento e installazione per l'infrastruttura del sito e della gerarchia

*Si applica a: System Center Configuration Manager (Current Branch)*


Quando si gestisce l'infrastruttura del sito e della gerarchia di System Center Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti.

## <a name="upgrade"></a>Upgrade
Il termine *upgrade* o *upgrade sul posto* viene usato per indicare la conversione del sito o della gerarchia di Configuration Manager 2012 in un sito o una gerarchia che esegue System Center Configuration Manager.
Quando si esegue l'upgrade di System Center 2012 Configuration Manager a System Center Configuration Manager, si continua a usare gli stessi server per ospitare i siti e i server dei siti e si mantengono i dati e le configurazioni esistenti per Configuration Manager.  Questo comportamento è diverso dalla [migrazione](/sccm/core/migration/migrate-data-between-hierarchies), che è un modo per mantenere le configurazioni e i dati sui dispositivi gestiti usando però i nuovi siti di System Center Configuration Manager installati nel nuovo hardware.

Per altre informazioni, vedere l'articolo [Eseguire l'aggiornamento a System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Aggiornamento
Il termine *aggiornamento* viene usato per indicare l'installazione di aggiornamenti nella console per System Center Configuration Manager e gli aggiornamenti fuori banda che non possono essere distribuiti dall'interno della console di Configuration Manager. Gli aggiornamenti nella console possono modificare la versione del sito Current Branch (o Technical Preview) in modo da eseguire una versione successiva. Se ad esempio il sito esegue una versione 1606, è possibile installare un aggiornamento per la versione 1610. Gli aggiornamenti possono inoltre installare correzioni per un problema noto, senza modificare la versione dei siti.      

In genere, gli aggiornamenti aggiungono correzioni per la sicurezza, miglioramenti della qualità e nuove funzionalità alla distribuzione esistente. Se si usa il ramo Technical Preview, un aggiornamento può installare una versione più recente della Technical Preview.
-   È l'utente stesso a scegliere quando installare l'aggiornamento nella console, a partire dal sito di livello superiore della gerarchia.
- È possibile installare qualsiasi aggiornamento disponibile dall'interno della console. Se ad esempio il sito esegue la versione 1602 e sono disponibili sia la 1606 sia la 1610, può essere opportuno installare la 1610 perché ogni versione include le funzionalità che sono state prima introdotte nelle versioni rilasciate in precedenza.
- Al termine dell'installazione di un nuovo aggiornamento nel sito di livello superiore, i siti primari figlio avviano automaticamente il processo di aggiornamento. È tuttavia possibile impostare [intervalli di servizio](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) per controllare i tempi di esecuzione degli aggiornamenti.
- I siti secondari non installano gli aggiornamenti automaticamente. Spetta all'utente avviare manualmente l'aggiornamento dall'interno della console di Configuration Manager.

Per altre informazioni, vedere [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates) e [Technical Preview per System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Installazione
Il termine *installazione* viene usato quando si crea una gerarchia di Configuration Manager completamente nuova o si aggiungono altri siti a una gerarchia esistente.  

Quando si installa un nuovo sito primario o di amministrazione centrale, il percorso del file setup.exe e dei file di origine correlati varia a seconda dello scenario di installazione.

Per altre informazioni, vedere [Preparare l'installazione di siti](/sccm/core/servers/deploy/install/prepare-to-install-sites).

