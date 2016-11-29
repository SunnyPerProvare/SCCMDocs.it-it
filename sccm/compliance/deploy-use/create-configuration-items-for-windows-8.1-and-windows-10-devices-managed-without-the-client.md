---
title: Creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client di System Center Configuration Manager | System Center Configuration Manager
description: Usare l'elemento di configurazione Windows 10 in System Center Configuration Manager per gestire le impostazioni dei computer Windows 10.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c262291a-80fe-47f3-a6d0-a605fe8b1f06
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84914426016c049de9bdf797b02bf0cc15301a71
ms.openlocfilehash: 1691fe56b9c6fb6aa6889a4451985a1bf6c2e1b5


---
# <a name="create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare l'elemento di configurazione **Windows 8.1 e Windows 10** di System Center Configuration Manager per gestire le impostazioni per i dispositivi Windows 8.1 e Windows 10 registrati in Microsoft Intune o gestiti localmente da Configuration Manager.  

## <a name="create-a-windows-81-and-windows-10-configuration-item"></a>Creare un elemento di configurazione Windows 8.1 e Windows 10  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Windows 8.1 e Windows 10**.  

6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

7.  Nella pagina **Piattaforme supportate** selezionare le piattaforme Windows specifiche che valuteranno l'elemento di configurazione.  

8.  Nella pagina **Impostazioni dispositivo** selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Windows 8.1 e Windows 10](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-81-and-windows-10-configuration-item-settings-reference) in questo argomento e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  

9. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  

10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato nei report di Configuration Manager quando viene trovato un elemento di configurazione non conforme:  

    -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore.  

    -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni**.  

    -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso**.  

    -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico**.  

    -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico**. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  

11. Nella pagina **Applicabilità piattaforma** verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  

    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  

12. Completare la procedura guidata.  

 È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  

##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Windows 8.1 e Windows 10  

