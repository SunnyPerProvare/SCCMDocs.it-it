---
title: Come creare piani di distribuzione
titleSuffix: Configuration Manager
description: Guida alle procedure per la creazione di piani di distribuzione in desktop Analytics.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03befc6758d70acd93f1d884b9f29ca01483fe01
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386530"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Come creare piani di distribuzione in desktop Analytics

Questo articolo illustra la procedura per la creazione di un piano di distribuzione in desktop Analytics. Prima di iniziare, informazioni [sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans).

## <a name="create-a-plan-for-windows-10"></a>Creazione di un piano per Windows 10

Eseguire la procedura descritta in questa sezione per usare analisi del desktop per creare un piano per la distribuzione di Windows 10.

1. Aprire il [portale di Analytics per desktop](https://aka.ms/desktopanalytics). Usare le credenziali che dispongono almeno delle autorizzazioni **Collaboratore area di lavoro** .  

2. Selezionare **piani di distribuzione** nel gruppo Gestisci.  

3. Nel riquadro **piani di distribuzione** selezionare **Crea**.  

4. Nel riquadro **crea piano di distribuzione** configurare le impostazioni seguenti:  

    - **Nome**: nome univoco per il piano di distribuzione  

    - **Prodotti e versioni**: scegliere la versione di Windows 10 da distribuire. Microsoft consiglia di creare piani di distribuzione che utilizzano la versione più recente.  

    - **Gruppi di dispositivi**: selezionare uno o più gruppi e quindi selezionare **Imposta come gruppi di destinazione**. I gruppi con **SCCM** come origine sono raccolte sincronizzate da Configuration Manager.  

    - **Regole di conformità**: queste regole consentono di determinare quali dispositivi sono idonei per l'aggiornamento. Per altre informazioni, vedere [regole di conformità](#readiness-rules).  

    - **Data di completamento**: scegliere la data in cui Windows deve essere distribuito completamente a tutti i dispositivi di destinazione.  

5. Selezionare **Crea**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione durante l'elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [domande frequenti su desktop Analytics](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Per aprire il piano di distribuzione, selezionarne il nome.  

7. Nel menu piano di distribuzione, nel gruppo **prepara** , selezionare **identifica importanza**.  

    1. Nella scheda **app** selezionare per visualizzare solo gli asset **non rivisti** .  

    2. Selezionare ogni app e quindi fare clic su **modifica**. È possibile selezionare più app da modificare nello stesso momento.  

    3. Scegliere un livello di importanza dall'elenco di **priorità** . Se si vuole che l'app venga convalidata da desktop Analytics durante il progetto pilota, selezionare **critico** o **importante**. Non convalida le app contrassegnate come **non importanti**. Valutare la [compatibilità](/sccm/desktop-analytics/compat-assessment) e altre informazioni sui piani quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere la decisione di aggiornamento.  

    4. Al termine, selezionare **Salva** .  

8. Nel menu piano di distribuzione, nel gruppo **prepara** , selezionare **identifica pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **Aggiungi a progetto pilota**. Se non si è d'accordo con la raccomandazione, selezionare **Sostituisci**.  

        Per ulteriori informazioni sul modo in cui l'analisi desktop esegue queste raccomandazioni, selezionare l'icona informazioni nell'angolo superiore destro del riquadro **identifica progetto pilota** .

## <a name="readiness-rules"></a>Regole di conformità

Queste regole consentono di determinare quali dispositivi sono idonei per l'aggiornamento sul posto. È possibile impostare queste regole quando si crea il piano di distribuzione o modificarle in un secondo momento.

Per modificare le regole di conformità:

1. Nel portale di analisi del desktop selezionare il piano di distribuzione.
1. Accanto al nome selezionare Edit ( **modifica**).
1. Selezionare **regole di conformità**.
1. Selezionare **sistema operativo Windows**.
1. Apportare le modifiche necessarie e selezionare **Salva**.

Per gli aggiornamenti del **sistema operativo Windows** sono disponibili due regole: i driver di dispositivo e le applicazioni Windows.

### <a name="device-drivers"></a>Driver di dispositivo

Consente di specificare se i dispositivi ottengono driver da Windows Update. Per impostazione predefinita, questo valore è **disattivato** . Abilitare questa regola quando si usa Windows Update for business per gestire gli aggiornamenti, inclusi i driver. Se si usa Configuration Manager per gestire gli aggiornamenti software, impostare questa regola su **disattivato**.

### <a name="windows-applications"></a>Applicazioni Windows

Le app che desktop Analytics Mostra come *degno* di nota si basano sulla soglia di numero di installazioni basso. Impostare questa soglia nelle regole di conformità per il piano di distribuzione. Per impostazione predefinita, questa soglia è pari al **2,0%**. È possibile modificare il valore da `0.0` a `10.0`.


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per la distribuzione nei dispositivi pilota.
> [!div class="nextstepaction"]  
> [Distribuisci in progetto pilota](/sccm/desktop-analytics/deploy-pilot)  
