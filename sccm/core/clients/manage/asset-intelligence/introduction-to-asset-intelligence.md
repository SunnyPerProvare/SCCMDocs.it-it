---
title: Introduzione ad Asset Intelligence | Microsoft Docs
description: Introduzione ad Asset Intelligence in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 6a851ddfeee78574fbb0b1eff0c7cc518a7bb598


---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Introduzione ad Asset Intelligence in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Asset Intelligence in System Center Configuration Manager consente di eseguire l'inventario e gestire l'utilizzo delle licenze software in tutta l'organizzazione mediante il catalogo di Asset Intelligence. Molte classi di Strumentazione gestione Windows (WMI) di inventario hardware estendono la gamma di informazioni raccolte sui componenti hardware e i titoli software in uso. Sono disponibili più di 60 report per la presentazione di queste informazioni in un formato di facile utilizzo. Molti di questi report sono collegati a report più specifici in cui è possibile eseguire una query per informazioni generali e il drill-down per informazioni più dettagliate. È possibile aggiungere informazioni personalizzate al catalogo di Asset Intelligence, ad esempio categorie software, famiglie software, etichette software e requisiti hardware. È anche possibile connettersi a System Center Online per aggiornare dinamicamente il catalogo di Asset Intelligence con le informazioni più aggiornate disponibili. I clienti Microsoft possono eseguire la riconciliazione dell'utilizzo delle licenze software aziendali in base alle licenze software acquistate tramite l'importazione di informazioni sulle licenze software nel database del sito di Configuration Manager.  

##  <a name="a-namebkmkassetintelligencecataloga-asset-intelligence-catalog"></a><a name="BKMK_AssetIntelligenceCatalog"></a> Catalogo di Asset Intelligence  

 Il catalogo di Asset Intelligence di Configuration Manager è un set di tabelle di database archiviate nel database del sito che contengono informazioni di categorizzazione e identificazione per oltre 300.000 titoli e versioni software. Queste tabelle di database vengono usate anche per gestire i requisiti hardware per specifici titoli software.  

 Il catalogo di Asset Intelligence offre informazioni sulle licenze software per i titoli software in uso, sia per software Microsoft che non Microsoft. Nel catalogo di Asset Intelligence è disponibile un set predefinito di requisiti hardware per i titoli software ed è possibile creare nuove informazioni per requisiti hardware definiti dall'utente per soddisfare requisiti personalizzati. È anche possibile personalizzare le informazioni nel catalogo di Asset Intelligence e caricare le informazioni sui titoli software personalizzati in System Center Online per la categorizzazione.  

 Sono disponibili aggiornamenti del catalogo di Asset Intelligence che contengono informazioni sui nuovi titoli software rilasciati e possono essere scaricati periodicamente per eseguire aggiornamenti in blocco del catalogo. In alternativa, è possibile aggiornare dinamicamente il catalogo tramite il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

###  <a name="a-namebkmksoftwarecategoriesa-software-categories"></a><a name="BKMK_SoftwareCategories"></a> Categorie software  
 Le categorie software di Asset Intelligence vengono usate per categorizzare in modo generale i titoli software di inventario e anche come raggruppamenti generali di famiglie software più specifiche. Un esempio di categoria software potrebbe essere "aziende del settore energetico" e una famiglia software all'interno di tale categoria software potrebbe essere "petrolio e gas" o "energia idroelettrica". Molte categorie software sono predefinite nel catalogo di Asset Intelligence ed è possibile creare categorie definite dall'utente per definire ulteriormente il software di inventario. Lo stato di convalida di tutte le categorie software predefinite è sempre **Convalidato**, mentre per le informazioni sulle categorie software personalizzate aggiunte al catalogo di Asset Intelligence lo stato è **Definito da utente**. Per altre informazioni su come gestire le categorie software, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

> [!NOTE]  
>  Le informazioni sulle categorie software predefinite archiviate nel catalogo di Asset Intelligence sono di sola lettura e non possono essere modificate o eliminate. Gli utenti amministratori possono aggiungere, modificare o eliminare categorie software definite dall'utente.  

