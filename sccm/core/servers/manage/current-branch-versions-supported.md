---
title: Versioni Current Branch
titleSuffix: Configuration Manager
description: Informazioni sulla cronologia delle versioni di Configuration Manager e sulle fasi del servizio offerto.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35b5baec-d313-46aa-9d14-c443aa0d6c09
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a8f646b1cd535809689daacb1390fd79f8ce5c1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383780"
---
# <a name="support-for-configuration-manager-current-branch-versions"></a>Supporto per le versioni Current Branch di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Microsoft prevede di rilasciare diversi aggiornamenti per le versioni Current Branch di Configuration Manager ogni anno. Per le versioni di Configuration Manager precedenti alla 1710, il supporto è per 12 mesi. A partire dalla versione 1710, ogni versione di aggiornamento continua a essere supportata per 18 mesi dalla data in cui viene resa disponibile a livello generale. Microsoft fornisce il supporto tecnico per l'intero periodo. Ci sono due fasi di manutenzione distinte che dipendono dalla disponibilità della versione Current Branch più recente.  

-   Fase di manutenzione **Aggiornamenti di sicurezza e critici**: quando si esegue la versione Current Branch più recente di Configuration Manager si ricevono sia gli aggiornamenti critici che gli aggiornamenti di sicurezza.  

-   Fase di manutenzione **Aggiornamenti della sicurezza (solo)**: quando viene resa disponibile una nuova versione Current Branch, Microsoft supporta solo gli aggiornamenti della sicurezza per le versioni precedenti per il ciclo di vita di supporto rimanente per tali versioni (mostrato nella figura 1).  

 ![Immagine della sequenza temporale per la manutenzione e il supporto di Configuration Manager](media/CM_Servicing_support_timeline1.png)  
Figura 1. Esempio di sovrapposizione del ciclo di rilascio per il supporto della manutenzione della versione Current Branch. Questo esempio ha il solo scopo di illustrare il ciclo e non rappresenta le date di rilascio effettive o previste.

> [!NOTE]  
>  La versione Current Branch più recente è sempre nella fase di manutenzione **Aggiornamenti di sicurezza e critici**. Questo significa che, nel caso in cui venga rilevato un errore del codice che richiede un aggiornamento critico, è necessario che sia installata la versione Current Branch più recente per ricevere una correzione. Tutte le altre versioni Current Branch supportate sono idonee a ricevere gli aggiornamenti della sicurezza.
> - Per le versioni 1710 e successive, il supporto termina completamente allo scadere del ciclo di vita di 18 mesi della versione Current Branch corrente.
> - Per le versioni precedenti alla 1710, il supporto termina allo scadere del ciclo di vita di 12 mesi.

> Aggiornare l'ambiente di Configuration Manager alla versione più recente prima della scadenza del supporto per la versione corrente.

Per un elenco di versioni Current Branch, vedere [Dettagli sulla versione](/sccm/core/servers/manage/updates#version-details).

Per altre informazioni sui numeri di versione e sulla disponibilità come aggiornamento nella console o versione di base, vedere [Versioni di base e di aggiornamento](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).
