---
title: Registri eventi del server
titleSuffix: Configuration Manager
description: Riferimento tecnico per le possibili voci del server BitLocker (MBAM) nel registro eventi di Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 54f6ec4442e729db4dd5c9d4d02f5903babb5f47
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662499"
---
# <a name="server-event-logs"></a>Registri eventi del server

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Utilizzare la Visualizzatore eventi Windows per visualizzare i registri eventi per i componenti del server di Gestione BitLocker seguenti in Configuration Manager:

- Servizio di ripristino nel punto di gestione
- Portale self-service
- Sito Web di amministrazione e monitoraggio

In un server che ospita uno o più di questi componenti, aprire il Visualizzatore eventi. Passare quindi a **registri applicazioni e servizi**, **Microsoft**, **Windows**ed espandere **mbam-Web**. Per impostazione predefinita, sono presenti registri eventi [operativi](#operational) e [amministrativi](#admin) .

Le sezioni seguenti contengono messaggi e informazioni per la risoluzione dei problemi relativi agli ID evento che possono verificarsi con i componenti del server di gestione di BitLocker.

## <a name="admin"></a>Amministrazione

### <a name="1-webappspnerror"></a>1: WebAppSpnError

Applicazione: {sitename} {VirtualDirectory} mancano i nomi dell'entità servizio (SPN) seguenti: {ListOfSpns} registrare i nomi SPN richiesti nell'account: {ExecutionAccount}.

Per la riuscita dell'autenticazione integrata di Windows, è necessario che i nomi SPN necessari siano soddisfatti. Questo messaggio indica che il nome SPN richiesto per l'applicazione non è configurato correttamente. I dettagli contenuti in questo evento dovrebbero fornire ulteriori informazioni.

<!-- See “Service Principal Name (SPN)” in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Possibili messaggi di errore:

- GetMachineUsers: si è verificato un errore durante il recupero delle informazioni utente dal database.
- GetRecoveryKey: si è verificato un errore durante il recupero della chiave di ripristino dal database.
- GetRecoveryKey: si è verificato un errore durante il recupero delle informazioni utente dal database.
- GetRecoveryKeyIds: si è verificato un errore durante il recupero degli ID chiave di ripristino dal database.
- GetTpmHashForUser: si è verificato un errore durante il recupero dei dati hash TPM dal database di ripristino.
- GetTpmHashForUser: si è verificato un errore durante il recupero dei dati hash TPM dal database di ripristino.
- QueryDriveRecoveryData: si è verificato un errore durante il recupero dei dati di ripristino dell'unità dal database.
- QueryRecoveryKeyIdsForUser: si è verificato un errore durante il recupero degli ID chiave di ripristino dal database.
- QueryVolumeUsers: si è verificato un errore durante il recupero delle informazioni utente dal database.

Questo messaggio viene registrato ogni volta che viene generata un'eccezione durante la comunicazione con il database di ripristino. Leggere le informazioni contenute nella traccia per ottenere dettagli specifici sull'eccezione.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Possibili messaggi di errore:

- GetRecoveryKey: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- GetRecoveryKeyIds: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- GetTpmHashForUser: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- QueryRecoveryKeyIdsForUser: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- QueryDriveRecoveryData: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.

Questo messaggio viene registrato ogni volta che viene generata un'eccezione durante la comunicazione con il database di conformità. Leggere le informazioni contenute nella traccia per ottenere dettagli specifici sull'eccezione.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Questo messaggio indica un'eccezione quando il servizio tenta di comunicare con il database di ripristino. Leggere il messaggio contenuto nell'evento per ottenere informazioni specifiche sull'eccezione.

Verificare che l'account del pool di applicazioni di MBAM disponga delle autorizzazioni necessarie per connettersi al database di ripristino.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Possibili messaggi di errore:

- Non è possibile rilevare l'account del computer client o l'account utente per la migrazione dei dati.

    Ogni volta che viene effettuata una chiamata ai metodi Web `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest`o `GetTpmHash`, viene recuperato il contesto del chiamante per ottenere le credenziali del chiamante. Se il contesto del chiamante è null o vuoto, il servizio registra questo messaggio.

- Verifica dell'account non riuscita per l'identità del chiamante.

    Questo messaggio viene registrato se il metodo Web prevede che il chiamante sia un account computer e non lo è. Può anche verificarsi se il metodo Web prevede che il chiamante sia un account utente e non è un account utente o un membro di un account di gruppo di migrazione dati.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

La stringa di connessione del database di conformità nel registro di sistema è vuota.

Questo messaggio viene registrato ogni volta che la stringa di connessione del database di conformità non è valida. Verificare il valore alla chiave del registro di sistema `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Questo errore indica che i siti Web o i servizi Web non sono stati in grado di connettersi al database di conformità. Verificare che l'account del pool di applicazioni IIS sia in grado di connettersi al database.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Errori noti e possibili cause:

- La richiesta all'URL ha causato un errore interno.

    Nell'applicazione è stata generata un'eccezione non gestita per il sito Web di Administration and Monitoring (supporto tecnico). Esaminare le voci di log nel registro eventi di **Amministrazione** per trovare l'eccezione specifica.

- Si è verificato un errore durante il recupero delle informazioni sul contesto di esecuzione. Impossibile verificare la registrazione del nome dell'entità servizio (SPN).

    Durante l'operazione di caricamento del sito Web del supporto tecnico iniziale, il nome SPN viene controllato. Per verificare il nome SPN, sono necessarie le informazioni sull'account, il nome sito di IIS e ApplicationVirtualPath corrispondenti al sito Web del supporto tecnico. Questo messaggio di errore viene registrato quando uno o più di questi attributi non sono validi o sono mancanti.

- Si è verificato un errore durante la verifica della registrazione del nome dell'entità servizio (SPN).

    Questo messaggio indica che viene generata un'eccezione di sicurezza durante la verifica del nome SPN. Fare riferimento all'eccezione contenuta nei dettagli dell'evento.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Errori noti e possibili cause:

- Si è verificato un errore durante il recupero della chiave di ripristino per un utente

    Indica che è stata generata un'eccezione imprevista quando è stata effettuata una richiesta per recuperare una chiave di ripristino. Fare riferimento al messaggio di eccezione nei dettagli dell'evento. Se la traccia è abilitata nell'app helpdesk, fare riferimento ai dati di traccia per ottenere messaggi di eccezione dettagliati.

- Si è verificato un errore durante il recupero delle informazioni sul contesto di esecuzione. Impossibile verificare la registrazione del nome dell'entità servizio (SPN)

    Durante un'operazione di caricamento iniziale, il portale self-service recupera le informazioni sull'account, il siteName IIS e ApplicationVirtualPath per il sito Web self-service per la verifica del nome SPN. Questo messaggio di errore viene registrato quando uno o più di questi attributi non sono validi.

- Si è verificato un errore durante la verifica della registrazione del nome dell'entità servizio (SPN). EventDetails: {ExceptionMessage}

    Questo messaggio indica che è stata generata un'eccezione di sicurezza durante la verifica del nome SPN. Fare riferimento all'eccezione contenuta nei dettagli dell'evento.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Errori noti e possibili cause:

- Si è verificato un errore durante la risoluzione del nome di dominio {domainname}. si è verificato un errore di allocazione della memoria.

    Per risolvere il nome di dominio, chiama l'API Windows `DsGetDcName`. Questo messaggio viene registrato quando l'API restituisce `ERROR_NOT_ENOUGH_MEMORY`, che indica un errore di allocazione della memoria.

- Non è stato possibile richiamare il metodo DsGetDcName

    Questo messaggio indica che l'API `DsGetDcName` non è disponibile nell'host.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Errori noti e possibili cause:

- Si è verificato un errore durante la lettura della configurazione del database di ripristino. La stringa di connessione al database di ripristino non è configurata.

    Questo messaggio indica che le informazioni sulla stringa di connessione del database di ripristino in `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` non sono valide. Verificare il valore della chiave del registro di sistema specificato.

Se viene visualizzato uno dei messaggi seguenti, verificare che le credenziali del pool di applicazioni del server IIS possano stabilire una connessione al database di ripristino:

- DoesUserHaveMatchingRecoveryKey: si è verificato un errore durante il recupero degli ID chiave di ripristino per un utente.
- QueryDriveRecoveryData: si è verificato un errore durante il recupero dei dati di ripristino dell'unità.
- QueryRecoveryKeyIdsForUser: si è verificato un errore durante il recupero degli ID chiave di ripristino per un utente.
- Si è verificato un errore durante il recupero dell'hash della password TPM dal database di ripristino.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Errori noti e possibili cause:

- Si è verificato un errore durante la lettura della configurazione del database di conformità. La stringa di connessione al database di conformità non è configurata.

    Questo messaggio indica che le informazioni sulla stringa di connessione del database di conformità nel `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` non sono valide. Verificare il valore di questa chiave del registro di sistema.

Se viene visualizzato uno dei messaggi seguenti, verificare che le credenziali del pool di applicazioni del server IIS possano stabilire una connessione al database di conformità:

- GetRecoveryKeyForCurrentUser: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- QueryRecoveryKeyIdsForUser: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.
- QueryRecoveryKeyIdsForUser: si è verificato un errore durante la registrazione di un evento di controllo nel database di conformità.

### <a name="111-webappdberror"></a>111: WebAppDbError

Questi errori indicano una delle due condizioni seguenti

- I siti Web e i servizi Web di MBAM non sono riusciti a connettersi al database di conformità o ripristino
- L'account di esecuzione di siti Web/servizi Web MBAM (account del pool di applicazioni) non è riuscito a eseguire il `GetVersion` stored procedure nel database di conformità o ripristino

Il messaggio contenuto nell'evento fornisce altri dettagli sull'eccezione.

Verificare che l'account del pool di applicazioni sia in grado di connettersi ai database di conformità o di ripristino. Verificare che disponga delle autorizzazioni per eseguire il `GetVersion` stored procedure.

### <a name="112-webapperror"></a>112: WebAppError

Si è verificato un errore durante la verifica della registrazione del nome dell'entità servizio (SPN).

Per verificare il nome SPN, viene eseguita una query Active Directory per recuperare un elenco di account di esecuzione mappati SPN. Viene inoltre eseguita una query sul `ApplicationHost.config` per ottenere i binding del sito Web. Questo messaggio di errore indica che non è stato possibile comunicare con Active Directory oppure non è stato in grado di caricare il file di `ApplicationHost.config`.

Verificare che l'account del pool di applicazioni disponga delle autorizzazioni per eseguire query Active Directory o il file di `ApplicationHost.config`. Verificare inoltre le voci di binding del sito nel file di `ApplicationHost.config`.

## <a name="operational"></a>Operativo

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Si è verificato un errore durante il recupero di un contatore delle prestazioni.

Il messaggio di traccia contiene il messaggio di eccezione effettivo, alcune delle quali sono elencate di seguito:

- ArgumentNullException: questa eccezione viene generata se la categoria, il contatore o l'istanza del contatore delle prestazioni richiesto non è valido.
- System. InvalidOperationException: CategoryName è una stringa vuota (""). counterName è una stringa vuota ("").
- L'impostazione dell'autorizzazione di lettura/scrittura richiesta non è valida per questo contatore.
- La categoria specificata non esiste (se readOnly è true).
- La categoria specificata non è un .NET Framework categoria personalizzata (se readOnly è false).
- La categoria specificata è contrassegnata come istanza a più istanze ed è necessario che il contatore delle prestazioni venga creato con un nome di istanza.
- Nomeistanza è più lungo di 127 caratteri.
- CategoryName e counterName sono stati localizzati in lingue diverse.
- System. ComponentModel. Win32exception: si è verificato un errore durante l'accesso a un'API di sistema.
- System. UnauthorizedAccessException: il codice in esecuzione senza privilegi amministrativi ha tentato di leggere un contatore delle prestazioni.

Il messaggio nell'evento fornisce altri dettagli sull'eccezione.

Per il `System.UnauthorizedAccessException`, verificare che l'account del pool di applicazioni abbia accesso alle API del contatore delle prestazioni.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

L'applicazione del sito Web di amministrazione è stata trovata e connessa a una versione supportata del database di ripristino/conformità.

Indica una connessione riuscita al database di ripristino o di conformità dal sito Web Helpdesk.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

L'applicazione del portale self-service è stata trovata e connessa a una versione supportata del database di ripristino/conformità.

Indica una connessione riuscita al database di ripristino o di conformità dal portale self-service.

### <a name="202-webappinformation"></a>202: WebAppInformation

I nomi SPN dell'applicazione sono registrati correttamente.

Indica che i nomi SPN richiesti per il sito Web Helpdesk sono registrati correttamente rispetto all'account in esecuzione.

## <a name="see-also"></a>Vedere anche

Per ulteriori informazioni sull'utilizzo di questi log, vedere la pagina relativa ai [registri eventi di BitLocker](/configmgr/protect/tech-ref/bitlocker/about-event-logs).

Per ulteriori informazioni sulla risoluzione dei problemi, vedere [Troubleshoot BitLocker](/configmgr/protect/tech-ref/bitlocker/troubleshoot).

Per ulteriori informazioni sull'installazione di questi siti Web, vedere [impostare i portali e i report di BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites).
