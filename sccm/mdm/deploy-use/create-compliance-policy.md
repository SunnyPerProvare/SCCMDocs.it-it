---
title: "Creare e distribuire criteri di conformità del dispositivo | Microsoft Docs"
description: "Informazioni su come creare e distribuire criteri di conformità del dispositivo in System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 6832bb6c6a26be76720938154942a5eb99022785
ms.lasthandoff: 03/27/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Creare e distribuire criteri di conformità del dispositivo

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Creare i criteri di conformità

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, quindi fare clic su **Criteri di conformità**.

3. Nel gruppo **Crea** della scheda **Home** fare clic su **Crea criterio di conformità**.

4. Nella pagina **Generale** della **Creazione guidata criterio di conformità**, specificare le seguenti informazioni:

  * **Nome**: immettere un nome univoco per il criterio di conformità. È possibile usare un massimo di 256 caratteri.
  * **Descrizione**: inserire una descrizione che offra una panoramica del profilo VPN e altre informazioni rilevanti per facilitarne l'identificazione nella console di Configuration Manager. È possibile usare un massimo di 256 caratteri.
  * **Tipo di criterio di conformità**: selezionare il tipo di criteri che si vuole creare a seconda che il dispositivo sia o meno gestito da Configuration Manager. **Si applica alla versione  o versioni successive**.<br /><br /> Per i dispositivi gestiti da Intune, scegliere l'opzione **Regole di conformità per i dispositivi gestiti senza il client di Configuration Manager** .  Quando si seleziona questa opzione, è anche possibile selezionare il tipo di piattaforma a cui si vuole applicare il criterio.
  * **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato se i criteri di conformità vengono valutati come non conformi. I livelli di gravità disponibili sono i seguenti:<br /><br />
    * **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.
    *  **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni** per i report di Configuration Manager.   
    * **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso** per i report di Configuration Manager.
    * **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager.
    * **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.|      

5.  Nella pagina **Piattaforme supportate** selezionare le piattaforme del dispositivo che verranno valutate dal criterio di conformità oppure selezionare **Seleziona tutto** per selezionare tutte le piattaforme del dispositivo. Le piattaforme supportate sono Windows 7, 8.1, 10, Windows Server 2008 R2, 2012, 2012 R2 e 2016.

6.  Nella pagina **Regole** , indicare una o più regole che definiscono la configurazione che i dispositivi devono possedere per essere ritenuti conformi. Quando si crea un criterio di conformità, alcune regole vengono attivate per impostazione predefinita. Tuttavia, è possibile modificarle o eliminarle. Per un elenco completo di tutte le regole, vedere la sezione **Regole dei criteri di conformità** più avanti in questo argomento.

> [!NOTE]  
>  In PC Windows la versione 8.1 del sistema operativo Windows verrà indicata come 6.3.    Se la regola della versione del sistema operativo è impostata su Windows 8.1 per Windows, il dispositivo risulterà non conforme anche se il sistema operativo installato è Windows 8.1. Assicurarsi di impostare la versione **restituita** corretta per le regole della versione minima e massima del sistema operativo Windows. Il numero di versione deve corrispondere alla versione restituita dal comando winver. Il problema non riguarda i dispositivi Windows Phone perché la versione restituita è la 8.1, come previsto. Per i PC Windows con sistema operativo Windows 10, la versione deve essere impostata come "10.0" + il numero di build del sistema operativo restituito dal comando **winver**.

7.  Nella pagina **Riepilogo** della procedura guidata, rivedere le impostazione regolate, quindi completare la procedura.

 Il nuovo criterio viene visualizzato nel nodo **Criteri di conformità** dell'area di lavoro **Asset e conformità** .

## <a name="deploy-a-compliance-policy"></a>Distribuire i criteri di conformità

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, quindi fare clic su **Criteri di conformità**.

3.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.

4.  Nella finestra di dialogo **Distribuisci criteri di conformità** , fare clic su **Sfoglia** per selezionare la raccolta utente a cui distribuire il criterio.

     È anche possibile selezionare le opzioni per creare avvisi da inviare quando il criterio non è conforme. È anche possibile configurare la pianificazione in base alla quale verrà valutata la conformità del criterio.

5.  Al termine, fare clic su **OK**.

## <a name="monitor-the-compliance-policy"></a>Monitorare i criteri di conformità

### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Per visualizzare i risultati di conformità nella console di Configuration Manager

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Distribuzioni**.

3.  Nell'elenco **Distribuzioni** selezionare la distribuzione del criterio di conformità di cui si vogliono esaminare le informazioni sulla conformità.

