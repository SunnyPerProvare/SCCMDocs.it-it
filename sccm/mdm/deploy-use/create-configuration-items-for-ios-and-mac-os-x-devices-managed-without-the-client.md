---
title: Creare elementi di configurazione per dispositivi iOS e Mac OS X gestiti con Intune | Microsoft Docs
description: Usare l&quot;elemento di configurazione iOS e Mac OS X di System Center Configuration Manager per gestire le impostazioni dei dispositivi iOS e Mac OS X.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 613a48ac-c55d-4c4a-94ea-d3747a1b10cb
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 6e2cb628217598480973d4f728a9e0a7cd5873e7
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-configuration-items-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Come creare elementi di configurazione per dispositivi iOS e Mac OS X gestiti con Intune
Usare l'elemento di configurazione **iOS e Mac OS X** di System Center Configuration Manager per gestire le impostazioni per i dispositivi iOS e Mac OS X registrati in Microsoft Intune o gestiti localmente da Configuration Manager.  
  
### <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>Per creare un elemento di configurazione per iOS e Mac OS X  
  
1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  
  
2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi fare clic su **Elementi di configurazione**.  
  
3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  
  
4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  
  
5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **iOS e Mac OS X**.  
  
6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  
  
7.  Nella pagina **Piattaforme supportate** della procedura guidata selezionare le piattaforme iOS o Mac OS X specifiche che valuteranno l'elemento di configurazione.  
  
