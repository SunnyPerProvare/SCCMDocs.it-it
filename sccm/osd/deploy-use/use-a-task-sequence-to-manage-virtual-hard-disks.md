---
title: "Usare una sequenza di attività per gestire dischi rigidi virtuali | Configuration Manager"
description: "È possibile creare e modificare un disco rigido virtuale, aggiungere applicazioni e aggiornamenti software e pubblicare il disco rigido virtuale in System Center Virtual Machine Manager (VMM) da Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e0ba309d8efc34cccce6acc4c59f0c4d218a617a


---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Usare una sequenza di attività per gestire dischi rigidi virtuali in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager è possibile gestire dischi rigidi virtuali e integrare quelli creati nel data center dalla console di Configuration Manager. In particolare, è possibile creare e modificare un disco rigido virtuale, aggiungere applicazioni e aggiornamenti software al disco e pubblicare il disco in System Center Virtual Machine Manager (VMM) dalla console di Configuration Manager.  

 Usare le seguenti sezioni per gestire dischi rigidi virtuali in Configuration Manager.

## <a name="prerequisites"></a>Prerequisiti  
 Prima di iniziare, verificare che i seguenti prerequisiti siano soddisfatti:  

-   Il computer da cui si gestiscono i dischi rigidi virtuali deve eseguire uno dei seguenti sistemi operativi:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   La virtualizzazione deve essere abilitata nel BIOS e Hyper-V deve essere installato sul computer da cui si esegue la console di Configuration Manager per gestire i dischi rigidi virtuali. Inoltre, è consigliabile installare gli strumenti di gestione di Hyper-V per facilitare la verifica e risolvere problemi dei dischi rigidi virtuali. Ad esempio, per monitorare il file di registro smsts.log per tenere traccia dello stato di avanzamento della sequenza attività in Hyper-V, è necessario che gli strumenti di gestione Hyper-V siano installati. Per ulteriori informazioni sui requisiti di Hyper-V, vedere [Prerequisiti di installazione di Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  Il processo per creare un disco rigido virtuale utilizza risorse del processore. Di conseguenza, si consiglia di gestire i dischi rigidi virtuali da un console di Configuration Manager che non è installata sul server del sito.  

-   Il server del sito deve disporre delle autorizzazioni di accesso in **scrittura** alla cartella che conterrà il file VHD quando si gestiscono dischi rigidi virtuali da un computer remoto rispetto al server del sito.  

-   Verificare di disporre di spazio libero su disco sufficiente nel computer da cui si gestiscono i dischi rigidi virtuali. I requisiti di spazio del disco rigido virtuale variano a seconda del sistema operativo e delle applicazioni installate.  

-   Verificare di disporre di memoria sufficiente nel computer da cui si gestiscono i dischi rigidi virtuali. Durante il processo di creazione del disco rigido virtuale, la macchina virtuale è configurata per utilizzare 2 GB di memoria.  

-   Installare la console di System Center Virtual Machine Manager (VMM) sul computer da cui si carica il disco rigido virtuale in VMM. È possibile installare la console VMM in un computer separato da cui si gestiscono i dischi rigidi virtuali. Questo significa che per importare il disco rigido virtuale in VMM non è necessario che Hyper-V sia installato.  

    > [!NOTE]  
    >  Se si installa la console VMM mentre la console di Configuration Manager è aperta, al termine dell'installazione della console VMM è necessario riavviare la console di Configuration Manager. In caso contrario, Configuration Manager non è in grado di collegarsi al server di gestione VMM per caricare un disco rigido virtuale.  

##  <a name="a-namebkmkcreatevhdstepsa-steps-to-create-a-vhd"></a><a name="BKMK_CreateVHDSteps"></a> Passaggi per la creazione di un disco rigido virtuale  
 Per creare un disco rigido virtuale è necessario creare una sequenza di attività che contiene i passaggi per creare il disco rigido virtuale e quindi utilizzare tale sequenza nella Creazione guidata disco rigido virtuale. Le sezioni seguenti forniscono i passaggi per la creazione del disco rigido virtuale.  

###  <a name="a-namebkmkcreatetsa-create-a-task-sequence-for-the-vhd"></a><a name="BKMK_CreateTS"></a> Creare una sequenza attività per il disco rigido virtuale  
 È necessario creare una sequenza attività contenente i passaggi per creare il disco rigido virtuale. In Creazione guidata della sequenza attività, è disponibile l'opzione **Installa un pacchetto immagine esistente in un disco rigido virtuale** che consente di creare i passaggi da utilizzare per creare il disco rigido virtuale. Ad esempio, la procedura guidata aggiunge i seguenti passaggi obbligatori: Riavvia in Windows PE, Formato e disco partizione, Applica sistema operativo e Arresta computer. Non è possibile creare il disco rigido virtuale nel sistema operativo completo. Configuration Manager deve inoltre rimanere in attesa finché la macchina virtuale non viene arrestata prima di completare il pacchetto. Per impostazione predefinita, la procedura guidata rimane in attesa 5 minuti prima di arrestare la macchina virtuale. Dopo aver creato la sequenza attività, è possibile aggiungere ulteriori passaggi, se richiesto.  

> [!IMPORTANT]  
>  La seguente procedura consente di creare la sequenza attività utilizzando l'opzione **Installa un pacchetto immagine esistente in un disco rigido virtuale** , che consente di includere automaticamente i passaggi richiesti per creare il disco rigido virtuale. Se si sceglie di utilizzare una sequenza attività esistente o di creare manualmente una sequenza attività, accertarsi di aggiungere il passaggio Arresta computer alla fine della sequenza attività. Senza questo passaggio, la macchina virtuale temporanea non viene eliminata e il processo di creazione del disco rigido virtuale non viene completato. La procedura guidata viene, tuttavia, correttamente completata.  

 Utilizzare la seguente procedura per creare la sequenza attività per creare il disco rigido virtuale:  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>Per creare la sequenza attività per creare il disco rigido virtuale  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza attività** fare clic su **Installa un pacchetto immagine esistente in un disco rigido virtuale**, quindi fare clic su **Avanti**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifichi la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione della sequenza di attività.  

    -   **Immagine di avvio**: specificare l'immagine di avvio che installa il sistema operativo nel computer di destinazione. Per altre informazioni, vedere la sezione relativa alla [gestione delle immagini di avvio](../get-started/manage-boot-images.md).  

6.  Nella pagina **Installa Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Pacchetto immagine**: specificare il pacchetto che contiene l'immagine del sistema operativo da installare.  

    -   **Immagine**: se il pacchetto dell'immagine del sistema operativo contiene più immagini, specificare l'indice dell'immagine del sistema operativo da installare.  

    -   **Codice Product Key**: specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di 5 caratteri deve essere separato da un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modalità di gestione licenze del server**: specificare che la licenza del server è **Per postazione**, **Per server**o che non è specificata alcuna licenza. Se la licenza del server è **Per server**, specificare anche il numero massimo di connessioni al server.  

    -   Specificare come gestire l'account amministratore usato quando viene distribuita l'immagine del sistema operativo.  

        -   **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)**: usare questa impostazione per creare una password casuale per l'account amministratore locale e disattivare l'account quando l'immagine del sistema operativo viene distribuita.  

        -   **Attiva l'account e specifica la password dell'amministratore locale**: usare questa impostazione per usare una password specifica per l'account amministratore locale in tutti i computer in cui viene distribuita l'immagine del sistema operativo.  

