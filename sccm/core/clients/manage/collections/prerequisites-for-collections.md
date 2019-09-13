---
title: Prerequisiti per le raccolte
titleSuffix: Configuration Manager
description: Ottenere i prerequisiti per l'uso delle raccolte in System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8beff2eb0d77d0dbed30b12a68a7882fc7eb320
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890164"
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Prerequisiti per le raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le raccolte contengono solo dipendenze nel prodotto.  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Punto di Reporting Services|Perché sia possibile eseguire i report per le raccolte, il ruolo del sistema del sito del punto di Reporting Services deve essere installato. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|È necessario aver ottenuto specifiche autorizzazioni di protezione per gestire le raccolte|È necessario disporre delle autorizzazioni di sicurezza seguenti per gestire le applicazioni:<br /><br /> - Per creare e gestire le raccolte: **Crea**, **Elimina**, **Modifica**, **Modifica cartella**, **Sposta oggetto**, **Lettura** e **Leggi risorsa** per l'oggetto **Raccolta**.<br /><br /> - Per gestire le impostazioni delle raccolte: **Modifica impostazione raccolta** per l'oggetto **Raccolta**.<br /><br /> L'autorizzazione **Modifica cartella** è obbligatoria per tutte le cartelle di raccolta, compresa la cartella radice.|  
