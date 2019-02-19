---
title: Client e dispositivi supportati
titleSuffix: Configuration Manager
description: Informazioni sulle versioni dei sistemi operativi supportate da Configuration Manager per client e dispositivi.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 100fdd8e9032b1d16ae79b3cd52ffba3b3609446
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140161"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versioni dei sistemi operativi per client e dispositivi supportate da Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 Configuration Manager supporta l'installazione di software client in computer Windows, Mac, Linux e UNIX.  

#### <a name="requirements-and-limitations-for-all-clients"></a>Requisiti e limitazioni per tutti i client  

-   La modifica delle impostazioni del tipo di avvio o di **accesso per tutti** i servizi di Configuration Manager non è supportata. Se vengono apportate modifiche, i servizi principali potrebbero non funzionare correttamente.    

-   Non è consentito installare o eseguire il client di Configuration Manager per Linux o UNIX o il client per Mac nei computer con un account diverso dall'account radice. In caso contrario, i servizi principali potrebbero non funzionare correttamente.  



##  <a name="windows-computers"></a>Computer Windows  

 Per gestire le versioni dei sistemi operativi Windows seguenti, usare il client incluso in Configuration Manager. Per altre informazioni, vedere [Come distribuire i client nei computer Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  


### <a name="supported-client-os-versions"></a>Versioni del sistema operativo client supportate

-   **Windows 10**  

    Per altre informazioni dettagliate, vedere [Supporto per Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 7 con SP1** (x86, x64): Professional, Enterprise e Ultimate    


### <a name="supported-server-os-versions"></a>Versioni del sistema operativo server supportate

-  **Windows Server 2019**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  
    (A partire da Configuration Manager versione 1806.)

-  **Windows Server 2016**: Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>  

-   **Windows Storage Server 2016**: Workgroup, Standard  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 con SP1** (x64): Standard, Enterprise, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Workgroup, Standard, Enterprise    

-   **Windows Server 2008 con SP2** (x86, x64): Standard, Enterprise, Datacenter <sup>[Nota 1](#bkmk_note1)</sup>    


#### <a name="server-core"></a>Server Core
Le versioni seguenti fanno riferimento in modo specifico all'installazione Server Core del sistema operativo. <sup>[Nota 3](#bkmk_note3)</sup>  

Le versioni del canale semestrale di Windows Server sono installazioni Server Core, ad esempio Windows Server versione 1809. Come client di Configuration Manager, sono supportate come la versione del canale semestrale di Windows 10 associata. Per altre informazioni, vedere [Supporto per Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).


-   **Windows Server 2019** (x64) <sup>[Nota 2](#bkmk_note2)</sup>  

-   **Windows Server 2016** (x64) <sup>[Nota 2](#bkmk_note2)</sup>   

-   **Windows Server 2012 R2** (x64) <sup>[Nota 2](#bkmk_note2)</sup>     

-   **Windows Server 2012** (x64) <sup>[Nota 2](#bkmk_note2)</sup>     

-   **Windows Server 2008 R2** senza Service Pack o con SP1 (x64)     

-   **Windows Server 2008 SP2** (x86, x64)   

#### <a name="bkmk_note1"></a> Nota 1
 Configuration Manager verifica e supporta le edizioni di Windows Server Datacenter, ma non è ufficialmente certificato per Windows Server. Il supporto hotfix di Configuration Manager non è disponibile per problemi specifici di Windows Server Datacenter Edition. Per altre informazioni sul programma di certificazione di Windows Server, vedere [Catalogo di Windows Server](https://www.windowsservercatalog.com/). 

#### <a name="bkmk_note2"></a> Nota 2
 Per supportare l'[installazione push client](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation), aggiungere il servizio File server del ruolo del server Servizi file e archiviazione. Per altre informazioni sull'installazione di funzionalità di Windows in Server Core, vedere [Install roles, role services, and features by using Windows PowerShell cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installwps) (Installare ruoli, servizi ruolo e funzionalità tramite cmdlet di Windows PowerShell).  

#### <a name="bkmk_note3"></a> Nota 3
 La nuova app Software Center non è supportata in alcuna versione di Windows Server Core.<!--SCCMDocs issue 683-->



##  <a name="windows-embedded-computers"></a>Computer Windows Embedded  

 È possibile gestire i dispositivi Windows Embedded installando il client di Configuration Manager nel dispositivo. Per altre informazioni, vedere [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).  


### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

-   Tutte le funzionalità client sono supportate nei sistemi Windows Embedded in cui non sono abilitati filtri di scrittura.  

-   I client che usano uno dei tipi di filtro seguenti sono supportati per tutte le funzionalità tranne che per il risparmio energia:  

    -   Filtri di scrittura avanzati    

    -   Filtri di scrittura basati su file RAM    

    -   Filtri di scrittura unificati  

-   Il Catalogo applicazioni non è supportato per alcun dispositivo Windows Embedded.  


### <a name="supported-os-versions"></a>Versioni dei sistemi operativi supportate  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  
    Questa versione include il canale di manutenzione a lungo termine. Per altre informazioni, vedere [Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) (Panoramica di Windows 10 IoT Enterprise).<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 con SP1** (x86, x64)    



## <a name="windows-ce-computers"></a>Computer Windows CE

 È possibile gestire i dispositivi Windows CE con il client legacy del dispositivo mobile di Configuration Manager incluso in Configuration Manager.  


### <a name="requirements-and-limitations"></a>Requisiti e limitazioni  

-   Il client del dispositivo mobile richiede 0,78 MB di spazio di archiviazione per l'installazione. L'accesso può richiedere fino a 256 KB di spazio di archiviazione aggiuntivo.    

-   Le funzionalità per questi dispositivi mobili variano a seconda della piattaforma e del tipo di client. Per informazioni sulle funzioni di gestione supportate, vedere [Scegliere una soluzione di gestione dei dispositivi](/sccm/core/plan-design/choose-a-device-management-solution).  


### <a name="supported-os-versions"></a>Versioni dei sistemi operativi supportate  

-   Windows CE 7.0 (processori ARM e x86)  

#### <a name="supported-languages-include"></a>Le lingue supportate includono

-   Cinese (semplificato e tradizionale)    

-   Inglese (Stati Uniti)    

-   Francese (Francia)    

-   Tedesco    

-   Italiano    

-   Giapponese  

-   Coreano  

-   Portoghese (Brasile)  

-   Russo  

-   Spagnolo (Spagna)  



## <a name="mac-computers"></a>Computer Mac  

 È possibile gestire i computer macOS con il client di Configuration Manager per Mac.  

 Il pacchetto di installazione del client per Mac non viene fornito con i supporti di Configuration Manager. Scaricare i **client per altri sistemi operativi** dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Per altre informazioni, vedere [Come distribuire i client in computer Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).  


### <a name="supported-versions"></a>Versioni supportate

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

- **macOS Mojave (10.14)** 


##  <a name="linux-and-unix-servers"></a>Server Linux e UNIX  

> [!Important]  
> I client Linux e UNIX per Configuration Manager sono deprecati dal 22 marzo 2018. Per altre informazioni, vedere, [Annuncio di supporto deprecato per i client Linux e Unix](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support).  

 Per gestire i server Linux e UNIX è possibile usare il client di Configuration Manager per Linux e UNIX.  

 I pacchetti di installazione del client per Linux e UNIX non sono inclusi con i supporti di Configuration Manager. Scaricare i **client per altri sistemi operativi** dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Oltre ai pacchetti di installazione client, il download del client include lo script che gestisce l'installazione del client in ogni computer.  


### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

-   Per informazioni dettagliate sulle dipendenze del file del sistema operativo per il client per Linux e UNIX, vedere [Prerequisiti per la distribuzione dei client ai server Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  

-   Per una panoramica delle funzionalità di gestione supportate per Linux o UNIX, vedere [Come distribuire i client nei server UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

-   Per le versioni supportate di Linux e UNIX, la versione indicata include tutte le versioni secondarie successive. Ad esempio, la versione 6 di CentOS include CentOS 6.3. Analogamente, il supporto per un sistema operativo che usa Service Pack, ad esempio SUSE Linux Enterprise Server 11 SP1, include i Service Pack successivi per tale versione del sistema operativo.  

-   Per informazioni sui pacchetti di installazione client e su Universal Agent, vedere [Come distribuire i client nei server UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  


### <a name="supported-versions"></a>Versioni supportate

Le versioni seguenti sono supportate tramite l'uso del file TAR indicato.  

#### <a name="aix"></a>AIX  

|Version|File TAR|  
|-|-|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versione 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Version|File TAR|  
|-|-|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Version|File TAR|  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|Version|File TAR|  
|-|-|  
|Versione 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versione 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versione 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Version|File TAR|  
|-|-|  
|Versione 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Version|File TAR|  
|-|-|  
|Versione 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  



##  <a name="bkmk_OnpremOS"></a> Gestione dei dispositivi mobili locale  

 Configuration Manager include funzionalità predefinite per la gestione dei dispositivi locali senza installare software client. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="requirements-and-limitations"></a>Requisiti e limitazioni

-   Configurare il **punto di connessione del servizio** nel sito di livello superiore della gerarchia.  


### <a name="supported-operating-systems"></a>Sistemi operativi supportati

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Questa versione include il canale di manutenzione a lungo termine. Per altre informazioni, vedere [Overview of Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise) (Panoramica di Windows 10 IoT Enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 Team per Surface Hub**  



##  <a name="bkmk_ExSrvConOS"></a> Connettore Exchange Server  

Configuration Manager supporta la gestione limitata dei dispositivi che si connettono a Exchange Server, senza installare il client di Configuration Manager. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="supported-versions-of-exchange-server"></a>Versioni di Exchange Server supportate

- **Exchange Online (Office 365)**: questa versione include Business Productivity Online Standard Suite  

- **Exchange Server 2016** (a partire dalla versione 1802)  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** o **Exchange Server 2010 SP2** 
