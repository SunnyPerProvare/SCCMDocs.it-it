---
title: Scegliere il ramo da usare | Microsoft Docs
description: Informazioni sulle differenze tra i rami disponibili di System Center Configuration Manager.
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 26356a80bd8c78d4517253bae73e53d8d8f3a73a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Scelta del ramo di Configuration Manager da usare

*Si applica a: System Center Configuration Manager (Current Branch, Long-Term Servicing Branch e Technical Preview)*


A partire da ottobre 2016, sono disponibili tre rami di System Center Configuration Manager. Questo argomento include informazioni utili per scegliere il ramo più adatto alle proprie esigenze.

> [!TIP]  
> Tutti i siti in una gerarchia devono eseguire lo stesso ramo. Le gerarchie con rami differenti in siti diversi non sono supportate.

## <a name="current-branch-of-system-center-configuration-manager"></a>Current Branch di System Center Configuration Manager
Si tratta di un ramo con licenza per l'uso in un ambiente di produzione in cui si desidera poter ottenere le funzionalità più recenti. Usare questo ramo se si dispone di System Center Datacenter, System Center Standard, System Center Configuration Manager o di diritti di sottoscrizione equivalenti. Per altre informazioni su Software Assurance e le opzioni di licenza, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> Current Branch può essere installato come copia di valutazione che non richiede una licenza, può essere usata per 180 giorni e supporta l'aggiornamento a una versione con licenza.

L'opzione Current Branch viene aggiornata diverse volte l'anno con nuove funzionalità. Ogni versione di aggiornamento è supportata per un anno a partire dal relativo rilascio. È necessario aggiornare Current Branch a una versione più recente entro la scadenza di tale periodo di un anno. Gli aggiornamenti alle versioni più recenti sono disponibili come aggiornamenti nella console.

