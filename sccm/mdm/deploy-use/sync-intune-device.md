---
title: Sincronizzare in remoto i criteri in dispositivi registrati in Intune
titleSuffix: Configuration Manager
description: Informazioni sulla sincronizzazione dei criteri in dispositivi registrati in Intune dalla console di Configuration Manager
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: a03ba69c679bcfdc54744314c7a4cb3ef8b2a7a0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizzare in remoto i criteri in dispositivi registrati in Intune dalla console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile richiedere una sincronizzazione dei criteri per un dispositivo registrato in Intune dalla console di Configuration Manager, senza dover richiedere la sincronizzazione dall'app Portale aziendale sul dispositivo stesso. 

Per eseguire questa operazione:

1.  Selezionare un dispositivo in **Asset e conformità** > **Panoramica** > **Dispositivi**.
2.  Nel menu **Azioni remote dispositivo** selezionare **Send Sync Request** (Invia richiesta di sincronizzazione).


Trascorsi 5/10 minuti, le modifiche nei criteri saranno sincronizzate nel dispositivo. È possibile visualizzare le informazioni sullo stato della richiesta di sincronizzazione come nuova colonna nelle viste dispositivo denominate **Remote Sync State** (Stato sincronizzazione remota), nonché nella sezione dei dati di individuazione della finestra di dialogo **Proprietà** di ogni dispositivo.
