---
title: Trovare le risorse del sito | System Center Configuration Manager
description: Informazioni su come e quando i client di System Center Configuration Manager usano la posizione del servizio per individuare le risorse del sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5d718d0f9b8c6121f3124a8ade7507c61b7313f2
ms.openlocfilehash: cad4ebd3f8fa275d7d2cad9b2b87c32b971c580d


---
# <a name="understand-how-clients-find-site-resources-and-services-for-system-center-configuration-manager"></a>Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I client di System Center Configuration Manager usano un processo denominato **posizione del servizio** per individuare i server del sistema del sito con cui possono comunicare e che offrono i servizi che i client devono usare.   Se si comprende come e quando i client usano la posizione del servizio per trovare le risorse del sito, è possibile configurare i siti in modo da supportare correttamente le operazioni client.   Queste configurazioni possono richiedere l'interazione del sito con configurazioni di rete e di dominio come Servizi di dominio Active Directory e DNS, oppure la configurazione di soluzioni alternative più complesse.  

 Sono ruoli del sistema del sito che forniscono servizi, ad esempio, il server del sistema del sito principale per i client, il punto di gestione e i server del sistema del sito aggiuntivi con cui il client può comunicare, come i punti di distribuzione e i punti di aggiornamento software.  



##  <a name="a-namebkmkfunda-fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Fundamentals of service location  
 Un client valuta il suo percorso di rete corrente, la preferenza del protocollo di comunicazione e il sito assegnato quando usa la posizione del servizio per trovare un punto di gestione con cui può comunicare.  

 **Un client comunica con un punto di gestione per:**  
-   Scaricare informazioni sugli altri punti di gestione per il sito, in modo da creare un elenco di punti di gestione per i cicli futuri di individuazione della posizione del servizio  
-   Caricare i dettagli di configurazione, ad esempio inventario e stato  
-   Scaricare i criteri che impostano le configurazioni nel client e possono informare il client in merito al software che può o deve installare e altre attività correlate.  
-   Richiedere informazioni su altri ruoli del sistema del sito che forniscono servizi il cui uso è stato configurato nel client, ad esempio punti di distribuzione per il software che può installare o un punto di aggiornamento software da cui ottenere gli aggiornamenti.  

**Il client di Configuration Manager esegue una richiesta di posizione del servizio:**  
-   Ogni 25 ore di funzionamento continuativo  
-   Quando il client rileva una modifica della propria posizione o configurazione di rete  
-   Quando il servizio **ccmexec.exe** nel computer, vale a dire il servizio client di base, viene avviato  
-   Quando il client deve trovare un ruolo del sistema del sito che fornisce un servizio necessario  

**Quando si tenta di individuare i server che ospitano i ruoli del sistema del sito**, il client usa la posizione del servizio per individuare un ruolo del sistema del sito che supporta il protocollo del client (HTTP o HTTPS). Per impostazione predefinita, i client usano il metodo più sicuro a loro disposizione:  

-   Per usare HTTPS, è necessario disporre di un'infrastruttura a chiave pubblica (PKI) e installare i certificati PKI sui client e sui server. Per informazioni sull'uso dei certificati, vedere [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager).  

-   Quando si distribuisce un ruolo del sistema del sito che usa Internet Information Services (IIS) e supporta le comunicazioni dai client, è necessario specificare se i client si connettono al sistema del sito tramite HTTP o HTTPS. Se si usa HTTP, è necessario considerare anche le opzioni di firma e crittografia. Per altre informazioni, vedere [Planning for Signing and Encryption](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) (Pianificazione di firma e crittografia) nell'argomento [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md) (Pianificare la sicurezza in System Center Configuration Manager).  

##  <a name="a-namebkmkplanservicelocationa-service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato  
Quando un client viene assegnato per la prima volta a un sito primario, seleziona un punto di gestione predefinito per tale sito. I siti primari supportano più punti di gestione e ogni client identifica in modo indipendente un punto di gestione come proprio punto di gestione predefinito.  Questo punto di gestione predefinito diventa quindi il punto di gestione assegnato di tale client. È anche possibile usare i comandi di installazione client per impostare il punto di gestione assegnato per un client al momento dell'installazione.  

-   I client selezionano un punto di gestione con cui comunicare in base al percorso di rete corrente del client e alle configurazioni del gruppo di limiti. Anche se ha un punto di gestione assegnato, questo potrebbe non essere il punto di gestione usato dal client.  

    > [!NOTE]  
    >  Un client usa sempre il punto di gestione assegnato per i messaggi di registrazione e per alcuni messaggi di criteri, anche quando vengono inviate altre comunicazioni a un punto di gestione proxy o locale.  

