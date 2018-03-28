---
title: Introduzione alla gestione delle applicazioni
titleSuffix: Configuration Manager
description: Individuare le informazioni di necessarie per gestire e distribuire applicazioni di System Center Configuration Manager.
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: ''
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: a8a66169f3c187f8fa0319548ddde23b399811f3
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2018
---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Introduzione alla gestione delle applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento fornisce una descrizione delle nozioni di base necessarie prima di iniziare a usare le applicazioni di System Center Configuration Manager.  

> [!TIP]  
>  Se si ha familiarità con le procedure per gestire le applicazioni in Configuration Manager, è possibile ignorare questo argomento e passare alla creazione di un'applicazione di esempio. Vedere [Creare e distribuire un'applicazione con System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Che cos'è un'applicazione?  
 Anche se *applicazione* è un termine ampiamente usato in informatica, in Configuration Manager indica un concetto diverso. Pensare a un'applicazione come a una scatola. Questa scatola contiene uno o più set di file di installazione per un pacchetto software (chiamato **tipo di distribuzione**) e le istruzioni su come distribuire il software.  

 Quando l'applicazione viene distribuita ai dispositivi, i **requisiti** stabiliscono il tipo di distribuzione installato nel dispositivo.  

 È possibile eseguire molte altre operazioni con un'applicazione. Altre informazioni su queste operazioni sono disponibili in questa guida. La tabella seguente introduce alcuni concetti che è necessario conoscere prima di avviare un'analisi più approfondita.  

