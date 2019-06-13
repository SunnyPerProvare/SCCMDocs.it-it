---
title: Come chiudere l'account
titleSuffix: Configuration Manager
description: Come rimuovere Analitica Desktop dall'account di Azure
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 499d24e20b8220e685cb7aed9adea3f21caa12ae
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/13/2019
ms.locfileid: "67039742"
---
# <a name="how-to-close-your-account"></a>Come chiudere l'account

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Se si imposta Analitica Desktop nell'ambiente in uso e quindi si decide di rimuoverlo, usare questo processo per chiudere l'account.

## <a name="contact-support"></a>Contattare il supporto tecnico

Il primo passaggio è necessario contattare il supporto tecnico Microsoft. Aprire un caso di supporto per chiudere l'account Desktop Analitica. Non proseguire con i passaggi aggiuntivi fino a quando non si riceve una conferma che Microsoft chiuso l'account.

## <a name="delete-the-solution"></a>Eliminare la soluzione

1. Accedi per il [portale di Azure](https://portal.azure.com) come utente con il **amministratore società** ruolo.

1. Eseguire la ricerca nella **tutte le risorse** per il nome dell'area di lavoro Desktop Analitica. Questo nome è ciò che è stato creato durante l'iscrizione per il servizio.

1. Eliminare `Microsoft365Analytics(YourWorkspaceName)` typu **soluzione**.

I dati di Analitica Desktop ormai base i criteri di conservazione dei dati per l'area di lavoro. È possibile continuare a usare altre soluzioni nella stessa area di lavoro.

> [!Important]  
> Se si usa l'area di lavoro di Log Analitica con altre soluzioni come Analitica di Windows, non eliminare l'area di lavoro.

## <a name="remove-user-and-app-access"></a>Rimuovere l'accesso utente e app

1. Accedi per il [portale di Azure](https://portal.azure.com) come utente con il **amministratore società** ruolo. Passare a **Azure Active Directory**.

1. Nelle **ruoli e gli amministratori**, cercare il **amministratore Desktop Analitica** ruolo. Rimuovere i relativi membri.

1. Nelle **gruppi**, rimuovere i membri dei gruppi seguenti:

    - **M365 Analitica Client Admins (Log Analitica proprietari)**
    - **M365 Analitica Client Admins (Log Analitica collaboratori)**

1. Nelle **applicazioni aziendali**, eliminare o revocare le autorizzazioni di accesso per le app seguenti:

    - `MaLogAnalyticsReader`

    - L'app di Configuration Manager. Per trovare il nome di questa app, passare alla console di Configuration Manager. Nel **Administration** dell'area di lavoro, espandere **servizi Cloud**e selezionare il **servizi di Azure** nodo. Aprire le proprietà del **Desktop Analitica** del servizio e passare al **applicazioni** scheda. Il **app Web** è questa app di Azure.

        > [!Important]  
        > Prima di apportare modifiche a questa app di Azure AD, assicurarsi che si sta riutilizzare non con un altro servizio in Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Disconnettere Configuration Manager

1. Aprire la console di Configuration Manager come un utente con il **amministratore completo** ruolo.

1. Andare alla **Administration** dell'area di lavoro, espandere **servizi Cloud**e selezionare il **servizi di Azure** nodo.

1. Eliminare il servizio Desktop Analitica.

## <a name="reconfigure-clients"></a>Riconfigurare i client

### <a name="unenroll-devices"></a>Annullare la registrazione di dispositivi

Nei dispositivi registrati, rimuovere il valore CommercialID dalle chiavi del Registro di sistema di Windows seguenti:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configurazione di dati di diagnostica Windows

Se non si vuole ai dispositivi di continuare a inviare dati di diagnostica:

- Windows 10: impostare il livello di dati di diagnostica su **sicurezza**
- Windows 7 SP1 o 8.1: disabilitare il **chiave dei dati commerciali del consenso esplicito**

Impostare questi valori usando uno dei metodi seguenti:

- Criteri di gruppo **configurazione Computer** > **modelli amministrativi** > **i componenti di Windows**  >  **Raccolta dei dati e build di anteprima**
- Gestione dei dispositivi mobili (MDM), ad esempio [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione).

> [!NOTE]  
> Quando si applicano queste modifiche, i dispositivi arrestare immediatamente l'invio di dati di diagnostica. Potrebbero occorrere 24-48 ore interrompere l'elaborazione delle informazioni dettagliate per l'area di lavoro Microsoft. Microsoft Elimina i dati dai servizi cloud entro 30 giorni o meno.
