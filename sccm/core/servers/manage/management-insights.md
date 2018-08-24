---
title: Informazioni dettagliate sulla gestione
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità Informazioni dettagliate sulla gestione disponibile nella console di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 92f82ee7247030d19df63e50b0ac4437f250717a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383498"
---
# <a name="management-insights-in-configuration-manager"></a>Informazioni dettagliate sulla gestione in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La funzionalità Informazioni dettagliate sulla gestione in Configuration Manager offre indicazioni utili sullo stato corrente dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. Questa funzionalità è stata rilasciata in Configuration Manager versione 1802. <!--1353967-->



## <a name="review-management-insights"></a>Esaminare le informazioni dettagliate sulla gestione 

Per visualizzare le regole, l'account deve disporre dell'autorizzazione di **lettura** per l'oggetto **sito**.

1. Aprire la console di Configuration Manager.  

2. Passare all'area di lavoro **Amministrazione** e fare clic su **Informazioni dettagliate sulla gestione**.  

3. Selezionare **Tutte le informazioni dettagliate**.  

4. Fare doppio clic sul **Nome del gruppo di informazioni dettagliate sulla gestione** che si desidera esaminare. In alternativa, evidenziarlo e fare clic su **Mostra le informazioni dettagliate** nella barra multifunzione.  

È possibile esaminare le quattro schede seguenti: 

- **Tutte le regole**: offre l'elenco completo delle regole per il gruppo di informazioni dettagliate di gestione scelto.  

- **Completa**: elenca le regole in cui non è necessaria alcuna azione.  

- **In corso**: mostra le regole in cui alcuni, ma non tutti i prerequisiti sono soddisfatti.  

- **Azione richiesta**: sono elencate le regole che richiedono le azioni adottate. Fare clic con il pulsante destro del mouse e scegliere **Altri dettagli** per recuperare elementi specifici in cui è necessaria un'azione.  

Nel riquadro **Prerequisiti** sono elencati gli elementi obbligatori per eseguire la regola.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Tutte le regole e i prerequisiti per il gruppo di servizi cloud
![Informazioni dettagliate sulla gestione- Tutte le regole e i prerequisiti per il gruppo di servizi cloud](./media/Management-insights-all-cloud-rules.png)


Selezionare una regola e fare clic su **Altri dettagli** per visualizzarne i dettagli.



## <a name="operations"></a>Operazioni

Le regole delle informazioni dettagliate sulla gestione rivalutano la loro applicabilità a una pianificazione settimanale. Per valutare nuovamente una regola su richiesta, fare clic con il pulsante destro del mouse sulla regola e selezionare **Valuta di nuovo**.

Il file di log per le regole di Informazioni dettagliate sulla gestione è **SMS_DataEngine.log** ed è disponibile nel server del sito.

<!--1357930--> A partire dalla versione 1806, alcune regole consentono di intervenire. Selezionare una regola, fare clic su **Altri dettagli** e quindi, se disponibile, fare clic su **Intervieni**. 

A seconda della regola, questa azione presenta uno dei comportamenti seguenti:  

- Passare direttamente nella console al nodo in cui è possibile eseguire ulteriori azioni. Ad esempio, se le informazioni dettagliate sulla gestione consigliano di modificare un'impostazione client, l'opzione per eseguire un'azione consente di passare al nodo Impostazioni client. Eseguire quindi ulteriori azioni modificando l'impostazione predefinita o un oggetto impostazioni client personalizzato.  

- Passare a una visualizzazione filtrata in base a una query. Ad esempio, eseguire l'azione per la regola delle raccolte vuote mostra semplicemente queste raccolte nell'elenco delle raccolte. Eseguire quindi eseguire ulteriori azioni, ad esempio eliminare una raccolta o modificarne le regole di appartenenza.  



## <a name="groups-and-rules"></a>Gruppi e regole

Le regole sono organizzate in diversi gruppi di informazioni dettagliate sulla gestione. Vedere l'elenco seguente per i gruppi e le regole attualmente disponibili:


### <a name="applications"></a>Applicazioni

Informazioni dettagliate per la gestione delle applicazioni.

- **Applicazioni senza distribuzioni**: elenca le applicazioni dell'ambiente per cui non esistono distribuzioni attive. Questa regola aiuta a individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](/sccm/apps/deploy-use/deploy-applications).  


### <a name="cloud-services"></a>Servizi cloud

Facilita l'integrazione con molti servizi cloud per una gestione moderna dei dispositivi. 

- **Valuta l'idoneità per la co-gestione**: consente di comprendere i passaggi necessari per abilitare la co-gestione. Questa regola ha dei prerequisiti. Per altre informazioni, vedere la [panoramica sulla co-gestione](/sccm/core/clients/manage/co-management-overview).  

