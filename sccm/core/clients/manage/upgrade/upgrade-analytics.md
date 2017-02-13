---
title: Upgrade Analytics | System Center Configuration Manager
description: "Integrare Upgrade Analytics con Configuration Manager. Accedere ai dati di compatibilità dell&quot;aggiornamento nella console di amministrazione. Definire i dispositivi di destinazione per l&quot;aggiornamento o la correzione."
keywords: 
author: nbigman
ms.author: nbigman
manager: angerobe
ms.date: 11/23/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
translationtype: Human Translation
ms.sourcegitcommit: bf28164fc2594d2557db5626a6f52c32ad99a1fe
ms.openlocfilehash: fa90fa0da348e7cca186ff8066c7a9fa98c57cf5


---

# <a name="integrate-upgrade-analytics-with-system-center-configuration-manager"></a>Integrare Upgrade Analytics con System Center Configuration Manager

Upgrade Analytics consente di valutare e analizzare la leggibilità e la compatibilità dei dispositivi con Windows 10, per facilitare l'esecuzione degli aggiornamenti. Integrare Upgrade Analytics con Configuration Manager per accedere ai dati di compatibilità dell'aggiornamento dei client nella console di amministrazione di Configuration Manager. Sarà quindi possibile impostare i dispositivi di destinazione dell'aggiornamento o della correzione dall'elenco dei dispositivi.

Upgrade Analytics è una soluzione di Microsoft Operations Management Suite (OMS). Per altre informazioni su Upgrade Analytics, vedere in [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introduzione a Upgrade Analytics).

## <a name="configure-clients"></a>Configurare i client

È necessario eseguire varie operazioni di configurazione per garantire che i client siano in grado di offrire dati a Upgrade Analytics:

-  Configurare le impostazioni di telemetria client, come descritto in [Configurare la telemetria di Windows nell'organizzazione](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Installare gli aggiornamenti descritti nella sezione *Deploy the compatibility update and related KBs* (Distribuire l'aggiornamento di compatibilità e gli aggiornamenti associati) di [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introduzione a Upgrade Analytics).

    > [!NOTE]
    > È possibile scaricare uno script per automatizzare molte attività di installazione client. Per informazioni sullo script, vedere la sezione *Run the Upgrade Analytics deployment script* (Eseguire lo script di distribuzione di Upgrade Analytics) di [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introduzione a Upgrade Analytics).

## <a name="create-a-connection-to-upgrade-analytics"></a>Creare una connessione a Upgrade Analytics

### <a name="prerequisites"></a>Prerequisiti

