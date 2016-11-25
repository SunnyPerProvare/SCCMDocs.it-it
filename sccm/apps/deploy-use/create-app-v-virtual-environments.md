---
title: Creare ambienti virtuali App-V | System Center Configuration Manager
description: Creare ambienti virtuali con Microsoft Application Virtualization in modo che le applicazioni possano condividere dati.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 625ea93d855089f6dbbdcc8368032e61b8a1ba0b


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Creare ambienti virtuali App-V con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli ambienti virtuali di Microsoft Application Virtualization (App-V) in System Center Configuration Manager consentono alle applicazioni virtuali distribuite di condividere lo stesso file system e registro di sistema nei PC Windows. Ciò significa che, a differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati tra loro. Gli ambienti virtuali vengono creati o modificati nei PC client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. È possibile ordinare queste applicazioni in modo che quando più applicazioni tentano di modificare un valore del Registro di sistema o di file system, la priorità viene assegnata all'applicazione con l'ordine più elevato.  

> [!IMPORTANT]  
>  Non fare affidamento su ambienti virtuali App-V per la protezione, ad esempio, da malware.  

 Usare la procedura seguente per creare ambienti virtuali App-V in Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Creare un ambiente virtuale App-V  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Ambienti virtuali App-V**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea ambiente virtuale**.  

4.  Nella finestra di dialogo **Crea ambiente virtuale** specificare le seguenti informazioni:  

    -   **Nome** - Specificare un nome univoco per l'ambiente virtuale con un massimo di 128 caratteri.  

    -   **Descrizione** - Specificare una descrizione per l'ambiente virtuale (facoltativo).  

5.  Fare clic su **Aggiungi** per aggiungere un nuovo tipo di distribuzione all'ambiente virtuale. È necessario aggiungere almeno un tipo di distribuzione.  

6.  Nella finestra di dialogo **Aggiungi applicazioni** specificare un **Nome gruppo** con un massimo di 128 caratteri che verrà utilizzato per fare riferimento al gruppo di applicazioni aggiunte all'ambiente virtuale.  

7.  Fare clic su **Aggiungi**, selezionare le applicazioni App-V 5 ei tipi di distribuzione che si desidera aggiungere al gruppo e quindi fare clic su **OK**.  

8.  Nella finestra di dialogo **Aggiungi applicazioni** è possibile fare clic su **Aumenta priorità** o **Diminuisci priorità** per specificare a quale applicazione viene assegnata la priorità se più applicazioni tentano di modificare le impostazioni del Registro di sistema o il file system nello stesso ambiente virtuale.  

9. Fare clic su **OK** per tornare alla finestra di dialogo **Crea ambiente virtuale** .  

10. Dopo aver aggiunto i gruppi fare clic su **OK** per creare l'ambiente virtuale. Il nuovo ambiente virtuale viene visualizzato nel nodo **Ambienti virtuali App-V** della console di Configuration Manager. È possibile monitorare lo stato degli ambienti virtuali utilizzando il report **Stato ambiente virtuale App-V**.  

    > [!NOTE]  
    >  Gli ambienti virtuali verranno aggiunti o modificati nei computer client quando viene installata l'applicazione o quando il client valuta le applicazioni installate.  



<!--HONumber=Nov16_HO1-->


