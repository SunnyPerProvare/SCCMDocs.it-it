---
title: Creare applicazioni iOS | Documentazione Microsoft
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi iOS.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5420109-6538-4430-9ca6-db352ee84c2e
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e9e34359f4412ba07b9fb49f871a1eb2d36cecf8
ms.openlocfilehash: eb2d1245932d71bd10fd63d95a155eae7d128836


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Creare applicazioni iOS con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Tenere presenti le seguenti considerazioni quando si creano e si distribuiscono applicazioni per i dispositivi iOS.  

## <a name="general-considerations"></a>Considerazioni generali  
 Configuration Manager supporta la distribuzione dei seguenti tipi di app:  

|Tipo di dispositivo|File supportati|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> In System Center Configuration Manager non è necessario specificare un file di elenco di proprietà (PLIST) quando si importa un'app iOS.|  

 Sono supportate le azioni di distribuzione seguenti:  

|Tipo di dispositivo|Azioni supportate|  
|-----------------|-----------------------|  
|iOS|**Disponibile**, **Richiesto**. L'utente deve accettare l'installazione e la disinstallazione.

> [!IMPORTANT]  
>  Al momento gli utenti finali non possono installare app aziendali dall'app Portale aziendale di Microsoft Intune per iOS. Ciò è dovuto a restrizioni relative alle app pubblicate in App Store iOS (vedere la sezione 2 delle linee guida di revisione di App Store). Gli utenti possono installare app aziendali (incluse le app gestite di App Store e i pacchetti di app line-of-business) passando al portale Web di Intune nel proprio dispositivo (portal.manage.microsoft.com). Per altre informazioni sulle funzionalità di gestione dei dispositivi mobili offerte dall'app Portale aziendale di Intune, vedere [Funzionalità di gestione dei dispositivi registrati di Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  



<!--HONumber=Dec16_HO3-->


