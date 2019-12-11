---
title: Configurare le app Android for Work con i criteri di configurazione delle app
titleSuffix: Configuration Manager
description: Questa operazione consente di evitare problemi di configurazione sui dispositivi che eseguono Android for Work distribuendo i criteri di configurazione delle app agli utenti prima che gli utenti eseguano le app.
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d6f8c25902be857e0eec3cd4b969d1fb5bda136
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62288769"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Applicare le impostazioni alle app Android for Work con i criteri di configurazione delle app in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare i criteri di configurazione delle app in System Center Configuration Manager per distribuire impostazioni che potrebbero essere necessarie quando un utente esegue un'app. Ad esempio, un'app potrebbe richiedere all'utente di specificare i seguenti dettagli:
- Un numero di porta personalizzato
- Impostazione della lingua
- Impostazioni di sicurezza
- Impostazioni di personalizzazione, ad esempio il logo aziendale

Se l'utente immette le impostazioni in modo errato, il carico di lavoro per la risoluzione ricade sul supporto tecnico e la distribuzione delle app risulta lenta. Per evitare questi problemi, è possibile usare criteri di configurazione delle app per distribuire le impostazioni necessarie agli utenti prima che questi eseguano l'app. Le impostazioni vengono associate a un utente in modo automatico. L'utente non deve eseguire nessuna operazione.
Anziché distribuire i criteri di configurazione direttamente a utenti e dispositivi, si associano i criteri a un tipo di distribuzione quando si distribuisce l'app. Le impostazioni dei criteri vengono applicate ogni volta che l'app controlla se sono disponibili, in genere alla prima esecuzione dell'app stessa.

I criteri di configurazione delle app per Android sono disponibili solo nei dispositivi che eseguono Android for Work e riguardano le app approvate per lo store Play for Work. Per informazioni dettagliate sulle app Android acquistate con Volume Purchase Program, vedere [Come distribuire app a dispositivi Android for Work con Intune](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Per altre informazioni sui tipi di installazione delle app, vedere l'[introduzione alla gestione delle applicazioni](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Creare criteri di configurazione delle app

1. Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Criteri di configurazione dell'app**.
2. Nella scheda **Home**, nel gruppo **Criteri di configurazione dell'app** fare clic su **Creare i criteri di configurazione dell'app**.
3. Nella pagina **Generale** della Creazione guidata criteri di configurazione dell'app impostare le seguenti informazioni per i criteri:
   - **Nome**. Immettere un nome univoco per i criteri.
   - **Descrizione**. (Facoltativo) Per rendere più semplice l'identificazione dei criteri, è possibile aggiungere una descrizione.
   -  **Selezionare un tipo di criteri di configurazione**. Specificare la piattaforma di destinazione per i criteri di configurazione dell'app: **Configuration policy for Android for Work apps** (Criteri di configurazione per app Android for Work).
   -  **Categorie assegnate per migliorare la ricerca e i filtri**. (Facoltativo) Per creare e assegnare categorie ai criteri, scegliere **Categorie**. Con le categorie è più semplice trovare e ordinare gli elementi nella console di Configuration Manager.
4. Nella pagina **Criteri Android for Work** scegliere come impostare le informazioni sui criteri di configurazione:
   - **Specify name and value pairs** (Specifica coppie nome/valore). È possibile usare questa opzione per i file elenco di proprietà senza annidamento. Per specificare una coppia nome/valore:
        1. Scegliere **Nuova** per aggiungere una nuova coppia JSON.
        2. Nella finestra di dialogo **Aggiungere la coppia nome-valore** specificare i dettagli seguenti:
            - **Tipo**. Scegliere il tipo di valore da specificare nell'elenco.
            - **Nome**. Immettere il nome della chiave dell'elenco di proprietà per la quale si vuole specificare un valore.
            - **Valore**. Digitare il valore che verrà applicato alla chiave immessa.

   - **Browse to a property list JSON file** (Passa a un file JSON elenco di proprietà). Usare questa opzione se è già presente un file JSON di configurazione app o per file più complessi con annidamento. Nel campo **Criteri di configurazione dell'app** immettere le informazioni sull'elenco di proprietà nel formato JSON corretto.
5. Per importare un file JSON creato in precedenza, scegliere **Seleziona file**.
6. Scegliere **Avanti**. Se sono presenti errori nel codice JSON, correggerli prima di continuare.
7. Completare i passaggi della procedura guidata.

I nuovi criteri di configurazione app vengono visualizzati nel nodo **Criteri di configurazione dell'app** dell'area di lavoro **Raccolta software**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associare un criterio di configurazione delle app a un'applicazione di Configuration Manager

Per associare criteri di configurazione delle app alla distribuzione di un'app per Android for Work, distribuire l'applicazione nel modo consueto con la procedura descritta nell'argomento [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications).

Nella pagina **Criteri di configurazione dell'app** della Distribuzione guidata del software fare clic su **Nuovo**. Nella finestra di dialogo **Select App Configuration Policy** (Seleziona criteri di configurazione dell'app) scegliere un tipo di distribuzione dell'applicazione e i criteri di configurazione dell'app ai quali associarla.
Quando viene installato il tipo di distribuzione, le impostazioni dei criteri di configurazione dell'app vengono applicate automaticamente.
