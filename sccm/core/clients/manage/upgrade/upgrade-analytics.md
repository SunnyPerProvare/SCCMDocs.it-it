---
title: Preparazione aggiornamenti
titleSuffix: Configuraton Manager
description: Integrare Upgrade Readiness con Configuration Manager. Accedere ai dati di compatibilità dell'aggiornamento nella console di amministrazione. Definire i dispositivi di destinazione per l'aggiornamento o la correzione.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 4360fc34e06d4c62c137f8c956274104112d54a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336732"
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrare Upgrade Readiness con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Preparazione aggiornamenti (in precedenza Upgrade Analytics) fa parte di [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) e consente di valutare e analizzare la conformità dei dispositivi nell'ambiente per un aggiornamento a Windows 10. È possibile configurare la versione specifica. Lo strumento Preparazione aggiornamenti può essere integrato con Configuration Manager per accedere ai dati di compatibilità dell'aggiornamento dei client nella console di amministrazione di Configuration Manager. È possibile specificare come destinazione i dispositivi per l'aggiornamento o la correzione usando raccolte dinamiche create in base a questi dati.

Preparazione aggiornamenti è una soluzione che viene eseguita in [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). Per altre informazioni su Preparazione aggiornamenti, vedere [Manage Windows upgrades with Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness) (Gestire gli aggiornamenti di Windows con Preparazione aggiornamenti).

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>Configurare i client

Come tutte le soluzioni di Windows Analytics, Preparazione aggiornamenti si basa sui dati di telemetria di Windows. Perché Preparazione aggiornamenti possa ricevere dati di telemetria sufficienti, devono essere soddisfatti i prerequisiti seguenti:

- Tutti i client devono essere configurati con una **chiave ID commerciale**. 
- Nei client Windows 10 è necessario configurare la telemetria in modo da segnalare almeno dati di telemetria di livello di base.
-  Nei client che eseguono versioni precedenti di Windows devono essere installati gli elementi della knowledge base specifici descritti in [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs) (Introduzione a Preparazione aggiornamenti). Nei client deve essere anche abilitata la telemetria in **Impostazioni client**.

