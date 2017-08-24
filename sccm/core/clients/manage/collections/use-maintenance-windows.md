---
title: Usare le finestre di manutenzione | Microsoft Docs
description: Usare le raccolte e le finestre di manutenzione per gestire in modo efficace i client in System Center Configuration Manager.
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fa67cf597c73bab47209c9b98539f97e174ae70b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Come usare le finestre di manutenzione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le finestre di manutenzione consentono di definire un periodo di tempo in cui è possibile eseguire le operazioni di Configuration Manager in una raccolta di dispositivi. È possibile usare le finestre di manutenzione per garantire che le modifiche alla configurazione client vengano eseguite quando non influiscono sulla produttività.  

 Le finestre di manutenzione sono supportate dalle operazioni seguenti:  

-   Distribuzioni software  

-   Distribuzioni di aggiornamenti software  

-   Distribuzione e valutazione delle impostazioni di conformità  

-   Distribuzioni del sistema operativo  

-   Distribuzioni di sequenze attività  

 Configurare le finestre di manutenzione con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. La durata massima di una finestra deve essere inferiore a 24 ore. Per impostazione predefinita, i riavvii del computer causati da una distribuzione non sono consentiti al di fuori di una finestra di manutenzione, ma è possibile sostituire questa impostazione. Le finestre di manutenzione interessano solo il periodo in cui il programma di distribuzione è in esecuzione. Le applicazioni configurate per il download e l'esecuzione in locale possono scaricare contenuto al di fuori della finestra.  

 Se un computer client è membro di una raccolta di dispositivi per la quale è configurata una finestra di manutenzione, il programma di distribuzione viene eseguito solo se il tempo di esecuzione massimo consentito non supera la durata configurata per la finestra. Se non è possibile eseguire il programma, viene generato un avviso e la distribuzione viene eseguita nuovamente durante la finestra di manutenzione pianificata successiva con tempo disponibile.  

## <a name="using-multiple-maintenance-windows"></a>Uso di più finestre di manutenzione  
 Quando un computer client appartiene a più raccolte dispositivi con finestre di manutenzione, vengono applicate queste regole:  

-   Se le finestre di manutenzione non si sovrappongono, vengono considerate come due finestre di manutenzione indipendenti.  

-   Se le finestre di manutenzione si sovrappongono, vengono considerate come una singola finestra di manutenzione che comprende il periodo di tempo coperto da entrambe le finestre di manutenzione. Se ad esempio due finestre, ognuna della durata di un'ora, si sovrappongono di 30 minuti, la durata effettiva della finestra di manutenzione sarà di 90 minuti.  

 Se un utente avvia l'installazione di un'applicazione da Software Center, l'applicazione viene installata immediatamente, indipendentemente dalle finestre di manutenzione.  

 Se la distribuzione di un'applicazione con scopo **Richiesto** raggiunge la scadenza dell'installazione durante l'orario non lavorativo configurato da un utente in Software Center, l'applicazione verrà installata.  

### <a name="how-to-configure-maintenance-windows"></a>Come configurare le finestre di manutenzione  

1.  Nella console di Configuration Manager scegliere **Asset e conformità**>  **Raccolte dispositivi**.  

3.  Nell'elenco **Raccolte dispositivi** selezionare una raccolta. È impossibile creare finestre di manutenzione per la raccolta **Tutti i sistemi** .  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella scheda **Finestre di manutenzione** della finestra di dialogo **Proprietà &lt;nome raccolta\>** scegliere l'icona **Nuovo**.  

6.  Completare la finestra di dialogo **&lt;nuova\> pianificazione**.  

7.  Effettuare una selezione nell'elenco a discesa **Applica pianificazione a**.  

8.  Scegliere **OK** e quindi chiudere la finestra di dialogo **Proprietà &lt;nome raccolta\>**.  
