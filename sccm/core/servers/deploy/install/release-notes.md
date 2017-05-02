---
title: Note sulla versione - Configuration Manager | Microsoft Docs
description: Leggere queste note su problemi urgenti non ancora risolti nel prodotto o illustrati in un articolo di Microsoft Knowledge Base.
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 761c3f58f7c57d8f87ee802da37821895062546d
ms.openlocfilehash: 44338c705e308896c5203be239c160a8220369a8
ms.lasthandoff: 04/19/2017


---
# <a name="release-notes-for-system-center-configuration-manager"></a>Note sulla versione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con System Center Configuration Manager, le note sulla versione del prodotto sono limitate ai problemi urgenti non ancora risolti (disponibili con un aggiornamento nella console) o descritti in dettaglio in un articolo di Microsoft Knowledge Base.  

 Per i problemi noti che interessano gli scenari di base, queste informazioni vengono comunicate nella documentazione online del prodotto nella libreria della documentazione di System Center Configuration Manager.  

> [!TIP]  
>  Questo argomento contiene le note sulla versione di System Center Configuration Manager (Current Branch). Per una versione Technical Preview di System Center Configuration Manager, vedere [Technical Preview per System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

## <a name="setup-and-upgrade"></a>Configurazione e aggiornamento  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Dopo l'aggiornamento di una console di Configuration Manager tramite ConsoleSetup.exe dalla cartella dei server del sito, le modifiche recenti ai Language Pack non sono disponibili
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
Dopo l'esecuzione di un aggiornamento sul posto di una console usando ConsoleSetup.exe da una cartella di installazione dei server del sito, è possibile che i Language Pack installati di recente non siano disponibili. Questo problema si verifica nelle situazioni seguenti:
- Il sito esegue la versione 1610 o 1702.
- La console viene aggiornata sul posto usando ConsoleSetup.exe dalla cartella di installazione del server del sito.

Quando si verifica questo problema, la console reinstallata non usa il set più recente di Language Pack configurati. Non vengono restituiti errori, ma i Language Pack disponibili per la console rimangono invariati.  

**Soluzione alternativa:** disinstallare la console corrente e quindi reinstallarla come nuova installazione. È possibile usare ConsoleSetup.exe dalla cartella di installazione dei server del sito. Durante l'installazione, verificare di selezionare i file dei Language Pack da usare.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Con la versione 1702, il gruppo di limiti del sito predefinito è configurato per l'assegnazione sito
<!--  SMS 486380   Applicability should only be to 1702. -->
Con la versione 1702, la scheda Riferimento dei gruppi di limiti del sito predefiniti contiene la casella di controllo **Utilizza questo gruppo limite per l'assegnazione sito**, riporta il sito come **Sito assegnato** e risulta inattiva per impedire la modifica o la rimozione della configurazione.

**Soluzione temporanea:** Nessuna. È possibile ignorare questa impostazione. Anche se è abilitato per l'assegnazione sito, il gruppo di limiti del sito predefinito non viene usato per questo scopo. Con la versione 1702, questa configurazione assicura che il gruppo di limiti del sito predefinito venga associato al sito corretto.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Quando si installa un sito di Long-Term Servicing Branch con la versione 1606, viene installato un sito Current Branch
<!-- Consider move to core content  -->
Quando si usa il supporto di base della versione 1606 della versione di ottobre 2016 per installare un sito Long-Term Servicing Branch (LTSB), il programma di installazione installa invece un sito Current Branch. Ciò si verifica perché l'opzione per installare un punto di connessione del servizio con l'installazione del sito non è selezionata.

 - Anche se non è richiesto, un punto di connessione del servizio deve essere selezionato per l'installazione di un sito LTSB.

Al termine dell'installazione, il punto di connessione del servizio può essere disinstallato.  Tuttavia, è necessario avere un punto di connessione del servizio in modalità offline o online per inviare i dati di telemetria e ottenere gli aggiornamenti della protezione sia per i siti Current Branch che per i siti LTSB.

Se il sito è stato installato come Current Branch ma originariamente si voleva installare un sito LTSB, è possibile disinstallare il sito e quindi reinstallarlo. In alternativa è possibile chiamare il [Supporto tecnico Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) per assistenza.  

Per confermare quale tipologia installare, nella console passare a **Amministrazione** > **Configurazione del sito** > **Siti** e aprire **Impostazioni gerarchia**. L'opzione per convertire il sito in un sito Current Branch è disponibile solo quando il sito esegue LTSB.  

**Soluzione alternativa:**  nessuna.   



### <a name="the--sql-server-backup-model-in-use-by-configuration-manager-can-change-from-full-to-simple"></a>Il modello di backup di SQL Server usato da Configuration Manager può essere modificato da completo a semplice  
<!-- Confirm applicability for upgrade to later baselines. 1511 is out of support. 1606 is minmum supported baseline  -->

 Quando si esegue l'aggiornamento a System Center Configuration Manager versione 1511, il modello di backup di SQL Server usato da Configuration Manager può essere modificato da completo a semplice.  

-   Se si usa un'attività di backup di SQL Server personalizzata con il modello di backup completo (invece dell'attività di backup predefinita per Configuration Manager), l'aggiornamento può modificare il modello di backup da completo a semplice.  

