---
title: Creare applicazioni Android
titleSuffix: Configuration Manager
description: Come creare e distribuire applicazioni per dispositivi Android in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef070186112642d204aade24039da87c0e3a22f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139671"
---
# <a name="create-android-applications-in-configuration-manager"></a>Creare applicazioni Android in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le applicazioni di Configuration Manager hanno uno o più tipi di distribuzione, I tipi di distribuzione comprendono i file di installazione e le informazioni necessarie per la distribuzione di software a un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere l'articolo su come [creare un'applicazione](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Tenere presenti le seguenti considerazioni quando si creano e si distribuiscono applicazioni per i dispositivi Android:  



## <a name="general-considerations-for-android-apps"></a>Considerazioni generali per le app Android

Configuration Manager supporta la distribuzione dei pacchetti Android con estensione apk. 

Sono supportate le azioni di distribuzione seguenti:

|Tipo di dispositivo|Azioni supportate|
|-|-|
|Android|**Disponibile**, **obbligatorio**: L'utente deve accettare l'installazione e la disinstallazione.|
|Android for Work |**Disponibile**, **Richiesto** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Approvare e distribuire le applicazioni Android for Work

Gli amministratori di Configuration Manager possono approvare le app anche nel [sito Web Play for Work](https://play.google.com/work). Possono quindi distribuire tali app nei dispositivi gestiti Android for Work.

Attenersi alla procedura seguente per approvare le applicazioni nello store di Play for Work, sincronizzarle con la console di Configuration Manager e quindi distribuirle ai dispositivi Android for Work gestiti. Per distribuire le app ai profili di lavoro degli utenti, è necessario approvare le app in Play for Work. Quindi è possibile sincronizzarle con la console di Configuration Manager.

1. Aprire un browser e andare a: https://play.google.com/work.  

2. Accedere usando l'account di amministratore di Google associato al tenant di Microsoft Intune.  

3. Cercare le app da distribuire nell'ambiente usato. Scegliere **Approva** per ognuna di esse per rendere l'app disponibile per Android for Work.  

4. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Android for Work**.  

5. Fare clic su **Sincronizza** nella barra multifunzione.  

6. Attendere fino a 10 minuti per la sincronizzazione delle app. Quindi andare nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e selezionare il nodo **Informazioni di licenza per le app dello Store**.  

7. Selezionare un'app sincronizzata da Play for Work e quindi fare clic su **Crea applicazione**.  

8. Completare la procedura guidata.  

9. Andare nell'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e quindi selezionare il nodo **Applicazioni**. Selezionare un'app Android for Work ed eseguire la distribuzione come di consueto.  

Per eseguire la sincronizzazione delle app Play for Work con Configuration Manager, è necessario prima approvare almeno un'app sul sito Web Play for Work.

Le app distribuite come **Disponibile** appaiono nell'app di Google Play con badge aziendale anziché nel portale aziendale. Ciò consente di distribuire le app da un'origine attendibile. L'app di Google Play con badge aziendale è un'origine attendibile. Non consentire le app da origini non attendibili.
