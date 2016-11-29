---
title: Come creare elementi di configurazione per dispositivi Windows Phone gestiti senza il client System Center Configuration Manager | System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fae7f9e0-d5e7-422f-a6ed-6f6d73f6a617
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 26f1a3b1df544c66d22ede74673d6e890038fea4


---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione per dispositivi Windows Phone gestiti senza il client System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare l'elemento di configurazione **Windows Phone** di System Center Configuration Manager per gestire le impostazioni per i dispositivi Windows Phone registrati in Microsoft Intune o gestiti localmente da Configuration Manager.  
  
## <a name="create-a-windows-phone-configuration-item"></a>Creare un elemento di configurazione Windows Phone  
  
1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  
  
3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  
  
4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  
  
5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Windows Phone**.  
  
6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  
  
7.  Nella pagina **Piattaforme supportate** selezionare le piattaforme Windows Phone specifiche che valuteranno l'elemento di configurazione.  
  
8.  Nella pagina **Impostazioni dispositivo** selezionare il gruppo di impostazioni da configurare. Per i dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client#windows-phone-configuration-item-settings-reference) in questo argomento e quindi fare clic su **Avanti**.  
  
    > [!TIP]  
    >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  
  
9. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  
  
10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato nei report di Configuration Manager quando viene trovato un elemento di configurazione non conforme:  
  
    -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore.  
  
    -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni**.  
  
    -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso**.  
  
    -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico**.  
  
    -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico**.   
  
11. Nella pagina **Applicabilità piattaforma** verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  
  
    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  
  
12. Completare la procedura guidata.  
  
 È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione Windows Phone  
  
### <a name="password"></a>Password  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|La lunghezza minima della password.|  
|**Scadenza password in giorni**|Il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password usate in precedenza.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.|  
|**Complessità password**|Scegliere se è possibile specificare un PIN, ad esempio "1234", o se è necessario fornire una password complessa.|  
|**Invia PIN di ripristino password a Exchange Server**||  
  
### <a name="device"></a>Dispositivo  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Acquisizione schermo**|Consente all'utente di acquisire uno screenshot del display del dispositivo.<br /><br /> Solo Windows Phone 8.1.|  
|**Invio dati diagnostici**|Consente l’invio dei file di log dell'app.|  
|**Georilevazione**|Consente al dispositivo di usare le informazioni dei servizi di posizione.<br /><br /> Solo Windows Phone 8.1.|  
|**Copia e Incolla**|Usare Copia e Incolla per trasferire dati tra app.<br /><br /> Solo Windows Phone 8.1.|  
|**Bluetooth**|Consente di usare la funzionalità Bluetooth del dispositivo.|  
  