|Concetto|Descrizione|    
|-|-|  
|**Requirements**|Nelle versioni precedenti di Configuration Manager spesso veniva creata una raccolta che conteneva i dispositivi in cui distribuire un'applicazione. Anche se è comunque possibile creare una raccolta, con i requisiti è possibile specificare criteri più dettagliati per la distribuzione di un'applicazione.<br /><br /> Ad esempio, è possibile indicare che un'applicazione può essere installata soltanto nei dispositivi che eseguono Windows 10. Quindi, l'applicazione potrà essere distribuita nei dispositivi, ma verrà installata solo nei dispositivi che eseguono Windows 10.<br /><br /> Configuration Manager valuta i requisiti per determinare se un'applicazione o uno dei tipi di distribuzione correlati verranno installati. Quindi, determina il tipo di distribuzione corretto usato per installare un'applicazione. Ogni sette giorni, per impostazione predefinita, le regole di requisiti vengono rivalutate per garantire la conformità in base all'impostazione client **Pianificare nuova valutazione per le distribuzioni**.<br /><br /> Per i dettagli, vedere [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md) (Creare e distribuire un'applicazione).|  
|**Condizioni globali**|I requisiti vengono usati con uno specifico tipo di distribuzione in una singola applicazione, ma è anche possibile creare delle condizioni globali, ossia una raccolta di requisiti predefiniti che è possibile usare con qualsiasi applicazione e tipo di distribuzione.<br /><br /> Configuration Manager contiene un set di condizioni globali predefinite e consente anche di creare set personalizzati.<br /><br /> Per i dettagli, vedere [Create global conditions](../../apps/deploy-use/create-global-conditions.md) (Creare condizioni globali).|  
|**Distribuzione simulata**|Valuta i requisiti, il metodo di rilevamento e le dipendenze di un'applicazione. Fornisce i risultati senza installare l'applicazione.<br /><br /> Per i dettagli, vedere [Simulate application deployments](../../apps/deploy-use/simulate-application-deployments.md) (Simulare distribuzioni di applicazioni).|  
|**Azione di distribuzione**|Specifica se installare o disinstallare (se l'operazione è supportata) l'applicazione che si sta distribuendo.<br /><br /> Per i dettagli, vedere [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Distribuire applicazioni).|  
|**Scopo della distribuzione**|Specifica se l'app di distribuzione sarà impostata su **Obbligatorio**o **Disponibile**.<br /><br /> **Richiesto**: l'applicazione viene distribuita automaticamente in base alla pianificazione configurata. Un utente può tuttavia tenere traccia dello stato della distribuzione, a meno che non sia nascosto, e può installare l'applicazione prima della scadenza usando Software Center.<br /><br /> **Disponibile** : se l'applicazione viene distribuita a un utente, l'utente visualizzerà l'applicazione pubblicata in Software Center e potrà installarla su richiesta.<br /><br /> Per i dettagli, vedere [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Distribuire applicazioni).|  
|**Revisioni**|Quando si eseguono revisioni a un'applicazione o a un tipo di distribuzione incluso in un'applicazione, Configuration Manager crea una nuova versione dell'applicazione. È possibile visualizzare la cronologia delle revisioni e le proprietà di ciascuna applicazione, ripristinare una versione precedente di un'applicazione oppure eliminare una versione precedente.<br /><br /> Per i dettagli, vedere [Update and retire applications](../../apps/deploy-use/update-and-retire-applications.md) (Aggiornare e ritirare applicazioni).|  
|**Metodo di rilevamento**|I metodi di rilevamento vengono usati per stabilire se un'applicazione distribuita è già installata. Se il metodo di rilevamento indica che l'applicazione è installata, Configuration Manager non prova a installarla nuovamente.<br /><br /> Per i dettagli, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).|  
|**Dipendenze**|Le dipendenze definiscono uno o più tipi di distribuzione da un'altra applicazione che deve essere installata prima dell'installazione di un tipo di distribuzione. È possibile configurare i tipi di distribuzione dipendenti per l'installazione automatica prima dell'installazione di un tipo di distribuzione.<br /><br /> Per i dettagli, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).|  
|**Sostituzione**|Configuration Manager consente di aggiornare o sostituire applicazioni esistenti usando una relazione di sostituzione. Quando si sostituisce un'applicazione, è possibile specificare un nuovo tipo di distribuzione che andrà a sostituire il tipo di distribuzione dell'applicazione sostituita. È anche possibile decidere se aggiornare o disinstallare l'applicazione sostituita prima di installare l'applicazione sostitutiva.<br /><br /> Per i dettagli, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).|  
|**Gestione incentrata sull'utente**|Le applicazioni di Configuration Manager supportano la gestione incentrata sull'utente, che consente di associare utenti specifici a dispositivi specifici. Invece di dover ricordare il nome del dispositivo di un utente, è possibile distribuire le app all'utente e al dispositivo. Questa funzionalità consente di verificare che le app più importanti siano sempre disponibili in ogni dispositivo a cui accede un utente specifico. Se un utente acquisisce un nuovo computer, è possibile installare automaticamente le app dell'utente nel dispositivo prima dell'accesso.<br /><br /> Per i dettagli, vedere [Link users and devices with user device affinity](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Collegare utenti e dispositivi tramite l'affinità utente-dispositivo).|  

## <a name="what-application-types-can-you-deploy"></a>Quali tipi di applicazione possono essere distribuiti?  
 Configuration Manager consente di distribuire i tipi di app seguenti:  

- Windows Installer (file *.msi)
- Pacchetto app Windows (*.appx, *.appxbundle)
- Pacchetto app Windows (in Windows Store)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization  5
- Windows Mobile Cabinet
- macOS  


Quando poi si gestiscono dispositivi tramite la gestione di dispositivi locale di Microsoft Intune o Configuration Manager, è possibile gestire anche questi tipi di applicazione:

- Pacchetto app Windows Phone (file *.xap)
- Pacchetto app per iOS (file *.ipa)
- Pacchetto app per Android (file *.apk)
- Pacchetto app Android in Google Play
- Pacchetto app Windows Phone (in Windows Phone Store)
- Windows Installer tramite MDM
- Applicazione Web