Per installare Current Branch come nuovo sito o aggiornamento da System Center 2012 Configuration Manager con Service Pack 2 o System Center 2012 R2 Configuration Manager con Service Pack 1, usare il [supporto di base](/sccm/core/servers/manage/updates#baseline-and-update-versions) per System Center Configuration Manager che viene fornito come DVD con System Center 2016 o che è disponibile come parte di una versione autonoma di System Center Configuration Manager. L'accesso a questo supporto dipende dalla licenza di System Center Configuration Manager. Le versioni di base più recenti, ad esempio la 1702, non supportano l'installazione di LTSB.

È anche possibile usare il supporto di base per installare un nuovo sito come copia di valutazione di Current Branch. Se si vuole installare solo una copia di valutazione, è possibile ottenere il software dal sito Web [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]
> Usare il supporto di base per installare siti per una nuova gerarchia di Configuration Manager. Se è stata precedentemente installata una versione di base come la versione 1511, usare gli aggiornamenti nella console per aggiornare i siti a una nuova versione, ad esempio alla versione 1606.
>
> I siti che vengono aggiornati usando gli aggiornamenti nella console sono uguali al nuovo sito installato usando il supporto di base.
>
> Per altre informazioni, vedere [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates) (Aggiornamenti per System Center Configuration Manager).

**Funzionalità di Current Branch**
- Riceve [aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates) che rendono le nuove funzionalità disponibili per l'uso.
- Riceve aggiornamenti nella console che forniscono correzioni della sicurezza e qualità alle funzionalità esistenti.
- Supporta aggiornamenti fuori programma quando necessario. Vedere [Usare lo strumento di registrazione dell'aggiornamento](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) o [Usare il programma di installazione di hotfix](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Può interagire con Microsoft Intune e altri servizi e infrastrutture basati su cloud.
- Supporta la [migrazione dei dati](/sccm/core/migration/migrate-data-between-hierarchies) da e verso altre installazioni di Configuration Manager.
- Supporta l'aggiornamento dalle versioni precedenti di Configuration Manager.
- Supporta l'installazione come copia di valutazione da cui è possibile eseguire un successivo aggiornamento a un'installazione con licenza completa.

La versione iniziale di Current Branch era la versione 1511. Gli aggiornamenti successivi includono le versioni 1602, 1606 e così via. Il supporto per ogni versione è previsto per un anno e si consiglia di eseguire l'aggiornamento alla versione più recente non appena viene rilasciata. È possibile attendere fino a un anno prima di passare a una versione più recente ed è anche possibile ignorare un aggiornamento per l'installazione dell'ultima versione. Poiché ogni versione è cumulativa, se si ignora un aggiornamento e si installa la versione più recente, si otterrà comunque l'accesso a tutte le funzionalità e i miglioramenti delle versioni precedenti.

Per altre informazioni, vedere [Support for Current Branch versions](/sccm/core/servers/manage/current-branch-versions-supported) (Supporto per versioni di Current Branch).

**Opzioni di aggiornamento**
- Con Software Assurance attivo, è possibile installare gli aggiornamenti nella console per le versioni di Current Branch.  
- Non è possibile convertire Current Branch in Technical Preview. Le Technical Preview sono installazioni distinte che non richiedono una licenza.
- Non è possibile convertire Current Branch in Long-Term Servicing Branch (LTSB). È necessario disinstallare Current Branch e quindi installare LTSB come una nuova installazione.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>Long-Term Servicing Branch di System Center Configuration
Si tratta di un ramo con licenza destinato all'uso nell'ambiente di produzione da parte di clienti di Configuration Manager che usano Current Branch e che hanno lasciato scadere la sottoscrizione Configuration Manager Software Assurance (SA) o diritti di sottoscrizione equivalenti dopo il 1° ottobre 2016. Per altre informazioni su Software Assurance e le opzioni di licenza, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).

L'opzione LTSB è basata sulla versione 1606. Questo ramo non riceve aggiornamenti nella console che offrono nuove funzionalità o aggiornano funzionalità esistenti. Tuttavia, vengono fornite correzioni critiche per la protezione. Per installare LTSB è necessario usare il [supporto di base](/sccm/core/servers/manage/updates#baseline-and-update-versions) della versione 1606 ricevuto come DVD con System Center 2016 o System Center Configuration Manager.

Per installare LTSB come un nuovo sito o un aggiornamento da un sito di Configuration Manager 2012 supportato, usare il [supporto di base](/sccm/core/servers/manage/updates#baseline-and-update-versions) versione 1606, che è possibile ottenere come un DVD con System Center 2016 o una versione di System Center Configuration Manager (Current Branch e Long-Term Servicing Branch 1606). È possibile usare il supporto di base per installare un nuovo sito che esegue la versione 1606 di Current Branch o che esegue Long-Term Servicing Branch.

> [!TIP]  
> Per informazioni su System Center 2016, vedere la relativa [documentazione](https://technet.microsoft.com/system-center-docs/system-center). Questa documentazione indica inoltre come ottenere System Center 2016, che richiede un contratto di licenza Microsoft o diritti analoghi.

> Per trovare System Center Configuration Manager versione 1606 in Volume Licensing Service Center (VLSC), passare alla scheda **Downloads and Keys** (Download e codici) di [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), cercare "system center config" e selezionare **System Center Config Mgr (Current Branch e LTSB)**.

> È possibile ottenere una copia di valutazione di System Center 2016 anche da [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Funzionalità di LTSB**
-   Riceve gli aggiornamenti nella console che offrono correzioni critiche per la sicurezza
- Offre un'opzione di installazione dopo che il contratto SA o i diritti equivalenti per Configuration Manager sono scaduti
- Supporta l'aggiornamento (conversione) a Current Branch quando si dispone di un contratto SA o diritti equivalenti validi per Configuration Manager

**Limitazioni**  
LTSB si basa su Current Branch 1606, con le limitazioni seguenti:
- Dopo la disponibilità generale (ottobre 2016), l'opzione LTSB sarà supportata per 10 anni di aggiornamenti critici per la sicurezza, periodo dopo il quale il supporto per questo ramo scadrà. Per altre informazioni sul ciclo di vita del supporto, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/en-us/lifecycle).
- Supporta un elenco definito limitato di sistemi operativi client e server e tecnologie correlate come le versioni di SQL Server. Per altre informazioni sugli elementi supportati con questo ramo, vedere [Configurazioni supportate per Long-Term Servicing Branch](supported-configurations-for-ltsb.md).
- Non riceve gli aggiornamenti per le nuove funzionalità.
- Non supporta l'aggiunta di una sottoscrizione Microsoft Intune. Ciò impedisce l'uso di:
  - Intune in una configurazione MDM ibrida
 - Software MDM locale
-   Non supporta l'uso del dashboard Manutenzione pacchetti di Windows 10, i piani di manutenzione, Current Branch (CB) e Current Branch for Business (CBB) di Windows 10.
- Non supporta le versioni future di LTSB di Windows 10 e Windows Server.
-   Non supporta Asset Intelligence.
-   Non supporta i punti di distribuzione basati sul cloud.
-   Non supporta Exchange Online come Exchange Connector.
-   Non supporta funzionalità di versioni non definitive.



**Opzioni di aggiornamento**
- È possibile convertire l'installazione LTSB a un'installazione Current Branch. La conversione a Current Branch è supportata prima o dopo la scadenza del supporto per LTSB.

  Per eseguire la conversione, è necessario disporre di un contratto Software Assurance attivo con Microsoft. Per altre informazioni, vedere i seguenti collegamenti:
  - [Aggiornare Long-Term Servicing Branch a Current Branch](convert-to-current-branch.md)
  - [Licenze e rami per System Center Configuration Manager](learn-more-editions.md)
  - La sezione[Versioni di base e di aggiornamento](/sccm/core/servers/manage/updates#baseline-and-update-versions) in [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates)
- Non è possibile convertire LTSB in Technical Preview. Le Technical Preview sono installazioni distinte che non richiedono una licenza.
-   Non è possibile aggiornare una copia di valutazione di Current Branch a un'installazione LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager
La Technical Preview è destinata all'uso in un ambiente di laboratorio in cui si desidera conoscere e provare le nuove funzionalità sviluppate per Configuration Manager. La Technical Preview non è supportata in un ambiente di produzione e non è necessario disporre di un contratto di licenza Software Assurance.

Per installare un nuovo sito che esegue la Technical Preview, usare la versione più recente del [supporto di base per System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Dopo aver installato la Technical Preview, saranno disponibili ogni mese le nuove versioni come aggiornamenti nella console.

**Funzionalità di Technical Preview**
-  Basata sulle versioni di base recenti di Current Branch
-  Riceve gli aggiornamenti nella console per l'aggiornamento dell'installazione all'ultima versione Technical Preview
-  Include nuove funzionalità in fase di sviluppo e per le quali gli sviluppatori desiderano ricevere commenti e suggerimenti degli utenti
-  Riceve gli aggiornamenti applicabili solo al ramo Technical Preview

**Limitazioni**
-  [Il supporto è limitato](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), tra cui un singolo sito primario e fino a 10 client.  
-  Non è possibile aggiornare a Current Branch o LTSB.
-  Non supporta l'uso della migrazione per importare o esportare dati in un'altra installazione di Configuration Manager.
-  Non supporta l'aggiornamento dalle versioni precedenti di Configuration Manager.
-  Non supporta l'installazione come copia di valutazione.

Le funzionalità inizialmente introdotte in una Technical Preview vengono spesso aggiunte a Current Branch in un aggiornamento successivo. Ogni nuova versione di Technical Preview include le funzionalità delle versioni precedenti, anche dopo che tali funzioni sono state aggiunte a Current Branch.

Per altre informazioni, vedere [Technical Preview per System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Opzioni di aggiornamento**
-   È possibile installare qualsiasi aggiornamento nella console per una nuova versione Technical Preview.
-   Non è possibile convertire Technical Preview in Current Branch o LTSB.


## <a name="identify-your-branch-and-version"></a>Identificare il ramo e la versione in uso
Visualizzando le informazioni sulla versione per un sito di Configuration Manager, è anche possibile visualizzare il ramo.

**Versione**   
Per controllare la versione del sito, nella console passare a **Informazioni su System Center Configuration Manager** nell'angolo in alto a sinistra della console dove viene visualizzata la **Versione sito**. Per un elenco completo delle versioni del sito, vedere []().

**Ramo**  
Per verificare il ramo del sito (LTSB o Current Branch), nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e aprire **Impostazioni gerarchia**. Se è disponibile un'opzione per la conversione in Current Branch e tale opzione è attiva, il sito esegue la versione LTSB. Se il sito esegue Current Branch, questa opzione è disabilitata.
Per informazioni sulle diverse versioni di Configuration Manager, vedere "Versioni di base e di aggiornamento" nell'argomento [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates).
