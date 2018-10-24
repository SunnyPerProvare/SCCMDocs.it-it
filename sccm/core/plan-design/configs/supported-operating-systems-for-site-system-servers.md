---
title: Server di sistema del sito supportati
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows che è possibile usare per ospitare un sito di Configuration Manager o un ruolo del sistema del sito.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fd8e815ab57730ad2186a7e75cd51f21012383a
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236175"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


L'articolo illustra in dettaglio le versioni di Windows che è possibile usare per ospitare un sito di Configuration Manager o un ruolo del sistema del sito.


Usare le informazioni di questo articolo con quelle contenute negli articoli seguenti:
-   [Recommended hardware for Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware) (Hardware consigliato per Configuration Manager)
-   [Prerequisiti del sito e del sistema del sito per Configuration Manager](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
-   [Numeri di ridimensionamento e scalabilità per Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers)



## <a name="bkmk_2016"></a> Windows Server 2016 - Standard e Datacenter

Con l'aggiornamento cumulativo 1 di Configuration Manager versione 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), questa versione del sistema operativo è supportata per i ruoli seguenti:

#### <a name="site-servers"></a>Server del sito

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto per servizi Web del Catalogo applicazioni  
-   Punto per siti Web del Catalogo applicazioni  
-   Punto di sincronizzazione di Asset Intelligence  
-   Punto di registrazione certificati  
-   Punto di connessione del gateway di gestione cloud  
-   Punto di servizio del data warehouse  
-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto di Endpoint Protection  
-   Punto di registrazione  
-   Punto proxy di registrazione  
-   Punto di stato di fallback  
-   Punto di gestione
-   Punto di Reporting Services  
-   punto di connessione del servizio  
-   Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
-   Provider_SMS  
-   Punto di aggiornamento software  
-   Punto di migrazione stato



## <a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>Server del sistema del sito

-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  



## <a name="bkmk_2012r2"></a> Windows Server 2012 R2 (x64) - Standard e Datacenter  

#### <a name="site-servers"></a>Server del sito

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto per servizi Web del Catalogo applicazioni  
-   Punto per siti Web del Catalogo applicazioni  
-   Punto di sincronizzazione di Asset Intelligence  
-   Punto di registrazione certificati  
-   Punto di connessione del gateway di gestione cloud  
-   Punto di servizio del data warehouse  
-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto di Endpoint Protection  
-   Punto di registrazione  
-   Punto proxy di registrazione  
-   Punto di stato di fallback  
-   Punto di gestione
-   Punto di Reporting Services  
-   punto di connessione del servizio  
-   Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
-   Provider_SMS  
-   Punto di aggiornamento software  
-   Punto di migrazione stato  



## <a name="bkmk_2012"></a> Windows Server 2012 (x64) - Standard e Datacenter  

#### <a name="site-servers"></a>Server del sito

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto per servizi Web del Catalogo applicazioni  
-   Punto per siti Web del Catalogo applicazioni  
-   Punto di sincronizzazione di Asset Intelligence  
-   Punto di registrazione certificati  
-   Punto di connessione del gateway di gestione cloud  
-   Punto di servizio del data warehouse  
-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  
-   Punto di Endpoint Protection  
-   Punto di registrazione  
-   Punto proxy di registrazione  
-   Punto di stato di fallback  
-   Punto di gestione
-   Punto di Reporting Services  
-   punto di connessione del servizio  
-   Server di database del sito <sup>[Nota 2](#bkmk_note2)</sup>  
-   Provider_SMS  
-   Punto di aggiornamento software  
-   Punto di migrazione stato  



## <a name="bkmk_2008r2sp1"></a> Windows Server 2008 R2 con SP1 (x64) - Standard, Enterprise e Datacenter  

Windows Server 2008 R2 è ora in modalità di supporto Extended e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Sistemi operativi del server deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Questo sistema operativo non è supportato per i server del sito o per la maggior parte dei ruoli del sistema del sito. È ancora supportato per il ruolo del sistema del sito dei punti di distribuzione, inclusi i punti di distribuzione pull, e per PXE e il multicast.

#### <a name="site-system-servers"></a>Server del sistema del sito
-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

    - I punti di distribuzione in questo sistema operativo supportano PXE e Multicast.  



## <a name="bkmk_2008sp2"></a> Windows Server 2008 con SP2 (x86, x64) - Standard, Enterprise e Datacenter  

Windows Server 2008 è ora in modalità di supporto Extended e non più in modalità di supporto Mainstream, come descritto in [Criteri relativi al ciclo di vita Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Sistemi operativi del server deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Questo sistema operativo non è supportato per i server del sito o per i ruoli del sistema del sito, fatta eccezione per il punto di distribuzione e il punto di distribuzione pull. È possibile continuare a usare questo sistema operativo come punto di distribuzione fino all'annuncio della deprecazione di questo supporto o fino alla scadenza del periodo di supporto "Extended" di questo sistema operativo. Per altre informazioni, vedere l'argomento relativo ai [problemi di installazione di System Center Configuration Manager CB in Windows Server 2008](https://support.microsoft.com/help/4015095).

#### <a name="site-system-servers"></a>Server del sistema del sito
-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

    -   I punti di distribuzione in questo sistema operativo supportano PXE e multicast.  

    -   I punti di distribuzione in questo sistema operativo non supportano l'avvio di rete dei computer client in modalità EFI. I computer client con BIOS o con avvio EFI in modalità legacy sono supportati.  



## <a name="bkmk_win10"></a> Windows 10 (x86, x64) - Pro ed Enterprise  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  



## <a name="bkmk_win81"></a> Windows 8.1 (x86, x64) - Professional ed Enterprise  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  



## <a name="bkmk_win7sp1"></a> Windows 7 con SP1 (x86, x64) - Professional, Enterprise e Ultimate  

#### <a name="site-system-servers"></a>Server del sistema del sito

-   Punto di distribuzione <sup>[Nota 1](#bkmk_note1)</sup>  

    -   I punti di distribuzione in questo sistema operativo non sono supportati per PXE con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

    -   I punti di distribuzione in questa versione del sistema operativo non supportano il multicast.  



## <a name="bkmk_core1803"></a> Installazione Server Core di Windows Server, versione 1803
<!--503702--> A partire da Configuration Manager 1802, [Windows Server, versione 1803](https://docs.microsoft.com/windows-server/get-started/get-started-with-1803) è supportato per l'uso come punto di distribuzione con le limitazioni seguenti:  

  -   È supportata solo la versione a x64 bit.  

  -   I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core1709"></a> Installazione Server Core di Windows Server, versione 1709

A partire da Configuration Manager 1710, [Windows Server, versione 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) è supportato per l'uso come punto di distribuzione con le limitazioni seguenti:  

  -   È supportata solo la versione a x64 bit.  

  -   I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2016"></a> Installazione Server Core di Windows Server 2016

Con l'aggiornamento cumulativo 1 di Configuration Manager versione 1606 ([KB3186654](https://support.microsoft.com/help/3186654)), questa versione del sistema operativo è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

  -   È supportata solo la versione a x64 bit.  

  -   I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012r2"></a> Installazione Server Core di Windows Server 2012 R2  

L'installazione Server Core di Windows Server 2012 R2 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   È supportata solo la versione a x64 bit.

-   I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  



## <a name="bkmk_core2012"></a> Installazione Server Core di Windows Server 2012  

L'installazione Server Core di Windows Server 2012 è supportata per l'uso come punto di distribuzione con le limitazioni seguenti:  

-   È supportata solo la versione a 64 bit.  

-   I punti di distribuzione in questo sistema operativo non supportano PXE o multicast con i Servizi di distribuzione Windows predefiniti. A partire dalla versione 1806, è possibile abilitare per PXE un punto di distribuzione in questo sistema operativo con l'opzione **Abilita un risponditore PXE senza i Servizi di distribuzione Windows**. Per altre informazioni, vedere [Installare e configurare i punti di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).



## <a name="general-notes"></a>Note generali

#### <a name="bkmk_note1"></a> Nota 1: Punti di distribuzione
I punti di distribuzione supportano varie configurazioni, ognuna delle quali presenta requisiti diversi. In alcuni casi, queste configurazioni supportano l'installazione non solo su server, ma anche su sistemi operativi client. Per altre informazioni, vedere [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gestire il contenuto e l'infrastruttura del contenuto).  

#### <a name="bkmk_note2"></a> Nota 2: Server di database del sito
I server di database del sito non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere l'articolo del supporto tecnico Microsoft [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](https://support.microsoft.com/help/2032911). 

Inoltre, i server del sito secondario non sono supportati in alcun controller di dominio.  