-   È possibile usare i punti di gestione preferiti. Un punto di gestione preferito è associato a un gruppo di limiti come server del sistema del sito, analogamente a come i punti di distribuzione o i punti di migrazione stato sono associati a un gruppo di limiti. Se si abilitano i punti di gestione preferiti per la gerarchia, quando un client usa un punto di gestione dal sito assegnato, verrà effettuato un tentativo di usare un punto di gestione preferito prima di altri punti di gestione dal sito assegnato.  

-   È possibile usare anche le informazioni nel blog seguente su TechNet.com per configurare l'affinità del punto di gestione. L'affinità del punto di gestione esegue l'override del comportamento predefinito per i punti di gestione assegnati e consente al client di usare uno o più punti di gestione specifici: [affinità del punto di gestione](http://blogs.technet.com/b/jchalfant/archive/2014/09/22/management-point-affinity-added-in-configmgr-2012-r2-cu3.aspx).  

Ogni volta che un client deve contattare un punto di gestione, controlla un **elenco di punti di gestione**noti archiviato in locale in WMI. Il client crea un elenco di punti di gestione iniziale al momento dell'installazione, quindi aggiorna periodicamente l'elenco con informazioni dettagliate su ogni punto di gestione nella gerarchia.  

Quando non riesce a trovare un punto di gestione valido nel proprio elenco di punti di gestione, il client esegue una ricerca nelle seguenti origini di posizioni del servizio, in ordine, finché non trova un punto di gestione da usare:  

1.  Punto di gestione  
2.  Servizi di dominio Active Directory  
3.  DNS  
4.  WINS  

Dopo avere individuato e contattato un punto di gestione da una di queste origini, il client scarica l'elenco corrente dei punti di gestione disponibili nella gerarchia e aggiorna il proprio elenco locale di punti di gestione. Questo vale per i client appartenenti o non appartenenti a un dominio.  

Ad esempio, quando un client di Configuration Manager che si trova su Internet si connette a un punto di gestione basato su Internet, il punto di gestione invia a tale client un elenco di punti di gestione basati su Internet disponibili nel sito. Analogamente, anche i client appartenenti a un dominio o in gruppi di lavoro ricevono l'elenco dei punti di gestione che possono usare.  
-   A un client non configurato per Internet non vengono forniti punti di gestione solo per Internet.  
-   I client di gruppi di lavoro configurati per Internet comunicano solo con punti di gestione per Internet.  

##  <a name="a-namebkmkmplista-the-mp-list"></a><a name="BKMK_MPList"></a> Elenco dei punti di gestione  
L'elenco dei punti di gestione è l'origine preferita per la posizione del servizio per un client perché si tratta di un elenco dei punti di gestione identificati in precedenza dal client, in ordine di priorità. Questo elenco viene ordinato per client, in base alla relativa posizione di rete al momento dell'aggiornamento dell'elenco, quindi viene archiviato in locale sul client in WMI.  

### <a name="building-the-initial-mp-list"></a>Creazione dell'elenco di punti di gestione iniziale  
Durante l'installazione del client vengono usate le regole seguenti per creare l' **elenco di punti di gestione**iniziale dei client:  

-   L'elenco iniziale include i punti di gestione specificati durante l'installazione del client (quando si usano le opzioni **SMSMP**= o **/MP** ).  
-   Il client esegue una query in Servizi di dominio Active Directory alla ricerca dei punti di gestione pubblicati. Affinché possa essere identificato da Active Directory Domain Services, è necessario che il punto di gestione provenga dal sito assegnato del client e che abbia la stessa versione di prodotto del client.  
-   Se durante l'installazione del client non è stato specificato alcun punto di gestione, e quando lo schema di Active Directory non è esteso, il client ricerca in DNS e WINS i punti di gestione pubblicati.  
-   Durante la creazione dell'elenco iniziale è possibile che alcuni punti di gestione nella gerarchia non siano noti.  

### <a name="organizing-the-management-point-list"></a>Organizzazione dell'elenco di punti di gestione  
I client organizzano il proprio elenco di punti di gestione usando la classificazione seguente:  

-   **Proxy**: un punto di gestione proxy è un punto di gestione in un sito secondario.  
-   **Locale**: qualsiasi punto di gestione associato al percorso di rete corrente del client, come definito dai limiti del sito.  
    -   Quando un client appartiene a più gruppi di limiti, l'elenco dei punti di gestione locali è determinato dall'unione di tutti i limiti che includono il percorso di rete corrente del client.  
    -   In genere, i punti di gestione **locali** sono un sottoinsieme dei punti di gestione **assegnati** , a meno che il client non si trovi in un percorso di rete associato a un altro sito con punti di gestione che servono i relativi gruppi di limiti.   