###  <a name="a-namebkmksoftwarefamiliesa-software-families"></a><a name="BKMK_SoftwareFamilies"></a> Famiglie software  
 Le famiglie software di Asset Intelligence vengono usate per definire i titoli software di inventario all'interno delle categorie software. Molte famiglie software sono predefinite nel catalogo di Asset Intelligence ed è possibile creare famiglie definite dall'utente per definire ulteriormente il software di inventario. Lo stato di convalida di tutte le famiglie software predefinite è sempre **Convalidato**, mentre per le informazioni sulle famiglie software personalizzate aggiunte al catalogo di Asset Intelligence lo stato è **Definito da utente**. Per altre informazioni su come gestire le famiglie software, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

> [!NOTE]  
>  Le informazioni sulle famiglie software predefinite sono di sola lettura e non possono essere modificate. Gli utenti amministratori possono aggiungere, modificare o eliminare famiglie software definite dall'utente.  

###  <a name="a-namebkmkcustomlabelsa-software-labels"></a><a name="BKMK_CustomLabels"></a> Etichette software  
 Le etichette software di Asset Intelligence personalizzate consentono di creare filtri che è possibile usare per raggruppare i titoli software e visualizzarli nei report di Asset Intelligence. È possibile usare le etichette software per creare gruppi definiti dall'utente di titoli software con un attributo comune. Ad esempio, è possibile creare un'etichetta software Shareware, associare tale etichetta ai titoli shareware di inventario ed eseguire un report per visualizzare tutti i titoli di software a cui è associata l'etichetta Shareware. Le etichette software non sono predefinite. Lo stato di convalida per le etichette software è sempre **Definito da utente**. Per altre informazioni su come gestire le etichette software, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

###  <a name="a-namebkmkhardwarerequirementsa-hardware-requirements"></a><a name="BKMK_HardwareRequirements"></a> Requisiti hardware  
 È possibile usare le informazioni sui requisiti hardware per verificare che i computer soddisfino i requisiti hardware per i titoli software prima di sceglierli come destinazione per le distribuzioni di software. È possibile gestire i requisiti hardware per i titoli software nell'area **Asset e conformità** nel nodo **Requisiti hardware** all'interno del nodo **Asset Intelligence** . Molti requisiti hardware sono predefiniti nel catalogo di Asset Intelligence ed è possibile creare nuove informazioni per requisiti hardware definiti dall'utente per soddisfare requisiti personalizzati. Lo stato di convalida di tutti i requisiti hardware predefiniti è sempre **Convalidato**, mentre per le informazioni sui requisiti hardware definiti dall'utente aggiunti al catalogo di Asset Intelligence lo stato è **Definito da utente**. Per altre informazioni su come gestire i requisiti hardware, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

> [!NOTE]  
>  I requisiti hardware visualizzati nella console di Configuration Manager vengono recuperati dal catalogo di Asset Intelligence e non sono basati sulle informazioni dei titoli software di inventario dei client di System Center 2012 Configuration Manager. Le informazioni sui requisiti hardware non vengono aggiornate nell'ambito del processo di sincronizzazione con System Center Online. È possibile creare requisiti hardware definiti dall'utente per software di inventario senza requisiti hardware associati.  

 Per impostazione predefinita, per ogni requisito hardware elencato vengono visualizzate le informazioni seguenti:  

-   **Titolo software**: specifica il titolo software associato al requisito hardware.  

-   **CPU minima (MHz)**: specifica la velocità minima del processore, in megahertz (MHz), richiesta dal titolo software.  

-   **RAM minima (KB)**: specifica la RAM minima, in kilobyte (KB), richiesta dal titolo software.  

-   **Dimensioni minime spazio su disco (KB)**: specifica le dimensioni minime dello spazio disponibile nel disco rigido, in KB, richieste dal titolo software.  

-   **Dimensioni disco minime (KB)**: specifica le dimensioni minime del disco rigido, in KB, richieste dal titolo software.  

