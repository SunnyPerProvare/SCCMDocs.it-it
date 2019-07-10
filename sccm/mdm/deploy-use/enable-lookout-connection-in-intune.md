---
title: Abilitare Lookout MTP in Intune
description: Abilitare Lookout Mobile Threat Defense (MTD) nel portale di Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0be485bd9b77613be9a647106e96c4e41bede064
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678135"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Abilitare la connessione Lookout MTD nella console di amministrazione di Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive come abilitare la connessione Lookout Mobile Threat Defense (MTD) in Microsoft Intune. Prima di procedere con questo passaggio è necessario aver configurato Intune Connector nella console di Lookout. Se ciò non è ancora stato fatto, eseguire i passaggi descritti in [Configurare la sottoscrizione per Lookout Mobile Threat Defense](set-up-your-subscription-with-lookout.md).



## <a name="enable-the-lookout-mtd-connector"></a>Abilitare il connettore Lookout MTD

1. Passare al [portale di Azure](https://portal.azure.com) e accedere con le credenziali di Intune. Dopo aver completato l'accesso, viene visualizzato il **dashboard di Azure**.  

2. Nel **dashboard di Azure** scegliere **Tutti i servizi** dal menu di sinistra e digitare **Intune** nel filtro della casella di testo.  

3. Scegliere **Intune**. Viene aperto il **dashboard di Intune**.  

4. Nel **dashboard di Intune** scegliere **Conformità del dispositivo** e quindi **Mobile Threat Defense** nella sezione **Installazione**.  

5. Nel riquadro **Mobile Threat Defense** scegliere **Aggiungi**.  

6. Selezionare **Lookout** come **connettore Mobile Threat Defense da configurare** dall'elenco a discesa.  

7. Abilitare le opzioni di attivazione/disattivazione in base ai requisiti dell'organizzazione.  



## <a name="mtd-toggle-options"></a>Opzioni di attivazione/disattivazione MTD

È possibile scegliere le opzioni di attivazione/disattivazione MTD da abilitare in base ai requisiti dell'organizzazione. Di seguito sono riportate informazioni dettagliate:

- **Android 4.1 + connettersi ai dispositivi di Lookout for Work MTD**: Quando si abilita questa opzione, è possibile avere Android 4.1 + segnalino i dispositivi rischi di sicurezza a Intune.  
    - **Contrassegna come non conforme se non vengono ricevuti dati**: Se Intune non riceve dati su un dispositivo in questa piattaforma da Lookout, prendere in considerazione il dispositivo non conforme.  

- **Connetti i dispositivi iOS 8.0 + a Lookout for Work MTD**: Quando si abilita questa opzione, è possibile riferire rischio per la sicurezza a Intune i dispositivi iOS 8.0 +.
    - **Contrassegna come non conforme se non vengono ricevuti dati**: Se Intune non riceve dati su un dispositivo in questa piattaforma da Lookout, prendere in considerazione il dispositivo non conforme.  

> [!TIP]  
> Lo **Stato connessione** e l'ora dell'**Ultima sincronizzazione** tra Intune e Lookout sono visibili dal riquadro Mobile Threat Defense.



## <a name="next-steps"></a>Passaggi successivi
L'integrazione di Lookout e Intune viene completata. I passaggi successivi dell'implementazione della soluzione includono la distribuzione delle [app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) e la configurazione dei criteri di [conformità](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> È *necessario* configurare l'app Lookout for Work prima di creare le regole dei criteri di conformità e di configurare l'accesso condizionale. Questa operazione garantisce che l'applicazione sia pronta e disponibile per l'installazione da parte degli utenti finali prima che questi ultimi possano accedere alla posta elettronica o ad altre risorse aziendali.

[Configurare l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