-   **Assegnato**: qualsiasi punto di gestione che corrisponde a un sistema del sito per il sito assegnato del client.  

     È possibile usare i punti di gestione preferiti. I punti di gestione preferiti sono punti di gestione del sito assegnato del client associati a un gruppo di limiti che il client usa per individuare i server del sistema del sito.  

     I punti di gestione di un sito che non sono associati a un gruppo di limiti o che non sono in un gruppo di limiti associato al percorso di rete corrente del client, non sono considerati preferiti e vengono usati se il client non riesce a identificare un punto di gestione preferito disponibile.  

### <a name="selecting-a-management-point-to-use"></a>Selezione di un punto di gestione da usare  
Per le comunicazioni tipiche, un client tenta di usare un punto di gestione dalle classificazioni nell'ordine seguente, in base al percorso di rete del client:  

1.  Proxy  
2.  Locale  
3.  assegnati  

Tuttavia, il client usa sempre il punto di gestione assegnato per i messaggi di registrazione e per alcuni messaggi di criteri, anche quando vengono inviate altre comunicazioni a un punto di gestione proxy o locale.  

All'interno di ogni classificazione (proxy, locale o assegnato), i client tentano di usare un punto di gestione in base alle preferenze, nell'ordine seguente:  

1.  Idoneo per HTTPS in una foresta trusted o locale (quando il client è configurato per le comunicazioni HTTPS)  
2.  Idoneo per HTTPS non in una foresta trusted o locale (quando il client è configurato per le comunicazioni HTTPS)  
3.  Idoneo per HTTP in una foresta trusted o locale  
4.  Idoneo per HTTP non in una foresta trusted o locale  

Dal set di punti di gestione ordinato in base alle preferenze, i client tentano di usare il primo punto di gestione nell'elenco:  

-   Questo elenco ordinato di punti di gestione è casuale e non può essere ordinato.  
-   L'ordine dell'elenco può cambiare ogni volta che il client aggiorna il proprio elenco di punti di gestione.  

Quando un client non riesce a mettersi in contatto con il primo punto di gestione, tenta ogni punto di gestione successivo nell'elenco, iniziando dai punti di gestione preferiti nella classificazione prima di passare a quelli non preferiti. Se un client non riesce a comunicare con nessun punto di gestione della classificazione, tenterà di contattare un punto di gestione preferito della classificazione successiva e così via fino a quando non individua un punto di gestione da usare.  

Dopo aver stabilito la comunicazione con un punto di gestione, i client continuano a usare lo stesso punto di gestione fino a quando:  

-   Dopo 25 ore il client seleziona casualmente un nuovo punto di gestione da usare.  
-   Il client non è in grado di comunicare con il punto di gestione per 5 tentativi in un periodo di 10 minuti, quindi seleziona un nuovo punto di gestione da usare.  

