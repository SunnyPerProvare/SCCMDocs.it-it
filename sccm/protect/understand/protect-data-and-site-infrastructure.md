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
ms.openlocfilehash: fc680486454957c83936525e7403a975d8d3f94a
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035075"
---
# <a name="protect-data-and-site-infrastructure"></a>Proteggere dati e infrastruttura e del sito

*Si applica a: Configuration Manager (Current Branch)*

Si vuole che gli utenti accedano in modo sicuro alle risorse dell'organizzazione. È necessario proteggere l'infrastruttura e i dati dall'esposizione o da attacchi dannosi. Usare Configuration Manager per abilitare l'accesso e proteggere le risorse dell'organizzazione.  

- [Endpoint Protection](/configmgr/protect/deploy-use/endpoint-protection) consente di gestire i criteri di Microsoft Defender seguenti per i computer client:

  - Microsoft Defender Antimalware
  - Microsoft Defender Firewall
  - Microsoft Defender Advanced Threat Protection
  - Microsoft Defender Exploit Guard
  - Microsoft Defender Application Guard
  - Controllo di applicazioni di Microsoft Defender

  > [!TIP]
  > Per gestire Endpoint Protection in dispositivi Windows 10 con co-gestione usando il servizio cloud di Microsoft Endpoint Manager, spostare il [carico di lavoro **Endpoint Protection**](/configmgr/comanage/workloads#endpoint-protection) in Intune. Per altre informazioni, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Proteggere i dati archiviati nei client Windows locali con Crittografia unità BitLocker (BDE). Configuration Manager offre una gestione completa del ciclo di vita di BitLocker che sostituisce l'uso di Microsoft BitLocker Administration and Monitoring (MBAM). Per altre informazioni, vedere [Pianificare la gestione di BitLocker](/configmgr/protect/plan-design/bitlocker-management).

- Invece delle password tradizionali, abilitare metodi di accesso alternativi nei dispositivi Windows 10 con Windows Hello for Business. Per altre informazioni, vedere [Impostazioni di Windows Hello for Business](/configmgr/protect/deploy-use/windows-hello-for-business-settings).

- Ridurre al minimo le operazioni eseguite dagli utenti per connettersi alle risorse abilitando la connettività VPN con i profili VPN. Per altre informazioni, vedere [Profili VPN](/configmgr/protect/deploy-use/vpn-profiles).  

- I profili Wi-Fi forniscono un set di strumenti e risorse che consentono di gestire le impostazioni di rete wireless nei dispositivi dell'organizzazione. Distribuendo queste impostazioni, è possibile ridurre al minimo l'impegno richiesto agli utenti finali per connettersi alle reti wireless. Per altre informazioni, vedere [Profili Wi-Fi](/configmgr/protect/deploy-use/create-wifi-profiles).  

- Eseguire il provisioning dei dispositivi con i certificati necessari agli utenti per connettersi alle risorse. Per altre informazioni, vedere i [profili certificato](/configmgr/protect/deploy-use/introduction-to-certificate-profiles).  