-   **Stato convalida**: specifica lo stato di convalida per il requisito hardware.  

 I requisiti hardware predefiniti archiviati nel catalogo di Asset Intelligence sono di sola lettura e non possono essere eliminati.  Gli utenti amministratori possono aggiungere, modificare o eliminare i requisiti hardware definiti dall'utente per i titoli software non archiviati nel catalogo di Asset Intelligence.  

##  <a name="a-namebkmkinventoriedsoftwaretitlesa-inventoried-software-titles"></a><a name="BKMK_InventoriedSoftwareTitles"></a> Titoli software di inventario  
 È possibile visualizzare informazioni sui titoli software di inventario nell'area di lavoro **Asset e conformità** nel nodo **Software di inventario** all'interno del nodo **Asset Intelligence** . Hardware Inventory Client Agent raccoglie le informazioni sul software di inventario dai client di Configuration Manager in base ai titoli software archiviati nel catalogo di Asset Intelligence.  

> [!WARNING]  
>  Hardware Inventory Client Agent raccoglie l'inventario in base alle classi di report di inventario hardware di Asset Intelligence. Per altre informazioni su come gestire le classi di report, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

 Per impostazione predefinita, per ogni titolo software di inventario vengono visualizzate le informazioni seguenti:  

-   **Nome**: specifica il nome del titolo software di inventario.  

-   **Fornitore**: specifica il nome del fornitore che ha sviluppato il titolo software di inventario.  

-   **Versione**: specifica la versione del prodotto del titolo software di inventario.  

-   **Categoria**: specifica la categoria software attualmente assegnata al titolo software di inventario.  

-   **Famiglia**: specifica la famiglia software attualmente assegnata al titolo software di inventario.  

-   **Etichetta** [**1**, **2**e **3**]: specifica le etichette personalizzate associate al titolo software. Ai titoli software di inventario possono essere associate fino a tre etichette personalizzate.  

-   **Conteggio**: specifica il numero di client di Configuration Manager che hanno il titolo software in inventario.  

-   **Stato**: specifica lo stato di convalida per il titolo software di inventario.  

> [!NOTE]  
>  È possibile modificare le informazioni di categorizzazione (nome prodotto, fornitore, categoria software e famiglia software) per il software di inventario solo nel sito principale nella gerarchia. Dopo aver modificato le informazioni di categorizzazione per software predefiniti, lo stato di convalida per le modifiche software cambia da **Convalidato** a **Definito da utente**.  

##  <a name="a-nameassetintelligencesycnronizationpointa-asset-intelligence-synchronization-point"></a><a name="AssetIntelligenceSycnronizationPoint"></a> Punto di sincronizzazione di Asset Intelligence  
 Il punto di sincronizzazione di Asset Intelligence è un ruolo del sistema del sito di Configuration Manager usato per connettersi a System Center Online (tramite la porta TCP 443) per gestire gli aggiornamenti dinamici alle informazioni del catalogo di Asset Intelligence. Questo ruolo del sito può essere installato solo nel sito principale della gerarchia. È necessario configurare tutte le personalizzazioni del catalogo di Asset Intelligence tramite una console di Configuration Manager connessa al sito principale. Anche se tutti gli aggiornamenti devono essere configurati nel sito principale, le informazioni del catalogo di Asset Intelligence vengono replicate negli altri siti nella gerarchia. Il ruolo del sito del punto di sincronizzazione di Asset Intelligence consente di richiedere la sincronizzazione del catalogo su richiesta con System Center Online o di pianificare la sincronizzazione automatica del catalogo. Oltre al download di nuove informazioni per il catalogo di Asset Intelligence, il punto di sincronizzazione di Asset Intelligence consente di caricare le informazioni sui titoli software personalizzati in System Center Online per la categorizzazione. Microsoft considera informazioni pubbliche tutti i titoli software caricati in System Center Online per la categorizzazione. È quindi necessario accertarsi che i titoli software personalizzati non contengano informazioni riservate o proprietarie.  

