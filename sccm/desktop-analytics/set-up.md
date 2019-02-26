---
title: Configurare Desktop Analytics
titleSuffix: Configuration Manager
description: Guida dettagliata per l'installazione e onboarding alla Analitica Desktop.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bd3a9efcbc76647ae39eb1a104b401b112d15fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755172"
---
# <a name="how-to-set-up-desktop-analytics"></a>Come configurare Desktop Analitica 

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Utilizzare questa procedura per accedere al Desktop Analitica e configurarlo nella sottoscrizione. Questa procedura è un processo unico per configurare Desktop Analitica per l'organizzazione.  



## <a name="initial-onboarding"></a>Onboarding iniziale

1. Aprire il [portal Desktop Analitica](https://aka.ms/m365aprod) nella gestione dei dispositivi Microsoft 365 come utente con **amministratore società** autorizzazioni. Selezionare **avviare**.  

2. Nel **accettare il contratto di servizio** pagina, esaminare il contratto di servizio e selezionare **Accept**.  

3. Nel **confermare la tua iscrizione** pagina, esaminare l'elenco delle necessarie licenze valide. Configurare l'impostazione **Yes** accanto a **sono una delle sottoscrizioni supportate o versioni successive**e quindi selezionare **Next**.  

4. Nel **concedere l'accesso degli utenti e app** pagina Desktop Analitica preconfigura i due gruppi di sicurezza in Azure Active Directory:  

    - **I proprietari dell'area di lavoro**: Creare e gestire le aree di lavoro. Questi account devono accesso come proprietario della sottoscrizione di Azure.  

    - **I collaboratori dell'area di lavoro**: Creare e gestire i piani di distribuzione nell'area di lavoro. Non è necessario alcun accesso di Azure aggiuntivo.  
  
   Per aggiungere un utente a entrambi i gruppi, digitare l'indirizzo di posta elettronica o nome nella **immettere l'indirizzo di posta elettronica o nome** sezione del gruppo appropriato. Al termine, selezionare **successivo**. 

5. Nella pagina per **configurare l'area di lavoro**:  

    - Per usare un'area di lavoro per Desktop Analitica, selezionarlo e continuare con il passaggio successivo.  

        > [!Note]  
        > Se si usa già Windows Analitica, selezionare tale area di lavoro stesso. È necessario ripetere la registrazione ai dispositivi di Analitica Desktop che sono registrati in precedenza in Analitica di Windows. 
        > 
        > È possibile avere solo un'area di lavoro di Analitica Desktop per ogni tenant di Azure AD. Dispositivi possono inviare solo i dati di diagnostica a un'area di lavoro.   

    - Per creare un'area di lavoro per Desktop Analitica, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome area di lavoro**.<!--do we have any guidance for this name?-->  

        2. Selezionare l'elenco a discesa per **selezionare il nome di sottoscrizione di Azure per l'area di lavoro**, scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. Selezionare il **regione** dall'elenco, quindi selezionare **Add**.  

6. Selezionare un'area di lavoro nuovo o esistente e quindi selezionare **imposta come area di lavoro di Analitica Desktop**.  Quindi selezionare **continuazione** nel **Confirm e concedere l'accesso** finestra di dialogo.  

7. Nella nuova scheda del browser, scegliere un account da usare per l'accesso. Selezionare l'opzione **fornire il consenso per conto dell'organizzazione** e selezionare **Accept**.  

    > [!Note]  
    > Questo consenso consiste nell'assegnare l'applicazione MALogAnalyticsReader il ruolo di lettura Log Analitica per l'area di lavoro. Questo ruolo applicazione è richiesto dal Desktop Analitica. Per altre informazioni, vedere [ruolo applicazione MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina al **configurare l'area di lavoro**, selezionare **successivo**.  

9. Nel **ultimi passaggi** pagina, selezionare **passare al Desktop Analitica**. 

Il portale di Azure Mostra il Desktop Analitica **Home** pagina.



## <a name="create-app-for-configuration-manager"></a>Creare app per Configuration Manager

Creare un'app in Azure AD per Configuration Manager.

1. Nel [portale di Azure](http://portal.azure.com)passare alla **Azure Active Directory**e selezionare **registrazioni per l'App**. Quindi selezionare **registrazione nuova applicazione**.  

2. Nel **Create** panel, configurare le impostazioni seguenti:  

    - **Nome**: un nome univoco che identifica l'app, ad esempio: `Desktop-Analytics-Connection`  

    - **Tipo di applicazione**: **App Web / API**  

    - **URL Sign-on**: questo valore non è usato da Configuration Manager, ma richiesto da Azure AD. Immettere un URL valido e univoco, ad esempio: `https://configmgrapp`  
  
   Selezionare **Create**.  

3. Selezionare l'app e prendere nota di **ID applicazione**. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager.  

4. Selezionare **le impostazioni** relativi all'app e quindi selezionare **chiavi**. Nel **password** , quindi immettere un **descrizione chiave**, specificare una scadenza **durata**e quindi selezionare **Salva**. Copia il **valore** della chiave, che consente di configurare la connessione di Configuration Manager. 

    > [!Important]  
    > Questa è l'unica possibilità per copiare il valore della chiave. Se si non copiarlo a questo punto, è necessario creare un'altra chiave.  
    > 
    > Salvare il valore della chiave in un luogo sicuro.  

5. Nell'app **le impostazioni** Pannello di selezione **autorizzazioni necessarie**.  

    1. Nel **autorizzazioni necessarie** riquadro, seleziona **Aggiungi**.  

    2. Nel **Aggiungi accesso all'API** pannello **selezionare un'API**.  

    3. Cercare il **Microservizio di Configuration Manager** API. Selezionarlo e quindi scegliere **seleziona**.  

    4. Nel **Abilita accesso** pannello, selezionare entrambe le autorizzazioni applicazione: **Scrivere i dati della raccolta CM** e **leggere i dati della raccolta CM**. Quindi scegliere **seleziona**.  

    5. Nel **Aggiungi accesso all'API** Pannello di selezione **eseguita**.  

6. Nel **autorizzazioni necessarie** pagina, selezionare **concedere le autorizzazioni**. Selezionare **Sì**.  

7. Copiare l'ID tenant di Azure AD. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager. Selezionare **Azure Active Directory** nel menu principale e quindi selezionare **proprietà**. Copia il **ID Directory** valore.  



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per connettere Configuration Manager con Desktop Analitica.
> [!div class="nextstepaction"]  
> [Connettere Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
