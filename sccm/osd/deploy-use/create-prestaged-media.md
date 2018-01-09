---
title: Creare supporti pre-installati
titleSuffix: Configuration Manager
description: Creare supporti preinstallati in System Center Configuration Manager per semplificare la distribuzione di Windows in diversi scenari.
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: a26fc3daf17aefe24a46ece561fc2ceaf5284ffb
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Creare supporti pre-installati con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I supporti preinstallati in System Center Configuration Manager sono file WIM (Windows Imaging Format) che possono essere installati in un computer bare metal dal produttore o in un centro di gestione temporanea aziendale non connesso all'ambiente di Configuration Manager.  
Il supporto pre-installato contiene l'immagine di avvio usata per avviare il computer di destinazione e l'immagine del sistema operativo applicata al computer di destinazione. È anche possibile specificare applicazioni, pacchetti e pacchetti driver da includere come parte del supporto pre-installato. La sequenza di attività che distribuisce il sistema operativo non è inclusa nel supporto. Il supporto pre-installato viene applicato al disco rigido di un nuovo computer prima che il computer venga inviato all'utente finale. Usare i supporti preinstallati per gli scenari di distribuzione del sistema operativo seguenti:  

-   [Creare un'immagine per un OEM presso un produttore computer o un deposito locale](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Distribuire Windows to Go](deploy-windows-to-go.md)  

 Quando viene avviato per la prima volta dopo l'applicazione del supporto pre-installato, il computer avvia Windows PE e si connette a un punto di gestione per trovare la sequenza di attività che completa il processo di distribuzione del sistema operativo. È possibile specificare applicazioni, pacchetti e pacchetti driver da includere come parte del supporto preinstallato. Quando si distribuisce una sequenza di attività che usa un supporto pre-installato, la procedura guidata verifica innanzitutto la presenza di contenuto valido nella cache della sequenza di attività locale. Se non è possibile trovare il contenuto oppure il contenuto è stato rivisto, la procedura guidata scarica il contenuto dal punto di distribuzione.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Come creare un supporto pre-installato  
 Prima di creare un supporto preinstallato usando la Creazione guidata del supporto per la sequenza attività, assicurarsi che siano soddisfatte tutte le condizioni seguenti:  

|Attività|Descrizione|  
|----------|-----------------|  
|Immagine d'avvio|Tenere presente quanto segue per l'immagine d'avvio da usare nella sequenza di attività per distribuire il sistema operativo:<br /><br /> - L'architettura dell'immagine di avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.<br />- Verificare che l'immagine di avvio contenga i driver di archiviazione di rete e di massa necessari per eseguire il provisioning del computer di destinazione.|  
|Creare una sequenza di attività per distribuire un sistema operativo|Come parte del supporto preinstallato, è necessario specificare la sequenza di attività per distribuire il sistema operativo.<br /><br /> - Per i passaggi necessari per creare una nuova sequenza di attività, vedere [Creare una sequenza di attività per installare un sistema operativo](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />- Per altre informazioni sulle sequenze di attività, vedere l'argomento sulla [gestione delle sequenze di attività per automatizzare le attività](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Distribuire tutto il contenuto associato alla sequenza di attività|È necessario distribuire in almeno un punto di distribuzione tutto il contenuto richiesto dalla sequenza di attività. Ciò include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie le informazioni dal punto di distribuzione quando viene creato il supporto autonomo. È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nel punto di distribuzione.  Per informazioni dettagliate, vedere [Informazioni sulla raccolta contenuto](../../core/plan-design/hierarchy/the-content-library.md).|  
|Disco rigido nel computer di destinazione|È necessario eseguire la formattazione del disco rigido del computer di destinazione prima che il supporto di pre-installazione venga installato nel disco rigido del computer. Se il disco rigido non è formattato quando viene applicato il supporto, la sequenza di attività che distribuisce il sistema operativo non riuscirà ad avviare il computer di destinazione.|  

> [!NOTE]  
>  La Creazione guidata del supporto per la sequenza di attività imposta la seguente condizione variabile di sequenza di attività nel supporto: **_SMSTSMediaType = OEMMedia**. È possibile usare questa condizione nella sequenza di attività.  

 Usare la procedura seguente per creare supporti pre-installati.  

#### <a name="to-create-prestaged-media"></a>Per creare supporti pre-installati  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4.  Nella pagina **Seleziona tipo di supporto** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   Selezionare **Supporti preinstallati**.  

    -   Se si desidera consentire la distribuzione del sistema operativo senza l'interazione dell'utente, selezionare **Consenti distribuzione automatica del sistema operativo**. Quando si seleziona questa opzione, all'utente non verrà chiesto di immettere informazioni sulla configurazione di rete o di scegliere se eseguire sequenze attività facoltative. Tuttavia, all'utente viene richiesta una password se il supporto è configurato per la protezione con password.  

5.  Nella pagina **Gestione del supporto** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   Selezionare **Supporto dinamico** se si desidera consentire a un punto di gestione di reindirizzare il supporto a un altro punto di gestione, in base al percorso del client nei limiti del sito.  

    -   Selezionare **Supporto basato su sito** se si desidera che il supporto contatti solo il punto di gestione specificato.  

6.  Nella pagina **Proprietà del supporto**  specificare le informazioni seguenti e fare clic su **Avanti**.  

    -   **Creato da**: specificare chi ha creato il supporto.  

    -   **Versione**: specificare il numero di versione del supporto.  

    -   **Commento**: specificare una descrizione univoca dello scopo per cui viene usato il supporto.  

    -   **File supporto**: specificare il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. Ad esempio: **\\\nomeserver\cartella\fileoutput.wim**  

7.  Nella pagina **Sicurezza** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   Selezionare la casella di controllo **Abilita supporto per computer sconosciuti** per consentire al supporto di distribuire un sistema operativo a un computer non gestito da Configuration Manager. Non sono presenti record di questi computer nel database di Configuration Manager.  Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Selezionare la casella di controllo **Proteggi supporto con password** e immettere una password complessa per proteggere il supporto da accesso non autorizzato. Quando si specifica una password l'utente deve immettere la password per usare il supporto pre-installato.  

        > [!IMPORTANT]  
        >  Come procedura consigliata di sicurezza, assegnare sempre una password per proteggere il supporto pre-installato.  

    -   Per le comunicazioni HTTP, selezionare **Crea certificato del supporto autofirmato**e quindi specificare la data di inizio e di scadenza del certificato.  

    -   Per le comunicazioni HTTPS, selezionare **Importa certificato PKI**e quindi specificare il certificato da importare e la relativa password.  

         Per altre informazioni su questo certificato client usato per le immagini di avvio, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Affinità utente dispositivo**: per supportare la gestione basata sugli utenti in Configuration Manager, specificare come si vuole che il supporto associ gli utenti al computer di destinazione. Per altre informazioni su come la distribuzione del sistema operativo supporti l'affinità utente dispositivo, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

        -   Specificare **Consenti affinità utente dispositivo con approvazione automatica** se si desidera che il supporto associ automaticamente gli utenti al computer di destinazione. Questa funzionalità si basa sulle azioni della sequenza di attività che distribuisce il sistema operativo. In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione quando distribuisce il sistema operativo nel computer di destinazione.  

        -   Specificare **Consenti approvazione amministratore in sospeso per affinità utente dispositivo** se si desidera che il supporto associ gli utenti al computer di destinazione dopo la concessione dell'approvazione. Questa funzionalità si basa sull'ambito della sequenza di attività che distribuisce il sistema operativo. In questo scenario, la sequenza di attività crea una relazione tra gli utenti specificati e il computer di destinazione, ma attende l'approvazione di un utente amministratore prima di distribuire il sistema operativo.  

        -   Specificare **Non consentire affinità utente dispositivo** se non si desidera che il supporto associ gli utenti al computer di destinazione. In questo scenario, la sequenza di attività non associa gli utenti al computer di destinazione quando distribuisce il sistema operativo.  

8.  Nella pagina **Sequenza di attività** specificare la sequenza di attività che verrà eseguita nel computer di destinazione. Il contenuto a cui fa riferimento la sequenza di attività viene visualizzato in **Questa sequenza attività fa riferimento al contenuto seguente**. Verificare il contenuto e quindi fare clic su **Avanti**.  

9. Nella pagina **Immagine di avvio** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  L'architettura dell'immagine di avvio distribuita deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.  

    -   Nella casella **Immagine di avvio** specificare l'immagine di avvio per avviare il computer di destinazione. Per altre informazioni, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

    -   Nella casella **Punto di distribuzione** specificare il punto di distribuzione in cui si trova l'immagine di avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        >  È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nel punto di distribuzione. Per altre informazioni, vedere [Informazioni sulla raccolta contenuto](../../core/plan-design/hierarchy/the-content-library.md).  

    -   Se è stato selezionato **Supporto basato su sito** nella pagina **Gestione del supporto** della procedura guidata, nella casella **Punto di gestione** specificare un punto di gestione da un sito primario.  

    -   Se è stato selezionato **Supporto dinamico** nella pagina **Gestione del supporto** della procedura guidata, nella casella **Punti di gestione associati** specificare i punti di gestione del sito primario da usare e un ordine di priorità per le comunicazioni iniziali.  

10. Nella pagina **Immagini** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   Nella casella **Pacchetto immagine** specificare l'immagine del sistema operativo. Per altre informazioni, vedere [Manage operating system images](../get-started/manage-operating-system-images.md) (Gestire le immagini del sistema operativo).  

    -   Se il pacchetto contiene più immagini del sistema operativo, nella casella **Pacchetto immagine** specificare l'immagine da distribuire.  

    -   Nella casella **Punto di distribuzione** specificare il punto di distribuzione in cui si trova il pacchetto immagine del sistema operativo. La procedura guidata recupera l'immagine del sistema operativo dal punto di distribuzione e la scrive sul supporto.  

11. Nella pagina **Personalizzazione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   Specificare le variabili usate dalla sequenza di attività per distribuire il sistema operativo.  

    -   Specificare i comandi preavvio da eseguire prima dell'esecuzione della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile in grado di interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività per l'installazione del sistema operativo. Per altre informazioni sui comandi di preavvio per il supporto, vedere [Comandi di preavvio per supporti per sequenza di attività](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Durante la creazione del supporto delle sequenza di attività, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file di registro CreateTSMedia.log nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

12. Completare la procedura guidata.  

## <a name="next-steps"></a>Passaggi successivi
[Scenari di distribuzione di sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md)
