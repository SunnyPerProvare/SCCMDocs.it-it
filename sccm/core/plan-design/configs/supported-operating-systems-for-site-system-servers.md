---
title: Server di sistema del sito supportati
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows che è possibile usare per ospitare un sito di Configuration Manager o un ruolo del sistema del sito.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7009e5995a8345471256a6675fff7352660271fc
ms.sourcegitcommit: b73f61371c8591e0c7340ee9d9e945cd5e68347e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2020
ms.locfileid: "77515859"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

L'articolo illustra in dettaglio le versioni di Windows che è possibile usare per ospitare un sito di Configuration Manager o un ruolo del sistema del sito.

Usare le informazioni di questo articolo con quelle contenute negli articoli seguenti:

- [Recommended hardware for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware) (Hardware consigliato per Configuration Manager)
- [Prerequisiti del sito e del sistema del sito per Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Numeri di ridimensionamento e scalabilità per Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)

## <a name="bkmk_2019"></a> Windows Server 2019

*Si applica a Windows Server 2019: Standard e Datacenter* 

A partire dalla versione 1810, questa versione del sistema operativo è supportata per i ruoli seguenti:

#### <a name="site-servers"></a>Server del sito

- Sito di amministrazione centrale  
- Sito primario  
- Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

- Punto per servizi Web del Catalogo applicazioni  
- Punto per siti Web del Catalogo applicazioni  
- Punto di sincronizzazione di Asset Intelligence  
- Punto di registrazione certificati  
- Punto di connessione del gateway di gestione cloud  
- Punto di servizio del data warehouse  
- Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto di Endpoint Protection  
- Punto di registrazione  
- Punto proxy di registrazione  
- Punto di stato di fallback  
- Punto di gestione
- Punto di Reporting Services  
- punto di connessione del servizio  
- Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
- Provider_SMS  
- Punto di aggiornamento software  
- Punto di migrazione stato

## <a name="bkmk_2016"></a> Windows Server 2016

*Si applica a Windows Server 2016: Standard e Datacenter*

Questa versione del sistema operativo è supportata per i ruoli seguenti:

#### <a name="site-servers"></a>Server del sito

- Sito di amministrazione centrale  
- Sito primario  
- Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

- Punto per servizi Web del Catalogo applicazioni  
- Punto per siti Web del Catalogo applicazioni  
- Punto di sincronizzazione di Asset Intelligence  
- Punto di registrazione certificati  
- Punto di connessione del gateway di gestione cloud  
- Punto di servizio del data warehouse  
- Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto di Endpoint Protection  
- Punto di registrazione  
- Punto proxy di registrazione  
- Punto di stato di fallback  
- Punto di gestione
- Punto di Reporting Services  
- punto di connessione del servizio  
- Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
- Provider_SMS  
- Punto di aggiornamento software  
- Punto di migrazione stato

## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>Server del sistema del sito

- Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

## <a name="bkmk_2012r2"></a> Windows Server 2012 R2

*Si applica a Windows Server 2012 R2: Standard e Datacenter*

#### <a name="site-servers"></a>Server del sito

- Sito di amministrazione centrale  
- Sito primario  
- Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

- Punto per servizi Web del Catalogo applicazioni  
- Punto per siti Web del Catalogo applicazioni  
- Punto di sincronizzazione di Asset Intelligence  
- Punto di registrazione certificati  
- Punto di connessione del gateway di gestione cloud  
- Punto di servizio del data warehouse  
- Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto di Endpoint Protection  
- Punto di registrazione  
- Punto proxy di registrazione  
- Punto di stato di fallback  
- Punto di gestione
- Punto di Reporting Services  
- punto di connessione del servizio  
- Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
- Provider_SMS  
- Punto di aggiornamento software  
- Punto di migrazione stato  

## <a name="bkmk_2012"></a> Windows Server 2012  

*Si applica a Windows Server 2012: Standard e Datacenter*

#### <a name="site-servers"></a>Server del sito

- Sito di amministrazione centrale  
- Sito primario  
- Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

- Punto per servizi Web del Catalogo applicazioni  
- Punto per siti Web del Catalogo applicazioni  
- Punto di sincronizzazione di Asset Intelligence  
- Punto di registrazione certificati  
- Punto di connessione del gateway di gestione cloud  
- Punto di servizio del data warehouse  
- Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
- Punto di Endpoint Protection  
- Punto di registrazione  
- Punto proxy di registrazione  
- Punto di stato di fallback  
- Punto di gestione
- Punto di Reporting Services  
- punto di connessione del servizio  
- Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
- Provider_SMS  
- Punto di aggiornamento software  
- Punto di migrazione stato  

## <a name="bkmk_client"></a> Versioni del sistema operativo client

Le versioni del sistema operativo client seguenti sono supportate per l'uso come **punto di distribuzione** <sup>[Nota 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): Pro ed Enterprise

    Per altre informazioni sulle versioni delle build supportate, vedere [Supporto per Windows 10](/configmgr/core/plan-design/configs/support-for-windows-10).

- Windows 8.1 (x86, x64): Professional ed Enterprise

Questo supporto presenta le limitazioni seguenti:  

- I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

## <a name="bkmk_core"></a> Installazioni dei componenti di base del server

L'installazione dei componenti di base è supportata per l'uso come **punto di distribuzione** per le versioni seguenti del sistema operativo server:

- Windows Server 2019 (a partire da Configuration Manager versione 1810)  
- Windows Server, versione 1809 (a partire da Configuration Manager versione 1810)  
- Windows Server, versione 1803 (a partire da Configuration Manager versione 1802)  
- Windows Server, versione 1709 (a partire da Configuration Manager versione 1710)  
- Windows Server 2016  
- R2 per Windows Server 2012  
- Windows Server 2012  

Questo supporto presenta le limitazioni seguenti:  

- I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

## <a name="general-notes"></a>Note generali

### <a name="bkmk_note1"></a> Nota 1: Punti di distribuzione

I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni, vedere [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gestire il contenuto e l'infrastruttura del contenuto).  

### <a name="bkmk_note2"></a> Nota 2: Server di database del sito

I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere l'articolo del supporto tecnico Microsoft: [You may encounter problems when installing SQL Server on a domain controller](https://support.microsoft.com/help/2032911) (Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio). 

Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  
