---
title: Sicurezza e privacy per la gestione delle applicazioni | Documentazione Microsoft
description: Questo argomento contiene informazioni sulle procedure consigliate per la sicurezza e la privacy della gestione delle applicazioni in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 521b90b9d497818a4c1e546fca38cd15d4cab487
ms.openlocfilehash: 6ee99fa0c07676f004e41a50bf16d0d17604e790


---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Sicurezza e privacy per la gestione delle applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-application-management"></a>Procedure ottimali di protezione per la gestione delle applicazioni  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Configurare i punti del Catalogo applicazioni per utilizzare le connessioni HTTPS e istruire gli utenti sui pericoli di siti Web dannosi.|Configurare il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni per accettare le connessioni HTTPS in modo che il server venga autenticato per gli utenti e i dati trasmessi siano protetti da manomissioni e visualizzazioni. Impedire attacchi di ingegneria sociale istruendo gli utenti a connettersi esclusivamente a siti Web attendibili.<br /><br /> Non usare opzioni di configurazione di personalizzazione che mostrano il nome dell'organizzazione nel Catalogo applicazioni per l'identificazione quando non si usa HTTPS.|  
|Utilizzare la separazione dei ruoli e installare il punto per siti Web del Catalogo applicazioni e il punto di servizio del Catalogo applicazioni su server separati.|Se il punto per siti Web del Catalogo applicazioni è compromesso, installarlo in un server separato dal punto per servizi Web del Catalogo applicazioni. Ciò consente di proteggere i client di Configuration Manager e l'infrastruttura di Configuration Manager. Questo è particolarmente importante se il punto per siti Web del Catalogo applicazioni accetta connessioni client da Internet perché questa configurazione rende il server vulnerabile agli attacchi.|  
|Istruire gli utenti a chiudere la finestra del browser dopo aver utilizzato il Catalogo applicazioni.|Se gli utenti navigano in un sito Web esterno nella stessa finestra del browser utilizzata per il Catalogo applicazioni, il browser continua a utilizzare le impostazioni di protezione adatte per i siti attendibili nell'intranet.|  
|Specificare manualmente l'affinità utente-dispositivo invece di consentire agli utenti di identificare il dispositivo primario. Non abilitare la configurazione basata sull'utilizzo.|Non considerare autorevoli le informazioni raccolte dagli utenti o dal dispositivo. Se si distribuisce software utilizzando l'affinità utente dispositivo non specificata da un utente amministratore attendibile, il software potrebbe essere installato su computer e utenti che non sono autorizzati a ricevere tale software.|  
|Configurare sempre le distribuzioni per scaricare il contenuto dai punti di distribuzione, anziché eseguirlo dai punti di distribuzione.|Quando si configurano le distribuzioni per scaricare il contenuto da un punto di distribuzione ed eseguirlo in locale, il client di Configuration Manager verifica l'hash del pacchetto dopo aver scaricato il contenuto. Il client scarta il pacchetto se l'hash non corrisponde all'hash nei criteri. Se invece si configura la distribuzione in modo da eseguirla direttamente da un punto di distribuzione, il client di Configuration Manager non verifica l'hash pacchetto, quindi il client di Configuration Manager può installare software che è stato manomesso.<br /><br /> Se si eseguono le distribuzioni direttamente da punti di distribuzione, usare autorizzazioni NTFS minime nei pacchetti nei punti di distribuzione e usare IPSec (Internet Protocol Security) per proteggere il canale tra il client e i punti di distribuzione e tra i punti di distribuzioni e il server del sito.|  
|Non consentire agli utenti di interagire con i programmi se è necessaria l'opzione **Esegui con diritti amministrativi**.|Quando si configura un programma, è possibile impostare l'opzione **Consenti agli utenti di interagire con il programma** in modo che gli utenti possano rispondere a qualsiasi richiesta necessaria nell'interfaccia utente. Se anche il programma è configurato con **Esegui con diritti amministrativi**, un utente malintenzionato nel computer in cui è in esecuzione il programma potrebbe utilizzare l'interfaccia utente per riassegnare i privilegi sul computer client.<br /><br /> Usare programmi che usano Windows Installer per l'installazione e privilegi elevati per utente per le distribuzioni software che richiedono credenziali amministrative. Il programma di installazione deve essere eseguito nel contesto di un utente che non ha credenziali amministrative. I privilegi elevati per utente di Windows Installer rappresentano il modo più sicuro per distribuire applicazioni con questo requisito.|  
|Limitare gli utenti che possono installare software in modo interattivo utilizzando l'impostazione client **Autorizzazioni installazione** .|Configurare l'impostazione **Autorizzazioni di installazione** del dispositivo client **Agente computer** per limitare i tipi di utenti che possono installare software usando il Catalogo applicazioni o Software Center. Ad esempio, creare un impostazione client personalizzata con **Autorizzazioni di installazione** impostato su **Solo amministratori**. Applicare quindi questa impostazione client a una raccolta di server per impedire agli utenti senza autorizzazioni amministrative di installare software in tali computer.|  
|Per i dispositivi mobili, distribuire solo le applicazioni firmate.|Distribuire applicazioni per dispositivi mobili solo se il relativo codice è firmato da un'autorità di certificazione (CA) considerata attendibile dal dispositivo mobile. Ad esempio:<br /><br /><ul><li>Un'applicazione di un fornitore, firmata da un'autorità di certificazione nota, come VeriSign.</li><li>Un'applicazione interna che viene firmata in modo indipendente da Configuration Manager usando l'autorità di certificazione interna.</li><li>Un'applicazione interna firmata con Configuration Manager quando si crea il tipo di applicazione e si usa un certificato di firma.</li></ul>|  
|Se si firmano applicazioni per dispositivi mobili usando la **Creazione guidata applicazione** in Configuration Manager, proteggere il percorso del file del certificato di firma e il canale di comunicazione.|Per proteggersi da attacchi di elevazione dei privilegi e man-in-the-middle, memorizzare il file del certificato di firma in una cartella protetta e usare IPSec o SMB (Server Message Block) tra i computer seguenti:<br /><br /><ul><li>Computer che esegue la console di Configuration Manager</li><li>Computer in cui è archiviato il file del certificato di firma</li><li>Computer in cui sono archiviati i file di origine dell'applicazione</li></ul> In alternativa, firmare l'applicazione indipendentemente da Configuration Manager e prima di eseguire la **Creazione guidata applicazione**.|  
|Implementare i controlli di accesso per proteggere i computer di riferimento.|Quando un utente amministratore configura il metodo di rilevamento in un tipo di distribuzione selezionando un computer di riferimento, assicurarsi che il computer non sia stato compromesso.|  
|Limitare e monitorare gli utenti amministratori a cui vengono concessi i ruoli di protezione basati su ruoli relativi alla gestione delle applicazioni:<br /><br /><ul><li>**Amministratore applicazione**</li><li>**Autore applicazione**</li><li> **Gestione distribuzione applicazioni**</li></ul>|Anche quando si configura l'amministrazione basata su ruoli, gli utenti amministratori che creano e distribuiscono le applicazioni potrebbero disporre di più autorizzazioni del previsto. Ad esempio, gli utenti amministratori che creano o modificano un'applicazione possono selezionare applicazioni dipendenti non incluse nel loro ambito di protezione.|  
|Durante la configurazione di ambienti virtuali Microsoft Application Virtualization (App-V), selezionare le applicazioni con lo stesso livello di attendibilità nell'ambiente virtuale.|Poiché le applicazioni in un ambiente virtuale App-V possono condividere risorse, come gli Appunti, configurare l'ambiente virtuale in modo che le applicazioni selezionate abbiano lo stesso livello di attendibilità.<br /><br /> Per altre informazioni, vedere [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Creare ambienti virtuali App-V).|  
|Se si distribuiscono applicazioni per computer Mac, accertarsi che i file di origine provengano da una fonte attendibile.|Lo strumento CMAppUtil non convalida la firma del pacchetto di origine, quindi assicurarsi che il pacchetto provenga da una fonte attendibile. Lo strumento CMAppUtil non consente di rilevare eventuali manomissioni dei file.|  
|Se si distribuiscono applicazioni per computer Mac, proteggere il percorso del file **CMMAC** e il canale di comunicazione quando si importa tale file in Configuration Manager.|Il file **CMMAC** generato dallo strumento CMAppUtil e importato in Configuration Manager non è firmato o convalidato. Per evitare la manomissione di questo file, archiviarlo in una cartella sicura e usare IPSec o SMB tra i computer seguenti:<br /><br /><ul><li>Computer che esegue la console di Configuration Manager</li><li>Computer in cui è archiviato il file **CMMAC**</li></ul>.|  
|Se si configura un tipo di distribuzione applicazioni Web, usare HTTPS anziché HTTP per proteggere la connessione.|Se si distribuisce un'applicazione Web usando un collegamento HTTP anziché un collegamento HTTPS, il dispositivo potrebbe essere reindirizzato a un server non autorizzato e i dati trasferiti tra il dispositivo e il server potrebbero essere manomessi.|  

