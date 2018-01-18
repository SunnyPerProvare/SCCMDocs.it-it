---
title: Impostazioni client
titleSuffix: Configuration Manager
description: Scegliere le impostazioni client tramite la console di System Center Configuration Manager.
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 230d608c9ebc8126d7d8e18f7211875a2155bb7b
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Informazioni sulle impostazioni client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile gestire tutte le impostazioni client nella console di Configuration Manager dal nodo **Impostazioni client** nell'area di lavoro **Amministrazione**. Con Configuration Manager viene specificato un set di impostazioni predefinite. Quando si modificano le impostazioni client predefinite, tali impostazioni vengono applicate a tutti i client nella gerarchia. È anche possibile configurare le impostazioni client personalizzate, che sostituiscono le impostazioni client predefinite quando vengono assegnate a raccolte. Per altre informazioni, vedere [Come configurare le impostazioni client](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Servizio trasferimento intelligente in background  

-   **Limitare la larghezza di banda di rete massima per i trasferimenti in background BITS**   </br>
   Se questa opzione corrisponde a **Sì**, i client usano la limitazione larghezza di banda BITS. Per configurare le altre impostazioni di questo gruppo, è necessario abilitare questa impostazione. 

-   **Ora di inizio dell'intervallo di limitazione**   </br>
   Specificare l'ora di inizio locale per l'intervallo di limitazione BITS.  

-   **Ora di fine dell'intervallo di limitazione**   </br>
   Specificare l'ora di fine locale per l'intervallo di limitazione BITS. Se il valore è lo stesso di **Ora di inizio dell'intervallo di limitazione**, la limitazione BITS è sempre abilitata.  

-   **Velocità massima di trasferimento durante l'intervallo di limitazione (Kbps)** </br>
    Specifica la velocità massima di trasferimento che i client possono usare durante l'intervallo.  

-   **Consentire i download BITS all'esterno dell'intervallo di limitazione**   </br>
   Consente ai client di usare impostazioni BITS separate all'esterno dell'intervallo specificato.  

-   **Velocità massima di trasferimento all'esterno dell'intervallo di limitazione (Kbps)**   </br>
   Specifica la velocità massima di trasferimento usata dai client al di fuori dell'intervallo di limitazione larghezza di banda BITS.  



## <a name="client-cache-settings"></a>Impostazioni della cache dei client

