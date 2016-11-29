---
title: Introduzione a Long-Term Servicing Branch | System Center Configuration Manager
description: Informazioni su Long-Term Servicing Branch di System Center Configuration Manager.
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 926d1b1299e7851bd1d9168237859c5cd7a65abe


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introduzione a Long-Term Servicing Branch di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Questo argomento offre informazioni su Long-Term Servicing Branch (LTSB) di Configuration Manager e aiuta a comprendere la documentazione relativa.


LTSB è un ramo distinto di Configuration Manager basato sulla versione 1606 di Current Branch. Rispetto a Current Branch, LTSB ha [funzionalità ridotte](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). È destinato ai clienti che hanno [lasciato scadere Software Assurance o una sottoscrizione equivalente](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Panoramica delle licenza:**   
I clienti con Software Assurance o sottoscrizione equivalente attiva per le licenze di System Center Configuration Manager a partire dal 1° ottobre 2016 hanno diritto a usare la versione 1606 (ottobre 2016) di System Center Configuration Manager. I clienti che il 1° ottobre 2016 o in data successiva hanno una sottoscrizione attiva a System Center Configuration Manager troveranno al momento dell'installazione due opzioni con licenza: Current Branch e Long-Term Servicing Branch (LTSB).

**Specifiche delle licenze:**  
[I termini e le condizioni relativi ai prodotti acquistati tramite i programmi multilicenza Microsoft sono disponibili qui](http://go.microsoft.com/fwlink/?LinkId=800052).

I clienti che dispongono di diritti perpetui su System Center Configuration Manager o che dopo il 1° ottobre lasciano scadere la sottoscrizione Software Assurance o equivalente possono installare la versione di System Center Configuration Manager LTSB corrente al momento della scadenza.
- Per informazioni su Software Assurance e i requisiti di licenza per System Center Configuration Manager, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).
-   Per informazioni sulle differenze tra i diversi rami, vedere [Which branch of Configuration Manager should I use](which-branch-should-i-use.md) (Scelta del ramo di Configuration Manager da usare).

Per installare un nuovo sito o effettuare l'aggiornamento da un sito di System Center Configuration Manager 2012 supportato a LTSB, usare il supporto di base della versione 1606. Il supporto di base è disponibile su DVD all'interno di Microsoft System Center 2016 o in System Center Configuration Manager Current Branch e Long-Term Servicing Branch 1606. Il supporto di base che consente di installare LTSB consente di installare anche Current Branch versione 1606 di Configuration Manager. Per informazioni sui supporti di base, vedere [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions) (Versioni base e di aggiornamento).

Per informazioni su come installare un sito LTSB, vedere [Install and Upgrade for the Long-Term Servicing Branch](install-the-ltsb.md) (Installare e aggiornare per Long-Term Servicing Branch). Per informazioni su come ottenere System Center 2016, vedere la [documentazione di System Center 2016](https:\technet.microsoft.com\system-center-docs\System-Center-2016).

> [!IMPORTANT]
> Tutti i siti in una gerarchia devono eseguire lo stesso ramo. Non è supportata una gerarchia con una combinazione di LTSB e Current Branch in siti diversi.
>
> Analogamente, quando si usa il ripristino, per il sito o il database del sito è necessario ripristinare il ramo originario. Non è possibile ripristinare un database del sito Current Branch con un'installazione LTSB o viceversa.


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funzionalità non disponibili in LTSB di Configuration Manager
Rispetto a Current Branch, LTSB presenta le seguenti limitazioni:

- Non riceve gli aggiornamenti per le nuove funzionalità.
- Non supporta l'aggiunta di una sottoscrizione Microsoft Intune. Ciò impedisce l'uso di:
  - Intune in una configurazione MDM ibrida
  - Software MDM locale
-   Non supporta l'uso del dashboard Manutenzione pacchetti di Windows 10, dei piani di manutenzione. Non supporta Current Branch e Current Branch for Business di Windows 10
- Non supporta le versioni future di LTSB di Windows 10 e Windows Server
-   Non supporta Asset Intelligence
-   Non supporta i punti di distribuzione basati sul cloud
-   Non supporta Exchange Online come Exchange Connector
-   Non supporta funzionalità in versione non definitiva


Il supporto per queste funzionalità non è incluso in LTSB. Alcune funzionalità, tuttavia, restano visibili nella console di Configuration Manager ma non possono essere selezionate o usate.

Eventuali nuovi sistemi operativi aggiunti di cui è previsto il supporto in Current Branch non sono supportati da LTSB.

## <a name="documentation-for-the-ltsb"></a>Documentazione per LTSB
LTSB si basa su Current Branch versione 1606. La documentazione da usare per LTSB è quindi la [documentazione online valida per Current Branch](https://docs.microsoft.com/sccm/), con le avvertenze e le limitazioni specifiche di LTSB come indicato negli argomenti seguenti:  

-   [Introduzione a Long-Term Servicing Branch](introduction-to-the-ltsb.md): questo argomento

-   [Which branch of Configuration Manager should I use](which-branch-should-i-use.md) (Scelta del ramo di Configuration Manager da usare): informazioni sui diversi rami di System Center Configuration Manager, per assicurarsi di installare il ramo più adatto alle proprie esigenze.

-   [Install the Long-Term Servicing Branch](install-the-ltsb.md) (Installare Long-Term Servicing Branch): come installare un nuovo sito LTSB o eseguire l'aggiornamento di un sito di System Center Configuration Manager 2012 a LTSB.

-   [Upgrade the Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md) (Aggiornare Long-Term Servicing Branch a Current Branch): come convertire l'installazione LTSB in installazione Current Branch.

-   [Licenze e rami per System Center Configuration Manager](learn-more-editions.md): informazioni su Software Assurance e i requisiti di licenza correlati per System Center Configuration Manager.
-   [Supported Configurations for the Long-Term Servicing Branch](supported-configurations-for-ltsb.md) (Configurazioni supportate per Long-Term Servicing Branch): versioni e requisiti di sistemi operativi e prodotti dipendenti, ad esempio SQL Server, che è possibile usare con LTSB.


Per riconoscere il ramo a cui si riferiscono le diverse parti della documentazione, basarsi sulle linee guida seguenti:  
-   Gli argomenti con intestazione *Si applica a: Current Branch* si riferiscono sia a Current Branch che a Long-Term Servicing Branch, anche se alcune parti dell'argomento potrebbero essere valide solo per una versione più recente di Current Branch.

-   Per distinguere le parti di un argomento che non si applicano a LTSB, le funzionalità e le modifiche introdotte dopo la versione 1606 di Current Branch sono identificate da una frase simile ad "A partire dalla versione 1610". Dato che sono state introdotte dopo la versione 1606 di Current Branch, non sono valide per LTSB.

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Analogie tra Current Branch e LTSB
LTSB si basa su Current Branch versione 1606, con alcune eccezioni, ad esempio l'integrazione di Intune e le funzionalità relative al cloud. Pertanto, la maggior parte delle attività per la pianificazione della distribuzione, della configurazione e della gestione dei due rami è identica.

LTSB, ad esempio, supporta lo stesso numero di siti, tipi di sito e client, nonché la stessa infrastruttura generale di Current Branch. È quindi possibile usare le indicazioni disponibili negli argomenti relativi alla pianificazione e alla progettazione dei siti e delle gerarchie per Current Branch. Analogamente, per le funzionalità supportate da entrambi i rami, ad esempio gli aggiornamenti software o la distribuzione del sistema operativo, è possibile usare le indicazioni disponibili nelle sezioni corrispondenti della documentazione di Current Branch, tenendo presente che non sono disponibili le modifiche introdotte dopo la versione 1606 di Current Branch.


## <a name="how-to-identify-your-branch-and-version"></a>Come identificare il ramo e la versione in uso
Visualizzando le informazioni sulla versione per un sito di Configuration Manager, è anche possibile visualizzare il ramo.

Per controllare la versione del sito, nella console passare a **Informazioni su System Center Configuration Manager** nell'angolo in alto a sinistra. Qui in **Versione sito** è visualizzato **5.0.8412.1000**.

Per verificare il ramo del sito (LTSB o Current Branch), nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti**, e aprire **Impostazioni gerarchia**.  Se è disponibile un'opzione per la conversione in Current Branch e tale opzione è attiva, il sito esegue la versione LTSB. Se il sito esegue Current Branch, questa opzione è disabilitata.

Per informazioni sulle diverse versioni di Configuration Manager, vedere **Baseline and update versions** (Versioni di base e di aggiornamento) nell'argomento [Updates for Configuration Manager](/sccm/core/servers/manage/updates) (Aggiornamenti per Configuration Manager).

## <a name="exceptions-for-using-the-ltsb"></a>Eccezioni per l'uso di LTSB
### <a name="updates-and-servicing-of-the-ltsb"></a>Aggiornamenti e manutenzione di LTSB
Solo gli aggiornamenti di sicurezza critici vengono resi disponibili come aggiornamenti nella console per LTSB.

Tuttavia,nella console sono visibili le informazioni sugli aggiornamenti periodici delle versioni di Current Branch successive. Questi non sono disponibili per LTSB e quindi non vengono scaricati e non possono essere installati.

Per supportare gli aggiornamenti di sicurezza critici all'interno della console, per i siti LTSB è necessario usare il [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point). È possibile configurare questo ruolo del sistema del sito in modalità offline o online, come avviene per Current Branch. LTSB raccoglie e invia gli stessi dati di telemetria e di utilizzo di Current Branch.

LTSB supporta l'uso del programma di installazione dell'aggiornamento rapido e dello strumento di registrazione dell'aggiornamento, come documentato per Current Branch.

Per informazioni generali sugli aggiornamenti e sulla manutenzione, vedere [Updates for Configuration Manager](/sccm/core/servers/manage/updates) (Aggiornamenti per Configuration Manager).

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Modifiche per l'espansione del sito e cartella CD.Latest
Quando si esegue LTSB e si espande un sito primario autonomo installando un nuovo sito di amministrazione centrale, è necessario usare il programma di installazione e i file di origine dal supporto di base della versione 1606.  Per Current Branch si esegue il programma di installazione e si usano i file di origine della cartella CD.Latest.

Anche se non si esegue il programma di installazione per l'espansione del sito dalla cartella CD.Latest, si continua a usare questa cartella per il ripristino del sito e per installare un nuovo sito primario figlio se il primo sito LTSB è un sito di amministrazione centrale.

Per altre informazioni sull'espansione del sito, vedere [Expand a stand-alone primary site](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)(Espandere un sito primario autonomo) in [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)(Usare l'installazione guidata per installare i siti).
Per altre informazioni sulla cartella CD.Latest, vedere [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) (Cartella CD.Latest).



<!--HONumber=Nov16_HO1-->


