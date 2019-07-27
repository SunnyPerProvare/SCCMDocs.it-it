---
title: Agente di raccolta log
titleSuffix: Configuration Manager
description: Usare lo strumento Log Collector per risolvere i problemi di analisi del desktop
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e99899ba9b12416e9549f88c7bc3b72fc09c6c28
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537639"
---
# <a name="desktop-analytics-log-collector"></a>Agente di raccolta log di analisi desktop

A partire da Configuration Manager versione 1906, usare lo strumento **DesktopAnalyticsLogsCollector. ps1** dalla directory di installazione Configuration Manager per risolvere i problemi di registrazione del dispositivo di analisi del desktop. Esegue alcuni passaggi di base per la risoluzione dei problemi e raccoglie i log rilevanti in un'unica directory di lavoro. È possibile condividere questo contenuto con il supporto tecnico Microsoft.


## <a name="prerequisites"></a>Prerequisiti

- Un client di analisi desktop che esegue Windows 10, Windows 8.1 o Windows 7 con Service Pack 1

- Eseguire lo script nel dispositivo come utente **amministratore ed eseguire come amministratore**.

    > [!Tip]
    > Con questo strumento è possibile utilizzare la funzionalità **script** Configuration Manager. Per ulteriori informazioni, vedere [l'esempio 5: Distribuire lo script tramite **script**](#bkmk_ex5)Configuration Manager.

- PowerShell versione 4,0 o successiva
    - .NET Framework versione 4,6 o successiva
    - Windows Management Framework versione 4,0 o successiva

## <a name="usage"></a>Utilizzo

Ottenere lo script dal contenuto del Configuration Manager installazione:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

```
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parametri

### `-LogPath`

Specifica un percorso locale o UNC per inserire il log e altri file di output.

**Valori**:

- Percorso locale (lunghezza massima = 130), ad esempio:`c:\myfolder`

- Percorso UNC (lunghezza massima = 130), ad esempio:`\\myserver\myfolder`

**Tipo**: String

**Posizione**: 1

**Valore predefinito**: `$Env:SystemDrive\M365AnalyticsLogs`Se questo parametro è null, vuoto o uno spazio vuoto, lo script crea la cartella M365AnalyticsLogs nell'unità di sistema.

### `-LogMode`

Specifica il livello dettagliato dei log.

**Valori**:

- `0`: Registra i messaggi di script nella finestra di comando di PowerShell.

- `1`: Registrare i messaggi di script in entrambi i file di log nella cartella di output e nella finestra di comando di PowerShell.

- `2`: Registra i messaggi di script nel file di log solo nella cartella di output.

**Tipo**: Int16

**Posizione**: 2

**Valore predefinito**: `1`(Registrare i messaggi di script nel file di log e nella finestra di comando di PowerShell).

### `-CollectNetTrace`

Specifica se lo script raccoglie la traccia di rete.

**Valori**:

- `0`: Non abilitare la traccia di rete.

- `1`(qualsiasi valore integer diverso da zero): Abilitare la traccia di rete e raccogliere i risultati.

**Tipo**: Int16

**Posizione**: 3

**Valore predefinito**: `0`(Non abilitare la traccia di rete)

### `-CollectUTCTrace`

Specifica se lo script raccoglie la traccia UTC di Windows ed esegue la diagnosi di connettività.

**Valori**:

- `0`: Non abilitare la traccia UTC o eseguire la diagnosi di connettività.

- `1`(qualsiasi valore integer diverso da zero): Abilitare la traccia UTC, eseguire la diagnostica della connettività e raccogliere i risultati.

**Tipo**: Int16

**Posizione**: 4

**Valore predefinito**: `0`(Non abilitare la traccia UTC o eseguire la diagnosi di connettività)


## <a name="output"></a>Output

Lo script crea una *cartella di lavoro* nel percorso specificato. Ad esempio, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Inserisce tutti i file di output in questa cartella di lavoro.

Se si Abilita lo script per la scrittura in un *file di log*, ne viene generato uno nella cartella di lavoro. Ad esempio, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

Lo script genera anche altri *file di diagnostica* nella cartella di lavoro. Ad esempio:

- `installedKBs.txt`: elenco di aggiornamenti di Windows installati nel dispositivo
- `appcompat`: dati di compatibilità delle applicazioni
- `Reg*.txt`: una serie di file con i dati esportati dal registro di sistema di Windows


## <a name="examples"></a>Esempi

### <a name="bkmk_ex1"></a>Esempio 1: Eseguire lo script tramite la finestra di comando di PowerShell con i valori predefiniti

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="bkmk_ex2"></a>Esempio 2: Eseguire lo script tramite la finestra di comando di PowerShell con i parametri specificati

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="bkmk_ex3"></a>Esempio 3: Esegui script tramite la finestra di comando di PowerShell con i parametri specificati nella posizione

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="bkmk_ex4"></a>Esempio 4: Esegui script tramite la finestra di comando di PowerShell con i parametri specificati e i messaggi dettagliati

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="bkmk_ex5"></a>Esempio 5: Distribuire lo script tramite **script** Configuration Manager

Per altre informazioni, vedere [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

DesktopAnalyticsLogsCollector. ps1 è firmato digitalmente da Microsoft. Potrebbe essere necessario aggiungere il certificato di firma codice Microsoft come autore attendibile nel dispositivo di destinazione.

1. Aprire le proprietà dello script in Esplora risorse. Passare alla scheda **firme digitali** e selezionare **Dettagli**.

1. Nella scheda **generale** selezionare **Visualizza certificato**.

    > [!Note]
    > Per distribuire il certificato tramite altri meccanismi, esportare prima il certificato in un file. Passare alla scheda **Dettagli** e selezionare **copia su file**.

1. Selezionare **Installa certificato**. Importare il certificato, inserendolo nell'archivio **autori attendibili** .


## <a name="see-also"></a>Vedere anche

- [Risolvere i problemi di Desktop Analytics](/sccm/desktop-analytics/troubleshooting)

- [Creare ed eseguire script di PowerShell dalla console di Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts)
