---
title: Escludere cartelle dall&quot;inventario software | Documentazione Microsoft
description: Escludere le cartelle dall&quot;inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 12/04/2016
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
ms.sourcegitcommit: 6d1aabbde576f01de920468fd3ef372bd23be9df
ms.openlocfilehash: 7850b69cdccb0e897ee71b75255004bdc8d0ae97


---
# <a name="how-to-exclude-folders-from-software-inventory-in-system-center-configuration-manager"></a>Come escludere cartelle dall'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 Questa procedura consente di configurare le impostazioni client predefinite per l'inventario software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer in cui si vuole usare l'inventario software. Per altre informazioni su come creare impostazioni dispositivo personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

### <a name="to-configure-software-inventory"></a>Per configurare l'inventario software  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario software**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare i valori seguenti:  

    -   **Abilitare inventario software nei client**: selezionare **Vero** dall'elenco a discesa.  

    -   **Pianificare inventario software e raccolta file**: consente di configurare l'intervallo di raccolta di file e inventario software da parte dei client.   

7.  Configurare le impostazioni client necessarie. Per un elenco delle impostazioni client dell'inventario software che è possibile configurare, vedere la sezione [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#software-inventory) (Inventario software) nell'argomento [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Dec16_HO3-->


