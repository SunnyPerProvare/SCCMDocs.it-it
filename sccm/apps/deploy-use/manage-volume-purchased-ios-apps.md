---
title: Gestire le app iOS acquistate con Volume Purchase Program | Microsoft Docs
description: Distribuire, gestire e tenere traccia delle licenze per le app acquistate tramite l&quot;App Store iOS.
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
ms.sourcegitcommit: 828e2ac9a3f9bcea1571d24145a1021fdf1091f3
ms.openlocfilehash: cd9edf61d151ac8334ace0bf668fa4c919d8c75b


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 L'App Store iOS consente di acquistare più licenze per un'app da eseguire nell'azienda. In questo modo, è possibile ridurre il carico amministrativo associato al monitoraggio di più copie delle app acquistate.  

 System Center Configuration Manager consente di distribuire e gestire le app iOS acquistate con il programma importando le informazioni di licenza dall'App Store e tenendo traccia del numero di licenze usate.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gestione delle app acquistate tramite Volume Purchase Program per dispositivi iOS  
 Per acquistare più licenze per app per iOS, è necessario usare il programma Volume Purchase Program (VPP) di Apple. A questo scopo, configurare un account VPP di Apple dal sito Web Apple e caricare il token VPP di Apple in Configuration Manager per poter usare le funzionalità seguenti:  

-   Sincronizzare i dati del programma Volume Purchase Program con Configuration Manager.  

-   Le app acquistate vengono visualizzate nella console di Configuration Manager.  

-   È possibile distribuire e monitorare le app e tenere traccia del numero di licenze usate per ogni app.  

-   Configuration Manager può essere usato per recuperare le licenze necessarie disinstallando le app acquistate con Volume Purchase Program distribuite agli utenti.  

## <a name="before-you-start"></a>Prima di iniziare  
 Prima di iniziare, è necessario ottenere un token VPP da Apple e caricarlo in Configuration Manager.  

> [!IMPORTANT]  
>  -   Attualmente, ogni organizzazione può avere solo un account e un token VPP.  
> -   È supportato solo il programma Volume Purchase Program for Business di Apple.  
> -   Dopo aver associato un account VPP di Apple a Intune, in seguito non sarà più possibile associare un account diverso. Per questo motivo, verificare che i dettagli dell'account usato vengano comunicati a più persone.  
> -   Se in passato è stato usato un token VPP con un prodotto MDM diverso nell'account VPP di Apple, è necessario generarne uno nuovo da usare con Configuration Manager.  
> -   Ogni token è valido per un anno.  
> -   Per impostazione predefinita, Configuration Manager si sincronizza con il servizio VPP di Apple due volte al giorno per garantire la sincronizzazione delle licenze.  
>   
>      Vengono sincronizzate solo le modifiche alle licenze. Tuttavia, una volta ogni sette giorni, verrà eseguita una sincronizzazione completa.  
>   
>      Quando si sceglie **Sincronizza** per eseguire una sincronizzazione manuale, verrà sempre eseguita una sincronizzazione completa.  
> -   Se è necessario recuperare o ripristinare il database di Configuration Manager, è consigliabile eseguire in seguito una sincronizzazione manuale per assicurarsi che i dati di licenza sincronizzati siano aggiornati.  
> -   Sebbene sia possibile distribuire le app iOS acquistate con il programma Volume Purchase Program a raccolte di utenti o dispositivi, le app VPP distribuite a un dispositivo senza utente (ad esempio un dispositivo registrato senza affinità utente usando Device Enrollment Program (DEP) o Apple Configurator) non verranno installate.  

 Inoltre, per gestire i dispositivi iOS e distribuire le app è necessario aver importato da Apple un certificato Apple Push Notification service (APNs) valido. Per altre informazioni, vedere [Set up iOS hybrid device management](../../mdm/deploy-use/enroll-hybrid-ios-mac.md) (Configurare la gestione di dispositivi iOS ibrida).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Passaggio 1: Ottenere e caricare un token VPP di Apple  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Servizi cloud** > **Token di Volume Purchase Program di Apple**.   

3.  Nella scheda **Home** nel gruppo **Token di Volume Purchase Program di Apple** scegliere **Aggiungere un token di Volume Purchase Program di Apple**.  

4.  Nella pagina **Generale** della procedura guidata **Aggiungere un token di Volume Purchase Program di Apple** configurare le opzioni seguenti:   

    -   **Nome**: immettere un nome per il token che verrà visualizzato nella console di Configuration Manager.  

    -   **Token**: scegliere **Sfoglia** e scegliere il token VPP scaricato dal sito Web Apple.  

         Scegliere il collegamento **Vedere l'account VPP di Apple** e, se non è ancora stata eseguita, procedere alla registrazione al programma Volume Purchase Program per le imprese o per l'istruzione. Dopo aver completato l'iscrizione, scaricare il token VPP di Apple per l'account.  

    -   **Descrizione**: facoltativamente, immettere una descrizione che consenta di identificare il token VPP nella console di Configuration Manager.  

    -   **Categorie assegnate per migliorare la ricerca e il filtraggio**: facoltativamente, è possibile assegnare le categorie al token VPP per facilitarne la ricerca nella console di Configuration Manager.  

5.  Scegliere **Avanti** e quindi completare la procedura guidata.  

Nel nodo **Token di Volume Purchase Program di Apple** è ora possibile visualizzare informazioni sul token VPP di Apple che includono la data dell'ultimo aggiornamento, di scadenza e dell'ultima sincronizzazione.

È possibile sincronizzare in qualsiasi momento tutti i dati di Apple con Configuration Manager scegliendo **Sincronizza** nella scheda **Home** nel gruppo **Sincronizza**.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Passaggio 2: Distribuire un'app acquistata tramite Volume Purchase Program  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Informazioni di licenza per le app dello Store**.  

3.  Scegliere l'app che si vuole distribuire e quindi nella scheda **Home** nel gruppo **Crea** scegliere **Crea applicazione**.
L'applicazione di Configuration Manager creata contiene l'app Windows Store per le aziende. Sarà quindi possibile distribuire e monitorare l'applicazione come qualsiasi altra applicazione di Configuration Manager.

    > [!IMPORTANT]  
    > È necessario scegliere lo scopo della distribuzione **Richiesto**. Le installazioni disponibili non sono attualmente supportate.

 Quando si distribuisce l'app, ogni utente che installa l'app usa una licenza.  

 Per revocare una licenza, è necessario modificare l'azione di distribuzione specificando **Disinstalla**. La licenza verrà revocata dopo la disinstallazione dell'app.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Passaggio 3: Monitorare le app VPP per iOS  
 Il nodo **Informazioni di licenza per le app dello Store** dell'area di lavoro **Libreria software** visualizza le informazioni sulle app iOS acquistate con Volume Purchase Program. Le informazioni includono il numero totale di licenze di cui si è proprietari per ogni app e il numero di licenze distribuite.

 È anche possibile monitorare l'utilizzo delle licenze di tutte le app VPP acquistate usando il report **App Volume Purchase Program di Apple per iOS con conteggi di licenze**.  

 Questo report visualizza il nome di ogni applicazione, insieme al numero totale di licenze acquistate, il numero di licenze disponibili e altri dati ancora.  

 Per informazioni sull'esecuzione dei report di Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Dec16_HO3-->