7.  Nella pagina **Configura rete** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Aggiunta a un gruppo di lavoro**: specificare se aggiungere il computer di destinazione a un gruppo di lavoro.  

    -   **Aggiunta a un dominio**: specificare se aggiungere il computer di destinazione a un dominio. In **Dominio**specificare il nome del dominio.  

        > [!IMPORTANT]  
        >  È possibile cercare i domini nella foresta locale, ma è necessario specificare il nome di dominio per una foresta remota.  

         È inoltre possibile specificare un'unità organizzativa. Si tratta di un'impostazione facoltativa che specifica il nome distinto LDAP X.500 dell'unità organizzativa in cui creare l'account computer se non esiste già.  

    -   **Account**: specificare il nome utente e la password per l'account con le autorizzazioni per l'aggiunta al dominio specificato. Ad esempio: *dominio\utente* o *%variabile%*.  

8.  Nella pagina **Installa Configuration Manager** specificare il pacchetto client di Configuration Manager da installare nel computer di destinazione e quindi fare clic su **Avanti**.  

9. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

10. Completare la procedura guidata.  

###  <a name="a-namebkmkcreatevhda-create-a-vhd"></a><a name="BKMK_CreateVHD"></a> Creare un disco rigido virtuale  
 Dopo aver creato una sequenza di attività per il disco rigido virtuale, utilizzare la Creazione guidata disco rigido virtuale per creare il disco rigido virtuale.  

