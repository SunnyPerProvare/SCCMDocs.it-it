---
title: Creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client di System Center Configuration Manager | System Center Configuration Manager
description: Usare l'elemento di configurazione Android e Samsung KNOX di System Center Configuration Manager per gestire le impostazioni dei dispositivi.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28d5ef5-3ea7-4ba2-af01-6600aa805d48
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d676d31d519b7b6099c878d94b4c81f1c972887


---
# <a name="create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 Usare l'elemento di configurazione **Android e Samsung KNOX** di System Center Configuration Manager per gestire le impostazioni per i dispositivi Android e Samsung KNOX registrati in Microsoft Intune o gestiti in locale da Configuration Manager.  

## <a name="create-an-android-and-samsung-knox-configuration-item"></a>Creare un elemento di configurazione Android e Samsung KNOX  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Android e Samsung KNOX**.  

6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

7.  Nella pagina **Piattaforme supportate** selezionare le piattaforme Android e Samsung KNOX specifiche che valuteranno l'elemento di configurazione.  

8.  Nella pagina **Impostazioni dispositivo** selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Android e Samsung KNOX](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference) in questo argomento e quindi fare clic su **Avanti**.  

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

###  <a name="device"></a>Dispositivo  
 Queste impostazioni si applicano solo ai dispositivi Samsung KNOX.  

|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Ripristino impostazioni predefinite**|Consente all'utente di eseguire il ripristino delle impostazioni di fabbrica del dispositivo.|  
|**Condivisione degli Appunti tra applicazioni**|Usare gli Appunti per copiare e incollare tra app.|  

### <a name="cloud"></a>Cloud  
 Queste impostazioni si applicano solo ai dispositivi Samsung KNOX.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Backup di Google**|Consente l'uso del backup di Google.|  
|**Sincronizzazione automatica dell'account Google**|Consente la sincronizzazione automatica delle impostazioni dell'account Google.|  

### <a name="security"></a>Sicurezza  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Fotocamera**|Consente l'uso della fotocamera del dispositivo.<br /><br /> Si applica ai dispositivi Android e Samsung KNOX.|  
|**YouTube**|Consente l'utilizzo dell'app YouTube sul dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  
|**Spegnimento**|Consente lo spegnimento del dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  

### <a name="encryption"></a>Crittografia  
 Queste impostazioni si applicano ai dispositivi Android e Samsung KNOX.  

|Impostazioni|Dettagli|  
|-------------|-------------|  
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file sul dispositivo mobile.|  

### <a name="kiosk-mode-samsung-knox-only"></a>Modalità tutto schermo (solo per Samsung KNOX)  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Per configurare la modalità tutto schermo per un dispositivo Samsung KNOX  

Nella pagina **Configura impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX** della **Creazione guidata dell'elemento di configurazione** specificare le informazioni seguenti:  

- **Seleziona app**: fare clic su **Sfoglia** per selezionare un'applicazione Android (con estensione **apk**) che possa essere eseguita quando il dispositivo è in modalità tutto schermo. Non sarà possibile eseguire altre applicazioni nel dispositivo.
- **Pulsanti volume**: abilita o disabilita l'uso dei pulsanti del volume del dispositivo.
- **Pulsante di riattivazione sospensione schermo**: abilita o disabilita il pulsante di riattivazione sospensione dello schermo del dispositivo.|  

###  <a name="compliant-and-noncompliant-apps-android"></a>App conformi e non conformi (Android)  
 Consente di specificare un elenco di app Android conformi oppure non conformi nella società. È quindi possibile usare i report per visualizzare i dispositivi nei quali sono installate app non conformi e gli utenti associati.  

 Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Per indicare le app conformi o non conformi  

1.  Nella pagina **App conformi e non conformi (Android)** specificare le informazioni seguenti:  

    |Impostazioni|Altre informazioni|  
    |-------------|----------------------|  
    |**Elenco app non conformi**|Selezionare questa opzione per specificare un elenco di app che verranno segnalate come non conformi, quando vengono installate dagli utenti.|  
    |**Elenco app conformi**|Selezionare questa opzione per specificare un elenco di applicazioni che gli utenti sono autorizzati a installare. Tutte le altre app installate verranno segnalate come non conformi.|  
    |**Aggiungi**|Aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.<br /><br /> Per specificare l'URL, cercare l'app da usare dalla [sezione delle app di Google Play](https://play.google.com/store/apps).<br /><br /> Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app conformi e non conformi.<br /><br /> **Esempio:** cercare **Microsoft Office Mobile**in Google Play. L'URL usato sarà **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
    |**Modifica**|Consente di modificare il nome, l'autore e l'URL dell'app selezionata.|  
    |**Rimuovi**|Elimina l'app selezionata dall'elenco.|  
    |**Importaa**|Importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.|  

2.  Al termine, fare clic su **Avanti**.  

 È possibile usare uno dei report seguenti per monitorare le app conformi e non conformi:  

-   **Elenco di app e dispositivi non conformi per un utente specificato** : Visualizza informazioni sugli utenti e sui dispositivi con app installate che non sono conformi ai criteri specificati.  

-   **Riepilogo degli utenti con app non conformi** : Visualizza informazioni sugli utenti che dispongono di app installate che non sono conformi ai criteri specificati.  

 Per informazioni sull'uso dei report, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


