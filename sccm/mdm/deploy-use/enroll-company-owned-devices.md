---
title: Registrare i dispositivi aziendali per le distribuzioni ibride con Configuration Manager
description: Informazioni sui vari metodi per registrare i dispositivi aziendali per le distribuzioni ibride con Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: 13
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 91f1d0d775236fe4cb6675b1017161520a281df5


---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrare i dispositivi aziendali per le distribuzioni ibride con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I dispositive aziendali possono essere gestiti in modi diversi a seconda del dispositivo e di come il dispositivo è stato acquistato.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Registrare i dispositivi IOS acquistati tramite Device Enrollment Program  
 È possibile distribuire un profilo di registrazione "over the air" ai dispositivi acquistati tramite il programma Device Enrollment Program di Apple. Quando l'utente esegue l'Assistente configurazione nel dispositivo, il dispositivo viene registrato in Intune.  La registrazione dei dispositivi registrati tramite DEP non può essere annullata dagli utenti. Vedere [iOS Device Enrollment Program (DEP) enrollment for hybrid deployments with Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).(Registrazione al programma DEP (Device Enrollment Program) per iOS per le distribuzioni ibride con Configuration Manager).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Registrare i dispositivi iOS con Apple Configurator  
 Per usare questo metodo è necessario che l'amministratore connetti tramite USB il dispositivo iOS a un computer Mac che esegue Apple Configurator per preconfigurare la registrazione. I dispositivi vengono poi consegnati agli utenti che eseguono l'Assistente configurazione, configurano il dispositivo con le proprie credenziali aziendali o dell'istituto di istruzione e completano il processo di registrazione. Vedere [iOS hybrid enrollment using Apple Configurator with Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md) (Registrazione ibrida di iOS tramite Apple Configurator con Configuration Manager).  

## <a name="device-enrollment-manager"></a>Manager di registrazione dispositivi  
 Le organizzazioni possono usare Intune per gestire un numero elevato di dispositivi mobili con un unico account utente, vale a dire un account del manager di registrazione dispositivi. Dopo aver creato un account del manager di registrazione dispositivi, è possibile usarlo da un programma di gestione per registrare più dei cinque dispositivi standard consentiti per impostazione predefinita agli utenti normali. Con il manager di registrazione dispositivi è possibile registrare solo quei dispositivi che non sono usati da un utente specifico. Questi dispositivi sono ad esempio ideali per app POS o di utilità, ma non sono consigliati agli utenti che devono poter accedere alla posta elettronica e alle risorse aziendali. Vedere [Registrare i dispositivi usando il manager di registrazione dispositivi con Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Affinità utente per dispositivi gestiti  
 Quando si configurano profili per i dispositivi di proprietà dell'azienda, l'amministratore può specificare se i dispositivi gestiti supportano un'*affinità utente* che identifica un utente specifico con il dispositivo. I dispositivi configurati con **user affinity** possono installare ed eseguire l'app Portale aziendale per scaricare le app e gestire i dispositivi. Vedere [User affinity for hybrid managed devices in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md) (Affinità utente per i dispositivi gestiti ibridi in Configuration Manager).  

## <a name="manage-devices-with-activation-lock"></a>Gestire i dispositivi con il blocco attivazione  
 Microsoft Intune consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone in un dispositivo. Vedere [Manage iOS Activation Lock with System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md) (Gestire il blocco attivazione iOS con System Center Configuration Manager).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predichiarare i dispositivi con i numeri di serie IMEI o iOS

È possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity) o i numeri di serie iOS. È possibile caricare un file con valori delimitati da virgole (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  Vedere [Predeclare devices with hardware ID numbers](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md) (Predichiarare i dispositivi con numeri ID hardware).

## <a name="see-also"></a>Vedere anche  
 [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md) (Gestione di dispositivi mobili ibridi (MDM) con System Center Configuration Manager e Microsoft Intune)



<!--HONumber=Nov16_HO1-->


