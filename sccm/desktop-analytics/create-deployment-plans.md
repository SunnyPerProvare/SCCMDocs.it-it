---
title: Come creare piani di distribuzione
titleSuffix: Configuration Manager
description: Informazioni di Guida per la creazione di piani di distribuzione in Desktop Analitica.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 696d2ecedc659330715d42c05ecc046f0a6cc7ff
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159171"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Come creare piani di distribuzione in Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Questo articolo fornisce i passaggi per la creazione di un piano di distribuzione in Desktop Analitica. Prima di iniziare, innanzitutto [altre informazioni sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans).

## <a name="create-a-plan-for-windows-10"></a>Creare un piano per Windows 10

Seguire i passaggi descritti in questa sezione usare Analitica Desktop per creare un piano per la distribuzione di Windows 10.

1. Aprire il [portale di Analitica Desktop](https://aka.ms/desktopanalytics). Usare le credenziali che dispongono di almeno **collaboratori dell'area di lavoro** autorizzazioni.  

2. Selezionare **piani di distribuzione** nel gruppo di gestione.  

3. Nel **piani di distribuzione** riquadro, selezionare **crea**.  

4. Nel **piano di distribuzione crea** riquadro, configurare le impostazioni seguenti:  

    - **Nome**: Un nome univoco per il piano di distribuzione  

    - **Prodotti e le versioni**: Scegliere la versione di Windows 10 da distribuire. Microsoft consiglia di creare piani di distribuzione che usano la versione più recente.  

    - **Gruppi di dispositivi**: Selezionare uno o più gruppi e quindi selezionare **imposta come destinazione gruppi**. Gruppi con **SCCM** come origine vengono raccolte sincronizzate da Configuration Manager.  

    - **Le regole di conformità**: Queste regole consentono di determinare i dispositivi che soddisfano le condizioni per l'aggiornamento. Per altre informazioni, vedere [regole di conformità](#readiness-rules).  

    - **Data completamento**: Scegliere la data da cui Windows deve essere completamente distribuito a tutti i dispositivi di destinazione.  

5. Selezionare **Create**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione relativi in fase di elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dei dati on demand. Per altre informazioni, vedere [domande frequenti su Analitica Desktop](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Aprire il piano di distribuzione selezionando il relativo nome.  

7. Nel menu piano di distribuzione, nelle **Prepara** gruppo, selezionare **identificare importanza**.  

    1. Nel **Apps** scheda, selezionare questa opzione per mostrare solo **non rivisti** asset.  

    2. Selezionare tutte le app e quindi selezionare **modifica**. È possibile selezionare più di un'app da modificare nello stesso momento.  

    3. Scegliere un livello di priorità dal **importanza** elenco. Se si vuole che Desktop Analitica per convalidare l'app durante la fase pilota, selezionare **critici** oppure **importante**. Le app contrassegnate come non vengono convalidate **importanti non**. Valutare la relativa [compatibilità](/sccm/desktop-analytics/compat-assessment) e altre importanti informazioni piano quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere le decisioni relative all'aggiornamento.  

    4. Selezionare **salvare** al termine.  

8. Nel menu piano di distribuzione, nelle **preparazione** gruppo, selezionare **Identify pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **aggiungere al progetto pilota**. Se non sono d'accordo con la raccomandazione, selezionare **sostituire**.  

        Per altre informazioni su come Desktop Analitica rende questi consigli, selezionare l'icona informazioni nell'angolo superiore destro del **pilota Identify** riquadro.

## <a name="readiness-rules"></a>Regole di conformità

Queste regole consentono di determinare i dispositivi che soddisfano le condizioni per l'aggiornamento sul posto. Quando si crea il piano di distribuzione o modificarli in un secondo momento, è possibile impostare queste regole.

Per modificare le regole di conformità:

1. Nel portale di Analitica Desktop, selezionare il piano di distribuzione.
1. Accanto al nome, selezionare **modifica**.
1. Selezionare **regole di conformità**.
1. Selezionare **Windows del sistema operativo**.
1. Apportare le modifiche necessarie e selezionare **salvare**.

Per la **sistemi operativi Windows** gli aggiornamenti, sono disponibili due regole: I driver di dispositivo e le applicazioni di Windows.

### <a name="device-drivers"></a>Driver di dispositivo

Configurare se i dispositivi recuperare i driver da Windows Update. Questo valore è **disattivata** per impostazione predefinita. Attivare questa regola quando si usa Windows Update for Business per gestire gli aggiornamenti inclusi i driver. Se si usa Configuration Manager per gestire gli aggiornamenti software, questa regola impostata su **disattivata**.

### <a name="windows-applications"></a>Applicazioni di Windows

Le app Desktop Analitica visualizzate come *degno di nota* sono basati sulla soglia conteggio installazione bassa. Impostare questa soglia nelle regole di conformità per il piano di distribuzione. Per impostazione predefinita, questa soglia viene **2.0%** . È possibile modificare il valore da `0.0` a `10.0`.


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per la distribuzione pilota nei dispositivi.
> [!div class="nextstepaction"]  
> [Distribuire per contenuto pilota](/sccm/desktop-analytics/deploy-pilot)  
