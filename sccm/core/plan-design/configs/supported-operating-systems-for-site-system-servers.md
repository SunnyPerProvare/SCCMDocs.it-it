---
title: Server di sistema del sito supportati | Microsoft Docs
description: "Informazioni sulle versioni di Windows che è possibile usare per ospitare un sito di System Center Configuration Manager o un ruolo del sistema del sito."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: d23b98b362fb016c53974f851c48fa7200d2b2e3
ms.openlocfilehash: b7c24dee94bca4ce69e0ba8f33129a0b21819d13


---
# <a name="supported-operating-systems-for-system-center-configuration-manager--site-system-servers"></a>Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


L'articolo illustra in dettaglio le versioni di Windows che è possibile usare per ospitare un sito di System Center Configuration Manager o un ruolo del sistema del sito.


Usare le informazioni di questo argomento con quelle contenute negli articoli relativi a:
-   [Recommended hardware for Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato per Configuration Manager)
-   [Prerequisiti del sito e del sistema del sito per Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Numeri di ridimensionamento e scalabilità per Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-----standard-datacenter"></a>Windows Server 2016 - Standard, Datacenter
Windows Server 2016 è supportato a partire da Configuration Manager versione 1606 con l'aggiornamento rapido cumulativo KB3186654, o versione di base 1606 rilasciata nell'ottobre del 2016.

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

     I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   Punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato

## <a name="windows-server-2012-r2-x64---standard-datacenter"></a>Windows Server 2012 R2 (x64) - Standard, Datacenter  
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

     I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   Punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

## <a name="windows-server-2012-x64---standard-datacenter"></a>Windows Server 2012 (x64) - Standard, Datacenter  
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

     I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   Punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

## <a name="windows-server-2008-r2-with-sp1-x64-----standard-enterprise-datacenter"></a>Windows Server 2008 R2 con SP1 (x64) - Standard, Enterprise, Datacenter  
 Windows Server 2008 R2 è ora in modalità di supporto "Extended" e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md) (Funzionalità rimosse e deprecate per System Center Configuration Manager).  

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

     I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   Punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

## <a name="windows-server-2008-with-sp2-x86-x64---standard-enterprise-datacenter"></a>Windows Server 2008 con SP2 (x86, x64) - Standard, Enterprise, Datacenter  
 Windows Server 2008 è ora in modalità di supporto "Extended" e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md) (Funzionalità rimosse e deprecate per System Center Configuration Manager).  

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

    -   I punti di distribuzione in questo sistema operativo non supportano il multicast.  

    -   I punti di distribuzione in questo sistema operativo sono supportati per PXE, ma non supportano l'avvio di rete dei computer client in modalità EFI. I computer client con BIOS o con avvio EFI in modalità legacy sono supportati.  

    -   I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione

-   Punto di Reporting Services  

-   Punto di connessione del servizio  

-   Server di database del sito  

     I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base. Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  

-   Provider_SMS  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

## <a name="windows-10-x86-x64---pro-enterprise"></a>Windows 10 (x86, x64) - Pro, Enterprise  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64---professional-enterprise"></a>Windows 8.1 (x86, x64) - Professional, Enterprise  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64---professional-enterprise-distribution-point"></a>Windows 8 (x86, x64) - Punto di distribuzione Professional, Enterprise  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64---professional-enterprise-ultimate"></a>Windows 7 con SP1 (x86, x64) - Professional, Enterprise, Ultimate  
**Server del sistema del sito:**  

-   Punto di distribuzione  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE.  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  

    -   I punti di distribuzione supportano alcune configurazioni diverse che hanno ognuna requisiti propri e in alcuni casi supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni sulle opzioni disponibili per i punti di distribuzione, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-2012"></a>Installazione Server Core di Windows Server 2012  
 Oltre ai sistemi operativi precedenti, l'installazione Server Core di Windows Server 2012 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   Sono supportati solo i sistemi x64  

-   I punti di distribuzione in questo sistema operativo non supportano PXE o il multicast  

## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Installazione Server Core di Windows Server 2012 R2  
 Oltre ai sistemi operativi precedenti, l'installazione Server Core di Windows Server 2012 R2 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   Sono supportati solo i sistemi x64  

-   I punti di distribuzione in questo sistema operativo non supportano PXE o il multicast  



<!--HONumber=Dec16_HO3-->


