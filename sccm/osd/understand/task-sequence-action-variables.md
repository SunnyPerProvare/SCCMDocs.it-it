---
title: "Variabili di azione della sequenza di attività | Microsoft Docs"
description: "Usare le variabili di azione della sequenza, ad esempio le variabili di impostazione della rete, per specificare le impostazioni di configurazione per un singolo passaggio in una sequenza di attività di Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variabili di azione delle sequenze di attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le variabili di azione delle sequenze di attività specificano le impostazioni di configurazione usate da un singolo passaggio in una sequenza di attività di System Center Configuration Manager. Per impostazione predefinita, le impostazioni usate da un passaggio di una sequenza di attività vengono inizializzate prima che il passaggio venga eseguito e sono disponibili solo mentre il passaggio della sequenza di attività associato viene eseguito. In altre parole, l'impostazione della variabile della sequenza di attività viene aggiunta all'ambiente della sequenza di attività prima dell'esecuzione del passaggio della sequenza di attività e il valore viene rimosso dall'ambiente della sequenza di attività dopo l'esecuzione del passaggio.  

## <a name="action-variable-example"></a>Esempio di variabile di azione  
 Ad esempio, è possibile specificare una directory di avvio per un'azione della riga di comando usando il passaggio della sequenza di attività **Esegui riga di comando** . Questo passaggio include una proprietà **Da** il cui valore predefinito è archiviato nell'ambiente della sequenza di attività come variabile **WorkingDirectory** . La variabile di ambiente **WorkingDirectory** viene inizializzata prima dell'esecuzione dell'azione della sequenza di attività **Esegui riga di comando** . Durante il passaggio **Esegui riga di comando** , è possibile accedere al valore di **WorkingDirectory** tramite la proprietà **Da** . Quindi, dopo il completamento del passaggio della sequenza di attività, il valore della variabile **WorkingDirectory** viene rimosso dall'ambiente della sequenza di attività. Se la sequenza contiene un altro passaggio **Esegui riga di comando** , la nuova variabile **WorkingDirectory** viene inizializzata e impostata sul valore iniziale per tale passaggio della sequenza di attività.  

 Mentre il valore predefinito per un'impostazione di un'azione della sequenza di attività è presente mentre viene eseguito il passaggio della sequenza di attività, qualsiasi nuovo valore impostato può essere usato da più passaggi nella sequenza. Se si usa uno dei metodi di creazione di variabili delle sequenze di attività per sostituire un valore di variabile predefinito, il nuovo valore rimane nell'ambiente e sostituisce il valore predefinito per gli altri passaggi nella sequenza di attività. Nell'esempio precedente, se viene aggiunto un passaggio **Imposta variabile della sequenza di attività** come primo passaggio della sequenza di attività e la variabile di ambiente **WorkingDirectory** viene impostata sul valore **C:\\**, i due passaggi **Esegui riga di comando** nella sequenza di attività useranno il nuovo valore della directory iniziale.  

## <a name="action-variables-for-task-sequence-actions"></a>Variabili di azione per le azioni delle sequenze di attività  
 Le variabili delle sequenze di attività di Configuration Manager sono raggruppate in base all'azione della sequenza di attività associata. Usare i collegamenti seguenti per raccogliere informazioni sulle variabili di azione associate a un'azione specifica. Le variabili della sequenza di attività regolano il funzionamento dell'azione di sequenziazione delle attività. L'azione di sequenziazione delle attività legge e utilizza le variabili contrassegnate come variabili di input. In alternativa, è possibile utilizzare l'azione Imposta variabile di sequenziazione delle attività o l'oggetto COM TSEnvironment per impostare le variabili al runtime. Solo l'azione di sequenziazione delle attività contrassegna le variabili come variabili di output, che vengono lette dalle azioni che si verificano successivamente nella sequenza delle attività.  

> [!NOTE]  
>  Non tutte le azioni delle sequenze di attività sono associate a un set di variabili della sequenza di attività. Ad esempio, anche se ci sono variabili associate all'azione Attiva BitLocker, non ci sono variabili associate all'azione Disattiva BitLocker.  