**Soluzione alternativa**: dopo l'aggiornamento alla versione 1511, rivedere la configurazione di SQL Server e ripristinarla su completa, se necessario.  



### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Un aggiornamento è bloccato con stato Download nel nodo Aggiornamenti e manutenzione della console di Configuration Manager  
<!-- Source bug pending. Consider move to core content.  -->
Durante il download automatico degli aggiornamenti tramite un punto di connessione del servizio online, un aggiornamento può bloccarsi con stato Download. Quando il download di un aggiornamento è bloccato, le voci simili a quelle seguenti sono incluse nei file di log indicati:  

Log DMPdownloader:  

-   ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log  

-   Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.  

-   Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Soluzione alternativa**: sul server del sito modificare la chiave del Registro di sistema seguente in modo che corrisponda a quanto indicato di seguito e quindi riavviare il servizio SMS_Executive o attendere fino a 24 ore il successivo ciclo di download automatico.  

-   **Chiave da modificare**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valore per lo stato**: impostare sul valore decimale **146944** o sul valore esadecimale **0x00023e00**  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>L'installazione non riesce quando si usano file redist dalla cartella CD.Latest con un errore di verifica del manifesto
<!-- Source bug pending  -->

Quando si esegue il programma di installazione dalla cartella CD.Latest creata per la versione 1606 e si usano i file redist inclusi nella cartella CD.Latest, il programma di installazione non riesce e restituisce gli errori seguenti nel registro di installazione di Configuration Manager:

  - ERRORE: Controllo di hash file non riuscito per defaultcategories.dll
  - ERRORE: Verifica del manifesto non riuscita. Versione errata del manifesto?

**Soluzione alternativa:** eseguire una delle operazioni seguenti:
 - Durante l'installazione, scegliere di scaricare i file redist più aggiornati da Microsoft e non usare quelli inclusi nella cartella CD.Latest.
 - Eliminare manualmente la cartella *cd.latest\redist\languagepack\zhh* ed eseguire di nuovo l'installazione.

### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>Lo strumento di connessione del servizio genera un'eccezione quando SQL Server è in remoto, o quando la memoria condivisa è disabilitata
A partire dalla versione 1606, lo strumento di connessione del servizio genera un'eccezione quando viene soddisfatta una delle condizioni seguenti:  
 -    Il database del sito è remoto dal computer che ospita il punto di connessione del servizio e usa una porta non standard, cioè una porta diversa dalla 1433
 -     Il database del sito è sullo stesso server del punto di connessione del servizio, ma il protocollo SQL **Memoria condivisa** è disabilitato

L'eccezione è simile alla seguente:
 - *Eccezione non gestita: System.Data.SqlClient.SqlException: Si è verificato un errore correlato alla rete o specifico dell'istanza mentre veniva stabilita una connessione con SQL Server. Il server non è stato trovato o non era accessibile. Verificare che il nome istanza sia corretto e che SQL Server sia configurato per consentire le connessioni remote. (provider: Provider named pipe, errore: 40 - Impossibile aprire una connessione a SQL Server) --*

