---
title: Creare applicazioni iOS | Microsoft Docs
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi iOS.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 22bfae0509a5ce0b52763ea3eda7b8d6891431ed
ms.lasthandoff: 03/06/2017


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Creare applicazioni iOS con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di System Center Configuration Manager contiene uno o più tipi di distribuzione che comprendono le informazioni e i file di installazione necessari per distribuire software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

 È possibile creare applicazioni usando due metodi:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere [Avviare la Creazione guidata applicazione](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). Inoltre, quando si creano e si distribuiscono applicazioni per i dispositivi iOS, tenere presenti le considerazioni seguenti.  

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
