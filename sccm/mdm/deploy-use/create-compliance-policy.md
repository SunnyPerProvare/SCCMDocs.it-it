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
ms.translationtype: Human Translation
ms.sourcegitcommit: 216d288aa7b7f2b98df86f59355d879366dcd44d
ms.openlocfilehash: 4baa6e0fe009f5f7dc33f5ab4adb1ec5e5c5271b
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---

# <a name="create-and-deploy-a-device-compliance-policy"></a>Creare e distribuire criteri di conformità del dispositivo

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Creare i criteri di conformità

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e scegliere**Criteri di conformità**.

3.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea criteri di conformità**.

4.  Nella pagina **Generale** della Creazione guidata criteri di conformità specificare le informazioni seguenti:

  * **Nome**. Immettere un nome univoco per il criterio di conformità. Non può superare i 256 caratteri.

  * **Descrizione**. Immettere una descrizione che offra una panoramica del profilo VPN e che consenta di facilitarne l'identificazione nella console di Configuration Manager. Non può superare i 256 caratteri.

  * **Tipo di criteri di conformità**. Selezionare il tipo di criteri che si vuole creare a seconda che il dispositivo sia o meno gestito da Configuration Manager. Si applica alla versione o alle versioni successive.<br /><br /> Per i dispositivi gestiti da Intune, scegliere l'opzione **Regole di conformità per i dispositivi gestiti senza il client di Configuration Manager** . Quando si seleziona questa opzione, è anche possibile selezionare il tipo di piattaforma alla quale applicare i criteri.

  * **Gravità della non conformità per i report**. Specificare il livello di gravità che viene segnalato se il criterio di conformità viene valutato come non conforme. I livelli di gravità disponibili sono i seguenti:

     * **Nessuno**. I dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.
     * **Informazioni**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.   
     * **Avviso**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.
     * **Errore critico**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.
     * **Errore critico con evento**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.      

5.  Nella pagina **Piattaforme supportate** scegliere le piattaforme del dispositivo che verranno valutate da questi criteri di conformità oppure scegliere **Seleziona tutto** per selezionare tutte le piattaforme del dispositivo. Le piattaforme supportate sono: Windows 7, Windows 8.1 e Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

6.  Nella pagina **Regole** , indicare una o più regole che definiscono la configurazione che i dispositivi devono possedere per essere ritenuti conformi. Quando si crea un criterio di conformità, alcune regole vengono attivate per impostazione predefinita. Tuttavia, è possibile modificarle o eliminarle. Per un elenco completo di tutte le regole, vedere la sezione "Regole dei criteri di conformità" più avanti in questo argomento.

  > [!NOTE]  
  >  Nei PC Windows la versione 8.1 del sistema operativo Windows viene indicata come 6.3. Se la regola della versione del sistema operativo è impostata su Windows 8.1 per Windows, il dispositivo risulterà non conforme anche se il sistema operativo installato è Windows 8.1. Assicurarsi di impostare la versione di Windows *riportata* corretta per le regole della versione minima e massima del sistema operativo. Il numero di versione deve corrispondere alla versione restituita dal comando **winver**. Il problema non riguarda i dispositivi Windows Phone perché la versione restituita è la 8.1, come previsto. Per i PC Windows con sistema operativo Windows 10, la versione deve essere impostata come **10.0** + il numero di build del sistema operativo restituito dal comando **winver**.

7.  Nella pagina **Riepilogo** della procedura guidata rivedere le impostazioni definite e completare la procedura.

 I nuovi criteri vengono visualizzati nel nodo **Criteri di conformità** dell'area di lavoro **Asset e conformità** .

## <a name="deploy-a-compliance-policy"></a>Distribuire i criteri di conformità

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e scegliere**Criteri di conformità**.

3.  Nel gruppo **Distribuzione** della scheda **Home** scegliere **Distribuisci**.

4.  Nella finestra di dialogo **Distribuisci criteri di conformità** scegliere **Sfoglia** per selezionare la raccolta utenti nella quale distribuire i criteri.

     È anche possibile selezionare le opzioni per creare avvisi da inviare quando i criteri non sono conformi e configurare la pianificazione in base alla quale verrà valutata la conformità dei criteri.

5.  Al termine, scegliere **Salva**.

## <a name="monitor-the-compliance-policy"></a>Monitorare i criteri di conformità

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Per visualizzare i risultati di conformità nella console di Configuration Manager

1.  Nella console di Configuration Manager scegliere **Monitoraggio**.

2.  Nell'area di lavoro **Monitoraggio** scegliere **Distribuzioni**.

3.  Nell'elenco **Distribuzioni** selezionare la distribuzione del criterio di conformità di cui si vogliono esaminare le informazioni sulla conformità.

