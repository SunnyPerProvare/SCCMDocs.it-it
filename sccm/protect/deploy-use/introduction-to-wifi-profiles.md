---
title: Introduzione ai profili Wi-Fi | System Center Configuration Manager
description: Di seguito viene illustrato come usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 86725460-c2f3-49ed-90aa-6b2724d34d69
caps.latest.revision: 8
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 30fefb291a6fccb630d5e3272ce7266339c9139c


---
# <a name="introduction-to-wi-fi-profiles-in-system-center-configuration-manager"></a>Introduzione ai profili Wi-Fi in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alla rete wireless.  

 Si immagini ad esempio di aver installato una nuova rete Wi-Fi denominata **Contoso Wi-Fi** e di voler ora eseguire il provisioning di tutti i dispositivi che eseguono il sistema operativo iOS con le impostazioni necessarie per connettersi alla rete. È quindi possibile creare un profilo Wi-Fi contenente le impostazioni necessarie per la connessione alla rete wireless **Contoso Wi-Fi** e distribuire questo profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. In questo modo gli utenti dei dispositivi iOS visualizzeranno la rete aziendale nell'elenco delle reti wireless e potranno facilmente connettersi a tale rete.  

 Con i profili Wi-Fi è possibile configurare i seguenti tipi di dispositivi:  

-   Dispositivi che eseguono Windows 8.1 a 32 bit  

-   Dispositivi che eseguono Windows 8.1 a 64 bit  

-   Dispositivi che eseguono Windows RT 8.1  

-   Dispositivi che eseguono Windows Phone 8.1  

-   Dispositivi che eseguono Windows 10 Desktop o Mobile  

-   Dispositivi IPhone che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivi IPad che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivi Android che eseguono la versione 4  

> [!IMPORTANT]  
>  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere registrati in Microsoft Intune. Per informazioni su come registrare i dispositivi, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

 Quando si crea un profilo Wi-Fi, è possibile includere una vasta gamma di impostazioni di protezione. Queste includono certificati per la convalida del server e l'autenticazione del client di cui è stato eseguito il provisioning usando profili certificato di Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  



<!--HONumber=Nov16_HO1-->