##  <a name="security-issues-for-application-management"></a>Problemi di protezione per la gestione delle applicazioni  

-   Utenti con diritti limitati possono copiare file dalla cache del client sul computer client.  

     Gli utenti possono leggere la cache del client, ma non possono scrivere al suo interno. Con le autorizzazioni di lettura, un utente può copiare i file di installazione applicazione da un computer a un altro.  

-   Gli utenti con diritti limitati possono modificare i file che registrano la cronologia della distribuzione software nel computer client.  

     Dato che le informazioni sulla cronologia applicazioni non sono protette, un utente può modificare i file che indicano se un'applicazione è installata.  

-   I pacchetti App-V non sono firmati.  

     I pacchetti App-V in Configuration Manager non supportano la firma per verificare che il contenuto provenga da una fonte attendibile e non sia stato alterato durante la trasmissione. Non è possibile ovviare a questo problema di sicurezza. Assicurarsi di seguire la procedura consigliata per la sicurezza per scaricare il contenuto da una fonte attendibile e da un percorso sicuro.  

-   Le applicazioni App-V pubblicate possono essere installate da tutti gli utenti sul computer.  

     Quando un'applicazione App-V viene pubblicata in un computer, tutti gli utenti che accedono a tale computer possono installare l'applicazione. Ciò significa che non è possibile limitare gli utenti che possono installare l'applicazione dopo la pubblicazione.  

