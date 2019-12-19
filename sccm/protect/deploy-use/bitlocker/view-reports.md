---
title: Visualizzare i report di BitLocker
titleSuffix: Configuration Manager
description: Informazioni sui report di gestione di BitLocker in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 177d5f025690b64581873023d4db02a414d88531
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662519"
---
# <a name="view-bitlocker-reports"></a>Visualizzare i report di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Dopo aver [installato i report](/configmgr/protect/deploy-use/bitlocker/setup-websites) nel punto di Reporting Services, è possibile visualizzare i report. I report mostrano la conformità a BitLocker per l'organizzazione e per i singoli dispositivi. Forniscono informazioni in tabelle e grafici e possono essere filtrati per visualizzare i dati da prospettive diverse.

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e selezionare il nodo **Report**. I report seguenti sono inclusi nella categoria **Gestione BitLocker** :

- [Conformità computer BitLocker](#bkmk-compliancereport)

- [Dashboard Conformità aziendale con BitLocker](#bkmk-dashboard)

- [Dettagli della conformità aziendale con Bitlocker](#bkmk-compliancedetails)

- [Riepilogo della conformità aziendale con Bitlocker](#bkmk-compliancesummary)

- [Report Controllo del ripristino](#bkmk-audit)

È possibile accedere a tutti i report direttamente dal sito Web del punto di Reporting Services.

> [!NOTE]
> Per visualizzare i dati completi nei report:
>
> - Creare e distribuire un criterio di gestione di BitLocker in una raccolta di dispositivi
> - I client nella raccolta di destinazione devono inviare l'inventario hardware

## <a name="bkmk-compliancereport"></a> Conformità computer BitLocker

Usare questo report per raccogliere informazioni specifiche su un computer. Fornisce informazioni dettagliate sulla crittografia sull'unità del sistema operativo e sulle unità dati fisse. Per visualizzare i dettagli di ogni unità, espandere la voce Nome computer. Indica anche i criteri applicati a ogni tipo di unità nel computer.

[![schermata di esempio di report conformità computer BitLocker](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

È inoltre possibile utilizzare questo report per determinare l'ultimo stato noto di crittografia BitLocker dei computer smarriti o rubati. Configuration Manager determina la conformità del dispositivo in base ai criteri di BitLocker distribuiti. Prima di provare a determinare lo stato di crittografia BitLocker di un dispositivo, verificare i criteri che sono stati distribuiti.

> [!NOTE]
> Questo report non Mostra lo stato di crittografia dei volumi di dati rimovibili.

### <a name="computer-details"></a>Dettagli computer

|Nome&nbsp;colonna|Descrizione|
|----------------|----|
|Nome computer|Nome computer DNS specificato dall'utente.|
|Nome di dominio|Nome di dominio completo del computer.|
|Tipo computer|Tipo di computer. i tipi validi sono **non** portabili e **portatili**.|
|Sistema operativo|Tipo di sistema operativo del computer.|
|Conformità generale|Stato di conformità generale di BitLocker del computer. Gli stati validi sono **Conforme** e **Non conforme**. Lo [stato di conformità per unità](#bkmk_volume) può indicare diversi Stati di conformità. Tuttavia, questo campo rappresenta lo stato di conformità secondo i criteri specificati.|
|Conformità del sistema operativo|Stato di conformità del sistema operativo nel computer. Gli stati validi sono **Conforme** e **Non conforme**.|
|Conformità delle unità dati fisse|Stato di conformità di un'unità dati fissa nel computer. Gli stati validi sono **Conforme** e **Non conforme**.|
|Data ultimo aggiornamento|Data e ora dell'ultimo contatto del computer con il server per segnalare lo stato di conformità.|
|Esenzione|Indica se l'utente è o meno esente dai criteri di BitLocker.|
|Utente esentato|Utente esentato dai criteri BitLocker.|
|Data esenzione|Data in cui è stata concessa l'esenzione.|
|Dettagli dello stato di conformità|Messaggi di errore e di stato sullo stato di conformità del computer in base ai criteri specificati.|
|Criterio: Livello di codifica|Livello di codifica selezionato nei criteri di gestione di BitLocker.|
|Criterio: Unità del sistema operativo|Indica se la crittografia è necessaria per l'unità del sistema operativo e viene visualizzato il tipo di protezione appropriato.|
|Criterio: Unità dati fissa|Indica se la crittografia è necessaria per l'unità dati fissa.|
|Produttore|Nome del produttore del computer così come appare nel BIOS del computer.|
|Modello|Nome del modello del produttore del computer così come appare nel BIOS del computer.|
|Utenti del dispositivo|Utenti noti del computer.|

### <a name="bkmk_volume"></a>Volume computer

|Nome&nbsp;colonna|Descrizione|
|----------------|----|
|Lettera unità|Lettera di unità nel computer.|
|Tipo di unità|Tipo di unità. I valori validi sono **Unità del sistema operativo** e **Unità dati fissa**. Queste voci sono unità fisiche piuttosto che volumi logici.|
|Livello di codifica|Livello di codifica selezionato durante i criteri di gestione di BitLocker.|
|Tipi di protezione|Tipo di protezione selezionato nei criteri per crittografare l'unità. I tipi di protezione validi per un'unità del sistema operativo sono **TPM** o **TPM + PIN**. Il tipo di protezione valido per un'unità dati fissa è **Password**.|
|Stato della protezione|Indica che il computer ha abilitato il tipo di protezione specificato nei criteri. Gli stati validi sono **Attivato** o **Disattivato**.|
|Stato della crittografia|Stato di crittografia dell'unità. Gli stati validi sono **Crittografato**, **Nessuna crittografia** e **Crittografia in corso**.|

## <a name="bkmk-dashboard"></a> Dashboard Conformità aziendale con BitLocker

Questo report include i grafici seguenti, che mostrano lo stato di conformità di BitLocker nell'organizzazione:

- Distribuzione dello stato di conformità

- Non conforme - Distribuzione degli errori

- Distribuzione dello stato di conformità per tipo di unità

[![schermata di esempio di dashboard conformità organizzazione BitLocker](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Distribuzione dello stato di conformità

Questo grafico a torta mostra lo stato di conformità per i computer dell'organizzazione. Viene anche mostrata la percentuale di computer con tale stato di conformità rispetto al numero totale di computer presenti nella raccolta selezionata. Viene anche visualizzato il numero effettivo di computer con ogni stato.

Il grafico a torta mostra i seguenti stati di conformità:

- conformi

- Non conformi

- Utente esente

- Utente temporaneo esente

- Non sono stati applicati criteri

- Sconosciuto. Per questi computer è segnalato uno errore di stato oppure fanno parte della raccolta ma non ne è mai stato segnalato lo stato di conformità. La mancanza di uno stato di conformità può verificarsi se il computer è disconnesso dall'organizzazione.

### <a name="non-compliant---errors-distribution"></a>Non conforme - Distribuzione degli errori

In questo grafico a torta vengono visualizzate le categorie di computer dell'organizzazione che non sono conformi ai criteri di Crittografia unità BitLocker. Mostra anche il numero di computer in ogni categoria. Il report calcola ogni percentuale rispetto al numero totale di computer non conformi nella raccolta.

- L'utente ha posticipato la crittografia

- Non è possibile trovare TPM compatibile

- La partizione di sistema non è disponibile o non è sufficientemente grande

- TPM visibile ma non inizializzato

- Conflitto tra criteri

- In attesa del provisioning automatico di TPM

- Si è verificato un errore sconosciuto

- Nessuna informazione. In questi computer non è installato l'agente di Gestione BitLocker oppure è installato ma non attivato. Il servizio, ad esempio, non funziona.

### <a name="compliance-status-distribution-by-drive-type"></a>Distribuzione dello stato di conformità per tipo di unità

Nel grafico a barre viene visualizzato lo stato corrente di conformità BitLocker in base al tipo di unità. Gli stati sono **Conforme** e **Non conforme**. Vengono visualizzate le barre per le unità dati fisse e le unità del sistema operativo. Il report include i computer senza un'unità dati fissa e Mostra solo un valore nella barra dell' **unità del sistema operativo** . Il grafico non include gli utenti a cui è stata concessa un'esenzione dai criteri di Crittografia unità BitLocker o attribuita la categoria Nessun criterio.

## <a name="bkmk-compliancedetails"></a> Dettagli della conformità aziendale con BitLocker

Questo report Mostra informazioni sulla conformità BitLocker complessiva all'interno dell'organizzazione per la raccolta di computer in cui sono stati distribuiti i criteri di gestione di BitLocker.

[![schermata di esempio di dettagli conformità organizzazione BitLocker](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Nome della colonna|Descrizione|
|--- |--- |
|Computer gestiti|Numero di computer in cui sono stati distribuiti i criteri di gestione di BitLocker.|
|Percentuale conformità|Percentuale di computer conformi all'interno dell'organizzazione.|
|Percentuale non conformità|Percentuale di computer non conformi all'interno dell'organizzazione.|
|% conformità sconosciuta|Percentuale di computer il cui stato di conformità non è noto.|
|% con esenzione|Percentuale di computer esenti dal requisito di crittografia BitLocker.|
|% non esente|Percentuale di computer non esenti dal requisito di crittografia BitLocker.|
|conformi|Conteggio dei computer conformi nell'organizzazione.|
|Non conforme|Numero di computer non conformi nell'organizzazione.|
|Conformità sconosciuta|Conteggio dei computer con uno stato di conformità non noto.|
|Esente|Numero di computer esenti dal requisito di crittografia BitLocker.|
|Non esente|Numero di computer non esenti dal requisito di crittografia BitLocker.|

### <a name="computer-details"></a>Dettagli computer

|Nome della colonna|Descrizione|
|--- |--- |
|Nome computer|Nome del computer DNS del dispositivo gestito.|
|Nome di dominio|Nome di dominio completo del computer.|
|Stato di conformità|Stato di conformità complessivo del computer. Gli stati validi sono **Conforme** e **Non conforme**.|
|Esenzione|Indica se l'utente è o meno esente dai criteri di BitLocker.|
|Utenti del dispositivo|Utenti del dispositivo.|
|Dettagli dello stato di conformità|Messaggi di errore e di stato sullo stato di conformità del computer in base ai criteri specificati.|
|Ultimo contatto|Data e ora dell'ultimo contatto del computer con il server per segnalare lo stato di conformità.|

## <a name="bkmk-compliancesummary"></a> Riepilogo della conformità aziendale con BitLocker

Utilizzare questo report per mostrare la conformità generale di BitLocker nell'organizzazione. Viene inoltre illustrata la conformità per i singoli computer in cui sono stati distribuiti i criteri di gestione di BitLocker.

[![schermata di esempio di riepilogo conformità organizzazione BitLocker](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Nome della colonna|Descrizione|
|--- |--- |
|Computer gestiti|Numero di computer gestiti con i criteri di BitLocker.|
|Percentuale conformità|Percentuale di computer conformi nell'organizzazione.|
|Percentuale non conformità|Percentuale di computer non conformi nell'organizzazione.|
|% conformità sconosciuta|Percentuale di computer il cui stato di conformità non è noto.|
|% con esenzione|Percentuale di computer esenti dal requisito di crittografia BitLocker.|
|% non esente|Percentuale di computer non esenti dal requisito di crittografia BitLocker.|
|conformi|Conteggio dei computer conformi nell'organizzazione.|
|Non conformi|Numero di computer non conformi nell'organizzazione.|
|Conformità sconosciuta|Conteggio dei computer con uno stato di conformità non noto.|
|Esente|Numero di computer esenti dal requisito di crittografia BitLocker.|
|Non esente|Numero di computer non esenti dal requisito di crittografia BitLocker.|

## <a name="bkmk-audit"></a> Report Controllo del ripristino

> [!NOTE]
> Questo report è disponibile anche nel [sito Web di Administration and Monitoring di BitLocker](/configmgr/protect/deploy-use/bitlocker/helpdesk-portal#reports).
>
> Per visualizzare questo report nella console di Configuration Manager, passare all'area di lavoro **Monitoraggio**. Nel riquadro di spostamento espandere il nodo **report** , espandere **report**, quindi espandere la cartella **Gestione BitLocker** . Selezionare la sottocartella per la versione localizzata del report, ad esempio **en-US**.

Usare questo report per controllare gli utenti che hanno richiesto l'accesso alle chiavi di ripristino di BitLocker. È possibile filtrare i criteri seguenti:

- Tipo specifico di utente, ad esempio un utente help desk o un utente finale
- Se la richiesta non è riuscita o ha avuto esito positivo
- Tipo specifico di chiave richiesta: password chiave di ripristino, ID chiave di ripristino o hash password TPM
- Un intervallo di date durante il quale si è verificato il recupero

[![schermata di esempio del report controllo ripristino BitLocker](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Nome&nbsp;colonna|Descrizione|
|----------------|----|
|Request date and time (Data e ora richiesta)|Data e ora in cui un utente finale o un help desk utente ha richiesto una chiave.|
|Origine richiesta di controllo|Sito da cui proviene la richiesta. I valori validi sono **portale self-service** o **helpdesk**.|
|Request result (Risultato richiesta)|Stato della richiesta. I valori validi sono **esito positivo** o **negativo**.|
|Helpdesk user (Utente supporto tecnico)|Utente amministratore che ha richiesto la chiave. Se un amministratore del supporto tecnico Recupera la chiave senza specificare il nome utente, il campo **utente finale** sarà vuoto. Un utente del supporto tecnico standard deve specificare il nome utente, che viene visualizzato in questo campo. Per il ripristino tramite il portale self-service, questo campo e il campo **utente finale** visualizzano il nome dell'utente che effettua la richiesta.|
|End user (Utente finale)|Nome dell'utente che ha richiesto il recupero della chiave.|
|Computer|Nome del computer ripristinato.|
|Key type (Tipo di chiave)|Tipo di chiave richiesta dall'utente. I tre tipi di chiavi sono:<br/><br/>- **Recovery key password** (Password chiave di ripristino): usata per ripristinare un computer in modalità di ripristino<br/>- **Recovery key ID**: (ID chiave di ripristino): usata per ripristinare un computer in modalità di ripristino per conto di un altro utente<br/>- **TPM password hash** (Hash password TPM): usata per ripristinare un computer con un TPM bloccato|
|Descrizione motivo|Motivo per cui l'utente ha richiesto il tipo di chiave specificato, in base all'opzione selezionata nel form.|
