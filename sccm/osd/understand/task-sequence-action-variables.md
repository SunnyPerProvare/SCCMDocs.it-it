---
title: Variabili di azione delle sequenze di attività
titleSuffix: Configuration Manager
description: Usare le variabili di azione della sequenza, ad esempio le variabili di impostazione della rete, per specificare le impostazioni di configurazione per un singolo passaggio in una sequenza di attività di Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variabili di azione delle sequenze di attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le variabili di azione delle sequenze di attività specificano le impostazioni di configurazione usate da un singolo passaggio in una sequenza di attività di System Center Configuration Manager. Per impostazione predefinita, il passaggio della sequenza di attività inizializza le impostazioni prima dell'esecuzione. Queste impostazioni sono disponibili solo mentre il passaggio della sequenza di attività associato è in esecuzione. In pratica, la sequenza di attività aggiunge il valore della variabile di azione all'ambiente della sequenza di attività prima dell'esecuzione del passaggio della sequenza di attività. La sequenza di attività rimuove il valore dall'ambiente dopo l'esecuzione del passaggio.  

## <a name="action-variable-example"></a>Esempio di variabile di azione  
 Ad esempio, è possibile specificare una directory di avvio per un'azione della riga di comando usando il passaggio della sequenza di attività **Esegui riga di comando** . Questo passaggio include una proprietà **Da** il cui valore predefinito è archiviato nell'ambiente della sequenza di attività come variabile **WorkingDirectory** . La variabile di ambiente **WorkingDirectory** viene inizializzata prima dell'esecuzione dell'azione della sequenza di attività **Esegui riga di comando** . Durante il passaggio **Esegui riga di comando** , è possibile accedere al valore di **WorkingDirectory** tramite la proprietà **Da** . Dopo il completamento del passaggio, la sequenza di attività rimuove il valore della variabile **WorkingDirectory** dall'ambiente. Se la sequenza contiene un altro passaggio **Esegui riga di comando**, la sequenza di attività inizializza una nuova variabile **WorkingDirectory** e la imposta sul valore iniziale per il passaggio corrente.  

 Il valore *predefinito* per una variabile di azione della sequenza di attività è presente quando il passaggio della sequenza di attività viene eseguito. Se si imposta un *nuovo* valore, questo è disponibile per più passaggi della sequenza di attività. Se si usa uno dei metodi di creazione di variabili delle sequenze di attività per sostituire un valore di variabile predefinito, il nuovo valore rimane nell'ambiente e sostituisce il valore predefinito per gli altri passaggi nella sequenza di attività. Se ad esempio si aggiunge un passaggio **Imposta variabile della sequenza di attività** come primo passaggio della sequenza di attività, che imposta la variabile **WorkingDirectory** su **C:\\**, qualsiasi passaggio **Esegui riga di comando** nella sequenza di attività usa il nuovo valore della directory iniziale.  

## <a name="action-variables-for-task-sequence-actions"></a>Variabili di azione per le azioni delle sequenze di attività  
 Le variabili delle sequenze di attività di Configuration Manager sono raggruppate in base all'azione della sequenza di attività associata. Usare i collegamenti seguenti per raccogliere informazioni sulle variabili di azione associate a un'azione specifica. Le variabili della sequenza di attività regolano il funzionamento dell'azione di sequenziazione delle attività. L'azione di sequenziazione delle attività legge e utilizza le variabili contrassegnate come variabili di input. In alternativa, è possibile usare il passaggio [Imposta variabile di sequenziazione delle attività](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) o l'oggetto COM TSEnvironment per impostare le variabili in fase di esecuzione. Solo l'azione della sequenza di attività contrassegna le variabili come variabili di output. Le azioni eseguite in seguito nella sequenza di attività leggono queste variabili di output.  

> [!NOTE]  
>  Non tutte le azioni delle sequenze di attività sono associate a un set di variabili della sequenza di attività. Ad esempio, anche se ci sono variabili associate all'azione Attiva BitLocker, non ci sono variabili associate all'azione Disattiva BitLocker.  



