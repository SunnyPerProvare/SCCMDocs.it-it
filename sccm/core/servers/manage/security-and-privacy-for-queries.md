---
title: Sicurezza e privacy per le query
titleSuffix: Configuration Manager
description: Procedure consigliate per la sicurezza e privacy quando si esegue una query per ottenere informazioni dal database del sito.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7cdd9731b2ae34e096159b9e73c730fcbd7ac728
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121533"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sicurezza e privacy per le query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le query restituiscono informazioni dal database del sito in base ai criteri specificati dall'utente. Configuration Manager raccoglie le informazioni del database del sito durante il funzionamento standard. Ad esempio, utilizzando le informazioni raccolte da individuazione o l'inventario, è possibile configurare una query per identificare i dispositivi che soddisfano criteri specificati.  

 Per altre informazioni sulle query, vedere [Introduzione alle query in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Per altre informazioni sulle procedure di sicurezza consigliate e le informazioni sulla privacy per le operazioni di Configuration Manager che raccolgono le informazioni richieste dall'utente usando le query, vedere [Protezione e privacy per System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedure ottimali di protezione per le query  
 Usare la seguente procedura di sicurezza consigliata per le query.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si esporta o si importa una query salvata in un percorso di rete, proteggere il percorso e il canale di rete.|Limitare l'accesso alla cartella di rete.<br /><br /> Usare la firma SMB (Server Message Block) o IPsec (Internet Protocol Security) tra il percorso di rete e il server del sito per impedire a un utente malintenzionato di manomettere i dati della query prima dell'importazione.|  

## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico per le query per System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
