---
title: Account | System Center Configuration Manager
description: Identificare e gestire i gruppi di Windows e gli account in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c3e19bd216523cc75b9a22672d030bb528b32555


---
# <a name="accounts-used-in-system-center-configuration-manager"></a>Account usati in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni seguenti per identificare i gruppi di Windows e gli account usati in System Center Configuration Manager, le relative modalità d'uso ed eventuali requisiti.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Gruppi Windows creati e usati da Configuration Manager  
 Configuration Manager crea automaticamente e, in molti casi, gestisce automaticamente i gruppi seguenti di Windows:  

> [!NOTE]  
>  Quando Configuration Manager crea un gruppo in un computer appartenente a un dominio, il gruppo è un gruppo di sicurezza locale. Se il computer è un controller di dominio, il gruppo è un gruppo locale di dominio condiviso da tutti i controller di dominio del dominio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Questo gruppo è usato da Configuration Manager per concedere l'accesso per la visualizzazione dei file raccolti dall'inventario software.  

Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato nel server del sito primario.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Appartenenze|Configuration Manager gestisce automaticamente l'appartenenza a gruppi. L'appartenenza comprende gli utenti amministratori a cui è concessa l'autorizzazione **Visualizza file raccolti** per l'oggetto a protezione diretta **Raccolta** da un ruolo di sicurezza assegnato.|  
|Autorizzazioni|Per impostazione predefinita, questo gruppo dispone dell'autorizzazione di **Read** per la seguente cartella nel server del sito: **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Questo gruppo è un gruppo di sicurezza locale creato nel server del database del sito o nel server di replica di database da Configuration Manager e non è attualmente usato. Questo gruppo è riservato per l'uso futuro da parte da Configuration Manager.  

### <a name="configmgr-remote-control-users"></a>Utenti di Controllo remoto di ConfigMgr  
 Questo gruppo viene usato dagli strumenti remoti di Configuration Manager per l'archiviazione di account e gruppi configurati nell'elenco dei visualizzatori autorizzati assegnati a ogni client.  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato nel client di Configuration Manager quando il client riceve criteri che abilitano gli strumenti remoti.<br /><br /> Dopo la disattivazione degli strumenti per un client, questo gruppo non viene rimosso automaticamente ed è necessario rimuoverlo manualmente da ogni computer client.|  
|Appartenenze|Per impostazione predefinita, non esistono membri per questo gruppo. Gli utenti aggiunti all'elenco dei visualizzatori autorizzati vengono aggiunti automaticamente a questo gruppo.<br /><br /> Invece di aggiungere direttamente utenti o gruppi, è possibile usare l'elenco dei visualizzatori autorizzati per gestire l'appartenenza a questo gruppo.<br /><br /> Oltre a essere un visualizzatore autorizzato, un utente amministratore deve disporre dell'autorizzazione **Controllo remoto** per l'oggetto **Raccolta** . È possibile assegnare questa autorizzazione tramite il ruolo di sicurezza Operatore strumenti remoti.|  
|Autorizzazioni|Per impostazione predefinita, questo gruppo non dispone delle autorizzazioni per accedere a qualsiasi percorso nel computer e viene usata esclusivamente per includere l'elenco dei visualizzatori autorizzati.|  

### <a name="sms-admins"></a>SMS Admins  
 Questo gruppo viene usato da Configuration Manager per concedere l'accesso al provider SMS tramite WMI. L'accesso al provider SMS è necessario per visualizzare e modificare gli oggetti nella console di Configuration Manager.  

> [!NOTE]  
>  La configurazione dell'amministrazione basata su ruoli di un utente amministratore determina gli oggetti che è possibile visualizzare e gestire usando la console di Configuration Manager.  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato in ogni computer che dispone di un provider SMS.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Appartenenze|Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, ogni utente amministratore di una gerarchia e l'account computer del server del sito appartengono al gruppo SMS Admins in ciascun computer del provider SMS in un sito.|  
|Autorizzazioni|I diritti e le autorizzazioni SMS Admins vengono impostati nello snap-in MMC del controllo WMI. Per impostazione predefinita, al gruppo SMS Admins vengono concessi **Enable Account** e **Remote Enable** nello spazio dei nomi Root\SMS. Gli utenti autenticati dispongono di **Execute Methods**, **Provider Write**e **Enable Account**<br /><br /> Gli utenti amministratori che usano una console di Configuration Manager remota richiedono autorizzazioni DCOM per l'attivazione remota sul computer del server di sito e sul computer del provider SMS. È consigliabile concedere questi diritti a SMS Admins per semplificare l'amministrazione anziché concedere questi diritti direttamente a utenti o a gruppi. Per ulteriori informazioni, vedere la sezione [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) nell'argomento [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;codicesito\>  
 Il gruppo è usato dai punti di gestione di Configuration Manager remoti per connettersi al database del sito dal server del sito. Questo gruppo consente l'accesso del punto di gestione alle cartelle della posta in arrivo nel server del sito e nel database del sito.  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato in ogni computer che dispone di un provider SMS.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Appartenenze|Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza include gli account computer dei computer remoti che dispongono di un punto di gestione per il sito.|  
