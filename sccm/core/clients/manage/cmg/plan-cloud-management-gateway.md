---
title: Pianificare il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Pianificare e progettare il gateway di gestione di cloud (CMG) per semplificare la gestione dei client basati su Internet.
ms.date: 10/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bf459474c00348f1da01a1a3958772376adbb01
ms.sourcegitcommit: 8c10745cb4e2baabba2af4821cb207a2f91d2eb3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/24/2020
ms.locfileid: "80138087"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Pianificare il gateway di gestione cloud in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1101764-->
Il gateway di gestione cloud (CMG) consente di gestire i client di Configuration Manager in Internet in modo semplice. Distribuendo il gateway di gestione cloud come servizio cloud in Microsoft Azure, è possibile gestire i client tradizionali che effettuano il roaming in Internet senza un'infrastruttura locale aggiuntiva. Inoltre non è necessario esporre l'infrastruttura locale a Internet.

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

Dopo aver definito i prerequisiti, la creazione del gateway di gestione cloud (CMG) prevede i tre passaggi seguenti nella console di Configuration Manager:

1. Distribuire il servizio cloud Cloud Management Gateway (CMG) in Azure.
2. Aggiungere il ruolo del punto di connessione del gateway di gestione cloud.
3. Configurare il sito e i ruoli del sito per il servizio.
Dopo la distribuzione e la configurazione, i client possono accedere facilmente ai ruoli dei siti locali, indipendentemente dal fatto che si trovino nella Intranet o in Internet.

Questo articolo offre le nozioni fondamentali sul gateway di gestione cloud, sulla progettazione per l'ambiente e sulla pianificazione dell'implementazione del gateway.


## <a name="scenarios"></a>Scenari

Un gateway di gestione cloud può essere utile in scenari diversi. Gli scenari seguenti sono alcuni degli scenari più comuni:  

- Gestire client Windows tradizionali con identità appartenente al dominio di Active Directory. Questi client includono Windows 8.1 e Windows 10. Per la protezione del canale di comunicazione vengono usati certificati PKI. Le attività di gestione includono:  
    - Aggiornamenti software e protezione degli endpoint
    - Inventario e stato del client
    - Impostazioni di conformità
    - Distribuzione del software al dispositivo
    - Sequenza di attività di aggiornamento sul posto di Windows 10

- Gestire i client Windows 10 tradizionali con identità moderna, ibridi o solo aggiunti al dominio cloud con Azure Active Directory (Azure AD). Per l'autenticazione i client usano Azure AD anziché i certificati PKI. L'uso di Azure AD è più semplice da configurare e gestire rispetto ai sistemi PKI più complessi. Le attività di gestione sono le stesse del primo scenario, come anche:  
    - Distribuzione del software all'utente  

- Installare il client Configuration Manager in dispositivi Windows 10 tramite Internet. L'uso di Azure AD consente al dispositivo di eseguire l'autenticazione nel gateway di gestione cloud per la registrazione e l'assegnazione dei client. È possibile installare il client manualmente oppure usando un altro metodo di distribuzione del software, ad esempio Microsoft Intune.  

- Nuovo provisioning di dispositivi von co-gestione. Quando si esegue la registrazione automatica dei client esistenti, CMG non è necessario per la co-gestione. È necessario per i nuovi dispositivi che prevedono l'uso di Windows AutoPilot, Azure AD, Microsoft Intune e Configuration Manager. Per altre informazioni, vedere [Percorsi della co-gestione](https://docs.microsoft.com/sccm/comanage/quickstart-paths).

### <a name="specific-use-cases"></a>Casi d'uso specifici

In questi scenari possono essere applicati i casi d'uso di dispositivi specifici seguenti:

- Dispositivi che effettuano il roaming, ad esempio i computer portatili  

- Dispositivi remoti o di succursali che offrono una gestione su Internet meno costosa e più efficiente rispetto a quella tramite WAN o VPN.  