> [!NOTE]  
>  Dopo l'invio di un titolo software senza categoria, quando ci sono almeno 4 richieste di categorizzazione dei clienti per lo stesso titolo software, i ricercatori di System Center Online identificano, categorizzano e quindi rendono disponibili le informazioni di categorizzazione del titolo software per tutti i clienti che usano il servizio online. Viene assegnata la massima priorità ai titoli software con il maggior numero di richieste di categorizzazione. È improbabile che al software personalizzato e alle applicazioni line-of-business venga assegnata una categoria e la procedura consigliata prevede di non inviare questi titoli software a Microsoft per la categorizzazione.  

> [!NOTE]  
>  Per connettersi a System Center Online, è necessario un ruolo del sistema del sito del punto di sincronizzazione. Per informazioni sull'installazione di un punto di sincronizzazione di Asset Intelligence, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).  

##  <a name="a-namebkmkassetintelligencehomepagea-asset-intelligence-home-page"></a><a name="BKMK_AssetIntelligenceHomePage"></a> Home page di Asset Intelligence  
 Il nodo **Asset Intelligence** nell'area di lavoro **Asset e conformità** è la home page di Asset Intelligence in Configuration Manager. La home page di **Asset Intelligence** visualizza un dashboard di riepilogo delle informazioni del catalogo di Asset Intelligence.  

> [!NOTE]  
>  La home page di **Asset Intelligence** non viene in genere aggiornata automaticamente mentre è visualizzata.  

 La home page di **Asset Intelligence** è divisa nelle sezioni seguenti:  

-   **Sincronizzazione catalogo**: fornisce informazioni sullo stato di abilitazione di Asset Intelligence e sullo stato corrente del punto di sincronizzazione di Asset Intelligence. In questa sezione sono anche disponibili informazioni sulla pianificazione della sincronizzazione, sul fatto che il resoconto delle licenze cliente sia stato o meno importato, sulla data dell'ultimo aggiornamento dello stato e sull'ora per il successivo aggiornamento pianificato, nonché sul numero di modifiche apportate dopo l'installazione del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

    > [!NOTE]  
    >  La sezione relativa alla sincronizzazione del catalogo di Asset Intelligence nella home page di **Asset Intelligence** viene visualizzata solo se è stato installato un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

-   **Stato software di inventario**: fornisce il conteggio e la percentuale per software, categorie software e famiglie software di inventario identificati da Microsoft, identificati da un amministratore, con identificazione online in sospeso o non identificati e non in sospeso. Le informazioni visualizzate in formato di tabella mostrano i conteggi, mentre le informazioni visualizzate nel grafico mostrano le percentuali.  

##  <a name="a-namebkmkassetintelligencereportsa-asset-intelligence-reports"></a><a name="BKMK_AssetIntelligenceReports"></a> Report di Asset Intelligence  
 I report di Asset Intelligence si trovano nella console di Configuration Manager, nell'area di lavoro **Monitoraggio** nella cartella Asset Intelligence nel nodo **Creazione report**. I report forniscono informazioni su hardware, gestione delle licenze e software. Per altre informazioni sui report in Configuration Manager, vedere [Creazione di report in Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  La precisione delle informazioni su licenze e quantità dei titoli software installati visualizzate nei report di Asset Intelligence può variare rispetto al numero effettivo di titoli software installati o licenze in uso nell'ambiente, a causa delle complesse dipendenze e limitazioni associate all'esecuzione dell'inventario delle informazioni sulle licenze per i titoli software installati in ambienti aziendali. Non usare i report di Asset Intelligence come unica fonte per determinare la conformità delle licenze software acquistate.  

###  <a name="a-namebkmkhardwarereportsa-asset-intelligence-hardware-reports"></a><a name="BKMK_HardwareReports"></a> Report di Asset Intelligence sull'hardware  
 I report di Asset Intelligence sull'hardware forniscono informazioni sulle risorse hardware nell'organizzazione. Sulla base delle informazioni di inventario hardware, come velocità, memoria, dispositivi e altre, i report di Asset Intelligence sull'hardware possono presentare informazioni sui dispositivi USB, sull'hardware che deve essere aggiornato e anche sui computer che non sono pronti per un aggiornamento software specifico.  

