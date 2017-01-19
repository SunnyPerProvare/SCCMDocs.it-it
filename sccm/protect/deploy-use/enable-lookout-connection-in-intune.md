---
title: Abilitare Lookout MTP in Intune | System Center Configuration Manager
description: Abilitare Lookout Mobile Threat Protection nella console di amministrazione di Intune.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9536efdd-0f29-47a8-8283-0edea7714319
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: a06f0b3a0080a06a0ccbfa7f3802c575aee2c9b7


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Abilitare Lookout MTP nella console di amministrazione di Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento viene illustrato come abilitare la connessione Lookout MTP in Intune. Prima di procedere con questo passaggio è necessario aver configurato Intune Connector nella console di Lookout.  Se ciò non è ancora stato fatto, eseguire i passaggi descritti in [Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md) (Configurare la sottoscrizione con Lookout Mobile Threat Protection).

Per abilitare la connessione Lookout MTP in Intune, nella pagina **Amministrazione** della [console di amministrazione di Microsoft Intune](https://manage.microsoft.com) scegliere **Third Party Service Integration** (Integrazione servizi di terze parti). Scegliere **Stato di Lookout** e abilitare **Sincronizzazione con MTP** usando l'interruttore.

![schermata della pagina di sincronizzazione di Lookout con l'interruttore evidenziato](../media/lookout-intune-synchronization.png)

In questo modo viene completata l'integrazione di Lookout e Intune nella console di amministrazione di Intune.  I passaggi successivi dell'implementazione della soluzione includono la distribuzione delle [app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) e la configurazione dei criteri di [conformità](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> È **necessario** configurare l'app Lookout for Work prima di creare le regole dei criteri di conformità e di configurare l'accesso condizionale. Ciò garantisce che l'applicazione sia pronta e disponibile per l'installazione da parte degli utenti finali prima che questi ultimi possano accedere alla posta elettronica o ad altre risorse aziendali.

## <a name="next-steps"></a>Passaggi successivi
[Configurare l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)



<!--HONumber=Dec16_HO3-->


