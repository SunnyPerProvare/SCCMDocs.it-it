---
title: Windows Defender Advanced Threat Protection | System Center Configuration Manager
description: Informazioni su come gestire e monitorare Windows Defender Advanced Threat Protection, un nuovo servizio che consente alle organizzazioni di rispondere agli attacchi avanzati.
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: a4ad2d93ecd994fff00dab33084a734252cac651

---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender Advanced Threat Protection

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1606 di Configuration Manager (Current Branch), Endpoint Protection consente di gestire e monitorare Windows Defender Advanced Threat Protection (ATP). Windows Defender ATP è un nuovo servizio che consente alle aziende di rilevare, analizzare e rispondere agli attacchi avanzati sulle reti.  Altre informazioni su [Windows Defender ATP](http://aka.ms/technet-wdatp). I criteri di Configuration Manager possono aiutare a caricare e monitorare Windows 10, versione 1607 (build 14328) o versione successiva.

Windows Defender ATP è un servizio disponibile nel [Centro sicurezza PC Windows](https://securitycenter.windows.com). Tramite l'aggiunta e la distribuzione di un file di configurazione per il caricamento di client, Configuration Manager è in grado di monitorare lo stato di distribuzione e l'integrità dell'agente di Windows Defender ATP. Windows Defender ATP è supportato solo nei computer che eseguono il client di Configuration Manager. Non sono supportati la soluzione Gestione di dispositivi mobili locale e computer gestiti da MDM Intune (ibrido).

 **Prerequisiti**  

-   Sottoscrizione al servizio online Windows Defender Advanced Threat Protection  

-   Client che eseguono Windows 10, 1607 e versioni successive  

## <a name="how-to-create-an-onboarding-configuration-file"></a>Come creare un file di configurazione per il caricamento  

 1.  Accedere al [servizio online Windows Defender ATP](https://securitycenter.windows.com/)   

 2.  Fare clic sulla voce di menu **Caricamento client**.  

 3.  Selezionare **System Center Configuration Manager** e fare clic su **Scarica pacchetto**.  

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



<!--HONumber=Nov16_HO1-->


