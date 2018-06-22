---
title: 'Gestire le immagini di avvio '
titleSuffix: Configuration Manager
description: In Configuration Manager viene illustrato come gestire le immagini d'avvio Windows PE usate durante la distribuzione di un sistema operativo.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a2fe20896a781d7c897bd5a827d25a7b70390b7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351514"
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gestire le immagini d'avvio con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'immagine d'avvio in Configuration Manager è un'immagine [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) che viene usata durante la distribuzione di un sistema operativo. Le immagini d'avvio si usano per avviare un computer in WinPE. Questo sistema operativo di base contiene servizi e componenti limitati. Configuration Manager usa WinPE per preparare il computer di destinazione per l'installazione di Windows. Usare le sezioni seguenti per gestire le immagini d'avvio.

## <a name="BKMK_BootImageDefault"></a> Immagini d'avvio predefinite
Configuration Manager offre due immagini d'avvio predefinite: una per il supporto delle piattaforme x86 e una per il supporto delle piattaforme x64. Queste immagini sono archiviate nel percorso: \\\\*nomeserver*>\SMS_<*codicesito*>\osd\boot\\<*x64*> or <*i386*>. Le immagini di avvio predefinite vengono aggiornate o rigenerate in base all'azione eseguita.

Tenere presente i comportamenti seguenti per le azioni descritte per le immagini d'avvio predefinite:
- Gli oggetti driver di origine devono essere validi. Questi oggetti includono i file di origine del driver. Se gli oggetti non sono validi, il sito non aggiunge i driver alle immagini d'avvio.
- Le immagini d'avvio che non sono basate sulle immagini d'avvio predefinite, anche se usano la stessa versione di Windows PE, non vengono modificate.
- Ridistribuire le immagini d'avvio modificate ai punti di distribuzione.
- Ricreare i supporti che usano le immagini d'avvio modificate.
- Se si preferisce non aggiornare automaticamente le immagini di avvio personalizzate/predefinite, non archiviarle nella posizione predefinita.

> [!NOTE]
> Lo strumento di registro traccia di Configuration Manager (CMTrace) viene aggiunto a tutte le immagini d'avvio presenti nella **Raccolta software**. Avviare lo strumento in Windows PE digitando **CMTrace** dal prompt dei comandi. A partire dalla versione 1802, quando si avvia cmtrace.exe in Windows PE non viene più richiesto di scegliere se rendere questo programma lo strumento di visualizzazione predefinito per i file di log.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Usare gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager
A partire dalla versione 1702, quando si aggiorna la versione di Windows Assessment and Deployment Kit (ADK) e quindi si usano gli aggiornamenti e le versioni di manutenzione per installare la versione più recente di Configuration Manager, il sito rigenera le immagini d'avvio predefinite. Questo aggiornamento include la nuova versione di WinPE contenuta nella versione aggiornata di Windows ADK, la nuova versione del client di Configuration Manager, i driver e le personalizzazioni. Il sito non modifica le immagini d'avvio personalizzate.

Nelle versioni precedenti alla 1702, Configuration Manager aggiorna l'immagine d'avvio esistente con i componenti client, i driver e le personalizzazioni, ma non usa la versione di WinPE più recente inclusa in Windows ADK. Modificare manualmente l'immagine d'avvio per usare la nuova versione di Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Eseguire l'aggiornamento da Configuration Manager 2012 a Configuration Manager Current Branch (CB)
Quando si esegue l'aggiornamento da Configuration Manager 2012 a Configuration Manager CB tramite il processo di installazione, il sito rigenera le immagini d'avvio predefinite. Questo aggiornamento include la nuova versione di WinPE contenuta nella versione aggiornata di Windows ADK e la nuova versione del client di Configuration Manager. Tutte le personalizzazioni delle immagini d'avvio rimangono invariate. Il sito non modifica le immagini d'avvio personalizzate.

### <a name="update-distribution-points-with-the-boot-image"></a>Aggiornare i punti di distribuzione con l'immagine d'avvio
Quando si usa l'azione **Aggiorna punti di distribuzione** dal nodo **Immagini d'avvio** nella console, il sito aggiorna le immagini d'avvio di destinazione con i componenti client, i driver e le personalizzazioni.    

