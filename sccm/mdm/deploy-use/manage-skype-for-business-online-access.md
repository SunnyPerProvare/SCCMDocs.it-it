---
title: Gestire l'accesso a Skype for Business Online | Microsoft Docs
description: Informazioni su come usare i criteri di accesso condizionale per gestire l'accesso a Skype for Business Online.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: cacb22a85e74a7d9cae75ad907d0206487cd4dc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-skype-for-business-online-access"></a>Gestire l'accesso a Skype for Business Online

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i criteri di accesso condizionale per  **Skype for Business Online** per gestire l'accesso a Skype for Business Online in base alle condizioni specificate.  


 Quando un utente di destinazione prova a usare Skype for Business Online nel proprio dispositivo, vengono effettuate le valutazioni seguenti:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Prerequisiti  

-   Abilitare l'autenticazione moderna per Skype for Business Online. Compilare il [modulo di connessione](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) per effettuare la registrazione nel programma di autenticazione moderna.  

-   Tutti gli utenti finali devono usare Skype for Business Online. Se si ha una distribuzione con Skype for Business Online e Skype for Business locale, i criteri di accesso condizionale non verranno applicati agli utenti finali.  

-   Il dispositivo che ha bisogno di accedere a Skype for Business Online deve:  

    -   Essere un dispositivo Android o iOS.  

    -   Essere registrato con Intune.  

    -   Essere compatibile con i criteri di compatibilità di Intune distribuiti.  

 Lo stato del dispositivo viene archiviato in Azure Active Directory che consente o blocca l'accesso, in base alle condizioni specificate.  
Se non viene soddisfatta una condizione, viene visualizzato uno dei due messaggi seguenti quando l'utente esegue l'accesso:  

-   Se il dispositivo non è registrato con Intune oppure non è registrato in Azure Active Directory, viene visualizzato un messaggio contenente le istruzioni su come installare l'app Portale aziendale ed eseguire la registrazione.  

-   Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al sito Web del portale aziendale di Intune o all'app Portale aziendale dove sono disponibili informazioni sul problema e su come risolverlo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurare l'accesso condizionale per Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passaggio 1: Configurare i gruppi di sicurezza di Active Directory  
 Prima di iniziare configurare i gruppi di sicurezza di Azure Active Directory per i criteri di accesso condizionale. È possibile configurare questi gruppi nel centro di amministrazione di Office 365. Questi gruppi contengono gli utenti a cui saranno destinati i criteri o che ne saranno esenti. Per poter accedere alle risorse, un utente di destinazione in un criterio deve usare solo dispositivi conformi.  

 È possibile specificare due tipi di gruppo da usare per i criteri di Skype for Business Online:  

-   Gruppi di destinazione: contiene i gruppi di utenti per i quali si applicano i criteri  

-   Gruppi esentati: contiene i gruppi di utenti che sono esentati dai criteri (facoltativo)  
    Se un utente si trova in entrambi i gruppi, sarà esentato dai criteri.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passaggio 2: Configurare e distribuire i criteri di conformità  
 Assicurarsi di creare e distribuire i criteri di conformità in tutti i dispositivi a cui saranno destinati i criteri di Skype for Business Online.  

 Per informazioni dettagliate su come configurare i criteri di conformità, vedere [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se non sono stati distribuiti criteri di conformità e non sono stati abilitati i criteri di Skype for Business Online, l'accesso sarà consentito a tutti i dispositivi di destinazione se sono registrati in Intune.  

 Quando si è pronti, continuare con il Passaggio 3.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Passaggio 3: Configurare i criteri di Skype for Business Online  
 A questo punto, configurare i criteri in modo che solo i dispositivi gestiti e conformi possano accedere a Skype for Business Online. Questi criteri verranno archiviati in Azure Active Directory.  

1.  Nella [console di amministrazione di Microsoft Intune](https://manage.microsoft.com) fare clic su **Criteri** > **Accesso condizionale** > **Criteri di Skype for Business Online**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selezionare **Abilitare i criteri di accesso condizionale**.  

3.  In **Accesso all'applicazione**è possibile scegliere di applicare i criteri di accesso condizionale a:  

    -   iOS  

    -   Android  

4.  In **Gruppi di destinazione**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali verranno applicati i criteri. È possibile scegliere applicare questa opzione a tutti gli utenti o solo a un gruppo selezionato di utenti.  

5.  Facoltativamente, in **Gruppi esentati**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.  

6.  Al termine, fare clic su **Salva**.  

 È stato configurato l'accesso condizionale per Skype for Business Online. Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorare i criteri di conformità e di accesso condizionale  
 Nell'area di lavoro Gruppi è possibile visualizzare lo stato dell'accesso condizionale per i dispositivi.  

 Selezionare un gruppo qualsiasi di dispositivi mobili e quindi nella scheda **Dispositivi** selezionare uno dei **Filtri**seguenti:  

-   **Dispositivi non registrati con AAD**: questi dispositivi non possono accedere a Skype for Business Online.  

-   **Dispositivi non conformi**: questi dispositivi non possono accedere a Skype for Business Online.  

-   **Dispositivi conformi e registrati con AAD**: questi dispositivi possono accedere a Skype for Business Online.  

### <a name="see-also"></a>Vedere anche  

 [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
