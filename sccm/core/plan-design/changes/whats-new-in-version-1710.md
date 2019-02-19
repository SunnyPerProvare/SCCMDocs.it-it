---
title: Nuova versione 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Ottenere informazioni dettagliate sulle modifiche e le nuove funzionalità introdotte nella versione 1710 di System Center Configuration Manager.
ms.date: 1/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1609f162460d525a146289e70426783cd126912
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123434"
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>Novità della versione 1710 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'aggiornamento 1710 per System Center Configuration Manager (Current Branch) è disponibile come aggiornamento nella console per siti precedentemente installati che eseguono la versione 1610, 1702 o 1706.

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in System Center Configuration Manager Current Branch, versione 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Sono ora disponibili anche i seguenti aggiornamenti aggiuntivi per questa versione:
- [Aggiornamento cumulativo per System Center Configuration Manager Current Branch, versione 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Aggiornamento cumulativo 2 per System Center Configuration Manager Current Branch, versione 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>  Sono disponibili altre informazioni su:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites) (Installare nuovi siti)  
>   - [Installing updates at sites](/sccm/core/servers/manage/updates) (Installare aggiornamenti nei siti)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions) (Versioni di base e di aggiornamento)  

Le sezioni seguenti offrono informazioni dettagliate sulle modifiche e le nuove funzionalità introdotte nella versione 1710 di Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruttura del sito

