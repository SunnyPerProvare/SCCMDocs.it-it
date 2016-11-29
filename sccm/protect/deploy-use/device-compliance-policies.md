---
title: "Criteri di conformità del dispositivo | System Center Configuration Manager"
description: "Informazioni su come gestire i criteri di conformità in System Center Configuration Manager per rendere i dispositivi conformi ai criteri di accesso condizionale."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 353ec99a-9982-4dab-ae21-d7fb595b3c50
caps.latest.revision: 22
author: karthikaraman
ms.author: karaman
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: d461f95f875632860238d503d7acd7ab8c320d58

---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Criteri di conformità del dispositivo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I **criteri di conformità** in System Center Configuration Manager definiscono le regole e le impostazioni che un dispositivo deve soddisfare per essere considerato conforme ai criteri di accesso condizionale. È anche possibile usare tali criteri per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale.  


> [!IMPORTANT]  
>  Questo articolo descrive i criteri di conformità per i dispositivi gestiti da Microsoft Intune.    I criteri di conformità per i PC gestiti da System Center Configuration Manager sono descritti in [Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

 Queste regole includono requisiti come:  

-   PIN e password per accedere a un dispositivo

-   Crittografia dei dati memorizzati sul dispositivo

-   Se il dispositivo è jailbroken o rooted  

-   Se la posta elettronica nel dispositivo viene gestita da un criterio Intune o se il dispositivo è segnalato come non integro dal servizio di attestazione dell'integrità del dispositivo Windows.  


 I criteri di conformità vengono distribuiti alle raccolte dell'utente. Quando un criterio di conformità viene distribuito a un utente, la conformità viene controllata su tutti i dispositivi dell’utente.  

 Nella tabella seguente sono elencati i tipi di dispositivi supportati dai criteri di conformità e il modo in cui le impostazioni di non conformità vengono gestite quando i criteri vengono usati con i criteri di accesso condizionale.  

|Regola|Windows 8.1 e versioni successive|Windows Phone 8.1 e versioni successive|iOS 6.0 e versioni successive|Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configurazione di PIN o password**|Corretto|Corretto|Corretto|In quarantena|  
|**Crittografia dispositivo**|N/D|Corretto|Corretto (impostando il PIN)|In quarantena|  
|**Dispositivo jailbroken o rooted**|N/D|N/D|In quarantena (non è un'impostazione)|In quarantena (non è un'impostazione)|  
|**Profilo di posta elettronica**|N/D|N/D|In quarantena|N/D|  
|**Versione minima del sistema operativo**|In quarantena|In quarantena|In quarantena|In quarantena|  
|**Versione massima del sistema operativo**|In quarantena|In quarantena|In quarantena|In quarantena|  
|**Attestazione dell'integrità dei dispositivi (aggiornamento 1602)**|Impostazione non applicabile a Windows 8.1<br /><br /> Windows 10 e Windows 10 Mobile vengono messi in quarantena.|N/D|N/D|N/D|  

 **Corretto** = la conformità viene forzata dal sistema operativo del dispositivo (ad esempio, l'utente è obbligato a impostare un PIN).  Non riguarda casi in cui l'impostazione non è conforme.  

 **In quarantena** = il sistema operativo del dispositivo non forza la conformità (ad esempio, i dispositivi Android non impongono la crittografia del dispositivo all'utente).  In questo caso:  

-   Il dispositivo viene bloccato se l'utente è la destinazione di un criterio di accesso condizionale.  

-   Il portale aziendale o il portale web informano l'utente di eventuali problemi di conformità.  


### <a name="next-steps"></a>Passaggi successivi  
[Create and deploy a device compliance policy](create-compliance-policy.md) (Creare e distribuire criteri di conformità del dispositivo)
### <a name="see-also"></a>Vedere anche  
 [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)



<!--HONumber=Nov16_HO1-->