|Autorizzazioni|Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la cartella **%percorso%\Microsoft Configuration Manager\inboxes** del server del sito. Questo gruppo dispone inoltre dell'autorizzazione di **Write** per varie sottocartelle delle **inboxes** in cui il punto di gestione scrive i dati client.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;codicesito\>  
 Il gruppo è usato dai computer del provider SMS di Configuration Manager remoti per connettersi al server del sito dal server del sito.  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato nel server del sito.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Appartenenze|Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza comprende l'account computer o l'account utente di dominio usato per la connessione al server del sito da ciascun computer remoto in cui è installato un provider SMS per il sito.|  
|Autorizzazioni|Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la cartella **%percorso%\Microsoft Configuration Manager\inboxes** del server del sito. Questo gruppo dispone inoltre dell'autorizzazione di **Write** o delle autorizzazioni di **Scrittura** e **Modifica** per varie sottocartelle delle **inboxes** per cui il provider SMS richiede l'accesso.<br /><br /> Questo gruppo include anche le autorizzazioni di **Lettura**, **Lettura ed esecuzione**, **Visualizzazione contenuto cartella**, **Scrittura** e **Modifica** per le cartelle in **%percorso%\Microsoft Configuration Manager\OSD\boot** e autorizzazione di **Lettura** per le cartelle in **%percorso%\Microsoft Configuration Manager\OSD\Bin** del server del sito.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;codicesito\>  
 Questo gruppo viene usato da Gestione invio file nei computer del sistema del sito remoto di Configuration Manager per la connessione al server del sito.  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato nel server del sito.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Appartenenze|Configuration Manager gestisce automaticamente l'appartenenza a gruppi. Per impostazione predefinita, l'appartenenza comprende l'account computer o l'account utente di dominio usato per la connessione al server del sito da ciascun computer del sistema del sito remoto che esegue Gestione invio file.|  
|Autorizzazioni|Per impostazione predefinita, questo gruppo include le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella** per la cartella **%percorso%\Microsoft Configuration Manager\inboxes** e per le varie sottocartelle in questo percorso del server del sito. Questo gruppo dispone inoltre delle autorizzazioni di **Scrittura** e **Modifica** per la cartella **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** nel server del sito.|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;codicesito\>  
 Questo gruppo viene usato da Configuration Manager per abilitare la replica basata su file tra siti di una gerarchia. Per ciascun sito remoto che esegue il trasferimento diretto di file in questo sito, questo gruppo contiene account configurati come un **account di replica file**  

 Nella seguente tabella sono elencati dettagli aggiuntivi per questo gruppo:  

|Dettagli|Altre informazioni|  
|------------|----------------------|  
|Tipo e percorso|Questo è un gruppo di sicurezza locale creato nel server del sito.|  
|Appartenenze|Quando viene installato un nuovo sito come sito figlio di un altro sito, Configuration Manager aggiunge automaticamente l'account computer del nuovo sito al gruppo nel server del sito padre e l'account computer del sito padre al gruppo nel nuovo server del sito. Se viene specificato un altro account per i trasferimenti basati su file, aggiungere l'account al gruppo nel server del sito di destinazione.<br /><br /> Quando si disinstalla un sito, questo gruppo non viene rimosso automaticamente e deve essere eliminato manualmente.|  
|Autorizzazioni|Per impostazione predefinita, il gruppo dispone del **controllo completo** per la cartella **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** .|  

## <a name="accounts-that-configuration-manager-uses"></a>Account usati da Configuration Manager  
 È possibile configurare gli account seguenti per Configuration Manager:  

