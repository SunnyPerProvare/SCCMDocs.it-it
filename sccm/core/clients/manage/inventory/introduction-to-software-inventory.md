---
title: Inventario software
titleSuffix: Configuration Manager
description: Introduzione all'inventario software in System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fe27423391cbdc4767e18a06c73b23cbb302ab5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introduzione all'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare l'inventario software per raccogliere informazioni sui file nei dispositivi client. L'inventario software consente anche di raccogliere i file dai dispositivi client e archiviarli nel server del sito. La raccolta dell'inventario software viene eseguita quando si sceglie l'impostazione **Abilitare inventario software nei client** nelle impostazioni client, dove è anche possibile pianificare l'operazione.  

Dopo aver abilitato l'inventario software e completato l'esecuzione di un ciclo di inventario software, il client invia le informazioni a un punto di gestione nel sito del client. Il punto di gestione inoltra quindi le informazioni di inventario al server del sito di Configuration Manager, che archivia tali informazioni nel database del sito.   

 Questi sono i modi disponibili per visualizzare i dati dell'inventario software:  

-   [Creare query](../../../../core/servers/manage/queries-technical-reference.md) che restituiscono i dispositivi con i file specificati.   

-   Creare [raccolte basate su query](../../../../core/clients/manage/collections/introduction-to-collections.md) che includono dispositivi con i file specificati.   

-   [Eseguire report](../../../../core/servers/manage/reporting.md) che forniscono dettagli sui file nei dispositivi.

-   Usare [Esplora inventario risorse](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) per visualizzare informazioni dettagliate relative ai file di inventario raccolti dai dispositivi client.   

 Quando si esegue l'inventario software in un dispositivo client, il primo report è un inventario completo. I report successivi contengono solo informazioni di inventario differenziale. Il server del sito elabora le informazioni differenziali in ordine di ricezione. Se mancano le informazioni differenziali per un client, il server del sito rifiuta informazioni differenziali aggiuntive e indica al client di eseguire un ciclo di inventario completo.  

 Configuration Manager può individuare i computer ad avvio doppio ma restituisce solo le informazioni di inventario relative al sistema operativo attivo nel momento in cui è stato eseguito l'inventario.  

**Dispositivi mobili:** per informazioni sulla raccolta delle informazioni di inventario per le app installate nei dispositivi mobili, vedere [Inventario software per dispositivi mobili registrati con Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md).
