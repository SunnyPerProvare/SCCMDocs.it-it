---
title: Prerequisiti per i profili di posta elettronica
titleSuffix: Configuration Manager
description: Informazioni sui profili di posta elettronica in System Center Configuration Manager e sulle dipendenze esterne e dipendenze nel prodotto.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1bb46973334dcec74715dd6123d71ddc4c0331b6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142341"
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