4.  È possibile esaminare le informazioni di riepilogo sulla conformità della distribuzione del criterio nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione. Nel gruppo **Distribuzione** della scheda **Home** scegliere **Visualizza stato** per aprire la pagina **Stato distribuzione**.

    La pagina **Stato distribuzione** contiene le schede seguenti:

    -   **Conforme**. Indica la conformità dei criteri in base al numero degli asset interessati. È possibile scegliere una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contenga tutti gli utenti o i dispositivi conformi a questa regola. Nel riquadro **Dettagli asset** vengono visualizzati gli utenti o i dispositivi conformi ai criteri. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive.

    -   **Errore**. Visualizza un elenco di tutti gli errori relativi alla distribuzione dei criteri selezionata, in base al numero di asset interessati. È possibile scegliere una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contenga tutti gli utenti o tutti i dispositivi che hanno generato errori con questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive sul problema.

    -   **Non conforme**. Visualizza un elenco di tutte le regole non conformi all'interno dei criteri, in base al numero di asset interessati. È possibile scegliere una regola per creare un nodo temporaneo nel nodo **Utenti** o **Dispositivi** dell'area di lavoro **Asset e conformità** che contenga tutti gli utenti o i dispositivi non conformi a questa regola. Quando si seleziona un utente o un dispositivo, il riquadro **Dettagli asset** visualizza gli utenti o i dispositivi interessati dal problema. Fare doppio clic su un dispositivo o su un utente presente nell'elenco per visualizzare informazioni aggiuntive sul problema.

    -   **Sconosciuto**. Visualizza un elenco di tutti gli utenti o di tutti i dispositivi che non sono conformi alla distribuzione dei criteri selezionata, insieme allo stato corrente del client dei dispositivi.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Per monitorare lo stato di conformità di un singolo dispositivo

1.  Nella console di Configuration Manager scegliere l'area di lavoro **Asset e conformità**.

2.  Scegliere **Dispositivi**.

3.  Fare clic con il pulsante destro del mouse su una delle colonne per abilitare altre colonne.

  È possibile aggiungere le colonne seguenti:

  - **ID dispositivo di Azure Active Directory**.  Identificatore univoco del dispositivo in Azure Active Directory.

  - **Dettagli dell'errore di conformità**.  Dettagli del messaggio di errore quando il processo end-to-end ha esito negativo. Se questa colonna è vuota, significa che non sono stati rilevati errori ed è stato segnalato lo stato di conformità.

  - **Posizione dell'errore di conformità**.  Informazioni dettagliate sulla posizione in cui si è verificato l'errore di conformità. Se questa colonna è vuota, significa che non sono stati rilevati errori ed è stato segnalato lo stato di conformità. Esempi di posizione in cui il processo di conformità può restituire un errore: 
      - Client di ConfigMgr
      - Punto di gestione
      - Intune
      - Azure Active Directory
<br></br>
  - **Ora della valutazione della conformità**. Ora dell'ultimo controllo di conformità.

  - **Impostazione ora per la conformità**. Ora dell'ultimo aggiornamento della conformità in Azure Active Directory.

  - **Conforme all'accesso condizionale**.  Se il computer è conforme o meno ai criteri di accesso condizionale.

  > [!IMPORTANT]
  > Queste colonne non vengono visualizzate per impostazione predefinita.

#### <a name="to-view-intune-compliance-policies-charts"></a>Per visualizzare i grafici dei criteri di conformità di Intune
1. A partire dalla versione 1610 di Configuration Manager, nella console di Configuration Manager scegliere **Monitoraggio**.

2. Nell'area di lavoro **Monitoraggio** passare a **Panoramica** > **Impostazioni di conformità** > **Criteri di conformità**.

   Vengono visualizzati i grafici seguenti:

    - **Conformità complessiva del dispositivo**. Visualizza la conformità complessiva dei dispositivi rispetto a tutti i criteri di conformità.
    - **Motivi principali per la mancata conformità**. Visualizza i criteri principali ai quali i dispositivi non sono conformi.

3. Scegliere una sezione di uno dei due grafici per eseguire il drill-down nell'elenco dei dispositivi della categoria corrispondente.

#### <a name="to-view-a-health-attestation-report"></a>Per visualizzare il report di attestazione dell'integrità

1.  A partire dalla versione 1602 di Configuration Manager, nella console di Configuration Manager scegliere **Monitoraggio**.

2.  Per visualizzare un report di riepilogo dello stato corrente dei dispositivi in base alla conformità, fare clic su **Sicurezza** e scegliere **Attestazione dell'integrità**.

