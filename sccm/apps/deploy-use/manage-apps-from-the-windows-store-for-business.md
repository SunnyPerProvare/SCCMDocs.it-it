---
title: Gestire le app da Windows Store per le aziende | Microsoft Docs
description: Gestire e distribuire le app da Windows Store per le aziende usando System Center Configuration Manager.
ms.custom: na
ms.date: 11/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3847a85c11d7b72b84095ba9add563bdf5c49a75
ms.openlocfilehash: 605cdd01d767dda3467198f5e6539448f9b559f6

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gestire le app da Windows Store per le aziende con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, con contratti singoli o multilicenza. Collegando lo Store a Configuration Manager è possibile sincronizzare l'elenco delle app acquistate, visualizzarle nella console di Configuration Manager e distribuirle come qualsiasi altra app.


## <a name="online-and-offline-apps"></a>App online e offline

Windows Store per le aziende supporta due tipi di app:

- **Online**: con questo tipo di licenza è necessario che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory.
- **Offline**: le organizzazioni possono memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale senza connettersi allo Store o avere una connessione Internet.

Altre informazioni su [Windows Store per le aziende](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager supporta la gestione delle app di Windows Store per le aziende su dispositivi Windows 10 che eseguono il client di Configuration Manager e su dispositivi Windows 10 registrati in Microsoft Intune (configurazione ibrida). Configuration Manager offre le funzionalità seguenti per le app online e offline.

> [!IMPORTANT]
> Per usare queste funzionalità, è necessario che i dispositivi Windows 10 eseguano la versione di novembre 2015 (1511) o una versione successiva.

|Funzionalità|App offline|App online|
|------------|------------|------------|
|Sincronizzazione dei dati delle app in Configuration Manager<br>(La sincronizzazione viene eseguita ogni 24 ore, oppure è possibile avviare una sincronizzazione immediata)|Sì|Sì|
|Creazione di applicazioni di Configuration Manager dalle app dello Store|Sì|Sì|
|Supporto delle app gratuite dello Store|Sì|Sì<sup>1</sup>|
|Supporto delle app a pagamento dello Store|No|Sì<sup>1</sup>|
|Supporto delle distribuzioni richieste nelle raccolte di utenti e dispositivi|Sì|Sì<sup>1</sup>|
|Supporto delle distribuzioni disponibili nelle raccolte di utenti e dispositivi|Sì<sup>2</sup>|No|

<sup>1</sup>Supportata solo per i dispositivi gestiti da Intune. Sebbene sia possibile creare un'applicazione online nella console di Configuration Manager e distribuirla in un dispositivo gestito dal client di Configuration Manager, la distribuzione avrà esito negativo. L'utente finale verrà reindirizzato alla pagina dell'App Store da cui dovrà eseguire l'installazione manuale dell'app.

<sup>2</sup>Supportata solo per i dispositivi gestiti con il client di Configuration Manager.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>Configurare la sincronizzazione di Windows Store per le aziende

> [!IMPORTANT]
> Quando si configura una connessione tra Configuration Manager e Windows Store per le aziende, è necessario specificare una cartella in cui verranno mantenuti i contenuti delle app sincronizzati dall'archivio.
Per assicurarsi che questa cartella sia protetta e che il relativo contenuto possa essere distribuito ai dispositivi, verificare che siano disponibili le autorizzazioni seguenti:
-   Il computer in cui si installa il ruolo del sistema del sito del punto di connessione del servizio (sito di livello superiore nella gerarchia) deve essere in possesso delle autorizzazioni lettura e scrittura per la cartella specificata quando si usa l'account **Computer$**.
-   L'autore di app deve essere in possesso delle autorizzazioni di lettura per la cartella specificata.
-   L'account **Computer$** di ogni computer che ospita un'istanza del provider SMS deve essere in grado di usare la cartella specificata.


In Azure Active Directory registrare Configuration Manager come strumento di gestione Applicazione Web o API Web. Si riceverà un ID client che sarà necessario in seguito.
1. Nel nodo Active Directory [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory e scegliere **Applicazioni** > **Aggiungi**.
2.  Scegliere **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e scegliere **Avanti**.
4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**. L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio, è possibile immettere *https://dominio/sccm*.
5.  Completa la procedura guidata.

In Azure Active Directory creare una chiave client per lo strumento di gestione registrato.
1.  Evidenziare l'applicazione appena creata e scegliere **Configura**.
2.  In **Chiavi** selezionare una durata nell'elenco e scegliere **Salva**. Verrà creata una nuova chiave client. Non uscire dalla pagina fino a quando non è stato completato il caricamento di Windows Store per le aziende in Configuration Manager.

In Windows Store per le aziende configurare Configuration Manager come strumento di gestione dello Store.
1.  Aprire [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e, se richiesto, eseguire l'accesso.
2.  Accettare le condizioni per l'utilizzo, se necessario.
3.  In **Strumenti di gestione** scegliere **Add a management tool** (Aggiungi strumento di gestione).
4.  In **Search for the tool by name** (Cerca strumento per nome) digitare il nome dell'applicazione creata in precedenza in Azure Active Directory e scegliere **Aggiungi**.
5.  Scegliere **Attiva** accanto all'applicazione appena importata.
6.  Nella pagina **Gestisci > Informazioni account** selezionare **Show Offline-Licensed Apps** (Mostra app con licenza offline) per consentire l'acquisto di app con licenza offline.

Aggiungere l'account dello Store in Configuration Manager.

1. Acquistare almeno un'app da Windows Store per le aziende. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e scegliere **Windows Store per le aziende**.
2.  Nella scheda **Home** nel gruppo **Windows Store per le aziende** fare clic su **Add Windows Store for Business Account** (Aggiungi account di Windows Store per le aziende).
3.  Aggiungere ID tenant, ID client e chiave privata del client da Azure Active Directory e completare la procedura guidata.
4. Al termine verrà visualizzato l'account configurato nell'elenco di **Windows Store per le aziende** nella console di Configuration Manager.

Modificare le lingue dell'applicazione che verranno visualizzate nel Catalogo applicazioni per il download.

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager scegliere **Servizi cloud** > **Aggiornamenti e manutenzione** > **Windows Store per le aziende**.
2.  Selezionare l'account Windows Store per le aziende e scegliere **Proprietà**.
3.  Selezionare la scheda **Lingua**.
4.  Aggiungere o rimuovere le lingue che verranno visualizzate nel Catalogo applicazioni. Selezionare la lingua predefinita del Catalogo applicazioni che verrà resa disponibile agli utenti.

>[!IMPORTANT]
>In questa versione, se si modificano le lingue che verranno sincronizzate, è necessario riavviare il servizio SMS Executive nel server del sito prima di rendere effettive le impostazioni della lingua.


Modificare la chiave privata del client da Azure Active Directory.

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager scegliere **Servizi cloud** > **Aggiornamenti e manutenzione** > **Windows Store per le aziende**.
2.  Selezionare l'account Windows Store per le aziende e scegliere **Proprietà**.
3.  Nella finestra di dialogo **Windows Store for Business Account Properties** (Proprietà account Windows Store per le aziende) immettere una nuova chiave nel campo **Client secret key** (Chiave privata client) e scegliere **Verifica**. Al termine della verifica, fare clic su **Applica** e chiudere la finestra di dialogo.

## <a name="synch-apps-from-the-store-with-configuration-manager"></a>Sincronizzare le app dallo Store con Configuration Manager

La sincronizzazione viene eseguita ogni 24 ore, oppure è possibile avviare una sincronizzazione immediata con la procedura seguente:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager scegliere **Servizi cloud** > **Aggiornamenti e manutenzione** > **Windows Store per le aziende**.
3.  Nella scheda **Home** nel gruppo **Sincronizza** scegliere **Sincronizza ora**.
4.  L'app acquistata viene visualizzata nel nodo **Informazioni di licenza per le app dello Store** dell'area di lavoro **Gestione applicazioni**.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Creare e distribuire un'applicazione di Configuration Manager da un'app di Windows Store per le aziende

Questa procedura presuppone di aver acquisito almeno un'app gratuita o acquistato almeno un'app con pagamento online della licenza da Windows Store per le aziende.

1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.
2.  Scegliere l'app che si vuole distribuire e quindi nella scheda **Home** nel gruppo **Crea** scegliere **Crea applicazione**.
Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. Sarà quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.

> [!IMPORTANT]
> Per i dispositivi registrati in Intune, le app distribuite sono disponibili solo per l'utente che ha originariamente registrato il dispositivo. Nessun altro utente può usare l'app.

## <a name="monitor-windows-store-for-business-apps"></a>Monitorare Windows Store per le app aziendali

Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e scegliere **Informazioni di licenza per le app dello Store**.

Per ogni app dello Store gestita è possibile visualizzare informazioni che includono nome, piattaforma, numero di licenze per l'app acquistate e numero di licenze disponibili.



<!--HONumber=Dec16_HO3-->


