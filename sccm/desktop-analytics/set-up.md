---
title: Configurare Desktop Analytics
titleSuffix: Configuration Manager
description: Guida alle procedure per la configurazione e l'onboarding in desktop Analytics.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad8111b7d49f89b85c2a4f8b0bd9336a13446a91
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243663"
---
# <a name="how-to-set-up-desktop-analytics"></a>Come configurare analisi desktop

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Usare questa procedura per accedere a desktop Analytics e configurarlo nella sottoscrizione. Questa procedura è un processo unico per la configurazione di analisi desktop per l'organizzazione.  


> [!Important]  
> Per informazioni sui prerequisiti generali per analisi desktop con Configuration Manager, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  

## <a name="initial-onboarding"></a>Onboarding iniziale

1. Aprire il [portale di analisi del desktop](https://aka.ms/desktopanalytics) in Microsoft 365 gestione dei dispositivi come utente con il ruolo di **amministratore globale** . Selezionare **Avvia**. In alternativa, nella console di Configuration Manager passare all'area di lavoro **raccolta software** , selezionare il nodo **servizio di analisi desktop** e selezionare **Pianifica distribuzioni**.

2. Nella pagina **accetta contratto di servizio** esaminare il contratto di servizio e selezionare **accetta**.  

3. Nella pagina **conferma sottoscrizione** esaminare l'elenco delle licenze idonee necessarie. Impostare l'opzione su **Sì** accanto a **una delle sottoscrizioni supportate o superiori**, quindi selezionare **Avanti**.  

4. Nella pagina **Give users access** :

    - **Consenti a desktop Analytics di gestire i ruoli della directory per conto dell'utente**: Desktop Analytics assegna automaticamente ai **proprietari dell'area di lavoro** il ruolo di amministratore di **Desktop Analytics** . Se tali gruppi sono già un **amministratore globale**, non vi sono modifiche.

        Se non si seleziona questa opzione, desktop Analytics aggiunge ancora gli utenti come membri del gruppo di sicurezza. Un **amministratore globale** deve assegnare manualmente il ruolo di **amministratore di analisi desktop** per gli utenti.   

        Per ulteriori informazioni sull'assegnazione delle autorizzazioni del ruolo amministratore in Azure Active Directory e sulle autorizzazioni assegnate agli **amministratori di desktop Analytics**, vedere autorizzazioni per i [ruoli di amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics preconfigura il gruppo di sicurezza **proprietari dell'area di lavoro** in Azure Active Directory per creare e gestire aree di lavoro e piani di distribuzione. 

        Per aggiungere un utente al gruppo, digitarne il nome o l'indirizzo di posta elettronica nella sezione **immettere il nome o l'indirizzo di posta elettronica** . Al termine, selezionare **Avanti**.

5. Nella pagina per **configurare l'area di lavoro**:  

    - Per usare un'area di lavoro esistente per analisi desktop, selezionarla e continuare con il passaggio successivo.  

        > [!Note]  
        > È possibile avere solo un'area di lavoro di analisi desktop per ogni tenant Azure AD. I dispositivi possono inviare i dati di diagnostica solo a un'area di lavoro.  

        Se si sta già usando Windows Analytics, selezionare la stessa area di lavoro. È necessario registrare nuovamente i dispositivi in desktop Analytics registrati in precedenza in Windows Analytics.

        Per eseguire la migrazione degli input dall'area di lavoro di Windows Analytics selezionata, impostare si **desidera visualizzare gli input da Windows Analytics?** su **Sì**. Se non si vuole eseguire la migrazione, impostare questa opzione su **No**. Per ulteriori informazioni, vedere le domande frequenti per [i clienti esistenti di Windows Analytics](/sccm/desktop-analytics/faq#existing-windows-analytics-customers).

    - Per creare un'area di lavoro per desktop Analytics, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome**per l'area di lavoro.<!--do we have any guidance for this name?-->  

        2. Selezionare l'elenco a discesa per **selezionare il nome della sottoscrizione di Azure per l'area di lavoro**e scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. **Crea nuovo** Gruppo di risorse o **utilizza esistente**.

        4. Selezionare l' **area** nell'elenco e quindi selezionare **Aggiungi**.  

6. Selezionare un'area di lavoro nuova o esistente e quindi selezionare **Imposta come area di lavoro di analisi del desktop**.  Quindi selezionare **continua** nella finestra di dialogo **conferma e Concedi accesso** .  

7. Nella scheda nuovo browser selezionare un account da usare per l'accesso. Selezionare l'opzione per il **consenso per conto dell'organizzazione** e selezionare **accetta**.  

    > [!Note]  
    > Questo consenso consiste nell'assegnare all'applicazione MALogAnalyticsReader il ruolo di lettore Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da desktop Analytics. Per ulteriori informazioni, vedere [ruolo applicazione MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina per **configurare l'area di lavoro**, quindi fare clic su **Avanti**.  

9. Nella pagina **Last Steps** selezionare **go to desktop Analytics**.

Il portale di Azure Mostra la **Home** page di analisi del desktop.


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per connettersi Configuration Manager con analisi desktop.
> [!div class="nextstepaction"]  
> [Connetti Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
