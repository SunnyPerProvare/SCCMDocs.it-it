---
title: Registri eventi di BitLocker
titleSuffix: Configuration Manager
description: Ulteriori informazioni su come utilizzare le informazioni di BitLocker nel registro eventi di Windows per risolvere i problemi
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 813975c200a281445a6fe24b9036216174acf393
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662339"
---
# <a name="bitlocker-event-logs"></a>Registri eventi di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

L'agente di Gestione BitLocker e i servizi Web utilizzano i registri eventi di Windows per registrare i messaggi. Nella Visualizzatore eventi passare a **registri applicazioni e servizi**, **Microsoft**, **Windows**. Il canale di log (nodo) varia a seconda del computer e del componente:

- **Mbam**: agente di Gestione BitLocker in un computer client
- **Mbam-Web**:
  - Servizio di ripristino nel punto di gestione
  - Portale self-service
  - Sito Web di amministrazione e monitoraggio

Per ulteriori informazioni su messaggi specifici in questi log, vedere gli articoli seguenti:

- [Registri eventi del client](/configmgr/protect/tech-ref/bitlocker/client-event-logs)
- [Registri eventi del server](/configmgr/protect/tech-ref/bitlocker/server-event-logs)

Per impostazione predefinita, in ogni nodo vengono visualizzati due canali di log: **admin** e **Operational**. Per informazioni più dettagliate sulla risoluzione dei problemi, è anche possibile visualizzare i [log di debug e di analisi](#bkmk_debug).

## <a name="log-properties"></a>Proprietà del log

In Visualizzatore eventi di Windows selezionare un log specifico. Ad esempio, **admin**. Scegliere **Proprietà** dal menu **Azione**. Configurare le seguenti impostazioni:

- **Dimensioni massime log (KB)** : per impostazione predefinita, questa impostazione è `1028` (1 MB) per tutti i log.
- **Quando viene raggiunta la dimensione massima del registro eventi**: per impostazione predefinita, i log di **Amministrazione** e **operativi** sono impostati per **sovrascrivere gli eventi in base alle esigenze (prima gli eventi meno recenti)** .

## <a name="bkmk_debug"></a> Registri analitici e di debug

È possibile abilitare log più dettagliati a scopo di risoluzione dei problemi. In Visualizzatore eventi andare al menu **Visualizza** e selezionare **Mostra log analitici e di debug**. A questo punto, quando si passa al canale di log, verranno visualizzati due log aggiuntivi: **analitico** e **debug**.

> [!TIP]
> Per impostazione predefinita, questi log hanno le proprietà seguenti:
>
> - **Dimensioni massime log (KB)** : `1028` (1 MB)
> - **Non sovrascrivere eventi (pulizia manuale del registro)**

## <a name="export-logs-to-text"></a>Esporta log in testo

In particolare con i [log analitici e di debug](#bkmk_debug), potrebbe risultare più semplice esaminare le voci di log in un singolo file di testo. Usare i comandi di PowerShell seguenti per esportare le voci del registro eventi in file di testo:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
