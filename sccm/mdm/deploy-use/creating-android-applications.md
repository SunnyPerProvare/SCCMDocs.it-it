---
title: Creare applicazioni Android | Microsoft Docs
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Android.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Creare applicazioni Android con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di System Center Configuration Manager contiene uno o più tipi di distribuzione che comprendono le informazioni e i file di installazione necessari per distribuire software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

 È possibile creare applicazioni usando due metodi:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere [Avviare la Creazione guidata applicazione](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). Inoltre, quando si creano e si distribuiscono applicazioni per i dispositivi Android, tenere presenti le considerazioni seguenti.  

## <a name="general-considerations"></a>Considerazioni generali

Configuration Manager supporta la distribuzione dei seguenti tipi di app per Android:

|Tipo di dispositivo|File supportati|
|-|-|
|Android|.apk|

Sono supportate le azioni di distribuzione seguenti:

|Tipo di dispositivo|Azioni supportate|
|-|-|
|Android|**Disponibile**, **Richiesto**. L'utente deve accettare l'installazione e la disinstallazione.

