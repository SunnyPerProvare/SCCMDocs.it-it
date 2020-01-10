---
title: 'Modalità di registrazione dei dispositivi nella gestione di dispositivi mobili locale '
titleSuffix: Configuration Manager
description: Informazioni su come gli utenti registrano i dispositivi con la gestione dei dispositivi mobili locale in Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6821a439e7ee054216a7ca73be027978ed659ae1
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826493"
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-configuration-manager"></a>Come gli utenti registrano i dispositivi con la gestione dei dispositivi mobili locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager gestione dei dispositivi mobili locale, gli utenti possono registrare i dispositivi se hanno ottenuto l'autorizzazione di registrazione (con le impostazioni client aggiornate) e i relativi dispositivi hanno il certificato radice richiesto installato per l'attendibilità comunicazioni con i server che ospitano i ruoli del sistema del sito richiesti. Per altre informazioni su come configurare la registrazione, vedere [configurare la registrazione dei dispositivi per la gestione dei dispositivi mobili locale](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  Il Current Branch di Configuration Manager supporta la registrazione nella gestione dispositivi mobili locale per i dispositivi che eseguono i sistemi operativi seguenti:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partire da Configuration Manager versione 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

Le attività seguenti illustrano come registrare e verificare la registrazione di computer e dispositivi per la gestione dei dispositivi mobili locale:  

-   [Registrare un computer Windows 10](#bkmk_enrollDesk)  

-   [Registrare un dispositivo Windows 10 Mobile](#bkmk_enrollMob)  

-   [Verificare la registrazione del dispositivo](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Registrare un computer Windows 10  

1.  In un computer Windows 10, passare a **Impostazioni**.  

2.  Fare clic su **Account**, quindi fare clic su **Accesso società**.  

3.  In **Connetti all'azienda o all'istituto di istruzione**di Accesso società fare clic su **Connetti**, immettere l'indirizzo di posta elettronica dell'ufficio e fare clic su **Continua**.  

4.  Immettere il nome FQDN del server che ospita il ruolo del sistema del sito punto proxy di registrazione e fare clic su **Continua**.  

5.  In Connessione a un servizio immettere la password di posta elettronica dell'ufficio e fare clic su **Accedi**.  

6.  Fare clic su **Ignora** per ricordare le informazioni di accesso; dopo un breve periodo di tempo il dispositivo è connesso.  

##  <a name="bkmk_enrollMob"></a> Registrare un dispositivo Windows 10 Mobile  

1.  In un dispositivo Windows 10 Mobile, passare a **Impostazioni**.  

2.  Fare clic su **Account**, quindi fare clic su **Accesso società**.  

3.  Fare clic su **Connetti**.  

4.  Immettere l'indirizzo di posta elettronica dell'ufficio e il nome FQDN del server che ospita il ruolo del sistema del sito del punto proxy di registrazione. Fare clic su **Connetti**.  

5.  Nella schermata successiva immettere la password e l'indirizzo di posta elettronica dell'ufficio e quindi fare clic su **Accedi**. Dopo un breve periodo di tempo il dispositivo è registrato. Fare clic su **Fine**.  

##  <a name="bkmk_verify"></a> Verificare la registrazione del dispositivo  
 È possibile verificare se i dispositivi sono stati registrati correttamente nella console di Configuration Manager.  

1.  Avviare la console di Configuration Manager.  

2.  Fare clic su **Asset e conformità** > **Panoramica** > **Dispositivi**. Il dispositivo registrato viene visualizzato nell'elenco.  
