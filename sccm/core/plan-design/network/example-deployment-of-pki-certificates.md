---
title: Distribuire certificati PKI | Microsoft Docs
description: Seguire un esempio dettagliato per conoscere il processo di creazione e distribuzione dei certificati PKI usati in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
caps.latest.revision: 11
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 2db82f0572df9519b3119d4dca4f4626ae09d936


---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo esempio dettagliato di distribuzione usa un'autorità di certificazione (CA) Windows Server 2008 e contiene le procedure guidate per il processo di creazione e distribuzione dei certificati di infrastruttura a chiave pubblica (PKI) usati in System Center Configuration Manager. Queste procedure utilizzano modelli di certificato e una CA globale (enterprise). I passaggi sono adatti esclusivamente a una rete di test, come un modello di prova.  

 Dal momento che non esiste un singolo metodo di distribuzione per i certificati richiesti, è necessario consultare la documentazione di distribuzione PKI specifica per le procedure richieste e consigliate di distribuzione dei certificati richiesti per un ambiente di produzione. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Le istruzioni riportate in questo argomento possono essere facilmente adattate per sistemi operativi diversi da quelli documentati nella sezione Requisiti della rete di test. Tuttavia, se si esegue la CA emittente su Windows Server 2012, non viene richiesta la versione del modello di certificato. Al contrario, specificarla nella scheda **Compatibilità** delle proprietà del modello, come indicato di seguito:  
