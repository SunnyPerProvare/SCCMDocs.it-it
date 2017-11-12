---
title: 'Gestione dei client di un''infrastruttura VDI '
titleSuffix: Configuration Manager
description: Gestire i client di System Center Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure).
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: "7"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 1d35865895a8837d4c30a4f43967f777e61d7cbf
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Considerazioni per la gestione dei client di System Center Configuration Manager in un'infrastruttura VDI (Virtual Desktop Infrastructure)

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supporta l'installazione del client di Configuration Manager nei seguenti scenari di infrastruttura VDI:  

-   **Macchine virtuali personali**: le macchine virtuali personali vengono in genere usate quando ci si desidera assicurare che i dati e le impostazioni utente vengano mantenute sulla macchina virtuale tra le sessioni.  

-   **Sessioni di Servizi Desktop remoto**: i Servizi Desktop remoto consentono a un server di ospitare più sessioni client simultanee. Gli utenti possono connettersi a una sessione e quindi eseguire le applicazioni su tale server.  

-   **Macchine virtuali in pool**: le macchine virtuali in pool non sono persistenti tra le sessioni. Alla chiusura di una sessione tutti i dati e le impostazioni vengono rimossi. Le macchine virtuali in pool sono utili quando i Servizi Desktop remoto non possono essere usati perché un'applicazione aziendale richiesta non può essere eseguita sul Windows Server che ospita le sessioni client.  

 Nella tabella seguente è riportato l'elenco di considerazioni per la gestione del client di Configuration Manager in un'infrastruttura VDI.  

|Tipo di macchina virtuale|Considerazioni|  
|--------------------------|--------------------|  
|Macchine virtuali personali|Configuration Manager considera le macchine virtuali personali in modo identico a un computer fisico. Il client di Configuration Manager può essere preinstallato sull'immagine della macchina virtuale o distribuito dopo il provisioning della macchina virtuale.|  
|Servizi Desktop remoto|Il client di Configuration Manager non viene installato per singole sessioni di Desktop remoto. Al contrario, il client viene installato solo una volta sul server dei Servizi Desktop remoto. Tutti le funzionalità di Configuration Manager possono essere usate nel server dei Servizi Desktop remoto.|  
|Macchine virtuali in pool|Quando viene effettuata la rimozione di una macchina virtuale in pool, vengono perse tutte le modifiche effettuate usando Configuration Manager .<br /><br /> I dati restituiti dalle funzionalità di Configuration Manager , come l'inventario hardware, l'inventario software e il controllo software potrebbero non essere rilevanti per le esigenze dell'utente, mentre la macchina virtuale potrebbe essere operativa solo per un breve periodo di tempo. Prendere in considerazione l'esclusione delle macchine virtuali in pool dalle attività di inventario.|  

 Poiché la virtualizzazione supporta l'esecuzione di più client di Configuration Manager sullo stesso computer fisico, molte operazioni client hanno un ritardo casuale incorporato per azioni pianificate come l'inventario hardware e l'inventario software, le scansioni antimalware, le installazioni software e le scansioni di aggiornamento software. Questo ritardo consente di distribuire l'elaborazione della CPU e il trasferimento dei dati per un computer che ha più macchine virtuali con il client di Configuration Manager in esecuzione.  

> [!NOTE]  
>  Con l'eccezione dei client di Windows Embedded che sono in modalità di manutenzione, anche i client di Configuration Manager che non sono in esecuzione in ambienti virtualizzati usano il ritardo casuale. Quando si è eseguita la distribuzione di molti client, questo comportamento consente di evitare dei picchi nella larghezza di banda di rete e riduce il requisito di elaborazione CPU nei sistemi del sito di Configuration Manager, come il punto di gestione e il server del sito. L'intervallo di ritardo varia in base alle funzionalità di Configuration Manager.  
>   
>  Il ritardo casuale è disabilitato per impostazione predefinita per le distribuzioni di applicazioni e gli aggiornamenti software richiesti usando le impostazioni client seguenti: **Agente computer**: **Disabilitare sequenza casuale scadenza**.
