---
title: Distribuire i client Mac| Microsoft Docs
description: Informazioni su come distribuire i client a computer Mac in System Center Configuration Manager.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 9cab5b91a94e8bf2ad96a8a706f46c58e2a3d712
ms.lasthandoff: 03/21/2017


---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento descrive come distribuire e gestire il client di Configuration Manager nei computer Mac. Per informazioni sulle configurazioni necessarie prima di distribuire i client nei computer Mac, vedere [Preparare la distribuzione del software client in computer Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quando si installa un nuovo client per i computer Mac, può essere necessario installare anche gli aggiornamenti di Configuration Manager per riflettere le nuove informazioni client nella console di Configuration Manager.

In queste procedure sono disponibili due opzioni per l'installazione dei certificati client. Altre informazioni sui certificati client per computer Mac sono disponibili in [Preparare la distribuzione del software client in computer Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Usare la registrazione di Configuration Manager tramite lo [strumento CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Il processo di registrazione non supporta il rinnovo automatico del certificato, di conseguenza è necessario registrare nuovamente i computer Mac prima della scadenza del certificato installato.    

-   [Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  


## <a name="configure-client-settings-for-enrollment"></a>Configurare le impostazioni client per la registrazione  
 È necessario usare le [impostazioni client predefinite](../../../core/clients/deploy/about-client-settings.md) per configurare la registrazione per i computer Mac. Non è possibile usare impostazioni client personalizzate.  

 Questa operazione è necessaria affinché Configuration Manager richieda e installi il certificato nel computer Mac.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Per configurare le impostazioni client predefinite per Configuration Manager per registrare i certificati per i computer Mac  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

5.  Selezionare la sezione **Registrazione** e quindi configurare le seguenti impostazioni:  

    1.  **Consentire agli utenti di registrare i dispositivi mobili e i computer Mac: Sì**  

    2.  **Profilo di registrazione**: scegliere **Imposta profilo**.  

6.  Nella finestra di dialogo **Profilo di registrazione del dispositivo mobile** scegliere **Crea**.  

7.  Nella finestra di dialogo **Crea profilo di registrazione** inserire un nome per questo profilo di registrazione e quindi configurare il **Codice del sito di gestione**. Selezionare il sito primario di Configuration Manager che contiene i punti di gestione che gestiranno i computer Mac.  

    > [!NOTE]  
    >  Se è impossibile selezionare il sito, verificare che almeno un punto di gestione nel sito sia configurato per supportare i dispositivi mobili.  

8.  Scegliere **Aggiungi**.  

9. Nella finestra di dialogo **Aggiungi autorità di certificazione per dispositivi mobili** selezionare il server dell'autorità di certificazione (CA) che emetterà i certificati per i computer Mac.  

10. Nella finestra di dialogo **Crea profilo di registrazione** selezionare il modello di certificato del computer Mac creato nel passaggio 3.  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Profilo di registrazione** e quindi la finestra di dialogo **Impostazioni client predefinite**.  

    > [!TIP]  
    >  Se si vuole modificare l'intervallo dei criteri client, usare l'impostazione **Intervallo di polling dei criteri client** nel gruppo di impostazioni client **Criteri client** .  

 Tutti gli utenti verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) (Avviare il recupero criteri per un client di Configuration Manager).  

 Oltre alle impostazioni client di registrazione, assicurarsi di aver configurato le impostazioni del dispositivo client seguenti:  

-   **Inventario hardware**: abilitare e configurare questa opzione se si vuole raccogliere l'inventario hardware dai computer client Mac e Windows. Per altre informazioni, vedere [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md) (Come estendere l'inventario hardware in System Center Configuration Manager).  

-   **Impostazioni di conformità**: abilitare e configurare questa opzione se si vuole valutare e correggere le impostazioni nei computer client Mac e Windows. Per altre informazioni, vedere [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità).  