-   Non è possibile limitare le autorizzazioni di installazione per il portale dell'azienda.  

     Sebbene sia possibile configurare un'impostazione client per limitare le autorizzazioni di installazione, ad esempio solo per utenti principali di un dispositivo o per agli amministratori locali, tale impostazione non funziona per il portale dell'azienda. Ciò potrebbe determinare una condizione di elevazione dei privilegi, perché gli utenti potrebbero installare app per cui non sono autorizzati.  

##  <a name="a-namebkmkcertificatessilverlight5a-certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a> Certificati per Microsoft Silverlight 5 e modalità di attendibilità elevata richiesta per il Catalogo applicazioni  
 I client di Configuration Manager richiedono Microsoft Silverlight 5, che deve essere eseguito in modalità di attendibilità elevata affinché gli utenti installino il software dal Catalogo applicazioni. Per impostazione predefinita, le applicazioni Silverlight vengono eseguite in modalità di attendibilità parziale per evitare l'accesso ai dati utente. Configuration Manager installa automaticamente Microsoft Silverlight 5 nei client se non è già installato. Per impostazione predefinita, Configuration Manager imposta su **Sì** l'impostazione client **Consentire alle applicazioni di Silverlight di essere eseguite in modalità attendibilità elevata**. Questa impostazione consente alle applicazioni Silverlight firmate e attendibili di richiedere la modalità attendibilità elevata.  

 Quando si installa il ruolo del sistema del sito del punto per siti Web del Catalogo applicazioni, il client installa anche un certificato di firma Microsoft nell'archivio certificati del computer Autori attendibili in ogni computer client di Configuration Manager. Questo certificato consente alle applicazioni Silverlight firmate da questo certificato l'esecuzione nella modalità attendibilità elevata che i computer richiedono per installare software dal Catalogo applicazioni. Configuration Manager gestisce automaticamente questo certificato di firma. Per garantire la continuità del servizio, non eliminare manualmente né spostare questo certificato di firma Microsoft.  

