---
title: Elementi deprecati per i server del sito
titleSuffix: Configuration Manager
description: Informazioni su prodotti e sistemi operativi che Configuration Manager non supporta più per i server del sito.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a1a15d803077f183897f182ef162d36896eb238a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126455"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Elementi rimossi e deprecati per i server del sito di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive i prodotti e i sistemi operativi rimossi dal supporto per i server del sito di Configuration Manager o che verranno rimossi in un aggiornamento futuro (deprecati). Anticipa informazioni sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni possono cambiare in futuro. Potrebbero non includere tutte le funzionalità, i prodotti o i sistemi operativi deprecati.  



## <a name="server-os"></a>Sistema operativo server  

|**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso** |  
|-|-|-| 
|Windows Server 2008 R2 con SP1|10 luglio 2015| Versione 1702 <sup>[Nota 1](#bkmk_note1)</sup>| 
|Windows Server 2008 con SP2|10 luglio 2015|Versione 1511 <sup>[Nota 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> Nota 1: Windows Server 2008 R2 con SP1
Windows Server 2008 R2 con Service Pack 1 non è supportato per i server del sito o la maggior parte dei ruoli del sistema del sito. Questo sistema operativo è ancora supportato per il ruolo del punto di distribuzione. Questo supporto include punti di distribuzione pull, PXE e multicast. 

> [!Important]  
> La data di fine del supporto "Extended" per Windows Server 2008 R2 con SP1 è il 14 gennaio 2020. Dopo questa data Configuration Manager non supporterà questo sistema operativo in nessun ruolo del sistema del sito. 

È possibile aggiornare il sistema operativo dei server del sito da Windows Server 2008 R2 a Windows Server 2012 R2. Per altre informazioni, vedere [Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Nota 2: Windows Server 2008 con SP2
Windows Server 2008 con Service Pack 2 non è supportato per i server del sito o la maggior parte dei ruoli del sistema del sito. Questo sistema operativo è ancora supportato per il ruolo del punto di distribuzione. Questo supporto include punti di distribuzione pull, PXE e multicast. 

> [!Important]  
> La data di fine del supporto "Extended" per Windows Server 2008 con SP2 è il 14 gennaio 2020. Dopo questa data Configuration Manager non supporterà questo sistema operativo in nessun ruolo del sistema del sito.  



## <a name="sql-server"></a>SQL Server   

|**Versioni di SQL Server**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|   
|-|-|-| 
|SQL Server 2008 R2|10 luglio 2015|Versione 1702| 
|SQL Server 2008|10 luglio 2015|Versione 1511|  


Se è necessario aggiornare la versione di SQL Server, è consigliabile usare i metodi seguenti, dal più semplice al più complesso:

1. [Aggiornare SQL Server sul posto](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (scelta consigliata).  

2. Installare una nuova versione di SQL Server in un nuovo computer. Quindi per fare in modo che il server del sito punti alla nuova versione di SQL server, [usare l'opzione di spostamento del database](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) delle impostazioni di Configuration Manager.  

3. Usare le funzionalità di [backup e ripristino](/sccm/protect/understand/backup-and-recovery).  



## <a name="more-information"></a>Altre informazioni

Per altre informazioni, vedere gli articoli seguenti: 

- [Elementi rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle)  

- [Supporto per le versioni Current Branch di System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

