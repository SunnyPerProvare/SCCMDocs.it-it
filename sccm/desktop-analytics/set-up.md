---
title: Configurare Desktop Analytics
titleSuffix: Configuration Manager
description: Guida dettagliata per l'installazione e onboarding alla Analitica Desktop.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7c899f56829d63cebc29518cbeb7497b6a203cd
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158912"
---
# <a name="how-to-set-up-desktop-analytics"></a>Come configurare Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Utilizzare questa procedura per accedere al Desktop Analitica e configurarlo nella sottoscrizione. Questa procedura è un processo unico per configurare Desktop Analitica per l'organizzazione.  



## <a name="initial-onboarding"></a>Onboarding iniziale

1. Aprire il [portale Desktop Analitica](https://aka.ms/desktopanalytics) nella gestione dei dispositivi Microsoft 365 come utente con il **amministratore globale** ruolo. Selezionare **avviare**.  

    > [!Tip]  
    > Per accedere al portale di Analitica Desktop dalla console di Configuration Manager, passare al **raccolta Software** dell'area di lavoro, seleziona il **Desktop Analitica Servicing** nodo e selezionare **piano le distribuzioni**.

2. Nel **accettare il contratto di servizio** pagina, esaminare il contratto di servizio e selezionare **Accept**.  

3. Nel **confermare la tua iscrizione** pagina, esaminare l'elenco delle necessarie licenze valide. Configurare l'impostazione **Yes** accanto a **sono una delle sottoscrizioni supportate o versioni successive**e quindi selezionare **Next**.  

4. Nel **consentire agli utenti accesso** pagina:

    - **Chcete Desktop Analitica per gestire i ruoli della Directory per gli utenti**: Desktop Analitica assegna automaticamente le **i proprietari dell'area di lavoro** e **collaboratori dell'area di lavoro** Raggruppa per il **Analitica Desktop Administrator** ruolo. Se tali gruppi ha già un **amministratore globale**, non è stata modificata.  

        Se non si seleziona questa opzione, Analitica Desktop aggiunge comunque agli utenti come membri di due gruppi di sicurezza. Oggetto **amministratore globale** deve assegnare manualmente le **Desktop Administrator Analitica** ruolo per gli utenti.  

        Per altre informazioni sull'assegnazione di autorizzazioni del ruolo amministratore in Azure Active Directory e le autorizzazioni assegnate ai **gli amministratori di Desktop Analitica**, vedere [le autorizzazioni del ruolo amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analitica preconfigura due gruppi di sicurezza in Azure Active Directory:  

        - **I proprietari dell'area di lavoro**: Un gruppo di sicurezza per creare e gestire le aree di lavoro. Questi account devono accesso come proprietario della sottoscrizione di Azure.  

        - **I collaboratori dell'area di lavoro**: Un gruppo di sicurezza per creare e gestire i piani di distribuzione nell'area di lavoro. Non è necessario alcun accesso di Azure aggiuntivo.  

        Per aggiungere un utente a entrambi i gruppi, digitare l'indirizzo di posta elettronica o nome nella **immettere l'indirizzo di posta elettronica o nome** sezione del gruppo appropriato. Al termine, selezionare **successivo**.

5. Nella pagina per **configurare l'area di lavoro**:  

    > [!Note]  
    > Completare questo passaggio come un **proprietario dell'area di lavoro** oppure **collaboratore**. Per altre informazioni, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  

    - Per usare un'area di lavoro per Desktop Analitica, selezionarlo e continuare con il passaggio successivo.  

        > [!Note]  
        > Se si usa già Windows Analitica, selezionare tale area di lavoro stesso. È necessario ripetere la registrazione ai dispositivi di Analitica Desktop che sono registrati in precedenza in Analitica di Windows.
        >
        > È possibile avere solo un'area di lavoro di Analitica Desktop per ogni tenant di Azure AD. Dispositivi possono inviare solo i dati di diagnostica a un'area di lavoro.  

    - Per creare un'area di lavoro per Desktop Analitica, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome area di lavoro**.<!--do we have any guidance for this name?-->  

        2. Selezionare l'elenco a discesa per **selezionare il nome di sottoscrizione di Azure per l'area di lavoro**, scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. **Creare un nuovo** gruppo di risorse oppure **Usa esistente**.

        4. Selezionare il **regione** dall'elenco, quindi selezionare **Add**.  

6. Selezionare un'area di lavoro nuovo o esistente e quindi selezionare **imposta come area di lavoro di Analitica Desktop**.  Quindi selezionare **continuazione** nel **Confirm e concedere l'accesso** finestra di dialogo.  

7. Nella nuova scheda del browser, scegliere un account da usare per l'accesso. Selezionare l'opzione **fornire il consenso per conto dell'organizzazione** e selezionare **Accept**.  

    > [!Note]  
    > Questo consenso consiste nell'assegnare l'applicazione MALogAnalyticsReader il ruolo di lettura Log Analitica per l'area di lavoro. Questo ruolo applicazione è richiesto dal Desktop Analitica. Per altre informazioni, vedere [ruolo applicazione MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina al **configurare l'area di lavoro**, selezionare **successivo**.  

9. Nel **ultimi passaggi** pagina, selezionare **passare al Desktop Analitica**.

Il portale di Azure Mostra il Desktop Analitica **Home** pagina.


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per connettere Configuration Manager con Desktop Analitica.
> [!div class="nextstepaction"]  
> [Connettere Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