**Soluzione alternativa**: durante l'uso dello strumento è necessario modificare il Registro di sistema del server che ospita il punto di connessione del servizio per includere informazioni sulla porta di SQL Server:

   1.    Prima di usare lo strumento, modificare la chiave del Registro di sistema seguente e aggiungere il numero della porta in uso al nome di SQL Server:
    - Chiave: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valore: &lt;Nome SQL Server>
    - Aggiungere: **,&lt;PORTA>**

    Ad esempio, per aggiungere la porta *15001* a un server denominato *testserver.test.net*, la chiave risultante sarà: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.    Dopo aver aggiunto la porta al Registro di sistema, lo strumento dovrebbe funzionare correttamente.  

   3.    Una volta finito di usare lo strumento, sia per **la connessione** che per **l'importazione**, riportare la chiave del Registro di sistema al valore originale.  




<!-- No current Backup and Recovery relenotes
## Backup and recovery
-->


<!-- No current  Client deployment and upgrade relenotes
## Client deployment and upgrade  
-->



## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

### <a name="issue-with-the-windows-adk-for-windows-10-version-1511"></a>Problema con Windows ADK per Windows 10, versione 1511  
Quando si esegue una sequenza di attività da Software Center che usa un'immagine di avvio Windows PE v.10.0.10586 da Windows ADK 10, versione 1511, il riavvio del computer in Windows PE avrà esito negativo nella fase "Inizializzazione dispositivi hardware" e verrà visualizzato l'errore: **Inizializzazione di Windows PE non riuscita con codice errore 0x80220014**  

