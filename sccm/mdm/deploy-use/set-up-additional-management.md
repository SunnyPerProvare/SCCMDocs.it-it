---
title: Impostare soluzioni di gestione aggiuntive
titleSuffix: Configuration Manager
description: Configurare la gestione aggiuntiva tramite Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6b361742cb8b7f4dbf2da2d4b582e645bdd7545
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519879"
---
# <a name="set-up-additional-management-with-configuration-manager"></a>Configurare la gestione aggiuntiva con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

(Facoltativo) È possibile impostare la gestione aggiuntive prima che i dispositivi vengano registrati. Queste soluzioni di gestione possono essere create e distribuite una volta registrati i dispositivi, anche se molte organizzazioni preferiscono distribuirle nel momento in cui i dispositivi iniziano a essere gestiti.

**Gli elementi di configurazione** consentono di gestire le impostazioni, ad esempio richiedere un PIN o la crittografia nei dispositivi registrati in base alla piattaforma dei dispositivi:
- [Dispositivi Windows 10 e Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Dispositivi Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Dispositivi iOS e Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Dispositivi Android e Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Le applicazioni** possono essere distribuite ai dispositivi gestiti:
- [Applicazioni iOS](creating-ios-applications.md)
- [Applicazioni Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Applicazioni PC Windows](../../apps/get-started/creating-windows-applications.md)
- [Applicazioni Windows Phone](creating-windows-phone-applications.md)
- [Applicazioni Android](creating-android-applications.md)

**L'accesso condizionale** consente di gestire l'accesso alle risorse aziendali tra cui:  
- [Accesso alla posta elettronica](manage-email-access.md)
- [Accesso a SharePoint](manage-sharepoint-online-access.md)
- [Accesso a Skype for Business](manage-skype-for-business-online-access.md)
- [Dynamics CRM Online](manage-dynamics-crm-online-access.md)

**Multi-Factor Authentication (MFA)** consente di richiedere più metodi di verifica, aggiungendo così un secondo livello di sicurezza di importanza critica agli accessi e alle transazioni degli utenti.
In precedenza, per impostare Multi-Factor Authentication per le registrazioni di Intune si accedeva alla console di Intune o alla console di Configuration Manager. Ora si accede al [portale di Microsoft Azure](https://manage.windowsazure.com) usando le credenziali di Intune e configurando le impostazioni di Multi-Factor Authentication tramite Azure AD. Per altre informazioni, vedere [Multi-Factor Authentication per Microsoft Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
> [Passaggio successivo](verify-mdm-configuration.md) [< passaggio precedente](enable-platform-enrollment.md)>
