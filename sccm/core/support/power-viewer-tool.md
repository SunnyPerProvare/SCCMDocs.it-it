---
title: Power Viewer Tool
titleSuffix: Configuration Manager
description: Usare Power Viewer Tool per visualizzare lo stato della funzionalità di gestione dell'alimentazione su un client Gestione configurazione.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a90982aa38bbe4c171af1246aa1b12bc67b335d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385952"
---
# <a name="power-viewer-tool"></a>Power Viewer Tool

*Si applica a: System Center Configuration Manager (Current Branch)*

Lo strumento Power Viewer è uno [strumento di Configuration Manager](/sccm/core/support/tools). Può essere usato per visualizzare lo stato della funzionalità di gestione dell'alimentazione su un client Gestione configurazione.

Eseguire **PowerVwr.exe** come amministratore. Quando viene avviato lo strumento, vengono visualizzati le funzionalità di alimentazione e le impostazioni di risparmio energia del computer locale nella scheda **Power Config**. 

Per visualizzare i dati relativi al risparmio energia di un computer remoto:  

1. Passare al menu **File** e fare clic su **Connessione**. 

2. Immettere il nome **computer** e un **nome utente** e **password**, se necessario. 

In Power Viewer sono disponibili tre schede:  

- **Power Config**: permette di visualizzare le funzionalità di alimentazione e le impostazioni di risparmio del computer di destinazione.  

- **Attività giornaliera**: permette di visualizzare i grafici dell'attività quotidiana del client, che includono le informazioni seguenti:  

    - **Computer on**: stato di alimentazione del computer in un giorno. La modalità di sospensione viene considerata come spegnimento.  

    - **Monitor acceso**: stato acceso o spento del monitor in un giorno.  

    - **Attività utente**: informazioni sull'attività dell'utente in un giorno.  

- **Eventi di risparmio energia**: consente di visualizzare tutti gli eventi di risparmio energia giornalieri. Il client riepiloga questi eventi alle ore 12:00. Questo riepilogo genera dati per il grafico attività giornaliere.  
