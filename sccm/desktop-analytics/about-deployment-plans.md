---
title: Piani di distribuzione in desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni sui piani di distribuzione in analisi desktop.
ms.date: 08/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65dff1dbf8e8154bc2d481e274dd47d352aa9d6e
ms.sourcegitcommit: fe8934487158ed3bd15c7a6a456c3cafe58aed64
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995386"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Informazioni sui piani di distribuzione in desktop Analytics

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analytics raccoglie e analizza i dati dei dispositivi, delle applicazioni e dei driver nell'organizzazione. In base a questa analisi e all'input, è possibile usare il servizio per creare piani di distribuzione per Windows 10. I piani di distribuzione includono le seguenti funzionalità:  

- Consigliare automaticamente i dispositivi da includere nei progetti pilota  

- Identificare i problemi di compatibilità e suggerire le mitigazioni  

- Valutare l'integrità della distribuzione prima, durante e dopo gli aggiornamenti  

- Tenere traccia dello stato di avanzamento della distribuzione  

Come parte del piano di distribuzione, eseguire le azioni seguenti:  

- Definire le versioni di Windows 10 che si desidera distribuire  

- Scegliere i gruppi di dispositivi in cui si vuole eseguire la distribuzione  

- Creare regole di conformità per la distribuzione  

- Definire l'importanza delle app  

- Scegli dispositivi pilota basati su consigli automatici  

- Decidere come risolvere i problemi con le app in base alle raccomandazioni di analisi desktop  

Per impostazione predefinita, desktop Analytics aggiorna quotidianamente i dati del piano di distribuzione. Tutte le modifiche apportate all'interno di un piano di distribuzione, ad esempio l'assegnazione dell'importanza a un'app o la scelta di un dispositivo da includere in un progetto pilota, richiedono fino a 24 ore per l'elaborazione. Per velocizzare questo processo, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [domande frequenti su desktop Analytics](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Dopo la connessione di desktop Analytics a Configuration Manager, selezionare le raccolte nei piani di distribuzione. Questa integrazione consente quindi di distribuire Windows in una raccolta basata sui dati di analisi del desktop.



## <a name="readiness-rules"></a>Regole di conformità

Nei piani di distribuzione sono disponibili le seguenti regole di conformità:

- Indica se i dispositivi ricevono automaticamente driver da Windows Update. Se i dispositivi ricevono gli aggiornamenti dei driver da Windows Update, tutti i problemi relativi ai driver identificati come parte della valutazione della conformità vengono contrassegnati automaticamente come **pronti**.  

- Soglia numero installazione bassa per le app di Windows. Se un'app è installata in una percentuale superiore di computer rispetto a questa soglia, il piano di distribuzione contrassegna l'app come **degno**di nota. Questo tag significa che è possibile decidere quanto sia importante eseguire il test dell'app durante la fase pilota.  


## <a name="plan-assets"></a>Pianificare asset

<!-- 4670224 -->

Mentre l'area [Asset](/sccm/desktop-analytics/about-assets) Mostra anche dispositivi e app, l'area **asset del piano** in un piano di distribuzione specifico include informazioni aggiuntive.

### <a name="devices"></a>Dispositivi

Vedere la **decisione di aggiornamento di Windows** per ogni dispositivo nel piano di distribuzione.

La decisione di aggiornamento di Windows per **sostituire il dispositivo** può essere dovuta a uno dei motivi seguenti:

- Il controllo del processore richiesto di Windows 10 non è riuscito. Per ulteriori informazioni, vedere [requisiti hardware minimi](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Ha un blocco BIOS
- Memoria insufficiente
- Un componente critico di avvio nel sistema ha un driver bloccato
- Non è possibile aggiornare la marca e il modello specifici
- È disponibile un componente della classe di visualizzazione con un blocco driver con tutti gli attributi seguenti:
    - Non eseguire l'override
    - Nessun driver nella nuova versione del sistema operativo
    - Non è già Windows Update
- Nel sistema è presente un altro componente plug-and-Play che blocca l'aggiornamento
- È disponibile un componente wireless che usa un driver emulato da XP
- Un componente di rete con una connessione attiva perderà il relativo driver. In altre parole, dopo l'aggiornamento potrebbe verificarsi una perdita di connettività di rete.

### <a name="apps"></a>App

Impostare la **decisione di aggiornamento** e l' **importanza** di questa app in questo piano di distribuzione. Per ulteriori informazioni, vedere [come creare piani di distribuzione](/sccm/desktop-analytics/create-deployment-plans).

Nei dettagli dell'app è possibile vedere anche le informazioni seguenti: Raccomandazioni, fattori di rischio per la compatibilità e problemi noti di Microsoft. Utilizzare queste informazioni per impostare la **decisione di aggiornamento**. Per ulteriori informazioni, vedere [Compatibility assessment](/sccm/desktop-analytics/compat-assessment).

Le app che desktop Analytics Mostra come *degno* di nota si basano sulla soglia per il numero di installazioni basso per le regole di conformità del piano di distribuzione. Per altre informazioni, vedere [regole di conformità](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

   > [!Tip]
   > Per altre informazioni sulla categoria di app "non importante", vedere l'argomento relativo alla [decisione di aggiornamento automatico delle app di sistema e dello Store](/sccm/desktop-analytics/about-assets#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>Driver

Vedere l'elenco dei driver inclusi in questo piano di distribuzione. Impostare la **decisione di aggiornamento**, esaminare le raccomandazioni di Microsoft e vedere fattori di rischio per la compatibilità.


## <a name="importance"></a>Importanza

Come parte del piano di distribuzione, impostare l' *importanza* delle app. Desktop Analytics rileva queste app come installate nei dispositivi di destinazione. Questa impostazione aiuta desktop Analytics a determinare quali dispositivi include nella fase pilota della distribuzione.

Se un'app è installata in meno del 2% dei dispositivi di destinazione, il numero di **installazioni**è contrassegnato come basso. Il valore predefinito è due%. È possibile regolare la soglia nelle impostazioni di conformità da 0% a 10%. Desktop Analytics contrassegna automaticamente queste app come **pronte per l'aggiornamento**.  

Per le app, scegliere un'importanza **critica**, **importante**o **non importante**. Se si contrassegna uno come critico o importante, desktop Analytics include nella distribuzione pilota alcuni dispositivi con tale app. Il servizio include nel progetto pilota più istanze di un'app critica. Se un'app viene contrassegnata come non importante, desktop Analytics la imposta automaticamente su **pronto per l'aggiornamento**.



## <a name="pilot-devices"></a>Dispositivi pilota

Desktop Analytics combina le informazioni di importanza con le impostazioni pilota globali. Viene quindi creata una raccomandazione per i dispositivi che devono far parte della distribuzione pilota. La distribuzione pilota consigliata include dispositivi con diverse configurazioni hardware e una o più istanze di tutte le app critiche e importanti. Se un'app è contrassegnata come critica, il servizio consiglia più dispositivi con tale app nel progetto pilota.



## <a name="deployment-plans-in-configuration-manager"></a>Piani di distribuzione in Configuration Manager

Dopo aver creato un piano di distribuzione, usare Configuration Manager per distribuire i prodotti. Una volta avviata la distribuzione, desktop Analytics monitora la distribuzione in base alle impostazioni del piano.


## <a name="next-steps"></a>Passaggi successivi

- Informazioni [sulle risorse di analisi desktop](/sccm/desktop-analytics/about-assets): dispositivi, driver e app  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](/sccm/desktop-analytics/about-updates)  

- [Creare un piano di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  
