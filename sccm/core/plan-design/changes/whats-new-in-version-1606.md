---
title: "Novità della versione 1606 | System Center Configuration Manager"
description: "Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1606 di System Center Configuration Manager."
ms.custom: na
ms.date: 10/09/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
caps.latest.revision: 40
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 8de28e112a2d7faf1d8aca9b7214498e9a65f919

---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>Novità della versione 1606 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'aggiornamento 1606 per System Center Configuration Manager è un aggiornamento nella console per siti installati in precedenza che eseguono la versione 1511 o 1602. La versione 1511 è la versione di base iniziale usata per installare nuovi siti di Configuration Manager.
> [!TIP]  
>  Sono disponibili altre informazioni su:  
>   
>  -   [Installing new sites](/sccm/core/servers/deploy/install) (Installazione di nuovi siti) (con una versione di base, ad esempio 1511)  
>  -   [Installing updates at sites](/sccm/core/servers/manage/updates) (Installazione di aggiornamenti nei siti) (ad esempio versione 1602 o 1606)  

 Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1606 di Configuration Manager.  



## <a name="a-nameupdatesandservicingaupdates-and-servicing"></a><a name="updatesandservicing"></a>Aggiornamenti e manutenzione

### <a name="changes-for-the-updates-and-servicing-node"></a>Modifiche per il nodo Aggiornamenti e manutenzione
Di seguito sono riportate le modifiche del nodo Aggiornamenti e manutenzione nella console di Configuration Manager:
> [!NOTE]
> Le modifiche saranno disponibili solo dopo l'installazione della versione 1606.

- **Modifica del nome del nodo:**

    Nell'area di lavoro **Monitoraggio** il nodo dello stato **Manutenzione del sito** è stato rinominato in **Aggiornamenti e stato di manutenzione**.
- **Altri stati di installazione:**

    Quando si visualizza lo stato di installazione dell'aggiornamento di un sito, nella console vengono ora mostrate informazioni distinte per le azioni seguenti:
    - **Download** (si applica solo al sito di livello superiore in cui è installato il ruolo del sistema del sito del punto di connessione del servizio)
    - **Replica**
    - **Controllo dei prerequisiti**
    - **Installazione**

  Inoltre, sono ora presenti più informazioni dettagliate per ogni passaggio, incluso il file di log nel quale è possibile visualizzare altre informazioni.  
-   **Nuova opzione per ignorare i messaggi sui prerequisiti non soddisfatti:**

    In entrambe le aree di lavoro **Amministrazione** e **Monitoraggio** il nodo **Aggiornamenti e manutenzione** include un nuovo pulsante sulla barra multifunzione denominato **Ignora avvisi dei prerequisiti**.

    Se si installa un aggiornamento senza usare l'opzione Ignora avvisi dei prerequisiti dalla procedura guidata e l'installazione dell'aggiornamento viene interrotta da un **avviso relativo ai prerequisiti** senza che si siano verificati errori, è possibile selezionare **Ignora avvisi dei prerequisiti** dalla barra multifunzione per riprendere automaticamente l'installazione ignorando gli avvisi dei prerequisiti.  



- **Visualizzazione più chiara degli aggiornamenti:**

    Quando si visualizza il nodo **Aggiornamenti e manutenzione**, ora è possibile visualizzare solo l'aggiornamento installato più recente e qualsiasi nuovo aggiornamento disponibile per l'installazione. Per visualizzare gli aggiornamenti installati in precedenza, fare clic sul nuovo pulsante **Cronologia** nella barra multifunzione.  

-   **Opzioni ridenominate per la fase di pre-produzione:**

    Nel nodo Aggiornamenti e manutenzione, il pulsante che era denominato **Opzioni client** è ora stato denominato **Alza di livello il client di pre-produzione**.


