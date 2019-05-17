---
title: Monitorare gli aggiornamenti software
titleSuffix: Configuration Manager
description: La console di System Center Configuration Manager invia avvisi e stati per monitorare gli aggiornamenti e la conformità.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cd5c27aa04f25b044f74533983a214dc9f9341b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500146"
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Monitorare gli aggiornamenti software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager offre vari modi per monitorare aggiornamenti software, processi e informazioni sulla conformità. Usare le sezioni seguenti per monitorare gli aggiornamenti software.

## <a name="software-updates-dashboard"></a>Dashboard Aggiornamenti software
A partire da Configuration Manager versione 1610, è possibile usare il nuovo dashboard Aggiornamenti software per visualizzare lo stato di conformità corrente dei dispositivi dell'organizzazione e analizzare rapidamente i dati, per vedere quali dispositivi sono a rischio. Per visualizzare il dashboard, scegliere **Monitoraggio** > **Panoramica** > **Sicurezza** > **Software Updates Dashboard** (Dashboard Aggiornamenti software).   

##  <a name="BKMK_SUAlerts"></a> Avvisi per gli aggiornamenti software  
 È possibile configurare avvisi per gli aggiornamenti software per inviare notifiche agli utenti amministratori quando i livelli di conformità per le distribuzioni degli aggiornamenti software sono al di sotto della percentuale configurata. È possibile configurare avvisi per gli aggiornamenti software nei seguenti punti:  

-   Impostazione ADR: è possibile configurare le impostazioni degli avvisi nella Creazione guidata delle regole di distribuzione automatica e nelle proprietà per ADR.  

-   Impostazione di distribuzione: è possibile configurare le impostazioni degli avvisi nella Distribuzione guidata degli aggiornamenti software e nelle proprietà di distribuzione.  

Dopo aver configurato le impostazioni degli avvisi, Configuration Manager genera un avviso se si verificano le condizioni specificate. È possibile esaminare gli avvisi per gli aggiornamenti software nei seguenti punti:  

1.  Gli avvisi recenti sono reperibili nel nodo **Aggiornamenti software** dell'area di lavoro **Raccolta software** .  

2.  Gli avvisi configurati possono essere gestiti nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** .  

##  <a name="BKMK_SUSyncStatus"></a> Stato di sincronizzazione degli aggiornamenti software  
 Dopo aver avviato il processo di sincronizzazione, è possibile monitorarlo dalla console di Configuration Manager per tutti i punti di aggiornamento software della gerarchia. Usare la seguente procedura per monitorare il processo di sincronizzazione degli aggiornamenti software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Per monitorare il processo di sincronizzazione degli aggiornamenti software  

- Nella console di Configuration Manager, passare a **Monitoraggio** > **Panoramica** > **Stato di sincronizzazione del punto di aggiornamento software**.  

    I punti di aggiornamento software nella gerarchia di Configuration Manager vengono visualizzati nel riquadro dei risultati. In questa vista è possibile monitorare lo stato di sincronizzazione per tutti i punti di aggiornamento software. Per visualizzare informazioni più dettagliate sul processo di sincronizzazione, è possibile esaminare il file wsyncmgr.log disponibile in <*PercorsoInstallazioneConfigurationManager*>\Logs di ogni server del sito.  

##  <a name="BKMK_SUDeployStatus"></a> Stato di distribuzione degli aggiornamenti software  
 Dopo aver distribuito un aggiornamento software singolo o un gruppo di aggiornamenti software, è possibile monitorare lo stato della distribuzione. Usare la procedura seguente per monitorare lo stato della distribuzione di un aggiornamento software o di un gruppo di aggiornamenti software.  

#### <a name="to-monitor-deployment-status"></a>Per monitorare lo stato di distribuzione  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Distribuzioni**.  

2.  Fare clic sull'aggiornamento software o sul gruppo di aggiornamenti software del quale si desidera monitorare lo stato di distribuzione.  

3.  Nella scheda **Home** fare clic su **Visualizza stato** nel gruppo **Distribuzione**.  

##  <a name="BKMK_SUReports"></a> Report degli aggiornamenti software  
 I messaggi di stato per gli aggiornamenti software offrono informazioni sulla conformità degli aggiornamenti software e sullo stato di valutazione e applicazione delle distribuzioni di aggiornamenti software. Per visualizzare tali messaggi di stato, è possibile eseguire i report degli aggiornamenti software. Sono disponibili oltre 30 report degli aggiornamenti software predefiniti. Sono organizzati in diverse categorie e forniscono informazioni specifiche sugli aggiornamenti e le distribuzioni di software. Oltre a usare i report preconfigurati, è anche possibile creare report degli aggiornamenti software personalizzati in base alle esigenze dell'azienda. Per altre informazioni, vedere [Operazioni e manutenzione per la creazione di report](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Report degli aggiornamenti software consigliati