- **Configura i servizi di Azure per l'uso con Configuration Manager**: questa regola consente di eseguire l'onboarding di Configuration Manager in Azure AD, in modo che i client possano usare Azure AD per eseguire l'autenticazione al sito. Per altre informazioni, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Consenti dispositivi ibridi aggiunti ad Azure Active Directory**: i dispositivi aggiunti ad Azure AD consentono agli utenti di accedere con le credenziali del dominio garantendo al contempo che i dispositivi soddisfino gli standard di sicurezza e conformità dell'organizzazione. Per altre informazioni, vedere [Considerazioni di progettazione dell'identità ibrida di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Aggiorna i client alla versione più recente di Windows 10**: Windows 10, versione 1709 o versioni successive, migliora e modernizza l'esperienza di elaborazione degli utenti. Per altre informazioni, vedere [Articoli principali sull'adozione di Windows as a Service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Raccolte

Informazioni dettagliate che consentono di semplificare la gestione tramite la pulizia e la riconfigurazione delle raccolte.

- **Raccolte vuote**: elenca le raccolte dell'ambiente che non contengono membri. Per altre informazioni, vedere [Come gestire le raccolte](/sccm/core/clients/manage/collections/manage-collections).  


### <a name="proactive-maintenance"></a>Manutenzione proattiva
<!--1352184--> A partire dalla versione 1806, le regole in questo gruppo evidenziano potenziali problemi di configurazione che possono essere evitati tramite la manutenzione degli oggetti di Configuration Manager.    

- **Gruppi di limiti senza sistemi del sito assegnati**: senza sistemi del sito assegnati, i gruppi di limiti possono essere usati solo per l'assegnazione del sito. Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Gruppi di limiti senza membri**: i gruppi di limiti non sono applicabili per l'assegnazione del sito o la ricerca di contenuto se non hanno membri. Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Distribution points not serving content to clients** (Punti di distribuzione che non servono contenuto ai client): punti di distribuzione che non hanno servito contenuto ai client negli ultimi 30 giorni. I dati sono basati sui report dai client della relativa cronologia di download. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Abilita la pulizia WSUS**: verifica che sia stata abilitata l'opzione per eseguire la pulizia WSUS sulle proprietà del componente del punto di aggiornamento software. Questa opzione consente di migliorare le prestazioni di WSUS. Per altre informazioni, vedere [Manutenzione degli aggiornamenti software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Immagini d'avvio inutilizzate**: immagini di avvio a cui non viene fatto riferimento per l'avvio PXE o per l'uso di sequenze di attività. Per altre informazioni, vedere [Manage boot images](/sccm/osd/get-started/manage-boot-images) (Gestire le immagini d'avvio).  

- **Elementi di configurazione inutilizzati**: elementi di configurazione che non fanno parte di una baseline di configurazione e sono anteriori a 30 giorni. Per altre informazioni, vedere [Creare configurazioni di base](/sccm/compliance/deploy-use/create-configuration-baselines).  


### <a name="security"></a>Sicurezza
Informazioni dettagliate per il miglioramento dell'infrastruttura e dei dispositivi. 

- **Versioni client dell'antimalware non supportate**: più del 10% dei client esegue versioni di System Center Endpoint Protection che non sono supportate. Per altre informazioni, vedere [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Gestione semplificata

Informazioni dettagliate utili per semplificare la gestione quotidiana dell'ambiente. 

- **Versioni client non CB**: elenca tutti i client le cui versioni non corrispondono a una build Current Branch (CB). Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients).  


### <a name="software-center"></a>Software Center

Informazioni dettagliate per la gestione di Software Center. 

- **Indirizza gli utenti a Software Center invece che al Catalogo applicazioni**: controlla se gli utenti hanno installato o richiesto applicazioni dal Catalogo applicazioni negli ultimi 14 giorni. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per il sito Web del Catalogo applicazioni è terminato con la versione 1806. Per altre informazioni, vedere [Funzionalità deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Usa la nuova versione di Software Center**: la versione precedente di Software Center non è più supportata. Configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#use-new-software-center) (Informazioni sulle impostazioni client).  


### <a name="windows-10"></a>Windows 10

Informazioni dettagliate correlate alla distribuzione e alla manutenzione di Windows 10. Il gruppo di informazioni dettagliate sulla gestione di Windows 10 è disponibile solo quando in più della metà dei client è in esecuzione Windows 7, Windows 8 o Windows 8.1.

- **Configura la telemetria di Windows e la chiave ID commerciale**: per usare i dati di Preparazione aggiornamenti, configurare i dispositivi con una chiave ID commerciale e abilitare la telemetria. Impostare i dispositivi Windows 10 sul livello di telemetria Avanzata (con limitazioni) o superiore. Per altre informazioni, vedere [Configurare i client per segnalare i dati a Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Connetti Configuration Manager a Preparazione aggiornamenti**: sfruttare Preparazione aggiornamenti per velocizzare le distribuzioni di Windows 10 prima che venga abbandonato il supporto di Windows 7. Per altre informazioni, vedere [Integrare Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Regole di Informazioni dettagliate sulla gestione di Windows 10
![Informazioni dettagliate sulla gestione - Regole per Windows 10](./media/Windows-10-insights-group.png)
