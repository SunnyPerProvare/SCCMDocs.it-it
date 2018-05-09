---
title: 'Registrare i dispositivi '
titleSuffix: Configuration Manager
description: Informazioni sui metodi per registrare i dispositivi per la gestione di dispositivi mobili locale in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3254fdad766260e3e162378894526e9b4a7249
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Registrare i dispositivi per la gestione di dispositivi mobili locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per gestire i computer e i dispositivi con la gestione di dispositivi mobili locale di System Center Configuration Manager, è necessario registrare i dispositivi in modo che Configuration Manager possa comunicare con i dispositivi ed eseguire le attività di gestione. Configuration Manager offre due metodi per la registrazione dei dispositivi:  

-   **Registrazione utente** : in questo metodo gli utenti avviano il processo di registrazione nei propri dispositivi. Per la corretta esecuzione della registrazione utente è necessario che nel dispositivo sia installato un certificato radice trusted e che sia stato effettuato il provisioning dell'utente per la registrazione da Configuration Manager.  Per registrare un dispositivo, l'utente fornisce semplicemente le credenziali di lavoro e il dispositivo viene registrato per la gestione.  

     Per altre informazioni, vedere [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md) (Come eseguire la registrazione utente dei dispositivi con la gestione di dispositivi mobili locale in System Center Configuration Manager)  

-   **Registrazione in blocco** : in questo metodo l'utente del dispositivo non deve avviare la registrazione. Viene invece creato un pacchetto di registrazione in blocco in Configuration Manager che viene immesso nel dispositivo e aperto. All'apertura il pacchetto fornisce le informazioni necessarie per registrare il dispositivo.  

     Per altre informazioni, vedere [How to bulk-enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md) (Come eseguire la registrazione in blocco dei dispositivi con la gestione di dispositivi mobili locale in System Center Configuration Manager)  

 > [!NOTE]  
>  Il Current Branch di Configuration Manager supporta la registrazione nella gestione dispositivi mobili locale per i dispositivi che eseguono i sistemi operativi seguenti:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   
