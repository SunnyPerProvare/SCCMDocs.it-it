---
title: "Creare una sequenza di attività per aggiornare un sistema operativo | Microsoft Docs"
description: "Usare le sequenze di attività in System Center Configuration Manager per aggiornare automaticamente un sistema operativo da Windows 7 o versione successiva a Windows 10."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 32af7da62bfe767a21a891338bd778ebf45f2685


---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Creare una sequenza di attività per aggiornare un sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività in System Center Configuration Manager per aggiornare automaticamente un sistema operativo da Windows 7 o versione successiva a Windows 10 su un computer di destinazione. Creare una sequenza attività che faccia riferimento all'immagine del sistema operativo da installare nel computer di destinazione ed eventuale contenuto aggiuntivo, ad esempio applicazioni o aggiornamenti software che si desidera installare. La sequenza di attività per aggiornare un sistema operativo fa parte dello scenario [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md).  

##  <a name="a-namebkmkupgradeosa-create-a-task-sequence-to-upgrade-an-operating-system"></a><a name="BKMK_UpgradeOS"></a> Creare una sequenza di attività per aggiornare un sistema operativo  
 Per aggiornare il sistema operativo nei computer a Windows 10, è possibile creare una sequenza di attività e selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** nella Creazione guidata della sequenza di attività. La procedura guidata aggiungerà i passaggi per aggiornare il sistema operativo, applicare gli aggiornamenti software e installare le applicazioni. Prima di creare la sequenza di attività, devono essere disponibili gli elementi seguenti:  

-   **Richiesto**  

     - Il [pacchetto di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) Windows 10 deve essere disponibile nella console di Configuration Manager.  

-   **Obbligatorio (se usato)**  

    -   Gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md) devono essere sincronizzati nella console di Configuration Manager.  

    -   Le [applicazioni](../../apps/deploy-use/create-applications.md) devono essere aggiunte alla console di Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Per creare una sequenza di attività che esegua l'aggiornamento di un sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** fare clic su **Aggiorna sistema operativo dal pacchetto di aggiornamento**e quindi fare clic su **Avanti**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifica la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione dell'attività eseguita dalla sequenza di attività.  

6.  Nella pagina **Aggiorna il sistema operativo Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo. È possibile verificare di avere selezionato il pacchetto di aggiornamento corretto esaminando le informazioni nel riquadro **Proprietà** . Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Indice edizione**: se sono presenti più indici edizione del sistema operativo nel pacchetto, selezionare l'indice edizione desiderato. Per impostazione predefinita, viene selezionato il primo elemento.  

    -   **Codice Product Key**: specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di 5 caratteri deve essere separato da un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX* Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key non è obbligatorio. Il codice Product Key è necessario solo quando l'aggiornamento è per un'edizione di Windows al dettaglio.  

7.  Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software e quindi fare clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

8.  Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

9. Completare la procedura guidata.  

## <a name="download-package-content-task-sequence-step"></a>Passaggio della sequenza di attività Scaricare il contenuto del pacchetto  
 Il passaggio [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) può essere usato prima del passaggio **Aggiorna sistema operativo** negli scenari seguenti:  

-   Si utilizza una singola sequenza di attività di aggiornamento che può funzionare con piattaforme x86 e x64. Per portare a termine la procedura, è necessario includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento** con le condizioni per rilevare l'architettura client e scaricare solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il valore **Contenuto preconfigurato** durante il passaggio **Aggiorna sistema operativo** .  

   > [!NOTE]
   > Quando sono presenti più pacchetti, Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, se si specifica una variabile %mycontent% come variabile personalizzata, questa è la radice in cui è archiviato tutto il contenuto di riferimento (può trattarsi anche di più pacchetti). Quando si fa riferimento alla variabile in un passaggio secondario della sequenza, ad esempio Aggiorna sistema operativo, viene usata con un suffisso numerico. In questo esempio, %mycontent01% o %mycontent02% , dove il numero corrisponde all'ordine di elencazione del pacchetto in questo passaggio.

## <a name="optional-post-processing-task-sequence-steps"></a>Passaggi della sequenza attività di post-elaborazione facoltativi  
 Dopo aver creato la sequenza di attività, è possibile aggiungere ulteriori passaggi per disinstallare le applicazioni con problemi di compatibilità noti o aggiungere azioni post-elaborazione da eseguire dopo il riavvio del computer e il corretto aggiornamento a Windows 10. Aggiungere questi passaggi aggiuntivi nel gruppo Post-elaborazione della sequenza di attività.  

> [!NOTE]  
>  Poiché questa sequenza di attività non è lineare, esistono condizioni sui passaggi che possono influenzare i risultati della sequenza di attività, a seconda che venga aggiornato correttamente il computer client o che sia necessario ripristinare il computer client alla versione del sistema operativo precedente.  

## <a name="optional-rollback-task-sequence-steps"></a>Passaggi della sequenza attività di rollback facoltativi  
 Quando si verificano problemi nel processo di aggiornamento dopo il riavvio del computer, il programma di installazione eseguirà il rollback dell'aggiornamento al sistema operativo precedente e la sequenza di attività continuerà con tutti i passaggi nel gruppo Rollback. Dopo aver creato la sequenza di attività, è possibile aggiungere passaggi facoltativi al gruppo Rollback.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Cartelle e file vengono rimossi dopo il riavvio del computer  
 Quando la sequenza di attività per eseguire l'aggiornamento di un sistema operativo a Windows 10 e tutti gli altri passaggi della sequenza di attività sono stati completati, gli script di post-elaborazione e di rollback non vengono rimossi fino a quando non viene riavviato il computer.  Questi file di script non contengono informazioni riservate.  



<!--HONumber=Dec16_HO3-->