> [!IMPORTANT]  
>  Prima di eseguire questa procedura, verificare che siano soddisfatti i prerequisiti elencati all'inizio di questo argomento.  

 Utilizzare la seguente procedura per creare un disco rigido virtuale.  

#### <a name="to-create-a-vhd"></a>Per creare un disco rigido virtuale  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Dischi rigidi virtuali**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea disco rigido virtuale** per avviare la Creazione guidata disco rigido virtuale.  

    > [!NOTE]  
    >  Hyper-V deve essere installato sul computer che esegue la console di Configuration Manager da cui si gestiscono i dischi rigidi virtuali, in caso contrario l'opzione **Crea disco rigido virtuale** non viene abilitata. Per ulteriori informazioni sui requisiti di Hyper-V, vedere [Prerequisiti di installazione di Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  Per organizzare i dischi rigidi virtuali, creare una nuova cartella o selezionare una cartella esistente nel nodo **Dischi rigidi virtuali** , quindi fare clic su **Crea disco rigido virtuale** dalla cartella.  

4.  Nella pagina **Generale** specificare le seguenti impostazioni, quindi fare clic su **Avanti**.  

    -   **Nome**: specificare un nome univoco per il disco rigido virtuale.  

    -   **Versione**: specificare un numero di versione per il disco rigido virtuale. Si tratta di un'impostazione facoltativa.  

    -   **Commento**: specificare una descrizione per il disco rigido virtuale.  

    -   **Percorso**: specificare il percorso e il nome file usati dalla procedura guidata per creare il file VHD.  

         È necessario immettere un percorso di rete valido nel formato UNC. Ad esempio: **\\\nomeserver\\<nomecondivisione\>\\<nomefile\>.vhd**.  

        > [!WARNING]  
        >  Configuration Manager deve avere autorizzazioni di accesso in **scrittura** al percorso specificato per creare il disco rigido virtuale. Se Configuration Manager non è in grado di accedere al percorso, l'errore associato verrà registrato nel file distmgr.log sul server del sito.  

5.  Nella pagina **Sequenza attività** specificare la sequenza attività descritta nella sezione precedente, quindi fare clic su **Avanti**.  

6.  Nella pagina **Punti di distribuzione** selezionare uno o più punti di distribuzione che includono il contenuto richiesto dalla sequenza attività e quindi fare clic su **Avanti**.  

7.  Nella pagina **Personalizzazione** fare clic su **Avanti**. Il processo per creare il disco rigido virtuale ignora eventuali impostazioni specificate in questa pagina.  

8.  Verificare le impostazioni e fare clic su **Avanti**. La procedura guidata crea il disco rigido virtuale.  

    > [!TIP]  
    >  Il tempo necessario per completare il processo di creazione del disco rigido virtuale può variare. Durante l'elaborazione del processo, è possibile monitorare i seguenti file di log per tenere traccia dello stato di avanzamento. Per impostazione predefinita, i log si trovano nel computer che esegue la console di Configuration Manager in %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: le informazioni vengono scritte in questo log durante la creazione del supporto della sequenza di attività. Esaminare il file di log per tenere traccia dello stato di avanzamento della procedura guidata durante la creazione del supporto autonomo.  
    > -   **DeployToVHD.log**: le informazioni vengono scritte in questo log durante l'elaborazione del processo di creazione del disco rigido virtuale. Esaminare il file di log per tenere traccia dello stato di avanzamento della procedura guidata durante la creazione del supporto autonomo.  
    >   
    >  Inoltre, all'avvio dell'installazione del sistema operativo, è possibile aprire la console di gestione di Hyper-V (se nel computer sono stati installati gli strumenti di gestione Hyper-V) e collegarsi alla macchina virtuale temporanea creata dalla procedura guidata per vedere la sequenza attività in esecuzione. Dalla macchina virtuale, è possibile monitorare il file Smsts log per tenere traccia dello stato di avanzamento della sequenza attività. Se si verificano problemi durante il completamento di un passaggio della sequenza attività, è possibile utilizzare questo file di log per risolvere il problema. Il file smsts.log si trova in x:\windows\temp\smstslog\smsts.log prima della formattazione del disco rigido e in c:\\_SMSTaskSequence\Logs\Smstslog\ dopo la formattazione. Al termine dei passaggi della sequenza attività, la macchina virtuale viene arrestata dopo 5 minuti (per impostazione predefinita) ed eliminata.  

 Dopo la creazione del disco rigido virtuale da parte di Configuration Manager, il disco si trova nel nodo **Dischi rigidi virtuali** nella console di Configuration Manager sotto il nodo **Distribuzione del sistema operativo** nell'area di lavoro **Raccolta software**.  