### <a name="password"></a>Password  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 10 e versioni successive.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|La lunghezza minima della password.|  
|**Scadenza password in giorni**|Il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password usate in precedenza.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.|  
|**Tempo di inattività prima del blocco del dispositivo**|Specificare la quantità di tempo per cui un dispositivo può rimanere inattivo (senza input dell'utente) prima che venga bloccato.|  
|**Complessità password**|Scegliere se è possibile specificare un PIN, ad esempio "1234", o se è necessario fornire una password complessa.|  
|**Complessità password** - **Numero di set di caratteri complessi necessario in una password**|Se è stata scelta una password **complessa**, usare questa impostazione per configurare il numero di set di caratteri complessi necessari. Per ottenere una password complessa, il valore deve essere impostato almeno su **3**, ovvero sono necessari lettere e numeri. Selezionare **4** per imporre una password che richiede anche caratteri speciali, ad esempio **(% $**.|
|**Invia PIN di ripristino password a Exchange Server**|Impostare su **Abilitato** o **Disabilitato**.|  

###  <a name="device"></a>Dispositivo  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Acquisizione schermo**|Consente di acquisire uno screenshot del display del dispositivo.<br /><br /> (solo Windows 10)|  
|**Invio dati diagnostici (Windows 8.1 e versioni precedenti)**|Consente l’invio dei file di log dell'app.<br /><br /> (solo Windows 8.1)|  
|**Invio dati diagnostici (Windows 10)**|Consente l’invio dei file di log dell'app.|  
|**Georilevazione**|Consente al dispositivo di usare le informazioni dei servizi di posizione.<br /><br /> (solo Windows 10)|  
|**Copia e Incolla**|Usare Copia e Incolla per trasferire dati tra app.<br /><br /> (solo Windows 10)|  
|**Bluetooth**|Consente di utilizzare la funzionalità Bluetooth dei dispositivi.|  
|**Modalità individuabile Bluetooth**|Consente l'individuazione del dispositivo da altri dispositivi Bluetooth.<br /><br /> (solo Windows 10)|  
|**Annunci con Bluetooth**|Consentire l'uso di annunci con Bluetooth.<br /><br /> (solo Windows 10)|  
|**Registrazione vocale**|Consente l'uso delle funzionalità di registrazione vocale del dispositivo.<br /><br /> (solo Windows 10)|  

### <a name="email-management"></a>Gestione della posta elettronica  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Posta elettronica IMAP e POP**|Consente la connessione agli account di posta elettronica che usano gli standard POP e IMAP.|  
|**Tempo massimo di conservazione della posta elettronica**|Il tempo di conservazione della posta elettronica prima che venga eliminata dal server.|  
|**Formati messaggi consentiti**|Specificare se i messaggi di posta elettronica dell’utente possono essere in formato HTML o solo in testo normale.|  
|**Dimensione massima per la posta elettronica con testo normale (scaricata automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica con testo normale quando vengono scaricati automaticamente.|  
|**Dimensione massima per la posta elettronica HTML (scaricata automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica HTML quando vengono scaricati automaticamente.|  
|**Dimensione massima di un allegato (scaricato automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica che verranno scaricati automaticamente.|  
|**Sincronizzazione calendario**|Consentire la sincronizzazione dei calendari con il dispositivo.|  
|**Account di posta elettronica personalizzato**|Consente di usare un account non Microsoft sul dispositivo.|  
|**Rendi l'account Microsoft facoltativo nell'applicazione Windows Mail**|Configurare questa opzione per rimuovere il requisito per un account Microsoft in Windows Mail.|  

### <a name="store"></a>Archivio  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 10 e versioni successive.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Archivio applicazioni**|Consente l'accesso all'archivio applicazioni sul dispositivo.|  
|**Immettere una password per accedere all'archivio applicazioni**|Gli utenti devono immettere una password per accedere all'archivio applicazioni.|  
|**Acquisti in-app**|Consente agli utenti di effettuare acquisti in-app.|  

### <a name="browser"></a>Browser  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Consenti browser Web**|Consentire l'uso del Web browser nel dispositivo.|  
|**Riempimento automatico**|L’utente può modificare le impostazioni di completamento automatico nel browser.|  
|**Esecuzione script attivo**|Il browser può eseguire script, ad esempio gli script ActiveX.|  
|**Plug-in**|L’utente può aggiungere plug-in a Internet Explorer.|  
|**Blocco popup**|Attiva o disattiva il blocco popup del browser.|  
|**Cookie**|Consente il salvataggio dei cookie nel dispositivo.|  
|**Avviso frodi**|Attiva o disattiva gli avvisi di potenziali siti Web fraudolenti.|  

###  <a name="internet-explorer"></a>Internet Explorer  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Invia sempre l'intestazione DNT (Do Not Track)**|Impedisce che le informazioni cercate vengano inviate a siti di terze parti.|  
|**Area di protezione Intranet**|Assegnare un livello di sicurezza all'area di protezione Intranet.|  
|**Livello di protezione per l'area Internet**|Configurare il livello di protezione per l'area Internet.|  
|**Livello di protezione per l'area Intranet**|Configurare il livello di protezione per l'area intranet.|  
|**Livello di protezione per l'area siti attendibili**|Configurare il livello di protezione per l'area siti attendibili.|  
|**Livello di protezione per l'area siti con restrizioni**|Configurare il livello di protezione per l'area siti con restrizioni.|  
|**Spazi dei nomi per l'area intranet**|Configurare siti Web che verranno aggiunti o rimossi dall'area intranet.|  
|**Accedi a un sito Intranet nel caso di immissione di una singola parola**|Abilita o disabilita l'impostazione che consente a Internet Explorer di passare automaticamente a un sito Intranet se viene immesso un nome di sito valido senza HTTP precedente:|  
|**Opzione di menu modalità Enterprise**|Consente agli utenti di attivare e disattivare la modalità Enterprise dal menu **Strumenti** di Internet Explorer.|  
|**Posizione report di registrazione (URL)**|Specificare un URL in cui verranno registrati i siti Web visitati quando è attiva la modalità Enterprise.|  
|**Posizione elenco siti modalità Enterprise (URL)**|Specificare il percorso dell'elenco di siti Web che useranno la modalità Enterprise quando è attiva.|  

###  <a name="cloud"></a>Cloud  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Sincronizzazione impostazioni**|Consente la sincronizzazione delle impostazioni tra i dispositivi.|  
|**Sincronizzazione credenziali**|Consente la sincronizzazione delle credenziali tra i dispositivi.|  
|**Account Microsoft**|Consente di usare un account Microsoft sul dispositivo.|  
|**Sincronizzazione delle impostazioni con connessione a consumo**|Consente la sincronizzazione delle impostazioni quando la connessione a Internet è a consumo.|  

###  <a name="security"></a>Sicurezza  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Installazione file non firmati**|Consente il caricamento di file non firmati.<br /><br /> (solo Windows 10)|  
|**Applicazioni non firmate**|Consente il caricamento di file non firmati.<br /><br /> (solo Windows 10)|  
|**Messaggistica SMS e MMS**|Consente la messaggistica SMS e MMS dal dispositivo.<br /><br /> (solo Windows 10)|  
|**Archivi rimovibili**|Consente di utilizzare archivi rimovibili, ad esempio una scheda SD sul dispositivo.<br /><br /> (solo Windows 10)|  
|**Fotocamera**|Consente di utilizzare la fotocamera del dispositivo.<br /><br /> (solo Windows 10)|  
|**NFC (Near Field Communication)**|Consente la comunicazione usando NFD nel dispositivo.<br /><br /> (solo Windows 10)|  
|**Modalità AntiTheft**|Controlla se è abilitata la modalità AntiTheft di Windows 10.<br /><br /> (solo Windows 10)|  
|**Tipo profilo**|Fornice un profilo VPN per i dispositivi Windows RT.<br /><br /> (solo Windows 8.1)|  
|**Nome profilo**|Fornice un profilo VPN per i dispositivi Windows RT.<br /><br /> (solo Windows 8.1)|  
|**Profilo per tutti gli utenti**|Fornice un profilo VPN per i dispositivi Windows RT.<br /><br /> (solo Windows 8.1)|  

###  <a name="peak-synchronization"></a>Sincronizzazione nelle ore di punta  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 10 e versioni successive.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Specificare l'ora di punta**|Configurare le ore di punta per la sincronizzazione del dispositivo mobile.|  
|**Frequenza di sincronizzazione nelle ore di punta**|Configurare la frequenza con cui viene eseguita la sincronizzazione durante le ore di picco configurate.|  
|**Frequenza di sincronizzazione nelle ore non di punta**|Configurare la frequenza con cui viene eseguita la sincronizzazione fuori dalle ore di picco configurate.|  

###  <a name="roaming"></a>Roaming  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Gestione dispositivi mobili durante il roaming**|Consente la gestione del dispositivo con Configuration Manager in caso di roaming.<br /><br /> (solo Windows 10)|  
|**Download del software durante il roaming**|Consente il download di applicazioni e software durante il roaming.<br /><br /> (solo Windows 10)|  
|**Download della posta elettronica durante il roaming**|Consente il download di posta elettronica durante il roaming.<br /><br /> (solo Windows 10)|  
|**Roaming dati**|Consente il roaming tra reti quando si accede a dati.|  

###  <a name="encryption"></a>Crittografia  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Crittografia scheda di memoria**|Richiede la crittografia delle schede di memoria usate con il dispositivo.<br /><br /> (solo Windows 10)|  
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file nel dispositivo.|  
|**Richiedi firma posta elettronica**|Richiede che i messaggi di posta elettronica vengano firmati prima dell'invio.|  
|**Algoritmo di firma**|Selezionare l'algoritmo di firma per i messaggi di posta elettronica firmati.|  
|**Richiedi crittografia posta elettronica**|Richiede che i messaggi di posta elettronica vengano crittografati prima dell'invio.|  
|**Algoritmo di crittografia**|Selezionare l'algoritmo per la crittografia dei messaggi di posta elettronica.|  

###  <a name="wireless-communications"></a>Comunicazioni wireless  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 10 e versioni successive.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Connessione rete wireless**|Abilita o disabilita la funzionalità Wi-Fi dei dispositivi.|  
|**Tethering Wi-Fi**|Consente agli utenti di usare il proprio dispositivo come hotspot mobile.|  
|**Offload dei dati con Wi-Fi quando possibile**|Configurare questa opzione in modo da usare la connessione Wi-Fi nel dispositivo quando possibile.|  
|**Reporting hotspot Wi-Fi**||  
|**Configurazione Wi-Fi manuale**||  

#### <a name="to-configure-a-wireless-network-connection"></a>Per configurare una connessione di rete wireless  

1.  Nella pagina **Configurare le impostazioni di comunicazione wireless per dispositivi mobili** fare clic su **Aggiungi**.  

2.  Nella finestra di dialogo **Connessione rete wireless** , specificare le informazioni seguenti sulla connessione wireless che sarà fornita nei dispositivi mobili:  

    |Impostazioni|Altre informazioni|  
    |-------------|----------------------|  
    |**Nome rete (SSID)**|Immettere il nome della rete Wi-Fi.|  
    |**Connessione di rete**|Scegliere **Internet** o **Lavoro**.|  
    |**Autenticazione**|Selezionare il metodo di autenticazione per la connessione:<br>- **Aperta**<br>-                             **Condivisa**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
    |**Crittografia dei dati**|Scegliere il metodo di crittografia usato dalla connessione. I valori che è possibile selezionare variano a seconda del metodo di **Autenticazione** scelto:<br>- **Disabilitato**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
    |**Indice chiavi**|Selezionare un indice chiavi da **1** a **4** da usare con l'impostazione di **Crittografia dei dati** **WEP**.|  
    |**Questa rete è connessa a Internet**|Selezionare questa opzione se si desidera specificare le impostazioni proxy che consentono la connessione a Internet dei dispositivi mobili su una connessione wireless.|  
    |**Impostazioni del server proxy**|Specificare le impostazioni **Server** e **Porta** necessarie per **HTTP**, **WAP** e **Socket**.|  
    |**Abilita accesso alla rete 802.1X**|Selezionare questa opzione per proteggere la connessione specificando un tipo di EAP.|  
    |**Tipo EAP**|Scegliere il tipo EAP da usare:<br>- **PEAP**<br>- **Smart card o certificato**|  

3.  Al termine, fare clic su **OK**.  

### <a name="certificates"></a>Certificati  
 Consente di importare certificati da installare nei dispositivi mobili.  

 Fare clic su **Importa**, quindi specificare i valori seguenti:  

-   **File di certificato** - Fare clic su Sfoglia e quindi selezionare il file di certificato con estensione **cer** che si vuole importare.  

-   **Archivio di destinazione** - Scegliere uno o più archivi di destinazione da cui sarà aggiunto il certificato importato sul dispositivo mobile:  

    -   **Radice**  

    -   **CA**  

    -   **Normale**  

    -   **Con privilegi**  

    -   **SPC**  

    -   **Peer**  

-   **Ruolo** - se **SPC** (Certificato autori software) viene selezionato come archivio di destinazione, scegliere il ruolo che verrà associato al certificato:  

    -   **Operatore di telefonia mobile**  

    -   **Gestore**  

    -   **Autenticazione utente**  

    -   **Amministratore IT**  

    -   **Utente non autenticato**  

    -   **Server di provisioning attendibile**  

### <a name="system-security"></a>Protezione del sistema  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Controllo dell'account utente**|Abilita o disabilita il controllo account utente di Windows sul dispositivo.|  
|**Firewall di rete**|Attiva o disattiva Windows Firewall.<br /><br /> (solo Windows 8.1)|  
|**Aggiornamenti (Windows 8.1 e versioni precedenti)**|Scegliere come gli aggiornamenti software di Windows verranno scaricati nel computer. Ad esempio, è possibile scaricare automaticamente gli aggiornamenti, ma consentire all'utente di scegliere quando installarli.|  
|**Classificazione minima degli aggiornamenti**|Scegliere la classificazione minima degli aggiornamenti che verranno scaricati nei computer Windows: **Nessuno**, **Importante**o **Consigliato**.|  
|**Aggiornamenti (Windows 10)**|Scegliere come gli aggiornamenti software di Windows verranno scaricati nel computer. Ad esempio, è possibile scaricare automaticamente gli aggiornamenti, ma consentire all'utente di scegliere quando installarli.<br /><br /> (solo Windows 10)|  
|**Giorno di installazione**|Scegliere il giorno in cui verranno installati gli aggiornamenti.<br /><br /> (solo Windows 10)|  
|**Ora di installazione**|Scegliere l'ora in cui verranno installati gli aggiornamenti.<br /><br /> (solo Windows 10)|  
|**SmartScreen**|Abilita o disabilita SmartScreen.|  
|**Protezione da virus**|Selezionare questa opzione per fare in modo che nel dispositivo sia installato un software antivirus.|  
|**Le firme per la protezione da virus sono aggiornate**|Selezionare questa opzione per fare in modo che i file delle firme antivirus siano aggiornati.|  
|**Funzionalità di versioni non definitive**|Consente a Microsoft di distribuire le impostazioni e le funzionalità della versione non definitiva nel dispositivo.<br /><br /> (solo Windows 10)|  
|**Installazione manuale del certificato radice**|(solo Windows 10)|  

###  <a name="windows-server-work-folders"></a>Cartelle di lavoro di Windows Server  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 8.1 e Windows 10.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**URL cartelle di lavoro**|Configura il percorso di una cartella di lavoro di Windows Server a cui gli utenti possono connettersi dal dispositivo.|  

### <a name="allowed-and-blocked-apps-windows-phone-only"></a>App consentite e bloccate (solo Windows Phone)  
 Consente di specificare un elenco di app gestite da Intune conformi oppure non conformi nella società. Windows Phone può consentire o bloccare l'installazione di queste applicazioni.  

 Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  

#### <a name="to-specify-apps-that-will-be-allowed-or-blocked"></a>Per specificare le app che saranno consentite o bloccate  

1.  Nella pagina **Elenco app consentite e bloccate** indicare le informazioni seguenti:  

    |Impostazioni|Altre informazioni|  
    |-------------|----------------------|  
    |**Elenco delle app bloccate**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti non sono autorizzati a installare.|  
    |**Elenco delle app consentite**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti sono autorizzati a installare. L'installazione di qualsiasi altra app verrà bloccata.|  
    |**Aggiungi**|Aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.<br /><br /> Per specificare l'URL, cercare l'app da usare nel Windows Store.<br /><br /> Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app consentite o bloccate.<br /><br /> **Esempio:** cercare l'app **Skype** nell'App Store. L'URL usato sarà**http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Modifica**|Consente di modificare il nome, l'autore e l'URL dell'app selezionata.|  
    |**Rimuovi**|Elimina l'app selezionata dall'elenco.|  
    |**Importaa**|Importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.|  

### <a name="windows-10-team"></a>Windows 10 Team  
 Queste impostazioni si riferiscono solo ai dispositivi che eseguono Windows 10 Team.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Consenti la riattivazione automatica dello schermo quando i sensori rilevano la presenza di qualcuno nella stanza**|Consente di riattivare automaticamente il dispositivo quando il sensore rileva la presenza di qualcuno nella stanza.|  
|**PIN obbligatorio per proiezione wireless**|Specifica se immettere un PIN prima di usare le funzionalità di proiezione wireless del dispositivo.|  
|**Finestra di manutenzione**|Configura la finestra durante la quale cui è possibile eseguire gli aggiornamenti del dispositivo. È possibile configurare l'ora di inizio della finestra e la durata (tra 1 e 5 ore).|  

### <a name="microsoft-edge"></a>Microsoft Edge  
 Queste impostazioni si riferiscono ai dispositivi che eseguono Windows 10 e versioni successive.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Consenti suggerimenti di ricerca nella barra degli indirizzi**|Consente al motore di ricerca di suggerire siti durante la digitazione delle frasi di ricerca.|  
|**Consenti l'invio di traffico Intranet a Internet Explorer**||  
|**Consenti Do Not Track**|Do Not Track informa i siti Web che non si vuole tenere traccia della visita a un sito.|  
|**Abilita SmartScreen**|Usare SmartScreen per controllare che i file scaricati dagli utenti non contengano codice dannoso.|  
|**Consenti popup**|Consentire o disabilitare i popup del browser.|  
|**Consenti cookie**|Consentire o disabilitare i cookie.|  
|**Consenti riempimento automatico**|Consente l'uso della funzionalità di riempimento automatico del browser Edge.|  
|**Consenti strumento per la gestione delle password**|Consentire l'uso della funzionalità dello strumento per la gestione delle password del browser Edge.|  
|**Posizione elenco siti modalità Enterprise**|Specifica dove trovare l'elenco di siti Web che verranno aperti in modalità Enterprise. L'elenco non è modificabile dagli utenti.|  

### <a name="windows-information-protection-formerly-enterprise-data-protection"></a>Windows Information Protection (noto in precedenza come Enterprise Data Protection)

Con l'aumento dei dispositivi personali nell'organizzazione, aumenta anche il rischio di perdita accidentale dei dati tramite app e servizi, ad esempio posta elettronica, social media e cloud pubblico, non controllati dall'organizzazione. È il caso, ad esempio, di un dipendente che invia le immagini di progettazione più recenti dall'account di posta elettronica personale, copia e incolla le informazioni su un prodotto in un tweet o salva il report di una vendita in corso nell'area di archiviazione nel cloud pubblico.

Windows Information Protection (WIP) offre protezione da questa potenziale perdita di dati senza interferire con l'esperienza del dipendente. Consente anche di proteggere le app e i dati aziendali da perdite di dati accidentali su dispositivi di proprietà dell'azienda e dispositivi personali che i dipendenti portano al lavoro senza richiedere modifiche all'ambiente o ad altre app.

 Gli elementi di configurazione di WIP gestiscono l'elenco di app protette da WIP, i percorsi di rete aziendali, il livello di protezione e le impostazioni di crittografia.

Per informazioni su come configurare la protezione dati con Configuration Manager, vedere [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).



<!--HONumber=Nov16_HO1-->

