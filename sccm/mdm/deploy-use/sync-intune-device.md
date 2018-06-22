---
title: Sincronizzare in remoto i criteri in dispositivi registrati in Intune
titleSuffix: Configuration Manager
description: Informazioni sulla sincronizzazione dei criteri in dispositivi registrati in Intune dalla console di Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ecd2c480ab67a82539edff6daa18ef0f93628c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345712"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizzare in remoto i criteri in dispositivi registrati in Intune dalla console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile richiedere una sincronizzazione dei criteri per un dispositivo registrato in Intune dalla console di Configuration Manager, senza dover richiedere la sincronizzazione dall'app Portale aziendale sul dispositivo stesso. 

Per eseguire questa operazione:

1.  Selezionare un dispositivo in **Asset e conformità** > **Panoramica** > **Dispositivi**.
2.  Nel menu **Azioni remote dispositivo** selezionare **Send Sync Request** (Invia richiesta di sincronizzazione).


Trascorsi 5/10 minuti, le modifiche nei criteri saranno sincronizzate nel dispositivo. È possibile visualizzare le informazioni sullo stato della richiesta di sincronizzazione come nuova colonna nelle viste dispositivo denominate **Remote Sync State** (Stato sincronizzazione remota), nonché nella sezione dei dati di individuazione della finestra di dialogo **Proprietà** di ogni dispositivo.
