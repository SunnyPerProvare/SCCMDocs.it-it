---
title: Creare ambienti virtuali App-V | Microsoft Docs
description: Creare ambienti virtuali con Microsoft Application Virtualization in modo che le applicazioni possano condividere dati.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 377ed9732fb16b062f53e78504aea394acdb7462
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Creare ambienti virtuali App-V con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In un ambiente virtuale Microsoft Application Virtualization (App-V) in System Center Configuration Manager (Configuration Manager) le applicazioni virtuali distribuite possono condividere lo stesso file system e lo stesso Registro di sistema nei PC Windows. A differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati tra loro. Gli ambienti virtuali vengono creati o modificati nei PC client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. È possibile ordinare queste applicazioni in modo che quando più applicazioni tentano di modificare un valore del Registro di sistema o di file system, la priorità viene assegnata all'applicazione con l'ordine più elevato.  

> [!IMPORTANT]  
>  Non fare affidamento su ambienti virtuali App-V per la protezione, ad esempio, da malware.  

 Usare la procedura seguente per creare ambienti virtuali App-V in Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Creare un ambiente virtuale App-V  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Ambienti virtuali App-V**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea ambiente virtuale**.  

4.  Nella finestra di dialogo **Crea ambiente virtuale** specificare le informazioni seguenti:  

    -   **Nome**.  Immettere un nome univoco per l'ambiente virtuale (massimo 128 caratteri).  

    -   **Descrizione**. (Facoltativo) Immettere una descrizione per l'ambiente virtuale.  

5.  Per aggiungere un nuovo tipo di distribuzione all'ambiente virtuale scegliere **Aggiungi**. È necessario aggiungere almeno un tipo di distribuzione.  

6.  Nella finestra di dialogo **Aggiungi applicazioni** specificare un **Nome gruppo** (massimo 128 caratteri). Questo nome verrà utilizzato per fare riferimento al gruppo di applicazioni aggiunte all'ambiente virtuale.  

7.  Scegliere **Aggiungi**, selezionare le applicazioni App-V 5 e i tipi di distribuzione che si vogliono aggiungere al gruppo e quindi scegliere **OK**.  

8.  Nella finestra di dialogo **Aggiungi applicazioni** è possibile selezionare **Aumenta priorità** o **Diminuisci priorità** per impostare l'applicazione a cui assegnare la priorità se più applicazioni tentano di modificare le impostazioni del Registro di sistema o il file system nello stesso ambiente virtuale.  

9. Per tornare alla finestra di dialogo **Crea ambiente virtuale** scegliere **OK**.  

10. Dopo aver aggiunto i gruppi scegliere **OK** per creare l'ambiente virtuale. Il nuovo ambiente virtuale viene visualizzato nel nodo **Ambienti virtuali App-V** della console di Configuration Manager. È possibile monitorare lo stato degli ambienti virtuali tramite il report Stato ambiente virtuale App-V.  

    > [!NOTE]  
    >  Gli ambienti virtuali vengono aggiunti o modificati nei computer client quando viene installata l'applicazione o quando il client valuta le applicazioni installate.  