> [!NOTE]  
>  Configuration Manager recupera la dimensione del disco rigido virtuale connettendosi al percorso di origine del disco rigido virtuale. Se Configuration Manager non è in grado di accedere al file del disco rigido virtuale, viene visualizzato **0** nella colonna **Dimensione (KB)** per il disco rigido virtuale.  

##  <a name="a-namebkmkmodifyvhdstepsa-steps-to-modify-an-existing-vhd"></a><a name="BKMK_ModifyVHDSteps"></a> Passaggi per la modifica di un disco rigido virtuale esistente  
 Per modificare un disco rigido virtuale, è necessario creare una sequenza di attività con i passaggi necessari per modificare il disco rigido virtuale. Selezionare quindi la sequenza di attività nella Modifica guidata disco rigido virtuale. La procedura guidata collega il disco rigido virtuale alla macchina virtuale, esegue la sequenza di attività nel disco rigido virtuale e quindi aggiorna il file VHD. Le sezioni seguenti forniscono i passaggi per modificare il disco rigido virtuale.  

###  <a name="a-namebkmkmodifytsa-create-a-task-sequence-to-modify-the-vhd"></a><a name="BKMK_ModifyTS"></a> Creare una sequenza di attività per modificare il disco rigido virtuale  
 Per modificare un disco rigido virtuale esistente, è innanzitutto necessario creare una sequenza di attività. Scegliere solo i passaggi necessari per modificare la sequenza di attività. Ad esempio, se si intende aggiungere un'applicazione al disco rigido virtuale, creare una sequenza di attività personalizzata e quindi aggiungere soltanto il passaggio Installa applicazione.  

 Utilizzare la seguente procedura per creare la sequenza di attività per creare il disco rigido virtuale.  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>Creare una sequenza di attività personalizzata per modificare il disco rigido virtuale  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza attività** , selezionare **Crea una nuova sequenza attività personalizzata**, quindi fare clic su **Avanti**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifichi la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione della sequenza di attività.  

    -   **Immagine di avvio**: specificare l'immagine di avvio che installa il sistema operativo nel computer di destinazione. Per altre informazioni, vedere la sezione relativa alla [gestione delle immagini di avvio](../get-started/manage-boot-images.md).  

6.  Completare la procedura guidata.  

 Utilizzare la seguente procedura per aggiungere i passaggi della sequenza di attività alla sequenza di attività personalizzata.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>Aggiungere i passaggi della sequenza di attività alla sequenza di attività personalizzata  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**e quindi selezionare la sequenza di attività personalizzata creata nella procedura precedente.  

3.  Nella scheda **Home** del gruppo **Sequenza attività** , fare clic su **Modifica** per avviare l'editor della sequenza attività.  

4.  Aggiungere i passaggi della sequenza di attività da utilizzare per modificare il disco rigido virtuale.  

5.  Fare clic su **OK** per uscire dall'editor della sequenza attività.  

###  <a name="a-namebkmkmodifyvhda-modify-a-vhd"></a><a name="BKMK_ModifyVHD"></a> Modificare un disco rigido virtuale  
 Dopo aver creato una sequenza di attività per il disco rigido virtuale, utilizzare la Modifica guidata disco rigido virtuale per modificare il disco rigido virtuale.  

 Utilizzare la seguente procedura per modificare un disco rigido virtuale.  

#### <a name="to-modify-a-vhd"></a>Modificare un disco rigido virtuale  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , espandere **Sistemi operativi**, quindi fare clic su **Dischi rigidi virtuali**e selezionare quindi il disco rigido virtuale da modificare.  

