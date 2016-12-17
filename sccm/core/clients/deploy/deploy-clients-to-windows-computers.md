---
title: Distribuire client Windows | System Center Configuration Manager
description: Informazioni su come distribuire i client ai computer Windows in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5a52386c6327ded3c5a400c7a046a6a12af96bae


---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Come distribuire i client nei computer Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare diversi metodi di distribuzione client per installare il software client di System Center Configuration Manager sui computer. Per decidere il metodo di distribuzione da usare, vedere [Metodi di installazione client in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

 Prima di installare i client di Configuration Manager, assicurarsi che siano presenti tutti i prerequisiti e che siano state completate tutte le configurazioni di distribuzione necessarie. Per altre informazioni, vedere [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Prerequisiti per la distribuzione dei client ai computer Windows in System Center Configuration Manager).  


##  <a name="a-namebkmkclientpusha-how-to-install-configuration-manager-clients-by-using-client-push"></a><a name="BKMK_ClientPush"></a> Come installare i client di Configuration Manager usando push client  

 Usare l'installazione push client per installare il software client di Configuration Manager sui computer individuati da Gestione configurazione. È possibile configurare l'installazione push client per un sito e l'installazione client verrà eseguita automaticamente sui computer individuati all'interno dei limiti configurati del sito quando tali limiti sono configurati come gruppo di limiti. In alternativa, è possibile avviare un'installazione push client eseguendo l'Installazione guidata push client per una raccolta specifica o una risorsa all'interno di una raccolta.  

 È possibile anche usare l'Installazione guidata push client per installare il client di Configuration Manager nei risultati ottenuti dall'esecuzione di una query. Affinché l'installazione abbia esito positivo in questo scenario, uno degli elementi restituiti dalla query selezionata deve essere l'attributo **ResourceID** dalla classe di attributi **Risorse di sistema**. Per altre informazioni sulle query, vedere [Riferimento tecnico per le query per System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md).  

 Se il server del sito non può contattare il computer client o avviare il processo di installazione, ripete automaticamente il tentativo di installazione per ogni ora fino a 7 giorni finché non ha esito positivo.  

 Per tenere traccia del processo di installazione client, installare un sistema del sito del punto di stato di fallback prima di installare i client. Quando viene installato un punto di stato di fallback, esso viene assegnato automaticamente ai client quando vengono installati con il metodo di installazione push client. Visualizzare i report di assegnazione e distribuzione client per tenere traccia dell'avanzamento dell'installazione client. Inoltre, i file di registro client forniscono che ulteriori informazioni dettagliate per la risoluzione dei problemi e non richiedono l'installazione di un punto di stato di fallback. Ad esempio, il file CCM.log nel server del sito registra qualsiasi problema che il server del sito presenta nella connessione al computer e il file CCMSetup.log nel client registra il processo di installazione.  

> [!IMPORTANT]  
>  Affinché il push client venga eseguito correttamente, assicurarsi che siano presenti tutti i prerequisiti. I prerequisiti sono riportati nella sezione "Installation Method Dependencies" ("Dipendenze del metodo di installazione) in [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) (Prerequisiti per la distribuzione dei client ai computer Windows in System Center Configuration Manager).  

#### <a name="to-configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Per configurare il sito per l'utilizzo automatico del push client per i computer individuati  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nell'elenco **Siti** selezionare il sito per cui si desidera configurare l'installazione push client automatica a livello di sito.  

4.  Nella scheda **Home** del gruppo **Impostazioni** fare clic su **Impostazioni di installazione client**, quindi su **Installazione push client**.  

5.  Nella scheda **Generale** della finestra di dialogo **Proprietà installazione push client** , selezionare **Abilita installazione push client automatica a livello di sito**. Selezionare i tipi di sistema in cui Configuration Manager dovrebbe eseguire il push del software client selezionando **Server**, **Workstation** o **Server di sistema di sito di Configuration Manager**. La selezione predefinita è **Server** e **Workstation**.  

6.  Specificare se si vuole che l'installazione push client automatica a livello di sito installi il software client di Configuration Manager sui controller di dominio.  

7.  Nella scheda **Account** , specificare uno o più account affinché Configuration Manager li usi durante la connessione al computer per l'installazione del software client. Fare clic sull'icona **Crea** , immettere **Nome utente** e **Password**, confermare la password, quindi fare clic su **OK**. È necessario specificare almeno un account di installazione push client, che deve disporre dei diritti di amministratore locale su ogni computer su cui si desidera installare il client. Se non si specifica un account di installazione push client, Configuration Manager prova a usare l'account del computer del sistema del sito, che provoca l'errore del push client tra domini.  

    > [!IMPORTANT]  
    >  La password per l'account di installazione push client deve essere lunga 38 caratteri o meno.  

    > [!NOTE]  
    >  Se si desidera usare il metodo di installazione push client da un sito secondario, l'account deve essere specificato nel sito secondario che avvia il push client.  
    >   
    >  Per altre informazioni sull'account di installazione push client, vedere la procedura successiva, "Per usare l'Installazione guidata push client".  

8.  Nella scheda **Proprietà di installazione** specificare tutte le proprietà di installazione da usare quando si installa il client di Configuration Manager. È possibile specificare le proprietà di installazione per il pacchetto Windows Installer (Client.msi) e le seguenti proprietà di CCMSetup.exe:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Le proprietà di installazione client che sono specificate in questa scheda vengono pubblicate in Active Directory Domain Services se lo schema è esteso a Configuration Manager e lette dalle installazioni client in cui è in esecuzione CCMSetup senza proprietà di installazione. Per altre informazioni sulle proprietà di installazione dei client, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!NOTE]  
    >  Se si abilita l'installazione push client su un sito secondario, assicurarsi che la proprietà SMSSITECODE sia impostata sul nome del sito di Configuration Manager del sito primario padre. Se lo schema di Active Directory è esteso a Configuration Manager, è anche possibile impostarlo su AUTO per trovare automaticamente la corretta assegnazione del sito.  

#### <a name="to-use-the-client-push-installation-wizard"></a>Per usare l'Installazione guidata push client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nell'elenco **Siti** selezionare il sito per cui si desidera configurare l'installazione push client automatica a livello di sito.  

4.  Nella scheda **Home** del gruppo **Impostazioni** fare clic su **Impostazioni di installazione client**, quindi su **Installazione push client**.  

5.  Nella scheda **Proprietà di installazione** specificare tutte le proprietà di installazione da usare quando si installa il client di Configuration Manager. È possibile specificare le proprietà di installazione per il pacchetto Windows Installer (Client.msi) e le seguenti proprietà di CCMSetup.exe:  

    -   /forcereboot  

    -   /skipprereq  

    -   /logon  

    -   /BITSPriority  

    -   /downloadtimeout  

    -   /forceinstall  

     Le proprietà di installazione client che sono specificate in questa scheda vengono pubblicate in Active Directory Domain Services se lo schema è esteso a Configuration Manager e lette dalle installazioni client in cui è in esecuzione CCMSetup senza proprietà di installazione. Per altre informazioni sulle proprietà di installazione dei client, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

7.  Nell'area di lavoro **Asset e conformità** , selezionare uno o più computer o una raccolta di computer.  

8.  Nella scheda **Home** scegliere una delle seguenti azioni:  

    -   Se si desidera installare il client in uno o più computer, nel gruppo **Dispositivo** , fare clic su **Installa client**.  

    -   Se si desidera installare il client in una raccolta di computer, nel gruppo **Raccolta** , fare clic su **Installa client**.  

9. Nella pagina **Prima di iniziare** dell' **Installazione guidata client**riesaminare le informazioni, quindi fare clic su **Avanti**.  

10. Nella pagina **Opzioni di installazione** , configurare se il client possa essere installato sui controller di dominio, se il client verrà reinstallato, aggiornato o ripristinato sui computer con un client esistente e il nome del sito che installerà il software client. Fare clic su **Avanti**.  

11. Esaminare le impostazioni di installazione, quindi chiudere la procedura guidata.  

> [!NOTE]  
>  È possibile usare la procedura guidata per installare i client, anche se il sito non è configurato per il push client.  

##  <a name="a-namebkmkclientsupa-how-to-install-configuration-manager-clients-by-using-software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Come installare i client di Configuration Manager usando l'Installazione basata sull'aggiornamento software  
 L'installazione client basata sull'aggiornamento software pubblica il client di Configuration Manager su un punto di aggiornamento software come aggiornamento software aggiuntivo. Questo metodo di installazione client può essere usato per installare il client di Configuration Manager su computer che non hanno ancora installato il client oppure per aggiornare i client esistenti di Configuration Manager.  

 Se un computer ha installato il client di Configuration Manager, Configuration Manager specifica al client il nome e la porta del server del punto di aggiornamento software da cui ottenere gli aggiornamenti software. Queste informazioni sono incluse nei criteri client.  

> [!IMPORTANT]  
>  Per usare l'installazione basata sull'aggiornamento software, è necessario usare lo stesso server di Windows Server Update Services (WSUS) per l'installazione client e gli aggiornamenti software. Questo server deve essere il punto di aggiornamento software attivo in un sito primario. Per altre informazioni, vedere [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Installare un punto di aggiornamento software).  

 Se un computer non ha installato il client di Configuration Manager, è necessario configurare e assegnare un oggetto Criteri di gruppo in Active Directory Domain Services per specificare il nome del server del punto di aggiornamento software da cui il computer otterrà gli aggiornamenti software.  

 Non è possibile aggiungere proprietà della riga di comando a un'installazione client basata sull'aggiornamento software. Se lo schema di Active Directory è stato esteso per Configuration Manager, i computer client inviano automaticamente la query delle proprietà di installazione a Active Directory Domain Services durante l'installazione.  

 Se lo schema di Active Directory non è stato esteso, è necessario usare i Criteri di gruppo per effettuare il provisioning delle impostazioni dell'installazione client nei computer presenti nel sito. Queste impostazioni vengono applicate automaticamente a tutte le installazioni basate sull'aggiornamento software. Per altre informazioni, vedere [Come eseguire il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software)](#BKMK_Provision) e [Come assegnare i client a un sito in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Usare le procedure seguenti per configurare i computer senza un client di Configuration Manager per l'uso del punto di aggiornamento software per l'installazione client e gli aggiornamenti software e per la pubblicazione del software client di Configuration Manager nel punto di aggiornamento software.  

> [!NOTE]  
>  Se i computer sono in uno stato di riavvio in sospeso in seguito a una precedente installazione software, un'installazione client basata sull'aggiornamento potrebbe causare il riavvio del computer.  

#### <a name="to-configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Per configurare un oggetto Criteri di gruppo nei Servizi di dominio Active Directory per specificare il punto di aggiornamento software per l'installazione client e gli aggiornamenti software  

1.  Usare la console Gestione criteri di gruppo per aprire un oggetto Criteri di gruppo nuovo o esistente.  

2.  Nella console, espandere **Configurazione computer**, **Modelli amministrativi**, **Componenti di Windows**, quindi fare clic su **Windows Update**.  

3.  Aprire le proprietà dell'impostazione **Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet**, quindi fare clic su **Attivato**.  

4.  Nella casella **Impostare il servizio di aggiornamento nella rete Intranet per il rilevamento degli aggiornamenti**, specificare il nome del server del punto di aggiornamento software che si desidera usare e la porta. Questi devono corrispondere esattamente al formato del nome server e alla porta usata dal punto di aggiornamento software:  

    -   Se il sistema del sito di Configuration manager è configurato per usare un nome di dominio completo (FQDN), specificare il nome server usando un formato FQDN.  

    -   Se il sistema del sito di Configuration manager non è configurato per usare un nome di dominio completo (FQDN), specificare il nome server usando un formato di nome breve.  

    > [!NOTE]  
    >  Per determinare il numero di porta usato dal punto di aggiornamento software, vedere [Come determinare le impostazioni della porta usate da WSUS in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

     Esempio: **http://server1.contoso.com:8530**  

5.  Nella casella **Impostare il server per le statistiche nella rete Intranet**, specificare il nome del server delle statistiche intranet che si desidera usare. Non sono previsti requisiti specifici per la specifica di questo server. Non deve essere lo stesso computer del server del punto di aggiornamento software e il formato non deve corrispondere se è lo stesso server.  

6.  Assegnare l'oggetto Criteri di gruppo ai computer su cui si desidera installare il client di Configuration Manager e ricevere gli aggiornamenti software.  

#### <a name="to-publish-the-configuration-manager-client-to-the-software-update-point"></a>Per pubblicare il client di Configuration Manager nel punto di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nell'elenco **Siti** selezionare il sito per cui si desidera configurare l'installazione client basata sull'aggiornamento software.  

4.  Nella scheda **Home** del gruppo **Impostazioni** fare clic su **Impostazioni di installazione client**, quindi su **Installazione client basata sull'aggiornamento software**.  

5.  Nella finestra di dialogo **Proprietà installazione client basata su aggiornamento software** , selezionare **Abilita installazione client basata su aggiornamento software** per abilitare questo metodo di installazione client.  

6.  Se il software client nel server del sito di Configuration Manager è una versione successiva alla versione client memorizzata nel punto di aggiornamento software, viene visualizzata la finestra di dialogo **Versione più recente del pacchetto client rilevata**. Fare clic su **Sì** per pubblicare la versione più recente del software client nel punto di aggiornamento software.  

    > [!NOTE]  
    >  Se il software client non è stato pubblicato in precedenza nel punto di aggiornamento punto, questa casella sarà vuota.  

7.  Per completare la configurazione dell'installazione client del punto di aggiornamento software, fare clic su **OK**.  

> [!NOTE]  
>  L'aggiornamento software per il client di Configuration Manager non viene automaticamente aggiornato quando c'è una nuova versione. Se si esegue l'aggiornamento del sito, che include una nuova versione client, è necessario ripetere questa procedura e fare clic su **Sì** per il passaggio 6.  

##  <a name="a-namebkmkclientgpa-how-to-install-configuration-manager-clients-by-using-group-policy"></a><a name="BKMK_ClientGP"></a> Come installare i client di Configuration Manager usando i Criteri di gruppo  
 È possibile usare i Criteri di gruppo in Active Directory Domain Services per pubblicare o assegnare il client di Configuration Manager da installare sui computer aziendali. Quando si assegna il client di Configuration Manager ai computer usando i Criteri di gruppo, questo viene installato al primo avvio del computer. Quando il client di Configuration Manager viene pubblicato per gli utenti usando i Criteri di gruppo, viene visualizzato in **Installazione applicazioni** nel Pannello di controllo ed è disponibile per l'installazione da parte dell'utente.  

 Usare il pacchetto di Windows Installer (CCMSetup.msi) per le installazioni basate su Criteri di gruppo. Il file si trova nella cartella **&lt;directory di installazione di ConfigMgr\>\bin\i386** nel server del sito di Configuration Manager. Non è possibile aggiungere proprietà a questo file per modificare il comportamento di installazione:  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client è necessario disporre delle autorizzazioni di amministratore per la cartella.  

-   Se lo schema di Active Directory viene esteso per Configuration Manager ed è selezionata l'opzione **Publish this site in Active Directory Domain Services** (Pubblica questo sito in Active Directory Domain Services) nella scheda **Avanzate** della finestra di dialogo **Proprietà sito**, i computer client eseguono automaticamente una ricerca in Active Directory Domain Services per individuare le proprietà di installazione. Per altre informazioni sulle proprietà di installazione pubblicate, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se lo schema di Active Directory non è stato esteso, è possibile usare la procedura seguente in questo argomento per memorizzare le proprietà di installazione nel Registro di sistema dei computer: [Come eseguire il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software).](#BKMK_Provision). Queste proprietà di installazione vengono quindi usate quando il client di Configuration Manager è installato.  

 Per informazioni sull'utilizzo dei Criteri di gruppo in Servizi di dominio Active Directory per l'installazione del software, fare riferimento alla documentazione di Windows Server.  

##  <a name="a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually"></a><a name="BKMK_Manual"></a> Come installare manualmente i client di Configuration Manager  
 È possibile installare manualmente il software dei client di Configuration Manager sui computer aziendali usando il programma CCMSetup.exe. Questo programma e i relativi file di supporto si trovano nella cartella **Client** all'interno della cartella di installazione di Configuration Manager sul server del sito e sui punti di gestione nel sito. La cartella è condivisa in rete come  

 \\\\*&lt;<Nome server del sito\>*\SMS_*&lt;Codice del sito\>*\Client\  

 dove *&lt;Nome server del sito\>* è il nome di uno dei server che ospitano un punto di gestione e *&lt;Codice del sito\>* è il codice per il sito primario al quale apparterrà il client.  Per eseguire CCMSetup.exe dalla riga di comando nel client, è necessario eseguire il mapping di un'unità di rete in questo percorso e quindi eseguire il comando.  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client è necessario disporre delle autorizzazioni di amministratore per la cartella.  

 CCMSetup.exe copia tutti i prerequisiti di installazione necessari per il computer client e chiama il pacchetto di Windows Installer (Client.msi) per eseguire l'installazione client.  

> [!IMPORTANT]  
>  Non è possibile eseguire Client.msi direttamente.  

 È possibile specificare le proprietà di riga di comando per CCMSetup.exe e Client.msi per modificare il comportamento dell'installazione client. Verificare di aver specificato le proprietà CCMSetup (le proprietà che iniziano con **/**) prima di specificare le proprietà Client.msi.  

 Ad esempio, è possibile specificare il comando seguente:  

```  
CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01  
```  

 e il client viene installato con le proprietà seguenti:  

|Proprietà|Descrizione|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Questa proprietà CCMSetup specifica al punto di gestione SMSMP01 di scaricare i file di installazione client richiesti.|  
|**/logon**|Questa proprietà CCMSetup specifica che l'installazione deve essere interrotta se viene rilevato un client di Configuration Manager sul computer.|  
|**SMSSITECODE=AUTO**|Questa proprietà Client.msi specifica che il client cerca di individuare il codice sito di Configuration Manager da usare, ad esempio usando Active Directory Domain Services.|  
|**FSP=SMSFP01**|Questa proprietà Client.msi specifica che il punto di stato di fallback denominato SMSFP01 sarà usato per ricevere i messaggi di stato inviati dal computer client.|  

 Per maggiori dettagli su tutte le proprietà CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md)  

### <a name="examples-for-installing-configuration-manager-clients-manually"></a>Esempi per l'installazione manuale dei client di Configuration Manager  
 Questi esempi riguardano i client di Active Directory sulla Intranet e usano i valori seguenti per rappresentare i vari aspetti del sito:  

 **MPSERVER** = server che ospita il punto di gestione   
**FSPSERVER** = server che ospita il punto di stato di fallback  
**ABC** = codice del sito  
**contoso.com** = nome di dominio  

 Tutti i server del sistema del sito sono configurati con un FQDN intranet e il sito è pubblicato nella foresta Active Directory del client.  

 Nel computer client accedere come amministratore locale, eseguire il mapping dell'unità (z:) a \\\MPSERVER\SMS_ABC\Client, passare al prompt dei comandi nell'unità z e quindi eseguire uno di questi comandi.  

 **Esempio 1:**  

```  
CCMSetup.exe  
```  

> [!NOTE]  
>  In questo esempio il client viene installato senza proprietà aggiuntive in modo che venga automaticamente configurato usando le proprietà di installazione pubblicate in Servizi di dominio Active Directory. Ad esempio, il client viene automaticamente configurato per il codice sito (richiede che il percorso di rete del client sia incluso in un gruppo di limiti configurato per l'assegnazione client), un punto di gestione, un punto di stato di fallback e per l'eventuale comunicazione solo tramite HTTPS. Per altre informazioni sulle proprietà di installazione del client configurabili automaticamente per i client Active Directory, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Esempio 2:**  

```  
CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com  
```  

> [!NOTE]  
>  Questo esempio sostituisce la configurazione automatica che Active Directory Domain Services è in grado di offrire e non richiede che il percorso di rete del client sia incluso in un gruppo di limiti configurato per l'assegnazione client. Al contrario, l'installazione specifica il sito, un punto di gestione intranet e un punto di gestione basato su Internet, un punto di stato di fallback che accetta connessioni da Internet e l'utilizzo di un certificato PKI client (se disponibile) con il periodo di validità più lungo.  

##  <a name="a-namebkmkclientlogonscripta-how-to-install-configuration-manager-clients-by-using-logon-scripts"></a><a name="BKMK_ClientLogonScript"></a> Come installare i client di Configuration Manager usando script di accesso  
 Configuration Manager supporta gli script di accesso per installare il software client di Configuration Manager. È possibile usare il file di programma **CCMSetup.exe** in uno script di accesso per avviare l'installazione client.  

 L'installazione con script di accesso usa gli stessi metodi dell'installazione client manuale. È possibile specificare la proprietà di installazione **/logon** per CCMSsetup.exe, che impedisce l'installazione del client in presenza di una versione del client esistente sul computer. In tal modo è possibile evitare la reinstallazione del client ogni volta che viene eseguito lo script di accesso.  

 Se non viene specificata alcuna origine dell'installazione che stia usando la proprietà **/Source** né viene specificato un punto di gestione da cui ottenere l'installazione usando la proprietà **/MP**, CCMSetup.exe può individuare il punto di gestione eseguendo una ricerca in Active Directory Domain Services se lo schema è stato esteso per Configuration Manager e il sito è pubblicato in Active Directory Domain Services. In alternativa, il client può usare DNS o WINS per individuare un punto di gestione.  

##  <a name="a-namebkmkclientappa-how-to-install-configuration-manager-clients-by-using-a-package-and-program"></a><a name="BKMK_ClientApp"></a> Come installare i client di Configuration Manager usando un pacchetto e un programma  
 È possibile usare Configuration Manager per creare e distribuire un pacchetto e un programma di aggiornamento per il software client di computer selezionati nella gerarchia. Con Configuration Manager viene offerto un file di definizione pacchetto che popola le proprietà del pacchetto con i valori generalmente usati. È possibile personalizzare il comportamento dell'installazione del client specificando proprietà di riga di comando aggiuntive.  

> [!NOTE]  
>  Non è possibile aggiornare i client di Configuration Manager 2007 con questo metodo. Usare invece l'aggiornamento automatico del client, che crea e distribuisce automaticamente un pacchetto contenente la versione più recente del client. Per altre informazioni, vedere [Aggiornare i client in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Per altre informazioni sulla migrazione da versioni precedenti del client di Configuration Manager, vedere [Planning a client migration strategy in System Center Configuration Manager](../../../core/migration/planning-a-client-migration-strategy.md) (Pianificazione di una strategia di migrazione client in System Center Configuration Manager).  

 Usare la procedura seguente per creare un pacchetto e un programma di Configuration Manager che possa essere distribuito nei computer client di Configuration Manager per aggiornare il software client.  

#### <a name="to-create-a-package-and-program-for-the-client-software"></a>Per creare un pacchetto e un programma per il software client  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi fare clic su **Pacchetti**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea pacchetto da definizione**.  

4.  Nella pagina **Definizione pacchetto** della **Creazione guidata pacchetto da definizione**selezionare **Microsoft** dall'elenco a discesa **Autore** , quindi **Aggiornamento client di Configuration Manager** dall'elenco **Definizione pacchetto** e, infine, fare clic su **Avanti**.  

5.  Nella pagina **File di origine** della procedura guidata selezionare **Reperisci sempre i file di origine da una cartella di origine**, quindi fare clic su **Avanti**.  

6.  Nella pagina **Cartella di origine** della **Creazione guidata pacchetto da definizione** selezionare **Percorso di rete (nome UNC)** e immettere il percorso di rete al computer e alla cartella contenente i file di installazione client di Configuration Manager.  

    > [!NOTE]  
    >  Il computer su cui è in esecuzione la distribuzione di Configuration Manager deve avere accesso alla cartella di rete specificata. Se il computer non dispone dell'accesso, l'installazione avrà esito negativo.  

7.  Fare clic su **Avanti** e completare la procedura guidata.  

8.  Se si desidera cambiare una proprietà di installazione client, è possibile modificare i parametri della riga di comando CCMSetup.exe nella scheda **Generale** della finestra di dialogo del programma **Proprietà di aggiornamento automatico dell'agente di Configuration Manager** . Le proprietà di installazione predefinite sono **/noservice SMSSITECODE=AUTO**.  

9. Distribuire il pacchetto a tutti i punti di distribuzione in cui si desidera venga ospitato il pacchetto di aggiornamento client. È quindi possibile distribuire il pacchetto alle raccolte di computer contenenti i client di Configuration Manager da aggiornare.  

##  <a name="a-namebkmkclientimagea-how-to-install-configuration-manager-clients-by-using-computer-imaging"></a><a name="BKMK_ClientImage"></a> Come installare i client di Configuration Manager usando la creazione dell'immagine del computer  
 È possibile preinstallare il software client di Configuration Manager su un computer con immagine master che sarà usato per costruire i computer aziendali. Per installare il client su un computer master, non specificare un codice sito per il client. Quando si crea un'immagine dei computer da questa immagine master, questi conterranno il client di Configuration Manager e dovranno completare l'assegnazione del sito al termine dell'installazione.  

> [!IMPORTANT]  
>  I computer con immagine non possono funzionare come client di Configuration Manager fino a quando i client di Configuration Manager non sono assegnati a un sito di Configuration Manager.  

 È necessario rimuovere i certificati specifici del computer installati nel computer dell'immagine master. Ad esempio, se si usano certificati di infrastruttura a chiave pubblica (PKI), è necessario rimuovere i certificati nell'archivio **Personale** per **Computer** e **Utente** prima di creare l'immagine del computer.  

 Se i client non possono eseguire query in Servizi di dominio Active Directory per individuare un punto di gestione, usano la chiave radice attendibile per determinare i punti di gestione attendibili. Se tutti i client creati da un'immagine verranno distribuiti nella stessa gerarchia del computer master, non rimuovere la chiave radice attendibile. Se i client saranno distribuiti in gerarchie differenti, rimuovere la chiave radice attendibile e, come procedura consigliata, eseguire il pre-provisioning di questi client con la nuova chiave radice attendibile. Per altre informazioni, vedere  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

#### <a name="to-prepare-the-client-computer-for-imaging"></a>Per preparare il computer client per la creazione dell'immagine  

1.  Installare manualmente il software client di Configuration Manager sul computer con immagine master. Per ulteriori informazioni, vedere [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Non specificare un codice sito di Configuration Manager per il client nelle proprietà della riga di comando CCMSetup.exe.  

2.  In un prompt dei comandi, digitare **net stop ccmexec** per accertarsi che il servizio **Host agenti di SMS** (Ccmexec.exe) non sia in esecuzione sul computer dell'immagine master.  

3.  Rimuovere i certificati memorizzati nell'archivio locale del computer dell'immagine master.  

4.  Se i client non saranno installati nella stessa gerarchia di Configuration Manager del computer con immagine master, rimuovere la chiave radice attendibile dal computer con immagine master.  

5.  Usare il software di creazione dell'immagine per acquisire l'immagine del computer master.  

6.  Distribuire l'immagine ai computer di destinazione.  

##  <a name="a-namebkmkclientworkgroupa-how-to-install-configuration-manager-clients-on-workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Come installare i client di Configuration Manager sui computer del gruppo di lavoro  
 Configuration Manager supporta l'installazione di client per i computer nei gruppi di lavoro. Installare il client nei computer nei gruppi di lavoro usando il metodo specificato in [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

 Per installare il client di Gestione configurazione nei computer del gruppo di lavoro devono essere soddisfatti i seguenti prerequisiti:  

-   Il client deve essere installato manualmente su ciascun computer del gruppo di lavoro. Durante l'installazione, l'utente connesso deve disporre dei diritti di amministratore locale sul computer del gruppo di lavoro.  

-   Per accedere alle risorse nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso di rete per il sito. È possibile specificare questo account come una proprietà del componente di distribuzione software. Per altre informazioni, vedere [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Sono previste alcune limitazioni al supporto dei computer del gruppo di lavoro:  

-   I client del gruppo di lavoro non possono individuare i punti di gestione dai Servizi di dominio Active Directory e devono quindi usare DNS, WINS o un altro punto di gestione.  

-   Il roaming globale non è supportato perché i client non possono eseguire query in Servizi di dominio Active Directory per ottenere le informazioni sul sito.  

-   I metodi di individuazione di Active Directory non sono in grado di individuare i computer nei gruppi di lavoro.  

-   Non è possibile distribuire software agli utenti dei computer del gruppo di lavoro.  

-   Non è possibile usare il metodo di installazione push client per installare il client sui computer del gruppo di lavoro.  

-   I client del gruppo di lavoro non possono usare l'autenticazione Kerberos e, pertanto, potrebbero richiedere l'approvazione manuale.  

-   Non è possibile configurare un client di un gruppo di lavoro come un punto di distribuzione. Configuration Manager richiede che i computer del punto di distribuzione siano membri di un dominio.  

#### <a name="to-install-the-client-on-workgroup-computers"></a>Per installare il client sui computer del gruppo di lavoro  

1.  Assicurarsi che i computer su cui si desidera installare il client soddisfino i precedenti prerequisiti.  

2.  Seguire le istruzioni della sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

     Esempio 1: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com**  

    > [!NOTE]  
    >  In questo esempio viene installato il client per la gestione client sulla intranet e vengono specificati codice sito e suffisso DNS per individuare un punto di gestione.  

     Esempio 2: **CCMSetup.exe FSP=fspserver.constoso.com**  

    > [!NOTE]  
    >  In questo esempio si richiede che il client si trovi in un percorso di rete configurato in un gruppo di limiti in modo che l'assegnazione automatica del sito sia completata correttamente. Il comando include un punto di stato di fallback sul server FSPSERVER, per tenere traccia della distribuzione client e per identificare eventuali problemi di comunicazione client.  

##  <a name="a-namebkmkclientinterneta-how-to-install-configuration-manager-clients-for-internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Come installare i client di Gestione configurazione per la gestione client basata su Internet  
 Quando il sito di Configuration Manager supporta la gestione client basata su Internet per client che si trovano a volte sulla intranet e a volte su Internet, sono disponibili due opzioni per l'installazione dei client sulla intranet:  

-   È possibile includere la proprietà Client.msi di CCMHOSTNAME=*&lt;FQDN Internet del punto di gestione basato su Internet\>* quando si installa il client, ad esempio usando l'installazione manuale o push client. Quando si usa questo metodo, è necessario anche assegnare direttamente il client al sito e non è possibile usare l'assegnazione automatica del sito. La sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual) in questo argomento fornisce un esempio di questo metodo di configurazione.  

-   È possibile installare il client per la gestione client sulla intranet e assegnare un punto di gestione client basato su Internet al client usando le proprietà client di Configuration Manager nel Pannello di controllo oppure usando uno script. Questo metodo consente di usare l'assegnazione client automatica. Per altre informazioni, vedere la sezione [Come configurare i client per la gestione client basata su Internet dopo l'installazione](#BKMK_ConfigureIBCM_MP) in questo argomento.  

 Se è necessario installare client che sono su Internet o perché sono esclusivamente client Internet o perché devono essere installati prima di tornare nella intranet, scegliere uno dei seguenti metodi supportati:  

-   Fornire un meccanismo che consenta a questi client di connettersi temporaneamente alla intranet usando una rete privata virtuale (VPN), quindi installarli usando uno dei metodi di installazione client appropriati.  

-   Usare un metodo di installazione indipendente da Configuration Manager, ad esempio creando un pacchetto dei file di origine dell'installazione client su un supporto rimovibile che può essere inviato agli utenti per l'installazione con le istruzioni. I file di origine dell'installazione client si trovano nella cartella *&lt;PercorsoInstallazione\>*\Client nel server del sito e nei punti di gestione di Configuration Manager. Includere nel supporto uno script per la copia manuale sulla cartella client e da questa cartella, installare il client usando CCMSetup.exe e tutte le proprietà della riga di comando CCMSetup appropriate.  

> [!NOTE]  
>  Configuration Manager non supporta l'installazione di un client direttamente dal punto di gestione basato su Internet o dal punto di aggiornamento software basato su Internet.  

 Dal momento che i client gestiti su Internet devono comunicare con i sistemi del sito basati su Internet, assicurarsi che su questi client siano anche installati certificati di infrastruttura a chiave pubblica (PKI) prima della loro installazione. È necessario installare tali certificati in modo indipendente da Configuration Manager. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

#### <a name="to-install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Per installare i client su Internet specificando le proprietà della riga di comando CCMSetup  

1.  Seguire le istruzioni nella sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual) e includere sempre quanto segue:  

    -   Proprietà della riga di comando CCMSetup **/source:***&lt;percorso locale alla cartella client copiata\>*  

    -   Proprietà della riga di comando CCMSetup **/UsePKICert**  

    -   Proprietà Client.msi **CCMHOSTNAME=***&lt;FQDN del punto di gestione basato su Internet\>*  

    -   Proprietà Client.msi **SMSSIGNCERT=***&lt;percorso locale al certificato di firma del server del sito esportato\>*  

    -   Proprietà Client.msi **SMSSITECODE=***&lt;codice sito del punto di gestione basato su Internet\>*  

    > [!NOTE]  
    >  Se il sito dispone di più di un punto di gestione basato su Internet, non avrà importanza quale punto di gestione basato su Internet sarà specificato per la proprietà CCMHOSTNAME. Quando un client di Configuration Manager si connette al punto di gestione basato su Internet specificato, questo invierà al client un elenco di punti di gestione basati su Internet disponibili nel sito e il client ne selezionerà uno. La selezione è non deterministica.  

2.  Se non si desidera che il client controlli l'elenco di revoche di certificati (CRL), specificare la proprietà della riga di comando CCMSetup **/NoCRLCheck**.  

3.  Se si sta usando un punto di stato di fallback basato su Internet, specificare la proprietà Client.msi **FSP=***&lt;FQDN Internet del punto di stato di fallback basato su Internet\>*.  

4.  Se si sta installando il client per la gestione client Internet esclusiva, specificare la proprietà Client.msi **CCMALWAYSINF=1**.  

5.  Verificare se è necessario specificare proprietà della riga di comando CCMSetup aggiuntive. Ad esempio, potrebbe essere necessario specificare un criterio di selezione del certificato qualora il client disponesse di più di un certificato PKI valido. Per un elenco delle proprietà disponibili, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

     Esempio: **CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1**  

    > [!NOTE]  
    >  In questo esempio vengono installati i file di origine client da una cartella sull'unità D con le impostazioni per l'utilizzo di un certificato client PKI e la selezione del certificato con il periodo di validità più lungo per la gestione client Internet esclusiva. Viene inoltre assegnato il client per l'utilizzo del punto di gestione basato su Internet denominato SERVER1 e il punto di stato di fallback basato su Internet nel dominio contoso.com, quindi il client viene assegnato al sito ABC.  

###  <a name="a-namebkmkconfigureibcmmpa-how-to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> Come configurare i client per la gestione client basata su Internet dopo l'installazione  
 Per assegnare il punto di gestione basato su Internet dopo l'installazione del client, usare una delle seguenti procedure. La prima procedura richiede la configurazione manuale e, pertanto, è adatta ai casi in cui si dispone di pochi client, mentre la seconda procedura è più indicata per la configurazione di molti client.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Per configurare i client per la gestione client basata su Internet dopo l'installazione tramite l'assegnazione del punto di gestione basato su Internet nelle proprietà di Configuration Manager  

1.  Passare a **Configuration Manager** nel Pannello di controllo del computer client, quindi fare doppio clic per aprirne le relative proprietà.  

2.  Nella scheda **Internet** immettere il nome di dominio completo del punto di gestione basato su Internet nella casella di testo dell'FQDN Internet.  

    > [!NOTE]  
    >  La scheda **Internet** è disponibile solo per i client che dispongono di un certificato PKI.  

3.  Se il client accede a Internet tramite un server proxy, immettere le impostazioni di tale server.  

4.  Fare clic su **OK**.  

##### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Per configurare i client per la gestione client basata su Internet dopo l'installazione tramite script  

1.  Aprire un editor di testo, come Blocco note.  

2.  Copiare e inserire quanto di seguito riportato nel file:  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the Internet-Based Management Point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

3.  Sostituire *mp.contoso.com* con l'FQDN Internet del punto di gestione basato su Internet.  

    > [!NOTE]  
    >  Se è necessario eliminare un punto di gestione basato su Internet specificato affinché il client non sia configurato per l'utilizzo di un punto di gestione basato su Internet, rimuovere il valore all'interno delle virgolette in modo che questa riga diventi **newInternetBasedManagementPointFQDN = ""**.  

4.  Salvare il file con un'estensione .vbs.  

5.  Usare cscript per eseguire lo script sui computer client, ricorrendo a uno dei seguenti metodi:  

    -   Distribuire il file ai client di Configuration Manager esistenti usando un pacchetto e un programma.  

    -   Eseguire il file localmente sui client di Configuration Manager esistenti facendo doppio clic sul file di script in Esplora risorse.  

 Potrebbe essere necessario riavviare il client affinché la nuova impostazione in questo script diventi effettiva.  

##  <a name="a-namebkmkprovisiona-how-to-provision-client-installation-properties-group-policy-and-software-update-based-client-installation"></a><a name="BKMK_Provision"></a> Come eseguire il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software)  
 È possibile usare i Criteri di gruppo di Windows per eseguire il provisioning dei computer nell'azienda con le proprietà di installazione client di Configuration Manager. Queste proprietà vengono memorizzate nel Registro di sistema del computer e lette al momento dell'installazione del software client. Questa procedura non è di norma necessaria per Configuration Manager. Tuttavia, potrebbe essere necessaria in alcuni scenari di installazione client, come i seguenti:  

-   Si stanno usando le impostazioni dei Criteri di gruppo o i metodi di installazione client basati su aggiornamento software e lo schema di Active Directory per Configuration Manager non è stato esteso.  

-   Si desidera sostituire le proprietà di installazione client su computer specifici.  

> [!NOTE]  
>  Se nella riga di comando CCMSetup.exe vengono specificate delle proprietà di installazione, le proprietà di cui viene eseguito il provisioning sui computer non saranno usate.  

 Il supporto di installazione di Configuration Manager offre un modello amministrativo di Criteri di gruppo denominato ConfigMgrInstallation.adm che può essere usato per eseguire il provisioning dei computer client con le proprietà di installazione. Usare la procedura seguente per configurare e assegnare tale modello ai computer dell'organizzazione.  

#### <a name="to-configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Per configurare e assegnare le proprietà di installazione client tramite un oggetto Criteri di gruppo  

1.  Importare il modello amministrativo ConfigMgrInstallation.adm in un oggetto Criteri di gruppo nuovo o esistente usando un editor quale l'Editor oggetti Criteri di gruppo di Windows.  

    > [!NOTE]  
    >  Tale file è disponibile nella cartella **TOOLS\ConfigMgrADMTemplates** del supporto di installazione di Configuration Manager.  

2.  Aprire le proprietà dell'impostazione importata **Configurare le impostazioni di distribuzione client**.  

3.  Fare clic su **Attivato**.  

4.  Nella casella **CCMSetup** immettere le proprietà necessarie della riga di comando di CCMSetup. Per un elenco di tutte le proprietà della riga di comando di CCMSetup con i relativi esempi di uso, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Assegnare l'oggetto Criteri di gruppo ai computer per i quali si intende eseguire il provisioning delle proprietà di installazione client di Configuration Manager.  

 Per informazioni sui Criteri di gruppo di Windows, consultare la documentazione di Windows Server.  



<!--HONumber=Nov16_HO1-->

