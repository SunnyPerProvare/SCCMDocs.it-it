---
title: Technical Preview 1707 | Microsoft Docs
description: "Informazioni sulle funzionalità disponibili nella versione Technical Preview 1707 per System Center Configuration Manager."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 1f57c63ceeb13c7f7d760d7ecfb48df749da6770
ms.openlocfilehash: 118f20768ffc99364eb9e8cf2074d7a23f4dc572
ms.contentlocale: it-it
ms.lasthandoff: 07/28/2017

---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>Funzionalità della versione Technical Preview 1707 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo presenta le funzionalità disponibili nella versione Technical Preview 1707 per System Center Configuration Manager. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Supporto della peer cache del client per i file di installazione rapida per Windows 10 e Office 365
<!-- 1352486 -->
A partire da questa versione, la peer cache supporta la distribuzione dei file di installazione rapida del contenuto per Windows 10 e dei file di aggiornamento per Office 365. Non sono richieste configurazioni aggiuntive.

## <a name="surface-device-dashboard"></a>Dashboard del dispositivo Surface
<!--1355788-->
Il dashboard del dispositivo Surface visualizza informazioni sui dispositivi Surface rilevati nell'ambiente in uso. Nella console passare a **Monitoraggio** > **Surface Devices** (Dispositivi Surface). È possibile visualizzare le seguenti informazioni:
- percentuale di dispositivi Surface
- percentuale di modelli Surface
- prime cinque versioni del sistema operativo

Fare clic su una sezione del grafico dei **modelli Surface** per un elenco completo dei dispositivi.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurare e distribuire i criteri di Windows Defender Application Guard
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) è una nuova funzionalità di Windows che consente di proteggere gli utenti con l'apertura di siti Web non attendibili in un contenitore protetto isolato non è accessibile da altre parti del sistema operativo. In questa versione Technical Preview, è stato aggiunto il supporto per configurare questa funzionalità usando le impostazioni di conformità di Configuration Manager configurate dall'utente e quindi distribuite in una raccolta. Questa funzionalità verrà rilasciata in anteprima per la versione a 64 bit di Windows 10 Creators Update (nome in codice: RS2). Per provare ora questa funzionalità è necessario usare una versione di anteprima dell'aggiornamento.

### <a name="before-you-start"></a>Prima di iniziare

Per creare e distribuire i criteri di Windows Defender Application Guard, configurare i dispositivi Windows 10 in cui vengono distribuiti i criteri con un criterio di isolamento rete. Per informazioni dettagliate, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Questa funzionalità funziona solo con le build correnti di Windows 10 Insider. Per provarla, i client devono eseguire una build recente di Windows 10 Insider.

### <a name="try-it-out"></a>Prova subito!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Per creare un criterio e per individuare le impostazioni disponibili:

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando il post di blog come riferimento, è possibile selezionare e configurare le impostazioni disponibili per provare la funzionalità.
5. In questa versione è stata aggiunta la nuova pagina **Definizione di rete** alla procedura guidata. Usare questa pagina per specificare l'identità aziendale e definire il limite di rete aziendale.<br>I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. In questa versione è possibile creare due tipi diversi di elenchi di isolamento rete, uno da Windows Information Protection e uno da Windows Defender Application Guard, e distribuirli al client. Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo.
Altre informazioni su come specificare le definizioni di rete sono disponibili nella [documentazione di Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
6. Al termine, completare la procedura guidata e distribuire il criterio in uno o più dispositivi Windows 10.

### <a name="further-reading"></a>Letture di approfondimento
Per altre informazioni su Windows Defender Application Guard, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Per altre informazioni sulla modalità autonoma di Windows Defender Application Guard vedere [questo post di blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Aggiungere i parametri quando si distribuiscono gli script di PowerShell da Configuration Manager

<!-- 1236459 --->

Nell'ultima versione Technical Preview è stata introdotta una nuova funzionalità che consente di [creare ed eseguire script di PowerShell dalla console di Configuration Manager]( /core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
La funzionalità è stata espansa in questa versione Technical Preview. Configuration Manager ora legge lo script di PowerShell e visualizza tutti i parametri nella procedura guidata Crea script. È possibile specificare nella procedura guidata un valore per il parametro che verrà usato durante l'esecuzione dello script. In alternativa, è possibile omettere il parametro. In questo caso è necessario specificare un valore per il parametro quando si esegue lo script.

### <a name="try-it-out"></a>Prova subito!

1. Seguire le istruzioni per [creare ed eseguire script di PowerShell dalla console di Configuration Manager]( /core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. Nella nuova pagina **Parametri script** della **procedura guidata Crea script** scegliere un parametro e quindi fare clic su **Modifica**.
3. Specificare un valore di parametro per il parametro selezionato e quindi fare clic su **OK**.
4. Completare la procedura guidata.

Quando viene eseguito lo script, verranno usati i valori dei parametri configurati.
