---
title: Informazioni dettagliate sulla gestione
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità Informazioni dettagliate sulla gestione disponibile nella console di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5f2f7e8c274930d5517ffab1b8d8bb7477127865
ms.sourcegitcommit: bfece120a6f9a79dbcc8bacc83905f16f3f1b144
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76917163"
---
# <a name="management-insights-in-configuration-manager"></a>Informazioni dettagliate sulla gestione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La funzionalità Informazioni dettagliate sulla gestione in Configuration Manager offre indicazioni utili sullo stato corrente dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. <!--1353967-->

## <a name="review-management-insights"></a>Esaminare le informazioni dettagliate sulla gestione

Per visualizzare le regole, l'account deve disporre dell'autorizzazione di **lettura** per l'oggetto **sito**.

1. Aprire la console di Configuration Manager.  

2. Nell'area di lavoro **Amministrazione** espandere **Informazioni dettagliate sulla gestione** e selezionare **Tutte le informazioni dettagliate**.  

    > [!Note]  
    > A partire dalla versione 1810, quando si seleziona il nodo **Informazioni dettagliate sulla gestione** viene visualizzato il [Dashboard di informazioni dettagliate sulla gestione](#bkmk_insights).  

3. Aprire il nome del gruppo di informazioni dettagliate sulla gestione che si vuole esaminare. Selezionare **Mostra le informazioni dettagliate** nella barra multifunzione.  

È possibile esaminare le quattro schede seguenti:

- **Tutte le regole**: offre l'elenco completo delle regole per il gruppo di informazioni dettagliate di gestione scelto.  

- **Completa**:  elenca le regole in cui non è necessaria alcuna azione.  

- **In corso**: mostra le regole in cui alcuni, ma non tutti i prerequisiti sono soddisfatti.  

- **Azione richiesta**: sono elencate le regole che richiedono le azioni adottate. Scegliere **Altri dettagli** per recuperare elementi specifici in cui è necessaria un'azione.  

Nel riquadro **Prerequisiti** sono elencati gli elementi obbligatori per eseguire la regola.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Tutte le regole e i prerequisiti per il gruppo di servizi cloud

![Informazioni dettagliate sulla gestione- Tutte le regole e i prerequisiti per il gruppo di servizi cloud](./media/Management-insights-all-cloud-rules.png)

Selezionare una regola e quindi selezionare **Altri dettagli** per visualizzarne i dettagli.

## <a name="operations"></a>Operazioni

Le regole delle informazioni dettagliate sulla gestione rivalutano la loro applicabilità a una pianificazione settimanale. Per valutare nuovamente una regola su richiesta, fare clic con il pulsante destro del mouse sulla regola e selezionare **Valuta di nuovo**.

Il file di log per le regole di Informazioni dettagliate sulla gestione è **SMS_DataEngine.log** ed è disponibile nel server del sito.

<!--1357930-->
Alcune regole consentono di intervenire. Selezionare una regola, selezionare **Altri dettagli** e quindi, se disponibile, selezionare **Intervieni**.

A seconda della regola, questa azione presenta uno dei comportamenti seguenti:  

- Passare direttamente nella console al nodo in cui è possibile eseguire ulteriori azioni. Ad esempio, se le informazioni dettagliate sulla gestione consigliano di modificare un'impostazione client, l'opzione per eseguire un'azione consente di passare al nodo Impostazioni client. Eseguire quindi ulteriori azioni modificando l'impostazione predefinita o un oggetto impostazioni client personalizzato.  

- Passare a una visualizzazione filtrata in base a una query. Ad esempio, eseguire l'azione per la regola delle raccolte vuote mostra semplicemente queste raccolte nell'elenco delle raccolte. Eseguire quindi eseguire ulteriori azioni, ad esempio eliminare una raccolta o modificarne le regole di appartenenza.  

## <a name="bkmk_insights"></a> Dashboard delle informazioni dettagliate sulla gestione

<!--1357979-->

A partire dalla versione 1810 il nodo **Informazioni dettagliate sulla gestione** include un dashboard grafico. Questo dashboard visualizza una panoramica degli stati delle regole che rende più semplice visualizzare lo stato di avanzamento.

Usare i filtri seguenti nella parte superiore del dashboard per ottimizzare la visualizzazione:

- Mostra completate
- Facoltativo
- Consigliato
- Critico

Il dashboard include i riquadri seguenti:  

- **Indice informazioni dettagliate sulla gestione**: registra l'avanzamento generale delle regole delle informazioni dettagliate sulla gestione. L'indice è una media ponderata. Le regole critiche hanno maggior valore. Questo indice assegna il minor peso alle regole facoltative.  

- **Gruppi di informazioni dettagliate sulla gestione**: mostra la percentuale di regole di ogni gruppo che soddisfa i filtri. Selezionare un gruppo per eseguire il drill-down nelle regole specifiche del gruppo.  

- **Priorità delle informazioni dettagliate sulla gestione**: mostra la percentuale di regole in base alla priorità che soddisfa i filtri.  

- **Tutte le informazioni dettagliate sulla gestione**: tabella delle informazioni dettagliate con priorità e stato. Usare il campo **Filtro** nella parte superiore della tabella per la corrispondenza con stringhe in una qualsiasi delle colonne disponibili. Il dashboard consente di ordinare la tabella nell'ordine seguente:

  - Stato: Azione necessaria, Completato, Sconosciuto  
  - Priorità: Critico, Consigliato, Facoltativo  
  - Ultima modifica: le date meno recenti sono visualizzate all'inizio  

![Screenshot del dashboard delle informazioni dettagliate sulla gestione](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Gruppi e regole

Le regole sono organizzate nei seguenti gruppi di informazioni dettagliate sulla gestione:

- [Applicazioni](#applications)  
- [Servizi cloud](#cloud-services)  
- [raccolte](#collections)  
- [Manutenzione proattiva](#proactive-maintenance)  
- [Security](#security)  
- [Gestione semplificata](#simplified-management)  
- [Software Center](#software-center)  
- [Windows 10](#windows-10)  

### <a name="applications"></a>Applicazioni

Informazioni dettagliate per la gestione delle applicazioni.

- **Applicazioni senza distribuzioni**: elenca le applicazioni dell'ambiente senza distribuzioni attive. Questa regola aiuta a individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](/sccm/apps/deploy-use/deploy-applications).  

### <a name="cloud-services"></a>Servizi cloud

Facilita l'integrazione con molti servizi cloud per una gestione moderna dei dispositivi.

- **Valuta l'idoneità per la co-gestione**: consente di comprendere i passaggi necessari per abilitare la co-gestione. Questa regola ha dei prerequisiti. Per altre informazioni, vedere la [panoramica sulla co-gestione](/sccm/comanage/overview).  

- **Configura i servizi di Azure per l'uso con Configuration Manager**: questa regola consente di eseguire l'onboarding di Configuration Manager in Azure AD, in modo che i client possano usare Azure AD per eseguire l'autenticazione nel sito. Per altre informazioni, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Consenti dispositivi ibridi aggiunti ad Azure Active Directory**: i dispositivi aggiunti ad Azure AD consentono agli utenti di accedere con le credenziali del dominio garantendo al contempo che i dispositivi soddisfino gli standard di sicurezza e conformità dell'organizzazione. Per altre informazioni, vedere [Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Aggiorna i client alla versione più recente di Windows 10**: Windows 10, versione 1709 o versioni successive, migliora e modernizza l'esperienza di elaborazione degli utenti. Per altre informazioni, vedere [Articoli principali sull'adozione di Windows as a Service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Raccolte

Informazioni dettagliate che consentono di semplificare la gestione tramite la pulizia e la riconfigurazione delle raccolte.

- **Raccolte vuote**: un elenco delle raccolte dell'ambiente che non hanno membri. Per altre informazioni, vedere [Come gestire le raccolte](/sccm/core/clients/manage/collections/manage-collections).  

A partire dalla versione 1902, sono disponibili nuove regole con raccomandazioni per la gestione delle raccolte.<!--3555752--> Usare queste informazioni dettagliate per semplificare la gestione e migliorare le prestazioni:

- **Raccolte senza regole di query e senza membri diretti**: per semplificare l'elenco di raccolte nella gerarchia, eliminare queste raccolte.  

- **Raccolte con la stessa ora di inizio di rivalutazione**: queste raccolte hanno la stessa ora di rivalutazione di altre raccolte. Modificare l'ora di rivalutazione in modo da evitare conflitti.  

- **Raccolte con tempo di query di oltre due secondi**: rivedere le regole di query per queste raccolte. Prendere in considerazione di modificarle o eliminarle.

- Le regole seguenti includono alcune configurazioni che possono causare un carico non necessario del sito. Rivedere queste raccolte e quindi eliminarle oppure disabilitare la valutazione delle regole:  

  - **Raccolte senza regole di query e con gli aggiornamenti incrementali abilitati**  

  - **Raccolte senza regole di query e abilitate per la valutazione pianificata o incrementale**  

  - **Raccolte senza regole di query e con pianificazione della valutazione completa selezionata**  

### <a name="proactive-maintenance"></a>Manutenzione proattiva

<!--1352184-->
Le regole in questo gruppo evidenziano potenziali problemi di configurazione che possono essere evitati tramite la manutenzione degli oggetti di Configuration Manager.

- **Gruppi di limiti senza sistemi del sito assegnati**: senza sistemi del sito assegnati, i gruppi di limiti possono essere usati solo per l'assegnazione del sito. Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Gruppi di limiti senza membri**: i gruppi di limiti non sono applicabili per l'assegnazione del sito o la ricerca di contenuto se non hanno membri. Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Punti di distribuzione che non forniscono contenuti ai client**: punti di distribuzione che non hanno reso disponibile contenuto ai client negli ultimi 30 giorni. I dati sono basati sui report dai client della relativa cronologia di download. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Abilita la pulizia WSUS**: verifica che sia stata abilitata l'opzione per eseguire la pulizia WSUS sulle proprietà del componente del punto di aggiornamento software. Questa opzione consente di migliorare le prestazioni di WSUS. Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Immagini d'avvio inutilizzate**: immagini di avvio a cui non viene fatto riferimento per l'avvio PXE o per l'uso di sequenze di attività. Per altre informazioni, vedere [Manage boot images](/sccm/osd/get-started/manage-boot-images) (Gestire le immagini d'avvio).  

- **Elementi di configurazione inutilizzati**: elementi di configurazione che non fanno parte di una linea di base di configurazione e sono anteriori a 30 giorni. Per altre informazioni, vedere [Creare configurazioni di base](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Aggiorna le origini di peer cache alla versione più recente del client di Configuration Manager**: identificare i client che fungono da origine di peer cache, ma non sono stati aggiornati da una versione del client precedente alla 1806. I client precedenti alla versione 1806 non possono essere usati come origine di peer cache per i client che eseguono la versione 1806 o versioni successive. Selezionare **Intervieni** per aprire una visualizzazione del dispositivo che mostra l'elenco dei client.<!--1358008-->  

### <a name="security"></a>Sicurezza

Informazioni dettagliate per il miglioramento dell'infrastruttura e dei dispositivi.

- **Fallback NTLM abilitato**:<!--4572953--> a partire dalla versione 1906, questa regola rileva se è stato abilitato il metodo di fallback dell'autenticazione NTLM meno sicuro per il sito. Quando si usa il metodo di installazione push client per il client Configuration Manager, il sito può richiedere l'autenticazione reciproca Kerberos. Questo miglioramento consente di proteggere la comunicazione tra il server e il client. Per altre informazioni , vedere [Come installare i client con l'installazione push client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

- **Versioni client dell'antimalware non supportate**: più del 10% dei cliente esegue versioni di System Center Endpoint Protection che non sono più supportate. Per altre informazioni, vedere [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  

### <a name="simplified-management"></a>Gestione semplificata

Informazioni dettagliate utili per semplificare la gestione quotidiana dell'ambiente.

- **Connettere il sito al cloud Microsoft per gli aggiornamenti di Configuration Manager**: Questa regola assicura che il punto di connessione del servizio Configuration Manager sia stato connesso al cloud Microsoft negli ultimi sette giorni. Questa connessione consente di scaricare il contenuto per gli aggiornamenti regolari. Vedere DMPDownloader.log e hman.log. Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints#bkmk_scp-updates).

- **Versioni client non CB**: elenca tutti i client le cui versioni non corrispondono a una build Current Branch (CB). Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients).  

- **Aggiorna i client a una versione di Windows 10 supportata**: A partire dalla versione 1902, questa regola segnala i client che eseguono una versione di Windows 10 che non è più supportata. Include anche i client con una versione di Windows 10 che sta per raggiungere la fine del servizio (tre mesi).<!--3897268-->  

### <a name="software-center"></a>Software Center

Informazioni dettagliate per la gestione di Software Center.

- **Indirizza gli utenti a Software Center invece che al Catalogo applicazioni**: controlla se gli utenti hanno installato o richiesto applicazioni dal Catalogo applicazioni negli ultimi 14 giorni. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per i ruoli del Catalogo applicazioni termina con la versione 1910. Per altre informazioni, vedere [Funzionalità deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Usa la nuova versione di Software Center**: La versione precedente di Software Center non è più supportata. Configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#use-new-software-center) (Informazioni sulle impostazioni client).  

### <a name="software-updates"></a>Aggiornamenti software

- **Le impostazioni client non sono configurate per consentire ai client di scaricare contenuto differenziale**: Alcuni aggiornamenti software sincronizzati nell'ambiente includono contenuto differenziale. Abilitare l'impostazione del client **Consenti ai client di scaricare contenuto differenziale quando disponibile**. Se non si abilita questa impostazione, quando si distribuiscono questi aggiornamenti, il client scaricherà inutilmente più contenuto del necessario. Per altre informazioni, vedere [Impostazioni del client - Aggiornamenti software](/sccm/core/clients/deploy/about-client-settings#software-updates).

- **Abilitare la categoria di prodotti per gli aggiornamenti software 'Windows 10 versione 1903 e versioni successive'** : È presente una nuova categoria di prodotti per gli aggiornamenti software per Windows 10 versione 1903 e versioni successive. Se si sincronizzano gli aggiornamenti di Windows 10 e si hanno client Windows 10 versione 1903 o versioni successive, selezionare la categoria di prodotti **Windows 10 versione 1903 e versioni successive** nelle proprietà del componente del punto di aggiornamento software. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](/sccm/sum/get-started/configure-classifications-and-products).

### <a name="windows-10"></a>Windows 10

Informazioni dettagliate correlate alla distribuzione e alla manutenzione di Windows 10. Il gruppo di informazioni dettagliate sulla gestione di Windows 10 è disponibile solo quando in più della metà dei client è in esecuzione Windows 7, Windows 8 o Windows 8.1.

- **Configurare i dati di diagnostica di Windows e la chiave ID commerciale**: per usare i dati da Desktop Analytics, configurare i dispositivi con una chiave ID commerciale e abilitare la raccolta dei dati di diagnostica. Impostare i dispositivi Windows 10 sul livello **Avanzata (con limitazioni)** o superiore. Per altre informazioni, vedere [Abilitare la condivisione dei dati per Desktop Analytics](/configmgr/desktop-analytics/enable-data-sharing).

#### <a name="windows-10-management-insights-rules"></a>Regole di Informazioni dettagliate sulla gestione di Windows 10

![Informazioni dettagliate sulla gestione - Regole per Windows 10](./media/Windows-10-insights-group.png)
