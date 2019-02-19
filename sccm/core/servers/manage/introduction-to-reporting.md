---
title: Introduzione ai report
titleSuffix: Configuration Manager
description: Informazioni sui set di strumenti e risorse disponibili per la gestione della creazione di report in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 760b159114796922e2c8707e3b7f14484591f7a2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141494"
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Introduzione ai report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La creazione di report in System Center Configuration Manager offre un set di strumenti e risorse che consente di usare le funzionalità avanzate di creazione di report di SQL Server Reporting Services (SSRS), con l'esperienza completa offerta da Generatore report di Reporting Services. La creazione di report consente di raccogliere, organizzare e presentare le informazioni relative agli utenti, all'inventario software e hardware, agli aggiornamenti software, alle applicazioni, allo stato del sito e alle altre operazioni di Configuration Manager all'interno dell'organizzazione. La creazione di report fornisce un numero di report predefiniti che è possibile utilizzare senza modifiche oppure modificare per soddisfare i requisiti ed è possibile creare report personalizzati. Le sezioni seguenti agevolano la pianificazione della creazione di report in Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services fornisce una gamma completa di strumenti e servizi pronti all'uso per creare, distribuire e gestire report per l'azienda e funzionalità di programmazione che consentono di estendere e personalizzare la funzionalità di creazione di report. Reporting Services è una piattaforma per la creazione di report basata su server che fornisce funzionalità di creazione di report complete per una vasta gamma di origini dati.  

 Configuration Manager usa SQL Server Reporting Services come soluzione per la creazione di report. L'integrazione con Reporting Services offre i seguenti vantaggi:  

- Usa un sistema di creazione di report standard di settore per eseguire query nel database di Configuration Manager.  

- Visualizza i report usando Visualizzatore report di Configuration Manager oppure Gestione report, che è una connessione al report basata su Web.  

- Fornisce scalabilità, disponibilità e prestazioni elevate.  

- Fornisce agli utenti sottoscrizioni ai report; ad esempio, un manager può eseguire una sottoscrizione per ricevere automaticamente tramite posta elettronica un report con i dettagli dello stato dell'implementazione di un aggiornamento software.  

- Esporta report che gli utenti possono selezionare in una gamma dei formati più diffusi.  

  Per ulteriori informazioni su Reporting Services, vedere [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) nella documentazione online di SQL Server 2008.  

##  <a name="BKMK_ReportingServicesPoint"></a> Punto di Reporting Services  
 Il punto di Reporting Services è un ruolo del sistema del sito installato su un server che esegue Microsoft SQL Server Reporting Services. Il punto di Reporting Services copia le definizioni report di Configuration Manager in Reporting Services, crea cartelle report basate sulle categorie report e imposta criteri di sicurezza per le cartelle report e i report basati sulle autorizzazioni basate su ruoli per gli utenti amministratori di Configuration Manager. In un intervallo di 10 minuti, il punto di Reporting Services si collega a Reporting Services per riapplicare i criteri di protezione se sono stati modificati, ad esempio utilizzando la Gestione report. Per ulteriori informazioni su come pianificare e installare un punto di Reporting Services, vedere la seguente documentazione:  

-   [Planning for reporting in System Center Configuration Manager](planning-for-reporting.md) (Pianificazione per la creazione di report in System Center Configuration Manager)  

-   [Configuring reporting in System Center Configuration Manager](configuring-reporting.md) (Configurazione della creazione di report in System Center Configuration Manager)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Report di Configuration Manager  
 Configuration Manager fornisce le definizioni di oltre 400 report in oltre 50 cartelle report, che vengono copiate nella cartella report radice di SQL Server Reporting Services durante il processo di installazione del punto di Reporting Services. I report vengono visualizzati nella console di Configuration Manager e organizzati in sottocartelle in base alla categoria. I report non vengono propagati nella gerarchia di Configuration Manager in alcuna direzione, ma vengono eseguiti solo per il database del sito in cui vengono creati. Tuttavia, poiché Configuration Manager replica i dati globali in tutta la gerarchia, è possibile accedere alle informazioni a livello di gerarchia. Quando un report recupera dati dal database di un sito, ha accesso ai dati del sito per il sito corrente e i relativi siti figlio e ai dati globali per ciascun sito della gerarchia. Come altri oggetti di Configuration Manager, per eseguire o modificare report un utente amministratore deve disporre delle autorizzazioni appropriate. Per eseguire un report, è necessario che un utente amministratore disponga dell'autorizzazione **Esegui report** per l'oggetto. Per creare o modificare un report, è necessario che un utente amministratore disponga dell'autorizzazione **Modifica report** per l'oggetto.  

