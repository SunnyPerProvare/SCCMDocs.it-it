---
title: Pianificare la gestione di BitLocker
titleSuffix: Configuration Manager
description: Pianificare la gestione di Crittografia unità BitLocker con Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 25f8b13cbf0aa6e505c7fe22980e5bce3a39a2e4
ms.sourcegitcommit: 3a0eaf3378632f312b46b2b8a524e286f9c4cd8e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75198728"
---
# <a name="plan-for-bitlocker-management"></a>Pianificare la gestione di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!-- 3601034 -->

A partire dalla versione 1910, usare Configuration Manager per gestire Crittografia unità BitLocker (BDE) per i client Windows locali. Fornisce la gestione completa del ciclo di vita di BitLocker che può sostituire l'utilizzo di Microsoft BitLocker Administration and Monitoring (MBAM).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/configmgr/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  

Per altre informazioni, vedere [Panoramica di BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Per gestire la crittografia nei dispositivi Windows 10 con co-gestione usando il servizio cloud di Microsoft Endpoint Manager, passare il [carico di lavoro **Endpoint Protection** ](/configmgr/comanage/workloads#endpoint-protection) a Intune. Per altre informazioni sull'uso di Intune, vedere [crittografia di Windows](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Caratteristiche

Configuration Manager offre le funzionalità di gestione seguenti per Crittografia unità BitLocker:

### <a name="client-deployment"></a>Distribuzione client

Distribuire il client di BitLocker nei dispositivi Windows gestiti che eseguono Windows 10, Windows 8.1 o Windows 7

### <a name="manage-encryption-policies"></a>Gestire i criteri di crittografia

- Ad esempio: scegliere crittografia unità e livello di codifica, configurare i criteri di esenzione utente, impostazioni crittografia unità dati fisse.

- Determinare gli algoritmi con cui crittografare il dispositivo e i dischi di destinazione per la crittografia.

- Forzare gli utenti a essere conformi ai nuovi criteri di sicurezza prima di usare il dispositivo.

- Personalizzare il profilo di sicurezza dell'organizzazione in base ai singoli dispositivi.

- Quando un utente sblocca l'unità del sistema operativo, specificare se sbloccare solo un'unità del sistema operativo o tutte le unità collegate.

### <a name="compliance-reports"></a>Report di conformità

Report predefiniti per:

- Stato di crittografia per volume o per dispositivo
- Utente primario del dispositivo
- Stato di conformità
- Motivi per la mancata conformità

### <a name="administration-and-monitoring-website"></a>Sito Web di amministrazione e monitoraggio

Consentire ad altri utenti dell'organizzazione all'esterno della console di Configuration Manager di semplificare il ripristino della chiave, inclusa la rotazione della chiave e altri supporti correlati a BitLocker. Ad esempio, gli amministratori help desk possono aiutare gli utenti con il recupero della chiave.

### <a name="user-self-service-portal"></a>Portale self-service degli utenti

Consentire agli utenti di utilizzare una chiave monouso per sbloccare un dispositivo crittografato con BitLocker. Una volta usata questa chiave, viene generata una nuova chiave per il dispositivo.

## <a name="prerequisites"></a>Prerequisiti

- Nella versione 1910, per creare un criterio di gestione di BitLocker, è necessario il ruolo **amministratore completo** in Configuration Manager.

- Per integrare il servizio di ripristino di BitLocker in Configuration Manager richiede un punto di gestione abilitato per HTTPS. Nelle proprietà del punto di gestione, l'impostazione **connessioni client** deve essere **https**.

    > [!NOTE]
    > Nella versione 1910 non supporta il protocollo HTTP avanzato.

- Per utilizzare i report di gestione di BitLocker, installare il ruolo del sistema del sito del punto di Reporting Services. Per altre informazioni, vedere [Configurare la creazione di report in Reporting Manager](/configmgr/core/servers/manage/configuring-reporting).

    > [!NOTE]
    > Nella versione 1910, affinché il **report controllo ripristino** funzioni dal sito Web di Administration and Monitoring, utilizzare solo un punto di Reporting Services nel sito primario.

- Per utilizzare il portale self-service o il sito Web di Administration and Monitoring, è necessario disporre di un server Windows che esegue IIS. È possibile riutilizzare un sistema del sito Configuration Manager oppure utilizzare un server Web autonomo con connettività al server di database del sito. Usare una [versione del sistema operativo supportata per i server del sistema del sito](/configmgr/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

    > [!NOTE]
    > Nella versione 1910, installare solo il portale self-service e il sito Web di Administration and Monitoring con un database del sito primario. In una gerarchia installare questi siti Web per ogni sito primario.

- Sul server Web che ospiterà il portale self-service, installare [Microsoft ASP.NET MVC 4,0](https://docs.microsoft.com/aspnet/mvc/mvc4).

- Per l'account utente che esegue lo script del programma di installazione del portale sono necessari i diritti di **sysadmin** di SQL per il server di database del sito. Durante il processo di installazione, lo script imposta i diritti di accesso, utente e ruolo SQL per l'account del computer del server Web. È possibile rimuovere l'account utente dal ruolo sysadmin dopo aver completato l'installazione del portale self-service e il sito Web di Administration and Monitoring.

> [!TIP]
> Per impostazione predefinita, il passaggio della sequenza di attività **attiva BitLocker** consente di crittografare solo *lo spazio utilizzato* sull'unità. Gestione BitLocker utilizza la crittografia *completa del disco* . Configurare questo passaggio della sequenza di attività per abilitare l'opzione per l' **uso della crittografia completa del disco**. Per ulteriori informazioni, vedere [passaggi della sequenza di attività-Abilita BitLocker](/configmgr/osd/understand/task-sequence-steps#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Passaggi successivi

[Crittografare i dati di ripristino](/configmgr/protect/deploy-use/bitlocker/encrypt-recovery-data) (un prerequisito facoltativo prima di distribuire i criteri per la prima volta)

[Distribuire il client di gestione di BitLocker](/configmgr/protect/deploy-use/bitlocker/deploy-management-agent)
