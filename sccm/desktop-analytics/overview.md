---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Una panoramica del servizio Desktop Analitica integrato con Configuration Manager.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 78e9454212bb8264926c1aba5262f06db1798abe
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673432"
---
# <a name="what-is-desktop-analytics"></a>Che cos'è Analitica Desktop?

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analitica è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio fornisce informazioni dettagliate e intelligence per poter prendere decisioni più informate sulla conformità di aggiornamento dei client di Windows. Combina i dati dell'organizzazione con dati aggregati provenienti da milioni di dispositivi connessi ai servizi cloud Microsoft.

Usare Desktop Analitica con Configuration Manager per:  

- Creare un inventario delle App in esecuzione all'interno dell'organizzazione  

- Valutare la compatibilità delle app con gli ultimi aggiornamenti di funzionalità di Windows 10  

- Identificare i problemi di compatibilità e ricevere i suggerimenti di mitigazione basate su informazioni dettagliate sui dati abilitata per il cloud  

- Creare gruppi pilota che rappresentano l'estate intera applicazione e il driver in un set minimo di dispositivi  

- Distribuire Windows 10 nei dispositivi pilota e di produzione gestite  

![Screenshot della home page del Desktop Analitica nel portale di Azure](media/portal-home.png)

> [!Note]  
> Desktop Analitica è il successore di Analitica di Windows. Il *Analitica Windows* service include Upgrade Readiness, conformità degli aggiornamenti e integrità del dispositivo.
>
> Tutte queste funzionalità vengono combinate nel *Analitica Desktop* servizio. Desktop Analitica inoltre è più strettamente integrato con Configuration Manager.



## <a name="benefits"></a>Vantaggi

Molti clienti hanno difficoltà di recupero e rimanere aggiornati con Windows 10. La sfida principale sta testando le applicazioni. Questo processo è in genere manuale. È molto tempo per gli amministratori IT e i proprietari dell'applicazione analizzare continuamente le applicazioni esistenti. Quindi, correggere eventuali problemi riscontrati.

Analitica desktop offre i vantaggi seguenti:

- **L'inventario software e dispositivo**: Inventario dei fattori chiave quali App e le versioni di Windows.  

- **Avviare un programma pilota identificazione**: Identificazione del set più piccolo di dispositivi che forniscono la copertura più ampia di fattori. Ma illustra i fattori più importanti per un progetto pilota di Windows gli aggiornamenti. Assicurandosi che il progetto pilota è più riuscito consente di procedere in modo più rapido e sicuro per ampie distribuzioni nell'ambiente di produzione.  

- **Emettere identificazione**: Usa i dati aggregati insieme ai dati dall'ambiente in uso, il servizio consente di prevedere potenziali problemi di recupero e rimanere aggiornati con Windows. Quindi suggerisce possibili soluzioni.  

- **Integrazione di Configuration Manager**: Il servizio cloud-Abilita l'infrastruttura locale esistente. Usare tali dati e analisi per distribuire e gestire Windows nei dispositivi.  



## <a name="prerequisites"></a>Prerequisiti

Per usare Desktop Analitica, assicurarsi che l'ambiente soddisfi i prerequisiti seguenti.


### <a name="technical"></a>Tecnici

- Una sottoscrizione di Azure attiva con [amministratore globale](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) autorizzazioni  

    - **Proprietario dell'area di lavoro** oppure **collaboratore** delle autorizzazioni per **impostare l'area di lavoro**e i ruoli seguenti:  

       - [**Desktop Administrator Analitica** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) ruolo.

       - [**Log Analitica per i collaboratori** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) e [ **amministratore accesso utenti** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) sul gruppo di risorse da usare un'area di lavoro o crearne una nuova area di lavoro in un gruppo di risorse esistente.

        - [**Proprietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), o [ **collaboratore** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) e [ **amministratore accesso utenti** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) le autorizzazioni per il sottoscrizione per creare un'area di lavoro in un nuovo gruppo di risorse.  

- Configuration Manager, versione 1810 con aggiornamento cumulativo 2 (4488598) o versione successiva. Per altre informazioni, vedere [aggiornamento Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Amministratore completo** ruoli in Configuration Manager  

- Dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10  

    - Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [aggiornare i dispositivi](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Inoltre necessario che nei dispositivi client di Configuration Manager, versione 1810 con aggiornamento cumulativo 2 (4488598) o versione successiva. Per altre informazioni, vedere [aggiornamento Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

- Dati di diagnostica di Windows. Per altre informazioni, vedere gli articoli seguenti:  

    - [Livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Desktop sulla privacy di Analitica](/sccm/desktop-analytics/privacy)  

- Connettività di rete dai dispositivi al cloud pubblico Microsoft. Per altre informazioni, vedere [come abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Licenza

Analitica desktop richiede una delle seguenti sottoscrizioni licenza:

- Windows 10 Enterprise E3 o E5; o Microsoft 365 F1 E3 o E5  

- Windows 10 Education A3 o A5; o Microsoft 365 A3 o A5  

- Windows VDA E3 o E5  




## <a name="next-steps"></a>Passaggi successivi

L'esercitazione seguente offre una Guida dettagliata di introduzione a Desktop Analitica e Configuration Manager:  

- [Distribuire Windows 10 in un progetto pilota](/sccm/desktop-analytics/tutorial-windows10)  