**Soluzione alternativa**: usare Windows 10 ADK originale. Per altre informazioni, vedere il blog del team di System Center Configuration Manager relativo al [problema con Windows ADK per Windows 10](http://blogs.technet.com/b/configmgrteam/archive/2015/11/20/issue-with-the-windows-adk-for-windows-10-version-1511.aspx)  

### <a name="dynamic-application-installation-fails-during-task-sequence-which-successfully-completes"></a>L'installazione dinamica dell'applicazione non riesce durante la sequenza di attività, che viene completata correttamente  
Quando si distribuisce una sequenza di attività che usa l'opzione **Installa le applicazioni in base all'elenco di variabili dinamiche**e l'installazione di una delle applicazioni non riesce per qualsiasi motivo, la sequenza di attività viene eseguita correttamente. Questo si verifica indipendentemente dalla modalità di configurazione delle opzioni seguenti:  

-   **Continua in caso di errore** (nella scheda Opzioni del passaggio Installa applicazione)  

-   **Se l'installazione di un'applicazione non riesce, continuare installando le altre applicazioni nell'elenco** (nella scheda delle Proprietà del passaggio Installa applicazione)  

È possibile visualizzare il file smsts.log per determinare se l'installazione di un'applicazione non è riuscita.  

**Soluzione alternativa**: usare la variabile **_TSAppInstallStatus** come condizione per una procedura successiva in una sequenza di attività con la condizione di non eseguire la sequenza di attività se si verifica un errore con una delle applicazioni dinamiche.  

### <a name="smb-might-not-work-properly-after-you-use-a-task-sequence-to-install-windows-10"></a>SMB può non funzionare correttamente dopo aver usato una sequenza di attività per installare Windows 10  
Quando si usa una sequenza di attività per installare un'immagine Windows 10, SMB potrebbe non funzionare correttamente dopo l'installazione del client di Configuration Manager. Ad esempio, i passaggi della sequenza di attività seguente potrebbero non riuscire:  

-   Ripristino dello stato utente se usato con un punto di migrazione stato  

-   Connessione a una cartella di rete  

Premendo F8 per avviare un prompt dei comandi amministrativo, è comunque possibile effettuare il PING del computer, ma il traffico di rete SMB, ad esempio tramite l'esecuzione di NET USE al prompt dei comandi, può non essere restituito, generando l'errore 1231 che indica che non è possibile raggiungere il percorso di rete.  

**Soluzione alternativa**:  
aggiungere un passaggio della sequenza di attività Esegui riga di comando dopo il passaggio Imposta Windows e ConfigMgr per arrestare e quindi avviare il servizio Workstation nel modo seguente:    
**net stop workstation /y & net start workstation**  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>I piani di manutenzione creano molte distribuzioni e molti gruppi di aggiornamento software duplicati per impostazione predefinita  
Per impostazione predefinita, la procedura guidata Crea piano di manutenzione viene attualmente eseguita dopo ogni sincronizzazione degli aggiornamenti software. A ogni esecuzione, la procedura guidata crea un nuovo gruppo di aggiornamento software e una nuova distribuzione. Se una sincronizzazione degli aggiornamenti software viene eseguita molte volte al giorno, ad esempio, la procedura guidata Crea piano di manutenzione crea più distribuzioni e gruppi di aggiornamento software, probabilmente identici, ogni giorno.  

**Soluzione alternativa**:    
dopo aver creato un piano di manutenzione, aprire le proprietà del piano, passare alla scheda **Pianificazione valutazione**, selezionare **Esegui la regola in base a una pianificazione**, fare clic su **Personalizza** e quindi creare una pianificazione personalizzata. Ad esempio, è possibile impostare l'esecuzione del piano di manutenzione ogni 60 giorni.  

### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quando viene visualizzata una finestra di dialogo per una distribuzione ad alto rischio, le finestre di dialogo per distribuzione ad alto rischio successive con scadenza più ravvicinata non vengono visualizzate
Dopo aver creato e distribuito una distribuzione ad alto rischio agli utenti, viene visualizzata una finestra di dialogo per distribuzione ad alto rischio all'utente. Se l'utente non chiude la finestra di dialogo e viene creata e distribuita un'altra distribuzione ad alto rischio con scadenza più ravvicinata rispetto alla prima, l'utente non visualizzerà una finestra di dialogo aggiornata fino alla chiusura della finestra di dialogo originale. Le distribuzioni verranno comunque eseguite in base alle scadenze configurate.

**Soluzione alternativa**:  
L'utente deve chiudere la finestra di dialogo per la prima distribuzione ad alto rischio per visualizzare la finestra di dialogo per la distribuzione ad alto rischio successiva.

## <a name="mobile-device-management"></a>Gestione dispositivi mobili  

### <a name="cannot-create-an-enrollment-profile-on-a-primary-site"></a>Non è possibile creare un profilo di registrazione in un sito primario  
Un amministratore non può creare un profilo di registrazione nella console di amministrazione di System Center Configuration Manager che si connette a un sito primario. Quando si prova a eseguire la registrazione, l'amministratore riceverà il messaggio di errore "Il token DEP non è stato aggiornato. Caricare un token DEP" nella Creazione guidata profilo di registrazione. Questo errore si verifica anche se è stato caricato un token DEP valido nel sito di amministrazione centrale.  

**Soluzione alternativa**: creare un profilo di registrazione nella console di amministrazione di System Center Configuration Manager che si connette a un sito di amministrazione centrale.  

### <a name="dep-cannot-use-non-alpha-numeric-characters-in-enrollment-profiles"></a>DEP non può usare caratteri non alfanumerici nei profili di registrazione  
I profili di registrazione associati al programma di registrazione dei dispositivi (DEP) di Apple non possono usare caratteri non alfanumerici nei campi **Nome**, **Descrizione**, **Reparto** e **Numero di telefono** per il profilo di registrazione quando DEP è attivato. L'uso di caratteri non alfanumerici in questi campi determina la creazione di un profilo di registrazione, ma il profilo non può essere caricato in Apple. Il server Apple non fornisce alcun messaggio di errore o avviso e i profili non verranno distribuiti ai dispositivi gestiti dal programma di registrazione dei dispositivi.  

**Soluzione alternativa:** nessuna.

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>La cancellazione completa disattiva i dispositivi Windows 10 con meno di 4 GB di RAM

L'esecuzione della cancellazione completa nei dispositivi Windows 10 RTM (versioni precedenti alla versione 1511) con meno di 4 GB di RAM può rendere i dispositivi inutilizzabili. Dopo aver tentato la cancellazione completa, il dispositivo non può essere avviato e non risponde.

**Soluzione alternativa**: verificare che i PC Windows 10 RTM abbiano almeno 4 GB di RAM disponibile prima di eseguire una cancellazione completa del dispositivo. Per visualizzare il numero di versione dei dispositivi Windows 10, immettere "winver" al prompt dei comandi. Se il dispositivo è già stato cancellato e non risponde, usare un'unità di avvio USB con Windows 10 per avviare e ripristinare l'accesso al dispositivo.

### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando un utente appartiene a due o più raccolte di utenti in cui sono distribuiti criteri di termini e condizioni, l'utente visualizza più insiemi degli stessi termini  

Quando un amministratore distribuisce un insieme di termini in più raccolte utente e un utente è membro di più di una di queste raccolte, tale utente visualizzerà più copie di termini identici all'apertura del portale aziendale.  Se, ad esempio, un utente denominato "UtenteEsempio" è un membro di due diverse raccolte di utenti, denominate "DipendentiAzienda1" e "DipendentiAzienda2" e i termini e le condizioni denominati "CondizioniAziendali" vengono distribuiti sia a DipendentiAzienda1 sia a DipendentiAzienda2, UtenteEsempio vedrà due set identici di CondizioniAziendali nella pagina di accettazione delle condizioni. Considerato che gli utenti possono solo accettare o rifiutare tutte le condizioni, non vi è alcun rischio di trovarsi in uno stato di accettazione ambiguo in cui l'utente ha sia accettato che rifiutato le condizioni. Il report di accettazione di termini e condizioni includerà una sola riga per ogni set di condizioni per ogni utente, quindi nel report non possono esserci errori. L'unico effetto riscontrato dall'utente è la visualizzazione di due insiemi di condizioni nella pagina di accettazione.  

**Soluzione alternativa**: assicurarsi che ogni utente sia incluso solo in solo una raccolta in cui vengono distribuite le condizioni.  

## <a name="reports-and-monitoring"></a>Report e monitoraggio  

### <a name="the-health-attestation-report-is-empty-even-though-health-attestation-data-was-previously-collected"></a>Il report di attestazione dell'integrità è vuoto anche se in precedenza sono stati raccolti dati di attestazione dell'integrità  
Quando un utente amministratore con un ruolo di sicurezza che include l'autorizzazione **Lettura** per il gruppo di autorizzazioni **Attestazione dell'integrità** visualizza il report di attestazione dell'integrità, il report è vuoto e non contiene alcun dato. Il motivo è che le autorizzazioni per visualizzare i dati nel report di attestazione dell'integrità son collegate al gruppo di autorizzazioni **Affinità utente dispositivo** invece che al gruppo Attestazione dell'integrità.  

Questo problema interessa System Center Configuration Manager con aggiornamento 1602 e verrà risolto in un aggiornamento futuro.  

**Soluzione alternativa**: assegnare all'utente amministratore un gruppo di sicurezza che include l'autorizzazione **Lettura** per il gruppo di autorizzazioni **Affinità utente dispositivo**.  

### <a name="conditional-access"></a>Accesso condizionale  

#### <a name="the-same-user-collection-is-not-blocked-from-being-added-to-both-exempted-and-targeted-collections"></a>L'aggiunta della stessa raccolta utenti alle pagine Raccolte esentate e Raccolte di destinazione non viene bloccata.  
Questo avviene solo quando si aggiunge la stessa **raccolta utenti** alla pagina **Raccolte esentate** **prima** di aggiungerla alla pagina **Raccolte di destinazione**.  Se si aggiunge una **raccolta utenti** prima di tutto alla pagina **Raccolte di destinazione** e quindi si prova ad aggiungere la stessa **raccolta utenti** alla pagina **Raccolte esentate**, in genere viene visualizzato il normale messaggio di blocco.  

Questo problema interessa l'accesso condizionale di System Center Configuration Manager per **Exchange locale** con l'aggiornamento 1602 e verrà risolto in un aggiornamento futuro.  

**Soluzione alternativa**: aggiungere la **raccolta utenti** alla pagina **Raccolte di destinazione** prima di selezionare **Raccolta utenti** nella pagina **Raccolte esentate** oppure evitare di aggiungere la stessa **raccolta utenti** a entrambe le pagine.

## <a name="endpoint-protection"></a>Endpoint Protection
<!--  Product Studio bug 485370 added by Nathbarn 04 19 2017 -->
### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>Non è possibile applicare i criteri antimalware in Windows Server 2016 Core
Non è possibile applicare i criteri antimalware in Windows Server 2016 Core.  Codice di errore: 0x80070002.  Manca una dipendenza per ConfigSecurityPolicy.exe.

**Soluzione alternativa:**  nessuna.  Come amministratore, è possibile usare i criteri di gruppo per gestire le impostazioni per Windows Server 2016 Core.