### <a name="active-directory-group-discovery-account"></a>Account di individuazione gruppo Active Directory  
 L' **account di individuazione gruppo Active Directory** viene usato per individuare gruppi di sicurezza locali, globali e universali, l'appartenenza all'interno di tali gruppi e l'appartenenza all'interno dei gruppi di distribuzione dei percorsi specificati in Servizi di dominio Active Directory. I gruppi di distribuzione non vengono rilevati come risorse di gruppo.  

 Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

### <a name="active-directory-system-discovery-account"></a>Account individuazione sistema Active Directory  
 L' **account individuazione sistema Active Directory** viene usato per individuare computer nei percorsi specificati in Servizi di dominio Active Directory.  

 Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

### <a name="active-directory-user-discovery-account"></a>Account individuazione utente Active Directory  
 L' **account individuazione utente Active Directory** viene usato per individuare gli account utente nei percorsi specificati in Servizi di dominio Active Directory.  

 Questo account può essere un account computer del server del sito che esegue l'individuazione o un account utente Windows. L'account deve disporre dell'autorizzazione di accesso in **Lettura** ai percorsi di Active Directory specificati per l'individuazione.  

### <a name="active-directory-forest-account"></a>Account foresta Active Directory  
 L' **account foresta Active Directory** viene usato per individuare l'infrastruttura di rete nelle foreste Active Directory e viene anche usato dai siti di amministrazione centrale e dai siti primari per la pubblicazione dei dati del sito in Servizi di dominio Active Directory di una foresta.  

> [!NOTE]  
>  I siti secondari usano sempre l'account computer del server del sito secondario per la pubblicazione in Active Directory.  

> [!NOTE]  
>  L'account foresta Active Directory deve essere un account globale per l'individuazione e la pubblicazione in foreste non trusted. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

 L'account deve disporre delle autorizzazioni di **Lettura** per ogni foresta Active Directory in cui di desidera individuare l'infrastruttura di rete.  

 L'account deve disporre delle autorizzazioni di **Controllo completo** per il contenitore di System Management e per i relativi oggetti figlio in tutte le foreste Active Directory in cui si desidera pubblicare i dati del sito.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Account server proxy del punto di sincronizzazione di Asset Intelligence  
 L' **account server proxy del punto di sincronizzazione di Asset Intelligence** viene usato dal punto di sincronizzazione di Asset Intelligence per accedere a Internet con un server proxy o un firewall che richiede l'accesso autenticato.  

> [!IMPORTANT]  
>  Specificare un account che disponga delle autorizzazioni minime per il server proxy o il firewall richiesti.  

### <a name="certificate-registration-point-account"></a>Account del punto di registrazione certificati  
 L'**account del punto di registrazione certificati** connette il punto di registrazione certificati al database di Configuration Manager. Per impostazione predefinita, viene usato l'account computer del server del punto di registrazione certificati, ma è tuttavia possibile configurare un account utente. È necessario specificare un account utente ogni volta che il punto di registrazione certificati si trova in un dominio non attendibile dal server del sito. Questo account richiede solo l'accesso in lettura al database del sito, poiché le operazioni di scrittura vengono gestite dal sistema dei messaggio di stato.  

### <a name="capture-operating-system-image-account"></a>Account di acquisizione immagine del sistema operativo  
 L' **account di acquisizione immagine del sistema operativo** viene usato da Configuration Manager per accedere alla cartella in cui sono archiviate le immagini acquisite quando si distribuiscono i sistemi operativi. Questo account è necessario se si aggiunge il passaggio **Acquisisci immagine del sistema operativo** a una sequenza di attività.  

 L'account deve disporre delle autorizzazioni di **Lettura** e **Scrittura** nella condivisione di rete in cui sono archiviate le immagini acquisite.  

 Se si cambia la password dell'account in Windows, è necessario aggiornare la sequenza di attività con la nuova password. Il client di Configuration Manager riceverà la nuova password durante il successivo download dei criteri client.  

 Se si usa questo account, è possibile creare un account utente di dominio con le autorizzazioni minime per accedere alle risorse di rete richieste e usarlo per tutti gli account delle sequenze di attività.  

> [!IMPORTANT]  
>  Non assegnare a questo account delle autorizzazioni di accesso interattivo.  
>   
>  Non usare l'account di accesso alla rete per questo account.  