> [!NOTE]  
>  Per altre informazioni sulle impostazioni client di Configuration Manager, vedere [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

## <a name="download-the-client-source-files-for-macs"></a>Scaricare i file di origine del client per i computer Mac  

1.  Scaricare il pacchetto di file del client Mac OS X, **ConfigmgrMacClient.msi**e salvarlo in un computer con sistema operativo Windows.  

     Questo file non è incluso nel supporto di installazione di Configuration Manager. È possibile scaricare questo file dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  Nel computer Windows eseguire **ConfigmgrMacClient.msi** per estrarre il pacchetto del client Mac Macclient.dmg in una cartella nel disco locale (per impostazione predefinita **C:\Programmi (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copiare il file Macclient.dmg in una cartella sul computer Mac.  

4.  Eseguire il file Macclient.dmg nel computer Mac per estrarre i file in una cartella sul disco locale.  

5.  Nella cartella, assicurarsi che i file Ccmsetup e CMClient.pkg vengano estratti e che venga creata una cartella denominata Strumenti che contenga gli strumenti CMDiagnostics, CMUninstall, CMAppUtil e CMEnroll.

    -  **Ccmsetup**: installa il client di Configuration Manager nei computer Mac.  

    -   **CMDiagnostics**: raccoglie informazioni di diagnostica correlate al client di Configuration Manager nei computer Mac.  

    -   **CMUninstall**: disinstalla il client dai computer Mac.  

    -   **CMAppUtil**: converte i pacchetti di applicazioni Apple in un formato che possa essere distribuito come applicazione di Configuration Manager.  

    -   **CMEnroll**: richiede e installa il certificato client per un computer Mac per poter quindi installare il client di Configuration Manager.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installare il client e registrare il certificato client nel computer Mac  

È possibile registrare singoli client con la [registrazione guidata computer Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Per automatizzare le operazioni per registrare molti client, usare lo [strumento CMEnroll](#client-and-certificate-automation-with-cmenroll).   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrare il client con la registrazione guidata computer Mac  

1.  Dopo aver completato l'installazione del client viene avviata la registrazione guidata computer. Se la procedura guidata non si apre oppure se viene chiusa in modo accidentale, fare clic su **Registra** dalla pagina delle preferenze **Configuration Manager** per aprirla.  

2.  Nella seconda pagina della procedura guidata specificare:  

    -   **Nome utente** : è possibile scegliere uno dei seguenti formati:  

        -   'dominio\nome'. Ad esempio: 'contoso\mnorth'  

        -   'user@domain'. Ad esempio: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Se si usa un indirizzo di posta elettronica per compilare il campo **Nome utente**, il nome di dominio dell'indirizzo di posta elettronica e il nome predefinito del server del punto proxy di registrazione vengono usati da Configuration Manager per compilare automaticamente il campo **Nome server**. Se il nome di dominio e il nome del server non corrispondono al nome del server del punto proxy di registrazione, comunicare agli utenti il nome corretto da usare durante la registrazione dei computer Mac.  

         Il nome utente e la relativa password devono corrispondere a un account utente Active Directory a cui sono concesse la autorizzazioni di Lettura e Registrazione nel modello di certificato del client Mac.  

    -   **Password**: immettere una password corrispondente per il nome utente specificato.  

    -   **Nome server**: immettere il nome del server del punto proxy di registrazione.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automazione di client e certificati con CMEnroll  

Usare questa procedura per automatizzare l'installazione del client e la richiesta e la registrazione dei certificati client con lo strumento CMEnroll. Per eseguire lo strumento, è necessario disporre di un account utente di Active Directory.

1.  Nel computer Mac passare alla cartella in cui è stato estratto il contenuto del file Macclient.dmg.  

2.  Immettere la riga di comando seguente: **sudo ./ccmsetup**  

3.  Attendere fino a visualizzare il messaggio **Installazione completata** . Sebbene il programma di installazione visualizzi un messaggio di riavvio necessario immediato, non riavviare e andare al passaggio successivo.  

4.  Dalla cartella Strumenti nel computer Mac, digitare quanto segue: **sudo ./CMEnroll -s &lt;nome_server_proxy_registrazione> -ignorecertchainvalidation -u &lt;nome utente'>**  

    Dopo l'installazione del client, viene avviata la procedura guidata di registrazione del computer Mac per semplificarne la registrazione. Per registrare il client con questo metodo, vedere [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) in questo argomento.  

5. Digitare la password per l'account utente di Active Directory.  Quando si immette questo comando vengono richieste due password: la prima richiesta è per l'esecuzione del comando da parte dell'account utente con privilegi avanzati. La seconda richiesta è relativa all'account utente di Active Directory. L'aspetto delle due richieste è identico, quindi accertarsi di specificarli nella sequenza corretta.  

    Il nome utente può essere nei seguenti formati:  

    -   'dominio\nome'. Ad esempio: 'contoso\mnorth'  

    -   'user@domain'. Ad esempio: 'mnorth@contoso.com'  

     Il nome utente e la relativa password devono corrispondere a un account utente Active Directory a cui sono concesse la autorizzazioni di Lettura e Registrazione nel modello di certificato del client Mac.  

     Esempio: se il server del punto proxy di registrazione è denominato **server02.contoso.com**e a un nome utente di **contoso\mnorth** sono state concesse le autorizzazioni per il modello di certificato client Mac, digitare: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Se il nome utente contiene i caratteri **&lt;>"+=,** la registrazione avrà esito negativo. Ottenere un certificato fuori banda con un nome utente che non contenga tali caratteri.  
    >  
    >  Per un'esperienza utente più fluida, è possibile eseguire lo script dei passaggi e comandi di installazione, in modo che gli utenti debbano fornire solo il nome utente e la password.  

5.  Attendere fino a visualizzare il messaggio **Registrazione completata** .  

6.  Per limitare il certificato registrato in Configuration Manager, sul computer Mac, aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

7.  Riavviare il computer Mac.  

 Verificare che l'installazione client sia avvenuta correttamente aprendo l'elemento **Configuration Manager** in **Preferenze di Sistema** nel computer Mac. È possibile inoltre aggiornare e visualizzare la raccolta **Tutti i sistemi** per confermare che il computer Mac venga visualizzato in questa raccolta come client gestito.  

> [!TIP]  
>  Per risolvere i problemi con il client Mac, è possibile usare il programma CMDiagnostics incluso nel pacchetto del client Mac OS X, per raccogliere le informazioni diagnostiche seguenti:  
>   
>  -   Un elenco dei processi in esecuzione  
> -   La versione del sistema operativo Mac OS X  
> -   Le segnalazioni di arresto anomalo del Mac OS X relative al client di Configuration Manager incluse **CCM\*.crash** e **System Preference.crash**.  
> -   Il file della distinta base (BOM) e dell'elenco delle proprietà (.plist) creato dall'installazione client di Configuration Manager.  
> -   Il contenuto della cartella /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  Le informazioni raccolte da CmDiagnostics vengono aggiunte a un file con estensione zip che viene salvato sul desktop del computer e denominato cmdiag-*<nomehost\>***-***&gt;data e ora\>*.zip.***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager  

Eseguire prima di tutto le attività specifiche seguenti descritte in [Preparare la distribuzione del software client in computer Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients):

1. [Distribuire un certificato server Web nei server del sistema del sito](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Distribuire un certificato di autenticazione client nei server del sistema del sito](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configurare il punto di gestione e il punto di distribuzione](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Facoltativo: installare il punto di Reporting Services](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Eseguire quindi queste attività:

5. [Scaricare i file di origine del client per i computer Mac](#download-the-client-source-files-for-macs).  
6. Usare le istruzioni associate al metodo di distribuzione del certificato scelto per richiedere e installare il certificato client nel computer Mac.  
7.  Spostarsi nella cartella in cui è stato estratto il contenuto del file macclient.dmg scaricato dall'Area download Microsoft.  

3.  Immettere la riga di comando seguente: **sudo ./ccmsetup –MP <FQDN Internet punto di gestione\> -SubjectName <valore oggetto certificato\>**.  Il valore dell'oggetto certificato distingue tra maiuscole e minuscole, quindi digitarlo esattamente come appare nei dettagli del certificato.  

     Esempio: se l'FQDN Internet nelle proprietà del sistema del sito è **server03.contoso.com** e il certificato del client Mac ha l'FQDN **mac12.contoso.com** come nome comune nel soggetto del certificato, digitare: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Attendere fino a visualizzare il messaggio **Installazione completata** , quindi riavviare il computer Mac.  

5.  Per verificare che questo certificato sia accessibile da Configuration Manager, sul computer Mac aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

6.  Se si dispone di più certificati contenenti lo stesso valore soggetto, specificare il numero di serie del certificato per identificare il certificato da usare per il client di Configuration Manager. A tale scopo, usare il comando seguente: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numero di serie\>"**.  

     Ad esempio: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Verificare che l'installazione client sia avvenuta correttamente aprendo l'elemento **Configuration Manager** in **Preferenze di Sistema** nel computer Mac. È anche possibile aggiornare e visualizzare la raccolta **Tutti i sistemi** per verificare se il computer Mac appare in questa raccolta come client gestito.  

## <a name="renewing-the-mac-client-certificate"></a>Rinnovo del certificato del client Mac  
 Attenersi alla seguente procedura prima di rinnovare il certificato del computer nei computer Mac.  

 Questa procedura rimuove l'SMSID, che è necessario affinché il client usi un certificato nuovo o rinnovato nel computer Mac.  

> [!IMPORTANT]  
>  Quando si rimuove e sostituisce l'SMSID del client, tutte le cronologie client archiviate, come l'inventario, vengono eliminate dopo aver eliminato il client dalla console di Configuration Manager.  

### <a name="to-renew-the-mac-client-certificate"></a>Per rinnovare il certificato del client Mac  

1.  Creare e popolare una raccolta di dispositivi per i computer Mac che devono rinnovare i certificati dei computer.  

2.  Nell'area di lavoro **Asset e conformità** , avviare la **Creazione guidata dell'elemento di configurazione**.  

3.  Nella pagina **Generale** della procedura guidata specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo:Mac OS X**  

4.  Nella pagina **Piattaforme supportate** della procedura guidata, assicurarsi che siano selezionate tutte le versioni di Mac OS X.  

5.  Nella pagina **Impostazioni** della procedura guidata fare clic su **Nuovo** , quindi nella finestra di dialogo **Crea impostazione** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo di impostazione:Script**  

    -   **Tipo di dati: stringa**  

6.  Nella finestra di dialogo **Crea impostazione** , per **Script di individuazione**, fare clic su **Aggiungi script** per specificare uno script che individui i computer Mac con un SMSID configurato.  

7.  Nella finestra di dialogo **Modifica script di individuazione** , immettere il seguente script della shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Modifica script di individuazione** .  

9. Nella finestra di dialogo **Crea impostazione**, per **Script di monitoraggio e aggiornamento (facoltativo)** scegliere **Aggiungi script** per specificare uno script che rimuova l'SMSID quando viene rilevato in computer Mac.  

10. Nella finestra di dialogo **Crea script di monitoraggio e aggiornamento** , immettere il seguente script della shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Crea script di monitoraggio e aggiornamento**.  

12. Nella pagina **Regole di conformità** della procedura guidata fare clic su **Nuovo**, quindi nella finestra di dialogo **Crea regola** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Impostazione selezionata:** fare clic su **Sfoglia** e selezionare lo script di individuazione specificato in precedenza.  

    -   Nel campo **i seguenti valori** immettere **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Abilitare l'opzione **Eseguire lo script di monitoraggio e aggiornamento specificato quando l'impostazione non è conforme**.  

13. Completare la Creazione guidata dell'elemento di configurazione.  

14. Creare una linea di base della configurazione che contenga l'elemento di configurazione appena creato e lo distribuisca nella raccolta dispositivi creata nel Passaggio 1.  

     Per altre informazioni su come creare e distribuire le linee di base di configurazione, vedere [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Come creare linee di base di configurazione in System Center Configuration Manager).  

15. Dopo aver installato un nuovo certificato nei computer Mac con l'SMSID rimosso, eseguire il comando seguente per configurare il client per l'utilizzo del nuovo certificato:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Se si hanno più certificati contenenti lo stesso valore soggetto, specificare il numero di serie del certificato per identificare il certificato da usare per il client di Configuration Manager. A tale scopo, usare il comando seguente: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numero di serie\>"**.  

     Ad esempio: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Riavvia.  


### <a name="see-also"></a>Vedere anche

[Gestire i client Mac](/sccm/core/clients/manage/maintain-mac-clients)