3.  Nella scheda **Home** del gruppo **Disco rigido virtuale** , fare clic su **Modifica disco rigido virtuale** per avviare la Modifica guidata disco rigido virtuale.  

    > [!NOTE]  
    >  Hyper-V deve essere installato sul computer che esegue la console di Configuration Manager da cui si gestiscono i dischi rigidi virtuali, in caso contrario l'opzione **Modifica disco rigido virtuale** non viene abilitata. Per ulteriori informazioni sui requisiti di Hyper-V, vedere [Prerequisiti di installazione di Hyper-V](http://technet.microsoft.com/library/cc731898.aspx).  

4.  Nella pagina **Generale** confermare le seguenti impostazioni, quindi fare clic su **Avanti**.  

    -   **Nome**: specifica il nome univoco per il disco rigido virtuale.  

    -   **Versione**: specifica il numero di versione per il disco rigido virtuale. Si tratta di un'impostazione facoltativa.  

    -   **Commento**: specifica la descrizione per il disco rigido virtuale.  

    -   **Percorso**: specifica il percorso e il nome file in cui si trova il file VHD. È impossibile modificare questa impostazione.  

        > [!WARNING]  
        >  Configuration Manager deve avere autorizzazioni di accesso in **scrittura** al percorso specificato per creare il disco rigido virtuale. Se Configuration Manager non è in grado di accedere al percorso, l'errore associato verrà registrato nel file distmgr.log sul server del sito.  

5.  Nella pagina **Sequenza attività** specificare la sequenza di attività descritta creata nella sezione precedente, quindi fare clic su **Avanti**.  

6.  Nella pagina **Punti di distribuzione** selezionare uno o più punti di distribuzione che includono il contenuto richiesto dalla sequenza attività e quindi fare clic su **Avanti**.  

7.  Nella pagina **Personalizzazione** fare clic su **Avanti**. Il processo per modificare il disco rigido virtuale ignora eventuali impostazioni specificate in questa pagina.  

8.  Verificare le impostazioni e fare clic su **Avanti**. La procedura guidata crea il disco rigido virtuale modificato.  

    > [!TIP]  
    >  Il tempo necessario per completare il processo di modifica del disco rigido virtuale può variare. Durante l'elaborazione del processo, è possibile monitorare i seguenti file di log per tenere traccia dello stato di avanzamento. Per impostazione predefinita, i log si trovano nel computer che esegue la console di Configuration Manager in %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: le informazioni vengono scritte in questo log durante la creazione del supporto della sequenza di attività. Esaminare il file di log per tenere traccia dello stato di avanzamento della procedura guidata durante la creazione del supporto autonomo.  
    > -   **DeployToVHD.log**: la procedura guidata scrive le informazioni in questo registro durante l'elaborazione del processo di modifica del disco rigido virtuale. Esaminare il file di log per tenere traccia dello stato di avanzamento della procedura guidata durante la creazione del supporto autonomo.  
    >   
    >  Inoltre, è possibile aprire la console di gestione di Hyper-V (se nel computer sono stati installati gli strumenti di gestione Hyper-V) e connettersi alla macchina virtuale temporanea creata dalla procedura guidata per vedere la sequenza di attività in esecuzione. Dalla macchina virtuale, è possibile monitorare il file Smsts log per tenere traccia dello stato di avanzamento della sequenza attività. Se si verificano problemi durante il completamento di un passaggio della sequenza attività, è possibile utilizzare questo file di log per risolvere il problema. Il file smsts.log si trova in x:\windows\temp\smstslog\smsts.log prima della formattazione del disco rigido e in c:\\_SMSTaskSequence\Logs\Smstslog\ dopo la formattazione. Al termine dei passaggi della sequenza attività, la macchina virtuale viene arrestata dopo 5 minuti (per impostazione predefinita) ed eliminata.  