3.  Per visualizzare un report contenente l'elenco di tutti i dispositivi e tutti gli attributi di attestazione dell'integrità, scegliere **Sicurezza** e **Attestazione dell'integrità**.

## <a name="compliance-policy-rules"></a>Regole dei criteri di conformità
* **Richiedi impostazioni password nei dispositivi mobili**. È possibile richiedere agli utenti di immettere una password per poter accedere al dispositivo.

  **Supportato in:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Richiedi una password per sbloccare un dispositivo inattivo** (aggiornamento 1602). È possibile richiedere agli utenti di immettere una password per poter accedere al dispositivo bloccato.

  **Supportato in:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minuti di inattività prima che venga richiesta la password** (aggiornamento 1602). È possibile specificare il tempo di inattività prima che l'utente debba immettere nuovamente la password. Impostare il valore su una delle opzioni disponibili: **1 minuto**, **5 minuti**, **15 minuti**, **30 minuti**, **1 ora**.

  Questa regola deve essere usata con **Richiedi una password per sbloccare un dispositivo inattivo**. Il valore qui impostato determina quando considerare il dispositivo inattivo e bloccato. Quando l'opzione **Richiedi una password per sbloccare un dispositivo inattivo** è impostata su **True**, l'utente deve immettere una password per accedere al dispositivo bloccato.

  **Supportato in:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Richiedi aggiornamenti automatici** (aggiornamento 1602). È possibile richiedere ai dispositivi con Windows 8.1 o versioni successive di installare automaticamente gli aggiornamenti e specificare la classe degli aggiornamenti.

  Il valore deve essere impostato su **Nessuno** per impedire l'installazione automatica, su **Consigliati** per installare automaticamente tutti gli aggiornamenti consigliati o su **Importanti** per installare solo gli aggiornamenti classificati come importanti.

  **Supportato in:**
  * Windows Phone 8+

* **Consenti password semplici**. Consente agli utenti di creare password semplici come "1234" o "1111." Per impostazione predefinita, questa impostazione è disabilitata.

  **Supportato in:**
  * Windows Phone 8+
  * iOS 6+

* **Lunghezza minima password**. È possibile specificare il numero minimo di cifre o caratteri che la password dell’utente deve contenere (6 per impostazione predefinita).

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >Per i dispositivi che eseguono Windows e sono protetti da un account Microsoft, i criteri di conformità non eseguono correttamente la convalida se **Lunghezza minima password** contiene più di otto caratteri o se **Numero minimo di set di caratteri** ne contiene più di due.