>   
>  -   **Autorità di certificazione**: **Windows Server 2003**  
> -   **Destinatario certificato**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Contenuto della sezione  
 Le sezioni seguenti comprendono istruzioni dettagliate di esempio per creare e distribuire i certificati seguenti che possono essere usati in System Center Configuration Manager:  

 [Requisiti della rete di test](#BKMK_testnetworkenvironment)  

 [Panoramica dei certificati](#BKMK_overview2008)  

 [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](#BKMK_webserver2008_cm2012)  

 [Distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](#BKMK_clouddp2008_cm2012)  

 [Distribuzione del certificato client per computer Windows](#BKMK_client2008_cm2012)  

 [Distribuzione del certificato client per punti di distribuzione](#BKMK_clientdistributionpoint2008_cm2012)  

 [Distribuzione del certificato di registrazione per i dispositivi mobili](#BKMK_mobiledevices2008_cm2012)  

 [Distribuzione dei certificati per AMT](#BKMK_AMT2008_cm2012)  

 [Distribuzione del certificato client per computer Mac](#BKMK_MacClient_SP1)  

##  <a name="a-namebkmktestnetworkenvironmenta-test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Requisiti della rete di test  
 Nelle istruzioni dettagliate sono richiesti i seguenti requisiti:  

-   Sulla rete di test è in esecuzione il ruolo Servizi di dominio Active Directory con Windows Server 2008 e la rete è installata come un dominio singolo, una foresta singola.  

-   Si dispone di un server membro su cui è in esecuzione Windows Server 2008 Enterprise Edition, su cui è installato il ruolo Servizi certificati Active Directory e che è configurato come CA radice dell'organizzazione (enterprise).  

-   È disponibile un computer su cui è installato Windows Server 2008 (Standard Edition o Enterprise Edition, R2 o versioni successive) e Internet Information Services (IIS) e che è designato come un server membro. Questo computer è il server del sistema del sito di System Center Configuration Manager che sarà configurato con un FQDN Intranet, per supportare le connessioni client nella Intranet, e con un FQDN Internet se è necessario supportare dispositivi mobili registrati da System Center Configuration Manager e client su Internet.  

-   Si dispone di un client Windows Vista su cui è installato il Service Pack più recente, configurato con un nome computer comprendente caratteri ASCII e associato al dominio. Questo computer è un computer client di System Center Configuration Manager.  

-   È possibile accedere con un account amministratore di dominio radice o un account amministratore di dominio organizzazione che dovrà essere utilizzato per tutte le procedure descritte in questo esempio di distribuzione.  

##  <a name="a-namebkmkoverview2008a-overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Panoramica dei certificati  
 Nella tabella seguente vengono elencati i tipi di certificati PKI che potrebbero essere richiesti per Center Configuration Manager e le informazioni sul loro uso.  

|Requisito del certificato|Descrizione del certificato|  
|-----------------------------|-----------------------------|  
|Certificato del server Web per i sistemi del sito che eseguono IIS|Questo certificato viene utilizzato per crittografare dati e per l'autenticazione tra server e client. Deve essere installato esternamente da System Center Configuration Manager nei server dei sistemi del sito che eseguono IIS e che sono configurati in System Center Configuration Manager per usare HTTPS.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](#BKMK_webserver2008_cm2012) in questo argomento.|  
|Certificato di servizio per i client per la connessione ai punti di distribuzione basati su cloud|Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](#BKMK_clouddp2008_cm2012) in questo argomento.<br /><br /> **Importante** : questo certificato viene usato in combinazione con il certificato di gestione di Windows Azure. Per ulteriori informazioni sul certificato di gestione, vedere [How to Create a Management Certificate (Come creare un certificato di gestione)](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [Come aggiungere un certificato di gestione a una sottoscrizione Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) nella sezione della piattaforma Windows Azure di MSDN Library.|  
|Certificato client per computer Windows|Questo certificato è usato per l'autenticazione tra i computer client di System Center Configuration Manager e i sistemi del sito che sono configurati per usare HTTPS. Può inoltre essere utilizzato per il monitoraggio dello stato operativo dei punti di gestione e dei punti di migrazione stato quando sono configurati per l'utilizzo di HTTPS. Deve essere installato esternamente da System Center Configuration Manager nei computer.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuzione del certificato client per computer Windows](#BKMK_client2008_cm2012) in questo argomento.|  
|Certificato client per punti di distribuzione|Questo certificato ha due scopi:<br /><br /> Il certificato viene utilizzato per l'autenticazione tra il punto di distribuzione e un punto di gestione abilitato HTTPS prima che il punto di distribuzione invii dei messaggi di stato.<br /><br /> Quando l'opzione del punto di distribuzione **Abilita supporto PXE per i client** è selezionata, il certificato viene inviato ai computer con avvio PXE in modo che possano connettersi a un punto di gestione abilitato HTTPS durante la distribuzione del sistema operativo.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuzione del certificato client per punti di distribuzione](#BKMK_clientdistributionpoint2008_cm2012) in questo argomento.|  
|Certificato di registrazione per dispositivi mobili|Questo certificato è usato per l'autenticazione tra i computer client dei dispositivi mobili di System Center Configuration Manager e i sistemi del sito che sono configurati per usare HTTPS. Deve essere installato come parte della registrazione dei dispositivi mobili in System Center Configuration Manager ed è necessario selezionare il modello di certificato configurato come impostazione client dei dispositivi mobili.<br /><br /> Per i passaggi relativi alla configurazione di questo certificato, vedere [Deploying the Enrollment Certificate for Mobile Devices](#BKMK_mobiledevices2008_cm2012) in questo argomento.|  
|Certificati per Intel AMT|Esistono tre certificati correlati alla gestione fuori banda per computer basati su Intel AMT: Un certificato di provisioning AMT, un certificato del server Web AMT e, facoltativamente, un certificato di autenticazione client per reti cablate o wireless 802.1 X.<br /><br /> È necessario installare il certificato di provisioning AMT esternamente da System Center Configuration Manager, nel computer del punto di servizio fuori banda, e selezionare il certificato installato nelle proprietà del punto di servizio fuori banda. Il certificato del server Web AMT e il certificato di autenticazione client vengono installati durante la gestione e il provisioning AMT e, successivamente, è necessario selezionare i modelli di certificato configurati nelle proprietà del componente di gestione fuori banda.<br /><br /> Per i passaggi relativi alla configurazione di questi certificati, vedere [Distribuzione dei certificati per AMT](#BKMK_AMT2008_cm2012) in questo argomento.|  
|Certificato client per computer Mac|È possibile richiedere e installare questo certificato da un computer Mac quando si usa la registrazione di System Center Configuration Manager e selezionare il modello di certificato configurato come impostazione client dei dispositivi mobili.<br /><br /> Per i passaggi relativi alla configurazione di questo certificato, vedere [Deploying the Client Certificate for Mac Computers](#BKMK_MacClient_SP1) in questo argomento.|  

##  <a name="a-namebkmkwebserver2008cm2012a-deploying-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Per creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  

-   Richiesta del certificato del server Web  

-   Configurazione di IIS per l'utilizzo del certificato del server Web  

###  <a name="a-namebkmkwebserver22008a-creating-and-issuing-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Per creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  
 Questa procedura crea un modello di certificato per i sistemi del sito di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza denominato **Server IIS di ConfigMgr** che contenga i server membro per installare i sistemi del sito di System Center Configuration Manager che eseguiranno IIS.  

2.  Sul server membro con il ruolo Servizi certificati installato nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato** , quindi su **Gestisci** per caricare la console **Modelli di certificato** .  

3.  All'interno del riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **Server Web** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati Web che saranno utilizzati sui sistemi del sito di Configuration Manager, come **Certificato server Web ConfigMgr**.  

6.  Fare clic sulla scheda **Nome oggetto** e verificare che **Inserisci nella richiesta** sia selezionato.  

7.  Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins**.  

8.  Fare clic su **Aggiungi**, immettere **Server IIS ConfigMgr** nella casella di testo, quindi fare clic su **OK**.  

9. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

10. Fare clic su **OK**e chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato server Web ConfigMgr**, quindi fare clic su **OK**.  

13. Se non è necessario creare ed emettere un altro certificato, chiudere **Autorità di certificazione**.  

###  <a name="a-namebkmkwebserver32008a-requesting-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Richiesta del certificato del server Web  
 Questa procedura consente di specificare i valori FQDN intranet e Internet che saranno configurati nelle proprietà del server del sistema del sito, quindi permette di installare il certificato del server Web sul server membro che esegue IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Per richiedere il certificato del server Web  

1.  Riavviare il server membro che esegue IIS per assicurarsi che il computer possa accedere al modello di certificato creato utilizzando le autorizzazioni **Lettura** e **Registrazione** configurate.  

2.  Fare clic su **Start**, quindi fare clic su **Esegui**e digitare **mmc.exe** . Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

4.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

5.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata e quindi fare clic su **Fine**.  

6.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

7.  Nella console, espandere **Certificati (computer locale)**, quindi fare clic su **Personale**.  

8.  Fare clic con il pulsante destro del mouse su **Certificati**, **Tutte le attività**, quindi su **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato** , fare clic su **Avanti**.  

11. Nella pagina **Richiedi certificati** identificare il **Certificato server Web ConfigMgr** dall'elenco dei certificati visualizzati e quindi fare clic su **Sono necessarie ulteriori informazioni per registrare il certificato. Per configurare le impostazioni, fare clic qui**.  

12. Nella finestra di dialogo **Proprietà certificato** della scheda **Oggetto** , non apportare alcuna modifica in **Nome oggetto**. Ciò significa che la casella **Valore** per la sezione **Nome oggetto** rimane vuota. Al contrario, nella sezione **Nome alternativo** , fare clic sull'elenco a discesa **Tipo** , quindi selezionare **DNS**.  

13. Nella casella **Valore** specificare i valori FQDN che saranno indicati nelle proprietà del sistema del sito di System Center Configuration Manager e fare clic su **OK** per chiudere la finestra di dialogo **Proprietà certificato**.  

     Esempi:  

    -   Se il sistema del sito accetterà solo connessioni client da intranet e l'FQDN intranet del server del sistema del sito è **server1.internal.contoso.com**: Digitare **server1.internal.contoso.com**, quindi fare clic su **Aggiungi**.  

    -   Se il sistema del sito accetterà connessioni client da intranet e Internet e l'FQDN intranet del server del sistema del sito è **server1.internal.contoso.com** e l'FQDN Internet del server del sistema del sito è **server.contoso.com**:  

        1.  Digitare **server1.internal.contoso.com**, quindi fare clic su **Aggiungi**.  

        2.  Digitare **server.contoso.com**, quindi fare clic su **Aggiungi**.  

        > [!NOTE]  
        >  L'ordine con cui si specificano gli FQDN non è importante per System Center Configuration Manager. Tuttavia, controllare che tutti i dispositivi che utilizzeranno il certificato, come dispositivi mobili e server Web proxy, possano utilizzare un certificato SAN e più valori nel SAN. Se i dispositivi hanno un supporto limitato per i valori SAN nei certificati, potrebbe essere necessario cambiare l'ordine degli FQDN oppure utilizzare in alternativa il valore soggetto.  

14. Nella pagina **Richiedi certificati** , selezionare **Certificato server Web ConfigMgr** dall'elenco dei certificati visualizzati, quindi fare clic su **Registrazione**.  

15. Nella pagina **Risultati installazione certificati** , attendere il completamento dell'installazione del certificato, quindi fare clic su **Fine**.  

16. Chiudere **Certificati (computer locale)**.  

###  <a name="a-namebkmkwebserver42008a-configuring-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Configurazione di IIS per l'utilizzo del certificato del server Web  
 Questa procedura consente di associare il certificato installato nel **Sito Web predefinito**di IIS.  

##### <a name="to-configure-iis-to-use-the-web-server-certificate"></a>Per configurare IIS per l'utilizzo del certificato del server Web  

1.  Sul server membro su cui è installato IIS, fare clic su **Avvia**, su **Programmi**, su **Strumenti di amministrazione**, quindi su **Gestione Internet Information Services (IIS)**.  

2.  Espandere **Siti**, fare clic con il pulsante destro del mouse su **Sito Web predefinito**, quindi selezionare **Modifica binding**.  

3.  Fare clic sulla voce **https** , quindi su **Modifica**.  

4.  Nella finestra di dialogo **Modifica binding sito** , selezionare il certificato richiesto utilizzando, il modello dei Certificati server Web ConfigMgr, quindi fare clic su **OK**.  

    > [!NOTE]  
    >  Se non si è certi di quale sia il certificato corretto, selezionarne uno e fare clic su **Visualizza**. In questo modo, è possibile confrontare i dettagli del certificato selezionato con i certificati visualizzati con lo snap-in Certificati. Ad esempio, lo snap-in Certificati visualizza il modello di certificato che è stato usato per richiedere il certificato. È possibile quindi confrontare l'identificazione personale del certificato richiesto con il modello dei Certificati server Web ConfigMgr con l'identificazione personale del certificato attualmente selezionato nella finestra di dialogo **Modifica binding sito** .  

5.  Fare clic su **OK** nella finestra di dialogo **Modifica binding sito** , quindi su **Chiudi**.  

6.  Chiudere **Gestione Internet Information Services (IIS)**.  

 Viene ora eseguito il provisioning del server membro con un modello di certificato server Web di System Center Configuration Manager.  

> [!IMPORTANT]  
>  Quando si installa il server del sistema del sito di System Center Configuration Manager in questo computer, assicurarsi di specificare nelle proprietà del sistema del sito gli stessi FQDN indicati al momento della richiesta del certificato.  

##  <a name="a-namebkmkclouddp2008cm2012a-deploying-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Distribuzione del certificato di servizio per i punti di distribuzione basati su cloud  

> [!NOTE]  
>  Il certificato di servizio per i punti di distribuzione basati sul cloud si applica a System Center Configuration Manager SP1 e alle versioni successive.  

 La distribuzione di questo certificato prevede le procedure seguenti:  

-   [Creazione ed emissione di un modello di certificato del server Web personalizzato nell'autorità di certificazione](#BKMK_clouddpcreating2008)  

-   [Richiesta del certificato del server Web personalizzato](#BKMK_clouddprequesting2008)  

-   [Esportazione del certificato del server Web personalizzato per i punti di distribuzione basati su Cloud](#BKMK_clouddpexporting2008)  

###  <a name="a-namebkmkclouddpcreating2008a-creating-and-issuing-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Creazione ed emissione di un modello di certificato del server Web personalizzato nell'autorità di certificazione  
 Questa procedura consente di creare un modello di certificato personalizzato basato sul modello del certificato del server Web. Il certificato è valido per i punti di distribuzione di System Center Configuration Manager basati sul cloud. La chiave privata deve essere esportabile. Dopo aver creato il modello di certificato, viene aggiunto all'autorità di certificazione.  

> [!NOTE]  
>  Questa procedura utilizza un modello di certificato diverso da quello del certificato del server Web creato per i sistemi del sito su cui è in esecuzione IIS, perché nonostante entrambi i certificati richiedano la funzionalità di autenticazione del server, il certificato con punti di distribuzione basati su cloud richiede all'utente di immettere un valore personalizzato definito per il Nome oggetto e la chiave privata deve essere esportata. Come procedura consigliata di sicurezza, non configurare i modelli di certificato per consentire l'esportazione della chiave privata a meno che questa configurazione non sia necessaria. Il punto di distribuzione basato su cloud richiede questa configurazione in quanto è necessario importare il certificato come file, anziché selezionarlo dall'archivio certificati.  
>   
>  Creando un nuovo modello di certificato per questo certificato, è possibile limitare il numero dei computer che richiedono un certificato che consenta l'esportazione della chiave privata. In una rete di produzione, è inoltre possibile aggiungere le seguenti modifiche per questo certificato:  
>   
>  -   Richiedere l'approvazione per installare il certificato per una maggiore sicurezza.  
> -   Aumentare il periodo di validità del certificato. Poiché è necessario esportare e importare il certificato ogni volta che scade, l'aumento del periodo di validità riduce la frequenza di ripetizione di questa procedura. Tuttavia, quando si aumenta il periodo di validità, tale operazione riduce la sicurezza del certificato perché si fornisce un tempo maggiore all'autore di un attacco per decrittografare la chiave privata e rubare il certificato.  
> -   Utilizzare un valore personalizzato nel nome alternativo del soggetto (SAN) del certificato per distinguere questo certificato dai certificati del server Web standard che si utilizzano con IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello del certificato del server Web personalizzato nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza denominato **Server del sito di ConfigMgr** che contenga i server membro per installare i server del sito primario di System Center Configuration Manager che gestiranno i punti di distribuzione basati sul cloud.  

2.  Sul server membro su cui è in esecuzione la console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console di gestione Modelli di certificato.  

3.  All'interno del riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **Server Web** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati del server Web per i punti di distribuzione basati su cloud, come **Certificato del punto di distribuzione basato su cloud di ConfigMgr**.  

6.  Fare clic sulla scheda **Gestione richiesta** e selezionare **Rendi la chiave privata esportabile**.  

7.  Fare clic sulla scheda **Sicurezza** e rimuovere l'autorizzazione **Registrazione** dal gruppo di protezione **Enterprise Admins** .  

8.  Fare clic su **Aggiungi**, immettere **Server del sito di ConfigMgr** nella casella di testo, quindi fare clic su **OK**.  

9. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

10. Fare clic su **OK** e chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato del punto di distribuzione basato su cloud di ConfigMgr**, quindi fare clic su **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="a-namebkmkclouddprequesting2008a-requesting-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Richiesta del certificato del server Web personalizzato  
 Questa procedura richiede e installa il certificato del server Web personalizzato sul server membro sul quale andrà in esecuzione il server del sito.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Per richiedere il certificato del server Web  

1.  Riavviare il server membro dopo aver creato e configurato il gruppo di protezione **Server del sito di ConfigMgr** per garantire che il computer possa accedere al modello di certificato creato, utilizzando le autorizzazioni **Lettura** e **Registrazione** configurate.  

2.  Fare clic su **Start**, quindi fare clic su **Esegui**e digitare **mmc.exe** . Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

4.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

5.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata e quindi fare clic su **Fine**.  

6.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

7.  Nella console, espandere **Certificati (computer locale)**, quindi fare clic su **Personale**.  

8.  Fare clic con il pulsante destro del mouse su **Certificati**, **Tutte le attività**, quindi su **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato** , fare clic su **Avanti**.  

11. Nella pagina **Richiedi certificati** identificare il **Certificato del punto di distribuzione basato su cloud di ConfigMgr** dall'elenco dei certificati visualizzati e quindi fare clic su **Sono necessarie ulteriori informazioni per registrare il certificato. Per configurare le impostazioni, fare clic qui**.  

12. Nella finestra di dialogo **Proprietà certificato** , nella scheda **Oggetto** , per il **Nome oggetto**, selezionare **Nome comune** come **Tipo**.  

13. Nella casella **Valore** , specificare la scelta del nome del servizio e il nome del dominio utilizzando un formato FQDN. Ad esempio, **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Non ha importanza quale nome di servizio si utilizza, purché sia univoco nello spazio dei nomi. Si utilizzerà il DNS per creare un alias (record CNAME) per il mapping del nome di questo servizio su un identificatore generato automaticamente (GUID) e un indirizzo IP di Windows Azure.  

14. Fare clic su **Aggiungi**, quindi su **OK** per chiudere la finestra di dialogo **Proprietà significato** .  

15. Nella pagina **Richiedi certificati** , selezionare **Certificato del punto di distribuzione basato su cloud di ConfigMgr** dall'elenco dei certificati visualizzati, quindi fare clic su **Registrazione**.  

16. Nella pagina **Risultati installazione certificati** , attendere il completamento dell'installazione del certificato, quindi fare clic su **Fine**.  

17. Chiudere **Certificati (computer locale)**.  

###  <a name="a-namebkmkclouddpexporting2008a-exporting-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Esportazione del certificato del server Web personalizzato per i punti di distribuzione basati su Cloud  
 Questa procedura consente di esportare il certificato del server Web personalizzato in un file in modo da importarlo al momento della creazione di un punto di distribuzione basato su cloud.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Per esportare il certificato del server Web personalizzato per i punti di distribuzione basati su cloud  

1.  Nella console **Certificati (computer locale)** , fare clic con il pulsante destro del mouse sul certificato appena installato, selezionare **Tutte le attività**, quindi fare clic su **Esporta**.  

2.  Nell'Esportazione guidata certificati, fare clic su **Avanti**.  

3.  Nella pagina **Esportazione della chiave privata con il certificato** , seleziona **Sì, esporta la chiave privata**, quindi fare clic su **Avanti**.  

    > [!NOTE]  
    >  Se questa opzione non è disponibile, il certificato è stato creato senza l'opzione per esportare la chiave privata. In questo scenario, non è possibile esportare il certificato nel formato richiesto. È necessario riconfigurare il modello di certificato per consentire l'esportazione della chiave e richiedere di nuovo il certificato.  

4.  Nella pagina **Formato file di esportazione** , assicurarsi che sia selezionata l'opzione **Scambio di informazioni personali - PKCS #12 (.PFX)** .  

5.  Nella pagina **Password** , specificare una password complessa per proteggere il certificato esportato con la relativa chiave privata, quindi fare clic su **Avanti**.  

6.  Nella pagina **File da esportare** , specificare il nome del file che si desidera esportare, quindi fare clic su **Avanti**.  

7.  Per chiudere la procedura guidata, fare clic su **Fine** nella pagina **Esportazione guidata certificato** , quindi fare clic su **OK** nella finestra di conferma.  

8.  Chiudere **Certificati (computer locale)**.  

9. Archiviare il file in modo protetto e assicurarsi che sia possibile accedervi dalla console di System Center Configuration Manager.  

 Il certificato è ora pronto per essere importato quando si crea un punto di distribuzione basato su cloud.  

##  <a name="a-namebkmkclient2008cm2012a-deploying-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Distribuzione del certificato client per computer Windows  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creazione ed emissione del modello di certificato di autenticazione della workstation nell'autorità di certificazione  

-   Configurazione della registrazione automatica del modello di autenticazione della workstation utilizzando i criteri di gruppo  

-   Registrazione automatica del certificato di autenticazione della workstation e verifica della sua installazione sui computer  

###  <a name="a-namebkmkclient02008a-creating-and-issuing-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Creazione ed emissione del modello di certificato di autenticazione della workstation nell'autorità di certificazione  
 Questa procedura crea un modello di certificato per i computer client di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello del certificato di autenticazione della workstation nell'autorità di certificazione  

1.  Sul server membro su cui è in esecuzione la console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console di gestione Modelli di certificato.  

2.  All'interno del riquadro dei risultati, fare clic con il pulsante destro del mouse sulla voce che visualizza **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

3.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

4.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati client che saranno utilizzati sui computer client di Configuration Manager, come **Certificato client di ConfigMgr**.  

5.  Fare clic sulla scheda **Sicurezza** , selezionare il gruppo **Computer del dominio** , quindi selezionare le autorizzazioni aggiuntive di **Lettura** e **Registrazione automatica**. Non deselezionare **Registrazione**.  

6.  Fare clic su **OK** e chiudere la console **Modelli di certificato**.  

7.  Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

8.  Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato client di ConfigMgr**, quindi fare clic su **OK**.  

9. Se non è necessario creare ed emettere un altro certificato, chiudere **Autorità di certificazione**.  

###  <a name="a-namebkmkclient12008a-configuring-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Configurazione della registrazione automatica del modello di autenticazione della workstation utilizzando i criteri di gruppo  
 Questa procedura consente di configurare i criteri di gruppo per registrare automaticamente il certificato client sui computer.  

##### <a name="to-configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Per configurare la registrazione automatica del modello di autenticazione della workstation utilizzando i criteri di gruppo  

1.  Nel controller di dominio, fare clic su **Avvia**, su **Strumenti di amministrazione**, quindi su **Gestione criteri di gruppo**.  

2.  Passare al dominio in questione, fare clic con il pulsante destro del mouse su di esso, quindi selezionare **Crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento**.  

    > [!NOTE]  
    >  Questo passaggio consente di utilizzare la procedura consigliata per creare nuovi criteri di gruppo per le impostazioni personalizzate piuttosto che modificare i criteri dominio predefiniti installati con i Servizi di dominio Active Directory. Assegnando questi criteri di gruppo al livello di dominio, essi verranno applicati a tutti i computer nel dominio. Tuttavia, in un ambiente di produzione, è possibile limitare la registrazione automatica in modo che avvenga solo su computer selezionati, assegnando i criteri di gruppo a livello di unità organizzativa, oppure è possibile filtrare i criteri di gruppo del dominio con un gruppo di protezione in modo che vengano applicati solo ai computer di quel gruppo. Se si limita la registrazione automatica, ricordarsi di includere il server configurato come il punto di gestione.  

3.  Nella finestra di dialogo **Nuovo oggetto Criteri di gruppo** , immettere un nome per i nuovi Criteri di gruppo, come ad esempio **Registrazione automatica certificati**e fare clic su **OK**.  

4.  Nel riquadro dei risultati, nella scheda **Oggetti Criteri di gruppo collegati** , fare clic sol il pulsante destro del mouse sui nuovi Criteri di gruppo, quindi fare clic su **Modifica**.  

5.  Nella finestra di dialogo **Editor Gestione Criteri di gruppo**, espandere **Criteri** in **Configurazione computer**, quindi andare a **Impostazioni Windows** / **Impostazioni di protezione** / **Public Key Criteri**.  

6.  Fare clic con il pulsante destro del mouse sul tipo di oggetto denominato **Client Servizi certificati - Registrazione automatica** e fare clic su **Proprietà**.  

7.  Dall'elenco a discesa **Modello configurazione** , selezionare **Attivato**, **Rinnova i certificati scaduti, aggiorna quelli in sospeso e rimuovi i certificati revocati**, **Aggiorna i certificati che utilizzano modelli di certificato**, quindi fare clic su **OK**.  

8.  Chiudere **Gestione criteri di gruppo**.  

###  <a name="a-namebkmkclient22008a-automatically-enrolling-the-workstation-authentication-certificate-and-verifying-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Registrazione automatica del certificato di autenticazione della workstation e verifica della sua installazione sui computer  
 Questa procedura consente di installare il certificato del client nei computer e verifica l'installazione.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Per registrare automaticamente il certificato di autenticazione della workstation e verificare la sua installazione nel computer client  

1.  Riavviare il computer della workstation e attendere alcuni minuti prima di effettuare l'accesso.  

    > [!NOTE]  
    >  Il riavvio di un computer è il metodo più affidabile per un registrazione automatica dei certificati corretta.  

2.  Accedere con un account che abbia privilegi amministrativi.  

3.  Nella casella di ricerca, digitare **mmc.exe.**, quindi premere **Invio**.  

4.  Nella console di gestione vuota, fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

5.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

6.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

7.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi fare clic su **Fine**.  

8.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

9. Nella console, espandere **Certificati (computer locale)**, espandere **Personale**, quindi fare clic su **Certificati**.  

10. Nel riquadro dei risultati, confermare che venga visualizzato un certificato con **Autenticazione client** visualizzato nella colonna **Scopo designato** e che **Certificato client di ConfigMgr** venga visualizzato nella colonna **Modello di certificato** .  

11. Chiudere **Certificati (computer locale)**.  

12. Ripetere i passaggi da 1 a 11 per il server membro per verificare che anche il server che verrà configurato come punto di gestione disponga di un certificato client.  

 Viene ora eseguito il provisioning del computer con un certificato client di System Center Configuration Manager.  

##  <a name="a-namebkmkclientdistributionpoint2008cm2012a-deploying-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Distribuzione del certificato client per punti di distribuzione  

> [!NOTE]  
>  Questo certificato può essere utilizzato anche per le immagini di supporto che non utilizzano l'avvio PXE, perché i requisiti del certificato sono gli stessi.  

 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creazione ed emissione di un modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  

-   Richiesta del certificato di autenticazione Workstation personalizzato  

-   Esportazione del certificato client per punti di distribuzione  

###  <a name="a-namebkmkclientdistributionpoint02008a-creating-and-issuing-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Creazione ed emissione di un modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  
 Questa procedura crea un modello di certificato personalizzato per i punti di distribuzione di System Center Configuration Manager che consente l'esportazione della chiave privata e l'aggiunta del modello di certificato all'autorità di certificazione.  

> [!NOTE]  
>  Questa procedura utilizza un modello di certificato diverso dal modello di certificato creato per i computer client, perché nonostante entrambi i certificati richiedano la funzionalità di autenticazione client, il certificato per i punti di distribuzione richiede l'esportazione della chiave privata. Come procedura consigliata di sicurezza, non configurare i modelli di certificato per consentire l'esportazione della chiave privata a meno che questa configurazione non sia necessaria. Il punto di distribuzione richiede questa configurazione in quanto è necessario importare il certificato come file, anziché selezionarlo dall'archivio certificati.  
>   
>  Creando un nuovo modello di certificato per questo certificato, è possibile limitare il numero dei computer che richiedono un certificato che consenta l'esportazione della chiave privata. Nel nostro esempio di distribuzione questo sarà il gruppo di sicurezza precedentemente creato per i server del sistema del sito di System Center Configuration Manager che eseguono IIS. In una rete di produzione che distribuisce i ruoli del sistema del sito IIS, creare un nuovo gruppo di protezione per i server su cui sono in esecuzione i punti di distribuzione in modo che sia possibile limitare il certificato solo a questi server del sistema del sito. È possibile anche aggiungere le seguenti modifiche per questo certificato:  
>   
>  -   Richiedere l'approvazione per installare il certificato per una maggiore sicurezza.  
> -   Aumentare il periodo di validità del certificato. Poiché è necessario esportare e importare il certificato ogni volta che scade, l'aumento del periodo di validità riduce la frequenza di ripetizione di questa procedura. Tuttavia, quando si aumenta il periodo di validità, tale operazione riduce la sicurezza del certificato perché si fornisce un tempo maggiore all'autore di un attacco per decrittografare la chiave privata e rubare il certificato.  
> -   Utilizzare un valore personalizzato nel campo Oggetto del certificato o Nome alternativo del soggetto (SAN) per identificare questo certificato dai certificati client standard. Può essere particolarmente utile se si utilizza lo stesso certificato per più punti di distribuzione.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  

1.  Sul server membro su cui è in esecuzione la console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console di gestione Modelli di certificato.  

2.  All'interno del riquadro dei risultati, fare clic con il pulsante destro del mouse sulla voce che visualizza **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

3.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

4.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati di autenticazione client per i punti di distribuzione, come **Certificato del punto di distribuzione di ConfigMgr**.  

5.  Fare clic sulla scheda **Gestione richiesta** e selezionare **Rendi la chiave privata esportabile**.  

6.  Fare clic sulla scheda **Sicurezza** e rimuovere l'autorizzazione **Registrazione** dal gruppo di protezione **Enterprise Admins** .  

7.  Fare clic su **Aggiungi**, immettere **Server IIS ConfigMgr** nella casella di testo, quindi fare clic su **OK**.  

8.  Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

9. Fare clic su **OK** e chiudere la console **Modelli di certificato**.  

10. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

11. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato del punto di distribuzione di ConfigMgr**, quindi fare clic su **OK**.  

12. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="a-namebkmkclientdistributionpoint12008a-requesting-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Richiesta del certificato di autenticazione Workstation personalizzato  
 Questa procedura richiede e installa il certificato client personalizzato sul server membro su cui sono in esecuzione gli IIS e che verrà configurato come punto di distribuzione.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Per richiedere il certificato di autenticazione della workstation personalizzato  

1.  Fare clic su **Start**, quindi fare clic su **Esegui**e digitare **mmc.exe** . Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

2.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

3.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

4.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata e quindi fare clic su **Fine**.  

5.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

6.  Nella console, espandere **Certificati (computer locale)**, quindi fare clic su **Personale**.  

7.  Fare clic con il pulsante destro del mouse su **Certificati**, **Tutte le attività**, quindi su **Richiedi nuovo certificato**.  

8.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

9. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato** , fare clic su **Avanti**.  

10. Nella pagina **Richiedi certificati** , selezionare **Certificato del punto di distribuzione di ConfigMgr** dall'elenco dei certificati visualizzati, quindi fare clic su **Registrazione**.  

11. Nella pagina **Risultati installazione certificati** , attendere il completamento dell'installazione del certificato, quindi fare clic su **Fine**.  

12. Nel riquadro dei risultati, confermare che venga visualizzato un certificato con **Autenticazione client** visualizzato nella colonna **Scopo designato** e che **Certificato del punto di distribuzione di ConfigMgr** venga visualizzato nella colonna **Modello di certificato** .  

13. Non chiudere **Certificati (computer locale)**.  

###  <a name="a-namebkmkexportclientdistributionpoint22008a-exporting-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Esportazione del certificato client per punti di distribuzione  
 Questa procedura consente di esportare il certificato di autenticazione della workstation personalizzato in un file, in modo che possa essere importato nelle proprietà del punto di distribuzione.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Per esportare il certificato client per i punti di distribuzione  

1.  Nella console **Certificati (computer locale)** , fare clic con il pulsante destro del mouse sul certificato appena installato, selezionare **Tutte le attività**, quindi fare clic su **Esporta**.  

2.  Nell'Esportazione guidata certificati, fare clic su **Avanti**.  

3.  Nella pagina **Esportazione della chiave privata con il certificato** , seleziona **Sì, esporta la chiave privata**, quindi fare clic su **Avanti**.  

    > [!NOTE]  
    >  Se questa opzione non è disponibile, il certificato è stato creato senza l'opzione per esportare la chiave privata. In questo scenario, non è possibile esportare il certificato nel formato richiesto. È necessario riconfigurare il modello di certificato per consentire l'esportazione della chiave e richiedere di nuovo il certificato.  

4.  Nella pagina **Formato file di esportazione** , assicurarsi che sia selezionata l'opzione **Scambio di informazioni personali - PKCS #12 (.PFX)** .  

5.  Nella pagina **Password** , specificare una password complessa per proteggere il certificato esportato con la relativa chiave privata, quindi fare clic su **Avanti**.  

6.  Nella pagina **File da esportare** , specificare il nome del file che si desidera esportare, quindi fare clic su **Avanti**.  

7.  Per chiudere la procedura guidata, fare clic su **Fine** nella pagina **Esportazione guidata certificato** , quindi fare clic su **OK** nella finestra di conferma.  

8.  Chiudere **Certificati (computer locale)**.  

9. Archiviare il file in modo protetto e assicurarsi che sia possibile accedervi dalla console di System Center Configuration Manager.  

 Il certificato è ora pronto per essere importato quando si configura il punto di distribuzione.  

> [!TIP]  
>  È possibile utilizzare lo stesso file del certificato quando si configurano le immagini di supporto per la distribuzione di un sistema operativo che non utilizza l'avvio PXE e la sequenza attività per installare l'immagine deve contattare un punto di gestione che richieda connessioni client HTTPS.  

##  <a name="a-namebkmkmobiledevices2008cm2012a-deploying-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Distribuzione del certificato di registrazione per i dispositivi mobili  
 Questa distribuzione del certificato dispone di una sola procedura per creare ed emettere il modello del certificato di registrazione nell'autorità di certificazione.  

### <a name="creating-and-issuing-the-enrollment-certificate-template-on-the-certification-authority"></a>Creazione ed emissione del modello di certificato di registrazione nell'autorità di certificazione  
 Questa procedura crea un modello di certificato di registrazione per i dispositivi mobili di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato di registrazione nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza che contenga gli utenti che registreranno i dispositivi mobili in System Center Configuration Manager.  

2.  Sul server membro con i Servizi certificati installati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console di gestione Modelli di certificato.  

3.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse sulla voce che visualizza **Sessione autenticata** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** immettere un nome di modello per generare i certificati di registrazione per i dispositivi mobili che saranno gestiti da System Center Configuration Manager, ad esempio **Certificato di registrazione del dispositivo mobile di ConfigMgr**.  

6.  Fare clic sulla scheda **Nome soggetto** , verificare che l'opzione **Crea in base alle informazioni di Active Directory** sia selezionata, selezionare **Nome comune** per **Formato del nome soggetto:** e cancellare **Nome entità utente (UPN)** da **Includere le seguenti informazioni nel nome soggetto alternativo**.  

7.  Fare clic sulla scheda **Sicurezza** , selezionare il gruppo di sicurezza che contiene gli utenti che devono registrare dei dispositivi mobili e selezionare l'autorizzazione aggiuntiva di **Registrazione**. Non deselezionare **Lettura**.  

8.  Fare clic su **OK** e chiudere la console **Modelli di certificato**.  

9. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

10. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato di registrazione del dispositivo mobile di ConfigMgr**, quindi fare clic su **OK**.  

11. Se non è necessario creare ed emettere un altro certificato, chiudere la console Autorità di certificazione.  

 Il modello di certificato di registrazione del dispositivo mobile è ora pronto per essere selezionato quando si configura un profilo di registrazione del dispositivo mobile nelle impostazioni client.  

##  <a name="a-namebkmkamt2008cm2012a-deploying-the-certificates-for-amt"></a><a name="BKMK_AMT2008_cm2012"></a> Distribuzione dei certificati per AMT  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creazione, emissione e installazione del certificato di provisioning AMT  

-   Creazione ed emissione del certificato del server Web per computer basati su AMT  

-   Creazione ed emissione dei certificati di autenticazione client per computer basati su AMT 802.1X  

###  <a name="a-namebkmkamtprovisioning2008a-creating-issuing-and-installing-the-amt-provisioning-certificate"></a><a name="BKMK_AMTprovisioning2008"></a> Creating, Issuing, and Installing the AMT Provisioning Certificate  
 Creare il certificato di provisioning con autorità di certificazione (CA) interna quando i computer basati su AMT sono configurati con l'identificazione personale del certificato della CA radice interna. Se non è possibile e occorre usare un'autorità di certificazione esterna, seguire le istruzioni della società che emette il certificato di provisioning AMT. In questo caso è spesso necessario richiedere il certificato sul sito Web pubblico della società. È inoltre possibile trovare istruzioni dettagliate per la prescelta CA esterna in Intel vPro Expert Center: sito Web Microsoft vPro Manageability ([http://go.microsoft.com/fwlink/?LinkId=132001](http://go.microsoft.com/fwlink/?LinkId=132001)).  

> [!IMPORTANT]  
>  Le CA esterne potrebbero non supportare l'identificatore di oggetto provisioning Intel AMT. Quando ciò è possibile, come metodo alternativo fornire l'attributo OU del **certificato di installazione client di Intel (R)**.  

 Quando si richiede un certificato di provisioning AMT da una CA esterna, installare il certificato nell'archivio certificati personale del computer sul server membro che ospiterà il punto di servizio fuori banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Per richiedere ed emettere il certificato di provisioning AMT  

1.  Creare un gruppo di protezione che contenga gli account computer dei server del sistema del sito che eseguiranno il punto di servizio fuori banda.  

2.  Sul server membro con Servizi certificati installato nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console **Modelli di certificato** .  

3.  All'interno del riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **Server Web** nella colonna **Nome visualizzato modello** , quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per il modello del certificato di provisioning AMT, come **Provisioning AMT di ConfigMgr**.  

6.  Fare clic sulla scheda **Nome oggetto** , selezionare **Crea in base alle informazioni di Active Directory**, quindi selezionare **Nome comune**.  

7.  Fare clic sulla scheda **Estensioni** , assicurarsi che sia selezionato **Criteri di applicazione** , quindi fare clic su **Modifica**.  

8.  Nella finestra di dialogo **Modifica estensione criteri di applicazione** , fare clic su **Aggiungi**.  

9. Nella finestra di dialogo **Aggiunta criterio di applicazione** fare clic su **Nuovo**.  

10. Nella finestra di dialogo **Nuovo criterio di applicazione** , digitare **Provisioning AMT** nel campo **Nome** , quindi digitare il numero che segue per l' **Identificatore oggetto**: **2.16.840.1.113741.1.2.3**.  

11. Fare clic su **OK**, quindi su **OK** nella finestra di dialogo **Aggiunta criterio di applicazione** .  

12. Fare clic su **OK** nella finestra di dialogo **Modifica estensione criteri di applicazione** .  

13. Nella finestra di dialogo **Proprietà nuovo modello** , si dovrebbe ora visualizzare quanto segue in elenco come descrizione dei **Criteri di applicazione** : **Autenticazione server** e **Provisioning AMT**.  

14. Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins**.  

15. Fare clic su **Aggiungi**, immettere il nome di un gruppo di protezione che contenga l'account computer account per il ruolo del sistema del sito del punto di servizio fuori banda, quindi fare clic su **OK**.  

16. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

17. Fare clic su **OK**e chiudere la console **Modelli di certificato** .  

18. In **Autorità di certificazione**, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

19. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Provisioning AMT di ConfigMgr**, quindi fare clic su **OK**.  

    > [!NOTE]  
    >  Se non è possibile completare i passaggi 18 o 19, controllare che si stia usando Enterprise Edition di Windows Server 2008. Nonostante si possano configurare modelli con Windows Server Standard Edition e Servizi certificati, non è possibile distribuire certificati usando modelli di certificati modificati a meno che non si stia utilizzando Enterprise Edition di Windows Server 2008.  

20. Non chiudere **Autorità di certificazione**.  

 Il certificato di provisioning AMT dalla CA interna è ora pronto per essere installato nel computer del punto di servizio di banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Per installare il certificato di provisioning AMT  

1.  Riavviare il server membro su cui è in esecuzione IIS, per assicurarsi che possa accedere al modello di certificato con l'autorizzazione configurata.  

2.  Fare clic su **Start**, quindi fare clic su **Esegui**e digitare **mmc.exe** . Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

4.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

5.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata e quindi fare clic su **Fine**.  

6.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

7.  Nella console, espandere **Certificati (computer locale)**, quindi fare clic su **Personale**.  

8.  Fare clic con il pulsante destro del mouse su **Certificati**, **Tutte le attività**, quindi su **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato** , fare clic su **Avanti**.  

11. Nella pagina **Richiedi certificati** , selezionare **Provisioning AMT** dall'elenco dei certificati visualizzati, quindi fare clic su **Registrazione**.  

12. Nella pagina **Risultati installazione certificati** , attendere il completamento dell'installazione del certificato, quindi fare clic su **Fine**.  

13. Chiudere **Certificati (computer locale)**.  

 Il certificato di provisioning AMT dalla CA interna viene ora installato ed è pronto per essere selezionato nelle proprietà del punto di servizio fuori banda.  

### <a name="creating-and-issuing-the-web-server-certificate-for-amt-based-computers"></a>Creazione ed emissione del certificato del server Web per computer basati su AMT  
 Utilizzare la procedura seguente per la preparazione dei certificati server Web per computer basati su AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Per creare ed emettere il modello di certificato del server Web  

1.  Creare un gruppo di sicurezza vuoto che contenga gli account computer AMT che System Center Configuration Manager crea durante il provisioning AMT.  

2.  Sul server membro con Servizi certificati installato nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console **Modelli di certificato** .  

3.  All'interno del riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **Server Web** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition.**  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati Web che saranno utilizzati per la gestione fuori banda sui computer AMT, come **Certificato server Web di ConfigMgr**.  

6.  Fare clic sulla scheda **Nome oggetto** , su **Crea in base alle informazioni di Active Directory**, quindi selezionare **Nome comune** per il **Formato nome oggetto**, cancellare il **Nome entità utente (UPN)** per il nome oggetto alternativo.  

7.  Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins**.  

8.  Fare clic su **Aggiungi** e immettere il nome del gruppo di protezione creato per il provisioning AMT. Fare quindi clic su **OK**.  

9. Selezionare le seguenti autorizzazioni **Consenti** per questo gruppo di protezione: **Lettura** e **Registrazione**.  

10. Fare clic su **OK**e chiudere la console **Modelli di certificato** .  

11. Nella console **Autorità di certificazione** , fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato server Web di ConfigMgr**, quindi fare clic su **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

 Il modello di server Web AMT è ora pronto per effettuare il provisioning dei computer basati su AMT con i certificati server Web. Selezionare questo modello di certificato nelle proprietà del componente della gestione fuori banda.  

### <a name="creating-and-issuing-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Creazione ed emissione dei certificati di autenticazione client per computer basati su AMT 802.1X  
 Utilizzare la procedura seguente se i computer basati su AMT utilizzeranno i certificati client per reti cablate o wireless autenticate 802.1 X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Per creare ed emettere il modello di certificato di autenticazione client nella CA  

1.  Sul server membro con Servizi certificati installato nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console **Modelli di certificato** .  

2.  All'interno del riquadro dei risultati, fare clic con il pulsante destro del mouse sulla voce che visualizza **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition.**  

3.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati client che saranno utilizzati per la gestione fuori banda sui computer AMT, come **Certificato di autenticazione client 802.1X AMT di ConfigMgr**.  

4.  Nella scheda **Nome oggetto** , fare clic su **Crea in base alle informazioni di Active Directory** , quindi selezionare **Nome comune** per il **Formato nome oggetto**. Cancellare il **Nome DNS** per il nome oggetto alternativo, quindi selezionare **Nome entità utente (UPN)**.  

5.  Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins**.  

6.  Fare clic su **Aggiungi** e immettere il nome del gruppo di protezione che si specificherà nelle proprietà del componente della gestione fuori banda, per contenere gli account dei computer basati su AMT. Fare quindi clic su **OK**.  

7.  Selezionare le seguenti autorizzazioni **Consenti** per questo gruppo di protezione: **Lettura** e **Registrazione**.  

8.  Fare clic su **OK** e chiudere la console di gestione **Modelli di certificato**, **certtmpl - [Modelli di certificato]**.  

9. Nella console di gestione **Autorità di certificazione** , fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

10. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato di autenticazione client 802.1X AMT di ConfigMgr**, quindi fare clic su **OK**.  

11. Se non è necessario creare ed emettere un altro certificato, chiudere **Autorità di certificazione**.  

 Il modello di certificato di autenticazione client è ora pronto per emettere certificati ai computer basati su AMT che possono essere utilizzati per l'autenticazione client 802.1 X. Selezionare questo modello di certificato nelle proprietà del componente della gestione fuori banda.  

##  <a name="a-namebkmkmacclientsp1a-deploying-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Distribuzione del certificato client per computer Mac  

> [!NOTE]  
>  Il certificato client per i computer Mac si applica a System Center Configuration Manager SP1 e versioni successive.  

 Questa distribuzione del certificato dispone di una sola procedura per creare ed emettere il modello del certificato di registrazione nell'autorità di certificazione.  

###  <a name="a-namebkmkmacclientcreatingissuinga-creating-and-issuing-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Creazione ed emissione di un modello di certificato client Mac nell'autorità di certificazione  
 Questa procedura crea un modello di certificato personalizzato per i computer Mac di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

> [!NOTE]  
>  Questa procedura utilizza un modello di certificato differente dal modello di certificato che potrebbe essere stato creato per i computer client di Windows o per i punti di distribuzione.  
>   
>  Creando un nuovo modello di certificato per questo certificato, è possibile limitare la richiesta di certificato agli utenti autorizzati.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato client Mac nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza che contenga gli account utenti per gli utenti amministratori che registreranno il certificato nel computer Mac usando System Center Configuration Manager.  

2.  Sul server membro su cui è in esecuzione la console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi su **Gestisci** per caricare la console di gestione Modelli di certificato.  

3.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse sulla voce che visualizza **Sessione autenticata** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** , immettere un nome modello per generare i certificati client Mac, come **Certificato client Mac di ConfigMgr**.  

6.  Fare clic sulla scheda **Nome soggetto** , verificare che l'opzione **Crea in base alle informazioni di Active Directory** sia selezionata, selezionare **Nome comune** per **Formato del nome soggetto:** e cancellare **Nome entità utente (UPN)** da **Includere le seguenti informazioni nel nome soggetto alternativo**.  

7.  Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins** .  

8.  Fare clic su **Aggiungi**, specificare il gruppo di protezione creato nel passaggio 1, quindi fare clic su **OK**.  

9. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

10. Fare clic su **OK** e chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** , selezionare il nuovo modello appena creato, **Certificato client Mac di ConfigMgr**, quindi fare clic su **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

 Il modello di certificato client Mac è ora pronto per essere selezionato quando si configurano le impostazioni client per la registrazione.



<!--HONumber=Dec16_HO3-->


