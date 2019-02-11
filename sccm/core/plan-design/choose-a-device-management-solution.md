---
title: Scegliere una soluzione di gestione dei dispositivi
titleSuffix: Configuration Manager
description: Informazioni sulle soluzioni di Configuration Manager disponibili per la gestione di PC, server e dispositivi.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1214a5b73b3e6b1bddab8a3918ddd32af0cacb68
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570201"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Scegliere una soluzione di gestione dei dispositivi per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager offre diverse soluzioni per la gestione di PC, server e dispositivi. Scegliere la soluzione adatta all'organizzazione. Basare la decisione sulle piattaforme di dispositivi da gestire e sulle funzionalità di gestione necessarie.  


> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>Panoramica

Questo articolo illustra le quattro soluzioni di gestione dei dispositivi seguenti: 
- [Client di Configuration Manager](#bkmk_sccm)
- [Gestione di dispositivi mobili (MDM) locale con Configuration Manager](#bkmk_opmdm)
- [Co-gestione con Microsoft Intune](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

È possibile usare queste soluzioni di gestione dei dispositivi da sole o in combinazione. Ad esempio, è possibile usare l'approccio alla gestione basata su client per gestire i computer e i server dell'organizzazione e usare anche la co-gestione per gestire i portatili basati su Internet. Combinando i due approcci in questo modo, è possibile coprire tutte le esigenze di gestione dei dispositivi.  

Questo articolo contiene anche due tabelle che consentono di confrontare le soluzioni di gestione in base ai fattori seguenti: 
- [Piattaforme supportate](#bkmk_comp1)
- [Funzionalità di gestione](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Client di Configuration Manager  

Questa opzione richiede l'installazione del client di Configuration Manager nei dispositivi. Fornisce la maggior parte delle funzionalità per la gestione di PC, server e altri dispositivi nell'ambiente in uso. 

Per altre informazioni, vedere [Metodi di installazione client](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> Software MDM locale  

Questa opzione usa le funzionalità di gestione dei dispositivi incorporate in Windows 10. Anche se non è completa come la gestione basata su client, la gestione dei dispositivi mobili locale offre un approccio più semplice. Usa le risorse di Configuration Manager in locale per gestire i dispositivi.  

Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a> Co-gestione con Microsoft Intune

La co-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente al cloud di Microsoft 365. Consente di gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune. La co-gestione consente di collegare al cloud gli investimenti esistenti in Configuration Manager tramite l'aggiunta di nuove funzionalità. 

Per altre informazioni, vedere [What is co-management?](/sccm/comanage/overview) (Informazioni sulla co-gestione).  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

Questa opzione usa il connettore Exchange Server per connettere più server Exchange a Configuration Manager. Consente di centralizzare la gestione dei dispositivi che possono connettersi a Exchange ActiveSync. È possibile configurare le funzionalità di gestione dei dispositivi mobili di Exchange dalla console di Configuration Manager. Le funzionalità di esempio includono la cancellazione dei dati del dispositivo remota e il controllo delle impostazioni per più server Exchange.

Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Confrontare le soluzioni in base alle piattaforme supportate  

|Piattaforma|Client di Configuration Manager|Software MDM locale|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Sì|  
|iOS| | |Sì|  
|Mac OS X|Sì| |Sì|  
|UNIX/Linux|Sì| |Sì|  
|Windows 10|Sì|Sì|Sì|  
|Windows 10 Mobile| |Sì|Sì|  
|Windows (versioni precedenti)|Sì| |Sì|  
|Windows Server|Sì| |Sì|  
|Windows CE|Sì (con client precedente del dispositivo mobile)| |Sì|  
|Windows Embedded|Sì| | |  
|Windows Mobile| | |Sì|  

Per un elenco completo delle piattaforme supportate, vedere [Supported operating systems for clients and devices for System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md) (Sistemi operativi supportati per client e dispositivi per System Center Configuration Manager).

Microsoft consiglia di usare Intune per gestire i dispositivi mobili Android, iOS e Windows 10. Per altre informazioni, vedere [Informazioni su Microsoft Intune](https://docs.microsoft.com/intune/what-is-intune).



##  <a name="bkmk_comp2"></a> Confrontare le soluzioni in base alle funzionalità di gestione  

|Funzionalità di gestione|Client di Configuration Manager|Software MDM locale|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Sicurezza dell'infrastruttura a chiave pubblica (PKI) tra il dispositivo mobile e Configuration Manager usando l'autenticazione reciproca e SSL per crittografare i trasferimenti dei dati|Sì|Sì| |  
|Installazione client|Sì| | |  
|Supporto via Internet|Sì| | |  
|Individuazione|Sì| |Sì|  
|Inventario hardware|Sì|Sì|Sì|  
|Inventario software|Sì| |Sì|  
|Impostazioni|Sì|Sì|Sì|  
|Distribuzione software|Sì|Sì| |  
|Monitorare con il punto di stato di fallback|Sì| | |  
|Connessioni ai punti di gestione|Sì|Sì| |  
|Connessioni ai punti di distribuzione|Sì|Sì| |  
|Blocco da Configuration Manager|Sì|Sì| |  
|Inserimento in quarantena e blocco da Exchange Server (e Configuration Manager)| | |Sì|  
|Cancellazione remota| |Sì|Sì|  