> [!NOTE]  
>  Alcuni dati utente nei report di Asset Intelligence sull'hardware vengono raccolti dal registro eventi di sicurezza del sistema. Per una maggiore accuratezza dei report, si consiglia di cancellare questo registro quando si riassegna un computer a un nuovo utente.  

###  <a name="a-namebkmklicensemanagementreportsa-asset-intelligence-license-management-reports"></a><a name="BKMK_LicenseManagementReports"></a> Report di Asset Intelligence sulla gestione delle licenze  
 I report di Asset Intelligence sulla gestione delle licenze forniscono dati relativi alle licenze in uso. Il report sul Ledger License elenca le applicazioni Microsoft installate in un formato congruente con un resoconto delle licenze Microsoft. Si tratta di un metodo pratico per abbinare le licenze acquistate a quelle usate. Altri report sulla gestione delle licenze forniscono informazioni sui computer che fungono da server per l'esecuzione del Servizio di gestione delle chiavi (KMS) per dati statistici sull'attivazione del sistema operativo.  

> [!IMPORTANT]  
>  Vari report di Asset Intelligence sulla gestione delle licenze presentano informazioni sulla funzione del Server di gestione delle chiavi, un metodo per l'amministrazione di contratti multilicenza. Se non è stato implementato un Server di gestione delle chiavi, alcuni report potrebbe non restituire dati. Per altre informazioni sul Server di gestione delle chiavi, cercare KMS in [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="a-namebkmksoftwarereportsa-asset-intelligence-software-reports"></a><a name="BKMK_SoftwareReports"></a> Report di Asset Intelligence sul software  
 I report di Asset Intelligence sul software forniscono informazioni su famiglie software, categorie software e titoli software specifici installati nei computer dell'organizzazione. I report sul software presentano informazioni sugli oggetti browser helper, il software avviato automaticamente e altro ancora. Questi report possono essere usati per identificare adware, spyware e altro malware, nonché per individuare software ridondante e quindi ottimizzare l'acquisto e il supporto tecnico del software.  

###  <a name="a-namebkmksoftwareidtagreportsa-asset-intelligence-software-identification-tag-reports"></a><a name="BKMK_SoftwareIdTagReports"></a> Report di Asset Intelligence sui tag di identificazione software  
 I report di Asset Intelligence sui tag di identificazione software forniscono informazioni sul software che contiene un tag di identificazione conforme allo standard ISO/IEC 19770-2. I tag di identificazione software forniscono informazioni autorevoli usate per identificare il software installato. Quando si abilita la classe di report di inventario hardware SMS_SoftwareTag, Configuration Manager raccoglie informazioni sul software con tag di identificazione software. I report seguenti forniscono informazioni sul software:  

-   **Software 14A - Ricerca di software con tag di identificazione software abilitato**: questo report fornisce il conteggio del software installato con un tag di identificazione software abilitato.  

-   **Software 14B - Computer con software specifico installato con tag di identificazione software abilitato**: questo report elenca tutti i computer con software installato con un tag di identificazione software specifico abilitato.  

-   **Software 14C - Software istallato con tag di identificazione software abilitato in un computer specifico**: questo report elenca tutto il software installato con un tag di identificazione software specifico abilitato in un computer specifico.  

###  <a name="a-namebkmkreportinglimitationsa-asset-intelligence-reporting-limitations"></a><a name="BKMK_ReportingLImitations"></a> Limitazioni dei report di Asset Intelligence  
 I report di Asset Intelligence possono fornire grandi quantità di informazioni sui titoli software installati e sulle licenze software acquistate in uso. Queste informazioni non dovrebbero essere tuttavia usate come unica fonte per determinare la conformità delle licenze software acquistate.  

