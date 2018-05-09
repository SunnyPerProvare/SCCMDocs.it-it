---
title: Elementi deprecati per i server del sito di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni su prodotti e sistemi operativi che System Center Configuration Manager non supporta più per i server del sito.
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Elementi rimossi e deprecati per i server del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive i prodotti e i sistemi operativi rimossi dal supporto per i server del sito di System Center Configuration Manager o che verranno rimossi in un aggiornamento futuro (deprecati). Lo scopo è quello di informare in maniera anticipata gli utenti sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifiche nelle versioni future e potrebbero non includere tutte le funzionalità, tutti i prodotti o i sistemi operativi deprecati.  


## <a name="deprecated-server-operating-systems"></a>Sistemi operativi del server deprecati  

|**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso** |  
|-|-|-| 
|Windows Server 2008 R2|10 luglio 2015| Versione 1702 (vedere nota 1)| 
|Windows Server 2008|10 luglio 2015|Versione 1511 </br></br>Il supporto come sistema del sito viene rimosso. Vedere nota 2.|  

>[!NOTE]
>-   A partire dalla versione 1702, Windows Server 2008 R2 non è supportato per i server del sito o la maggior parte dei ruoli del sistema del sito. Continua tuttavia a essere supportato dalle versioni precedenti la 1702. Questo sistema operativo resta comunque supportato per il ruolo del sistema del sito del punto di distribuzione (compresi i punti di distribuzione pull, PXE e il multicast) fino all'annuncio della deprecazione del supporto o alla scadenza del periodo di supporto "Extended" del sistema operativo. A partire dalla versione 1602, è possibile aggiornare sul posto il sistema operativo di un server del sito da Windows Server 2008 R2 a Windows Server 2012 R2.  
>- Per altre informazioni sull'aggiornamento sul posto del sistema operativo dei server del sito, vedere la sezione [Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) in [Aggiornare l'infrastruttura locale che supporta System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Windows Server 2008 non è supportato per i server del sito o ruoli del sistema del sito fatta eccezione per il punto di distribuzione e il punto di distribuzione pull. È possibile continuare a usare questo sistema operativo come punto di distribuzione fino all'annuncio della deprecazione di questo supporto o alla scadenza del periodo di supporto "Extended" di questo sistema operativo. Per altre informazioni, vedere l'argomento relativo ai [problemi di installazione di System Center Configuration Manager CB in Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Supporto deprecato per le versioni di SQL Server usate come database del sito  

|**Versioni di SQL Server**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|   
|-|-|-| 
|SQL Server 2008 R2|10 luglio 2015|Versione 1702| 
|SQL Server 2008|10 luglio 2015|Versione 1511|  


Se è necessario aggiornare la versione di SQL Server, è consigliabile seguire i metodi seguenti, dal più semplice al più complesso.
1. [Aggiornare SQL Server sul posto](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (scelta consigliata).
2. Installare una nuova versione di SQL Server in un nuovo computer. Quindi [usare l'opzione di spostamento del database](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) delle impostazioni di Configuration Manager in modo che il server del sito punti alla nuova versione di SQL Server.
3. Usare le funzionalità di [backup e ripristino](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Altre informazioni
Per altre informazioni, vedere:
 - [Elementi rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).
 - [Supporto per le versioni Current Branch di Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).