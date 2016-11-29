---
title: Creare applicazioni Android | System Center Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Android.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 379b4601-107a-4ea9-99be-1fc70b7bb377
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b600217338e2f0fb3b077036c59aaea13f76c0d6

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Creare applicazioni Android con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di System Center Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni per i dispositivi Android è necessario tenere presente quanto segue.  

## <a name="general-considerations"></a>Considerazioni generali

Configuration Manager supporta la distribuzione dei seguenti tipi di app per Android:

|Tipo di dispositivo|File supportati|
|-|-|
|Android|.apk|

Sono supportate le azioni di distribuzione seguenti:

|Tipo di dispositivo|Azioni supportate|
|-|-|
|Android|**Disponibile**, **Obbligatorio** (ma l'utente deve accettare l'installazione), **Disinstalla** (anche in questo caso è necessario il consenso).|



<!--HONumber=Nov16_HO1-->


