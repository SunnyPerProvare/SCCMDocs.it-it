---
title: Requisiti dell&quot;infrastruttura per la distribuzione del sistema operativo | Microsoft Docs
description: Assicurarsi di conoscere le dipendenze esterne e le dipendenze del prodotto prima di usare System Center Configuration Manager 2012 per la distribuzione del sistema operativo.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: 24
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b9e49da1a5bbfca93fe683b82d2c0056a22cc1f
ms.openlocfilehash: 562e81df12e46a2332aa5e4de8b7c9e5819bde80
ms.lasthandoff: 03/21/2017


---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Requisiti dell'infrastruttura per la distribuzione del sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La distribuzione del sistema operativo in System Center Configuration Manager 2012 ha dipendenze esterne e dipendenze all'interno del prodotto. Usare le sezioni seguenti per prepararsi per la distribuzione del sistema operativo.  

##  <a name="BKMK_ExternalDependencies"></a> Dipendenze esterne a Configuration Manager  
 Di seguito sono riportate informazioni su strumenti esterni, kit di installazione e sistemi operativi richiesti per distribuire sistemi operativi in Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK per Windows 10  
 Windows ADK è un insieme di strumenti e documentazione che supporta la configurazione e la distribuzione dei sistemi operativi Windows. Configuration Manager usa Windows ADK per automatizzare l'installazione e acquisire immagini di Windows, eseguire la migrazione di dati e profili utente e così via.  

 È necessario installare le seguenti funzionalità di Windows ADK nel server del sito del sito di livello superiore della gerarchia, nel server del sito di ogni sito primario nella gerarchia e nel server del sistema del sito del provider SMS:  

-   Utilità di migrazione stato utente (USMT) <sup>1</sup>  

-   Strumenti di distribuzione Windows  

-   Ambiente preinstallazione di Windows (Windows PE)  

 <sup>1</sup> USMT non è richiesto nel server del sistema del sito del provider SMS.  

> [!NOTE]  
>  È necessario installare manualmente Windows ADK in ogni computer che ospiterà un sito di amministrazione centrale o un server del sito primario prima di installare il sito di Configuration Manager.  

 Per altre informazioni, vedere:  