###  <a name="BKMK_CreatingReports"></a> Creazione e modifica di report  
 Configuration Manager usa Generatore report di Microsoft SQL Server come strumento esclusivo di creazione e modifica sia per i report basati su modello che per quelli basati su SQL. Quando si crea o si modifica un report nella console di Configuration Manager, viene aperto Generatore report. Per altre informazioni sulla gestione dei report, vedere [Operazioni e manutenzione per la creazione di report in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Esecuzione di report  
 Quando si esegue un report nella console di Configuration Manager, il Visualizzatore report si apre e si collega a Reporting Services. Dopo aver specificato tutti i parametri di report richiesti, Reporting Services recupera i dati e visualizza i risultati nel Visualizzatore. È possibile inoltre connettersi a SQL Services Reporting Services, connettersi all'origine dati per il sito ed eseguire i report.  

###  <a name="BKMK_ReportPrompts"></a> Richieste di report  
 Una richiesta o un parametro di report in Configuration Manager è una proprietà dei report che è possibile configurare quando si crea o si modifica un report. Le richieste di report vengono create per limitare o assegnare i dati che recupera un report. Un report può contenere più di una richiesta purché i nomi richiesta siano univoci e contengano solo caratteri alfanumerici conformi alle regole SQL Server per identificatori.  

 Quando si esegue un report, la richiesta richiede un valore per un parametro obbligatorio e, in base al valore, recupera i dati del report. Ad esempio, il report **Informazioni computer per un computer specifico** recupera le informazioni computer per un computer specifico e richiede l'utente amministratore per un nome computer. Reporting Services passa il valore specificato per una variabile definita nell'istruzione SQL per il report.  

###  <a name="BKMK_ReportLinks"></a> Collegamenti ai report  
 I collegamenti al report in Configuration Manager vengono usati in un report di origine per fornire agli utenti amministratori un accesso semplice a dati aggiuntivi, ad esempio informazioni più dettagliate su ognuno degli elementi del report di origine. Se il report di destinazione richiede uno o più richieste da eseguire, il report di origine deve contenere una colonna con i valori appropriati per ciascuna richiesta. È necessario specificare il numero della colonna che fornisce il valore per la richiesta. Ad esempio, è possibile collegare un report che elenca i computer che sono stati individuati di recente a un report che elenca gli ultimi messaggi ricevuti per un computer specifico. Quando viene creato il collegamento, è possibile specificare che la colonna 2 nel report di origine contiene i nomi computer, cosa che costituisce una richiesta obbligatoria per il report di destinazione. Quando viene eseguito il report di origine, vengono visualizzate le icone dei collegamenti a sinistra di ogni riga di dati. Quando si fa clic sull'icona in una riga, il Visualizzatore report passa il valore nella colonna specificata per tale riga come valore di richiesta che è necessario per visualizzare il report di destinazione. Un report può essere configurato con un solo collegamento e tale collegamento può connettersi solo a una risorsa unica di destinazione.  

> [!WARNING]  
>  Se si sposta un report di destinazione in una cartella report diversa, cambia il percorso del report di destinazione. Il collegamento del report nel report di origine non viene automaticamente aggiornato con il nuovo percorso e il collegamento del report non funzionerà nel report di origine.  

##  <a name="BKMK_ReportFolders"></a> Cartelle report  
 Le cartelle report in System Center Configuration Manager costituiscono un metodo per ordinare e filtrare i report archiviati in Reporting Services. Le cartelle report sono particolarmente utili quando si devono gestire numerosi report. Quando si installa un punto di Reporting Services, i report vengono copiati in Reporting Services e organizzati in più di 50 cartelle report. Le cartelle report sono di sola lettura. Non è possibile modificarle nella console di Configuration Manager.  

##  <a name="BKMK_ReportSubscriptions"></a> Sottoscrizioni report  
 Una sottoscrizione report in Reporting Services è una richiesta ricorrente per recapitare un report a un orario specifico o in risposta a un evento e in un formato file applicazione che viene specificato nella sottoscrizione. Le sottoscrizione forniscono un'alternativa all'esecuzione di un report su richiesta. La creazione di report su richiesta richiede la selezione attiva del report ogni volta che si desidera visualizzare il report. Al contrario, le sottoscrizioni possono essere utilizzate per pianificare e quindi automatizzare il recapito di un report.  

 È possibile gestire le sottoscrizioni report nella console di Configuration Manager. Vengono elaborate nel server di report. Le sottoscrizioni vengono distribuite utilizzando le estensioni per il recapito distribuite nel server. Per impostazione predefinita, è possibile creare sottoscrizioni che inviano report a una cartella condivisa o a un indirizzo di posta elettronica. Per altre informazioni sulla gestione delle sottoscrizioni report, vedere [Operazioni e manutenzione per la creazione di report in System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Generatore report  
 Configuration Manager usa Generatore report di Microsoft SQL Server Reporting Services come strumento esclusivo di creazione e modifica per i report basati su modello e per quelli basati su SQL. Quando si avvia l'azione per creare o modificare un report nella console di Configuration Manager, si apre Generatore report. Generatore report viene installato automaticamente quando si crea o si modifica un report per la prima volta. Quando si eseguono o modificano report viene aperta la versione di Generatore report associata alla versione installata di SQL Server.  

 L'installazione di Generatore report aggiunge il supporto per più di 20 lingue. Quando si esegue Generatore report, i dati vengono visualizzati nella lingua del sistema operativo in esecuzione sul computer locale. Se Generatore report non supporta la lingua, i dati vengono visualizzati in inglese. Generatore report supporta tutte le funzionalità di SQL Server 2008 Reporting Services, tra cui:  

- Offre un ambiente di creazione report intuitivo con un aspetto simile a Microsoft Office.  

- Offre il layout report flessibile di SQL Server 2008 Report Definition Language (RDL).  

- Offre vari moduli di visualizzazione dei dati, compresi grafici e indicatori.  

- Fornisce caselle di testo con formattazione completa.  

- Effettua l'esportazione in formato Microsoft Word.  

  È inoltre possibile aprire Generatore report da SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Modelli di report in SQL Server Reporting Services  
 SQL Reporting Services in Configuration Manager usa modelli di report per consentire agli utenti amministratori di selezionare dal database elementi da includere nei report basati su modello. Per l'utente amministratore che crea il report, i modelli di report mostrano solo visualizzazioni ed elementi specifici da selezionare. Per creare report basati su modello, deve essere disponibile almeno un modello. I modelli di report dispongono delle seguenti funzionalità:  

- È possibile assegnare campi di database e visualizzazioni con nomi aziendali logici per facilitare la produzione di report. Non è necessario conoscere la struttura del database per la produzione di report.  

- È possibile raggruppare logicamente gli elementi.  

- È possibile definire relazioni tra elementi.  

- È possibile proteggere gli elementi del modello in modo che gli utenti amministrativi possano vedere solo i dati che sono autorizzati a vedere.  

  Nonostante Configuration Manager fornisca modelli di report campione, è anche possibile definire modelli di report per soddisfare i requisiti della propria azienda. Per altre informazioni su come creare modelli di report, vedere [Creazione di modelli di report personalizzati per System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## <a name="next-steps"></a>Passaggi successivi
[Pianificazione della creazione di report](planning-for-reporting.md)
