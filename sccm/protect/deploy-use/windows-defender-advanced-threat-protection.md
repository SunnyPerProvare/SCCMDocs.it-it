---
title: Windows Defender Advanced Threat Protection | Documentazione Microsoft
description: Informazioni su come gestire e monitorare Windows Defender Advanced Threat Protection, un nuovo servizio che consente alle organizzazioni di rispondere agli attacchi avanzati.
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ebda27c0f3848615346c2ecf1ab8b9bb9ab6f0d
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.contentlocale: it-it
ms.lasthandoff: 05/26/2017

---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1606 di Configuration Manager (Current Branch), Endpoint Protection consente di gestire e monitorare Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP è un nuovo servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti.  Altre informazioni su [Windows Defender ATP](http://aka.ms/technet-wdatp). I criteri di Configuration Manager possono aiutare a caricare e monitorare Windows 10, versione 1607 (build 14328) o versione successiva.

Windows Defender ATP è un servizio disponibile nel [Centro sicurezza PC Windows](https://securitycenter.windows.com). Tramite l'aggiunta e la distribuzione di un file di configurazione per il caricamento di client, Configuration Manager è in grado di monitorare lo stato di distribuzione e l'integrità dell'agente di Windows Defender ATP. Windows Defender ATP è supportato solo nei computer che eseguono il client di Configuration Manager. Non sono supportati la soluzione Gestione di dispositivi mobili locale e computer gestiti da MDM Intune (ibrido).

 **Prerequisiti**  

-   Sottoscrizione al servizio online Windows Defender Advanced Threat Protection  
-   Computer cient che eseguono Windows 10, 1607 e versioni successive  
-   Computer client che eseguono Configuration Manager 1610 o l'agente client di versioni successive

## <a name="how-to-create-an-onboarding-configuration-file"></a>Come creare un file di configurazione per il caricamento  

 1.  Accedere al [servizio online Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Fare clic sulla voce di menu **Endpoint Management** (Gestione Endpoint).  

 3.  Selezionare **System Center Configuration Manager (current branch) version 1606** (System Center Configuration Manager (Current Branch) versione 1606) e fare clic su **Download package** (Scarica pacchetto).  

 4.  Scaricare il file di archivio compresso (zip) ed estrarre il contenuto.

> [!IMPORTANT]
> Il file di configurazione di Windows Defender ATP contiene informazioni riservate che devono essere protette.

## <a name="onboard-devices-for-windows-defender-atp"></a>Caricare dispositivi per Windows Defender ATP  

1.  Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Protezione endpoint** > **Criteri di Windows Defender ATP** e fare clic su **Creare criteri di Windows Defender ATP**. Verrà visualizzata la Creazione guidata criteri di Windows Defender ATP.  

2.  Digitare il **nome** e la **descrizione** per il criterio di Windows Defender ATP e selezionare **Onboarding** (Caricamento). Fare clic su **Avanti**.  

3.  Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Windows Defender ATP dell'organizzazione. Fare clic su **Avanti**.  

4.  Specificare i file campione che vengono raccolti e condivisi dai dispositivi gestiti per l'analisi.  

    -   **Nessuno**   

    -   **Tutti i tipi di file**  

     Fare clic su **Avanti**.  

5.  Esaminare le informazioni di riepilogo e completare la procedura guidata.  

6.  È ora possibile distribuire i criteri di Windows Defender ATP nei computer client gestiti facendo clic su **Distribuisci**.  

## <a name="monitor-windows-defender-atp"></a>Monitorare Windows Defender ATP  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Sicurezza** e quindi fare clic su **Windows Defender ATP**.  

2.  Esaminare il dashboard di Windows Defender Advanced Threat Protection.  

    -   **Windows Defender Agent Deployment Status** (Stato distribuzione agente Windows Defender): il numero e la percentuale di computer client gestiti idonei con criteri Windows Defender ATP attivi caricati  

    -   **Integrità dell'agente di Windows Defender ATP**: percentuale di computer client che inviano informazioni sullo stato per i relativi agenti di Windows Defender ATP  

        -   **Integro**: funziona correttamente  

        -   **Inattivo**: nessun dato inviato al servizio durante il periodo di tempo  

        -   **Stato agente**: il servizio di sistema per l'agente in Windows non è in esecuzione  

        -   **Non caricati**: i criteri sono stati applicati ma l'agente non ha segnalato il caricamento dei criteri  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Come creare e distribuire un file di configurazione per l'offboarding  

1.  Accedere al [servizio online Windows Defender ATP](https://securitycenter.windows.com/)   

2.  Fare clic sulla voce di menu **Endpoint Management** (Gestione Endpoint).  

3.  Selezionare **System Center Configuration Manager (current branch) version 1606** (System Center Configuration Manager (Current Branch) versione 1606) e fare clic su **Endpoint offboarding** (Offobarding endpoint).  

4.  Scaricare il file di archivio compresso (zip) ed estrarre il contenuto. I file per l'offboarding sono validi per 30 giorni.

5.  Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Protezione endpoint** > **Criteri di Windows Defender ATP** e fare clic su **Creare criteri di Windows Defender ATP**. Verrà visualizzata la Creazione guidata criteri di Windows Defender ATP.  

6.  Digitare il **nome** e la **descrizione** per il criterio di Windows Defender ATP e selezionare **Offboarding**. Fare clic su **Avanti**.  

7.  Usare **Sfoglia** per cercare il file di configurazione fornito dal tenant del servizio cloud Windows Defender ATP dell'organizzazione. Fare clic su **Avanti**.  

8.  Esaminare le informazioni di riepilogo e completare la procedura guidata.  

9.  È ora possibile distribuire i criteri di Windows Defender ATP nei computer client gestiti facendo clic su **Distribuisci**.  

> [!IMPORTANT]
> I file di configurazione di Windows Defender ATP contengono informazioni sensibili che devono essere protette.

[Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Risolvere i problemi di onboarding di Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)