### <a name="updates-for-peer-cache-----sms500850---"></a>Aggiornamenti per Peer cache <!-- sms500850 -->
A partire da questa versione, Peer cache non è più una funzionalità in versione non definitiva.  In questa versione non sono state introdotte altre modifiche per Peer cache. Per altre informazioni, vedere [Peer cache per i client di Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Supporto per punti di distribuzione cloud per il cloud di Azure per enti pubblici   <!-- sms491428 -->
È ora possibile usare [punti di distribuzione basati sul cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) nel cloud di Azure per enti pubblici.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revisione dell'unità predefinita di inventario <!-- sms503697 -->
Poiché i moderni dispositivi includono unità disco rigido con dimensioni in gigabyte (GB), terabyte (TB) e scale di dimensioni maggiori, in questa versione l'unità predefinita (SMS_Units) usata in molte visualizzazioni viene modificata da megabyte (MB) a GB. Ad esempio, il valore v_gs_LogicalDisk.FreeSpace riporta ora GB come GB.


<!-- ## Migration  -->


## <a name="client-management"></a>Gestione dei client

### <a name="co-management-for-windows-10-devices"></a>Co-gestione per dispositivi Windows 10    
<!-- 1350871 --> Negli aggiornamenti precedenti di Windows 10 è già possibile aggiungere un dispositivo Windows 10 ad Active Directory (AD) locale e ad Azure AD basata sul cloud allo stesso tempo (Azure AD ibrida). A partire da Configuration Manager versione 1710, la co-gestione sfrutta questo miglioramento e consente di gestire contemporaneamente i dispositivi Windows 10 versione 1709 (noto anche come Fall Creators Update) usando sia Configuration Manager sia Intune. È una soluzione che costituisce un ponte tra la gestione tradizionale e quella moderna e che consente di eseguire la transizione mediante un approccio per fasi. Per i dettagli, vedere [Co-gestione per dispositivi Windows 10](/sccm/comanage/overview).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Riavviare i computer dalla console di Configuration Manager <!-- 1356283 -->
A partire da questa versione, è possibile usare la console di Configuration Manager per identificare i dispositivi client che richiedono il riavvio e quindi usare un'azione di notifica client per riavviarli.

Vedere [Come gestire i client in System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Gestione delle applicazioni
### <a name="improvements-for-run-scripts------1236459---"></a>Miglioramenti per la funzionalità Esegui script   <!-- 1236459 -->
Questa versione introduce diversi miglioramenti per la funzionalità **Esegui script**, che consente di distribuire script di PowerShell da eseguire nei dispositivi gestiti. Questa funzionalità è stata introdotta per la prima volta nella versione 1706.

Sono inclusi i miglioramenti seguenti:
- Uso di ambiti di protezione per semplificare il controllo degli utenti autorizzati a usare Esegui script
- Monitoraggio in tempo reale degli script eseguiti
- Visualizzazione dei parametri per lo script nella procedura guidata di creazione degli script, con supporto per la convalida e identificazione dei parametri come obbligatori o facoltativi.

Per altre informazioni sull'uso della funzionalità Esegui script, vedere [Creare ed eseguire script](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nuove impostazioni dei criteri di gestione delle applicazioni mobili
<!-- 1324760 --> Sono state aggiunte le impostazioni seguenti relative ai criteri di gestione delle applicazioni per dispositivi mobili:
- **Disabilita la sincronizzazione dei contatti**: impedisce all'app di salvare i dati nell'app dei contatti nativa del dispositivo.
- **Disabilita stampa**: impedisce all'app di stampare dati aziendali o dell'istituto di istruzione.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Software Center non deforma più le icone maggiori di 250x250 pixel  
<!-- 1356194 -->

Con questa versione, Software Center non distorce più le icone maggiori di 250x250 pixel. In Software Center tali icone apparivano sfocate. È ora possibile impostare icone con dimensioni massime pari a 512x512 pixel. Tali icone verranno visualizzate senza distorsione.

Per aggiungere un'icona per l'app in Software Center, vedere [Creare applicazioni](/sccm/apps/deploy-use/create-applications).

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo
 > [!TIP]   
 > <!-- 1354281 --> A partire da Windows 10 versione 1709 (denominata anche Fall Creators Update), Windows Media include più edizioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento o di un'immagine del sistema operativo, assicurarsi di selezionare un'[edizione utilizzabile da Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Aggiungere sequenze di attività figlio a una sequenza di attività
<!-- 1261338 -->

È possibile aggiungere un nuovo passaggio della sequenza di attività per l'esecuzione di un'altra sequenza di attività, che crea una relazione padre/figlio tra le sequenze di attività. In questo modo è possibile creare più sequenze di attività modulari riusabili.  

Per altre informazioni sulla sequenza di attività figlio, vedere [Sequenza di attività figlio](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## <a name="software-center-customization"></a>Personalizzazione di Software Center
<!-- 1351224 --> È possibile aggiungere elementi di branding aziendale e specificare la visibilità delle schede in Software Center. È possibile aggiungere il nome specifico della società per Software Center, impostare un tema di colori per la configurazione di Software Center, impostare il logo della società e impostare le schede visibili per i dispositivi client.

Per altre informazioni, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## <a name="software-updates"></a>Aggiornamenti software

### <a name="surface-driver-updates-----1098490---"></a>Aggiornamenti dei driver di Surface <!-- 1098490 -->
A partire da questa versione, la gestione degli aggiornamenti dei driver di Surface non è più una funzionalità in versione non definitiva.  


## <a name="reporting"></a>Reporting

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limitare la telemetria avanzata di Windows 10 al solo invio dei dati pertinenti a Integrità del dispositivo di Windows Analytics
<!-- 1356148 -->

È ora possibile impostare il livello di raccolta dei dati di telemetria di Windows 10 su **Enhanced (Limited)** (Avanzato - Limitato). Questa impostazione consente di ottenere informazioni utili sui dispositivi presenti nell'ambiente in uso senza che i dispositivi segnalino tutti i dati nel livello di telemetria **Avanzato** con Windows 10 1709 o versione successiva.

Per altre informazioni, vedere [Come configurare le impostazioni client in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gestione di dispositivi mobili

### <a name="actions-for-non-compliance"></a>Azioni per la mancata conformità 
<!--1321366 -->    
Ora è possibile configurare una sequenza in ordine temporale delle azioni applicate ai dispositivi che non soddisfano la conformità. Ad esempio, è possibile segnalare agli utenti i dispositivi non conformi inviando notifiche via posta elettronica o contrassegnando tali dispositivi come non conformi. Per informazioni dettagliate, vedere [Configurare azioni per la mancata conformità](/sccm/mdm/deploy-use/actions-for-noncompliance).

### <a name="windows-10-arm64-device-support"></a>Supporto per dispositivi ARM64 Windows 10
<!-- 1355000 -->

Nei dispositivi ARM64 che eseguono Windows 10 sarà supportata la gestione ibrida dei dispositivi mobili quando questi dispositivi saranno disponibili.

Gli scenari supportati includono le operazioni seguenti:

- [Registrare i dispositivi](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Eseguire azioni di cancellazione remota complete e selettive](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Gestire le impostazioni tramite linee di base ed elementi di configurazione](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Gestire i criteri di conformità](../../../mdm/deploy-use/device-compliance-policies.md) e [l'accesso condizionale](../../../protect/deploy-use/manage-access-to-services.md)
- Gestire l'accesso alle risorse aziendali tramite:
   - [Profili certificato](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [Profili VPN in Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Profili Wi-Fi](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Profili di posta elettronica](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configurare Windows Hello per criteri aziendali](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Gestire le applicazioni](../../../mdm/deploy-use/management-tasks-applications.md)

> [!NOTE]
> La distribuzione delle applicazioni .appxbundle compilate per architetture multiple potrebbe non funzionare in questi dispositivi, e questo scenario non è supportato al momento.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Esperienza del profilo VPN migliorata nella console di Configuration Manager 
<!-- 1318232 -->

In questa versione sono state aggiornate la procedura guidata di creazione del profilo VPN e le pagine delle proprietà per visualizzare le impostazioni appropriate per la piattaforma selezionata:


- Ogni piattaforma ha un proprio flusso di lavoro, vale a dire che i nuovi profili VPN contengono solo l'impostazione supportata dalla piattaforma.
- La pagina **Piattaforme supportate** viene ora visualizzata dopo la pagina **Generale**.  È ora possibile scegliere la piattaforma prima di impostare i valori delle proprietà.
- Quando la piattaforma è impostata su **Android**, **Android for Work** o **Windows Phone 8.1**, la pagina **Piattaforme supportate** non è necessaria e non viene visualizzata.
- Il flusso di lavoro basato su client di Configuration Manager è stato combinato con i flussi di lavoro di Windows 10 basato su client dei dispositivi mobili ibridi (MDM), visto che supportano le stesse impostazioni.
- Ogni flusso di lavoro di piattaforma include solo le impostazioni appropriate per il flusso di lavoro.  Ad esempio, il flusso di lavoro Android contiene le impostazioni appropriate per Android; le impostazioni appropriate per iOS e Windows 10 Mobile non vengono più visualizzate nel flusso di lavoro Android.
- La pagina VPN automatico è obsoleta ed è stata rimossa.

Queste modifiche vengono applicate ai nuovi profili VPN.  

Per ridurre al minimo i rischi relativi alla compatibilità, i profili VPN esistenti non vengono modificati.  Quando viene modificato un profilo esistente, le impostazioni vengono visualizzate come quando è stato creato il profilo.  

Per altre informazioni, vedere [Profili VPN nei dispositivi mobili in System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Supporto limitato per certificati CNG (Cryptography: Next Generation) <!-- 1356191 -->

Configuration Manager offre un supporto limitato per CNG (Cryptography: Next Generation). I client di Configuration Manager possono usare certificati di autenticazione client con chiave privata nel provider di archiviazione chiavi (KSP) CNG. Con il supporto per i provider di archiviazione chiavi, i client di Configuration Manager supportano chiavi private basate sull'hardware, ad esempio TPM KSP per i certificati di autenticazione client PKI.

Per altre informazioni, vedere [Panoramica dei certificati CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Proteggere i dispositivi

### <a name="create-and-deploy-exploit-guard-policies"></a>Creare e distribuire criteri di Exploit Guard
<!-- 1355468 -->

È possibile [creare e distribuire criteri](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) per la gestione di tutti e quattro i componenti di Windows Defender Exploit Guard, tra cui riduzione della superficie di attacco, accesso controllato alle cartelle, protezione dagli exploit e protezione di rete.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creare e distribuire criteri di Windows Defender Application Guard
<!-- 1351960 -->

È possibile [creare e distribuire criteri di Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy) usando Endpoint Protection di Configuration Manager.

### <a name="device-guard-policy-changes"></a>Modifiche apportate ai criteri di Device Guard
<!-- 1355092 --> Sono state apportate le tre modifiche seguenti in relazione ai criteri di Device Guard:

- I criteri di Device Guard sono stati rinominati in criteri di controllo delle applicazioni di Windows Defender. Ad esempio la **procedura guidata Crea criterio di Device Guard** è ora denominata **Create Windows Defender Application Control policy wizard** (Creazione di criteri di controllo delle applicazioni di Windows Defender).
- I dispositivi che usano la versione Fall Creators Update per Windows 1709 non devono essere riavviati per applicare i criteri di controllo delle applicazioni di Windows Defender. Anche se il riavvio è sempre il comportamento predefinito, è possibile [disattivare i riavvii](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- È possibile [impostare i dispositivi per l'esecuzione automatica di software](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) ritenuto attendibile da Intelligent Security Graph.





## <a name="next-steps"></a>Passaggi successivi
Quando si è pronti per installare questa versione, vedere [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates).
