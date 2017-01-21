---
title: Prerequisiti per le raccolte | Microsoft Docs
description: Ottenere i prerequisiti per l&quot;uso delle raccolte in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 81342ab0d064e3f2da19126819bdd048270a4320


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Prerequisiti per le raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le raccolte contengono solo dipendenze nel prodotto.  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Punto di Reporting Services|Perché sia possibile eseguire i report per le raccolte, il ruolo del sistema del sito del punto di Reporting Services deve essere installato. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|È necessario aver ottenuto specifiche autorizzazioni di protezione per gestire le raccolte|È necessario disporre delle autorizzazioni di sicurezza seguenti per gestire le applicazioni:<br /><br /> Per creare e gestire le raccolte: **Crea**, **Elimina**, **Modifica**, **Modifica cartella**, **Sposta oggetto**, **Lettura** e **Leggi risorsa** per l'oggetto **Raccolta**.<br /><br /> Per gestire le impostazioni delle raccolte: **Modifica impostazione raccolta** per l'oggetto **Raccolta**.<br /><br /> L'autorizzazione **Modifica cartella** è obbligatoria per tutte le cartelle di raccolta, compresa la cartella radice.|  



<!--HONumber=Dec16_HO3-->


