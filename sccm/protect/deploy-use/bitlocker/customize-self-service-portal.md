---
title: Personalizzare il portale self-service
titleSuffix: Configuration Manager
description: Aggiungere informazioni personalizzate specifiche dell'organizzazione al portale self-service per la gestione di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 6bc26e36-9914-4606-ae8d-f7b23218942f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c35641e809092b832a081dbcba6ad7b5006beb70
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662409"
---
# <a name="customize-the-self-service-portal"></a>Personalizzare il portale self-service

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Dopo aver [installato il portale self-service di BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites), è possibile personalizzarlo per l'organizzazione. Aggiungere un avviso personalizzato, il nome dell'organizzazione e altre informazioni specifiche dell'organizzazione.

## <a name="branding"></a>Personalizzazione

Personalizzare il portale self-service con il nome dell'organizzazione, l'URL help desk e il testo di avviso.

1. Accedere come amministratore nel server Web che ospita il portale self-service.

1. Avviare **gestione Internet Information Services (IIS)** (eseguire **inetmgr. exe**).

1. Espandere **siti**, **sito Web predefinito**e selezionare il nodo **selfservice** . Nel riquadro dei dettagli, **ASP.NET** gruppo, aprire **Impostazioni applicazione**.

    [schermata di esempio ![delle impostazioni dell'applicazione SelfService in Gestione IIS](media/bitlocker-self-service-iis-app-settings.png)](media/bitlocker-self-service-iis-app-settings.png#lightbox)

1. Selezionare l'elemento che si desidera modificare e fare clic su **modifica**nel riquadro **azioni** . Modificare il **valore** con il nuovo nome che si desidera utilizzare.

    > [!CAUTION]
    > Non modificare i valori del **nome** . Ad esempio, non modificare `CompanyName`, modificare `Contoso IT`. Se si modificano i valori del **nome** , il portale self-service smette di funzionare.

Le modifiche hanno effetto immediato.

### <a name="supported-branding-values"></a>Valori di personalizzazione supportati

Per i valori che è possibile impostare, vedere la tabella seguente:

|Name|Descrizione|Valore&nbsp;predefinito|
|--- |--- |--- |
|CompanyName|Il nome dell'organizzazione visualizzato nel portale self-service come intestazione nella parte superiore di ogni pagina.|`Contoso IT`|
|DisplayNotice|Visualizza una notifica iniziale che l'utente deve confermare.|`true`|
|HelpdeskText|Stringa nel riquadro destro sotto "per tutti gli altri problemi correlati"|`Contact Helpdesk or IT Department`|
|HelpdeskUrl|Collegamento per la stringa HelpdeskText.|(vuoto)|
|NoticeTextPath|Testo dell'avviso iniziale che l'utente deve riconoscere. Per impostazione predefinita, il percorso completo del file nel server Web è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`. Modificare e salvare il file in un editor di testo normale. Il valore di questo percorso è relativo all'applicazione SelfService.|`Notice.txt`|

<!-- Not sure if we support changing these values. At a minimum need a description.
|ClientValidationEnabled||`true`|
|UnobtrusiveJavaScriptEnabled||`true`|
-->

Per una schermata del portale Self-Service predefinito, vedere il [portale self-service BitLocker](/configmgr/protect/deploy-use/bitlocker/self-service-portal).

> [!TIP]
> Se necessario, è possibile localizzare alcune di queste stringhe per la visualizzazione in lingue diverse. Per altre informazioni, vedere [Localizzazione](#bkmk_localize).

## <a name="session-time-out"></a>Timeout sessione

Per far scadere la sessione dell'utente dopo un periodo di inattività specificato, è possibile modificare l'impostazione di timeout della sessione per il portale self-service.

1. Accedere come amministratore nel server Web che ospita il portale self-service.

1. Avviare **gestione Internet Information Services (IIS)** (eseguire **inetmgr. exe**).

1. Espandere **siti**, **sito Web predefinito**e selezionare il nodo **selfservice** . Nel riquadro dei dettagli, **ASP.NET** gruppo, aprire **stato sessione**.

1. Nel gruppo **Impostazioni cookie** , modificare il valore **di timeout (in minuti)** . Il numero di minuti trascorsi i quali la sessione dell'utente scade. Il valore predefinito è `5`. Per disabilitare questa impostazione in modo da disattivare il timeout, impostare il valore su `0`.

1. Nel riquadro **azioni** selezionare **applica**.

## <a name="bkmk_localize"></a>Localizzare il testo e l'URL del supporto tecnico

È possibile configurare le versioni localizzate del portale self-service `HelpdeskText` istruzione e `HelpdeskUrl` collegamento. Questa stringa informa gli utenti su come ottenere ulteriore assistenza durante l'uso del portale. Se si configura il testo localizzato, nel portale viene visualizzata la versione localizzata per i Web browser in tale lingua. Se non trova una versione localizzata, visualizzerà il valore predefinito nelle impostazioni `HelpdeskText` e `HelpdeskUrl`.

1. Accedere come amministratore nel server Web che ospita il portale self-service.

1. Avviare **gestione Internet Information Services (IIS)** (eseguire **inetmgr. exe**).

1. Espandere **siti**, **sito Web predefinito**e selezionare il nodo **selfservice** . Nel riquadro dei dettagli, **ASP.NET** gruppo, aprire **Impostazioni applicazione**.

1. Nel riquadro **azioni** selezionare **Aggiungi**.

1. Nella finestra **Aggiungi impostazione applicazione** configurare i valori seguenti:

    - **Nome**: immettere `HelpdeskText_<language>`, dove `<language>` è il codice della lingua per il testo.

      Per creare, ad esempio, un'istruzione `HelpdeskText` localizzata in spagnolo (Spagna), il nome è `HelpdeskText_es-es`.

    - **Valore**: la stringa localizzata da visualizzare nel riquadro destro del portale self-service di seguito "per tutti gli altri problemi correlati"

1. Selezionare **OK** per salvare la nuova impostazione.

1. Ripetere questo processo per aggiungere una nuova impostazione di applicazione per `HelpdeskUrl_<language>` corrispondente all'impostazione `HelpdeskText_<language>` associata.

Ripetere questa procedura per aggiungere una coppia di impostazioni per tutti i linguaggi supportati nell'organizzazione.

## <a name="localize-the-notice-file"></a>Localizzare il file di avviso

È possibile configurare le versioni localizzate dell'avviso iniziale che l'utente deve confermare nel portale self-service. Per impostazione predefinita, il percorso completo del file nel server Web è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\Notice.txt`.

Per visualizzare il testo di avviso localizzato, creare un file notice. txt localizzato. Quindi salvarlo in una cartella specifica della lingua. Ad esempio: `Self Service Website\es-es\Notice.txt` per lo spagnolo (Spagna).

Il portale self-service Visualizza il testo di avviso in base alle regole seguenti:

- Se il file di avviso predefinito non è presente, nel portale viene visualizzato un messaggio che indica che il file predefinito è mancante.

- Se si crea un file di avviso localizzato nella cartella della lingua appropriata, viene visualizzato il testo di avviso localizzato.

- Se il server Web non trova una versione localizzata del file di avviso, viene visualizzato l'avviso predefinito.

- Se l'utente imposta il browser su una lingua che non dispone di un avviso localizzato, il portale Visualizza l'avviso predefinito.

### <a name="create-a-localized-notice-file"></a>Creazione di un file di avviso localizzato

1. Accedere come amministratore nel server Web che ospita il portale self-service.

1. Creare una cartella `<language>` per ogni lingua supportata nel percorso dell'applicazione `Self Service Website`. Ad esempio, `es-es` per lo spagnolo (Spagna). Per impostazione predefinita, il percorso completo è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es`.

    Per un elenco dei codici lingua validi che è possibile usare, vedere [National Language Support (NLS) API Reference](https://docs.microsoft.com/windows/win32/intl/locale-identifiers#predefined-locale-identifiers) (Riferimento API NLS).

    > [!TIP]
    > Il nome della cartella della lingua può essere anche il nome indipendente dalla lingua. Ad esempio, **es** per spagnolo, anziché **es-es** per spagnolo (Spagna) ed **es-AR** per spagnolo (Argentina). Se l'utente imposta il browser su **es-es**e la cartella della lingua non esiste, il server Web controlla in modo ricorsivo la cartella delle impostazioni locali padre (**es**). Le impostazioni locali padre sono definite in .NET. `Self Service Website\es\Notice.txt` Ad esempio: Questo fallback ricorsivo simula le regole di caricamento delle risorse .NET.

1. Creare una copia del file di avviso predefinito con il testo localizzato. Salvarlo nella cartella per il codice della lingua. Ad esempio, per lo spagnolo (Spagna), per impostazione predefinita il percorso completo è `C:\inetpub\Microsoft BitLocker Management Solution\Self Service Website\es-es\Notice.txt`.

Ripetere questo processo in un file di avviso localizzato per tutte le lingue supportate nell'organizzazione.

## <a name="next-steps"></a>Passaggi successivi

Ora che è stato installato e personalizzato il portale self-service, provare a usarlo. Per ulteriori informazioni, vedere il [portale self-service BitLocker](/configmgr/protect/deploy-use/bitlocker/self-service-portal).
