---
title: 'Creare supporti di acquisizione '
titleSuffix: Configuration Manager
description: "Usare la Creazione guidata del supporto per la sequenza di attività per creare supporti di acquisizione in Configuration Manager per acquisire un'immagine del sistema operativo da un computer di riferimento."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c25eade287d254907c7d7d02948eb25a88ed0a11
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Creare supporti di acquisizione con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il supporto di acquisizione in Configuration Manager consente di acquisire un'immagine del sistema operativo da un computer di riferimento. Usare i supporti di acquisizione per lo scenario seguente:  

-   [Creare una sequenza di attività per acquisire un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> Come creare supporti di acquisizione  
 Usare il supporto di acquisizione per acquisire un'immagine del sistema operativo da un computer di riferimento. Il supporto di acquisizione contiene l'immagine di avvio che avvia il computer di riferimento e la sequenza di attività che acquisisce l'immagine del sistema operativo.

Per creare i supporti di acquisizione, usare la Creazione guidata del supporto per la sequenza di attività. Prima di eseguire la procedura guidata, verificare che siano soddisfatte tutte le condizioni seguenti:  

|Attività|Descrizione|  
|----------|-----------------|  
|Immagine d'avvio|Tenere presente quanto segue per l'immagine d'avvio da usare nella sequenza di attività per acquisire il sistema operativo:<br /><br /> - L'architettura dell'immagine di avvio deve essere appropriata per l'architettura del computer di destinazione. Ad esempio, un computer di destinazione x64 può avviare ed eseguire un'immagine d'avvio x86 o x64. Tuttavia, un computer di destinazione x86 può avviare ed eseguire solo un'immagine di avvio x86.<br />- Verificare che l'immagine di avvio contenga i driver di archiviazione di rete e di massa necessari per eseguire il provisioning del computer di destinazione.|  
|Distribuire tutto il contenuto associato alla sequenza di attività|È necessario distribuire in almeno un punto di distribuzione tutto il contenuto richiesto dalla sequenza di attività. Ciò include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie le informazioni dal punto di distribuzione quando viene creato il supporto autonomo. È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nel punto di distribuzione.  Per altre informazioni, vedere [Distribuire il contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Preparare l'unità USB rimovibile|Per un'unità USB rimovibile:<br /><br /> Se si usa un'unità USB rimovibile, l'unità deve essere collegata al computer in cui viene eseguita la procedura guidata e rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto.|  
|Creare una cartella di output|Per un set di CD/DVD:<br /><br /> Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, è necessario creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.|  

 Usare la procedura seguente per creare supporti di acquisizione.  

#### <a name="to-create-capture-media"></a>Per creare supporti di acquisizione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4.  Nella pagina **Seleziona tipo di supporto** selezionare **Acquisisci supporto**, quindi fare clic su **Avanti**.  

5.  Nella pagina **Tipo di supporto** specificare se il supporto è un'unità flash o un set di CD/DVD, quindi configurare quanto segue:  

    -   Se si seleziona **Unità memoria flash USB**, è necessario specificare l'unità in cui archiviare il contenuto.  

    -   Se si seleziona l'opzione **CD/DVD impostato**, specificare la capacità del supporto e il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. Ad esempio: **\\\nomeserver\cartella\filedioutput.iso**  

         Se la capacità del supporto non è sufficiente per archiviare l'intero contenuto, vengono creati più file ed è necessario archiviare il contenuto in più CD o DVD. Quando sono necessari più supporti, Configuration Manager aggiunge un numero di sequenza al nome di ogni file di output creato. Se insieme al sistema operativo si distribuisce un'applicazione e questa non può essere contenuta in un unico supporto, Configuration Manager archivia l'applicazione in più supporti. Quando il supporto autonomo viene eseguito Configuration Manager chiede all'utente il supporto successivo contenente l'applicazione.  

        > [!IMPORTANT]  
        >  Se si seleziona un'immagine iso esistente, la Creazione guidata del supporto per la sequenza di attività elimina l'immagine dall'unità o dalla condivisione non appena si passa alla pagina successiva della procedura guidata. L'immagine esistente viene eliminata, anche se si annulla la procedura guidata.  

     Fare clic su **Avanti**.  

6.  Nella pagina **Immagine di avvio** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  L'architettura dell'immagine di avvio specificata deve essere appropriata per l'architettura del computer di riferimento. Ad esempio, un computer di riferimento x64 può avviare ed eseguire un'immagine di avvio x86 o x64. Tuttavia, un computer di riferimento x86 può avviare ed eseguire solo un'immagine di avvio x86.  

    -   Nella casella **Immagine di avvio** specificare l'immagine di avvio per avviare il computer di riferimento.  

    -   Nella casella **Punto di distribuzione** specificare il punto di distribuzione in cui si trova l'immagine di avvio. La procedura guidata consente di recuperare l'immagine di avvio dal punto di distribuzione e di scriverla sul supporto.  

        > [!NOTE]  
        >  È necessario disporre dei diritti di accesso in lettura alla raccolta contenuto nel punto di distribuzione.  

7.  Completare la procedura guidata.  
