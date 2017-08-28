---
title: Note sulla versione - Configuration Manager | Microsoft Docs
description: Leggere queste note su problemi urgenti non ancora risolti nel prodotto o illustrati in un articolo di Microsoft Knowledge Base.
ms.custom: na
ms.date: 08/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 24f30bddb345e3a08d4b655d89693c226005cb0e
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2017
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
Dopo l'esecuzione di un aggiornamento sul posto in una console usando ConsoleSetup.exe da una cartella di installazione dei server del sito, è possibile che i Language Pack installati di recente non siano disponibili. Questo problema si verifica nelle situazioni seguenti:
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


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Un aggiornamento è bloccato con stato Download nel nodo Aggiornamenti e manutenzione della console di Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
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
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Quando si esegue il programma di installazione dalla cartella CD.Latest creata per la versione 1606 e si usano i file redist inclusi nella cartella CD.Latest, il programma di installazione non riesce e restituisce gli errori seguenti nel registro di installazione di Configuration Manager:

  - ERRORE: Controllo di hash file non riuscito per defaultcategories.dll
  - ERRORE: Verifica del manifesto non riuscita. Versione errata del manifesto?

**Soluzione alternativa:** eseguire una delle operazioni seguenti:
 - Durante l'installazione, scegliere di scaricare i file redist più aggiornati da Microsoft e non usare quelli inclusi nella cartella CD.Latest.
 - Eliminare manualmente la cartella *cd.latest\redist\languagepack\zhh* ed eseguire di nuovo l'installazione.


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>Lo strumento di connessione del servizio genera un'eccezione quando SQL Server è in remoto, o quando la memoria condivisa è disabilitata
<!-- 479223   Fixed in 1702 and later   -->
A partire dalla versione 1606, lo strumento di connessione del servizio genera un'eccezione quando viene soddisfatta una delle condizioni seguenti:  
 -  Il database del sito è remoto dal computer che ospita il punto di connessione del servizio e usa una porta non standard, cioè una porta diversa dalla 1433
 -  Il database del sito è sullo stesso server del punto di connessione del servizio, ma il protocollo SQL **Memoria condivisa** è disabilitato

L'eccezione è simile alla seguente:
 - *Eccezione non gestita: System.Data.SqlClient.SqlException: Si è verificato un errore correlato alla rete o specifico dell'istanza mentre veniva stabilita una connessione con SQL Server. Il server non è stato trovato o non era accessibile. Verificare che il nome istanza sia corretto e che SQL Server sia configurato per consentire le connessioni remote. (provider: Provider named pipe, errore: 40 - Impossibile aprire una connessione a SQL Server) --*

**Soluzione alternativa**: durante l'uso dello strumento è necessario modificare il Registro di sistema del server che ospita il punto di connessione del servizio per includere informazioni sulla porta di SQL Server:

   1.   Prima di usare lo strumento, modificare la chiave del Registro di sistema seguente e aggiungere il numero della porta in uso al nome di SQL Server:
    - Chiave: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valore: &lt;Nome SQL Server>
    - Aggiungere: **,&lt;PORTA>**

    Ad esempio, per aggiungere la porta *15001* a un server denominato *testserver.test.net*, la chiave risultante sarà: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   Dopo aver aggiunto la porta al Registro di sistema, lo strumento dovrebbe funzionare correttamente.  

   3.   Una volta finito di usare lo strumento, sia per **la connessione** che per **l'importazione**, riportare la chiave del Registro di sistema al valore originale.  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Distribuzione e aggiornamento del client  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>L'installazione del client non riesce e viene restituito il codice di errore 0x8007064c
<!--- SMS 486973 -->
Quando si distribuisce il client in computer Windows, l'installazione ha esito negativo. Il file ccmsetup.log contiene la voce "File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation" seguita da "InstallFromManifest failed 0x8007064c".

**Soluzione alternativa** Il problema è causato da una versione danneggiata di Silverlight installata in precedenza. Per risolvere il problema, provare a eseguire lo strumento seguente sul computer interessato: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

