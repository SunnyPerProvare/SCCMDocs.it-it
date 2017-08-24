---
title: Usare PXE per distribuire Windows in rete | Documentazione Microsoft
description: Usare le distribuzioni del sistema operativo avviate da PXE per aggiornare il sistema operativo di un computer o per installare una nuova versione di Windows in un nuovo computer.
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: "19"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: b88ab3799027c78a8c605e934b247097b31e1d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usare PXE per distribuire Windows in rete con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le distribuzioni del sistema operativo avviate da Pre-Boot eXecution Environment (PXE) in System Center Configuration Manager consentono ai computer client di richiedere e distribuire sistemi operativi in rete. In questo scenario di distribuzione l'immagine del sistema operativo e le immagini d'avvio di Windows PE, sia x86 che x64, vengono inviate a un punto di distribuzione configurato per accettare le richieste di avvio PXE.

> [!NOTE]  
>  Quando si crea una distribuzione del sistema operativo destinata solo a computer BIOS x64, nel punto di distribuzione devono essere disponibili sia l'immagine di avvio x64 che l'immagine di avvio x86.

È possibile usare distribuzioni del sistema operativo avviate da PXE negli scenari di distribuzione del sistema operativo seguenti:

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi usare le sezioni seguenti per preparare le distribuzioni avviate da PXE.

##  <a name="BKMK_Configure"></a> Configurare almeno un punto di distribuzione per accettare le richieste PXE
Per distribuire i sistemi operativi ai client che eseguono richieste di avvio PXE, usare uno o più punti di distribuzioni configurati per rispondere alle richieste di avvio PXE. Per i passaggi relativi all'abilitazione di PXE per un punto di distribuzione, vedere [Configurazione dei punti di distribuzione per accettare le richieste PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparare un'immagine d'avvio che supporta PXE
Per usare PXE per distribuire un sistema operativo, è necessario avere immagini d'avvio che supportano PXE sia x86 sia x64, distribuite in uno o più punti di distribuzione che supportano PXE. Usare le informazioni per abilitare PXE in un'immagine d'avvio e distribuirla nei punti di distribuzione:

-   Per abilitare PXE in un'immagine d'avvio, selezionare **Distribuire questa immagine d'avvio dal punto di distribuzione che supporta PXE** nella scheda **Origine dati** nelle proprietà dell'immagine d'avvio.

-   Se si modificano le proprietà per l'immagine d'avvio, ridistribuirla nei punti di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).

##  <a name="BKMK_PXEExclusionList"></a> Creare un elenco di esclusione per le distribuzioni PXE
Quando si distribuiscono sistemi operativi con PXE, è possibile creare un elenco di esclusione in ogni punto di distribuzione. Aggiungere gli indirizzi MAC all'elenco di esclusione dei computer che si vuole vengano ignorati dal punto di distribuzione. I computer elencati non riceveranno le sequenze di attività di distribuzione usate da Configuration Manager per la distribuzione PXE.

#### <a name="to-create-the-exclusion-list"></a>Per creare l'elenco di esclusione

1.  Creare un file di testo nel punto di distribuzione che supporta PXE. Ad esempio, assegnare al file di testo il nome **pxeExceptions.txt**.

2.  Usare un editor di testo semplice, ad esempio Blocco note, e aggiungere gli indirizzi MAC dei computer che il punto di distribuzione che supporta PXE deve ignorare. Separare i valori degli indirizzi MAC con i due punti e immettere ogni indirizzo in una riga separata. Ad esempio: `01:23:45:67:89:ab`

3.  Salvare il file di testo nel server del sistema del sito del punto distribuzione che supporta PXE. Il file di testo può essere salvato in qualsiasi posizione nel server.

4.  Modificare il Registro di sistema del punto di distribuzione che supporta PXE per creare una chiave del Registro di sistema **MACIgnoreListFile**. Aggiungere il valore della stringa del percorso completo per il file di testo nel server del sistema del sito del punto distribuzione che supporta PXE. Utilizzare il seguente percorso del Registro di sistema:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  L'errato utilizzo dell'editor del Registro di sistema può provocare gravi problemi che potrebbero richiedere la reinstallazione del sistema operativo. La risoluzione dei problemi derivanti dall'errato utilizzo dell'editor del Registro di sistema non è garantita. L'utilizzo dell'editor del Registro di sistema è a rischio dell'utente.

     Non è necessario riavviare il server dopo aver modificato il Registro di sistema.

