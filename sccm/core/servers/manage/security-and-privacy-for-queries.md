---
title: Sicurezza e privacy per le query
titleSuffix: Configuration Manager
description: Procedure consigliate per la sicurezza e privacy quando si esegue una query per ottenere informazioni dal database del sito.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0315124b44af4359528b590bf0a6b325bfd14eb1
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "67561977"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sicurezza e privacy per le query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le query consentono di recuperare informazioni dal database del sito in base ai criteri specificati. Configuration Manager raccoglie le informazioni del database del sito durante il funzionamento standard. Ad esempio, usando le informazioni raccolte durante l'individuazione o l'inventario, è possibile configurare una query per identificare i dispositivi che soddisfano i criteri specificati.  

 Per altre informazioni sulle query, vedere [Introduzione alle query in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Per informazioni sulle procedure di sicurezza consigliate e sulla privacy per le operazioni di Configuration Manager che raccolgono i dati recuperabili tramite query, vedere [Protezione e privacy per System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedure di sicurezza consigliate per le query

 Usare questa procedura consigliata di sicurezza per le query.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si esporta o si importa una query salvata in un percorso di rete, proteggere il percorso e il canale di rete.|Limitare l'accesso alla cartella di rete.<br /><br /> Usare la firma SMB (Server Message Block) o IPSec (Internet Protocol Security) tra il percorso di rete e il server del sito per impedire a un utente malintenzionato di manomettere i dati della query prima dell'importazione.|  

## <a name="next-steps"></a>Passaggi successivi
  
[Sicurezza e privacy per System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
