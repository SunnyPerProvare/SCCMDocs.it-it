---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Informazioni su come gestire e monitorare Microsoft Defender Advanced Threat Protection, un nuovo servizio che consente alle organizzazioni di rispondere agli attacchi avanzati.
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72ad06228a7ae0dd0fa375ff1152771790b10bbe
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379978"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1606 di Configuration Manager (Current Branch), Endpoint Protection consente di gestire e monitorare [Microsoft Defender Advanced Threat Protection (ATP)](https://aka.ms/technet-wdatp), noto in precedenza come Windows Defender ATP. Microsoft Defender ATP consente alle aziende di rilevare e analizzare attacchi avanzati alle loro reti e di reagire in modo efficace.  I criteri di Configuration Manager o di Microsoft Intune semplificano il caricamento e il monitoraggio di Windows 10, versione 1607 (build 14328) o successiva.

Microsoft Defender ATP è un servizio disponibile in [Windows Defender Security Center](https://securitycenter.windows.com). Tramite l'aggiunta e la distribuzione di un file di configurazione per il caricamento di client, Configuration Manager è in grado di monitorare lo stato di distribuzione e l'integrità dell'agente di Microsoft Defender ATP. Microsoft Defender ATP è supportato nei PC che eseguono il client di Configuration Manager o che sono gestiti da Microsoft Intune. I computer gestiti tramite la gestione dei dispositivi mobili ibrida di Intune, tuttavia, non sono supportati.

 **Prerequisiti**  

-   Sottoscrizione al servizio online Microsoft Defender Advanced Threat Protection  
-   Computer cient che eseguono Windows 10, 1607 e versioni successive  
-   Computer client che eseguono l'agente client di Configuration Manager versione 1610 o successiva o gestiti da Microsoft Intune

## <a name="how-to-create-an-onboarding-configuration-file"></a>Come creare un file di configurazione per il caricamento  

 1.  Accedere al [servizio online di Microsoft Defender ATP](https://securitycenter.windows.com/)   

 2.  Fare clic sulla voce di menu **Endpoint Management** (Gestione Endpoint).  

 3.  Selezionare **System Center Configuration Manager (current branch) version 1606** (System Center Configuration Manager (Current Branch) versione 1606) e fare clic su **Download package** (Scarica pacchetto).  

 4.  Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.

> [!IMPORTANT]
> Il file di configurazione di Microsoft Defender ATP contiene informazioni riservate che devono essere protette.

## <a name="onboard-devices-for-microsoft-defender-atp"></a>Onboarding dei dispositivi per Microsoft Defender ATP  

1. Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Protezione endpoint** > **Criteri di Windows Defender ATP** e fare clic su **Creare criteri di Windows Defender ATP**. Si apre la procedura guidata criteri di Microsoft Defender ATP.  

2. Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Onboarding** (Caricamento). Fare clic su **Avanti**.  

3. Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Microsoft Defender ATP dell'organizzazione. Fare clic su **Avanti**.  

4. Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  

   - **Nessuno**   

   - **Tutti i tipi di file**  

     Fare clic su **Avanti**.  

5. Esaminare le informazioni di riepilogo e completare la procedura guidata.  

6. È ora possibile distribuire i criteri di Microsoft Defender ATP nei computer client gestiti facendo clic su **Distribuisci**.  

## <a name="monitor-microsoft-defender-atp"></a>Monitora Microsoft Defender ATP  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Sicurezza** e quindi fare clic su **Windows Defender ATP**.  

2.  Esaminare il dashboard di Microsoft Defender Advanced Threat Protection.  

    -   **Windows Defender Agent Deployment Status** (Stato distribuzione agente Windows Defender): il numero e la percentuale di computer client gestiti idonei con criteri Microsoft Defender ATP attivi caricati  

    -   **Integrità dell'agente di Windows Defender ATP**: percentuale di computer client che inviano informazioni sullo stato per i relativi agenti di Microsoft Defender ATP  

        -   **Integro**: funziona correttamente  

        -   **Inattivo**: nessun dato inviato al servizio durante il periodo di tempo  

        -   **Stato agente**: il servizio di sistema per l'agente in Windows non è in esecuzione  

        -   **Non caricati**: i criteri sono stati applicati ma l'agente non ha segnalato il caricamento dei criteri  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Come creare e distribuire un file di configurazione per l'offboarding  

1.  Accedere al [servizio online di Microsoft Defender ATP](https://securitycenter.windows.com/)   

2.  Fare clic sulla voce di menu **Endpoint Management** (Gestione Endpoint).  

3.  Selezionare **System Center Configuration Manager (current branch) version 1606** (System Center Configuration Manager (Current Branch) versione 1606) e fare clic su **Endpoint offboarding** (Offobarding endpoint).  

4.  Scaricare il file di archivio compresso (zip) ed estrarre il contenuto. I file per l'offboarding sono validi per 30 giorni.

5.  Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Protezione endpoint** > **Criteri di Windows Defender ATP** e fare clic su **Creare criteri di Windows Defender ATP**. Si apre la procedura guidata criteri di Microsoft Defender ATP.  

6.  Digitare il **nome** e la **descrizione** per il criterio di Microsoft Defender ATP e selezionare **Offboarding**. Fare clic su **Avanti**.  

7.  Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Microsoft Defender ATP dell'organizzazione. Fare clic su **Avanti**.  

8.  Esaminare le informazioni di riepilogo e completare la procedura guidata.  

9.  È ora possibile distribuire i criteri di Microsoft Defender ATP nei computer client gestiti facendo clic su **Distribuisci**.  

> [!IMPORTANT]
> I file di configurazione di Microsoft Defender ATP contengono informazioni sensibili che devono essere protette.

[Microsoft Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Risolvere i problemi di onboarding di Microsoft Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