### <a name="email-management"></a>Gestione della posta elettronica  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Posta elettronica IMAP e POP**|Consente la connessione agli account di posta elettronica che usano gli standard POP e IMAP.|  
|**Tempo massimo di conservazione della posta elettronica**|Il tempo di conservazione della posta elettronica prima che venga eliminata dal server.|  
|**Formati messaggi consentiti**|Specificare se i messaggi di posta elettronica dell’utente possono essere in formato HTML o solo in testo normale.|  
|**Dimensione massima per la posta elettronica con testo normale (scaricata automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica con testo normale quando vengono scaricati automaticamente.|  
|**Dimensione massima per la posta elettronica HTML (scaricata automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica HTML quando vengono scaricati automaticamente.|  
|**Dimensione massima di un allegato (scaricato automaticamente)**|Controlla la dimensione massima dei messaggi di posta elettronica che verranno scaricati automaticamente.|  
|**Sincronizzazione calendario**||  
|**Account di posta elettronica personalizzato**|Consente di usare un account non Microsoft sul dispositivo.|  
|**Rendi l'account Microsoft facoltativo nell'applicazione Windows Mail**||  
  
### <a name="store"></a>Archivio  
 Queste impostazioni si applicano solo ai dispositivi Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Archivio applicazioni**|Consente l'accesso all'archivio applicazioni sul dispositivo.|  
|**Immettere una password per accedere all'archivio applicazioni**|Gli utenti devono immettere una password per accedere all'archivio applicazioni.|  
|**Acquisti in-app**|Consente agli utenti di effettuare acquisti in-app.|  
  
### <a name="browser"></a>Browser  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Browser predefinito**|È possibile modificare il browser Internet predefinito.|  
|**Riempimento automatico**|L’utente può modificare le impostazioni di completamento automatico nel browser.|  
|**Esecuzione script attivo**|Il browser può eseguire script, ad esempio gli script ActiveX.|  
|**Plug-in**|L’utente può aggiungere plug-in a Internet Explorer.|  
|**Blocco popup**|Attiva o disattiva il blocco popup del browser.|  
|**Cookie**|Consente il salvataggio dei cookie nel dispositivo.|  
|**Avviso frodi**|Attiva o disattiva gli avvisi di potenziali siti Web fraudolenti.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Invia sempre l'intestazione DNT (Do Not Track)**|Impedisce che le informazioni cercate vengano inviate a siti di terze parti.|  
|**Area di protezione Intranet**||  
|**Livello di protezione per l'area Internet**|Configurare il livello di protezione per l'area Internet.|  
|**Livello di protezione per l'area Intranet**|Configurare il livello di protezione per l'area intranet.|  
|**Livello di protezione per l'area siti attendibili**|Configurare il livello di protezione per l'area siti attendibili.|  
|**Livello di protezione per l'area siti con restrizioni**|Configurare il livello di protezione per l'area siti con restrizioni.|  
|**Spazi dei nomi per l'area intranet**||  
|**Accedi a un sito Intranet nel caso di immissione di una singola parola**|Abilita o disabilita l'impostazione che consente a Internet Explorer di passare automaticamente a un sito Intranet se viene immesso un nome di sito valido senza HTTP precedente:|  
|**Opzione di menu modalità Enterprise**|Consente agli utenti di attivare e disattivare la modalità Enterprise dal menu **Strumenti** di Internet Explorer.|  
|**Posizione report di registrazione (URL)**|Specificare un URL in cui verranno registrati i siti Web visitati quando è attiva la modalità Enterprise.|  
|**Posizione elenco siti modalità Enterprise (URL)**|Specificare il percorso dell'elenco di siti Web che useranno la modalità Enterprise quando è attiva.|  
  
### <a name="cloud"></a>Cloud  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Sincronizzazione impostazioni**|Consente la sincronizzazione delle impostazioni tra i dispositivi.|  
|**Sincronizzazione credenziali**|Consente la sincronizzazione delle credenziali tra i dispositivi.|  
|**Account Microsoft**|Consente di usare un account Microsoft sul dispositivo.<br /><br /> Solo Windows Phone 8.1.|  
|**Sincronizzazione delle impostazioni con connessione a consumo**|Consente la sincronizzazione delle impostazioni quando la connessione a Internet è a consumo.|  
  
### <a name="security"></a>Sicurezza  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Installazione file non firmati**|Consente il caricamento di file non firmati.|  
|**Applicazioni non firmate**|Consente il caricamento di file non firmati.|  
|**Messaggistica SMS e MMS**|Consente la messaggistica SMS e MMS dal dispositivo.|  
|**Archivi rimovibili**|Consente di utilizzare archivi rimovibili, ad esempio una scheda SD sul dispositivo.|  
|**Fotocamera**|Consente di utilizzare la fotocamera del dispositivo.|  
|**NFC (Near Field Communication)**|Consente la comunicazione usando NFD nel dispositivo.<br /><br /> Solo Windows Phone 8.1.|  
  
### <a name="peak-synchronization"></a>Sincronizzazione nelle ore di punta  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Specificare l'ora di punta**||  
|**Frequenza di sincronizzazione nelle ore di punta**||  
|**Frequenza di sincronizzazione nelle ore non di punta**||  
  
### <a name="roaming"></a>Roaming  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Gestione dispositivi mobili durante il roaming**|Consente la gestione del dispositivo con Configuration Manager in caso di roaming.|  
|**Download del software durante il roaming**|Consente il download di applicazioni e software durante il roaming.|  
|**Download della posta elettronica durante il roaming**|Consente il download di posta elettronica durante il roaming.|  
|**Roaming dati**|Consente il roaming tra reti quando si accede a dati.|  
  
### <a name="encryption"></a>Crittografia  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Crittografia scheda di memoria**|Richiede la crittografia delle schede di memoria usate con il dispositivo.|  
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file sul dispositivo mobile.|  
|**Richiedi firma posta elettronica**|Richiede la firma dei messaggi di posta elettronica prima dell'invio.|  
|**Algoritmo di firma**|Selezionare l'algoritmo usato per firmare i messaggi di posta elettronica.|  
|**Richiedi crittografia posta elettronica**|Richiede la crittografia dei messaggi di posta elettronica prima dell'invio.|  
|**Algoritmo di crittografia**|Selezionare l'algoritmo usato per crittografare i messaggi di posta elettronica.|  
  
###  <a name="wireless-communications"></a>Comunicazioni wireless  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Connessione rete wireless**|Abilita o disabilita la funzionalità Wi-Fi dei dispositivi.|  
|**Tethering Wi-Fi**|Consente agli utente di usare il proprio dispositivo come hotspot mobile.|  
|**Offload dei dati con Wi-Fi quando possibile**||  
|**Reporting hotspot Wi-Fi**||  
  
#### <a name="to-configure-a-wireless-network-connection"></a>Per configurare una connessione di rete wireless  
  
1.  Nella pagina **Configurare le impostazioni di comunicazione wireless per dispositivi mobili** fare clic su **Aggiungi**.  
  
2.  Nella finestra di dialogo **Connessione rete wireless** specificare le informazioni che seguono sulla connessione wireless che sarà disponibile nei dispositivi mobili, quindi fare clic su **OK**:

|Impostazioni|Altre informazioni|  
|-------------|----------------------|  
|**Nome rete (SSID)**||  
|**Connessione di rete**|Scegliere **Internet** o **Lavoro**.|  
|**Autenticazione**|Selezionare il metodo di autenticazione per la connessione:<br><br>- **Aperta**<br>-                    **Condivisa**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
|**Crittografia dei dati**|Scegliere il metodo di crittografia usato dalla connessione. I valori che è possibile selezionare variano a seconda del metodo di **Autenticazione** scelto:<br><br>- **Disabilitato**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
|**Indice chiavi**|Selezionare un indice chiavi da **1** a **4** da usare con l'impostazione di **Crittografia dei dati** **WEP**.|  
|**Questa rete è connessa a Internet**|Selezionare questa opzione se si desidera specificare le impostazioni proxy che consentono la connessione a Internet dei dispositivi mobili su una connessione wireless.|  
|**Impostazioni del server proxy**|Specificare le impostazioni **Server** e **Porta** necessarie per **HTTP**, **WAP** e **Socket**.|  
|**Abilita accesso alla rete 802.1X**|Selezionare questa opzione per proteggere la connessione specificando un tipo di EAP.|  
|**Tipo EAP**|Scegliere il tipo EAP da usare:<br><br>- **PEAP**<br>- **Smart card o certificato**|  

  
###  <a name="certificates"></a>Certificati  
 È opportuno importare certificati da installare nei dispositivi mobili.  
  
 Fare clic su **Importa**, quindi specificare i valori seguenti:  
  
-   **File di certificato** - fare clic su **Sfoglia** , quindi selezionare il file di certificato con estensione **cer** da importare.  
  
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
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Controllo dell'account utente**|Abilita o disabilita il controllo account utente di Windows sul dispositivo.|  
|**Firewall di rete**|Attiva o disattiva Windows Firewall.|  
|**Aggiornamenti**|Scegliere come gli aggiornamenti software di Windows verranno scaricati nel computer. Ad esempio, è possibile scaricare automaticamente gli aggiornamenti, ma consentire all'utente di scegliere quando installarli.|  
|**Classificazione minima degli aggiornamenti**|Scegliere la classificazione minima degli aggiornamenti che verranno scaricati nei computer Windows: **Nessuno**, **Importante**o **Consigliato**.|  
|**SmartScreen**|Abilita o disabilita SmartScreen.|  
|**Protezione da virus**|Verifica che il dispositivo sia protetto da software antivirus.|  
|**Le firme per la protezione da virus sono aggiornate**|Verifica che le firme del software antivirus siano aggiornate.|  
  
### <a name="windows-server-work-folders"></a>Cartelle di lavoro di Windows Server  
 Queste impostazioni si applicano a Windows Phone 8 e Windows Phone 8.1.  
  
|Impostazioni|Dettagli|  
|-------------|-------------|  
|**URL cartelle di lavoro**|Configura il percorso di una cartella di lavoro di Windows Server a cui gli utenti possono connettersi dal dispositivo.|  
  
### <a name="windows-phone-allowed-and-blocked-apps-list-windows-phone-81-only"></a>Elenco delle app consentite e bloccate in Windows Phone (solo Windows Phone 8.1)  
 Consente di specificare un elenco di app Windows Phone conformi o non conformi all'interno della società. Le app specificate come bloccate non possono essere installate dagli utenti. Se si specifica un elenco di app consentite, gli utenti potranno installare solo tali applicazioni.  
  
 Non è possibile specificare sia le app consentite che quelle bloccate nello stesso elemento di configurazione.  
  
> [!IMPORTANT]  
>  Se si specifica un elenco di app consentite, è necessario garantire che l'app del portale aziendale e tutte le altre app distribuite nei dispositivi Windows Phone 8.1 siano incluse nell'elenco **Consentito** .  
  
#### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Per specificare un elenco di app consentite o bloccate  
  
1.  Nella pagina **Elenco delle app consentite e bloccate (Windows Phone 8.1)** indicare le informazioni seguenti:  
  
|Impostazioni|Altre informazioni|  
|-|-|  
|**Elenco delle app bloccate**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti non sono autorizzati a installare.|  
|**Elenco delle app consentite**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti sono autorizzati a installare.|  
|**Aggiungi**|Aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.<br /><br /> Per specificare l'URL, nella pagina di Windows Phone Store cercare l'app da usare.<br /><br /> **Esempio:** cercare l'app **Skype** nello store. L'URL usato sarà http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Nel caso dell'app del portale aziendale o delle app line-of-business, non è necessario specificare un URL completo ma soltanto il GUID dell'app.|  
|**Modifica**|Consente di modificare il nome, l'autore e l'URL dell'app selezionata.|  
|**Rimuovi**|Elimina l'app selezionata dall'elenco.|  
|**Importaa**|Importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.|  
  




<!--HONumber=Nov16_HO1-->


