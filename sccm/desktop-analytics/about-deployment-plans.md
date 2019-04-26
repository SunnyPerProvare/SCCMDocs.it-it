---
title: Piani di distribuzione in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sui piani di distribuzione in Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62243359"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Informazioni sui piani di distribuzione in Desktop Analitica 

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analitica raccoglie e analizza i dati di dispositivi, applicazioni e driver all'interno dell'organizzazione. In base all'input e l'analisi, è possibile utilizzare il servizio per creare piani di distribuzione per Windows 10 e Office 365 ProPlus. I piani di distribuzione includono le funzionalità seguenti:  

- Consiglia automaticamente ai dispositivi da includere nei progetti pilota  

- Identificare i problemi di compatibilità e suggerire soluzioni di attenuazione  

- Valutare l'integrità della distribuzione prima, durante e dopo gli aggiornamenti  

- Tenere traccia dell'avanzamento della distribuzione  


Come parte del piano di distribuzione, eseguire le operazioni seguenti:  

 - Definire quali prodotti e le versioni da distribuire: Windows 10, Office 365 ProPlus, o entrambi  

 - Scegliere i gruppi di dispositivi a cui si desidera distribuire  

 - Creare regole di conformità per la distribuzione  

 - Definire l'importanza delle App e dei componenti aggiuntivi di Office  

 - Scegliere i dispositivi pilota in base ai suggerimenti automatici  

 - Decidere come risolvere i problemi con le App e componenti aggiuntivi di Office in base alle raccomandazioni da Desktop Analitica  


Desktop Analitica dati del piano di distribuzione viene aggiornato ogni giorno. Le modifiche apportate potrebbero non essere per 24 ore. Tali modifiche includono l'assegnazione di priorità a un'app o scelta di un dispositivo da includere in un progetto pilota.  

Se ci si connette Analitica Desktop a Configuration Manager, selezionare le raccolte nei piani di distribuzione. Quindi questa integrazione consente di distribuire Windows o dell'ufficio per una raccolta in base ai dati di Analitica Desktop. 

Se non si usa Configuration Manager, è possibile creare gruppi in Log Analitica. Per altre informazioni, vedere [ricerche nei log di gruppi di Computer in Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups). 



## <a name="readiness-rules"></a>Regole di conformità

Le regole di conformità seguenti sono disponibili nei piani di distribuzione:

- Indica se i dispositivi ricevono automaticamente i driver da Windows Update. Se i dispositivi ricevono gli aggiornamenti dei driver da Windows Update, quindi vengono contrassegnati automaticamente i problemi di driver identificati come parte della valutazione della conformità **pronti**.  

- Bassa installare soglia conteggio per le app di Windows. Se un'app è installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come **Noteworthy**. Questo tag indica che è possibile decidere di quanto sia importante per eseguire il test durante la fase pilota.  

- L'aggiornamento di Office 365 ProPlus da 32 bit a 64 bit su dispositivi che hanno una versione a 64 bit di Windows. Questo comportamento è quello predefinito.  

- Durante l'aggiornamento da una versione precedente di Office, lasciare le applicazioni Office meno recenti, anche se tali App non presenti nella versione più recente di Office. Per impostazione predefinita, questo comportamento non è in.  

- Bassa installare soglia conteggio per i componenti aggiuntivi di Office. La soglia predefinita è `2%`. Componenti aggiuntivi sotto questa soglia vengono impostati automaticamente su *bassa conteggio installazioni*. Desktop Analitica non convalida questi componenti aggiuntivi durante la fase pilota. 

    Se un componente aggiuntivo viene installato in una percentuale di computer superiore a questa soglia, contrassegna il piano di distribuzione come il componente aggiuntivo *Noteworthy*. È quindi possibile decidere la sua importanza per eseguire il test durante la fase pilota.   



## <a name="importance"></a>importanza

Come parte del piano di distribuzione, impostare il *importanza* delle App e dei componenti aggiuntivi di Office. Desktop Analitica rileva queste App come installata nei dispositivi di destinazione. Questa impostazione consente Desktop Analitica di determinare quali dispositivi include nella fase pilota della distribuzione. 

Se un'app o un componente aggiuntivo viene installato in meno di 2% dei dispositivi di destinazione, viene contrassegnato **bassa conteggio installazioni**. % 2% è il valore predefinito. È possibile regolare la soglia nelle impostazioni di conformità da 0% al 10%. Desktop Analitica Contrassegna automaticamente queste App e componenti aggiuntivi come **pronto per l'aggiornamento**.  

Per le App e componenti aggiuntivi, scegliere un livello di importanza della **critici**, **importante**, o **non rilevanti**. Se si contrassegna una come importanti o critici, Analitica Desktop sono inclusi nella distribuzione pilota alcuni dispositivi dotati di tale applicazione o un componente aggiuntivo. Il servizio include in una distribuzione pilota di più istanze di un'app critico o di un componente aggiuntivo. Se si contrassegna un'app o componente aggiuntivo non è urgente, Analitica Desktop impostata automaticamente su **pronto per l'aggiornamento**.



## <a name="pilot-devices"></a>Dispositivi pilota

Desktop Analitica combina le informazioni di importanza con le impostazioni globali di pilota. Viene quindi creata una raccomandazione per il quale i dispositivi devono far parte della distribuzione pilota. La distribuzione pilota consigliata include i dispositivi con diverse configurazioni hardware e uno o più istanze di tutte le app critiche e importanti. Se un'app è contrassegnato come critico, il servizio consiglia ulteriori dispositivi con app in una distribuzione pilota.



## <a name="deployment-plans-in-configuration-manager"></a>Piani di distribuzione in Configuration Manager

Dopo aver creato un piano di distribuzione, usare Configuration Manager per distribuire i prodotti. Una volta avviata la distribuzione, Analitica Desktop monitora la distribuzione basata sulle impostazioni del piano.

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Analitica Desktop](/sccm/desktop-analytics/about-assets): i dispositivi, App, le app di Office, componenti aggiuntivi di Office e macro di Office  

- [Informazioni sugli aggiornamenti di sicurezza e funzionalità](/sccm/desktop-analytics/about-updates)  

- [Creare un piano di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  

