---
title: Risolvere i problemi di integrazione con MSfB
titleSuffix: Configuration Manager
description: Fornisce suggerimenti e soluzioni per risolvere alcuni dei problemi più comuni con Microsoft Store per l'integrazione aziendale e dell'istruzione.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e8f59e874d89bcb64d3331d40ef044c4c8beb01
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74814278"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Risolvere i problemi relativi all'integrazione di Microsoft Store for business e Education con Configuration Manager

Questo articolo fornisce suggerimenti e correzioni principali per la risoluzione dei problemi che si possono avere con l'integrazione di Microsoft Store for Business and Education (MSfB) con Configuration Manager.

Per ulteriori informazioni sull'utilizzo di Microsoft Store for business e Education con Configuration Manager, vedere la pagina relativa alla [gestione delle app da Microsoft Store for business e Education con Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

## <a name="monitor"></a>Monitoraggio

### <a name="component-status"></a>Stato componente

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato componente**. Monitorare lo stato dei componenti seguenti:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Stato di sincronizzazione

Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**. Controllare la colonna **stato ultima sincronizzazione** .

### <a name="view-synchronized-apps"></a>Visualizza app sincronizzate

Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione applicazioni** e selezionare il nodo **Informazioni di licenza per le app dello Store**.


## <a name="log-files"></a>File di registro

### <a name="msfbsyncworkerlog"></a>MSfBSyncWorker.log

Questo file di log si trova nel punto di connessione del servizio, in `\Logs` nella directory di installazione Configuration Manager. Registra le informazioni sulla comunicazione con il servizio cloud. Queste informazioni includono metadati, icone, pacchetti e recupero di file di licenza.

