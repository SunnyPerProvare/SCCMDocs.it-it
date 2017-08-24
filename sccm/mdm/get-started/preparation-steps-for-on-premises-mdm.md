---
title: Passaggi di preparazione | Microsoft Docs
description: Preparare la gestione dei dispositivi con la gestione dei dispositivi mobili locale in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
caps.latest.revision: "4"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 85bdadaaaeed9a42cfa5165d2b9f0f3ef434dc03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="preparation-steps-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Preparativi per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione di dispositivi con la gestione dei dispositivi mobili locale in System Center Configuration Manager richiede che l'infrastruttura di Configuration Manager sia impostata in modo che i ruoli di sistema necessari del sito (punto proxy di registrazione, punto di registrazione, punto di gestione dispositivi e punto di distribuzione) possano comunicare attraverso un canale affidabile con i dispositivi mobili da gestire.  

 Le attività seguenti di alto livello sono necessarie per preparare il sistema di Configuration Manager per la gestione dei dispositivi mobili locale:  

-   [Impostare una sottoscrizione di Microsoft Intune per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     In questa attività, è necessario registrarsi a Microsoft Intune e aggiungere la sottoscrizione a Configuration Manager tramite la console di Configuration Manager. Questo passaggio è necessario solo per scopi correlati alla gestione delle licenze. Intune non viene usato per gestire i dispositivi o archiviare le informazioni di gestione. Tutte le attività di coordinamento e gestione dei dispositivi sono a carico dell'azienda che usa l'infrastruttura di Configuration Manager locale.  

-   [Installare i ruoli di sistema del sito per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     In questa attività si installano e configurano i ruoli di sistema del sito necessari per gestire i dispositivi con l'infrastruttura di Configuration Manager locale. La gestione dei dispositivi mobili locale richiede minimo i ruoli di sistema del sito del punto proxy di registrazione, del punto di registrazione, del punto di gestione dispositivo e del punto di distribuzione.  

-   [Impostare i certificati per comunicazioni affidabili per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     In questa attività si configura l'infrastruttura di Configuration Manager locale per consentire comunicazioni attendibili (HTTPS) tra i dispositivi gestiti e i server che ospitano i ruoli di sistema del sito necessari.  

-   [Impostare la registrazione dei dispositivi per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     In questa attività si concedono le autorizzazioni agli utenti per registrare computer e dispositivi e si installa il certificato radice attendibile nei dispositivi (in genere quelli non aggiunti al dominio) per consentire le connessioni HTTPS ai server del sistema del sito.  