- Fusioni e acquisizioni in cui può risultare più semplice aggiungere dispositivi ad Azure AD e gestirli tramite un gateway di gestione cloud.  

> [!Important]
> Per impostazione predefinita tutti i client ricevono i criteri di un gateway di gestione cloud e iniziano a usarli quando diventano basati su Internet. A seconda dello scenario e del caso d'uso applicabile all'organizzazione, può essere necessario definire l'ambito di utilizzo del gateway di gestione cloud. Per altre informazioni, vedere l'impostazione client [Consenti ai client di usare un gateway di gestione cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).


## <a name="topology-design"></a>Progettazione della topologia

### <a name="cmg-components"></a>Componenti del gateway di gestione cloud

La distribuzione e l'utilizzo del gateway di gestione cloud includono i componenti seguenti:  

- Il **servizio cloud Cloud Management Gateway (CMG)** in Azure esegue l'autenticazione e inoltra le richieste del client Configuration Manager al punto di connessione del gateway di gestione cloud.  

- Il ruolo del sistema del sito del **punto di connessione del gateway di gestione cloud** abilita una connessione coerente e ad alte prestazioni dalla rete locale al servizio Cloud Management Gateway (CMG) in Azure. Pubblica anche le impostazioni nel gateway di gestione cloud, incluse le informazioni sulla connessione e le impostazioni di sicurezza. Il punto di connessione del gateway di gestione cloud inoltra le richieste del client dal gateway di gestione cloud ai ruoli locali in base al mapping degli URL.

- Il ruolo del sistema del sito del [**punto di connessione del servizio**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) esegue il componente di gestione del servizio cloud che gestisce tutte le attività di distribuzione del gateway di gestione cloud. Esegue inoltre il monitoraggio e l'invio di informazioni sull'integrità del servizio e di registrazione da Azure AD. Verificare che il punto di connessione del servizio sia in [modalità online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- Il ruolo del sistema del sito del **punto di gestione** risponde alle richieste del client normalmente.  

- Il ruolo del sistema del sito del **punto di aggiornamento software** risponde alle richieste del client normalmente.  

- I **client basati su Internet** si connettono al gateway di gestione cloud per accedere ai componenti di Configuration Manager locali.

- Il gateway di gestione cloud usa un servizio Web **HTTPS basato sui certificati** per proteggere la comunicazione di rete con i client.  

- I client basati su Internet usano i **certificati PKI o Azure AD** per l'identità e l'autenticazione.  

- Un [**punto di distribuzione cloud**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) fornisce i contenuti ai client basati su Internet, in base alle esigenze.  

    - A partire dalla versione 1806, un CMG può anche trasferire contenuti ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. Per altre informazioni, vedere [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificare un gateway di gestione cloud).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Creare il Cloud Management Gateway usando una **distribuzione Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) è una piattaforma moderna per la gestione di tutte le risorse di una soluzione come una singola entità detta [gruppo di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando si distribuisce Cloud Management Gateway con Azure Resource Manager, il sito usa Azure Active Directory (Azure AD) per autenticare e creare le risorse cloud necessarie. Questa distribuzione modernizzata non richiede il certificato di gestione classico di Azure.  

> [!Note]  
> Questa funzionalità non supporta i provider di servizi cloud di Azure. La distribuzione del gateway di gestione cloud con Azure Resource Manager continua infatti a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services) (servizi di Azure disponibili in Azure CSP).

A partire da Configuration Manager versione 1902, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze di Cloud Management Gateway. Le distribuzioni esistenti continuano a funzionare normalmente.<!-- 3605704 -->

