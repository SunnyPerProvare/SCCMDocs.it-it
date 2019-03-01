---
title: Microsoft Store per le aziende
titleSuffix: Configuration Manager
description: Gestire e distribuire app da Microsoft Store per le aziende con Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0a32357001f37f537f13fe85e71a41f9cb658ac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122441"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-configuration-manager"></a>Gestire app da Microsoft Store per le aziende con Configuration Manager

In [Microsoft Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e ottenere le app Windows per l'organizzazione. Quando si connette lo Store a Configuration Manager, viene eseguita quindi la sincronizzazione dell'elenco di app ottenute. È possibile visualizzare le app nella console di Configuration Manager e distribuirle come si distribuisce qualsiasi altra app.


## <a name="bkmk_apps"></a> App online e offline

Microsoft Store per le aziende supporta due tipi di app:

- **Online**: questo tipo di licenza richiede che gli utenti e i dispositivi si connettano allo Store per ottenere un'app e la relativa licenza. I dispositivi Windows 10 devono appartenere a un dominio Azure Active Directory (Azure AD).  

- **Offline**: questo tipo consente di memorizzare nella cache le app e le licenze da distribuire direttamente nella rete locale, senza che i dispositivi debbano connettersi allo Store o avere una connessione Internet.

[Altre informazioni](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) su Microsoft Store per le aziende.

Configuration Manager supporta la gestione delle app di Microsoft Store per le aziende sia in dispositivi Windows 10 con il client di Configuration Manager che in dispositivi Windows 10 registrati in Microsoft Intune. Configuration Manager offre le funzionalità seguenti per le app online e offline:


|Funzionalità|App offline|App online|
|------------|------------|------------|
|Sincronizzazione dei dati delle app in Configuration Manager<br>(la sincronizzazione viene eseguita ogni 24 ore)|Sì|Sì|
|Creazione di applicazioni di Configuration Manager dalle app dello Store|Sì|Sì|
|Supporto delle app gratuite dello Store|Sì|Sì|
|Supporto delle app a pagamento dello Store|No|Sì<sup>1</sup>|
|Supporto delle distribuzioni richieste nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle distribuzioni disponibili nelle raccolte di utenti e dispositivi|Sì|Sì|
|Supporto delle app line-of-business dello Store|Sì|Sì|
|Provisioning di un'app dello Store per tutti gli utenti in un dispositivo<sup>2</sup><!--1358310-->|Sì|Sì|

- <sup>1</sup> Per distribuire app con licenza online in dispositivi Windows 10 con il client di Configuration Manager, è necessario che sia in esecuzione Windows 10 versione 1703 o successiva.  

- <sup>2</sup> A partire dalla versione 1806. Per altre informazioni, vedere [Creare applicazioni Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  


### <a name="deploying-online-apps-using-the-microsoft-store-for-business-to-devices-that-run-the-configuration-manager-client"></a>Distribuzione di app online tramite Microsoft Store per le aziende in dispositivi che eseguono il client di Configuration Manager

Prima di distribuire app di Microsoft Store per le aziende in dispositivi che eseguono il client completo di Configuration Manager, considerare quanto segue:

- Per ottenere le funzionalità complete, i dispositivi devono eseguire Windows 10 versione 1703 o successiva.  

- I dispositivi devono essere aggiunti ad Azure AD nello stesso tenant in cui Microsoft Store per le aziende è stato registrato come strumento di gestione.  

- Quando l'account dell'amministratore locale accede al dispositivo, non può accedere alle app di Microsoft Store per le aziende.  

- I dispositivi devono avere una connessione Internet dinamica a Microsoft Store per le aziende. Per altre informazioni, inclusa la configurazione del proxy, vedere [Prerequisiti](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  


### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Note per i dispositivi che eseguono versioni precedenti di Windows 10

Nei dispositivi con il client di Configuration Manager che eseguono Windows 10 versione 1607 o precedente sono disponibili le funzionalità seguenti:  

Quando si impone l'installazione dell'app nel dispositivo tramite uno dei metodi seguenti:  

- L'utente installa l'app  

- La distribuzione raggiunge la rispettiva scadenza dell'installazione   

- Ripetizione della valutazione dopo l'installazione per le distribuzioni richieste  

Si verificano quindi i comportamenti seguenti:  

- Il client di Configuration Manager "impone" l'app avviando l'app Microsoft Store per le aziende  

- L'utente deve completare l'installazione dallo Store  

- Nella console di Configuration Manager, lo stato di distribuzione dell'app segnala l'esito negativo con l'errore seguente: "L'app di Microsoft Store è stata aperta nel computer client ed è in attesa del completamento dell'installazione da parte dell'utente".  

Al successivo ciclo di valutazione dell'applicazione:  

- Se l'utente ha installato l'applicazione dallo Store, lo stato dell'applicazione è **Operazione riuscita**  

- Se l'utente non ha provato a installare l'app dallo Store:  

    - Per le distribuzioni richieste il client di Configuration Manager prova ad avviare di nuovo l'app dello Store  

    - Non viene ripetuta l'imposizione delle distribuzioni disponibili


#### <a name="further-notes-for-devices-running-earlier-versions-of-windows-10"></a>Note aggiuntive per i dispositivi che eseguono versioni precedenti di Windows 10:

- Non è possibile distribuire app line-of-business da Microsoft Store per le aziende  

- Quando si distribuiscono app a pagamento dallo Store, gli utenti devono accedere allo Store e ottenere personalmente le app  

- Se si distribuiscono criteri di gruppo che disabilitano l'accesso alla versione consumer di Windows Store, le distribuzioni di Microsoft Store per le aziende non funzionano. Questo comportamento si verifica anche se Microsoft Store per le aziende è abilitato.  



## <a name="bkmk_setup"></a> Configurare la sincronizzazione di Microsoft Store per le aziende

La sincronizzazione dell'elenco di app ottenute dall'organizzazione consente di visualizzare tali app nella console di Configuration Manager.

Connettere il sito di Configuration Manager ad Azure AD e a Microsoft Store per le aziende. Per altre informazioni e dettagli relativi a questo processo, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Creare una connessione al servizio **Microsoft Store per le aziende**.


### <a name="bkmk_config"></a> Informazioni e configurazioni aggiuntive 

Nella pagina **App** della Procedura guidata per i servizi di Azure configurare prima di tutto l'**Ambiente di Azure** e l'**App Web**. Leggere quindi la sezione **Altre informazioni** nella parte inferiore della pagina. Queste informazioni includono le azioni aggiuntive seguenti nel portale di Microsoft Store per le aziende:  

- Configurare Configuration Manager come strumento di gestione dello Store. Per altre informazioni, vedere [Configurare un provider di gestione](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Abilitare il supporto per le app con licenza offline. Per altre informazioni, vedere [Distribuire app offline](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Ottenere almeno un'app. Per altre informazioni, vedere [Trovare e acquisire app](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Nella pagina **Configurazioni** della Procedura guidata per i servizi di Azure specificare le informazioni seguenti:  

- **Percorso per la risorsa di archiviazione dei contenuti dell'app di Microsoft Store per le aziende**: specificare un percorso di rete condiviso, compresa una cartella. Ad esempio, `\\server\share\folder`. Quando il server del sito si sincronizza con lo Store, memorizza il contenuto nella cache usando questo percorso. Quando si crea un'applicazione in Configuration Manager, il server del sito copia il contenuto dell'app da questa cache locale nella raccolta contenuto del sito.  

- **Lingue selezionate**: selezionare le lingue da sincronizzare dallo Store e da visualizzare per gli utenti in Software Center. Se ad esempio l'utente configura Windows per il tedesco, Software Center mostra stringhe in tedesco per l'app dello Store. Questo comportamento richiede che tale lingua sia sincronizzata e che sia disponibile per l'applicazione specifica.    

- **Lingua predefinita**: se la lingua dell'utente non è disponibile, selezionare una lingua predefinita da usare.  



## <a name="bkmk_deploy"></a> Creare e distribuire un'applicazione di Configuration Manager da un'app di Microsoft Store per le aziende

Dopo la sincronizzazione, creare e distribuire le app dello Store come se si trattasse di qualsiasi altra app.

1.  Nell'area di lavoro **Raccolta software** della console di Configuration Manager espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.  

2.  Scegliere l'app da distribuire, quindi fare clic su **Crea applicazione** sulla barra multifunzione.  

Il sito crea un'applicazione di Configuration Manager contenente l'app di Microsoft Store per le aziende. 

È quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager. Per altre informazioni, vedere gli articoli seguenti:  
- [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications)
- [Monitorare le applicazioni dalla console](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> Per i dispositivi registrati in Microsoft Intune, le app distribuite sono disponibili solo per l'utente che ha originariamente registrato il dispositivo. Nessun altro utente può accedere all'app.



## <a name="next-steps"></a>Passaggi successivi

Nell'area di lavoro **Raccolta software** espandere **Gestione delle applicazioni** e fare clic su **Informazioni di licenza per le app dello Store**.

Per ogni app dello Store gestita è possibile visualizzare le informazioni seguenti:
- Nome dell'app
- Piattaforma dell'app
- Numero di licenze dell'app di cui si è proprietari
- Numero di licenze disponibili

Dopo aver distribuito le app online, tutte le app vengono aggiornate direttamente da Microsoft Store. Configuration Manager non verifica inoltre che le app online siano conformi alla versione. Windows segnala solo che l'app è installata.  

Quando vengono distribuite app offline in dispositivi Windows 10 tramite il client di Configuration Manager, non consentire agli utenti di aggiornare le applicazioni esterne alle distribuzioni di Configuration Manager. Il controllo degli aggiornamenti per le app offline è particolarmente importante in ambienti multiutente, come ad esempio nelle classi. Per disabilitare Microsoft Store è possibile usare i [criteri di gruppo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Quando l'amministratore di Microsoft Store per le aziende ottiene un'app offline, non pubblicare l'app per gli utenti tramite lo Store. In questo modo si impedisce agli utenti di eseguire l'installazione o l'aggiornamento online. Gli utenti ricevono gli aggiornamenti delle app offline solo tramite Configuration Manager. 
