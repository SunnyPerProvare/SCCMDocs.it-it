---
title: "Funzionalità della versione Technical Preview 1703 per Configuration Manager"
description: "Informazioni sulle funzionalità disponibili nella versione Technical Preview 1703 per System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f4cb711f369698fe8e045f8c83dd96ec6fb29d70
ms.openlocfilehash: bb1b96a56db68dcea22270855b899ba3a90afd0d
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Funzionalità della versione Technical Preview 1703 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo presenta le funzionalità disponibili nella versione Technical Preview 1703 per System Center Configuration Manager. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi

È ora possibile distribuire app con licenza sia ai dispositivi che agli utenti. In base alla possibilità dell'app di supportare la gestione delle licenze dei dispositivi, al momento della distribuzione verrà richiesta una licenza appropriata, come indicato di seguito:

|||||
|-|-|-|-|
|Versione di Configuration Manager|Gestione delle licenze dei dispositivi supportata|Tipo di raccolta della distribuzione|Licenza richiesta|
|Precedente la 1702|Sì|utente|Licenza utente|
|Precedente la 1702|No|utente|Licenza utente|
|Precedente la 1702|Sì|Dispositivo|Licenza utente|
|Precedente la 1702|No|Dispositivo|Licenza utente|
|1702 e versioni successive|Sì|utente|Licenza utente|
|1702 e versioni successive|No|utente|Licenza utente|
|1702 e versioni successive|Sì|Dispositivo|Licenza dispositivo|
|1702 e versioni successive|No|Dispositivo|Licenza utente|

Per altre informazioni sulle app iOS acquistate tramite Volume Purchase Program, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Collegamenti diretti alle applicazioni in Software Center

È ora possibile fornire agli utenti finali un collegamento diretto a un'applicazione in Software Center. Questo significa che non è più necessario aprire Software Center e cercare un'applicazione prima di poterla installare. Questa funzionalità è disponibile solo per le applicazioni di Configuration Manager applicazioni e non per pacchetti e programmi o sequenze di attività.

### <a name="try-it-out"></a>Procedura                 

Usare il formato di URL seguente per aprire Software Center per una determinata applicazione:

**Softwarecenter:SoftwareId =*Identificatore dell'applicazione***

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Come ottenere l'identificatore dell'applicazione di un'applicazione

1.    Nella console di Configuration Manager fare clic su **Raccolta software**.
2.    Nell'area di lavoro Raccolta software espandere **Gestione applicazioni** e quindi fare clic su **Applicazioni**.
3.    Nella visualizzazione **Applicazioni** fare clic con il pulsante destro del mouse su una delle intestazioni di colonna e quindi scegliere **ID CI univoco** nell'elenco. Si noterà che l'ID univoco di ogni applicazione viene ora visualizzato nell'elenco.
4.    Prendere nota dell'**ID CI univoco** dell'applicazione per cui si vuole fornire un collegamento, ad esempio: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.    Rimuovere quindi qualsiasi testo che segue il GUID dell'applicazione. In questo caso **/2**. Rimane così l'identificatore dell'applicazione.
6.    Per completare la creazione del collegamento, anteporre **Softwarecenter:SoftwareID=**. Con riferimento all'esempio precedente, il collegamento finale sarà: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Gli utenti possono usare questo collegamento per aprire Software Center direttamente nell'applicazione specificata.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificati PFX per i computer client Windows di Configuration Manager

È ora possibile distribuire i profili di certificato PFX importati nei computer client di Configuration Manager che eseguono Windows 10.

### <a name="try-it-out"></a>Procedura

Usare le istruzioni in [Come creare profili certificato PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) per importare un profilo PFX, distribuire il profilo e quindi verificare se il certificato è stato installato per l'utente interessato.



## <a name="configure-azure-services-wizard"></a>Configurazione guidata servizi di Azure
La versione Technical Preview 1703 introduce la **Configurazione guidata servizi di Azure**. Questa procedura guidata offre un'esperienza di configurazione comune che sostituisce i singoli flussi di lavoro per configurare i servizi cloud usati con Configuration Manager. Questo risultato si ottiene usando un'**app Web di Azure** per fornire i dettagli di sottoscrizione e configurazione, che in caso contrario devono essere immessi ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure.

Nella versione Technical Preview 1703 solo Windows Store per le aziende Business (WSfB) viene configurato con questa procedura guidata.  Gli altri servizi cloud vengono configurati usando i flussi di lavoro corrispondenti separati.

