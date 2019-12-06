---
title: Configurare l'inventario hardware
titleSuffix: Configuration Manager
description: Configurare l'inventario hardware per tutti i client o per una raccolta in System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fecaa5a9fb74c9f8d473cc9dba6a307800fd70f9
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "65499944"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Come configurare l'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa procedura consente di configurare le impostazioni client predefinite per l'inventario hardware e applicarle a tutti i client nella gerarchia. Per applicare queste impostazioni solo ad alcuni client, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i dispositivi per cui si vuole usare l'inventario hardware. Vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se un dispositivo client riceve impostazioni di inventario hardware da più set di impostazioni client, le classi di inventario hardware di ogni set di impostazioni verranno unite quando il client eseguirà report di inventario hardware. Se inoltre non si seleziona una classe in un'impostazione client personalizzata con priorità più alta, non viene disabilitato l'inventario di tale classe da parte del client. 

Per disabilitare una classe di inventario hardware specifica nella maggior parte dei sistemi, ad eccezione di alcuni, la classe deve essere deselezionata nelle impostazioni client predefinite. Creare quindi un'impostazione client personalizzata per abilitare la classe e distribuirla nei sistemi di destinazione.


### <a name="to-configure-hardware-inventory"></a>Per configurare l'inventario hardware  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario hardware**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare le impostazioni seguenti:  

    -   **Abilitare inventario hardware nei client**: selezionare **Sì**.  

    -   **Pianificazione inventario hardware**: fare clic su **Pianifica** per specificare l'intervallo di raccolta dell'inventario hardware da parte dei client.  

7.  Configurare altre [impostazioni client di inventario hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) necessarie.  

I dispositivi client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [Come gestire i client in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
