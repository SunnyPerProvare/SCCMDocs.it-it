---
title: Escludere le cartelle dall'inventario software | System Center Configuration Manager
description: Escludere le cartelle dall'inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 07328e086a09e924a4807b05759937929152bda9


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Come escludere cartelle dall'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Seguire questa procedura per configurare l'inventario software di System Center Configuration Manage per il sito.  

 Questa procedura consente di configurare le impostazioni client predefinite per l'inventario software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer in cui si vuole usare l'inventario software. Per altre informazioni su come creare impostazioni dispositivo personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

### <a name="to-configure-software-inventory"></a>Per configurare l'inventario software  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3.  Fare clic su **Impostazioni client predefinite**.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** fare clic su **Inventario software**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare i valori seguenti:  

    -   **Abilitare inventario software nei client**: selezionare **Vero** dall'elenco a discesa.  

    -   **Pianificare inventario software e raccolta file**: consente di configurare l'intervallo di raccolta di file e inventario software da parte dei client. Usare il valore predefinito di **7 giorni** oppure fare clic su **Pianifica** per configurare un intervallo personalizzato.  

7.  Configurare le impostazioni client necessarie. Per un elenco delle impostazioni client dell'inventario software che è possibile configurare, vedere la sezione [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#BKMK_SoftInventoryDeviceSettings) (Inventario software) nell'argomento [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Configura impostazione client** .  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