La chiave ID commerciale e la telemetria di Windows possono essere configurate in **Impostazioni client**. Per altre informazioni, vedere [Usare Windows Analytics con Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>In caso di problemi per cui Preparazione aggiornamenti non riceve i dati di telemetria dai dispositivi nell'ambiente nel modo previsto, è possibile risolvere alcuni di questi problemi usando lo [script di distribuzione di Preparazione aggiornamenti](/windows/deployment/upgrade/upgrade-readiness-deployment-script). Tuttavia, nella maggior parte degli ambienti in cui vengono distribuiti gli elementi della knowledge base corretti, è sufficiente configurare la chiave ID commerciale e la telemetria in **Impostazioni client**.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Connettere Configuration Manager a Preparazione aggiornamenti

A partire da Current Branch versione 1706, viene usata la [Procedura guidata per i servizi di Azure](../../../servers/deploy/configure/azure-services-wizard.md) per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager. Per connettere Configuration Manager a Preparazione aggiornamenti, è necessario creare la registrazione di un'app Azure AD di tipo *App Web/API* nel [portale di Azure](https://portal.azure.com). Per altre informazioni su come creare la registrazione di un'app, vedere [Registrare l'applicazione nel tenant di Azure Active Directory](/azure/active-directory/active-directory-app-registration). Nel **portale di Azure** sarà anche necessario concedere alla nuova app Web registrata autorizzazioni di *Collaboratore* per il gruppo di risorse che contiene l'area di lavoro OMS che ospita i dati di Preparazione aggiornamenti. La **Procedura guidata per i servizi di Azure** userà questa registrazione dell'app per consentire a Configuration Manager di comunicare in modo sicuro con Azure AD e connettere l'infrastruttura ai dati di Preparazione aggiornamenti.

>[!IMPORTANT]
>Le autorizzazioni di *Collaboratore* devono essere concesse all'app stessa e non a un'identità utente di Azure AD. Il motivo è che è l'app registrata, e non un utente di Azure AD, ad accedere ai dati per conto dell'infrastruttura di Configuration Manager. Per concedere le autorizzazioni, durante l'assegnazione dell'autorizzazione è necessario cercare il nome della registrazione dell'app nell'area **Aggiungi utenti**. Questo è lo stesso processo da seguire per [concedere a Configuration Manager autorizzazioni per OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) per le connessioni a [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). È necessario completare questi passaggi prima che la registrazione dell'app venga importata in Configuration Manager con la *Procedura guidata per i servizi di Azure*.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Usare la procedura guidata per Azure per creare la connessione

Seguire le istruzioni incluse in [Configurare i servizi di Azure da usare con Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) per creare una connessione a Preparazione aggiornamenti importando la registrazione dell'app Web creata sopra. 

Nella pagina *Configurazione* vengono immessi automaticamente i valori seguenti se l'importazione dell'app Web è riuscita e sono state assegnate le autorizzazioni corrette nel **portale di Azure**. 
-  Sottoscrizioni Azure
-  Gruppo di risorse di Azure
-  Area di lavoro di Windows Analytics

Saranno disponibili più di un gruppo di risorse o di un'area di lavoro solo se l'app Web Azure AD registrata ha autorizzazioni di *Collaboratore* per più di un gruppo di risorse o se il gruppo di risorse selezionato ha più di un'area di lavoro OMS.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Visualizzare e usare le informazioni di Preparazione aggiornamenti in Configuration Manager

Dopo aver integrato Preparazione aggiornamenti con Configuration Manager, è possibile visualizzare l'analisi della conformità agli aggiornamenti dei client.

1. Nella console di Configuration Manager, scegliere **Monitoraggio** > **Panoramica** > **Upgrade Readiness**.
2. Esaminare i dati, che includono lo stato di preparazione per l'aggiornamento e la percentuale di dispositivi Windows che eseguono report di telemetria.
3. È possibile filtrare il dashboard per visualizzare i dati di dispositivi appartenenti a raccolte specifiche.
4. È possibile visualizzare i dispositivi in uno stato di conformità specifico e creare una raccolta dinamica per tali dispositivi, per poterli aggiornare quando sono pronti o in modo da intervenire per correggere i dispositivi per cui è stato bloccato l'aggiornamento.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Uso del connettore di Preparazione aggiornamenti (versione 1702 e precedenti)

In Configuration Manager 1702 o versioni precedenti è necessario completare un insieme diverso di passaggi e requisiti per creare una connessione a Preparazione aggiornamenti.

### <a name="prerequisites"></a>Prerequisiti

- Per l'aggiunta della connessione, è necessario che nell'ambiente di Configuration Manager sia stato configurato un [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in [modalità online](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Quando si aggiunge la connessione all'ambiente, viene installato anche Microsoft Monitoring Agent nel computer che esegue questo ruolo del sistema del sito.
- Registrare Configuration Manager come strumento di gestione "Applicazione Web e/o API Web" e ottenere l'[ID client della registrazione](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Creare una chiave client per lo strumento di gestione registrato in Azure Active Directory.
- Nel portale di Azure specificare l'autorizzazione per accedere a OMS per l'app Web registrata, come descritto in [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quando si configura l'autorizzazione per accedere a OMS, assicurarsi di scegliere il ruolo **Collaboratore** e di assegnare a tale ruolo le autorizzazioni per il gruppo di risorse dell'app registrata.

### <a name="create-the-connection"></a>Creare la connessione

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Servizi cloud** > **Upgrade Analytics Connector (Connettore Upgrade Analytics)** > **Crea connessione ad Upgrade Analytics** per avviare **Aggiungi la connessione guidata a Upgrade Analytics**.
3.  Nella schermata **Azure Active Directory** specificare valori per **Tenant**, **ID client**  e **Chiave privata del client** e selezionare **Avanti**.
4.  Nella schermata **Upgrade Readiness** specificare le impostazioni di connessione in **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.
5.  Verificare le impostazioni di connessione nella schermata **Riepilogo** e selezionare **Avanti**.

    > [!NOTE]
    > È necessario che Upgrade Readiness sia connesso al sito di livello più alto nella gerarchia. Se si connette Upgrade Readiness a un sito primario autonomo e poi si aggiunge un sito di amministrazione centrale all'ambiente, è necessario eliminare e ricreare la connessione di OMS nella nuova gerarchia.
