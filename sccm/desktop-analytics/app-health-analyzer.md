---
title: Analizzatore dell'integrità di App
titleSuffix: Configuration Manager
description: Guida alle procedure di valutazione della compatibilità con l'analizzatore dell'integrità di App in Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 122a27276adcaf57461157e9df03ee1092e52af5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755341"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>Come valutare la compatibilità con analizzatore dell'integrità di App

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Usare il toolkit di analizzatore dell'integrità di App per Desktop Analitica per valutare le app desktop per problemi di compatibilità. Consente di concentrare l'attenzione di convalida per le app desktop, incluse le app line-of-business. Lo strumento fornisce un livello di rischio e le azioni correttive possibili. Include anche un report di conformità app che consentono di valutare la conformità delle app per gli aggiornamenti di Windows 10. 



## <a name="download"></a>Download

Scaricare il toolkit dal [Microsoft Download Center](http://download.microsoft.com/download/3/7/D/37D7E378-D805-4822-A712-4EADBF50FC08/AppHealthAnalyzer.zip)<!-- (https://www.microsoft.com/download/details.aspx?id=57276) -->. Usare sempre la versione più recente.

Il download è un file Windows Installer (MSI). Installare il toolkit di analizzatore dell'integrità di App nel computer dell'utente. Quando si esegue il toolkit, una procedura guidata è il processo di creazione di un report di conformità app. 

Il toolkit include script di esempio. Se è necessario automatizzare la raccolta di informazioni di conformità dei dispositivi in tutta l'organizzazione, usare Configuration Manager per distribuire questi script. Per altre informazioni, vedere [automazione](#automation). 



## <a name="how-it-works"></a>Come funziona

Lo strumento esegue un'analisi statica di applicazioni che sono già installati in un dispositivo. Non esegue analisi di un programma di installazione di app del pacchetto. Un utente non è necessario eseguire l'app. Lo strumento consente di valutare tutte le applicazioni installate registrate con Windows nel dispositivo. 

Analizzatore dell'integrità di App non è necessario mantenere i programmi di installazione per le app legacy che non si gestiscono attivamente. Identifica i problemi di compatibilità con l'app nello stato installato. Tutte le app vengono valutate per le regole di compatibilità predefinito. Questi segnali sono comuni problemi più comuni segnalati a Microsoft quando i clienti di eseguire l'aggiornamento a Windows 10. Le informazioni di compatibilità includono anche le azioni correttive possibili o correzioni. Se si hanno App con problemi, iniziare con le azioni consigliate.

> [!Important]  
> Il toolkit non supporta funzionalità per ripristinare o correggere le tue app. Se si crea un report di conformità app, fornisce informazioni dettagliate e linee guida che consentono di monitorare e aggiornare le tue App prima dell'aggiornamento a Windows 10.  



## <a name="prerequisites"></a>Prerequisiti

Prima di installare e usando il toolkit, assicurarsi che il dispositivo soddisfi i requisiti seguenti:  

- Windows 7 Service Pack 1 o versione successivo  

- Si dispone dei privilegi di amministratore del dispositivo  

- Microsoft .NET Framework 4.5.1 o versioni successive  

- Registrazione nel servizio Analitica Desktop, che include i requisiti seguenti:  

    - Aggiornamenti più recenti. Per altre informazioni, vedere [aggiornare i dispositivi](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Livello di dati di diagnostica. Per altre informazioni, vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  



## <a name="analyze"></a>Analizzare 

1. Installare l'analizzatore dell'integrità di App nel dispositivo di destinazione. Per impostazione predefinita, viene installato nel percorso seguente: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. Passare a di Windows **avviare** menu, espandere il **analizzatore dell'integrità di Microsoft App** raggruppare e aprire il **analizzatore dell'integrità di App** come amministratore. Può richiedere alcuni minuti per generare il report.  

    > [!Note]  
    > Se le impostazioni necessarie i dati di diagnostica non sono configurate, si verrà visualizzato un errore. Accertarsi di che configurare correttamente le impostazioni dei prerequisiti. Per altre informazioni, vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

3. Quando si apre il report di conformità app, inizia la valutazione delle applicazioni. Attendere che il toolkit per il completamento, che può richiedere tempo a seconda del numero di applicazioni nel dispositivo.   

![Screenshot del report di conformità app dell'analizzatore dell'integrità di App](media/app-readiness-report-evaluating.png)

È possibile ridurre a icona la finestra e continuare con altre attività mentre il toolkit è in esecuzione in background.


### <a name="app-readiness-report-features"></a>Caratteristiche di report di conformità App

#### <a name="get-started"></a>Introduzione
Questa scheda offre una panoramica dei segnali supportati in questa versione corrente. Include anche le azioni correttive possibili. 

#### <a name="insights"></a>Insights
Questa scheda fornisce una visualizzazione di tutte le app di cui lo strumento di valutazione. Mostra la valutazione dei rischi e i segnali diversi usati per identificare i problemi di compatibilità. 

- **Segnali** menu: Filtrare le app tramite segnali usando il menu a sinistra  

- **Esporta CSV**: Esportare queste informazioni come file con valori delimitati da virgole (CSV)   

- **Ripeti analisi applicazioni**: Se si installano qualsiasi nuova applicazione, usare questa opzione per eseguire nuovamente lo strumento  

- **Risoluzione degli ID**: Se il dispositivo è installato l'App, ma viene non visualizzato alcun insights nel report, fornire questo ID per il supporto  

#### <a name="desktop-analytics"></a>Desktop Analytics
Questa scheda fornisce una panoramica del modo in cui è possibile usare analizzatore dell'integrità di App per offrire informazioni dettagliate dello stato di preparazione per le app nell'intera organizzazione.



## <a name="automation"></a>Automazione

Per ottenere queste informazioni sull'app su diversi dispositivi, distribuire la versione della riga di comando di analizzatore dell'integrità di App con Configuration Manager. Distribuire in un piccolo set di dispositivi rappresentativi all'interno dell'organizzazione. Ad esempio, usare il Desktop di Analitica *pilota* raccolta. Lo stesso [prerequisiti](#prerequisites) si applicano per questi dispositivi.


Prima di eseguire una distribuzione più ampia, verificare prima di tutto al completamento dell'esecuzione. Assicurarsi che i dati vengono visualizzati in Desktop Analitica. 

Il toolkit di analizzatore dell'integrità di App include uno script di esempio, run_silent.cmd. Per impostazione predefinita, questo script è nel percorso seguente: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`. Usare questo script per automatizzare il processo con Configuration Manager.


### <a name="tips"></a>Suggerimenti

- Prima dell'aggiornamento al sistema operativo di destinazione, distribuire l'analizzatore dell'integrità di App a tutti i dispositivi nel progetto pilota. Per ottenere informazioni dettagliate di conformità effettivo, eseguirla almeno una volta nel gruppo di pilota per un piano di distribuzione.  

- Analitica desktop ha una funzionalità integrata per consigliare gruppi progetto pilota per piani di distribuzione. Eseguire il toolkit in tutti i dispositivi pilota per ottenere una copertura completa per le app importanti.  

- Pianificare lo strumento da eseguire quando un utente non è connesso o se non si usa il dispositivo.  

- Configurare una pianificazione ricorrente. Ad esempio, eseguirlo ogni 30 giorni. Questa pianificazione Ottiene le informazioni di conformità più recenti dai dispositivi per aiutarli a essere sempre aggiornati.  



## <a name="desktop-analytics-integration"></a>Integrazione Analitica desktop

Lo screenshot seguente del Desktop Analitica Mostra i dettagli di ContosoApp versione 1.15.25. 
- Ha un **Medium** valutazione dei rischi  
- È disponibile una versione adottata  
- E presenta una dipendenza di driver  

![Desktop Analitica che mostra i fattori di rischio di compatibilità di un'app](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>Troubleshooting

Questa sezione descrive i passaggi di risoluzione dei problemi e problemi operativi più comuni che potrebbe essere visualizzato con analizzatore dell'integrità di App. Ad esempio:

- Non è visualizzato la schermata iniziale in analizzatore dell'integrità di App  

- Sono disponibili le app installate nel dispositivo, ma non viene visualizzato nel report di conformità app alcun insights  

- Non accade nulla quando si esegue lo strumento  


#### <a name="diagnostic-data-settings"></a>Impostazioni di dati di diagnostica
Verificare le configurazioni per le impostazioni di dati di diagnostica di Windows. Configuration Manager deve impostare questi valori quando il dispositivo esegue l'onboarding ad Analitica Desktop. È possibile usare altri metodi, ad esempio criteri di gruppo o script come soluzione alternativa. Per altre informazioni, vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

#### <a name="verbose-mode"></a>Modalità dettagliata
Eseguire lo strumento in modalità dettagliata con lo script run_verbose.cmd. Per impostazione predefinita, lo script è nel percorso seguente: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

La modalità dettagliata genera i log, che possono aiutarti a risolvere i problemi potenziali. Salva i log per il `LogCollection` cartella nel percorso di installazione. Ad esempio, il percorso di raccolta log predefinito è: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`

<!--Send the logs to AHASupport, who will follow up for further investigations. --do we really want to include this in public documentation?-->

