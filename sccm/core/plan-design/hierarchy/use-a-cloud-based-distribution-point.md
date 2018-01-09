---
title: Punto di distribuzione basato su cloud
titleSuffix: Configuration Manager
description: Informazioni sulle configurazioni e le limitazioni per l'uso di un punto di distribuzione basato sul cloud con System Center Configuration Manager.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: "9"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 87c60ac597baa8726333e317f42924130dd1a685
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Usare un punto di distribuzione basato sul cloud con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un punto di distribuzione basato sul cloud è un punto di distribuzione di System Center Configuration Manager ospitato in Microsoft Azure. Le informazioni seguenti hanno lo scopo di illustrare le configurazioni e le limitazioni relative all'uso di un punto di distribuzione basato sul cloud.

Se dopo aver installato un sito primario si è pronti a installare un punto di distribuzione basato sul cloud, vedere [Installare punti di distribuzione basati sul cloud in Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Pianificare l'uso di un punto di distribuzione basato sul cloud
Quando si usa una distribuzione basata sul cloud:  

-   **Configurare le impostazioni client** per consentire l'accesso al contenuto a utenti e dispositivi.  

-   **Specificare un sito primario per gestire il trasferimento del contenuto** al punto di distribuzione.  

-   **Specificare le soglie** per la quantità di contenuti da archiviare nel punto di distribuzione e la quantità di contenuti di cui i client possono eseguire il trasferimento dal punto di distribuzione.  


In base alle soglie configurate, Configuration Manager può generare degli avvisi per l'utente quando la quantità combinata di contenuto archiviato nel punto di distribuzione si avvicina alla quantità di archiviazione specificata oppure quando i dati trasferiti dai client si avvicinano alle soglie definite.  

I punti di distribuzione basati sul cloud supportano diverse funzionalità, che sono offerte anche dai punti di distribuzione locali:  

-   I punti di distribuzione basati sul cloud sono gestiti singolarmente o come membri di gruppi di punti di distribuzione.  

-   È possibile usare un punto di distribuzione basato sul cloud come percorso di fallback per il contenuto.  

-   Si riceve supporto per client basati su Internet e intranet.  


I punti di distribuzione basati sul cloud offrono i seguenti vantaggi aggiuntivi:  

-   Configuration Manager esegue la crittografia del contenuto destinato a un punto di distribuzione basato sul cloud prima di inviarlo ad Azure.  

-   In Azure è possibile ridimensionare manualmente il servizio cloud per soddisfare le esigenze mutevoli in termini di richieste di contenuto da parte dei client, senza la necessità di installare ed effettuare il provisioning di punti di distribuzione aggiuntivi.  

-   Il punto di distribuzione basato su cloud supporta il download del contenuto da parte dei client configurati per Windows BranchCache.  


Un punto di distribuzione basato su cloud presenta le limitazioni seguenti:  

-  Se non si usa la versione 1610 con l'hotfix KB4010155, non è possibile usare un punto di distribuzione basato su cloud per ospitare i pacchetti di aggiornamento software. Questo problema viene risolto a partire dalla versione 1702 e successive.  

-   Non è possibile usare un punto di distribuzione basato sul cloud per distribuzioni abilitate per PXE o per il multicast.  

-   Ai client non viene offerto un punto di distribuzione basato su cloud come un percorso contenuto per una sequenza di attività che viene distribuita usando l'opzione di distribuzione **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**. Tuttavia, le sequenze di attività distribuite usando l'opzione di distribuzione di **Scarica tutto il contenuto localmente prima di avviare la sequenza di attività** possono usare un punto di distribuzione basato su cloud come un percorso contenuto valido.  

-   Un punto di distribuzione basato su cloud non supporta pacchetti eseguiti dal punto di distribuzione. Tutto il contenuto deve essere scaricato dal client e quindi eseguito in locale.  

-   Un punto di distribuzione basato su cloud non supporta lo streaming di applicazioni usando Application Virtualization o programmi simili.  

-   Un punto di distribuzione basato su cloud non supporta contenuto pre-installazione. La gestione distribuzione del sito primario che gestisce il punto di distribuzione trasferisce tutto il contenuto al punto di distribuzione.  

-   Il punto di distribuzione basato su cloud non può essere configurato come punto di distribuzione pull.  

##  <a name="BKMK_PrereqsCloudDP"></a> Prerequisiti dei punti di distribuzione basati sul cloud  
 Un punto di distribuzione basato su cloud richiede i seguenti prerequisiti per l'uso:  

-   Una sottoscrizione di Azure (vedere [Informazioni sulle sottoscrizioni e sui certificati](#BKMK_CloudDPCerts) in questo argomento).

-   Un certificato di gestione autofirmato o di infrastruttura a chiave pubblica (PKI) per la comunicazione da un server del sito primario di Configuration Manager al servizio cloud in Azure (vedere [Informazioni sulle sottoscrizioni e sui certificati](#BKMK_CloudDPCerts) in questo argomento).

-   Un certificato di servizio (PKI) usato dai client di Configuration Manager per connettersi ai punti di distribuzione basati su cloud e scaricarne il relativo contenuto usando HTTPS.  

-  Perché un dispositivo o un utente possa accedere al contenuto da un punto di distribuzione basato sul cloud, è necessario che l'opzione **Consentire accesso al punto di distribuzione cloud** sia impostata su **Sì** nell'impostazione client per **Servizi cloud** per tale dispositivo o utente. Per impostazione predefinita, questo valore è configurato su **No**.  

-   Un client deve poter risolvere il nome del servizio cloud, che richiede un alias DNS (Domain Name System) e un record CNAME nello spazio dei nomi DNS.  

-   Un client deve essere in grado di accedere a Internet per usare il punto di distribuzione basato su cloud.  

##  <a name="BKMK_CloudDPCost"></a> Costo dell'uso della distribuzione basata sul cloud  
 Quando si usa un punto di distribuzione basato sul cloud, pianificare i costi dell'archiviazione dei dati e dei download per i trasferimenti eseguiti dai client di Configuration Manager.  

 Configuration Manager include opzioni per il controllo dei costi e il monitoraggio dell'accesso ai dati:  

-   È possibile controllare e monitorare la quantità dei contenuti archiviati in un servizio cloud.  

-   È possibile configurare Configuration Manager in modo che avvisi l'utente quando le **soglie** per i download del client raggiungono o superano i limiti mensili.  

-   Inoltre, è possibile usare il peer caching (Windows BranchCache) per ridurre il numero di trasferimenti di dati dai punti di distribuzione basati sul cloud eseguiti dai client. I client di Configuration Manager configurati per BranchCache possono trasferire il contenuto usando i punti di distribuzione basati sul cloud.  


**Opzioni:**  

-   **Impostazioni client per il cloud**: è possibile controllare l'accesso a tutti i punti di distribuzione basati sul cloud in una gerarchia usando **Impostazioni client**.  

     In **Impostazioni client**la categoria **Impostazioni cloud** supporta l'impostazione **Consentire accesso al punto di distribuzione cloud**. Per impostazione predefinita, questa impostazione è impostata su **No**. È possibile abilitare questa impostazione per utenti e dispositivi.  

-   **Soglie per i trasferimenti di dati**: è possibile specificare le soglie per la quantità di dati da archiviare nel punto di distribuzione e per la quantità di dati che i client possono scaricare dal punto di distribuzione.  

     Le soglie per i punti di distribuzione basati sul cloud includono le seguenti caratteristiche:  

    -   **Soglia di avviso di archiviazione**: Una soglia di avviso di archiviazione imposta un limite massimo per la quantità di dati o contenuto da archiviare nel punto di distribuzione basato sul cloud. Configuration Manager può generare un avviso quando lo spazio libero rimanente raggiunge il livello specificato.  

    -   **Soglia di avviso di trasferimento**: Una soglia di avviso di trasferimento consente di monitorare la quantità di contenuto trasferita dal punto di distribuzione ai client per un periodo di 30 giorni. La soglia di avviso di trasferimento monitora il trasferimento dei dati per i 30 giorni precedenti e può generare un avviso e un avviso critico quando i trasferimenti raggiungono i valori definiti dall'utente.  

        > [!IMPORTANT]  
        >  Configuration Manager monitora il trasferimento dei dati, ma non lo interrompe quando viene superata la soglia di avviso di trasferimento specificata.  

 È possibile specificare delle soglie per ogni punto di distribuzione basato sul cloud durante l'installazione del punto di distribuzione oppure è possibile modificare le proprietà di ogni punto di distribuzione basato sul cloud dopo l'installazione.  

-   **Avvisi**: è possibile configurare Configuration Manager in modo che generi avvisi sul trasferimento dei dati da e verso ogni punto di distribuzione basato sul cloud, a seconda delle soglie di trasferimento dei dati specificate. Questi avvisi consentono di monitorare i trasferimenti dei dati e di decidere quando arrestare il servizio cloud, modificare il contenuto archiviato nel punto di distribuzione o modificare i client che possono usare i punti di distribuzione basati sul cloud.  

     In un ciclo orario, il sito primario che monitora il punto di distribuzione basato sul cloud scarica i dati di transazione da Azure e li archivia in CloudDP-&lt;NomeServizio\>.log nel server del sito. Configuration Manager valuta quindi queste informazioni in rapporto alle quote di trasferimento e archiviazione per ogni punto di distribuzione basato sul cloud. Quando il trasferimento dei dati raggiunge o supera il volume specificato per gli avvisi o gli avvisi critici, Configuration Manager genera l'avviso appropriato.  

    > [!WARNING]  
    >  Dato che le informazioni sui trasferimenti dei dati vengono scaricate da Azure ogni ora, l'utilizzo di quei dati potrebbe superare una soglia di avviso o critica prima che Configuration Manager possa accedere ai dati e generare un avviso.  

    > [!NOTE]  
    >  Gli avvisi per un punto di distribuzione basato sul cloud dipendono dalle statistiche di utilizzo di Azure, che possono richiedere fino a 24 ore per diventare disponibili. Per informazioni su Storage Analytics per Azure, incluse informazioni sulla frequenza con cui Azure aggiorna le statistiche di utilizzo, vedere [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) in MSDN Library.  


-   **Arrestare o avviare il servizio cloud su richiesta**: è possibile usare l'opzione per arrestare un servizio cloud in qualsiasi momento per impedire ai client di usare il servizio in modo continuo. Quando si arresta il servizio cloud, viene immediatamente impedito ai client di scaricare contenuto aggiuntivo dal servizio. È inoltre possibile riavviare il servizio cloud per ripristinare l'accesso per i client. È ad esempio possibile arrestare un servizio cloud quando vengono raggiunte le soglie dei dati.  

     Quando si arresta un servizio cloud, tale servizio non elimina il contenuto dal punto di distribuzione e non impedisce al server del sito di trasferire contenuto aggiuntivo nel punto di distribuzione basato sul cloud.  

     Per arrestare un servizio cloud, nella console di Configuration Manager selezionare il punto di distribuzione nel nodo **Punti di distribuzione del cloud** in **Servizi cloud** nell'area di lavoro **Amministrazione** . Scegliere quindi **Arresta servizio** per arrestare il servizio cloud eseguito in Azure.  

##  <a name="BKMK_CloudDPCerts"></a> Informazioni sulle sottoscrizioni e sui certificati per i punti di distribuzione basati sul cloud  
 I punti di distribuzione basati sul cloud richiedono dei certificati per abilitare Configuration Manager per la gestione del servizio cloud che ospita il punto di distribuzione e per l'accesso al contenuto dal punto di distribuzione da parte dei client. Di seguito sono riportate informazioni generali su questi certificati. Per maggiori dettagli, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificati**  

-   **Certificato di gestione per la comunicazione tra il server del sito e il punto di distribuzione**: il certificato di gestione stabilisce relazioni di trust tra l'API di gestione di Azure e Configuration Manager. Questa autenticazione consente a Configuration Manager di chiamare l'API di Azure quando si eseguono attività quali la distribuzione del contenuto o l'avvio e l'arresto del servizio cloud. Azure consente di creare propri certificati di gestione, nella forma di un certificato autofirmato o di certificati rilasciati da un'autorità di certificazione (CA):  

    -   Fornire ad Azure il file con estensione cer del certificato di gestione quando si configura Azure per Configuration Manager. Il file .cer contiene la chiave pubblica per il certificato di gestione. Prima di installare un punto di distribuzione basato sul cloud, è necessario caricare questo certificato in Azure. Questo certificato consente a Configuration Manager di accedere all'API di Azure.  

    -   Trasmettere il file .pfx del certificato di gestione a Configuration Manager quando si installa il punto di distribuzione basato sul cloud. Il file .pfx contiene la chiave privata per il certificato di gestione. Configuration Manager archivia questo certificato nel database del sito. Dal momento che il file .pfx contiene la chiave privata, è necessario immettere la password per importare questo file del certificato nel database di Configuration Manager.  

    Se si crea un certificato autofirmato, è necessario prima di tutto esportare il certificato come file CER e quindi esportarlo nuovamente come file PFX.  

    Facoltativamente, è possibile specificare un file con estensione **publishsettings** versione 1 di Azure SDK 1.7. Per informazioni sui file con estensione publishsettings, vedere la documentazione di Azure.  

    Per altre informazioni, vedere [Come creare un certificato di gestione](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [Come aggiungere un certificato di gestione a una sottoscrizione di Azure](http://go.microsoft.com/fwlink/p/?LinkId=241722) nella sezione dedicata alla piattaforma Azure in MSDN Library.  

-   **Certificato di servizio per la comunicazione tra client e punto di distribuzione**: il certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager stabilisce relazioni di trust tra i client di Configuration Manager e il punto di distribuzione basato sul cloud e protegge i dati che i client scaricano da quest'ultimo usando Secure Socket Layer (SSL) su HTTPS.  

    > [!IMPORTANT]  
    >  Il nome comune nella casella Soggetto certificato del certificato di servizio deve essere univoco nel dominio e non deve corrispondere ad alcun dispositivo appartenente a un dominio.  

   Per un esempio di distribuzione di questo certificato, vedere la sezione **Distribuzione del certificato di servizio per i punti di distribuzione basati sul cloud** nell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Attività di gestione comuni per i punti di distribuzione basati sul cloud  

-   **Comunicazione tra il server del sito e il punto di distribuzione basato sul cloud**: quando si installa un punto di distribuzione basato sul cloud, è necessario assegnare un sito primario per gestire il trasferimento del contenuto al servizio cloud. Ciò equivale a installare il ruolo del sistema del sito del punto di distribuzione in un sito specifico.  

-   **Comunicazione tra il client e il punto di distribuzione basato sul cloud**: quando un dispositivo o un utente di un dispositivo viene configurato con l'impostazione client che consente l'utilizzo di un punto di distribuzione basato sul cloud, il dispositivo può ricevere tale punto di distribuzione come percorso del contenuto valido:  

    -   Il punto di distribuzione basato sul cloud viene considerato come un punto di distribuzione remoto quando un client valuta i percorsi del contenuto disponibili.  

    -   I client nella intranet usano i punti di distribuzione basati su cloud solo come un'opzione di fallback se non sono disponibili punti di distribuzione locali.  

    Anche se si installano punti di distribuzione basati su cloud in specifiche aree di Azure, i client che usano i punti di distribuzione basati sul cloud non sono a conoscenza delle aree di Azure e selezionano in modo non deterministico un punto di distribuzione basato sul cloud.

Ciò significa che se si installano punti di distribuzione basati sul cloud in più aree e un client riceve più punti di distribuzione basati sul cloud come percorsi del contenuto, il client potrebbe non usare un punto di distribuzione basato sul cloud della stessa area di Azure del client.  

I client che usano i punti di distribuzione basati sul cloud usano la sequenza seguente per le richieste di percorso del contenuto:  

1.  Un client configurato per l'utilizzo di punti di distribuzione basati su cloud tenta sempre prima di ottenere il contenuto da un punto di distribuzione preferito.  

2.  In assenza di un punto di distribuzione preferito, il client usa un punto di distribuzione remoto eventualmente disponibile se la distribuzione supporta questa opzione.  

3.  In assenza di un punto di distribuzione preferito o remoto disponibile, il client può cercare di ottenere il contenuto da un punto di distribuzione basato su cloud.  



  Quando un client usa un punto di distribuzione basato su cloud come un percorso del contenuto, si autentica a tale punto di distribuzione usando un token di accesso di Configuration Manager. Se il client considera attendibile il certificato del punto di distribuzione basato su cloud di Configuration Manager, può scaricare il contenuto richiesto.  

-   **Monitorare i punti di distribuzione basati sul cloud**: è possibile monitorare il contenuto distribuito a ciascun punto di distribuzione basato sul cloud e il servizio cloud che ospita il punto di distribuzione.  

    -   **Contenuto**: è possibile monitorare il contenuto distribuito in un punto di distribuzione basato sul cloud nello stesso modo con cui si distribuisce il contenuto nei punti di distribuzione locali.  

    -   **Servizio cloud**: Configuration Manager controlla periodicamente il servizio di Azure e genera un avviso se il servizio non è attivo o se vengono rilevati problemi relativi alla sottoscrizione o al certificato. È anche possibile visualizzare i dettagli sul punto di distribuzione nel nodo **Punti di distribuzione del cloud** in **Servizi cloud** nell'area di lavoro **Amministrazione** della console di Configuration Manager. Da questa posizione è possibile visualizzare informazioni di livello generale sul punto di distribuzione. Si può anche selezionare un punto di distribuzione e quindi modificarne le proprietà.  

    Quando si modificano le proprietà di un punto di distribuzione basato sul cloud, è possibile:  

    -   Adattare le soglie dei dati per l'archiviazione e gli avvisi.  

    -   Gestire il contenuto come per un punto di distribuzione locale.  

    Per ogni punto di distribuzione basato sul cloud, è infine possibile visualizzare, ma non modificare, l'ID sottoscrizione, il nome servizio e altri dettagli correlati specificati durante l'installazione della distribuzione basata su cloud.  

-   **Eseguire backup e ripristino dei punti di distribuzione basati sul cloud**: quando si usa un punto di distribuzione basato sul cloud nella gerarchia, usare le informazioni seguenti per pianificare il backup o il ripristino del punto di distribuzione:  

    -   Quando si usa l'attività di manutenzione predefinita **Backup server sito**, Configuration Manager include automaticamente le configurazione per il punto di distribuzione basato sul cloud.  

    -   È consigliabile eseguire il backup e salvare una copia sia del certificato di gestione che del certificato di servizio in uso con un punto di distribuzione basato sul cloud. Se il sito primario di Configuration Manager che gestisce il punto di distribuzione basato sul cloud viene ripristinato in un computer diverso, è necessario importare nuovamente i certificati prima di continuare a usarli.  

-   **Disinstallare un punto di distribuzione basato sul cloud**: per eseguire la disinstallazione, selezionare il punto di distribuzione nella console di Configuration Manager e quindi scegliere **Elimina**.  

    Quando un punto di distribuzione basato sul cloud viene eliminato da una gerarchia, Configuration Manager rimuove il contenuto dal servizio cloud in Azure.  