### <a name="client-push-installation-account"></a>Account di installazione push client  
 L' **account di installazione push client** viene usato per la connessione ai computer e per l'installazione del software client di Configuration Manager se si distribuiscono i client usando l'installazione push client. Se questo account non è specificato, l'account del server del sito viene usato per tentare di installare il software client.  

 Questo account deve essere membro del gruppo **Amministratori** locale nei computer in cui deve essere installato il software client di Configuration Manager. Questo account non necessita di diritti di amministratore di dominio.  

 È possibile specificare uno o più account di installazione push client, che Configuration Manager proverà in successione fino a quando uno di essi non avrà esito positivo.  

> [!TIP]  
>  Per coordinare in modo più efficace gli aggiornamenti di account in distribuzioni ampie di Active Directory, creare un nuovo account con un nome diverso e aggiungere il nuovo account all'elenco degli account di installazione push client in Configuration Manager. Attendere un tempo sufficiente per la replica del nuovo account da parte di Active Directory Domain Services e rimuovere il vecchio account da Configuration Manager e da Active Directory Domain Services.  

> [!IMPORTANT]  
>  Non concedere a questo account il diritto di accesso locale.  

### <a name="enrollment-point-connection-account"></a>account di connessione al punto di registrazione  
 L' **account di connessione al punto di registrazione** connette il punto di registrazione al database del sito di Configuration Manager. Per impostazione predefinita, viene usato l'account computer del punto di registrazione, ma è tuttavia possibile configurare un account utente. È necessario specificare un account utente ogni volta che il punto di registrazione si trova in un dominio non attendibile dal server del sito. Questo account richiede l'accesso in lettura e scrittura al database del sito.  

### <a name="exchange-server-connection-account"></a>Account di connessione a Exchange Server  
 L' **account di connessione a Exchange Server** collega il server del sito al computer Exchange Server specificato per trovare e gestire i dispositivi mobili che si connettono a Exchange Server. Questo account richiede i cmdlet di Exchange PowerShell che forniscono le autorizzazioni necessarie per il computer Exchange Server. Per altre informazioni sui cmdlet, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Account server proxy del connettore Exchange Server  
 L' **account server proxy del connettore Exchange Server** viene usato dal connettore Exchange Server per accedere a Internet con un server proxy o un firewall che richiede l'accesso autenticato.  

> [!IMPORTANT]  
>  Specificare un account che disponga delle autorizzazioni minime per il server proxy o il firewall richiesti.  

### <a name="management-point-connection-account"></a>Account di connessione al punto di gestione  
 L'**account di connessione al punto di gestione** viene usato per collegare il punto di gestione al database del sito di Configuration Manager, in modo che possa inviare e recuperare informazioni per i client. Per impostazione predefinita, viene usato l'account computer del punto di gestione, ma è tuttavia possibile configurare un account utente. È necessario specificare un account utente ogni volta che il punto di gestione si trova in un dominio non attendibile dal server del sito.  

 Creare l'account come account locale e con diritti limitati sul computer con Microsoft SQL Server in esecuzione.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti di accesso interattivo.  

### <a name="multicast-connection-account"></a>Account di connessione multicast  
 L' **account di connessione multicast** viene usato dai punti di distribuzione configurati in modo che il multicast legga le informazioni dal database del sito. Per impostazione predefinita, viene usato l'account computer del punto di distribuzione, ma è tuttavia possibile configurare un account utente. Ogni volta che il database del sito si trova in una foresta non trusted, è necessario specificare un account utente. Ad esempio, se il data center dispone di una rete perimetrale in una foresta diversa dal server del sito e dal database del sito, è possibile usare questo account per leggere le informazioni multicast dal database del sito.  

 Se si crea questo account, crearlo come account locale e con diritti limitati sul computer con Microsoft SQL Server in esecuzione.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti di accesso interattivo.  

### <a name="network-access-account"></a>Account di accesso alla rete  
 L' **account di accesso alla rete** viene usato dai computer client quando questi non possono usare il loro account computer locale per accedere al contenuto nei punti di distribuzione. Ad esempio, si applica a client e computer di gruppi di lavoro di domini non attendibili. Questo account può anche essere usato durante la distribuzione del sistema operativo quando il computer che installa il sistema operativo non dispone ancora di un account computer nel dominio.  