Di seguito sono riportati alcuni dei report utili per identificare potenziali problemi. 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Conformità 9 - Dati complessivi su integrità e conformità (a partire dalla versione 1806)
Il report include le parti seguenti:

- **Healthy Clients vs Total Clients** (Client integri rispetto a totale client): questo grafico a barre confronta i client "integri" che hanno comunicato con il sito nel periodo di tempo specificato rispetto al numero totale di client nella raccolta specificata.
- **Compliance Overview** (Panoramica conformità): grafico a torta che mostra lo stato di conformità generale per il gruppo di aggiornamenti software specifico nei client attivi nella raccolta specificata.
- **Top 5 Non-Compliant by Article ID** (Primi 5 non conformi in base a ID articolo): questo grafico a barre visualizza i primi cinque aggiornamenti software nel gruppo specificato che non sono conformi nei client attivi nella raccolta specificata.
- La parte inferiore del report è una tabella con altri dettagli, in cui sono elencati gli aggiornamenti software nel gruppo specificato.

#### <a name="management-2---updates-required-but-not-deployed"></a>Gestione 2 - Aggiornamenti richiesti ma non distribuiti

Questo report mostra gli aggiornamenti software specifici del fornitore in una determinata classificazione degli aggiornamenti che sono stati rilevati come richiesti nei client ma non sono stati distribuiti in una raccolta specifica. 

#### <a name="troubleshooting-2---deployment-errors"></a>Risoluzione dei problemi 2 - Errori di distribuzione

Questo report restituisce gli errori di distribuzione nel sito e un conteggio dei computer in cui ogni errore viene riscontrato. 


##  <a name="BKMK_MonitorContent"></a> Monitoraggio del contenuto  
 È possibile monitorare il contenuto nella console di Configuration Manager per verificare lo stato di tutti i tipi di pacchetti in relazione ai punti di distribuzione associati. Sono inclusi lo stato di convalida del contenuto del pacchetto, lo stato del contenuto assegnato a un gruppo di punti di distribuzione specifico, lo stato del contenuto assegnato a un punto di distribuzione e lo stato di funzionalità facoltative per ogni punto di distribuzione (convalida contenuto, PXE e multicast).  

###  <a name="BKMK_ContentStatus"></a> Monitoraggio dello stato del contenuto  
 Il nodo **Stato componente** dell'area di lavoro **Monitoraggio** fornisce informazioni sui pacchetti contenuto. È possibile esaminare le informazioni generali sul pacchetto, lo stato di distribuzione del pacchetto e informazioni dettagliate sullo stato del pacchetto. Usare la procedura seguente per visualizzare lo stato del contenuto.  

#### <a name="to-monitor-content-status"></a>Per monitorare lo stato del contenuto  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Stato distribuzione** > **Stato contenuto**. Vengono visualizzati i pacchetti.  

2.  Selezionare il pacchetto di cui visualizzare informazioni dettagliate sullo stato.  

3.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate informazioni dettagliate sullo stato per il pacchetto.  

###  <a name="BKMK_DPGroupStatus"></a> Stato del gruppo di punti di distribuzione  
 Il nodo **Stato gruppo di punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sui gruppi di punti di distribuzione. È possibile esaminare informazioni generali sul gruppo di punti di distribuzione, quali lo stato, il grado di conformità e le informazioni dettagliate sullo stato. Usare la procedura seguente per visualizzare lo stato del gruppo di punti di distribuzione.  

#### <a name="to-monitor-distribution-point-group-status"></a>Per monitorare lo stato del gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Stato distribuzione** > **Stato gruppo di punti di distribuzione**. Vengono visualizzati i gruppi di punti di distribuzione.  

2.  Selezionare il gruppo di punti di distribuzione di cui visualizzare informazioni dettagliate sullo stato.  

3.  Nella scheda **Home** fare clic su **Visualizza stato**. Vengono visualizzate le informazioni dettagliate sullo stato per il gruppo di punti di distribuzione.  

###  <a name="BKMK_DPConfigStatus"></a> Stato di configurazione dei punti di distribuzione  
 Il nodo **Stato di configurazione dei punti di distribuzione** nell'area di lavoro **Monitoraggio** fornisce informazioni sul punto di distribuzione. È possibile esaminare gli attributi abilitati per il punto di distribuzione, come PXE, Multicast e convalida del contenuto. È inoltre possibile visualizzare informazioni dettagliate sullo stato per il punto di distribuzione. Usare la procedura seguente per visualizzare lo stato di configurazione del punto di distribuzione.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Per monitorare lo stato di configurazione del punto di distribuzione  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Stato distribuzione** > **Stato di configurazione dei punti di distribuzione**. Vengono visualizzati i punti di distribuzione.  

2.  Selezionare il punto di distribuzione per il quale si desidera visualizzare le informazioni sullo stato.  

3.  Nel riquadro dei risultati fare clic sulla scheda **Dettagli** . Verranno visualizzate le informazioni sullo stato per il punto di distribuzione.  