####  <a name="a-namebkmkexampledependenciesa-example-dependencies"></a><a name="BKMK_ExampleDependencies"></a> Esempi di dipendenze  
 La precisione delle quantità visualizzate nei report di Asset Intelligence per i titoli software installati e le licenze possono variare rispetto alle quantità effettive in uso, a causa delle complesse dipendenze associate all'esecuzione dell'inventario delle informazioni sulle licenze per i titoli software in uso in ambienti aziendali. Gli esempi seguenti mostrano le dipendenze correlate all'esecuzione dell'inventario del software installato nell'organizzazione tramite Asset Intelligence, che potrebbero influire sulla precisione dei report di Asset Intelligence:  

 **Dipendenze dell'inventario hardware dei client**  
 I report di Asset Intelligence sul software installato si basano sui dati raccolti dai client di Configuration Manager mediante l'estensione dell'inventario hardware per abilitare i report di Asset Intelligence. A causa di questa dipendenza dai report di inventario hardware, i report di Asset Intelligence includono solo i dati dai client di Configuration Manager che completano correttamente i processi di inventario hardware con le classi di report WMI di Asset Intelligence richieste abilitate. Poiché poi i client di Configuration Manager eseguono i processi di inventario hardware in base a una pianificazione definita dall'utente amministratore, potrebbe verificarsi un ritardo nella generazione dei report dei dati, con effetti sulla precisione dei report di Asset Intelligence. Ad esempio, un titolo software in licenza di inventario potrebbe essere disinstallato dopo il completamento di un ciclo di inventario hardware corretto del client. Tuttavia, il titolo software viene indicato come installato nei report di Asset Intelligence fino al successivo ciclo di report di inventario hardware pianificato del client.  

 **Dipendenze di pacchetti software**  
 Dato che i report di Asset Intelligence sono basati sui dati relativi ai titoli software installati tramite i processi di inventario hardware standard dei client di Configuration Manager, la raccolta di alcuni dati sui titoli software potrebbe non essere corretta. Ad esempio, si potrebbero ottenere report di Asset Intelligence non accurati a causa di installazioni software non conformi ai processi di installazione standard o modificate prima dell'installazione.  

####  <a name="a-namebkmklegallimitationsa-legal-limitations"></a><a name="BKMK_LegalLimitations"></a> Limitazioni legali  
 Le informazioni visualizzate nei report di Asset Intelligence sono soggette a molte limitazioni e non rappresentano suggerimenti di tipo legale, finanziario o professionale. Le informazioni fornite dai report di Asset Intelligence sono solo a scopo informativo e non dovrebbero essere usate come unica fonte di informazioni per determinare la conformità di utilizzo delle licenze software.  

 Gli esempi seguenti illustrano le limitazioni correlate all'esecuzione dell'inventario del software installato e dell'utilizzo delle licenze nell'organizzazione tramite Asset Intelligence, che potrebbero influire sulla precisione dei report di Asset Intelligence:  

 **Limitazioni relative alle quantità di utilizzo delle licenze Microsoft**  
 -   La quantità di licenze software Microsoft acquistate si basa sulle informazioni fornite dagli amministratori e dovrebbe essere verificata attentamente per assicurarsi che venga fornito il numero corretto di licenze software.  

-   La quantità di licenze software Microsoft indicata nei report contiene informazioni solo sulle licenze software Microsoft acquistate tramite contratti multilicenza e non include informazioni per le licenze software acquistate al dettaglio, tramite OEM o altri canali di vendita.  

-   Le licenze software acquistate negli ultimi 45 giorni potrebbero non essere incluse nella quantità di licenze software Microsoft indicata nei report a causa dei requisiti e delle pianificazioni per i report del rivenditore del software.  

-   Le quantità di licenze software Microsoft potrebbero non rispecchiare le modifiche dovute a trasferimenti delle licenze software in seguito a fusioni o acquisizioni.  

