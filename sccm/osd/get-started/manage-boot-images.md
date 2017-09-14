---
title: Gestire le immagini d'avvio - Configuration Manager | Microsoft Docs
description: In Configuration Manager viene illustrato come gestire le immagini d'avvio Windows PE usate durante la distribuzione di un sistema operativo.
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
caps.latest.revision: "23"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5668ba3ead3b7415508f9ecf02f2e119c3cd9cc6
ms.sourcegitcommit: 2a1328da3facb20b0c78f3b12adbb5fdbe0dcc11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2017
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gestire le immagini d'avvio con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'immagine d'avvio in Configuration Manager è un'immagine [Windows PE (WinPE)](https://msdn.microsoft.com/library/windows/hardware/dn938389%28v=vs.85%29.aspx) usata durante la distribuzione di un sistema operativo. Le immagini d'avvio vengono usate per avviare un computer in Windows PE, un sistema operativo minimo con componenti e servizi limitati che prepara il computer di destinazione per l'installazione di Windows.  Usare le sezioni seguenti per gestire le immagini d'avvio.

## <a name="BKMK_BootImageDefault"></a> Immagini d'avvio predefinite
Configuration Manager offre due immagini d'avvio predefinite: una per il supporto delle piattaforme x86 e una per il supporto delle piattaforme x64. Queste immagini sono archiviate nel percorso: \\\\*nomeserver*>\SMS_<*codicesito*>\osd\boot\\<*x64*> or <*i386*>. Le immagini di avvio predefinite vengono aggiornate o rigenerate in base all'azione eseguita.

Per le azioni descritte nelle sezioni seguenti, tenere presente quanto segue:
- Gli oggetti del driver di origine devono essere validi e inclusi i file di origine del driver, altrimenti i driver non verranno aggiunti alle immagini di avvio nel sito.
- Le immagini di avvio che non sono basate sulle immagini di avvio predefinite, anche se usano la stessa versione di Windows PE, non verranno modificate.
- È necessario ridistribuire le immagini di avvio modificate ai punti di distribuzione.
- È necessario ricreare tutti i supporti che usano le immagini di avvio modificate.
- Se si preferisce non aggiornare automaticamente le immagini di avvio personalizzate/predefinite, non archiviarle nella posizione predefinita.

> [!NOTE]
> Lo strumento del registro di traccia di Configuration Manager viene aggiunto a tutte le immagini di avvio inserite nella **Raccolta software**. In Windows PE è possibile avviare lo strumento del registro di traccia di Configuration Manager digitando **CMTrace** al prompt dei comandi.  

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Usare gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager
A partire dalla versione 1702, quando si aggiorna la versione di Windows ADK e quindi si usano gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager, Configuration Manager rigenera le immagini di avvio predefinite. Ciò include la nuova versione di Windows PE dalla versione aggiornata di Windows ADK, la nuova versione del client di Configuration Manager, i driver, le personalizzazioni e così via. Le immagini di avvio personalizzate non vengono modificate.

Prima della versione 1702, Configuration Manager aggiorna l'immagine di avvio (boot.wim) esistente con i componenti client, i driver, le personalizzazioni e così via, ma non usa la versione più recente di Windows PE da Windows ADK. È necessario modificare manualmente l'immagine di avvio per usare la nuova versione di Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Eseguire l'aggiornamento da Configuration Manager 2012 a Configuration Manager Current Branch (CB)
Quando si esegue l'aggiornamento da Configuration Manager 2012 a Configuration Manager CB tramite il processo di installazione, Configuration Manager rigenera le immagini di avvio predefinite. Ciò include la nuova versione di Windows PE dalla versione aggiornata di Windows ADK, la nuova versione del client di Configuration Manager e tutte le personalizzazioni rimangono invariate. Le immagini di avvio personalizzate non vengono modificate.

### <a name="update-distribution-points-with-the-boot-image"></a>Aggiornare i punti di distribuzione con l'immagine d'avvio
Quando si usa l'azione **Aggiorna punti di distribuzione** dal nodo **Immagini d'avvio** nella console di Configuration Manager, Configuration Manager aggiorna le immagini d'avvio predefinite con i componenti client, i driver, le personalizzazioni e così via.    

A partire dal Configuration Manager versione 1706, è possibile scegliere di ricaricare nell'immagine d'avvio la versione più recente di Windows PE (dalla directory di installazione di Windows ADK). La pagina **Generale** dell'Aggiornamento guidato punti di distribuzione offre informazioni sulla versione di Windows ADK installata nel server del sito, sulla versione di Windows ADK dalla quale è stato usato Windows PE nell'immagine d'avvio e sulla versione del client di Configuration Manager. È possibile usare queste informazioni per decidere se ricaricare l'immagine d'avvio. Inoltre la nuova colonna **Versione client** aggiunta alla visualizzazione delle immagini d'avvio nel nodo **Immagini d'avvio** visualizza la versione del client di Configuration Manager usata da ogni immagine d'avvio.    


##  <a name="BKMK_BootImageCustom"></a> Personalizzare un'immagine d'avvio  
 È possibile personalizzare o [modificare un'immagine d'avvio](#BKMK_ModifyBootImages) dalla console di Configuration Manager basata su una versione di Windows PE dalla versione supportata di Windows ADK. Quando un sito viene aggiornato con una nuova versione e viene installata una nuova versione di Windows ADK, le immagini di avvio personalizzate (non nel percorso dell'immagine di avvio predefinita) non vengono aggiornate con la nuova versione di Windows ADK. In questo caso, non sarà possibile personalizzare le immagini d'avvio nella console di Configuration Manager. Tuttavia, continueranno a funzionare come prima dell'aggiornamento.  

 Quando un'immagine di avvio si basa su una versione differente di Windows ADK installata in un sito, è necessario personalizzare le immagini di avvio usando un altro metodo, ad esempio lo strumento della riga di comando Gestione e manutenzione immagini distribuzione, che fa parte di Windows AIK e Windows ADK. Per altre informazioni, vedere [Customize boot images](customize-boot-images.md) (Personalizzare le immagini d'avvio).  

##  <a name="BKMK_AddBootImages"></a> Aggiungere un'immagine d'avvio  

 Durante l'installazione del sito, Configuration Manager aggiunge automaticamente immagini d'avvio basate su una versione di WinPE dalla versione supportata di Windows ADK. A seconda della versione di Configuration Manager, è possibile aggiungere immagini d'avvio basate su una diversa versione di WinPE dalla versione supportata di Windows ADK.  Quando si prova ad aggiungere un'immagine d'avvio che contiene una versione non supportata di WinPE, si verifica un errore.  

 Di seguito sono riportate la versione supportata di Windows ADK, la versione Windows PE su cui si basa l'immagine d'avvio che può essere personalizzata dalla console di Configuration Manager e le versioni Windows PE su cui è basata l'immagine d'avvio che è possibile personalizzare usando DISM e aggiungere a Configuration Manager.  

-   **Versione di Windows ADK**  

     Windows ADK per Windows 10  

-   **Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager**  

     Windows PE 10  

-   **Versioni di Windows PE supportate per le immagini d'avvio non personalizzabili dalla console di Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> È possibile aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE 3.1. Installare il supplemento Windows AIK per Windows 7 SP1 per aggiornare Windows AIK per Windows 7 (basato su Windows PE 3) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). È possibile scaricare il supplemento Windows AIK per Windows 7 SP1 dall' [Area download Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Ad esempio, se si ha Configuration Manager, è possibile personalizzare le immagini d'avvio da Windows ADK per Windows 10 (basato su Windows PE 10) dalla console di Configuration Manager. Tuttavia, anche se le immagini di avvio basate su Windows PE 5 sono supportate, è necessario personalizzarle da un computer diverso e usare la versione di Gestione e manutenzione immagini distribuzione installata con Windows AIK per Windows 8. È quindi possibile aggiungere l'immagine d'avvio alla console di Configuration Manager. Per altre informazioni sui passaggi per personalizzare un'immagine d'avvio (aggiungere componenti e driver facoltativi), abilitare il supporto comandi nell'immagine d'avvio, aggiungere l'immagine d'avvio alla console di Configuration Manager e aggiornare i punti di distribuzione con l'immagine d'avvio, vedere [Customize boot images](customize-boot-images.md) (Personalizzare le immagini d'avvio).

 Usare la procedura seguente per aggiungere manualmente un'immagine d'avvio.  

#### <a name="to-add-a-boot-image"></a>Per aggiungere un'immagine di avvio  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi immagine di avvio** per avviare l'Aggiunta guidata immagine d'avvio.  

4.  Nella pagina **Origine dati** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

    -   Nella casella **Percorso** specificare il percorso del file WIM dell'immagine di avvio.  

         Il percorso specificato deve essere un percorso di rete valido in formato UNC. Ad esempio: \\\\<*nomeserver*\\<*nomecondivisione*>\\<*nomeimmagineavvio*>.wim.  

    -   Selezionare l'immagine di avvio dall'elenco a discesa **Immagine di avvio** . Se il file WIM contiene più immagini di avvio, selezionare l'immagine appropriata.  

5.  Nella pagina **Generale**  specificare le opzioni seguenti e quindi fare clic su **Avanti**.  

    -   Nella casella **Nome** specificare un nome univoco per l'immagine di avvio.  

    -   Nella casella **Versione** specificare un numero di versione per l'immagine di avvio.  

    -   Nella casella **Commento** specificare una breve descrizione di come viene usata l'immagine di avvio.  

6.  Completare la procedura guidata.  

 L'immagine d'avvio appare ora elencata nel nodo **Immagine d'avvio** della console di Configuration Manager. Tuttavia, prima di poter utilizzare l'immagine di avvio per distribuire un sistema operativo, è necessario distribuire tale immagine ai punti di distribuzione, ai gruppi di punti di distribuzione o alle raccolte associate ai gruppi di punti di distribuzione.  

> [!NOTE]  
>  Quando si seleziona il nodo **Immagine d'avvio** nella console di Configuration Manager, la colonna **Dimensione (KB)** visualizza la dimensione decompressa per ogni immagine d'avvio. Tuttavia, quando Configuration Manager invia un'immagine d'avvio in rete, invia una copia compressa dell'immagine che è generalmente molto più piccola della dimensione elencata nella colonna **Dimensione (KB)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuire immagini d'avvio in un punto di distribuzione  
 Le immagini di avvio vengono distribuite nei punti di distribuzione nello stesso modo in cui vengono distribuiti gli altri contenuti. Nella maggior parte dei casi, è necessario distribuire l'immagine d'avvio almeno in un punto di distribuzione prima di distribuire il sistema operativo e prima di creare supporti.  

> [!NOTE]  
>  Per usare PXE per la distribuzione di un sistema operativo, prima di distribuire l'immagine d'avvio tenere presente quanto segue:  
>   
>  -   Il punto di distribuzione deve essere configurato per accettare le richieste PXE.  
> -   È necessario distribuire sia un'immagine d'avvio abilitata per PXE x86, sia una abilitata per PXE x64, in almeno un punto di distribuzione che supporta PXE.  
> -   Configuration Manager distribuisce l'immagine d'avvio nella cartella **RemoteInstall** del punto di distribuzione abilitato per PXE.  
>   
>  Per altre informazioni sull'uso di PXE per la distribuzione di sistemi operativi, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Per la procedura di distribuzione di un'immagine d'avvio, vedere [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modificare un'immagine d'avvio  
 È possibile aggiungere o rimuovere driver di dispositivo dall'immagine o modificare le proprietà associate all'immagine d'avvio. Ad esempio, è possibile aggiungere o rimuovere driver per scheda di rete o per dispositivi di archiviazione di massa. Quando si modificano le immagini di avvio, tenere presente quanto segue:  

-   Per poter aggiungere driver di dispositivo all'immagine d'avvio, è necessario prima importarli e abilitarli nel catalogo dei driver di dispositivo.  

-   Quando si modifica un'immagine d'avvio, l'immagine non modifica i pacchetti associati a cui fa riferimento.  

-   Dopo aver apportato delle modifiche a un'immagine d'avvio, è necessario **aggiornarla** nei punti di distribuzione che già la contengono, in modo che sia disponibile la versione più recente dell'immagine. Per ulteriori informazioni, vedere [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Usare la procedura seguente per modificare un'immagine d'avvio.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Per modificare le proprietà di un'immagine di avvio  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

3.  Selezionare l'immagine di avvio da modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà** per l'immagine di avvio.  

5.  Impostare le seguenti impostazioni per modificare il comportamento dell'immagine di avvio:  

    -   Nella scheda **Immagini** , se sono state modificate le proprietà dell'immagine di avvio utilizzando uno strumento esterno, fare clic su **Ricarica**.  

    -   Nella scheda **Driver** aggiungere i driver di dispositivo di Windows necessari per avviare WinPE. Quando si aggiungono i driver di dispositivo, è necessario valutare quanto segue:  

        -   Selezionare **Nascondi driver che non corrispondono all'architettura dell'immagine d'avvio** per visualizzare solo i driver relativi all'architettura dell'immagine d'avvio. L'architettura è basata su quella riportata nel file con estensione inf fornito dal produttore.  

        -   Selezionare **Nascondi driver non inclusi in una classe di archiviazione o di rete (per immagini d'avvio)** per visualizzare solo i driver di archiviazione e di rete e per nascondere gli altri driver in genere non necessari per le immagini di avvio, ad esempio, i driver video o quelli del modem.  

        -   Selezionare **Nascondi driver senza firma digitale** per nascondere i driver privi di firma digitale.  

        -   Come procedura consigliata, aggiungere solo i driver di archiviazione di massa e per la scheda di rete (NIC) alle immagini di avvio a meno che non vengano richiesti altri driver per WinPE.  

        -   Poiché WinPE include già molti driver, aggiungere solo i driver di archiviazione di massa e per la scheda di rete (NIC) non forniti da WinPE.  

        -   Assicurarsi che i driver aggiunti all'immagine d'avvio corrispondano all'architettura dell'immagine d'avvio.  

        > [!NOTE]  
        >  È necessario importare i driver di dispositivo nel catalogo driver prima di aggiungerli a un'immagine di avvio. Per informazioni su come importare i driver di dispositivo, vedere [Gestire i driver](manage-drivers.md).  

    -   Nella scheda **Personalizzazione** selezionare una delle seguenti impostazioni:  

        -   Selezionare la casella di controllo **Attiva comando di preavvio** per specificare un comando da eseguire prima della sequenza attività. Quando si attivano i comandi di preavvio, è possibile specificare la riga di comando da eseguire, se sono richiesti file di supporto per eseguire il comando e il percorso di origine di tali file di supporto.  

            > [!WARNING]  
            >  È necessario aggiungere **cmd /c** all'inizio della riga di comando. Se non si specifica **cmd /c**, il comando non verrà chiuso al termine dell'esecuzione. La distribuzione continua ad attendere la fine del comando e non avvierà altri comandi o azioni configurati.  

            > [!TIP]  
            >  Durante la creazione del supporto per sequenza di attività, la sequenza di attività scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore di eventuali variabili della sequenza di attività, nel file di log CreateTSMedia.log nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

        -   Configurare l'impostazione **Sfondo Windows PE** per specificare se si vuole usare lo sfondo Windows PE predefinito o uno sfondo personalizzato.  

        -   Selezionare **Abilita supporto comandi (solo test)** per aprire un prompt dei comandi usando il tasto **F8** mentre l'immagine d'avvio viene distribuita. Questa operazione è utile per la risoluzione di problemi durante la verifica della distribuzione. Non è consigliabile utilizzare questa impostazione in un ambiente di produzione.  

        -   Configurare l'area scratch di Windows PE, ovvero l'archivio temporaneo (unità RAM) usato da WinPE. Ad esempio, quando un'applicazione viene eseguita in WinPE e richiede la scrittura di file temporanei, WinPE reindirizza tali file all'area scratch in memoria per simulare la presenza di un disco rigido. Per impostazione predefinita, WinPE alloca 32 megabyte (MB) di memoria scrivibile.  

    -   Nella scheda **Origine dati** aggiornare le seguenti impostazioni:  

        -   Impostare **Percorso immagine** e **Indice immagini** per modificare il file di origine dell'immagine d'avvio.  

        -   Selezionare **Aggiorna i punti di distribuzione in base alla pianificazione** per creare una pianificazione per l'aggiornamento dell'immagine d'avvio.  

        -   Selezionare **Mantieni contenuto nella cache del client** se non si vuole che il contenuto del pacchetto venga eliminato dalla cache client per liberare spazio per altro contenuto.  

        -   Selezionare **Abilita replica differenziale binaria** per specificare che solo i file modificati vengono distribuiti quando il pacchetto dell'immagine d'avvio viene aggiornato nel punto di distribuzione. Questa impostazione riduce al minimo il traffico di rete tra siti, soprattutto quando il pacchetto di immagini di avvio è di grandi dimensioni e le modifiche sono relativamente piccole.  

        -   Selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE** se l'immagine d'avvio viene usata in una distribuzione che supporta PXE.  

            > [!NOTE]  
            >  Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Nella scheda **Accesso dati** selezionare una delle seguenti impostazioni:  

        -   Selezionare **Impostazioni condivisione pacchetto** se si desidera che i client installino il contenuto in questo pacchetto dalla rete.  

        -   In **Impostazioni aggiornamento pacchetto** specificare in che modo si vuole che Configuration Manager disconnetta gli utenti dal punto di distribuzione. È possibile che Configuration Manager non sia in grado di aggiornare l'immagine d'avvio quando gli utenti sono connessi al punto di distribuzione.  

    -   Nella scheda **Impostazioni distribuzione** selezionare una delle seguenti impostazioni:  

        -   Nell'elenco **Priorità di distribuzione** specificare il livello di priorità utilizzato da Configuration Manager durante la distribuzione di più pacchetti nello stesso punto di distribuzione.  

        -   Selezionare **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti** per attivare la distribuzione del contenuto su richiesta nei punti di distribuzione preferiti. Quando questa impostazione è attivata, il punto di gestione distribuisce il contenuto in tutti i punti di distribuzione preferiti quando un client richiede il contenuto per il pacchetto e tale contenuto non è disponibile in nessuno dei punti di distribuzione preferiti.  

        -   Selezionare **Impostazioni punto di distribuzione pre-installazione** per specificare la modalità di distribuzione dell'immagine di avvio nei punti di distribuzione abilitati per il contenuto pre-installato.  

            > [!NOTE]  
            >  Per altre informazioni sui contenuti in versione di preproduzione, vedere [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   Nella scheda **Percorsi contenuto** selezionare il punto di distribuzione o il gruppo di punti di distribuzione ed eseguire le seguenti azioni:  

        -   Fare clic su **Ridistribuisci** per distribuire nuovamente l'immagine di avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

        -   Fare clic su **Convalida** per verificare l'integrità del pacchetto di immagini di avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

    -   Nella scheda **Componenti facoltativi** specificare i componenti aggiunti a Windows PE per l'utilizzo con Configuration Manager. Per altre informazioni sui componenti facoltativi disponibili, vedere [WinPE: aggiungere pacchetti (informazioni di riferimento sui componenti facoltativi)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx).  

    -   Nella scheda **Protezione** selezionare un utente amministratore e modificare le operazioni che può eseguire.  

6.  Dopo aver configurato le proprietà, fare clic su **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configurare un'immagine d'avvio per eseguire la distribuzione da un punto di distribuzione che supporta PXE  
 Prima di usare un'immagine d'avvio per una distribuzione del sistema operativo PXE, è necessario configurare l'immagine d'avvio per la distribuzione da un punto di distribuzione che supporta PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Per configurare un'immagine d'avvio per eseguire la distribuzione da un punto di distribuzione che supporta PXE  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

3.  Selezionare l'immagine di avvio da modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà** per l'immagine di avvio.  

5.  Nella scheda **Origine dati** selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE**.  

    > [!NOTE]  
    >  Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Dopo aver configurato le proprietà, fare clic su **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Configurare più lingue per la distribuzione di immagini d'avvio  
 Le immagini di avvio sono indipendenti dalla lingua. Questo consente di usare un'unica immagine d'avvio che mostra il testo della sequenza di attività in più lingue, in WinPE, a condizione che si includa il supporto lingua appropriato dai componenti facoltativi di Windows PE e si imposti la variabile della sequenza di attività appropriata per indicare quale lingua può essere visualizzata. La lingua del sistema operativo distribuito non dipende dalla lingua visualizzata in WinPE, indipendentemente dalla versione di Configuration Manager. La lingua visualizzata all'utente viene determinata come segue:  

-   Quando un utente esegue la sequenza di attività da un sistema operativo esistente, Configuration Manager usa automaticamente la lingua configurata per l'utente. Quando la sequenza di attività viene eseguita automaticamente a causa della scadenza di una distribuzione obbligatoria, Configuration Manager usa la lingua del sistema operativo.  

-   Per le distribuzioni di sistemi operativi avviate da PXE o da supporto, è possibile impostare il valore di ID lingua nella variabile SMSTSLanguageFolder come parte di un comando di preavvio. Quando il computer si avvia in Windows PE, i messaggi vengono visualizzati nella lingua specificata nella variabile. Se si verifica un errore durante l'accesso al file di risorse di lingua nella cartella specificata o non si imposta la variabile, i messaggi vengono visualizzati nella lingua di WinPE.  

    > [!NOTE]  
    >  Quando il supporto è protetto da una password, il testo di richiesta di immissione della password viene sempre visualizzato nella lingua di WinPE.  

 Usare la procedura seguente per impostare la lingua di WinPE per distribuzioni del sistema operativo avviate da PXE o da supporto.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Per impostare la lingua di Windows PE per una distribuzione del sistema operativo avviata da PXE o da supporto  

1.  Prima di aggiornare l'immagine d'avvio, verificare che il file di risorse della sequenza attività appropriato (tsres.dll) sia contenuto nella cartella di lingua corrispondente. Ad esempio, il file di risorse inglese si trova nel percorso seguente: <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Come parte del comando di preavvio, impostare la variabile di ambiente SMSTSLanguageFolder sull'ID lingua appropriato. L'ID lingua deve essere specificato usando valori decimali e non esadecimali. Per impostare l'ID lingua su Inglese, è ad esempio necessario specificare il valore decimale 1033 in luogo del valore esadecimale 00000409 utilizzato per il nome della cartella.  