-   [Scenari di Windows ADK per Windows 10 per i professionisti IT](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Scaricare Windows ADK per Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

### <a name="user-state-migration-tool-usmt"></a>Utilità di migrazione stato utente (USMT)  
 Configuration Manager usa un pacchetto USMT che contiene i file di origine di USMT 10 per acquisire e ripristinare lo stato utente nell'ambito della distribuzione del sistema operativo. Il programma di installazione di Configuration Manager crea automaticamente nel sito di livello superiore il pacchetto USMT. USMT 10 consente di acquisire lo stato utente da Windows 7, Windows 8, Windows 8.1 e Windows 10. USMT 10 è distribuito in Windows Assessment and Deployment Kit (Windows ADK) per Windows 10.  

 Per altre informazioni, vedere:  

-   [Scenari di migrazione comuni per USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Gestire lo stato utente](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE viene usato per le immagini di avvio per avviare un computer. Si tratta di un sistema operativo Windows con servizi limitati che viene usano durante la pre-installazione e la distribuzione dei sistemi operativi Windows. Di seguito sono riportate la versione di Configuration Manager e la versione supportata di Windows ADK, la versione di Windows PE su cui si basa l'immagine d'avvio che può essere personalizzata dalla console di Configuration Manager e le versioni di Windows PE su cui si basa l'immagine d'avvio che può essere personalizzata usando DISM e quindi aggiunta alla versione di Configuration Manager specificata.  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager versione 1511  
 Di seguito sono riportate la versione supportata di Windows ADK, la versione di Windows PE su cui si basa l'immagine d'avvio che può essere personalizzata dalla console di Configuration Manager e le versioni di Windows PE su cui è basata l'immagine d'avvio che è possibile personalizzare usando DISM e quindi aggiungere a Configuration Manager.  

-   **Versione di Windows ADK**  

     Windows ADK per Windows 10  

-   **Versioni di Windows PE per le immagini d'avvio personalizzabili dalla console di Configuration Manager**  

     Windows PE 10  

-   **Versioni di Windows PE supportate per le immagini d'avvio non personalizzabili dalla console di Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> È possibile aggiungere un'immagine d'avvio a Configuration Manager solo se è basata su Windows PE 3.1. Installare il supplemento Windows AIK per Windows 7 SP1 per aggiornare Windows AIK per Windows 7 (basato su Windows PE 3) con il supplemento Windows AIK per Windows 7 SP1 (basato su Windows PE 3.1). È possibile scaricare il supplemento Windows AIK per Windows 7 SP1 dall' [Area download Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Ad esempio, se si ha Configuration Manager, è possibile personalizzare le immagini d'avvio da Windows ADK per Windows 10 (basato su Windows PE 10) dalla console di Configuration Manager. Tuttavia, anche se le immagini di avvio basate su Windows PE 5 sono supportate, è necessario personalizzarle da un computer diverso e usare la versione di Gestione e manutenzione immagini distribuzione installata con Windows AIK per Windows 8. È quindi possibile aggiungere l'immagine d'avvio alla console di Configuration Manager. Per altre informazioni sui passaggi per personalizzare un'immagine d'avvio (aggiungere componenti e driver facoltativi), abilitare il supporto comandi nell'immagine d'avvio, aggiungere l'immagine d'avvio alla console di Configuration Manager e aggiornare i punti di distribuzione con l'immagine d'avvio, vedere [Customize boot images](../get-started/customize-boot-images.md) (Personalizzare le immagini d'avvio). Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini d'avvio con System Center Configuration Manager](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
È necessario installare i seguenti hotfix di WSUS 4.0:
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) è necessario per la manutenzione di Windows 10, che usa l'infrastruttura di aggiornamenti software per ottenere gli aggiornamenti delle funzionalità di Windows 10. Se si usa WSUS 3.2, è necessario usare sequenze di attività per aggiornare Windows 10. Per altre informazioni, vedere [Gestire Windows come servizio](../deploy-use/manage-windows-as-a-service.md).  
  - L'[hotfix 3159706](https://support.microsoft.com/kb/3159706) è necessario per usare la manutenzione di Windows 10 per aggiornare i computer a Windows 10 Anniversary Update e alle versioni successive. Per installare l'hotfix è necessario eseguire i passaggi manuali descritti nell'articolo del supporto tecnico. Per altre informazioni, vedere [Gestire Windows come servizio](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) nei server del sistema del sito  
 IIS è richiesto per il punto di distribuzione, il punto di migrazione stato e il punto di gestione. Per altre informazioni su questo requisito, vedere [Prerequisiti del sito e del sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>Servizi di distribuzione Windows (WDS)  
 WDS è necessario per le distribuzioni PXE, quando si usa il multicast per ottimizzare la larghezza di banda nelle distribuzioni e per la manutenzione offline delle immagini. Se il provider è installato in un server remoto, è necessario installare WDS nel server del sito e nel provider remoto. Per altre informazioni, vedere [Servizi di distribuzione Windows](#BKMK_WDS) in questo argomento.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration Protocol (DHCP)  
 DHCP è necessario per le distribuzioni PXE. È necessario un server DHCP funzionante con un host attivo per distribuire i sistemi operativi utilizzando PXE. Per altre informazioni sulle distribuzioni PXE, vedere [Usare PXE per distribuire Windows in rete](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemi operativi supportati e configurazioni del disco rigido  
 Per altre informazioni sulle versioni del sistema operativo e le configurazioni del disco rigido supportate da Configuration Manager quando vengono distribuiti i sistemi operativi, vedere [Sistemi operativi supportati](#BKMK_SupportedOS) e [Configurazioni supportate per il disco](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Driver di dispositivo Windows  
 È possibile utilizzare i driver di dispositivo Windows durante l'installazione del sistema operativo nel computer di destinazione e durante l'esecuzione di Windows PE tramite un'immagine di avvio. Per altre informazioni sui driver di dispositivo, vedere [Gestire i driver](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Dipendenze di Configuration Manager  
 Di seguito sono riportate informazioni sui prerequisiti di distribuzione del sistema operativo di Configuration Manager.  

### <a name="operating-system-image"></a>Immagine del sistema operativo  
 Le immagini del sistema operativo in Configuration Manager vengono archiviate in file in formato Windows Imaging (WIM) e rappresentano una raccolta compressa dei file e delle cartelle di riferimento necessari per installare e configurare correttamente un sistema operativo in un computer. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Catalogo driver  
 Per distribuire un driver di dispositivo, è necessario importare tale driver, attivarlo e renderlo disponibile in un punto di distribuzione accessibile dal client di Configuration Manager. Per altre informazioni sul catalogo driver, vedere [Gestire i driver](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Punto di gestione  
 I punti di gestione trasferiscono le informazioni tra i computer client e il sito di Configuration Manager. Il client utilizza un punto di gestione per eseguire le sequenze attività necessarie per completare la distribuzione del sistema operativo.  

 Per altre informazioni sulle sequenze di attività, vedere [Considerazioni sulla pianificazione dell'automazione delle attività](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Punto di distribuzione  
 I punti di distribuzione vengono utilizzati nella maggior parte delle distribuzioni per archiviare i dati utilizzati per distribuire un sistema operativo, quali l'immagine del sistema operativo o i pacchetti driver di dispositivo. In genere, le sequenze attività recuperano i dati da un punto di distribuzione per distribuire il sistema operativo.  

 Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>Punto di distribuzione che supporta PXE  
 Per distribuire le distribuzioni avviate da PXE, è necessario configurare un punto di distribuzione in modo che accetti le richieste PXE dai client. Per altre informazioni, vedere [Configurare un punto di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Punto di distribuzione abilitato per multicast  
 Per ottimizzare le distribuzioni del sistema operativo tramite multicast, è necessario configurare un punto di distribuzione per il supporto di multicast. Per altre informazioni, vedere [Configurare un punto di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Punto di migrazione stato  
 Quando vengono acquisiti e ripristinati i dati sullo stato dell'utente per distribuzioni side-by-side e di aggiornamento, è necessario configurare un punto di migrazione stato per archiviare i dati sullo stato dell'utente in un altro computer.  

 Per altre informazioni su come configurare il punto di migrazione stato, vedere [Punto di migrazione stato](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)  

 Per altre informazioni su come acquisire e ripristinare lo stato utente, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>punto di connessione del servizio  
 Quando si usa Windows come servizio (WaaS) per distribuire il ramo corrente di Windows 10, è necessario installare il punto di connessione del servizio. Per altre informazioni, vedere [Gestire Windows come servizio](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Punto di Reporting Services  
 Per usare i report di Configuration Manager per le distribuzioni del sistema operativo, è necessario installare e configurare un punto di Reporting Services. Per altre informazioni, vedere [Reporting](../../core/servers/manage/reporting.md) (Creazione di report).  

### <a name="security-permissions-for-operating-system-deployments"></a>Autorizzazioni di sicurezza per le distribuzioni del sistema operativo  
 Il ruolo di sicurezza **Gestione distribuzione del sistema operativo** è un ruolo incorporato e non può essere modificato. Tuttavia, è possibile copiare il ruolo, apportare modifiche e quindi salvare tali modifiche come un nuovo ruolo di sicurezza personalizzato. Di seguito vengono riportate alcune delle autorizzazioni che si applicano direttamente alle distribuzioni del sistema operativo:  

-   **Pacchetto immagine d'avvio**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

-   **Driver dispositivo**: Crea, Elimina, Modifica, Modifica cartella, Modifica report, Sposta oggetto, Lettura, Esegui report  

-   **Pacchetto driver**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

-   **Immagine del sistema operativo**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

-   **Pacchetto di installazione sistema operativo**: Crea, Elimina, Modifica, Modifica cartella, Sposta oggetto, Lettura, Imposta ambito di protezione  

-   **Pacchetto sequenza di attività**: Crea, Crea supporto per sequenza di attività, Elimina, Modifica, Modifica cartella, Modifica report, Sposta oggetto, Lettura, Esegui report, Imposta ambito di protezione  

 Per altre informazioni sui ruoli di sicurezza personalizzati, vedere [Creare ruoli di sicurezza personalizzati](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Ambiti di protezione per le distribuzioni del sistema operativo  
 Utilizzare gli ambiti di protezione per consentire agli utenti amministratori di accedere agli oggetti a protezione diretta utilizzati nelle distribuzioni del sistema operativo, quali immagini di avvio e del sistema operativo, pacchetti driver e pacchetti sequenza attività. Per altre informazioni, vedere [Ambiti di protezione](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Servizi di distribuzione Windows  
 È necessario installare Servizi di distribuzione Windows (WDS) sullo stesso server dei punti di distribuzione configurati per il supporto PXE o di multicast. Servizi di distribuzione Windows è incluso nel sistema operativo del server. Per le distribuzioni PXE, WDS è il servizio che esegue l'avvio PXE. Quando il punto di distribuzione viene installato e attivato per PXE, Configuration Manager installa un provider in WDS che usa le funzioni di avvio PXE di WDS.  

> [!NOTE]  
>  L'installazione di WDS potrebbe non riuscire se il server richiede un riavvio.  

 È necessario considerare altre configurazioni di WDS, tra cui:  

-   Per l'installazione di WDS sul server è necessario che l'amministratore sia un membro del gruppo di amministratori locali.  

-   È necessario che il server di WDS sia membro di un dominio Active Directory oppure controller di dominio per un dominio Active Directory. Tutte le configurazioni della foresta e del dominio di Windows supportano WDS.  

-   Se il provider è installato in un server remoto, è necessario installare WDS nel server del sito e nel provider remoto.  

###  <a name="BKMK_WDSandDHCP"></a> Considerazioni in presenza di Servizi di distribuzione Windows e DHCP nello stesso server  
 Se si prevede di co-ospitare il punto di distribuzione in un server DHCP, prendere in considerazione i seguenti aspetti di configurazione.  

-   È necessario disporre di un server DHCP funzionante con un ambito attivo. I Servizi di distribuzione Windows utilizzano PXE, che richiede un server DHCP.  

-   DHCP e i Servizi di distribuzione Windows richiedono entrambi il numero di porta 67. Se si co-ospitano i Servizi di distribuzione Windows e DHCP, è possibile spostare DHCP o il punto di distribuzione configurato per PXE su un server separato. In alternativa, è possibile utilizzare la procedura seguente per configurare il server dei Servizi di distribuzione Windows in modo che sia in ascolto su una porta diversa.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>Per configurare il server dei Servizi di distribuzione Windows in modo che sia in ascolto su una porta diversa  

    1.  Modificare la seguente chiave del Registro di sistema:  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Impostare il valore del Registro di sistema su: **UseDHCPPorts = 0**  

    3.  Affinché la nuova configurazione abbia effetto, è necessario eseguire il comando seguente sul server:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   È necessario un server DNS per l'esecuzione dei Servizi di distribuzione Windows.  

-   Le seguenti porte UDP devono essere aperte sul server dei Servizi di distribuzione Windows.  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Inoltre, se è necessaria l'autorizzazione DHCP sul server, occorre che la porta del client DHCP 68 sia aperta sul server.  

##  <a name="BKMK_SupportedOS"></a> Sistemi operativi supportati  
 Tutti i sistemi operativi Windows indicati come sistemi operativi client supportati in [Sistemi operativi supportati per client e dispositivi](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) sono supportati per le distribuzioni del sistema operativo.  

##  <a name="BKMK_SupportedDiskConfig"></a> Configurazioni del disco supportate  
 Le combinazioni di configurazioni del disco rigido nei computer di riferimento e di destinazione supportate per la distribuzione del sistema operativo di Configuration Manager sono visualizzate nella tabella seguente.  

|Configurazione del disco rigido del computer di riferimento|Configurazione del disco rigido del computer di destinazione|  
|------------------------------------------------|--------------------------------------------------|  
|Disco di base|Disco di base|  
|Volume semplice su un disco dinamico|Volume semplice su un disco dinamico|  

 Configuration Manager supporta l'acquisizione di un'immagine del sistema operativo solo da computer configurati con volumi semplici. Le seguenti configurazioni del disco rigido non sono supportate:  

-   Volumi con spanning  

-   Volumi con striping (RAID 0)  

-   Volumi con mirroring (RAID 1)  

-   Volumi di parità (RAID 5)  

 Nella tabella seguente viene elencata una configurazione del disco rigido aggiuntiva nei computer di riferimento e di destinazione non supportata con la distribuzione del sistema operativo di Configuration Manager.  

|Configurazione del disco rigido del computer di riferimento|Configurazione del disco rigido del computer di destinazione|  
|------------------------------------------------|--------------------------------------------------|  
|Disco di base|Disco dinamico|  

## <a name="next-steps"></a>Passaggi successivi
[Prepare for operating system deployment](../get-started/prepare-for-operating-system-deployment.md) (Preparare la distribuzione del sistema operativo)

