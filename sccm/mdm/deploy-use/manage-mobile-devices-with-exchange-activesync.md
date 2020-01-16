---
title: Gestione di dispositivi con Exchange
titleSuffix: Configuration Manager
description: Gestire i dispositivi mobili con il connettore Exchange Server in Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 426bf16d984f364020362680e3eb7539c7f80ef3
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035262"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Gestione dei dispositivi con Exchange e Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Se si dispone di dispositivi mobili che si connettono a Exchange Server tramite il protocollo ActiveSync, è possibile utilizzare il connettore Exchange Server in Configuration Manager per gestire tali dispositivi. Il connettore funziona sia con Exchange Server locale che con Exchange Online. Utilizzare la console di Configuration Manager per configurare le funzionalità di gestione dei dispositivi mobili di Exchange. Ad esempio, la cancellazione remota del dispositivo e il controllo delle impostazioni per più server Exchange.

![Diagramma logico del connettore Exchange Server con Configuration Manager](media/configmgr-with-exchange.png)  

Quando si gestiscono i dispositivi mobili con questo connettore, non installa il client Configuration Manager o registra i dispositivi tramite MDM. Le funzioni di gestione di Exchange Server sono limitate rispetto a quelle di altre opzioni. Ad esempio, non è possibile installare il software o usare gli elementi di configurazione per configurare questi dispositivi. Per ulteriori informazioni, vedere [scegliere una soluzione di gestione dei dispositivi per Configuration Manager](/configmgr/core/plan-design/choose-a-device-management-solution).  

## <a name="policies"></a>Criteri

Quando si usa il connettore, Configuration Manager configura le impostazioni nei dispositivi mobili. I dispositivi non usano i criteri cassetta postale di Exchange ActiveSync predefiniti. Definire le impostazioni che si desidera utilizzare nei gruppi seguenti:

- **Generalee**
- **Password**
- **Gestione della posta elettronica**
- **Security**
- **Applicazione**

Ad esempio, nel gruppo **password** è possibile configurare le impostazioni seguenti:

- Se i dispositivi mobili richiedono una password
- Lunghezza minima della password
- Complessità password
- Indica se il ripristino della password è consentito

Quando si configura almeno un'impostazione nel gruppo, Configuration Manager gestisce tutte le impostazioni nel gruppo per i dispositivi mobili. Se non si configura alcuna impostazione in un gruppo, Exchange continua a gestire tali impostazioni per i dispositivi mobili. Tutti i criteri cassetta postale di Exchange ActiveSync configurati in Exchange Server e assegnati agli utenti vengono comunque applicati.

## <a name="access-rules-and-remote-actions"></a>Regole di accesso e azioni remote

È inoltre possibile configurare il connettore Exchange Server per gestire le regole di accesso a Exchange. Queste regole di accesso includono i dispositivi mobili Consenti, blocca o quarantena. È possibile cancellare i dispositivi mobili da remoto utilizzando la console di Configuration Manager e gli utenti possono cancellare i dispositivi mobili da remoto utilizzando il Catalogo applicazioni.

Il dispositivo mobile di un utente viene visualizzato automaticamente nel Catalogo applicazioni quando lo si gestisce e il server Exchange è in locale. Affinché il dispositivo mobile venga visualizzato nel Catalogo applicazioni quando si usa Exchange Online, configurare manualmente l'affinità utente dispositivo. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](/configmgr/apps/deploy-use/link-users-and-devices-with-user-device-affinity).

> [!TIP]  
> Quando un dispositivo mobile viene trasferito a un altro utente, prima che il nuovo proprietario configuri l'account di Exchange nel dispositivo, eliminare il dispositivo mobile dalla console di Configuration Manager.

## <a name="prerequisites"></a>Prerequisiti

> [!IMPORTANT]  
> Prima di installare questo connettore, confermare che Configuration Manager supporta la versione di Exchange in uso. Per ulteriori informazioni, vedere [configurazioni supportate-connettore Exchange Server](/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Autorizzazioni per configurare il connettore

Per configurare il connettore Exchange Server in Configuration Manager, è necessario disporre delle autorizzazioni di sicurezza seguenti:

- Per aggiungere, modificare ed eliminare il connettore Exchange Server: autorizzazione di **Modifica** per l'oggetto **Sito** .  

- Per configurare le impostazioni del dispositivo mobile: autorizzazione **ModifyConnectorPolicy** per l'oggetto **Sito** .  

Il ruolo predefinito **amministratore completo** , ad esempio, include le autorizzazioni necessarie.  

### <a name="permissions-to-manage-mobile-devices"></a>Autorizzazioni per la gestione dei dispositivi mobili

Per gestire i dispositivi mobili sono necessarie le autorizzazioni di sicurezza seguenti:  

- Per cancellare un dispositivo mobile: **Elimina risorsa** per l'oggetto **Raccolta** .  

- Per annullare un comando di cancellazione: **Modifica risorsa** per l'oggetto **Raccolta** .  

- Per consentire e bloccare i dispositivi mobili: **Modifica risorsa** per l'oggetto **Collection** .  

Il ruolo predefinito **amministratore operazioni** , ad esempio, include le autorizzazioni necessarie.

Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](/configmgr/core/servers/deploy/configure/configure-role-based-administration).

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Installare e configurare Exchange Connector](/configmgr/mdm/deploy-use/install-configure-exchange-connector)