In Configuration Manager versione 1810 e precedenti la procedura guidata di Cloud Management Gateway offre ancora l'opzione per una **distribuzione classica del servizio** tramite un certificato di gestione di Azure. Per semplificare la distribuzione e la gestione delle risorse, è consigliabile usare il modello di distribuzione Azure Resource Manager per tutte le nuove istanze di Cloud Management Gateway. Se possibile, ridistribuire le istanze di Cloud Management Gateway esistenti tramite Resource Manager. Per altre informazioni, vedere [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificare un gateway di gestione cloud).

> [!Important]  
> A partire dalla versione 1810, la distribuzione classica del servizio in Azure è deprecata in Configuration Manager. Si tratta dell'ultima versione che supporta la creazione di queste distribuzioni di Azure. Questa funzionalità verrà rimossa in una versione futura di Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Progettazione della gerarchia

Creare il gateway di gestione client nel sito di livello superiore della gerarchia. Se si tratta di un sito di amministrazione centrale, creare punti di connessione del gateway di gestione cloud nei siti primari figlio. Il componente di gestione del servizio cloud è sul punto di connessione del servizio, che si trova nel sito di amministrazione centrale. Questa progettazione consente di condividere il servizio tra diversi siti primari, se necessario.

È possibile creare più servizi Cloud Management Gateway (CMG) in Azure ed è possibile creare più punti di connessione del gateway di gestione cloud. Più punti di connessione del gateway di gestione cloud offrono un bilanciamento del carico del traffico client dal gateway di gestione cloud ai ruoli locali. Per ridurre la latenza di rete, assegnare il gateway di gestione cloud associato alla stessa area geografica del sito primario.

A partire dalla versione 1902 è possibile associare un Cloud Management Gateway a un gruppo di limiti. Questa configurazione consente ai client di usare Cloud Management Gateway per impostazione predefinita o come fallback per le comunicazioni client in base alle [relazioni del gruppo di limiti](/sccm/core/servers/deploy/configure/boundary-groups). Questo comportamento è particolarmente utile in scenari con succursali e VPN. È possibile indirizzare il traffico client da collegamenti WAN lenti e dispendiosi per usare invece servizi più veloci in Microsoft Azure.<!--3640932-->

> [!Note]  
> I client basati su Internet non rientrano in alcun gruppo di limiti.
>
> In Configuration Manager versione 1810 e precedenti Cloud Management Gateway non rientra in alcun gruppo di limiti.