- Per l'aggiunta della connessione, è necessario che nell'ambiente di Configuration Manager sia stato configurato un [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in [modalità online](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quando si aggiunge la connessione all'ambiente, viene installato anche Microsoft Monitoring Agent nel computer che esegue questo ruolo del sistema del sito.
- Registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web" e ottenere l'[ID client della registrazione](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Creare una chiave client per lo strumento di gestione registrato in Azure Active Directory.
- Nel portale di gestione di Azure specificare l'autorizzazione di accesso OMS per l'app Web registrata, come descritto in [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quando si configura l'autorizzazione per accedere a OMS, assicurarsi di scegliere il ruolo **Collaboratore** e di assegnare a tale ruolo le autorizzazioni per il gruppo di risorse dell'app registrata.

### <a name="create-the-connection"></a>Creare la connessione

1.  Nella console di Configuration Manager, scegliere **Amministrazione** > **Servizi cloud** > **Upgrade Analytics Connector (Connettore Upgrade Analytics)** > **Crea connessione ad Upgrade Analytics** per avviare **Aggiungi la connessione guidata a Upgrade Analytics**.
3.  Nella schermata **Azure Active Directory**, specificare valori per **Tenant**, **ID client ** e **Client Secret Key** (Chiave privata client), quindi selezionare **Avanti**.
4.  Nella schermata **Upgrade Analytics** specificare le impostazioni di connessione in **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.
5.  Verificare le impostazioni di connessione nella schermata **Riepilogo** e selezionare **Avanti**.

    > [!NOTE]
    > È necessario che Upgrade Analytics sia connesso al sito di livello più alto nella gerarchia. Se si connette Upgrade Analytics a un sito primario autonomo e poi si aggiunge un sito di amministrazione centrale all'ambiente, è necessario eliminare e ricreare la connessione di OMS nella nuova gerarchia.

### <a name="complete-upgrade-analytics-tasks"></a>Completare le attività di Upgrade Analytics  

Dopo aver creato la connessione in Configuration Manager, eseguire queste attività, come descritto in [Get started with Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started) (Introduzione a Upgrade Analytics).  

1. Aggiungere il servizio UpgradeAnalytics all'area di lavoro OMS.  
2. Generare un ID commerciale.  
3. Effettuare la sottoscrizione a Upgrade Analytics.   

## <a name="use-the-upgrade-analytics-deployment-script"></a>Usare lo script di distribuzione di Upgrade Analytics  

È possibile automatizzare molte attività di Upgrade Analytics e risolvere i problemi di condivisione con lo **script di distribuzione di Microsoft Upgrade Analytics**.  
Lo script di distribuzione di Upgrade Analytics esegue le operazioni seguenti:  

- Imposta la chiave ID commerciale e le chiavi CommercialDataOptIn e RequestAllAppraiserVersions.  
- Verifica che i computer degli utenti siano in grado di inviare dati a Microsoft.  
- Controlla se il computer è in attesa di riavvio.   
- Verifica che sia installata la versione più recente del pacchetto KB 10.0 (richiede la versione 10.0.14348 o versioni successive).  
- Se abilitata, attiva la modalità dettagliata per la risoluzione dei problemi.  
- Avvia la raccolta dei dati di telemetria necessari a Microsoft per valutare il grado di preparazione dell'organizzazione per l'aggiornamento.  
- Se abilitata, consente la visualizzazione dello stato dello script in una finestra di comando, offrendo visibilità per i problemi (esito positivo o negativo per ogni passaggio) e/o le operazioni di scrittura nel file di registro.  
  
### <a name="to-run-the-upgrade-analytics-deployment-script"></a>Per eseguire lo script di distribuzione di Upgrade Analytics:  
  
1. Scaricare lo [script di distribuzione di Upgrade Analytics](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) ed estrarre UpgradeAnalytics.zip. I file nella cartella **Diagnostics** sono necessari solo se si prevede di eseguire lo script in modalità di risoluzione dei problemi.  
2. Modificare i seguenti parametri in RunConfig.bat:  
- Percorso di archiviazione per le informazioni del registro. Esempio: % SystemDrive%\UADiagnostics. È possibile archiviare le informazioni del registro in una condivisione file remota o in una directory locale. Se lo script non può creare il file di registro per il percorso specificato, lo crea nell'unità che include la directory di Windows.  
- Chiave ID commerciale.  
- Per impostazione predefinita, lo script invia informazioni di registro sia alla console sia al file di registro. Per modificare il comportamento predefinito, usare una delle opzioni seguenti:  
    - logMode = 0 - Registrazione solo nella console  
    - logMode = 1 - Registrazione nel file e nella console  
    - logMode = 2 - Registrazione solo nel file  
    - Per la risoluzione dei problemi, impostare **isVerboseLogging** su **$true** per generare informazioni di registro che possono facilitare la diagnosi dei problemi. Per impostazione predefinita, **isVerboseLogging** è impostata su **$false**. Per usare questa modalità, verificare che la cartella Diagnostics sia installata nella stessa directory dello script.  
    - Notificare agli utenti se è necessario riavviare il computer. Per impostazione predefinita, questa opzione è disattivata.  
  
3. Dopo aver completato la modifica dei parametri in RunConfig.bat, eseguire lo script come amministratore.  
  
  
## <a name="view-microsoft-upgrade-analytics-properties-in-configuration-manager"></a>Visualizzare le proprietà di Microsoft Upgrade Analytics in Configuration Manager  
  
1.  Nella console di Configuration manager, passare a **Servizi cloud** e selezionare **Connettore OMS** per aprire la pagina **OMS Connection Properties** (Proprietà connessione OMS).  

2.  In questa pagina sono disponibili due schede:
  * La scheda **Azure Active Directory** visualizza **Tenant**, **ID client** e **Client secret key expiration** (Scadenza chiave privata del client) e consente la **Verifica** della **Chiave privata del client** se è scaduta.
  * La scheda **Upgrade Analytics** visualizza **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Visualizzare e usare le informazioni sull'aggiornamento

Dopo il completamento dell'integrazione di Upgrade Analytics con Configuration Manager, è possibile visualizzare l'analisi di preparazione dell'aggiornamento dei client ed eseguire le azioni necessarie.

1. Nella console di Configuration Manager, scegliere **Monitoraggio** > **Panoramica** > **Upgrade Analytics**.
2. Esaminare i dati, che includono lo stato di preparazione per l'aggiornamento e la percentuale di dispositivi Windows che eseguono report di telemetria.
3. È possibile filtrare il dashboard per visualizzare i dati di dispositivi appartenenti a raccolte specifiche.
4. È anche possibile visualizzare i dispositivi in uno stato di conformità specifico e creare una raccolta dinamica per tali dispositivi, in modo da poterli aggiornare quando sono pronti o da portarli allo stato di conformità desiderato.



<!--HONumber=Dec16_HO3-->