###  <a name="BKMK_ApplyDataImage"></a> Applica immagine dei dati   
 Per altre informazioni, vedere [Applica immagine dei dati](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|Specifica il valore di indice dell'immagine che viene applicata al computer di destinazione.|  
|OSDWipeDestinationPartition<br /><br /> (input)|Specifica se eliminare i file contenuti nella partizione di destinazione.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Applica pacchetto di driver   
Per altre informazioni, vedere [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|Specifica l'ID contenuto del driver di dispositivo di archiviazione di massa da installare dal pacchetto di driver. Se questa variabile non viene specificata, non viene installato alcun driver di archiviazione di massa.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|Specifica il file INF del driver di archiviazione di massa da installare.<br /><br /> <br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|Specifica se è installato un driver del dispositivo di archiviazione di massa. La variabile deve essere **scsi**.<br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|Specifica l'ID critico per l'avvio del driver di dispositivo di archiviazione di massa da installare. Questo ID è elencato nella sezione **scsi** del file txtsetup.oem del driver del dispositivo.<br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifica se è necessario configurare Windows per consentire l'installazione di driver di dispositivo non firmati. Questa variabile della sequenza di attività non viene usata in caso di distribuzione di Windows Vista e sistemi operativi successivi.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Applica impostazioni di rete   
 Per altre informazioni, vedere [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|Questa variabile della sequenza di attività è una variabile di matrice. Ogni elemento della matrice rappresenta le impostazioni per una singola scheda di rete nel computer. Accedere alle impostazioni per ogni scheda combinando il nome della variabile di matrice con l'indice in base zero della scheda di rete e il nome della proprietà.<br /><br />Se questo passaggio configura più schede di rete, definisce le proprietà per la seconda scheda di rete usando l'indice nel nome della variabile. Ad esempio, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList e OSDAdapter1EnableWINS.<br /><br />Ad esempio, usare i nomi di variabile seguenti per definire le proprietà per configurare la prima scheda di rete per questo passaggio della sequenza di attività:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** abilita il protocollo DHCP (Dynamic Host Configuration Protocol) per la scheda.<br />    Questa impostazione è necessaria. I valori possibili sono: **True** o **False**.</li><li>**OSDAdapter0IPAddressList**: elenco di indirizzi IP delimitati da virgole per la scheda. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0SubnetMask**: elenco di subnet mask delimitate da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0Gateways**: elenco di indirizzi IP del gateway delimitati da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0DNSDomain**: dominio DNS (Domain Name System) per la scheda.</li><li>**OSDAdapter0DNSServerList**: elenco di server DNS delimitati da virgole per la scheda.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0EnableDNSRegistration**: **true** per registrare l'indirizzo IP per la scheda in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: **true** per registrare l'indirizzo IP per la scheda in DNS con il nome DNS completo per il computer.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **true** per abilitare il filtro del protocollo IP nella scheda.</li><li>**OSDAdapter0IPProtocolFilterList**: elenco di protocolli delimitati da virgole di cui è consentita l'esecuzione su IP. Questa proprietà viene ignorata se il valore di **EnableIPProtocolFiltering** è impostato su **false**.</li><li>**OSDAdapter0EnableTCPFiltering**: **true** per abilitare il filtro della porta TCP per la scheda.</li><li>**OSDAdapter0TCPFilterPortList**: elenco di porte delimitate da virgole a cui concedere le autorizzazioni di accesso per TCP. Questa proprietà viene ignorata se il valore di **EnableTCPFiltering** è impostato su **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: opzioni per NetBIOS su TCP/IP. I possibili valori sono i seguenti:<br /><br /> <ul><li>**0**: usa le impostazioni NetBIOS del server DHCP.</li><li>**1**: abilita NetBIOS su TCP/IP.</li><li>**2**: disabilita NetBIOS su TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS**: **true** per usare WINS per la risoluzione dei nomi.</li><li>**OSDAdapter0WINSServerList**: elenco di indirizzi IP del server WINS delimitati da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableWINS** non sia impostato su **true**.</li><li>**OSDAdapter0MacAddress**: indirizzo MAC usato per mettere in corrispondenza le impostazioni con la scheda di rete fisica.</li><li>**OSDAdapter0Name**: nome della connessione di rete visualizzato nel pannello di controllo delle connessioni di rete. Il nome è composto da un numero di caratteri compreso tra 0 e 255.</li><li>**OSDAdapter0Index**: indice delle impostazioni della scheda di rete nella matrice di impostazioni.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|Specifica il numero di schede di rete installate nel computer di destinazione. Quando il valore di **OSDAdapterCount** è impostato, è necessario impostare tutte le opzioni di configurazione per ogni scheda. Ad esempio, se si imposta il valore di **OSDAdapterTCPIPNetbiosOptions** per una scheda specifica, è necessario configurare anche tutti i valori per tale scheda.<br /><br />Se questo valore non è specificato, tutti i valori di **OSDAdapter** vengono ignorati.|  
|OSDDNSDomain<br /><br /> (input)|Specifica il server DNS primario usato dal computer di destinazione.|  
|OSDDomainName<br /><br /> (input)|Specifica il nome del dominio Windows a cui viene aggiunto il computer di destinazione. Il valore specificato deve essere un nome di dominio di Servizi di dominio Active Directory valido.|  
|OSDDomainOUName<br /><br /> (input)|Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo.<br /><br /> Esempio:<br /><br /> **LDAP://OU=UnitàOrganizzativa,DC=Dominio,DC=Società,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|Specifica se il filtro TCP/IP è abilitato.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDJoinAccount<br /><br /> (input)|Specifica l'account di rete usato per aggiungere il computer di destinazione a un dominio Windows.|  
|OSDJoinPassword<br /><br /> (input)|Specifica la password di rete usata per aggiungere il computer di destinazione a un dominio Windows.|  
|OSDNetworkJoinType<br /><br /> (input)|Specifica se il computer di destinazione viene aggiunto a un gruppo di lavoro o a un dominio Windows.<br /><br /> **0** indica che il computer di destinazione viene aggiunto a un dominio Windows. **1** specifica che il computer viene aggiunto un gruppo di lavoro.<br /><br /> Valori validi:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|Specifica l'ordine di ricerca DNS per il computer di destinazione.|  
|OSDWorkgroupName<br /><br /> (input)|Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione.<br /><br /> Specificare questo valore o il valore di **OSDDomainName**. Il nome del gruppo di lavoro può essere costituito da un massimo di 32 caratteri.<br /><br /> Esempio:<br /><br /> **Contabilità**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Applica immagine del sistema operativo   
 Per altre informazioni, vedere [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|Specifica il nome del file di risposte per la distribuzione del sistema operativo associato al pacchetto di distribuzione del sistema operativo.|  
|OSDImageIndex<br /><br /> (input)|Specifica il valore di indice dell'immagine del file WIM applicato al computer di destinazione.|  
|OSDInstallEditionIndex<br /><br /> (input)|Specifica la versione di Windows Vista o di un sistema operativo successivo installato. Se non viene specificata alcuna versione, Installazione di Windows determina la versione da installare usando il codice Product Key di riferimento.<br /><br /> Usare solo un valore zero (0) se sono vere le condizioni seguenti:<br /><br /> -   Si sta installando un sistema operativo precedente a Windows Vista<br />-   Si sta installando un'edizione con contratto multilicenza di Windows Vista o versione successiva senza specificare un codice Product Key.<br /><br /> Valori validi:<br /><br /> **0** (impostazione predefinita)|  
|OSDTargetSystemDrive (output)|Specifica la lettera di unità della partizione che contiene i file del sistema operativo.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Applica impostazioni Windows   
 Per altre informazioni, vedere [Applicare le impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|Specifica il nome del computer di destinazione.<br /><br /> Esempio:<br /><br /> **%_SMSTSMachineName%** (impostazione predefinita)|  
|OSDProductKey<br /><br /> (input)|Specifica il codice Product Key di Windows. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDRegisteredUserName<br /><br /> (input)|Specifica il nome predefinito dell'utente registrato nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDRegisteredOrgName<br /><br /> (input)|Specifica il nome predefinito dell'organizzazione registrata nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDTimeZone<br /><br /> (input)|Specifica l'impostazione predefinita del fuso orario usata nel nuovo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (input)|Specifica la modalità di licenza di Windows Server usata.<br /><br /> Valori validi:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|Specifica il numero massimo di connessioni consentito. Il numero specificato deve essere compreso tra 5 e 9999 connessioni.|  
|OSDRandomAdminPassword<br /><br /> (input)|Specifica una password generata in modo casuale per l'account amministratore nel nuovo sistema operativo. Se il valore è impostato su **true**, Installazione di Windows disabilita l'account amministratore locale nel computer di destinazione. Se è impostato su **false**, Installazione di Windows abilita l'account amministratore locale nel computer di destinazione e imposta la password dell'account sul valore di **OSDLocalAdminPassword**.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (input)|Specifica la password dell'amministratore locale. Se si abilita **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate**, il passaggio ignora questa variabile. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Applica automaticamente i driver   
 Per altre informazioni, vedere [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|Elenco delimitato da virgole di ID categoria univoci del catalogo driver. Il passaggio **Applica automaticamente i driver** considera solo i driver in almeno una delle categorie specificate. Questo valore è facoltativo e non prevede un'impostazione predefinita. Ottenere gli ID categoria disponibili enumerando l'elenco di oggetti **SMS_CategoryInstance** nel sito.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifica se Windows è configurato per consentire l'installazione di driver non firmati. Questa variabile della sequenza di attività non viene usata in caso di distribuzione di Windows Vista e di sistemi operativi successivi.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|Se nel catalogo driver ci sono più driver di dispositivo compatibili con un dispositivo hardware, questa variabile determina l'azione del passaggio. Se il valore è impostato su **true**, il passaggio installa solo il driver migliore. Se è **false**, il passaggio installa tutti i driver di dispositivo compatibili e Windows sceglie il driver migliore da usare.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende la connessione al server HTTP. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.|  
|SMSTSDriverRequestReceiveTimeOut|Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende una risposta. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **480** secondi.|
|SMSTSDriverRequestResolveTimeOut|Quando si richiede il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende la risoluzione dei nomi HTTP. Se la connessione richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.|
|SMSTSDriverRequestSendTimeOut|Quando si invia una richiesta per il catalogo driver, questa variabile indica per quanti secondi la sequenza di attività attende prima di inviare la richiesta. Se la richiesta richiede più tempo rispetto all'impostazione del timeout, la sequenza di attività annulla la richiesta. L'impostazione predefinita del timeout è di **60** secondi.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Acquisisci impostazioni di rete   
 Per altre informazioni, vedere [Acquisisci impostazioni di rete](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|Specifica se le informazioni di configurazione delle impostazioni della scheda di rete (TCP/IP, DNS e WINS) vengono acquisite.<br /><br /> Esempi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (input)|Specifica se viene eseguita la migrazione delle informazioni sull'appartenenza al gruppo di lavoro o al dominio come parte della distribuzione del sistema operativo.<br /><br /> Esempi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Acquisisci immagine del sistema operativo   
 Per altre informazioni, vedere [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (input)|Specifica un nome account di Windows con le autorizzazioni per l'archiviazione dell'immagine acquisita in una condivisione di rete.|  
|OSDCaptureAccountPassword<br /><br /> (input)|Specifica la password per l'account di Windows usato per archiviare l'immagine acquisita in una condivisione di rete.|  
|OSDCaptureDestination<br /><br /> (input)|Specifica il percorso in cui viene salvata l'immagine acquisita del sistema operativo. La lunghezza massima del nome directory è di 255 caratteri.|  
|OSDImageCreator<br /><br /> (input)|Nome facoltativo dell'utente che ha creato l'immagine. Questo nome viene archiviato nel file WIM. La lunghezza massima del nome utente è di 255 caratteri.|  
|OSDImageDescription<br /><br /> (input)|Descrizione facoltativa definita dall'utente dell'immagine acquisita del sistema operativo. Questa descrizione viene archiviata nel file WIM. La lunghezza massima della descrizione è di 255 caratteri.|  
|OSDImageVersion<br /><br /> (input)|Numero di versione facoltativo definito dall'utente da assegnare all'immagine acquisita del sistema operativo. Questo numero di versione viene archiviato nel file WIM. Questo valore può essere costituito da qualsiasi combinazione di lettere, con una lunghezza massima di 32 caratteri.|  
|OSDTargetSystemRoot<br /><br /> (input)|Specifica il percorso della directory di Windows del sistema operativo installato nel computer di riferimento. Questo sistema operativo viene verificato per stabilire che si tratti di un sistema operativo supportato per l'acquisizione da parte di Configuration Manager.|  



###  <a name="BKMK_CaptureUserState"></a> Acquisisci stato utente   
 Per altre informazioni, vedere [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|Nome di percorso locale o UNC della cartella in cui viene salvato lo stato utente. Non sono previsti valori predefiniti.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|Opzioni aggiuntive della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate dalla sequenza di attività per acquisire lo stato utente. Il passaggio non espone queste impostazioni nell'editor delle sequenze di attività. Specificare queste opzioni come stringa, che la sequenza di attività aggiunge alla riga di comando USMT generata automaticamente.<br /><br />Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.|  
|OSDMigrateMode<br /><br /> (input)|Consente di personalizzare i file acquisiti da USMT. Se questa variabile è impostata su **Simple**, la sequenza di attività usa solo i file di configurazione USMT standard. Se questa variabile è impostata su **Advanced**, la variabile della sequenza di attività OSDMigrateConfigFiles specifica i file di configurazione usati da USMT.<br /><br /> Valori validi:<br /><br /> **Simple**<br /><br /> **Advanced**|  
|OSDMigrateConfigFiles<br /><br /> (input)|Specifica i file di configurazione usati per controllare l'acquisizione dei profili utente. Questa variabile viene usata solo se il valore di OSDMigrateMode è impostato su Advanced. Questo valore di elenco delimitato da virgole è impostato per eseguire la migrazione personalizzata dei profili utente.<br /><br /> Esempio: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|Se USMT non riesce ad acquisire alcuni file, questa variabile consente all'acquisizione stato utente di continuare.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Consente la registrazione dettagliata per USMT.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|Specifica se i file crittografati vengono acquisiti.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|Specifica l'ID del pacchetto di Configuration Manager che contiene i file USMT. Questa variabile è obbligatoria.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Acquisisci impostazioni Windows   
 Per altre informazioni, vedere [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|Specifica se viene eseguita la migrazione del nome del computer.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**<br /><br /> Se il valore è **true**, la variabile OSDComputerName è impostata sul nome NetBIOS del computer.|  
|OSDComputerName<br /><br /> (output)|Valore impostato sul nome NetBIOS del computer. Il valore viene impostato solo se la variabile OSDMigrateComputerName è impostata su **true**.|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|Specifica se il passaggio esegue la migrazione delle informazioni sull'organizzazione e sugli utenti.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**<br /><br /> Se il valore è **true**, la variabile OSDRegisteredOrgName è impostata sul nome dell'organizzazione registrata del computer.|  
|OSDRegisteredOrgName<br /><br /> (output)|Valore impostato sul nome dell'organizzazione registrata del computer. Il valore viene impostato solo se la variabile OSDMigrateRegistrationInfo è impostata su **true**.|  
|OSDMigrateTimeZone<br /><br /> (input)|Specifica se viene eseguita la migrazione del fuso orario del computer.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**<br /><br /> Se il valore è **true**, la variabile OSDTimeZone è impostata sul fuso orario del computer.|  
|OSDTimeZone<br /><br /> (output)|Valore impostato sul fuso orario del computer. Il valore viene impostato solo se la variabile OSDMigrateTimeZone è impostata su **true**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Connetti alla cartella di rete   
 Per altre informazioni, vedere [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|Specifica l'account amministratore usato per connettersi alla condivisione di rete.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|Specifica la lettera di unità di rete a cui connettersi. Questo valore è facoltativo. Se non viene specificato, la connessione di rete non è mappata a una lettera di unità. Se questo valore è specificato, deve essere compreso nell'intervallo tra D: e Z:. Inoltre, non usare X:, perché è la lettera di unità usata da Windows PE durante la fase Windows PE.<br /><br /> Esempi:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|Specifica la password di rete usata per connettersi alla condivisione di rete.|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|Specifica il percorso di rete per la connessione.<br /><br /> Esempio:<br /><br /> **\\\nomeserver\nomecondivisione**|  



###  <a name="BKMK_EnableBitLocker"></a> Attiva BitLocker   
 Per altre informazioni, vedere [Abilitare BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|Invece di generare una password di ripristino casuale, l'azione della sequenza di attività **Attiva BitLocker** usa il valore specificato come password di ripristino. Il valore deve essere una password di ripristino di BitLocker numerica valida.|  
|OSDBitLockerStartupKey<br /><br /> (input)|Invece di generare una chiave di avvio casuale per l'opzione **Chiave di avvio solo su USB** per la gestione delle chiavi, il passaggio **Attiva BitLocker** usa il modulo TPM (Trusted Platform Module) come chiave di avvio. Il valore deve essere una chiave di avvio di BitLocker con codifica Base64 a 256 bit valida.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Formato e disco partizione   
 Per altre informazioni, vedere [Formato e partizione del disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|Specifica il numero del disco fisico da partizionare.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|Durante il partizionamento del disco rigido, per compatibilità con alcuni tipi di BIOS, questa variabile specifica se disabilitare le ottimizzazioni di allineamento della cache. Ciò è necessario quando si distribuiscono sistemi operativi Windows XP o Windows Server 2003. Per altre informazioni, vedere l' [articolo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e l' [articolo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) nella Microsoft Knowledge Base.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)| 
|OSDGPTBootDisk<br /><br /> (input)|Specifica se creare una partizione EFI su un disco rigido GPT. I computer basati su EFI usano questa partizione come disco di avvio.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDPartitions<br /><br /> (input)|Specifica una matrice di impostazioni di partizione. Vedere l'argomento relativo all'SDK per l'accesso alle variabili di matrice nell'ambiente della sequenza di attività.<br /><br /> Questa variabile della sequenza di attività è una variabile di matrice. Ogni elemento della matrice rappresenta le impostazioni per una singola partizione del disco rigido. Accedere alle impostazioni definite per ogni partizione combinando il nome della variabile di matrice con il numero in base zero della partizione del disco e il nome della proprietà.<br /><br /> Usare ad esempio i nomi di variabile seguenti per definire le proprietà per la prima partizione che viene creata da questo passaggio nel disco rigido:<br /><br /> - **OSDPartitions0Type**: specifica il tipo di partizione. Questa proprietà è obbligatoria. I valori validi sono **Primary**, **Extended**, **Logical** e **Hidden**.<br />-   **OSDPartitions0FileSystem**: specifica il tipo di file system da usare quando si formatta la partizione. Questa proprietà è facoltativa. Se non si specifica un file system, il passaggio non formatta la partizione. I valori validi sono **FAT32** e **NTFS**.<br />-   **OSDPartitions0Bootable**: specifica se la partizione è di avvio. Questa proprietà è obbligatoria. Se questo valore è impostato su **TRUE** per i dischi MBR, il passaggio contrassegna questa partizione come attiva.<br />-   **OSDPartitions0QuickFormat**: specifica il tipo di formato usato. Questa proprietà è obbligatoria. Se questo valore è impostato su **TRUE**, il passaggio esegue una formattazione rapida. In caso contrario, il passaggio esegue una formattazione completa.<br />-   **OSDPartitions0VolumeName**: specifica il nome assegnato al volume quando viene formattato. Questa proprietà è facoltativa.<br />-   **OSDPartitions0Size**: specifica le dimensioni della partizione. Le unità vengono specificate dalla variabile **OSDPartitions0SizeUnits** . Questa proprietà è facoltativa. Se questa proprietà non è specificata, la partizione viene creata usando tutto lo spazio disponibile rimanente.<br />-   **OSDPartitions0SizeUnits**: il passaggio usa queste unità per interpretare la variabile **OSDPartitions0Size**. Questa proprietà è facoltativa. I valori validi sono **MB** (predefinito), **GB** e **Percent**.<br />-   **OSDPartitions0VolumeLetterVariable**: quando questo passaggio crea le partizioni, usa sempre la lettera di unità disponibile successiva in Windows PE. Usare questa proprietà facoltativa per specificare il nome di un'altra variabile della sequenza di attività. Il passaggio usa questa variabile per salvare la nuova lettera di unità per riferimenti futuri.<br /><br />Se si definiscono più partizioni con questa azione della sequenza di attività, le proprietà per la seconda partizione vengono definite usando l'indice nel nome della variabile. Ad esempio: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** e **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (input)|Specifica lo stile di partizione da usare per il partizionamento del disco. **MBR** indica lo stile di partizione record di avvio principale e **GPT** indica lo stile tabella di partizione GUID.<br /><br /> Valori validi:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Installa applicazione   
 Per altre informazioni, vedere [Installa applicazione](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Specificare se il motore di esecuzione della sequenza di attività considera un avviso rilevato come errore durante questo passaggio. La sequenza di attività imposta la variabile _TSAppInstallStatus su **Avviso** quando una o più applicazioni o una dipendenza richiesta non viene installata perché non ha soddisfatto un requisito. Quando si imposta questa variabile su **True** e la sequenza di attività imposta _TSAppInstallStatus su Avviso, il risultato è un errore. Il comportamento predefinito è **False** .| 
|SMSTSMPListRequestTimeoutEnabled|Usare questa variabile per abilitare le richieste MPList ripetute per aggiornare il client se questo non si trova nella Intranet. <br />Per impostazione predefinita, questa variabile è impostata su **True**. Quando i client sono su Internet, è possibile impostare questa variabile su **False** per evitare inutili ritardi. Questa variabile è applicabile solo ai passaggi della sequenza di attività Installa applicazione e Installa aggiornamenti software.|  
|SMSTSMPListRequestTimeout|Specificare, in millisecondi, il tempo di attesa di una sequenza di attività prima che riprovi a installare un'applicazione in seguito all'impossibilità di recuperare l'elenco dei punti di gestione dai servizi di posizione. Per impostazione predefinita, la sequenza di attività attende **60000** millisecondi (60 secondi) prima di riprovare a eseguire il passaggio ed effettua fino a tre tentativi.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Installa aggiornamenti software   
Per altre informazioni, vedere [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|Specifica se installare tutti gli aggiornamenti o solo quelli obbligatori.<br /><br /> Valori validi:<br /><br /> **Tutti**<br /><br /> **Mandatory**|  
|SMSTSSoftwareUpdateScanTimeout| Controllare il timeout per l'analisi degli aggiornamenti software durante questo passaggio. Aumentare ad esempio il valore se si prevedono numerosi aggiornamenti durante l'analisi. Il valore predefinito è **1800** secondi (30 minuti). Il valore della variabile è impostato in secondi. |
|SMSTSWaitForSecondReboot|Questa variabile della sequenza di attività facoltativa controlla il comportamento del client quando l'installazione dell'aggiornamento software richiede due riavvii. Impostare questa variabile prima di questo passaggio per impedire che una sequenza di attività non riesca a causa di un secondo riavvio dall'installazione dell'aggiornamento software.<br /><br /> Impostare il valore SMSTSWaitForSecondReboot in secondi per specificare il tempo di sospensione della sequenza di attività in questo passaggio durante il riavvio del computer. Consentire il tempo necessario in caso di un secondo riavvio. <br />Ad esempio, se si imposta SMSTSWaitForSecondReboot su 600, la sequenza di attività viene sospesa per 10 minuti dopo il riavvio prima di eseguire i passaggi aggiuntivi. Questa variabile è utile quando un singolo passaggio della sequenza di attività Installa aggiornamenti software installa centinaia di aggiornamenti software.| 
|SMSTSMPListRequestTimeoutEnabled|Usare questa variabile per abilitare le richieste MPList ripetute per aggiornare il client se questo non si trova nella Intranet. <br />Per impostazione predefinita, questa variabile è impostata su **True**. Quando i client sono su Internet, è possibile impostare questa variabile su **False** per evitare inutili ritardi. Questa variabile è applicabile solo ai passaggi della sequenza di attività Installa applicazione e Installa aggiornamenti software.|  
|SMSTSMPListRequestTimeout|Specificare, in millisecondi, il tempo di attesa di una sequenza di attività prima che riprovi a installare un aggiornamento software in seguito all'impossibilità di recuperare l'elenco dei punti di gestione dai servizi di posizione. Per impostazione predefinita, la sequenza di attività attende **60000** millisecondi (60 secondi) prima di riprovare a eseguire il passaggio ed effettua fino a tre tentativi.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Aggiunta a dominio o gruppo di lavoro   
 Per altre informazioni, vedere [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|Specifica l'account usato dal computer di destinazione per l'aggiunta al dominio di Active Directory. Questa variabile è obbligatoria per l'aggiunta a un dominio.|  
|OSDJoinDomainName<br /><br /> (input)|Specifica il nome di un dominio di Active Directory a cui viene aggiunto il computer di destinazione. La lunghezza del nome di dominio deve essere compresa tra 1 e 255 caratteri.|  
|OSDJoinDomainOUName<br /><br /> (input)|Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo. La lunghezza del nome OU deve essere compresa tra 0 e 32.767 caratteri. Questo valore non è impostato se la variabile **OSDJoinType** è impostata su **1** (aggiunta a un gruppo di lavoro).<br /><br /> Esempio:<br /><br /> **LDAP://OU=UnitàOrganizzativa,DC=Dominio,DC=Società,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|Specifica la password di rete usata dal computer di destinazione per l'aggiunta al dominio di Active Directory. Se l'ambiente della sequenza di attività non include questa variabile, Installazione di Windows prova una password vuota. Se la variabile **OSDJoinType** è impostata su **0** (aggiunta a un dominio), questo valore è obbligatorio.|  
|OSDJoinSkipReboot<br /><br /> (input)|Specifica se ignorare il riavvio dopo l'aggiunta del computer di destinazione al dominio o al gruppo di lavoro.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (input)|Specifica se il computer di destinazione viene aggiunto a un gruppo di lavoro o a un dominio Windows. Per aggiungere il computer di destinazione a un dominio Windows, specificare **0**. Per aggiungere il computer di destinazione a un gruppo di lavoro, specificare **1**.<br /><br /> Valori validi:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (input)|Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione. La lunghezza del nome del gruppo di lavoro deve essere compresa tra 1 e 32 caratteri.<br /><br /> Esempio:<br /><br /> **Contabilità**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Prepara Windows per l'acquisizione   
 Per altre informazioni, vedere [Prepara Windows per l'acquisizione](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|Specifica se Sysprep crea un elenco di driver di dispositivo di archiviazione di massa. Questa impostazione si applica solo a Windows XP e Windows Server 2003. Questa variabile popola la sezione [SysprepMassStorage] di sysprep.inf con informazioni su tutti i driver di archiviazione di massa supportati dall'immagine da acquisire.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDKeepActivation<br /><br /> (input)|Specifica se Sysprep reimposta il flag di attivazione del prodotto.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDTargetSystemRoot<br /><br /> (output)|Specifica il percorso della directory di Windows del sistema operativo installato nel computer di riferimento. Questo sistema operativo viene verificato per stabilire che si tratti di un sistema operativo supportato per l'acquisizione da parte di Configuration Manager.|  



###  <a name="BKMK_ReleaseStateStore"></a> Rilascia archiviazione stati   
 Per altre informazioni, vedere [Rilascia archiviazione stati](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|UNC o nome percorso locale della posizione da cui viene ripristinato lo stato utente. Questo valore è usato sia dall'azione della sequenza di attività **Acquisisci stato utente** sia dall'azione della sequenza di attività **Ripristina stato utente** .|  



###  <a name="BKMK_RequestState"></a> Richiedi archiviazione stati   
  Per altre informazioni, vedere [Rilascia archiviazione stati](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|Quando l'account computer non riesce a connettersi al punto di migrazione stato, questa variabile specifica se la sequenza di attività esegue il fallback per usare l'account di accesso alla rete.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDStateSMPRetryCount<br /><br /> (input)|Specifica il numero di tentativi effettuati dal passaggio della sequenza di attività per trovare un punto di migrazione stato prima di restituire un esito negativo. Il numero specificato deve essere compreso tra 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (input)|Specifica il numero di secondi di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi. Il numero di secondi può essere composto da un massimo di 30 caratteri.|  
|OSDStateStorePath<br /><br /> (output)|Percorso UNC della cartella nel punto di migrazione stato in cui è archiviato lo stato utente.|  



###  <a name="BKMK_RestartComputer"></a> Riavvia computer   
 Per altre informazioni, vedere [Riavviare il computer](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|Specifica il messaggio da visualizzare agli utenti prima di riavviare il computer di destinazione. Se questa variabile non è impostata, viene visualizzato il testo del messaggio predefinito. Il messaggio specificato non deve superare i 512 caratteri.<br /><br /> Esempio:<br /><br /> **Salvare il lavoro prima del riavvio del computer.**|  
|SMSRebootTimeout<br /><br /> (input)|Specifica il numero di secondi durante i quali l'avviso viene visualizzato all'utente prima del riavvio del computer. Specificare zero secondi per indicare che non deve essere visualizzato alcun messaggio di riavvio.<br /><br /> Esempi:<br /><br /> **0** (impostazione predefinita)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Ripristina stato utente   
  Per altre informazioni, vedere [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|UNC o nome percorso locale della cartella da cui viene ripristinato lo stato utente.|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|Continuare il processo, anche se USMT non riesce a ripristinare alcuni file.<br /><br /> Valori validi:<br /><br /> **true** (impostazione predefinita)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Consente la registrazione dettagliata per lo strumento USMT. Questo valore è richiesto dall'azione.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDMigrateLocalAccounts<br /><br /> (input)|Specifica se l'account computer locale viene ripristinato.<br /><br /> Valori validi:<br /><br /> **true**<br /><br /> **false** (impostazione predefinita)|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|Se la variabile **OSDMigrateLocalAccounts** è "true", questa variabile deve contenere la password assegnata a tutti gli account locali di cui viene eseguita la migrazione. USMT assegna la stessa password a tutti gli account locali di cui viene eseguita la migrazione. Considerare questa password come temporanea e cambiarla in seguito con un altro metodo.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|Specifica le opzioni aggiuntive della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate quando si ripristina lo stato utente. Le opzioni aggiuntive vengono specificate in forma di stringa aggiunta alla riga di comando USMT generata automaticamente. Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|Specifica l'ID del pacchetto di Configuration Manager che contiene i file USMT. Questa variabile è obbligatoria.|  



###  <a name="BKMK_RunCommand"></a> Esegui riga di comando   
  Per altre informazioni, vedere [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|Per impostazione predefinita, in un sistema operativo a 64 bit la sequenza di attività individua ed esegue il programma nella riga di comando usando il redirector del file system WOW64. Questo comportamento consente al comando di trovare le versioni a 32 bit dei programmi e delle DLL del sistema operativo. L'impostazione di questa variabile su **true** disabilita l'uso del redirector del file system WOW64. Il comando trova le versioni a 64 bit native dei programmi e delle DLL del sistema operativo. Questa variabile non ha effetto quando l'esecuzione avviene in un sistema operativo a 32 bit.|  
|WorkingDirectory<br /><br /> (input)|Specifica la directory di avvio per un'azione della riga di comando. Il nome di directory specificato non deve superare i 255 caratteri.<br /><br /> Esempi:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|Specifica l'account da cui viene eseguita la riga di comando. Il valore è una stringa nel formato nomeutente o dominio\nome utente.|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|Specifica la password per l'account specificato dalla variabile SMSTSRunCommandLineUserName.|  



### <a name="set-dynamic-variables"></a>Imposta variabili dinamiche  
Per altre informazioni, vedere [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Specifica la marca del computer.|  
|_SMSTSModel|Specifica il modello del computer.|  
|_SMSTSMacAddresses|Specifica gli indirizzi MAC usati dal computer.|  
|_SMSTSIPAddresses|Specifica gli indirizzi IP usati dal computer.|  
|_SMSTSSerialNumber|Specifica il numero di serie del computer.|  
|_SMSTSAssetTag|Specifica il tag asset per il computer.|  
|_SMSTSUUID|Specifica l'UUID del computer.|  
|_SMSTSDefaultGateways|Specifica i gateway predefiniti usati dal computer.|  



###  <a name="BKMK_SetupWindows"></a> Imposta Windows e ConfigMgr   
  Per altre informazioni, vedere [Impostare Windows e Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|Specifica le proprietà di installazione del client usate per l'installazione del client di Configuration Manager.|  



### <a name="upgrade-operating-system"></a>Aggiorna sistema operativo  
 Per altre informazioni, vedere [Aggiorna sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|Specifica le opzioni aggiuntive della riga di comando che vengono aggiunte a Installazione di Windows durante un aggiornamento a Windows 10. La sequenza di attività non verifica le opzioni della riga di comando.<br /><br /> Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
