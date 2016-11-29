---
title: 'Differenze rispetto a Configuration Manager 2012 | System Center Configuration Manager '
description: "Identificare le modifiche e le nuove funzionalità di System Center Configuration Manager rispetto a System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: 51
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f3b68fb17920b0abacc1428c8763ec8c06e6b22


---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Novità in System Center Configuration Manager rispetto a System Center 2012 Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Il ramo corrente di System Center Configuration Manager introduce importanti modifiche rispetto a System Center 2012 Configuration Manager. Le informazioni contenute in questo argomento identificano le modifiche più significative e le nuove funzionalità disponibili nella versione di base 1511 di System Center Configuration Manager. Per informazioni sulle altre modifiche introdotte negli aggiornamenti successivi per System Center Configuration Manager, vedere l'argomento relativo alle [novità delle versioni incrementali di System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 La versione di dicembre 2015 di System Center Configuration Manager (versione 1511) è la versione più recente di Configuration Manager da Microsoft.   Viene indicata generalmente come System Center Configuration Manager (Current Branch). *Current Branch*, ovvero ramo corrente, indica che si tratta di una versione che supporta aggiornamenti incrementali del prodotto e che può esservi una differenza rilevante tra questa e le versioni precedenti di Configuration Manager.  

 Con questa versione System Center Configuration Manager:  

-   Non usa un identificatore di anno o prodotto nel nome del prodotto, come in versioni precedenti come Configuration Manager 2007 o System Center 2012 Configuration Manager.

-   Supporta gli aggiornamenti di prodotto incrementali, definite anche versioni di aggiornamento. La versione iniziale è la versione 1511. Le versioni successive vengono rilasciate più volte all'anno come aggiornamenti nella console, come la versione 1602 o 1606.




