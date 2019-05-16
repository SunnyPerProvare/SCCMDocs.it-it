---
title: Piani di distribuzione in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sui piani di distribuzione in Desktop Analitica.
ms.date: 05/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b44684f897e7aad4365c39e58c9bfd486bde7cbb
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673289"
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

Desktop Analitica dati del piano di distribuzione viene aggiornato ogni giorno. Le modifiche apportate potrebbero non essere per 24 ore. Tali modifiche includono l'assegnazione di priorità a un'app o scelta di un dispositivo da includere in un progetto pilota.  

Dopo la connessione Desktop Analitica a Configuration Manager, selezionare le raccolte nei piani di distribuzione. Quindi questa integrazione consente di distribuire Windows in una raccolta in base ai dati di Analitica Desktop.



## <a name="readiness-rules"></a>Regole di conformità

Le regole di conformità seguenti sono disponibili nei piani di distribuzione:

- Indica se i dispositivi ricevono automaticamente i driver da Windows Update. Se i dispositivi ricevono gli aggiornamenti dei driver da Windows Update, quindi vengono contrassegnati automaticamente i problemi di driver identificati come parte della valutazione della conformità **pronti**.  

- Bassa installare soglia conteggio per le app di Windows. Se un'app è installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come **Noteworthy**. Questo tag indica che è possibile decidere di quanto sia importante per eseguire il test durante la fase pilota.  



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