> [!NOTE]  
>  L'Account di accesso alla rete non viene mai usato come contesto di protezione per eseguire programmi, installare aggiornamenti software oppure eseguire sequenze di attività, ma solo per l'accesso alle risorse in rete.  

 Concedere a questo account le autorizzazioni minime appropriate sul contenuto che il client richiede per accedere al software. L'account deve disporre del diritto **Accedi al computer dalla rete** nel punto di distribuzione o in un altro server che contiene il contenuto del pacchetto.  È possibile configurare fino a 10 account di accesso alla rete per sito.  

> [!WARNING]  
>  Quando Configuration Manager tenta di usare l'account nomecomputer$ per scaricare il contenuto ma non ci riesce, ritenta automaticamente con l'Account di accesso alla rete anche se ci ha già provato in precedenza non riuscendoci.  

 Creare l'account in tutti i domini che forniranno l'accesso necessario alle risorse. L'account di accesso alla rete deve sempre includere un nome di dominio. La protezione pass-through non è supportata per questo account. Se si dispone di punti di distribuzione in più domini, creare l'account in un dominio attendibile.  

> [!TIP]  
>  Per evitare blocchi degli account, non modificare la password per un account di accesso alla rete esistente. Al contrario, creare un nuovo account e configurarlo in Configuration Manager. Quando è trascorso tempo sufficiente e tutti i client hanno ricevuto i dettagli del nuovo account, rimuovere il vecchio account dalle cartelle condivise in rete ed eliminare l'account.  

> [!IMPORTANT]  
>  Non concedere a questo account i diritti di accesso interattivo.  
>   
>  Non concedere a questo account il diritto di aggiungere computer al dominio. Se è necessario aggiungere computer al dominio durante una sequenza di attività, usare l'account di aggiunta dominio dell'editor della sequenza di attività.  

### <a name="package-access-account"></a>Account di accesso al pacchetto  
 Un **account di accesso ai pacchetti** consente di impostare le autorizzazioni NTFS per specificare gli utenti e i gruppi di utenti che possono accedere a una cartella del pacchetto nei punti di distribuzione. Per impostazione predefinita, Configuration Manager concede accesso solo agli account di accesso generici **Utenti** e **Amministratori**, ma è possibile controllare l'accesso per i computer client usando gruppi o account Windows aggiuntivi. I dispositivi mobili recuperano sempre il contenuto del pacchetto in modo anonimo, in modo che gli Account di accesso al pacchetto non vengono usati dal dispositivo mobile.  

 Per impostazione predefinita, quando Configuration Manager crea la condivisione pacchetto in un punto di distribuzione, concede l'accesso di **Lettura** al gruppo **Utenti** locale e **Controllo completo** al gruppo **Amministratori** locale. Le autorizzazioni effettivamente necessarie dipenderanno dal pacchetto. Se si dispone di client in gruppi di lavoro o in foreste non trusted, tali client usano l'account di accesso alla rete per accedere al contenuto del pacchetto. Assicurarsi che l'Account di accesso alla rete disponga delle autorizzazioni per il pacchetto usando gli Account di accesso al pacchetto definiti.  

 Usare gli account in un dominio che possa accedere ai punti di distribuzione. Se si crea o si modifica l'account dopo la creazione del pacchetto, è necessario ridistribuire il pacchetto. L'aggiornamento del pacchetto non modifica le autorizzazioni NTFS sul pacchetto.  

 Non è necessario aggiungere l'account di accesso alla rete come account di accesso al pacchetto, poiché l'appartenenza al gruppo Utenti lo aggiunge automaticamente. La limitazione dell'account di accesso al pacchetto al solo account di accesso alla rete non impedisce ai client di accedere al pacchetto.  

### <a name="reporting-services-point-account"></a>Account punto di Reporting Services  
 L' **account punto di Reporting Services** viene usato da SQL Server Reporting Services per recuperare i dati per i report di Configuration Manager dal database del sito. La password e l'account utente Windows specificati vengono crittografati e archiviati nel database di SQL Server Reporting Services.  

### <a name="remote-tools-permitted-viewer-accounts"></a>Account visualizzatori autorizzati di strumenti remoti  
 Gli account specificati come **Visualizzatori autorizzati** per il controllo remoto sono un elenco di utenti a cui è consentito usare le funzionalità di strumenti remoti nei client.  

