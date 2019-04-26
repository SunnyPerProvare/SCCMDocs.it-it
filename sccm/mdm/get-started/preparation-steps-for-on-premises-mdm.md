---
title: Preparare per la MDM locale
titleSuffix: Configuration Manager
description: Preparare la gestione di dispositivi con la gestione dei dispositivi mobili locale in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62288644"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Preparativi per la MDM locale in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per gestire i dispositivi con gestione dei dispositivi mobili locale di Configuration Manager (MDM), prima di tutto configurare l'infrastruttura necessaria. I ruoli del sistema del sito devono comunicare attraverso un canale affidabile con i dispositivi mobili. Questi ruoli sono il punto proxy di registrazione, punto di registrazione, punto di Gestione periferiche e punto di distribuzione.

Le attività di alto livello seguenti sono necessarie per preparare Configuration Manager per MDM locale:  

- [Configurare una sottoscrizione di Microsoft Intune per MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Iscriversi a Microsoft Intune e quindi aggiungere la sottoscrizione a Configuration Manager tramite la console di Configuration Manager. Questo passaggio è necessario solo per scopi correlati alla gestione delle licenze. Intune non viene usato per gestire i dispositivi o archiviare le informazioni di gestione. Tutte le attività di coordinamento e gestione dei dispositivi sono a carico dell'azienda che usa l'infrastruttura di Configuration Manager locale.  

    > [!Note]  
    > A partire dalla versione 1810, una connessione di Intune non è più necessaria per le nuove distribuzioni MDM locale.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Installare ruoli del sistema del sito per MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Installare e configurare i sistemi del sito necessari per gestire i dispositivi con l'infrastruttura di Configuration Manager in locale. Come minimo, questa funzionalità richiede il punto proxy di registrazione, punto di registrazione, punto di gestione dei dispositivi e i ruoli punto di distribuzione.  

- [Configurare i certificati per le comunicazioni attendibili per MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configurare l'infrastruttura di Configuration Manager in locale per consentire le comunicazioni attendibili (HTTPS) tra i dispositivi gestiti e i server che ospitano i ruoli del sistema del sito necessari.  

- [Impostare la registrazione dei dispositivi per MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Concedere l'autorizzazione agli utenti di registrare i computer e dispositivi. Installare il certificato radice attendibile nei dispositivi per consentire le connessioni HTTPS al server del sistema del sito. Questi dispositivi non sono in genere aggiunti al dominio.  

