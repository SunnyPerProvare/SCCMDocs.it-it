---
title: Configurare l&quot;inventario hardware | Microsoft Docs
description: Configurare l&quot;inventario hardware per tutti i client o per una raccolta in System Center Configuration Manager.
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 05c27c7aa36e0b4236867766dab36125c31467b3
ms.openlocfilehash: deed112cca011b3b410c1197b7abf0f36a864f3c


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa procedura consente di configurare le impostazioni client predefinite per l'inventario hardware e applicarle a tutti i client nella gerarchia. Per applicare queste impostazioni solo ad alcuni client, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i dispositivi per cui si vuole usare l'inventario hardware. Vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se un dispositivo client riceve impostazioni di inventario hardware da più set di impostazioni client, le classi di inventario hardware di ogni set di impostazioni verranno unite quando il client eseguirà report di inventario hardware.  

### <a name="to-configure-hardware-inventory"></a>Per configurare l'inventario hardware  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario hardware**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare le impostazioni seguenti:  

    -   **Abilitare inventario hardware nei client**: selezionare **Vero**.  

    -   **Pianificazione inventario hardware**: fare clic su **Pianifica** per specificare l'intervallo di raccolta dell'inventario hardware da parte dei client.  

7.  Configurare altre [impostazioni client di inventario hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) necessarie.  

I dispositivi client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Jan17_HO1-->


