---
title: Estensioni SCAP
titleSuffix: Configuration Manager
description: Informazioni sulle estensioni SCAP (Security Content Automation Protocol) per Configuration Manager.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e42027663f06bff715cb7e9087ececbc421cc495
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482453"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Informazioni sulle estensioni SCAP (Security Content Automation Protocol)

*Si applica a: System Center Configuration Manager (Current Branch)*

Le estensioni SCAP per Configuration Manager consentono di analizzare e valutare la conformità dell'ambiente di rete in uso con il protocollo SCAP (Security Content Automation Protocol). SCAP è definito e gestito dal National Institute of Standards and Technology (NIST). Per altre informazioni, vedere la [panoramica del progetto SCAP](https://csrc.nist.gov/projects/security-content-automation-protocol).

> [!Note]  
> Questa versione dello strumento è una versione non definitiva disponibile solo nella versione 1806. Questa versione non è certificata da NIST. <!--SCCMDocs-pr issue 3323-->
> 
> Se è richiesto uno strumento certificato o si usa un'altra versione di Configuration Manager Current Branch, usare la versione seguente delle estensioni SCAP:
> - [Scaricare le estensioni SCAP per System Center Configuration Manager](https://www.microsoft.com/download/details.aspx?id=48741)
> - [Documentazione per la versione 3.0 delle estensioni SCAP](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

Le estensioni SCAP per Configuration Manager usano la funzionalità Impostazioni di conformità per eseguire una prima analisi dei computer nell'ambiente in uso. Documentano quindi il livello di conformità con quanto previsto dall'iniziativa United States Government Configuration Baseline (USGCB).

Le estensioni consentono a Configuration Manager di utilizzare i flussi di dati del protocollo SCAP, valutare la conformità dei sistemi e generare i risultati dei report in formato SCAP. L'organizzazione può usare l'infrastruttura di Configuration Manager esistente per garantire che i computer gestiti soddisfino questo requisito di conformità federale. È anche possibile usare Configuration Manager per generare i report USGCB richiesti dal NIST e dall'Office of Management and Budget (OMB).

Questo articolo fornisce informazioni su come installare, configurare ed eseguire le estensioni SCAP nell'infrastruttura di Configuration Manager.



## <a name="whats-new"></a>Novità

Questa versione delle estensioni SCEP per Configuration Manager include e supporta le funzionalità seguenti:  

- Estensione console di Configuration Manager che supporta la conversione di contenuto SCAP in linee di base di impostazioni di conformità.  

- SCAP versione 1.2, che include i componenti seguenti:  

  - Extensible Configuration Checklist Description Format (XCCDF), versione 1.2
  - Open Vulnerability and Assessment Language (OVAL), fino alla versione 5.10
  - Generazione di report Asset Reporting Format (ARF) 1.1
  - Common Platform Enumeration (CPE) 2.3
  - Common Vulnerabilities and Exposures (CVE)
  - Common Configuration Enumeration (CCE), versione 5
  - USGCB Internet Explorer 8, USGCB Windows 7 e USGCB Windows 7 Firewall  

- Compatibilità con le versioni precedenti di SCAP (versioni 1.1 e 1.0)  

- Procedura guidata della console per importare contenuto SCAP 1.2/1.1/1.0 e OVAL per la conversione in linee di base di configurazione.  

  - Consente la selezione di flussi di dati di origine SCAP e di profili e benchmark XCCDF per la conversione.

- Procedura guidata della console per esportare i risultati della valutazione della configurazione in report XML in formato SCAP.  

  - Consente di visualizzare il file di origine, il flusso dei dati SCAP, il benchmark XCCDF e il profilo XCCDF usati per generare la linea di base.
  - Generazione del report Cyberscope Lightweight Asset Summary Results (LASR).  

- Generazione di report SCAP basati sulla distribuzione della linea di base di configurazione. Questo componente include un nuovo dashboard per la visualizzazione della conformità dei client, nonché della conformità alla regola XCCDF. Il dashboard supporta il drill-through per report più dettagliati in cui è possibile eseguire ricerche e applicare filtri.  

- Prestazioni migliorate di vari tipi di elementi di configurazione convertiti da test OVAL, consentendo una valutazione più rapida.  

- Corregge diversi problemi rilevati in contenuto DISA v1r3 in Windows 10.  



## <a name="terms"></a>Termini

- **ID OVAL**: identificatore di una definizione OVAL specifica conforme al formato per gli ID OVAL.  

- **Flusso dei dati dei risultati SCAP:** aggregazione di componenti SCAP, insieme ai mapping dei riferimenti tra i componenti SCAP, che contiene il contenuto di output (risultati).  

- **Flusso dei dati di origine SCAP**: aggregazione di componenti SCAP, insieme ai mapping dei riferimenti tra i componenti SCAP, che contiene il contenuto di input (origine).



## <a name="deployment-process"></a>Processo di distribuzione

Di seguito è riportato un riepilogo del processo di distribuzione complessivo:  

- [Preparare l'infrastruttura](#bkmk_prepare) per l'uso delle estensioni  

- [Installare e configurare le estensioni SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) per Configuration Manager  

- [Scaricare e installare i file di flusso dei dati SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) da NIST  

- Convertire e importare i file dei flussi di dati SCAP in una linea di base di impostazioni di conformità di Configuration Manager. Usare uno dei due metodi seguenti:   

    - [Processo manuale](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) tramite l'importazione guidata nella console di Configuration Manager  

    - [Processo automatizzato](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) tramite lo strumento da riga di comando Microsoft.Sces.ScapToDcm.exe  

- [Distribuire](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) le linee di base di configurazione alle raccolte  

- [Monitorare](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) i dati di conformità  

- Esportare i risultati di conformità in formato SCAP usando uno dei due metodi seguenti:  

    - [Processo manuale](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) tramite l'esportazione guidata nella console  

    - [Processo automatizzato](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) tramite lo strumento da riga di comando Microsoft.Sces.DcmToScap.exe  



## <a name="bkmk_prepare"></a> Preparare l'infrastruttura

### <a name="software-requirements"></a>Requisiti software

Per installare, configurare ed eseguire le estensioni SCAP per Configuration Manager, è necessario un computer con il software seguente:

- [Versione supportata](/sccm/core/servers/manage/current-branch-versions-supported) della console di Configuration Manager Current Branch.  

- Versione del sistema operativo compatibile con la console di Configuration Manager. Per altre informazioni, vedere [Sistemi operativi supportati per le console di Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

Oltre al computer che esegue le estensioni SCAP, sono anche necessari gli elementi seguenti:

- Un'infrastruttura Configuration Manager Current Branch. Per altre informazioni sui requisiti per una distribuzione di Configuration Manager, vedere l'articolo [Configurazioni supportate per System Center Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).  

I computer per i quali si desidera valutare la conformità SCAP devono disporre delle seguenti configurazioni e del seguente software:

- Client di Configuration Manager.  

- Windows PowerShell 2.0 o versione successiva.  

- Criteri di esecuzione di PowerShell di Configuration Manager impostati su **Ignora**. Per altre informazioni, vedere l'articolo [Criteri di esecuzione di PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Uno dei seguenti sistemi operativi:  
  - Windows 7 SP1, a 32 bit o a 64 bit
  - Windows 10 a 32 bit o a 64 bit
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>Requisiti hardware

Per altre informazioni sui requisiti di sistema minimi per Configuration Manager, vedere [Pianificazione delle configurazioni hardware per Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## <a name="accessibility-features"></a>Funzionalità di accesso facilitato

Le estensioni SCAP per Configuration Manager includono gli strumenti da riga di comando di Windows. Questi strumenti consentono di usufruire delle funzionalità e degli strumenti di accessibilità in Windows.

- I parametri della riga di comando per gli strumenti Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe sono documentati. Per altre informazioni, vedere [Parametri della riga di comando dello strumento Microsoft.Sces.ScapToDcm.exe](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) e [Parametri della riga di comando dello strumento Microsoft.Sces.DcmToScap.exe](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- I parametri della riga di comando `-help` e `-?` per ogni strumento visualizzano le informazioni per l'utilizzo sullo schermo. I dettagli per l'utilizzo sono quindi disponibili per le utilità per la lettura dello schermo e altri strumenti di Assistive Technology.  

- Per altre informazioni, vedere [Accessibilità di Windows](http://windows.microsoft.com/windows/help/accessibility).

Le estensioni SCAP usano anche le funzionalità di accessibilità disponibili in Configuration Manager. Per altre informazioni, vedere [Funzionalità di accessibilità in Configuration Manager](/sccm/core/understand/accessibility-features).

Per informazioni generali sui prodotti e i servizi di accessibilità Microsoft, visitare il [sito Web Accessibilità in Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).



## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Installare e configurare le estensioni SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