### <a name="if-the-boot-image-contains-drivers-the-image-fails-to-reload-the-current-windows-pe-version-from-the-windows-assessment-and-deployment-kit-adk"></a>Se l'immagine di avvio contiene driver, l'immagine non riesce a ricaricare la versione di Windows PE da Windows Assessment and Deployment Kit (ADK)
<!-- 495087 -->
È possibile usare Aggiornamento guidato punti di distribuzione per aggiornare i punti di distribuzione con un'immagine di avvio archiviata insieme alla versione più recente di Windows PE dalla directory di installazione di Windows Assessment and Deployment Kit (ADK). Per aggiornare, aprire Aggiornamento guidato punti di distribuzione e selezionare **Ricarica questa immagine di avvio con la versione corrente di Windows PE da Windows ADK**.

Se l'immagine di avvio contiene driver, l'aggiornamento non riuscirà. La procedura guidata ricarica l'immagine da Windows ADK, visualizza una finestra di dialogo contenente un'eccezione che l'utente può ignorare e quindi visualizza una schermata di operazione riuscita. Tuttavia, i componenti più recenti del client di Configuration Manager non verranno aggiunti all'immagine di avvio. L'immagine di avvio non viene aggiornata nel punto di distribuzione

**Soluzione alternativa**: eseguire l'Aggiornamento guidato punti di distribuzione due volte.

1. Eseguire la procedura guidata con l'opzione **Ricarica questa immagine di avvio con la versione corrente di Windows PE da Windows ADK** selezionata. In questo modo, si otterrà la versione più recente di Windows PE.
2. Eseguire di nuovo la procedura guidata con l'opzione **Ricarica questa immagine di avvio con la versione corrente di Windows PE da Windows ADK** non selezionata. In questo modo, verranno recuperati i file binari del client più recenti e l'immagine di avvio nel punto di distribuzione verrà aggiornata.

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>I piani di manutenzione creano molte distribuzioni e molti gruppi di aggiornamento software duplicati per impostazione predefinita  
Per impostazione predefinita, la procedura guidata Crea piano di manutenzione viene attualmente eseguita dopo ogni sincronizzazione degli aggiornamenti software. A ogni esecuzione, la procedura guidata crea un nuovo gruppo di aggiornamento software e una nuova distribuzione. Se una sincronizzazione degli aggiornamenti software viene eseguita molte volte al giorno, ad esempio, la procedura guidata Crea piano di manutenzione crea più distribuzioni e gruppi di aggiornamento software, probabilmente identici, ogni giorno.  

**Soluzione alternativa**:    
dopo aver creato un piano di manutenzione, aprire le proprietà del piano, passare alla scheda **Pianificazione valutazione**, selezionare **Esegui la regola in base a una pianificazione**, fare clic su **Personalizza** e quindi creare una pianificazione personalizzata. Ad esempio, è possibile impostare l'esecuzione del piano di manutenzione ogni 60 giorni.  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Quando viene visualizzata una finestra di dialogo per una distribuzione ad alto rischio, le finestre di dialogo per distribuzione ad alto rischio successive con scadenza più ravvicinata non vengono visualizzate
<!-- Fixed in 1702 and later -->
Dopo aver creato e distribuito una distribuzione ad alto rischio agli utenti, viene visualizzata una finestra di dialogo per distribuzione ad alto rischio all'utente. Se l'utente non chiude la finestra di dialogo e viene creata e distribuita un'altra distribuzione ad alto rischio con scadenza più ravvicinata rispetto alla prima, l'utente non visualizzerà una finestra di dialogo aggiornata fino alla chiusura della finestra di dialogo originale. Le distribuzioni verranno comunque eseguite in base alle scadenze configurate.

**Soluzione alternativa**:  
L'utente deve chiudere la finestra di dialogo per la prima distribuzione ad alto rischio per visualizzare la finestra di dialogo per la distribuzione ad alto rischio successiva.