4.  È possibile esaminare le informazioni di riepilogo sulla conformità della distribuzione del criterio nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione e quindi nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Visualizza stato** per aprire il riquadro **Stato distribuzione** .

     La pagina **Stato distribuzione** contiene le seguenti schede:

    -   **Conforme**: visualizza la conformità del criterio in base al numero degli asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o i dispositivi conformi a questa regola. Il riquadro **Dettagli asset** visualizza utenti o dispositivi che sono conformi al criterio. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive.

    -   **Errore**: visualizza un elenco di tutti gli errori relativi alla distribuzione del criterio, in base al numero di asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o tutti i dispositivi che hanno generato errori con questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema selezionato. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive sul problema.

    -   **Non conforme**: visualizza un elenco di tutte le regole non conformi all'interno di un criterio, in base al numero di asset interessati. È possibile fare clic su una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contiene tutti gli utenti o i dispositivi non conformi a questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema selezionato. Fare doppio clic su un utente o su un dispositivo presente nell'elenco per visualizzare informazioni aggiuntive sul problema.

    -   **Sconosciuto**: visualizza un elenco di tutti gli utenti o di tutti i dispositivi che non sono conformi alla distribuzione del criterio selezionata e lo stato del client dei dispositivi.

### <a name="to-monitor-the-individual-compliance-status"></a>Per monitorare lo stato di conformità dei singoli dispositivi

È anche possibile visualizzare lo stato dei singoli dispositivi:

1.  Nella console di Configuration Manager fare clic sull'area di lavoro **Asset e conformità**.

2.  Fare clic su **Dispositivi**.
3.  Fare clic con il pulsante destro del mouse su una delle colonne per abilitare altre colonne.

È possibile aggiungere le colonne seguenti:

- **ID dispositivo di Azure Active Directory**: identificatore univoco del dispositivo in AAD.

- **Dettagli dell'errore conformità**: dettagli del messaggio di errore quando il processo end-to-end ha esito negativo. Se questa colonna è vuota, significa che non sono stati rilevati errori ed è stato segnalato lo stato di conformità.

- **Posizione dell'errore di conformità**: fornisce altri dettagli sulla posizione in cui è stato rilevato lo stato di non conformità. Se questa colonna è vuota, significa che non sono stati rilevati errori ed è stato segnalato lo stato di conformità. Esempi della posizione in cui il processo di conformità può restituire un errore: 
    - Client di ConfigMgr
    - Punto di gestione
    - Intune
    - Azure Active Directory
<br></br>
- **Ora della valutazione della conformità**: ora dell'ultima verifica di conformità.

- **Impostazione ora per la conformità**: ora dell'ultimo aggiornamento della conformità in Azure Active Directory.

- **Conforme all'accesso condizionale**: indica se il computer è conforme ai criteri di accesso condizionale.

> [!IMPORTANT]
> Queste colonne non vengono visualizzate per impostazione predefinita.

### <a name="to-view-intune-compliance-policies-charts"></a>Per visualizzare i grafici dei criteri di conformità di Intune
1. A partire dalla versione 1610 di Configuration Manager, nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** passare a **Panoramica** > **Impostazioni di conformità** >  **Criteri di conformità**.
3. Vengono visualizzati i grafici seguenti:
    - **Overall Device Compliance** (Conformità generale del dispositivo): visualizza la conformità generale dei dispositivi per tutti i criteri di conformità.
    - **Top Non-Compliance Reasons** (Motivi principali di mancata conformità): visualizza i criteri principali alla base della mancata conformità dei dispositivi.
4. Fare clic su una sezione di uno dei due grafici per eseguire il drill-down nell'elenco dei dispositivi della categoria corrispondente.

### <a name="to-view-a-health-attestation-report"></a>Per visualizzare il report di attestazione dell'integrità

1.  **A partire dalla versione 1602 di Configuration Manager**, nella console di Configuration Manager, fare clic su **Monitoraggio**.

2.  Per visualizzare un report di riepilogo dello stato corrente dei dispositivi in base alla conformità, fare clic su **Sicurezza**. Quindi fare clic su **Attestazione dell'integrità**.

3.  Per visualizzare un report contenente l'elenco di tutti i dispositivi e tutti gli attributi di attestazione dell'integrità, fare clic su **Sicurezza**. Quindi fare clic su **Attestazione dell'integrità**.

## <a name="compliance-policy-rules"></a>Regole dei criteri di conformità
* **Richiedi impostazioni password nei dispositivi mobili**: richiede agli utenti di immettere una password per poter accedere al dispositivo.

  **Supportato in:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