##  <a name="a-namebkmkada-active-directory"></a><a name="bkmk_ad"></a> Active Directory  
I client appartenenti a un dominio possono usare Servizi di dominio Active Directory per la posizione del servizio. Questa operazione richiede che i siti [pubblichino dati in Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

I client possono usare Servizi di dominio Active Directory per il percorso del servizio quando si verificano tutte le condizioni seguenti:  

-   Lo [schema di Active Directory è stato esteso](https://technet.microsoft.com/library/mt345589.aspx) o è stato esteso per System Center 2012 Configuration Manager.  
-   La [foresta Active Directory è configurata per la pubblicazione](http://technet.microsoft.com/library/hh696542.aspx)e i siti di Configuration Manager sono configurati per la pubblicazione.  
-   Il computer client è membro di un dominio Active Directory ed è in grado di accedere a un server di catalogo globale.  

Se un client non trova un punto di gestione da usare per la posizione del servizio in Servizi di dominio Active Directory, tenta di usare DNS. I client appartenenti a un dominio possono usare Servizi di dominio Active Directory per la posizione del servizio. Questa operazione richiede che i siti [pubblichino dati in Active Directory](http://technet.microsoft.com/library/hh696543.aspx).  

##  <a name="a-namebkmkdnsa-dns"></a><a name="bkmk_dns"></a> DNS  
I client sulla Intranet possono usare DNS per il percorso del servizio. In questo caso è necessario almeno un sito in una gerarchia per pubblicare informazioni sui punti di gestione in DNS.  

È consigliabile usare DNS per la posizione del servizio in presenza di una delle condizioni seguenti:
-   Lo schema di Active Directory Domain Services non viene esteso per supportare Configuration Manager.
-   I client della Intranet si trovano in una foresta che non è abilitata per la pubblicazione in Configuration Manager.  
-   Sono presenti client nei computer del gruppo di lavoro che non sono configurati per la gestione client basata solo su Internet (un client del gruppo di lavoro configurato per Internet comunicherà solo con i punti di gestione per Internet e non userà DNS per la posizione del servizio).  
-   È possibile [configurare i client per individuare i punti di gestione da DNS](http://technet.microsoft.com/library/gg682055).  

Quando un sito pubblica i record di individuazione del servizio per i punti di gestione in DNS:  

-   La pubblicazione è applicabile solo ai punti di gestione che accettano le connessioni client dalla rete Intranet.  
-   La pubblicazione aggiunge un record di risorse di posizione del servizio nella zona DNS del computer del punto di gestione. Deve essere presente una voce host corrispondente in DNS per il computer.  

Per impostazione predefinita, i client aggiunti a un dominio cercano in DNS i record dei punti di gestione provenienti dal dominio locale del client. È possibile configurare una proprietà client che specifica un suffisso di dominio per un dominio in cui le informazioni relative ai punti di gestione vengono pubblicate in DNS.  

Per altre informazioni su come configurare la proprietà client del suffisso DNS, vedere [How to configure client computers to find management points by using DNS publishing in System Center Configuration Manager](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md) (Come configurare i computer client per individuare i punti di gestione tramite la pubblicazione DNS in System Center Configuration Manager).  

Se un client non trova un punto di gestione da usare per la posizione del servizio in DNS, tenta di usare WINS.  

### <a name="publish-management-points-to-dns"></a>Pubblicare punti di gestione in DNS  
Per pubblicare punti di gestione in DNS, devono verificarsi le due condizioni seguenti:  

-   I server DNS supportano i record di risorse di individuazione del servizio usando una versione di BIND corrispondente a 8.1.2.  
-   Gli FQDN Intranet specificati per i punti di gestione in Configuration Manager includono voci host, ad esempio record A, in DNS.  

> [!IMPORTANT]  
>  La pubblicazione DNS in Configuration Manager non supporta uno spazio dei nomi indipendente. Se si dispone di uno spazio dei nomi indipendente, è possibile pubblicare manualmente i punti di gestione in DNS o usare uno degli altri metodi alternativi di individuazione del servizio documentati in questa sezione.  

**Quando i server DNS supportano gli aggiornamenti automatici**, è possibile configurare Configuration Manager per la pubblicazione automatica dei punti di gestione della Intranet in DNS oppure per la pubblicazione manuale di tali record in DNS. Quando i punti di gestione vengono pubblicati in DNS, il nome FQDN Intranet e il numero di porta corrispondenti sono pubblicati nel record di individuazione del servizio (SRV). La pubblicazione DNS in un sito viene configurata nelle proprietà del componente del punto di gestione dei siti. Per altre informazioni, vedere [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md) (Componenti del sito per System Center Configuration Manager).  

**Quando la zona DNS è impostata su "Secure only" (Solo protetti) per gli aggiornamenti dinamici**, solo il primo punto di gestione da pubblicare in DNS è in grado di eseguire correttamente l'operazione con le autorizzazioni predefinite.
- È possibile aggiungere al gruppo DnsAdmins ogni server che ospita un punto di gestione per assicurare che tali punti di gestione dispongano delle autorizzazioni per la modifica dei relativi record.  
- Quando soltanto un punto di gestione è in grado di pubblicare e modificare il proprio record DNS, solo se tale punto di gestione rimane integro i client possono ottenere l'elenco completo dei punti di gestione e quindi individuare quello preferito.


**Quando i server DNS non supportano gli aggiornamenti automatici ma supportano i record di individuazione del servizio**, è possibile pubblicare manualmente i punti di gestione in DNS. A tale scopo, è necessario specificare manualmente il record di risorse di individuazione del servizio (SRV RR) in DNS.  

Configuration Manager supporta RFC 2782 per i record relativi alla posizione del servizio, che hanno il formato seguente: *_Servizio._Proto.Nome TTL Classe SRV Priorità Peso Porta Destinazione*  

Per pubblicare un punto di gestione in Configuration Manager, specificare i valori seguenti:  

-   **_Service**: immettere **_mssms_mp***_&lt;sitecode\>*, dove *&lt;sitecode\>* corrisponde al codice del sito del punto di gestione.  
-   **._Proto**: specificare **._tcp**.  
-   **.Name**: immettere il suffisso DNS del punto di gestione, ad esempio **contoso.com**.  
-   **TTL**: immettere **14400**, che corrisponde a quattro ore.  
-   **Classe**: specificare **IN** (in conformità con RFC 1035).  
-   **Priorità**: questo campo non è usato da Configuration Manager.
-   **Peso**: questo campo non è usato da Configuration Manager.  
-   **Porta**: immettere il numero di porta usato dal punto di gestione, ad esempio **80** per HTTP e **443** per HTTPS.  

    > [!NOTE]  
    >  La porta dei record SRV deve corrispondere alla porta di comunicazione usata dal punto di gestione. Per impostazione predefinita si tratta della porta **80** per le comunicazioni HTTP e **443** per le comunicazioni HTTPS.  

-   **Destinazione**: immettere il nome di dominio completo Intranet specificato per il sistema del sito configurato con il ruolo del sito del punto di gestione.  

Se si usa il DNS di Windows Server, è possibile usare la procedura seguente per immettere questo record DNS per i punti di gestione Intranet. Se si usa un'implementazione differente per DNS, usare le informazioni riportate in questa sezione sui valori dei campi e consultare la documentazione relativa al DNS per adattare questa procedura.  

##### <a name="to-configure-automatic-publishing"></a>Per configurare la pubblicazione automatica:  

1.  Nella console di Configuration Manager espandere **Amministrazione** > **Configurazione del sito** > **Siti**.  

2.  Selezionare il sito e quindi fare clic su **Configura componenti del sito**.  

3.  Selezionare **Punto di gestione**.  

4.  Selezionare i punti di gestione da pubblicare (questa selezione vale per la pubblicazione in Servizi di dominio Active Directory e DNS).  

5.  Selezionare la casella di controllo per la pubblicazione in DNS:  

    -   Questa finestra di dialogo consente di selezionare i punti di gestione da pubblicare e di pubblicare in DNS.  

    -   Questa finestra di dialogo non consente di configurare la pubblicazione in Servizi di dominio Active Directory.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Per pubblicare manualmente i punti di gestione in DNS in Windows Server  

1.  Nella console di Configuration Manager specificare i nomi FQDN Intranet dei sistemi del sito.  

2.  Nella console di gestione DNS selezionare la zona DNS per il computer del punto di gestione.  

3.  Verificare che sia presente un record host (A o AAAA) per il nome FQDN Intranet del sistema del sito. Se il record non esiste, crearlo.  

4.  Usando l'opzione **Altri nuovi record** , fare clic su **Posizione servizio (SRV)** nella finestra di dialogo **Tipo record di risorse** , fare clic su **Crea record**, immettere le informazioni seguenti e infine fare clic su **Chiudi**:  

    -   **Dominio**: se necessario, immettere il suffisso DNS del punto di gestione, ad esempio **contoso.com**.  
    -   **Service**: digitare **_mssms_mp***_&lt;sitecode\>*, dove *&lt;sitecode\>* corrisponde al codice del sito del punto di gestione.  
    -   **Protocollo**: digitare **_tcp**.  
    -   **Priorità**: questo campo non è usato da Configuration Manager.  
    -   **Peso**: questo campo non è usato da Configuration Manager.  
    -   **Porta**: immettere il numero di porta usato dal punto di gestione, ad esempio **80** per HTTP e **443** per HTTPS.  

        > [!NOTE]  
        >  La porta dei record SRV deve corrispondere alla porta di comunicazione usata dal punto di gestione. Per impostazione predefinita si tratta della porta **80** per le comunicazioni HTTP e **443** per le comunicazioni HTTPS.  

    -   **Host che offre il servizio**: immettere il nome di dominio completo Intranet specificato per il sistema del sito configurato con il ruolo del sito del punto di gestione.  

Ripetere questi passaggi per ogni punto di gestione della rete Intranet che si desidera pubblicare in DNS.  

##  <a name="a-namebkmkwinsa-wins"></a><a name="bkmk_wins"></a> WINS  
Quando gli altri meccanismi di individuazione del servizio hanno esito negativo, i client possono trovare un punto di gestione iniziale tramite WINS.  

Per impostazione predefinita, un sito primario pubblica in WINS il primo punto di gestione nel sito configurato per HTTP e il primo punto di gestione configurato per HTTPS.  

Se non si desidera che i client trovino un punto di gestione HTTP in WINS, configurare i client con la proprietà CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.  



<!--HONumber=Nov16_HO1-->


