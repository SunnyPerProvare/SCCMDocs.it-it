---
title: Configurare l'inventario software
titleSuffix: Configuration Manager
description: Configurare l'inventario software ed escludere cartelle dall'inventario software in Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 346ff3254f4c1833f49bf256cbf5ad0c489d77e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332580"
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Come configurare l'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa procedura consente di configurare le impostazioni client predefinite per l'inventario software e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta. Per altre informazioni su come creare impostazioni dispositivo personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).   

## <a name="to-configure-software-inventory"></a>Per configurare l'inventario software  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni predefinite** scegliere **Inventario software**.  

6.  Nell'elenco **Impostazioni dispositivo** configurare i valori seguenti:  

    -   **Abilitare inventario software nei client**: selezionare **Vero** dall'elenco a discesa.  

    -   **Pianificare inventario software e raccolta file**: consente di configurare l'intervallo di raccolta di file e inventario software da parte dei client.   

7.  Configurare le impostazioni client necessarie. La sezione [Inventario software](../../../../core/clients/deploy/about-client-settings.md#software-inventory) nell'argomento [Informazioni sulle impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) contiene un elenco delle impostazioni client.  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [Come gestire i client in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 > [!TIP]  
        >   Il codice di errore 80041006 in inventoryprovider.log significa che il provider WMI ha esaurito la memoria. Ciò significa che è stato raggiunto il limite di quota di memoria per un provider e il provider di inventario non può continuare.
In questo caso, l'agente di inventario crea un report con 0 voci in modo che non venga segnalato alcun articolo di inventario. <br/>
Una possibile soluzione per questo errore è ridurre l'ambito della raccolta inventario software. Nelle circostanze in cui l'errore si verifica dopo la limitazione dell'ambito di inventario, una soluzione può essere aumentare la proprietà [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) definita nella classe[_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671).

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Per escludere cartelle dall'inventario software  

1.  Usando Notepad.exe, creare un file vuoto denominato **Skpswi.dat**.  

2.  Fare clic con il pulsante destro del mouse sul file **Skpswi.dat** e quindi scegliere **Proprietà**. Nelle proprietà per il file Skpswi.dat selezionare l'attributo **Hidden** .  

3.  Inserire il file **Skpswi.dat** nella radice di ogni disco rigido o struttura di cartelle del client che si vuole escludere dall'inventario software.  

> [!NOTE]  
>  L'inventario software non effettua l'inventario dell'unità del client a meno che questo file non venga eliminato dall'unità nel computer client.