A partire dalla versione 1706 di Configuration Manager, ricaricare nell'immagine d'avvio la versione più recente di WinPE dalla directory di installazione di Windows ADK. La pagina **Generale** dell'Aggiornamento guidato punti di distribuzione contiene le informazioni seguenti: 
 - La versione di Windows ADK installata nel server del sito
 - La versione Windows ADK di WinPE nell'immagine d'avvio
 - La versione del client di Configuration Manager. Usare questa informazione per decidere se ricaricare l'immagine d'avvio. Il nodo **Immagini d'avvio** include anche una nuova colonna per (**Versione client**). Usare questa colonna per visualizzare rapidamente la versione del client di Configuration Manager in ogni immagine d'avvio.    


##  <a name="BKMK_BootImageCustom"></a> Personalizzare un'immagine d'avvio  
 Quando un'immagine d'avvio è basata sulla versione di WinPE della versione supportata di Windows ADK, è possibile personalizzare o [modificare un'immagine d'avvio](#BKMK_ModifyBootImages) dalla console. Quando un sito viene aggiornato con una nuova versione e viene installata una nuova versione di Windows ADK, le immagini d'avvio personalizzate, ovvero quelle che non si trovano nel percorso delle immagini d'avvio predefinite, non vengono aggiornate con la nuova versione di Windows ADK. In questi casi, non è possibile personalizzare le immagini d'avvio nella console di Configuration Manager. Queste immagini continueranno tuttavia a funzionare come prima dell'aggiornamento.  

 Quando un'immagine d'avvio è basata su una versione di Windows ADK diversa da quella installata in un sito, è necessario personalizzarla. Per personalizzare queste immagini d'avvio usare un altro metodo, ad esempio lo strumento da riga di comando Gestione e manutenzione immagini distribuzione. Gestione e manutenzione immagini distribuzione è incluso in Windows ADK. Per altre informazioni, vedere [Customize boot images](customize-boot-images.md) (Personalizzare le immagini d'avvio).  

##  <a name="BKMK_AddBootImages"></a> Aggiungere un'immagine d'avvio  

 Durante l'installazione del sito, Configuration Manager aggiunge automaticamente immagini d'avvio basate su una versione di WinPE dalla versione supportata di Windows ADK. A seconda della versione di Configuration Manager, è possibile aggiungere immagini d'avvio basate su una diversa versione di WinPE dalla versione supportata di Windows ADK. Quando si prova ad aggiungere un'immagine d'avvio che contiene una versione non supportata di WinPE si verifica un errore. L'elenco seguente include le versioni di Windows ADK e WinPE attualmente supportate: 

-   **Versione di Windows ADK**  

     Windows ADK per Windows 10  

-   **Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager**  

     Windows PE 10  

-   **Versioni di Windows PE supportate per le immagini d'avvio non personalizzabili dalla console di Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> È possibile aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE 3.1. Aggiornare Windows AIK per Windows 7 (basato su Windows PE 3.0) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). Scaricare il supplemento Windows AIK per Windows 7 SP1 dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

     Ad esempio, usare la console di Configuration Manager per personalizzare le immagini d'avvio basate su Windows PE 10 di Windows ADK per Windows 10. Nel caso di un'immagine d'avvio basata su Windows PE 5, personalizzarla in un altro computer usando la versione di Gestione e manutenzione immagini distribuzione di Windows ADK per Windows 8. Aggiungere quindi l'immagine d'avvio personalizzata alla console di Configuration Manager. Per altre informazioni, vedere [Customize boot images](customize-boot-images.md) (Personalizzare le immagini d'avvio).

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

 L'immagine d'avvio appare ora elencata nel nodo **Immagine d'avvio** della console di Configuration Manager. Prima di usare l'immagine d'avvio per distribuire un sistema operativo, distribuirla ai punti di distribuzione. 