8.  Nella pagina **Impostazioni dispositivo** della creazione guidata selezionare il gruppo di impostazioni da configurare. Per dettagli, vedere [Informazioni di riferimento sulle impostazioni degli elementi di configurazione per iOS e Mac OS X](#BKMK_Setref) in questo argomento e quindi fare clic su **Avanti**.  
  
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
  
##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Informazioni di riferimento sulle impostazioni degli elementi di configurazione per iOS e Mac OS X  
  
###  <a name="password"></a>Password  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Richiedi impostazioni password nei dispositivi mobili**|Richiede una password nei dispositivi supportati.|  
|**Lunghezza minima password (caratteri)**|La lunghezza minima della password.|  
|**Scadenza password in giorni**|Il numero di giorni prima che sia necessario modificare una password.|  
|**Numero di password memorizzate**|Impedisce il riutilizzo delle password usate in precedenza.|  
|**Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo**|Cancella il dispositivo se questo numero di tentativi di accesso ha esito negativo.<br /><br /> (solo iOS)|  
|**Complessità password**|Scegliere se è possibile specificare un PIN, ad esempio "1234", o se è necessario fornire una password complessa.| 
|**Consenti password semplici**|Consente l'uso di password semplici come **0000** e **1234**.|
|**Sblocco mediante impronta digitale**|Consente di usare un'impronta digitale per sbloccare il dispositivo.|
|**Modifica del passcode** (solo supervisione)|Consente di aggiungere, modificare o rimuovere la password del dispositivo.|
  
###  <a name="device"></a>Dispositivo  
 Queste impostazioni si applicano ai dispositivi iOS e Mac OS X.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Aggiungi amici dell'area giochi**|Consente di aggiungere amici nell'app di area giochi.|
|**Chiamata vocale**|Consente l'utilizzo della funzionalità di composizione vocale sul dispositivo.|  
|**Assistente vocale**|Consente l'utilizzo di un'applicazione di assistenza vocale come Siri.|  
|**Assistente vocale durante il blocco**|Consente l'utilizzo di un'applicazione di assistenza vocale come Siri quando il dispositivo è bloccato.|  
|**Acquisizione schermo**|Consente di acquisire uno screenshot del display del dispositivo.|  
|**Client chat video**|Consente l'uso di applicazioni chat video, ad esempio Facetime.|  
|**Gioco multiplayer**|Consente di giocare con gli altri giocatori su Internet.|  
|**Software portafoglio personale durante il blocco**|Consente l'utilizzo di un software di portafoglio personale come Passbook.|  
|**Invio dati diagnostici**|Consente l’invio dei file di log dell'app.|  
|**Notifiche del centro notifiche**|Consente di accedere alla visualizzazione delle notifiche senza sbloccare il dispositivo.|
|**Apple Music** (solo supervisione)|Consente l'uso dell'app Apple Music.|
|**Podcast** (solo supervisione)|Consente l'uso dell'app Podcast.|
|**App Messages** (solo supervisione)|Consente l'uso dell'app Messages per l'invio di messaggi di testo.|
|**Modifica dello sfondo** (solo supervisione)|Consente all'utente di modificare lo sfondo del dispositivo.|
|**Ricerca della definizione della parola** (solo supervisione)|Abilita la funzionalità di iOS che consente di evidenziare una parola e cercarne la definizione.|
|**Rilevamento del polso per Apple Watch associati**|Quando questa opzione è abilitata, l'Apple Watch non visualizza le notifiche quando non è indossato.|
|**Filtro di Siri per le espressioni volgari** (solo supervisione)|Impedisce a Siri di dettare o parlare usando un linguaggio volgare.|
|**Modifica del nome dispositivo** (solo supervisione)|Consente all'utente di modificare il nome del dispositivo.|
|**Modifica delle impostazioni di invio dei dati di diagnostica** (solo supervisione)|Consente o impedisce al dispositivo di inviare dati di diagnostica ad Apple.|
|**Game Center** (solo supervisione)|Consente l'uso dell'app Game Center.|
|**iTunes Radio** (solo supervisione)|Consente l'uso dell'app iTunes.|
|**Apple News** (solo supervisione)|Consente l'uso dell'app Apple News.|
|**Associazione di Apple Watch** (solo supervisione)|Consente di associare il dispositivo a un Apple Watch.|
|**Correzione automatica** (solo supervisione)|Consente al dispositivo di correggere automaticamente le parole errate.|
|**Modifica Bluetooth** (solo supervisione)|Consente all'utente di modificare le impostazioni di Bluetooth nel dispositivo.|
|**Modifiche alle impostazioni dell'utilizzo della rete dati dell'app** (solo supervisione)|Consente all'utente di controllare quali app possono usare la rete dati.|
|**Scelte rapide da tastiera** (solo supervisione)|Consente l'uso dei tasti di scelta rapida.|
|**Tastiere predittive** (solo supervisione)|Consente l'uso di tastiere predittive che suggeriscono all'utente le parole che potrebbero essergli utili.|
|**Controllo ortografico tastiera** (solo supervisione)|Abilita il controllo ortografico nel dispositivo.|
|**Modifica delle impostazioni di notifica** (solo supervisione)|Consente all'utente di modificare le impostazioni di notifica del dispositivo.|
|**Restituisci risultati da Internet nella ricerca Spotlight** (solo supervisione)|Consente alla ricerca Spotlight di connettersi a Internet per fornire altri risultati.|
|**Usa Siri per eseguire query nel contenuto generato dall'utente da Internet** (solo supervisione)|Consente a Siri di accedere ai siti Web per rispondere alle domande.|

  
###  <a name="store"></a>Archivio  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Archivio applicazioni**|Consente l'accesso all'archivio applicazioni sul dispositivo.|  
|**Immettere una password per accedere all'archivio applicazioni**|Gli utenti devono immettere una password per accedere all'archivio applicazioni.|  
|**Acquisti in-app**|Consente agli utenti di effettuare acquisti in-app.|
|**Installazione di app solo con Apple Configurator e iTunes** (solo supervisione)|Abilita o disabilita l'App Store dalla schermata principale del dispositivo. Gli utenti possono ancora usare iTunes o lo strumento Apple Configurator per installare e aggiornare le app.|
|**Accesso a iBooks Store** (solo supervisione)|Consente all'utente di selezionare e acquistare libri da iBooks Store.|
|**Download automatici delle app** (solo supervisione)|Consente il download automatico nel dispositivo delle app acquistate su altri dispositivi. Questa impostazione non ha alcun effetto sugli aggiornamenti dell'app.|

  
###  <a name="browser"></a>Browser  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Browser predefinito**|È possibile modificare il browser Internet predefinito.|  
|**Riempimento automatico**|L’utente può modificare le impostazioni di completamento automatico nel browser.|  
|**Esecuzione script attivo**|Il browser può eseguire script, ad esempio gli script ActiveX.|  
|**Blocco popup**|Attiva o disattiva il blocco popup del browser.|  
|**Cookie**|Consente il salvataggio dei cookie nel dispositivo.|  
|**Avviso frodi**|Attiva o disattiva gli avvisi di potenziali siti Web fraudolenti.|  
  
###  <a name="content-rating"></a>Classificazione del contenuto  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Contenuti espliciti nell'archivio multimediale**|Specifica se si desidera consentire l’accesso a contenuti per adulti dall’archivio applicazioni.|  
|**Area classificazioni**|Specifica il paese per il quale si desidera applicare restrizioni di classificazioni.|  
|**Classificazione film**|Specifica la classificazione massima consentita per il contenuto dei film.|  
|**Classificazione programma TV**|Specifica la classificazione massima consentita per il contenuto dei programmi TV.|  
|**Classificazione app**|Specifica la classificazione massima consentita per il contenuto delle app.| 
|**Contenuti da iBook Store contrassegnati come 'Erotici'** (solo supervisione)|Consente all'utente di scaricare i libri inclusi nella categoria relativa ai contenuti erotici.| 
  
> [!NOTE]  
>  Le classificazioni che è possibile selezionare variano a seconda dell’ **area classificazioni** selezionata.  
  
###  <a name="cloud"></a>Cloud  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Backup cloud**|Consente il backup su un servizio cloud come iCloud.|  
|**Backup crittografato**|Consente la crittografia del backup su un servizio cloud.|  
|**Sincronizzazione documenti**|Consente la sincronizzazione dei documenti a un servizio cloud.|  
|**Sincronizzazione foto**|Consente la sincronizzazione foto in un servizio cloud.| 
|**Libreria foto di iCloud**|Se è impostata su **No**, disabilita l'uso della libreria foto di iCloud che consente agli utenti di archiviare foto e video nel cloud. Le foto non completamente scaricate dalla libreria foto di iCloud nel dispositivo vengono rimosse dal dispositivo se l'opzione è impostata su **No**.|
|**Condivisione foto iCloud**|Impostare su **No** per disabilitare Condivisione foto iCloud sul dispositivo.|
|**Esegui handoff per continuare le attività nell'altro dispositivo**|Consente all'utente di continuare il lavoro iniziato su un dispositivo iOS in un altro dispositivo iOS o Mac OS X.|
|**Sincronizza i dati dalle app gestite a iCloud**|Consente alle app gestite con Intune di sincronizzare i dati con l'account iCloud dell'utente.|

  
###  <a name="security"></a>Sicurezza  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Fotocamera**|Consente di utilizzare la fotocamera del dispositivo.| 
|**Ritieni attendibili gli autori di una nuova app aziendale**|Consente all'utente di scegliere di considerare attendibili le app che non sono state scaricate dall'App Store.| 
  
###  <a name="roaming"></a>Roaming  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Roaming vocale**|Consente le chiamate vocali durante il roaming.|  
|**Sincronizzazione automatica durante il roaming**|Consente la sincronizzazione automatica del dispositivo durante il roaming.|  
|**Roaming dati**|Consente il roaming tra reti quando si accede a dati.|  
  
###  <a name="system-security"></a>Protezione del sistema  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Accettare certificati TLS non attendibili**|Se **consentito**, permette all'utente di accettare tali certificati. Se **non consentito**, rifiuta automaticamente i certificati non attendibili.|
|**Consenti blocco attivazione (solo modalità di supervisione)**|Usare questa impostazione per abilitare il blocco attivazione iOS Activation per i dispositivi iOS **con supervisione** gestiti. Per altre informazioni sul blocco attivazione, vedere [Gestire il blocco attivazione iOS con System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).
|**Centro di controllo schermata di blocco**|Controlla se l'applicazione di centro di controllo è accessibile quando il dispositivo è bloccato.|  
|**Visualizzazione notifiche schermata di blocco**|Controlla se è possibile visualizzare le notifiche quando il dispositivo è bloccato.|  
|**Visualizzazione Oggi schermata di blocco**|Controlla se è possibile visualizzare la vista Today quando il dispositivo è bloccato.|  
|**Modifica le impostazioni dell'account** (solo supervisione)|Consente all'utente di modificare le impostazioni dell'account, ad esempio le configurazioni di posta elettronica.|
|**Modifica le impostazioni dell'app Find My Friends** (solo supervisione)|Consente all'utente di modificare le impostazioni per l'app Find My Friends.|
|**Usa l'associazione di host per controllare i dispositivi a cui può essere associato un dispositivo iOS** (solo supervisione)|Abilita l'associazione di host per consentire all'amministratore di controllare i dispositivi a cui può essere associato un dispositivo iOS.|
|**Elimina tutti i contenuti e tutte le impostazioni** (solo supervisione)|Consente all'utente di eliminare tutti i contenuti e le impostazioni del dispositivo.|
|**Configura le restrizioni nel dispositivo** (solo supervisione)|Consente all'utente di configurare restrizioni (Controllo genitori) sul dispositivo.|
|**Installa i profili di configurazione e i certificati** (solo supervisione)|Consente all'utente di installare i certificati e i profili di configurazione.|
|**Password per le richieste in uscita di AirPlay**|Richiede una password di associazione quando l'utente usa AirPlay per trasmettere i contenuti ad altri dispositivi Apple.|
  
###  <a name="data-protection"></a>Protezione dati  
 Queste impostazioni si applicano solo ai dispositivi iOS.  
  
|Nome impostazione|Dettagli|  
|------------------|-------------|  
|**Apre i documenti nelle app gestite in altre app non gestite**|Per l'utilizzo con app gestite da Configuration Manager con criteri di gestione delle applicazioni.|  
|**Apre i documenti nelle app gestite in altre app gestite**|Per l'utilizzo con app gestite da Configuration Manager con criteri di gestione delle applicazioni.| 
|**Considera AirDrop come destinazione non gestita** (solo supervisione)|Impedisce alle app gestite di inviare dati tramite AirDrop.|
|**AirDrop** (solo supervisione)|Consente l'uso della funzionalità AirDrop per scambiare contenuti con dispositivi vicini.|
  
###  <a name="compliant-and-noncompliant-apps-ios"></a>App conformi e non conformi (iOS)  
 Consente di specificare un elenco di app iOS conformi oppure non conformi nella società. È quindi possibile usare i report per visualizzare i dispositivi nei quali sono installate app non conformi e gli utenti associati.  
  
 Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Per indicare le app conformi o non conformi  
  
1.  Nella pagina **App conformi e non conformi (iOS)** specificare le informazioni seguenti:  
  
    -   **Elenco App non conformi**: selezionare questa opzione per specificare un elenco di app da segnalare come non conformi se installate dagli utenti.  
  
    -   **Elenco App conformi**: selezionare questa opzione per specificare un elenco di app che gli utenti sono autorizzati a installare. Tutte le altre app installate verranno segnalate come non conformi.  
  
    -   **Aggiungi** aggiunge un'app all'elenco selezionato. Specificare un nome desiderato, facoltativamente l'autore dell'app e l'URL dell'app nell'App Store.  
  
         Per specificare l'URL, cercare l'app da usare nell'App Store di iTunes.  
  
         Aprire la pagina dell'app e copiare l'URL negli Appunti. A questo punto l'URL può essere usato in entrambi gli elenchi di app conformi e non conformi.  
  
         **Esempio:** cercare l'app **Microsoft Word per iPad** nell'App Store. L'URL usato sarà **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
    -   **Modifica**: consente di modificare il nome, l'autore e l'URL dell'app selezionata.  
  
    -   **Rimuovi**: elimina l'app selezionata dall'elenco.  
  
    -   **Importa**: importa un elenco di app specificate in un file con valori delimitati da virgole. Per il file usare il formato nome applicazione, autore, URL.  
  
2.  Al termine, fare clic su **Avanti**.  
  
 È possibile usare uno dei report seguenti per monitorare le app conformi e non conformi:  
  
-   **Elenco di app e dispositivi non conformi per un utente specificato** : Visualizza informazioni sugli utenti e sui dispositivi con app installate che non sono conformi ai criteri specificati.  
  
-   **Riepilogo degli utenti con app non conformi** : Visualizza informazioni sugli utenti che dispongono di app installate che non sono conformi ai criteri specificati.  
  
 Per informazioni sull'uso dei report, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>App conformi e non conformi (Mac OS X)  
 Consente di specificare un elenco di app Mac OS X conformi oppure non conformi nella società. È quindi possibile usare i report per visualizzare i dispositivi nei quali sono installate app non conformi e gli utenti associati.  
  
 Non è possibile specificare sia le app conformi che quelle non conformi nello stesso elemento di configurazione.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Per indicare le app conformi o non conformi  
  
1.  Nella pagina **App conformi e non conformi (Mac OS X)** specificare le informazioni seguenti:  
  
    -   **Elenco App non conformi**: selezionare questa opzione per specificare un elenco di app da segnalare come non conformi se installate dagli utenti.  
  
    -   **Elenco App conformi**: selezionare questa opzione per specificare un elenco di app che gli utenti sono autorizzati a installare. Tutte le altre app installate verranno segnalate come non conformi.  
  
    -   **Aggiungi** aggiunge un'app all'elenco selezionato. Specificare il nome scelto, l'autore dell'app (facoltativo) e l'ID bundle dell'app.  
  
        > [!TIP]  
        >  Per trovare l'ID bundle di un'app, usare i passaggi seguenti in un computer Mac in cui è installata l'app:  
        >   
        >  1.  Aprire la cartella in cui è installata l'app, ad esempio, **/Applications**  
        > 2.  Selezionare il bundle *<Nome app\>***.app** e scegliere **Show Package Contents** (Mostra contenuti pacchetto)  
        > 3.  Aprire il file **Info.plist**  
        > 4.  Controllare il valore associato alla chiave **CFBundleIdentifier**  
        >   
        >  Il formato per l'ID bundle è **com.contoso.nomeapp**  
  
    -   **Modifica**: consente di modificare il nome, l'autore e l'ID bundle dell'app selezionata.  
  
    -   **Rimuovi**: elimina l'app selezionata dall'elenco.  
  
    -   **Importa**: importa un elenco di app specificate in un file con valori delimitati da virgole. Nel file usare il formato, il nome dell'app, l'autore e l'ID bundle dell'app.  
  
2.  Al termine, fare clic su **Avanti**.  
  
 È possibile usare uno dei report seguenti per monitorare le app conformi e non conformi:  
  
-   **Elenco di app e dispositivi non conformi per un utente specificato** : Visualizza informazioni sugli utenti e sui dispositivi con app installate che non sono conformi ai criteri specificati.  
  
-   **Riepilogo degli utenti con app non conformi** : Visualizza informazioni sugli utenti che dispongono di app installate che non sono conformi ai criteri specificati.  
  
 Per informazioni sull'uso dei report, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
### <a name="ios-and-mac-os-x-custom-profile-settings"></a>Impostazioni dei profili personalizzati di iOS e Mac OS X  
 Usare i **profili personalizzati di iOS e Mac OS X** per distribuire le impostazioni create tramite lo [strumento Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) nei dispositivi iOS e Mac OS X. Questo strumento consente di creare molte impostazioni che controllano il funzionamento di questi dispositivi e di esportarle in un profilo di configurazione. È quindi possibile importare il profilo di configurazione nel profilo personalizzato di iOS e Mac OS X e distribuire le impostazioni a utenti e dispositivi nell'organizzazione.  
  
> [!NOTE]  
>  Assicurarsi che le impostazioni esportate dallo strumento Apple Configurator siano compatibili con la versione di iOS o Mac OS X sui dispositivi in cui viene distribuito il profilo. Per informazioni sulla risoluzione delle impostazioni incompatibili, cercare Configuration Profile Reference e Mobile Device Management Protocol Reference nel sito Web di [Apple Developer](https://developer.apple.com/) .  
  
#### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>Per creare un profilo personalizzato di iOS e Mac OS X  
  
1.  Nella pagina **Configura le impostazioni del profilo personalizzato di iOS e Mac OS X** della **Creazione guidata dell'elemento di configurazione**specificare le informazioni seguenti:  
  
    -   **Nome del profilo di configurazione personalizzato (visualizzato agli utenti)**: specificare un nome per il criterio con cui verrà visualizzato nel dispositivo e nei report di Configuration Manager.  
  
    -   **Importa**: scegliere un file esportato dallo strumento Apple Configurator.  
  
    -   **Dettagli del profilo di configurazione**: visualizza il file importato.  
  
    -   **Monitora e aggiorna impostazioni non conformi** -  
  
         Selezionare se si desidera monitorare e aggiornare le impostazioni di configurazione non conformi (se supportate).  
  
    -   **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato se i criteri di conformità vengono valutati come non conformi. I livelli di gravità disponibili sono i seguenti:  
  
        > [!NOTE]  
        >  Quando un dispositivo Mac OS X è in modalità di sospensione, criteri e profili non possono essere forniti né inclusi in un inventario. Di conseguenza, la console di Configuration Manager potrebbe visualizzare temporaneamente lo stato Impostazioni criteri errate fino alla successiva riattivazione del dispositivo dalla modalità sospensione.  
  
        -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
        -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni** per i report di Configuration Manager.  
  
        -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso** per i report di Configuration Manager.  
  
        -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager.  
  
        -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  
  
#### <a name="how-to-create-a-configuration-profile-file"></a>Come creare un file del profilo di configurazione  
 Il file del profilo di configurazione usato dai criteri personalizzati può essere creato in due modi:  
  
-   Esportare il file, con estensione **mobileconfig**, dallo strumento Apple Configurator.  
  
-   Creare il file manualmente usando lo schema appropriato dalla pagina delle [informazioni di riferimento sulle chiavi del profilo di configurazione Apple](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  
  
###  <a name="kiosk-mode-ios"></a>Modalità tutto schermo (iOS)  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS.  
  
#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>Per configurare la modalità tutto schermo per dispositivi iOS  
  
1.  Nella pagina di **Configura impostazioni modalità tutto schermo per dispositivi iOS** della **Creazione guidata dell'elemento di configurazione**specificare le seguenti informazioni:  
  
    -   **Seleziona app**: selezionare l'app che potrà essere eseguita quando il dispositivo è in modalità tutto schermo. Non sarà possibile eseguire altre applicazioni nel dispositivo. È possibile scegliere tra:  
  
        -   **App gestita e** - fare clic su Sfoglia, quindi selezionare un'app gestita.  
  
        -   **App dello Store** - specificare l'URL di un'app dell’app store, quindi fare clic su **Ottieni ID app** per popolare il campo **ID app** .  
  
         Per trovare l'URL dell'app:  
  
        -   Usando un motore di ricerca, individuare l'app da usare nell'App Store iTunes e aprire la pagina per l'app.  
  
        -   Copiare l'URL della pagina e usarlo come URL per specificare l'app da eseguire in modalità tutto schermo.  
  
        -   **Esempio:** cercare **Microsoft Word per iPad**. L'URL usato sarà **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
    -   **Tocco**: abilita o disabilita il touchscreen nel dispositivo.  
  
    -   **Rotazione schermo**: abilita o disabilita la modifica dell'orientamento dello schermo quando si ruota il dispositivo.  
  
    -   **Pulsanti volume**: abilita o disabilita l'uso dei pulsanti del volume del dispositivo.  
  
    -   **Commutatore suoneria**: abilita o disabilita la suoneria nel dispositivo.  
  
    -   **Pulsante di riattivazione sospensione schermo**: abilita o disabilita il pulsante di riattivazione sospensione dello schermo del dispositivo.  
  
    -   **Blocco automatico**: abilita o disabilita il blocco automatico del dispositivo.  
  
    -   **Audio mono**: abilita o disabilita l'impostazione di accessibilità **Audio mono**.  
  
    -   **Voice over**: abilita o disabilita l'impostazione di accessibilità **Voice over** per la lettura a voce alta del testo sullo schermo del dispositivo.  
  
    -   **Regolazioni di voice over**: abilita o disabilita le regolazioni del voice over che consentono di modificare la funzione Voice over, ad esempio la velocità con cui viene letto il testo visualizzato sullo schermo.  
  
    -   **Zoom**: abilita o disabilita l'impostazione di accessibilità **Zoom** che consente di usare le funzionalità di tocco per ingrandire la visualizzazione del dispositivo.  
  
    -   **Regolazioni dello zoom**: abilita o disabilita le regolazioni dello zoom che consentono di modificare la funzione di zoom.  
  
    -   **Inversione colori**: abilita o disabilita l'impostazione di accessibilità **Inversione colori** che consente di regolare la visualizzazione per gli utenti con problemi visivi.  
  
    -   **Regolazioni dell'inversione colori**: abilita o disabilita le regolazioni dell'inversione colori che consentono di modificare la funzione Inversione colori.  
  
    -   **Tocco per l'accesso facilitato**: abilita o disabilita l'impostazione di accessibilità **Tocco per l'accesso facilitato** che consente agli utenti di eseguire sullo schermo movimenti che potrebbero essere difficili da eseguire.  
  
    -   **Regolazioni del tocco per l'accesso facilitato**: abilita o disabilita le regolazioni del tocco per l'accesso facilitato che consentono di modificare la funzione Tocco per l'accesso facilitato.  
  
    -   **Selezione comandi vocali**: abilita o disabilita l'impostazione di accessibilità **Leggi selezione** che consente di leggere a voce alta il testo selezionato.  
  
    -   **Monitora e aggiorna impostazioni non conformi**: selezionare se si vogliono monitorare e aggiornare le impostazioni di configurazione non conformi (se supportate).  
  
    -   **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato se i criteri di conformità vengono valutati come non conformi. I livelli di gravità disponibili sono i seguenti:  
  
        -   **Nessuno**: i dispositivi che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
        -   **Informazioni**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni** per i report di Configuration Manager.  
  
        -   **Avviso**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso** per i report di Configuration Manager.  
  
        -   **Errore critico**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager.  
  
        -   **Errore critico con evento**: i dispositivi che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel log eventi dell'applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi di configurazione per dispositivi gestiti senza il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)

