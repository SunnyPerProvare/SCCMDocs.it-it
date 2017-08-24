---
title: Gestire l'accesso a Dynamics CRM Online | Microsoft Docs
description: Informazioni su come controllare l'accesso a Microsoft Dynamics CRM Online da dispositivi iOS e Android con accesso condizionale di Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Gestire l'accesso a Dynamics CRM Online in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile controllare l'accesso a Microsoft Dynamics CRM Online da dispositivi iOS e Android con accesso condizionale di Microsoft Intune.  L'accesso condizionale di Intune include due componenti:
* I [criteri di conformità dei dispositivi](../../protect/deploy-use/device-compliance-policies.md) che il dispositivo deve soddisfare per essere considerato conforme.
* I [criteri di accesso condizionale](../../protect/deploy-use/manage-access-to-services.md) che consentono di specificare le condizioni che il dispositivo deve soddisfare per poter accedere al servizio.

Per altre informazioni sul funzionamento dell'accesso condizionale, leggere l'articolo [Gestire l'accesso ai servizi](../../protect/deploy-use/manage-access-to-services.md).


Quando un utente di destinazione prova a usare l'app Dynamics CRM nel proprio dispositivo, vengono effettuate le valutazioni seguenti:

![La figura mostra i punti decisionali usati per determinare se consentire a un dispositivo di accedere a un servizio o bloccare l'accesso](media/mdm-ca-dynamics-crm-flow-diagram.png)

Il dispositivo che necessita di accedere a Dynamics CRM Online deve:
* Essere un dispositivo **Android** o **iOS**.
* Essere **registrato** in Microsoft Intune.
* Essere **conforme** ai criteri di conformità di Microsoft Intune distribuiti.

Lo stato del dispositivo viene archiviato in Azure Active Directory che consente o blocca l'accesso, in base alle condizioni specificate.

Se non viene soddisfatta una condizione, viene visualizzato uno dei due messaggi seguenti quando l'utente esegue l'accesso:
* Se il dispositivo non è registrato con Microsoft Intune oppure non è registrato in Azure Active Directory, viene visualizzato un messaggio contenente le istruzioni su come installare l'app Portale aziendale ed eseguire la registrazione.
* Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al sito Web del portale aziendale di Microsoft Intune o all'app Portale aziendale dove sono disponibili informazioni sul problema e su come risolverlo.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configurare l'accesso condizionale per Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Passaggio 1: Configurare i gruppi di sicurezza di Active Directory

Prima di iniziare configurare i gruppi di sicurezza di Azure Active Directory per i criteri di accesso condizionale. È possibile configurare questi gruppi nel **centro di amministrazione di Office 365**. I gruppi verranno usati per applicare o ignorare i criteri per gli utenti. Per poter accedere alle risorse, un utente di destinazione in un criterio deve usare solo dispositivi conformi.

È possibile specificare due tipi di gruppo da usare per i criteri di Dynamics CRM:
* **Gruppi di destinazione**: contiene i gruppi di utenti per i quali si applicano i criteri.
* **Gruppi esentati**: contiene i gruppi di utenti che sono esentati dai criteri.

Se un utente si trova in entrambi i gruppi, sarà esentato dai criteri.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passaggio 2: Configurare e distribuire i criteri di conformità
[Creare e distribuire](../../protect/deploy-use/device-compliance-policies.md) i criteri di conformità in tutti i dispositivi cui verranno applicati i criteri. Si tratta di tutti i dispositivi usati dagli utenti dei gruppi di destinazione.

> [!NOTE]
> Mentre i criteri di conformità vengono distribuiti nei gruppi di Microsoft Intune, i criteri di accesso condizionale sono destinati ai gruppi di sicurezza di Azure Active Directory.

> [!IMPORTANT]
> Se non sono stati distribuiti criteri di conformità, i dispositivi verranno considerati conformi.

Quando si è pronti, continuare con il Passaggio 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Passaggio 3: Configurare i criteri di Dynamics CRM
A questo punto, configurare i criteri in modo che solo i dispositivi gestiti e conformi possano accedere a Dynamics CRM. Questi criteri verranno archiviati in Azure Active Directory.

1.  Nella console di amministrazione di Microsoft Intune scegliere **Criteri > Accesso condizionale > Criteri di Dynamics CRM Online**.

     ![Schermata della pagina dei criteri di accesso condizionale di Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  Selezionare **Abilitare i criteri di accesso condizionale**.
3.  In **Accesso all'applicazione**è possibile scegliere di applicare i criteri di accesso condizionale a:
  * **iOS**
  * **Android**
4.  In **Gruppi di destinazione** scegliere **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali verranno applicati i criteri. È possibile scegliere applicare questa opzione a tutti gli utenti o solo a un gruppo selezionato di utenti.
5.  Facoltativamente, in **Gruppi esentati** scegliere **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.
6.  Al termine, scegliere **Salva**.

L'accesso condizionale per Dynamics CRM è stato configurato. Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorare i criteri di conformità e di accesso condizionale

Nell'area di lavoro **Gruppi** è possibile visualizzare lo stato dell'accesso condizionale per i dispositivi.

Selezionare un gruppo qualsiasi di dispositivi mobili e quindi nella scheda **Dispositivi** selezionare uno dei **Filtri**seguenti:
* **Dispositivi non registrati con AAD**: si tratta dei dispositivi che non possono accedere a Dynamics CRM.
* **Dispositivi non conformi**: si tratta dei dispositivi che non possono accedere a Dynamics CRM.
* **Dispositivi conformi e registrati con AAD**: si tratta dei dispositivi che possono accedere a Dynamics CRM.

###  <a name="see-also"></a>Vedere anche
[Gestire l'accesso alla posta elettronica](../../protect/deploy-use/manage-email-access.md)

[Gestire l'accesso a SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Gestire l'accesso a Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)