> [!NOTE]  
>  Nel nodo **Immagine d'avvio** della console la colonna **Dimensione (KB)** visualizza la dimensione decompressa per ogni immagine d'avvio. Quando il sito invia un'immagine d'avvio in rete, ne invia una copia compressa. Le dimensioni di questa copia sono in genere inferiori rispetto a quelle indicate nella colonna **Dimensione (KB)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuire immagini d'avvio in un punto di distribuzione  
 Le immagini di avvio vengono distribuite nei punti di distribuzione nello stesso modo in cui vengono distribuiti gli altri contenuti. Nella maggior parte dei casi, è necessario distribuire l'immagine d'avvio almeno in un punto di distribuzione prima di distribuire il sistema operativo e prima di creare supporti.   

> [!NOTE]  
> Per usare PXE per la distribuzione di un sistema operativo, prima di distribuire l'immagine d'avvio tenere presente i punti seguenti:  
> - Configurare il punto di distribuzione in modo che accetti le richieste PXE.  
> - Distribuire un'immagine d'avvio x86 e una x64 abilitate per PXE in almeno un punto di distribuzione che supporta PXE.  
> - Configuration Manager distribuisce l'immagine d'avvio nella cartella **RemoteInstall** del punto di distribuzione abilitato per PXE.  
>   
> Per altre informazioni sull'uso di PXE per la distribuzione di sistemi operativi, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Per la procedura di distribuzione di un'immagine d'avvio, vedere [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modificare un'immagine d'avvio  
 È possibile aggiungere o rimuovere driver di dispositivo dall'immagine o modificare le proprietà associate all'immagine d'avvio. Ad esempio, è possibile aggiungere o rimuovere driver per scheda di rete o per dispositivi di archiviazione di massa. Quando si modificano le immagini di avvio, tenere presente quanto segue:  

-   Prima di aggiungere i driver di dispositivo all'immagine d'avvio, è necessario importarli e abilitarli nel catalogo dei driver di dispositivo.  

-   Quando si modifica un'immagine d'avvio, l'immagine non modifica i pacchetti associati a cui fa riferimento.  

