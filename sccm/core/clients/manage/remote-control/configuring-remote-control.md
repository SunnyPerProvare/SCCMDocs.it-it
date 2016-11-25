---
title: Configurare il controllo remoto | System Center Configuration Manager
description: Configurare il controllo remoto in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aea35afe970e20bc2b22f9ae3f413a3c735caae1


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurazione del controllo remoto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di usare il controllo remoto in System Center Configuration Manager, è necessario eseguire i passaggi di configurazione seguenti.  

## <a name="how-to-enable-remote-control-and-configure-client-settings"></a>Come abilitare il controllo remoto e configurare le impostazioni client  
 Questa procedura descrive la configurazione delle impostazioni client predefinite per il controllo remoto e si applica a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer che si vogliono usare in una sessione di controllo remoto. Per altre informazioni su come creare impostazioni di dispositivo personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Per abilitare il controllo remoto e configurare le impostazioni client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3.  Fare clic su **Impostazioni client predefinite**.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Predefinito**  fare clic su **Strumenti remoti**.  

6.  Configurare le impostazioni client necessarie per il controllo remoto, Assistenza remota e Desktop remoto. Per un elenco di impostazioni client di strumenti remoti che è possibile configurare, vedere la sezione [Strumenti remoti](../../../../core/clients/deploy/about-client-settings.md#BKMK_RemoteToolsDeviceSettings) nell'argomento [Informazioni sulle impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  È possibile modificare il nome della società visualizzato nella finestra di dialogo **Controllo remoto di Configuration Manager** configurando un valore per **Nome organizzazione visualizzato in Software Center** nelle impostazioni client **Agente computer** .  

    > [!IMPORTANT]  
    >  Per usare Assistenza remota o Desktop remoto è necessario installare e configurare questi programmi nel computer che esegue la console di Configuration Manager. Per altre informazioni su come installare e configurare Assistenza remota o Desktop remoto, vedere la documentazione di Windows.  

7.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni dispositivo** .  

 I computer client vengono configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  



<!--HONumber=Nov16_HO1-->


