---
title: Gestire le app da Windows Store per le aziende | Microsoft Docs
description: Gestire e distribuire le app da Windows Store per le aziende usando System Center Configuration Manager.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 369b6a82a20a90ca534f9484c0be71096dd35a30
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gestire le app da Windows Store per le aziende con System Center Configuration Manager
In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate con Configuration Manager. È quindi possibile visualizzare le app nella console di Configuration Manager e distribuirle come si distribuisce qualsiasi altra app.


## <a name="online-and-offline-apps"></a>App online e offline

Windows Store per le aziende supporta due tipi di app:

- **Online**: con questo tipo di licenza è necessario che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory.
- **Offline**: consente di memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale senza connettersi allo Store o avere una connessione Internet.

[Altre informazioni](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) su Windows Store per le aziende.

Configuration Manager supporta la gestione delle app di Windows Store per le aziende su dispositivi Windows 10 che eseguono il client di Configuration Manager e su dispositivi Windows 10 registrati in Microsoft Intune (configurazione ibrida). Configuration Manager offre le funzionalità seguenti per le app online e offline.

> [!IMPORTANT]
> Per usare questa funzionalità, è necessario che i dispositivi Windows 10 eseguano la versione di novembre 2015 (1511) o una versione successiva.


|Funzionalità|App offline|App online|
|------------|------------|------------|
|Sincronizzazione dei dati delle app in Configuration Manager<br>(la sincronizzazione viene eseguita ogni 24 ore)|Sì|Sì|
|Creazione di applicazioni di Configuration Manager dalle app dello Store|Sì|Sì|
|Supporto delle app gratuite dello Store|Sì|Sì|
|Supporto delle app a pagamento dello Store|No|Sì|
|Supporto delle distribuzioni richieste nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle distribuzioni disponibili nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle app line-of-business dello Store|Sì|Sì|

Per distribuire app con licenza online a PC Windows 10 con il client di Configuration Manager, è necessario che sia in esecuzione Windows 10 Creators Update o versione successiva.

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Distribuzione di app online tramite Windows Store per le aziende con PC che eseguono il client di Configuration Manager
Prima di distribuire app di Windows Store per le aziende a PC che eseguono il client completo di Configuration Manager, considerare quanto segue:

- Per la funzionalità completa, nei PC deve essere in esecuzione Windows 10 Creators Update o versione successiva.
- I PC devono essere aggiunti all'area di lavoro di Azure Active Directory e devono trovarsi nello stesso tenant di AAD in cui Windows Store per le aziende è stato registrato come strumento di gestione.
- Quando i PC sono connessi con l'account Administrator predefinito, non possono accedere alle app di Windows Store per le aziende.
- I PC devono avere una connessione Internet dinamica a Windows Store per le aziende.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Note per i PC che eseguono versioni precedenti di Windows 10
Nei PC che eseguono una versione di Windows 10 precedente la versione Creators Update (con il client di Configuration Manager) si verifica quanto segue:


- Quando l'installazione è imposta dall'utente che installa l'applicazione, dall'applicazione che ha raggiunto il termine di scadenza dell'installazione o dalla rivalutazione post-installazione per le distribuzioni richieste:
    - L'applicazione viene "imposta" dall'avvio dell'app di Windows Store per le aziende. 
    - L'utente finale deve quindi completare l'installazione dallo Store prima che l'app venga installata
    - Lo stato dell'applicazione nella console di Configuration Manager indica l'esito negativo con l'errore "L'app di Windows Store è stata aperta nel computer client ed è in attesa del completamento dell'installazione da parte dell'utente".
- Al successivo ciclo di valutazione dell'applicazione:
    - Se l'applicazione è stata installata dall'utente finale dallo Store, lo stato indica che l'**operazione è riuscita**. 
    - Se l'utente finale non ha provato a installare l'app dallo Store:
        - Le distribuzioni richieste proveranno ad avviare lo Store e a imporre nuovamente l'installazione dell'applicazione.
        - Le distribuzioni disponibili non vengono nuovamente imposte.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Altre note per i PC che eseguono versioni precedenti di Windows 10:

- Non è possibile distribuire app line-of-business da Windows Store per le aziende
- Quando si distribuiscono app a pagamento dallo Store, gli utenti finali devono accedere allo Store e acquistare le app.
- Se sono stati distribuiti criteri di gruppo che disabilitano l'accesso alla versione consumer di Windows Store, le distribuzioni di Windows Store per le aziende non funzionano, anche se Windows Store per le aziende è abilitato.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configurare la sincronizzazione di Windows Store per le aziende

### <a name="for-configuration-manager-versions-prior-to-1706"></a>Per le versioni di Configuration Manager precedenti alla versione 1706

