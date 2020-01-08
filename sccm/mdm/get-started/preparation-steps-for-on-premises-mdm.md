---
title: Prepararsi per MDM locale
titleSuffix: Configuration Manager
description: Preparare la gestione dei dispositivi con la gestione di dispositivi mobili locale in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dc67512ac6ec0dc9712402189ac6d02f3552eea3
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519556"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Procedura di preparazione per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per gestire i dispositivi con Configuration Manager gestione di dispositivi mobili (MDM) locale, configurare prima di tutto l'infrastruttura necessaria. I ruoli del sistema del sito richiesti devono comunicare attraverso un canale attendibile con i dispositivi mobili. Questi ruoli includono il punto proxy di registrazione, il punto di registrazione, il punto di gestione periferiche e il punto di distribuzione.

Le attività di alto livello seguenti sono necessarie per preparare Configuration Manager per MDM locale:  

- [Configurare una sottoscrizione di Microsoft Intune per MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Iscriversi a Microsoft Intune e quindi aggiungere la sottoscrizione Configuration Manager tramite la console di Configuration Manager. Questo passaggio è necessario solo per scopi correlati alla gestione delle licenze. Intune non viene usato per gestire i dispositivi o archiviare le informazioni di gestione. Tutte le attività di coordinamento e gestione dei dispositivi sono a carico dell'azienda che usa l'infrastruttura di Configuration Manager locale.  

    > [!Note]  
    > A partire dalla versione 1810, una connessione a Intune non è più necessaria per le nuove distribuzioni MDM locali.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Installare i ruoli del sistema del sito per MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Installare e configurare i sistemi del sito necessari per gestire i dispositivi con l'infrastruttura Configuration Manager locale. Come minimo, questa funzionalità richiede i ruoli punto proxy di registrazione, punto di registrazione, punto di gestione periferiche e punto di distribuzione.  

- [Configurare i certificati per le comunicazioni attendibili per MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configurare l'infrastruttura Configuration Manager locale per consentire le comunicazioni attendibili (HTTPS) tra i dispositivi gestiti e i server che ospitano i ruoli del sistema del sito richiesti.  

- [Configurare la registrazione dei dispositivi per MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Concedere l'autorizzazione agli utenti per registrare computer e dispositivi. Installare il certificato radice attendibile nei dispositivi per consentire le connessioni HTTPS ai server del sistema del sito. Questi dispositivi non sono in genere aggiunti a un dominio.  