##  <a name="a-namebkmkapplyupdatesa-apply-software-updates-to-a-vhd"></a><a name="BKMK_ApplyUpdates"></a> Applicare aggiornamenti software a un disco rigido virtuale  
 Periodicamente, vengono rilasciati nuovi aggiornamenti software applicabili al sistema operativo nel disco rigido virtuale. È possibile applicare gli aggiornamenti software a un disco rigido virtuale in base a una pianificazione specificata. Nella pianificazione specificata, Configuration Manager consente di applicare gli aggiornamenti software selezionati al disco rigido virtuale.  

 Le informazioni relative al disco rigido virtuale vengono archiviate nel database del sito, inclusi gli aggiornamenti software applicati al momento della creazione del disco rigido virtuale. Nel database del sito vengono archiviati anche gli aggiornamenti software applicati al disco rigido virtuale da quando è stato inizialmente creato. Quando si avvia la procedura guidata per applicare gli aggiornamenti software al disco rigido virtuale, viene recuperato un elenco di aggiornamenti software validi e selezionabili che non sono ancora stati applicati al disco rigido virtuale.  

 È possibile selezionare l'impostazione **Continua in caso di errore** per consentire a Configuration Manager di continuare ad applicare aggiornamenti software anche in presenza di un errore durante l'applicazione di uno o più degli aggiornamenti software selezionati.  

> [!NOTE]  
>  Gli aggiornamenti software vengono copiati dalla raccolta contenuto nel server del sito.  

 Utilizzare la seguente procedura per applicare gli aggiornamenti software al disco rigido virtuale.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>Per applicare gli aggiornamenti software a un disco rigido virtuale  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Dischi rigidi virtuali**.  

3.  Selezionare il disco rigido virtuale a cui applicare gli aggiornamenti software.  

4.  Nella scheda **Home** del gruppo **Disco rigido virtuale** , fare clic su **Pianifica aggiornamenti** per avviare la procedura guidata.  

5.  Nella pagina **Scegli aggiornamenti** selezionare gli aggiornamenti software da applicare al disco rigido virtuale, quindi fare clic su **Avanti**.  

6.  Nella pagina **Imposta pianificazione** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    1.  **Pianificazione**: specificare la pianificazione per l'applicazione degli aggiornamenti software al disco rigido virtuale.  

    2.  **Continua in caso di errore**: selezionare questa opzione per continuare ad applicare gli aggiornamenti software all'immagine anche quando si verifica un errore.  

7.  Nella pagina **Riepilogo** verificare le informazioni e quindi fare clic su **Avanti**.  

8.  Nella pagina **Completamento** verificare che gli aggiornamenti software siano stati applicati correttamente all'immagine del sistema operativo.  

##  <a name="a-namebkmkimporttovmma-import-the-vhd-to-system-center-virtual-machine-manager"></a><a name="BKMK_ImportToVMM"></a> Importare il disco rigido virtuale in System Center Virtual Machine Manager  
 System Center VMM è una soluzione di gestione per il data center virtualizzato che consente di configurare e gestire l'host di virtualizzazione, la rete e le risorse di archiviazione per creare e distribuire macchine virtuali e servizi nei cloud privati creati. Dopo aver creato un disco rigido virtuale in Configuration Manager, è possibile importare e gestire il disco rigido virtuale usando VMM.  

> [!TIP]  
>  Prima di caricare un disco rigido virtuale in VMM, verificare che la console VMM sia in grado di connettersi al server di gestione di VMM.  

 Utilizzare la seguente procedura per importare un disco rigido virtuale in VMM.  

#### <a name="to-import-a-vhd-to-vmm"></a>Per importare un disco rigido virtuale in VMM  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Dischi rigidi virtuali**.  

3.  Nella scheda **Home** del gruppo **Disco rigido virtuale** , fare clic su **Carica in Virtual Machine Manager** per avviare il caricamento guidato in Virtual Machine Manager.  

4.  Nella pagina **Generale** configurare le seguenti impostazioni, quindi fare clic su **Avanti**.  

    -   **Nome del server VMM**: specificare l'FQDN del computer in cui è installato il server di gestione VMM. La procedura guidata si connette al server di gestione VMM per scaricare le condivisioni di libreria per il server.  

    -   **Condivisione di libreria VMM**: specificare la condivisione di libreria VMM nell'elenco a discesa.  

    -   **Utilizzare trasferimento non crittografato**: selezionare questa opzione per trasferire il file VHD nel server di gestione VMM senza usare la crittografia.  

5.  Nella pagina di riepilogo, verificare le impostazioni, quindi completare la procedura guidata. Il tempo richiesto per caricare il disco rigido virtuale può variare in base alle dimensioni del file VHD e alla larghezza di banda di rete per il server di gestione VMM.  



<!--HONumber=Nov16_HO1-->


