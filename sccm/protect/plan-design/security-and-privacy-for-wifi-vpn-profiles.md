---
title: Sicurezza e privacy per i profili Wi-Fi e VPN
titleSuffix: Configuration Manager
description: Informazioni sulle procedure di sicurezza consigliate per gestire i profili Wi-Fi e VPN per i dispositivi in Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1d582679009b90d7d8806c98a1598e040f80390d
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75819081"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Protezione e privacy per i profili Wi-Fi e VPN in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Procedure di sicurezza consigliate per i profili Wi-Fi e VPN  
 Usare le procedure di sicurezza consigliate seguenti per gestire i profili Wi-Fi e VPN per i dispositivi.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Se possibile, scegliere le opzioni più sicure supportate dall'infrastruttura Wi-Fi e VPN e dai sistemi operativi client.|I profili Wi-Fi e VPN rappresentano un metodo pratico per distribuire e gestire in modo centralizzato le impostazioni Wi-Fi e VPN già supportate dai dispositivi in uso. Configuration Manager non aggiunge funzionalità Wi-Fi o VPN.<br /><br /> Identificare, implementare e seguire le procedure consigliate per la protezione per i dispositivi e l'infrastruttura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informazioni sulla privacy per i profili Wi-Fi  
 È possibile usare i profili Wi-Fi e VPN per configurare i dispositivi client per connettersi ai server Wi-Fi e VPN e quindi valutare se questi dispositivi diventano conformi dopo che sono stati applicati i profili. Il punto di gestione invia informazioni sulla conformità al server del sito e le informazioni vengono memorizzate nel database del sito. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono memorizzate in forma crittografata nel database del sito. Il database conserva le informazioni fino a quando l'attività di manutenzione del sito **Elimina dati di gestione configurazione obsoleti** le elimina. L'intervallo di eliminazione predefinito è 90 giorni, ma è possibile modificarlo. Le informazioni sulla conformità non vengono inviate a Microsoft.  

 Per impostazione predefinita, i dispositivi non valutano i profili Wi-Fi e VPN. È necessario anche configurare i profili e quindi distribuirli agli utenti.  

 Prima di configurare i profili Wi-Fi e VPN, considerare i requisiti sulla privacy.  