## <a name="state-based-applications"></a>Applicazioni basate sullo stato  
 Le applicazioni di Configuration Manager usano il monitoraggio basato sugli stati, che consente di tenere traccia dell'ultimo stato di distribuzione delle applicazioni per utenti e dispositivi. I messaggi di stato visualizzano informazioni sui singoli dispositivi. Ad esempio, se un'applicazione viene distribuita a una raccolta di utenti, è possibile visualizzare lo stato di conformità e lo scopo della distribuzione nella console di Configuration Manager. È possibile monitorare la distribuzione di tutti i software usando l'area di lavoro **Monitoraggio** nella console di Configuration Manager. Le distribuzioni software includono aggiornamenti software, impostazioni di conformità, applicazioni, sequenze attività e pacchetti e programmi. Per altre informazioni, vedere [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console) (Monitoraggio delle applicazioni).  

 Le distribuzioni di applicazioni vengono regolarmente sottoposte a valutazione da Configuration Manager. Ad esempio:  

-   un'applicazione distribuita viene disinstallata dall'utente finale. Al ciclo di valutazione successivo Configuration Manager rileva che l'applicazione non è presente e la reinstalla.  

-   Un'applicazione non è stata installata in un dispositivo poiché non soddisfa i requisiti. In seguito, viene apportata una modifica al dispositivo in modo che soddisfi i requisiti. Configuration Manager rileva la modifica apportata e l'applicazione viene installata.  


 È possibile impostare l'intervallo di rivalutazione per le distribuzioni delle applicazioni usando l'impostazione del client **Pianificare nuova valutazione per le distribuzioni**. Per altre informazioni, vedere [About client settings](../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client).  

## <a name="get-started-creating-an-application"></a>Introduzione alla creazione di un'applicazione  
 Per iniziare a creare subito un'applicazione semplice, usare la procedura dettagliata nell'argomento [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md) (Creare e distribuire un'applicazione).  

 Se si ha familiarità con le nozioni di base e si cercano informazioni di riferimento più dettagliate su tutte le opzioni disponibili, iniziare da [Create applications](/sccm/apps/deploy-use/create-applications) (Creare applicazioni).  

## <a name="software-center-and-the-application-catalog"></a>Software Center e Catalogo applicazioni  
 Nelle versioni precedenti di Configuration Manager per installare e pianificare le installazioni di software, configurare le impostazioni di controllo remoto e configurare le opzioni di risparmio energia veniva usato Software Center. Gli utenti potevano connettersi al Catalogo applicazioni per cercare e richiedere software, impostare alcune preferenze e cancellare in remoto i dati dei propri dispositivi mobili.  

 Anche se queste impostazioni sono ancora disponibili in System Center Configuration Manager, è ora disponibile una nuova versione di Software Center che consente di cercare le applicazioni. Non è necessario usare il Catalogo applicazioni, che richiede un Web browser abilitato per Silverlight. Tuttavia, i ruoli del sistema del sito del punto per siti Web del Catalogo applicazioni e del punto per servizi Web del Catalogo applicazioni continuano a essere necessari per visualizzare le app disponibili per gli utenti in Software Center.  

 Per altre informazioni, vedere [Plan for and configure application management](../../apps/plan-design/plan-for-and-configure-application-management.md) (Pianificare e configurare la gestione delle applicazioni).  

## <a name="configuration-manager-packages-and-programs"></a>Pacchetti e programmi di Configuration Manager  
 Configuration Manager continua a supportare pacchetti e programmi usati nelle versioni precedenti del prodotto. Una distribuzione che usa pacchetti e programmi può essere più adatta rispetto a una che usa un'applicazione quando si distribuisce uno degli elementi seguenti:  

-   Script che non installano un'applicazione su un computer, ad esempio uno script per deframmentare l'unità disco del computer.  

-   Script "One-off" che non è necessario monitorare costantemente.  

-   Script eseguiti in base a una pianificazione ricorrente e che non possono usare la valutazione globale.

 Per altre informazioni, vedere [Packages and programs](../../apps/deploy-use/packages-and-programs.md) (Pacchetti e programmi).  