Per modificare il livello di registrazione, modificare il valore di `LoggingLevel` in `0` nella chiave del registro di sistema `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION`. Per altre informazioni, vedere [configurare le opzioni di registrazione](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

Questo file di log si trova nel punto di connessione del servizio, in `\Logs` nella directory di installazione Configuration Manager. Se il servizio MSfBSyncWorker non è avviato o viene avviato e interrotto ripetutamente, rivedere le voci del file di log.

> [!NOTE]
> Questo file di log è condiviso con altre funzionalità.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

Questo file di log si trova nel server del sito per il sito di livello superiore nella gerarchia. È sotto `\Logs` nella directory di installazione Configuration Manager. Registra le informazioni sui processi seguenti:

- Inserire le informazioni sui metadati sincronizzate dal componente BusinessAppProcessWorker nel database
- Elaborare i file in `\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

Questo file di log si trova nel server del sito per il sito di livello superiore nella gerarchia. È sotto `\Logs` nella directory di installazione Configuration Manager. Se il servizio BusinessAppProcessWorker non è avviato o viene avviato e interrotto ripetutamente, rivedere le voci del file di log.



## <a name="last-sync-failed"></a>L'ultima sincronizzazione non è riuscita

Quando lo stato dell'ultima sincronizzazione *non è riuscito*, iniziare esaminando i seguenti [file di log](#log-files) per identificare il sintomo:

- MSfBSyncWorker.log
- SMS_CLOUDCONNECTION.log

Esaminare quindi una delle sezioni seguenti per i problemi comuni:

- [Errore di autorizzazione](#bkmk_fail-symptom1)
- [La chiave privata non è valida](#bkmk_fail-symptom2)
- [Errore durante il recupero del token dell'applicazione](#bkmk_fail-symptom3)
- [Il percorso del contenuto non esiste](#bkmk_fail-symptom4)
- [Si è verificato un errore durante la chiamata al metodo ' GET ' della richiesta http](#bkmk_fail-symptom5)
- [Non è possibile scrivere altri byte nel buffer](#bkmk_fail-symptom6)

### <a name="bkmk_fail-symptom1"></a> Errore di autorizzazione

#### <a name="cause"></a>Causa

Questo problema può verificarsi se l'applicazione di Azure Active Directory (Azure AD) configurata non dispone delle autorizzazioni per gestire l'Microsoft Store per le aziende e la formazione per questo tenant.

#### <a name="workaround"></a>Soluzione alternativa

1. Accedere come amministratore al portale di Microsoft Store for business o Education.
1. Passare a **Impostazioni**e selezionare **strumenti di gestione**.
1. Se l'applicazione non è inclusa nell'elenco, selezionare **Aggiungi uno strumento di gestione**. Quindi cercare in base al nome e selezionare l'applicazione Azure AD associata allo stesso oggetto ClientID come Configuration Manager.
1. Se lo stato non Mostra **attivo**, selezionare **Activate (attiva** ) nella sezione **Action (azione** ).
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**. Eseguire la sincronizzazione con l'archivio o attendere che si verifichi il successivo intervallo di sincronizzazione.

> [!Tip]
> Per trovare i ClientID in Configuration Manager:
>
> 1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Tenant di Azure Active Directory**.
> 1. Selezionare il tenant usato per l'integrazione di Microsoft Store for Business and Education.
> 1. Nel riquadro dei risultati trovare l'applicazione corrispondente ed esaminare la colonna **ID client** .

### <a name="bkmk_fail-symptom2"></a>La chiave privata non è valida

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la chiave privata è scaduta nell'app Azure AD per la configurazione Microsoft Store for business e Education.

#### <a name="resolution"></a>Risoluzione

Rinnovare la chiave privata per l'applicazione Azure AD. Per altre informazioni, vedere [Rinnovare la chiave privata](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).

### <a name="bkmk_fail-symptom3"></a>Errore durante il recupero del token dell'applicazione

#### <a name="cause"></a>Causa

Questo problema può verificarsi se l'app connessa non esiste più nel Azure AD.

#### <a name="resolution"></a>Risoluzione

Eliminare e ricreare la connessione al Microsoft Store per le aziende e la formazione.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.
1. Consente di selezionare la connessione esistente.
1. Selezionare **Elimina** nella barra multifunzione.

Quindi ricreare la connessione. Per altre informazioni, vedere gli articoli seguenti:

- [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [Configurare Microsoft Store per la sincronizzazione aziendale e dell'istruzione](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_setup)

### <a name="bkmk_fail-symptom4"></a>Il percorso del contenuto non esiste

#### <a name="cause"></a>Causa

Quando si configura la connessione Microsoft Store for Business and Education, è necessario specificare una condivisione di rete per l'archiviazione del contenuto sincronizzato. Questo problema può verificarsi se la condivisione non esiste o non dispone di autorizzazioni corrette.

Per visualizzare la posizione configurata:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.

1. Selezionare l'account e aprirne le **Proprietà**.

1. Passare alla scheda **Configurazione**. L'impostazione **località** Mostra il percorso di rete in cui archiviare il contenuto dell'applicazione scaricato dal Microsoft Store per le aziende e la formazione.

#### <a name="workaround"></a>Soluzione alternativa

1. Se non esiste già, creare la condivisione.

1. Controllare le autorizzazioni NTFS per la cartella e le autorizzazioni per la condivisione di rete. Concedere all'account computer le autorizzazioni di **lettura** e **scrittura** del punto di connessione del servizio.

Se si desidera riconfigurare il percorso, eliminare e ricreare la connessione con il nuovo percorso del contenuto.

### <a name="bkmk_fail-symptom5"></a>Si è verificato un errore durante la chiamata al metodo ' GET ' della richiesta http

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la sincronizzazione delle applicazioni dall'archivio ha richiesto fino a quando l'URL del contenuto è scaduto.

#### <a name="workaround"></a>Soluzione alternativa

Ripetere il processo di sincronizzazione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Microsoft Store per le aziende**.
1. Selezionare la connessione. Sulla barra multifunzione selezionare **Sincronizza da Microsoft Store for business**.

Ogni volta, deve continuare. Potrebbero essere necessari diversi tentativi a seconda dei fattori seguenti:

- Numero di applicazioni offline
- Dimensioni dei pacchetti
- Velocità di rete

Ogni volta che viene eseguito un tentativo, l'errore verrà visualizzato meno volte. Se il numero di errori non diminuisce, si verifica un altro problema.

### <a name="bkmk_fail-symptom6"></a>Non è possibile scrivere altri byte nel buffer

#### <a name="cause"></a>Causa

Questo problema può verificarsi se il pacchetto dell'applicazione è superiore a 500 MB. Configuration Manager supporta solo la sincronizzazione automatica di applicazioni offline con pacchetti inferiori a 500 MB.

#### <a name="workaround"></a>Soluzione alternativa

Non è possibile sincronizzare automaticamente queste app, ma è possibile scaricare il contenuto e creare manualmente l'applicazione:

1. Ottenere l'ID applicazione che ha avuto esito negativo dalla riga seguente in **MSfBSynWorker. log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Accedere come amministratore al portale di Microsoft Store for business o Education. Trovare la pagina per questa applicazione.

    > [!Tip]
    > L'URL della pagina è simile a: `https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Selezionare **offline**, se non è già selezionato. Quindi selezionare **Gestisci**.

    1. Creare una cartella separata nella condivisione del contenuto dell'applicazione per tutte le piattaforme supportate.

    1. Scaricare il pacchetto nella cartella del pacchetto.

    1. Scaricare il file di licenza codificato come file di `.bin` nella cartella del pacchetto.

    1. Scaricare tutti i Framework necessari nella cartella del pacchetto.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.

1. [Creare un'applicazione](/sccm/apps/deploy-use/create-applications), specificando manualmente le informazioni sull'applicazione.

    1. Creare un tipo di distribuzione per ogni piattaforma supportata scaricata in precedenza.

    1. Tipo: **Pacchetto app Windows (\*.appx, \*.appxbundle)**

    1. Specificare appx/appxbundle per il pacchetto dell'app effettivo, non un pacchetto di dipendenze obbligatorio.

Nella pagina **informazioni sull'importazione** finale verificare i dettagli seguenti:

- **File di licenza:** Specifica il file di `.bin`. Questo file di licenza è necessario per le app offline.
- **Dipendenze app di Windows:** Verificare che tutte le dipendenze necessarie vengano scaricate per il pacchetto.


## <a name="sync-doesnt-run"></a>La sincronizzazione non viene eseguita

In questa sezione vengono illustrati i problemi di sincronizzazione seguenti:

- Si avvia manualmente il processo di sincronizzazione, ma non viene eseguito
- Il sito non viene sincronizzato automaticamente ogni giorno

Per identificare il sintomo, iniziare esaminando i [file di log](#log-files) seguenti:

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- MSfBSyncWorker.log
- SMS_CLOUDCONNECTION.log

Esaminare quindi una delle sezioni seguenti per i problemi comuni:

- [La sincronizzazione manuale non viene avviata](#bkmk_sync-symptom1)
- [La sincronizzazione giornaliera automatica non viene eseguita e l'errore "chiusura di # Workers" in SMS_BUSINESS_APP_PROCESS_MANAGER. log](#bkmk_sync-symptom2)

### <a name="bkmk_sync-symptom1"></a>La sincronizzazione manuale non viene avviata

#### <a name="cause"></a>Causa

Questo problema può verificarsi se si avvia una sincronizzazione inferiore a 10 minuti dopo la sincronizzazione precedente. Non è possibile sincronizzare con frequenza superiore a ogni 10 minuti.

#### <a name="resolution"></a>Risoluzione

Attendere almeno 10 minuti prima di avviare un'altra sincronizzazione.

### <a name="bkmk_sync-symptom2"></a>La sincronizzazione giornaliera automatica non viene eseguita e l'errore "chiusura di # Workers" in SMS_BUSINESS_APP_PROCESS_MANAGER. log

#### <a name="cause"></a>Causa

Questo problema può verificarsi se il componente SMS_BUSINESS_APP_PROCESS_MANAGER interrompe il thread MSfBSyncWorker. L'errore può specificare `2` o `4` i ruoli di lavoro.

#### <a name="workaround"></a>Soluzione alternativa

Riavviare il servizio **SMS_EXECUTIVE** .

Se non si è in grado di riavviare il servizio principale, arrestare entrambi i componenti con MSfB Worker e quindi avviare entrambi:

1. Aprire il registro di sistema di Windows nel server che esegue il punto di connessione del servizio

1. Passare a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Impostare l'operazione richiesta su **Interrompi**.

    1. Aggiorna per verificare lo stato corrente = **arrestato**.

1. Passare a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Impostare l'operazione richiesta su **Interrompi**.

    1. Aggiorna per verificare lo stato corrente = **arrestato**.

1. In **SMS_CLOUDCONNECTION**impostare l'operazione richiesta su **Avvia**.

1. In **SMS_BUSINESS_APP_PROCESS_MANAGER**impostare l'operazione richiesta su **Avvia**.


## <a name="language-related-issues"></a>Problemi relativi alla lingua

Questa sezione include i problemi comuni seguenti:

- [Modifiche della selezione della lingua non applicate](#bkmk_lang-symptom1)
- [Non tutte le lingue selezionate sono presenti per tutte le informazioni sulla licenza](#bkmk_lang-symptom2)

### <a name="bkmk_lang-symptom1"></a>Modifiche della selezione della lingua non applicate

#### <a name="cause"></a>Causa

Questo problema può verificarsi se la selezione della lingua viene memorizzata nella cache e non viene cancellata dopo la modifica dei valori delle proprietà.

#### <a name="workaround"></a>Soluzione alternativa

Per risolvere il problema, riavviare il servizio **SMS_EXECUTIVE** .

### <a name="bkmk_lang-symptom2"></a>Non tutte le lingue selezionate sono presenti per tutte le informazioni sulla licenza

#### <a name="cause"></a>Causa

Questo problema può verificarsi se le informazioni sulle licenze dell'applicazione Microsoft Store for business e Education non contengono dati localizzati per la lingua specificata.

#### <a name="workaround"></a>Soluzione alternativa

Aggiungere manualmente eventuali lingue mancanti per le applicazioni create.


## <a name="offline-applications"></a>Applicazioni offline

Questa sezione include i problemi comuni seguenti:

- [Impossibile creare l'applicazione offline perché non è possibile verificare il contenuto](#bkmk_off-symptom1)
- [Impossibile installare l'applicazione creata dalle informazioni sulle licenze offline](#bkmk_off-symptom2)

### <a name="bkmk_off-symptom1"></a>Impossibile creare l'applicazione offline perché non è possibile verificare il contenuto

#### <a name="cause"></a>Causa

Questo problema può verificarsi se il contenuto sincronizzato per l'applicazione offline è danneggiato o modificato.

#### <a name="workaround"></a>Soluzione alternativa

Avviare una nuova sincronizzazione. Al termine della sincronizzazione, è necessario verificare e scaricare i file di contenuto non corretti.

### <a name="bkmk_off-symptom2"></a>Impossibile installare l'applicazione creata dalle informazioni sulle licenze offline

#### <a name="cause"></a>Causa

Questo problema può verificarsi se si distribuisce l'applicazione in un client che esegue una versione di Windows 10 precedente alla versione 1511. Le app con licenza offline di Microsoft Store for business e Education sono supportate solo in Windows 10 versione 1511 e successive.

#### <a name="resolution"></a>Risoluzione

Installare l'ultima versione di Windows 10.


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere l'argomento [relativo alla ricerca di informazioni sull'utilizzo di Configuration Manager](/sccm/core/understand/find-help).
