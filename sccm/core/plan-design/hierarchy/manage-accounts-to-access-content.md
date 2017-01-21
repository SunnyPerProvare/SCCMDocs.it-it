---
title: Account per accedere al contenuto | Microsoft Docs
description: Informazioni sugli account in cui i client accedono al contenuto di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 4bf8dbd007f2ff122d1447ffcb2a963579034033

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gestire gli account per l'accesso al contenuto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di distribuire il contenuto in System Center Configuration Manager, è opportuno considerare la modalità con cui i client avranno accesso a tale contenuto nei punti di distribuzione.  

-   **Account di accesso alla rete** : usato dai client per connettersi a un punto di distribuzione e accedere al contenuto. Per impostazione predefinita, i client proveranno prima a usare l'account del proprio computer  

     Questo account viene anche usato dai punti di distribuzione pull per ottenere il contenuto da un punto di distribuzione di origine in una foresta remota  

-   **Account di accesso ai pacchetti**: per impostazione predefinita, Configuration Manager concede l'accesso al contenuto in un punto di distribuzione agli account di accesso generici Utenti e Amministratori. È tuttavia possibile configurare autorizzazioni aggiuntive per limitare l'accesso.  

-   **Account di connessione multicast** : usato per le distribuzioni del sistema operativo.  

##  <a name="a-namebkmknaaa-network-access-account"></a><a name="bkmk_NAA"></a> Account di accesso alla rete  
 I computer client usano l'account di accesso alla rete quando non possono usare l'account computer locale per accedere al contenuto nei punti di distribuzione, come accade, ad esempio, con i client dei gruppi di lavoro e i computer di domini non attendibili. Questo account può anche essere usato durante la distribuzione del sistema operativo quando il computer che installa il sistema operativo non dispone ancora di un account computer nel dominio.  

-   I client usano l'account di accesso alla rete solo per l'accesso alle risorse della rete  

-   È possibile configurare più account da usare come account di accesso alla rete in ogni sito primario  

-   I client proveranno ad accedere al contenuto in un punto di distribuzione usando prima di tutto il proprio account *nomecomputer*$. Se l'accesso non riesce, si prova con un account di accesso alla rete. I client continueranno a provare a usare l'account di accesso alla rete anche se non è riuscito in precedenza.  

**Autorizzazioni**: concedere a questo account le autorizzazioni minime appropriate per accedere al software per il contenuto richiesto dal client.  

-   L'account deve disporre del diritto **Accedi al computer dalla rete** per il punto di distribuzione.  

-   Creare l'account in tutti i domini che forniscono l'accesso necessario alle risorse. L'account di accesso alla rete deve sempre includere un nome di dominio. La protezione pass-through non è supportata per questo account. Se si dispone di punti di distribuzione in più domini, creare l'account in un dominio attendibile.  

> [!TIP]  
>  Per evitare blocchi degli account, non modificare la password per un account di accesso alla rete esistente. Al contrario, creare un nuovo account e configurarlo in Configuration Manager. Quando è trascorso tempo sufficiente e tutti i client hanno ricevuto i dettagli del nuovo account, rimuovere il vecchio account dalle cartelle condivise in rete ed eliminare l'account.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti di accesso interattivo.  
>   
>  Non concedere a questo account il diritto di aggiungere computer al dominio. Se è necessario aggiungere computer al dominio durante una sequenza di attività, usare l'account di aggiunta dominio dell'editor della sequenza di attività.  

### <a name="to-configure-the-network-access-account"></a>Per configurare l'account di accesso alla rete  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** >   **Configurazione sito** >  **Siti** e quindi selezionare il sito.  

2.  Nel gruppo **Impostazioni** fare clic su **Configura componenti del sito** > **Distribuzione software**.  

3.  Fare clic sulla scheda **Account di accesso alla rete** . Configurare uno o più account e quindi fare clic su **OK**.  

