---
title: Inventario software | Microsoft Docs
description: Introduzione all&quot;inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a468ce93e9536fe3f6bf0fc191ff9764dd1c3343
ms.openlocfilehash: 401ba6e37d740310d49ab9e96112ce576d7130e4


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introduzione all'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare l'inventario software in System Center Configuration Manager per raccogliere informazioni relative ai file contenuti nei dispositivi client dell'organizzazione. Inoltre, l'inventario software può raccogliere i file dai dispositivi client e archiviarli nel server del sito. L'inventario software viene raccolto quando nelle impostazioni client l'impostazione **Abilitare inventario software nei client** è abilitata.  

 Dopo che l'inventario software è stato abilitato e i client hanno eseguito un ciclo di inventario software, il client invia le informazioni di inventario a un punto di gestione nel sito del client. Il punto di gestione inoltra quindi le informazioni di inventario al server del sito di Configuration Manager, che archivia tali informazioni nel database del sito stesso. L'inventario software viene eseguito nei client in base alla pianificazione specificata nelle impostazioni client.  

 È possibile usare numerosi metodi per visualizzare i dati di inventario software raccolti da Configuration Manager, tra cui:  

-   Creare query che restituiscono i dispositivi basati su file presenti nei dispositivi specificati. Per altre informazioni, vedere [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Riferimento tecnico per le query per System Center Configuration Manager).  

-   Creare raccolte basate su query basate su file presenti nei dispositivi specificati. Le appartenenze alle raccolte basate su query vengono aggiornate automaticamente in base a una pianificazione. È possibile usare le raccolte per una serie di attività quali la distribuzione software. Per altre informazioni, vedere [Introduzione alle raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

-   Eseguire i report che consentono di visualizzare informazioni dettagliate specifiche sui dispositivi all'interno dell'organizzazione. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

-   Usare Esplora inventario risorse per visualizzare informazioni dettagliate relative ai file di inventario raccolti dai dispositivi client. Per altre informazioni, vedere [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) (Come usare Esplora inventario risorse per visualizzare l'inventario software in Configuration Manager).  

 Quando si esegue l'inventario software in un dispositivo client, il primo report restituito costituisce sempre l'inventario completo. I report inventario successivi contengono solo informazioni di inventario differenziale. Il server del sito elabora le informazioni di inventario differenziale nell'ordine di ricezione. Se le informazioni di inventario differenziale per un client mancano, il server del sito rifiuta altre informazioni di inventario differenziale e indica al client di eseguire un ciclo di inventario completo.  

 Configuration Manager offre un supporto limitato per i computer ad avvio doppio. Configuration Manager può individuare i computer ad avvio doppio ma restituisce solo le informazioni di inventario relative al sistema operativo attivo nel momento in cui è stato eseguito l'inventario.  

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario software per dispositivi mobili registrati con Microsoft Intune  
 È possibile raccogliere l'inventario in app installate nei dispositivi mobili. Le app vengono inserite nell'inventario a seconda che il dispositivo sia di proprietà dell'azienda o personale. Per quanto riguarda i dispositivi personali, le uniche app che vengono inserite nell'inventario sono quelle gestite da Microsoft Intune.  

> [!NOTE]  
>  L'inventario nelle app installate in dispositivi mobili viene eseguito nell'ambito del processo di inventario hardware in Configuration Manager. Per altre informazioni, vedere [How to Configure Hardware Inventory for Mobile Devices Enrolled by Microsoft Intune and Configuration Manager](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md) (Come configurare l'inventario hardware per i dispositivi mobili registrati tramite Microsoft Intune e System Center Configuration Manager).  

 Nella tabella seguente sono elencate le app di inventario per i dispositivi di proprietà personale o dell'azienda.  

|Piattaforma|Per i dispositivi di proprietà personale|Per i dispositivi di proprietà dell'azienda|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite| 
|Windows 8.1 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite|  
|Windows Phone 8|Solo le app gestite|Solo le app gestite|  
|Windows RT|Solo le app gestite|Solo le app gestite|  
|iOS|Solo le app gestite|Tutte le app installate nel dispositivo|  
|Android|Solo le app gestite|Tutte le app installate nel dispositivo|  



<!--HONumber=Dec16_HO3-->


