---
title: Anteprima dell'analisi dell'esperienza utente
titleSuffix: Configuration Manager
description: Istruzioni per l'anteprima dell'analisi dell'esperienza utente.
ms.date: 03/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 4758a4ef36896c2d4cfa08e261cef48fec2910bb
ms.sourcegitcommit: fa806f4691befecc7f95a3213f709acfa520a132
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78287731"
---
# <a name="bkmk_uea"></a> Anteprima privata dell'analisi dell'esperienza utente

> [!Note]  
> Queste informazioni fanno riferimento a una funzionalità di anteprima che può essere modificata sostanzialmente prima del rilascio della versione commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="user-experience-analytics-overview"></a>Panoramica dell'analisi dell'esperienza utente

Non è insolito per gli utenti finali riscontrare tempi di avvio lunghi o interruzioni di altro tipo. Le interruzioni possono essere dovute a una combinazione dei seguenti fattori:

- Hardware legacy
- Configurazioni software non ottimizzate per l'esperienza dell'utente finale
- Problemi causati da aggiornamenti e modifiche della configurazione

Questi problemi e altri problemi relativi all'esperienza dell'utente finale persistono perché l'IT non ha molta visibilità nell'esperienza dell'utente finale. In genere, l'unica visibilità su questi problemi proviene da un canale di supporto lento e costoso che in genere non offre informazioni chiare su ciò che deve essere ottimizzato. Non è solo il supporto IT a sopportare il peso di questi problemi. Anche il tempo che gli information worker dedicano alla gestione dei problemi è costoso. Le prestazioni, l'affidabilità e i problemi di supporto che riducono la produttività degli utenti possono avere un impatto notevole anche sul bilancio di un'azienda.

L'**analisi dell'esperienza utente** mira a migliorare la produttività dell'utente e a ridurre i costi del supporto IT mettendo a disposizione informazioni approfondite sull'esperienza utente. Tali informazioni consentono al reparto IT di ottimizzare l'esperienza utente con il supporto proattivo e di rilevare eventuali regressioni valutando l'impatto delle modifiche apportate alla configurazione sull'esperienza utente.

Questa versione iniziale si concentra su tre elementi:

- [**Software consigliato**](#bkmk_uea_rs): Suggerimenti per offrire la migliore esperienza utente
- [**Script di correzione proattiva**](#bkmk_uea_prs): Risolvere i problemi di supporto comuni prima che gli utenti finali li riscontrino
- [**Prestazioni di avvio**](#bkmk_uea_bp): Consentire all'IT di guidare rapidamente gli utenti dall'accensione alla produttività, senza lunghi ritardi nelle procedure di avvio e accesso

Questa versione è solo l'inizio. Verranno implementate rapidamente nuove informazioni per le altre esperienze utente principali subito dopo la versione iniziale.

## <a name="bkmk_uea_prereq"></a> Guida introduttiva

Per iniziare a usare l'analisi dell'esperienza utente, verificare i prerequisiti e quindi iniziare a raccogliere i dati. 

### <a name="technical-prerequisites"></a>Prerequisiti tecnici

La versione di anteprima corrente richiede:
- Dispositivi registrati in Intune che eseguono Windows 10
- Le informazioni dettagliate sulle prestazioni di avvio sono disponibili solo per i dispositivi che eseguono la versione 1903 o successiva di Windows 10.
- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per altre informazioni, vedere [Endpoint](#bkmk_uea_endpoints).
- Il [ruolo di amministratore del servizio Intune](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) è necessario per [iniziare a raccogliere i dati](#bkmk_uea_start).
   - Facendo clic su **Avvia**, l'utente accetta e conferma che i dati dei clienti possono essere archiviati al di fuori del percorso selezionato durante il provisioning del tenant di Microsoft Intune.
   - Dopo aver fatto clic su **Avvia** per la raccolta dei dati, altri ruoli di sola lettura possono visualizzare i dati.

I dispositivi Configuration Manager e i dispositivi registrati in Intune con versioni precedenti di Windows 10 non sono attualmente supportati per questa anteprima.

### <a name="licensing-prerequisites"></a>Prerequisiti per le licenze

L'analisi dell'esperienza utente è inclusa nei piani seguenti: 

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) o superiore
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) o superiore. 

Per le correzioni proattive, gli utenti del dispositivo devono avere una delle licenze seguenti:
- Windows 10 Enterprise E3 o E5 (incluso in Microsoft 365 F1, E3 o E5)
- Windows 10 Education A3 o A5 (incluso in Microsoft 365 A3 o A5)
- Accesso a Desktop virtuale Windows E3 o E5

### <a name="bkmk_uea_start"></a> Iniziare a raccogliere i dati

1. Passare a `https://devicemanagement.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`
1. Fare clic su **Avvia**. Verrà assegnato automaticamente un profilo di configurazione per raccogliere i dati sulle prestazioni di avvio da tutti i dispositivi idonei. È possibile [modificare i dispositivi assegnati](#bkmk_uea_profile) in un secondo momento. Il popolamento dei dati sulle prestazioni di avvio nei dispositivi registrati in Intune dopo il riavvio può richiedere fino a 24 ore.

## <a name="overview-page"></a>Pagina di panoramica

Quando i dati sono pronti, si noteranno alcune informazioni nella pagina di **panoramica**, illustrata più in dettaglio di seguito:

- Il **punteggio dell'esperienza utente** è una media ponderata 50/50 del **software consigliato** e dei **punteggi delle prestazioni di avvio**. Il set di punteggi parziali verrà ampliato nel tempo.

- È possibile confrontare il punteggio corrente con altri punteggi impostando una linea di base.
  - Come descritto nella sezione relativa alla [linea di base](#bkmk_uea_baselines), esiste una linea di base predefinita per *Mediana commerciale* per vedere come si esegue il confronto con un'azienda tipica. È possibile creare nuove linee di base facendo riferimento alle metriche correnti, in modo da tenere traccia dello stato di avanzamento o visualizzare le regressioni nel tempo.
   - Gli indicatori della linea di base sono visualizzati per il punteggio complessivo e i punteggi parziali. Se uno dei punteggi regredisce oltre la soglia configurabile rispetto alla linea di base selezionata, il punteggio viene visualizzato in rosso e il punteggio di primo livello viene contrassegnato come elemento che richiede attenzione.
  - Lo stato **dati insufficienti** significa che non si ha a disposizione un numero sufficiente di dispositivi per ottenere un punteggio significativo. Attualmente sono necessari almeno cinque dispositivi.

- I **filtri** consentiranno di visualizzare il punteggio in un sottogruppo di dispositivi o utenti. Tuttavia, la funzionalità di filtro non è abilitata in questa versione di anteprima.

- Per migliorare il punteggio, consultare l'elenco di **informazioni dettagliate e raccomandazioni**, ordinate in base alla priorità. L'elenco è filtrato in base al contesto del sottonodo quando si passa a **Procedure consigliate** o **Software consigliato**.

[![Pagina di panoramica di Analisi dell'esperienza utente](media/uea-overview-page.png)](media/uea-overview-page.png#lightbox)

## <a name="bkmk_uea_rs"></a> Software consigliato

Alcuni software sono noti per migliorare l'esperienza dell'utente finale, indipendentemente dalle metriche di integrità di livello inferiore. Windows 10, ad esempio, ha un punteggio Net Promoter molto più elevato rispetto a Windows 7. Il punteggio di **adozione del software** è un numero compreso tra 0 e 100 che rappresenta una media ponderata della percentuale di dispositivi in cui sono stati distribuiti diversi software consigliati. La ponderazione corrente è superiore per Windows rispetto alle altre metriche poiché gli utenti interagiscono con essi più di frequente. Le metriche sono descritte di seguito: 

[![Pagina Software consigliato di Analisi dell'esperienza utente](media/uea-recommended-software.png)](media/uea-recommended-software.png#lightbox)

### <a name="bkmk_uea_win10"></a> Windows 10

Windows 10 offre un'esperienza utente migliore rispetto alle versioni precedenti di Windows. Per altre informazioni, vedere il [white paper TEI](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf).

Questa metrica misura la percentuale di dispositivi in Windows 10 rispetto a una versione precedente di Windows.

L'azione di correzione consigliata per il passaggio dei dispositivi dalle versioni precedenti di Windows è creare un piano di distribuzione usando [Desktop Analytics](/sccm/desktop-analytics/overview).

### <a name="bkmk_uea_ap"></a> Autopilot

Microsoft Autopilot offre un'esperienza di provisioning iniziale dei PC Windows 10 più semplice rispetto all'esperienza nativa; presenta infatti un numero di schermate inferiore nella configurazione guidata e fornisce le impostazioni predefinite per assicurarsi che venga correttamente eseguito il provisioning dei dispositivi dei dipendenti sia dalla factory che in fase di reimpostazione.

Questa metrica misura la percentuale di dispositivi Windows 10 registrati per Autopilot.

L'azione di correzione consigliata è registrare i dispositivi esistenti in Autopilot usando [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="bkmk_uea_aad"></a> Azure Active Directory

Azure Active Directory (Azure AD) offre agli utenti numerosi vantaggi di produttività, tra cui l'accesso Single Sign-On a livello di dispositivo per app e servizi, l'accesso a Windows Hello, il ripristino self-service della chiave BitLocker e il roaming dei dati aziendali.

Questa metrica misura la percentuale di dispositivi registrati in Azure AD.

I dispositivi gestiti in Microsoft Intune sono già registrati in Azure AD. L'azione di correzione consigliata per i dispositivi gestiti da Configuration Manager è [registrarli in Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) o [co-gestirli](/sccm/comanage/overview). La co-gestione dei dispositivi migliora anche il punteggio della gestione cloud.

### <a name="bkmk_uea_intune"></a> Gestione cloud

Microsoft Intune offre agli utenti diversi vantaggi per la produttività, tra cui l'abilitazione dell'accesso alle risorse aziendali anche quando si trovano fuori dalla rete aziendale, oltre ad eliminare la necessità di usare Criteri di gruppo, evitando così un sovraccarico di prestazioni e garantendo una migliore esperienza dell'utente finale. Questa metrica misura la percentuale di PC registrati in Microsoft Intune. Informazioni su come [Microsoft sta abilitando questa funzionalità per i propri dipendenti](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

L'azione di correzione consigliata per i dispositivi gestiti da Configuration Manager non ancora registrati in Intune è [co-gestirli](/sccm/comanage/overview).

### <a name="bkmk_uea_np"></a> Nessuna mediana commerciale

La linea di base predefinita **Mediana commerciale** attualmente non ha metriche per i punteggi parziali indicati nelle sezioni precedenti.

## <a name="bkmk_uea_bp"></a> Prestazioni di avvio

> [!NOTE]
> I dati necessari per calcolare il punteggio di avvio per un dispositivo vengono generati in fase di avvio. A seconda delle impostazioni di risparmio energia e del comportamento dell'utente, potrebbero trascorrere settimane dopo l'assegnazione corretta dei criteri a un dispositivo prima che venga visualizzato il punteggio di avvio nella console di amministrazione.  

Il punteggio delle prestazioni di avvio consente all'IT di guidare rapidamente gli utenti dall'accensione alla produttività, senza lunghi ritardi nelle procedure di avvio e accesso. Il **punteggio di avvio** è un numero compreso tra 0 e 100. Questo punteggio è una media ponderata del **punteggio di avvio** e del punteggio di **accesso**, che vengono calcolati come segue:

- **Punteggio di avvio**: Basato sul tempo che trascorre tra l'accensione e l'accesso. Si prende in considerazione l'ultimo tempo di avvio di ogni dispositivo, esclusa la fase di aggiornamento, quindi si assegna un punteggio tra 0 (scarso) e 100 (eccezionale). Su questi punteggi viene calcolata una media per ottenere un punteggio complessivo dell'avvio del tenant.
- **Punteggio di accesso**: Basato sul tempo che trascorre dal momento in cui vengono immesse le credenziali al momento in cui l'utente può accedere al desktop. Si prende in considerazione l'ultimo tempo di accesso per ogni dispositivo, esclusi i primi accessi o gli accessi eseguiti subito dopo l'aggiornamento di una funzionalità, quindi si assegna un punteggio compreso tra 0 (scarso) e 100 (eccezionale). Su questi punteggi viene calcolata una media per ottenere un punteggio complessivo dell'avvio del tenant.

[![Pagina Prestazioni di avvio di Analisi dell'esperienza utente](media/uea-startup-performance.png)](media/uea-startup-performance.png#lightbox)

La pagina **Prestazioni di avvio** contiene anche un elenco di **informazioni dettagliate e raccomandazioni**, ordinate in base alla priorità, descritte nelle sezioni seguenti:

### <a name="bkmk_uea_hdd"></a> Unità disco rigido

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi in cui l'unità di avvio è un disco rigido. Le unità disco rigido per l'avvio in genere richiedono tempi da tre a quattro volte più lunghi rispetto alle unità SSD. È anche previsto un miglioramento delle prestazioni di avvio se si passa alle unità SSD.

Fare clic per visualizzare l'elenco dei dispositivi con unità disco rigido. L'azione consigliata è aggiornare questi dispositivi alle unità SSD.

### <a name="bkmk_uea_gp"></a> Criteri di gruppo

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi che presentano ritardi nell'avvio e nell'accesso a causa di Criteri di gruppo. Fare clic per visualizzare i dispositivi. La visualizzazione è ordinata in base al tempo di Criteri di gruppo, quindi è possibile vedere quali sono i dispositivi interessati per ulteriori procedure di risoluzione dei problemi.

Se si fa clic su un dispositivo specifico, è possibile visualizzarne la cronologia degli avvii e degli accessi. La cronologia consente di determinare se il problema è una regressione e quando potrebbe essersi verificato.

Sebbene esistano molti articoli su come ottimizzare le prestazioni di Criteri di gruppo, è possibile scegliere di eseguire la migrazione alla gestione cloud. La migrazione alla gestione cloud consente di usare le [linee di base di sicurezza di Intune](https://docs.microsoft.com/intune/protect/security-baselines) e lo strumento di analisi dei criteri presto disponibile.

### <a name="bkmk_uea_sb"></a> Tempi di avvio e accesso lenti

Le prestazioni di avvio offrono informazioni dettagliate sul numero di dispositivi con tempi di avvio o accesso lenti. Un punteggio di avvio o di accesso pari a "0" significa lento. Fare clic per visualizzare i dispositivi. I dispositivi sono ordinati rispettivamente in base al tempo di avvio core o al tempo di accesso di base, quindi è possibile visualizzare i dispositivi interessati per ulteriori procedure di risoluzione dei problemi.

Se si fa clic su un dispositivo specifico, è possibile visualizzarne la cronologia degli avvii e degli accessi. La cronologia consente di determinare se il problema era una regressione e quando potrebbe essersi verificato.

### <a name="more-startup-performance-insights-are-on-the-way"></a>Altre informazioni dettagliate sulle prestazioni di avvio saranno presto disponibili

Microsoft sta lavorando ad altre informazioni dettagliate sulle prestazioni di avvio, che saranno disponibili nelle future versioni di anteprima.

## <a name="bkmk_uea_prs"></a> Correzioni proattive

Le correzioni proattive sono pacchetti di script che consentono di rilevare e risolvere problemi di supporto comuni in un dispositivo prima che l'utente si renda conto che si è verificato un problema. Queste correzioni consentono di ridurre le chiamate al supporto tecnico. È possibile creare un pacchetto di script personalizzato o distribuire uno degli script scritti e usati nell'ambiente per ridurre i ticket di supporto.

Ogni pacchetto di script è costituito da uno script di rilevamento, uno script di correzione e metadati. Con Intune sarà possibile distribuire questi pacchetti di script e visualizzare i report sulla loro efficacia. Microsoft sta sviluppando attivamente nuovi script e invita gli utenti a condividere le proprie esperienze. Rivolgersi al proprio contatto per l'anteprima dell'analisi dell'esperienza utente per condividere commenti e suggerimenti sui pacchetti di script.

### <a name="bkmk_uea_prs_ps1"></a> Ricevere gli script di rilevamento e correzione

1. Copiare gli script riportati in fondo a questo articolo nella sezione [Script di PowerShell](#bkmk_uea_ps_scripts).
    - I file di script i cui nomi iniziano con `det` sono script di rilevamento. Gli script di correzione iniziano con `rem`.
    - Per informazioni sui singoli script, vedere [Descrizioni degli script](#bkmk_uea_scripts).
1. Salvare ogni script usando il nome specificato. Il nome è anche indicato nei commenti all'inizio di ogni script.
    - È possibile usare un altro nome di script, ma non corrisponderà al nome indicato nella sezione [Descrizioni degli script](#bkmk_uea_scripts).


### <a name="bkmk_uea_prs_deploy"></a> Distribuzione e monitoraggio di script
Il servizio **Microsoft Intune Management Extension** ottiene gli script da Intune e li esegue. Gli script vengono rieseguiti ogni 24 ore. Per distribuire e monitorare gli script, seguire questa procedura:

1. Passare al nodo **Correzioni proattive** nella console.
1. Fare clic sul pulsante **Crea** per creare un pacchetto di script.
     [![Pagina Correzioni proattive di Analisi dell'esperienza utente. Selezionare il collegamento Crea.](media/uea-proactive-remediations-create.png)](media/uea-proactive-remediations-create.png#lightbox)
1. Nel passaggio delle **nozioni di base** assegnare al pacchetto di script un **nome** e, facoltativamente, una **descrizione**. Il campo del **server di pubblicazione** può essere modificato, ma per impostazione predefinita contiene il nome del tenant. Non è possibile modificare la **versione**. 
1. Nel passaggio delle **impostazioni** copiare il testo dagli script scaricati nei campi **Script di rilevamento** e **Script di monitoraggio e aggiornamento**. 
   - È necessario che lo script di rilevamento e lo script di correzione corrispondenti siano nello stesso pacchetto. Ad esempio, lo script di rilevamento `DetGPLastUpd.ps1` corrisponde allo script di correzione `RemGPLastUpd.ps11`.
       [![Pagina delle impostazioni dello script per Correzioni proattive di Analisi dell'esperienza utente.](media/uea-proactive-remediations-script-settings.png)](media/uea-proactive-remediations-script-settings.png#lightbox)
1. Completare le opzioni nella pagina **Impostazioni** con le seguenti configurazioni consigliate:
   - **Esegui lo script con le credenziali dell'utente connesso**: Configurazione che dipende dallo script. Per altre informazioni, vedere la sezione [Descrizioni degli script](#bkmk_uea_scripts).
   - **Imponi il controllo della firma degli script**: No
   - **Esegui lo script in PowerShell a 64 bit**: No
1. Fare clic su **Avanti** quindi assegnare i **tag di ambito** necessari.
1. Nel passaggio delle **assegnazioni** selezionare i gruppi di dispositivi in cui verrà distribuito il pacchetto di script.
1. Completare il passaggio di **verifica e creazione** per la distribuzione.
1. In **Reporting** > **Analisi dell'esperienza utente - Correzioni proattive** è possibile visualizzare una panoramica dello stato del rilevamento e delle correzioni.
       [![Report in Correzioni proattive di Analisi dell'esperienza utente, pagina di panoramica.](media/uea-proactive-remediations-report-overview.png)](media/uea-proactive-remediations-report-overview.png#lightbox)
1. Fare clic su **Stato dispositivo** per ottenere i dettagli sullo stato per ogni dispositivo della distribuzione.
       [![Stato dispositivo in Correzioni proattive di Analisi dell'esperienza utente.](media/uea-proactive-remediations-device-status.png)](media/uea-proactive-remediations-device-status.png#lightbox)


## <a name="bkmk_uea_set"></a> Impostazioni dell'analisi dell'esperienza utente

Dalla pagina delle impostazioni è possibile selezionare **Generale** o **Linea di base**. Di seguito sono descritte entrambe le impostazioni.

### <a name="bkmk_uea_gen"></a> Generale

La pagina **Generale** in **Impostazioni** consente di verificare se è stata abilitata la raccolta dei dati sulle prestazioni di avvio di Intune. Per impostazione predefinita, viene abilitata automaticamente per tutti i dispositivi quando si fa clic su **Avvia** per abilitare l'analisi dell'esperienza utente. È possibile scegliere di passare al nodo Criteri di raccolta dati di Intune per modificare il set di dispositivi per cui vengono raccolti i record di avvio e di accesso.


#### <a name="bkmk_uea_profile"></a> Criteri di raccolta dati di Intune

Per assegnare questa impostazione a un subset di dispositivi, [creare un profilo](/intune/configuration/device-profile-create#create-the-profile) con le informazioni seguenti: 

  - **Nome**: immettere un nome descrittivo per il profilo, ad esempio **Criteri di raccolta dati di Intune**
   
  - **Descrizione**: Immettere una descrizione del profilo. Questa impostazione è facoltativa ma consigliata.
    
  - **Piattaforma**: selezionare **Windows 10 e versioni successive**
   
  - **Tipo di profilo**: selezionare **Monitoraggio dello stato di Windows**
   
  - Configurare le **impostazioni**:
   
    - **Monitoraggio dello stato di integrità**: selezionare **Abilita** per raccogliere informazioni sugli eventi dai dispositivi Windows 10
    
    - **Ambito**: Selezionare **Prestazioni di avvio** 

  - Usare i [tag di ambito](/intune/configuration/device-profile-create#scope-tags) e le [regole di applicabilità](/intune/configuration/device-profile-create#applicability-rules) per filtrare il profilo in base a gruppi IT o dispositivi specifici in un gruppo che soddisfano criteri specifici.

> [!NOTE]
> È disponibile un segnaposto per le istruzioni per la configurazione del connettore dati di Configuration Manager. Questa funzionalità, tuttavia, non è stata implementata in questa anteprima privata iniziale.

  [![Pagina delle impostazioni generali di Analisi dell'esperienza utente](media/uea-settings-general.png)](media/uea-settings-general.png#lightbox)

### <a name="bkmk_uea_baselines"></a> Gestione della linea di base

È possibile confrontare i punteggi totali e parziali correnti con altri punteggi impostando una linea di base.

1. È disponibile una linea di base predefinita per **Mediana commerciale**, che consente di confrontare i punteggi con un'azienda tipo.
1. È possibile creare nuove linee di base facendo riferimento alle metriche correnti per tenere traccia dello stato di avanzamento o visualizzare le regressioni nel tempo. Fare clic sul pulsante **Crea nuovo** e assegnare un nome alla nuova linea di base. Si consiglia di usare un nome che includa la data, poiché è più semplice effettuare una selezione dall'elenco a discesa nelle pagine dei report.
1. È previsto un limite di 100 linee di base per ogni tenant. È possibile eliminare le linee di base obsolete che non sono più necessarie.
1. Le metriche correnti verranno contrassegnate in rosso e visualizzate come regressione se scendono sotto la linea di base corrente nei report. Poiché è perfettamente normale una variazione delle metriche da un giorno all'altro, è possibile impostare una soglia di regressione, che per impostazione predefinita è 10%. Con questa soglia, le metriche vengono contrassegnate come regressione solo se la regressione è superiore al 10%.

   [![Pagina delle impostazioni della linea di base di Analisi dell'esperienza utente](media/uea-settings-baseline.png)](media/uea-settings-baseline.png#lightbox)

## <a name="bkmk_uea_tshoot"></a> Risoluzione dei problemi

Per registrare i dispositivi per l'analisi dell'esperienza utente, è necessario inviare i dati funzionali richiesti a Microsoft. Se l'ambiente usa un server proxy, usare queste informazioni per configurare il proxy.

### <a name="bkmk_uea_endpoints"></a> Endpoint

Per abilitare la condivisione dei dati funzionali, configurare il server proxy in modo che consenta gli endpoint seguenti:

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft (associazione del certificato) durante la comunicazione con gli endpoint di condivisione dei dati funzionali richiesti. L'intercettazione e l'ispezione SSL non sono possibili. Per usare la funzionalità Analisi dell'esperienza utente, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Usato per inviare i [dati funzionali richiesti](#bkmk_uea_datacollection) all'endpoint di raccolta dati di Intune. |
| `https://graph.windows.net` | Usato per recuperare automaticamente le impostazioni quando si connette la gerarchia all'analisi dell'esperienza utente (per il ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare la raccolta di dispositivi e i dispositivi con l'analisi dell'esperienza utente (solo per il ruolo del server di Configuration Manager). Per altre informazioni, vedere [Configurare il proxy per un server del sistema del sito](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Verificare che un proxy non blocchi i dati a causa dell'autenticazione. Se l'organizzazione usa l'autenticazione del server proxy per il traffico in uscita, usare uno o più degli approcci seguenti:

#### <a name="bypass-recommended"></a>Ignorare (scelta consigliata)

Configurare i server proxy in modo che non richiedano l'autenticazione proxy per il traffico verso gli endpoint di condivisione dei dati. Questa opzione è la soluzione più completa. Può essere usata per tutte le versioni di Windows 10.  

#### <a name="user-proxy-authentication"></a>Autenticazione proxy dell'utente

Configurare i dispositivi per l'uso del contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede le configurazioni seguenti:

- Dispositivi con aggiornamento qualitativo corrente per Windows 10
- Configurare il proxy a livello di utente (proxy WinINET) in **Impostazioni proxy** nel gruppo Rete e Internet delle Impostazioni di Windows. È anche possibile usare il pannello di controllo Opzioni Internet legacy. 
- Verificare che gli utenti abbiano l'autorizzazione proxy per raggiungere gli endpoint di condivisione dei dati. Poiché questa opzione richiede che i dispositivi abbiano utenti console con autorizzazioni proxy, non è possibile usare questo metodo con dispositivi senza intestazioni.

> [!IMPORTANT]
> L'approccio di autenticazione proxy dell'utente non è compatibile con l'uso di Microsoft Defender Advanced Threat Protection. Questo comportamento è dovuto al fatto che questa autenticazione si basa sulla chiave del Registro di sistema **DisableEnterpriseAuthProxy** impostata su `0`, mentre Microsoft Defender ATP richiede che sia impostata su `1`. Per altre informazioni, vedere [Configurare le impostazioni del proxy del computer e della connettività Internet](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Autenticazione proxy del dispositivo

Questo approccio è il più complesso poiché richiede le configurazioni seguenti:

- Assicurarsi che i dispositivi possano raggiungere il server proxy tramite WinHTTP nel contesto del sistema locale. Usare una delle opzioni seguenti per configurare questo comportamento:
  - `netsh winhttp set proxy` sulla riga di comando
  - Protocollo WPAD (Web Proxy Auto-Discovery)
  - Proxy trasparente
  - Connessione indirizzata o che usa NAT (Network Address Translation)

- Configurare i server proxy per consentire agli account del computer in Active Directory di accedere agli endpoint dei dati di diagnostica. Questa configurazione richiede che i server proxy supportino l'autenticazione integrata di Windows.  

## <a name="bkmk_uea_faq"></a> Domande frequenti

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Perché gli script si chiudono con codice 1?

Gli script si chiudono con codice 1 per segnalare a Intune che è necessaria una correzione. In questo caso, la chiusura di uno script di rilevamento con 1 indica che è vero che è necessaria la correzione. Molti pacchetti di script eseguiti esclusivamente in CM possono risultare conformi, ma si chiudono con codice 1. Per questi script, la chiusura con codice 1 non indica un problema grave, ma è opportuno verificare se la correzione nel dispositivo viene eseguita.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Perché lo script di aggiornamento dei criteri di gruppo non aggiornati restituisce un errore 0x87D00321?

0x87D00321 è un errore di timeout esecuzione dello script. Questo errore si verifica in genere con i computer connessi in remoto. Una possibile mitigazione potrebbe essere effettuare la distribuzione solo in una raccolta dinamica di computer con connettività di rete interna.

## <a name="bkmk_uea_scripts"></a> Descrizioni degli script

In questa tabella sono riportati i nomi degli script, le descrizioni, i rilevamenti, le correzioni e gli elementi configurabili. I file di script i cui nomi iniziano con `det` sono script di rilevamento. Gli script di correzione iniziano con `rem`. Questi script possono essere copiati dalla sezione successiva di questo articolo.

|Nome script|Descrizione|
|---|---|
|**Update stale Group Policies** (Aggiorna criteri di gruppo non aggiornati) </br>`DetGPLastUpd.ps1` </br> `RemGPLastUpd.ps1`| Rileva se l'ultimo aggiornamento dei criteri di gruppo è precedente a `7 days`.  </br>Personalizzare la soglia di 7 giorni modificando il valore per `$numDays` nello script di rilevamento. </br></br>Le correzioni vengono applicate eseguendo `gpupdate /target:computer /force` e `gpupdate /target:user /force`  </br> </br>Può aiutare a ridurre le chiamate al supporto tecnico relative alla connettività di rete quando i certificati e le configurazioni vengono recapitati con Criteri di gruppo. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: Sì|
|**Restart Office Click-to-Run service** (Riavvia il servizio A portata di clic di Office) </br> `DetectClickToRunServiceState.ps1` </br> `RemediateClickToRunServiceState.ps1`| Rileva se il servizio A portata di clic è impostato per l'avvio automatico e se il servizio viene arrestato. </br> </br> Le correzioni vengono applicate impostando il servizio per l'avvio automatico e avviando il servizio se viene arrestato. </br></br> Consente di risolvere i problemi in cui Win32 Office 365 ProPlus non viene avviato perché il servizio A portata di clic viene arrestato. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: No|
|**Check network certificates** (Verifica certificati di rete) </br>`DetExpIssuerCerts.ps1` </br>`RemExpIssuerCerts.ps1`|Rileva i certificati emessi da un'autorità di certificazione scaduti o prossimi alla scadenza nell'archivio personale del computer o dell'utente. </br> Per specificare l'autorità di certificazione, modificare il valore per `$strMatch` nello script di rilevamento. Specificare 0 per `$expiringDays` per trovare i certificati scaduti o specificare un altro numero di giorni per trovare i certificati prossimi alla scadenza.  </br></br>Le correzioni vengono applicate generando una notifica di tipo avviso popup per l'utente. </br> Specificare i valori `$Title` e `$msgText` con il titolo e il testo del messaggio che verrà visualizzato dagli utenti. </br> </br> Notifica agli utenti i certificati scaduti che potrebbero dover essere rinnovati. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: No|
|**Clear stale certificates** (Cancella certificati non aggiornati) </br>`DetExpUserCerts.ps1` </br> `RemExpUserCerts.ps1`| Rileva i certificati scaduti emessi da un'autorità di certificazione nell'archivio personale dell'utente corrente. </br> Per specificare l'autorità di certificazione, modificare il valore per `$certCN` nello script di rilevamento. </br> </br> Per applicare la correzione, rileva nell'archivio personale dell'utente corrente i certificati scaduti emessi da un'autorità di certificazione. </br> Per specificare l'autorità di certificazione, modificare il valore per `$certCN` nello script di correzione. </br> </br> Rileva ed elimina i certificati scaduti emessi da un'autorità di certificazione nell'archivio personale dell'utente corrente. </br> </br> **Esegui lo script con le credenziali dell'utente connesso**: Sì|

## <a name="bkmk_uea_ps_scripts"></a> Script di PowerShell

### <a name="detgplastupdps1"></a>DetGPLastUpd.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     DetGPLastUpd.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern “Last time Group Policy was applied:” | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remgplastupdps1"></a>RemGPLastUpd.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     RemGPLastUpd.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detectclicktorunservicestateps1"></a>DetectClickToRunServiceState.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     DetectClickToRunServiceState.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediateclicktorunservicestateps1"></a>RemediateClickToRunServiceState.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     RemediateClickToRunServiceState.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detexpissuercertsps1"></a>DetExpIssuerCerts.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     DetExpIssuerCerts.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remexpissuercertsps1"></a>RemExpIssuerCerts.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     RemExpIssuerCerts.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detexpusercertsps1"></a>DetExpUserCerts.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     DetExpUserCerts.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remexpusercertsps1"></a>RemExpUserCerts.ps1

```powershell
#=============================================================================================================================
#
# Script Name:     RemExpUserCerts.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="bkmk_uea_privacy"></a> Privacy dei dati nell'analisi dell'esperienza utente

### <a name="data-flow"></a>Flusso di dati

La figura seguente illustra il flusso dei dati funzionali richiesti dai singoli dispositivi attraverso i servizi dati e l'archiviazione temporanea fino al tenant. I dati passano attraverso le pipeline aziendali esistenti senza affidarsi ai dati di diagnostica di Windows.

[![Diagramma del flusso di dati dell'esperienza utente](media/uea-dataflow.png)](media/uea-dataflow.png#lightbox)

1. Configurare i criteri di **raccolta dati di Intune** per i dispositivi registrati. Per impostazione predefinita, questi criteri vengono assegnati a "Tutti i dispositivi" quando si **avvia** l'analisi dell'esperienza utente. Tuttavia, è possibile [modificare l'assegnazione](#bkmk_uea_set) in qualsiasi momento per un subset di dispositivi o nessun dispositivo.

2. I dispositivi inviano i dati funzionali richiesti.

    - Per i dispositivi Intune con i criteri assegnati, i dati vengono inviati dall'estensione di gestione di Intune. Per altre informazioni, vedere [Requisiti](#bkmk_uea_prereq).
    - Per i dispositivi gestiti da Configuration Manager, i dati possono essere propagati a Microsoft Endpoint Management anche attraverso il connettore ConfigMgr. Il connettore ConfigMgr è collegato al cloud. Richiede solo la connessione a un tenant di Intune, non l'attivazione della co-gestione.

> [!Note]  
> I dati necessari per calcolare il punteggio di avvio per un dispositivo vengono generati in fase di avvio. A seconda delle impostazioni di risparmio energia e del comportamento dell'utente, potrebbero trascorrere settimane dopo l'assegnazione corretta dei criteri a un dispositivo prima che venga visualizzato il punteggio di avvio nella console di amministrazione.  

3. Il servizio di gestione degli endpoint Microsoft elabora i dati per ogni dispositivo e pubblica i risultati per i singoli dispositivi e per le aggregazioni organizzative nella console di amministrazione usando le API di MS Graph.

La latenza media end-to-end è di circa 12 ore ed è vincolata dal tempo necessario per l'elaborazione giornaliera. Tutte le altre parti del flusso di dati sono quasi in tempo reale.

### <a name="bkmk_uea_datacollection"></a>Raccolta dati

Attualmente, la funzionalità di base di analisi dell'esperienza utente raccoglie le informazioni associate ai record delle prestazioni di avvio. Con l'aggiunta di altre funzionalità nel tempo, i dati raccolti varieranno in base alle esigenze. I punti dati principali attualmente raccolti:

- **id:** ID dispositivo univoco usato da Windows Update
- **localId:** ID univoco definito localmente per il dispositivo. Questo non è il nome del dispositivo leggibile. Probabilmente uguale al valore archiviato in HKLM\Software\Microsoft\SQMClient\MachineId.
- **aaddeviceid:** ID dispositivo di Azure Active Directory
- **orgId:** GUID univoco che rappresenta il tenant di Microsoft O365
- **authIdEnt**
- **make:** produttore del dispositivo
- **model:** modello del dispositivo
- **deviceClass:** classificazione del dispositivo. Ad esempio, Desktop, Server o Mobile.
- **Country:** impostazione dell'area del dispositivo
- **logOnId**
- **bootId:** ID di avvio del sistema
- **coreBootTimeInMilliseconds:** tempo per l'avvio core
- **totalBootTimeInMilliseconds:** tempo di avvio totale
- **updateTimeInMilliseconds:** tempo per il completamento degli aggiornamenti del sistema operativo
- **gpLogonDurationInMilliseconds**: tempo per l'elaborazione dei Criteri di gruppo
- **desktopShownDurationInMilliseconds:** tempo per il caricamento del desktop (explorer.exe)
- **desktopUsableDurationInMilliseconds:** tempo per rendere utilizzabile il desktop (explorer.exe)
- **name:** Windows
- **ver:** versione del sistema operativo corrente.
- **topProcesses:** elenco dei processi caricati durante l'avvio con il nome, con le statistiche di utilizzo della CPU e i dettagli dell'app (nome, editore, versione). Ad esempio *{\"ProcessName\":\"svchost\",\"CpuUsage\":43,\"ProcessFullPath\":\"C:\\\\Windows\\\\System32\\\\svchost.exe\",\"ProductName\":\"Microsoft® Windows® Operating System\",\"Publisher\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1\"}*

> [!Important]  
> I criteri di gestione dei dati sono descritti nell'[informativa sulla privacy di Microsoft Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). I dati dei clienti vengono usati solo per fornire i servizi per i quali si è iscritti. Come descritto durante il processo di onboarding, i punteggi da tutte le organizzazioni registrate vengono anonimizzati e aggregati per mantenere aggiornate le baseline.


### <a name="resources"></a>Risorse

Per altre informazioni sugli aspetti correlati alla privacy, vedere gli articoli seguenti:

- [Informativa sulla privacy di Windows Intune](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Windows 10 e conformità in materia di privacy](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Sicurezza e privacy nei data center di Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  
- [Fidati del tuo cloud](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centro protezione](https://www.microsoft.com/trustcenter)  
