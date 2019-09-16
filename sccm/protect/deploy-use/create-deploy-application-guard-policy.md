---
title: Gestire i criteri di Application Guard
titleSuffix: Configuration Manager
description: Informazioni su come creare e distribuire criteri di Windows Defender Application Guard
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9567dc53a204d639b3da5920cf1fc452426a11f
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892480"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creare e distribuire criteri di Windows Defender Application Guard

*Si applica a: System Center Configuration Manager (Current Branch)*
<!-- 1351960 -->  
È possibile creare e distribuire criteri di [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) usando Configuration Manager Endpoint Protection. Questi criteri consentono di proteggere gli utenti aprendo i siti Web non attendibili in un contenitore isolato protetto non accessibile da altre parti del sistema operativo.

## <a name="prerequisites"></a>Prerequisiti

Per creare e distribuire criteri di Windows Defender Application Guard, è necessario usare la versione Fall Creators Update di Windows 10 (1709). I dispositivi Windows 10 in cui verranno distribuiti i criteri devono essere configurati con criteri di isolamento di rete. Per altre informazioni, vedere [Panoramica di Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Creare un criterio e individuare le impostazioni disponibili

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando l'[articolo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) come riferimento, è possibile selezionare e configurare le impostazioni disponibili. Configuration Manager consente di impostare determinate impostazioni dei criteri:
   - [Impostazioni per l'interazione degli host](#bkmk_HIS)
   - [Comportamento dell'applicazione](#bkmk_ABS)
   - [Gestione file](#bkmk_FM)
5. Nella pagina **Definizione di rete** specificare l'identità aziendale e definire il limite di rete aziendale.

    > [!NOTE]
    > I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. È possibile creare due tipi diversi di elenchi di isolamento di rete e quindi distribuirli nel client:
    >
    >  - uno da Windows Information Protection
    >  - un altro da Windows Defender Application Guard
    >
    > Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo. Per altre informazioni, vedere la [documentazione di Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

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

### <a name="bkmk_FM"></a> Gestione file
<!--3555858-->
A partire da Configuration Manager versione 1906, è disponibile un'impostazione dei criteri che consente agli utenti di considerare attendibili i file che normalmente si aprono in Application Guard. Al termine dell'esecuzione, i file vengono aperti nel dispositivo host anziché in Application Guard. Per altre informazioni sui criteri di Application Guard, vedere [Configurare le impostazioni dei criteri di Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard).

- **Consenti agli utenti di considerare attendibili i file aperti in Windows Defender Application Guard** : consente all'utente di contrassegnare i file come attendibili. Quando un file è attendibile, viene aperto nell'host anziché in Application Guard. Si applica ai client Windows 10 versione 1809 o versioni successive.
  - **Non consentito:** Impedisce agli utenti di contrassegnare i file come attendibili (impostazione predefinita).
  - **File controllato da antivirus:** Consente agli utenti di contrassegnare i file come attendibili dopo un controllo antivirus.
  - **Tutti i file:** Consente agli utenti di contrassegnare qualsiasi file come attendibile.

Quando si Abilita la gestione dei file, è possibile che vengano visualizzati errori registrati nel DCMReporting. log del client. Gli errori riportati di seguito in genere non hanno effetto sulle funzionalità: <!--4619457-->

- Nei dispositivi compatibili:
  - FileTrustCriteria_condition not found (Impossibile trovare FileTrustCriteria_condition)
- Nei dispositivi non compatibili:
  - FileTrustCriteria_condition not found (Impossibile trovare FileTrustCriteria_condition)
  - FileTrustCriteria_condition could not be located in the map (Impossibile trovare FileTrustCriteria_condition nella mappa)
  - FileTrustCriteria_condition not found in digest (Impossibile trovare FileTrustCriteria_condition nel digest)

Per modificare le impostazioni di Application Guard, espandere **Endpoint Protection** nell'area di lavoro **asset e conformità** , quindi fare clic sul nodo **Windows Defender Application Guard** . Fare clic con il pulsante destro del mouse sui criteri da modificare e quindi selezionare **Proprietà**.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni su Windows Defender Application Guard: [Windows Defender Application Guard Overview](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) (Panoramica di Windows Defender Application Guard).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard) (Domande frequenti su Windows Defender Application Guard).
