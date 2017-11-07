---
title: 'Creare supporti di avvio '
titleSuffix: Configuration Manager
description: In Configuration Manager i supporti di avvio semplificano l'installazione di una nuova versione di Windows o la sostituzione di un computer e il trasferimento delle impostazioni.
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f75a29ff27a1f806d4329bd2dfc5e30a8991fac9
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Creare supporti di avvio con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I supporti di avvio in Configuration Manager contengono l'immagine d'avvio, i comandi di preavvio opzionali e i rispettivi file associati e i file di Configuration Manager. Usare i supporti preinstallati per gli scenari di distribuzione del sistema operativo seguenti:  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Creare supporti di avvio  
 All'avvio dei supporti di avvio, il computer di destinazione viene avviato, si connette alla rete e recupera la sequenza di attività specificata, l'immagine del sistema operativo e qualsiasi altro contenuto necessario dalla rete. Poiché la sequenza di attività non è presente sul supporto, è possibile modificare la sequenza di attività o il contenuto senza dover ricreare il supporto. I pacchetti nei supporti di avvio non sono crittografati. È necessario adottare le misure di sicurezza appropriate, ad esempio l'aggiunta di una password al supporto, per garantire che il contenuto del pacchetto sia protetto da utenti non autorizzati.  

 Prima di creare supporti di avvio usando la Creazione guidata del supporto per la sequenza attività, assicurarsi che siano soddisfatte tutte le condizioni seguenti:  

