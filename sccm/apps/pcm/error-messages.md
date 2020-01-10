---
title: Messaggi di errore
titleSuffix: Configuration Manager
description: Informazioni sui messaggi di errore di Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1baaf1a57471d52656b1266f4f580cc9003494e8
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75817483"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Informazioni tecniche sui messaggi di errore di Package Conversion Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1357861-->

Questo articolo descrive i messaggi di errore visualizzati da Package Conversion Manager. Sono inclusi anche le possibili cause di ogni errore e i metodi per correggerlo. Package Conversion Manager registra i messaggi di errore in **PCMTrace.log**. Per altre informazioni, incluse le operazioni per controllare il livello di dettaglio, vedere [File di log](/sccm/apps/pcm/troubleshoot-pcm#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>La creazione dell'applicazione non è riuscita e si è verificata l'eccezione seguente

L'eccezione specificata si è verificata durante l'invio dell'oggetto applicazione al server di Configuration Manager.

Controllare le autorizzazioni in Configuration Manager, verificare la connettività e quindi riprovare. Se queste operazioni non consentono di risolvere il problema, esaminare il file **PCMtrace.log** (livello di dettaglio 4) e **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Errore di conversione - SI APPLICA ALLO STATO DI CONVERSIONE DEL PACCHETTO

Si è verificata un'eccezione durante la conversione del pacchetto. Esaminare il file **PCMtrace.log** (livello di dettaglio 4).

Controllare le autorizzazioni utente per la condivisione di rete (origine dati del pacchetto), verificare la connettività e quindi riprovare. Se queste operazioni non consentono di risolvere il problema, esaminare il file **PCMtrace.log** (livello di dettaglio 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Negli output del flusso di lavoro non è stato trovato alcun pacchetto convertito, né la relativa app risultante
L'applicazione (pacchetto/programma convertito) è stata eliminata.

Modificare il programma/pacchetto dipendente per garantire che esista.


#### <a name="objects-were-not-created-successfully"></a>Gli oggetti non sono stati creati
Ci sono diverse cause possibili.

Controllare le autorizzazioni in Configuration Manager, verificare la connettività e quindi riprovare. Se queste operazioni non consentono di risolvere il problema, esaminare il file **PCMtrace.log** (livello di dettaglio 4) e il file **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Chiudere la procedura guidata e risolvere eventuali problemi relativi al pacchetto selezionato. Per altri dettagli, vedere il file PCMTrace.Log
Ci sono diverse cause possibili.

Controllare le autorizzazioni in Configuration Manager, verificare la connettività e quindi riprovare. Se queste operazioni non consentono di risolvere il problema, esaminare il file **PCMtrace.log** (livello di dettaglio 4) e il file **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Alcuni tipi di distribuzione non dispongono dei metodi di rilevamento. I metodi di rilevamento sono obbligatori per tutti i tipi di distribuzione
I metodi di rilevamento non sono presenti nel programma.

Aggiungere uno o più metodi di rilevamento durante la procedura **Correggi e converti**.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Si è verificato un errore durante la preparazione del pacchetto per la conversione
Ci sono diverse cause possibili.

Controllare le autorizzazioni in Configuration Manager, verificare la connettività e quindi riprovare. Se queste operazioni non consentono di risolvere il problema, esaminare il file **PCMtrace.log** (livello di dettaglio 4) e il file **SMSProv.log**.


