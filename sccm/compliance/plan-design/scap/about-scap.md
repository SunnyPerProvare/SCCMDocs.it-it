---
title: Informazioni sulle estensioni SCAP (Security Content Automation Protocol)
titleSuffix: Configuraton Manager
description: Informazioni sulle estensioni SCAP (Security Content Automation Protocol)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 18463e4f87c60135bdc29d0f7ce4cb2f80a0eea7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336188"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Informazioni sulle estensioni SCAP (Security Content Automation Protocol)

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella Technical Preview versione 1803 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features). Questa versione non definitiva delle estensioni SCAP può essere installata in qualsiasi versione attualmente supportata di Configuration Manager Current Branch e LTSB 1606. A partire dalla Technical Preview 1803, il file di installazione si trova in cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

Le estensioni SCAP per Microsoft System Center Configuration Manager consentono di analizzare e valutare la conformità dell'ambiente di rete in uso con il protocollo SCAP (Security Content Automation Protocol). SCAP è definito e gestito dal National Institute of Standards and Technology (NIST) degli Stati Uniti d'America.

Le estensioni SCAP per Microsoft System Center Configuration Manager usano la funzionalità Impostazioni di conformità in Microsoft System Center Configuration Manager per analizzare i computer nell'ambiente in uso e quindi documentarne il livello di conformità con l'autorizzazione USGCB (United States Government Configuration Baseline).

Le estensioni consentono a Configuration Manager di utilizzare i flussi di dati del protocollo SCAP, valutare la compatibilità dei sistemi e generare i risultati dei report in formato SCAP. L'organizzazione può usare l'infrastruttura di Configuration Manager esistente per assicurare che i computer gestiti soddisfino il requisito di conformità federale e per generare i report USGCB obbligatori per il National Institute of Standards and Technology (NIST) e l'Office of Management and Budget (OMB) degli Stati Uniti d'America.

Questo manuale fornisce informazioni in grado di agevolare l'installazione, la configurazione e l'esecuzione delle estensioni SCAP nell'infrastruttura di System Center Configuration Manager.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Novità della versione non definitiva delle estensioni SCAP per Microsoft System Center Configuration Manager

Usare questa sezione per apprendere le novità della versione più recente.

Versione non definitiva delle estensioni SCAP per System Center Configuration Manager:

- Include un'estensione della console di Configuration Manager che supporta completamente la conversione di contenuto SCAP in linee di base delle Impostazioni di conformità di System Center Configuration Manager Current Branch
- SCAP 1.2 ed è compatibile con le versioni SCAP 1.1 e 1.0.


  - Extensible Configuration Checklist Description Format (XCCDF) 1.2.
  - Open Vulnerability and Assessment Language (OVAL) versioni fino a 5.10.
  - La generazione di report Asset Reporting Format (ARF) 1.1.
  - Common Platform Enumeration (CPE) 2.3
  - Common Vulnerabilities and Exposures (CVE)
  - Common Configuration Enumeration (CCE) 5
  - Supporta USGCB Internet Explorer 8, USGCB Windows 7 e USGCB Windows 7 Firewall.

- Include una procedura guidata dell'interfaccia utente per importare SCAP 1.2/1.1/1.0 e contenuto OVAL per la conversione in linee di base di configurazione.


  - La selezione di flussi di dati di origine SCAP e di profili e benchmark XCCDF per la conversione.

- Include una procedura guidata dell'interfaccia utente per esportare i risultati di valutazione di configurazione in report XML in formato SCAP


  - Consente di visualizzare il file di origine, il flusso dei dati SCAP, il benchmark XCCDF e il profilo XCCDF usati per generare la linea di base.
  - La generazione del report Cyberscope Lightweight Asset Summary Results (LASR).

- Supporta la generazione di report SCAP basati sulla distribuzione della linea di base di configurazione. Include un nuovo dashboard per la visualizzazione della conformità dei client, nonché della conformità alla regola XCCDF. Il dashboard supporta il drill-through per report più dettagliati in cui è possibile eseguire ricerche e applicare filtri.
- Migliora le prestazioni di elementi di configurazione di diversi tipi convertiti da test OVAL, consentendo una valutazione più rapida.

- Corregge diversi problemi rilevati in contenuto DISA v1r3 in Windows 10.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Processo di distribuzione delle estensioni SCAP per Microsoft System Center Configuration Manager

