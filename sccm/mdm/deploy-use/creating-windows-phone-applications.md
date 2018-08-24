---
title: Creare applicazioni Windows Phone
titleSuffix: Configuration Manager
description: Come creare e distribuire applicazioni per dispositivi Windows Phone in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77eb0b750934641ceb66b2c8aa611544c654f54f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385440"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Creare applicazioni di Windows Phone in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le applicazioni di Configuration Manager hanno uno o più tipi di distribuzione. Il tipo di distribuzione include i file di installazione e le informazioni necessarie per distribuire il software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere l'articolo su come [creare un'applicazione](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Quando si creano e si distribuiscono applicazioni per dispositivi Windows Phone, tenere presenti le considerazioni seguenti.  


Configuration Manager supporta la distribuzione dei tipi di file app seguenti:  

|Tipo di dispositivo|Tipi di file supportati|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Distribuire le app di Windows Phone come **disponibili** oppure **obbligatorie**. Usare le distribuzioni anche per disinstallare le app.  
