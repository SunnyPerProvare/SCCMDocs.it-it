---
title: Gestire i pacchetti di aggiornamento del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni su come gestire i pacchetti di aggiornamento del sistema operativo in Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7b8b18cbec5a3b5972a448e8a70339533dc11fb
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456007"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gestire i pacchetti di aggiornamento del sistema operativo in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un pacchetto di aggiornamento in Configuration Manager contiene i file di origine dell'installazione di Windows per l'aggiornamento di un sistema operativo esistente in un computer. Questo articolo descrive come aggiungere, distribuire e gestire un pacchetto di aggiornamento del sistema operativo.



##  <a name="BKMK_AddOSUpgradePkgs"></a> Aggiungere pacchetto di aggiornamento del sistema operativo  

Prima di poter usare un pacchetto di aggiornamento del sistema operativo, è necessario aggiungerlo al sito di Configuration Manager. 

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Pacchetti di aggiornamento del sistema operativo**.  

2.  Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi pacchetto di aggiornamento del sistema operativo**. Questa azione avvia l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

3.  Nella pagina **Origine dati** specificare le impostazioni seguenti: 

    - In **Percorso** specificare il percorso di rete dei file di origine per l'installazione del pacchetto di aggiornamento del sistema operativo. Ad esempio, `\\server\share\path`.  

        > [!NOTE]  
        >  I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

        > [!IMPORTANT]  
        >  Limitare l'accesso a questi file di origine dell'installazione per impedire manomissioni indesiderate.  

    - Se si desidera memorizzare in anteprima contenuto nella cache in un client, specificare **Architettura** e **Lingua** dell'immagine. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  Nella pagina **Generale** specificare le informazioni seguenti. Queste informazioni sono utili per scopi di identificazione quando sono presenti più pacchetti di aggiornamento del sistema operativo.  

    -   **Nome**: nome univoco del pacchetto di aggiornamento per il sistema operativo.  

    -   **Versione**: identificatore di versione facoltativo. Questa proprietà non deve corrispondere alla versione del sistema operativo del pacchetto di aggiornamento. Si tratta spesso della versione assegnata dall'organizzazione al pacchetto.  

    -   **Commento**: breve descrizione facoltativa.  

5.  Completare la procedura guidata.  


Quindi distribuire il pacchetto di aggiornamento del sistema operativo ai punti di distribuzione.  



##  <a name="BKMK_Distribute"></a> Distribuire il contenuto a un punto di distribuzione  

Distribuire i pacchetti di aggiornamento del sistema operativo nei punti di distribuzione, con le stesse modalità usate per altri contenuti. Prima di distribuire la sequenza di attività, distribuire il pacchetto di aggiornamento del sistema operativo ad almeno un punto di distribuzione. Per altre informazioni, vedere [Distribuire il contenuto](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>Passaggi successivi

[Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)