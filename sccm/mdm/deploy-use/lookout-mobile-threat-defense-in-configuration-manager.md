---
title: Limitare l'accesso in base ai rischi
titleSuffix: Configuration Manager
description: Limitare l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50d79da3ab4e7ace9a682baaa5cfd8d2bdbdce10
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678881"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

Controllare l'accesso dai dispositivi mobili alle risorse aziendali in base alla valutazione dei rischi eseguita da Lookout. Lookout è un soluzione di protezione dalle minacce per il dispositivo integrata con Microsoft Intune. Il rischio si basa sui dati raccolti dal servizio Lookout. Raccoglie dai dispositivi i dati relativi a vulnerabilità del sistema operativo, app dannose installate e profili di rete dannosa. 

In base alla valutazione dei rischi segnalati da Lookout abilitata tramite i criteri di conformità di Configuration Manager, si configurano i criteri di accesso condizionale. Questi criteri consentono o bloccano i dispositivi rilevati come non conformi da Configuration Manager a causa delle minacce rilevate in tali dispositivi.

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>Funzionamento

In che modo la distribuzione MDM ibrida e la protezione dalle minacce per i dispositivi di Lookout aiutano a proteggere le risorse aziendali?

L'app per dispositivi mobili di Lookout (Lookout for Work) viene eseguita nei dispositivi mobili. Acquisisce i dati di utilizzo di file system, stack di rete, dispositivi e applicazioni, se disponibili. L'app invia questi dati al servizio cloud di protezione dalle minacce per il dispositivo di Lookout per calcolare un rischio complessivo per il dispositivo in relazione alle minacce per i dispositivi mobili. Usare la console di Lookout per modificare la classificazione del livello di rischio per le minacce in base alle proprie esigenze.  

I criteri di conformità in Configuration Manager includono ora una nuova regola per la protezione dalle minacce per i dispositivi mobili di Lookout basata sulla valutazione del rischio delle minacce per i dispositivi di Lookout. Quando si abilita questa regola, Configuration Manager valuta la conformità del dispositivo.

Se il dispositivo non è conforme ai criteri di conformità, è possibile bloccare l'accesso a risorse come Exchange Online e SharePoint Online tramite criteri di accesso condizionale. Quando viene bloccato l'accesso, l'utente finale riceve una procedura dettagliata per risolvere il problema e ottenere l'accesso alle risorse aziendali. L'utente avvia questa procedura dettagliata tramite l'app Lookout for work.



## <a name="supported-platforms"></a>Piattaforme supportate

- **Android 4.1 e versioni successive** e registrate in Microsoft Intune.  

- **iOS 8 e versioni successive** e registrate in Microsoft Intune.  


Per informazioni sulle piattaforme e i linguaggi supportati da Lookout, vedere questo [articolo del supporto tecnico di Lookout](https://personal.support.lookout.com/hc/articles/114094140253).



## <a name="prerequisites"></a>Prerequisiti

- [Gestione dei dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Una sottoscrizione a Microsoft Intune e Azure Active Directory.  

- Una sottoscrizione aziendale a Lookout Mobile EndPoint Security. Per altre informazioni, vedere [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## <a name="example-scenarios"></a>Scenari di esempio


### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controllare l'accesso in base alle minacce da app dannose

Quando vengono rilevate app dannose, ad esempio malware sul dispositivo, è possibile impedire ai dispositivi di:

- Connettersi alla posta elettronica aziendale prima di aver risolto la minaccia  

- Sincronizzare file aziendali tramite l'app OneDrive per il lavoro  

- Accedere ad app critiche per l'azienda  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>Accesso bloccato quando vengono rilevate app dannose

![Criteri di accesso condizionale che bloccano l'accesso quando vengono rilevate app dannose](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>Dispositivo sbloccato e in grado di accedere alle risorse aziendali dopo che la minaccia è stata corretta

![Criteri di accesso condizionale che concedono l'accesso quando il dispositivo è conforme](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Controllare l'accesso in base alle minacce per la rete

Rilevare le minacce alla rete, ad esempio attacchi di tipo man-in-the-middle, e limitare l'accesso alle reti Wi-Fi in base al rischio per il dispositivo.

#### <a name="access-to-network-through-wifi-blocked"></a>Accesso bloccato alla rete Wi-Fi

![Criteri di accesso condizionale che bloccano l'accesso alla rete Wi-Fi in base alle minacce per la rete](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>Accesso concesso dopo la correzione

![Accesso condizionale che consente l'accesso dopo la correzione della minaccia](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controllare l'accesso a SharePoint Online in base alle minacce alla rete

Rilevare le minacce alla rete, ad esempio attacchi di tipo man-in-the-middle, e impedire la sincronizzazione dei file aziendali in base al rischio per il dispositivo.

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>Accesso bloccato a SharePoint Online in base alla minaccia per la rete rilevata sul dispositivo

![Accesso condizionale che blocca l'accesso del dispositivo a SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>Accesso concesso dopo la correzione

![Accesso condizionale che consente l'accesso dopo la correzione della minaccia](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>Passaggi successivi

Per implementare questa soluzione, seguire questa procedura:  

1. [Configurare la sottoscrizione con la protezione dalle minacce mobili Lookout](set-up-your-subscription-with-lookout.md)
2. [Abilitare la connessione MTP di Lookout in Intune](enable-lookout-connection-in-intune.md)
3.  [Configurare e distribuire l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4. [Configurare i criteri di conformità](enable-device-threat-protection-rule-compliance-policy.md)
5. [Risoluzione dei problemi di integrazione di Lookout](troubleshoot-lookout-integration.md)
