---
title: Sicurezza e privacy per Asset Intelligence | System Center Configuration Manager
description: Informazioni sulla sicurezza e la privacy per Asset Intelligence in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 85e0b6e3a96852cbf9c8781a3124bff13a6c6fdd


---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>Sicurezza e privacy per Asset Intelligence in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento vengono illustrate informazioni sulla sicurezza e la privacy per Asset Intelligence in System Center Configuration Manager.  

##  <a name="a-namebkmksecurityaia-security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Procedura consigliate per la sicurezza per Asset Intelligence  
 Usare le procedure consigliate per la sicurezza seguenti per i casi in cui si usa Asset Intelligence.  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Quando si importa un file di licenza (file Microsoft Volume Licensing o file di resoconto licenze generale), proteggere il file e il canale di comunicazione.|Usare le autorizzazioni del file system NTFS per garantire che solo gli utenti autorizzati possano accedere ai file di licenza e usare firme Server Message Block (SMB) per assicurare l'integrità dei dati quando vengono trasferiti al server del sito durante il processo di importazione.|  
|Usare il principio di autorizzazione con privilegi minimi per importare i file di licenza.|Usare l'amministrazione basata su ruoli per concedere l'autorizzazione Gestisci Asset Intelligence all'utente amministratore che importa i file di licenza. Il ruolo predefinito di Gestione asset include questa autorizzazione.|  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per Asset Intelligence  
 Asset Intelligence estende le funzionalità di inventario di Configuration Manager in modo da offrire un livello maggiore di visibilità delle risorse nell'azienda. La raccolta di informazioni di Asset Intelligence non è abilitata automaticamente. È possibile modificare il tipo di informazioni raccolte abilitando le classi di report di inventario hardware. Per altre informazioni, vedere [Configurazione di Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Le informazioni di Asset Intelligence vengono archiviate nel database di Configuration Manager analogamente alle informazioni relative all'inventario. Quando i client si connettono ai punti di gestione tramite HTTPS, i dati vengono sempre crittografati durante il trasferimento al punto di gestione. Quando i client si connettono tramite HTTP, è possibile configurare il trasferimento dei dati di inventario in modo che i dati siano firmati e crittografati. I dati di inventario non vengono archiviati in formato crittografato nel database. Le informazioni vengono mantenute nel database fino a quando non vengono eliminate, ogni 90 giorni, dall'attività di manutenzione del sito **Elimina cronologia inventario obsoleta** . È possibile configurare l'intervallo di eliminazione.  

 Asset Intelligence non invia a Microsoft informazioni su utenti e computer o sull'utilizzo delle licenze. È possibile scegliere di inviare a System Center Online richieste per la categorizzazione, ovvero contrassegnare uno o più titoli software non categorizzati e inviarli a System Center Online per la ricerca e la categorizzazione. Una volta caricato un titolo software, i ricercatori Microsoft identificano, categorizzano e rendono disponibili le informazioni a tutti i clienti che usano il servizio online. È consigliabile considerare le implicazioni per la privacy seguenti relative all'invio di informazioni a System Center Online:  

-   Il caricamento si applica solo alle informazioni dei titoli software generiche (nome, autore e così via) che si sceglie di inviare a System Center Online. Le informazioni relative all'inventario non vengono inviate con un caricamento.  

-   Il caricamento non avviene mai automaticamente e il sistema non è progettato per l'automatizzazione di questa attività. È necessario selezionare manualmente e approvare il caricamento di ogni titolo di software.  

-   Prima che venga avviato il processo di caricamento, una finestra di dialogo mostra esattamente quali dati verranno caricati.  

-   Le informazioni sulle licenze non vengono inviate a Microsoft. Le informazioni sulle licenze vengono archiviate in un'area separata del database di Configuration Manager e non possono essere inviate a Microsoft.  

-   Tutti i titoli software caricati diventano pubblici, nel senso che le informazioni su una determinata applicazione e la relativa categorizzazione diventano parte del catalogo di Asset Intelligence in System Center Online e possono quindi essere scaricate da altri utenti del catalogo.  

-   L'origine del titolo software non viene registrata nel catalogo di Asset Intelligence e non viene resa disponibile agli altri clienti. È comunque necessario verificare di non caricare alcun titolo di applicazione che contiene informazioni private.  

-   Non è possibile annullare il caricamento dei dati selezionati.  

 Prima di configurare la raccolta dati di Asset Intelligence e di scegliere se inviare informazioni a System Center Online, prendere in considerazione i requisiti per la privacy della propria organizzazione.  



<!--HONumber=Nov16_HO1-->

