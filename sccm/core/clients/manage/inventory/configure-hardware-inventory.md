---
title: Configurare l'inventario hardware | System Center Configuration Manager
description: Configurare l'inventario hardware per tutti i client o per una raccolta in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 41bf42228e41785a05359c08e8dfedae48d50e30


---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per configurare l'inventario hardware di System Center Configuration Manager per il sito, eseguire i passaggi seguenti.  

 Questa procedura consente di configurare le impostazioni client predefinite per l'inventario hardware e applicarle a tutti i client nella gerarchia. Per applicare queste impostazioni solo ad alcuni client, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i dispositivi per cui si vuole usare l'inventario hardware. Per altre informazioni su come creare impostazioni di dispositivo personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se un dispositivo client riceve impostazioni di inventario hardware da più set di impostazioni client, le classi di inventario hardware di ogni set di impostazioni verranno unite quando il client eseguirà report di inventario hardware.  

### <a name="to-configure-hardware-inventory"></a>Per configurare l'inventario hardware  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3.  Fare clic su **Impostazioni client predefinite**.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** fare clic su **Inventario hardware**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare le impostazioni seguenti:  

    -   **Abilitare inventario hardware nei client** : selezionare **Vero**nell'elenco a discesa.  

    -   **Pianificazione inventario hardware**: specificare l'intervallo di raccolta dell'inventario hardware da parte dei client. Usare il valore predefinito di **7 giorni** oppure fare clic su **Pianifica** per configurare un intervallo personalizzato.  

7.  Configurare eventuali altre impostazioni client necessarie. Per un elenco di impostazioni client relative all'inventario hardware che è possibile configurare, vedere la sezione [Inventario hardware](../../../../core/clients/deploy/about-client-settings.md#BKMK_HardwareInventoryDeviceSettings) dell'argomento [Informazioni sulle impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni dispositivo** .  

 I dispositivi client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


