---
title: Gestire le immagini del sistema operativo | Documentazione Microsoft
description: "Informazioni sui metodi disponibili in Configuration Manager che è possibile usare per gestire le immagini del sistema operativo archiviate nei file Windows Imaging (WIM)."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6953c3834ca303b949f22436010a87b3da9688dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Gestire le immagini del sistema operativo con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le immagini del sistema operativo in Configuration Manager vengono archiviate in file in formato Windows Imaging (WIM) e rappresentano una raccolta compressa dei file e delle cartelle di riferimento necessari per installare e configurare correttamente un sistema operativo in un computer. Per tutti gli scenari di distribuzione del sistema operativo, è necessario selezionare un'immagine del sistema operativo.   È possibile usare l'immagine del sistema operativo predefinita o crearne una da un computer di riferimento configurato. Quando si crea il computer di riferimento, è possibile aggiungere al sistema operativo file del sistema operativo, driver, file di supporto, aggiornamenti software, strumenti e altre applicazioni software prima di acquisirlo per creare il file di immagine. Di seguito sono elencate le informazioni su ogni metodo.  

 **Immagine predefinita**  

 L'immagine del sistema operativo predefinita, install.wim, è inclusa con i file di installazione del sistema operativo Windows. Questa immagine del sistema operativo è un'immagine di base che contiene un set standard di driver. Quando si usa l'immagine del sistema operativo predefinita, è possibile installare app ed eseguire altre configurazioni dopo l'installazione del sistema operativo usando passaggi della sequenza di attività.  L'immagine del sistema operativo predefinita si trova in <*percorso di origine del sistema operativo*>\Sources\install.wim.  

-   **Vantaggi**  

    -   Le dimensioni dell'immagine sono minori di quelle di un'immagine acquisita.  

    -   L'installazione di app e l'esecuzione di configurazioni con i passaggi di una sequenza di attività sono operazioni più dinamiche. Ad esempio, è possibile modificare le app da installare e le configurazioni nella sequenza di attività senza dover ricreare l'immagine del sistema operativo.  

-   **Svantaggi**  

    -   L'installazione del sistema operativo può richiedere più tempo, perché l'installazione delle app e le altre configurazioni vengono eseguite al termine dell'installazione del sistema operativo.  

 **Immagine acquisita**  

 Per creare un'immagine del sistema operativo personalizzata, è necessario creare un computer di riferimento con il sistema operativo desiderato e installare le app, configurare le impostazioni e così via. Quindi, è possibile acquisire l'immagine del sistema operativo dal computer di riferimento per creare il file WIM. È possibile creare manualmente il computer di riferimento o usare una sequenza di attività per automatizzare alcune o tutte le istruzioni di generazione.   
Per informazioni sui passaggi necessari per creare un'immagine del sistema operativo personalizzata, vedere [Personalizzare le immagini del sistema operativo](customize-operating-system-images.md).  

-   **Vantaggi**  

    -   L'installazione può essere più rapida rispetto all'uso dell'immagine predefinita. Ad esempio, le app possono essere preinstallate con l'immagine del sistema operativo acquisita e non sarà necessario installare app in seguito seguendo i passaggi di una sequenza di attività.  

-   **Svantaggi**  

    -   L'installazione del sistema operativo può richiedere più tempo, perché l'installazione delle app e le altre configurazioni vengono eseguite al termine dell'installazione del sistema operativo.  


##  <a name="BKMK_AddOSImages"></a> Aggiungere immagini del sistema operativo a Configuration Manager  
 Prima di poter usare un'immagine del sistema operativo, è necessario aggiungere l'immagine a un sito di Configuration Manager. Usare la procedura seguente per aggiungere un'immagine del sistema operativo a un sito.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>Per aggiungere un'immagine del sistema operativo a un sito  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini del sistema operativo**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi immagine del sistema operativo** per avviare l'Aggiunta guidata immagine del sistema operativo.  

4.  Nella pagina **Origine dati** specificare il percorso di rete dell'immagine del sistema operativo. Ad esempio, specificare **\\\server\percorso\sistemaoperativo.WIM**.  

5.  Nella pagina **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**. Queste informazioni sono utili per scopi di identificazione quando si aggiungono più immagini del sistema operativo allo stesso sito.  

    -   **Nome**: specificare il nome dell'immagine. Per impostazione predefinita, il nome dell'immagine viene ricavato dal file WIM.  

    -   **Versione**: specificare la versione dell'immagine.  

    -   **Commento**: specificare una breve descrizione dell'immagine.  

