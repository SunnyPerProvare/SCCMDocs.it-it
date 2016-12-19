---
title: Impostazioni client | Documentazione Microsoft
description: Selezionare le impostazioni client tramite la console di System Center Configuration Manager.
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 809c7938968b4a6efce6ef37fe7b7baf2c9dd3e7
ms.openlocfilehash: 1615c183c440b44084651d52bfc50be2d65c2e11

---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Informazioni sulle impostazioni client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Tutte le impostazioni client di System Center Configuration Manager vengono gestite nella console di Configuration Manager nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione**. Con Configuration Manager viene specificato un set di impostazioni predefinite. Quando si modificano le impostazioni client predefinite, tali impostazioni vengono applicate a tutti i client nella gerarchia. È inoltre possibile configurare le impostazioni client personalizzate, che sostituiscono le impostazioni client predefinite quando le si assegnano a raccolte. Per altre informazioni su come configurare le impostazioni client, vedere [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

 Molte delle impostazioni client non necessitano di spiegazione, mentre altre sono descritte in questo articolo.  

## <a name="background-intelligent-transfer"></a>Trasferimento intelligente in background  

-   **Limitare la larghezza di banda di rete massima per i trasferimenti in background BITS**  

   Se questa opzione è impostata su **True** o **Sì**, i client useranno la limitazione della larghezza di banda BITS.  

-   **Ora di inizio dell'intervallo di limitazione**  

   Ora di inizio locale per l'intervallo di limitazione BITS.  

-   **Ora di fine dell'intervallo di limitazione**  

  Ora di fine locale per l'intervallo di limitazione BITS. Se il valore è lo stesso dell'**ora di inizio dell'intervallo di limitazione**, la limitazione BITS è sempre abilitata.  

-   **Velocità massima di trasferimento durante l'intervallo di limitazione (Kbps)**  

   Specificare la velocità massima di trasferimento che può essere usata dai client durante l'intervallo.  

-   **Consentire i download BITS all'esterno dell'intervallo di limitazione**  

   Consente ai client di Configuration Manager di usare impostazioni BITS separate all'esterno dell'intervallo specificato.  

-   **Velocità massima di trasferimento all'esterno dell'intervallo di limitazione (Kbps)**  

   Velocità massima di trasferimento che verrà usata dai client all'esterno dell'intervallo di limitazione BITS, se è stata selezionata l'opzione che consente la limitazione BITS all'esterno dell'intervallo.  

## <a name="client-cache-settings"></a>Impostazione della cache client

- **Configura BranchCache**

  A partire dalla versione 1606, questa opzione viene usata per configurare il computer client per [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Per consentire la memorizzazione nella cache BranchCache nel client, impostare **Abilita BranchCache** su **Sì**. 

- **Configurare la dimensione della cache client**

  Nei computer Windows la cache client archivia i file temporanei usati per installare applicazioni e programmi. Selezionare **Sì** per specificare le **Dimensioni cache massime** (MB o percentuale del disco). Se questa opzione è impostata su **No**, il valore predefinito è 5120 MB.

## <a name="client-policy"></a>Criteri client  

-   **Intervallo di polling dei criteri client (minuti)**  

   Specificare la frequenza con cui i client seguenti di Configuration Manager scaricano criteri client:  

  -   Computer Windows (ad esempio, desktop, server, portatili)  

  -   Dispositivi mobili registrati da Configuration Manager  

  -   Computer Mac  

  -   Computer con sistema operativo Linux o UNIX  

-   **Abilitare il polling dei criteri utente sui client**  

   Quando questa opzione viene impostata su **True** o **Sì** e Configuration Manager [ha individuato l'utente](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), i client sui computer ricevono applicazioni e programmi destinati all'utente che ha effettuato l'accesso.  

   Poiché il Catalogo applicazioni riceve l'elenco del software disponibile per gli utenti dal server del sito, questa impostazione non deve essere configurata su **True** o **Sì** affinché gli utenti visualizzino e richiedano le applicazioni dal Catalogo applicazioni. Tuttavia, se tale impostazione è **False** o **No**, quanto segue non funzionerà quando gli utenti utilizzeranno il Catalogo applicazioni:  

  -   Gli utenti non possono installare le applicazioni che vedono nel Catalogo applicazioni.  

  -   Gli utenti non visualizzeranno le notifiche relative alle richieste di approvazione delle applicazioni. Al contrario, devono aggiornare il Catalogo applicazioni e verificare lo stato di approvazione.  

  -   Gli utenti non riceveranno revisioni e aggiornamenti per le applicazioni che vengono pubblicate nel Catalogo applicazioni. Tuttavia, visualizzeranno le modifiche alle informazioni sulle applicazioni nel Catalogo applicazioni.  

  -   Se si rimuove la distribuzione di un'applicazione dopo che il client ha installato l'applicazione dal catalogo applicazioni, i client continuano a controllare che l'applicazione sia installata per un periodo di tempo fino a 2 giorni.  

   Inoltre, quando questa impostazione è **False** o **No**, gli utenti non riceveranno le applicazioni richieste che si distribuiscono agli utenti o qualsiasi altra operazione di gestione contenuta nei criteri utente.  

   Questa impostazione viene applicata agli utenti quando i relativi computer si trovano nell'intranet e su Internet; deve essere configurata su **True** o **Sì** se si desidera inoltre abilitare i criteri utente su Internet.  

-   **Abilitare le richieste dei criteri utente dai client Internet**  

   Quando il client e il sito sono configurati per la gestione client basata su Internet e si configura questa opzione su **True** o **Sì** e si applicano entrambe le seguenti condizioni, gli utenti ricevono i criteri utente quando il relativo computer si trova su Internet:  

  -   L'impostazione client **Abilita il polling dei criteri utente sui client** è configurata su **True** o **Abilita i criteri utente nei client** è configurata su **Sì**.  

  -   Il punto di gestione basato su Internet autentica automaticamente l'utente usando l'autenticazione di Windows (Kerberos o NTLM).  

   Se si lascia l'opzione su **False** o **No**o una delle due condizione non riesce, un computer su Internet riceverà solo i criteri computer. In questo scenario, gli utenti possono comunque visualizzare, richiedere e installare applicazioni da un Catalogo applicazioni basato su Internet. Se questa impostazione è **False** **No** ma **Abilita il polling dei criteri utente sui client** è configurato su **True** o **Abilita i criteri utente nei client** è configurato su **Sì**, gli utenti non riceveranno i criteri client finché il computer non è connesso alla intranet.  

   Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non attendibile](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in  [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Le richieste di approvazione dell'applicazione da parte degli utenti non richiedono criteri utente o l'autenticazione dell'utente.  

##  <a name="compliance-settings"></a>Impostazioni di conformità  

-   **Valutazione di conformità della pianificazione**  

     Fare clic su **Pianifica** per creare la pianificazione predefinita che verrà visualizzata agli utenti quando distribuiscono una linea di base della configurazione. Questo valore può essere configurato per ogni linea di base nella finestra di dialogo **Linea di base configurazione distribuzione** .  

-   **Abilitare i dati e profili utente**  

     Selezionare **Sì**, se si vuole distribuire elementi di configurazione di [dati e profili utente](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) a computer con Windows 8 nella gerarchia.  

## <a name="computer-agent"></a>Agente computer  

-   **Punto per siti Web del Catalogo applicazioni predefinito**  

     Configuration Manager usa questa impostazione per connettere gli utenti al Catalogo applicazioni dal Software Center. È possibile specificare un server che ospiti il punto per siti Web del catalogo applicazioni per nome NetBIOS o FQDN, specificare il rilevamento automatico o un URL per distribuzioni personalizzate. Nella maggior parte dei casi, il rilevamento automatico è la scelta migliore in quanto offre i seguenti vantaggi:  

    -   Ai client viene assegnato automaticamente un punto per siti Web del Catalogo applicazioni dal relativo sito, se il sito contiene un punto per siti Web del Catalogo applicazioni.  

    -   Protezione contro un server non autorizzato, perché ai punti per siti Web del Catalogo applicazioni sull'intranet configurati per HTTPS viene data la preferenza rispetto ai punti che non sono configurati per HTTPS.  

    -   Quando i client sono configurati per la gestione client basata su Internet e intranet, a essi verrà assegnato un punto per siti Web del Catalogo applicazioni basato su Internet quando si trovano su Internet e un punto per siti Web del catalogo applicazioni basato su intranet quando si trovano sulla intranet.  

     Il rilevamento automatico non garantisce che ai client verrà assegnato il punto per siti Web del Catalogo applicazioni più vicino. Si potrebbe decidere di non usare **Rileva automaticamente** per i seguenti motivi:  

    -   Si desidera configurare manualmente il server più vicino per il client o assicurarsi che non si connettano a un server con una connessione di rete lenta.  

    -   Si desidera controllare quali client si connettono a quale server. Questo potrebbe avvenire per motivi di test, di prestazioni o aziendali.  

    -   Non si desidera aspettare fino a 25 ore o una modifica di rete affinché i client vengano configurati con un punto per siti Web del Catalogo applicazioni diverso.  

     Se si specifica il punto per siti Web del Catalogo applicazioni invece di usare il rilevamento automatico, specificare il nome NetBIOS invece dell'FQDN dell'intranet per ridurre la probabilità che agli utenti vengano richieste le credenziali quando si collegano al Catalogo applicazioni nella intranet. Per usare il nome NetBIOS, è necessario che siano applicabili le seguenti condizioni:  

    -   Il nome NetBIOS viene specificato nelle proprietà del punto per siti Web del Catalogo applicazioni.  

    -   Si usa WINS oppure tutti i client si trovano nello stesso dominio del punto per siti Web del Catalogo applicazioni.  

    -   Il punto per siti Web del Catalogo applicazioni viene configurato per connessioni client HTTP oppure per connessioni client HTTPS e il certificato del server Web contiene il nome NetBIOS.  

     In genere, agli utenti vengono richieste le credenziali quando l'URL contiene un FQDN, ma non quando l'URL è un nome NetBIOS. Agli utenti verrà sempre richiesto quando si connettono da Internet, poiché questa connessione deve usare l'FQDN Internet. Quando agli utenti vengono richieste le credenziali quando si trovano su Internet, assicurarsi che il server su cui è in esecuzione il punto per siti Web del Catalogo applicazioni possa connettersi a un controller di dominio per l'account dell'utente cosicché l'utente possa essere autenticato con Kerberos.  

    > [!NOTE]  
    >  Funzionamento del rilevamento automatico:  
    >   
    >  Il client effettua una richiesta di posizione del servizio a un punto di gestione. Se nello stesso sito del client c'è un punto per siti Web del Catalogo applicazioni, tale server viene assegnato al client come server del Catalogo applicazioni da usare. Quando nel sito c'è più di un punto per siti Web del Catalogo applicazioni disponibile, un server abilitato per HTTPS ha la precedenza su un server non abilitato per HTTPS. Dopo l'applicazione di questo filtro, a tutti i client viene assegnato uno dei server da usare come Catalogo applicazioni; Configuration Manager non bilancia il carico tra più server. Quando il sito del client non contiene un punto per siti Web del Catalogo applicazioni, il punto di gestione restituisce in modo non deterministico un punto per siti Web del Catalogo applicazioni dalla gerarchia.  
    >   
    >  Quando il client si trova sulla intranet, se il punto per siti Web del Catalogo applicazioni selezionato è configurato con un nome NetBIOS per l'URL del Catalogo applicazioni, ai client viene assegnato questo nome NetBIOS invece dell'FQDN dell'intranet. Quando il client viene rilevato su Internet, gli viene assegnato solo l'FQDN Internet.  
    >   
    >  Il client effettua questa richiesta di posizione del servizio ogni 25 ore oppure ogni volta che rileva una modifica di rete. Ad esempio, se il client di sposta dalla intranet su Internet e il client può individuare un punto di gestione basato su Internet, tale punto assegna i server del punto per siti Web del Catalogo applicazioni ai client.  

-   **Aggiungere il sito Web del Catalogo applicazioni predefinito all'area siti attendibili di Internet Explorer**  

     Se questa opzione è configurata su **True** o **Sì**, l'URL del sito Web del Catalogo applicazioni corrente predefinito viene automaticamente aggiunto all'area siti attendibili di Internet Explorer nei client.  

     Questa impostazione garantisce che l'impostazione di Internet Explorer in modalità protetta non sia abilitata. Se la modalità protetta è abilitata, il client di Configuration Manager potrebbe non essere in grado di installare applicazioni dal Catalogo applicazioni. Per impostazione predefinita, l'area siti attendibili supporta inoltre l'accesso utente per il Catalogo applicazioni, il che richiede l'autenticazione di Windows.  

     Se si lascia questa opzione impostata su **False**, i client di Configuration Manager potrebbero non essere in grado di installare applicazioni dal Catalogo applicazioni a meno che queste impostazioni di Internet Explorer non siano configurate in un'altra area per l'URL del Catalogo applicazioni usata dai client.  

    > [!NOTE]  
    >  Ogni volta che Configuration Manager aggiunge un Catalogo applicazioni predefinito all'area siti attendibili, rimuove un URL del Catalogo applicazioni precedentemente predefinito e aggiunto prima di aggiungere una nuova voce.  
    >   
    >  Configuration Manager non può aggiungere l'URL se è già specificato in una delle aree di sicurezza. In questo scenario, è necessario rimuovere l'URL dall'altra area o configurare manualmente le impostazioni di Internet Explorer necessarie.  

-   **Consentire l'esecuzione in modalità di attendibilità elevata delle applicazioni Silverlight**  

     Questa impostazione deve essere impostata su **Sì** se gli utenti eseguono il client di Configuration Manager e usano il Catalogo applicazioni.  

     L'eventuale modifica di questa impostazione ha effetto al successivo caricamento del browser o aggiornamento della finestra del browser attualmente aperta da parte degli utenti.  

     Per altre informazioni su questa impostazione, vedere [Certificati per Microsoft Silverlight 5 e modalità attendibile elevata richiesta per il Catalogo applicazioni](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) in [Sicurezza e privacy per la gestione di applicazioni in System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nome organizzazione visualizzato in Software Center**  

     Digitare il nome visualizzato dagli utenti in Software Center. Queste informazioni di personalizzazione consentono agli utenti di identificare questa applicazione come origine attendibile.  

-   **Usa il nuovo Software Center**  

     Se questa impostazione è abilitata, tutti i computer client di destinazione di queste impostazioni client useranno il nuovo Software Center, che consente di visualizzare le app disponibili per gli utenti a cui in precedenza era possibile accedere solo dal Catalogo applicazioni dipendente da Silverlight.  

     Tuttavia, i ruoli del sistema del sito del punto per siti Web del Catalogo applicazioni e del punto per servizi Web del Catalogo applicazioni continuano a essere necessari per visualizzare le app disponibili per gli utenti in Software Center.  

     Per altre informazioni, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Autorizzazioni di installazione**  

    > [!WARNING]  
    >  Questa impostazione è valida per il Catalogo applicazioni e Software Center. Questa impostazione non ha alcun effetto se gli utenti usano il portale aziendale.  

     Configurare la modalità di avvio dell'installazione del software, degli aggiornamenti software e delle sequenze attività da parte degli utenti:  

    -   **Tutti gli utenti**: gli utenti connessi a un computer client con qualsiasi autorizzazione ad eccezione di Guest possono avviare l'installazione del software, degli aggiornamenti software e delle sequenze di attività.  

    -   **Solo amministratori**: gli utenti connessi a un computer client devono essere membri del gruppo Administrators locale per avviare l'installazione del software, degli aggiornamenti software e delle sequenze di attività.  

    -   **Solo amministratori e utenti primari**: gli utenti connessi a un computer client devono essere membri del gruppo Administrators locale o un utente primario del computer per avviare l'installazione del software, degli aggiornamenti software e delle sequenze di attività.  

    -   **Nessun utente**: nessun utente connesso a un computer client può avviare l'installazione del software, degli aggiornamenti software e delle sequenze di attività. Le distribuzioni richieste per il computer sono sempre installate alla scadenza e gli utenti non sono in grado di avviare l'installazione del software dal Catalogo applicazioni o da Software Center.  

-   **Sospendere immissione PIN di BitLocker al riavvio**  

     Se l'immissione PIN di BitLocker è configurata sui computer, questa opzione può ignorare la richiesta di immissione di un PIN quando il computer viene riavviato dopo un'installazione software.  

    -   **Sempre**: Configuration Manager sospende temporaneamente la richiesta di BitLocker di immissione di un PIN al successivo avvio del computer dopo aver installato il software che richiede un riavvio e dopo aver riavviato il computer. Questa impostazione si applica solo ai riavvii del computer eseguiti da Configuration Manager e non sospende la richiesta di immissione del PIN di BitLocker quando l'utente riavvia il computer. La richiesta di immissione del PIN di BitLocker è ripristinata dopo l'avvio di Windows.  

    -   **Mai**: Configuration Manager non sospende la richiesta di BitLocker di immissione di un PIN al successivo avvio del computer dopo aver installato software che richiede un riavvio. In questo scenario, l'installazione del software non può finire fino a quando l'utente immette il PIN per completare il processo di avvio e caricamento standard di Windows.  

-   **Il software aggiuntivo gestisce la distribuzione delle applicazioni e degli aggiornamenti software**  

     Attivare questa opzione solo in presenza di una delle seguenti condizioni:  

    -   Si usa una soluzione per fornitori che richiede l'abilitazione di questa impostazione.  

    -   Per gestire le notifiche dell'agente client e l'installazione delle applicazioni e degli aggiornamenti software, si usa il Software Development Kit (SDK) di Configuration Manager.  

    > [!WARNING]  
    >  Se si seleziona questa opzione quando nessuna di queste condizioni è applicabile, gli aggiornamenti software e le applicazioni richiesti non verranno installati nei client. Questa impostazione non impedisce agli utenti di installare le applicazioni del Catalogo applicazioni o l'installazione di pacchetti, programmi e sequenze attività sui computer client.  

-   **Criteri di esecuzione di PowerShell**  

     Configurare la modalità di esecuzione degli script di Windows PowerShell da parte dei client di Configuration Manager. Questi script sono spesso usati per il rilevamento negli elementi di configurazione per le impostazioni di conformità, ma possono anche essere inviati in una distribuzione come uno script standard.  

    -   **Ignora**: il client di Configuration Manager ignora la configurazione di Windows PowerShell nel computer client per consentire l'esecuzione degli script non firmati.  

    -   **Con restrizioni**: il client di Configuration Manager usa la configurazione di Windows PowerShell corrente nel computer client, che determina se è possibile eseguire gli script non firmati.  

    -   **Tutti firmati**: il client di Configuration Manager esegue gli script solo se sono firmati da un autore attendibile. Questa restrizione si applica in modo indipendente dalla configurazione di Windows PowerShell corrente sul computer client.  

     Questa opzione richiede almeno Windows PowerShell versione 2.0 e l'impostazione predefinita è **Tutti firmati**.  

    > [!TIP]  
    >  Se non è possibile eseguire gli script non firmati a causa di questa impostazione client, Configuration Manager segnala questo errore nei modi seguenti:  
    >   
    >  -   ID errore **0X87D00327** e la descrizione di **Script non firmato** come errore di stato distribuzione nell'area di lavoro **Monitoraggio** della console di Configuration Manager.  
    > -   I codici di errore e le descrizioni di **0X87D00327** e **Script non firmato** o **0X87D00320** e **L'host script non è stato ancora installato** con il tipo di errore **Errore di individuazione** nei report, come **Dettagli degli errori degli elementi di configurazione in una linea di base configurazione per un asset**.  
    > -   Il messaggio **Script is not signed (Error: 87D00327; Source: CCM)** nel file **DcmWmiProvider.log** .  

-   **Disabilitare sequenza casuale scadenza**  

     Questa impostazione determina se il client usa un ritardo di attivazione di un massimo di due ore per installare gli aggiornamenti software richiesti al raggiungimento della scadenza. Per impostazione predefinita, il ritardo di attivazione è disabilitato.  

     Per gli scenari relativi all'infrastruttura VDI, questo ritardo consente di distribuire l'elaborazione della CPU e il trasferimento dei dati per un computer che ha più macchine virtuali che eseguono il client di Configuration Manager. Anche se non si usa l'infrastruttura VDI, uno scenario in cui gli stessi aggiornamenti vengono installati contemporaneamente in molti client potrebbe determinare un incremento dell'utilizzo della CPU nel server del sito con impatto negativo, il rallentamento dei punti di distribuzione e una riduzione notevole della larghezza di banda della rete disponibile.  

     Se gli aggiornamenti software richiesti devono essere installati senza ritardo al raggiungimento della scadenza configurata, selezionare **Sì** per questa opzione.  

-   **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** 
    
     In alcuni casi, è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti del software obbligatori, anche oltre eventuali scadenze configurate. In genere questo potrebbe essere necessario quando un computer è stato disattivato per un lungo periodo di tempo ed è necessario installare un numero elevato di distribuzioni di applicazioni o aggiornamenti. Ad esempio, se un utente finale è appena tornato da una vacanza, potrebbe dover attendere un po' tempo mentre vengono installate le distribuzioni delle applicazioni scadute. Per risolvere il problema è possibile definire un periodo di tolleranza di imposizione distribuendo le impostazioni del client di Configuration Manager a una raccolta.
    È possibile impostare un periodo di tolleranza compreso tra 1 e 120 ore. Questa impostazione viene usata in combinazione con la proprietà di distribuzione **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente**. Per altre informazioni dettagliate, vedere [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Distribuire applicazioni)

##  <a name="computer-restart"></a>Riavvio del computer  
 Quando si specificano queste impostazioni di riavvio del computer, assicurarsi che il valore per l'intervallo di notifica temporanea di riavvio e quello per l'intervallo del conto alla rovescia finale siano inferiori, in termini di durata, alla finestra di manutenzione più breve applicata al computer.  

 Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **Gestire il client Endpoint Protection nei computer client**  

     Selezionare **True** o **Sì** se si vuole gestire i client di Endpoint Protection esistenti nei computer della gerarchia.  

     Selezionare questa opzione se il client di Endpoint Protection è già installato e si vuole gestirlo con Configuration Manager.  

     È anche possibile selezionare questa opzione se si vuole creare uno script per disinstallare una soluzione antimalware esistente, installare il client di Endpoint Protection e distribuire questo script usando un'applicazione di Configuration Manager o un pacchetto e programma.  

-   **Installare il client Endpoint Protection nei computer client**  

     Selezionare **True** **Sì** per installare e abilitare il client di Endpoint Protection in computer client in cui non è già installato.  

    > [!NOTE]  
    >  Se il client di Endpoint Protection è già installato, selezionando **False** **No** non verrà disinstallato il client di Endpoint Protection. Per disinstallare il client di Endpoint Protection, configurare l'impostazione client **Gestire il client Endpoint Protection nei computer client** su **False** o **No**, quindi distribuire un pacchetto e programma per disinstallare il client di Endpoint Protection.  

-   **Per i dispositivi con Windows Embedded con filtri di scrittura, confermare l'installazione del client di Endpoint Protection (richiesto riavvio)**  

     Selezionare **Sì** per disattivare il filtro di scrittura sul dispositivo con Windows Embedded e riavviare il dispositivo. Ciò conferma l'installazione nel dispositivo.  

     Se viene specificato **No** , il client viene installato in una sovrapposizione temporanea che viene cancellata al riavvio del dispositivo. In questo scenario, il client di Endpoint Protection non viene confermato fino a quando un'altra installazione non conferma le modifiche al dispositivo. Questa è l'impostazione predefinita.  

-   **Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection**  

     Selezionare **True** **Sì** per evitare un riavvio necessario del computer dopo l'installazione del client di Endpoint Protection.  

    > [!IMPORTANT]  
    >  Se il client di Endpoint Protection richiede un riavvio del computer e questa impostazione è configurata su **False**, il riavvio avrà luogo indipendentemente da qualsiasi finestra di manutenzione configurata.  

-   **Periodo di tempo consentito agli utenti per rimandare un riavvio necessario per completare l'installazione di Endpoint Protection (ore)**  

     Specificare il numero di ore che gli utenti possono impostare per rimandare un riavvio necessario del computer dopo l'installazione del client di Endpoint Protection. Questa opzione può essere configurata solo se l'opzione **Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection** è impostata su **False**.  

-   **Disattivare le origini alternative (quali Windows Update, Microsoft Windows Server Update Services o condivisioni UNC) per l'aggiornamento della definizione iniziale nei computer client**  

     Selezionare **True** o **Sì** se si vuole che Configuration Manager installi solo l'aggiornamento della definizione iniziale nei computer client. Questa impostazione può essere utile per evitare connessioni di rete non necessarie e ridurre la larghezza di banda durante l'installazione iniziale dell'aggiornamento della definizione.  

##  <a name="hardware-inventory"></a>Inventario hardware  

-   **Dimensioni massime file MIF personalizzate (KB)**  

     Specificare le dimensioni massime, in kilobyte (KB), consentite per ciascun file Management Information Format (MIF) personalizzato che sarà raccolto da un client durante il ciclo di inventario hardware. Se un file MIF supera questa dimensione, non sarà elaborato dall'inventario hardware di Configuration Manager. È possibile specificare una dimensione compresa tra 1 e 5.000 KB. Per impostazione predefinita, il valore è impostato su 250 KB. Questa impostazione non influenza la dimensione del file di dati di inventario hardware normale.  

    > [!NOTE]  
    >  Questa impostazione è disponibile solo nelle impostazioni del client predefinite.  

-   **Classi di inventario hardware**  

     In Configuration Manager è possibile estendere le informazioni hardware raccolte dai client senza modificare manualmente il file sms_def.mof. Fare clic su **Imposta classi** se si vuole estendere l'inventario hardware di Configuration Manager. Per altre informazioni, vedere [Come estendere l'inventario hardware in System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Raccogli file MIF**  

     Usare questa impostazione per specificare se raccogliere i file Managed Information Format (MIF) dai client di Configuration Manager durante l'inventario hardware.  

     Affinché un file MIF sia raccolto dall'inventario hardware, deve trovarsi nella posizione corretta nel computer client. Per impostazione predefinita, i file devono trovarsi dove di seguito descritto:  

    -   I file IDMIF devono trovarsi nella cartella Windows\System32\CCM\Inventory\Idmif.  

    -   I file NOIDMIF devono trovarsi nella cartella Windows\System32\CCM\Inventory\Noidmif.  

    > [!NOTE]  
    >  Questa impostazione è disponibile solo nelle impostazioni del client predefinite.  

##  <a name="metered-internet-connections"></a>Connessioni Internet a consumo  
 È possibile gestire la modalità di comunicazione dei computer client Windows 8 con i siti di Configuration Manager quando vengono usate connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

> [!NOTE]  
>  L'impostazione del client configurato non viene applicata ai computer client Windows 8 nei seguenti scenari:  
>   
>  -   Il computer usa una connessione dati in roaming: il client di Configuration Manager non esegue alcuna operazione che richiede il trasferimento dei dati nei siti di Configuration Manager.  
> -   Le proprietà di connessione di rete di Windows sono configurate come connessioni non a consumo: il client di Configuration Manager si comporta come se fosse in presenza di una connessione Internet non a consumo e pertanto trasferisce i dati ai siti di Configuration Manager.  

-   **Comunicazione dei client nelle connessioni Internet a consumo**  

     Dall'elenco a discesa, scegliere una delle seguenti operazioni per i computer client Windows 8:  

    -   **Consenti**: tutte le comunicazioni client sono consentite tramite la connessione Internet a consumo a meno che il dispositivo client non stia usando una connessione dati in roaming.  

    -   **Limite**: sono consentite solo le comunicazioni client seguenti tramite la connessione Internet a consumo:  

        -   Recupero dei criteri client  

        -   Messaggi di stato del client da inviare al sito  

        -   Richieste di installazione di software mediante il Catalogo applicazioni  

        -   Distribuzioni richieste (quando viene raggiunta la scadenza per l'installazione)  

        > [!IMPORTANT]  
        >  Se un utente avvia un'installazione software da Software Center o dal Catalogo applicazioni, queste sono sempre consentite, indipendentemente dalle impostazioni della connessione Internet a consumo.  

         Se viene raggiunto il limite per il trasferimento dei dati per la connessione Internet a consumo, il client non prova più a comunicare con i siti di Configuration Manager.  

    -   **Blocca**: il client di Configuration Manager non prova a comunicare con i siti di Configuration Manager in presenza di una connessione Internet a consumo. Questo è il valore predefinito.  

##  <a name="power-management"></a>Risparmio energia  

-   **Consentire agli utenti di escludere il dispositivo usato dal risparmio energia**  

     Nel menu a discesa selezionare **True** o **Sì** per consentire agli utenti di Software Center di escludere i computer dalle impostazioni di risparmio energia configurate.  

-   **Abilitare il proxy di riattivazione**  

     Specificare **Sì** per integrare l'impostazione Riattivazione LAN del sito quando è configurata per i pacchetti unicast.  

     Per altre informazioni sul proxy di riattivazione, vedere [Pianificare la riattivazione dei client in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Non abilitare il proxy di riattivazione in una rete di produzione senza prima comprenderne il funzionamento e valutarlo in un ambiente di test.  

-   **Numero di porta del proxy di riattivazione (UDP)**  

     Mantenere il valore predefinito per il numero di porta i computer di gestione usano per inviare i pacchetti di riattivazione ai computer in modalità di sospensione o modificare il numero in un valore a scelta.  

     Il numero della porta specificato viene configurato automaticamente per i client che eseguono Windows Firewall quando si configura l'opzione **Eccezione di Windows Firewall per il proxy di riattivazione** . Se i client eseguono un firewall diverso, è necessario configurarlo manualmente per consentire il numero della porta UDP specificato per questa impostazione.  

-   **Numero di porta di riattivazione LAN (UDP)**  

     Mantenere il valore predefinito di 9 a meno che non è stato modificato il numero di porta di riattivazione LAN (UDP) nelle **Proprietà**del sito nella scheda **Porte** .  

    > [!IMPORTANT]  
    >  Questo numero deve corrispondere al numero nelle **Proprietà**del sito. Se si modifica questo numero in un'unica posizione, non viene aggiornato automaticamente in un'altra posizione.  

##  <a name="remote-tools"></a>Strumenti remoti  

-   **Abilitare controllo remoto nei client** e **Profili delle eccezioni firewall**  

     Selezionare se il controllo remoto di Configuration Manager è abilitato per tutti i computer client che ricevono queste impostazioni client. Fare clic su **Configura** per abilitare il controllo da remoto e facoltativamente configurare le impostazioni firewall per consentire al controllo da remoto di funzionare nei computer client.  

     Per impostazione predefinita, il controllo remoto è disattivato.  

    > [!IMPORTANT]  
    >  Se le impostazioni del firewall non sono configurate, il controllo remoto potrebbe non funzionare correttamente.  

-   **Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center**  

     Selezionare se gli utenti possono modificare le opzioni di controllo remoto da Software Center.  

-   **Consentire il controllo remoto di un computer senza intervento dell'utente**  

     Selezionare se un amministratore può usare il comando remoto per accedere a un computer client che è disconnesso o bloccato. Solo un computer connesso e sbloccato può essere controllato da remoto quando questa impostazione è disattivata.  

-   **Richiedere all'utente l'autorizzazione di controllo remoto**  

     Selezionare se nel computer client verrà visualizzato un messaggio che richiede l'autorizzazione dell'utente prima di consentire una sessione di controllo remoto.  

-   **Concedere l'autorizzazione di controllo remoto al gruppo Administrators locale**  

     Selezionare se gli amministratori locali nel server che avviano la connessione di controllo remoto possono stabilire sessioni di controllo remoto nei computer client.  

-   **Livello di accesso consentito**  

     Specificare il livello di accesso di controllo remoto che sarà consentito. È possibile scegliere tra:  

    -   Controllo completo  

    -   Solo visualizzazione  

    -   Nessuno  

-   **Visualizzatori autorizzati**  

     Fare clic su **Imposta visualizzatori** per aprire la finestra di dialogo **Configura impostazione client** e specificare i nomi degli utenti Windows che possono stabilire sessioni di controllo remoto nei computer client.  

-   **Mostra icona di notifica sessione nella barra delle applicazioni**  

     Selezionare questa opzione per visualizzare un'icona nella barra delle applicazioni dei computer client per indicare che è attiva una sessione di controllo remoto.  

-   **Mostrare barra delle connessioni sessione**  

     Selezionare questa opzione per visualizzare una barra di connessione della sessione ad alta visibilità nei computer client per indicare che è attiva una sessione di controllo remoto.  

-   **Riprodurre un suono nel client**  

     Selezionare questa opzione per usare un suono per indicare quando una sessione di controllo remoto è attiva in un computer client. È possibile riprodurre un suono quando la sessione si connette o disconnette, oppure è possibile riprodurre un suono più volte durante la sessione.  

-   **Gestire le impostazioni di assistenza remota non richiesta**  

     Selezionare questa opzione per consentire a Configuration Manager di gestire le sessioni di assistenza remota non richiesta.  

     Nelle sessioni di assistenza remota non richiesta l'utente nel computer client non richiede assistenza per avviare una sessione.  

-   **Gestire le impostazioni di assistenza remota su richiesta**  

     Selezionare questa opzione per consentire a Configuration Manager di gestire le sessioni di assistenza remota richiesta.  

     Nelle sessioni di assistenza remota su richiesta l'utente nel computer client invia una richiesta di assistenza remota all'amministratore.  

-   **Livello di accesso per assistenza remota**  

     Selezionare il livello di accesso da assegnare alle sessioni di assistenza remota avviate nella console di Configuration Manager.  

    > [!NOTE]  
    >  L'utente nel computer client deve sempre concedere l'autorizzazione per avviare una sessione di assistenza remota.  

-   **Gestire le impostazioni di desktop remoto**  

     Selezionare questa opzione per consentire a Configuration Manager di gestire le sessioni di Desktop remoto per i computer.  

-   **Consentire ai visualizzatori autorizzati di connettersi mediante connessione desktop remoto**  

     Selezionare questa opzione per consentire agli utenti specificati nell'elenco di visualizzatori autorizzati di essere aggiunti al gruppo di utenti locale di Desktop remoto nei computer client.  

-   **Richiedere Autenticazione a livello di rete nei computer che eseguono il sistema operativo Windows Vista e versioni successive**  

     Selezionare questa opzione più sicura se si desidera usare l'autenticazione a livello di rete per stabilire connessioni di Desktop remoto nei computer client che eseguono Windows Vista o sistemi operativi successivi. L'autenticazione a livello di rete richiede inizialmente meno risorse del computer remoto perché completa l'autenticazione utente prima di stabilire una connessione di Desktop remoto. Questo metodo è più sicuro perché permette di proteggere il computer da utenti o software dannosi e riduce il rischio di attacchi di tipo Denial of Service.  

## <a name="software-deployment"></a>Distribuzione software  

-   **Pianificare nuova valutazione per le distribuzioni**  

     Configurare una pianificazione che indichi quando Configuration Manager deve eseguire una nuova valutazione delle regole dei requisiti per tutte le distribuzioni. Il valore predefinito è ogni 7 giorni.  

    > [!IMPORTANT]  
    >  È consigliabile non modificare questo valore in un valore inferiore rispetto al valore predefinito poiché potrebbe influire negativamente sulla prestazione della rete e dei computer client.  

     È anche possibile avviare questa azione da un computer client di Configuration Manager selezionando l'azione **Ciclo di valutazione distribuzione applicazione** dalla scheda **Azioni** di **Configuration Manager** nel Pannello di controllo.  

##  <a name="software-inventory"></a>Inventario software  

-   **Dettaglio report inventario**  

     Specificare il livello delle informazioni sui file nell'inventario. È possibile includere nell'inventario i dettagli solo sul file, i dettagli sul prodotto associato con il file, oppure è possibile includere nell'inventario tutte le informazioni sul file.  

-   **Tipi di file da includere nell'inventario**  

     Per specificare i tipi di file nell'inventario, fare clic su **Imposta tipi** , quindi configurare le opzioni seguenti nella finestra di dialogo **Configura impostazione client** :  

    > [!NOTE]  
    >  Se più impostazioni client personalizzate vengono applicate a un computer, l'inventario restituito da ogni impostazione verrà unito.  

    -   Fare clic sull'icona Nuovo per aggiungere un nuovo tipo di file nell'inventario, quindi specificare le informazioni seguenti nella finestra di dialogo **Proprietà file in inventario** :  

    -   **Nome** : specificare un nome per il file che si desidera includere nell'inventario. È possibile usare il carattere **\*** per rappresentare qualsiasi stringa di testo e il carattere **?** per rappresentare qualsiasi carattere. Ad esempio, se si vuole includere nell'inventario tutti i file con estensione doc, specificare **\*.doc**.  

    -   **Percorso** : fare clic su **Imposta** per aprire la finestra di dialogo **Proprietà percorso** . È possibile configurare l'inventario software per cercare il file specificato in tutti i dischi rigidi del client, cercare un percorso specificato (ad esempio **C:\Cartella**) o una variabile specificata (ad esempio, *%windir%*) ed è inoltre possibile cercare tutte le sottocartelle in un percorso specificato.  

    -   **Escludi file crittografati e compressi** : quando si seleziona questa opzione, tutti i file che sono stati compressi o crittografati non verranno inclusi nell'inventario.  

    -   **Escludi file nella cartella Windows** : quando si seleziona questa opzione, tutti i file nella cartella Windows e nelle relative sottocartelle non verranno inclusi nell'inventario.  

    -   Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà file in inventario** .  

    -   Aggiungere tutti i file che si desidera includere nell'inventario e quindi fare clic su **OK** per chiudere la finestra di dialogo **Configura impostazione client** .  

-   **Raccogli file**  

     Se si desidera raccogliere i file dai computer client, fare clic su **Imposta file** e quindi configurare le opzioni seguenti:  

    > [!NOTE]  
    >  Se più impostazioni client personalizzate vengono applicate a un computer, l'inventario restituito da ogni impostazione verrà unito.  

    -   Nella finestra di dialogo **Configura impostazione client** fare clic sull'icona Nuovo per aggiungere un file da recuperare.  

    -   Nella finestra di dialogo **Proprietà file recuperato** immettere le informazioni seguenti:  

    -   **Nome** : specificare un nome per il file che si desidera recuperare. È possibile usare il carattere **\*** per rappresentare qualsiasi stringa di testo e il carattere **?** per rappresentare qualsiasi carattere.  

    -   **Percorso** : fare clic su **Imposta** per aprire la finestra di dialogo **Proprietà percorso** . È possibile configurare l'inventario software per cercare il file specificato in tutti i dischi rigidi del client, cercare un percorso specificato (ad esempio **C:\Cartella**) o una variabile specificata (ad esempio, *%windir%*) ed è inoltre possibile cercare tutte le sottocartelle in un percorso specificato.  

    -   **Escludi file crittografati e compressi** : quando si seleziona questa opzione, tutti i file che sono stati compressi o crittografati non verranno recuperati.  

    -   **Interrompere la raccolta file quando le dimensioni totali dei file superano (KB)** : specificare le dimensioni del file (in KB) oltre le quali non verranno più recuperati altri file specificati in **Nome** .  

        > [!NOTE]  
        >  Il server del sito raccoglie le cinque versioni più recenti dei file e le archivia nella *&lt;directory di installazione di Configuration Manager\>***\Inboxes\Sinv.box\Filecol**. Se un file non è stato modificato dopo l'ultima raccolta dell'inventario software, il file non verrà raccolto nuovamente.  
        >   
        >  File di dimensioni superiori a 20 MB non vengono raccolti dall'inventario software.  
        >   
        >  Il valore **Dimensioni massime per tutti i file raccolti (KB)** nella finestra di dialogo **Configura impostazione client** visualizza le dimensioni massime per tutti i file raccolti. Quando viene raggiunta questa dimensione, la raccolta di file verrà interrotta. Tutti i file già raccolti vengono mantenuti e inviati al server del sito.  

        > [!IMPORTANT]
        >  Se si configura l'inventario software per raccogliere molti file di grandi dimensioni, questo potrebbe influire negativamente sulle prestazioni del server di rete e del sito.  

         Per informazioni sulla cronologia di inventario, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario software in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà file recuperato** .  

    -   Aggiungere tutti i file che si desidera raccogliere e quindi fare clic su **OK** per chiudere la finestra di dialogo **Configura impostazione client** .  

-   **Impostare i nomi**  

     Durante l'inventario del software, i nomi di produttore e prodotto vengono recuperati dalle informazioni di intestazione dei file installati sui client nel sito. Poiché questi nomi non sono sempre standardizzati nelle informazioni di intestazione dei file, quando si visualizzano le informazioni sull'inventario del software in Esplora inventario risorse o si eseguono query, è possibile che vengano visualizzate versioni diverse dello stesso nome di produttore o prodotto. Per standardizzare questi nomi visualizzati, fare clic su **Imposta nomi** , quindi configurare le opzioni seguenti nella finestra di dialogo **Configura impostazione client** :  

    -   **Tipo nome:** l'inventario software raccoglie informazioni su produttori e prodotti. Dall'elenco a discesa selezionare se si desidera configurare i nomi visualizzati per un **Produttore** o un **Prodotto**.  

    -   **Nome visualizzato:** specifica il nome visualizzato da usare al posto dei nomi inclusi nell'elenco **Nomi di inventario** . È possibile fare clic sull'icona Nuovo per specificare un nuovo nome visualizzato.  

    -   **Nomi di inventario** : fare clic sull'icona Nuovo per aggiungere un nuovo nome di inventario, che verrà sostituito nell'inventario software dal nome selezionato nell'elenco **Nome visualizzato** . È possibile aggiungere più nomi che verranno sostituiti.  

##  <a name="software-updates"></a>Aggiornamenti software  

-   **Abilitare aggiornamento software nei client**  

     Usare questa impostazione per abilitare gli aggiornamenti software nei client di Configuration Manager. Se si deseleziona questa impostazione, Configuration Manager rimuoverà i criteri di distribuzione esistenti dal client. Quando si riattiva questa impostazione, il client scaricherà il criterio di distribuzione corrente.  

    > [!IMPORTANT]  
    >  Quando si deseleziona questa impostazione, Protezione accesso alla rete e i criteri di Impostazioni di conformità basati sulle impostazioni dei dispositivi per gli aggiornamenti software non funzioneranno più.  

-   **Pianificazione analisi aggiornamento software**  

     Usare questa impostazione per specificare la frequenza con cui il client avvia un'analisi di valutazione conformità per l'aggiornamento software. L'analisi di valutazione della conformità determina lo stato degli aggiornamenti software sul client (ad esempio, obbligatorio o installato). Per altre informazioni sulla valutazione della conformità, vedere [Valutazione della conformità negli aggiornamenti software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Per impostazione predefinita, viene usata una pianificazione semplice e l'analisi di conformità viene avviata ogni 7 giorni. È possibile scegliere di creare una pianificazione personalizzata per specificare una data e un'ora di avvio specifiche, per determinare se usare UTC o l'ora locale e per configurare l'intervallo ricorrente per un giorno specifico della settimana.  

    > [!NOTE]  
    >  Se si specifica un intervallo inferiore a 1 giorno, Configuration Manager userà automaticamente il valore pari a 1 giorno come impostazione predefinita.  

    > [!WARNING]  
    >  L'ora di avvio effettiva nei computer client corrisponde all'ora di avvio con l'aggiunta di una quantità di tempo casuale, fino a un massimo di due ore. Ciò impedisce ai computer client di avviare l'analisi e di connettersi contemporaneamente a Windows Server Update Services (WSUS) sul server del punto di aggiornamento software attivo.  

-   **Pianificare nuova valutazione di distribuzione**  

     Usare questa impostazione per configurare la frequenza della nuova valutazione degli aggiornamenti software da parte dell'Agente client aggiornamenti software per la verifica dello stato di installazione nei computer client di Configuration Manager. Se gli aggiornamenti software installati in precedenza non sono più disponibili nei computer client, ma sono ancora necessari, verranno reinstallati. È necessario che la pianificazione della nuova valutazione della distribuzione venga modificata in base ai criteri aziendali per la conformità degli aggiornamenti software, in base alla possibilità o meno degli utenti di disinstallare aggiornamenti software e così via. Occorre inoltre tenere presente che ogni ciclo di nuova valutazione della distribuzione produce attività di rete e della CPU del computer client. Per impostazione predefinita, viene usata una pianificazione semplice e l'analisi della nuova valutazione della distribuzione viene avviata ogni 7 giorni.  

    > [!NOTE]  
    >  Se si specifica un intervallo inferiore a 1 giorno, Configuration Manager userà automaticamente il valore pari a 1 giorno come impostazione predefinita.  

-   **Quando viene raggiunta la data di scadenza qualsiasi aggiornamento software, installare tutte le altre distribuzioni di aggiornamento software con scadenze che rientrano nel periodo di tempo specificato**  

     Usare questa impostazione per installare tutti gli aggiornamenti software in installazioni necessarie con scadenze che rientrano in un periodo di tempo specificato. Quando viene raggiunta una scadenza per una distribuzione dell'aggiornamento software necessaria, verrà avviata l'installazione nei client per gli aggiornamenti software nella distribuzione. Questa impostazione determina se viene avviata anche l'installazione degli aggiornamenti software definiti in altre distribuzioni necessarie con scadenza configurata entro il periodo di tempo specificato.  

     Usare questa impostazione per accelerare l'installazione di aggiornamenti software per aggiornamenti software necessari, per incrementare potenzialmente la sicurezza, ridurre potenzialmente le notifiche visualizzate e ridurre potenzialmente il numero di riavvii di sistema nei computer client. Per impostazione predefinita, questa impostazione non è attivata.  

-   **Periodo di tempo entro cui verranno installate anche tutte le distribuzioni in sospeso con scadenza in questo periodo**  

     Usare questa impostazione per specificare l'intervallo di tempo per l'impostazione precedente. È possibile immettere un valore compreso tra 1 e 23 e tra 1 e 365 giorni. Per impostazione predefinita, questa impostazione è configurata su 7 giorni.  

##  <a name="user-and-device-affinity"></a>Affinità dispositivi e utenti  

-   **Soglia di utilizzo di affinità utente dispositivo (minuti)**  

     Specificare il numero di minuti prima della creazione di un mapping di affinità del dispositivo utente da parte di Configuration Manager.  

-   **Soglia di utilizzo di affinità utente dispositivo (giorni)**  

     Specificare il numero di giorni in cui viene misurata la soglia di affinità in base all'utilizzo.  

    > [!NOTE]  
    >  Ad esempio, se **Soglia di utilizzo di affinità utente dispositivo (minuti)** viene specificato come **60** minuti e **Soglia di utilizzo di affinità utente dispositivo (giorni)** viene specificato come **5** giorni, l'utente dovrà usare il dispositivo per 60 minuti in un periodo di 5 giorni per creare automaticamente un'affinità utente dispositivo.  

-   **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo**  

     Selezionare **True** o **Sì** per abilitare Configuration Manager a creare automaticamente affinità utente dispositivo in base alle informazioni raccolte sull'utilizzo.  

##  <a name="mobile-devices"></a>Dispositivi mobili  

-   **Profilo di registrazione del dispositivo mobile**  

     Per configurare questa impostazione, è innanzitutto necessario impostare su **True** l'impostazione **Consentire agli utenti di registrare i dispositivi mobili**dell'utente del dispositivo mobile. È quindi possibile fare clic su **Imposta profilo** per specificare un profilo di registrazione contenente informazioni sul modello di certificato da usare durante il processo di registrazione, il sito contenente un punto di registrazione e un punto proxy di registrazione e infine il sito che gestirà il dispositivo dopo la registrazione.  

    > [!IMPORTANT]  
    >  Assicurarsi di aver configurato un modello di certificato da usare per la registrazione del dispositivo mobile prima di configurare questa opzione.  

##  <a name="enrollment"></a>Registrazione  

-   **Profilo di registrazione del dispositivo mobile**  

     Per configurare questa impostazione, è innanzitutto necessario impostare su **Sì** l'impostazione **Consentire agli utenti di registrare i dispositivi mobili e i computer Mac**dell'utente di registrazione. È quindi possibile fare clic su **Imposta profilo** per specificare un profilo di registrazione contenente informazioni sul modello di certificato da usare durante il processo di registrazione, il sito contenente un punto di registrazione e un punto proxy di registrazione e infine il sito che gestirà il dispositivo dopo la registrazione.  

    > [!IMPORTANT]  
    >  Assicurarsi di aver configurato un modello di certificato da usare per la registrazione del dispositivo mobile o per la registrazione del certificato client Mac prima di configurare questa opzione.  

## <a name="user-and-device-affinity"></a>Affinità dispositivi e utenti  

-   **Consentire all'utente di definire i dispositivi primari**  

     Specificare se gli utenti sono autorizzati a identificare i propri dispositivi primari dal Catalogo applicazioni nella scheda **Dispositivi personali** .  



<!--HONumber=Dec16_HO3-->


