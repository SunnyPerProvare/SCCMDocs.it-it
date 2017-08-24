---
title: Sicurezza e privacy per il risparmio energia | Microsoft Docs
description: Informazioni sulla sicurezza e la privacy per il risparmio di energia in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 94d5418c364c318dba92dc9f9066f54d1130aa34
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Sicurezza e privacy per il risparmio energia in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa sezione contiene informazioni sulla sicurezza e la privacy per il risparmio di energia in System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Procedure di sicurezza consigliate per il risparmio energia  
 Non esistono procedure consigliate correlate alla sicurezza per il risparmio energia.  

## <a name="privacy-information-for-power-management"></a>Informazioni sulla privacy per il risparmio energia  
 La funzione di risparmio energia usa funzionalità integrate in Windows per monitorare il consumo di energia e applicare impostazioni di risparmio energia ai computer durante l'orario lavorativo e non lavorativo. Configuration Manager raccoglie informazioni sul consumo di energia dai computer, compresi i dati relativi agli orari di uso dei computer da parte degli utenti. Anche se Configuration Manager esegue il monitoraggio del consumo di energia per una raccolta anziché per i singoli computer, una raccolta può contenere un solo computer. La funzionalità di risparmio energia non è abilitata per impostazione predefinita e deve essere configurata da un amministratore.  

 Le informazioni relative al consumo di energia vengono archiviate nel database di Configuration Manager e non vengono inviate a Microsoft. Informazioni dettagliate vengono conservate nel database per 31 giorni e le informazioni riepilogative vengono conservate per 13 mesi. Non è possibile configurare l'intervallo di eliminazione.  

 Prima di configurare il risparmio energia, prendere in considerazione i requisiti in vigore relativi alla privacy.  
