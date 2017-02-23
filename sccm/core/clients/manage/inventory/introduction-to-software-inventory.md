---
title: Inventario software | Microsoft Docs
description: Introduzione all&quot;inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
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
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: c9956dd4ef94a1b109d761e44e42f512c42eb8d2


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

## <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario software per dispositivi mobili registrati con Microsoft Intune  
 È possibile raccogliere l'inventario per le app installate in dispositivi mobili. Le app vengono inserite nell'inventario a seconda che il dispositivo sia di proprietà dell'azienda o personale. Per quanto riguarda i dispositivi personali, le uniche app che vengono inserite nell'inventario sono quelle gestite da Microsoft Intune.  

> [!NOTE]  
>  L'inventario per le app installate in dispositivi mobili viene eseguito nell'ambito del processo di [inventario hardware](../../../../core/clients/manage/inventory/mobile-device-hardware-inventory-hybrid.md).  

 Queste sono le app incluse nell'inventario per i dispositivi personali o di proprietà dell'azienda.  

|Piattaforma|Per i dispositivi di proprietà personale|Per i dispositivi di proprietà dell'azienda|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite| 
|Windows 8.1 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite|  
|Windows Phone 8|Solo le app gestite|Solo le app gestite|  
|Windows RT|Solo le app gestite|Solo le app gestite|  
|iOS|Solo le app gestite|Tutte le app installate nel dispositivo|  
|Android|Solo le app gestite|Tutte le app installate nel dispositivo|  





<!--HONumber=Dec16_HO5-->


