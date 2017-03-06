---
title: Client e dispositivi supportati | Microsoft Docs
description: Informazioni su quali sistemi operativi sono supportati da System Center Configuration Manager per client e dispositivi.
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bdd7961d9126dc6f3c1ae1fec1842c862e8a7c6d
ms.openlocfilehash: 12633a7b9f799ffc74e0ee657e091595ed7eaf67
ms.lasthandoff: 02/22/2017

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Sistemi operativi supportati per client e dispositivi per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager supporta l'installazione di software client in un'ampia gamma di computer Windows, Mac, Linux e UNIX.  

 **Requisiti e limitazioni per tutti i client:**  

-   Non è consentito modificare il tipo di avvio o le impostazioni **Accedi come** per qualsiasi servizio di Configuration Manager, poiché può impedire il corretto funzionamento di alcuni dei servizi principali.    

-   Non è consentito installare o eseguire il client di Configuration Manager per Linux o UNIX o il client per Mac nei computer con un account diverso dall'account radice. In caso contrario, i servizi principali potrebbero non funzionare correttamente.  

##  <a name="windows-computers"></a>Computer Windows  
 È possibile usare il client di Configuration Manager incluso con Configuration Manager per gestire i sistemi operativi Windows seguenti. Per altre informazioni, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Sistemi operativi supportati:**  


-  **Windows Server 2016** - Standard, Datacenter <sup>1</sup>
  - Questo sistema operativo è supportato a partire da Configuration Manager versione 1606 con l'hotfix rollup di KB3186654 o dalla versione 1606 di base rilasciata nell'ottobre del 2016.  

-   **Windows Server 2012 R2** (x64) - Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64) - Standard, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 con SP1** (x64) - Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64) - Workgroup, Standard, Enterprise    

-   **Windows  Server 2008 con SP2** (x86, x64) - Standard, Enterprise, Datacenter <sup>1</sup>    

-   **Windows 10**: Pro, Enterprise  
   Vedere [Support for versions of Windows 10](/sccm/core/plan-design/configs/support-for-windows-10) (Supporto delle versioni di Windows 10) per informazioni dettagliate sulle diverse versioni di rilascio di Windows 10 supportate dalle varie versioni di Configuration Manager.

-   **Windows 8.1** (x86, x64) - Professional, Enterprise    

-   **Windows 8** (x86, x64) - Professional, Enterprise    

-   **Windows 7 con SP1** (x86, x64) - Professional, Enterprise e Ultimate    

-   **Installazione dei componenti di base di Windows Server 2016** (x64) <sup>2</sup>
  - Questo sistema operativo è supportato a partire dalla versione 1606 con l'hotfix rollup di KB3186654 o dalla versione 1606 di base rilasciata nell'ottobre del 2016. Questo sistema operativo, tuttavia, non supporta l'uso con Endpoint Protection.


-   **Installazione dei componenti di base di Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **Installazione dei componenti di base di Windows Server 2012** (x64) <sup>2</sup>    

-   **Installazione dei componenti di base di Windows Server 2008 R2**  
    **(senza Service Pack o con SP1)** (x64)    

