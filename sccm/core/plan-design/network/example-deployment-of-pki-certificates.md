---
title: Distribuire certificati PKI
titleSuffix: Configuration Manager
description: È disponibile un esempio dettagliato che fornisce informazioni su come creare e distribuire i certificati PKI usati in System Center Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d686baa95cc29a2e4923c0572a0d056beeff9f5b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499221"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo esempio dettagliato di distribuzione usa un'autorità di certificazione (CA) Windows Server 2008 e contiene procedure che illustrano come creare e distribuire i certificati di infrastruttura a chiave pubblica (PKI) usati in System Center Configuration Manager. Queste procedure utilizzano modelli di certificato e una CA globale (enterprise). I passaggi sono adatti esclusivamente a una rete di test, come un modello di prova.  

 Dal momento che non esiste un singolo metodo di distribuzione per i certificati richiesti, consultare la documentazione di distribuzione PKI specifica per le procedure richieste e consigliate di distribuzione dei certificati richiesti per un ambiente di produzione. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]
>  È possibile adattare le istruzioni riportate in questo argomento per sistemi operativi diversi da quelli documentati nella sezione Requisiti della rete di test. Tuttavia, se si esegue la CA emittente su Windows Server 2012, non viene richiesta la versione del modello di certificato. Al contrario, specificarla nella scheda **Compatibilità** delle proprietà del modello:  
> 
> - **Autorità di certificazione**: **Windows Server 2003**  
>   -   **Destinatario certificato**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>In questa sezione  
 Le sezioni seguenti comprendono istruzioni dettagliate di esempio per creare e distribuire i certificati seguenti che possono essere usati in System Center Configuration Manager:  

 [Requisiti della rete di test](#BKMK_testnetworkenvironment)  

 [Panoramica dei certificati](#BKMK_overview2008)  

 [Distribuire il certificato del server Web per sistemi del sito che eseguono IIS](#BKMK_webserver2008_cm2012)  

 [Distribuire il certificato di servizio per i punti di distribuzione basati su cloud](#BKMK_clouddp2008_cm2012)  

 [Distribuire il certificato client per computer Windows](#BKMK_client2008_cm2012)  

 [Distribuire il certificato client per punti di distribuzione](#BKMK_clientdistributionpoint2008_cm2012)  

 [Distribuire il certificato di registrazione per i dispositivi mobili](#BKMK_mobiledevices2008_cm2012)  

 [Distribuire i certificati per AMT](#BKMK_AMT2008_cm2012)  

 [Distribuire il certificato client per computer Mac](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a> Requisiti della rete di test  
 Nelle istruzioni dettagliate sono richiesti i seguenti requisiti:  

-   Sulla rete di test è in esecuzione il ruolo Servizi di dominio Active Directory con Windows Server 2008 e la rete è installata come un dominio singolo, una foresta singola.  

-   Si dispone di un server membro su cui è in esecuzione Windows Server 2008 Enterprise Edition, in cui è installato il ruolo Servizi certificati Active Directory e che è configurato come CA radice dell'organizzazione (enterprise).  

-   È disponibile un computer in cui sono installati Windows Server 2008 (Standard Edition o Enterprise Edition, R2 o versioni successive) e Internet Information Services (IIS) e che è designato come un server membro. Questo computer è il server del sistema del sito di System Center Configuration Manager che sarà configurato con un nome di dominio completo (FQDN) Intranet per supportare le connessioni client nella Intranet e con un FQDN Internet se è necessario supportare dispositivi mobili registrati da System Center Configuration Manager e client su Internet.  

-   Si dispone di un client Windows Vista in cui è installato il Service Pack più recente, configurato con un nome computer comprendente caratteri ASCII e associato al dominio. Questo computer è un computer client di System Center Configuration Manager.  

-   È possibile accedere con un account amministratore di dominio radice o un account amministratore di dominio organizzazione che dovrà essere usato per tutte le procedure descritte in questo esempio di distribuzione.  

##  <a name="BKMK_overview2008"></a> Panoramica dei certificati  
 Nella tabella seguente vengono elencati i tipi di certificati PKI che potrebbero essere richiesti per Center Configuration Manager e le informazioni sul loro uso.  

|Requisito del certificato|Descrizione del certificato|  
|-----------------------------|-----------------------------|  
|Certificato del server Web per i sistemi del sito che eseguono IIS|Questo certificato viene utilizzato per crittografare dati e per l'autenticazione tra server e client. Deve essere installato esternamente da System Center Configuration Manager nei server dei sistemi del sito che eseguono Internet Information Services (IIS) e che sono configurati in System Center Configuration Manager per usare HTTPS.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuire il certificato del server Web per sistemi del sito che eseguono IIS](#BKMK_webserver2008_cm2012) in questo argomento.|  
|Certificato di servizio per i client per la connessione ai punti di distribuzione basati su cloud|Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuire il certificato di servizio per i punti di distribuzione basati su cloud](#BKMK_clouddp2008_cm2012) in questo argomento.<br /><br /> **Importante:** Questo certificato viene usato in combinazione con il certificato di gestione di Microsoft Azure. Per altre informazioni sul certificato di gestione, vedere [Come creare un certificato di gestione per Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=220281) e [Come aggiungere un certificato di gestione a una sottoscrizione Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) nella sezione della piattaforma Windows Azure di MSDN Library.|  
|Certificato client per computer Windows|Questo certificato è usato per l'autenticazione tra i computer client di System Center Configuration Manager e i sistemi del sito che sono configurati per usare HTTPS. Può inoltre essere usato per il monitoraggio dello stato operativo dei punti di gestione e dei punti di migrazione stato quando sono configurati per l'uso di HTTPS. Deve essere installato esternamente da System Center Configuration Manager nei computer.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuire il certificato client per computer Windows](#BKMK_client2008_cm2012) in questo argomento.|  
|Certificato client per punti di distribuzione|Questo certificato ha due scopi:<br /><br /> Il certificato viene utilizzato per l'autenticazione tra il punto di distribuzione e un punto di gestione abilitato HTTPS prima che il punto di distribuzione invii dei messaggi di stato.<br /><br /> Quando l'opzione del punto di distribuzione **Abilita supporto PXE per i client** è selezionata, il certificato viene inviato ai computer con avvio PXE in modo che possano connettersi a un punto di gestione abilitato HTTPS durante la distribuzione del sistema operativo.<br /><br /> Per i passaggi relativi alla configurazione e installazione di questo certificato, vedere [Distribuire il certificato client per punti di distribuzione](#BKMK_clientdistributionpoint2008_cm2012) in questo argomento.|  
|Certificato di registrazione per dispositivi mobili|Questo certificato è usato per l'autenticazione tra i computer client dei dispositivi mobili di System Center Configuration Manager e i sistemi del sito che sono configurati per usare HTTPS. Deve essere installato come parte della registrazione dei dispositivi mobili in System Center Configuration Manager ed è necessario scegliere il modello di certificato configurato come impostazione client dei dispositivi mobili.<br /><br /> Per i passaggi relativi alla configurazione di questo certificato, vedere [Distribuire il certificato di registrazione per i dispositivi mobili](#BKMK_mobiledevices2008_cm2012) in questo argomento.|  
|Certificati per Intel AMT|Alla gestione fuori banda per i computer basati su Intel AMT sono correlati tre certificati:<ul><li>Un certificato di provisioning AMT (Active Management Technology)</li><li>Un certificato server Web AMT</li><li>Facoltativamente, un certificato di autenticazione client per reti cablate o wireless 802.1X</li></ul>È necessario installare il certificato di provisioning AMT esternamente da System Center Configuration Manager, nel computer del punto di servizio fuori banda, e scegliere il certificato installato nelle proprietà del punto di servizio fuori banda. Il certificato del server Web AMT e il certificato di autenticazione client vengono installati durante la gestione e il provisioning AMT e, successivamente, è necessario scegliere i modelli di certificato configurati nelle proprietà del componente di gestione fuori banda.<br /><br /> Per i passaggi relativi alla configurazione di questi certificati, vedere [Distribuire i certificati per AMT](#BKMK_AMT2008_cm2012) in questo argomento.|  
|Certificato client per computer Mac|È possibile richiedere e installare questo certificato da un computer Mac quando si usa la registrazione di System Center Configuration Manager e scegliere il modello di certificato configurato come impostazione client dei dispositivi mobili.<br /><br /> Per i passaggi relativi alla configurazione di questo certificato, vedere [Distribuire il certificato client per computer Mac](#BKMK_MacClient_SP1) in questo argomento.|  

##  <a name="BKMK_webserver2008_cm2012"></a> Distribuire il certificato del server Web per sistemi del sito che eseguono IIS  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  

-   Richiedere il certificato del server Web  

-   Configurare IIS per l'uso del certificato del server Web  

###  <a name="BKMK_webserver22008"></a> Creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  
 Questa procedura crea un modello di certificato per i sistemi del sito di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato del server Web nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza denominato **Server IIS di ConfigMgr** che contenga i server membro per l'installazione dei sistemi del sito di System Center Configuration Manager che eseguiranno IIS.  

2.  Nel server membro in cui è installato Servizi certificati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console **Modelli di certificato**.  

3.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Server Web** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato server Web ConfigMgr** per generare i certificati Web che saranno usati nei sistemi del sito di Configuration Manager.  

6.  Scegliere la scheda **Nome soggetto** e verificare che **Inserisci nella richiesta** sia selezionato.  

7.  Scegliere la scheda **Protezione** e quindi rimuovere l'autorizzazione **Registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins**.  

8.  Scegliere **Aggiungi**, immettere **Server IIS ConfigMgr** nella casella di testo, quindi scegliere **OK**.  

9. Scegliere l'autorizzazione **Registrazione** per questo gruppo e non deselezionare l'autorizzazione **Lettura**.  

10. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato server Web ConfigMgr**, quindi scegliere **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="BKMK_webserver32008"></a> Richiedere il certificato del server Web  
 Questa procedura consente di specificare i valori FQDN Intranet e Internet che saranno configurati nelle proprietà del server del sistema del sito, quindi permette di installare il certificato del server Web nel server membro che esegue IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Per richiedere il certificato del server Web  

1.  Riavviare il server membro che esegue IIS per assicurarsi che il computer possa accedere al modello di certificato creato usando le autorizzazioni **Lettura** e **Registrazione** configurate.  

2.  Fare clic su **Start**, scegliere **Esegui** e quindi digitare **mmc.exe.** Nella console vuota scegliere **File**, quindi **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **Certificati** dall'elenco **Snap-in disponibili**, quindi scegliere **Aggiungi**.  

4.  Nella finestra di dialogo **Snap-in certificati** scegliere **Account computer**, quindi scegliere **Avanti**.  

5.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi scegliere **Fine**.  

6.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **OK**.  

7.  Nella console espandere **Certificati (computer locale)**, quindi scegliere **Personale**.  

8.  Fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività**, quindi **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** scegliere **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato**, scegliere **Avanti**.  

11. Nella pagina **Richiedi certificati** identificare **Certificato server Web ConfigMgr** nell'elenco dei certificati disponibili e quindi scegliere **Sono necessarie ulteriori informazioni per registrare il certificato. Per configurare le impostazioni, fare clic qui**.  

12. Nella finestra di dialogo **Proprietà certificato** della scheda **Soggetto** non apportare alcuna modifica in **Nome soggetto**. Ciò significa che la casella **Valore** per la sezione **Nome oggetto** rimane vuota. Al contrario, nella sezione **Nome alternativo** fare clic sull'elenco a discesa **Tipo**, quindi scegliere **DNS**.  

13. Nella casella **Valore** specificare i valori FQDN che saranno indicati nelle proprietà del sistema del sito di System Center Configuration Manager e scegliere **OK** per chiudere la finestra di dialogo **Proprietà certificato**.  

     Esempi:  

    -   Se il sistema del sito accetterà solo connessioni client da intranet e l'FQDN intranet del server del sistema del sito è **server1.internal.contoso.com**, immettere **server1.internal.contoso.com**, quindi scegliere **Aggiungi**.  

    -   Se il sistema del sito accetterà connessioni client da intranet e Internet e l'FQDN intranet del server del sistema del sito è **server1.internal.contoso.com** e l'FQDN Internet del server del sistema del sito è **server.contoso.com**:  

        1.  Immettere **server1.internal.contoso.com**, quindi scegliere **Aggiungi**.  

        2.  Immettere **server.contoso.com**, quindi scegliere **Aggiungi**.  

        > [!NOTE]  
        >  È possibile specificare gli FQDN per System Center Configuration Manager in qualsiasi ordine. Tuttavia, controllare che tutti i dispositivi che useranno il certificato, come dispositivi mobili e server Web proxy, possano usare un nome alternativo del soggetto (SAN) del certificato e più valori nel SAN. Se i dispositivi hanno un supporto limitato per i valori SAN nei certificati, potrebbe essere necessario cambiare l'ordine degli FQDN oppure utilizzare in alternativa il valore soggetto.  

14. Nella pagina **Richiedi certificati** scegliere **Certificato server Web ConfigMgr** dall'elenco dei certificati disponibili, quindi scegliere **Registrazione**.  

15. Nella pagina **Risultati installazione certificati** attendere il completamento dell'installazione del certificato, quindi scegliere **Fine**.  

16. Chiudere **Certificati (computer locale)**.  

###  <a name="BKMK_webserver42008"></a> Configurare IIS per l'uso del certificato del server Web  
 Questa procedura consente di associare il certificato installato nel **Sito Web predefinito**di IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Per configurare IIS per l'uso del certificato del server Web  

1. Nel server membro in cui è installato IIS fare clic su **Start**, scegliere **Programmi**, **Strumenti di amministrazione**, quindi **Gestione Internet Information Services (IIS)**.  

2. Espandere **Siti**, fare clic con il pulsante destro del mouse su **Sito Web predefinito**, quindi scegliere **Modifica binding**.  

3. Scegliere la voce **https**, quindi scegliere **Modifica**.  

4. Nella finestra di dialogo **Modifica binding sito** selezionare il certificato richiesto usando il modello Certificati server Web ConfigMgr, quindi scegliere **OK**.  

   > [!NOTE]  
   >  Se non si è certi di quale sia il certificato corretto, sceglierne uno e quindi scegliere **Visualizza**. In questo modo è possibile confrontare i dettagli del certificato selezionato con i certificati nello snap-in Certificati. Ad esempio, lo snap-in Certificati mostra il modello di certificato che è stato usato per richiedere il certificato. È possibile quindi confrontare l'identificazione personale del certificato richiesto usando il modello Certificati server Web ConfigMgr con l'identificazione personale del certificato attualmente selezionato nella finestra di dialogo **Modifica binding sito**.  

5. Scegliere **OK** nella finestra di dialogo **Modifica binding sito**, quindi scegliere **Chiudi**.  

6. Chiudere **Gestione Internet Information Services (IIS)**.  

   A questo punto, il server membro è configurato con un certificato server Web di System Center Configuration Manager.  

> [!IMPORTANT]  
>  Quando si installa il server del sistema del sito di System Center Configuration Manager in questo computer, assicurarsi di specificare nelle proprietà del sistema del sito gli stessi FQDN indicati al momento della richiesta del certificato.  

##  <a name="BKMK_clouddp2008_cm2012"></a> Distribuire il certificato di servizio per i punti di distribuzione basati su cloud  

La distribuzione di questo certificato prevede le procedure seguenti:  

-   [Creare ed emettere il modello del certificato del server Web personalizzato nell'autorità di certificazione](#BKMK_clouddpcreating2008)  

-   [Richiedere il certificato del server Web personalizzato](#BKMK_clouddprequesting2008)  

-   [Esportare il certificato del server Web personalizzato per i punti di distribuzione basati su cloud](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a> Creare ed emettere il modello del certificato del server Web personalizzato nell'autorità di certificazione  
 Questa procedura consente di creare un modello di certificato personalizzato basato sul modello del certificato del server Web. Il certificato è valido per i punti di distribuzione di System Center Configuration Manager basati sul cloud. La chiave privata deve essere esportabile. Dopo aver creato il modello di certificato, viene aggiunto all'autorità di certificazione.  

> [!NOTE]
>  In questa procedura viene usato un modello di certificato diverso dal modello di certificato del server Web che è stato creato per i sistemi del sito che eseguono IIS. Sebbene entrambi i certificati richiedano la funzionalità di autenticazione server, il certificato per i punti di distribuzione basati su cloud richiede di immettere un valore definito in modo personalizzato per il nome del soggetto e la chiave privata deve essere esportata. Come procedura consigliata di sicurezza, non configurare i modelli di certificato per consentire l'esportazione della chiave privata, a meno che questa configurazione non sia necessaria. Il punto di distribuzione basato su cloud richiede questa configurazione in quanto è necessario importare il certificato come file, anziché sceglierlo dall'archivio certificati.  
> 
>  Quando si crea un nuovo modello di certificato per questo certificato, è possibile limitare il numero dei computer che possono richiedere un certificato che consenta l'esportazione della chiave privata. In una rete di produzione, è inoltre possibile aggiungere le seguenti modifiche per questo certificato:  
> 
> - Richiedere l'approvazione per installare il certificato per una maggiore sicurezza.  
>   -   Aumentare il periodo di validità del certificato. Poiché è necessario esportare e importare il certificato ogni volta che scade, un aumento del periodo di validità riduce la frequenza di ripetizione di questa procedura. Tuttavia, l'aumento del periodo di validità riduce anche la sicurezza del certificato, perché fornisce un tempo maggiore all'autore di un attacco per decrittografare la chiave privata e rubare il certificato.  
>   -   Utilizzare un valore personalizzato nel nome alternativo del soggetto (SAN) del certificato per distinguere questo certificato dai certificati del server Web standard che si utilizzano con IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello del certificato del server Web personalizzato nell'autorità di certificazione  

1.  Creare un gruppo di sicurezza denominato **Server del sito di ConfigMgr** che contenga i server membro per installare i server del sito primario di System Center Configuration Manager che gestiranno i punti di distribuzione basati su cloud.  

2.  Nel server membro su cui è in esecuzione la console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console di gestione Modelli di certificato.  

3.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Server Web** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5.  Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato del punto di distribuzione basato su cloud di ConfigMgr** per generare i certificati del server Web per i punti di distribuzione basati su cloud.  

6.  Scegliere la scheda **Gestione richiesta**, quindi scegliere **Rendi la chiave privata esportabile**.  

7.  Scegliere la scheda **Sicurezza** e quindi rimuovere l'autorizzazione **Registrazione** dal gruppo di sicurezza **Enterprise Admins**.  

8.  Scegliere **Aggiungi**, immettere **Server del sito di ConfigMgr** nella casella di testo, quindi scegliere **OK**.  

9. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

    > [!NOTE]
    > Assicurarsi che l'opzione **Dimensioni minime chiave** nella scheda **Crittografia** sia stata impostata su **2048**

10. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato del punto di distribuzione basato su cloud di ConfigMgr**, quindi scegliere **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="BKMK_clouddprequesting2008"></a> Richiedere il certificato del server Web  
 Questa procedura richiede e installa il certificato del server Web personalizzato nel server membro in cui sarà in esecuzione il server del sito.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Per richiedere il certificato del server Web  

1.  Riavviare il server membro dopo aver creato e configurato il gruppo di sicurezza **Server del sito di ConfigMgr** per garantire che il computer possa accedere al modello di certificato creato usando le autorizzazioni **Lettura** e **Registrazione** configurate.  

2.  Fare clic su **Start**, scegliere **Esegui** e quindi digitare **mmc.exe.** Nella console vuota scegliere **File**, quindi **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **Certificati** dall'elenco **Snap-in disponibili**, quindi scegliere **Aggiungi**.  

4.  Nella finestra di dialogo **Snap-in certificati** scegliere **Account computer**, quindi scegliere **Avanti**.  

5.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi scegliere **Fine**.  

6.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **OK**.  

7.  Nella console espandere **Certificati (computer locale)**, quindi scegliere **Personale**.  

8.  Fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività**, quindi **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** scegliere **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato**, scegliere **Avanti**.  

11. Nella pagina **Richiedi certificati** identificare il **Certificato del punto di distribuzione basato su cloud di ConfigMgr** dall'elenco dei certificati disponibili e quindi scegliere **Sono necessarie ulteriori informazioni per registrare il certificato. Per configurare le impostazioni, fare clic qui**.  

12. Nella finestra di dialogo **Proprietà certificato**, nella scheda **Soggetto**, per **Nome soggetto** scegliere **Nome comune** come **Tipo**.  

13. Nella casella **Valore** , specificare la scelta del nome del servizio e il nome del dominio utilizzando un formato FQDN. Ad esempio, **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Rendere il nome del servizio univoco nello spazio dei nomi. Si utilizzerà il DNS per creare un alias (record CNAME) per il mapping del nome di questo servizio su un identificatore generato automaticamente (GUID) e un indirizzo IP di Windows Azure.  

14. Scegliere **Aggiungi**, quindi scegliere **OK** per chiudere la finestra di dialogo **Proprietà certificato**.  

15. Nella pagina **Richiedi certificati** scegliere **Certificato del punto di distribuzione basato su cloud di ConfigMgr** dall'elenco dei certificati disponibili, quindi scegliere **Registrazione**.  

16. Nella pagina **Risultati installazione certificati** attendere il completamento dell'installazione del certificato, quindi scegliere **Fine**.  

17. Chiudere **Certificati (computer locale)**.  

###  <a name="BKMK_clouddpexporting2008"></a> Esportare il certificato del server Web personalizzato per i punti di distribuzione basati su cloud  
 Questa procedura consente di esportare il certificato del server Web personalizzato in un file in modo da importarlo al momento della creazione di un punto di distribuzione basato su cloud.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Per esportare il certificato del server Web personalizzato per i punti di distribuzione basati su cloud  

1. Nella console **Certificati (computer locale)** fare clic con il pulsante destro del mouse sul certificato appena installato, scegliere **Tutte le attività**, quindi scegliere **Esporta**.  

2. Nell'Esportazione guidata certificati scegliere **Avanti**.  

3. Nella pagina **Esportazione della chiave privata con il certificato** scegliere **Sì, esporta la chiave privata**, quindi scegliere **Avanti**.  

   > [!NOTE]  
   >  Se questa opzione non è disponibile, il certificato è stato creato senza l'opzione per esportare la chiave privata. In questo scenario, non è possibile esportare il certificato nel formato richiesto. È necessario configurare il modello di certificato per consentire l'esportazione della chiave privata e richiedere di nuovo il certificato.  

4. Nella pagina **Formato file di esportazione** assicurarsi che sia selezionata l'opzione **Scambio di informazioni personali - PKCS #12 (.PFX)**.  

5. Nella pagina **Password** specificare una password complessa per proteggere il certificato esportato con la relativa chiave privata, quindi scegliere **Avanti**.  

6. Nella pagina **File da esportare** specificare il nome del file da esportare, quindi scegliere **Avanti**.  

7. Per chiudere la procedura guidata, scegliere **Fine** nella pagina **Esportazione guidata certificato**, quindi scegliere **OK** nella finestra di conferma.  

8. Chiudere **Certificati (computer locale)**.  

9. Archiviare il file in modo protetto e assicurarsi che sia possibile accedervi dalla console di System Center Configuration Manager.  

   Il certificato è ora pronto per essere importato quando si crea un punto di distribuzione basato su cloud.  

##  <a name="BKMK_client2008_cm2012"></a> Distribuire il certificato client per computer Windows  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creare ed emettere il modello del certificato di autenticazione della workstation nell'autorità di certificazione  

-   Configurare la registrazione automatica del modello di autenticazione della workstation usando i criteri di gruppo  

-   Registrare automaticamente il certificato di autenticazione della workstation e verificarne l'installazione nei computer  

###  <a name="BKMK_client02008"></a> Creare ed emettere il modello del certificato di autenticazione della workstation nell'autorità di certificazione  
 Questa procedura crea un modello di certificato per i computer client di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello del certificato di autenticazione della workstation nell'autorità di certificazione  

1.  Nel server membro su cui è in esecuzione la console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console di gestione Modelli di certificato.  

2.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

3.  Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

4.  Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato client di ConfigMgr** per generare i certificati client che saranno usati sui computer client di Configuration Manager.  

5.  Scegliere la scheda **Sicurezza**, selezionare il gruppo **Computer del dominio**, quindi selezionare le autorizzazioni aggiuntive **Lettura** e **Registrazione automatica**. Non deselezionare **Registrazione**.  

6.  Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

7.  Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

8.  Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato client di ConfigMgr**, quindi scegliere **OK**.  

9. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="BKMK_client12008"></a> Configurare la registrazione automatica del modello di autenticazione della workstation usando i criteri di gruppo  
 Questa procedura consente di configurare i criteri di gruppo per registrare automaticamente il certificato client sui computer.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Per configurare la registrazione automatica del modello di autenticazione della workstation usando i criteri di gruppo  

1.  Nel controller di dominio fare clic su **Start**, scegliere **Strumenti di amministrazione**, quindi **Gestione criteri di gruppo**.  

2.  Passare al dominio in questione, fare clic con il pulsante destro del mouse su di esso, quindi scegliere **Crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento**.  

    > [!NOTE]  
    >  Questo passaggio consente di utilizzare la procedura consigliata per creare nuovi criteri di gruppo per le impostazioni personalizzate piuttosto che modificare i criteri dominio predefiniti installati con i Servizi di dominio Active Directory. Quando si assegnano questi criteri di gruppo al livello di dominio, i criteri verranno applicati a tutti i computer nel dominio. In un ambiente di produzione, è possibile limitare la registrazione automatica in modo che venga eseguita solo nei computer selezionati. È possibile assegnare i criteri di gruppo a livello di unità organizzativa oppure filtrare i criteri di gruppo di dominio con un gruppo di sicurezza, in modo che vengano applicati solo ai computer del gruppo. Se si limita la registrazione automatica, ricordarsi di includere il server configurato come punto di gestione.  

3.  Nella finestra di dialogo **Nuovo oggetto Criteri di gruppo** immettere un nome come **Registrazione automatica certificati** per i nuovi criteri di gruppo e scegliere **OK**.  

4.  Nel riquadro dei risultati, nella scheda **Oggetti Criteri di gruppo collegati**, fare clic con il pulsante destro del mouse sui nuovi criteri di gruppo, quindi scegliere **Modifica**.  

5.  Nella finestra di dialogo **Editor Gestione Criteri di gruppo** espandere **Criteri** in **Configurazione computer**, quindi passare a **Impostazioni Windows** / **Impostazioni di protezione** / **Criteri chiave pubblica**.  

6.  Fare clic con il pulsante destro del mouse sul tipo di oggetto denominato **Client Servizi certificati - Registrazione automatica**, quindi scegliere **Proprietà**.  

7.  Dall'elenco a discesa **Modello configurazione** scegliere **Attivato**, **Rinnova i certificati scaduti, aggiorna quelli in sospeso e rimuovi i certificati revocati**, **Aggiorna i certificati che utilizzano modelli di certificato**, quindi scegliere **OK**.  

8.  Chiudere **Gestione criteri di gruppo**.  

###  <a name="BKMK_client22008"></a> Registrare automaticamente il certificato di autenticazione della workstation e verificarne l'installazione nei computer  
 Questa procedura consente di installare il certificato del client nei computer e verifica l'installazione.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Per registrare automaticamente il certificato di autenticazione della workstation e verificare la sua installazione nel computer client  

1. Riavviare il computer della workstation e attendere alcuni minuti prima di effettuare l'accesso.  

   > [!NOTE]  
   >  Il riavvio di un computer è il metodo più affidabile per un registrazione automatica dei certificati corretta.  

2. Accedere con un account che abbia privilegi amministrativi.  

3. Nella casella di ricerca digitare **mmc.exe**, quindi premere **INVIO**.  

4. Nella console di gestione vuota scegliere **File**, quindi **Aggiungi/Rimuovi snap-in**.  

5. Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **Certificati** dall'elenco **Snap-in disponibili**, quindi scegliere **Aggiungi**.  

6. Nella finestra di dialogo **Snap-in certificati** scegliere **Account computer**, quindi scegliere **Avanti**.  

7. Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi scegliere **Fine**.  

8. Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **OK**.  

9. Nella console espandere **Certificati (computer locale)**, espandere **Personale**, quindi scegliere **Certificati**.  

10. Nel riquadro dei risultati verificare che sia presente un certificato con **Autenticazione client** nella colonna **Scopo designato** e **Certificato client di ConfigMgr** nella colonna **Modello di certificato**.  

11. Chiudere **Certificati (computer locale)**.  

12. Ripetere i passaggi da 1 a 11 per il server membro per verificare che anche il server che verrà configurato come punto di gestione disponga di un certificato client.  

    A questo punto, il computer è configurato con un certificato client di System Center Configuration Manager.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a> Distribuire il certificato client per punti di distribuzione  

> [!NOTE]  
>  Questo certificato può essere utilizzato anche per le immagini di supporto che non utilizzano l'avvio PXE, perché i requisiti del certificato sono gli stessi.  

 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creare ed emettere un modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  

-   Richiedere il certificato di autenticazione della workstation personalizzato  

-   Esportare il certificato client per i punti di distribuzione  

###  <a name="BKMK_clientdistributionpoint02008"></a> Creare ed emettere un modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  
 Questa procedura crea un modello di certificato personalizzato per i punti di distribuzione di System Center Configuration Manager che consente l'esportazione della chiave privata e l'aggiunta del modello di certificato all'autorità di certificazione.  

> [!NOTE]
>  In questa procedura viene usato un modello di certificato diverso dal modello di certificato che è stato creato per i computer client. Sebbene entrambi i certificati richiedano la funzionalità di autenticazione client, il certificato per i punti di distribuzione richiede l'esportazione della chiave privata. Come procedura consigliata di sicurezza, non configurare i modelli di certificato per consentire l'esportazione della chiave privata, a meno che questa configurazione non sia necessaria. Il punto di distribuzione richiede questa configurazione in quanto è necessario importare il certificato come file, anziché sceglierlo dall'archivio certificati.  
> 
>  Quando si crea un nuovo modello di certificato per questo certificato, è possibile limitare il numero dei computer che possono richiedere un certificato che consenta l'esportazione della chiave privata. Nel nostro esempio di distribuzione questo sarà il gruppo di sicurezza precedentemente creato per i server del sistema del sito di System Center Configuration Manager che eseguono IIS. In una rete di produzione che distribuisce i ruoli del sistema del sito IIS, creare un nuovo gruppo di protezione per i server su cui sono in esecuzione i punti di distribuzione in modo che sia possibile limitare il certificato solo a questi server del sistema del sito. È possibile anche aggiungere le seguenti modifiche per questo certificato:  
> 
> - Richiedere l'approvazione per installare il certificato per una maggiore sicurezza.  
>   -   Aumentare il periodo di validità del certificato. Poiché è necessario esportare e importare il certificato ogni volta che scade, un aumento del periodo di validità riduce la frequenza di ripetizione di questa procedura. Tuttavia, l'aumento del periodo di validità riduce anche la sicurezza del certificato, perché fornisce un tempo maggiore all'autore di un attacco per decrittografare la chiave privata e rubare il certificato.  
>   -   Utilizzare un valore personalizzato nel campo Oggetto del certificato o Nome alternativo del soggetto (SAN) per identificare questo certificato dai certificati client standard. Può essere particolarmente utile se si utilizza lo stesso certificato per più punti di distribuzione.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato di autenticazione della workstation personalizzato nell'autorità di certificazione  

1.  Nel server membro su cui è in esecuzione la console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console di gestione Modelli di certificato.  

2.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

3.  Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

4.  Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato del punto di distribuzione di ConfigMgr** per generare i certificati di autenticazione client per i punti di distribuzione.  

5.  Scegliere la scheda **Gestione richiesta**, quindi scegliere **Rendi la chiave privata esportabile**.  

6.  Scegliere la scheda **Sicurezza** e quindi rimuovere l'autorizzazione **Registrazione** dal gruppo di sicurezza **Enterprise Admins**.  

7.  Scegliere **Aggiungi**, immettere **Server IIS ConfigMgr** nella casella di testo, quindi scegliere **OK**.  

8.  Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

9. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

10. Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

11. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato del punto di distribuzione di ConfigMgr**, quindi scegliere **OK**.  

12. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

###  <a name="BKMK_clientdistributionpoint12008"></a> Richiedere il certificato di autenticazione della workstation personalizzato  
 Questa procedura richiede e installa il certificato client personalizzato nel server membro in cui è in esecuzione IIS e che verrà configurato come punto di distribuzione.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Per richiedere il certificato di autenticazione della workstation personalizzato  

1.  Fare clic su **Start**, scegliere **Esegui** e quindi digitare **mmc.exe.** Nella console vuota scegliere **File**, quindi **Aggiungi/Rimuovi snap-in**.  

2.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **Certificati** dall'elenco **Snap-in disponibili**, quindi scegliere **Aggiungi**.  

3.  Nella finestra di dialogo **Snap-in certificati** scegliere **Account computer**, quindi scegliere **Avanti**.  

4.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi scegliere **Fine**.  

5.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **OK**.  

6.  Nella console espandere **Certificati (computer locale)**, quindi scegliere **Personale**.  

7.  Fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività**, quindi **Richiedi nuovo certificato**.  

8.  Nella pagina **Prima di iniziare** scegliere **Avanti**.  

9. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato**, scegliere **Avanti**.  

10. Nella pagina **Richiedi certificati** scegliere **Certificato del punto di distribuzione di ConfigMgr** dall'elenco dei certificati disponibili, quindi scegliere **Registrazione**.  

11. Nella pagina **Risultati installazione certificati** attendere il completamento dell'installazione del certificato, quindi scegliere **Fine**.  

12. Nel riquadro dei risultati verificare che sia presente un certificato con **Autenticazione client** nella colonna **Scopo designato** e **Certificato del punto di distribuzione di ConfigMgr** nella colonna **Modello di certificato**.  

13. Non chiudere **Certificati (computer locale)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a> Esportare il certificato client per i punti di distribuzione  
 Questa procedura consente di esportare il certificato di autenticazione della workstation personalizzato in un file, in modo che possa essere importato nelle proprietà del punto di distribuzione.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Per esportare il certificato client per i punti di distribuzione  

1. Nella console **Certificati (computer locale)** fare clic con il pulsante destro del mouse sul certificato appena installato, scegliere **Tutte le attività**, quindi scegliere **Esporta**.  

2. Nell'Esportazione guidata certificati scegliere **Avanti**.  

3. Nella pagina **Esportazione della chiave privata con il certificato** scegliere **Sì, esporta la chiave privata**, quindi scegliere **Avanti**.  

   > [!NOTE]  
   >  Se questa opzione non è disponibile, il certificato è stato creato senza l'opzione per esportare la chiave privata. In questo scenario, non è possibile esportare il certificato nel formato richiesto. È necessario configurare il modello di certificato per consentire l'esportazione della chiave privata e richiedere di nuovo il certificato.  

4. Nella pagina **Formato file di esportazione** assicurarsi che sia selezionata l'opzione **Scambio di informazioni personali - PKCS #12 (.PFX)**.  

5. Nella pagina **Password** specificare una password complessa per proteggere il certificato esportato con la relativa chiave privata, quindi scegliere **Avanti**.  

6. Nella pagina **File da esportare** specificare il nome del file da esportare, quindi scegliere **Avanti**.  

7. Per chiudere la procedura guidata, scegliere **Fine** nella pagina **Esportazione guidata certificato**, quindi scegliere **OK** nella finestra di conferma.  

8. Chiudere **Certificati (computer locale)**.  

9. Archiviare il file in modo protetto e assicurarsi che sia possibile accedervi dalla console di System Center Configuration Manager.  

   A questo punto, il certificato è pronto per essere importato durante la configurazione del punto di distribuzione.  

> [!TIP]  
>  È possibile usare lo stesso file del certificato quando si configurano le immagini di supporto per la distribuzione di un sistema operativo che non usa l'avvio PXE e la sequenza attività per installare l'immagine deve contattare un punto di gestione che richieda connessioni client HTTPS.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a> Distribuire il certificato di registrazione per i dispositivi mobili  
 Questa distribuzione del certificato dispone di una sola procedura per creare ed emettere il modello del certificato di registrazione nell'autorità di certificazione.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Creare ed emettere il modello di certificato di registrazione nell'autorità di certificazione  
 Questa procedura crea un modello di certificato di registrazione per i dispositivi mobili di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato di registrazione nell'autorità di certificazione  

1. Creare un gruppo di sicurezza che contenga gli utenti che registreranno i dispositivi mobili in System Center Configuration Manager.  

2. Nel server membro in cui è installato Servizi certificati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console di gestione Modelli di certificato.  

3. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Sessione autenticata** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4. Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

   > [!IMPORTANT]  
   >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5. Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato di registrazione del dispositivo mobile di ConfigMgr** per generare i certificati di registrazione per i dispositivi mobili che saranno gestiti da System Center Configuration Manager.  

6. Scegliere la scheda **Nome soggetto**, verificare che l'opzione **Crea in base alle informazioni di Active Directory** sia selezionata, selezionare **Nome comune** per **Formato del nome soggetto** e deselezionare **Nome entità utente (UPN)** in **Includere le seguenti informazioni nel nome soggetto alternativo**.  

7. Scegliere la scheda **Sicurezza**, scegliere il gruppo di sicurezza che contiene gli utenti che devono registrare i dispositivi mobili, quindi scegliere l'autorizzazione aggiuntiva **Registrazione**. Non deselezionare **Lettura**.  

8. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

9. Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

10. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato di registrazione del dispositivo mobile di ConfigMgr**, quindi scegliere **OK**.  

11. Se non è necessario creare ed emettere altri certificati, chiudere la console Autorità di certificazione.  

    A questo punto, il modello di certificato di registrazione del dispositivo mobile è pronto per essere selezionato durante la configurazione di un profilo di registrazione del dispositivo mobile nelle impostazioni client.  

##  <a name="BKMK_AMT2008_cm2012"></a> Distribuire i certificati per AMT  
 La distribuzione di questo certificato prevede le procedure seguenti:  

-   Creare, emettere e installare il certificato di provisioning AMT  

-   Creare ed emettere il certificato del server Web per computer basati su AMT  

-   Creare ed emettere i certificati di autenticazione client per computer basati su AMT 802.1X  

###  <a name="BKMK_AMTprovisioning2008"></a> Creare, emettere e installare il certificato di provisioning AMT  
 Creare il certificato di provisioning con l'autorità di certificazione (CA) interna quando i computer basati su AMT sono configurati con l'identificazione personale del certificato della CA radice interna. Se non è possibile e occorre usare un'autorità di certificazione esterna, seguire le istruzioni della società che ha emesso il certificato di provisioning AMT. In questo caso, è spesso necessario richiedere il certificato sul sito Web pubblico della società. È inoltre possibile trovare istruzioni dettagliate per la CA esterna prescelta nel [sito Web Intel vPro Expert Center: Microsoft vPro Manageability](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  Le CA esterne potrebbero non supportare l'identificatore di oggetto provisioning Intel AMT. In questo caso, fornire l'attributo OU del **certificato di installazione client di Intel(R)**.  

 Quando si richiede un certificato di provisioning AMT da una CA esterna, installare il certificato nell'archivio certificati personale del computer sul server membro che ospiterà il punto di servizio fuori banda.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Per richiedere ed emettere il certificato di provisioning AMT  

1. Creare un gruppo di sicurezza che contenga gli account computer dei server del sistema del sito che eseguiranno il punto di servizio fuori banda.  

2. Nel server membro in cui è installato Servizi certificati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console **Modelli di certificato**.  

3. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Server Web** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4. Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

   > [!IMPORTANT]  
   >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5. Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Provisioning AMT di ConfigMgr** per il modello del certificato di provisioning AMT.  

6. Scegliere la scheda **Nome soggetto**, scegliere **Crea in base alle informazioni di Active Directory**, quindi scegliere **Nome comune**.  

7. Scegliere la scheda **Estensioni**, assicurarsi che sia selezionato **Criteri di applicazione**, quindi scegliere **Modifica**.  

8. Nella finestra di dialogo **Modifica estensione criteri di applicazione** scegliere **Aggiungi**.  

9. Nella finestra di dialogo **Aggiunta criterio di applicazione** scegliere **Nuovo**.  

10. Nella finestra di dialogo **Nuovo criterio di applicazione** immettere **Provisioning AMT** nel campo **Nome**, quindi immettere il numero seguente per **Identificatore oggetto**: **2.16.840.1.113741.1.2.3**.  

11. Scegliere **OK**, quindi **OK** nella finestra di dialogo **Aggiunta criterio di applicazione**.  

12. Scegliere **OK** nella finestra di dialogo **Modifica estensione criteri di applicazione**.  

13. Nella finestra di dialogo **Proprietà nuovo modello** verrà visualizzato quanto segue come descrizione di **Criteri di applicazione**: **Autenticazione server** e **Provisioning AMT**.  

14. Scegliere la scheda **Protezione** e quindi rimuovere l'autorizzazione **Registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins**.  

15. Scegliere **Aggiungi**, immettere il nome di un gruppo di sicurezza che contenga l'account computer per il ruolo del sistema del sito del punto di servizio fuori banda, quindi scegliere **OK**.  

16. Scegliere l'autorizzazione **Registrazione** per questo gruppo e non deselezionare l'autorizzazione **Lettura**.  

17. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

18. In **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

19. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Provisioning AMT di ConfigMgr**, quindi scegliere **OK**.  

    > [!NOTE]  
    >  Se non è possibile completare i passaggi 18 o 19, controllare che si stia usando Enterprise Edition di Windows Server 2008. Nonostante si possano configurare modelli con Windows Server Standard Edition e Servizi certificati, non è possibile distribuire certificati usando modelli di certificati modificati a meno che non si stia usando Windows Server 2008 Enterprise Edition.  

20. Non chiudere **Autorità di certificazione**.  

    Il certificato di provisioning AMT dalla CA interna è ora pronto per essere installato nel computer del punto di servizio fuori banda.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Per installare il certificato di provisioning AMT  

1. Riavviare il server membro in cui è in esecuzione IIS, per assicurarsi che possa accedere al modello di certificato con l'autorizzazione configurata.  

2. Fare clic su **Start**, scegliere **Esegui** e quindi digitare **mmc.exe.** Nella console vuota scegliere **File**, quindi **Aggiungi/Rimuovi snap-in**.  

3. Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **Certificati** dall'elenco **Snap-in disponibili**, quindi scegliere **Aggiungi**.  

4. Nella finestra di dialogo **Snap-in certificati** scegliere **Account computer**, quindi scegliere **Avanti**.  

5. Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi scegliere **Fine**.  

6. Nella finestra di dialogo **Aggiungi o rimuovi snap-in** scegliere **OK**.  

7. Nella console espandere **Certificati (computer locale)**, quindi scegliere **Personale**.  

8. Fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività**, quindi **Richiedi nuovo certificato**.  

9. Nella pagina **Prima di iniziare** scegliere **Avanti**.  

10. Se viene visualizzata la pagina **Seleziona criteri di registrazione certificato**, scegliere **Avanti**.  

11. Nella pagina **Richiedi certificati** selezionare **Provisioning AMT** dall'elenco dei certificati disponibili, quindi scegliere **Registrazione**.  

12. Nella pagina **Risultati installazione certificati** attendere il completamento dell'installazione del certificato, quindi scegliere **Fine**.  

13. Chiudere **Certificati (computer locale)**.  

    A questo punto, il certificato di provisioning AMT dalla CA interna è installato e pronto per essere selezionato nelle proprietà del punto di servizio fuori banda.  

### <a name="create-and-issue-the-web-server-certificate-for-amt-based-computers"></a>Creare ed emettere il certificato del server Web per computer basati su AMT  
 Utilizzare la procedura seguente per la preparazione dei certificati server Web per computer basati su AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Per creare ed emettere il modello di certificato del server Web  

1. Creare un gruppo di sicurezza vuoto che contenga gli account computer AMT creati da System Center Configuration Manager durante il provisioning AMT.  

2. Nel server membro in cui è installato Servizi certificati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console **Modelli di certificato**.  

3. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Server Web** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4. Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

   > [!IMPORTANT]  
   >  Non selezionare **Windows 2008 Server, Enterprise Edition.**  

5. Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato server Web di ConfigMgr** per generare i certificati Web che saranno usati per la gestione fuori banda sui computer AMT.  

6. Scegliere la scheda **Nome soggetto**, scegliere **Crea in base alle informazioni di Active Directory**, quindi scegliere **Nome comune** per **Formato del nome soggetto** e deselezionare **Nome entità utente (UPN)** per il nome soggetto alternativo.  

7. Scegliere la scheda **Protezione** e quindi rimuovere l'autorizzazione **Registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins**.  

8. Scegliere **Aggiungi**, immettere il nome del gruppo di sicurezza creato per il provisioning AMT, quindi scegliere **OK**.  

9. Scegliere le seguenti autorizzazioni **Consenti** per questo gruppo di sicurezza: **Lettura** e **Registrazione**.  

10. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

11. Nella console **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato server Web di ConfigMgr**, quindi scegliere **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

    A questo punto, il modello di server Web AMT è pronto per la configurazione dei computer basati su AMT con i certificati del server Web. Scegliere questo modello di certificato nelle proprietà del componente della gestione fuori banda.  

### <a name="create-and-issue-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Creare ed emettere i certificati di autenticazione client per computer basati su AMT 802.1X  
 Utilizzare la procedura seguente se i computer basati su AMT utilizzeranno i certificati client per reti cablate o wireless autenticate 802.1 X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Per creare ed emettere il modello di certificato di autenticazione client nella CA  

1. Nel server membro in cui è installato Servizi certificati, nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console **Modelli di certificato**.  

2. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Autenticazione workstation** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

   > [!IMPORTANT]  
   >  Non selezionare **Windows 2008 Server, Enterprise Edition.**  

3. Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato di autenticazione client 802.1X AMT di ConfigMgr** per generare i certificati client che saranno usati per la gestione fuori banda nei computer AMT.  

4. Scegliere la scheda **Nome soggetto**, scegliere **Crea in base alle informazioni di Active Directory**, quindi scegliere **Nome comune** per **Formato del nome soggetto**. Deselezionare **Nome DNS** per il nome soggetto alternativo, quindi scegliere **Nome entità utente (UPN)**.  

5. Scegliere la scheda **Protezione** e quindi rimuovere l'autorizzazione **Registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins**.  

6. Scegliere **Aggiungi**, immettere il nome del gruppo di sicurezza che verrà specificato nelle proprietà del componente della gestione fuori banda per contenere gli account dei computer basati su AMT, quindi scegliere **OK**.  

7. Selezionare le seguenti autorizzazioni **Consenti** per questo gruppo di sicurezza: **Lettura** e **Registrazione**.  

8. Scegliere **OK**, quindi chiudere la console di gestione **Modelli di certificato**, **certtmpl - [Modelli di certificato]**.  

9. Nella console di gestione **Autorità di certificazione** fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

10. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato di autenticazione client 802.1X AMT di ConfigMgr**, quindi scegliere **OK**.  

11. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

    Il modello di certificato di autenticazione client è ora pronto per emettere certificati ai computer basati su AMT che possono essere utilizzati per l'autenticazione client 802.1 X. Scegliere questo modello di certificato nelle proprietà del componente della gestione fuori banda.  

##  <a name="BKMK_MacClient_SP1"></a> Distribuire il certificato client per computer Mac  

Questa distribuzione del certificato dispone di una sola procedura per creare ed emettere il modello del certificato di registrazione nell'autorità di certificazione.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a> Creare ed emettere un modello di certificato client Mac nell'autorità di certificazione  
 Questa procedura crea un modello di certificato personalizzato per i computer Mac di System Center Configuration Manager e lo aggiunge all'autorità di certificazione.  

> [!NOTE]  
>  Questa procedura utilizza un modello di certificato differente dal modello di certificato che potrebbe essere stato creato per i computer client di Windows o per i punti di distribuzione.  
>   
>  Quando si crea un nuovo modello di certificato per questo certificato, è possibile limitare la richiesta di certificato agli utenti autorizzati.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Per creare ed emettere il modello di certificato client Mac nell'autorità di certificazione  

1. Creare un gruppo di sicurezza che contenga gli account utente per gli utenti amministratori che registreranno il certificato nel computer Mac usando System Center Configuration Manager.  

2. Nel server membro su cui è in esecuzione la console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi scegliere **Gestisci** per caricare la console di gestione Modelli di certificato.  

3. Nel riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce con **Sessione autenticata** nella colonna **Nome visualizzato modello**, quindi scegliere **Duplica modello**.  

4. Nella finestra di dialogo **Duplica modello** verificare che sia selezionato **Windows 2003 Server, Enterprise Edition**, quindi scegliere **OK**.  

   > [!IMPORTANT]  
   >  Non selezionare **Windows 2008 Server, Enterprise Edition**.  

5. Nella finestra di dialogo **Proprietà nuovo modello**, nella scheda **Generale**, immettere un nome di modello come **Certificato client Mac di ConfigMgr** per generare i certificati client Mac.  

6. Scegliere la scheda **Nome soggetto**, verificare che l'opzione **Crea in base alle informazioni di Active Directory** sia selezionata, scegliere **Nome comune** per **Formato del nome soggetto** e deselezionare **Nome entità utente (UPN)** in **Includere le seguenti informazioni nel nome soggetto alternativo**.  

7. Scegliere la scheda **Protezione** e quindi rimuovere l'autorizzazione **Registrazione** dai gruppi di sicurezza **Domain Admins** ed **Enterprise Admins**.  

8. Scegliere **Aggiungi**, specificare il gruppo di sicurezza creato nel passaggio 1, quindi scegliere **OK**.  

9. Scegliere l'autorizzazione **Registrazione** per questo gruppo e non deselezionare l'autorizzazione **Lettura**.  

10. Scegliere **OK** e quindi chiudere la console **Modelli di certificato**.  

11. Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** scegliere il nuovo modello appena creato, **Certificato client Mac di ConfigMgr**, quindi scegliere **OK**.  

13. Se non è necessario creare ed emettere altri certificati, chiudere **Autorità di certificazione**.  

    A questo punto, il modello di certificato client Mac è pronto per essere selezionato durante la configurazione delle impostazioni client per la registrazione.
