---
title: Server di sistema del sito supportati
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows che è possibile usare per ospitare un sito di System Center Configuration Manager o un ruolo del sistema del sito.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5bcaddb38ea6ecf1c3b5e0543c676c6a99e06101
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemi operativi supportati per i server dei sistemi del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


L'articolo illustra in dettaglio le versioni di Windows che è possibile usare per ospitare un sito di System Center Configuration Manager o un ruolo del sistema del sito.


Usare le informazioni di questo articolo con quelle contenute negli articoli seguenti:
-   [Recommended hardware for Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato per Configuration Manager)
-   [Prerequisiti del sito e del sistema del sito per Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Numeri di ridimensionamento e scalabilità per Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016 - Standard e Datacenter
Con l'hotfix rollup da KB3186654 questo sistema operativo è supportato per i ruoli seguenti:

**Server del sito:**  

-   Sito di amministrazione centrale  

-   Sito primario  

-   Sito secondario  

**Server del sistema del sito:**  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di sincronizzazione di Asset Intelligence  

-   Punto di registrazione certificati  

-   Punto di distribuzione  

     I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](https://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64) - Standard e Datacenter  
**Server del sito:**  

-   Sito di amministrazione centrale  

-   Sito primario  

-   Sito secondario  

**Server del sistema del sito:**  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di sincronizzazione di Asset Intelligence  

-   Punto di registrazione certificati  

-   Punto di distribuzione  

     I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](https://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64) - Standard e Datacenter  
**Server del sito:**  

-   Sito di amministrazione centrale  

-   Sito primario  

-   Sito secondario  

**Server del sistema del sito:**  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di sincronizzazione di Asset Intelligence  

-   Punto di registrazione certificati  

-   Punto di distribuzione  

     I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](https://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 con SP1 (x64) - Standard, Enterprise e Datacenter  
 Windows Server 2008 R2 è ora in modalità di supporto Extended e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Sistemi operativi del server deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

 Questo sistema operativo non è supportato per i server del sito o per la maggior parte dei ruoli del sistema del sito. È ancora supportato per il ruolo del sistema del sito dei punti di distribuzione, inclusi i punti di distribuzione pull, e per PXE e il multicast.

**Server del sistema del sito:**  
-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non supportano il multicast.  

    -   I punti di distribuzione in questo sistema operativo sono supportati per PXE.

    -   I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 con SP2 (x86, x64) - Standard, Enterprise e Datacenter  
 Windows Server 2008 è ora in modalità di supporto Extended e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Sistemi operativi del server deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Questo sistema operativo non è supportato per i server del sito o per i ruoli del sistema del sito, fatta eccezione per il punto di distribuzione e il punto di distribuzione pull. È possibile continuare a usare questo sistema operativo come punto di distribuzione fino all'annuncio della deprecazione di questo supporto o fino alla scadenza del periodo di supporto "Extended" di questo sistema operativo. Per altre informazioni, vedere l'argomento relativo ai [problemi di installazione di System Center Configuration Manager CB in Windows Server 2008](https://support.microsoft.com/help/4015095).

**Server del sistema del sito:**  
-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non supportano il multicast.  

    -   I punti di distribuzione in questo sistema operativo sono supportati per PXE, ma non supportano l'avvio di rete dei computer client in modalità EFI. I computer client con BIOS o con avvio EFI in modalità legacy sono supportati.  

    -   I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64) - Pro e Enterprise  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE. 

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64) - Professional e Enterprise  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 con SP1 (x86, x64) - Professional, Enterprise e Ultimate  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="the-server-core-installation-of-windows-server-2016"></a>Installazione Server Core di Windows Server 2016
Con l'hotfix rollup da KB3186654, questo sistema operativo è supportato per l'uso come punto di distribuzione con le limitazioni seguenti:  
  -   È supportata solo la versione a x64 bit.
  -   I punti di distribuzione in questo sistema operativo non supportano PXE né il multicast.  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Installazione Server Core di Windows Server 2012 R2  
 L'installazione Server Core di Windows Server 2012 R2 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   È supportata solo la versione a x64 bit.

-   I punti di distribuzione in questo sistema operativo non supportano PXE né il multicast.  



## <a name="the-server-core-installation-of-windows-server-2012"></a>Installazione Server Core di Windows Server 2012  
 L'installazione Server Core di Windows Server 2012 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   È supportata solo la versione a 64 bit.  

-   I punti di distribuzione in questo sistema operativo non supportano PXE né il multicast.