* **Richiedi una password per sbloccare un dispositivo inattivo (aggiornamento 1602):** richiede agli utenti di immettere una password per poter accedere al dispositivo bloccato.

  **Supportato in:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minuti di inattività prima che venga richiesta la password (aggiornamento 1602):** Specifica il tempo di inattività prima che l'utente debba immettere nuovamente la password. Impostare il valore su una delle opzioni disponibili: **1 minuto**, **5 minuti**, **15 minuti**, **30 minuti**, **1 ora**.

  Questa regola deve essere usata con **Richiedi una password per sbloccare un dispositivo inattivo**. Il valore impostato qui determina i casi in cui il dispositivo è considerato inattivo e viene bloccato e se la regola  **Richiedi una password per sbloccare un dispositivo inattivo** è impostata su **True**, verrà quindi richiesto all'utente di immettere una password per accedere al dispositivo bloccato.

  **Supportato in:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Richiedi aggiornamenti automatici (aggiornamento 1602):** è possibile richiedere ai dispositivi con Windows 8.1 o versioni successive di installare automaticamente gli aggiornamenti e di specificare la classe degli aggiornamenti.

  Il valore deve essere impostato su **Nessuno** per impedire l'installazione automatica, su **Consigliati** per installare automaticamente tutti gli aggiornamenti consigliati o su **Importanti** per installare solo gli aggiornamenti classificati come importanti.

  **Supportato in:**
  * Windows Phone 8+

* **Consenti password semplici:** consente agli utenti di creare password semplici come "1234" o "1111". Per impostazione predefinita, questa impostazione è **disabilitata**.

  **Supportato in:**
  * Windows Phone 8+
  * iOS 6+

* **Lunghezza minima password:** Specifica il numero minimo di cifre o caratteri che la password dell'utente deve contenere (**6** per impostazione predefinita).

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  >[!NOTE]
  >Per i dispositivi che eseguono Windows e sono protetti con un account Microsoft, i criteri di conformità non eseguono correttamente la convalida se **Lunghezza minima password** contiene più di otto caratteri e **Numero minimo di set di caratteri** più di due.