6.  Completare la procedura guidata.  

 È ora possibile distribuire l'immagine del sistema operativo nei punti di distribuzione.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuire immagini del sistema operativo nei punti di distribuzione  
 Le immagini del sistema operativo vengono distribuite nei punti di distribuzione allo stesso modo in cui vengono distribuiti gli altri contenuti. Nella maggior parte dei casi, è necessario distribuire l'immagine del sistema operativo almeno in un punto di distribuzione prima di distribuire il sistema operativo. Per informazioni sui passaggi necessari per distribuire un'immagine del sistema operativo, vedere [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="BKMK_OSImagesApplyUpdates"></a> Applicare aggiornamenti software a un'immagine del sistema operativo  
 Periodicamente, vengono rilasciati nuovi aggiornamenti software applicabili al sistema operativo nell'immagine del sistema operativo. Prima di poter applicare aggiornamenti software a un'immagine, è necessario che l'infrastruttura degli aggiornamenti software sia già predisposta, che gli aggiornamenti software siano stati sincronizzati correttamente e che gli aggiornamenti software siano stati scaricati nella raccolta contenuto nel server del sito. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md).  

 È possibile applicare gli aggiornamenti software applicabili a un'immagine in base a una pianificazione specificata. Nella pianificazione specificata, Configuration Manager applica gli aggiornamenti software selezionati all'immagine del sistema operativo e poi, facoltativamente, distribuisce l'immagine aggiornata ai punti di distribuzione. Le informazioni sull'immagine del sistema operativo, inclusi gli aggiornamenti software applicati al momento dell'importazione, vengono archiviate nel database del sito. Anche gli aggiornamenti software applicati all'immagine dopo che è stata aggiunta vengono archiviati nel database del sito. Quando si avvia la procedura guidata per applicare gli aggiornamenti software all'immagine del sistema operativo, tale procedura recupera un elenco di aggiornamenti software applicabili non ancora applicati all'immagine da selezionare. Configuration Manager copia gli aggiornamenti software dalla raccolta contenuto al server del sito e li applica all'immagine del sistema operativo.  

 Utilizzare la seguente procedura per applicare gli aggiornamenti software a un'immagine del sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>Per applicare aggiornamenti software a un'immagine del sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini del sistema operativo**.  

3.  Selezionare l'immagine del sistema operativo a cui applicare gli aggiornamenti software.  

4.  Nella scheda **Home** , nel gruppo **Immagine del sistema operativo** , fare clic su **Pianifica aggiornamenti** per avviare la procedura guidata.  

5.  Nella pagina **Scegli aggiornamenti** selezionare gli aggiornamenti software da applicare all'immagine del sistema operativo e quindi fare clic su **Avanti**.  

6.  Nella pagina **Imposta pianificazione** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    1.  **Pianificazione**: specificare la pianificazione per l'applicazione degli aggiornamenti software all'immagine del sistema operativo.  

    2.  **Continua in caso di errori**: selezionare questa opzione per continuare ad applicare gli aggiornamenti software all'immagine anche quando si verifica un errore.  

    3.  **Distribuisci l'immagine nei punti di distribuzione**: selezionare questa opzione per aggiornare l'immagine del sistema operativo nei punti di distribuzione una volta applicati gli aggiornamenti software.  

7.  Nella pagina **Riepilogo** verificare le informazioni e quindi fare clic su **Avanti**.  

8.  Nella pagina **Completamento** verificare che gli aggiornamenti software siano stati applicati correttamente all'immagine del sistema operativo.  

##  <a name="BKMK_OSImageMulticast"></a> Preparare l'immagine del sistema operativo per le distribuzioni multicast  
 Usare le distribuzioni multicast per consentire a più computer di scaricare simultaneamente un'immagine del sistema operativo. Il punto di distribuzione esegue il multicast dell'immagine nei client e non deve inviare una copia dell'immagine a ogni client con una connessione separata. Quando si sceglie il metodo di distribuzione del sistema operativo [Usare il multicast per distribuire Windows in rete](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), è necessario configurare il pacchetto dell'immagine del sistema operativo in modo che supporti il multicast prima di distribuire l'immagine del sistema operativo in un punto di distribuzione abilitato per il multicast. Utilizzare la seguente procedura per impostare le opzioni di multicast per un pacchetto immagine del sistema operativo esistente.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>Per modificare un pacchetto immagine del sistema operativo per l'utilizzo di multicast  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Immagini del sistema operativo**.  

3.  Selezionare l'immagine del sistema operativo che si desidera distribuire nel punto di distribuzione abilitato per multicast.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Selezionare la scheda **Impostazioni distribuzione** , quindi configurare le seguenti opzioni:  

    -   **Consenti trasferimento del pacchetto via multicast (solo WinPE);**: è necessario selezionare questa opzione per abilitare la distribuzione simultanea delle immagini del sistema operativo da parte di Configuration Manager.  

    -   **Crittografa pacchetti multicast**: Specificare se l'immagine è crittografata prima che venga inviata al punto di distribuzione. Utilizzare questa opzione se il pacchetto contiene informazioni riservate. Se l'immagine non è crittografata, i contenuti del pacchetto saranno visibili nella rete come testo non crittografato e saranno quindi potenzialmente leggibili da parte di utenti non autorizzati.  

    -   **Trasferisci il pacchetto solo via multicast**: Specificare se si desidera che il punto di distribuzione distribuisca l'immagine solo durante una sessione multicast.  

         Se viene selezionata l'opzione **Trasferisci il pacchetto solo via multicast**, è necessario specificare anche **Scaricare il contenuto localmente quando necessario eseguendo la sequenza attività** come opzione di distribuzione per l'immagine del sistema operativo. È possibile specificare le opzioni di distribuzione per l'immagine durante la distribuzione dell'immagine del sistema operativo, oppure è possibile specificarle in seguito modificando le proprietà della distribuzione. Le opzioni di distribuzione si trovano nella scheda **Punti di distribuzione** della pagina **Proprietà** dell'oggetto di distribuzione.  

6.  Fare clic su **OK**.  