### <a name="site-system-installation-account"></a>Account di installazione sistema del sito  
 L' **account di installazione del sistema del sito** viene usato dal server del sito per installare, reinstallare, disinstallare e configurare i sistemi del sito. Se si configura il sistema del sito in modo che il server del sito avvii le connessioni a questo sistema del sito, Configuration Manager usa anche questo account per eseguire il pull dei dati dal computer di sistema del sito dopo l'installazione del sistema del sito e di tutti i ruoli di sistema del sito. Ogni sistema del sito può disporre di un account di installazione sistema del sito diverso, ma è possibile configurare solo un account di installazione sistema del sito per gestire tutti i ruoli del sistema del sito in tale sistema del sito.  

 Questo account richiede le autorizzazioni amministrative locali nei sistemi del sito che verranno installati e configurati. Inoltre, questo account deve disporre del diritto **Accedi al computer dalla rete** del criterio di sicurezza nei sistemi del sito che verranno installati e configurati.  

> [!TIP]  
>  Se si dispone di numerosi controller di dominio e questi account verranno usati nei domini, verificare che gli account siano stati replicati prima di configurare il sistema del sito.  
>   
>  Quando si specifica un account locale in ogni sistema del sito da gestire, questa configurazione è più sicura dell'utilizzo di account di dominio poiché limita il danno che gli utenti malintenzionati possono causare se l'account viene compromesso. Tuttavia, gli account di dominio sono più facili da gestire, quindi tenere presente il compromesso tra protezione e amministrazione efficiente.  

### <a name="smtp-server-connection-account"></a>Account di connessione al server SMTP  
 L' **account di connessione al server SMTP** viene usato dal server del sito per inviare avvisi e-mail quando il server SMTP richiede l'accesso autenticato.  

> [!IMPORTANT]  
>  Specificare un account che disponga delle autorizzazioni minime per l'invio di e-mail.  

### <a name="software-update-point-connection-account"></a>Account di connessione al punto di aggiornamento software  
 L' **account di connessione al punto di aggiornamento software** viene usato dal server del sito per i due servizi di aggiornamento software seguenti:  

-   Configuration Manager WSUS, che configura impostazioni quali classificazioni, definizioni di prodotti e impostazioni upstream.  

-   Gestione sincronizzazione WSUS, che richiede la sincronizzazione a un server WSUS upstream o a Microsoft Update.  

L'account di installazione sistema del sito può installare i componenti per gli aggiornamenti software, ma non può eseguire funzioni specifiche di aggiornamenti software nel punto di aggiornamento software. Se non è possibile usare l'account del computer del server di sito per questa funzionalità poiché il punto di aggiornamento software si trova in una foresta non trusted, è necessario specificare questo account oltre all'account di installazione sistema del sito.  

Questo account deve essere un amministratore locale nel computer in cui è installato Windows Server Update Services e deve far parte del gruppo Administrators WSUS locale.  

### <a name="software-update-point-proxy-server-account"></a>Account del server proxy del punto di aggiornamento software  
 L' **account del server proxy del punto di aggiornamento software** viene usato dal punto di aggiornamento software per accedere a Internet con un server proxy o un firewall che richiede l'accesso autenticato.  

> [!IMPORTANT]  
>  Specificare un account che disponga delle autorizzazioni minime per il server proxy o il firewall richiesti.  

### <a name="source-site-account"></a>Account del sito di origine  
 L' **account del sito di origine** viene usato dal processo di migrazione per accedere al provider SMS del sito di origine. Questo account richiede autorizzazioni di **Lettura** per gli oggetti del sito presenti nel sito di origine per raccogliere dati per i processi di migrazione.  

 Se si aggiornano siti secondari o punti di distribuzione di Configuration Manager 2007 che hanno punti di distribuzione condivisi nei punti di distribuzione per System Center Configuration Manager, questo account deve avere anche le autorizzazioni **Elimina** per la classe **Sito** per rimuovere il punto di distribuzione dal sito di Configuration Manager 2007 durante l'aggiornamento.  

> [!NOTE]  
>  L'account del sito di origine e l'account del database del sito di origine vengono identificati come **Gestione migrazione** nel nodo **Account** dell'area di lavoro **Amministrazione** nella console di Configuration Manager.  

### <a name="source-site-database-account"></a>Account del database del sito di origine  
 L' **account del database del sito di origine** viene usato dal processo di migrazione per accedere al database di SQL Server per il sito di origine. Per raccogliere dati dal database di SQL Server del sito di origine, l'account del database del sito di origine deve disporre delle autorizzazioni **Lettura** e **Esegui** per il database di SQL Server del sito di origine.  

