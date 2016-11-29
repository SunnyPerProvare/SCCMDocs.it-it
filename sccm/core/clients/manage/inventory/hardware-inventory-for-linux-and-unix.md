---
title: Inventario hardware | Linux UNIX |System Center Configuration Manager
description: Informazioni su come usare l'inventario hardware per Linux e UNIX in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
caps.latest.revision: 6
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d0db2afd9a16daf4069a746a8dda59895048ca53


---
# <a name="hardware-inventory-for-linux-and-unix-in-system-center-configuration-manager"></a>Inventario hardware per Linux e UNIX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il client di System Center Configuration Manager per Linux e UNIX supporta l'inventario hardware. Dopo aver eseguito l'inventario hardware, è possibile visualizzarlo in Esplora inventario risorse o nei report di Configuration Manager e usare le informazioni per creare query e raccolte che consentono le operazioni seguenti:  

-   Distribuzione software  

-   Imposizione delle finestre di manutenzione  

-   Distribuzione di impostazioni client personalizzate  

 La funzionalità di inventario hardware per server Linux e UNIX usa un server CIM (Common Information Model) basato su standard. Il server CIM viene eseguito come servizio software (o daemon) e fornisce un'infrastruttura di gestione basata sugli standard DMTF (Distributed Management Task Force). Il server CIM fornisce funzionalità simili alle funzionalità CIM WMI (Windows Management Infrastructure) disponibili nei computer basati su Windows.  

 A partire dall'aggiornamento cumulativo 1, il client per Linux e UNIX usa **omiserver** versione 1.0.6 open source di **The Open Group**. Prima dell'aggiornamento cumulativo 1, il client usava **nanowbem** come server CIM.  

 Il server CIM viene installato come parte del client per Linux e UNIX. Il client per Linux e UNIX comunica direttamente con il server CIM e non usa l'interfaccia WS-MAN del server CIM. La porta WS-MAN nel server CIM viene disabilitata quando si installa il client. Microsoft ha sviluppato il server CIM che è ora disponibile come open source tramite il progetto OMI (Open Management Infrastructure). Per altre informazioni sul progetto OMI, vedere il sito Web di [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) .  

 L'inventario hardware nei server Linux e UNIX funziona tramite il mapping delle classi e proprietà WMI Win32 esistenti alle classi e proprietà equivalenti per i server Linux e UNIX. Questo mapping uno-a-uno di classi e proprietà consente l'integrazione dell'inventario hardware di Linux e UNIX con Configuration Manager. I dati di inventario dai server Linux e UNIX vengono visualizzati insieme all'inventario dai computer basati su Windows nella console e nei report di Configuration Manager. Ciò offre un'esperienza di gestione eterogenea e coerente.  

> [!TIP]  
>  È possibile usare il valore **Didascalia** per la classe **Sistema operativo** per identificare i diversi sistemi operativi Linux e UNIX nelle query e nelle raccolte.  

##  <a name="a-namebkmkconfighardwareforlnua-configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Configurazione dell'inventario hardware per server Linux e UNIX  
 Per configurare l'inventario hardware, è possibile usare le impostazioni client predefinite o creare impostazioni personalizzate per i dispositivi client. Quando si usano impostazioni personalizzate per i dispositivi client, è possibile configurare le classi e proprietà da raccogliere solo dai server Linux e UNIX. È anche possibile specificare pianificazioni personalizzate per stabilire quando raccogliere inventari completi e differenziali dai server Linux e UNIX.  

 Il client per Linux e UNIX supporta le seguenti classi di inventario hardware disponibili nei server Linux e UNIX:  

-   Win32_BIOS  

-   Win32_ComputerSystem  

-   Win32_DiskDrive  

-   Win32_DiskPartition  

-   Win32_NetworkAdapter  

-   Win32_NetworkAdapterConfiguration  

-   Win32_OperatingSystem  

-   Win32_Process  

-   Win32_Service  

-   Win32Reg_AddRemovePrograms  

-   SMS_LogicalDisk  

-   SMS_Processor  

 Non tutte le proprietà di queste classi di inventario sono abilitate per i computer Linux e UNIX in Configuration Manager.  

##  <a name="a-namebkmkoperationsforhardwareforlnua-operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Operazioni per l'inventario hardware  
 Dopo aver raccolto l'inventario hardware dai server Linux e UNIX, è possibile visualizzare e usare tali informazioni con le stesse modalità valide per l'inventario raccolto dagli altri computer:  

