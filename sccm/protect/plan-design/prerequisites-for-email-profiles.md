---
title: Prerequisiti per i profili di posta elettronica | Microsoft Docs
description: Informazioni sui profili di posta elettronica in System Center Configuration Manager e sulle dipendenze esterne e dipendenze nel prodotto.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0fa837c68eb073d2ceaf48c938137a94141a102e
ms.openlocfilehash: bdb7f78480f73bc4559c4ff49ecb7b047581780a
ms.contentlocale: it-it
ms.lasthandoff: 01/24/2017


---
# <a name="email-profile-prerequisites"></a>Prerequisiti dei profili di posta elettronica

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili di posta elettronica in System Center Configuration Manager hanno dipendenze esterne e dipendenze nel prodotto.  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|È necessario aver ottenuto specifiche autorizzazioni di sicurezza per gestire i profili di posta elettronica|È necessario disporre delle autorizzazioni di sicurezza seguenti per gestire le impostazioni di accesso alle risorse aziendali, ad esempio i profili di posta elettronica:<br /><br /> Per visualizzare e gestire avvisi e report per i profili di posta elettronica: autorizzazioni **Crea**, **Elimina**, **Modifica**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Avvisi**.<br /><br /> Per creare e gestire profili dei certificati: autorizzazioni **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo certificato**.<br /><br /> Per gestire le distribuzioni dei profili di posta elettronica: autorizzazioni **Distribuisci criteri di configurazione**, **Modifica avviso stato client**, **Lettura** e **Leggi risorsa** per l'oggetto **Raccolta**.<br /><br /> Per gestire tutti i criteri di configurazione: autorizzazioni **Crea**, **Elimina**, **Modifica**, **Lettura** e **Imposta ambito di protezione** per l'oggetto **Criteri di configurazione**.<br /><br /> Per eseguire query relativi ai profili di posta elettronica: autorizzazione **Lettura** per l'oggetto **Query**.<br /><br /> Per visualizzare le informazioni sui profili di posta elettronica nella console di System Center Configuration Manager: autorizzazione **Lettura** per l'oggetto **Sito**.<br /><br /> Per visualizzare i messaggi di stato per i profili di posta elettronica: autorizzazione **Lettura** per l'oggetto **Messaggi di stato**.<br /><br /> Per creare e gestire profili di posta elettronica: autorizzazioni **Criteri autore**, **Modifica report**, **Lettura** ed **Esegui report** per l'oggetto **Profilo di provisioning delle comunicazioni**.<br /><br /> Il ruolo di sicurezza **Gestione accesso risorse aziendali** include queste autorizzazioni necessarie per gestire i profili di posta elettronica in System Center Configuration Manager. Per altre informazioni, vedere [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md)|  
|Attributo di posta in Active Directory|Se si vuole generare l'indirizzo di posta elettronica degli utenti in un profilo di posta elettronica usando l'indirizzo SMTP primario dell'utente, è necessario configurare l'individuazione utente di System Center Configuration Manager per individuare l'attributo **mail** di Active Directory (configurato per impostazione predefinita).|  

## <a name="external-dependencies"></a>Dipendenze esterne  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Attributo di posta in Active Directory|Se si vuole generare l'indirizzo di posta elettronica degli utenti in un profilo di posta elettronica usando l'indirizzo SMTP primario dell'utente, l'indirizzo deve esistere nell'attributo **mail** di Active Directory.<br /><br /> Per altre informazioni, vedere la documentazione di Windows Server.|

