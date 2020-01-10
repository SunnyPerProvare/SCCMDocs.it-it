---
title: Caratteristiche e funzionalità
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità di gestione principali di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c50efb804787bb8288e6b1f200cee005ed2d0370
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75802838"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Caratteristiche e funzionalità di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo include un riepilogo delle principali funzionalità di gestione di Configuration Manager. Poiché ogni funzionalità ha prerequisiti diversi, la modalità d'uso di ciascuna potrebbe influire sulla struttura e l'implementazione della gerarchia di Configuration Manager. Se, ad esempio, si vogliono distribuire gli aggiornamenti del software nei dispositivi della gerarchia, è necessario installare il ruolo del sistema del sito del punto di aggiornamento software.  

Per altre informazioni su come pianificare e installare Configuration Manager per supportare queste funzionalità di gestione nel proprio ambiente, vedere [Preparativi per Configuration Manager](/sccm/core/plan-design/get-ready).  

## <a name="co-management"></a>Co-gestione

La co-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente al cloud di Microsoft 365. Consente di gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune. La co-gestione consente di collegare al cloud gli investimenti esistenti in Configuration Manager tramite l'aggiunta di nuove funzionalità, come l'accesso condizionale. Per altre informazioni, vedere [Informazioni sulla co-gestione](/sccm/comanage/overview).

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio offre dati analitici e intelligenza per consentire agli utenti di prendere decisioni più informate sull'idoneità degli aggiornamenti dei client Windows. Combina i dati dell'organizzazione con i dati aggregati di milioni di dispositivi connessi a servizi cloud Microsoft. Per altre informazioni, vedere [Che cos'è Desktop Analytics?](/configmgr/desktop-analytics/overview)

## <a name="cloud-attached-management"></a>Gestione collegata al cloud

Usare funzionalità come Cloud Management Gateway, i punti di distribuzione basati sul cloud e Azure Active Directory per gestire i client basati su Internet.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire i client su Internet](/sccm/core/clients/manage/manage-clients-internet)
- [Pianificare per Azure AD](/sccm/core/plan-design/security/plan-for-security#bkmk_planazuread)
- [Servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)

## <a name="real-time-management"></a>Gestione in tempo reale

Con CMPivot è possibile eseguire immediatamente query sui dispositivi online e quindi filtrare e raggruppare i dati per informazioni dettagliate più approfondite. È inoltre possibile usare la console di Configuration Manager per gestire e distribuire script di Windows PowerShell nei client. Per altre informazioni, vedere [CMPivot](/sccm/core/servers/manage/cmpivot) e [Creare ed eseguire script di PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

## <a name="application-management"></a>Gestione delle applicazioni

È disponibile un set di strumenti e risorse che consentono di creare, gestire, distribuire e monitorare le applicazioni in una vasta gamma di dispositivi gestiti. Dalla console di Configuration Manager è anche possibile distribuire, aggiornare e gestire Office 365. Configuration Manager si integra con il Microsoft Store per le aziende e la formazione per distribuire app basate sul cloud. Per altre informazioni, vedere [Introduzione alla gestione delle applicazioni](/sccm/apps/understand/introduction-to-application-management).

## <a name="os-deployment"></a>Distribuzione del sistema operativo

È possibile distribuire un aggiornamento sul posto di Windows 10 oppure acquisire e distribuire immagini del sistema operativo. Per la distribuzione di immagini è possibile usare supporti di avvio, PXE o multicast. Per la ridistribuzione di dispositivi esistenti può inoltre essere utile Windows AutoPilot. Per altre informazioni, vedere [Introduzione alla distribuzione del sistema operativo](/sccm/osd/understand/introduction-to-operating-system-deployment).  

## <a name="software-updates"></a>Aggiornamenti software

È possibile gestire, distribuire e monitorare gli aggiornamenti software nell'organizzazione. Questa funzionalità di aggiornamento del software può essere integrata con Ottimizzazione recapito di Windows e altre tecnologie di peer caching per facilitare il controllo dell'utilizzo della rete. Per altre informazioni, vedere [Introduzione agli aggiornamenti software](/sccm/sum/understand/software-updates-introduction).  

## <a name="company-resource-access"></a>Accesso alle risorse aziendali

Gli utenti dell'organizzazione hanno la possibilità di accedere a dati e applicazioni da postazioni remote. Include Wi-Fi, VPN, posta elettronica e profili di certificato. Per altre informazioni, vedere [Proteggere dati e infrastruttura e del sito](/sccm/protect/understand/protect-data-and-site-infrastructure).

## <a name="compliance-settings"></a>Impostazioni di conformità

È possibile valutare, rilevare e correggere la conformità della configurazione dei dispositivi client nell'organizzazione. Inoltre, è possibile usare le impostazioni di conformità per configurare una gamma di funzionalità e impostazioni di sicurezza nei dispositivi gestiti. Per altre informazioni, vedere [Garantire la conformità dei dispositivi](/sccm/compliance/understand/ensure-device-compliance).  

## <a name="endpoint-protection"></a>Endpoint Protection

Sono disponibili funzionalità di sicurezza, antimalware e gestione di Windows Firewall per i computer dell'organizzazione. Questa area consente la gestione e l'integrazione con le funzionalità seguenti di Windows Defender:

- Windows Defender Antivirus
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Controllo delle applicazioni di Windows Defender
- Windows Defender Firewall

Per altre informazioni, vedere [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  

## <a name="inventory"></a>Argomento

Consente di identificare e monitorare gli asset.

### <a name="hardware-inventory"></a>Inventario hardware

Raccoglie informazioni dettagliate sull'hardware dei dispositivi nell'organizzazione. Per altre informazioni, vedere [Introduzione all'inventario hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

### <a name="software-inventory"></a>Inventario software

Raccoglie e segnala le informazioni sui file archiviati sui computer client dell'organizzazione. Per altre informazioni, vedere [Introduzione all'inventario software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

### <a name="asset-intelligence"></a>Asset Intelligence

Sono disponibili strumenti per raccogliere i dati di inventario e monitorare l'utilizzo delle licenze software nell'organizzazione. Per altre informazioni, vedere [Introduzione ad Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence).  

## <a name="on-premises-mobile-device-management"></a>Gestione di dispositivi mobili locale

È possibile registrare e gestire i dispositivi usando l'infrastruttura locale di Configuration Manager con la funzionalità di gestione integrata nelle piattaforme dei dispositivi. La modalità di gestione tipica prevede l'uso di un client di Configuration Manager installato separatamente. Questa funzionalità supporta attualmente la gestione dei dispositivi Windows 10 Enterprise e Windows 10 Mobile. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

## <a name="power-management"></a>Risparmio energia

Sono disponibili funzionalità per gestire e monitorare il consumo di energia dei computer client nell'organizzazione. È possibile configurare combinazioni per il risparmio di energia e usare la tecnologia di riattivazione LAN per eseguire gli interventi di manutenzione al di fuori dell'orario di lavoro. Per altre informazioni, vedere [Introduzione alle raccolte](/sccm/core/clients/manage/power/introduction-to-power-management).  

## <a name="remote-control"></a>Controllo remoto

Offre strumenti per amministrare in remoto i computer client dalla console di Configuration Manager. Per altre informazioni, vedere [Introduzione al controllo remoto](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).  

## <a name="reporting"></a>Reporting

È possibile usare le funzionalità avanzate per la creazione di report di SQL Server Reporting Services dalla console di Configuration Manager. Sono disponibili centinaia di report predefiniti. Per altre informazioni, vedere [Introduzione ai report](/sccm/core/servers/manage/introduction-to-reporting).  

## <a name="software-metering"></a>Controllo del software

Sono disponibili strumenti per monitorare e raccogliere i dati di utilizzo del software dai client di Configuration Manager. È possibile usare questi dati per determinare se il software viene usato dopo l'installazione. Per altre informazioni, vedere [Monitorare l'utilizzo delle app con la misurazione del software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering).  
