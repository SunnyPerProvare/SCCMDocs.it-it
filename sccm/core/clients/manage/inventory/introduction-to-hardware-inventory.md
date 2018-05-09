---
title: 'Inventario hardware '
titleSuffix: Configuration Manager
description: Introduzione all'inventario hardware in System Center Configuration Manager
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 688bb6dc57f5d50e1807bff40a1d1a4c66f4b349
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introduzione all'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare l'inventario hardware in System Center Configuration Manager per raccogliere informazioni relative alla configurazione hardware dei dispositivi client nell'organizzazione. Per raccogliere l'inventario hardware, nelle impostazioni client l'impostazione **Abilitare inventario hardware nei client** deve essere abilitata.  

 Dopo che l'inventario hardware è stato abilitato e il client ha eseguito un ciclo di inventario hardware, il client invia le informazioni di inventario a un punto di gestione nel sito del client. Il punto di gestione inoltra quindi le informazioni di inventario al server del sito di Configuration Manager, che archivia tali informazioni nel database del sito stesso. L'inventario hardware nei client viene eseguito in base alla pianificazione specificata nelle impostazioni client.  

 È possibile usare diversi metodi per visualizzare i dati di inventario hardware raccolti da Configuration Manager, tra cui:  

-   [Creare query che restituiscono i dispositivi basati su una configurazione hardware specifica](../../../../core/servers/manage/queries-technical-reference.md).  

-   [Creare raccolte basate su query secondo una configurazione hardware specifica](../../../../core/clients/manage/collections/introduction-to-collections.md). Le appartenenze alle raccolte basate su query vengono aggiornate automaticamente in base a una pianificazione. È possibile usare le raccolte per numerose attività, tra cui la distribuzione software. .  

-   [Eseguire i report che consentono di visualizzare informazioni dettagliate specifiche sulle configurazioni hardware all'interno dell'organizzazione](../../../../core/servers/manage/reporting.md).   

-   [Usare Esplora inventario risorse](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) per visualizzare informazioni dettagliate relative all'inventario hardware raccolto dai dispositivi client.   

 Quando si esegue l'inventario hardware in un dispositivo client, i primi dati di inventario restituiti dal client costituiscono sempre l'inventario completo. Le informazioni degli inventari successivi sono solo informazioni di inventario differenziale. Il server del sito elabora le informazioni di inventario differenziale nell'ordine di ricezione. Se le informazioni differenziali per un client mancano, il server del sito rifiuta informazioni differenziali aggiuntive e indica al client di eseguire un ciclo di inventario completo.  

 Configuration Manager offre un supporto limitato per i computer ad avvio doppio. Configuration Manager può individuare i computer ad avvio doppio ma restituisce solo le informazioni di inventario relative al sistema operativo attivo al momento dell'esecuzione del ciclo di inventario.  

> [!NOTE]  
>  Per informazioni su come usare l'inventario hardware con i client che eseguono Linux e UNIX, vedere [Inventario hardware per Linux e UNIX in Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Estensione dell'inventario hardware di Configuration Manager  
 Oltre all'inventario hardware predefinito in Configuration Manager è possibile usare uno dei metodi seguenti per estendere l'inventario hardware e raccogliere informazioni aggiuntive:  

- È possibile abilitare, disabilitare, aggiungere e rimuovere classi di inventario per l'inventario hardware dalla console di Configuration Manager.  
- Usare file NOIDMIF per raccogliere informazioni sui dispositivi client che non possono essere inclusi nell'inventario da Configuration Manager. È ad esempio raccogliere informazioni sul numeri dispositivo asset che esiste solo come un'etichetta sul dispositivo. Inventario NOIDMIF viene associato automaticamente al dispositivo raccolti dai client.  
- Usare i file IDMIF per raccogliere informazioni sugli asset non associati a un client di Configuration Manager, ad esempio proiettori, fotocopiatrici e stampanti di rete.  

 Per informazioni su come usare questi metodi per estendere l'inventario hardware di Configuration Manager, vedere [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware in System Center Configuration Manager).  