Questa guida descrive come analizzare, valutare e creare report sulla conformità SCAP mediante SCAP Extensions per Microsoft System Center Configuration Manager. Ecco un breve riepilogo delle procedure da seguire:

- Preparare l'infrastruttura dei prerequisiti per sfruttare i vantaggi delle estensioni.
- Installare e configurare SCAP Extensions per Microsoft System Center Configuration Manager.
- Scaricare, installare e configurare i file di flusso dei dati SCAP dal [National Vulnerability Database](http://nvd.nist.gov) (NVD).
- Convertire e importare i file di flusso dei dati SCAP direttamente in una linea di base di impostazioni di conformità di System Center Configuration Manager usando l'Importazione guidata **o** tramite un file cabinet (con estensione cab) dallo strumento da riga di comando Microsoft.Sces.ScapToDcm.exe.
- Esportare i risultati di conformità nel formato SCAP tramite l'Esportazione guidata o lo strumento da riga di comando Microsoft.Sces.DcmToScap.exe.

# <a name="terms"></a>Termini

**ID OVAL:** identificatore di una definizione OVAL specifica conforme al formato per gli ID OVAL.

**Flusso dei dati dei risultati SCAP:** aggregazione di componenti SCAP, insieme ai mapping dei riferimenti tra i componenti SCAP, che contiene il contenuto di output (risultati).

**Flusso dei dati di origine SCAP:** aggregazione di componenti SCAP, insieme ai mapping dei riferimenti tra i componenti SCAP, che contiene il contenuto di input (origine).

# <a name="prepare-the-prerequisite-infrastructure"></a>Preparare l'infrastruttura dei prerequisiti

Per sfruttare i vantaggi delle estensioni SCAP per Microsoft System Center Configuration Manager, assicurarsi che siano soddisfatti i requisiti hardware e software seguenti.

## <a name="software-requirements"></a>Requisiti software

Per installare, configurare ed eseguire SCAP Extensions per Microsoft System Center Configuration Manager, è necessario un computer con il software seguente:

- Una [versione supportata](/sccm/core/servers/manage/current-branch-versions-supported) della console di System Center Configuration Manager Current Branch.
- Un sistema operativo compatibile con la console di System Center Configuration Manager. Per un elenco di sistema operativi compatibili, vedere l'articolo [Sistemi operativi supportati per le console di System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

Oltre al computer che esegue le estensioni SCAP, sono anche necessari gli elementi seguenti:

- Un'infrastruttura System Center Configuration Manager Current Branch. Per altre informazioni sui requisiti per una distribuzione di Configuration Manager, vedere l'articolo [Configurazioni supportate per System Center Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).

I computer per i quali si desidera valutare la conformità SCAP devono disporre delle seguenti configurazioni e del seguente software:

- Componente Gestione conformità e impostazioni abilitato nel client di Configuration Manager.
- Windows PowerShell 2.0 o versione successiva.
- Criteri di esecuzione di PowerShell di Configuration Manager impostati su **Ignora**. Per altre informazioni, vedere l'articolo [Criteri di esecuzione di PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).
- Uno dei sistemi operativi seguenti
  - Versione di rilascio di Windows 7 o Sp1, 32 bit o 64 bit
  - Windows 10 a 32 bit o a 64 bit
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Requisiti hardware

Sono qui indicati i requisiti minimi di sistema:

[Pianificazione delle configurazioni hardware per Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Funzionalità di accessibilità

Le estensioni SCAP per System Center Configuration Manager includono strumenti da riga di comando Windows in grado di sfruttare le funzionalità e gli strumenti di accessibilità di Windows.

- Questo manuale dell'utente documenta i parametri della riga di comando per Microsoft.Sces.ScapToDcm.exe e Microsoft.Sces.DcmToScap.exe.
- Con -help e -? vengono visualizzati gli strumenti utilizzabili sullo schermo, dove saranno disponibili per le utilità per la lettura dello schermo e altre tecnologie per l'accesso facilitato.
- [Accessibilità](http://windows.microsoft.com/windows/help/accessibility) di Windows

Le estensioni SCAP usano anche le funzionalità di System Center Configuration Manager.  Configuration Manager include funzionalità che rendono il prodotto più accessibile a persone con particolari esigenze.

- [Funzionalità di accessibilità in System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Per informazioni generali sui prodotti e i servizi di accessibilità Microsoft, visitare il [sito Web Accessibilità in Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Installare e configurare le estensioni SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
