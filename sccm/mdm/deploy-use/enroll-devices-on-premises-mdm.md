---
title: 'Registrare i dispositivi '
titleSuffix: Configuration Manager
description: Informazioni sui metodi per registrare i dispositivi per la gestione dei dispositivi mobili locale in Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18dd4566e37f691b6450b105234fc17cbc10ea3d
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826935"
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-configuration-manager"></a>Registrare i dispositivi per la gestione dei dispositivi mobili locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per gestire computer e dispositivi con Configuration Manager gestione di dispositivi mobili locale, è necessario registrare i dispositivi in modo che Configuration Manager possano comunicare con i dispositivi per le attività di gestione. Configuration Manager offre due metodi per la registrazione dei dispositivi:  

- **Registrazione utente** : in questo metodo gli utenti avviano il processo di registrazione nei propri dispositivi. Per la corretta esecuzione della registrazione utente è necessario che nel dispositivo sia installato un certificato radice trusted e che sia stato effettuato il provisioning dell'utente per la registrazione da Configuration Manager.  Per registrare un dispositivo, l'utente fornisce semplicemente le credenziali di lavoro e il dispositivo viene registrato per la gestione.  

   Per altre informazioni, vedere [come gli utenti registrano i dispositivi con la gestione dei dispositivi mobili locale](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

- **Registrazione in blocco** : in questo metodo l'utente del dispositivo non deve avviare la registrazione. Viene invece creato un pacchetto di registrazione in blocco in Configuration Manager che viene immesso nel dispositivo e aperto. All'apertura il pacchetto fornisce le informazioni necessarie per registrare il dispositivo.  

   Per altre informazioni, vedere [come registrare in blocco i dispositivi con la gestione dei dispositivi mobili locale](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

  > [!NOTE]
  >  Il Current Branch di Configuration Manager supporta la registrazione nella gestione dispositivi mobili locale per i dispositivi che eseguono i sistemi operativi seguenti:  
  > 
  > - Windows 10 Enterprise  
  >   -   Windows 10 Pro  
  >   -   Windows 10 Team 
  >   -   Windows 10 Mobile  
  >   -   Windows 10 Mobile Enterprise   