-   Dopo aver apportato modifiche a un'immagine d'avvio, **aggiornarla** nei punti di distribuzione in cui è già presente. Grazie a questo processo, i client avranno a disposizione la versione più recente dell'immagine d'avvio. Per ulteriori informazioni, vedere [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

 Usare la procedura seguente per modificare un'immagine d'avvio.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Per modificare le proprietà di un'immagine di avvio  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini d'avvio**.  

3.  Selezionare l'immagine di avvio da modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà** per l'immagine di avvio.  

5.  Impostare le seguenti impostazioni per modificare il comportamento dell'immagine di avvio:  

    -   Nella scheda **Immagini** , se sono state modificate le proprietà dell'immagine di avvio utilizzando uno strumento esterno, fare clic su **Ricarica**.  

    -   Nella scheda **Driver** aggiungere i driver di dispositivo di Windows necessari per avviare WinPE. Quando si aggiungono i driver di dispositivo, tenere presente i punti seguenti:  

        -   Selezionare **Nascondi driver che non corrispondono all'architettura dell'immagine d'avvio** per visualizzare solo i driver relativi all'architettura dell'immagine d'avvio. L'architettura è basata su quella indicata nel file con estensione inf fornito dal produttore.  

        -   Selezionare **Nascondi driver non inclusi in una classe di archiviazione o di rete (per immagini d'avvio)** per visualizzare solo i driver di archiviazione e di rete. Questa opzione consente di nascondere anche altri driver in genere non necessari per le immagini d'avvio, ad esempio i driver video o quelli del modem.  

        -   Selezionare **Nascondi driver senza firma digitale** per nascondere i driver privi di una firma digitale valida.  

        -   Si consiglia di aggiungere all'immagine d'avvio solo i driver di rete e di archiviazione di massa, a meno che WinPE non richieda altri driver.  

        -   Poiché WinPE include già molti driver predefiniti, aggiungere solo i driver di rete e di archiviazione di massa non forniti da WinPE.  

        -   Verificare che i driver aggiunti all'immagine d'avvio corrispondano all'architettura dell'immagine d'avvio.  

        > [!NOTE]  
        >  È necessario importare i driver di dispositivo nel catalogo driver prima di aggiungerli a un'immagine di avvio. Per informazioni su come importare i driver di dispositivo, vedere [Gestire i driver](manage-drivers.md).  

    -   Nella scheda **Personalizzazione** selezionare una delle seguenti impostazioni:  

        -   Selezionare la casella di controllo **Attiva comando di preavvio** per specificare un comando da eseguire prima della sequenza attività. Quando si abilita questa opzione, specificare anche la riga di comando da eseguire e i file di supporto richiesti dal comando.  

            > [!WARNING]  
            >  Aggiungere **cmd /c** all'inizio della riga di comando. Se non si specifica **cmd /c**, il comando non verrà chiuso al termine dell'esecuzione. La distribuzione continuerà ad attendere la fine del comando e non avvierà altri comandi o azioni configurati.  

            > [!TIP]  
            >  Durante la creazione del supporto per la sequenza di attività, la procedura guidata scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per le eventuali variabili della sequenza di attività, nel file di log CreateTSMedia.log. Questo log si trova nel computer in cui viene eseguita la console di Configuration Manager. Rivedere questo file di log per verificare il valore per le variabili della sequenza di attività.  

        -   Configurare l'impostazione **Sfondo Windows PE** per specificare se si vuole usare lo sfondo Windows PE predefinito o uno sfondo personalizzato.  

        -   Selezionare **Abilita supporto comandi (solo test)** per aprire un prompt dei comandi usando il tasto **F8** mentre l'immagine d'avvio viene distribuita. Questa opzione è utile per la risoluzione dei problemi durante la verifica della distribuzione. Non è consigliabile utilizzare questa impostazione in un ambiente di produzione.  

        -   Configurare l'area scratch di Windows PE, ovvero l'archivio temporaneo (unità RAM) usato da WinPE. Ad esempio, quando un'applicazione viene eseguita in WinPE e richiede la scrittura di file temporanei, WinPE reindirizza tali file all'area scratch in memoria per simulare la presenza di un disco rigido. Per impostazione predefinita, WinPE alloca 32 megabyte (MB) di memoria scrivibile.  

    -   Nella scheda **Origine dati** aggiornare le seguenti impostazioni:  

        -   Per modificare il file di origine dell'immagine d'avvio, impostare **Percorso immagine** e **Indice immagine**.  

        -   Per creare una pianificazione di aggiornamento dell'immagine d'avvio da parte del sito, selezionare **Aggiorna i punti di distribuzione in base alla pianificazione**.  

        -   Se non si vuole che il contenuto del pacchetto venga eliminato dalla cache del client per liberare spazio per altro contenuto, selezionare **Mantieni contenuto nella cache del client**.  

        -   Per specificare che il sito distribuisce solo i file modificati quando aggiorna il pacchetto dell'immagine d'avvio nel punto di distribuzione, selezionare **Abilita la replica differenziale binaria** (BDR). Questa impostazione riduce al minimo il traffico di rete tra siti. La replica differenziale binaria è particolarmente utile quando il pacchetto dell'immagine d'avvio è di grandi dimensioni e le modifiche sono piuttosto limitate.  

        -   Se l'immagine d'avvio viene usata in una distribuzione che supporta PXE, selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE**.  

            > [!NOTE]  
            >  Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Nella scheda **Accesso dati** selezionare una delle seguenti impostazioni:  

        -   Selezionare **Impostazioni condivisione pacchetto** se si desidera che i client installino il contenuto in questo pacchetto dalla rete.  

        -   In **Impostazioni aggiornamento pacchetto** specificare in che modo si vuole che Configuration Manager disconnetta gli utenti dal punto di distribuzione. È possibile che Configuration Manager non sia in grado di aggiornare l'immagine d'avvio quando gli utenti sono connessi al punto di distribuzione.  

    -   Nella scheda **Impostazioni distribuzione** selezionare una delle seguenti impostazioni:  

        -   Nell'elenco **Priorità di distribuzione** specificare il livello di priorità. Configuration Manager usa questo elenco delle priorità quando il sito distribuisce più pacchetti allo stesso punto di distribuzione.  

        -   Per attivare la distribuzione del contenuto su richiesta nei punti di distribuzione preferiti, selezionare **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**. Quando si abilita questa impostazione, se un client richiede il contenuto per il pacchetto e il contenuto non è disponibile in nessuno dei punti di distribuzione preferiti, il punto di gestione distribuisce il contenuto a tutti i punti di distribuzione preferiti.  

        -   Per specificare come il sito distribuirà l'immagine d'avvio ai punti di distribuzione abilitati per i contenuti in versione di preproduzione, selezionare **Impostazioni punto di distribuzione pre-installazione**.  

            > [!NOTE]  
            >  Per altre informazioni sui contenuti in versione di preproduzione, vedere [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   Nella scheda **Percorsi contenuto** selezionare il punto di distribuzione o il gruppo di punti di distribuzione ed eseguire le seguenti azioni:  

        -   Fare clic su **Ridistribuisci** per distribuire nuovamente l'immagine di avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

        -   Fare clic su **Convalida** per verificare l'integrità del pacchetto di immagini di avvio nel punto di distribuzione o nel gruppo di punti di distribuzione selezionato.  

    -   Nella scheda **Componenti facoltativi** specificare i componenti aggiunti a Windows PE per l'utilizzo con Configuration Manager. Per altre informazioni sui componenti facoltativi disponibili, vedere [WinPE: aggiungere pacchetti (informazioni di riferimento sui componenti facoltativi)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

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
 Le immagini di avvio sono indipendenti dalla lingua. Questa funzionalità consente di usare un'immagine d'avvio per visualizzare il testo della sequenza di attività in più lingue all'interno di WinPE. Includere il supporto della lingua appropriato dalla scheda **Componenti facoltativi** dell'immagine d'avvio. Impostare quindi la variabile della sequenza di attività appropriata per indicare la lingua da visualizzare. La lingua del sistema operativo distribuito è indipendente dalla lingua usata in WinPE. La lingua che WinPE visualizza all'utente viene determinata nel modo seguente:  

-   Quando un utente esegue la sequenza di attività da un sistema operativo esistente, Configuration Manager usa automaticamente la lingua configurata per l'utente. Quando la sequenza di attività viene eseguita automaticamente a causa della scadenza di una distribuzione obbligatoria, Configuration Manager usa la lingua del sistema operativo.  

-   Per le distribuzioni di sistemi operativi avviate da PXE o da supporti, impostare il valore di ID lingua nella variabile **SMSTSLanguageFolder** all'interno di un comando di preavvio. Quando il computer si avvia in Windows PE, i messaggi vengono visualizzati nella lingua specificata nella variabile. Se si verifica un errore durante l'accesso al file di risorse della lingua nella cartella specificata o se la variabile non viene impostata, WinPE visualizza i messaggi nella lingua predefinita.  

    > [!NOTE]  
    >  Quando il supporto è protetto da una password, il testo di richiesta di immissione della password viene sempre visualizzato nella lingua di WinPE.  

 Usare la procedura seguente per impostare la lingua di WinPE per distribuzioni del sistema operativo avviate da PXE o da supporto.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Per impostare la lingua di Windows PE per una distribuzione del sistema operativo avviata da PXE o da supporto  

1.  Prima di aggiornare l'immagine d'avvio, verificare che il file di risorse della sequenza di attività appropriato (tsres.dll) sia incluso nella cartella della lingua corrispondente nel server del sito. Il file di risorse inglese, ad esempio, si trova nel percorso seguente: <*ConfigMgrInstallationFolder*>\OSD\bin\x64\00000409\tsres.dll.  

2.  Come parte del comando di preavvio, impostare la variabile di ambiente SMSTSLanguageFolder sull'ID lingua appropriato. L'ID lingua deve essere specificato usando valori decimali e non esadecimali. Ad esempio, per impostare l'ID lingua su Inglese, specificare il valore decimale 1033, non il valore esadecimale 00000409 del nome della cartella.  