##  <a name="BKMK_RamDiskTFTP"></a>Dimensioni del blocco e della finestra TFTP RamDisk
È possibile personalizzare le dimensioni del blocco TFTP RamDisk e, a partire da Configuration Manager versione 1606, le dimensioni della finestra per i punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout perché le dimensioni del blocco o della finestra sono troppo grandi. La personalizzazione delle dimensioni della finestra e del blocco TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare requisiti di rete specifici. Testare le impostazioni personalizzate nel proprio ambiente per stabilire quale sia il metodo più efficiente. Per altre informazioni, vedere [Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione
Per usare la distribuzione del sistema operativo avviata da PXE, è necessario configurarla per rendere disponibile il sistema operativo per le richieste di avvio PXE. È possibile configurare i sistemi operativi disponibili nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione. Per l'impostazione **Rendi disponibile per** , configurare uno degli elementi seguenti:

-   Client di Configuration Manager, supporti e PXE

-   Solo supporti e PXE

-   Solo supporti e PXE (nascosto)

##  <a name="BKMK_Deploy"></a> Distribuire la sequenza di attività
Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando si distribuiscono sistemi operativi tramite PXE, è possibile specificare se la distribuzione è obbligatoria o disponibile.

-   **Distribuzione richiesta**: le distribuzioni richieste usano PXE senza alcun intervento da parte dell'utente. L'utente non sarà in grado di ignorare l'avvio di PXE. Tuttavia, se l'utente annulla l'avvio di PXE prima della risposta del punto di distribuzione, il sistema operativo non verrà distribuito.

-   **Distribuzione disponibile**: le distribuzioni disponibili richiedono che l'utente sia presente sul computer di destinazione, per poter premere il tasto F12 per continuare il processo di avvio PXE. Se l'utente non è presente per premere F12, il computer avvierà il sistema operativo corrente oppure verrà avviato dal dispositivo di avvio successivo disponibile.

È possibile ridistribuire una distribuzione PXE richiesta cancellando lo stato dell'ultima distribuzione PXE assegnato a una raccolta di Configuration Manager o a un computer. Questa azione consente di reimpostare lo stato di quella distribuzione e reinstalla le distribuzioni richieste più recenti.

> [!IMPORTANT]
> Il protocollo PXE non è sicuro. Assicurarsi che il server PXE e il client PXE si trovino su una rete fisicamente protetta, come ad esempio in un data center, per evitare accessi non autorizzati al sito.

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Come viene selezionata l'immagine di avvio per i client avviati con PXE?
Quando un client viene avviato con PXE Configuration Manager rende disponibile per il client un'immagine di avvio. A partire dalla versione 1606, Configuration Manager usa un'immagine di avvio con un'architettura esattamente corrispondente. Se non è disponibile un'immagine di avvio con l'architettura esatta, Configuration Manager usa un'immagine di avvio con un'architettura compatibile. L'elenco seguente contiene informazioni dettagliate sulle modalità di selezione di un'immagine di avvio per i client avviati con PXE.
1. Configuration Manager cerca nel database del sito il record di sistema corrispondente all'indirizzo MAC o al SMBIOS del client che sta tentando di eseguire l'avvio.  

    > [!NOTE]
    > Se un computer assegnato a un sito viene avviato in PXE per un sito diverso, i criteri non sono visibili per il computer. Ad esempio, se un client è già assegnato al sito A, il punto di gestione e il punto di distribuzione per il sito B non saranno in grado di accedere ai criteri dal sito A. Il client non riuscirà a completare l'avvio di PXE.

2. Configuration Manager cerca le sequenze di attività che vengono distribuite nel record di sistema menzionato nel passaggio 1.

3. Nell'elenco di sequenze di attività menzionato nel passaggio 2 Configuration Manager cerca un'immagine di avvio corrispondente all'architettura del client che sta tentando di eseguire l'avvio. Se viene trovata un'immagine di avvio con la stessa architettura, verrà usata quell'immagine.

4. Se non viene trovata un'immagine di avvio con la stessa architettura, Configuration Manager cerca un'immagine di avvio compatibile con l'architettura del client. Esegue la ricerca nell'elenco di sequenze di attività indicato nel passaggio 2. Ad esempio, un client a 64 bit è compatibile con immagini di avvio a 32 bit e 64 bit. Un client a 32 bit è compatibile solo con le immagini di avvio a 32 bit. Un client UEFI è compatibile solo con le immagini di avvio a 64 bit.
