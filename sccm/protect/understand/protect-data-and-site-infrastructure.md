---
title: Proteggere dati e infrastruttura e del sito
titleSuffix: Configuration Manager
description: Informazioni su come proteggere le risorse dell'organizzazione da esposizione o attacchi dannosi con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86eed6ef79a098bb53237890e410747d78788acd
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74660819"
---
# <a name="protect-data-and-site-infrastructure"></a>Proteggere dati e infrastruttura e del sito

*Si applica a: Configuration Manager (Current Branch)*

Si vuole che gli utenti accedano in modo sicuro alle risorse dell'organizzazione. Proteggi la tua infrastruttura e i tuoi dati da esposizione o attacchi dannosi. Usare Configuration Manager per abilitare l'accesso e proteggere le risorse dell'organizzazione.  

- [Endpoint Protection](/configmgr/protect/deploy-use/endpoint-protection) consente di gestire i criteri di Microsoft Defender seguenti per i computer client:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Controllo di applicazioni di Microsoft Defender

  > [!TIP]
  > Per gestire Endpoint Protection in dispositivi Windows 10 con co-gestione usando il servizio cloud di Microsoft Endpoint Manager, passare il [carico di lavoro **Endpoint Protection** ](/configmgr/comanage/workloads#endpoint-protection) a Intune. Per ulteriori informazioni, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Proteggi i dati archiviati nei client Windows locali con Crittografia unità BitLocker (BDE). Configuration Manager offre una gestione completa del ciclo di vita di BitLocker che può sostituire l'utilizzo di Microsoft BitLocker Administration and Monitoring (MBAM). Per ulteriori informazioni, vedere [pianificare la gestione di BitLocker](/configmgr/protect/plan-design/bitlocker-management).

- Anziché le password tradizionali, abilitare metodi di accesso alternativi nei dispositivi Windows 10 che usano Windows Hello for business. Per altre informazioni, vedere [Impostazioni di Windows Hello for Business](/configmgr/protect/deploy-use/windows-hello-for-business-settings).

- Ridurre al minimo le operazioni eseguite dagli utenti per connettersi alle risorse abilitando la connettività VPN con i profili VPN. Per altre informazioni, vedere [Profili VPN](/configmgr/protect/deploy-use/vpn-profiles).  

- I profili Wi-Fi forniscono un set di strumenti e risorse che consentono di gestire le impostazioni di rete wireless nei dispositivi della propria organizzazione. Distribuendo queste impostazioni, è possibile ridurre al minimo l'impegno richiesto agli utenti finali per connettersi alle reti wireless. Per altre informazioni, vedere [Profili Wi-Fi](/configmgr/protect/deploy-use/create-wifi-profiles).  

- Eseguire il provisioning dei dispositivi con i certificati necessari agli utenti per connettersi alle risorse. Per altre informazioni, vedere i [profili certificato](/configmgr/protect/deploy-use/introduction-to-certificate-profiles).  

- I profili di posta elettronica offrono un set di strumenti e risorse per creare, distribuire e monitorare le impostazioni di posta elettronica nei dispositivi. Consentire agli utenti di accedere alla posta elettronica sui dispositivi personali senza alcuna configurazione necessaria. Per altre informazioni, vedere [Profili di posta elettronica](/configmgr/protect/deploy-use/introduction-to-email-profiles).  