> [!NOTE]  
>  Se si usa un account computer di System Center Configuration Manager, verificare che tutte le opzioni seguenti siano vere per tale account:  
>   
>  -   È un membro del gruppo di sicurezza **Distributed COM Users** nel dominio in cui risiede il sito di Configuration Manager 2007.  
> -   È un membro del gruppo di sicurezza **SMS Admins** .  
> -   Ha l'autorizzazione **Lettura** per tutti gli oggetti di Configuration Manager 2007.  

> [!NOTE]  
>  L'account del sito di origine e l'account del database del sito di origine vengono identificati come **Gestione migrazione** nel nodo **Account** dell'area di lavoro **Amministrazione** nella console di Configuration Manager.  

### <a name="task-sequence-editor-domain-joining-account"></a>Account di aggiunta dominio dell'editor della sequenza di attività  
 L' **account per l'aggiunta al dominio nell'editor delle sequenze di attività** viene usato in una sequenza di attività per aggiungere un nuovo computer con immagine a un dominio. Questo account è necessario se si aggiunge il passaggio **Aggiunta a dominio o gruppo di lavoro** a una sequenza di attività e quindi si seleziona **Aggiunta a un dominio**. Questo account può essere configurato anche se si aggiunge il passaggio **Applica impostazioni di rete** a una sequenza di attività, ma non è necessario.  

 Questo account richiede il diritto **Aggiungi a dominio** nel dominio a cui il computer verrà aggiunto.  

> [!TIP]  
>  Se è necessario questo account per le sequenze attività, è possibile creare un account utente di dominio con le autorizzazioni minime per accedere alle risorse di rete richieste e usarlo per tutti gli account delle sequenze attività.  

> [!IMPORTANT]  
>  Non assegnare a questo account delle autorizzazioni di accesso interattivo.  
>   
>  Non usare l'account di accesso alla rete per questo account.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Account di connessione cartella di rete dell'editor della sequenza di attività  
 L' **account di connessione di cartelle di rete nell'editor delle sequenze di attività** viene usato da una sequenza di attività per la connessione a una cartella condivisa in rete. Questo account è necessario se si aggiunge il passaggio **Connetti alla cartella di rete** a una sequenza di attività.  

 Questo account richiede autorizzazioni per accedere alla cartella condivisa specificata e deve essere un account utente di dominio.  

> [!TIP]  
>  Se è necessario questo account per le sequenze attività, è possibile creare un account utente di dominio con le autorizzazioni minime per accedere alle risorse di rete richieste e usarlo per tutti gli account delle sequenze attività.  

> [!IMPORTANT]  
>  Non assegnare a questo account delle autorizzazioni di accesso interattivo.  
>   
>  Non usare l'account di accesso alla rete per questo account.  

### <a name="task-sequence-run-as-account"></a>Sequenza di attività eseguita come account  
 La **sequenza di attività eseguita come account** viene usata per eseguire righe di comando in sequenze di attività e usare credenziali diverse dall'account di sistema locale. Questo account è necessario se si aggiunge il passaggio **Esegui riga di comando** a una sequenza di attività ma non si desidera che questa venga eseguita con autorizzazioni dell'account di sistema locale nel computer gestito.  

 Configurare l'account in modo che disponga delle autorizzazioni minime necessarie per eseguire la riga di comando specificata nella sequenza di attività. L'account deve disporre dei diritti di accesso interattivo e in genere richiede la possibilità di installare il software e accedere alle risorse di rete.  

> [!IMPORTANT]  
>  Non usare l'account di accesso alla rete per questo account.  
>   
>  Non modificare mai l'account in amministratore di dominio.  
>   
>  Non configurare mai profili mobili per questo account. Quando viene eseguita la sequenza di attività, verrà scaricato il profilo mobile per l'account, che rende il profilo vulnerabile all'accesso sul computer locale.  
>   
>  Limitare l'ambito dell'account. Ad esempio, creare diverse esecuzioni della sequenza di attività come account per ciascuna sequenza di attività, in modo che nel caso in cui venga compromesso un account, vengano compromessi solo i computer client a cui tale account ha accesso.  
>   
>  Se la riga di comando richiede accesso amministrativo al computer, creare un account amministratore locale unicamente per l'esecuzione della sequenza di attività come account su tutti i computer che eseguiranno la sequenza di attività ed eliminare l'account non appena non è più necessario.  



<!--HONumber=Nov16_HO1-->


