---
title: Distribuire la gestione di BitLocker
titleSuffix: Configuration Manager
description: Distribuire l'agente di Gestione BitLocker per Configuration Manager client e il servizio di ripristino ai punti di gestione
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8cb3f8763b0789dcf593c71190e4772ce4b977ac
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662639"
---
# <a name="deploy-bitlocker-management"></a>Distribuire la gestione di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

La gestione di BitLocker in Configuration Manager include i componenti seguenti:

- **Agente di Gestione BitLocker**: Configuration Manager Abilita questo agente in un dispositivo quando si [Crea un criterio](#create-a-policy) e [lo si distribuisce in una raccolta](#deploy-a-policy).

- **Servizio di ripristino**: componente server che riceve i dati di ripristino di BitLocker dai client. Per ulteriori informazioni, vedere [servizio di ripristino](#recovery-service).

Prima di creare e distribuire i criteri di gestione di BitLocker, assicurarsi di esaminare i [prerequisiti](/configmgr/protect/plan-design/bitlocker-management#prerequisites).

## <a name="create-a-policy"></a>Creare un criterio

Quando si crea e si distribuisce questo criterio, il client Configuration Manager Abilita l'agente di Gestione BitLocker nel dispositivo.

> [!NOTE]
> Nella versione 1910, per creare un criterio di gestione di BitLocker, è necessario il ruolo **amministratore completo** in Configuration Manager.

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Endpoint Protection** e selezionare il nodo **Gestione di BitLocker**.

1. Sulla barra multifunzione selezionare **Crea criteri di controllo di Gestione BitLocker**.

1. Nella pagina **Generale** specificare un nome e una descrizione facoltativa. Selezionare i componenti da attivare nei client con questi criteri:  

    - **Gestione client**: gestire il backup del servizio di recupero chiave per le informazioni di ripristino di Crittografia unità BitLocker  

    - **Unità del sistema operativo**: gestire se l'unità del sistema operativo è crittografata

1. Nella pagina **installazione** configurare le impostazioni seguenti per crittografia unità BitLocker:

    > [!NOTE]
    > Configuration Manager applica queste impostazioni quando si attiva BitLocker. Se l'unità è già crittografata o è in corso, qualsiasi modifica apportata alle impostazioni dei criteri non modifica la crittografia dell'unità nel dispositivo.
    >
    > Se queste impostazioni vengono disabilitate o non configurate, BitLocker userà il metodo di crittografia predefinito (AES 128 bit).

    - Per i dispositivi Windows 8.1 o Windows 7, abilitare l'opzione per **scegliere una crittografia dell'unità e un**livello di codifica. Selezionare quindi il metodo di crittografia:

        - AES a 128 bit con diffusione (solo Windows 7)
        - AES a 256 bit con diffusione (solo Windows 7)
        - AES 128 bit (impostazione predefinita)
        - AES a 256 bit

    - Per i dispositivi Windows 10, abilitare l'opzione per **scegliere una crittografia dell'unità e un livello di codifica (Windows 10)** . Selezionare quindi individualmente il metodo di crittografia per le unità del sistema operativo, le unità dati fisse e le unità dati rimovibili:

        - AES-CBC a 128 bit
        - AES-CBC a 256 bit
        - XTS-AES a 128 bit
        - XTS-AES a 256 bit

    > [!TIP]
    > BitLocker utilizza Advanced Encryption Standard (AES) come algoritmo di crittografia con lunghezze di chiave configurabili di 128 o 256 bit. Nei dispositivi Windows 10 la crittografia AES supporta la crittografia dei blocchi crittografici (CBC) o il furto del testo crittografato (XTS).

1. Nella pagina **Gestione dei client** specificare le impostazioni seguenti:

    > [!IMPORTANT]
    > Se non si dispone di un punto di gestione abilitato per HTTPS, non configurare questa impostazione. Per ulteriori informazioni, vedere [servizio di ripristino](#recovery-service).

    - **Configurare i servizi di Gestione BitLocker**: se si abilita questa impostazione, Configuration Manager esegue automaticamente il backup delle informazioni di recupero delle chiavi nel database del sito in modo automatico e invisibile all'utente. Se si disattiva o non si configura questa impostazione, Configuration Manager non salva le informazioni di recupero della chiave.

        - **Selezionare le informazioni di ripristino di BitLocker da archiviare**: configurarlo per l'utilizzo di una password di ripristino e di un pacchetto di chiavi oppure solo una password di ripristino.

        - **Consenti l'archiviazione delle informazioni di ripristino in testo normale**: senza un certificato di crittografia di Gestione BitLocker, Configuration Manager archivia le informazioni di recupero della chiave in testo normale. Per altre informazioni, vedere [crittografare i dati di ripristino](/configmgr/protect/deploy-use/bitlocker/encrypt-recovery-data).

        - **Frequenza stato controllo client (minuti)** : per impostazione predefinita, il client di Configuration Manager aggiorna le informazioni di ripristino di BitLocker ogni 90 minuti.

1. Nella pagina **Unità sistema operativo** specificare le impostazioni seguenti:  

    - **Impostazioni di crittografia dell'unità del sistema operativo**: se si abilita questa impostazione, l'utente deve proteggere l'unità del sistema operativo e BitLocker crittografa l'unità. Se viene disabilitata, l'utente non può proteggere l'unità.  

        > [!Note]  
        > Se l'unità è già crittografata e si disabilita questa impostazione, BitLocker esegue la decrittografia dell'unità.  

    - **Consenti BitLocker senza un TPM compatibile (richiede una password)** : consente a BitLocker di crittografare l'unità del sistema operativo anche se il dispositivo non dispone di un [Trusted Platform Module (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node). Se si consente questa opzione, Windows chiede all'utente di specificare una password di BitLocker.

    - **Selezionare la protezione per l'unità del sistema operativo**: configurarla per l'uso di un TPM e un PIN o solo del TPM.

    - **Configurare la lunghezza minima del PIN per l'avvio**: se è necessario un PIN, questo valore corrisponde alla lunghezza più breve che l'utente può specificare. L'utente immette il PIN all'avvio del computer per sbloccare l'unità. Per impostazione predefinita, la lunghezza minima del PIN è `4`.

1. Completare la procedura guidata.

Per modificare le impostazioni di un criterio esistente, selezionarlo nell'elenco e selezionare **Proprietà**.

Quando si crea più di un criterio, è possibile configurarne la priorità relativa. Se si distribuiscono più criteri a un client, viene utilizzato il valore Priority per determinarne le impostazioni.

## <a name="deploy-a-policy"></a>Distribuire un criterio

1. Scegliere un criterio esistente nel nodo **Gestione BitLocker** . Sulla barra multifunzione selezionare **Distribuisci**.

1. Selezionare una raccolta di dispositivi come destinazione della distribuzione.

1. Se si vuole che il dispositivo possa crittografare o decrittografare le proprie unità in qualsiasi momento, selezionare l'opzione **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**. Se la raccolta ha una finestra di manutenzione, risolve comunque questo criterio BitLocker.

1. Configurare una pianificazione **semplice** o **personalizzata** . Per impostazione predefinita, il client valuta la conformità con questi criteri ogni 12 ore.

1. Selezionare **OK** per distribuire il criterio.

È possibile creare più distribuzioni dello stesso criterio. Per visualizzare ulteriori informazioni su ogni distribuzione, selezionare il criterio nel nodo **Gestione BitLocker** , quindi nel riquadro dei dettagli passare alla scheda **distribuzioni** .

## <a name="monitor"></a>Monitoraggio

Visualizzare le statistiche di conformità di base sulla distribuzione del criterio nel riquadro dei dettagli del nodo di **Gestione BitLocker** :

- Conteggio di conformità
- Conteggio errori
- Conteggio di mancata conformità

Passare alla scheda **distribuzioni** per visualizzare la percentuale di conformità e l'azione consigliata. Selezionare la distribuzione, quindi nella barra multifunzione selezionare **Visualizza stato**. Questa azione consente di passare dalla visualizzazione all'area di lavoro **monitoraggio** , ovvero al nodo **distribuzioni** . Analogamente alla distribuzione di altre distribuzioni dei criteri di configurazione, in questa vista è possibile visualizzare lo stato di conformità più dettagliato.

Per comprendere il motivo per cui i client inviano report non conformi ai criteri di gestione di BitLocker, vedere [codici non di conformità](/configmgr/protect/tech-ref/bitlocker/non-compliance-codes).

Per ulteriori informazioni sulla risoluzione dei problemi, vedere [Troubleshoot BitLocker](/configmgr/protect/tech-ref/bitlocker/troubleshoot).

Usare i log seguenti per il monitoraggio e la risoluzione dei problemi:

### <a name="client-logs"></a>Log del client

- Registro eventi MBAM: nel Visualizzatore eventi di Windows, passare ad Applicazioni e servizi > Microsoft > Windows > MBAM.  Per ulteriori informazioni, vedere [informazioni sui registri eventi di BitLocker e sui](/configmgr/protect/tech-ref/bitlocker/about-event-logs) [registri eventi del client](/configmgr/protect/tech-ref/bitlocker/client-event-logs).

- **BitlockerMangementHandler.log** nel percorso dei log del client, `%WINDIR%\CCM\Logs` per impostazione predefinita

### <a name="management-point-logs-recovery-service"></a>Log del punto di gestione (servizio di ripristino)

- Registro eventi del servizio di ripristino: nel Visualizzatore eventi di Windows, passare ad Applicazioni e servizi > Microsoft > Windows > MBAM-Web. Per ulteriori informazioni, vedere [informazioni sui registri eventi di BitLocker e sui](/configmgr/protect/tech-ref/bitlocker/about-event-logs) [registri eventi del server](/configmgr/protect/tech-ref/bitlocker/server-event-logs).

- Log di traccia del servizio di ripristino: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Servizio di ripristino

Il servizio di ripristino di BitLocker è un componente server che riceve i dati di ripristino di BitLocker dai client di Configuration Manager. Il sito distribuisce il servizio di ripristino quando si creano i criteri di gestione di BitLocker. Configuration Manager installa automaticamente il servizio di ripristino in ogni punto di gestione abilitato per HTTPS.

> [!IMPORTANT]
> Il servizio di ripristino richiede un punto di gestione abilitato per HTTPS. Non è possibile installarlo in un punto di gestione configurato per HTTP o qualsiasi altro sistema del sito.

Configuration Manager archivia le informazioni di ripristino nel database del sito. Senza un certificato di crittografia di Gestione BitLocker, Configuration Manager archivia le informazioni di recupero della chiave in testo normale. Per altre informazioni, vedere [crittografare i dati di ripristino](/configmgr/protect/deploy-use/bitlocker/encrypt-recovery-data).

## <a name="migration-considerations"></a>Considerazioni sulla migrazione

Se attualmente si utilizza Microsoft BitLocker Administration and Monitoring (MBAM), è possibile eseguire facilmente la migrazione della gestione a Configuration Manager. Quando si distribuiscono i criteri di gestione di BitLocker in Configuration Manager, i client caricano automaticamente le chiavi e i pacchetti di ripristino nel servizio Configuration Manager Recovery.

### <a name="group-policy"></a>Criteri di gruppo

- Le impostazioni di gestione di BitLocker sono completamente compatibili con le impostazioni di criteri di gruppo di MBAM. Se i dispositivi ricevono sia le impostazioni di criteri di gruppo che Configuration Manager criteri, configurarli in modo che corrispondano.

- Configuration Manager non implementa tutte le impostazioni di criteri di gruppo di MBAM. Se si configurano impostazioni aggiuntive in criteri di gruppo, l'agente di Gestione BitLocker nei client Configuration Manager rispetta tali impostazioni.

### <a name="tpm-password-hash"></a>Hash della password TPM

- I client MBAM precedenti non caricano l'hash della password TPM in Configuration Manager. Il client carica solo l'hash della password TPM una sola volta.

- Se è necessario eseguire la migrazione di queste informazioni nel servizio Configuration Manager Recovery, cancellare il TPM sul dispositivo. Dopo il riavvio, verrà caricato il nuovo hash della password TPM nel servizio di ripristino.

### <a name="re-encryption"></a>Nuova crittografia

Configuration Manager non crittografa nuovamente le unità che sono già protette con Crittografia unità BitLocker. Se si distribuisce un criterio di gestione di BitLocker che non corrisponde alla protezione corrente dell'unità, questo viene segnalato come non conforme. L'unità è ancora protetta.

Ad esempio, è stato usato MBAM per crittografare l'unità senza la protezione dei PIN, ma i criteri di Configuration Manager richiedono un PIN. L'unità non è conforme ai criteri, anche se l'unità è crittografata.

Per risolvere questo problema, disabilitare prima di tutto BitLocker nel dispositivo. Quindi, distribuire un nuovo criterio con le nuove impostazioni.

## <a name="next-steps"></a>Passaggi successivi

[Crittografare i dati di ripristino](/configmgr/protect/deploy-use/bitlocker/encrypt-recovery-data)

[Configurare i report e i portali di BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites)
