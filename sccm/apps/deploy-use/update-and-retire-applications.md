---
title: Aggiornare e ritirare applicazioni
titleSuffix: Configuration Manager
description: Rivedere, sostituire o disinstallare le applicazioni distribuite tramite System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 831edd1d2c606253dcdc372a0a1503199734835c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32331591"
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Aggiornare e ritirare le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile che in un determinato momento si voglia apportare modifiche a un'applicazione, disinstallarla o sostituire un'applicazione già distribuita con un'applicazione nuova. System Center Configuration Manager offre queste funzionalità, che consentono di aggiornare e ritirare le applicazioni:  

-   **Modificare applicazioni**. Quando si apportano modifiche a un'applicazione o a un tipo di distribuzione, Configuration Manager mantiene una cronologia delle modifiche. È possibile ripristinare l'applicazione a una revisione precedente in qualsiasi momento. È anche possibile visualizzarne le proprietà, ripristinare una revisione precedente o eliminare una revisione precedente di un'applicazione.  

  Per altre informazioni, vedere [Application revisions](revise-and-supersede-applications.md#application-revisions) (Revisioni delle applicazioni).  

-   **Sostituire applicazioni**. È possibile aggiornare o sostituire applicazioni esistenti usando una relazione di sostituzione. Quando si sostituisce un'applicazione, è possibile specificare un nuovo tipo di distribuzione che andrà a sostituire il tipo di distribuzione dell'applicazione sostituita. È anche possibile impostare l'aggiornamento o la disinstallazione dell'applicazione sostituita prima di installare l'applicazione sostitutiva.  

  Per altre informazioni, vedere [Application revisions](revise-and-supersede-applications.md#application-supersedence) (Sostituzione delle applicazioni).  

-   **Disinstallare applicazioni**. Configuration Manager consente di disinstallare un'applicazione in modo semplice. L'operazione può essere effettuata in modalità invisibile, senza l'intervento dell'utente dell'applicazione o del dispositivo.  

  Per altre informazioni, vedere [Disinstallare applicazioni](uninstall-applications.md).  