###  <a name="pre-release-features"></a>Funzionalità di versioni non definitive
A partire dalla versione 1606, è necessario dare il consenso all'uso delle funzionalità di versioni non definitive in System Center Configuration Manager per poterle selezionare e abilitarne l'uso. Per altre informazioni, vedere la sezione relativa all'[abilitazione delle funzionalità facoltative dagli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Nuovo comportamento di aggiornamento dei punti di distribuzione
L'aggiornamento 1606 introduce modifiche che migliorano la disponibilità dei punti di distribuzione durante l'installazione degli aggiornamenti successivi.

Dopo l'installazione dell'aggiornamento 1606, quando nel sito verrà installato un aggiornamento che richiede la reinstallazione automatica dei ruoli del sistema del sito del punto di distribuzione standard e pull, i punti di distribuzione non andranno offline contemporaneamente. Al contrario, il server del sito usa le impostazioni di distribuzione del contenuto del sito per distribuire l'aggiornamento a un sottoinsieme di punti di distribuzione alla volta. Ne consegue che solo alcuni punti di distribuzione saranno offline per consentire l'installazione dell'aggiornamento. I punti di distribuzione per i quali non è stato avviato l'aggiornamento o che lo hanno completato restano in linea e continuano a fornire contenuto ai client.



## <a name="a-nameaccessibilitya-accessibility"></a><a name="accessibility"></a> Accessibilità
A partire dalla versione 1606, per spostarsi tra i vari nodi di un'area di lavoro è possibile immettere la prima lettera del nome del nodo. Quando si preme il tasto, il cursore si sposta sul nodo successivo che inizia con tale lettera; se si usa un'utilità per la lettura dello schermo, verrà letto il nome del nodo. Per altre informazioni sulle opzioni di accessibilità, vedere [Funzionalità di accessibilità di System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="a-nameadministrationaadministration"></a><a name="administration"></a>Amministrazione
Di seguito sono riportate le modifiche del nodo Amministrazione nella console di Configuration Manager:
### <a name="oms-connector"></a>Connettore OMS

È ora possibile connettere le raccolte di Configuration Manager da System Center Configuration Manager a [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/en-us/documentation/articles/operations-management-suite-overview/). In questo modo i dati, ad esempio le raccolte delle distribuzioni di Configuration Manager, sono visibili in OMS. Altre informazioni sulla [sincronizzazione dei dati da Configuration Manager in Microsoft Operations Management Suite](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

Il connettore OMS è una funzionalità di versione non definitiva. Per abilitarla, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Supporto per la dimensione della cache in Impostazioni client

È ora possibile configurare la dimensione della cartella cache nei computer client usando Impostazioni client nella console di Configuration Manager. In precedenza, era possibile impostare la dimensione della cache client soltanto durante l'installazione o la reinstallazione del software client, usando la proprietà SMSCACHESIZE. Ora è possibile specificare la dimensione della cache come impostazione client predefinita o personalizzata e quindi applicare tale impostazione al successivo aggiornamento dei criteri nel client, senza dover reinstallare il client stesso. Per altre informazioni, vedere [Configurare la cache del client per i client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestione dei dispositivi mobili (MDM) locale

### <a name="support-for-multiple-device-management-points"></a>Supporto per più punti di gestione periferiche

Gestione di dispositivi mobili (MDM) locale supporta ora una nuova funzionalità dell'aggiornamento dell'anniversario di Windows 10 che configura automaticamente un dispositivo registrato affinché usi più di un punto di gestione periferiche. Questa funzionalità consente al dispositivo il fallback su un altro punto di gestione periferiche quando quello che usa di solito non è disponibile. La funzionalità è operativa solo nei PC e nei dispositivi nei quali è stato installato l'aggiornamento dell'anniversario di Windows 10.


## <a name="application-management"></a>Gestione delle applicazioni

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gestire le app da Windows Store per le aziende

In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, singolarmente o con Volume Purchase Program. Collegando lo store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate, visualizzarle nella console di Configuration Manager e distribuirle come qualsiasi altra app.

Per informazioni dettagliate, vedere [Gestire le app da Windows Store per le aziende con System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gestione delle app iOS acquistate con Volume Purchase Program

Il flusso di lavoro per la gestione delle app iOS acquistate con Volume Purchase Program e per la loro distribuzione con Configuration Manager è stato migliorato.

Per informazioni dettagliate, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program con System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interfaccia utente di Software Center

L'interfaccia di Software Center è stata ottimizzata per semplificare l'esperienza utente finale.
*  Le schede **Stato dell'installazione** e **Software installato** sono state unificate nella scheda **Stato dell'installazione**.
*  **Aggiornamenti**, **Sistemi operativi** e **Applicazioni** sono ora tre schede distinte.
* È possibile selezionare più aggiornamenti da installare singolarmente, o installare tutti gli aggiornamenti contemporaneamente facendo clic sul pulsante **Install all** (Installa tutti).

### <a name="content-status-links"></a>Collegamenti allo stato del contenuto
Quando si visualizzano le proprietà di un'applicazione o di un pacchetto, è ora presente un collegamento che indirizza allo stato dell'oggetto visualizzato.

## <a name="software-updates"></a>Aggiornamenti software

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Impostazione del client per la gestione dell'agente client di Office 365
È ora possibile utilizzare un'impostazione del client Configuration Manager per gestire l'agente client di Office 365. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager comunica con l'agente client di Office 365 al fine di scaricare gli aggiornamenti di Office 365 da un punto di distribuzione e installarli.

Per informazioni dettagliate, vedere [Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Passaggio manuale dei client a un nuovo punto di aggiornamento software
È possibile abilitare l'opzione per consentire ai client di Configuration Manager di passare a un nuovo punto di aggiornamento software quando si verificano problemi con il punto di aggiornamento software attivo. Dopo che l'opzione è stata abilitata, in occasione dell'analisi successiva il client cercherà un altro punto di aggiornamento software.

Per informazioni dettagliate, vedere [Pianificare gli aggiornamenti software in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software
Quando un aggiornamento software che richiede il riavvio viene distribuito tramite Configuration Manager e viene installato in un computer, viene pianificato un riavvio in sospeso e viene visualizzata una finestra di dialogo di riavvio. A partire da Configuration Manager versione 1606, ogni volta che è pianificato un riavvio in sospeso per un aggiornamento software di Configuration Manager nei computer Windows 10 tra le opzioni di risparmio energia di Windows sono disponibili le opzioni **Aggiorna e riavvia**e **Aggiorna e arresta** . Dopo che una di queste opzioni è stata usata e il computer è stato riavviato, la finestra di dialogo di riavvio non verrà visualizzata.

Per informazioni dettagliate, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo

### <a name="improvements-to-the-install-software-updates-task-sequence-step"></a>Miglioramenti del passaggio sequenza di attività Installa aggiornamenti software
La nuova impostazione **Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache** consente l'esecuzione di un'analisi completa degli aggiornamenti software invece di usare i risultati dell'analisi memorizzati nella cache. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività in System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

È inoltre disponibile la nuova variabile di sequenza di attività **SMSTSSoftwareUpdateScanTimeout** che consente di controllare il timeout dell'analisi degli aggiornamenti software durante il passaggio della sequenza di attività Installa aggiornamenti software. Il valore predefinito è 30 minuti. Per informazioni dettagliate, vedere [Variabili predefinite della sequenza di attività in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata
A partire dalla versione 1606 di Configuration Manager, questa variabile della sequenza di attività è stata deprecata. A partire dalla versione 1606 di Configuration Manager, durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows stabilisce qual è la lettera di unità migliore da usare (in genere C:).

Per informazioni dettagliate, vedere [Variabili predefinite della sequenza di attività in System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personalizzazione delle dimensioni della finestra TFTP RamDisk nei punti di distribuzione abilitati per PXE
È ora possibile personalizzare le dimensioni della finestra nei punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout perché le dimensioni della finestra sono troppo grandi. La personalizzazione delle dimensioni della finestra TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare requisiti di rete specifici.

Per informazioni dettagliate, vedere [Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo con System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Impostazioni di conformità

### <a name="smart-lock-setting-for-android-devices"></a>Impostazione di Smart Lock per dispositivi Android
La nuova impostazione **Consenti Smart Lock e altri agenti di attendibilità** è stata aggiunta all'elemento di configurazione Android e Samsung KNOX.

L'impostazione consente di controllare la funzionalità Smart Lock su dispositivi compatibili con Android. Questa funzionalità del telefono, talvolta nota anche come agenti di attendibilità, consente di disabilitare o ignorare la password della schermata di blocco del dispositivo se il dispositivo si trova in una posizione attendibile, ad esempio quando è connesso a un dispositivo Bluetooth specifico oppure quando è nelle vicinanze di un tag NFC. È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock.

Per informazioni dettagliate, vedere [Come creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client di System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Configurazione e protezione del dispositivo

### <a name="product-name-changes"></a>Modifiche del nome del prodotto

* Microsoft Passport for Work è ora noto come **Windows Hello per le aziende**.
* Enterprise Data Protection è ora noto come **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Distribuzione di Windows Hello per le aziende (Passport for Work)

È ora possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 e gestiti dal client di Configuration Manager.

La console di Configuration Manager è stata aggiornata per riflettere tali modifiche.

### <a name="ios-activation-lock"></a>Blocco attivazione di iOS
Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Quando il blocco attivazione iOS è abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima che sia possibile:
* Disattivare Trova il mio iPhone
* Cancellare il dispositivo
* Riattivare il dispositivo

Configuration Manager consente di gestire il blocco attivazione in due modi:

1. Abilitando il blocco attivazione nei dispositivi con supervisione.
2. Effettuando il bypass del blocco attivazione nei dispositivi con supervisione.

Per informazioni dettagliate, vedere [Gestire il blocco attivazione iOS con System Center Configuration Manager](../../../mdm/deploy-use/manage-ios-activation-lock.md).


### <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

Endpoint Protection facilita la gestione e il monitoraggio di Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP è un nuovo servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti. I criteri di Configuration Manager possono aiutare a caricare e monitorare Windows 10, versione 1607 (build 14328) o versione successiva.

Per informazioni dettagliate, vedere [Windows Defender Advanced Threat Protection](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Categorie di dispositivi
È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivo quando eseguono la registrazione di un dispositivo in Intune. È anche possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

Per informazioni dettagliate, vedere [Come classificare automaticamente i dispositivi in raccolte con System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predichiarare dispositivi con i numeri di serie IMEI o iOS

È possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity) o i numeri di serie iOS. È possibile caricare un file con valori separati da virgola (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi. Le informazioni importate imposteranno la **proprietà** dei dispositivi registrati come "**Corporate**" negli elenchi di dispositivi. È tuttavia necessaria una licenza di Intune per ogni utente che accede al servizio.

Per informazioni dettagliate, vedere [Predichiarare dispositivi con i numeri di serie IMEI o iOS](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Comunicazione del servizio di attestazione dell'integrità locale

È ora possibile abilitare il monitoraggio dei servizi di Attestazione dell'integrità per i PC Windows 10 usando solo l'infrastruttura locale, in modo che i computer senza accesso a Internet possano creare report di attestazione dell'integrità dei dispositivi.

Per informazioni dettagliate, vedere [Attestazione dell'integrità per System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#How-to-enable-Health-Attestation-service-communication-on-Configuration-Manager-client-computers).  

## <a name="remote-control"></a>Controllo remoto
Offre agli utenti finali la possibilità di accettare o rifiutare il trasferimento di file prima di trasferire il contenuto degli appunti condivisi in una sessione di controllo remoto. Gli utenti finali dovranno concedere l'autorizzazione una sola volta per sessione e il visualizzatore non avrà la possibilità di concedere l'autorizzazione per procedere con il trasferimento dei file. La nuova impostazione è disponibile nell'area di lavoro **Amministrazione**. Passare a **Impostazioni client** quindi aprire il riquadro **Strumenti remoti** in **Impostazioni predefinite**.



<!--HONumber=Nov16_HO1-->


