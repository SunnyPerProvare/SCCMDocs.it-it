---
title: Dashboard del ciclo di vita del prodotto
titleSuffix: Configuration Manager
description: Informazioni sul dashboard del ciclo di vita del prodotto in System Center Configuration Manager.
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8f24fcd2d75d34e2d2d69c9c54f4f47991be7301
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Usare il dashboard del ciclo di vita del prodotto per gestire il criterio Ciclo di vita del prodotto Microsoft in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

A partire dalla [Technical Preview versione 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802) è possibile usare il dashboard del ciclo di vita del prodotto di Configuration Manager. Il dashboard mostra lo stato del criterio Ciclo di vita del prodotto Microsoft per i prodotti Microsoft installati nei dispositivi gestiti con Configuration Manager. Fornisce informazioni sui prodotti Microsoft in uso nell'ambiente, sullo stato del supporto e sulle date di fine del supporto. È possibile usare il dashboard per conoscere la disponibilità del supporto per ogni prodotto. Il dashboard consente anche di pianificare l'aggiornamento dei prodotti Microsoft in uso prima della fine del supporto.  

Per altre informazioni sul criterio Ciclo di vita del prodotto Microsoft, vedere [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Prerequisiti 

 Per visualizzare i dati nel dashboard del ciclo di vita del prodotto, sono necessari i requisiti seguenti: 
- Internet Explorer 9 o versione successiva deve essere installato nel computer che esegue la console di Configuration Manager. 
- Un punto di Reporting Services è necessario per il funzionamento dei collegamenti ipertestuali nel dashboard, poiché collegano a un report di SQL Server Reporting Services. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](/sccm/core/servers/manage/reporting). 
- Il punto di sincronizzazione Asset Intelligence deve essere configurato e sincronizzato. Per altre informazioni, vedere [Configurare Asset Intelligence in System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

I dati nel dashboard dipendono dall'installazione o meno del punto di sincronizzazione di Asset Intelligence. Il dashboard usa il catalogo di Asset Intelligence come metadati per i titoli dei prodotti. I metadati vengono confrontati con i dati di inventario nella gerarchia. 

>[!NOTE]
>Se si sta configurando il punto di sincronizzazione di Asset Intelligence per la prima volta, assicurarsi di [abilitare le classi dell'inventario hardware di Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). Il dashboard del ciclo di vita del prodotto dipende da queste classi di inventario hardware di Asset Intelligence e non visualizza dati fino a quando i client non eseguono un'analisi dell'hardware e restituiscono l'inventario hardware.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Usare il dashboard del ciclo di vita del prodotto Microsoft

In base ai dati di inventario raccolti dai dispositivi gestiti, il dashboard visualizza informazioni su tutti i prodotti correnti. Tuttavia le informazioni visualizzate per i sistemi operativi e SQL Server sono limitate alle versioni seguenti:

- Windows Server 2008 e versioni successive
- Windows XP e versioni successive
- SQL Server 2008 e versioni successive

Per accedere al dashboard del ciclo di vita, nella console di Configuration Manager scegliere **Asset e conformità** > **Asset Intelligence** > **Ciclo di vita del prodotto**.

>[!NOTE]
>I dati del dashboard sono basati sul sito a cui la console di Configuration Manager si connette. Se la console si connette al sito di livello superiore, vengono visualizzati i dati dell'intera gerarchia. Se si connette a un sito figlio primario, vengono visualizzati solo i dati di quel sito.

### <a name="product-lifecycle-dashboard"></a>Dashboard del ciclo di vita del prodotto

![Dashboard del ciclo di vita del prodotto](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

Il dashboard include i riquadri seguenti: 
- **Primi 5 prodotti che hanno superato la scadenza:** questo riquadro è una visualizzazione dati consolidata dei prodotti trovati nell'ambiente che hanno superato la scadenza. Il grafico mostra il software installato scaduto rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.  
- **Primi 5 prodotti che si avvicinano alla scadenza nei sei mesi successivi:** questo riquadro è una visualizzazione dati consolidata dei prodotti trovati nell'ambiente che si avvicinano alla scadenza nei sei mesi successivi. Il grafico mostra il software installato che scadrà entro sei mesi rispetto al ciclo di vita del supporto dei sistemi operativi e dei prodotti SQL Server.
- **Dati sul ciclo di vita per i prodotti installati:** questo riquadro offre un'idea generale della transizione di un prodotto dallo stato supportato allo stato scaduto. Il grafico presenta in dettaglio il numero di client in cui il prodotto è installato, lo stato di disponibilità del supporto e un collegamento ad altre informazioni sui passaggi successivi da eseguire. Nel grafico sono incluse le informazioni seguenti:     
    - Tempo rimanente per il supporto tecnico
    - Numero nell'ambiente 
    - Data di fine del supporto Mainstream
    - Data di fine del supporto " Extended"
    - Passaggi successivi 

>[!IMPORTANT]
>Le informazioni visualizzate in questo dashboard vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità del proprio ambiente. Verificare l'esattezza delle informazioni fornite e la disponibilità delle informazioni sul supporto visitando la pagina https://support.microsoft.com/en-us/lifecycle.

## <a name="reporting"></a>Reporting
I nuovi report seguenti sono stati aggiunti alla categoria **Ciclo di vita del prodotto**:
- **Panoramica generale del ciclo di vita del prodotto:** offre un elenco dei cicli di vita dei prodotti. L'elenco può essere filtrato in base al nome del prodotto e ai giorni alla scadenza definibili dall'utente. 
- **Computer con un prodotto software specifico:** visualizza un elenco dei computer in cui è stato rilevato un prodotto specifico.
- **Elenco di prodotti scaduti rilevati nell'organizzazione:** mostra i dettagli relativi ai prodotti trovati nell'ambiente con date del ciclo di vita scadute. 
- **Elenco di computer con prodotti scaduti nell'organizzazione:** visualizza i computer in cui sono installati prodotti scaduti. È possibile filtrare questo report in base al nome del prodotto.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

