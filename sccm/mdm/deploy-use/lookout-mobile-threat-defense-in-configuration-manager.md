---
title: Limitare l'accesso in base ai rischi | Microsoft Docs
description: Limitare l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile controllare l'accesso dai dispositivi mobili alle risorse aziendali in base alla valutazione dei rischi condotta da Lookout, una soluzione di protezione dalle minacce per i dispositivi integrata con Microsoft Intune. Il rischio si basa su dati di telemetria che il servizio Lookout raccoglie dai dispositivi per vulnerabilità del sistema operativo, app dannose installate e profili di rete dannosi. 

In base alla valutazione dei rischi segnalati da Lookout abilitata tramite i criteri di conformità di System Center Configuration Manager (SCCM), è possibile configurare criteri di accesso condizionale e consentire o bloccare i dispositivi che sono stati rilevati come non conformi a causa di minacce in essi rilevate.

La [distribuzione MDM ibrida (SCCM con Intune) ](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) consente di controllare l'accesso alle risorse e ai dati aziendali in base alla valutazione dei rischi offerta da soluzioni di protezione dalle minacce per i dispositivi come Lookout.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>In che modo la distribuzione MDM ibrida e la protezione dalle minacce per i dispositivi di Lookout aiutano a proteggere le risorse aziendali?
L'app per dispositivi mobili di Lookout (Lookout for work), in esecuzione sui dispositivi mobili, acquisisce file system, stack di rete e dati di telemetria di dispositivi e applicazioni (se disponibili) e li invia al servizio cloud di protezione dalle minacce per i dispositivi di Lookout per calcolare un rischio complessivo del dispositivo per le minacce per i dispositivi mobili. È anche possibile modificare la classificazione del livello di rischio per le minacce nella console di Lookout in base alle proprie esigenze.  

I criteri di conformità in SCCM includono ora una nuova regola per la protezione dalle minacce per i dispositivi mobili di Lookout basata sulla valutazione del rischio delle minacce per i dispositivi di Lookout. Quando questa regola è abilitata, il dispositivo viene valutato per la conformità.

Se il dispositivo viene indicato come non conforme ai criteri di conformità, è possibile bloccare l'accesso a risorse come Exchange Online e SharePoint Online tramite criteri di accesso condizionale. Quando viene bloccato l'accesso, agli utenti finali viene indicata una procedura dettagliata per risolvere il problema e ottenere l'accesso alle risorse aziendali. Questa procedura dettagliata viene avviata tramite l'app Lookout for work.

## <a name="supported-platforms"></a>Piattaforme supportate:
* **Android 4.1 e versioni successive** e registrate in Microsoft Intune.
* **iOS 8 e versioni successive** e registrate in Microsoft Intune.
Per informazioni sulle piattaforme e i linguaggi supportati da Lookout, vedere questo [articolo](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Prerequisiti:
* [Distribuzione MDM ibrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Una sottoscrizione a Microsoft Intune e Azure Active Directory.
* Una sottoscrizione aziendale a Lookout Mobile EndPoint Security.  Per altre informazioni, vedere [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Scenari di esempio
Di seguito sono riportati alcuni scenari comuni:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da app dannose:
Quando vengono rilevate app dannose, ad esempio malware sul dispositivo, è possibile impedire ai dispositivi di:
* Connettersi alla posta elettronica aziendale prima di aver risolto la minaccia.
* Sincronizzare file aziendali tramite l'app OneDrive per il lavoro.
* Accedere ad app critiche per l'azienda.

**Accesso bloccato quando vengono rilevate app dannose:**

![diagramma che illustra i criteri di accesso condizionale che bloccano l'accesso quando il dispositivo viene indicato come non conforme a causa della presenza di app dannose su di esso](media/config-mgr-maliciousapps_blocked.png)

**Dispositivo sbloccato e in grado di accedere alle risorse aziendali dopo che la minaccia è stata corretta:**

![diagramma che illustra i criteri di accesso condizionale che concedono l'accesso quando il dispositivo viene indicato come conforme dopo la correzione](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete:
Rilevare le minacce alla rete, ad esempio attacchi di tipo man-in-the-middle, e limitare l'accesso alle reti Wi-Fi in base al rischio per il dispositivo.

**Accesso bloccato alla rete Wi-Fi:**

![diagramma che illustra i criteri di accesso condizionale che bloccano l'accesso alla rete Wi-Fi in base alle minacce per la rete](media/config-mgr-network-wifi-blocked.png)

**Accesso concesso dopo la correzione:**

![diagramma che illustra l'accesso condizionale che consente l'accesso dopo la correzione della minaccia](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete:

Rilevare le minacce alla rete, ad esempio attacchi di tipo man-in-the-middle, e impedire la sincronizzazione dei file aziendali in base al rischio per il dispositivo.

**Accesso bloccato a SharePoint Online in base alla minaccia per la rete rilevata sul dispositivo:**

![Diagramma che illustra l'accesso condizionale che blocca l'accesso del dispositivo a SharePoint Online in base al rilevamento della minaccia](media/config-mgr-network-spo-blocked.png)


**Accesso concesso dopo la correzione:**

![Diagramma che illustra l'accesso condizionale che consente l'accesso dopo la correzione della minaccia per la rete](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Passaggi successivi
Ecco i passaggi principali da seguire per implementare questa soluzione:
1.  [Configurare la sottoscrizione con la protezione dalle minacce mobili Lookout](set-up-your-subscription-with-lookout.md)
2.  [Abilitare la connessione MTP di Lookout in Intune](enable-lookout-connection-in-intune.md)
3.  [Configurare e distribuire l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4.  [Configurare i criteri di conformità](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Risoluzione dei problemi di integrazione di Lookout](troubleshoot-lookout-integration.md)