* **Crittografia file nel dispositivo mobile:** Richiede la crittografia del dispositivo per la connessione alle risorse. I dispositivi che eseguono **Windows Phone 8** sono **crittografati automaticamente**. I dispositivi che eseguono **iOS** vengono crittografati quando si configura l'impostazione **Richiedi impostazioni password nei dispositivi mobili** (abilitata per impostazione predefinita).

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Il dispositivo non deve essere jailbroken o rooted:** se abilitata, i dispositivi jailbroken (iOS) o rooted (Android) non risultano conformi (disattivata per impostazione predefinita).

  **Supportato in:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Il profilo di posta elettronica deve essere gestito da Intune:**quando questa opzione è impostata su Sì, il dispositivo deve usare il profilo di posta elettronica distribuito al dispositivo. Il dispositivo viene considerato non conforme se il profilo di posta elettronica non viene distribuito allo stesso gruppo di utenti a cui si applicano i criteri di conformità.

  Il dispositivo risulta non conforme anche se l'utente ha già configurato un account di posta elettronica nel dispositivo che corrisponde a un profilo di posta elettronica di Intune distribuito al dispositivo. In questo caso, Intune non può sovrascrivere il profilo con provisioning dell'utente, quindi non può gestirlo. L'utente può portare il dispositivo in conformità rimuovendo le impostazioni di posta elettronica esistenti, consentendo quindi a Intune di installare il profilo di posta elettronica gestito.

  Per consultare dettagli sui profili di posta elettronica, vedere [Consentire l'accesso alla posta elettronica aziendale usando profili di posta elettronica con Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Per impostazione predefinita, questa impostazione è disabilitata.

  **Supportato in:**
  * iOS 6+

* **Profilo di posta elettronica:** Se **L'account di posta elettronica deve essere gestito da Intune** è selezionato, fare clic su **Seleziona** per scegliere il profilo di posta elettronica da cui gestire i dispositivi. Il profilo di posta elettronica deve essere presente nel dispositivo.

  **Supportato in:**
  * iOS 6+

* **Versione minima richiesta del sistema operativo:** quando un dispositivo non soddisfa il requisito relativo alla versione minima del sistema operativo, verrà segnalato come non conforme e verrà visualizzato un collegamento con informazioni su come eseguire l'aggiornamento. L'utente finale può scegliere di aggiornare il dispositivo e dopo l'aggiornamento potrà accedere alle risorse aziendali.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Versione massima consentita del sistema operativo**: quando un dispositivo usa una versione del sistema operativo successiva rispetto a quella specificata nella regola, l'accesso alle risorse aziendali risulterà bloccato e l'utente dovrà contattare l'amministratore IT. Fino a quando la regola non viene modificata in modo da consentire la versione del sistema operativo, non è possibile usare questo dispositivo per accedere alle risorse aziendali.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
* **Richiedi che i dispositivi siano riportati come integri (aggiornamento 1602):** è possibile impostare una regola per richiedere che i dispositivi Windows 10 vengano segnalati come integri in criteri di conformità nuovi o esistenti. Se questa impostazione è abilitata, i dispositivi Windows 10 verranno valutati tramite il servizio di attestazione dell'integrità riguardo ai punti dati seguenti:
 - **BitLocker è attivato:** quando Bitlocker è attivato, il dispositivo può proteggere dall'accesso non autorizzato i dati archiviati nell'unità, quando il sistema viene spento o passa alla modalità di ibernazione.

   Crittografia unità BitLocker di Windows crittografa tutti i dati archiviati nel volume del sistema operativo Windows. BitLocker usa il TPM per proteggere il sistema operativo Windows e i dati utente e contribuisce a evitare che il computer venga manomesso, anche se viene lasciato incustodito o se viene smarrito o rubato.<br />Se il computer è dotato di un TPM compatibile, BitLocker usa il TPM per bloccare le chiavi di crittografia che proteggono i dati. Di conseguenza, non è possibile accedere alle chiavi finché il TPM non ha verificato lo stato del computer.
  - **L'integrità del codice è abilitata:** la funzionalità Integrità del codice convalida l'integrità di un driver o di un file system ogni volta che viene caricato nella memoria. Questa funzionalità rileva se viene caricato nel kernel un driver o un file system non firmato o se un file system è stato modificato da software dannoso eseguito da un account utente con privilegi di amministratore.
  - **L'avvio protetto è abilitato:** quando la funzionalità Avvio protetto è abilitata, viene forzato l'avvio del sistema in uno stato attendibile predefinito. Inoltre, i componenti di base usati per avviare il computer devono avere le firme di crittografia corrette ritenute attendibili dall'organizzazione che ha prodotto il dispositivo. Il firmware UEFI verifica questo aspetto prima di permettere l'avvio del computer. Se uno o più file sono stati manomessi, danneggiandone la firma, il sistema non viene avviato.
  - **La funzionalità antimalware ad esecuzione anticipata è abilitata (l'impostazione si applica solo ai PC):** la funzionalità antimalware ad esecuzione anticipata offre protezione per i computer in rete quando vengono avviati e prima dell'inizializzazione di driver di terze parti.<br />Questa regola è disattivata per impostazione predefinita.

  Per informazioni sul funzionamento del servizio di attestazione dell'integrità, vedere l'argomento relativo al [provider di servizi di configurazione HealthAttestation](https://msdn.microsoft.com/library/dn934876.aspx).
  **Supportato in:**
  * Windows 10 e Windows 10 Mobile

- **App che non possono essere installate nel dispositivo**: se gli utenti installano un'app dall'elenco di app non conformi per l'amministratore, l'installazione viene bloccata quando cercano di accedere alla posta elettronica aziendale o ad altre risorse aziendali che supportano l'accesso condizionale. Questa regola richiede il nome e l'ID dell'app quando si aggiunge un'app all'elenco di app non conformi definito dall'amministratore. È possibile aggiungere anche l'autore dell'app, ma non è obbligatorio.
    - **Supportato in:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+

#### <a name="whats-app-id"></a>Che cos'è l'ID dell'app?

L'ID dell'app è un identificatore che identifica in modo univoco l'app all'interno dei servizi per applicazioni di Apple e Google, ad esempio com.contoso.myapp.

#### <a name="find-app-ids"></a>Trovare gli ID delle app

- **Android**
    - È possibile trovare l'ID di un'app nell'URL di Google Play Store usato per creare l'app:
        - Esempio di ID dell'app: ***…?id=com.nomeazienda.nomeapp&hl=en***

- **iOS**
    - Nell'URL di iTunes Store individuare il numero di ID (**ID#**), ad esempio: ***/id875948587?mt=8***
    - In un Web browser passare all'URL seguente, sostituendo il numero con il numero di ID trovato: 
        - https://itunes.apple.com/lookup?id=875948587
    - Scaricare e aprire il file di testo
    - Cercare il testo *bundleid*
    - Esempio di ID dell'app: "*bundleId*":"*com.nomeazienda.nomeapp*" 


