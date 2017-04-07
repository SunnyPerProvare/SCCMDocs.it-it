---
title: Creare applicazioni Android | Microsoft Docs
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Android.
ms.custom: na
ms.date: 03/27/2017
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 45dbf119ed5eaf875293f4eb3d89b986af6019e5
ms.lasthandoff: 03/27/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Creare applicazioni Android con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di System Center Configuration Manager contiene uno o più tipi di distribuzione che comprendono le informazioni e i file di installazione necessari per distribuire software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

 È possibile creare applicazioni usando due metodi:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere [Avviare la Creazione guidata applicazione](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). Inoltre, quando si creano e si distribuiscono applicazioni per i dispositivi Android, tenere presenti le considerazioni seguenti.  

## <a name="general-considerations-for-android-apps"></a>Considerazioni generali per le app Android

Configuration Manager supporta la distribuzione dei seguenti tipi di app per Android:

|Tipo di dispositivo|File supportati|
|-|-|
|Android|.apk|

Sono supportate le azioni di distribuzione seguenti:

|Tipo di dispositivo|Azioni supportate|
|-|-|
|Android|**Disponibile**, **Richiesto**. L'utente deve accettare l'installazione e la disinstallazione.

## <a name="approve-and-deploy-android-for-work-apps"></a>Approvare e distribuire le applicazioni Android for Work
Gli amministratori di Configuration Manager possono anche approvare e distribuire app nel [sito Web Play for Work](https://play.google.com/work) e distribuirle in dispositivi Android for Work gestiti.

Attenersi alla procedura seguente per approvare le applicazioni nello store di Play for Work, sincronizzarle con la console di Configuration Manager e quindi distribuirle ai dispositivi Android for Work gestiti. Per distribuire applicazioni a profili di lavoro degli utenti, è necessario approvarle in Play for Work e quindi sincronizzarle con la console di Configuration Manager.

1. Aprire un browser e passare a: https://play.google.com/work.
2. Accedere usando l'account di amministratore di Google associato al tenant di Intune.
3. Cercare le app che si vuole distribuire nell'ambiente e fare clic su **Approva** per ognuna di esse per renderle disponibili per Android for Work.
4. Nella console di Configuration Manager passare a **Amministratore** > **Panoramica** > **Servizi cloud** > **Android for Work** e fare clic su **Sincronizza**.
5. Attendere fino a 10 minuti che le applicazioni si sincronizzino e passare a **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Informazioni di licenza per le app dello Store**.
6. Fare clic su un'app sincronizzata da Play for Work e quindi su **Crea applicazione**.
7. Completare la procedura guidata e fare clic su **Chiudi**.
8. Passare a **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**, selezionare un'applicazione Android for Work e distribuire come di consueto.

Per eseguire la sincronizzazione delle app Play for Work con Configuration Manager, è necessario prima approvare almeno un'app sul sito Web Play for Work.