## <a name="software-updates"></a>Aggiornamenti software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>L'importazione delle impostazioni client di Office 365 da un file di configurazione non ha esito positivo quando contiene lingue non supportate
<!-- 489258  Fixed in 1706  -->
Si verificherà un errore quando si importano le impostazioni del client di Office 365 da un file di configurazione XML esistente e il file contiene lingue non supportate dal client di Office 365 ProPlus. Per i dettagli vedere [Distribuire le app di Office 365 ai client dal dashboard di gestione client di Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Soluzione alternativa**:    
Usare solo [lingue supportate dal client di Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) nel file di configurazione XML.  



## <a name="mobile-device-management"></a>Gestione dispositivi mobili  

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>La cancellazione completa disattiva i dispositivi Windows 10 con meno di 4 GB di RAM
L'esecuzione della cancellazione completa nei dispositivi Windows 10 RTM (versioni precedenti alla versione 1511) con meno di 4 GB di RAM può rendere i dispositivi inutilizzabili. Dopo aver tentato la cancellazione completa, il dispositivo non può essere avviato e non risponde.

**Soluzione alternativa**: verificare che i PC Windows 10 RTM abbiano almeno 4 GB di RAM disponibile prima di eseguire una cancellazione completa del dispositivo. Per visualizzare il numero di versione dei dispositivi Windows 10, immettere "winver" al prompt dei comandi. Se il dispositivo è già stato cancellato e non risponde, usare un'unità di avvio USB con Windows 10 per avviare e ripristinare l'accesso al dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Quando un utente appartiene a due o più raccolte di utenti in cui sono distribuiti criteri di termini e condizioni, l'utente visualizza più insiemi degli stessi termini  
<!-- 454394    -->
Quando un amministratore distribuisce un insieme di termini in più raccolte utente e un utente è membro di più di una di queste raccolte, tale utente visualizzerà più copie di termini identici all'apertura del portale aziendale.  Se, ad esempio, un utente denominato "UtenteEsempio" è un membro di due diverse raccolte di utenti, denominate "DipendentiAzienda1" e "DipendentiAzienda2" e i termini e le condizioni denominati "CondizioniAziendali" vengono distribuiti sia a DipendentiAzienda1 sia a DipendentiAzienda2, UtenteEsempio vedrà due set identici di CondizioniAziendali nella pagina di accettazione delle condizioni. Considerato che gli utenti possono solo accettare o rifiutare tutte le condizioni, non vi è alcun rischio di trovarsi in uno stato di accettazione ambiguo in cui l'utente ha sia accettato che rifiutato le condizioni. Il report di accettazione di termini e condizioni includerà una sola riga per ogni set di condizioni per ogni utente, quindi nel report non possono esserci errori. L'unico effetto riscontrato dall'utente è la visualizzazione di due insiemi di condizioni nella pagina di accettazione.  

**Soluzione alternativa**: assicurarsi che ogni utente sia incluso solo in solo una raccolta in cui vengono distribuite le condizioni.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>I profili di posta elettronica Android for Work che usano l'autenticazione del certificato non vengono applicati ai dispositivi
<!--  487657      -->
Quando si crea un profilo di posta elettronica Android for Work, per l'autenticazione sono disponibili due opzioni. La prima consiste nell'uso del nome utente e della password, l'altra nell'uso di certificati. A questo punto, l'opzione "certificati" non funziona. Se il profilo viene creato con il metodo di autenticazione impostato su **certificati**, tale profilo non viene applicato al dispositivo e all'utente verrà chiesto di immettere manualmente i dettagli dell'account di posta elettronica.

**SOLUZIONE ALTERNATIVA**: nessuna. Gli amministratori devono usare l'opzione **nome utente e password** o attendere fino alla risoluzione del problema.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>Non è possibile applicare i criteri antimalware in Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
Non è possibile applicare i criteri antimalware in Windows Server 2016 Core.  Codice di errore: 0x80070002.  Manca una dipendenza per ConfigSecurityPolicy.exe.

**Soluzione alternativa:** per risolvere questo problema, vedere l'[articolo 4019472 della Knowledge Base](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distribuito il 9 maggio 2017.


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>I criteri di Windows Defender Advanced Threat Protection generano un errore negli agenti client meno recenti.
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
I criteri di Windows Defender Advanced Threat Protection creati da Configuration Manager versione 1610 o successiva non vengono applicati a Configuration Manager versione 1606 e ai client precedenti.  I client non vengono caricati correttamente e viene generato un errore in fase di valutazione dei criteri. Lo **stato di distribuzione** nella configurazione di Windows Defender Advanced Threat Protection indica un **errore**.

**SOLUZIONE ALTERNATIVA**: aggiornare il client di Configuration Manager alla versione 1610 o successiva.
