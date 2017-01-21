---
title: Supporto requisiti internazionali | Microsoft Docs
description: "Configurare System Center Configuration Manager per la conformità a requisiti internazionali specifici."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 37e45e604e89d3ce280bb2bff47d4a55b6cdfaf8


---
# <a name="international-support-in-system-center-configuration-manager"></a>Supporto internazionale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sezioni seguenti forniscono i dettagli tecnici per la configurazione di System Center Configuration Manager in modo che sia conforme a requisiti internazionali specifici.  

## <a name="gb18030-requirements"></a>Requisiti GB18030  
 Configuration Manager soddisfa gli standard definiti in GB18030. È quindi possibile usare Configuration Manager in Cina. Una distribuzione di Configuration Manager deve disporre delle seguenti configurazioni per soddisfare i requisiti GB18030:  

-   Ogni computer del server di sito e ogni computer SQL Server in uso con Configuration Manager deve usare un sistema operativo in cinese.  

-   Ogni database del sito e ogni istanza di SQL Server nella gerarchia deve utilizzare le stesse regole di confronto e deve essere una delle seguenti opzioni:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Queste regole di confronto di database rappresentano un'eccezione ai requisiti indicati in [Supporto per le versioni di SQL Server per System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Il file denominato **GB18030.SMS** deve trovarsi nella cartella radice del volume di avvio di ogni computer server del sito presente nella gerarchia. Questo file non contiene dati e può essere un file di testo vuoto denominato in modo da soddisfare questo requisito.  



<!--HONumber=Dec16_HO3-->


