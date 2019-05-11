---
title: Domande frequenti per l'Analitica Desktop
titleSuffix: Configuration Manager
description: Domande frequenti su Desktop Analitica.
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4596923f9a6a42ad98dc17257b22925ad0bc5eed
ms.sourcegitcommit: 9af73f5c1b93f6ccaea3e6a096f75a5fecd65c2f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2019
ms.locfileid: "64562448"
---
# <a name="desktop-analytics-faq"></a>Domande frequenti di Analitica desktop

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="windows-upgrade"></a>Aggiornamento di Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>È possibile eseguire l'aggiornamento di Windows e modificare l'architettura?

Desktop Analitica è progettato per gli aggiornamenti sul posto del migliori supporto. Gli aggiornamenti sul posto non supportano le migrazioni da architettura a 32 bit a 64 bit. Se è necessario eseguire la migrazione di computer in questo scenario, usare lo scenario di aggiornamento. Insights Analitica desktop sono ancora utili in questo scenario, ma è possibile ignorare le linee guida specifiche di aggiornamento.

Per altre informazioni, vedere [Aggiornare un computer esistente con una nuova versione di Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>È possibile modificare da BIOS a UEFI durante l'aggiornamento di Windows?

Sì. Per altre informazioni, vedere [conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>È possibile usare Analitica Desktop con Windows 10 LTSC?

Sebbene sia possibile usare Desktop Analitica per agevolare l'aggiornamento di dispositivi da Windows 10 Long-Term Servicing Channel (LTSC) su canale semestrale di Windows 10, Analitica Desktop non supporta gli aggiornamenti per Windows 10 LTSC. Questo canale di Windows 10 non è destinato all'uso ampio e non riceve gli aggiornamenti delle funzionalità, pertanto non è una destinazione supportata con Desktop Analitica. Per altre informazioni, vedere [Windows come una panoramica del servizio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

## <a name="privacy"></a>Privacy

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Desktop Analitica può essere usata senza una connessione client diretto al servizio di gestione dati di Microsoft?

No, l'intero servizio si basa su Windows i dati di diagnostica, che richiede che i dispositivi hanno la connettività diretta.

### <a name="can-i-choose-the-data-center-location"></a>È possibile scegliere la posizione del data center?

Per Analitica di Log di Azure: Sì, quando si imposta Desktop Analitica e crea l'area di lavoro di Log Analitica.

Per il servizio di gestione dati Microsoft e Analitica archiviazione di Azure: No, questi due servizi sono ospitati negli Stati Uniti.

### <a name="where-is-my-organizations-data-stored"></a>Dove vengono archiviati i dati dell'organizzazione?

I dati di diagnostica di Windows dai computer vengano crittografati, inviati a ed elaborati con i sicura gestita da Microsoft Data Center situati negli Stati Uniti. L'analisi dei dati correlati Analitica Desktop viene quindi fornito all'utente tramite la soluzione Analitica Desktop nel portale di Azure. Desktop Analitica è supportata in tutte le aree di Azure. Selezione di un'area di Azure internazionale non impedire i dati di diagnostica inviati a ed elaborati nel Data Center di proteggere i dati di Microsoft negli Stati Uniti.
