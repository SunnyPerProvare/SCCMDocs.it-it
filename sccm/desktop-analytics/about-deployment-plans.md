---
title: Piani di distribuzione in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sui piani di distribuzione in Desktop Analitica.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e1f084f1f3fdfd8b51caa7db696a841ffbf2e57
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159262"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Informazioni sui piani di distribuzione in Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analitica raccoglie e analizza i dati di dispositivi, applicazioni e driver all'interno dell'organizzazione. In base all'input e l'analisi, è possibile utilizzare il servizio per creare piani di distribuzione per Windows 10. I piani di distribuzione includono le funzionalità seguenti:  

- Consiglia automaticamente ai dispositivi da includere nei progetti pilota  

- Identificare i problemi di compatibilità e suggerire soluzioni di attenuazione  

- Valutare l'integrità della distribuzione prima, durante e dopo gli aggiornamenti  

- Tenere traccia dell'avanzamento della distribuzione  

Come parte del piano di distribuzione, eseguire le operazioni seguenti:  

- Definire quali versioni di Windows 10 da distribuire  

- Scegliere i gruppi di dispositivi a cui si desidera distribuire  

- Creare regole di conformità per la distribuzione  

- Definire l'importanza delle tue App  

- Scegliere i dispositivi pilota in base ai suggerimenti automatici  

- Decidere come risolvere i problemi relativi alle App basate su consigli da Desktop Analitica  

Per impostazione predefinita, Analitica Desktop Aggiorna i dati del piano di distribuzione ogni giorno. Le modifiche apportate all'interno di un piano di distribuzione, ad esempio l'assegnazione di priorità a un'app o scelta di un dispositivo da includere in un progetto pilota, accetta fino a 24 ore per l'elaborazione. Per accelerare questo processo, richiedere un aggiornamento dei dati on demand. Per altre informazioni, vedere [domande frequenti su Analitica Desktop](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Dopo la connessione Desktop Analitica a Configuration Manager, selezionare le raccolte nei piani di distribuzione. Quindi questa integrazione consente di distribuire Windows in una raccolta in base ai dati di Analitica Desktop.



## <a name="readiness-rules"></a>Regole di conformità

Le regole di conformità seguenti sono disponibili nei piani di distribuzione:

- Indica se i dispositivi ricevono automaticamente i driver da Windows Update. Se i dispositivi ricevono gli aggiornamenti dei driver da Windows Update, quindi vengono contrassegnati automaticamente i problemi di driver identificati come parte della valutazione della conformità **pronti**.  

- Bassa installare soglia conteggio per le app di Windows. Se un'app è installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come **Noteworthy**. Questo tag indica che è possibile decidere di quanto sia importante per eseguire il test durante la fase pilota.  


## <a name="plan-assets"></a>Pianificare gli asset

<!-- 4670224 -->

Mentre il [asset](/sccm/desktop-analytics/about-assets) ' area Mostra anche i dispositivi e App, il **pianificare asset** area in un piano di distribuzione specifico include informazioni aggiuntive.

### <a name="devices"></a>Dispositivi

Vedere le **decisione di aggiornamento Windows** per ogni dispositivo nel piano di distribuzione.

Decisione di eseguire l'aggiornamento di Windows **Replace dispositivo** può dipendere da uno dei motivi seguenti:

- Non è riuscito una verifica del processore richiesto Windows 10. Per altre informazioni, vedere [requisiti hardware minimi](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Dispone di un blocco di BIOS
- Non ha memoria sufficiente
- Un componente fondamentale di avvio del sistema include un driver bloccato
- Impossibile aggiornare la marca e modello
- È presente un componente di visualizzazione della classe con un blocco di driver con tutti gli attributi seguenti:
    - Non si sostituiscono
    - Non vi è alcun driver nella nuova versione del sistema operativo
    - Non è già in Windows Update
- È un altro componente plug and play nel sistema che blocca l'aggiornamento
- È presente un componente senza fili che usa un driver emulati XP
- Un componente di rete con una connessione attiva perderà il relativo driver. In altre parole, dopo l'aggiornamento potrebbe perdere la connettività di rete.

### <a name="apps"></a>App

Impostare il **decisione di aggiornamento** , nonché **importanza** per questa app in questo piano di distribuzione. Per altre informazioni, vedere [come creare piani di distribuzione](/sccm/desktop-analytics/create-deployment-plans).

I dettagli dell'app, è anche possibile vedere le informazioni seguenti: Indicazioni, compatibilità fattori di rischio e problemi noti di Microsoft. Usare queste informazioni per impostare il **decisione di aggiornamento**. Per altre informazioni, vedere [valutazione della compatibilità](/sccm/desktop-analytics/compat-assessment).

Le app che Analitica Desktop viene visualizzato come *degno di nota* sono basati sulla soglia conteggio installazione bassa per le regole di preparazione del piano di distribuzione. Per altre informazioni, vedere [regole di conformità](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

### <a name="drivers"></a>Driver

Vedere l'elenco di driver incluso con questo piano di distribuzione. Impostare il **decisione di aggiornamento**, verificare la raccomandazione di Microsoft e vedere i fattori di rischio di compatibilità.


## <a name="importance"></a>importanza

Come parte del piano di distribuzione, impostare il *importanza* delle app. Desktop Analitica rileva queste App come installata nei dispositivi di destinazione. Questa impostazione consente Desktop Analitica di determinare quali dispositivi include nella fase pilota della distribuzione.

Se un'app viene installata in meno di 2% dei dispositivi di destinazione, viene contrassegnato **bassa conteggio installazioni**. % 2% è il valore predefinito. È possibile regolare la soglia nelle impostazioni di conformità da 0% al 10%. Desktop Analitica Contrassegna automaticamente queste App come **pronto per l'aggiornamento**.  

Per le app, scegliere un livello di importanza della **critici**, **importante**, o **non rilevanti**. Se si contrassegna una come importanti o critici, alcuni dispositivi con app Desktop Analitica include nella distribuzione pilota. Il servizio include in una distribuzione pilota più istanze di un'app critica. Se si contrassegna un'app come non importante, Analitica Desktop impostata automaticamente su **pronto per l'aggiornamento**.



## <a name="pilot-devices"></a>Dispositivi pilota

Desktop Analitica combina le informazioni di importanza con le impostazioni globali di pilota. Viene quindi creata una raccomandazione per il quale i dispositivi devono far parte della distribuzione pilota. La distribuzione pilota consigliata include i dispositivi con diverse configurazioni hardware e uno o più istanze di tutte le app critiche e importanti. Se un'app è contrassegnato come critico, il servizio consiglia ulteriori dispositivi con app in una distribuzione pilota.



## <a name="deployment-plans-in-configuration-manager"></a>Piani di distribuzione in Configuration Manager

Dopo aver creato un piano di distribuzione, usare Configuration Manager per distribuire i prodotti. Una volta avviata la distribuzione, Analitica Desktop monitora la distribuzione basata sulle impostazioni del piano.


## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Analitica Desktop](/sccm/desktop-analytics/about-assets): i dispositivi, driver e le app  

- [Informazioni sugli aggiornamenti di sicurezza e funzionalità](/sccm/desktop-analytics/about-updates)  

- [Creare un piano di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  
