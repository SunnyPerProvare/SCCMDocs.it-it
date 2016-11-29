---
title: Inventario hardware | System Center Configuration Manager
description: Introduzione all'inventario hardware in System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6a0addd31f6e8cd7ef91303cc664d9242c22e0f2


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introduzione all'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare l'inventario hardware in System Center Configuration Manager per raccogliere informazioni relative alla configurazione hardware dei dispositivi client nell'organizzazione. Per raccogliere l'inventario hardware, nelle impostazioni client l'impostazione **Abilitare inventario hardware nei client** deve essere abilitata.  

 Dopo che l'inventario hardware è stato abilitato e il client ha eseguito un ciclo di inventario hardware, il client invia le informazioni di inventario raccolte a un punto di gestione nel sito del client. Il punto di gestione inoltra quindi le informazioni di inventario al server del sito di Configuration Manager, che archivia tali informazioni nel database del sito stesso. L'inventario hardware nei client viene eseguito in base alla pianificazione specificata nelle impostazioni client.  

 È possibile usare diversi metodi per visualizzare i dati di inventario hardware raccolti da Configuration Manager, tra cui:  

-   Creare query che restituiscono i dispositivi basati su una configurazione hardware specifica. Per altre informazioni, vedere [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Riferimento tecnico per le query per System Center Configuration Manager).  

-   Creare raccolte basate su query secondo una configurazione hardware specifica. Le appartenenze alle raccolte basate su query vengono aggiornate automaticamente in base a una pianificazione. È possibile usare le raccolte per numerose attività, tra cui la distribuzione software. Per altre informazioni, vedere [Collections technical reference for System Center Configuration Manager](../../../../core/clients/manage/collections/collections-technical-reference.md) (Riferimento tecnico per le raccolte per System Center Configuration Manager).  

-   Eseguire i report che consentono di visualizzare informazioni dettagliate specifiche sulle configurazioni hardware all'interno dell'organizzazione. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Usare Esplora inventario risorse per visualizzare informazioni dettagliate relative all'inventario hardware raccolto con l'analisi dei dispositivi client. Per altre informazioni, vedere [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) (Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager).  

 Quando si esegue l'inventario hardware in un dispositivo client, i primi dati di inventario restituiti dal client costituiscono sempre l'inventario completo. Le informazioni degli inventari successivi sono solo informazioni di inventario differenziale. Il server del sito elabora le informazioni di inventario differenziale nell'ordine di ricezione. Se le informazioni di inventario differenziale per un client mancano, il server del sito rifiuta informazioni di inventario differenziale aggiuntive e indica al client di eseguire un ciclo di inventario completo.  

 Configuration Manager offre un supporto limitato per i computer ad avvio doppio. Configuration Manager può individuare i computer ad avvio doppio ma restituisce solo le informazioni di inventario relative al sistema operativo attivo al momento dell'esecuzione del ciclo di inventario.  

> [!NOTE]  
>  Per informazioni su come usare l'inventario hardware con i client che eseguono Linux e UNIX, vedere [Inventario hardware per Linux e UNIX in Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Estensione dell'inventario hardware di Configuration Manager  
 Oltre all'inventario hardware predefinito in Configuration Manager è possibile usare uno dei metodi seguenti per estendere l'inventario hardware e raccogliere informazioni aggiuntive:  

|Metodo|Descrizione|  
|------------|-----------------|  
|Aggiungere e rimuovere classi di inventario dalla console di Configuration Manager|In Configuration Manager è possibile abilitare, disabilitare, aggiungere e rimuovere classi di inventario per l'inventario hardware dalla console di Configuration Manager.|  
|File NOIDMIF|Usare file NOIDMIF per raccogliere informazioni sui dispositivi client che non possono essere inclusi nell'inventario da Configuration Manager. È ad esempio raccogliere informazioni sul numeri dispositivo asset che esiste solo come un'etichetta sul dispositivo. L'inventario NOIDMIF viene associato automaticamente al dispositivo client da cui è stato raccolto.|  
|File IDMIF|Usare i file IDMIF per raccogliere informazioni sulle risorse dell'organizzazione non associate a un client di Configuration Manager, ad esempio proiettori, fotocopiatrici e stampanti di rete.|  

 Per informazioni su come usare questi metodi per estendere l'inventario hardware di Configuration Manager, vedere [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md) (Come configurare l'inventario hardware in System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


