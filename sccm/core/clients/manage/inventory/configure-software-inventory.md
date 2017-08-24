---
title: Configurare l'inventario software | Microsoft Docs
description: Configurare l'inventario software ed escludere cartelle dall'inventario software in Configuration Manager.
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e60cec71c425e5e42d450cbeee366528d4b42405
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Come configurare l'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 Questa procedura consente di configurare le impostazioni client predefinite per l'inventario software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer in cui si vuole usare l'inventario software. Per altre informazioni su come creare impostazioni dispositivo personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

## <a name="to-configure-software-inventory"></a>Per configurare l'inventario software  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario software**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare i valori seguenti:  

    -   **Abilitare inventario software nei client**: selezionare **Vero** dall'elenco a discesa.  

    -   **Pianificare inventario software e raccolta file**: consente di configurare l'intervallo di raccolta di file e inventario software da parte dei client.   

7.  Configurare le impostazioni client necessarie. Per un elenco delle impostazioni client dell'inventario software che è possibile configurare, vedere la sezione [Software Inventory](../../../../core/clients/deploy/about-client-settings.md#software-inventory) (Inventario software) nell'argomento [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client in System Center Configuration Manager).  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  


## <a name="to-exclude-folders-from-software-inventory"></a>Per escludere cartelle dall'inventario software  

1.  Usando Notepad.exe, creare un file vuoto denominato **Skpswi.dat**.  

2.  Fare clic con il pulsante destro del mouse sul file **Skpswi.dat** e quindi scegliere **Proprietà**. Nelle proprietà per il file Skpswi.dat selezionare l'attributo **Hidden** .  

3.  Inserire il file **Skpswi.dat** nella radice di ogni disco rigido o struttura di cartelle del client che si vuole escludere dall'inventario software.  

> [!NOTE]  
>  L'inventario software non effettua l'inventario dell'unità del client a meno che questo file non venga eliminato dall'unità nel computer client.