> [!WARNING]  
>  Se abilitata, l'impostazione client **Consentire alle applicazioni di Silverlight di essere eseguite in modalità attendibilità elevata** consente l'esecuzione in modalità attendibilità elevata per tutte le applicazioni Silverlight firmate da certificati nell'archivio certificati Autori attendibili nell'archivio computer o nell'archivio utente. L'impostazione client non può abilitare la modalità di attendibilità elevata specificamente per il Catalogo applicazioni di Configuration Manager o per l'archivio certificati Autori attendibili nell'archivio computer. Se un malware aggiunge un certificato non autorizzato nell'archivio Autori attendibili, ad esempio nell'archivio utente, anche il malware che utilizza l'applicazione Silverlight può essere eseguito in modalità di attendibilità elevata.  

 Se si configura l'impostazione client **Consentire alle applicazioni di Silverlight di essere eseguite in modalità attendibilità elevata** su **No**, ciò non rimuove il certificato di firma Microsoft dai client.  

 Per altre informazioni sulle applicazioni attendibili in Silverlight, vedere [Trusted Applications (Applicazioni attendibili)](http://go.microsoft.com/fwlink/p/?LinkId=252842).  

##  <a name="privacy-information-for-application-management"></a>Informazioni sulla privacy per la gestione delle applicazioni  
 La gestione delle applicazioni consente l'esecuzione di qualsiasi applicazione, programma o script su qualsiasi computer client o dispositivo mobile client della gerarchia. Configuration Manager non controlla i tipi di applicazioni, programmi o script eseguiti né il tipo di informazioni trasmesse. Durante il processo di distribuzione delle applicazioni, Configuration Manager può trasmettere informazioni che identificano gli account di accesso e del dispositivo tra i client e i server.  

 Configuration Manager conserva le informazioni sullo stato relative al processo di distribuzione del software. Le informazioni sullo stato di distribuzione del software non vengono crittografate durante la trasmissione, a meno che il client non comunichi utilizzando HTTPS. Le informazioni sullo stato non vengono memorizzate in forma crittografata nel database.  

 L'uso delle funzionalità di installazione delle applicazioni di Configuration Manager per installare in remoto, in modo interattivo o automatico il software nei client può essere soggetto alle condizioni di licenza software per tali software, distinte dalle Condizioni di licenza software per System Center Configuration Manager. Rivedere sempre e accettare le Condizioni di licenza software prima di distribuire il software usando Configuration Manager.  

 La distribuzione delle applicazioni non avviene per impostazione predefinita e richiede diversi passaggi di configurazione.  

 Due funzionalità facoltative che consentono la corretta distribuzione del software sono l'affinità utente dispositivo e il Catalogo applicazioni:  

-   L'affinità utente-dispositivo esegue il mapping di un utente ai dispositivi in modo che un amministratore di Configuration Manager possa distribuire il software all'utente e il software venga automaticamente installato in uno o più computer che l'utente usa più di frequente.  

-   Il Catalogo applicazioni è un sito Web che consente agli utenti di richiedere software da installare.  

 Visualizzare le sezioni seguenti per informazioni sulla privacy sull'affinità utente dispositivo e il Catalogo applicazioni.  

 Prima di configurare la gestione delle applicazioni, considerare i requisiti sulla privacy.  

##  <a name="user-device-affinity"></a>Affinità utente dispositivo  
-  È possibile che Configuration Manager trasmetta informazioni tra i client e i sistemi del sito del punto di gestione, che identificano il computer e l'account di accesso, nonché dati di utilizzo aggregati relativi agli account di accesso.  
-  Le informazioni trasmesse tra il client e il server non vengono crittografate, a meno che il punto di gestione non sia configurato in modo da richiedere che i client comunichino tramite HTTPS.  
-  Le informazioni sul computer e sull'utilizzo dell'account di accesso, usate per eseguire il mapping di un utente a un dispositivo, vengono archiviate nei computer client, inviate ai punti di gestione e quindi archiviate nel database di Configuration Manager. Le informazioni precedenti vengono eliminate dal database per impostazione predefinita dopo 90 giorni. È possibile configurare il comportamento di eliminazione impostando l'attività di manutenzione del sito **Elimina dati di affinità utente dispositivo obsoleti** .
-  Configuration Manager conserva informazioni sullo stato relative all'affinità utente dispositivo. Le informazioni sullo stato non vengono crittografate durante la trasmissione, a meno che i client non siano configurati in modo da comunicare con i punti di gestione tramite HTTPS. Le informazioni sullo stato non vengono memorizzate in forma crittografata nel database.  
-  Le informazioni sul computer, le informazioni sull'utilizzo dell'account di accesso e le informazioni sullo stato non vengono inviate a Microsoft.  
-  Le informazioni sul computer e sull'utilizzo dell'account di accesso, usate per stabilire l'affinità tra utenti e dispositivi, sono sempre abilitate. Inoltre, gli utenti e gli utenti amministrativi possono fornire informazioni sull'affinità utente dispositivo.  

##  <a name="application-catalog"></a>Catalogo applicazioni  
-  Il Catalogo applicazioni consente all'amministratore di Configuration Manager di pubblicare tutte le applicazioni, i programmi o gli script che gli utenti dovranno eseguire. Configuration Manager non ha alcun controllo sui tipi di programmi o script che vengono pubblicati nel catalogo, né sul tipo di informazioni trasmesse.    
-  Configuration Manager potrebbe trasmettere informazioni tra i client e i ruoli del sistema del sito del Catalogo applicazioni. Queste informazioni potrebbero consentire l'identificazione di computer e account di accesso. Le informazioni trasmesse tra il client e i server non vengono crittografate, a meno che tali ruoli del sistema non siano configurati in modo da richiedere che i client si connettano tramite HTTPS.  
-  Le informazioni relative alla richiesta di approvazione applicazione vengono memorizzate nel database di Configuration Manager. Le richieste annullate o respinte vengono eliminate per impostazione predefinita dopo 30 giorni, insieme alle relative voci di cronologia delle richieste. È possibile configurare il comportamento di eliminazione impostando l'attività di manutenzione del sito **Elimina dati richiesta applicazione obsoleti** . Le richieste di approvazione di applicazioni con stato approvato e in attesa non vengono mai eliminate.  
-  Le informazioni scambiate con il Catalogo applicazioni non vengono inviate a Microsoft.  
-  Il Catalogo applicazioni non viene installato per impostazione predefinita. Questa installazione richiede diversi passaggi di configurazione.  



<!--HONumber=Dec16_HO3-->