-    Usare le informazioni disponibili in questo argomento di anteprima in sostituzione della procedura di configurazione descritta nella sezione [Configurare la sincronizzazione di Windows Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) dell'argomento per la versione Current Branch [Gestire le app da Windows Store per le aziende con System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-    Per altre informazioni sulle app Web, vedere [Autenticazione e autorizzazione nel servizio app di Azure](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) e [Panoramica di App Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Prerequisiti e pianificazione
Quando si configura una connessione tra Configuration Manager e Windows Store per le aziende, è necessario specificare una cartella in cui verranno mantenuti i contenuti delle app sincronizzati dall'archivio. Per assicurarsi che questa cartella sia protetta e che il relativo contenuto possa essere distribuito ai dispositivi, verificare che siano disponibili le autorizzazioni seguenti:
-    Il computer in cui si installa il ruolo del sistema del sito del punto di connessione del servizio (sito di livello superiore nella gerarchia) deve essere in possesso delle autorizzazioni lettura e scrittura per la cartella specificata quando si usa l'account **Computer$**.  

-    L'autore di app deve essere in possesso delle autorizzazioni di lettura per la cartella specificata.  

-    L'account **Computer$** di ogni computer che ospita un'istanza del provider SMS deve essere in grado di usare la cartella specificata.

In Azure Active Directory registrare Configuration Manager come strumento di gestione di applicazioni Web o API Web. Viene così creato l'ID client che sarà necessario in seguito.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Usare la procedura guidata per configurare il servizio cloud WSfB

1. Nella console passare a **Amministrazione** > **Panoramica** > **Cloud Services Management (Gestione dei servizi cloud)** > **Azure** > **Servizi di Azure** e quindi scegliere **Configure Azure Services (Configura servizi di Azure)** per avviare **Azure Services Wizard (Configurazione guidata servizi di Azure)**.

2. Nella pagina **Servizi di Azure** selezionare il servizio che si vuole configurare e quindi fare clic su **Avanti**. In questa versione di anteprima è possibile configurare solo WSfB.

3. Nella pagina **Generale** specificare un nome descrittivo per **Nome del servizio Azure** e una descrizione facoltativa, quindi fare clic su **Avanti**.

4. Nella pagina **App** specificare l'ambiente di Azure e quindi fare clic su **Sfoglia** per aprire la finestra Server App (App server).

5. Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**.
Le app server sono app Web di Azure che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client. Se non è disponibile un'app server, usare una delle opzioni seguenti:
  -    **Crea**: per creare una nuova app server, fare clic su **Crea**. Specificare un nome descrittivo per l'app e il tenant. Quindi, dopo avere effettuato l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, inclusi l'ID Client e la chiave privata da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.
  -    **Importa**: per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver fatto clic su **Verifica** per verificare le informazioni, fare clic su **OK** per continuare.  </br></br>

6. Controllare la pagina **Informazioni** ed eseguire gli eventuali passaggi aggiuntivi e le configurazioni indicati. Queste configurazioni sono necessarie per usare il servizio con Configuration Manager.
Ad esempio, per configurare WSfB:

  1. In Azure è necessario registrare Configuration Manager come applicazione Web o API Web e registrare l'ID client. È anche necessario specificare una chiave client utilizzabile dallo strumento di gestione, ovvero Configuration Manager.

  2.    Nella console di WSfB è necessario configurare Configuration Manager come strumento di gestione dello Store, abilitare il supporto per le app con licenza offline e quindi acquistare almeno un'app.   </br>

  Quando si è pronti per continuare, fare clic su **Avanti**.

7. Nella pagina **Configurazioni dell'applicazione** completare le configurazioni per il catalogo app e la lingua per il servizio, quindi fare clic su **Avanti**.
8. Al termine della procedura guidata, nella console di Configuration Manager viene indicato che **Windows Store per le aziende** è stato configurato come **Tipo di servizio cloud**.

È ora possibile usare il resto del [contenuto Current Branch](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) per gestire le app da WSfB per sincronizzare, creare, distribuire e monitorare le app di Windows Store per le aziende.

### <a name="modify-a-cloud-service-configuration"></a>Modificare la configurazione di un servizio cloud
È possibile visualizzare e modificare le proprietà di un servizio cloud per modificare la configurazione.

