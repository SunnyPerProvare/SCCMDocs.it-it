---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/27/2018
ms.openlocfilehash: c91cf0abb8cb79fe92e34b6b234a4c8264af75ab
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456941"
---
##  <a name="BKMK_OSImagesApplyUpdates"></a> Applicare aggiornamenti software a un'immagine  

> [!Note]  
> Questa sezione si applica sia alle **immagini del sistema operativo** sia ai **pacchetti di aggiornamento del sistema operativo**. Il termine generale "immagine" viene usato per fare riferimento al file di immagine Windows (WIM). Entrambi questi oggetti prevedono un file WIM, che contiene i file di installazione di Windows. Gli aggiornamenti software sono applicabili a questi file in entrambi gli oggetti. Il comportamento di questo processo è uguale in entrambi gli oggetti.  

Ogni mese sono disponibili nuovi aggiornamenti software applicabili all'immagine. Prima di poter applicare gli aggiornamenti software all'immagine, sono necessari i prerequisiti seguenti: 

- Infrastruttura di aggiornamento del software  
- Aggiornamenti software sincronizzati correttamente  
- Aggiornamenti software scaricati nella raccolta contenuto nel server del sito  

Per altre informazioni, vedere [Distribuire gli aggiornamenti software](/sccm/sum/deploy-use/deploy-software-updates).  

Applicare gli aggiornamenti software applicabili a un'immagine in base a una pianificazione specificata. Questo processo viene talvolta chiamato *installazione offline*. In questa pianificazione, Configuration Manager applica gli aggiornamenti software selezionati all'immagine. È quindi possibile ridistribuire anche l'immagine aggiornata ai punti di distribuzione. 

Le informazioni sull'immagine, inclusi gli aggiornamenti software applicati al momento dell'importazione, vengono archiviate nel database del sito. Anche gli aggiornamenti software applicati all'immagine dopo che è stata inizialmente aggiunta vengono archiviati nel database del sito. Quando si avvia la procedura guidata per applicare gli aggiornamenti software, viene recuperato l'elenco degli aggiornamenti software applicabili che il sito non ha ancora applicato all'immagine. Configuration Manager copia gli aggiornamenti software selezionati dalla raccolta contenuto nel server del sito. Gli aggiornamenti software vengono quindi applicati all'immagine.  


### <a name="servicing-process"></a>Processo di manutenzione  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Immagini del sistema operativo** o **Pacchetti di aggiornamento del sistema operativo**.  

2.  Selezionare l'oggetto a cui applicare gli aggiornamenti software.  

3.  Selezionare **Pianifica aggiornamenti** sulla barra multifunzione per avviare la procedura guidata.  

4.  Nella pagina **Scegli aggiornamenti** selezionare gli aggiornamenti software da applicare all'immagine. Potrebbe essere necessario qualche minuto prima che l'elenco degli aggiornamenti venga visualizzato nella procedura guidata. Usare il **Filtro** per cercare stringhe nei metadati. Usare l'elenco a discesa **Architettura di sistema** per applicare il filtro in base a **X86**, **X64** o **Tutti**. È possibile selezionare uno, molti o tutti gli aggiornamenti nell'elenco. Dopo aver completato la selezione degli aggiornamenti, selezionare **Avanti**.  

5.  Nella pagina **Imposta pianificazione** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    a.  **Pianificazione**: specificare il momento in cui si vuole che il sito applichi gli aggiornamenti software all'immagine.  

    b.  **Continua in caso di errore**: selezionare questa opzione per continuare ad applicare gli aggiornamenti software all'immagine anche quando si verifica un errore.  

    c.  **Aggiorna punti di distribuzione con l'immagine**: selezionare questa opzione per aggiornare l'immagine nei punti di distribuzione dopo che il sito ha applicato gli aggiornamenti software.  

6.  Completare la procedura guidata pianificazione aggiornamenti.  

> [!NOTE]  
>  Per ridurre al minimo le dimensioni del payload, il processo di manutenzione dei pacchetti di aggiornamento del sistema operativo e delle immagini del sistema operativo rimuove la versione precedente.  


### <a name="servicing-operations"></a>Operazioni di manutenzione

Nel nodo **Immagini sistema operativo** o **Pacchetti di aggiornamento del sistema operativo** della console di Configuration Manager aggiungere le colonne seguenti alla visualizzazione:
- **Data aggiornamenti pianificati**: questa proprietà indica la pianificazione successiva definita.  
- **Stato aggiornamenti pianificati**: questa proprietà indica lo stato. Ad esempio, **Completato** oppure **In elaborazione**.  

Selezionare un oggetto immagine specifico e quindi passare alla scheda **Stato aggiornamento** nel riquadro dei dettagli. In questa scheda viene visualizzato l'elenco degli aggiornamenti nell'immagine. 

Selezionare un pacchetto immagine specifico e selezionare **Proprietà** nella barra multifunzione. La scheda **Aggiornamenti installati** indica l'elenco degli aggiornamenti nell'immagine. La scheda **Manutenzione** offre una vista di sola lettura della pianificazione di manutenzione corrente e gli aggiornamenti pianificati da applicare. 

Quando lo stato è **In elaborazione**, è possibile selezionare **Annulla aggiornamenti pianificati** sulla barra multifunzione. L'azione annulla il processo di manutenzione attivo. 

Per risolvere i problemi di questo processo, visualizzare i file **OfflineServicingMgr.log** e **dism.log** nel server del sito. Per altre informazioni, vedere [File di log](/sccm/core/plan-design/hierarchy/log-files).


### <a name="bkmk_servicing-drive"></a> Specificare l'unità per la manutenzione di immagini del sistema operativo offline  
<!--1358924-->

A partire dalla versione 1810, specificare l'unità usata da Configuration Manager durante la manutenzione offline delle immagini del sistema operativo. Questo processo può occupare una grande quantità di spazio su disco con i file temporanei. Questa opzione la flessibilità di poter selezionare l'unità da usare. 

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Sulla barra multifunzione fare clic su **Configura componenti del sito** e selezionare **Distribuzione del sistema operativo**.  

2. Nella scheda **Installazione offline** specificare l'opzione per **Unità locale che deve essere usata dall'installazione offline delle immagini:**.  

L'impostazione predefinita di questa opzione è **Automatic** (Automatica). Con questo valore, Configuration Manager seleziona l'unità in cui è installato. 

Se si seleziona un'unità che non esiste nel server del sito, Configuration Manager si comporta come se fosse selezionata l'opzione **Automatica**. 

Durante l'installazione offline, Configuration Manager archivia i file temporanei nella cartella `<drive>:\ConfigMgr_OfflineImageServicing` e monta anche l'immagine del sistema operativo in questa cartella. 