-   **Installazione dei componenti di base di Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> Le versioni Datacenter sono supportate, ma non certificate, per Configuration Manager. Il supporto hotfix non è disponibile per problemi specifici di Windows Server Datacenter Edition.  

 <sup>2</sup> Per supportare l'installazione push client, il computer che esegue questa versione del sistema operativo deve eseguire il servizio ruolo File server per il ruolo del server Servizi file e archiviazione. Per altre informazioni sull'installazione di funzionalità di Windows in un computer Server Core, vedere [Installare i ruoli e le funzionalità server in un server Server Core](http://go.microsoft.com/fwlink/p/?LinkId=299359) nella libreria TechNet per Windows Server 2012.  


##  <a name="windows-embedded-computers"></a>Computer Windows Embedded  
 È possibile gestire i dispositivi Windows Embedded installando il software client di Configuration Manager nel dispositivo.  Per altre informazioni, vedere [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md) (Pianificazione della distribuzione client a dispositivi con Windows Embedded in System Center Configuration Manager).  

**Requisiti e limitazioni:**  

-   Tutte le funzionalità client sono supportate nei sistemi Windows Embedded in cui non sono abilitati filtri di scrittura.  

-   I client che usano uno dei tipi di filtro seguenti sono supportati per tutte le funzionalità tranne che per il risparmio energia:  

    -   Filtri di scrittura avanzati    

    -   Filtri di scrittura basati su file RAM    

    -   Filtri di scrittura unificati  

-   Il Catalogo applicazioni non è supportato per alcun dispositivo Windows Embedded.  

-   Prima di poter monitorare malware rilevati nei dispositivi Windows Embedded basati su Windows XP, è necessario installare il pacchetto di scripting WMI di Microsoft Windows nel dispositivo. Usare Windows Embedded Target Designer per installare questo pacchetto.
I file **WBEMDISP.DLL** e **WBEMDISP.TLB** devono essere presenti e registrati nella cartella **%windir%\System32\WBEM** nel dispositivo Windows Embedded per garantire la segnalazione del malware rilevato.  

**Sistemi operativi supportati:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows Thin PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 con SP1** (x86, x64)    

-   **WEPOS 1.1 con SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Windows Fundamentals for Legacy PCs (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce-computers"></a>Computer Windows CE
 È possibile gestire i dispositivi Windows CE con il client legacy del dispositivo mobile di Configuration Manager incluso in Configuration Manager.  

**Requisiti e limitazioni**  

-   Il client del dispositivo mobile richiede 0,78 MB di spazio di archiviazione per l'installazione. L'accesso può richiedere fino a 256 KB di spazio di archiviazione aggiuntivo.    

-   Le funzionalità per questi dispositivi mobili variano a seconda della piattaforma e del tipo di client. Per informazioni sulle funzioni di gestione supportate, vedere [Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

**Sistemi operativi supportati:**  

-   Windows CE 7.0 (processori ARM e x86)  

**Le lingue supportate includono:**  

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
 È possibile usare il client di Configuration Manager per Mac per gestire i computer Mac OS X.  

 Il pacchetto di installazione del client per Mac non viene fornito con i supporti di Configuration Manager. Scaricare i **client per sistemi operativi aggiuntivi** dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Per altre informazioni, vedere [How to deploy clients to Macs in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-macs.md) (Come distribuire i client per i computer Mac in System Center Configuration Manager).  

**Versioni supportate:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

##  <a name="linux-and-unix-servers"></a>Server Linux e UNIX  
 Per gestire i server Linux e UNIX è possibile usare il client di Configuration Manager per Linux e UNIX.  

 I pacchetti di installazione client per Linux e UNIX non vengono forniti con i supporti di Configuration Manager. Scaricare i **client per sistemi operativi aggiuntivi** dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Oltre ai pacchetti di installazione client, il download del client include lo script che gestisce l'installazione del client in ogni computer.  

**Requisiti e limitazioni:**  

-   Per informazioni dettagliate sulle dipendenze del file del sistema operativo per il client per Linux e UNIX, vedere [Prerequisites for Client Deployment to Linux and UNIX Servers](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU) (Prerequisiti per la distribuzione client a server Linux e UNIX).  

-   Per una panoramica delle funzionalità di gestione supportate, vedere [Come distribuire i client nei server UNIX e Linux in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Per le versioni supportate di Linux e UNIX, la versione indicata include tutte le versioni secondarie successive. Ad esempio, la versione 6 di CentOS include CentOS 6.3. Analogamente, il supporto per un sistema operativo che usa Service Pack, ad esempio SUSE Linux Enterprise Server 11 SP1, include i Service Pack successivi per questo sistema operativo.  

-   Per informazioni sui pacchetti di installazione client e su Universal Agent, vedere [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md) (Come distribuire i client a server UNIX e Linux in System Center Configuration Manager).  

**Versioni supportate:** le versioni seguenti sono supportate tramite l'uso del file TAR indicato.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Versione 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Version 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versione 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|||  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|||  
|-|-|  
|Version 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Versione 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Version 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Versione 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Versione 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Versione 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Versione 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Versione 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Versione 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Version 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versione 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versione 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Versione 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Versione 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Versione 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versione 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versione 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>Dispositivi mobili registrati con Microsoft Intune  
 Per informazioni dettagliate sui computer e sui dispositivi che è possibile gestire quando si integra Microsoft Intune con Configuration Manager, vedere i due argomenti seguenti nella raccolta della documentazione di Microsoft Intune:  

-   [Scegliere come gestire i dispositivi](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Funzionalità di gestione di PC Windows quando si usa il client software di Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="a-namebkmkonpremosa-on-premises-mobile-device-management"></a><a name="bkmk_OnpremOS"></a> Gestione dei dispositivi mobili locale  
 Configuration Manager include funzionalità predefinite per la gestione dei dispositivi locali senza installare software client.  Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Requisiti e limitazioni:**  

-   Nel sito di livello superiore della gerarchia è necessario configurare il **punto di connessione del servizio**  

**Sistemi operativi supportati:**  

-   **Windows 10 Pro** (x86, x64)  

-   **Windows 10 Pro Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)

-   **Windows 10 Mobile**  

-   **Windows 10 Mobile Enterprise**  

-  **Windows 10 IoT Mobile Enterprise**

##  <a name="a-namebkmkexsrvconosa-exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Connettore Exchange Server  
Configuration Manager supporta la gestione limitata dei dispositivi che si connettono a Exchange Server, senza installare il client di Configuration Manager. Per altre informazioni, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Requisiti e limitazioni:**  

-   Configuration Manager offre una gestione limitata dei dispositivi mobili quando si usano dispositivi con il connettore Exchange Server per Exchange Active Sync (EAS) che si connettono a un server che esegue Exchange Server o Exchange Online.  

-   Per altre informazioni sulle funzioni di gestione supportate da Configuration Manager per i dispositivi mobili gestiti dal connettore Exchange Server, vedere Determinare la modalità di gestione dei dispositivi mobili in Configuration Manager.  

**Versioni di Exchange Server supportate:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: include Business Productivity Online Standard Suite  

