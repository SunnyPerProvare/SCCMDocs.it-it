---
title: Gestire le app da Windows Store per le aziende | System Center Configuration Manager
description: Gestire e distribuire le app da Windows Store per le aziende usando System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Gestire le app da Windows Store per le aziende con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app Windows per l'organizzazione, con contratti singoli o multilicenza. Collegando lo Store a Configuration Manager, è possibile sincronizzare l'elenco delle app acquistate, visualizzarle nella console di Configuration Manager e distribuirle come qualsiasi altra app.


## <a name="online-and-offline-apps"></a>App online e offline

Windows Store per le aziende supporta due tipi di app:

- **Online**: con questo tipo di licenza è necessario che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory.
- **Offline**: le organizzazioni possono memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale senza connettersi allo Store o avere una connessione Internet.

[Altre informazioni](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview) su Windows Store per le aziende.

Configuration Manager supporta la gestione delle app di Windows Store per le aziende su dispositivi Windows 10 che eseguono il client di Configuration Manager e su dispositivi Windows 10 registrati in Microsoft Intune (configurazione ibrida). Configuration Manager offre le funzionalità seguenti per le app online e offline.

> [!IMPORTANT]
> Per usare questa funzionalità, è necessario che i dispositivi Windows 10 eseguano la versione di novembre 2015 (1511) o una versione successiva.

|Funzionalità|App offline|App online|
|------------|------------|------------|
|Sincronizzazione dei dati delle app in Configuration Manager<br>(la sincronizzazione viene eseguita ogni 24 ore)|Sì|Sì|
|Creazione di applicazioni di Configuration Manager dalle app dello Store|Sì|Sì|
|Supporto delle app gratuite dello Store|Sì|Sì|
|Supporto delle app a pagamento dello Store|No|No|
|Supporto delle distribuzioni richieste nelle raccolte di utenti e dispositivi|Sì|Sì<sup>1</sup>|
|Supporto delle distribuzioni disponibili nelle raccolte di utenti e dispositivi|Sì<sup>3</sup>|No<sup>2</sup>|

<sup>1</sup>Supporta solo dispositivi gestiti da Intune. Sebbene sia possibile creare un'applicazione online nella console di Configuration Manager e distribuirla in un dispositivo gestito dal client di Configuration Manager, questa operazione avrà esito negativo. L'utente finale verrà reindirizzato alla pagina dell'App Store da cui dovrà eseguire l'installazione manuale dell'app.

<sup>2</sup>Le app online possono essere distribuite come disponibili per raccolte di utenti o dispositivi per dispositivi gestiti solo dal client di Configuration Manager. Tuttavia, quando l'utente finale seleziona l'app in Software Center, verrà reindirizzato a Windows Store per le aziende da cui dovrà installare l'app manualmente. Non sono supportate le distribuzioni disponibili per i dispositivi registrati in Microsoft Intune.

<sup>3</sup>Non supportata per i dispositivi gestiti da Intune.

> [!IMPORTANT]
> In questa versione se è presente una gerarchia di Configuration Manager che contiene un sito di amministrazione centrale e almeno un sito primario, la distribuzione di app offline di Windows Store per le aziende in dispositivi gestiti da Intune non riuscirà.


## <a name="activate-the-windows-store-for-business-capability"></a>Attivare la funzionalità Windows Store per le aziende
Poiché si tratta di una funzionalità di versione non definitiva, prima di connettere Configuration Manager a Windows Store per le aziende, è necessario eseguire i passaggi seguenti:

**Accettare l'uso delle funzionalità di versioni non definitive**
1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager fare clic su **Configurazione sito** > **Siti**.
2. Selezionare il sito principale della gerarchia e aprire **Impostazioni gerarchia**.
3. Nella finestra di dialogo **Proprietà delle impostazioni di gerarchia** selezionare la casella **Consenso a usare funzionalità di versioni non definitive**.
4. Fare clic su **OK**.

**Attivare la funzionalità Windows Store per le aziende**
1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager fare clic su **Servizi cloud** > **Aggiornamenti e manutenzione** > **Funzionalità**.
2. Selezionare **Integrazione di Windows Store per le aziende**, quindi nella scheda **Home** nel gruppo **Funzionalità** fare clic su **Attiva**.
3. Chiudere e quindi riaprire la console di Configuration Manager.
4. Sarà ora visibile il nodo **Windows Store per le aziende** nell'area di lavoro **Amministrazione** in **Servizi cloud**.

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

1. Assicurarsi di aver acquistato almeno un'app da Windows Store per le aziende. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Windows Store per le aziende**.
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



<!--HONumber=Nov16_HO1-->


