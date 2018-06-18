---
title: Note sulla versione di MDT
description: Informazioni sulle piattaforme supportate, su prerequisiti e limitazioni di Microsoft Deployment Toolkit.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814281"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Note sulla versione di Microsoft Deployment Toolkit  

Questo articolo offre informazioni dettagliate sulla versione più recente di Microsoft Deployment Toolkit (MDT). Questi dettagli includono piattaforme supportate, prerequisiti e possibili limitazioni. Si presuppone una familiarità con i concetti, le caratteristiche e le funzionalità di MDT.



## <a name="latest-release"></a>Versione più recente

**MDT build 8450** è la versione più recente disponibile nell'[area download Microsoft](https://aka.ms/mdtdownload). 

Questo aggiornamento abilita per la prima volta il supporto per Windows Assessment and Deployment Kit (ADK) per Windows 10, versione 1709. 

***Aggiornamento***: a partire da maggio 2018, la build supporta anche Windows 10, versione 1803.

Per altre informazioni, vedere la sezione [Piattaforme supportate](#supported-platforms).


### <a name="significant-changes"></a>Modifiche significative
Di seguito è riportato un riepilogo delle modifiche significative di questa build di MDT.

#### <a name="supported-configuration-updates"></a>Aggiornamenti della configurazione supportati
- Windows ADK per Windows 10, versione 1709
- Windows 10, versione 1709
- Configuration Manager, versione 1710

#### <a name="quality-updates"></a>Aggiornamenti qualitativi
Di seguito sono riportati i titoli delle correzioni di bug in questa versione:
- Dipendenze e licenza delle app Win10 con trasferimento locale non installate
- La sequenza dell'attività CaptureOnly non consente l'acquisizione di un'immagine
- Errore ricevuto all'avvio di una sequenza di attività di MDT: valore DeploymentType "" specificato non valido. Non sarà possibile proseguire con la distribuzione
- ZTIMoveStateStore cerca la cartella di archivio di stato nel percorso errato, di conseguenza lo spostamento non riesce
- Il file con estensione xml contiene un errore di digitazione semplice che ha causato un comportamento indesiderato
- L'installazione di ruoli e funzionalità ha esito negativo per la funzionalità Console di gestione IIS di Windows Server 2016
- La ricerca di immagini del sistema operativo nella sequenza di attività di aggiornamento ha esito negativo quando si usano le cartelle
- Lo strumento di MDT esegue il provisioning del TPM in modo non corretto nello stato con funzionalità ridotte. Per altre informazioni, vedere [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- Aggiornamenti alla logica di rilevamento del tipo di chassis ZTIGather
- Il passaggio di aggiornamento del sistema operativo non include SetupComplete.cmd, impedendo le distribuzioni future
- Problemi di avvio UEFI in Windows 10 ADK 1607 e versioni successive per alcuni componenti hardware
- Include i file binari della sequenza di attività di Configuration Manager aggiornati



## <a name="supported-platforms"></a>Piattaforme supportate

Le versioni di MDT non sono più contrassegnate con l'anno o l'aggiornamento della versione. Per un migliore allineamento con i Current Branch di Windows 10 e Configuration Manager e per semplificare il processo di personalizzazione e rilascio, ora la denominazione è solo **Microsoft Deployment Toolkit**. Per distinguere ogni versione, viene usato il numero di build. Ad esempio, la build più recente disponibile per il download è la 8450.

A differenza di Configuration Manager per cui esiste una pianificazione di rilascio predeterminata, MDT viene rilasciato solo su richiesta per supportare le nuove versioni di Windows 10, Windows ADK o Configuration Manager Current Branch. Eventuali problemi noti con questi componenti verranno documentati in questo articolo in base alle esigenze.

Le versioni del sistema operativo seguenti sono supportate per la distribuzione con MDT:
- Windows 10, versione 1803
- Windows 10, versione 1709
- Altre [versioni supportate](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) di Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>Prerequisiti

MDT richiede i componenti seguenti, inclusi in Windows:
- Microsoft .NET Framework 4.0
- Windows PowerShell versione 3.0

Usare la versione più recente di [Windows ADK per Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install). 

> [!Note]  
> È consigliato l'uso della versione di Windows ADK corrispondente alla versione di Windows che si vuole distribuire. Ad esempio, usare Windows ADK per Windows 10 versione 1703 per la distribuzione di Windows 10 versione 1703. Per altre informazioni sul supporto del componente Windows ADK, vedere [Piattaforme supportate di Gestione e manutenzione immagini distribuzione](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisiti USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1).

Quando si esegue l'integrazione di MDT con Configuration Manager per gli scenari ZTI e UDI, usare la versione più recente di Configuration Manager Current Branch.



## <a name="upgrading-mdt"></a>Aggiornamento di MDT

Il processo di installazione di MDT rimuove tutte le istanze esistenti di MDT installate nello stesso computer. Durante il processo vengono mantenuti le condivisioni di distribuzione, i punti di distribuzione e i database. Al termine dell'installazione, è necessario aggiornarli.

La versione corrente di MDT supporta l'aggiornamento dalle versioni seguenti di MDT:
- MDT build 8443

> [!Tip]  
> Creare un backup dell'infrastruttura di MDT esistente prima di tentare di eseguire un aggiornamento.

### <a name="lti"></a>LTI
Dopo aver installato MDT, aggiornare una condivisione di distribuzione esistente eseguendo **Open Deployment Share Wizard** (Procedura guidata apertura condivisione di distribuzione) dal nodo Deployment Shares (Condivisioni di distribuzione) nel Deployment Workbench. Specificare il percorso della directory di condivisione di distribuzione esistente e selezionare la casella di controllo **Aggiorna**. Il processo aggiorna anche le condivisioni di distribuzione di rete e le condivisioni di distribuzione di supporti esistenti, quindi tali condivisioni dovrebbero essere accessibili. Non eseguire l'aggiornamento durante l'esecuzione di distribuzioni, poiché i file in uso possono causare problemi di aggiornamento.

### <a name="zti"></a>ZTI
Le sequenze di attività MDT presenti in Configuration Manager non vengono modificate durante il processo di installazione di MDT. Continuano a funzionare senza alcun problema. Non viene implementato alcun meccanismo per aggiornare le sequenze di attività. Se si vuole usare una delle nuove funzionalità di MDT, creare nuove sequenze di attività integrate con MDT in Configuration Manager.

Quando il processo di aggiornamento è stato completato:  

- Eseguire **Configure ConfigMgr Integration Wizard** (Procedura guidata configurazione integrazione Configuration Manager) dopo l'aggiornamento. Registra i nuovi componenti e installa i modelli di sequenza di attività ZTI aggiornati.  

- Creare un nuovo pacchetto di **file di Microsoft Deployment Toolkit** per tutte le nuove sequenze di attività ZTI create. È possibile usare il pacchetto di file Microsoft Deployment Toolkit esistente per le sequenze di attività ZTI create prima dell'aggiornamento, ma è necessario crearne uno nuovo per le sequenze di attività ZTI nuove.



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>Domande frequenti

#### <a name="whats-the-mdt-support-life-cycle"></a>Che cos'è il ciclo di vita del supporto MDT?  
Per altre informazioni, vedere [Ciclo di vita di supporto Microsoft Deployment Toolkit](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>Questa versione è supportata solo con Windows 10, Windows ADK o Configuration Manager versione *X*?
Questa build di MDT è stata testata principalmente con la configurazione elencata in precedenza. A meno che non vi siano problemi noti espliciti, qualsiasi elemento esterno a tale configurazione ha comunque probabilità elevate di funzionamento. Il ciclo di vita può variare in quanto non sono state testate esplicitamente altre combinazioni.

#### <a name="how-do-i-get-help-with-mdt"></a>Come ottenere assistenza per MDT?
Usare uno dei metodi seguenti per ottenere assistenza con MDT (in ordine di priorità):

1. Postare sul [forum di MDT](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). Gli MVP e altri utenti della community leggono i post e rispondono ai messaggi. Si tratta forse del modo più efficace per avere aiuto.
2. Contattare il supporto tecnico Microsoft. Aprire una richiesta di supporto e ottenere assistenza professionale.
3. Se è possibile riprodurre in modo coerente un problema e si pensa che sia un bug del prodotto, registrarlo nell'[hub di commenti e suggerimenti](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) di Windows 10. Il team del prodotto analizza tutto ciò che viene segnalato. Quando si inserisce un commento o un suggerimento, usare la categoria **Enterprise Management** e la sottocategoria **Distribuzione del sistema operativo**. Questa classificazione consente di classificare e inoltrare commenti e suggerimenti al team di MDT.
     - L'hub di commenti e suggerimenti può essere usato anche per inviare suggerimenti, come ad esempio richieste di modifica di progettazione, per un prodotto.
     - Se in precedenza si è inserito un commento o un suggerimento tramite Connect, non è necessario inserirlo nuovamente nell'hub di commenti e suggerimenti.