Anche altri fattori, ad esempio il numero di client da gestire, influiscono sulla progettazione del gateway di gestione cloud. Per altre informazioni, vedere [Prestazioni e scalabilità](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Esempio 1: sito primario autonomo

Contoso ha un sito primario autonomo in un data center locale nella sede di New York City.

- Viene creato un gateway di gestione cloud nell'area di Azure degli Stati Uniti orientali per ridurre la latenza di rete.
- Vengono creati due punti di connessione del gateway di gestione cloud, entrambi collegati all'unico servizio Cloud Management Gateway.  

Quando effettuano il roaming in Internet, i client comunicano con il gateway di gestione cloud nell'area di Azure degli Stati Uniti orientali. Il gateway di gestione cloud inoltra le comunicazioni tramite entrambi i punti di connessione del gateway di gestione cloud.

#### <a name="example-2-hierarchy"></a>Esempio 2: gerarchia

Fourth Coffee ha un sito di amministrazione centrale in un data center locale nella sede di Seattle. Un sito primario è nel data center, mentre l'altro sito primario è nella sede centrale europea di Parigi.

- Nel sito di amministrazione centrale viene creato un servizio CMG (Cloud Management Gateway) nell'area di Azure degli Stati Uniti occidentali. Il numero di macchine virtuali viene ridimensionato per il carico di client roaming previsto nell'intera gerarchia.
- Nel sito primario di Seattle viene creato un punto di connessione di CMG collegato al singolo gateway CMG.
- Nel sito primario di Parigi viene creato un punto di connessione di CMG collegato al singolo gateway CMG.

Quando effettuano il roaming in Internet, i client comunicano con CMG nell'area di Azure degli Stati Uniti occidentali. CMG trasmette questa comunicazione al punto di connessione di CMG nel sito primario assegnato del client.

> [!TIP]
> Non è necessario distribuire più istanze di CMG ai fini della georilevazione. Il client Configuration Manager non è in genere influenzato dalla latenza minima che si verifica con il servizio cloud, anche se geograficamente distante.

## <a name="requirements"></a>Requisiti

- Una **sottoscrizione di Azure** per l'hosting del gateway di gestione cloud.  

- Un **amministratore di Azure** deve partecipare alla creazione iniziale di alcuni componenti, a seconda della progettazione. Questo utente tipo non necessita di autorizzazioni in Configuration Manager.  
    - Per distribuire Cloud Management Gateway è necessario un **amministratore della sottoscrizione**
    - Per integrare il sito con Azure AD per distribuire Cloud Management Gateway tramite Azure Resource Manager è necessario un **amministratore globale**

- Almeno un server Windows locale per l'hosting del **punto di connessione del gateway di gestione cloud**. È possibile condividere il percorso di questo ruolo con altri ruoli del sistema del sito di Configuration Manager.  

- Il **punto di connessione del servizio** deve essere in [modalità online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- Integrazione con **Azure AD** per distribuire il servizio con Azure Resource Manager. Per altre informazioni, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Un [**certificato di autenticazione server**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth) per il gateway di gestione cloud.  

- Possono essere necessari **altri certificati**, a seconda della versione del sistema operativo del client e del modello di autenticazione. Per altre informazioni, vedere [CMG certificates](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway) (Certificati per il gateway di gestione cloud).  

    A partire dalla versione 1806, quando si usa l'opzione del sito **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**, il punto di gestione può essere HTTP. Per altre informazioni, vedere [HTTP migliorato](/sccm/core/plan-design/hierarchy/enhanced-http).

- In Configuration Manager versione 1810 o precedenti con il metodo di distribuzione classico di Azure è necessario usare un [**certificato di gestione di Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_azuremgmt).  

    > [!TIP]  
    > Usare il modello di distribuzione **Azure Resource Manager**. che non richiede il certificato di gestione.
    >
    > Il metodo di distribuzione classica è deprecato a partire dalla versione 1810.  

- I client devono usare **IPv4**.  


## <a name="specifications"></a>Specifiche

- Tutte le versioni di Windows elencate in [Sistemi operativi supportati per client e dispositivi ](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sono supportate per il gateway di gestione cloud.  

- Il gateway di gestione cloud supporta solo i ruoli del punto di gestione e del punto di aggiornamento software.  

- CMG non supporta i client che comunicano solo con indirizzi IPv6.<!--495606-->  

- I punti di aggiornamento software che usano un bilanciamento del carico di rete non funzionano con il gateway di gestione cloud. <!--505311-->  

- Le distribuzioni del gateway di gestione cloud che usano il modello Azure Resource Manager non abilitano il supporto dei provider di servizi cloud di Azure. La distribuzione del gateway di gestione cloud con Azure Resource Manager continua infatti a usare il servizio cloud classico, non supportato dal provider di servizi cloud. Per altre informazioni, vedere [Available Azure services in Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servizi di Azure disponibili in Azure CSP).  

### <a name="support-for-configuration-manager-features"></a>Supporto delle funzionalità di Configuration Manager

La tabella seguente elenca il supporto di Cloud Management Gateway (CMG) per le funzionalità di Configuration Manager:

|Funzionalità  |Supporto  |
|---------|---------|
| Aggiornamenti software     | ![Supportato](media/green_check.png) |
| Protezione degli endpoint     | ![Supportato](media/green_check.png) |
| Inventario hardware e software     | ![Supportato](media/green_check.png) |
| Stato del client e notifiche     | ![Supportato](media/green_check.png) |
| Esecuzione di script     | ![Supportato](media/green_check.png) |
| Impostazioni di conformità     | ![Supportato](media/green_check.png) |
| Installazione client<br>(con integrazione di Azure AD)     | ![Supportato](media/green_check.png) |
| Distribuzione del software (indirizzata a dispositivi)     | ![Supportato](media/green_check.png) |
| Distribuzione del software (indirizzata a utenti, obbligatoria)<br>(con integrazione di Azure AD)     | ![Supportato](media/green_check.png) |
| Distribuzione del software (indirizzata a utenti, disponibile)<br>([tutti i requisiti](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Supportato](media/green_check.png) |
| Sequenza di attività di aggiornamento sul posto di Windows 10      | ![Supportato](media/green_check.png) |
| Sequenze di attività che non usano le immagini d'avvio e vengono distribuite con un'opzione: **Scaricare tutto il contenuto in locale prima di avviare la sequenza di attività**      | ![Supportato](media/green_check.png) |
| Sequenze di attività che non usano immagini d'avvio  | ![Supportato](media/green_check.png) (1910)|
| CMPivot     | ![Supportato](media/green_check.png)  (1806) |
| Qualsiasi altro scenario di sequenza di attività     | ![Non supportato](media/Red_X.png) |
| Push client     | ![Non supportato](media/Red_X.png) |
| Assegnazione automatica al sito     | ![Non supportato](media/Red_X.png) |
| Richieste di approvazione del software     | ![Non supportato](media/Red_X.png) |
| Console di Configuration Manager     | ![Non supportato](media/Red_X.png) |
| Strumenti remoti     | ![Non supportato](media/Red_X.png) |
| Sito Web di Reporting     | ![Non supportato](media/Red_X.png) |
| Riattivazione LAN     | ![Non supportato](media/Red_X.png) |
| Client Mac, Linux e UNIX     | ![Non supportato](media/Red_X.png) |
| Peer cache     | ![Non supportato](media/Red_X.png) |
| Software MDM locale     | ![Non supportato](media/Red_X.png) |

|Chiave|
|--|
|![Supportato](media/green_check.png) = Questa funzionalità è supportata con Cloud Management Gateway (CMG) da tutte le versioni supportate di Configuration Manager  |
|![Supportato](media/green_check.png) (*AAMM*) = Questa funzionalità è supportata con Cloud Management Gateway (CMG) a partire dalla versione *AAMM* di Configuration Manager  |
|![Non supportato](media/Red_X.png) = Questa funzionalità non è supportata con CMG |


## <a name="cost"></a>Costi

> [!IMPORTANT]  
> Le informazioni sui costi seguenti sono puramente stime. Altre variabili di ambiente possono influire sul costo complessivo dell'uso di Cloud Management Gateway (CMG).

Cloud Management Gateway (CMG) usa i componenti di Azure seguenti, che implicano l'addebito di costi per l'account della sottoscrizione di Azure:

### <a name="virtual-machine"></a>Macchina virtuale

- Cloud Management Gateway (CMG) usa i servizi cloud di Azure come piattaforma distribuita come servizio (PaaS). Questo servizio usa macchine virtuali che comportano costi di calcolo.  

- CMG usa una macchina virtuale standard A2 V2.  

- Selezionare il numero di istanze di macchina virtuale che supportano Cloud Management Gateway (CMG). 1 è il valore predefinito e 16 è il valore massimo. Questo numero viene impostato durante la creazione del gateway di gestione cloud e può essere modificato in un secondo momento per ridimensionare il servizio in base alle esigenze.

- Per altre informazioni sul numero di macchine virtuali necessarie per supportare i client, vedere [Prestazioni e scalabilità](#performance-and-scale).

- Vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/) per determinare i costi potenziali.

    > [!NOTE]  
    > I costi delle macchine virtuali variano a seconda dell'area.

### <a name="outbound-data-transfer"></a>Trasferimento dati in uscita

- Gli addebiti si basano sul flusso di dati in uscita da Azure (dati in uscita o download). I flussi di dati verso Azure sono gratuiti (dati in ingresso o caricamento). I flussi di dati del gateway di gestione cloud in uscita da Azure includono i criteri per il client, le notifiche del client e le risposte del client inoltrate dal gateway di gestione cloud al sito. Queste risposte includono i report di inventario, i messaggi di stato e lo stato di conformità.  

- Anche in assenza di client che comunicano con un gateway di gestione cloud, alcune comunicazioni in background causano traffico di rete tra il gateway di gestione cloud e il sito locale.  

- Visualizzare il valore **Trasferimento di dati in uscita (GB)** nella console di Configuration Manager. Per altre informazioni, vedere [Monitor clients on CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway) (Monitorare i client in Cloud Management Gateway).  

- Vedere i [dettagli sui prezzi per la larghezza di banda di Azure](https://azure.microsoft.com/pricing/details/bandwidth/) per determinare i costi potenziali. I prezzi del trasferimento dei dati sono diversificati. Un maggior utilizzo comporta un costo minore per gigabyte.  

- *Per una stima*, prevedere circa 100-300 MB per client al mese per i client basati su Internet. La stima inferiore è per una configurazione di client predefinito. La stima superiore è per una configurazione di client più aggressiva. L'utilizzo effettivo può variare a seconda della configurazione delle impostazioni del client.  

    > [!NOTE]  
    > L'esecuzione di altre azioni, ad esempio la distribuzione di aggiornamenti software o di applicazioni, aumenta la quantità di dati in uscita da Azure.

- Una configurazione errata dell'opzione Gateway di gestione cloud per **verificare la revoca del certificato client** può causare un traffico aggiuntivo dai client al gateway di gestione cloud. Questo traffico aggiuntivo può aumentare i dati in uscita di Azure e quindi i relativi costi.<!-- SCCMDocs#1434 --> Per altre informazioni, vedere [Pubblicare l'elenco di revoche di certificati (CRL)](https://docs.microsoft.com/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway#bkmk_crl).  

### <a name="content-storage"></a>Archivio del contenuto

- I client basati su Internet ottengono i contenuti degli aggiornamenti del software Microsoft da Windows Update senza alcun costo. Non distribuire i pacchetti di aggiornamento con i contenuti degli aggiornamenti Microsoft a un punto di distribuzione cloud per non incorrere in costi di archiviazione e dati in ingresso.  

- Altri contenuti necessari, ad esempio applicazioni o aggiornamenti software di terze parti, devono essere distribuiti a un punto di distribuzione cloud. Attualmente il gateway di gestione cloud supporta solo il punto di distribuzione cloud per l'invio di contenuti ai client.  

- Per altre informazioni, vedere i costi d'uso dei [punti di distribuzione cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

- A partire dalla versione 1806, un CMG può anche essere un punto di distribuzione cloud per distribuire contenuti ai client. Questa funzionalità riduce i certificati necessari e i costi delle macchine virtuali di Azure. Per altre informazioni, vedere [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificare un gateway di gestione cloud).<!--1358651-->  

- A partire dalla versione 1810 CMG usa l'archiviazione con ridondanza locale di Azure. Per altre informazioni, vedere [Archiviazione con ridondanza locale](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

### <a name="other-costs"></a>Altri costi

- Ogni servizio cloud ha un indirizzo IP dinamico. Ogni gateway di gestione cloud usa un nuovo indirizzo IP dinamico. L'aggiunta di macchine virtuali per il gateway di gestione cloud non aumenta il numero di indirizzi.  


## <a name="performance-and-scale"></a>Prestazioni e scalabilità

Per altre informazioni sulla scalabilità del gateway di gestione cloud, vedere [Numeri di ridimensionamento e scalabilità](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

I suggerimenti seguenti consentono di migliorare le prestazioni del gateway di gestione cloud:

- Se possibile, configurare il gateway di gestione cloud, il punto di connessione del gateway di gestione cloud e il server del sito di Configuration Manager nella stessa area di rete per ridurre la latenza.  

- La connessione tra il client di Configuration Manager e il CMG non è in grado di riconoscere l'area. Le comunicazioni client sono in gran parte non interessate dalla latenza e/o dalla separazione geografica. Non è necessario distribuire più CMG ai fini della prossimità geografica. Distribuire il CMG nel sito di livello superiore nella gerarchia e aggiungere istanze per aumentare la disponibilità.

- Per la disponibilità elevata del servizio, creare un CMG con almeno due istanze di CMG e due punti di connessione CMG per ogni sito.  

- Scalare il gateway di gestione cloud per supportare più client mediante l'aggiunta di più istanze di macchine virtuali. Il bilanciamento del carico di Azure controlla le connessioni client al servizio.  

- Creare altri punti di connessione del gateway di gestione cloud per distribuire il carico tra di essi. Il gateway di gestione cloud distribuisce il traffico ai punti di connessione mediante un approccio 'round robin'.  

- Quando il CMG è sottoposto a un carico elevato con un numero di client maggiore di quello supportato, le richieste continuano a essere gestite ma potrebbero verificarsi ritardi.  

> [!Note]  
> Mentre Configuration Manager non ha limiti hardware per il numero di client per punto di connessione del gateway di gestione cloud, Windows Server ha un intervallo di porte dinamico TCP massimo predefinito di 16.384. Se un sito di Configuration Manager gestisce più di 16.384 client con un unico punto di connessione del gateway di gestione cloud, è necessario aumentare il limite di Windows Server. Tutti i client hanno un canale per le notifiche client che mantiene una porta aperta sul punto di connessione del gateway di gestione cloud. Per altre informazioni su come usare il comando netsh per aumentare questo limite, vedere l'[articolo del supporto tecnico Microsoft 929851](https://support.microsoft.com/help/929851).


## <a name="ports-and-data-flow"></a>Porte e flusso di dati

Non è necessario aprire alcuna porta in ingresso per la rete locale. Il punto di connessione del servizio e il punto di connessione del gateway di gestione cloud avviano tutte le comunicazioni con Azure e il gateway di gestione cloud. Questi due ruoli del sistema del sito devono creare connessioni in uscita per il cloud Microsoft. Il punto di connessione del servizio distribuisce ed esegue il monitoraggio del servizio in Azure e pertanto deve essere in modalità online. Il punto di connessione del gateway di gestione cloud si connette a gateway per gestire le comunicazioni tra il gateway di gestione cloud e i ruoli del sistema del sito locali.

Il diagramma seguente rappresenta un flusso di dati concettuale di base per il gateway di gestione cloud:

![Flusso di dati del CMG](media/cmg-data-flow.png)

1. Il punto di connessione del servizio si connette ad Azure tramite la porta HTTPS 443. Esegue l'autenticazione usando Azure AD o il certificato di gestione di Azure. Il punto di connessione del servizio distribuisce il gateway di gestione cloud in Azure. Il gateway di gestione cloud crea il servizio cloud HTTPS usando il certificato di autenticazione del server.  

2. Il punto di connessione del gateway di gestione cloud si connette al gateway in Azure tramite TCP-TLS o HTTPS. Mantiene la connessione aperta e crea il canale per le future comunicazioni bidirezionali.  

3. Il client si connette al gateway di gestione cloud sulla porta HTTPS 443. Esegue l'autenticazione usando Azure AD o il certificato di autenticazione del client.  

4. Il gateway di gestione cloud inoltra la comunicazione client tramite la connessione esistente al punto di connessione del gateway di gestione cloud locale. Non è necessario aprire alcuna porta del firewall in entrata.  

5. Il punto di connessione del gateway di gestione cloud inoltra la comunicazione client al punto di gestione locale e al punto di aggiornamento software.  

Per altre informazioni sull'hosting di contenuti in Azure, vedere [Usare un punto di distribuzione basato sul cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).

### <a name="required-ports"></a>Porte richieste

La tabella seguente elenca le porte e i protocolli di rete richiesti. Il *client* è il dispositivo che avvia la connessione e richiede una porta in uscita. Il *server* è il dispositivo che accetta la connessione e richiede una porta in ingresso.

| Client  | Protocollo | Porta  | Server  | Descrizione  |
|---------|---------|---------|---------|---------|
| punto di connessione del servizio     | HTTPS | 443        | Azure        | Distribuzione del gateway di gestione cloud |
| Punto di connessione del gateway di gestione cloud     |  TCP-TLS | 10140-10155        | Servizio Cloud Management Gateway        | Protocollo preferito per la creazione del canale del gateway di gestione cloud<sup>1</sup> |
| Punto di connessione del gateway di gestione cloud     | HTTPS | 443        | Servizio Cloud Management Gateway       | Protocollo di fallback per la creazione del canale del gateway di gestione cloud in una sola istanza di macchina virtuale<sup>2</sup> |
| Punto di connessione del gateway di gestione cloud     |  HTTPS   | 10124-10139     | Servizio Cloud Management Gateway       | Protocollo di fallback per la creazione del canale del gateway di gestione cloud in due o più istanze di macchina virtuale<sup>3</sup> |
| Client     |  HTTPS | 443         | Gateway di gestione cloud        | Comunicazione client generale |
| Punto di connessione del gateway di gestione cloud      | HTTPS o HTTP | 443 o 80         | Punto di gestione<br>(versione 1710) | Traffico locale, la porta dipende dalla configurazione del punto di gestione |
| Punto di connessione del gateway di gestione cloud      | HTTPS | 443      | Punto di gestione<br>(versione 1802) | Il traffico locale deve essere HTTPS |
| Punto di connessione del gateway di gestione cloud      | HTTPS o HTTP | 443 o 80         | Punto di aggiornamento software | Traffico locale, la porta dipende dalla configurazione del punto di aggiornamento software |

<sup>1</sup> Il punto di connessione del gateway di gestione cloud tenta innanzitutto di stabilire una connessione TCP-TLS di lunga durata con ogni istanza di macchina virtuale del gateway di gestione cloud. Si connette alla prima istanza di macchina virtuale sulla porta 10140. La seconda istanza di macchina virtuale usa la porta 10141, fino alla sedicesima sulla porta 10155. Una connessione TCP-TLS offre le prestazioni migliori, ma non supporta proxy Internet. Se il punto di connessione del gateway di gestione cloud non può connettersi tramite TCP-TLS, torna a HTTPS<sup>2</sup>.  

<sup>2</sup> Se il punto di connessione del gateway di gestione cloud non può connettersi a gateway tramite TCP-TLS<sup>1</sup>, si connette al bilanciamento del carico di rete di Azure su HTTPS 443 per una sola istanza di macchina virtuale.  

<sup>3</sup> Se sono presenti due o più istanze di macchina virtuale, il punto di connessione del gateway di gestione cloud usa HTTPS 10124 per la prima istanza di macchina virtuale, non HTTPS 443. Si connette alla seconda istanza di macchina virtuale su HTTPS 10125, fino alla sedicesima sulla porta HTTPS 10139.

### <a name="internet-access-requirements"></a>Requisiti per l'accesso a Internet

Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire al punto di connessione del Cloud Management Gateway e al punto di connessione del servizio di accedere agli endpoint Internet.

Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints#bkmk_cloud).


## <a name="next-steps"></a>Passaggi successivi

- [Certificati per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sicurezza e privacy per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Numeri di ridimensionamento e scalabilità del gateway di gestione cloud](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Domande frequenti sul gateway di gestione cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
