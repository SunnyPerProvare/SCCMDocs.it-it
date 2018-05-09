---
title: Gestire l'accesso a Skype for Business Online
titleSuffix: Configuration Manager
description: Informazioni su come usare i criteri di accesso condizionale per gestire l'accesso a Skype for Business Online.
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a88706233e85be6960585963c26bd740e9ff6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-skype-for-business-online-access"></a>Gestire l'accesso a Skype for Business Online

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i criteri di accesso condizionale per Skype for Business Online per gestire l'accesso a Skype for Business Online in base alle condizioni specificate.  


 Quando un utente di destinazione prova a usare Skype for Business Online nel proprio dispositivo, vengono effettuate le valutazioni seguenti:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Prerequisiti  

-   Abilitare l'[autenticazione moderna](https://aka.ms/SkypeModernAuth) per Skype for Business Online.   

-   Tutti gli utenti devono usare Skype for Business Online. Se si ha una distribuzione con Skype for Business Online e Skype for Business locale, i criteri di accesso condizionale non vengono applicati agli utenti locali.  

-   Il dispositivo che ha bisogno di accedere a Skype for Business Online deve:  

    -   Essere un dispositivo Android o iOS

    -   Essere registrato in Microsoft Intune

    -   Essere conforme ai criteri di conformità di Microsoft Intune distribuiti

 Azure Active Directory archivia lo stato del dispositivo che consente o blocca l'accesso, in base alle condizioni specificate.  
Se non viene soddisfatta una condizione, viene visualizzato uno dei messaggi seguenti quando l'utente esegue l'accesso:  

-   Se il dispositivo non è registrato in Microsoft Intune oppure non è registrato in Azure Active Directory, viene visualizzato un messaggio contenente le istruzioni su come installare l'app del portale aziendale ed eseguire la registrazione.  

-   Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al sito Web o all'app del portale aziendale. Il portale aziendale contiene informazioni sul problema e su come risolverlo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurare l'accesso condizionale per Skype for Business Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passaggio 1: Configurare i gruppi di sicurezza di Active Directory  
 Prima di iniziare configurare i gruppi di sicurezza di Azure Active Directory per i criteri di accesso condizionale. Configurare questi gruppi nell'interfaccia di amministrazione di Office 365. Questi gruppi contengono gli utenti ai quali destinare i criteri o da escludere. Per poter accedere alle risorse, un utente di destinazione in un criterio deve usare solo dispositivi conformi.  

 È possibile specificare due tipi di gruppo da usare per i criteri di Skype for Business Online:  

-   I **gruppi di destinazione** contengono gli utenti ai quali applicare i criteri  

-   I **gruppi esentati** contengono gli utenti che devono essere esclusi dai criteri  
    Se un utente è presente in entrambi i gruppi, viene esentato.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passaggio 2: Configurare e distribuire i criteri di conformità  
 Creare e distribuire i criteri di conformità in tutti i dispositivi a cui sono destinati i criteri di Skype for Business Online.  

 Per informazioni dettagliate su come configurare i criteri di conformità, vedere [Gestire i criteri di conformità del dispositivo](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se non sono stati distribuiti criteri di conformità e non sono stati abilitati i criteri di Skype for Business Online, l'accesso è consentito a tutti i dispositivi di destinazione se sono registrati in Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Passaggio 3: Configurare i criteri di Skype for Business Online  
 Configurare i criteri in modo che solo i dispositivi gestiti e conformi possano accedere a Skype for Business Online. Questi criteri vengono archiviati in Azure Active Directory.  

1.  Nella [console di amministrazione di Microsoft Intune](https://manage.microsoft.com) fare clic su **Criteri** > **Accesso condizionale** > **Criteri di Skype for Business Online**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selezionare **Abilitare i criteri di accesso condizionale**.  

3.  In **Accesso all'applicazione**è possibile scegliere di applicare i criteri di accesso condizionale a:  

    -   iOS  

    -   Android  

4.  In **Gruppi di destinazione** fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali vengono applicati i criteri. È possibile scegliere di applicare questi criteri a tutti gli utenti o solo a un gruppo selezionato di utenti.  

5.  Facoltativamente, in **Gruppi esentati**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.  

6.  Al termine, fare clic su **Salva**.  

 È stato configurato l'accesso condizionale per Skype for Business Online. Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorare i criteri di conformità e di accesso condizionale  
 Nell'area di lavoro Gruppi è possibile visualizzare lo stato dell'accesso condizionale per i dispositivi.  

 Selezionare un gruppo qualsiasi di dispositivi mobili e quindi nella scheda **Dispositivi** selezionare uno dei **Filtri**seguenti:  

-   **Dispositivi non registrati con AAD**: si tratta dei dispositivi che non possono accedere a Skype for Business Online

-   **Dispositivi non conformi**: si tratta dei dispositivi che non possono accedere a Skype for Business Online  

-   **Dispositivi conformi e registrati con AAD**: si tratta dei dispositivi che possono accedere a Skype for Business Online  

### <a name="see-also"></a>Vedere anche  

 [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