##  <a name="a-namebkmkupdatesa-in-console-updates-for-configuration-manager"></a><a name="bkmk_updates"></a> Aggiornamenti eseguiti nella console per Configuration Manager  
 System Center Configuration Manager usa un metodo di manutenzione nella console denominato **Aggiornamenti e manutenzione** che semplifica l'individuazione e quindi l'installazione degli aggiornamenti consigliati per l'infrastruttura di Configuration Manager.  

 Alcune versioni sono disponibili solo come aggiornamenti per i siti esistenti (dall'interno della console di Configuration Manager) e non possono essere usati per installare nuovi siti di Configuration Manager.   
Ad esempio, l'aggiornamento 1602 è disponibile solo nella console di Configuration Manager e viene usato per aggiornare un sito che esegue una versione di base 1511 alla versione 1602.  

Periodicamente, verrà rilasciata anche una versione di aggiornamento come nuova versione di base (ad esempio, 1606) che può essere usata per installare una nuova gerarchia senza dover iniziare con una versione di base precedente (ad esempio, 1511) ed eseguire subito l'aggiornamento alla versione più recente.


 Per altre informazioni sull'uso degli aggiornamenti, vedere [Aggiornamenti per System Center Configuration Manager](../../../core/servers/manage/updates.md).  

##  <a name="a-namebkmkservicepointa-service-connection-point-replaces-microsoft-intune-connector"></a><a name="bkmk_servicepoint"></a> Il punto di connessione del servizio sostituisce il connettore Microsoft Intune  
 Il **connettore Microsoft Intune** viene sostituito dal **punto di connessione del servizio**, un nuovo ruolo del sistema del sito che consente di aggiungere ulteriori funzionalità. Il punto di connessione del servizio:  

-   Sostituisce il connettore Microsoft Intune durante l'integrazione di Intune con la funzionalità di gestione locale dei dispositivi mobili in System Center Configuration Manager  

-   Viene usato come punto di contatto per i dispositivi gestiti con  

-   Carica i dati di utilizzo relativi alla distribuzione nel servizio cloud Microsoft  

-   Rende disponibili gli aggiornamenti pertinenti alla distribuzione dall'interno della console di Configuration Manager  

Questo ruolo del sistema del sito supporta sia una modalità online che una modalità offline di funzionamento che può influenzare il relativo utilizzo aggiuntivo. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="a-namebkmkusagea-usage-data-collection"></a><a name="bkmk_usage"></a> Raccolta dei dati di utilizzo  
 System Center Configuration Manager raccoglie dati di utilizzo relativi ai siti e all'infrastruttura. Le informazioni vengono compilate e inviate al servizio cloud Microsoft dal punto di connessione di servizio (un nuovo ruolo del sistema del sito) ed è necessario abilitare Configuration Manager per scaricare gli aggiornamenti per la distribuzione che si applicano alla versione di Configuration Manager in uso. Quando si configura il punto di connessione del servizio è possibile configurare sia il livello di dati raccolti sia la modalità di invio, che può essere automatica (modalità online) o manuale (modalità offline).  

 Per altre informazioni, vedere [Usage data levels and settings](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="a-namebkmkamta-support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Supporto per la tecnologia Intel AMT (Active Management Technology)  
 Con System Center Configuration Manager il supporto nativo per i computer basati su AMT dalla console di Configuration Manager è stato rimosso.  

-   I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   L'uso del componente aggiuntivo consente di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche  

-   La gestione fuori banda in System Center 2012 Configuration Manager non è interessata da questa modifica.  

La rimozione della tecnologia AMT integrata per System Center Configuration Manager include:  

-   Il ruolo del sistema del sito per il punto di gestione fuori banda non viene più usato e non è più disponibile  

##  <a name="a-namebkmkouta-deprecated-functionality"></a><a name="bkmk_out"></a> Funzionalità obsolete  
 Con System Center Configuration Manager alcune funzionalità, ad esempio il [supporto nativo per i computer basati sulla tecnologia Intel AMT (Active Management Technology)](#bkmk_AMT), vengono rimosse dalla console di Configuration Manager, mentre altre funzionalità come Protezione accesso alla rete vengono rimosse completamente. Inoltre, alcuni prodotti Microsoft precedenti come Windows Vista, Windows Server 2008 e SQL Server 2008 non sono più supportati.  

 Per un elenco delle funzionalità deprecate, vedere [Funzionalità rimosse e deprecate per System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Per informazioni dettagliate su prodotti, configurazioni e sistemi operativi supportati, vedere [Configurazioni supportate per System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Distribuzione client  
 System Center Configuration Manager introduce una nuova funzionalità per testare le nuove versioni del client di Configuration Manager prima di aggiornare il resto del sito con il nuovo software.  La nuova funzionalità offre l'opportunità di configurare una raccolta di preproduzione in cui si eseguire la distribuzione pilota di un nuovo client. Quando si sarà soddisfatti del software del nuovo client in fase di preproduzione, è possibile promuovere il client per aggiornare automaticamente il resto del sito con la nuova versione.  

 Per altre informazioni su come testare i client, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

-   Un nuovo tipo di sequenza di attività è disponibile nella Creazione guidata della sequenza di attività  **Aggiorna sistema operativo dal pacchetto di aggiornamento**, che crea i passaggi per aggiornare i computer da Windows 7, Windows 8 o Windows 8.1 a Windows 10.  Per ulteriori informazioni, vedere [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   La cache peer di Windows PE è disponibile quando si distribuiscono sistemi operativi. I computer che eseguono la sequenza di attività possono usare la peer cache di Windows PE per ottenere contenuto da un peer locale (un'origine peer cache) invece di scaricarlo da un punto di distribuzione. In tal modo il traffico WAN viene ridotto al minimo negli scenari con le filiali, in cui non esiste un punto di distribuzione locale. Per altre informazioni, vedere [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Ora è possibile visualizzare lo stato di Windows come servizio nell'ambiente in uso, creare piani di manutenzione per formare anelli di distribuzione, verificare che i computer con rami correnti di Windows 10 siano mantenuti aggiornati quando vengono rilasciate nuove build e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto per la build in uso di Current Branch (CB) o Current Branch for Business (CBB). Per altre informazioni, vedere [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Gestione delle applicazioni  

-   System Center Configuration Manager consente di distribuire app della piattaforma UWP (Universal Windows Platform) per i dispositivi che eseguono Windows 10 e versioni successive. Vedere [Creazione di applicazioni Windows con System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Software Center ha un aspetto nuovo e moderno e le app che in precedenza venivano visualizzate solo nel Catalogo applicazioni (app disponibili per gli utenti) ora compaiono in Software Center nella scheda Applicazioni. In tal modo, queste distribuzioni sono maggiormente individuabili per gli utenti, che pertanto non dovranno più usare necessariamente il Catalogo applicazioni. Inoltre, non è più richiesto un browser abilitato per Silverlight. Vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   Il nuovo tipo di applicazione Windows Installer tramite MDM consente di creare e distribuire app basate su Windows Installer nei PC registrati che eseguono Windows 10. Vedere [Creazione di applicazioni Windows con System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Quando si crea un'applicazione per un'app iOS interna, è necessario solo specificare il file del programma di installazione (con estensione IPA) per l'app. Non è più necessario specificare un file di elenco di proprietà (con estensione PLIST) corrispondente. Vedere [Creazione di applicazioni iOS con System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   In Configuration Manager 2012, per specificare un collegamento a un'app in Windows Store, era possibile specificare direttamente il collegamento oppure passare a un computer remoto in cui era installata l'app. In System Center Configuration Manager è possibile immettere direttamente il collegamento ma è anche possibile cercare l'app nell'archivio direttamente dalla console di Configuration Manager anziché passare a un computer di riferimento.  

## <a name="software-updates"></a>Aggiornamenti software  

-   System Center Configuration Manager ora è in grado di distinguere un computer Windows 10 che si connette a Windows Update for Business (WUfB) per gestire gli aggiornamenti software dai computer connessi a WSUS per la gestione degli aggiornamenti software. L'attributo **UseWUServer** è nuovo e specifica se il computer viene gestito con WUfB. È possibile usare questa impostazione in una raccolta per rimuovere questi computer dalla gestione degli aggiornamenti software. Per altre informazioni, vedere [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   È ora possibile pianificare ed eseguire l'attività di pulizia WSUS dalla console di Configuration Manager.  
    A questo punto è possibile eseguire manualmente l'attività di pulizia WSUS nelle proprietà del componente del punto di aggiornamento software. Quando si sceglie di eseguire l'attività di pulizia WSUS, questa verrà eseguita alla successiva sincronizzazione degli aggiornamenti software. Gli aggiornamenti software scaduti verranno impostati su uno stato rifiutato nel server WSUS e l'Agente di Windows Update nei computer non eseguirà più la scansione di questi aggiornamenti software. Per ulteriori informazioni, vedere [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Impostazioni di conformità  

-   System Center Configuration Manager introduce un flusso di lavoro ottimizzato per la creazione degli elementi di configurazione. Ora, quando si crea un elemento di configurazione e si selezionano le piattaforme supportate, sono disponibili solo le impostazioni rilevanti per tale piattaforma. Vedere [Introduzione alle impostazioni di conformità in System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   La Creazione guidata dell'elemento di configurazione semplifica la scelta del tipo di elemento di configurazione che si vuole creare. Inoltre, sono disponibili elementi di configurazione nuovi e aggiornati per:  

    -   Dispositivi Windows 10 gestiti con il client di Configuration Manager  

    -   Dispositivi OS X gestiti con il client di Configuration Manager  

    -   Computer desktop e server Windows gestiti con il client di Configuration Manager  

    -   Dispositivi Windows 8.1 e Windows 10 gestiti senza il client di Configuration Manager  

    -   Dispositivi Windows Phone gestiti senza il client di Configuration Manager  

    -   Dispositivi iOS e Mac OS X gestiti senza il client di Configuration Manager  

    -   Dispositivi Android e Samsung KNOX gestiti senza il client di Configuration Manager  

     Vedere [Come creare elementi di configurazione in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Supporto per la gestione delle impostazioni nei computer Mac OS X che possono essere registrati con Microsoft Intune o gestiti con il client di Configuration Manager. Vedere [Come creare elementi di configurazione per dispositivi iOS e Mac OS X gestiti senza il client System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Proteggere dati e infrastruttura del sito  
-   System Center Configuration Manager consente di eseguire l'integrazione con Windows Hello for Business (in precedenza Microsoft Passport for Work), un metodo di accesso alternativo che usa Active Directory o un account di Azure Active Directory per sostituire una password, una smart card o una smart card virtuale su dispositivi che eseguono Windows 10. Vedere [Impostazioni di Windows Hello for Business in System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Gestione dei dispositivi mobili con Microsoft Intune  
 In System Center Configuration Manager sono stati introdotti miglioramenti per la gestione dei dispositivi mobili, tra cui:  

-   Limitazione del numero di dispositivi che può registrare un utente  

-   Definizione dei termini e delle condizioni che gli utenti del portale aziendale devono accettare per poter registrare o usare l'app  

-   Aggiunta di un ruolo di manager di registrazione dispositivi che consente di gestire un numero elevato di dispositivi  

Per altre informazioni sulle funzionalità di gestione dei dispositivi mobili con Configuration Manager e Intune, vedere [Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Gestione dei dispositivi mobili (MDM) locale  
 Con System Center Configuration Manager è ora possibile gestire i dispositivi mobili usando l'infrastruttura locale di Configuration Manager. Tutti i dati di gestione e la gestione dei dispositivi vengono gestiti in locale e non fanno parte di Microsoft Intune o altri servizi cloud. Questo tipo di gestione dei dispositivi non richiede il software client perché le funzionalità usate da Configuration Manager per gestire i dispositivi sono integrate nei sistemi operativi dei dispositivi.  

 Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).



<!--HONumber=Nov16_HO1-->

