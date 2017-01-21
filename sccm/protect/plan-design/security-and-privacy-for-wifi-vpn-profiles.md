---
title: Privacy e sicurezza dei profili Wi-Fi e VPN | Microsoft Docs
description: Informazioni sulle procedure di sicurezza consigliate per gestire i profili Wi-Fi e VPN per i dispositivi in System Center Configuration Manager.
ms.custom: na
ms.date: 10/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: fb168e3af33648e06c2c6be77ddd7d0c1f65d95d


---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Sicurezza e privacy per i profili Wi-Fi e VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


In questo argomento vengono illustrate informazioni sulla sicurezza e la privacy per i profili Wi-Fi e VPN in System Center Configuration Manager.  

##  <a name="a-namebkmksecurityremoteconnectionsa-security-best-practices-for-wi-fi--and-vpn-profiles"></a><a name="BKMK_Security_RemoteConnections"></a> Procedure di sicurezza consigliate per i profili Wi-Fi e VPN  
 Usare le procedure di sicurezza consigliate seguenti per gestire i profili Wi-Fi e VPN per i dispositivi.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Se possibile, scegliere le opzioni più sicure supportate dall'infrastruttura Wi-Fi e VPN e dai sistemi operativi client.|I profili Wi-Fi e VPN rappresentano un metodo pratico per distribuire e gestire in modo centralizzato le impostazioni Wi-Fi e VPN già supportate dai dispositivi in uso. System Center Configuration Manager non aggiunge funzionalità Wi-Fi o VPN.<br /><br /> Identificare, implementare e seguire le procedure consigliate per la protezione per i dispositivi e l'infrastruttura.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informazioni sulla privacy per i profili Wi-Fi  
 È possibile usare i profili Wi-Fi e VPN per configurare i dispositivi client per connettersi ai server Wi-Fi e VPN e quindi valutare se questi dispositivi diventano conformi dopo che sono stati applicati i profili. Il punto di gestione invia informazioni sulla conformità al server del sito e le informazioni vengono memorizzate nel database del sito. Le informazioni vengono crittografate quando i dispositivi le inviano al punto di gestione, ma non vengono memorizzate in forma crittografata nel database del sito. Il database conserva le informazioni fino a quando l'attività di manutenzione del sito **Elimina dati di gestione configurazione obsoleti** le elimina. L'intervallo di eliminazione predefinito è 90 giorni, ma è possibile modificarlo. Le informazioni sulla conformità non vengono inviate a Microsoft.  

 Per impostazione predefinita, i dispositivi non valutano i profili Wi-Fi e VPN. È necessario anche configurare i profili e quindi distribuirli agli utenti.  

 Prima di configurare i profili Wi-Fi e VPN, considerare i requisiti sulla privacy.  



<!--HONumber=Dec16_HO3-->