-   Usare Esplora inventario risorse per visualizzare informazioni dettagliate relative all'inventario hardware dai server Linux e UNIX  

-   Creare query basate su una configurazione hardware specifica  

-   Creare raccolte basate su query secondo configurazioni hardware specifiche  

-   Eseguire i report che consentono di visualizzare informazioni dettagliate specifiche sulle configurazioni hardware  

 L'inventario hardware in un server Linux o UNIX viene eseguito in base alla pianificazione configurata nelle impostazioni client. L'intervallo predefinito è di sette giorni. Il client per Linux e UNIX supporta sia cicli di inventario completo che cicli di inventario differenziale.  

 È anche possibile imporre l'esecuzione immediata dell'inventario hardware per il client in un server Linux o UNIX. Per eseguire l'inventario hardware, in un client usare credenziali **root** per eseguire il comando seguente per avviare un ciclo di inventario hardware: **/opt/microsoft/configmgr/bin/ccmexec -rs hinv**  

 Le azioni per l'inventario hardware vengono immesse nel file di log client **scxcm.log**.  

##  <a name="a-namebkmkcustomhinvforlinuxa-how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Come usare OMI (Open Management Infrastructure) per creare un inventario hardware personalizzato  
 Il client per Linux e UNIX supporta l'inventario hardware personalizzato che è possibile creare tramite OMI (Open Management Infrastructure). A tale scopo, seguire questa procedura:  

1.  Creare un provider di inventario personalizzato usando l'origine OMI  

2.  Configurare i computer in modo che usino il nuovo provider per l'inventario  

3.  Abilitare Configuration Manager per supportare il nuovo provider  

###  <a name="a-namebkmklinuxprovidera-create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Creare un provider di inventario hardware personalizzato per i computer Linux e UNIX:  
 Per creare un provider di inventario hardware personalizzato per il client di Configuration Manager per Linux e UNIX, usare **OMI Source - v.1.0.6** e seguire le istruzioni della guida introduttiva a OMI. Questo processo include la creazione di un file MOF (Managed Object Format) che definisce lo schema del nuovo provider. Importare successivamente il file MOF in Configuration Manager per abilitare il supporto della nuova classe di inventario personalizzato.  

 Sia OMI Source - v.1.0.6 che la guida introduttiva a OMI sono disponibili per il download dal sito Web di [The Open Group](http://go.microsoft.com/fwlink/p/?LinkId=262317) . È possibile trovare questi download nella scheda **Documents** della pagina Web seguente nel sito Web OpenGroup.org: [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="a-namebkmkaddprovidertolinuxa-configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Configurare ogni computer che esegue Linux o UNIX con il provider di inventario hardware personalizzato:  
 Dopo aver creato un provider di inventario personalizzato, è necessario copiare e quindi registrare il file della libreria del provider in ogni computer da cui si vuole raccogliere l'inventario.  

1.  Copiare la libreria del provider in ogni computer Linux e UNIX da cui si vuole raccogliere l'inventario. Il nome della libreria del provider è simile al seguente: **XYZ_MyProvider.so**  

2.  Registrare poi la libreria del provider nel server OMI in ogni computer Linux e UNIX. Il server OMI viene installato nel computer quando si installa il client di Configuration Manager per Linux e UNIX. È necessario tuttavia registrare manualmente i provider personalizzati. Usare la riga di comando seguente per registrare il provider: **/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so**  

3.  Dopo aver registrato il nuovo provider, testarlo con lo strumento **omicli** . Lo strumento **omicli** viene installato in ogni computer Linux e UNIX quando si installa il client di Configuration Manager per Linux e UNIX. Ad esempio, eseguire il comando seguente nel computer, in cui **XYZ_MyProvider** è il nome del provider creato: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Per informazioni su **omicli** e sui test dei provider personalizzati, vedere la guida introduttiva a OMI.  

> [!TIP]  
>  Usare la distribuzione software per distribuire i provider personalizzati e per registrarli in ogni computer client Linux e UNIX.  

###  <a name="a-namebkmkaddlinuxprovidertocma-enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Abilitare la nuova classe di inventario in Configuration Manager:  
 Prima che Configuration Manager possa elaborare l'inventario fornito dal nuovo provider nei computer Linux e UNIX, è necessario importare il file MOF (Managed Object Format) che definisce lo schema del provider personalizzato.  

 Per importare un file MOF personalizzato in Configuration Manager, vedere [Come configurare l'inventario hardware in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  



<!--HONumber=Nov16_HO1-->