##  <a name="a-namebkmkpaaa-package-access-accounts"></a><a name="bkmk_Paa"></a> Account di accesso ai pacchetti  
 Gli account di accesso al pacchetto consentono di impostare le autorizzazioni del file system NTFS per specificare gli utenti e i gruppi di utenti che possono accedere al contenuto del pacchetto nei punti di distribuzione. Per impostazione predefinita, Configuration Manager concede l'accesso solo agli account di accesso generici **Utenti** e **Amministratori**, ma è possibile controllare l'accesso per i computer client usando gruppi o account Windows aggiuntivi. I dispositivi mobili recuperano sempre il contenuto del pacchetto in modo anonimo; pertanto, i dispositivi mobili non utilizzano gli account di accesso al pacchetto.  

 Per impostazione predefinita, quando Configuration Manager copia i file di contenuto in un pacchetto in un punto di distribuzione, garantisce l'accesso di **Lettura** al gruppo **Utenti** locale e **Controllo completo** al gruppo **Amministratori** locale. Le autorizzazioni effettive necessarie dipendono dal pacchetto. Se si dispone di client in gruppi di lavoro o in foreste non trusted, tali client usano l'account di accesso alla rete per accedere al contenuto del pacchetto. Assicurarsi che l'account di accesso alla rete disponga delle autorizzazioni per il pacchetto utilizzando gli account di accesso al pacchetto definiti.  

 Usare gli account in un dominio che possa accedere ai punti di distribuzione. Se si crea o si modifica l'account dopo la creazione del pacchetto, è necessario ridistribuire il pacchetto. L'aggiornamento dei pacchetti non modifica le autorizzazioni del file system NTFS sul pacchetto.  

 Non è necessario aggiungere l'account di accesso alla rete come account di accesso al pacchetto, perché l'appartenenza al gruppo **Utenti** lo aggiunge automaticamente. La limitazione dell'account di accesso al pacchetto al solo account di accesso alla rete non impedisce ai client di accedere al pacchetto.  

### <a name="to-manage-access-accounts"></a>Per gestire gli account di accesso  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** , selezionare uno dei seguenti passaggi per il tipo di contenuto per cui si desidera gestire gli account di accesso:  

    -   **Applicazioni**: espandere **Gestione applicazioni**, fare clic su **Applicazioni**, quindi selezionare le applicazioni per cui si desidera gestire gli account di accesso.  

    -   **Pacchetti**: espandere **Gestione applicazioni**, fare clic su **Pacchetti**, quindi selezionare i pacchetti per cui si desidera gestire gli account di accesso.  

    -   **Pacchetti di distribuzione**: espandere **Aggiornamenti software**, fare clic su **Pacchetti di distribuzione**, quindi selezionare i pacchetti di distribuzione per cui gestire gli account di accesso.  

    -   **Pacchetti driver**: espandere **Sistemi operativi**, fare clic su **Pacchetti driver**, quindi selezionare i pacchetti driver per cui gestire gli account di accesso.  

    -   **Immagini del sistema operativo**: espandere **Sistemi operativi**, fare clic su **Immagini del sistema operativo**, quindi selezionare le immagini del sistema operativo per cui gestire gli account di accesso.  

    -   **Programmi di installazione sistema operativo**: espandere **Sistemi operativi**, fare clic su **Programmi di installazione sistema operativo**, quindi selezionare i programmi di installazione del sistema operativo per cui gestire gli account di accesso.  

    -   **Immagini d'avvio**: espandere **Sistemi operativi**, fare clic su **Immagini d'avvio**, quindi selezionare le immagini d'avvio per cui gestire gli account di accesso.  

3.  Fare clic con il pulsante destro del mouse sull'oggetto selezionato, quindi fare clic su **Gestione account di accesso**.  

4.  Nella finestra di dialogo **Aggiungi account** , specificare il tipo di account al quale sarà garantito l'accesso al contenuto, quindi specificare i diritti di accesso associati all'account.  

    > [!NOTE]  
    >  Quando si aggiunge un nome utente per l'account e Configuration Manager trova un account utente locale e un account utente di dominio con tale nome, Configuration Manager imposta i diritti di accesso per l'account utente di dominio.  

##  <a name="a-namebkmkmultia-multicast-connection-account"></a><a name="bkmk_multi"></a> Account di connessione multicast  
 L'Account di connessione multicast viene usato dai punti di distribuzione configurati affinché il multicast legga le informazioni dal database del sito.  

-   Specificare un account da usare quando si configurano le connessioni del database di Configuration Manager per il multicast  

-   Per impostazione predefinita, viene usato l'account computer del punto di distribuzione, ma è comunque possibile configurare un account utente  

-   Ogni volta che il database del sito si trova in una foresta non trusted, è necessario specificare un account utente  

-   L'account deve avere le autorizzazioni di **lettura** per il database del sito  

Ad esempio, se il data center dispone di una rete perimetrale in una foresta diversa dal server del sito e dal database del sito, è possibile usare questo account per leggere le informazioni multicast dal database del sito.  
Durante la creazione, impostare questo account come account locale e con diritti limitati sul computer che esegue Microsoft SQL Server.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti di accesso interattivo.  



<!--HONumber=Dec16_HO3-->


