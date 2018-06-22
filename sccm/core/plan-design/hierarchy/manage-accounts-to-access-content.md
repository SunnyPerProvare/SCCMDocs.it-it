---
title: Account per accedere al contenuto
titleSuffix: Configuration Manager
description: Informazioni sugli account in cui i client accedono al contenuto di System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c21601246cb0024837256b7cf8d4c1576c00149d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338687"
---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gestire gli account per l'accesso al contenuto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di distribuire il contenuto in System Center Configuration Manager, è opportuno considerare il modo in cui i client avranno accesso a tale contenuto dai punti di distribuzione. Questo articolo descrive gli account seguenti usati per questo scopo:

-   **Account di accesso alla rete**. Usato dai client per connettersi a un punto di distribuzione e accedere al contenuto. Per impostazione predefinita, i client provano prima a usare il proprio account computer locale.

     Questo account viene usato anche dai punti di distribuzione pull per ottenere il contenuto da un punto di distribuzione di origine in una foresta remota.  

-   **Account di accesso ai pacchetti**. Per impostazione predefinita, Configuration Manager concede l'accesso al contenuto in un punto di distribuzione agli account predefiniti denominati **Utenti** e **Amministratori**. È possibile configurare altre autorizzazioni per limitare l'accesso.  

-   **Account di connessione multicast**. Usato per le distribuzioni del sistema operativo.  

##  <a name="bkmk_NAA"></a> Account di accesso alla rete  
 I computer client usano l'account di accesso alla rete quando non possono usare il proprio account computer locale per accedere al contenuto nei punti di distribuzione. Ad esempio, si applica a client e computer di gruppi di lavoro di domini non attendibili. Questo account può anche essere usato durante la distribuzione del sistema operativo quando il computer che installa il sistema operativo non dispone ancora di un account computer nel dominio.  

-   I client usano solo l'account di accesso alla rete per l'accesso alle risorse della rete.  

-   In ogni sito primario è possibile configurare più account da usare come account di accesso alla rete.  

-   I client provano prima ad accedere al contenuto in un punto di distribuzione usando il proprio account *computername*$. Se l'accesso non riesce, i client eseguono un tentativo con un account di accesso alla rete e continuano a provare usando tale account anche in caso di insuccesso.  

### <a name="permissions"></a>Autorizzazioni
Concedere a questo account le autorizzazioni minime appropriate per accedere al software per il contenuto richiesto dal client.  

-   L'account deve disporre del diritto **Accedi al computer dalla rete** per il punto di distribuzione.  

-   Creare l'account in tutti i domini che forniscono l'accesso necessario alle risorse. L'account di accesso alla rete deve sempre includere un nome di dominio. La protezione pass-through non è supportata per questo account. Se si dispone di punti di distribuzione in più domini, creare l'account in un dominio attendibile.  

> [!TIP]  
>  Per evitare blocchi degli account, non modificare la password per un account di accesso alla rete esistente. Al contrario, creare un nuovo account e configurarlo in Configuration Manager. Quando è trascorso tempo sufficiente e tutti i client hanno ricevuto i dettagli del nuovo account, rimuovere l'account precedente dalle cartelle condivise in rete ed eliminare l'account.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti interattivi per l'accesso.  
>   
>  Non concedere a questo account il diritto di aggiungere computer al dominio. Se è necessario aggiungere computer al dominio durante una sequenza di attività, usare l'account di aggiunta dominio dell'editor della sequenza di attività.  

### <a name="to-configure-the-network-access-account"></a>Per configurare l'account di accesso alla rete  

1.  Nella console di Configuration Manager scegliere **Amministrazione** >   **Configurazione sito** >  **Siti** e quindi selezionare il sito.  

2.  Nel gruppo **Impostazioni** scegliere **Configura componenti del sito** > **Distribuzione software**.  

3.  Scegliere la scheda **Account di accesso alla rete**. Configurare uno o più account e quindi scegliere **OK**.  

