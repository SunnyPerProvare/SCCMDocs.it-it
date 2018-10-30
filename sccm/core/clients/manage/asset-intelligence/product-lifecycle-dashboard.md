---
title: Dashboard del ciclo di vita del prodotto
titleSuffix: Configuration Manager
description: Visualizzare i criteri del ciclo di vita Microsoft con il dashboard del ciclo di vita del prodotto in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd1a3a56bac6d7917c70db731b1735a195fae3df
ms.sourcegitcommit: dfb2cb01c1608b848f2f2fee7c84500e7adcb7a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2018
ms.locfileid: "49101246"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gestire i criteri del ciclo di vita Microsoft con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1806 è possibile usare il dashboard del ciclo di vita del prodotto di Configuration Manager per visualizzare i criteri del ciclo di vita Microsoft. Il dashboard mostra lo stato dei criteri del ciclo di vita Microsoft per i prodotti Microsoft installati nei dispositivi gestiti con Configuration Manager. Fornisce informazioni sui prodotti Microsoft in uso nell'ambiente, sullo stato del supporto e sulle date di fine del supporto. Usare il dashboard per conoscere la disponibilità del supporto per ogni prodotto. Queste informazioni consentono anche di pianificare l'aggiornamento dei prodotti Microsoft in uso prima del raggiungimento della fine del supporto.  

Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).



## <a name="prerequisites"></a>Prerequisiti 

 Per visualizzare i dati nel dashboard del ciclo di vita del prodotto, sono necessari i componenti seguenti:  

- Internet Explorer 9 o versione successiva deve essere installato nel computer che esegue la console di Configuration Manager.  

- Un punto di Reporting Services è necessario per la funzionalità di collegamento ipertestuale nel dashboard. Il dashboard è collegato ai report di SQL Server Reporting Services (SSRS). Per altre informazioni, vedere [Creazione di report in Configuration Manager](/sccm/core/servers/manage/reporting).  

- Il punto di sincronizzazione di Asset Intelligence deve essere configurato e sincronizzato. Il dashboard usa il catalogo di Asset Intelligence come metadati per i titoli dei prodotti. I metadati vengono confrontati con i dati di inventario nella gerarchia. Per altre informazioni, vedere [Configurare Asset Intelligence in Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

     > [!NOTE]  
     > Se si sta configurando il punto di sincronizzazione di Asset Intelligence per la prima volta, assicurarsi di [abilitare le classi di inventario hardware di Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). Il dashboard del ciclo di vita dipende da tali classi di inventario hardware di Asset Intelligence. Il dashboard non mostrerà dati fino a quando i client non saranno stati analizzati e non sarà stato restituito l'inventario hardware.  



## <a name="use-the-product-lifecycle-dashboard"></a>Usare il dashboard del ciclo di vita del prodotto

In base ai dati di inventario che il sito raccoglie dai dispositivi gestiti, il dashboard visualizza informazioni su tutti i prodotti correnti. Tuttavia le informazioni visualizzate per i sistemi operativi e SQL Server sono limitate alle versioni seguenti:

- Windows Server 2008 e versioni successive
- Windows XP e versioni successive
- SQL Server 2008 e versioni successive

Per accedere al dashboard del ciclo di vita, nella console di Configuration Manager scegliere l'area di lavoro **Asset e conformità**, espandere **Asset Intelligence** e selezionare il nodo **Ciclo di vita del prodotto**.

> [!NOTE]  
> I dati del dashboard sono basati sul sito a cui la console di Configuration Manager si connette. Se la console si connette al sito di livello superiore, vengono visualizzati i dati dell'intera gerarchia. Se si connette a un sito figlio primario, vengono visualizzati solo i dati di quel sito.

### <a name="product-lifecycle-dashboard"></a>Dashboard del ciclo di vita del prodotto

![Screenshot del dashboard del ciclo di vita del prodotto nella console](media/product-lifecycle-dashboard.png)

Il dashboard include i riquadri seguenti:  

- **Primi 5 prodotti che hanno superato la scadenza:** questo riquadro è una visualizzazione dati consolidata dei prodotti che hanno superato la scadenza trovati nell'ambiente. Il grafico mostra il software installato scaduto rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.  

- **Primi 5 prodotti che si avvicinano alla scadenza nei sei mesi successivi:** questo riquadro è una visualizzazione dati consolidata dei prodotti che si avvicinano alla scadenza nei 18 mesi successivi trovati nell'ambiente. Il grafico mostra il software installato che scadrà entro 18 mesi rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.  

- **Dati sul ciclo di vita per i prodotti installati:** questo riquadro offre un'idea generale della transizione di un prodotto dallo stato supportato allo stato scaduto. Il grafico presenta in dettaglio il numero di client in cui il prodotto è installato, lo stato di disponibilità del supporto e un collegamento ad altre informazioni sui passaggi successivi da eseguire. Nel grafico sono incluse le informazioni seguenti:     
    - Tempo rimanente per il supporto tecnico
    - Numero nell'ambiente 
    - Data di fine del supporto Mainstream
    - Data di fine del supporto " Extended"
    - Passaggi successivi  

> [!IMPORTANT]  
> Le informazioni visualizzate in questo dashboard vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità del proprio ambiente. Verificare l'esattezza delle informazioni fornite e la disponibilità delle informazioni sul supporto visitando la pagina [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Reporting

Sono disponibili anche report aggiuntivi. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e quindi espandere **Report**. I nuovi report seguenti sono stati aggiunti alla categoria **Ciclo di vita del prodotto**:  

- **Panoramica generale del ciclo di vita del prodotto:** offre un elenco dei cicli di vita dei prodotti. Filtrare l'elenco in base al nome del prodotto e ai giorni mancanti alla scadenza.  

- **Computer con un prodotto software specifico:** visualizza un elenco dei computer in cui è stato rilevato un prodotto specifico.  

- **Elenco di prodotti scaduti rilevati nell'organizzazione:** mostra i dettagli relativi ai prodotti trovati nell'ambiente con date del ciclo di vita scadute.  

- **Elenco di computer con prodotti scaduti nell'organizzazione:** visualizza i computer in cui sono installati prodotti scaduti. È possibile filtrare questo report in base al nome del prodotto.

