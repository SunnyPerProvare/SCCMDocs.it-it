---
title: Gestire le app da Windows Store per le aziende | Microsoft Docs
description: Gestire e distribuire le app da Windows Store per le aziende usando System Center Configuration Manager.
ms.custom: na
ms.date: 3/29/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: f2d9da1c584f78e27e84b7f55e7ffe4dd052a27c
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gestire le app da Windows Store per le aziende con System Center Configuration Manager
In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, singolarmente o con Volume Purchase Program. Collegando lo Store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate, visualizzarle nella console di Configuration Manager e distribuirle come qualsiasi altra app.


## <a name="online-and-offline-apps"></a>App online e offline

Windows Store per le aziende supporta due tipi di app:

- **Online**: con questo tipo di licenza è necessario che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory.
- **Offline**: le organizzazioni possono memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale senza connettersi allo Store o avere una connessione Internet.

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


- Quando l'installazione viene imposta dall'utente che installa l'applicazione o dall'applicazione che ha raggiunto il termine di scadenza dell'installazione o la rivalutazione post-installazione per le distribuzioni richieste:
    - L'applicazione verrà "imposta" dall'avvio dell'app di Windows Store per le aziende. 
    - L'utente finale deve quindi completare l'installazione dallo Store prima che venga effettivamente installata.
    - Lo stato dell'applicazione nella console di Configuration Manager verrà segnalato come non riuscito con l'errore "L'app di Windows Store è stata aperta nel computer client ed è in attesa del completamento dell'installazione da parte dell'utente".
- Al successivo ciclo di valutazione dell'applicazione:
    - Se l'applicazione è stata installata dall'utente finale dallo Store, verrà segnalato lo stato **Operazione completata**. 
    - Se l'utente finale non ha provato a installare l'app dallo Store:
        - Le distribuzioni richieste proveranno ad avviare lo Store e a imporre nuovamente l'installazione dell'applicazione.
        - L'installazione delle distribuzioni disponibili non verrà imposta nuovamente.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Altre note per i PC che eseguono versioni precedenti di Windows 10:

- Non è possibile distribuire app line-of-business da Windows Store per le aziende.
- Quando si distribuiscono app a pagamento dallo Store, agli utenti finali verrà chiesto di accedere allo Store e di acquistare le app.
- Se si sono distribuiti criteri di gruppo che disabilitano l'accesso alla versione consumer di Windows Store, le distribuzioni di Windows Store per le aziende non funzioneranno, anche se Windows Store per le aziende è abilitato.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configurare la sincronizzazione di Windows Store per le aziende

**In Azure Active Directory registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web". Si riceverà un ID client che sarà necessario in seguito.**
1. Nel nodo Active Directory di [https://manage.windowsazure.com](https://manage.windowsazure.com) selezionare Azure Active Directory e quindi fare clic su **Applicazioni** > **Aggiungi**.
2.  Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
3.  Immettere un nome per l'applicazione, selezionare **Applicazione Web** e/o **API Web** e quindi fare clic sulla freccia **Avanti**.
4.  Immettere lo stesso URL per **URL accesso** e **URI ID app**. L'URL può essere di qualsiasi tipo e non è necessario che venga risolto in un indirizzo reale. Ad esempio, è possibile immettere *https://dominio/sccm*.
5.  Completare la procedura guidata.

**In Azure Active Directory creare una chiave client per lo strumento di gestione registrato**
1.  Evidenziare l'applicazione appena creata e fare clic su **Configura**.
2.  In **Chiavi** selezionare una durata nell'elenco e fare clic su **Salva**. Verrà creata una nuova chiave client. Non uscire dalla pagina fino a quando non è stato completato il caricamento di Windows Store per le aziende in Configuration Manager.

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
4. Al termine verrà visualizzato l'account configurato nell'elenco di **Windows Store per le aziende** nella console di Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Creare e distribuire un'applicazione di Configuration Manager da un'app di Windows Store per le aziende.
1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.
2.  Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.
Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. Sarà quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.
> [!IMPORTANT]
> Per i dispositivi registrati in Intune, le app distribuite sono disponibili solo per l'utente che ha originariamente registrato il dispositivo. Nessun altro utente può accedere all'app.

## <a name="monitor-windows-store-for-business-apps"></a>Monitorare Windows Store per le app aziendali

Nell'area di lavoro **Raccolta software** espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.

Per ogni app dello Store gestita è possibile visualizzare informazioni che includono nome, piattaforma, numero di licenze per l'app acquistate e numero di licenze disponibili.

