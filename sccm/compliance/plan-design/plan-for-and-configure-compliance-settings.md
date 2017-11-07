---
title: "Pianificare e configurare le impostazioni di conformità"
titleSuffix: Configuration Manager
description: "Informazioni sui prerequisiti e sulle attività di configurazione per l'uso delle impostazioni di conformità in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 970ebabc8a275f46cf005c6f3571c62d64889ea8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Pianificare e configurare le impostazioni di conformità in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di usare le impostazioni di conformità di System Center Configuration Manager, è necessario conoscere alcuni prerequisiti ed eseguire alcune attività di configurazione.  

## <a name="prerequisites-for-compliance-settings"></a>Prerequisiti per le impostazioni di conformità  

|Prerequisito|Altre informazioni|  
|------------------|----------------------|  
|I client Windows di Configuration Manager devono essere abilitati e configurati per la valutazione della conformità.|Vedere di seguito|  
|Se si vogliono eseguire report, è necessario configurare la creazione di report per il sito.|[Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Autorizzazioni di sicurezza obbligatorie.|Il ruolo di sicurezza **Gestione impostazioni di conformità** include le autorizzazioni necessarie per gestire le impostazioni di conformità, gli elementi di configurazione di profili e dati utente e i profili di connessione remota.<br /><br /> [Configurare un'amministrazione basata su ruoli](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Abilitare e configurare le impostazioni di conformità (solo per PC Windows)  

Questa procedura consente di configurare le impostazioni client predefinite per le impostazioni di conformità e applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer per cui si vogliono usare le impostazioni di conformità. Per altre informazioni su come creare le impostazioni personalizzate del dispositivo, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Altri tipi di dispositivo non richiedono una configurazione specifica per valutare le impostazioni di conformità.  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Impostazioni client** > **Impostazioni predefinite**.  
2.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
3.  Nella finestra di dialogo **Impostazioni predefinite** fare clic su **Impostazioni di conformità**.  
4.  Configurare le impostazioni client seguenti per le impostazioni di conformità:
    - **Abilitare valutazione di conformità nei client**: impostare a **True** se si vuole valutare la conformità nei dispositivi client.
    - **Pianificare valutazione di conformità**: fare clic su **Pianifica** se si vuole modificare la pianificazione di valutazione di conformità predefinita nei dispositivi client.
    - **Abilitare profili e dati utente**: abilitare questa opzione se si vuole creare e distribuire elementi di configurazione di profili e dati utente in computer Windows. Per informazioni dettagliate, vedere [Creare elementi di configurazione dei profili e di dati utente](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni dispositivo** .  

I computer client vengono configurati con queste impostazioni al successivo download dei criteri client.  