Nella console passare a **Amministrazione** > **Panoramica** > **Cloud Services Management (Gestione dei servizi cloud)** > **Azure** > **Servizi di Azure** e quindi scegliere **Configure Azure Services (Configura servizi di Azure)**, selezionare un servizio cloud e quindi scegliere **Proprietà**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversione da BIOS a UEFI durante un aggiornamento sul posto
Windows 10 Creators Update introduce un semplice strumento di conversione che automatizza il processo di ripartizione del disco rigido per l'hardware abilitato per UEFI e integra lo strumento di conversione nel processo di aggiornamento sul posto da Windows 7 a Windows 10. Quando si usa questo strumento in combinazione con la sequenza di attività di aggiornamento del sistema operativo e con lo strumento OEM che converte il firmware da BIOS a UEFI, è possibile convertire i computer da BIOS a UEFI durante un aggiornamento sul posto a Windows 10 Creators Update. Per informazioni dettagliate, vedere [Passaggi della sequenza di attività per la gestione della conversione da BIOS a UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Gruppi di sequenze di attività comprimibili
Questa versione introduce la possibilità di espandere e comprimere i gruppi di sequenze di attività. È possibile espandere o comprimere singoli gruppi oppure espandere o comprimere tutti i gruppi in una sola volta.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Impostazioni client per configurare Windows Analytics per Upgrade Readiness
A partire da questa versione, è possibile usare le impostazioni client dei dispositivi per semplificare la configurazione della telemetria di Windows necessaria per usare soluzioni [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) come [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) con Configuration Manager. Configuration Manager è in grado di recuperare da Windows Analytics dati che possono fornire informazioni utili sullo stato corrente dell'ambiente in base ai dati di telemetria di Windows riportati dai computer client. I dati di telemetria di Windows vengono inoltrati dal computer client al servizio di telemetria di Windows. I dati rilevanti vengono quindi trasferiti alle soluzioni Windows Analytics ospitate in una delle aree di lavoro OMS dell'organizzazione. Upgrade Readiness è una soluzione Windows Analytics che consente di definire le priorità per prendere decisioni oculate in merito agli aggiornamenti di Windows per i dispositivi gestiti.

Per informazioni sulle impostazioni di telemetria di Windows, vedere [Configurare la telemetria di Windows nell'organizzazione](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Prerequisiti
- È necessario aver configurato il sito per l'uso del servizio cloud Upgrade Readiness. Per altre informazioni, vedere [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>Configurare le impostazioni client di Windows Analytics
Per configurare Windows Analytics, nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client**, fare doppio clic su **Create Custom Device Client Settings** (Crea impostazioni client del dispositivo personalizzate), quindi selezionare **Windows Analytics**.  

Dopo l'accesso alla scheda delle impostazioni di **Windows Analytics**, configurare quanto segue:
- **ID commerciale**  
L'ID commerciale consente di associare le informazioni dai dispositivi gestiti all'area di lavoro OMS che ospita i dati Windows Analytics dell'organizzazione. Se è già stata configurata una chiave ID commerciale per l'uso con Upgrade Readiness, usare tale ID. Se non è ancora disponibile una chiave ID commerciale, vedere [Generate your commercial ID key]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key) (Generare l'ID commerciale).

- Impostare un **livello di telemetria per i dispositivi Windows 10**   
Per informazioni sulle informazioni raccolte da ogni livello di telemetria di Windows 10, vedere [Configure Windows telemetry in your organization]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels) (Configurare i livelli di telemetria dell'organizzazione).

- **Acconsentire esplicitamente alla raccolta di dati commerciali nei dispositivi Windows 7, 8 e 8.1**   
Per informazioni sui dati raccolti da questi sistemi operativi dopo il consenso esplicito, scaricare il file PDF sui [campi e gli eventi di telemetria per la valutazione di Windows 7, Windows 8 e Windows 8.1](https://go.microsoft.com/fwlink/?LinkID=822965) da Microsoft.

- **Configurare la raccolta dati di Internet Explorer** Nei dispositivi che eseguono Windows 8.1 o versioni precedenti, la raccolta dati di Internet Explorer consente ad Upgrade Readiness di rilevare incompatibilità di app Web che potrebbero impedire un aggiornamento semplice e rapido a Windows 10. La raccolta dati di Internet Explorer può essere abilitata per ogni area Internet. Per altre informazioni sulle aree Internet, vedere [About URL Security Zones](https://msdn.microsoft.com/en-us/library/ms537183(v=vs.85).aspx) (Informazioni sulle aree di sicurezza degli URL).