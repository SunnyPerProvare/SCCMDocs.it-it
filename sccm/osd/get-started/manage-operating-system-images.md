---
title: Gestire le immagini del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni sui metodi per gestire le immagini del sistema operativo archiviate nei file di immagine di Windows (WIM).
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 700a9d8f88c64e11449349ace8c431b4ad6611cf
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456176"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gestire le immagini del sistema operativo con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le immagini del sistema operativo in Configuration Manager sono archiviate nel formato file di immagine di Windows (WIM). Queste immagini sono una raccolta compressa dei file e delle cartelle di riferimento usati per installare e configurare un nuovo sistema operativo in un computer. Molti scenari di distribuzione del sistema operativo richiedono un'immagine del sistema operativo. 

È possibile usare un'[immagine del sistema operativo predefinita](#default-image) o crearne una da un [computer di riferimento](#bkmk_capture) configurato dall'utente. Quando si configura il computer di riferimento, si aggiungono al sistema operativo i file del sistema operativo e driver, file di supporto, aggiornamenti software, strumenti ed applicazioni. Quindi si acquisisce il sistema operativo per creare il file immagine. 

### <a name="default-image"></a>Immagine predefinita

I file di installazione di Windows includono l'immagine del sistema operativo predefinita. Questa immagine è un'immagine del sistema operativo di base, che contiene un set di driver standard. Quando si usa l'immagine del sistema operativo predefinita, usare i passaggi della sequenza di attività per installare le app e aggiungere altre configurazioni dopo l'installazione del sistema operativo in un dispositivo. Individuare l'immagine del sistema operativo predefinita nei file di origine di Windows: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Vantaggi dell'immagine predefinita

- Le dimensioni dell'immagine sono minori di quelle di un'immagine acquisita.  

- L'installazione di app e l'esecuzione di configurazioni con i passaggi di una sequenza di attività sono operazioni più dinamiche. Ad esempio è possibile modificare le configurazioni e le app installate nella sequenza di attività, senza dover ricreare l'immagine del dispositivo.  

#### <a name="default-image-disadvantages"></a>Svantaggi dell'immagine predefinita

- L'installazione del sistema operativo può richiedere più tempo. L'installazione delle applicazioni e altre configurazioni si verificano al termine dell'installazione del sistema operativo.  


### <a name="bkmk_capture"></a> Immagine acquisita da un computer di riferimento

Per creare un'immagine del sistema operativo personalizzata, creare un computer di riferimento con il sistema operativo desiderato. Quindi installare le applicazioni e configurare le impostazioni desiderate. Acquisire l'immagine del sistema operativo dal computer di riferimento per creare il file con estensione wim. Creare manualmente il computer di riferimento oppure usare una sequenza di attività per automatizzare alcune o tutte le istruzioni di creazione. Per altre informazioni, vedere [Customize OS images](/sccm/osd/get-started/customize-operating-system-images) (Personalizzare le immagini del sistema operativo).  

#### <a name="captured-image-advantages"></a>Vantaggi dell'immagine acquisita

- L'installazione può essere più rapida rispetto all'uso dell'immagine predefinita. Ad esempio è possibile preinstallare le applicazioni con l'immagine acquisita del sistema operativo. Quindi non è necessario installare le stesse applicazioni in un secondo momento usando i passaggi della sequenza di attività.  

#### <a name="captured-image-disadvantages"></a>Svantaggi dell'immagine predefinita

- Le dimensioni dell'immagine sono potenzialmente maggiori di quelle dell'immagine predefinita.  

- Se sono necessari aggiornamenti per le applicazioni e gli strumenti, sarà necessario creare una nuova immagine.  



##  <a name="BKMK_AddOSImages"></a> Aggiungere un'immagine del sistema operativo  

Prima di poter usare un'immagine del sistema operativo, è necessario aggiungerla al sito di Configuration Manager. 

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Immagini del sistema operativo**.  

2.  Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi immagine del sistema operativo**. Questa azione avvia l'Aggiunta guidata immagine del sistema operativo.  

3.  Nella pagina **Origine dati** specificare il **Percorso** di rete del file immagine del sistema operativo. Ad esempio, `\\server\share\path\image.wim`.  

4.  Nella pagina **Generale** specificare le informazioni seguenti. Queste informazioni sono utili per scopi di identificazione quando sono presenti più immagini del sistema operativo.  

    -   **Nome**: nome univoco per l'immagine. Per impostazione predefinita il nome deriva dal nome del file con estensione wim.  

    -   **Versione**: identificatore di versione facoltativo. Questa proprietà non deve corrispondere alla versione del sistema operativo dell'immagine. Si tratta spesso della versione assegnata dall'organizzazione al pacchetto.   

    -   **Commento**: breve descrizione facoltativa.  

5.  Completare la procedura guidata.  


Quindi distribuire l'immagine del sistema operativo ai punti di distribuzione.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuire contenuti ai punti di distribuzione  

Distribuire le immagini del sistema operativo nei punti di distribuzione, con le stesse modalità usate per altri contenuti. Prima di distribuire la sequenza di attività, distribuire l'immagine del sistema operativo ad almeno un punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



##  <a name="BKMK_OSImageMulticast"></a> Preparare l'immagine del sistema operativo per le distribuzioni multicast  

Usare le distribuzioni multicast per consentire a più computer di scaricare simultaneamente un'immagine del sistema operativo. Il punto di distribuzione esegue il multicast dell'immagine nei client e, evitando che ogni client scarichi una copia dell'immagine dal punto di distribuzione con una connessione separata. Quando si sceglie come metodo di distribuzione del sistema operativo l'[uso del multicast per distribuire Windows in rete](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network), configurare l'immagine del sistema operativo in modo che supporti il multicast. Quindi distribuire l'immagine ai punti di distribuzione abilitati per il multicast. 

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Immagini del sistema operativo**.  

2.  Selezionare l'immagine del sistema operativo che si desidera distribuire a un punto di distribuzione abilitato per il multicast.  

3.  Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

4.  Passare alla scheda **Impostazioni distribuzione** e configurare le seguenti opzioni:  

    -   **Consenti trasferimento del pacchetto via multicast (solo WinPE)**: selezionare questa opzione per abilitare la distribuzione simultanea delle immagini del sistema operativo da parte di Configuration Manager tramite multicast.  

    -   **Crittografa pacchetti multicast**: specifica se il sito crittografa l'immagine prima di inviarla al punto di distribuzione. Usare questa opzione se l'immagine contiene informazioni riservate. Se l'immagine non è crittografata, il relativo contenuto è visibile in rete come testo non crittografato. Un utente non autorizzato può intercettare e visualizzare il contenuto dell'immagine.  

    -   **Trasferisci il pacchetto solo via multicast**: Specificare se si desidera che il punto di distribuzione distribuisca l'immagine solo durante una sessione multicast.  

         Se si seleziona l'opzione **Trasferisci il pacchetto solo via multicast**, è necessario specificare anche l'opzione di distribuzione della sequenza attività **Scaricare il contenuto localmente quando necessario eseguendo la sequenza attività**. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).   

5.  Selezionare **OK** per salvare le impostazioni e chiudere le proprietà dell'immagine.  