-   I termini e le condizioni in un contratto multilicenza Microsoft potrebbero influire sul numero di licenze software indicato nei report e potrebbero quindi essere necessarie ulteriori verifiche da parte di un rappresentante Microsoft.  

 **Limitazioni relative alle quantità di titoli software installati**  
 I client di Configuration Manager devono completare correttamente i cicli di report di inventario hardware per far sì che i report di Asset Intelligence contengano informazioni accurate sulle quantità di titoli software installati. Potrebbe anche verificarsi un ritardo tra l'installazione o la disinstallazione di un titolo software concesso in licenza dopo un ciclo di report di inventario hardware corretto e le informazioni aggiornate potrebbero non comparire nei report di Asset Intelligence prima dell'inventario hardware pianificato successivo del client.  

 **Limiti relativi alla riconciliazione delle licenze**  
 La riconciliazione della quantità di titoli software installati e della quantità di licenze software acquistate viene eseguita confrontando la quantità di licenze specificata dall'amministratore e la quantità di titoli software installati raccolta dagli inventari hardware dei client di Configuration Manager in base alla pianificazione impostata dall'amministratore. Questo confronto non offre dati conclusivi per Microsoft in merito alla situazione delle licenze. La situazione effettiva delle licenze dipende dalle licenze e dai diritti di utilizzo effettivi concessi per uno specifico titolo software in base alle condizioni di licenza.  

##  <a name="a-namebkmkvalidationstatesa-asset-intelligence-validation-states"></a><a name="BKMK_ValidationStates"></a> Stati di convalida di Asset Intelligence  
 Gli stati di convalida di Asset Intelligence rappresentano lo stato di convalida di origine e corrente delle informazioni nel catalogo di Asset Intelligence. La tabella seguente illustra i possibili stati di convalida di Asset Intelligence e le azioni dell'amministratore che possono causarli.  

|**Stato**|**Definizione**|**Azione dell'amministratore**|**Commentoo**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Convalidato**|L'elemento del catalogo è stato definito dai ricercatori di System Center Online.|Nessuna.|Stato ottimale.|  
|**Definito da utente**|L'elemento del catalogo non è stato definito dai ricercatori di System Center Online.|Personalizzazione delle informazioni del catalogo locale.|Questo stato viene visualizzato nei report di Asset Intelligence.|  
|**In sospeso**|L'elemento del catalogo non è stato definito dai ricercatori di System Center Online, ma l'elemento è stato inviato a System Center Online per la categorizzazione.|Richiesta di categorizzazione da System Center Online.|L'elemento del catalogo rimane in questo stato fino a quando i ricercatori di System Center Online non categorizzano l'elemento e il catalogo di Asset Intelligence non viene sincronizzato.|  
|**Aggiornabile**|Un elemento di catalogo definito dall'utente è stato categorizzato in modo diverso da System Center Online durante una categorizzazione del catalogo successiva.|Personalizzazione del catalogo di Asset Intelligence locale per classificare un elemento come definito dall'utente.|È possibile usare l'azione Risolvi conflitto per decidere se usare le nuove informazioni di categorizzazione o il valore definito dall'utente precedente. Per altre informazioni su come risolvere i conflitti, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).|  
|**Senza categoria**|L'elemento del catalogo non è stato definito dai ricercatori di System Center Online, l'elemento non è stato inviato a System Center Online per la categorizzazione e l'amministratore non ha assegnato un valore di categorizzazione definito dall'utente.|Nessuna.|Richiesta di categorizzazione o personalizzazione delle informazioni del catalogo locale.<br /><br /> Per altre informazioni su come richiedere la categorizzazione, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).<br /><br /> Per altre informazioni su come modificare la categoria per il titolo software, vedere [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md) (Configurazione di Asset Intelligence in System Center Configuration Manager).|  

> [!NOTE]  
>  Gli elementi del catalogo inviati a System Center Online per la categorizzazione hanno lo stato di convalida **In attesa** in un sito di amministrazione centrale, ma vengono ancora visualizzati con lo stato di convalida **Senza categoria** nei siti primari figlio.  

> [!NOTE]  
>  Dopo aver risolto un conflitto di categorizzazione, l'elemento non viene convalidato di nuovo come in conflitto, a meno che gli aggiornamenti della categorizzazione successivi non introducano nuove informazioni sull'elemento.  

 Per esempi di quando uno stato di convalida può eseguire la transizione da uno stato a un altro, vedere [Example validation state transitions for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md) (Transizioni dello stato di convalida di esempio per Asset Intelligence in System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


