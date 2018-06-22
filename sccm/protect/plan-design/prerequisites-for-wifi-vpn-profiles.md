---
title: Prerequisiti per i profili Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Informazioni sulle autorizzazioni di sicurezza necessarie per gestire i profili di certificato, i profili Wi-Fi e VPN in System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 894717df4b5acb7142aa7d171a8b8b63a28f8dc0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347383"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Prerequisiti per i profili Wi-Fi e VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili Wi-Fi e VPN in System Center Configuration Manager hanno solo dipendenze nel prodotto.  

 È necessario disporre delle seguenti autorizzazioni di protezione per gestire le impostazioni di accesso alle risorse aziendali, quali profili certificato, Wi-Fi e VPN:  

-   Per visualizzare e gestire avvisi e report per i profili Wi-Fi e VPN: autorizzazioni **Crea**, **Elimina**, **Modifica**, **Modifica report**, **Lettura**e **Esegui report** per l'oggetto **Avvisi**.  

-   Per creare e gestire profili dei certificati: **Criteri autore**, **Modifica report**, **Lettura**e **Esegui report** per l'oggetto **Profilo certificato** .  

-   Per gestire le distribuzioni Wi-Fi, certificato e profilo VPN: **Distribuisci criteri di configurazione**, **Modifica avviso stato client**, **Lettura**e **Leggi risorsa** per l'oggetto **Raccolta** .  

-   Per gestire tutti i criteri di configurazione: **Crea**, **Elimina**, **Modifica**, **Lettura**e **Imposta ambito di protezione** per l'oggetto **Criteri di configurazione** .  

-   Per eseguire query correlate ai profili Wi-Fi e VPN: autorizzazione **Lettura** per l'oggetto **Query**.  

-   Per visualizzare le informazioni sui profili Wi-Fi e VPN nella console di System Center Configuration Manager: autorizzazione **Lettura** per l'oggetto **Sito**.  

-   Per visualizzare i messaggi di stato per i profili Wi-Fi e VPN: autorizzazione **Lettura** per l'oggetto **Messaggi di stato**.  

-   Per creare e modificare il profilo del certificato CA attendibile: **Criteri autore**, **Modifica report**, **Lettura**e **Esegui report** per l'oggetto **Profilo certificato CA attendibile** .  

-   Per creare e gestire profili VPN: **Criteri autore**, **Modifica report**, **Lettura**e **Esegui report** per l'oggetto **Profilo VPN** .  

-   Per creare e gestire profili Wi-Fi: **Criteri autore**, **Modifica report**, **Lettura**e **Esegui report** per l'oggetto **Profilo Wi-Fi** .  

 Il ruolo di sicurezza **Gestione accesso risorse aziendali** include queste autorizzazioni necessarie per gestire i profili Wi-Fi in System Center Configuration Manager. Per altre informazioni, vedere [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md)