* **Crittografia file nel dispositivo mobile**. È possibile richiede la crittografia del dispositivo per la connessione alle risorse. I dispositivi che eseguono Windows Phone 8 vengono crittografati automaticamente. I dispositivi che eseguono iOS vengono crittografati quando si configura l'impostazione **Richiedi impostazioni password nei dispositivi mobili**. Questa opzione è attivata per impostazione predefinita.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Il dispositivo non deve essere jailbroken o rooted**. Se si abilita questa impostazione, i dispositivi jailbroken (iOS) o rooted (Android) non sono conformi. Per impostazione predefinita, questa impostazione è disabilitata.

  **Supportato in:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Il profilo di posta elettronica deve essere gestito da Intune**. Quando questa opzione è impostata su **Sì**, il dispositivo deve usare il profilo di posta elettronica distribuito nel dispositivo. Il dispositivo viene considerato non conforme se il profilo di posta elettronica non viene distribuito allo stesso gruppo di utenti a cui si applicano i criteri di conformità.

  Il dispositivo risulta non conforme anche se l'utente ha già configurato un account di posta elettronica nel dispositivo che corrisponde a un profilo di posta elettronica di Intune distribuito al dispositivo. In questo caso, Intune non può sovrascrivere il profilo con provisioning dell'utente, quindi non può gestirlo. L'utente può rendere conforme il dispositivo rimuovendo le impostazioni di posta elettronica esistenti, consentendo quindi a Intune di installare il profilo di posta elettronica gestito.

  Per consultare dettagli sui profili di posta elettronica, vedere [Consentire l'accesso alla posta elettronica aziendale usando profili di posta elettronica con Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Per impostazione predefinita, questa impostazione è disabilitata.

  **Supportato in:**
  * iOS 6+

* **Profilo di posta elettronica**. Se è selezionata l'opzione **L'account di posta elettronica deve essere gestito da Intune**, scegliere **Seleziona** per scegliere il profilo di posta elettronica con cui gestire i dispositivi. Il profilo di posta elettronica deve essere presente nel dispositivo.

  **Supportato in:**
  * iOS 6+

* **Versione minima richiesta del sistema operativo**. Quando un dispositivo non soddisfa il requisito per la versione minima del sistema operativo, viene segnalato come non conforme e viene visualizzato un collegamento con informazioni su come eseguire l'aggiornamento. È possibile scegliere di aggiornare il dispositivo e dopo l'aggiornamento si potrà accedere alle risorse aziendali.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Versione massima consentita del sistema operativo**. Quando un dispositivo usa una versione del sistema operativo successiva rispetto a quella specificata nella regola, l'accesso alle risorse aziendali risulta bloccato. È necessario contattare l'amministratore IT. Fino a quando la regola non viene modificata in modo da consentire la versione del sistema operativo, non è possibile usare questo dispositivo per accedere alle risorse aziendali.

  **Supportato in:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Richiedi che i dispositivi siano riportati come integri** (aggiornamento 1602). È possibile impostare una regola per richiedere che i dispositivi Windows 10 vengano segnalati come integri in criteri di conformità nuovi o esistenti. Se questa impostazione è abilitata, i dispositivi Windows 10 vengono valutati tramite il servizio di attestazione dell'integrità del dispositivo riguardo ai punti dati seguenti:

  - **BitLocker è abilitato**. Quando Bitlocker è abilitato, il dispositivo può proteggere dall'accesso non autorizzato i dati archiviati nell'unità, quando il sistema viene spento o passa alla modalità di ibernazione.

   Crittografia unità BitLocker di Windows crittografa tutti i dati archiviati nel volume del sistema operativo Windows. BitLocker usa il TPM per proteggere il sistema operativo Windows e i dati utente. Consente di garantire che un computer non venga manomesso, anche se viene perso, rubato o lasciato incustodito.
   
   Se il computer è dotato di un TPM compatibile, BitLocker usa il TPM per bloccare le chiavi di crittografia che proteggono i dati. Di conseguenza, non è possibile accedere alle chiavi finché il TPM non ha verificato lo stato del computer.

  - **L'integrità del codice è abilitata**. La funzionalità Integrità del codice convalida l'integrità di un driver o di un file system ogni volta che viene caricato nella memoria. L'integrità del codice rileva se un driver o un file di sistema non firmato viene caricato nel kernel. Rileva anche se un file di sistema è stato modificato da un software dannoso eseguito da un account utente con privilegi di amministratore.

  - **L'avvio protetto è abilitato**. Quando l'avvio protetto è abilitato, viene forzato l'avvio del sistema in uno stato attendibile predefinito. È anche necessario che i componenti di base usati per avviare il computer abbiano le firme crittografate corrette ritenute attendibili dall'organizzazione che ha prodotto il dispositivo. Il firmware UEFI verifica questo aspetto prima di permettere l'avvio del computer. Se alcuni file sono stati manomessi, danneggiandone la firma, il sistema non viene avviato.

  - **L'antimalware ad esecuzione anticipata è abilitato**. Questa impostazione si applica solo ai PC. La funzionalità Antimalware ad esecuzione anticipata offre protezione per i computer in rete quando vengono avviati e prima dell'inizializzazione di driver di terze parti.
  
   Questa regola è disattivata per impostazione predefinita.

  Per informazioni sul funzionamento del servizio di attestazione dell'integrità, vedere l'argomento relativo al [provider di servizi di configurazione HealthAttestation](https://msdn.microsoft.com/library/dn934876.aspx).

  **Supportato in:**
  * Windows 10 e Windows 10 Mobile

- **App che non possono essere installate nel dispositivo**. Se viene installata un'app dall'elenco di app non conformi per l'amministratore, l'accesso alla posta elettronica aziendale e ad altre risorse aziendali che supportano l'accesso condizionale viene bloccato. Questa regola richiede il nome e l'ID dell'app quando si aggiunge un'app all'elenco di app non conformi definito dall'amministratore. È possibile aggiungere anche l'autore dell'app, ma non è obbligatorio.

    **Supportato in:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Trovare l'ID di un'app

L'ID dell'app è un identificatore che identifica in modo univoco l'app all'interno dei servizi per applicazioni di Apple e Google, ad esempio com.contoso.myapp. Per trovare un ID:

- **Android**
    - È possibile trovare l'ID di un'app nell'URL di Google Play Store usato per creare l'app. Esempio di ID app: *…?id=com.companyname.appname&hl=en*

- **iOS**
    1. È possibile trovare il numero ID nell'URL di iTunes Store, ad esempio */id875948587?mt=8*

    2. In un Web browser digitare l'URL seguente sostituendo il numero con il numero ID appena rilevato (in questo caso l'esempio precedente): https://itunes.apple.com/lookup?id=875948587

    3. Scaricare e aprire il file di testo.
  
    4. Cercare il testo **bundleId**.

    Esempio di ID app: "*bundleId*":"*com.companyname.appname*" 


