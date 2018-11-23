---
title: Creare e distribuire criteri di Windows Defender Application Guard
titleSuffix: Configuration Manager
description: Creare e distribuire criteri di Windows Defender Application Guard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82423914b1d1f5cae8fa4ecea3d02ef02d23703a
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52258911"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creare e distribuire criteri di Windows Defender Application Guard 
*Si applica a: System Center Configuration Manager (Current Branch)* 
 <!-- 1351960 --> è possibile creare e distribuire [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) criteri usando l'endpoint di Configuration Manager protezione dati. Questi criteri consentono di proteggere gli utenti tramite l'apertura dei siti Web non attendibili in un contenitore isolato protetto e non accessibile da altre parti del sistema operativo.

## <a name="prerequisites"></a>Prerequisiti

Per creare e distribuire criteri di Windows Defender Application Guard, è necessario usare la versione Fall Creators Update di Windows 10 (1709). Inoltre, i dispositivi Windows 10 in cui verranno distribuiti i criteri devono essere configurati con criteri di isolamento di rete. Per altre informazioni, vedere [Panoramica di Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Creare un criterio e passare alle impostazioni disponibili:

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando l'[articolo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) come riferimento, è possibile selezionare e configurare le impostazioni disponibili. Configuration Manager consente di definire impostazioni di criteri specifiche, vedere [Impostazioni per l'interazione degli host](#BKMK_HIS) e [Comportamento delle applicazioni](#BKMK_AppB).
5. Nella pagina **Definizione di rete** specificare l'identità aziendale e definire il limite di rete aziendale.

    > [!NOTE]
    > I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. È possibile creare due tipi diversi di elenchi di isolamento di rete e quindi distribuirli nel client:
    >
    >  - uno da Windows Information Protection
    >  - un altro da Windows Defender Application Guard
    >
    > Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo. Per altre informazioni, vedere la [documentazione di Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Al termine, completare la procedura guidata e distribuire i criteri in uno o più dispositivi Windows 10 1709.

### <a name="bkmk_HIS"></a> Impostazioni per l'interazione degli host
Configura le interazioni tra i dispositivi host e il contenitore Application Guard. Prima di Configuration Manager versione 1802, le impostazioni relative al comportamento delle applicazioni e all'interazione degli host si trovavano nella scheda **Impostazioni**.

- **Appunti**: in Impostazioni prima di Configuration Manager 1802
    - Tipo di contenuto consentito
        - Testo
        - Immagini
- **Stampa:**
    - Abilitazione della stampa in XPS
    - Abilitazione della stampa in PDF
    - Abilitazione della stampa nelle stampanti locali
    - Abilitazione della stampa nelle stampanti di rete
- **Grafica:** (a partire da Configuration Manager versione 1802)
    - Accesso all'unità di elaborazione grafica virtuale
- **File:** (a partire da Configuration Manager versione 1802)
    - Salvataggio dei file scaricati nell'host

### <a name="bkmk_ABS"></a> Impostazioni relative al comportamento delle applicazioni
Consentono di configurare il comportamento delle applicazioni all'interno della sessione di Application Guard. Prima di Configuration Manager versione 1802, le impostazioni relative al comportamento delle applicazioni e all'interazione degli host si trovavano nella scheda **Impostazioni**.

- **Contenuto:**
   - I siti aziendali possono caricare contenuti non aziendali, ad esempio plug-in di terze parti.
- **Altro:**
    - Conserva i dati del browser generati dall'utente
    - Controlla gli eventi di sicurezza nella sessione Application Guard isolata



## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Windows Defender Application Guard: [Windows Defender Application Guard Overview](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) (Panoramica di Windows Defender Application Guard).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard) (Domande frequenti su Windows Defender Application Guard).
