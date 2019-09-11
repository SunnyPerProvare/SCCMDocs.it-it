---
title: Come chiudere l'account
titleSuffix: Configuration Manager
description: Come rimuovere Desktop Analytics dall'account Azure
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 387d16b75c688640eba0ed6658b281badd3c7c54
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891743"
---
# <a name="how-to-close-your-account"></a>Come chiudere l'account

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Se si configura desktop Analytics nell'ambiente in uso e quindi si decide di rimuoverlo, usare questo processo per chiudere l'account.

## <a name="prerequisites"></a>Prerequisiti

Solo un **amministratore globale** può chiudere o riattivare l'account nell'portale di Azure.

## <a name="process-to-offboard"></a>Elabora in offboard

1. Aprire il [portale di analisi del desktop](https://aka.ms/desktopanalytics) in Microsoft 365 gestione dei dispositivi come utente con il ruolo di **amministratore globale** .

1. Nel menu **Impostazioni globali** selezionare **servizi connessi**. Nella sezione registrazione dei dispositivi selezionare l'opzione **offboard**.

1. Se si decide di continuare, l'account viene chiuso.

> [!Important]
> Continuare con il resto di questo articolo dopo 90 giorni, oppure se non si riattivano.
>
> Se si vuole chiudere completamente l'account senza attendere 90 giorni, è necessario innanzitutto [reimpostare](/sccm/desktop-analytics/account-reset) l'account.

## <a name="reactivate"></a>Riattivare

Per i prossimi 90 giorni, tutti gli amministratori dell'organizzazione che accedono al portale di analisi desktop visualizzeranno un avviso che si è scelto di offboard.

Un amministratore globale può riattivare l'account entro 90 giorni. Per ripristinare desktop Analytics per l'organizzazione, selezionare l'opzione che consente di **tornare indietro**.

## <a name="delete-the-solution"></a>Eliminare la soluzione

> [!Warning]
> Continuare con il resto di questo articolo dopo 90 giorni, oppure se non si riattivano. Se si eliminano e disconnettono questi componenti, non provare a riattivare.

1. Accedere al [portale di Azure](https://portal.azure.com) come utente con il ruolo di **amministratore globale** .

1. Cercare in **tutte le risorse** il nome dell'area di lavoro di analisi del desktop. Questo nome è quello creato durante l'iscrizione al servizio.

1. Eliminazione `Microsoft365Analytics(YourWorkspaceName)` della **soluzione**del tipo.

I dati di analisi desktop sono obsoleti in base ai criteri di conservazione dei dati per l'area di lavoro. È possibile continuare a usare qualsiasi altra soluzione nella stessa area di lavoro.

> [!Important]  
> Se si usa l'area di lavoro Log Analytics con altre soluzioni come Windows Analytics, non eliminare l'area di lavoro.

## <a name="remove-user-and-app-access"></a>Rimuovere l'accesso dell'utente e dell'app

1. Accedere al [portale di Azure](https://portal.azure.com) come utente con il ruolo di **amministratore globale** . Passare a **Azure Active Directory**.

1. In **ruoli e amministratori**cercare il ruolo di **amministratore di Analytics per desktop** . Rimuovere i relativi membri.

1. In **gruppi**rimuovere i membri dei gruppi seguenti:

    - **Amministratori client di M365 Analytics (proprietari Log Analytics)**
    - **Amministratori client di M365 Analytics (collaboratori Log Analytics)**

1. In **applicazioni aziendali**, eliminare o revocare le autorizzazioni di accesso per le app seguenti:

    - `MaLogAnalyticsReader`

    - App ConfigMgr. Per trovare il nome dell'app, passare alla console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **servizi cloud**e selezionare il nodo **servizi di Azure** . Aprire le proprietà del servizio **Desktop Analytics** e passare alla scheda **applicazioni** . L' **app Web** è questa app Azure.

        > [!Important]  
        > Prima di apportare modifiche all'app in Azure AD, assicurarsi che non venga riutilizzata con un altro servizio in Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Disconnetti Configuration Manager

1. Aprire la console di Configuration Manager come utente con il ruolo di **amministratore completo** .

1. Passare all'area di lavoro **Amministrazione** , espandere **servizi cloud**e selezionare il nodo **servizi di Azure** .

1. Eliminare il servizio desktop Analytics.

## <a name="reconfigure-clients"></a>Riconfigurare i client

### <a name="unenroll-devices"></a>Annulla la registrazione dei dispositivi

Nei dispositivi registrati rimuovere il valore commercializzato dalle seguenti chiavi del registro di sistema di Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configurazione dei dati di diagnostica di Windows

Se non si vuole che i dispositivi continuino a inviare i dati di diagnostica:

- Windows 10: impostare il livello di dati di diagnostica su **sicurezza**
- Windows 7 SP1 o 8,1: disabilitare la **chiave di consenso esplicito per i dati commerciali**

Impostare questi valori utilizzando uno dei metodi seguenti:

- Criteri di gruppo, in **configurazione** > computer**modelli amministrativi** > **componenti** > di Windows**raccolta dati e compilazioni anteprima**
- Gestione di dispositivi mobili (MDM), ad esempio [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione).

> [!NOTE]  
> Quando si applicano queste modifiche, i dispositivi interrompono immediatamente l'invio dei dati di diagnostica. Potrebbero essere necessarie 24-48 ore per arrestare l'elaborazione di informazioni dettagliate per l'area di lavoro. Microsoft Elimina i dati dai servizi cloud entro 30 giorni o meno.