- **Configura BranchCache** </br>
  Usare questa opzione per configurare il computer client per [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Per consentire la memorizzazione nella cache BranchCache nel client, impostare **Abilita BranchCache** su **Sì**.

    - **Abilita BranchCache** </br>
    Abilita BranchCache nei computer client.

    - **Dimensioni massime della cache BranchCache (percentuale del disco)** </br>
    Percentuale del disco consentita dall'utente per l'uso da parte di BranchCache. 

- **Configurare la dimensione della cache client** </br>
  Nei computer Windows la cache client di Configuration Manager archivia i file temporanei usati per installare applicazioni e programmi. Se questa opzione è impostata su **No**, il valore predefinito è 5.120 MB.</br>
    Scegliere **Sì** e quindi specificare:
    - **Dimensioni massime della cache (MB)**
    - **Dimensioni massime della cache (percentuale del disco)** </br>
    La cache client può raggiungere la dimensione massima consentita, in MB o in percentuale del disco, *a seconda di quale di questi due valori è inferiore*. 

- **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** </br>
    Abilita la [peer cache](/sccm/core/plan-design/hierarchy/client-peer-cache) per i client di Configuration Manager. Scegliere **Sì** e quindi specificare le informazioni relative alla porta attraverso la quale il client comunica con il computer peer. 
    - **Porta per la trasmissione di rete iniziale** (impostazione predefinita 8004)
    - **Porta per il download di contenuto da peer** (impostazione predefinita 8003) </br>
    Configuration Manager configura automaticamente le regole di Windows Firewall in modo che questo tipo di traffico sia consentito. Se si usa un firewall diverso, è necessario configurare le regole manualmente.




## <a name="client-policy"></a>Criteri client  

-   **Intervallo di polling dei criteri client (minuti)**  </br>
     Specifica la frequenza con cui i client di Configuration Manager seguenti scaricano criteri client:  
      -   Computer Windows (ad esempio, desktop, server, portatili)  
      -   Dispositivi mobili registrati da Configuration Manager  
      -   Computer Mac  
      -   Computer con sistema operativo Linux o UNIX  

-   **Abilitare i criteri utente nei client**   </br>
   Se si imposta questa opzione su **Sì** e si usa l'[individuazione utente](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), i client ricevono applicazioni e programmi destinati all'utente connesso.  

    Il Catalogo applicazioni riceve l'elenco del software disponibile per gli utenti dal server del sito. Questa impostazione quindi non deve corrispondere necessariamente a **Sì** perché gli utenti possano visualizzare e richiedere applicazioni dal Catalogo applicazioni. Se questa impostazione corrisponde a **No**, quando gli utenti usano il Catalogo applicazioni i comportamenti seguenti non funzionano:  

      -   Gli utenti non possono installare le applicazioni che vedono nel Catalogo applicazioni.  

      -   Gli utenti non visualizzano le notifiche relative alle proprie richieste di approvazione applicazione. Al contrario, devono aggiornare il Catalogo applicazioni e verificare lo stato di approvazione.  

      -   Gli utenti non ricevono revisioni e aggiornamenti per le applicazioni pubblicate nel Catalogo applicazioni. Gli utenti però visualizzano le modifiche alle informazioni sulle applicazioni nel Catalogo applicazioni.  

      -   Se si rimuove la distribuzione di un'applicazione dopo che il client ha installato quest'ultima dal Catalogo applicazioni, i client continuano a controllare che l'applicazione sia installata per un massimo di due giorni.  

    Se, in aggiunta, questa impostazione corrisponde a **No**, gli utenti non ricevono le applicazioni obbligatorie distribuite dall'amministratore per gli utenti stessi. Utenti non ricevono neanche le altre attività di gestione nei criteri utente.  

    Questa impostazione si applica agli utenti i cui computer si trovino nell'intranet e su Internet. Se si vuole che i criteri utente siano abilitati anche su Internet, l'impostazione deve corrispondere a **Sì**.  

-   **Abilitare le richieste dei criteri utente dai client Internet**   </br>
   Configurare questa impostazione su **Sì** perché gli utenti ricevano i criteri utente nei computer basati su Internet. Devono essere rispettati anche i requisiti seguenti:  

      -   Il client e il sito devono essere configurati per la gestione client basata su Internet

      -   L'impostazione **Abilitare i criteri utente nei client** deve essere **Sì**  

      -   Il punto di gestione basato su Internet esegue l'autenticazione dell'utente tramite l'autenticazione di Windows (Kerberos o NTLM)  

       Se si imposta questa opzione su **No** o uno o più dei requisiti precedenti non vengono soddisfatti, un computer connesso a Internet riceve solo criteri computer. In questo scenario, gli utenti possono comunque visualizzare, richiedere e installare applicazioni da un Catalogo applicazioni basato su Internet. Se questa impostazione corrisponde a **No**, ma **Abilitare i criteri utente nei client** corrisponde a **Sì**, gli utenti ricevono i criteri client solo quando il computer è connesso alla Intranet.  

       Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Le richieste di approvazione dell'applicazione da parte degli utenti non richiedono criteri utente o l'autenticazione dell'utente.  


## <a name="cloud-services"></a>Servizi cloud

-   **Consentire accesso al punto di distribuzione cloud** </br>
    Configurare questa impostazione su **Sì** perché i client possano ottenere contenuto da un punto di distribuzione cloud. Questa impostazione non richiede che il dispositivo sia basato su Internet.

-    **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory** </br> Quando si configura Azure Active Directory per il supporto dell'aggiunta ibrida, Configuration Manager configura i dispositivi Windows 10 per questa funzionalità. Per altre informazioni, vedere [How to configure hybrid Azure Active Directory joined devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (Come configurare dispositivi aggiunti ad Azure Active Directory in modo ibrido).

-   **Consenti ai client di usare un gateway di gestione cloud** </br>
    Per impostazione predefinita, tutti i client connessi a Internet possono usare qualsiasi [Cloud Management Gateway ](/sccm/core/clients/manage/plan-cloud-management-gateway) disponibile. Un esempio in cui questa impostazione viene configurata su **No** è la necessità di definire un ambito per l'utilizzo del servizio, ad esempio un progetto pilota o la riduzione dei costi.



##  <a name="compliance-settings"></a>Impostazioni di conformità  

-   **Abilitare valutazione di conformità nei client** </br>
    Per configurare le altre impostazioni di questo gruppo, questa impostazione deve corrispondere a **Sì**.
 
-   **Valutazione di conformità della pianificazione**   </br>
     Fare clic su **Pianificazione** per creare la pianificazione predefinita per le distribuzioni della linea di base di configurazione. Questo valore può essere configurato per ogni linea di base nella finestra di dialogo **Linea di base configurazione distribuzione**.  

-   **Abilitare i dati e profili utente**   </br>
     Scegliere **Sì** se si vogliono distribuire elementi di configurazione [dati e profili utente](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente computer  
-   Notifiche utente per le distribuzioni richieste </br>
    Per altre informazioni sulle tre impostazioni seguenti, vedere [Notifiche utente per le distribuzioni richieste](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -   **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)**
    -   **Meno di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)**  </br>
    -   **Meno di 1 ora alla scadenza di distribuzione. Avvisare l'utente ogni (minuti)**  </br>

-   **Punto per siti Web del Catalogo applicazioni predefinito**   </br>
     Configuration Manager usa questa impostazione per connettere gli utenti al Catalogo applicazioni dal Software Center. Fare clic su **Imposta sito** per specificare un server che ospita il punto per siti Web del Catalogo applicazioni. Immettere il nome NetBIOS o l'FQDN e specificare il rilevamento automatico o un URL per distribuzioni personalizzate. Nella maggior parte dei casi, il rilevamento automatico è la scelta migliore in quanto offre i seguenti vantaggi:  

    -   Se il sito ha un punto per siti Web del Catalogo applicazioni, ai client viene assegnato automaticamente un punto per siti Web del Catalogo applicazioni dal sito stesso.  

    -   I client preferiscono punti per siti Web del Catalogo applicazioni abilitati per HTTPS nell'Intranet rispetto ai server solo HTTP. Questa funzionalità garantisce la protezione da server non autorizzati.

    -   Il punto di gestione offre ai client basati su Internet un punto per siti Web del Catalogo applicazioni basato su Internet. Il punto di gestione offre ai client basati su Intranet un punto per siti Web del Catalogo applicazioni basato su Intranet.  

     Il rilevamento automatico non garantisce che ai client venga assegnato il punto per siti Web del Catalogo applicazioni più vicino. Si potrebbe decidere di non usare **Rileva automaticamente** per i seguenti motivi:  

     -   Si desidera configurare manualmente il server più vicino per il client o assicurarsi che non si connettano a un server con una connessione di rete lenta.  

     -   Si desidera controllare quali client si connettono a quale server. Questa configurazione può essere usata a scopo di test, per migliorare le prestazioni o per motivi aziendali.  

     -   È necessario evitare di attendere fino a 25 ore o una modifica di rete perché i client possano usare un altro punto per siti Web del Catalogo applicazioni.  

     Se si specifica il punto per siti Web del Catalogo applicazioni invece di usare il rilevamento automatico, specificare il nome NetBIOS invece del valore FQDN dell'intranet. Questa configurazione riduce la probabilità che il Web browser chieda le credenziali all'utente al momento dell'accesso a un Catalogo applicazioni basato su Intranet. Per usare il nome NetBIOS, è necessario che siano applicabili le seguenti condizioni:  

     -   Il nome NetBIOS viene specificato nelle proprietà del punto per siti Web del Catalogo applicazioni.  

     -   Si usa WINS oppure tutti i client si trovano nello stesso dominio del punto per siti Web del Catalogo applicazioni.  

     -   È possibile configurare il punto per siti Web del Catalogo applicazioni per connessioni client HTTP oppure configurare il server per HTTPS. Il certificato del server Web contiene il nome NetBIOS.  

     In genere, agli utenti vengono richieste le credenziali quando l'URL contiene un FQDN, ma non quando l'URL è un nome NetBIOS. Agli utenti verrà sempre richiesto quando si connettono da Internet, poiché questa connessione deve usare l'FQDN Internet. Quando si usa un client basato su Internet e il Web browser chiede le credenziali all'utente, assicurarsi che il punto per siti Web del Catalogo applicazioni possa connettersi a un controller di dominio per l'account dell'utente stesso. Questa configurazione consente l'autenticazione dell'utente tramite Kerberos.  

    > [!NOTE]  
    >  Funzionamento del rilevamento automatico:  
    >   
    >  Il client effettua una richiesta di posizione del servizio a un punto di gestione. Se nello stesso sito del client c'è un punto per siti Web del Catalogo applicazioni, tale server viene assegnato al client come server del Catalogo applicazioni da usare. Quando nel sito è disponibile più di un punto per siti Web del Catalogo applicazioni, un server abilitato per HTTPS ha la precedenza su un server non abilitato per HTTPS. Dopo l'applicazione di questo filtro, a tutti i client viene assegnato uno dei server da usare come Catalogo applicazioni; Configuration Manager non bilancia il carico tra più server. Quando il sito del client non contiene un punto per siti Web del Catalogo applicazioni, il punto di gestione restituisce in modo non deterministico un punto per siti Web del Catalogo applicazioni dalla gerarchia.  
    >   
    >  Per i client basati su Intranet, se si configura il punto per siti Web del Catalogo applicazioni con un nome NetBIOS per l'URL del Catalogo applicazioni, il punto di gestione assegna ai client questo nome NetBIOS anziché il valore FQDN dell'Intranet. Per i client basati su Internet, il punto di gestione assegna ai client solo l'FQDN Internet.  
    >   
    >  Il client effettua questa richiesta di posizione del servizio ogni 25 ore oppure ogni volta che rileva una modifica di rete. Ad esempio, se il client passa dalla Intranet a Internet e individua un punto di gestione basato su Internet, tale punto assegna i server del punto per siti Web del Catalogo applicazioni ai client.  

-   **Aggiungere il sito Web del Catalogo applicazioni predefinito all'area siti attendibili di Internet Explorer**   </br>
     Se questa opzione corrisponde a **Sì**, il client aggiunge automaticamente l'URL del sito Web del Catalogo applicazioni predefinito corrente all'area siti attendibili di Internet Explorer.  

     Questa impostazione garantisce che l'impostazione di Internet Explorer in modalità protetta non sia abilitata. Se la modalità protetta è abilitata, il client di Configuration Manager potrebbe non essere in grado di installare applicazioni dal Catalogo applicazioni. Per impostazione predefinita, l'area siti attendibili supporta inoltre l'accesso utente per il Catalogo applicazioni, il che richiede l'autenticazione di Windows.  

     Se si lascia questa opzione impostata su **No**, i client di Configuration Manager potrebbero non essere in grado di installare applicazioni dal Catalogo applicazioni. Un metodo alternativo consiste nel configurare queste impostazioni di Internet Explorer in un'altra area per l'URL del Catalogo applicazioni usata dai client.  

    > [!NOTE]  
    >  Ogni volta che Configuration Manager aggiunge un Catalogo applicazioni predefinito all'area siti attendibili, rimuove gli URL del Catalogo applicazioni aggiunti in precedenza.  
    >   
    >  Se l'URL è già specificato in una delle aree di sicurezza, Configuration Manager non può aggiungerlo. In questo scenario è necessario rimuovere l'URL dall'altra area o configurare manualmente le impostazioni di Internet Explorer richieste.  

-   **Consentire l'esecuzione in modalità di attendibilità elevata delle applicazioni Silverlight**   </br>
     Perché gli utenti possano usare il Catalogo applicazioni, questa impostazione deve corrispondere a **Sì**.  

     L'eventuale modifica di questa impostazione ha effetto al successivo caricamento del browser o aggiornamento della finestra del browser attualmente aperta da parte degli utenti.  

     Per altre informazioni su questa impostazione, vedere [Certificati per Microsoft Silverlight 5 e modalità di attendibilità elevata richiesta per il Catalogo applicazioni](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Nome organizzazione visualizzato in Software Center**   </br>
     Digitare il nome visualizzato dagli utenti in Software Center. Queste informazioni di personalizzazione consentono agli utenti di identificare questa applicazione come origine attendibile.  

-   **Usa il nuovo Software Center**   </br>
     Se si configura questa impostazione client su **Sì**, tutti i computer client usano il nuovo Software Center. Software Center visualizza le applicazioni disponibili per gli utenti precedentemente accessibili solo nel Catalogo applicazioni. Il Catalogo applicazioni richiede Silverlight, che non è un prerequisito per il nuovo Software Center.   

     I ruoli del sistema del sito del punto per siti Web del Catalogo applicazioni e del punto per servizi Web del Catalogo applicazioni continuano a essere necessari per visualizzare le app disponibili per gli utenti in Software Center.  

     Per altre informazioni, vedere [Plan for and configure application management](../../../apps/plan-design/plan-for-and-configure-application-management.md) (Pianificare e configurare la gestione delle applicazioni).  

-   **Abilita le comunicazioni con il servizio di attestazione dell'integrità**  </br>
    Configurare questa impostazione su **Sì** perché i dispositivi Windows 10 possano usare l'[attestazione dell'integrità](/sccm/core/servers/manage/health-attestation). Quando si abilita questa impostazione, è disponibile per la configurazione anche l'impostazione seguente.

    -   **Usare il servizio di attestazione dell'integrità locale** </br>
        Configurare questa impostazione su **Sì** perché i dispositivi usino un servizio locale. Configurare questa impostazione su **No** perché i dispositivi usino un servizio basato sul cloud di Microsoft.  

-   **Autorizzazioni di installazione**   </br>
    > [!WARNING]  
    >  Questa impostazione è valida per il Catalogo applicazioni e Software Center. Questa impostazione non ha alcun effetto se gli utenti usano il Portale aziendale.  

     Configurare la modalità di avvio dell'installazione del software, degli aggiornamenti software e delle sequenze attività da parte degli utenti:  

    -   **Tutti gli utenti**: utenti con qualsiasi autorizzazione eccetto Guest  

    -   **Solo amministratori**: gli utenti devono far parte del gruppo Administrators locale  

    -   **Solo amministratori e utenti primari**: gli utenti devono far parte del gruppo Administrators locale o devono essere utenti primari del computer  

    -   **Nessun utente**: nessun utente connesso a un computer client può avviare l'installazione del software, degli aggiornamenti software e delle sequenze di attività. Le distribuzioni obbligatorie per il computer vengono sempre installate alla scadenza. Gli utenti non possono avviare l'installazione del software dal Catalogo applicazioni o da Software Center.  

-   **Sospendere immissione PIN di BitLocker al riavvio**  </br>
     Se il computer richiede l'immissione PIN di BitLocker, questa opzione ignora tale richiesta quando il computer viene riavviato dopo l'installazione di software.  

    -   **Sempre**: Configuration Manager sospende temporaneamente BitLocker dopo aver installato il software che richiede un riavvio e aver iniziato un riavvio del computer. Questa impostazione si applica solo se il riavvio del computer viene avviato da Configuration Manager. Questa impostazione non sospende la richiesta di immissione PIN di BitLocker quando l'utente riavvia il computer. La richiesta di immissione PIN di BitLocker viene ripristinata dopo l'avvio di Windows.

    -   **Mai**: Configuration Manager non sospende BitLocker al successivo avvio del computer dopo aver installato software che richiede un riavvio. In questo scenario, l'installazione del software non può finire fino a quando l'utente immette il PIN per completare il processo di avvio e caricamento standard di Windows.

-   **Il software aggiuntivo gestisce la distribuzione delle applicazioni e degli aggiornamenti software**  </br>
     Attivare questa opzione solo in presenza di una delle seguenti condizioni:  

    -   Si usa una soluzione per fornitori che richiede l'abilitazione di questa impostazione.  

    -   Per gestire le notifiche dell'agente client e l'installazione delle applicazioni e degli aggiornamenti software, si usa il Software Development Kit (SDK) di Configuration Manager.  

    > [!WARNING]  
    >  Se si sceglie questa opzione quando non è soddisfatta alcuna di queste condizioni, il client non installa gli aggiornamenti software e le applicazioni obbligatorie. Questa impostazione non impedisce agli utenti di installare le applicazioni del Catalogo applicazioni né di installare pacchetti, programmi e sequenze di attività.  

-   **Criteri di esecuzione di PowerShell**  </br>
     Configurare la modalità di esecuzione degli script di Windows PowerShell da parte dei client di Configuration Manager. Questi script sono spesso usati per il rilevamento negli elementi di configurazione per le impostazioni di conformità. Possono anche essere inviati in una distribuzione come script standard.  

    -   **Ignora**: il client di Configuration Manager ignora la configurazione di Windows PowerShell nel computer client per consentire l'esecuzione degli script non firmati.  

    -   **Con restrizioni**: il client di Configuration Manager usa la configurazione di Windows PowerShell corrente nel computer client. Questa configurazione determina se possono essere eseguiti script non firmati.  

    -   **Tutti firmati**: il client di Configuration Manager esegue gli script solo se sono firmati da un autore attendibile. Questa restrizione si applica in modo indipendente dalla configurazione di Windows PowerShell corrente sul computer client.  

     Questa opzione richiede almeno Windows PowerShell versione 2.0. Il valore predefinito è **Tutti firmati**.  

    > [!TIP]  
    >  Se non è possibile eseguire gli script non firmati a causa di questa impostazione client, Configuration Manager segnala questo errore nei modi seguenti:  
    >   
    > -   L'area di lavoro **Monitoraggio** nella console visualizza l'ID errore stato distribuzione **0x87D00327** e la descrizione **Script non firmato**  
    > -   I report visualizzano il tipo di errore **Errore di individuazione** e quindi il codice errore **0x87D00327** e la descrizione **Script non firmato** oppure il codice errore **0x87D00320** e la descrizione **L'host script non è stato ancora installato**. Un report di esempio è **Dettagli degli errori degli elementi di configurazione in una linea di base configurazione per un asset**.  
    > -   Il file **DcmWmiProvider.log** visualizza il messaggio **Script non firmato (errore: 87D00327; origine: CCM)**.  

-   **Mostra notifiche per nuove distribuzioni**  </br>
     Scegliere **Sì** per visualizzare una notifica per le distribuzioni disponibili per meno di una settimana.  Questo messaggio viene visualizzato a ogni avvio dell'agente client.

-   **Disabilitare sequenza casuale scadenza**  </br>
     Dopo la scadenza della distribuzione, questa impostazione determina se il client usa un ritardo di attivazione di un massimo di due ore per installare gli aggiornamenti software obbligatori. Per impostazione predefinita, il ritardo di attivazione è disabilitato.  

     Per gli scenari relativi all'infrastruttura VDI, questo ritardo consente di distribuire l'elaborazione della CPU e il trasferimento dei dati per un computer host con più macchine virtuali. Anche se non si usa l'infrastruttura VDI, uno scenario in cui gli stessi aggiornamenti vengono installati contemporaneamente in molti client può determinare un incremento dell'uso della CPU nel server del sito con impatto negativo. Questo comportamento può anche rallentare i punti di distribuzione e ridurre in modo significativo la larghezza di banda di rete disponibile.  

     Se i client devono installare gli aggiornamenti software obbligatori alla scadenza della distribuzione senza alcun ritardo, configurare questa impostazione su **Sì**. 

-   **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** </br>
     Se si vuole concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti software obbligatori, configurare questa impostazione su **Sì**. Questo periodo di tolleranza tiene conto dei computer rimasti spenti per molto tempo, i cui utenti devono installare molte distribuzioni di applicazioni o aggiornamenti, come nel caso, ad esempio, di un utente che, tornato da una vacanza, deve attendere parecchio tempo mentre il client installa le distribuzioni di applicazioni scadute. 

     Impostare un periodo di tolleranza compreso tra 1 e 120 ore. Usare questa impostazione in combinazione con la proprietà di distribuzione **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente**. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](/sccm/apps/deploy-use/deploy-applications).



