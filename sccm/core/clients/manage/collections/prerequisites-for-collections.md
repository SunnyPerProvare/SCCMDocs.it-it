---
title: Prerequisiti per le raccolte
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per le raccolte in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e761eeffa23f7787b318291951b0cfbf27bdc49
ms.sourcegitcommit: 6ed22f0aa4a0a66428cfa27de13f6b950e79f7ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80542214"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Prerequisiti per le raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager le raccolte contengono solo dipendenze nel prodotto.  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Punto di Reporting Services|Perché sia possibile eseguire i report per le raccolte, il ruolo del sistema del sito del punto di Reporting Services deve essere installato. Per altre informazioni, vedere [Introduzione ai report](/configmgr/core/servers/manage/introduction-to-reporting).|  
|È necessario aver ottenuto specifiche autorizzazioni di protezione per gestire le raccolte|È necessario disporre delle autorizzazioni di sicurezza seguenti per gestire le applicazioni:<br /><br /> - Per creare e gestire le raccolte: **Crea**, **Elimina**, **Modifica**, **Modifica cartella**, **Sposta oggetto**, **Lettura** e **Leggi risorsa** per l'oggetto **Raccolta**.<br /><br /> - Per gestire le impostazioni delle raccolte: **Modifica impostazione raccolta** per l'oggetto **Raccolta**.<br /><br /> L'autorizzazione **Modifica cartella** è obbligatoria per tutte le cartelle di raccolta, compresa la cartella radice.|  