##  <a name="bkmk_Paa"></a> Account di accesso ai pacchetti  
 Gli account di accesso ai pacchetti consentono di impostare le autorizzazioni del file system NTFS per specificare gli utenti e i gruppi di utenti che possono accedere al contenuto dei pacchetti nei punti di distribuzione. Per impostazione predefinita, Configuration Manager concede l'accesso solo agli account generici **Utenti** e **Amministratori**. È tuttavia possibile controllare l'accesso per i computer client usando gruppi o account di Windows aggiuntivi. I dispositivi mobili non usano gli account di accesso ai pacchetti perché recuperano sempre il contenuto dei pacchetti in modo anonimo.  

 Per impostazione predefinita, quando Configuration Manager copia i file di contenuto in un pacchetto in un punto di distribuzione, garantisce l'accesso di **Lettura** al gruppo **Utenti** locale e **Controllo completo** al gruppo **Amministratori** locale. Le autorizzazioni effettive necessarie dipendono dal pacchetto. Se si dispone di client in gruppi di lavoro o in foreste non trusted, tali client usano l'account di accesso alla rete per accedere al contenuto del pacchetto. Assicurarsi che l'account di accesso alla rete disponga delle autorizzazioni per il pacchetto utilizzando gli account di accesso al pacchetto definiti.  

 Usare gli account in un dominio che possa accedere ai punti di distribuzione. Se si crea o si modifica l'account dopo la creazione del pacchetto, è necessario ridistribuire il pacchetto. L'aggiornamento dei pacchetti non modifica le autorizzazioni del file system NTFS sul pacchetto.  

 Non è necessario aggiungere l'account di accesso alla rete come account di accesso al pacchetto, perché l'appartenenza al gruppo **Utenti** lo aggiunge automaticamente. La limitazione dell'account di accesso al pacchetto al solo account di accesso alla rete non impedisce ai client di accedere al pacchetto.  

### <a name="to-manage-access-accounts"></a>Per gestire gli account di accesso  

1.  Nella console di Configuration Manager scegliere **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** determinare il tipo di contenuto per cui gestire gli account di accesso e seguire i passaggi indicati:  

    -   **Applicazioni**: espandere **Gestione applicazioni**, scegliere **Applicazioni** e quindi selezionare le applicazioni per cui gestire gli account di accesso.  

    -   **Pacchetti**: espandere **Gestione applicazioni**, scegliere **Pacchetti** e quindi selezionare i pacchetti per cui gestire gli account di accesso.  

    -   **Pacchetti di distribuzione**: espandere **Aggiornamenti software**, scegliere **Pacchetti di distribuzione** e quindi selezionare i pacchetti di distribuzione per cui gestire gli account di accesso.  

    -   **Pacchetti driver**: espandere **Sistemi operativi**, scegliere **Pacchetti driver** e quindi selezionare i pacchetti driver per cui gestire gli account di accesso.  

    -   **Immagini del sistema operativo**: espandere **Sistemi operativi**, scegliere **Immagini del sistema operativo** e quindi selezionare le immagini del sistema operativo per cui gestire gli account di accesso.  

    -   **Programmi di installazione sistema operativo**: espandere **Sistemi operativi**, scegliere **Programmi di installazione sistema operativo** e quindi selezionare i programmi di installazione del sistema operativo per cui gestire gli account di accesso.  

    -   **Immagini d'avvio**: espandere **Sistemi operativi**, scegliere **Immagini d'avvio** e quindi selezionare le immagini d'avvio per cui gestire gli account di accesso.  

3.  Fare clic con il pulsante destro del mouse sull'oggetto selezionato e quindi scegliere **Gestione account di accesso**.  

4.  Nella finestra di dialogo **Aggiungi account** , specificare il tipo di account al quale sarà garantito l'accesso al contenuto, quindi specificare i diritti di accesso associati all'account.  

    > [!NOTE]  
    >  Quando si aggiunge un nome utente per l'account e Configuration Manager trova sia un account utente locale sia un account utente di dominio con tale nome, Configuration Manager imposta i diritti di accesso per l'account utente di dominio.  

##  <a name="bkmk_multi"></a> Account di connessione multicast  
 L'account di connessione multicast viene usato dai punti di distribuzione configurati per consentire al multicast di leggere le informazioni dal database del sito.  

-   Specificare un account da usare quando si configurano le connessioni del database di Configuration Manager per il multicast.  

-   Per impostazione predefinita, viene usato l'account computer del punto di distribuzione, ma è possibile configurare in alternativa un account utente.  

-   Ogni volta che il database del sito si trova in una foresta non trusted, è necessario specificare un account utente.  

-   L'account deve avere le autorizzazioni **Lettura** per il database del sito.  

Ad esempio, se il data center dispone di una rete perimetrale in una foresta diversa dal server del sito e dal database del sito, è possibile usare questo account per leggere le informazioni multicast dal database del sito.

Durante la creazione, impostare questo account come account locale e con diritti limitati sul computer che esegue Microsoft SQL Server.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti interattivi per l'accesso.  
