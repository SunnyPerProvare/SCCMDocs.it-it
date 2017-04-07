---
title: Creare elementi di configurazione per dispositivi Android e Samsung KNOX Standard gestiti con Intune | Microsoft Docs
description: Usare l&quot;elemento di configurazione Android e Samsung KNOX Standard di System Center Configuration Manager per gestire le impostazioni dei dispositivi.
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: a8682db0d1def583413e59cf2251a48c6afbdb53
ms.lasthandoff: 03/27/2017


---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client System Center Configuration Manager

Usare l'elemento di configurazione **Android e Samsung KNOX** di System Center Configuration Manager per gestire le impostazioni per i dispositivi Android e Samsung KNOX registrati in Microsoft Intune o gestiti in locale da Configuration Manager.  

### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Per creare un elemento di configurazione per Android e Samsung KNOX  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi fare clic su **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Android e Samsung KNOX**.  

6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

7.  Nella pagina **Piattaforme supportate** della procedura guidata selezionare le piattaforme Android e Samsung KNOX specifiche che valuteranno l'elemento di configurazione.  

8.  Nella pagina **Impostazioni dispositivo** della creazione guidata selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Android e Samsung KNOX](#BKMK_setref) in questo argomento e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Se l'impostazione da modificare non è inclusa nell'elenco, selezionare la casella di controllo **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  

9. In ogni pagina di impostazioni configurare le impostazioni necessarie e specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  

10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato quando viene trovato un elemento di configurazione non conforme, selezionando uno dei livelli seguenti:  

    -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  

    -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  

    -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  

    -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  

    -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  

11. Nella pagina **Applicabilità piattaforma** della creazione guidata, verificare le eventuali impostazioni non compatibili con le piattaforme supportate selezionate in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  

    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  

12. Completare la procedura guidata.  

 È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  

##  <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Android e Samsung KNOX  

### <a name="password"></a>Password  
 Queste impostazioni si applicano ai dispositivi Android e Samsung KNOX.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|La lunghezza minima della password.|  
|**Scadenza password in giorni**|Il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password usate in precedenza.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.|  
|**Tempo di inattività prima del blocco del dispositivo**|Selezionare il tempo che deve trascorrere prima che il dispositivo venga bloccato se non è in uso.|
|**Qualità password**|Selezionare il livello di complessità delle password necessario e indicare se possono essere usati anche dispositivi biometrici.|  
|**Consenti Smart Lock e altri agenti di attendibilità**|Consente di controllare la funzionalità Smart Lock su dispositivi compatibili con Android. Questa funzionalità del telefono, talvolta nota anche come agenti di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock.|
|**Impronta digitale per lo sblocco (KNOX 5.0+)**|Consente di usare un'impronta digitale per sbloccare i dispositivi compatibili.|

###  <a name="device"></a>Dispositivo   

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Chiamata vocale**|Abilita o disabilita la funzionalità di composizione vocale sul dispositivo.|
|**Assistente vocale**|Consente di usare un assistente vocale sul dispositivo.|
|**Acquisizione schermo**|Consente all'utente di acquisire il contenuto dello schermo sotto forma di immagine.|
|**Invio dati diagnostici**|Consente al dispositivo di inviare i dati di diagnostica a Google.|
|**Georilevazione**|Consente al dispositivo di usare informazioni sulla posizione geografica.|
|**Copia e Incolla**|Consente di usare le funzioni di copia e incolla nel dispositivo.|
|**Ripristino impostazioni predefinite**|Consente all'utente di eseguire il ripristino delle impostazioni di fabbrica del dispositivo.|  |
|**Condivisione degli Appunti tra applicazioni**|Usare gli Appunti per copiare e incollare tra app.|  |
|**Bluetooth**|Consente l'uso del Bluetooth sul dispositivo.|

### <a name="store"></a>Archivio
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Archivio applicazioni**|Consente all'utente di accedere all'app Google Play Store sul dispositivo.|

### <a name="browser"></a>Browser
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Consenti browser Web**|Specifica se è possibile usare il Web browser predefinito del dispositivo.|
|**Riempimento automatico**|Specifica se è possibile usare la funzione di riempimento automatico del Web browser.|
|**Esecuzione script attivo**|Consente al Web browser del dispositivo di eseguire lo script attivo.|
|**Blocco popup**|Consente l'uso del blocco popup nel Web browser.|
|**Cookie**|Consente l'uso dei cookie nel Web browser.|

### <a name="cloud"></a>Cloud  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Backup di Google**|Consente l'uso del backup di Google.|  
|**Sincronizzazione automatica dell'account Google**|Consente la sincronizzazione automatica delle impostazioni dell'account Google.|  

### <a name="security"></a>Sicurezza  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Messaggistica SMS e MMS**|Consente l'uso della messaggistica SMS e MMS sul dispositivo.|
|**Archivi rimovibili**|Consente l'uso di archivi rimovibili, ad esempio una scheda SD, sul dispositivo.|
|**Fotocamera**|Consente l'uso della fotocamera del dispositivo.<br /><br /> Si applica ai dispositivi Android e Samsung KNOX.|
|**NFC (Near Field Communication)**|Consente operazioni che usano Near Field Communication (se supportato dal dispositivo).|
|**YouTube**|Consente l'utilizzo dell'app YouTube sul dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  
|**Spegnimento**|Consente lo spegnimento del dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  

### <a name="roaming"></a>Roaming

|Impostazioni|Dettagli|  
|-------------|-------------|  
|Roaming vocale|Consente il roaming vocale quando il dispositivo si trova in una rete cellulare.|
|Roaming dati|Consente il roaming dati quando il dispositivo si trova in una rete cellulare.|


### <a name="encryption"></a>Crittografia  
 Queste impostazioni si applicano ai dispositivi Android e Samsung KNOX.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Crittografia scheda di memoria**|È necessario che la scheda di memoria del dispositivo sia crittografata.|
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file sul dispositivo mobile.|  

### <a name="wireless-communications"></a>Comunicazioni wireless

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Connessione rete wireless**|Consente l'uso delle funzionalità Wi-Fi sul dispositivo.|
|**Tethering Wi-Fi**|Consente l'uso del tethering Wi-Fi sul dispositivo.|


###  <a name="compliant-and-noncompliant-apps-android"></a>App conformi e non conformi (Android)  
 Consente di specificare un elenco di app Android conformi oppure non conformi nella società. È quindi possibile usare i report per visualizzare i dispositivi nei quali sono installate app non conformi e gli utenti associati.  

 Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Per indicare le app conformi o non conformi  

Nella pagina **App conformi e non conformi (Android)** specificare le informazioni seguenti:  

|Impostazioni|Altre informazioni|  
|-------------|----------------------|  
|**Elenco app non conformi**|Selezionare questa opzione per specificare un elenco di app che verranno segnalate come non conformi, quando vengono installate dagli utenti.|  
|**Elenco app conformi**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti sono autorizzati a installare. Tutte le altre app installate verranno segnalate come non conformi.|  
|**Aggiungi**|Aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.<br /><br /> Per specificare l'URL, cercare l'app da usare dalla [sezione delle app di Google Play](https://play.google.com/store/apps).<br /><br /> Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app conformi e non conformi.<br /><br /> **Esempio:** cercare **Microsoft Office Mobile**in Google Play. L'URL usato sarà **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
|**Modifica**|Consente di modificare il nome, l'autore e l'URL dell'app selezionata.|  
|**Rimuovi**|Elimina l'app selezionata dall'elenco.|  
|**Importa**|Importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.|  

## <a name="android-for-work-configuration-items"></a>Elementi di configurazione di Android for Work
Android for Work ha due gruppi di impostazioni per gli elementi di configurazione:
-    Password: identica alle impostazioni di Android "classico"
- Profilo di lavoro: abilita le impostazioni di Android for Work seguenti:
  -    Consenti la condivisione dei dati tra i profili di lavoro e personali
  - Nascondi le notifiche del profilo di lavoro quando il dispositivo è bloccato (Android 6.0+)
  -    Imposta i criteri di autorizzazione predefiniti delle app (Android 6.0+)

Per creare un elemento di configurazione nel profilo di lavoro di Android, scegliere **Android for Work** nella pagina **Generale** e configurare le impostazioni per ognuno dei gruppi di impostazioni, aggiungendo l'elemento di configurazione a una linea di base ed eseguendo la distribuzione come di consueto. Queste impostazioni verranno applicate solo ai dispositivi registrati come Android for Work e non a quelli registrati come Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Modalità tutto schermo (solo per Samsung KNOX)  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Per configurare la modalità tutto schermo per un dispositivo Samsung KNOX  

1.  Nella pagina **Configura impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX** della **Creazione guidata dell'elemento di configurazione** specificare le informazioni seguenti:  

|Impostazioni|Altre informazioni|  
|-------------|----------------------|  
|**Seleziona app**|Fare clic su **Sfoglia** per selezionare un'applicazione Android (con estensione **apk**) che possa essere eseguita quando il dispositivo è in modalità tutto schermo. Non sarà possibile eseguire altre applicazioni nel dispositivo.|  
|**Pulsanti volume**|Abilita o disabilita l'uso dei pulsanti del volume nel dispositivo.|  
|**Pulsante di riattivazione e sospensione schermo**|Abilita o disabilita il pulsante di riattivazione sospensione dello schermo del dispositivo.|  



2.  Al termine, fare clic su **Avanti**.  

 È possibile usare uno dei report seguenti per monitorare le app conformi e non conformi:  

-   **Elenco di app e dispositivi non conformi per un utente specificato** : Visualizza informazioni sugli utenti e sui dispositivi con app installate che non sono conformi ai criteri specificati.  

-   **Riepilogo degli utenti con app non conformi** : Visualizza informazioni sugli utenti che dispongono di app installate che non sono conformi ai criteri specificati.  

 Per informazioni sull'uso dei report, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Vedere anche  
 [Elementi di configurazione per dispositivi gestiti senza il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)

