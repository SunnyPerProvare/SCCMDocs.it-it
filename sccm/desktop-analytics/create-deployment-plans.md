---
title: Come creare piani di distribuzione
titleSuffix: Configuration Manager
description: Informazioni di Guida per la creazione di piani di distribuzione in Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b56fac3060acc16fe46221464ddc6535b478399
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755282"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Come creare piani di distribuzione in Desktop Analitica 

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Questo articolo fornisce i passaggi per la creazione di un piano di distribuzione in Desktop Analitica. Prima di iniziare, innanzitutto [altre informazioni sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans).

Seguire i passaggi descritti in questo articolo usare Analitica Desktop per creare un piano per la distribuzione di Windows 10 e Office 365 ProPlus. Creare piani di distribuzione per Windows 10, Office 365 ProPlus o entrambi.

1. Aprire il [portale di Analitica Desktop](https://aka.ms/m365aprod). Usare le credenziali che dispongono di almeno **collaboratori dell'area di lavoro** autorizzazioni.  

2. Selezionare **piani di distribuzione** nel gruppo di gestione.  

3. Nel **piani di distribuzione** riquadro, selezionare **crea**.  

4. Nel **piano di distribuzione crea** riquadro, configurare le impostazioni seguenti:  

    - **Nome**: Un nome univoco per il piano di distribuzione  

    - **Prodotti e le versioni**: Scegliere i prodotti e le versioni per la distribuzione. Microsoft consiglia di creare piani di distribuzione per Office e Windows insieme e usare le versioni più recenti.  

    - **Gruppi di dispositivi**: Selezionare uno o più gruppi e quindi selezionare **imposta come destinazione gruppi**. Gruppi con **SCCM** come origine vengono raccolte sincronizzate da Configuration Manager.  

    - **Le regole di conformità**: Queste regole consentono di determinare i dispositivi che soddisfano le condizioni per l'aggiornamento. 

    - **Data completamento**: Scegliere la data da cui Windows e Office devono essere completamente distribuiti a tutti i dispositivi di destinazione.  

5. Selezionare **Create**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione relativi in fase di elaborazione. L'elaborazione può richiedere fino a 48 ore prima di procedere al passaggio successivo.   

6. Aprire il piano di distribuzione selezionando il relativo nome.  

7. Nel menu piano di distribuzione, nelle **Prepara** gruppo, selezionare **identificare importanza**.  

    1. Nel **Apps** scheda, selezionare questa opzione per mostrare solo **non rivisti** asset.  

    2. Selezionare tutte le app e quindi selezionare **modifica**. È possibile selezionare più di un'app da modificare nello stesso momento.   

    3. Scegliere un livello di priorità dal **importanza** elenco. Se si vuole che Desktop Analitica per convalidare il componente aggiuntivo durante la fase pilota, selezionare **critici** oppure **importante**. Componenti aggiuntivi contrassegnati come non vengono convalidate **importanti non**. Valutare i rischi di compatibilità e altre importanti informazioni piano quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere le decisioni relative all'aggiornamento.  

    4. Selezionare **salvare** al termine.  

    5. Ripetere questi passaggi per la **componenti aggiuntivi di Office**.  

8. Nel menu piano di distribuzione, nelle **preparazione** gruppo, selezionare **Identify pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **aggiungere al progetto pilota**. Se non sono d'accordo con la raccomandazione, selezionare **sostituire**.  

        Per altre informazioni su come Desktop Analitica rende questi consigli, selezionare l'icona informazioni nell'angolo superiore destro del **pilota Identify** riquadro.



### <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per la distribuzione pilota nei dispositivi.
> [!div class="nextstepaction"]  
> [Distribuire per contenuto pilota](/sccm/desktop-analytics/deploy-pilot)  
