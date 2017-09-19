---
title: Sicurezza e privacy per le query | Microsoft Docs
description: Procedure consigliate per la sicurezza e privacy quando si esegue una query per ottenere informazioni dal database del sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f844b44333f5bf2c728ce84588210212ee270eec
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sicurezza e privacy per le query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le query restituiscono informazioni dal database del sito in base ai criteri specificati dall'utente. Configuration Manager raccoglie le informazioni del database del sito durante il funzionamento standard. Ad esempio, con le informazioni raccolte tramite individuazione o inventario è possibile configurare una query per identificare i dispositivi che soddisfano criteri specifici.  

 Per altre informazioni sulle query, vedere [Introduzione alle query in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Per altre informazioni sulle procedure di sicurezza consigliate e le informazioni sulla privacy per le operazioni di Configuration Manager che raccolgono le informazioni richieste dall'utente usando le query, vedere [Protezione e privacy per System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedure di sicurezza consigliate per le query  
 Usare la seguente procedura di sicurezza consigliata per le query.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si esporta o si importa una query salvata in un percorso di rete, proteggere il percorso e il canale di rete.|Limitare l'accesso alla cartella di rete.<br /><br /> Usare la firma SMB (Server Message Block) o IPsec (Internet Protocol Security) tra il percorso di rete e il server del sito per impedire a un utente malintenzionato di manomettere i dati della query prima dell'importazione.|  

## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per le query per System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
