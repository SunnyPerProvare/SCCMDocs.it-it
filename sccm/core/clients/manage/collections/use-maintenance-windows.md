---
title: Usare finestre di manutenzione
titleSuffix: Configuration Manager
description: Usare le raccolte e le finestre di manutenzione per gestire in modo efficace i client in System Center Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc4a984b15af66a5426d30f3fb4f0b68c794ba5f
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "65673333"
---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Come usare le finestre di manutenzione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le finestre di manutenzione consentono di definire un periodo di tempo in cui è possibile eseguire le operazioni di Configuration Manager in una raccolta di dispositivi. È possibile usare le finestre di manutenzione per garantire che le modifiche alla configurazione client vengano eseguite quando non influiscono sulla produttività. A partire da Configuration Manager versione 1806, gli utenti possono visualizzare quando verrà eseguita la finestra di manutenzione successiva nella scheda **Stato dell'installazione** nel **Software Center**. <!--1358131-->

 Le finestre di manutenzione sono supportate dalle operazioni seguenti:  

- Distribuzioni software  

- Distribuzioni di aggiornamenti software  

- Distribuzione e valutazione delle impostazioni di conformità  

- Distribuzioni del sistema operativo  

- Distribuzioni di sequenze attività  

  Configurare le finestre di manutenzione con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. La durata massima di una finestra deve essere inferiore a 24 ore. Per impostazione predefinita, i riavvii del computer causati da una distribuzione non sono consentiti al di fuori di una finestra di manutenzione, ma è possibile eseguire l'override di questa impostazione. Le finestre di manutenzione interessano solo il periodo in cui il programma di distribuzione è in esecuzione. Le applicazioni configurate per il download e l'esecuzione in locale possono scaricare contenuto al di fuori della finestra.  

  Se un computer client è membro di una raccolta di dispositivi per la quale è configurata una finestra di manutenzione, il programma di distribuzione viene eseguito solo se il tempo di esecuzione massimo consentito non supera la durata configurata per la finestra. Se non è possibile eseguire il programma, viene generato un avviso e la distribuzione viene eseguita nuovamente durante la finestra di manutenzione pianificata successiva con tempo disponibile.  

## <a name="using-multiple-maintenance-windows"></a>Uso di più finestre di manutenzione  
 Quando un computer client appartiene a più raccolte dispositivi con finestre di manutenzione, vengono applicate queste regole:  

- Se le finestre di manutenzione non si sovrappongono, vengono considerate come due finestre di manutenzione indipendenti.  

- Se le finestre di manutenzione si sovrappongono, vengono considerate come una singola finestra di manutenzione che comprende il periodo di tempo coperto da entrambe le finestre di manutenzione. Se ad esempio due finestre, ognuna della durata di un'ora, si sovrappongono di 30 minuti, la durata effettiva della finestra di manutenzione sarà di 90 minuti.  

  Se un utente avvia l'installazione di un'applicazione da Software Center, l'applicazione viene installata immediatamente, indipendentemente dalle finestre di manutenzione.  

  Se la distribuzione di un'applicazione con scopo **Richiesto** raggiunge la scadenza dell'installazione durante l'orario non lavorativo configurato da un utente in Software Center, l'applicazione verrà installata. 

### <a name="how-to-configure-maintenance-windows"></a>Come configurare le finestre di manutenzione  

1.  Nella console di Configuration Manager scegliere **Asset e conformità**>  **Raccolte dispositivi**.  

3.  Nell'elenco **Raccolte dispositivi** selezionare una raccolta. Non è possibile creare finestre di manutenzione per la raccolta **Tutti i sistemi**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

5.  Nella scheda **Finestre di manutenzione** della finestra di dialogo **Proprietà &lt;nome raccolta\>** scegliere l'icona **Nuovo**.  

6.  Completare la finestra di dialogo **&lt;nuova\> pianificazione**.  

7.  Effettuare una selezione nell'elenco a discesa **Applica pianificazione a**.  

8.  Scegliere **OK** e quindi chiudere la finestra di dialogo **Proprietà &lt;nome raccolta\>** .  
 
## <a name="bkmk_powershell"></a> Uso di PowerShell

È possibile usare PowerShell per configurare le finestre di manutenzione.  Per altre informazioni, vedere:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
