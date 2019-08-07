---
title: Creare gruppi di applicazioni
titleSuffix: Configuration Manager
description: Creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2698105d125abbbf1354cb045753586899e003ba
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537659"
---
# <a name="create-application-groups"></a>Creare gruppi di applicazioni

<!--3555907-->

A partire dalla versione 1906, creare un gruppo di applicazioni che è possibile inviare a un utente o a una raccolta di dispositivi come singola distribuzione. I metadati specificati in relazione al gruppo di app sono visualizzati in Software Center come una singola entità. È possibile ordinare le app del gruppo in modo che il client le installi in un ordine specifico.

> [!Note]  
> In questa versione di Configuration Manager, i gruppi di app sono in una versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**. Espandere **Gestione applicazioni** e selezionare il nodo **Gruppo applicazioni**.  

1. Nel gruppo Crea della barra multifunzione selezionare **Crea gruppo di applicazioni**.

1. Nella pagina **Informazioni generali** specificare le informazioni sul gruppo di app.  

1. Nella pagina **Software Center** includere le informazioni visualizzate in Software Center.  

1. Nella pagina **Gruppo di applicazioni** selezionare **Aggiungi**. Selezionare una o più app per questo gruppo. Riordinarle usando le azioni **Sposta su** e **Sposta giù**.  

1. Completare la procedura guidata.  

Distribuire il gruppo di app seguendo la stessa procedura usata per un'applicazione. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](/sccm/apps/deploy-use/deploy-applications).

Se si aggiunge una nuova app al gruppo dopo aver distribuito il gruppo, è necessario distribuire separatamente il nuovo contenuto dell'app nei punti di distribuzione.

Per risolvere i problemi relativi alla distribuzione di un gruppo di app, usare i file di log seguenti nel client:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> Non creare o distribuire un gruppo di app fino a quando non si aggiorna l'intera gerarchia e i client di destinazione almeno alla versione 1906.

### <a name="known-issues"></a>Problemi noti

- Le app del gruppo possono contenere solo tipi di distribuzione **Windows Installer** o **script** . Impostare il comportamento di installazione del tipo di distribuzione per **installare per il sistema**.
- È possibile distribuire il gruppo di app solo in una raccolta di dispositivi.