###  <a name="BKMK_ApplyDataImage"></a> Variabili di azione della sequenza di attività Applica immagine dei dati  
 Le variabili per questa azione specificano quale immagine di un file WIM viene applicata al computer di destinazione e se eliminare i file nella partizione di destinazione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Passaggio Applica immagine dei dati della sequenza di attività](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|Specifica il valore di indice dell'immagine che viene applicata al computer di destinazione.|  
|OSDWipeDestinationPartition<br /><br /> (input)|Specifica se eliminare i file contenuti nella partizione di destinazione.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  

###  <a name="BKMK_ApplyDriverPackage"></a> Variabili di azione della sequenza di attività Applica pacchetto di driver  
 Le variabili per questa azione specificano le informazioni di installazione di driver di archiviazione di massa e se installare driver senza firma. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Applica pacchetto di driver](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|Specifica l'ID contenuto del driver di dispositivo di archiviazione di massa da installare dal pacchetto di driver. Se non viene specificato un valore, non viene installato alcun driver di archiviazione di massa.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|Specifica il file INF del driver di archiviazione di massa da installare.<br /><br /> <br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|Specifica se è installato un driver del dispositivo di archiviazione di massa. Il valore deve essere **scsi**.<br /><br /> <br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|Specifica l'ID critico per l'avvio del driver di dispositivo di archiviazione di massa da installare. Questo ID è elencato nella sezione "**scsi**" del file txtsetup.oem del driver del dispositivo.<br /><br /> <br /><br /> Questa variabile della sequenza di attività è obbligatoria se si imposta OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifica se è necessario configurare Windows per consentire l'installazione di driver di dispositivo non firmati. Questa variabile della sequenza di attività non viene usata in caso di distribuzione di Windows Vista e sistemi operativi successivi.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> Variabili di azione della sequenza di attività Applica impostazioni di rete  
 Le variabili per questa azione specificano le impostazioni di rete per il computer di destinazione, ad esempio le impostazioni per le schede di rete del computer, le impostazioni di dominio e le impostazioni del gruppo di lavoro. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Passaggio Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|Questa variabile della sequenza di attività è una variabile di matrice. Ogni elemento della matrice rappresenta le impostazioni per una singola scheda di rete nel computer. Le impostazioni definite per ogni scheda sono accessibili combinando il nome della variabile di matrice con l'indice in base zero della scheda di rete e il nome della proprietà.<br /><br /> <br /><br /> Se con questa azione della sequenza di attività verranno configurate più schede di rete, le proprietà per la seconda scheda di rete vengono definite usando il relativo indice nel nome della variabile, ad esempio OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS e così via.<br /><br /> <br /><br /> Ad esempio, i nomi di variabile seguenti possono essere usati per definire le proprietà per la prima scheda di rete che verrà configurata da questa azione della sequenza di attività:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: true per abilitare il protocollo DHCP (Dynamic Host Configuration Protocol) per la scheda.<br />    Questa impostazione è necessaria. I valori possibili sono True o False.</li><li>**OSDAdapter0IPAddressList**: elenco di indirizzi IP delimitato da virgole per la scheda. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0SubnetMask**: elenco di subnet mask delimitato da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0Gateways**: elenco di indirizzi IP del gateway delimitato da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableDHCP** non sia impostato su **false**.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0DNSDomain** : dominio DNS (Domain Name System) per la scheda.</li><li>**OSDAdapter0DNSServerList**: elenco di server DNS delimitato da virgole per la scheda.<br />    Questa impostazione è necessaria.</li><li>**OSDAdapter0EnableDNSRegistration** - **true** per registrare l'indirizzo IP per la scheda in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** per registrare l'indirizzo IP per la scheda in DNS con il nome DNS completo per il computer.</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true** per abilitare il filtro del protocollo IP nella scheda.</li><li>**OSDAdapter0IPProtocolFilterList**: elenco di protocolli delimitato da virgole di cui è consentita l'esecuzione su IP. Questa proprietà viene ignorata se il valore di **EnableIPProtocolFiltering** è impostato su **false**.</li><li>**OSDAdapter0EnableTCPFiltering** - **true** per abilitare il filtro della porta TCP per la scheda.</li><li>**OSDAdapter0TCPFilterPortList**: elenco di porte delimitato da virgole a cui concedere le autorizzazioni di accesso per TCP. Questa proprietà viene ignorata se il valore di **EnableTCPFiltering** è impostato su **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: opzioni per NetBIOS su TCP/IP. I possibili valori sono i seguenti:<br /><br /> <ul><li>0 Usa le impostazioni NetBIOS del server DHCP.</li><li>1 Abilita NetBIOS su TCP/IP.</li><li>2 Disabilita NetBIOS su TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** per usare WINS per la risoluzione dei nomi.</li><li>**OSDAdapter0WINSServerList**: elenco di indirizzi IP del server WINS delimitato da virgole. Questa proprietà viene ignorata a meno che il valore di **EnableWINS** non sia impostato su **true**.</li><li>**OSDAdapter0MacAddress**: indirizzo MAC usato per mettere in corrispondenza le impostazioni con la scheda di rete fisica.</li><li>**OSDAdapter0Name**: nome della connessione di rete visualizzato nel pannello di controllo delle connessioni di rete. Il nome è composto da un numero di caratteri compreso tra 0 e 255.</li><li>**OSDAdapter0Index**: indice delle impostazioni della scheda di rete nella matrice di impostazioni.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|Specifica il numero di schede di rete installate nel computer di destinazione. Quando il valore di **OSDAdapterCount** è impostato, è necessario impostare tutte le opzioni di configurazione per ogni scheda. Ad esempio, se si imposta il valore di **OSDAdapterTCPIPNetbiosOptions** per una scheda specifica, è necessario configurare anche tutti i valori per tale scheda.<br /><br /> <br /><br /> Se questo valore non è specificato, tutti i valori di **OSDAdapter** vengono ignorati.|  
|OSDDNSDomain<br /><br /> (input)|Specifica il server DNS primario usato dal computer di destinazione.|  
|OSDDomainName<br /><br /> (input)|Specifica il nome del dominio Windows a cui viene aggiunto il computer di destinazione. Il valore specificato deve essere un nome di dominio di Servizi di dominio Active Directory valido.|  
|OSDDomainOUName<br /><br /> (input)|Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo.<br /><br /> Esempio:<br /><br /> **LDAP://OU=UnitàOrganizzativa,DC=Dominio,DC=Società,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|Specifica se il filtro TCP/IP è abilitato.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDJoinAccount<br /><br /> (input)|Specifica l'account di rete usato per aggiungere il computer di destinazione a un dominio Windows.|  
|OSDJoinPassword<br /><br /> (input)|Specifica la password di rete usata per aggiungere il computer di destinazione a un dominio Windows.|  
|OSDNetworkJoinType<br /><br /> (input)|Specifica se il computer di destinazione viene aggiunto a un gruppo di lavoro o a un dominio Windows.<br /><br /> **"0"** indica che il computer di destinazione viene aggiunto a un dominio Windows. **"1"** specifica che il computer viene aggiunto un gruppo di lavoro.<br /><br /> Valori validi:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|Specifica l'ordine di ricerca DNS per il computer di destinazione.|  
|OSDWorkgroupName<br /><br /> (input)|Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione.<br /><br /> È necessario specificare questo valore o il valore di **OSDDomainName** . Il nome del gruppo di lavoro può essere costituito da un massimo di 32 caratteri.<br /><br /> Esempio:<br /><br /> **"Contabilità"**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> Variabili di azione della sequenza di attività Applica immagine del sistema operativo  
 Le variabili per questa azione specificano le impostazioni per il sistema operativo che si vuole installare nel computer di destinazione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Applica immagine del sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|Specifica il nome del file di risposte per la distribuzione del sistema operativo associato al pacchetto di distribuzione del sistema operativo.|  
|OSDImageIndex<br /><br /> (input)|Specifica il valore di indice dell'immagine del file WIM applicato al computer di destinazione.|  
|OSDInstallEditionIndex<br /><br /> (input)|Specifica la versione di Windows Vista o di un sistema operativo successivo installato. Se non viene specificata alcuna versione, il programma di installazione di Windows determina la versione da installare usando il codice Product Key di riferimento.<br /><br /> Usare solo un valore zero (0) se sono vere le condizioni seguenti:<br /><br /> -   Si sta installando un sistema operativo precedente a Windows Vista<br />-   Si sta installando un'edizione con contratto multilicenza di Windows Vista o versione successiva senza specificare un codice Product Key.<br /><br /> Valori validi:<br /><br /> **"0"** (impostazione predefinita)|  
|OSDTargetSystemDrive (output)|Specifica la lettera di unità della partizione che contiene i file del sistema operativo.|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Variabili di azione della sequenza di attività Applica impostazioni Windows  
 Le variabili per questa azione specificano le impostazioni di Windows per il computer di destinazione, ad esempio il nome del computer, il codice Product Key di Windows, l'utente e l'organizzazione registrati e la password dell'amministratore locale. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Applica impostazioni Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|Specifica il nome del computer di destinazione.<br /><br /> Esempio:<br /><br /> **"%_SMSTSMachineName%"** (valore predefinito)|  
|OSDProductKey<br /><br /> (input)|Specifica il codice Product Key di Windows. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDRegisteredUserName<br /><br /> (input)|Specifica il nome predefinito dell'utente registrato nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDRegisteredOrgName<br /><br /> (input)|Specifica il nome predefinito dell'organizzazione registrata nel nuovo sistema operativo. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  
|OSDTimeZone<br /><br /> (input)|Specifica l'impostazione predefinita del fuso orario usata nel nuovo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (input)|Specifica la modalità di licenza di Windows Server usata.<br /><br /> Valori validi:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|Specifica il numero massimo di connessioni consentito. Il numero specificato deve essere compreso tra 5 e 9999 connessioni.|  
|OSDRandomAdminPassword<br /><br /> (input)|Specifica una password generata in modo casuale per l'account amministratore nel nuovo sistema operativo. Se il valore è impostato su **true**, l'account amministratore locale sarà disabilitato nel computer di destinazione. Se il valore è impostato su **false**, l'account amministratore locale sarà abilitato nel computer di destinazione e alla password di tale account verrà assegnato il valore della variabile **OSDLocalAdminPassword**.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  
|OSDLocalAdminPassword<br /><br /> (input)|Specifica la password dell'amministratore locale. Questo valore viene ignorato se l'opzione **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate** è abilitata. Il valore specificato deve essere compreso tra 1 e 255 caratteri.|  

###  <a name="BKMK_AutoApplyDrivers"></a> Variabili di azione della sequenza di attività Applica automaticamente i driver  
 Le variabili per questa azione specificano i driver di Windows che vengono installati nel computer di destinazione e se i driver non firmati vengono installati. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Applica automaticamente i driver](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|Elenco delimitato da virgole di ID categoria univoci del catalogo driver. Se il valore viene specificato, l'azione della sequenza di attività **Applica automaticamente i driver** considera solo i driver presenti in almeno una di queste categorie durante l'installazione dei driver. Questo valore è facoltativo e non prevede un'impostazione predefinita. Gli ID categoria disponibili possono essere ottenuti enumerando l'elenco di oggetti **SMS_CategoryInstance** nel sito.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifica se Windows è configurato per consentire l'installazione di driver non firmati. Questa variabile della sequenza di attività non viene usata in caso di distribuzione di Windows Vista e di sistemi operativi successivi.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|Specifica cosa fa l'azione della sequenza di attività se nel catalogo driver ci sono più driver di dispositivo compatibili con un dispositivo hardware. Se il valore è impostato su **true**, verrà installato solo il driver migliore.  Se il valore è impostato su **false**, verranno installati tutti i driver di dispositivo compatibili e il sistema operativo sceglierà il driver migliore da usare.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> Variabili di azione della sequenza di attività Acquisisci impostazioni di rete  
 Le variabili per questa azione di specificano se le informazioni di configurazione delle impostazioni della scheda di rete (TCP/IP, DNS e WINS) vengono acquisite e se viene eseguita la migrazione delle informazioni sull'appartenenza al gruppo di lavoro o al dominio come parte della distribuzione del sistema operativo. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Acquisisci impostazioni di rete](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|Specifica se le informazioni di configurazione delle impostazioni della scheda di rete (TCP/IP, DNS e WINS) vengono acquisite.<br /><br /> Esempi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  
|OSDMigrateNetworkMembership<br /><br /> (input)|Specifica se viene eseguita la migrazione delle informazioni sull'appartenenza al gruppo di lavoro o al dominio come parte della distribuzione del sistema operativo.<br /><br /> Esempi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> Variabili di azione della sequenza di attività Acquisisci immagine del sistema operativo  
 Le variabili per questa azione specificano informazioni sull'immagine del sistema operativo che viene acquisita, ad esempio dove viene archiviata l'immagine, chi l'ha creata e una descrizione dell'immagine. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Acquisisci immagine del sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

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

###  <a name="BKMK_CaptureUserState"></a> Variabili di azione della sequenza di attività Acquisisci stato utente  
 Le variabili per questa azione specificano le informazioni usate dall'Utilità di migrazione stato utente (USMT, User State Migration Tool), ad esempio la cartella in cui viene salvato lo stato utente, le opzioni della riga di comando per USMT e i file di configurazione usati per controllare l'acquisizione dei profili utente.  Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Acquisisci stato utente](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|Nome di percorso locale o UNC della cartella in cui viene salvato lo stato utente. Non sono previsti valori predefiniti.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|Specifica le opzioni della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate quando si acquisisce lo stato utente, ma che non sono esposte nell'interfaccia utente di Configuration Manager. Le opzioni aggiuntive vengono specificate in forma di stringa aggiunta alla riga di comando USMT generata automaticamente.<br /><br /> <br /><br /> Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.|  
|OSDMigrateMode<br /><br /> (input)|Consente di personalizzare i file acquisiti da USMT. Se questa variabile è impostata su "Simple", vengono usati solo i file di configurazione USMT standard. Se questa variabile è impostata su "Advanced", la variabile della sequenza di attività OSDMigrateConfigFiles specifica i file di configurazione usati da USMT.<br /><br /> Valori validi:<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (input)|Specifica i file di configurazione usati per controllare l'acquisizione dei profili utente. Questa variabile viene usata solo se il valore di OSDMigrateMode è impostato su "Advanced". Questo valore di elenco delimitato da virgole è impostato per eseguire la migrazione personalizzata dei profili utente.<br /><br /> Esempio: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|Consente il proseguimento dell'acquisizione dello stato utente anche se non è possibile acquisire alcuni file.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Consente la registrazione dettagliata per USMT.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|Specifica se i file crittografati vengono acquisiti.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|Specifica l'ID del pacchetto di Configuration Manager che conterrà i file USMT. Questa variabile è obbligatoria.|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Variabili di azione della sequenza di attività Acquisisci impostazioni Windows  
 Le variabili per questa azione specificano se viene eseguita la migrazione nel computer di destinazione di impostazioni di Windows specifiche, ad esempio il nome del computer, il nome dell'organizzazione registrata e le informazioni sul fuso orario. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Acquisisci impostazioni Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|Specifica se viene eseguita la migrazione del nome del computer.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**<br /><br /> Se il valore è "true", la variabile OSDComputerName è impostata sul nome NetBIOS del computer.|  
|OSDComputerName<br /><br /> (output)|Valore impostato sul nome NetBIOS del computer. Il valore viene impostato solo se la variabile OSDMigrateComputerName è impostata su "true".|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|Specifica se viene eseguita la migrazione delle informazioni sull'organizzazione e sugli utenti del computer.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**<br /><br /> Se il valore è "true", la variabile OSDRegisteredOrgName è impostata sul nome dell'organizzazione registrata del computer.|  
|OSDRegisteredOrgName<br /><br /> (output)|Valore impostato sul nome dell'organizzazione registrata del computer. Il valore viene impostato solo se la variabile OSDMigrateRegistrationInfo è impostata su "true".|  
|OSDMigrateTimeZone<br /><br /> (input)|Specifica se viene eseguita la migrazione del fuso orario del computer.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**<br /><br /> Se il valore è "true", la variabile OSDTimeZone è impostata sul fuso orario del computer.|  
|OSDTimeZone<br /><br /> (output)|Valore impostato sul fuso orario del computer. Il valore viene impostato solo se la variabile OSDMigrateTimeZone è impostata su "true".|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> Variabili di azione della sequenza di attività Connetti alla cartella di rete  
 Le variabili per questa azione specificano le informazioni relative a una cartella in una rete, ad esempio l'account, con la relativa password, usato per connettersi alla cartella di rete, la lettera di unità della cartella e il percorso della cartella. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Connetti alla cartella di rete](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|Specifica l'account amministratore usato per connettersi alla condivisione di rete.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|Specifica la lettera di unità di rete a cui connettersi. Questo valore è facoltativo. Se non viene specificato, la connessione di rete non è mappata a una lettera di unità. Se questo valore è specificato, deve essere compreso nell'intervallo tra D: e Z:.  Inoltre, non usare X:, perché è la lettera di unità usata da Windows PE durante la fase Windows PE.<br /><br /> Esempi:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|Specifica la password di rete usata per connettersi alla condivisione di rete.|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|Specifica il percorso di rete per la connessione.<br /><br /> Esempio:<br /><br /> **"\\\servername\sharename"**|  

###  <a name="BKMK_ConvertDisk"></a> Variabili di azione della sequenza di attività Converti il disco selezionato in disco dinamico  
 La variabile per questa azione specifica il numero del disco fisico da convertire da disco di base in disco dinamico. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Converti il disco selezionato in disco dinamico](task-sequence-steps.md#BKMK_ConvertDisktoDynamic).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (input)|Specifica il numero del disco fisico che viene convertito.|  

###  <a name="BKMK_EnableBitLocker"></a> Variabili di azione della sequenza di attività Attiva BitLocker  
 Le variabili per questa azione specificano le opzioni relative a password di ripristino e chiave di avvio usate per abilitare BitLocker nel computer di destinazione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Attiva BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|Invece di generare una password di ripristino casuale, l'azione della sequenza di attività **Attiva BitLocker** usa il valore specificato come password di ripristino. Il valore deve essere una password di ripristino di BitLocker numerica valida.|  
|OSDBitLockerStartupKey<br /><br /> (input)|Invece di generare una chiave di avvio casuale per l'opzione **Chiave di avvio solo su USB** per la gestione delle chiavi, l'azione della sequenza di attività **Attiva BitLocker** usa il modulo TPM (Trusted Platform Module) come chiave di avvio. Il valore deve essere una chiave di avvio di BitLocker con codifica Base64 a 256 bit valida.|  

###  <a name="BKMK_FormatPartitionDisk"></a> Variabili di azione della sequenza di attività Formato e disco partizione  
 Le variabili per questa azione specificano le informazioni di formattazione e partizionamento di un disco fisico, ad esempio il numero di disco e una matrice di impostazioni di partizione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|Specifica il numero del disco fisico da partizionare.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|Specifica se disabilitare le ottimizzazioni di allineamento della cache durante il partizionamento del disco rigido, per compatibilità con alcuni tipi di BIOS Ciò può essere necessario quando si distribuiscono sistemi operativi Windows XP o Windows Server 2003. Per altre informazioni, vedere l' [articolo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) e l' [articolo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) nella Microsoft Knowledge Base.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDGPTBootDisk<br /><br /> (input)|Specifica se creare una partizione EFI in un disco rigido GPT, per poterlo usare come disco di avvio nei computer basati su EFI.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDPartitions<br /><br /> (input)|Specifica una matrice di impostazioni di partizione. Vedere l'argomento relativo all'SDK per l'accesso alle variabili di matrice nell'ambiente della sequenza di attività.<br /><br /> Questa variabile della sequenza di attività è una variabile di matrice. Ogni elemento della matrice rappresenta le impostazioni per una singola partizione del disco rigido. Le impostazioni definite per ogni partizione sono accessibili combinando il nome della variabile di matrice con il numero in base zero della partizione del disco e il nome della proprietà.<br /><br /> Ad esempio, i nomi di variabile seguenti possono essere usati per definire le proprietà per la prima partizione che verrà creata da questa azione della sequenza di attività nel disco rigido:<br /><br /> - **OSDPartitions0Type**: specifica il tipo di partizione. Questa è una proprietà obbligatoria. I valori validi sono "**Primary**", "**Extended**", "**Logical**" e "**Hidden**".<br />-   **OSDPartitions0FileSystem** : specifica il tipo di file system da usare quando si formatta la partizione. Questa è una proprietà facoltativa. Se non viene specificato un file system, la partizione non verrà formattata. I valori validi sono "**FAT32**" e "**NTFS**".<br />-   **OSDPartitions0Bootable** : specifica se la partizione è di avvio. Questa è una proprietà obbligatoria. Se questo valore è impostato su "**TRUE**" per i dischi MBR, la partizione verrà impostata come attiva.<br />-   **OSDPartitions0QuickFormat** : specifica il tipo di formato usato. Questa è una proprietà obbligatoria. Se questo valore è impostato su "**TRUE**", verrà eseguita una formattazione veloce; in caso contrario, verrà eseguita una formattazione completa.<br />-   **OSDPartitions0VolumeName** : specifica il nome assegnato al volume quando viene formattato. Questa è una proprietà facoltativa.<br />-   **OSDPartitions0Size** : specifica le dimensioni della partizione. Le unità vengono specificate dalla variabile **OSDPartitions0SizeUnits** . Questa è una proprietà facoltativa. Se questa proprietà non è specificata, la partizione viene creata usando tutto lo spazio disponibile rimanente.<br />-   **OSDPartitions0SizeUnits** : specifica le unità che verranno usate per interpretare la variabile della sequenza di attività **OSDPartitions0Size** . Questa è una proprietà facoltativa. I valori validi sono "**MB**" (predefinito), "**GB**" e "**Percent**".<br />-   **OSDPartitions0VolumeLetterVariable** : le partizioni useranno sempre la lettera di unità disponibile successiva in Windows PE quando vengono create. Usare questa proprietà facoltativa per specificare il nome di un'altra variabile della sequenza di attività, che verrà usata per salvare la nuova lettera di unità per riferimento futuro.<br /><br /> <br /><br /> Se con questa azione della sequenza di attività verranno definite più partizioni, è possibile definire le proprietà per la seconda partizione usando il relativo indice nel nome della variabile. Ad esempio, **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName** e così via.|  
|OSDPartitionStyle<br /><br /> (input)|Specifica lo stile di partizione da usare per il partizionamento del disco. "**MBR**" indica lo stile di partizione record di avvio principale e "**GPT**" indica lo stile tabella di partizione GUID.<br /><br /> Valori validi:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> Variabili di azione della sequenza di attività Installa aggiornamenti software  
 La variabile per questa azione specifica se installare tutti gli aggiornamenti o solo quelli obbligatori. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Installa aggiornamenti software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|Specifica se installare tutti gli aggiornamenti o solo quelli obbligatori.<br /><br /> Valori validi:<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> Variabili di azione della sequenza di attività Aggiunta a dominio o gruppo di lavoro  
 Le variabili per questa azione specificano le informazioni necessarie per aggiungere il computer di destinazione a un gruppo di lavoro o un dominio Windows. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Aggiunta a dominio o gruppo di lavoro](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|Specifica l'account usato dal computer di destinazione per l'aggiunta al dominio Windows. Questa variabile è obbligatoria per l'aggiunta a un dominio.|  
|OSDJoinDomainName<br /><br /> (input)|Specifica il nome di un dominio Windows a cui viene aggiunto il computer di destinazione. La lunghezza del nome di dominio Windows deve essere compresa tra 1 e 255 caratteri.|  
|OSDJoinDomainOUName<br /><br /> (input)|Specifica il nome in formato RFC 1779 dell'unità organizzativa (OU) a cui viene aggiunto il computer di destinazione. Se specificato, il valore deve contenere il percorso completo. La lunghezza del nome dell'unità organizzativa di dominio Windows deve essere compresa tra 0 e 32.767 caratteri. Questo valore non è impostato se la variabile **OSDJoinType** è impostata su "1" (aggiunta a un gruppo di lavoro).<br /><br /> Esempio:<br /><br /> **LDAP://OU=UnitàOrganizzativa,DC=Dominio,DC=Società,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|Specifica la password di rete usata dal computer di destinazione per l'aggiunta al dominio Windows. Se la variabile non viene specificata, viene eseguito un tentativo di usare una password vuota. Questo valore è obbligatorio se la variabile **OSDJoinType** è impostata su "**0**" (aggiunta a un dominio).|  
|OSDJoinSkipReboot<br /><br /> (input)|Specifica se ignorare il riavvio dopo l'aggiunta del computer di destinazione al dominio o al gruppo di lavoro.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"**|  
|OSDJoinType<br /><br /> (input)|Specifica se il computer di destinazione viene aggiunto a un gruppo di lavoro o a un dominio Windows. Per aggiungere il computer di destinazione a un dominio Windows, specificare "**0**". Per aggiungere il computer di destinazione a un gruppo di lavoro, specificare "**1**".<br /><br /> Valori validi:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDJoinWorkgroupName<br /><br /> (input)|Specifica il nome del gruppo di lavoro a cui viene aggiunto il computer di destinazione. La lunghezza del nome del gruppo di lavoro deve essere compresa tra 1 e 32 caratteri.<br /><br /> Esempio:<br /><br /> **"Contabilità"**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Variabili di azione della sequenza di attività Prepara Windows per l'acquisizione  
 Le variabili per questa azione specificano le informazioni usate per acquisire il sistema operativo Windows dal computer di destinazione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Prepara Windows per l'acquisizione](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|Specifica se Sysprep crea un elenco di driver di dispositivi di archiviazione di massa. Questa impostazione si applica solo a Windows XP e Windows Server 2003. Popola la sezione [SysprepMassStorage] di sysprep.inf con informazioni su tutti i driver di archiviazione di massa supportati dall'immagine da acquisire.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDKeepActivation<br /><br /> (input)|Specifica se Sysprep reimposta il flag di attivazione del prodotto.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDTargetSystemRoot<br /><br /> (output)|Specifica il percorso della directory di Windows del sistema operativo installato nel computer di riferimento. Questo sistema operativo viene verificato per stabilire che si tratti di un sistema operativo supportato per l'acquisizione da parte di Configuration Manager.|  

###  <a name="BKMK_ReleaseStateStore"></a> Variabili di azione della sequenza Rilascia archiviazione stati  
 Le variabili per questa azione specificano le informazioni usate per rilasciare lo stato utente archiviato. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Rilascia archiviazione stati](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|UNC o nome percorso locale della posizione da cui viene ripristinato lo stato utente. Questo valore è usato sia dall'azione della sequenza di attività **Acquisisci stato utente** sia dall'azione della sequenza di attività **Ripristina stato utente** .|  

###  <a name="BKMK_RequestState"></a> Variabili di azione della sequenza di attività Richiedi archiviazione stati  
 Le variabili per questa azione specificano le informazioni usate per richiedere lo stato utente archiviato, ad esempio la cartella nel punto di migrazione stato dove sono archiviati i dati utente. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Richiedi archiviazione stati](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|Specifica se l'account di accesso alla rete viene usato come fallback quando l'account computer non riesce a connettersi al punto di migrazione stato.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDStateSMPRetryCount<br /><br /> (input)|Specifica il numero di tentativi effettuati dal passaggio della sequenza di attività per trovare un punto di migrazione stato prima di restituire un esito negativo. Il numero specificato deve essere compreso tra 0 e 600.|  
|OSDStateSMPRetryTime<br /><br /> (input)|Specifica il numero di secondi di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi. Il numero di secondi può essere composto da un massimo di 30 caratteri.|  
|OSDStateStorePath<br /><br /> (output)|Percorso UNC della cartella nel punto di migrazione stato in cui è archiviato lo stato utente.|  

###  <a name="BKMK_RestartComputer"></a> Variabili di azione della sequenza di attività Riavvia computer  
 Le variabili per questa azione specificano le informazioni usate per riavviare il computer di destinazione. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Riavvia computer](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|Specifica il messaggio da visualizzare agli utenti prima di riavviare il computer di destinazione. Se questa variabile non è impostata, viene visualizzato il testo del messaggio predefinito. Il messaggio specificato non deve superare i 512 caratteri.<br /><br /> Esempio:<br /><br /> -   "Il computer verrà riavviato. Salvare il lavoro."|  
|SMSRebootTimeout<br /><br /> (input)|Specifica il numero di secondi durante i quali l'avviso viene visualizzato all'utente prima del riavvio del computer. Specificare zero secondi per indicare che non deve essere visualizzato alcun messaggio di riavvio.<br /><br /> Esempi:<br /><br /> **"0"** (impostazione predefinita)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> Variabili di azione della sequenza di attività Ripristina stato utente  
 Le variabili per questa azione specificano le informazioni usate per ripristinare lo stato utente del computer di destinazione, ad esempio il nome percorso della cartella da cui viene ripristinato lo stato utente e se deve essere ripristinato l'account computer locale. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Ripristina stato utente](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|UNC o nome percorso locale della cartella da cui viene ripristinato lo stato utente.|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|Specifica che il ripristino dello stato utente continua anche se non è possibile ripristinare alcuni file.<br /><br /> Valori validi:<br /><br /> **"true"** (impostazione predefinita)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Consente la registrazione dettagliata per lo strumento USMT. Questo valore è richiesto dall'azione e deve essere impostato su "true" o "false".<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDMigrateLocalAccounts<br /><br /> (input)|Specifica se l'account computer locale viene ripristinato.<br /><br /> Valori validi:<br /><br /> **"true"**<br /><br /> **"false"** (impostazione predefinita)|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|Se la variabile **OSDMigrateLocalAccounts** è "true", questa variabile deve contenere la password assegnata a tutti gli account locali di cui viene eseguita la migrazione. Poiché a tutti gli account locali di cui viene eseguita la migrazione viene assegnata la stessa password, questa viene considerata una password temporanea che verrà modificata in seguito da un metodo diverso dalla distribuzione del sistema operativo di Configuration Manager.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|Specifica le opzioni aggiuntive della riga di comando dell'Utilità di migrazione stato utente (USMT, User State Migration Tool) che vengono usate quando si ripristina lo stato utente. Le opzioni aggiuntive vengono specificate in forma di stringa aggiunta alla riga di comando USMT generata automaticamente. Le opzioni USMT specificate con questa variabile della sequenza di attività non vengono convalidate per verificarne l'accuratezza prima di eseguire la sequenza di attività.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|Specifica l'ID del pacchetto di Configuration Manager che contiene i file USMT. Questa variabile è obbligatoria.|  

###  <a name="BKMK_RunCommand"></a> Variabili di azione della sequenza di attività Esegui riga di comando  
 Le variabili per questa azione specificano le informazioni usate per eseguire un comando dalla riga di comando, ad esempio la directory di lavoro in cui viene eseguito il comando. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Esegui riga di comando](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione|Descrizione|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|Per impostazione predefinita, quando l'esecuzione avviene in un sistema operativo a 64 bit, il programma nella riga di comando viene individuato ed eseguito usando il redirector del file system WOW64, in modo che vengano individuate le versioni a 32 bit dei programmi del sistema operativo e delle DLL. Se si imposta questa variabile su "true", viene disabilitato l'uso del redirector del file system WOW64, in modo tale che vengano trovate le versioni native a 64 bit dei programmi e delle DLL del sistema operativo. Questa variabile non ha effetto quando l'esecuzione avviene in un sistema operativo a 32 bit.|  
|WorkingDirectory<br /><br /> (input)|Specifica la directory di avvio per un'azione della riga di comando. Il nome di directory specificato non deve superare i 255 caratteri.<br /><br /> Esempi:<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|Specifica l'account da cui viene eseguita la riga di comando. Il valore è una stringa nel formato nomeutente o dominio\nome utente.|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|Specifica la password per l'account specificato dalla variabile SMSTSRunCommandLineUserName.|  

### <a name="set-dynamic-variables"></a>Imposta variabili dinamiche  
 Le variabili per questa azione vengono impostate automaticamente quando si aggiunge il passaggio della sequenza di attività Imposta variabili dinamiche. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Imposta variabili dinamiche](task-sequence-steps.md#BKMK_SetDynamicVariables).  

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

###  <a name="BKMK_SetupWindows"></a> Variabili di azione della sequenza di attività Imposta Windows e ConfigMgr  
 La variabile per questa azione specifica le proprietà di installazione del client che vengono usate quando si installa il client di Configuration Manager. Per altre informazioni sul passaggio della sequenza di attività associato a queste variabili, vedere [Imposta Windows e ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|Specifica le proprietà di installazione del client usate per l'installazione del client di Configuration Manager.|  

### <a name="upgrade-operating-system"></a>Aggiorna sistema operativo  
 La variabile per questa azione specifica che le opzioni aggiuntive della riga di comando non disponibili nella console di Configuration Manager vengono aggiunte al programma di installazione per un aggiornamento a Windows 10. Per altre informazioni sul passaggio della sequenza di attività associato a questa variabile, vedere [Aggiorna sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Dettagli  

|Nome variabile azione<br /><br /> (input)|Descrizione|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|Specifica le opzioni aggiuntive della riga di comando che vengono aggiunte al programma di installazione durante un aggiornamento a Windows 10. Le opzioni della riga di comando non vengono verificate. Di conseguenza, verificare che l'opzione immessa sia corretta.<br /><br /> Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  
