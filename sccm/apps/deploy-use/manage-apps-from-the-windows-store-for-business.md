---
title: Gestire le app da Microsoft Store per le aziende
titleSuffix: Configuration Manager
description: Gestire e distribuire le app da Microsoft Store per le aziende usando System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 15644a8c1acdbde85c7ca194a72a10c3cc2c0fcc
ms.sourcegitcommit: f1535281b2c3fecff773b722c3f7590bf6ba10a0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/03/2018
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Gestire le app da Microsoft Store per le aziende usando System Center Configuration Manager
In [Microsoft Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate con Configuration Manager. È quindi possibile visualizzare le app nella console di Configuration Manager e distribuirle come si distribuisce qualsiasi altra app.


## <a name="online-and-offline-apps"></a>App online e offline

Microsoft Store per le aziende supporta due tipi di app:

- **Online**: con questo tipo di licenza è necessario che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory.
- **Non in linea**: consente di memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale. senza che i dispositivi debbano connettersi allo Store o avere una connessione Internet.

[Altre informazioni](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) su Microsoft Store per le aziende.

Configuration Manager supporta la gestione delle app di Microsoft Store per le aziende sia in dispositivi Windows 10 con il client di Configuration Manager che in dispositivi Windows 10 registrati in Microsoft Intune. Configuration Manager offre le funzionalità seguenti per le app online e offline.

> [!IMPORTANT]
> Per usare Microsoft Store per le aziende, è necessario che i dispositivi Windows 10 eseguano la versione di novembre 2015 (1511) o una versione successiva.


|Funzionalità|App offline|App online|
|------------|------------|------------|
|Sincronizzazione dei dati delle app in Configuration Manager<br>(la sincronizzazione viene eseguita ogni 24 ore)|Sì|Sì|
|Creazione di applicazioni di Configuration Manager dalle app dello Store|Sì|Sì|
|Supporto delle app gratuite dello Store|Sì|Sì|
|Supporto delle app a pagamento dello Store|No|Sì<sup>1</sup>|
|Supporto delle distribuzioni richieste nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle distribuzioni disponibili nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle app line-of-business dello Store|Sì|Sì|

<sup>1</sup>Per distribuire app con licenza online a PC Windows 10 con il client di Configuration Manager, è necessario che sia in esecuzione Windows 10 Creators Update o versione successiva.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Distribuzione di app online tramite Microsoft Store per le aziende con PC che eseguono il client di Configuration Manager
Prima di distribuire app di Microsoft Store per le aziende in PC che eseguono il client completo di Configuration Manager, considerare quanto segue:

- Per la funzionalità completa, nei PC deve essere in esecuzione Windows 10 Creators Update o versione successiva.
- I PC devono essere aggiunti ad Azure Active Directory nello stesso tenant in cui Microsoft Store per le aziende è stato registrato come strumento di gestione.
- Quando i PC sono connessi all'account Administrator predefinito, non possono accedere alle app di Microsoft Store per le aziende.
- I PC devono avere una connessione Internet dinamica a Microsoft Store per le aziende.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Note per i PC che eseguono versioni precedenti di Windows 10
Nei PC che eseguono una versione di Windows 10 precedente la versione Creators Update (con il client di Configuration Manager) si verifica quanto segue:


- Quando l'installazione è imposta dall'utente che installa l'applicazione, dall'applicazione che ha raggiunto il termine di scadenza dell'installazione o dalla rivalutazione post-installazione per le distribuzioni richieste:
    - L'applicazione viene "imposta" all'avvio dell'app di Microsoft Store per le aziende. 
    - L'utente finale deve quindi completare l'installazione dallo Store prima che l'app venga installata
    - Nella console di Configuration Manager lo stato dell'applicazione segnala l'errore specificando "L'app di Windows Store è stata aperta nel computer client ed è in attesa del completamento dell'installazione da parte dell'utente."
- Al successivo ciclo di valutazione dell'applicazione:
    - Se l'applicazione è stata installata dall'utente finale dallo Store, lo stato indica che l'**operazione è riuscita**. 
    - Se l'utente finale non ha provato a installare l'app dallo Store:
        - Le distribuzioni richieste proveranno ad avviare lo Store e a imporre nuovamente l'installazione dell'applicazione.
        - Le distribuzioni disponibili non vengono nuovamente imposte.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Altre note per i PC che eseguono versioni precedenti di Windows 10:

- Non è possibile distribuire app line-of-business da Microsoft Store per le aziende
- Quando si distribuiscono app a pagamento dallo Store, gli utenti finali devono accedere allo Store e acquistare le app.
- Se si distribuiscono criteri di gruppo che disabilitano l'accesso alla versione consumer di Windows Store, le distribuzioni di Windows Store per le aziende non funzionano, anche se Windows Store per le aziende è abilitato.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurare la sincronizzazione di Microsoft Store per le aziende
Sincronizzare l'elenco delle app acquistate dall'organizzazione per poterle visualizzare nella console di Configuration Manager.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Per le versioni di Configuration Manager precedenti alla versione 1706

**In Azure Active Directory registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web". Questa azione rende disponibile un ID client che sarà necessario in un secondo tempo.**
1. Nel nodo Active Directory di [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory e quindi fare clic su **Applicazioni** > **Aggiungi**.
2.  Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e quindi fare clic sulla freccia **Avanti**.
4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**. L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio, è possibile immettere *https://dominio/sccm*.
5.  Completare la procedura guidata.

**In Azure Active Directory creare una chiave client per lo strumento di gestione registrato**
1.  Evidenziare l'applicazione creata e fare clic su **Configura**.
2.  In **Chiavi** selezionare una durata nell'elenco e fare clic su **Salva**. Questa azione crea una nuova chiave client. Non uscire dalla pagina fino a quando non è stato completato il caricamento di Microsoft Store per le aziende in Configuration Manager.

**In Microsoft Store per le aziende configurare Configuration Manager come strumento di gestione dello Store**
1.  Aprire [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e, se viene chiesto, eseguire l'accesso.
2.  Accettare le condizioni per l'utilizzo, se necessario.
3.  In **Management Tools** (Strumenti di gestione) fare clic su **Add a management tool** (Aggiungi strumento di gestione).
4.  In **Search for the tool by name** digitare il nome dell'applicazione creata in precedenza in AAD e quindi fare clic su **Add**.
5.  Fare clic su **Activate** (Attiva) accanto all'applicazione importata.
6.  Nella pagina **Manage > Account Information** (Gestisci > Informazioni account) selezionare **Show Offline-Licensed Apps** (Mostra app con licenza offline) per consentire l'acquisto di app con licenza offline.

**Aggiungere l'account dello Store in Configuration Manager**

1. Verificare di avere acquistato almeno un'app da Microsoft Store per le aziende. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e fare clic su **Microsoft Store per le aziende**.
2.  Nella scheda **Home** nel gruppo **Microsoft Store per le aziende** fare clic su **Aggiungi l'account di Microsoft Store per le aziende**. 
3.  Aggiungere l'ID tenant, l'ID client e la chiave client da Azure Active Directory e completare la procedura guidata.
4. Al termine viene visualizzato l'account in **Microsoft Store per le aziende** nella console di Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Per Configuration Manager versione 1706 e successive
<!-- ...remove above after 1802 -->

1. Nella console passare a **Amministrazione** > **Servizi cloud** > **Servizi di Azure** e scegliere **Configura i servizi di Azure** per avviare la **Procedura guidata per i servizi di Azure**.
2. Nella pagina **Servizi di Azure** selezionare il servizio che si vuole configurare e quindi fare clic su **Avanti**.
3. Nella pagina **Generale** specificare un nome descrittivo per il servizio di Azure e una descrizione facoltativa, quindi fare clic su **Avanti**.
4. Nella pagina **App** specificare l'ambiente di Azure e quindi fare clic su **Sfoglia** per aprire la finestra **App server**.
5. Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**. Le app server sono app Web di Azure che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client. Se non è disponibile un'app server, usare una delle azioni seguenti:
    - **Crea:** per creare una nuova app server, fare clic su **Crea**. Specificare un nome descrittivo per l'app e il tenant. A questo punto, dopo avere eseguito l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, insieme all'ID Client e alla chiave privata da usare con l'app Web. Queste informazioni sono poi visualizzabili nel portale di Azure.
    - **Importa:** per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant. A questo punto indicare l'ID tenant, l'ID client e la chiave privata per l'app Web di Azure che si vuole usare con Configuration Manager. Dopo aver fatto clic su **Verifica** per verificare le informazioni, fare clic su **OK** per continuare. 
6. Controllare la pagina **Informazioni** ed eseguire gli eventuali passaggi aggiuntivi e le configurazioni indicati. Queste configurazioni sono necessarie per usare il servizio con Configuration Manager. Ad esempio, per configurare Microsoft Store per le aziende:
    - In Azure è necessario registrare Configuration Manager come applicazione Web o API Web e registrare l'ID client. È anche necessario specificare una chiave client utilizzabile dallo strumento di gestione, ovvero Configuration Manager.
    - Nel portale di Microsoft Store per le aziende è necessario configurare Configuration Manager come strumento di gestione dello Store, abilitare il supporto per le app con licenza offline e acquistare almeno un'app. 
7. Quando si è pronti per continuare, fare clic su **Avanti**.
8. Nella pagina **Configurazioni dell'applicazione** completare le configurazioni per il catalogo app e la lingua per il servizio, quindi fare clic su **Avanti**.
9. Al termine della procedura guidata, nella console di Configuration Manager viene indicato che **Microsoft Store per le aziende** è stato configurato come **Tipo di servizio cloud**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Creare e distribuire un'applicazione di Configuration Manager da un'app di Microsoft Store per le aziende
Dopo la sincronizzazione, creare e distribuire le app dello Store come se si trattasse di qualsiasi altra app.

1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.
2.  Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.
Viene creata un'applicazione di Configuration Manager contenente l'app di Microsoft Store per le aziende. È quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.

> [!IMPORTANT]
> Per i dispositivi registrati in Microsoft Intune, le app distribuite sono disponibili solo per l'utente che ha originariamente registrato il dispositivo. Nessun altro utente può accedere all'app.

## <a name="next-steps"></a>Passaggi successivi

Nell'area di lavoro **Raccolta software** espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.

È possibile visualizzare informazioni su qualsiasi app dello Store che viene gestita, tra cui nome dell'app, piattaforma, numero di licenze per l'app acquistata e numero di licenze disponibili.

Dopo aver distribuito le app online, tutte le app vengono aggiornate direttamente da Microsoft Store. Configuration Manager non verifica che le app online siano conformi alla versione. Windows segnala solo che l'app è installata.  

Quando vengono distribuite app offline in dispositivi Windows 10 usando il client di Configuration Manager, non consentire agli utenti di aggiornare le applicazioni esterne alle distribuzioni di Configuration Manager. Il controllo degli aggiornamenti per le app offline è particolarmente importante in ambienti multiutente, come ad esempio nelle classi. Per disabilitare Microsoft Store è possibile usare i [criteri di gruppo](https://docs.microsoft.com/en-us/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Dopo che l'amministratore di Microsoft Store per le aziende ha acquistato l'app offline, non pubblicare l'app agli utenti tramite lo Store. In questo modo si impedisce agli utenti di eseguire l'installazione o l'aggiornamento online. Gli utenti riceveranno gli aggiornamenti delle app solo tramite Configuration Manager. 
