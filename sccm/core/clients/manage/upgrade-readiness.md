---
title: Preparazione aggiornamenti
titleSuffix: Configuration Manager
description: Integrare Preparazione aggiornamenti con Configuration Manager per accedere ai dati relativi alla compatibilità con l'aggiornamento a Windows 10 e specificare come destinazione i dispositivi da aggiornare o correggere.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11cb935eef2d214cf541142aea81fbe8e12bd06b
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72384593"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integrare Preparazione aggiornamenti con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Important]  
> A partire da ottobre 2019, l'integrazione di Preparazione aggiornamenti in Configuration Manager è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Il servizio Windows Analytics verrà ritirato il 31 gennaio 2020.
>
> [Desktop Analytics ](/sccm/desktop-analytics/overview) è l'evoluzione di Windows Analytics. I clienti esistenti di Windows Analytics possono [eseguire la migrazione a Desktop Analytics](/sccm/desktop-analytics/faq#existing-windows-analytics-customers).
>
> Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

Preparazione aggiornamenti fa parte di [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). Consente di valutare e analizzare l'idoneità dei dispositivi nell'ambiente per un aggiornamento a Windows 10. Integrare Preparazione aggiornamenti con Configuration Manager per accedere ai dati di compatibilità dell'aggiornamento dei client nella console di Configuration Manager. Usare quindi questi dati per creare raccolte e specificare come destinazione i dispositivi da aggiornare o correggere.



## <a name="configure-clients"></a>Configurare i client

Preparazione aggiornamenti si basa sui dati di Windows Analytics. Perché Preparazione aggiornamenti possa ricevere dati sufficienti, configurare i prerequisiti seguenti:

- Configurare tutti i client con una *chiave ID commerciale*  

- Configurare i client Windows 10 in modo che Windows Analytics segnali almeno i dati di livello base  

- Per i client che eseguono Windows 7 o 8.1:  

    - Installare gli aggiornamenti come descritto in [Introduzione a Preparazione aggiornamenti](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Abilitare le impostazioni client di Windows Analytics  

Configurare queste impostazioni usando le impostazioni del client di Configuration Manager. Per altre informazioni, vedere [Usare Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> Nella maggior parte degli ambienti basterà distribuire gli aggiornamenti obbligatori corretti e configurare le impostazioni client. In caso di problemi per cui Preparazione aggiornamenti non riceve i dati dai dispositivi nell'ambiente, è possibile risolvere alcuni di questi problemi usando lo [script di distribuzione di Preparazione aggiornamenti](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Connettere Configuration Manager a Preparazione aggiornamenti

Usare la [Procedura guidata per i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager. Per connettere Configuration Manager a Preparazione aggiornamenti, creare la registrazione di un'app Azure Active Directory (Azure AD) di tipo *App Web/API* nel [portale di Azure](https://portal.azure.com). Per altre informazioni su come creare la registrazione di un'app, vedere [Registrare l'applicazione nel tenant di Azure AD](/azure/active-directory/active-directory-app-registration). 

Nel portale di Azure assegnare le autorizzazioni seguenti all'app Web appena registrata:
- Autorizzazioni di *Lettore* per il gruppo di risorse contenente l'area di lavoro di Log Analytics che ospita i dati di Preparazione aggiornamenti
- Autorizzazioni di *Collaboratore* per l'area di lavoro di Log Analytics che ospita i dati di Preparazione aggiornamenti

La Procedura guidata per i servizi di Azure usa questa registrazione dell'app per consentire a Configuration Manager di comunicare in modo sicuro con Azure AD e connettere l'infrastruttura ai dati di Preparazione aggiornamenti.

> [!IMPORTANT]  
> Concedere le autorizzazioni all'app stessa e non a un'identità utente di Azure AD. È l'app registrata ad accedere ai dati per conto dell'infrastruttura di Configuration Manager. Per concedere le autorizzazioni, cercare il nome della registrazione dell'app nell'area **Aggiungi utenti** quando si assegna l'autorizzazione. 
> 
> Questo processo è analogo a quello che aggiunge a Configuration Manager le autorizzazioni per Log Analytics. È necessario completare questi passaggi prima che la registrazione dell'app venga importata in Configuration Manager con la *Procedura guidata per i servizi di Azure*.
> 
> Per altre informazioni, vedere [Connettere Configuration Manager a Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Usare la procedura guidata per Azure per creare la connessione

Seguire le istruzioni incluse in [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per creare una connessione a Preparazione aggiornamenti importando la registrazione dell'app Web creata sopra. 

Se l'importazione dell'app Web è riuscita e sono state assegnate le autorizzazioni corrette nel portale di Azure, la pagina *Configurazione* viene prepopolata con i valori seguenti:   
-  Sottoscrizioni Azure  
-  Gruppo di risorse di Azure  
-  Area di lavoro di Windows Analytics  

È disponibile più di un gruppo di risorse o di un'area di lavoro nelle circostanze seguenti: 
- Se l'app Web di Azure AD registrata ha le autorizzazioni di *Collaboratore* per più di un gruppo di risorse   
- Se il gruppo di risorse selezionato ha più di un'area di lavoro di Log Analytics  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Visualizzare e usare le informazioni di Preparazione aggiornamenti in Configuration Manager

Dopo aver integrato Preparazione aggiornamenti con Configuration Manager, è possibile visualizzare l'analisi della conformità agli aggiornamenti dei client.

1. Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Preparazione aggiornamenti**.  

2. Rivedere i dati. Ad esempio:  
    - Stato di Preparazione aggiornamenti  
    - Percentuale di Dispositivi Windows che inviano dati  

3. Filtrare il dashboard per visualizzare i dati di dispositivi appartenenti a raccolte specifiche.  

4. Visualizzare i dispositivi con un determinato stato di preparazione e quindi creare una raccolta dinamica per tali dispositivi. Usare quindi tale raccolta per aggiornare i dispositivi o intervenire per correggere i dispositivi bloccati.  

> [!Note]  
> Il sito sincronizza i dati con Preparazione aggiornamenti una volta alla settimana.<!--SCCMDocs issue 732--> Per attivare manualmente la sincronizzazione:
> 1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**.  
> 2. Selezionare la connessione a Preparazione aggiornamenti nell'elenco.  
> 3. Nella barra multifunzione selezionare l'opzione da sincronizzare.  



## <a name="next-steps"></a>Passaggi successivi

- [Aggiornare Windows alla versione più recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Creare distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
