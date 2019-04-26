---
title: Creare elementi di configurazione per dispositivi Android e Samsung KNOX Standard gestiti con Intune
titleSuffix: Configuration Manager
description: Usare l'elemento di configurazione Android e Samsung KNOX Standard di System Center Configuration Manager per gestire le impostazioni dei dispositivi.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 47d2ee0cf82e9739d8e6364098be6c3033ce1ea2
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62218195"
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client System Center Configuration Manager

Usare l'elemento di configurazione **Android e Samsung KNOX** di System Center Configuration Manager per gestire le impostazioni per i dispositivi Android e Samsung KNOX registrati in Microsoft Intune o gestiti in locale da Configuration Manager.  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Per creare un elemento di configurazione per Android e Samsung KNOX  

1. Nella console di Configuration Manager scegliere **Asset e conformità**.  

2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi scegliere **Elementi di configurazione**.  

3. Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea elemento di configurazione**.  

4. Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5. In **Specificare il tipo di elemento di configurazione da creare** scegliere **Android e Samsung KNOX**.  

6. Scegliere **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

7. Nella pagina **Piattaforme supportate** della procedura guidata scegliere le piattaforme Android e Samsung KNOX specifiche che valuteranno l'elemento di configurazione.  

8. Nella pagina **Impostazioni dispositivo** della creazione guidata scegliere il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Android e Samsung KNOX](#BKMK_setref) in questo argomento e scegliere **Avanti**.  

    > [!TIP]  
    >  Se l'impostazione da modificare non è inclusa nell'elenco, scegliere la casella **Configura impostazioni aggiuntive non presenti nei gruppi di impostazioni predefinite**.  

9. In ogni pagina di impostazioni configurare le impostazioni necessarie. Specificare se si vuole monitorarle e aggiornarle nel caso non siano conformi nei dispositivi (se questa funzionalità è supportata).  

10. Per ogni gruppo di impostazioni, è anche possibile configurare il livello di gravità che verrà segnalato quando viene trovato un elemento di configurazione non conforme, selezionando uno dei livelli seguenti:  

    - **Nessuno**. I dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  

    - **Informazioni**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  

    - **Avviso**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  

    - **Errore critico**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  

    - **Errore critico con evento**. I dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  

11. Nella pagina **Applicabilità piattaforma** della creazione guidata, verificare le eventuali impostazioni non compatibili con le piattaforme supportate scelte in precedenza. È possibile tornare indietro e rimuovere queste impostazioni oppure continuare.  

    > [!TIP]  
    >  Non viene valutata la conformità delle impostazioni non supportate.  

12. Completare la procedura guidata.  

    È possibile visualizzare il nuovo elemento di configurazione nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione per Android e Samsung KNOX  

### <a name="password"></a>Password  
Queste impostazioni si applicano ai dispositivi Android e Samsung KNOX.  

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|Specifica la lunghezza minima della password.|  
|**Scadenza password in giorni**|Specifica il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password usate in precedenza.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.|  
|**Tempo di inattività prima del blocco del dispositivo**|Specifica il tempo che deve trascorrere prima che il dispositivo venga bloccato se non è in uso.|
|**Qualità password**|Specifica il livello di complessità delle password necessario e se possono essere usati dispositivi biometrici.|  
|**Consenti Smart Lock e altri agenti di attendibilità**|Consente di controllare la funzionalità Smart Lock su dispositivi compatibili con Android. Questa funzionalità del telefono consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti di configurare Smart Lock.|
|**Impronta digitale per lo sblocco (KNOX 5.0+)**|Consente l'uso di un'impronta digitale per sbloccare i dispositivi compatibili.|

### <a name="device"></a>Dispositivo   

|                 Impostazione                  |                             Dettagli                             |
|------------------------------------------|-----------------------------------------------------------------|
|            **Chiamata vocale**             |  Abilita o disabilita la funzionalità di composizione vocale sul dispositivo.   |
|           **Assistente vocale**            |    Consente di usare un assistente vocale sul dispositivo.    |
|            **Acquisizione schermo**            |     Consente all'utente di acquisire il contenuto dello schermo sotto forma di immagine.      |
|      **Invio dati diagnostici**      |    Consente al dispositivo di inviare i dati di diagnostica a Google.     |
|             **Georilevazione**              |            Consente al dispositivo di usare informazioni sulla posizione geografica.            |
|            **Copia e Incolla**            |         Consente di usare le funzioni di copia e incolla nel dispositivo.          |
|            **Ripristino impostazioni predefinite**             |      Consente all'utente di eseguire il ripristino delle impostazioni di fabbrica del dispositivo.       |
| **Condivisione degli Appunti tra applicazioni** | Consente all'utente di usare gli Appunti per copiare e incollare tra app. |
|              **Bluetooth**               |           Consente l'uso del Bluetooth sul dispositivo.            |

### <a name="store"></a>Archivio

|Impostazione|Dettagli|  
|------------------|-------------|  
|**Archivio applicazioni**|Consente all'utente di accedere all'app Google Play Store sul dispositivo.|

### <a name="browser"></a>Browser

|Impostazione|Dettagli|  
|------------------|-------------|  
|**Consenti browser Web**|Consente di usare il Web browser predefinito del dispositivo.|
|**Riempimento automatico**|Specifica se è possibile usare la funzione di riempimento automatico del Web browser.|
|**Esecuzione script attivo**|Consente al Web browser del dispositivo di eseguire lo script attivo.|
|**Blocco popup**|Consente l'uso del blocco popup nel Web browser.|
|**Cookie**|Consente l'uso dei cookie nel Web browser.|

### <a name="cloud"></a>Cloud  

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Backup di Google**|Consente l'uso del backup di Google.|  
|**Sincronizzazione automatica dell'account Google**|Consente la sincronizzazione automatica delle impostazioni dell'account Google.|  

### <a name="security"></a>Sicurezza  

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Messaggistica SMS e MMS**|Consente l'uso della messaggistica SMS e MMS sul dispositivo.|
|**Archivi rimovibili**|Consente l'uso di archivi rimovibili, ad esempio una scheda SD, sul dispositivo.|
|**Fotocamera**|Consente l'uso della fotocamera del dispositivo.<br /><br /> Si applica ai dispositivi Android e Samsung KNOX.|
|**NFC (Near Field Communication)**|Consente attività che usano Near Field Communication (se supportato dal dispositivo).|
|**YouTube**|Consente l'uso dell'app YouTube sul dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  
|**Spegnimento**|Consente lo spegnimento del dispositivo.<br /><br /> Si applica solo ai dispositivi Samsung KNOX.|  

### <a name="roaming"></a>Roaming

|Impostazione|Dettagli|  
|-------------|-------------|  
|Roaming vocale|Consente il roaming vocale quando il dispositivo si trova in una rete cellulare.|
|Roaming dati|Consente il roaming dati quando il dispositivo si trova in una rete cellulare.|


### <a name="encryption"></a>Crittografia  
 Queste impostazioni si applicano ai dispositivi Android e Samsung KNOX.  

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Crittografia scheda di memoria**|È necessario che la scheda di memoria del dispositivo sia crittografata.|
|**Crittografia file nel dispositivo mobile**|Richiede la crittografia dei file sul dispositivo mobile.|  

### <a name="wireless-communications"></a>Comunicazioni wireless

|Impostazione|Dettagli|  
|-------------|-------------|  
|**Connessione rete wireless**|Consente l'uso delle funzionalità Wi-Fi sul dispositivo.|
|**Tethering Wi-Fi**|Consente l'uso del tethering Wi-Fi sul dispositivo.|


### <a name="compliant-and-noncompliant-apps-android"></a>App conformi e non conformi (Android)  
È possibile specificare un elenco di app Android conformi oppure non conformi nella società. È quindi possibile usare i report per mostrare i dispositivi nei quali sono installate app non conformi e gli utenti associati.  

Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Per indicare le app conformi o non conformi  

Nella pagina **App conformi e non conformi (Android)** specificare le informazioni seguenti:  


|          Impostazione           |                                                                                                                                                                                                                                                                                                                 Altre informazioni                                                                                                                                                                                                                                                                                                                  |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Elenco app non conformi** |                                                                                                                                                                                                                                                                               Specifica un elenco di app che verranno segnalate come non conformi, quando vengono installate dagli utenti.                                                                                                                                                                                                                                                                               |
|  **Elenco app conformi**   |                                                                                                                                                                                                                                                              Specifica un elenco di app Mac OS X che gli utenti sono autorizzati a installare. Tutte le altre app installate verranno segnalate come non conformi.                                                                                                                                                                                                                                                               |
|          **Aggiungi**           | Aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.<br /><br /> Per specificare l'URL, cercare l'app da usare dalla [sezione delle app di Google Play](https://play.google.com/store/apps).<br /><br /> Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app conformi e non conformi.<br /><br /> **Esempio:** Cercare Google Play **Microsoft Office Mobile**. L'URL da usare sarà **<https://play.google.com/store/apps/details?id=com.microsoft.office.officehub>**. |
|          **Modifica**          |                                                                                                                                                                                                                                                                                          Consente di modificare il nome, l'autore e l'URL dell'app selezionata.                                                                                                                                                                                                                                                                                          |
|         **Rimuovi**         |                                                                                                                                                                                                                                                                                                      Elimina l'app selezionata dall'elenco.                                                                                                                                                                                                                                                                                                      |
|         **Importa**         |                                                                                                                                                                                                                                                 Importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.                                                                                                                                                                                                                                                 |

## <a name="android-for-work-configuration-items"></a>Elementi di configurazione di Android for Work
Android for Work ha due gruppi di impostazioni per gli elementi di configurazione:

- **Password**. Identica alle impostazioni di Android "classico".

- **Profilo di lavoro**. Abilita le impostazioni di Android for Work seguenti:
  - **Consenti la condivisione dei dati tra i profili di lavoro e personali**
  - **Nascondi le notifiche del profilo di lavoro quando il dispositivo è bloccato** (Android 6.0+)
  - **Imposta i criteri di autorizzazione predefiniti delle app** (Android 6.0+)

Per creare un elemento di configurazione nel profilo di lavoro di Android, scegliere **Android for Work** nella pagina **Generale** e configurare le impostazioni per ognuno dei gruppi di impostazioni. Aggiungere l'elemento di configurazione a una linea di base ed eseguire la distribuzione come di consueto. Queste impostazioni verranno applicate solo ai dispositivi registrati come Android for Work e non ai dispositivi registrati come Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Modalità tutto schermo (solo per Samsung KNOX)  
È possibile usare la modalità tutto schermo per bloccare un dispositivo per consentire l'uso solo di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo. In alternativa, potrebbero essere usate per un dispositivo dedicato all'esecuzione di una sola funzione, come un dispositivo POS.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Per configurare la modalità tutto schermo per un dispositivo Samsung KNOX  

1. Nella pagina **Configura impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX** della Creazione guidata dell'elemento di configurazione specificare le informazioni seguenti:  

   |Impostazione|Altre informazioni|  
   |-------------|----------------------|  
   |**Seleziona app**|Scegliere **Sfoglia** per selezionare un'applicazione Android (con estensione **apk**) che possa essere eseguita quando il dispositivo è in modalità tutto schermo. Non sarà possibile eseguire altre applicazioni nel dispositivo.|  
   |**Pulsanti volume**|Abilita o disabilita l'uso dei pulsanti del volume nel dispositivo.|  
   |**Pulsante di riattivazione e sospensione schermo**|Abilita o disabilita il pulsante di riattivazione sospensione dello schermo del dispositivo.|  

2. Al termine, scegliere **Avanti**.  

## <a name="reports-for-monitoring"></a>Report per il monitoraggio
È possibile usare uno dei report seguenti per monitorare le app conformi e non conformi:  

- **Elenco di app e dispositivi non conformi per un utente specificato**. Mostra informazioni sugli utenti e sui dispositivi che dispongono di app installate che non sono conformi ai criteri specificati.  

- **Riepilogo degli utenti con app non conformi**. Mostra informazioni sugli utenti che hanno installato app non conformi ai criteri specificati.  

Per informazioni sull'uso dei report, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Vedere anche  
[Elementi di configurazione per dispositivi gestiti senza il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