**In Azure Active Directory registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web". Questa azione rende disponibile un ID client che sarà necessario in un secondo tempo.**
1. Nel nodo Active Directory di [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory e quindi fare clic su **Applicazioni** > **Aggiungi**.
2.  Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e quindi fare clic sulla freccia **Avanti**.
4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**. L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio, è possibile immettere *https://dominio/sccm*.
5.  Completare la procedura guidata.

**In Azure Active Directory creare una chiave client per lo strumento di gestione registrato**
1.  Evidenziare l'applicazione creata e fare clic su **Configura**.
2.  In **Chiavi** selezionare una durata nell'elenco e fare clic su **Salva**. Questa azione crea una nuova chiave client. Non uscire dalla pagina fino a quando non è stato completato il caricamento di Windows Store per le aziende in Configuration Manager.

**In Windows Store per le aziende configurare Configuration Manager come strumento di gestione dello Store**
1.  Aprire [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e, se richiesto, eseguire l'accesso.
2.  Accettare le condizioni per l'utilizzo, se necessario.
3.  In **Management Tools** (Strumenti di gestione) fare clic su **Add a management tool** (Aggiungi strumento di gestione).
4.  In **Search for the tool by name** digitare il nome dell'applicazione creata in precedenza in AAD e quindi fare clic su **Add**.
5.  Fare clic su **Activate** (Attiva) accanto all'applicazione importata.
6.  Nella pagina **Manage > Account Information** (Gestisci > Informazioni account) selezionare **Show Offline-Licensed Apps** (Mostra app con licenza offline) per consentire l'acquisto di app con licenza offline.

**Aggiungere l'account dello Store in Configuration Manager**

1. Verificare di avere acquistato almeno un'app da Windows Store per le aziende. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Windows Store per le aziende**.
2.  Nella scheda **Home** nel gruppo **Windows Store per le aziende** fare clic su **Aggiungere un account di Windows Store per le aziende**. 
3.  Aggiungere l'ID tenant, l'ID client e la chiave client da Azure Active Directory, quindi completare la procedura guidata.
4. Al termine viene visualizzato l'account configurato nell'elenco di **Windows Store per le aziende** nella console di Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Per Configuration Manager versione 1706 e successive

1. Nella console passare a **Amministrazione** > **Panoramica** > **Cloud Services Management (Gestione dei servizi cloud)** > **Azure** > **Servizi di Azure** e quindi scegliere **Configure Azure Services (Configura servizi di Azure)** per avviare **Azure Services Wizard (Configurazione guidata servizi di Azure)**.
2. Nella pagina **Servizi di Azure** selezionare il servizio che si vuole configurare e quindi fare clic su **Avanti**.
3. Nella pagina **Generale** specificare un nome descrittivo per il servizio di Azure e una descrizione facoltativa, quindi fare clic su **Avanti**.
4. Nella pagina **App** specificare l'ambiente di Azure e quindi fare clic su **Sfoglia** per aprire la finestra **App server**.
5. Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**. Le app server sono app Web di Azure che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client. Se non è disponibile un'app server, usare una delle opzioni seguenti:
    - **Crea:** per creare una nuova app server, fare clic su **Crea**. Specificare un nome descrittivo per l'app e il tenant. Quindi, dopo avere effettuato l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, inclusi l'ID Client e la chiave privata da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.
    - **Importa:** per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver fatto clic su **Verifica** per verificare le informazioni, fare clic su **OK** per continuare. 
6. Controllare la pagina **Informazioni** ed eseguire gli eventuali passaggi aggiuntivi e le configurazioni indicati. Queste configurazioni sono necessarie per usare il servizio con Configuration Manager. Ad esempio, per configurare Windows Store per le aziende:
    - In Azure è necessario registrare Configuration Manager come applicazione Web o API Web e registrare l'ID client. È anche necessario specificare una chiave client utilizzabile dallo strumento di gestione, ovvero Configuration Manager.
    - Nella console di Windows Store per le aziende è necessario configurare Configuration Manager come strumento di gestione dello Store, abilitare il supporto per le app con licenza offline e quindi acquistare almeno un'app. 
7. Quando si è pronti per continuare, fare clic su **Avanti**.
8. Nella pagina **Configurazioni dell'applicazione** completare le configurazioni per il catalogo app e la lingua per il servizio, quindi fare clic su **Avanti**.
9. Al termine della procedura guidata, nella console di Configuration Manager viene indicato che **Windows Store per le aziende** è stato configurato come **Tipo di servizio cloud**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Creare e distribuire un'applicazione di Configuration Manager da un'app di Windows Store per le aziende.
1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.
2.  Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.
Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. Sarà quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.

> [!IMPORTANT]
> Per i dispositivi registrati in Intune, le app distribuite sono disponibili solo per l'utente che ha originariamente registrato il dispositivo. Nessun altro utente può accedere all'app.

## <a name="next-steps"></a>Passaggi successivi

Nell'area di lavoro **Raccolta software** espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.

Per ogni app dello Store gestita è possibile visualizzare informazioni che includono nome, piattaforma, numero di licenze per l'app acquistate e numero di licenze disponibili.