|Attività|Descrizione|  
|----------|-----------------|  
|Immagine d'avvio|Tenere presente quanto segue per l'immagine d'avvio da usare nella sequenza di attività per distribuire il sistema operativo:<br /><br /> - L'architettura dell'immagine di avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.<br />- Verificare che l'immagine di avvio contenga i driver di archiviazione di rete e di massa necessari per eseguire il provisioning del computer di destinazione.|  
|Creare una sequenza di attività per distribuire un sistema operativo|Come parte del supporto di avvio, è necessario specificare la sequenza di attività per distribuire il sistema operativo. - Per i passaggi necessari per creare una nuova sequenza di attività, vedere [Creare una sequenza di attività per installare un sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Distribuire tutto il contenuto associato alla sequenza di attività|È necessario distribuire in almeno un punto di distribuzione tutto il contenuto richiesto dalla sequenza di attività. Ciò include l'immagine d'avvio e altri file di preavvio associati. La procedura guidata raccoglie le informazioni dal punto di distribuzione quando crea il supporto di avvio. È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nel punto di distribuzione.  Per informazioni dettagliate, vedere [Informazioni sulla raccolta contenuto](../../core/plan-design/hierarchy/the-content-library.md).|  
|Preparare l'unità USB rimovibile|Per un'unità USB rimovibile:<br /><br /> Se si usa un'unità USB rimovibile, l'unità deve essere collegata al computer in cui viene eseguita la procedura guidata e rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto. Supporto autonomo usa un file system FAT32. Non è possibile creare supporti autonomi in un'unità flash USB il cui contenuto include un file di oltre 4 GB.|  
|Creare una cartella di output|Per un set di CD/DVD:<br /><br /> Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, è necessario creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.|  

 Usare la procedura seguente per creare supporti di avvio.  

### <a name="to-create-bootable-media"></a>Per creare il supporto di avvio  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4.  Nella pagina **Seleziona tipo di supporto** specificare le opzioni seguenti e quindi fare clic su **Avanti**.  

    -   Selezionare **Supporto di avvio**.  

    -   Se si desidera solo consentire la distribuzione del sistema operativo senza richiedere l'input utente, è possibile selezionare **Consenti distribuzione automatica del sistema operativo**.  

        > [!IMPORTANT]  
        >  Quando si seleziona questa opzione, all'utente non vengono richieste informazioni sulla configurazione di rete o le sequenze attività facoltative. Tuttavia, all'utente viene richiesta una password se il supporto è configurato per la protezione con password.  

5.  Nella pagina **Gestione del supporto** specificare una delle opzioni seguenti e quindi fare clic su **Avanti**.  

    -   Selezionare **Supporto dinamico** se si desidera consentire a un punto di gestione di reindirizzare il supporto a un altro punto di gestione, in base al percorso del client nei limiti del sito.  

    -   Selezionare **Supporto basato su sito** se si desidera che il supporto contatti solo il punto di gestione specificato.  

6.  Nella pagina **Tipo di supporto** specificare se il supporto è un'unità flash o un set di CD/DVD, quindi configurare quanto segue:  

    > [!IMPORTANT]  
    >  Supporto autonomo usa un file system FAT32. Non è possibile creare supporti autonomi in un'unità flash USB il cui contenuto include un file di oltre 4 GB.  

    -   Se si seleziona **Unità memoria flash USB**, è necessario specificare l'unità in cui archiviare il contenuto.  

    -   Se si seleziona l'opzione **CD/DVD impostato**, specificare la capacità del supporto e il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. Ad esempio: **\\\nomeserver\cartella\filedioutput.iso**  

         Se la capacità del supporto non è sufficiente per archiviare l'intero contenuto, vengono creati più file ed è necessario archiviare il contenuto in più CD o DVD. Quando sono necessari più supporti, Configuration Manager aggiunge un numero di sequenza al nome di ogni file di output creato. Se insieme al sistema operativo si distribuisce un'applicazione e questa non può essere contenuta in un unico supporto, Configuration Manager archivia l'applicazione in più supporti. Quando il supporto autonomo viene eseguito Configuration Manager chiede all'utente il supporto successivo contenente l'applicazione.  

        > [!IMPORTANT]  
        >  Se si seleziona un'immagine iso esistente, la Creazione guidata del supporto per la sequenza di attività elimina l'immagine dall'unità o dalla condivisione non appena si passa alla pagina successiva della procedura guidata. L'immagine esistente viene eliminata, anche se si annulla la procedura guidata.  

     Fare clic su **Avanti**.  

7.  Nella pagina **Sicurezza** specificare le opzioni seguenti e quindi fare clic su **Avanti**.  

    -   Selezionare la casella di controllo **Abilita supporto per computer sconosciuti** per consentire al supporto di distribuire un sistema operativo a un computer non gestito da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager.  

         I computer sconosciuti includono i seguenti:  

        -   Computer in cui non è installato il client di Configuration Manager  

        -   Computer che non sono stati importati in Configuration Manager  

        -   Computer che non sono stati rilevati da Configuration Manager  

    -   Selezionare la casella di controllo **Proteggi supporto con password** e immettere una password complessa per proteggere il supporto da accesso non autorizzato. Quando si specifica una password, l'utente deve immettere la password per usare il supporto di avvio.  

        > [!IMPORTANT]  
        >  Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto di avvio.  

    -   Per le comunicazioni HTTP, selezionare **Crea certificato del supporto autofirmato**e quindi specificare la data di inizio e di scadenza del certificato.  

    -   Per le comunicazioni HTTPS, selezionare **Importa certificato PKI**e quindi specificare il certificato da importare e la relativa password.  

         Per altre informazioni su questo certificato client usato per le immagini di avvio, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Affinità utente dispositivo**: per supportare la gestione basata sugli utenti in Configuration Manager, specificare come si vuole che il supporto associ gli utenti al computer di destinazione. Per altre informazioni su come la distribuzione del sistema operativo supporti l'affinità utente dispositivo, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

        -   Specificare **Consenti affinità utente dispositivo con approvazione automatica** se si desidera che il supporto associ automaticamente gli utenti al computer di destinazione. Questa funzionalità si basa sulle azioni della sequenza di attività che distribuisce il sistema operativo. In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

        -   Specificare **Consenti approvazione amministratore in sospeso per affinità utente dispositivo** se si desidera che il supporto associ gli utenti al computer di destinazione dopo la concessione dell'approvazione. Questa funzionalità si basa sull'ambito della sequenza di attività che distribuisce il sistema operativo.  In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione, ma attende l'approvazione di un utente amministratore prima di distribuire il sistema operativo.  

        -   Specificare **Non consentire affinità utente dispositivo** se non si desidera che il supporto associ gli utenti al computer di destinazione. In questo scenario, la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.  

8.  Nella pagina **Immagine di avvio** specificare le opzioni seguenti e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  L'architettura dell'immagine di avvio distribuita deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.  

    -   Nella casella **Immagine di avvio** specificare l'immagine di avvio per avviare il computer di destinazione.  

    -   Nella casella **Punto di distribuzione** specificare il punto di distribuzione in cui si trova l'immagine di avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        >  È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nel punto di distribuzione.  

    -   Se si crea un supporto di avvio basato su sito nella pagina **Gestione del supporto** della procedura guidata, specificare un punto di gestione da un sito primario nella casella **Punto di gestione** .  

    -   Se si crea un supporto di avvio dinamico nella pagina **Gestione del supporto** della procedura guidata, specificare i punti di gestione del sito primario da usare e un ordine di priorità per le comunicazioni iniziali in **Punti di gestione associati**.  

9. Nella pagina **Personalizzazione** specificare le seguenti opzioni e quindi fare clic su **Avanti**.  

    -   Specificare le variabili usate dalla sequenza di attività per distribuire il sistema operativo.  

    -   Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile in grado di interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività per l'installazione del sistema operativo. Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante la creazione del supporto delle sequenza di attività, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file di registro CreateTSMedia.log nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

         Se necessario, selezionare la casella di controllo **Includi file per il comando di preavvio** per includere eventuali file richiesti dal comando di preavvio.  

10. Completare la procedura guidata.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Creare supporti di avvio in un'unità USB da una condivisione di rete
Le informazioni contenute in questa sezione consentono di creare supporti di avvio in un'unità memoria flash USB quando l'unità non è connessa al computer che esegue la console di Configuration Manager. Per creare il supporto di avvio nell'unità USB, è possibile creare il supporto di avvio della sequenza di attività, montare l'immagine ISO e trasferire i file dall'immagine ISO all'unità USB.

1. [Creare il supporto di avvio della sequenza di attività](#to-create-task-boobable-media). Nella pagina **Tipo di supporto** selezionare **CD/DVD impostato**. La procedura guidata scrive i file di output nella posizione specificata. Ad esempio: **\\\nomeserver\cartella\filedioutput.iso**.  
2. Preparare l'unità USB rimovibile. L'unità deve essere formattata, vuota e di avvio.
3. Montare l'immagine ISO dal percorso di condivisione e trasferire i file dall'immagine ISO all'unità USB.

## <a name="next-steps"></a>Passaggi successivi  
[Usare i supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  
