---
title: 'Monitorare i client: usare Windows Analytics con Configuration Manager | Microsoft Docs'
description: "Windows Analytics è un set di soluzioni eseguite in Operations Management Suite, che consentono di ottenere indicazioni preziose sullo stato corrente dell'ambiente sfruttando i dati di telemetria di Windows segnalati dai dispositivi nell'ambiente."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.contentlocale: it-it
ms.lasthandoff: 07/29/2017

---

# <a name="use-windows-analytics-with-configuration-manager"></a>Usare Windows Analytics con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) è un set di soluzioni eseguite in [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). Le soluzioni consentono di ottenere indicazioni sullo stato corrente dell'ambiente. I dispositivi dell'ambiente segnalano i dati di telemetria di Windows. È possibile accedere a questi dati e analizzarli tramite le soluzioni del [portale Web di Operations Management Suite](https://mms.microsoft.com). Nel caso di [Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade/upgrade-analytics) i dati possono anche essere resi direttamente disponibili nel nodo di monitoraggio della console di Configuration Manager connettendo Preparazione aggiornamenti a Configuration Manager.

I dati di telemetria di Windows usati da Windows Analytics non vengono trasferiti direttamente al server del sito di Configuration Manager. I computer client inviano i dati di telemetria di Windows al servizio di telemetria. I dati pertinenti vengono quindi trasferiti alle soluzioni di Windows Analytics ospitate in una delle aree di lavoro di OMS dell'organizzazione. Configuration Manager può quindi indirizzare ai dati pertinenti nel portale Web con collegamenti contestuali o visualizzare direttamente i dati che fanno parte delle soluzioni connesse a Configuration Manager. È anche possibile eseguire query dirette sui dati dal portale Web di Operation Management Suite.

>[!Important]
>I [dati di utilizzo e di diagnostica di Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), segnalati a Microsoft dal server del sito di Configuration Manager sono completamente distinti dai dati di telemetria di Windows Analytics e di Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurare i client per segnalare i dati a Windows Analytics

I dispositivi client, per poter segnalare i dati a Windows Analytics, devono essere configurati con una chiave ID commerciale associata all'area di lavoro di Operations Management Suite che ospita i dati di Windows Analytics per l'organizzazione. I dispositivi devono anche essere configurati per segnalare i dati di telemetria a un livello di telemetria appropriato per la soluzione o le soluzioni specifiche che si vogliono usare. 

### <a name="configure-windows-analytics-client-settings"></a>Configurare le impostazioni client di Windows Analytics
Per configurare Windows Analytics, nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**, fare doppio clic su **Create Custom Device Client Settings** (Crea impostazioni client del dispositivo personalizzate), quindi selezionare **Windows Analytics**.  

Dopo l'accesso alla scheda delle impostazioni di **Windows Analytics**, configurare quanto segue:
  -  **ID commerciale**  
L'ID commerciale consente di associare le informazioni dai dispositivi gestiti all'area di lavoro OMS che ospita i dati Windows Analytics dell'organizzazione. Se è già stata configurata una chiave ID commerciale per l'uso con Upgrade Readiness, usare tale ID. Se non è ancora disponibile una chiave ID commerciale, vedere [Generate your commercial ID key]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key) (Generare l'ID commerciale).

  -  **Livello di telemetria nei dispositivi Windows 10**   
Per informazioni sulle informazioni raccolte da ogni livello di telemetria di Windows 10, vedere [Configure Windows telemetry in your organization](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels) (Configurare i livelli di telemetria dell'organizzazione).

  -  **Acconsentire esplicitamente alla raccolta dei dati commerciali in dispositivi Windows 7, 8 e 8.1**   
Per informazioni sui dati raccolti da questi sistemi operativi dopo il consenso esplicito, scaricare il file PDF sui [campi e gli eventi di telemetria per la valutazione di Windows 7, Windows 8 e Windows 8.1](https://go.microsoft.com/fwlink/?LinkID=822965) da Microsoft.

  -  **Configurare la raccolta dati di Internet Explorer**  
Nei dispositivi che eseguono Windows 8.1 o versioni precedenti la raccolta dati di Internet Explorer consente a Preparazione aggiornamenti di rilevare incompatibilità di applicazioni Web che potrebbero impedire un aggiornamento semplice e rapido a Windows 10. La raccolta dati di Internet Explorer può essere abilitata per ogni area Internet. Per altre informazioni sulle aree Internet, vedere [About URL Security Zones](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx) (Informazioni sulle aree di sicurezza degli URL).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usare Preparazione aggiornamenti per identificare i problemi di compatibilità con Windows 10

Preparazione aggiornamenti (precedentemente denominato Upgrade Analytics) consente di analizzare la conformità e la compatibilità dei dispositivi con Windows 10. Questa valutazione facilita l'esecuzione degli aggiornamenti. Dopo avere connesso Configuration Manager a Preparazione aggiornamenti, è possibile accedere a questi dati di compatibilità dell'aggiornamento dei client direttamente nella console di Configuration Manager. Sarà quindi possibile impostare i dispositivi di destinazione dell'aggiornamento o della correzione dall'elenco dei dispositivi.

Per altre informazioni e dettagli su come configurare e connettersi a Preparazione aggiornamenti, vedere [Preparazione aggiornamenti](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Usare Windows Analytics per identificare le lacune nei criteri di Windows Information Protection

I dispositivi con Windows 10 versione 1703 e successive configurati con un criterio di [Windows Information Protection](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) segnalano i dati di telemetria nelle applicazioni che accedono ai dati aziendali dell'ambiente, ma che non sono tenute in considerazione nelle regole di applicazione dei criteri WIP. Si tratta di applicazioni che tendenzialmente devono mantenere la produttività per gli utenti dell'ambiente, ma a cui viene bloccato l'accesso, quindi sapere che accedono ai dati aziendali può essere utile nella manutenzione dei criteri di Windows Information Protection in Configuration Manager. 

Questi dati di Windows Information Protection sono accessibili tramite questa [query di Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).
