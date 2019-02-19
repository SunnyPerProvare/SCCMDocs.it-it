---
title: Supporto internazionale
titleSuffix: Configuration Manager
description: Configurare System Center Configuration Manager per la conformità a requisiti internazionali specifici.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c76f0213ffb30432c51430f3fd98b911ab5d627
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129154"
---
# <a name="international-support-in-system-center-configuration-manager"></a>Supporto internazionale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sezioni seguenti illustrano i dettagli tecnici che consentono di garantire la conformità di System Center Configuration Manager a requisiti internazionali specifici.  

## <a name="gb18030-requirements"></a>Requisiti GB18030  
 Configuration Manager soddisfa gli standard definiti in GB18030. È quindi possibile usare Configuration Manager in Cina. Una distribuzione di Configuration Manager deve disporre delle seguenti configurazioni per soddisfare i requisiti GB18030:  

-   Ogni computer del server di sito e ogni computer SQL Server in uso con Configuration Manager deve usare un sistema operativo in cinese.  

-   Ogni database del sito e ogni istanza di SQL Server nella gerarchia deve utilizzare le stesse regole di confronto e deve essere una delle seguenti opzioni:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Queste regole di confronto di database rappresentano un'eccezione ai requisiti indicati in [Supporto per le versioni di SQL Server per System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Il file denominato **GB18030.SMS** deve trovarsi nella cartella radice del volume di avvio di ogni computer server del sito presente nella gerarchia. Questo file non contiene dati e può essere un file di testo vuoto denominato in modo da soddisfare questo requisito.  
