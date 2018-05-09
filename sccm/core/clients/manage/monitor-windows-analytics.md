---
title: Monitorare i client con Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics è un set di soluzioni eseguite in Operations Management Suite, che consentono di ottenere indicazioni preziose sullo stato corrente dell'ambiente sfruttando i dati di telemetria di Windows segnalati dai dispositivi nell'ambiente.
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e792f421520798a0e000384aafcb99f31dc8eb14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Usare Windows Analytics con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) è un set di soluzioni eseguite in [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS). Queste soluzioni consentono di ottenere indicazioni sullo stato corrente dell'ambiente. I dispositivi presenti nell'ambiente forniscono dati di telemetria di Windows a cui è possibile accedere e che possono essere analizzati tramite le soluzioni del [portale Web di Operations Management Suite](https://mms.microsoft.com). Se si collega [Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade/upgrade-analytics) a Configuration Manager, è possibile accedere direttamente ai dati nel nodo **Monitoraggio** della console di Configuration Manager.

I dati di telemetria di Windows usati da Windows Analytics non vengono trasferiti direttamente al server del sito di Configuration Manager. I computer client inviano i dati di telemetria di Windows al servizio di telemetria relativo. Tale servizio trasferisce quindi i dati pertinenti alle soluzioni di Windows Analytics ospitate in una delle aree di lavoro di OMS dell'organizzazione. Configuration Manager può quindi indirizzare gli utenti ai dati pertinenti nel portale Web con collegamenti contestuali o visualizzare direttamente i dati che fanno parte delle soluzioni connesse a Configuration Manager. È anche possibile eseguire query dirette sui dati dal portale Web di Operation Management Suite.

>[!Important]
>I [dati di diagnostica e di utilizzo di Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), segnalati a Microsoft dal server del sito di Configuration Manager, sono distinti dai dati di telemetria di Windows Analytics e di Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurare i client per segnalare i dati a Windows Analytics

Per poter segnalare i dati a Windows Analytics, i dispositivi client devono essere configurati con una chiave ID commerciale associata all'area di lavoro di OMS che ospita i dati di Windows Analytics. I dispositivi devono anche essere configurati per segnalare i dati di telemetria a un livello di telemetria appropriato per le soluzioni specifiche che si vogliono usare. 

### <a name="configure-windows-analytics-client-settings"></a>Configurare le impostazioni client di Windows Analytics
Per configurare Windows Analytics, nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**, fare doppio clic su **Create Custom Device Client Settings** (Crea impostazioni client del dispositivo personalizzate), quindi selezionare **Windows Analytics**.  

Dopo l'accesso alla scheda delle impostazioni di **Windows Analytics**, configurare le impostazioni seguenti:
  -  **Chiave ID commerciale**  
L'ID commerciale consente di associare le informazioni dai dispositivi gestiti all'area di lavoro OMS che ospita i dati Windows Analytics dell'organizzazione. Se è già stata configurata una chiave ID commerciale per l'uso con Upgrade Readiness, usare tale ID. Se non è ancora disponibile una chiave ID commerciale, vedere [Generate your commercial ID key]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key) (Generare l'ID commerciale).

  -  **Livello di telemetria nei dispositivi Windows 10**   
Per informazioni sui livelli di telemetria di Windows 10, vedere [Configurare la telemetria di Windows nell'organizzazione](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > Con l'aggiornamento 1710 è possibile impostare il livello di raccolta dei dati di telemetria di Windows 10 su **Enhanced (Limited)** (Avanzato - Limitato). Questa impostazione consente di ottenere informazioni utili sui dispositivi presenti nell'ambiente in uso senza che i dispositivi segnalino tutti i dati nel livello di telemetria **Avanzato** con Windows 10 1709 o versione successiva. Il livello di telemetria Avanzata (con limitazioni) include metriche del livello di base e un subset di dati raccolti dal livello Avanzato pertinenti per Windows Analytics.


  -  **Acconsentire esplicitamente alla raccolta dei dati commerciali in dispositivi Windows 7, 8 e 8.1**   
Per altre informazioni, vedere [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Eventi e campi di valutazione telemetrica per Windows 7, Windows 8 e Windows 8.1).

  -  **Configurare la raccolta dati di Internet Explorer**  
Nei dispositivi che eseguono Windows 8.1 o versioni precedenti la raccolta dati di Internet Explorer consente a Preparazione aggiornamenti di rilevare incompatibilità di applicazioni Web che potrebbero impedire un aggiornamento semplice e rapido a Windows 10. La raccolta dati di Internet Explorer può essere abilitata per ogni area Internet. Per altre informazioni sulle aree Internet, vedere [About URL Security Zones](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx) (Informazioni sulle aree di sicurezza degli URL).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usare Preparazione aggiornamenti per identificare i problemi di compatibilità con Windows 10

Preparazione aggiornamenti (precedentemente denominato Upgrade Analytics) consente di analizzare la conformità e la compatibilità dei dispositivi con Windows 10. Questa valutazione facilita l'esecuzione degli aggiornamenti. Dopo avere connesso Configuration Manager a Preparazione aggiornamenti, accedere ai dati di compatibilità dell'aggiornamento dei client direttamente nella console di Configuration Manager. Quindi specificare i dispositivi da aggiornare o correggere dall'elenco relativo.

Per altre informazioni e dettagli su come configurare e connettersi a Preparazione aggiornamenti, vedere [Preparazione aggiornamenti](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Usare Windows Analytics per identificare le lacune nei criteri di Windows Information Protection

I dispositivi con Windows 10 versione 1703 e successive configurati con criteri di [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) segnalano i dati di telemetria nelle applicazioni che accedono ai dati aziendali dell'ambiente, ma che non sono incluse nelle regole di applicazione dei criteri di Windows Information Protection. Tali applicazioni possono essere necessarie agli utenti al fine di mantenere una produttività elevata ma Windows Information Protection ne blocca l'accesso. Le informazioni sull'accesso ai dati aziendali da parte degli utenti sono utili nella gestione dei criteri di Windows Information Protection in Configuration Manager. 

Accedere ai dati di Windows Information Protection mediante la [query di Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952) seguente.