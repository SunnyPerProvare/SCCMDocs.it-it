---
title: Gestire le app iOS acquistate con Volume Purchase Program | System Center Configuration Manager
description: Distribuire, gestire e tenere traccia delle licenze per le app acquistate tramite l'App Store iOS.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 L'App Store iOS consente di acquistare più licenze per un'app da eseguire nell'azienda. In questo modo, è possibile ridurre il sovraccarico amministrativo associato al monitoraggio di più copie delle app acquistate.  

 System Center Configuration Manager consente di distribuire e gestire le app iOS acquistate con il programma importando le informazioni di licenza dall'App Store e tenendo traccia del numero di licenze usate.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gestire app acquistate tramite Volume Purchase Program per dispositivi iOS  
 Per acquistare più licenze per app per iOS, è necessario usare il programma Volume Purchase Program (VPP) di Apple. A questo scopo, configurare un account VPP di Apple dal sito Web Apple e caricare il token VPP di Apple in Configuration Manager per poter usare le funzionalità seguenti:  

-   Sincronizzare i dati del programma Volume Purchase Program con Configuration Manager.  

-   Le app acquistate vengono visualizzate nella console di Configuration Manager.  

-   È possibile distribuire e monitorare le app e tenere traccia del numero di licenze usate per ogni app.  

-   Configuration Manager può essere usato per recuperare le licenze necessarie disinstallando le app acquistate con il programma Volume Purchase Program distribuite agli utenti.  

## <a name="before-you-start"></a>Prima di iniziare  
 Prima di iniziare, è necessario ottenere un token VPP da Apple e caricarlo in Configuration Manager.  

> [!IMPORTANT]  
>  -   Attualmente, ogni organizzazione può avere solo un account e un token VPP.  
> -   È supportato solo il programma Volume Purchase Program for Business di Apple.  
> -   Dopo aver associato un account VPP di Apple a Intune, in seguito non sarà più possibile associare un account diverso. Per questo motivo, è molto importante comunicare a più persone i dettagli dell'account usato.  
> -   Se in passato è stato usato un token VPP con un prodotto MDM diverso nell'account VPP di Apple, è necessario generarne uno nuovo da usare con Configuration Manager.  
> -   Ogni token è valido per un anno.  
> -   Per impostazione predefinita, Configuration Manager si sincronizza con il servizio VPP di Apple due volte al giorno per garantire la sincronizzazione delle licenze.  
>   
>      Vengono sincronizzate solo le modifiche alle licenze. Tuttavia, ogni 7 giorni, viene eseguita una sincronizzazione completa.  
>   
>      Quando fa clic su **Sincronizza** per eseguire una sincronizzazione manuale, viene sempre eseguita una sincronizzazione completa.  
> -   Se è necessario recuperare o ripristinare il database di Configuration Manager, è consigliabile eseguire in seguito una sincronizzazione manuale per assicurarsi che i dati di licenza sincronizzati siano aggiornati.  
> -   Sebbene sia possibile distribuire le app iOS acquistate con il programma Volume Purchase Program a raccolte di utenti o dispositivi, le app VPP distribuite a un dispositivo senza utente (ad esempio un dispositivo registrato senza affinità utente usando Device Enrollment Program (DEP) o Apple Configurator) non verranno installate.  

 Inoltre, per gestire i dispositivi iOS e distribuire le app è necessario aver importato da Apple un certificato Apple Push Notification service (APNs) valido. Per altre informazioni, vedere [Set up iOS hybrid device management](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md) (Configurare la gestione di dispositivi iOS ibrida).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Passaggio 1: Ottenere e caricare un token VPP di Apple  
  
1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Servizi cloud** > **Token di Volume Purchase Program di Apple**.   
  
3.  Nella scheda **Home** nel gruppo **Token di Volume Purchase Program di Apple** fare clic su **Aggiungere un token di Volume Purchase Program di Apple**.  

4.  Nella pagina **Generale** della procedura guidata **Aggiungere un token di Volume Purchase Program di Apple** configurare le opzioni seguenti:   

    -   **Nome**: immettere un nome per il token che verrà visualizzato nella console di Configuration Manager.  

    -   **Token**: fare clic su **Sfoglia** e selezionare il token VPP scaricato dal sito Web Apple.  

         Fare clic sul collegamento **Vedere l'account VPP di Apple** e, se non è ancora stata eseguita, eseguire la registrazione al programma Volume Purchase Program per le imprese o per l'istruzione. Dopo aver completato l'iscrizione, scaricare il token VPP di Apple per l'account.  

    -   **Descrizione**: facoltativamente, immettere una descrizione che consenta di identificare il token VPP nella console di Configuration Manager.  

    -   **Categorie assegnate per migliorare la ricerca e il filtraggio**: facoltativamente, è possibile assegnare le categorie al token VPP per facilitarne la ricerca nella console di Configuration Manager.  

5.  Fare clic su **Avanti** e completare la procedura guidata.  
  
Nel nodo **Token di Volume Purchase Program di Apple** è ora possibile visualizzare informazioni sul token VPP di Apple che includono la data dell'ultimo aggiornamento, di scadenza e dell'ultima sincronizzazione. 
  
È possibile sincronizzare in qualsiasi momento tutti i dati di Apple con Configuration Manager facendo clic su **Sincronizza** nella scheda **Home** nel gruppo **Sincronizza**.  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>Passaggio 2: Distribuire un'app acquistata tramite Volume Purchase Program  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Informazioni di licenza per le app dello Store**.  

3.  Scegliere l'app che si vuole distribuire quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione**.
Viene creata un'applicazione di Configuration Manager contenente l'archivio di Windows per l'applicazione aziendale. Sarà quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.

    > [!IMPORTANT]  
    > È necessario scegliere lo scopo della distribuzione **Richiesto**. Le installazioni disponibili non sono attualmente supportate.

 Durante la distribuzione dell'app, viene usata una licenza da ogni utente che installa l'app.  

 Per revocare una licenza, è necessario modificare l'azione di distribuzione specificando **Disinstalla**. La licenza verrà revocata al termine della disinstallazione dell'app.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Passaggio 3: Monitorare le app VPP per iOS  
 Il nodo **Informazioni di licenza per le app dello Store** dell'area di lavoro **Raccolta software** visualizza informazioni sulle app iOS acquistate con il programma Volume Purchase Program, incluso il totale delle licenze per ogni app e il numero di licenze distribuite.

 È anche possibile monitorare l'utilizzo delle licenze di tutte le app VPP acquistate usando il report **App Volume Purchase Program di Apple per iOS con conteggi di licenze**.  

 Questo report visualizza il nome di ogni applicazione, insieme al numero totale di licenze acquistate, il numero di licenze disponibili e altri dati ancora.  

 Per informazioni sull'esecuzione dei report di Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