##  <a name="computer-restart"></a>Riavvio del computer  
 Le impostazioni seguenti devono avere una durata più breve della finestra di manutenzione più breve applicata al computer.  

 Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Visualizzare una notifica temporanea in cui viene indicato l'intervallo di disconnessione dell'utente o di riavvio del computer (minuti)**
-   **Visualizzare una finestra di dialogo che l'utente non può chiudere in cui viene indicato l'intervallo per il conto alla rovescia prima della disconnessione dell'utente o del riavvio del computer (minuti)**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Oltre alle informazioni seguenti, è possibile trovare altri dettagli sull'uso delle impostazioni client di Endpoint Protection in [Scenario di esempio: uso di System Center Endpoint Protection per proteggere i computer dal malware in System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Gestire il client Endpoint Protection nei computer client**  </br>
     Scegliere **Sì** se si vogliono gestire i client di Endpoint Protection e di Windows Defender esistenti nei computer della gerarchia.  

     Scegliere questa opzione se il client di Endpoint Protection è già installato e si vuole gestirlo con Configuration Manager.  Questa installazione separata include un processo con script che usa un'applicazione di Configuration Manager o un pacchetto e un programma.

-   **Installare il client Endpoint Protection nei computer client**   </br>
     Scegliere **Sì** per installare e abilitare il client di Endpoint Protection nei computer client in cui non è già in esecuzione.  

    > [!NOTE]  
    >  Se il client di Endpoint Protection è già installato e si sceglie **No**, il client non viene disinstallato. Per disinstallare il client di Endpoint Protection, configurare l'impostazione del client **Gestire il client Endpoint Protection nei computer client** su **No**. In seguito distribuire un pacchetto e programma per disinstallare il client di Endpoint Protection.  

-   **Rimuovere automaticamente il software antimalware installato in precedenza prima di installare Endpoint Protection** </br>
    Configurare questa impostazione su **Sì** perché il client di Endpoint Protection tenti di disinstallare altre applicazioni antimalware. Più client antimalware nello stesso dispositivo possono entrare in conflitto e influire negativamente sulle prestazioni del sistema.

-   **Consentire l'installazione del client di Endpoint Protection e i riavvii al di fuori delle finestre di manutenzione. Le finestre di manutenzione devono avere una durata di almeno 30 minuti per l'installazione del client.** </br>
    Configurare questa impostazione su **Sì** per sostituire i comportamenti di installazione tipici con finestre di manutenzione. Questa impostazione soddisfa i requisiti aziendali relativi alla priorità della manutenzione del sistema per motivi di sicurezza. 

-   **Per i dispositivi Windows Embedded con filtri di scrittura, eseguire il commit dell'installazione del client di Endpoint Protection (richiede il riavvio)**  </br>
     Selezionare **Sì** per disattivare il filtro di scrittura nel dispositivo con Windows Embedded e riavviarlo. Questa azione conferma l'installazione nel dispositivo.  

     Se si configura questa impostazione su **No**, il client viene installato in una sovrimpressione temporanea che viene cancellata al riavvio del dispositivo. In questo scenario, il client di Endpoint Protection viene installato completamente solo quando un'altra installazione conferma le modifiche al dispositivo. Questa configurazione corrisponde all'impostazione predefinita.  

-   **Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection**  </br>
     Scegliere **Sì** per evitare un riavvio del computer, se necessario, dopo l'installazione del client di Endpoint Protection.  

    > [!IMPORTANT]  
    >  Se il client di Endpoint Protection richiede il riavvio del computer e questa impostazione corrisponde a **No**, il computer viene riavviato indipendentemente da qualsiasi finestra di manutenzione configurata.  

-   **Periodo di tempo consentito agli utenti per rimandare un riavvio necessario per completare l'installazione di Endpoint Protection (ore)**  </br>
     Se dopo l'installazione del client di Endpoint Protection è necessario il riavvio, questa impostazione specifica di quante ore gli utenti possono posticipare il riavvio. Questa impostazione richiede che l'impostazione **Evitare il riavvio necessario del computer dopo l'installazione del client Endpoint Protection** corrisponda a **No**.  

-   **Disabilitare le origini alternative, ad esempio Microsoft Windows Update, Microsoft Windows Server Update Services o condivisioni UNC, per l'aggiornamento iniziale delle definizioni nei computer client**  </br>
     Scegliere **Sì** se si vuole che Configuration Manager installi solo l'aggiornamento della definizione iniziale nei computer client. Questa impostazione può essere utile per evitare connessioni di rete non necessarie e ridurre la larghezza di banda durante l'installazione iniziale dell'aggiornamento della definizione.  



##  <a name="enrollment"></a>Registrazione

-   **Intervallo di polling per client precedenti del dispositivo mobile** </br>
    Fare clic su **Imposta intervallo** per specificare per quanto tempo, in minuti o ore, i dispositivi mobili legacy possono eseguire il polling dei criteri. Questi dispositivi includono piattaforme quali Windows CE, Mac OS X e Unix o Linux.

-   **Intervallo di polling per i dispositivi moderni (minuti)** </br>
    Immettere per quanti minuti i dispositivi moderni possono eseguire il polling dei criteri. Questa impostazione è destinata ai dispositivi Windows 10 gestiti tramite la gestione dei dispositivi mobili locale.

-   **Consenti agli utenti di registrare i dispositivi mobili e i computer Mac** </br>
    Per consentire la registrazione dei dispositivi legacy basata sugli utenti, configurare questa impostazione su **Sì** e quindi configurare le impostazioni seguenti:

    -   **Profilo di registrazione** </br>
        Fare clic su **Imposta profilo** per creare o selezionare un profilo di registrazione. Per altre informazioni, vedere [Configurare le impostazioni client per la registrazione](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Consenti agli utenti di registrare i dispositivi moderni** </br>
    Per consentire la registrazione dei dispositivi moderni basata sugli utenti, configurare questa impostazione su **Sì** e quindi configurare le impostazioni seguenti:

    -   **Profilo di registrazione per dispositivi moderni** </br>
        Fare clic su **Imposta profilo** per creare o selezionare un profilo di registrazione. Per altre informazioni, vedere [Creare un profilo di registrazione che consenta agli utenti di registrare i dispositivi moderni](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventario hardware  

-   **Abilitare inventario hardware nei client** </br>
    Questa impostazione corrisponde a **Sì** per impostazione predefinita. Per altre informazioni, vedere [Introduzione all'inventario hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Pianificazione inventario hardware** </br>
    Fare clic su **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di inventario hardware. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.

-   **Ritardo casuale massimo (minuti)** </br>
    Specificare per quanti minuti al massimo il client di Configuration Manager può impostare in modo casuale il ciclo di inventario hardware dalla pianificazione definita. Questa impostazione casuale in tutti i client consente di bilanciare il carico dell'elaborazione dell'inventario nel server del sito. È possibile specificare un valore compreso tra 0 e 480 minuti. Per impostazione predefinita, il valore è impostato su 240 minuti (quattro ore).

-   **Dimensioni massime file MIF personalizzate (KB)**  </br>
     Specificare la dimensione massima consentita, in KB, per ogni file MIF (Management Information Format) personalizzato raccolto dal client durante il ciclo di inventario hardware. L'agente inventario hardware di Configuration Manager non elabora alcun file MIF che superi tale dimensione. È possibile specificare una dimensione compresa tra 1 KB e 5.120 KB. Per impostazione predefinita, il valore è impostato su 250 KB. Questa impostazione non influenza la dimensione del file di dati di inventario hardware normale.  

    > [!NOTE]  
    >  Questa impostazione è disponibile solo nelle impostazioni del client predefinite.  

-   **Classi di inventario hardware**  </br>
     Fare clic su **Imposta classi** per estendere le informazioni hardware raccolte dai client senza modificare manualmente il file sms_def.mof. Per altre informazioni, vedere [Come configurare l'inventario hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Raccogli file MIF**  </br>
     Usare questa impostazione per specificare se raccogliere i file MIF dai client di Configuration Manager durante l'inventario hardware.  

     Perché un file MIF venga raccolto dall'inventario hardware, deve trovarsi nel percorso corretto nel computer client. Per impostazione predefinita, i file si trovano nei percorsi seguenti:  

    -   I **file IDMIF** devono trovarsi nella cartella Windows\System32\CCM\Inventory\Idmif 

    -   I **file NOIDMIF** devono trovarsi nella cartella Windows\System32\CCM\Inventory\Noidmif

    > [!NOTE]  
    >  Questa impostazione è disponibile solo nelle impostazioni del client predefinite.

   

##  <a name="metered-internet-connections"></a>Connessioni Internet a consumo  
 È possibile gestire la modalità con cui i computer Windows 8 e versioni successive usano connessioni Internet a consumo per comunicare con Configuration Manager. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

> [!NOTE]  
>  L'impostazione client configurata non viene applicata negli scenari seguenti:  
>   
> -   Il computer usa una connessione dati in roaming: il client di Configuration Manager non esegue alcuna operazione che richiede il trasferimento dei dati nei siti di Configuration Manager.  
> -   Le proprietà di connessione di rete di Windows sono configurate come connessioni non a consumo: il client di Configuration Manager si comporta come se la connessione non fosse a consumo e pertanto trasferisce i dati al sito.  

-   **Comunicazione dei client nelle connessioni Internet a consumo**  </br>
     Per questa impostazione scegliere una delle opzioni seguenti:  

    -   **Consenti**: tutte le comunicazioni client sono consentite tramite la connessione Internet a consumo a meno che il dispositivo client non stia usando una connessione dati in roaming.  

    -   **Limite**: sono consentite solo le comunicazioni client seguenti tramite la connessione Internet a consumo:  

        -   Recupero dei criteri client  

        -   Messaggi di stato del client da inviare al sito  

        -   Richieste di installazione di software mediante il Catalogo applicazioni  

        -   Distribuzioni richieste (quando viene raggiunta la scadenza per l'installazione)  

        > [!IMPORTANT]  
        >  Il client consente sempre le installazioni software da Software Center o dal Catalogo applicazioni, indipendentemente dalle impostazioni della connessione Internet a consumo.  

         Se viene raggiunto il limite per il trasferimento dei dati per la connessione Internet a consumo, il client non prova più a comunicare con i siti di Configuration Manager.  

    -   **Blocca**: il client di Configuration Manager non prova a comunicare con i siti di Configuration Manager in presenza di una connessione Internet a consumo. Questa opzione corrisponde all'impostazione predefinita.  



##  <a name="power-management"></a>Risparmio energia  

-   **Consentire il risparmio energia dei dispositivi** </br>
    Configurare questa impostazione su **Sì** per abilitare il risparmio energia nei client. Per altre informazioni, vedere [Introduzione alle raccolte](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Consentire agli utenti di escludere il dispositivo usato dal risparmio energia**  </br>
     Scegliere **Sì** per consentire agli utenti di Software Center di escludere il computer dalle impostazioni di risparmio energia configurate.  

-   **Abilitare il proxy di riattivazione** </br> 
     Specificare **Sì** per integrare l'impostazione Riattivazione LAN del sito quando è configurata per i pacchetti unicast.  

     Per altre informazioni sul proxy di riattivazione, vedere [Pianificare la riattivazione dei client in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Non abilitare il proxy di riattivazione in una rete di produzione senza prima comprenderne il funzionamento e valutarlo in un ambiente di test.  

    Configurare quindi le impostazioni aggiuntive seguenti in base alle esigenze:

    -   **Numero di porta del proxy di riattivazione (UDP)**  </br>
         Numero di porta usato dai client per inviare pacchetti di riattivazione ai computer in sospensione. Mantenere la porta predefinita 25536 o modificare il numero con un valore a propria scelta.  

    -   **Numero di porta di riattivazione LAN (UDP)** </br> 
         Mantenere il valore predefinito 9 a meno che non sia stato modificato il numero di porta di riattivazione LAN (UDP) nelle **Proprietà** del sito nella scheda **Porte**.  

        > [!IMPORTANT]  
        >  Questo numero deve corrispondere al numero nelle **Proprietà**del sito. Se si modifica questo numero in una posizione, non viene aggiornato automaticamente nell'altra.  

    -   **Eccezione di Windows Defender Firewall per il proxy di riattivazione** </br>
         Il client di Configuration Manager configura automaticamente il numero di porta del proxy di riattivazione nei dispositivi che eseguono Windows Defender Firewall. Fare clic su **Configura** per specificare i profili firewall desiderati.

        Se i client eseguono un firewall diverso, è necessario configurarlo manualmente per consentire **Numero di porta del proxy di riattivazione (UDP)**.  
        
    -   **Prefissi IPv6 se richiesti per DirectAccess o altri dispositivi di rete. Utilizzare una virgola per specificare più voci** </br>
        Immettere i prefissi IPv6 necessari per il funzionamento del proxy di riattivazione nella rete in uso.



##  <a name="remote-tools"></a>Strumenti remoti  

-   **Abilitare controllo remoto nei client** e **Profili delle eccezioni firewall**  </br>
     Fare clic su **Configura** per abilitare la funzionalità di controllo remoto di Configuration Manager. Facoltativamente, configurare le impostazioni del firewall per consentire al controllo remoto di funzionare nei computer client.  

     Per impostazione predefinita, il controllo remoto è disattivato.  

    > [!IMPORTANT]  
    >  Se le impostazioni del firewall non sono configurate, il controllo remoto potrebbe non funzionare correttamente.  

-   **Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center**  </br>
     Scegliere se gli utenti possono modificare le opzioni di controllo remoto da Software Center.  

-   **Consentire il controllo remoto di un computer senza intervento dell'utente**  </br>
     Scegliere se un amministratore può usare il controllo remoto per accedere a un computer client disconnesso o bloccato. Solo un computer connesso e sbloccato può essere controllato da remoto quando questa impostazione è disattivata.  

-   **Richiedere all'utente l'autorizzazione di controllo remoto**  </br>
     Scegliere se il computer client deve visualizzare un messaggio per richiedere l'autorizzazione dell'utente prima di consentire una sessione di controllo remoto.  

-   **Richiedere all'utente l'autorizzazione per il trasferimento di contenuto dagli Appunti condivisi** </br>
    Offre agli utenti la possibilità di accettare o rifiutare il trasferimento di file prima di trasferire il contenuto dagli Appunti condivisi in una sessione di controllo remoto. Gli utenti devono solo concedere l'autorizzazione una sola volta per sessione e il visualizzatore non ha la possibilità di concedere l'autorizzazione per procedere con il trasferimento dei file.

-   **Concedere l'autorizzazione di controllo remoto al gruppo Administrators locale**  </br>
     Scegliere se gli amministratori locali del server che avvia la connessione di controllo remoto possono stabilire sessioni di controllo remoto nei computer client.  

-   **Livello di accesso consentito**  </br>
     Specificare il livello di accesso di controllo remoto da consentire. Scegliere tra le impostazioni seguenti:  
    - **Nessun accesso**
    - **Solo visualizzazione**
    - **Controllo completo**  

-   **Visualizzatori autorizzati di controllo remoto e assistenza remota**  </br>
     Fare clic su **Imposta** per specificare i nomi degli utenti Windows che possono stabilire sessioni di controllo remoto per i computer client.  

-   **Mostra icona di notifica sessione nella barra delle applicazioni**  </br>
     Configurare questa impostazione su **Sì** per indicare una sessione di controllo remoto attiva tramite la visualizzazione di un'icona sulla barra delle applicazioni di Windows del client.  

-   **Mostrare barra delle connessioni sessione**  </br>
     Configurare questa impostazione su **Sì** per indicare una sessione di controllo remoto attiva tramite la visualizzazione di una barra di connessione della sessione ad alta visibilità nei client.  

-   **Riprodurre un suono nel client**  </br>
     Configurare questa impostazione per indicare tramite un suono quando una sessione di controllo remoto è attiva in un computer client. Selezionare una delle opzioni seguenti:
    - **Nessun suono**
    - **Inizio e fine della sessione** (impostazione predefinita)
    - **Ripetutamente nel corso della sessione**  

-   **Gestire le impostazioni di assistenza remota non richiesta**  </br>
     Configurare questa impostazione su **Sì** per consentire a Configuration Manager di gestire le sessioni di assistenza remota non richiesta.  

     Nelle sessioni di assistenza remota non richiesta la sessione viene avviata senza che l'utente del computer client abbia richiesto assistenza.  

-   **Gestire le impostazioni di assistenza remota su richiesta**  </br>
     Configurare questa impostazione su **Sì** per consentire a Configuration Manager di gestire le sessioni di assistenza remota su richiesta.  

     Nelle sessioni di assistenza remota su richiesta l'utente nel computer client ha inviato una richiesta di assistenza remota all'amministratore.  

-   **Livello di accesso per assistenza remota**  </br>
     Scegliere il livello di accesso da assegnare alle sessioni di assistenza remota avviate nella console di Configuration Manager.  Selezionare una delle opzioni seguenti:
    - **Nessuno** (impostazione predefinita)
    - **Visualizzazione remota**
    - **Controllo completo**

    > [!NOTE]  
    >  L'utente nel computer client deve sempre concedere l'autorizzazione per avviare una sessione di assistenza remota.  

-   **Gestire le impostazioni di desktop remoto**  </br>
     Configurare questa impostazione su **Sì** per consentire a Configuration Manager di gestire le sessioni di Desktop remoto per i computer.  

-   **Consentire ai visualizzatori autorizzati di connettersi mediante connessione desktop remoto**  </br>
     Configurare questa impostazione su **Sì** per aggiungere gli utenti specificati nell'elenco di visualizzatori autorizzati al gruppo utenti locale di Desktop remoto nei client.  

-   **Richiedere Autenticazione a livello di rete nei computer che eseguono il sistema operativo Windows Vista e versioni successive**  </br>
     Configurare questa impostazione su **Sì** per stabilire connessioni Desktop remoto a computer client tramite Autenticazione a livello di rete (NLA, Network-Level Authentication). NLA inizialmente richiede meno risorse del computer remoto perché completa l'autenticazione utente prima di stabilire una connessione Desktop remoto. NLA rappresenta una configurazione più sicura. NLA consente di proteggere il computer da utenti malintenzionati o da software dannoso e riduce il rischio di attacchi Denial of Service.  



## <a name="software-center"></a>Software Center

-   **Selezionare le nuove impostazioni per specificare le informazioni aziendali** </br>
    Configurare questa impostazione su **Sì**e quindi specificare le impostazioni seguenti per personalizzare Software Center per l'organizzazione:

    - **Nome società** </br>
        Immettere il nome dell'organizzazione visualizzato dagli utenti in Software Center.
    - **Combinazione colori per il Software Center** </br>
        Fare clic su **Seleziona il colore** per definire il colore primario usato da Software Center.
    - **Seleziona un logo per il Software Center** </br>
        Fare clic su **Sfoglia** per selezionare un'immagine da visualizzare in Software Center. Il logo deve essere un file JPEG, PNG o BMP di 400 x 100 pixel, con una dimensione massima di 750 KB. Il nome del file del logo non deve contenere spazi. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

-   Visibilità delle schede di Software Center </br>
    Configurare le impostazioni aggiuntive di questo gruppo su **Sì** per rendere visibili in Software Center le schede seguenti:
    - **Applicazioni**
    - **Aggiornamenti**
    - **Sistemi operativi**
    - **Stato installazione**
    - **Conformità del dispositivo**
    - **Opzioni**

    Se ad esempio l'organizzazione non usa criteri di conformità e si vuole nascondere la scheda Conformità del dispositivo in Software Center, configurare l'impostazione **Abilita la scheda Conformità del dispositivo** su **No**.



## <a name="software-deployment"></a>Distribuzione software  

-   **Pianificare nuova valutazione per le distribuzioni**  </br>
     Configurare una pianificazione che indichi quando Configuration Manager deve eseguire una nuova valutazione delle regole dei requisiti per tutte le distribuzioni. Il valore predefinito è ogni sette giorni.  

    > [!IMPORTANT]  
    >  È consigliabile non modificare questo valore in un valore inferiore a quello predefinito Una pianificazione di rivalutazione più aggressiva influisce negativamente sulle prestazioni della rete e dei computer client.  

     Avviare questa azione da un client scegliendo **Ciclo di valutazione distribuzione applicazione** dalla scheda**Azioni** del pannello di controllo di **Configuration Manager**.  



##  <a name="software-inventory"></a>Inventario software  

-   **Abilitare inventario software nei client** </br>
    Questa impostazione corrisponde a **Sì** per impostazione predefinita. Per altre informazioni, vedere [Introduzione all'inventario software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Pianificare inventario software e raccolta file** </br>
    Fare clic su **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di inventario software e quello di raccolta file. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.

-   **Dettaglio report inventario**  </br>
     Specificare uno dei livelli di informazioni seguenti dei file per l'inventario:
    - **Solo file**
    - **Solo prodotto**
    - **Dettagli completi** (impostazione predefinita)

-   **Tipi di file da includere nell'inventario**  </br>
     Per specificare i tipi di file per l'inventario, fare clic su **Imposta tipi** e quindi configurare le opzioni seguenti:  

    > [!NOTE]  
    >  Se a un computer vengono applicate più impostazioni client personalizzate, l'inventario restituito da ogni impostazione viene unito.  

    -   Fare clic sull'icona **Nuovo** per aggiungere un nuovo tipo di file all'inventario. Specificare quindi le informazioni seguenti nella finestra di dialogo **Proprietà file in inventario**:  

        -   **Nome**: specificare un nome per il file che si vuole includere nell'inventario. Usare il carattere jolly asterisco (**&#42;**) per rappresentare qualsiasi stringa di testo e un punto interrogativo (**?**) per rappresentare qualsiasi carattere singolo. Ad esempio, se si vuole includere nell'inventario tutti i file con estensione doc, specificare il nome del file **\*.doc**.  

        -   **Percorso** : fare clic su **Imposta** per aprire la finestra di dialogo **Proprietà percorso**. Configurare l'inventario software per cercare in tutti i dischi rigidi del client il file specificato, un percorso specifico (ad esempio **C:\Cartella**) o una variabile specifica (ad esempio, *%windir%*). È anche possibile cercare tutte le sottocartelle nel percorso specificato.  

        -   **Escludi file crittografati e compressi**: quando si seleziona questa opzione, tutti i file compressi o crittografati non vengono inclusi nell'inventario.  

        -   **Escludi file nella cartella Windows**: quando si seleziona questa opzione, tutti i file nella cartella Windows e nelle relative sottocartelle non vengono inclusi nell'inventario.  

    -   Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà file in inventario** .  

    -   Aggiungere tutti i file che si vogliono includere nell'inventario e quindi fare clic su **OK** per chiudere la finestra di dialogo **Configura impostazione client**.  

-   **Raccogli file**  </br>
     Se si vogliono raccogliere i file dai computer client, fare clic su **Imposta file** e quindi configurare le impostazioni seguenti:  

    > [!NOTE]  
    >  Se a un computer vengono applicate più impostazioni client personalizzate, l'inventario restituito da ogni impostazione viene unito.  

    -   Nella finestra di dialogo **Configura impostazione client** fare clic sull'icona **Nuovo** per aggiungere un file da raccogliere.  

    -   Nella finestra di dialogo **Proprietà file recuperato** immettere le informazioni seguenti:  

        -   **Nome**: specificare un nome per il file che si vuole raccogliere. Usare il carattere jolly asterisco (**&#42;**) per rappresentare qualsiasi stringa di testo e un punto interrogativo (**?**) per rappresentare qualsiasi carattere singolo.  

        -   **Percorso** : fare clic su **Imposta** per aprire la finestra di dialogo **Proprietà percorso**. Configurare l'inventario software per cercare in tutti i dischi rigidi del client il file che si vuole raccogliere, un percorso specifico (ad esempio **C:\Cartella**) o una variabile specifica (ad esempio, *%windir%*). È anche possibile cercare tutte le sottocartelle nel percorso specificato.  

        -   **Escludi file crittografati e compressi**: quando si seleziona questa opzione, tutti i file compressi o crittografati non vengono raccolti.  

        -   **Interrompere la raccolta file quando le dimensioni totali dei file superano (KB)**: specificare le dimensioni del file (in KB) oltre le quali il client interrompe la raccolta dei file specificati.  

          > [!NOTE]  
          >  Il server del sito raccoglie le cinque versioni più recenti dei file raccolti e le archivia nella directory *&lt;directory di installazione di ConfigMgr\>*\Inboxes\Sinv.box\Filecol. Se dopo l'ultimo ciclo di inventario software un file non è stato modificato, non viene raccolto nuovamente.  
          >   
          >  L'inventario software non raccoglie file di dimensioni superiori a 20 MB.  
          >   
          >  Il valore **Dimensioni massime per tutti i file raccolti (KB)** nella finestra di dialogo **Configura impostazione client** visualizza le dimensioni massime per tutti i file raccolti. Quando viene raggiunta questa dimensione, la raccolta file viene interrotta. Tutti i file già raccolti vengono mantenuti e inviati al server del sito.  

          > [!IMPORTANT]
          >  Se si configura l'inventario software in modo da raccogliere molti file di grandi dimensioni, questa configurazione può influire negativamente sulle prestazioni del server di rete e del sito.  

        Per informazioni su come visualizzare i file raccolti, vedere [Come usare Esplora inventario risorse per visualizzare l'inventario software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà file recuperato** .  

    -   Aggiungere tutti i file che si vogliono raccogliere e quindi fare clic su **OK** per chiudere la finestra di dialogo **Configura impostazione client**.  

-   **Impostare i nomi**  </br>
     L'agente inventario software recupera i nomi del produttore e del prodotto dalle informazioni di intestazione dei file. Questi nomi non sono sempre standardizzati all'interno di queste informazioni. Quando si visualizza l'inventario software in Esplora inventario risorse, possono essere visualizzate versioni diverse dello stesso nome di produttore o di prodotto. Per standardizzare i nomi visualizzati, fare clic su **Imposta nomi** e quindi configurare le impostazioni seguenti:  

    -   **Tipo nome**: l'inventario software raccoglie informazioni su produttori e prodotti. Scegliere se configurare i nomi visualizzati per un **Produttore** o un **Prodotto**.  

    -   **Nome visualizzato:** specificare il nome visualizzato da usare al posto dei nomi inclusi nell'elenco **Nomi di inventario**. Fare clic sull'icona **Nuovo** per specificare un nuovo nome visualizzato.  

    -   **Nomi di inventario**: fare clic sull'icona **Nuovo** per aggiungere un nome di inventario. Questo nome viene sostituito nell'inventario software dal nome scelto nell'elenco **Nome visualizzato**. È possibile aggiungere più nomi da sostituire.  



##  <a name="software-metering"></a>Controllo software

-   **Abilitare controllo software nei client** </br>
    Questa impostazione corrisponde a **Sì** per impostazione predefinita. Per altre informazioni, vedere [Controllo del software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Pianifica raccolta dati** </br>
    Fare clic su **Pianificazione** per regolare la frequenza con cui i client devono eseguire il ciclo di controllo del software. Per impostazione predefinita, il ciclo viene eseguito ogni sette giorni.



##  <a name="software-updates"></a>Aggiornamenti software  

-   **Abilitare aggiornamento software nei client**  </br>
     Usare questa impostazione per abilitare gli aggiornamenti software nei client di Configuration Manager. Quando si disabilita questa opzione, Configuration Manager rimuove i criteri di distribuzione esistenti dal client. Quando si riattiva questa impostazione, il client scaricherà il criterio di distribuzione corrente.  

    > [!IMPORTANT]  
    >  Quando si deseleziona questa impostazione, i criteri di conformità basati sugli aggiornamenti software non funzioneranno più.  

-   **Pianificazione analisi aggiornamento software**  </br>
     Fare clic su **Pianificazione** per specificare la frequenza con cui il client avvia un'analisi di valutazione conformità. Questa analisi determina lo stato degli aggiornamenti software nel client (ad esempio, aggiornamento obbligatorio o installato). Per altre informazioni sulla valutazione della conformità, vedere [Valutazione della conformità negli aggiornamenti software](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     Per impostazione predefinita, questa analisi usa una pianificazione semplice da avviare ogni sette giorni. È possibile creare una pianificazione personalizzata per specificare una data e un'ora di avvio specifiche, per usare l'ora UTC o l'ora locale e per configurare l'intervallo ricorrente per un giorno specifico della settimana.  

    > [!NOTE]  
    >  Se si specifica un intervallo inferiore a un giorno, Configuration Manager usa automaticamente il valore pari a un giorno come impostazione predefinita.  

    > [!WARNING]  
    >  L'ora di avvio effettiva nei computer client corrisponde all'ora di avvio con l'aggiunta di una quantità di tempo casuale, fino a un massimo di due ore. Questa impostazione casuale impedisce ai computer client di avviare l'analisi e contemporaneamente di connettersi al punto di aggiornamento software attivo.  

-   **Pianificare nuova valutazione di distribuzione**  </br>
     Fare clic su **Pianificazione** per configurare la frequenza di esecuzione della valutazione degli aggiornamenti software da parte dell'agente client aggiornamenti software per la verifica dello stato di installazione nei computer client di Configuration Manager. Se gli aggiornamenti software installati in precedenza non sono più presenti nei client ma sono ancora necessari, il client li reinstalla.

     Regolare la pianificazione in base ai criteri aziendali di conformità degli aggiornamenti software e in base al fatto che gli utenti possano disinstallare o meno gli aggiornamenti software. Ogni ciclo di rivalutazione della distribuzione comporta attività del processore del computer client e della rete. Per impostazione predefinita, questa impostazione usa una pianificazione semplice per avviare la rivalutazione della distribuzione ogni sette giorni.  

    > [!NOTE]  
    >  Se si specifica un intervallo inferiore a un giorno, Configuration Manager usa automaticamente il valore pari a un giorno come impostazione predefinita.  

-   **Quando viene raggiunta la scadenza di una distribuzione di aggiornamenti software, installare tutte le altre distribuzione di aggiornamenti software con scadenza entro un periodo di tempo specificato**  </br>
     Configurare questa impostazione su **Sì** per installare tutti gli aggiornamenti software da distribuzioni obbligatorie con scadenze che rientrano in un periodo di tempo specifico. Quando la distribuzione di aggiornamenti software obbligatori raggiunge la scadenza, il client avvia l'installazione degli aggiornamenti software nella distribuzione. Questa impostazione determina se installare aggiornamenti software da altre distribuzioni obbligatorie con una scadenza compresa nel periodo specificato.  

     Usare questa impostazione per accelerare l'installazione di aggiornamenti software obbligatori. Questa impostazione potenzialmente è anche in grado di aumentare la sicurezza dei client, ridurre le notifiche per l'utente finale e diminuire il numero di riavvii dei client stessi. Per impostazione predefinita, questa impostazione è impostata su **No** e quindi non è abilitata.  

-   **Periodo di tempo entro cui verranno installate anche tutte le distribuzioni in sospeso con scadenza in questo periodo**  </br>
     Usare questa impostazione per specificare il periodo di tempo per l'impostazione precedente. È possibile immettere un valore compreso tra 1 e 23 e tra 1 e 365 giorni. Per impostazione predefinita, questa impostazione è configurata su sette giorni.  

-   **Abilita l'installazione di file per l'installazione rapida nei client** </br>
    Configurare questa impostazione su **Sì** per consentire ai client di usare file di installazione rapida. Per altre informazioni, vedere [Gestire i file di installazione rapida per gli aggiornamenti di Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Porta usata per scaricare contenuto per i file per l'installazione rapida** </br>
        Questa impostazione consente di configurare la porta locale per il listener HTTP per il download del contenuto dell'installazione rapida. Per impostazione predefinita, corrisponde a 8005. Non è necessario aprire questa porta nel firewall client.

-   **Abilitare la gestione dell'agente del client Office 365** </br>
    Usare questa impostazione per abilitare la gestione dell'agente client Office 365. Quando questa opzione è impostata su **Sì**, consente la configurazione delle impostazioni di installazione di Office 365, il download di file dalle reti per la distribuzione di contenuti (CDN, Content Delivery Network) di Office e la distribuzione di file come applicazione in Configuration Manager. Per altre informazioni, vedere [Gestire gli aggiornamenti di Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Messaggistica di stato

-   **Ciclo di segnalazione messaggi di stato (minuti)**  </br>
     Specifica la frequenza con cui i client segnalano i messaggi di stato. Per impostazione predefinita, questa impostazione corrisponde a 15 minuti.



##  <a name="user-and-device-affinity"></a>Affinità utente-dispositivo  

-   **Soglia di utilizzo di affinità utente dispositivo (minuti)**  </br>
     Specificare il numero di minuti prima della creazione di un mapping di affinità del dispositivo utente da parte di Configuration Manager.  Per impostazione predefinita, questo valore è impostato su 2880 minuti (due giorni).

-   **Soglia di utilizzo di affinità utente dispositivo (giorni)**  </br>
     Specificare il numero di giorni in cui il client misura la soglia di affinità del dispositivo in base all'utilizzo.  Per impostazione predefinita, questo valore è impostato su 30 giorni.

    > [!NOTE]  
    >  È ad esempio possibile impostare **Soglia di utilizzo di affinità utente dispositivo (minuti)** su **60** minuti e **Soglia di utilizzo di affinità utente dispositivo (giorni)** su **5** giorni. L'utente deve quindi usare il dispositivo per 60 minuti in un periodo di cinque giorni per creare affinità automatica con il dispositivo.  

-   **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo**  </br>
     Scegliere **Sì** per creare automaticamente affinità utente-dispositivo in base alle informazioni sull'utilizzo raccolte da Configuration Manager.  

-   **Consentire all'utente di definire i dispositivi primari** </br>
    Se questa impostazione corrisponde a **Sì**, gli utenti possono identificare i propri dispositivi primari in Software Center.



## <a name="windows-analytics"></a>Windows Analytics

Per altre informazioni su queste impostazioni, vedere [Configurare i client per segnalare i dati a Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
