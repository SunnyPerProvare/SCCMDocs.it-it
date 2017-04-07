---
title: Confermare i requisiti del nome di dominio tramite System Center Configuration Manager | Microsoft Docs
description: Confermare i requisiti del nome di dominio tramite System Center Configuration Manager.
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: 18
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 51dc2cec2138c13f413853727ab956b2871d47b0
ms.lasthandoff: 03/06/2017

---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confermare i requisiti del nome di dominio con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Se necessario, eseguire i passaggi seguenti per soddisfare le dipendenze esterne a Configuration Manager:

1. Ogni utente deve avere assegnata una licenza Intune per registrare i dispositivi. Per essere associato a una licenza di Intune, ogni utente deve avere un nome entità utente (UPN) che può essere risolto pubblicamente, ad esempio johndoe@contoso.com o un ID di accesso alternativo configurato in Azure Active Directory. La configurazione di un ID di accesso alternativo consente agli utenti di accedere con un indirizzo di posta elettronica, ad esempio, anche se il loro UPN è in formato NetBIOS (ad esempio, CONTOSO\davidemilano).

  - Se l'azienda usa UPN risolvibili pubblicamente, ad esempio johndoe@contoso.com, non sono necessarie altre configurazioni.
  - Se la società usa un UPN non risolvibile, ad esempio CONTOSO\davidemilano, è necessario [configurare un ID alternativo in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Distribuire e configurare Active Directory Federation Services (AD FS). Facoltativo

     Quando viene configurato l'accesso Single Sign-On, gli utenti possono usare le credenziali aziendali per accedere ai servizi di Intune.

     Per altre informazioni, vedere i seguenti argomenti:
    -   [Preparazione dell'accesso Single Sign-On](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Pianificare e distribuire AD FS 2.0 per l'uso con l'accesso Single Sign-On](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Distribuire e configurare la sincronizzazione directory.

     La sincronizzazione della directory consente di popolare Intune con gli account utente sincronizzati. I gruppi di sicurezza e gli account utente sincronizzati vengono aggiunti a Intune. La mancata abilitazione di Sincronizzazione della directory è una causa comune dell'impossibilità di registrare i dispositivi quando si configura la gestione dei dispositivi mobili per Configuration Manager con Microsoft Intune.

     Per altre informazioni, vedere [Integrazione di directory](http://go.microsoft.com/fwlink/?LinkID=271120) nella libreria della documentazione di Active Directory.

4.  Facoltativo, non consigliato: se non si usa Active Directory Federation Services, reimpostare le password di Microsoft Online degli utenti.

     Se non si usa ADFS, è necessario impostare una password di Microsoft Online per ciascun utente.

> [!div class="button"]
[< Passaggio precedente](create-mdm-collection.md)  [Passaggio successivo >](configure-intune-subscription.md)
