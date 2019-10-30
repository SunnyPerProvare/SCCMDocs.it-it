---
title: Valutazione della compatibilità
titleSuffix: Configuration Manager
description: Informazioni sulla valutazione della compatibilità per le app e i driver di Windows in desktop Analytics.
ms.date: 10/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f0832dc96a5b03e0ed603b76c794444eff7d967
ms.sourcegitcommit: 07756e9b4ed7b134e32349acb1eeae93c6de9e28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049429"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Valutazione della compatibilità in desktop Analytics

Le valutazioni dell'aggiornamento in Windows Analytics erano generiche, ad esempio: attenzione necessaria o correzione disponibile. Non fornisce alcun indicatore visivo su come classificare in ordine di priorità le app o i driver con problemi o informazioni dettagliate sull'aggiornamento. Desktop Analytics sostituisce questa funzionalità con i rischi per la **compatibilità**. Desktop Analytics mostra la valutazione per le app solo nella visualizzazione distribuzione per uno scenario di pre-aggiornamento. Suddivide le app in base alle informazioni ottenute da Microsoft dalle macchine virtuali incluse in un piano di distribuzione corrente.

Desktop Analytics usa le seguenti categorie di valutazione della compatibilità:

- **Bassa**: il servizio non ha rilevato segnali per inserire questa app a rischio di un aggiornamento di Windows. È probabile che funzioni sul sistema operativo di destinazione così com'è.  

- **Media**: Analytics indica che è possibile che l'applicazione abbia funzionalità disaccoppiate, anche se è probabile che la correzione sia possibile.  

- **Alta**: l'applicazione è quasi certo che si verifichi un errore durante o dopo l'aggiornamento. Potrebbe essere necessaria una correzione.  

- **Sconosciuto**: l'app non è stata valutata. Non sono disponibili altre informazioni, ad esempio *problemi noti di MS* o *pronto per Windows*.  

Nell'elenco di asset app o driver in un piano di distribuzione, questo valore verrà visualizzato per ogni asset nella colonna **rischio di compatibilità** .


## <a name="app-risk-assessment"></a>Valutazione del rischio delle app

![Diagramma delle origini di valutazione del rischio di app](media/app-risk-assessment-sources.png)

Sono disponibili diverse origini usate da desktop Analytics per generare la valutazione della valutazione per le applicazioni:

- [Problemi noti di Microsoft](#microsoft-known-issues)
- [Pronto per il catalogo di Windows](#ready-for-windows)
- [Informazioni dettagliate avanzate](#advanced-insights)

È possibile trovare la valutazione per ogni origine nell'app in desktop Analytics. Nell'elenco di asset app in un piano di distribuzione selezionare una singola app per aprire il riquadro a comparsa Proprietà. Verrà visualizzato un livello generale di raccomandazione e valutazione. La sezione **fattori di rischio** per la compatibilità Mostra i dettagli per queste valutazioni.


## <a name="microsoft-known-issues"></a>Problemi noti di Microsoft

Desktop Analytics esamina il database di compatibilità delle app Microsoft per individuare eventuali problemi noti. Usa questo database per determinare eventuali blocchi di compatibilità esistenti per le applicazioni disponibili pubblicamente da Microsoft o da altri editori. Questo controllo si applica solo al sistema operativo di destinazione per il piano di distribuzione selezionato.

Verranno visualizzati i seguenti problemi nel riquadro Proprietà app come **problemi noti di MS**:

### <a name="asset-is-removed-during-upgrade"></a>Asset rimosso durante l'aggiornamento

Windows ha rilevato problemi di compatibilità con un'applicazione o un driver. L'asset non verrà migrato alla nuova versione del sistema operativo. Per continuare l'aggiornamento, non è necessaria alcuna azione. Installare una versione compatibile dell'applicazione o del driver nella nuova versione del sistema operativo.

<!-- 3594545 -->
Windows può rimuovere parzialmente o completamente questi asset:

- Rimozione completa: il programma di installazione di Windows rimuove completamente l'app o il driver dal dispositivo durante l'aggiornamento.
- Rimozione parziale: il programma di installazione di Windows rimuove parzialmente l'app o il driver dal dispositivo. È necessario disinstallarlo manualmente dopo l'aggiornamento di Windows.

In entrambi i casi, dopo l'aggiornamento di Windows l'utente non può usare l'app o l'hardware associato al driver.

Per visualizzare questa raccomandazione nel portale di analisi dei desktop:

1. In un piano di distribuzione selezionare **prepara pilota**.
1. Selezionare un asset dall'elenco.
1. Visualizzare i fattori di rischio e le raccomandazioni per la compatibilità nel riquadro laterale.

![Screenshot della raccomandazione asset nel portale di analisi del desktop](media/3594545-app-removed.png)

### <a name="blocking-upgrade"></a>Aggiornamento del blocco

Windows ha rilevato problemi di blocco e non può rimuovere l'applicazione durante l'aggiornamento. Potrebbe non funzionare con la nuova versione del sistema operativo. Prima di eseguire l'aggiornamento, rimuovere l'applicazione. Reinstallare e testare la nuova versione del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Blocco dell'aggiornamento, ma è possibile reinstallarlo dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma non verrà eseguita la migrazione. Rimuovere l'applicazione prima di aggiornare Windows. Reinstallarlo nella nuova versione del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Blocco dell'aggiornamento, aggiornamento dell'applicazione alla versione più recente

La versione esistente dell'applicazione non è compatibile con la nuova versione del sistema operativo e non viene migrata. È disponibile una versione compatibile dell'applicazione. Aggiornare l'applicazione prima di eseguire l'aggiornamento.

### <a name="disk-encryption-blocking-upgrade"></a>Aggiornamento del blocco della crittografia del disco

Le funzionalità di crittografia dell'applicazione bloccano l'aggiornamento. Disabilitare la funzionalità di crittografia prima di aggiornare Windows e abilitarla dopo l'aggiornamento.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Non funziona con il nuovo sistema operativo, ma non blocca l'aggiornamento

L'applicazione non è compatibile con la nuova versione del sistema operativo, ma non blocca l'aggiornamento. Per continuare l'aggiornamento, non è necessaria alcuna azione. Installare una versione compatibile dell'applicazione nella nuova versione del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Non funziona con il nuovo sistema operativo e blocca l'aggiornamento

L'applicazione non è compatibile con la nuova versione del sistema operativo e blocca l'aggiornamento. Rimuovere l'applicazione prima di eseguire l'aggiornamento. Potrebbe essere disponibile una versione compatibile dell'applicazione.

### <a name="evaluate-application-on-new-os"></a>Valutazione dell'applicazione nel nuovo sistema operativo

Windows eseguirà la migrazione dell'applicazione, ma ha rilevato problemi che potrebbero influito sulle prestazioni dell'app sulla nuova versione del sistema operativo. Per continuare l'aggiornamento, non è necessaria alcuna azione. Testare l'applicazione nella nuova versione del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Può bloccare l'aggiornamento, testare l'applicazione

Sono stati rilevati problemi che potrebbero interferire con l'aggiornamento, ma è necessario approfondire l'analisi. Testare il comportamento dell'applicazione durante l'aggiornamento. Se blocca l'aggiornamento, rimuoverlo prima dell'aggiornamento. Quindi reinstallare e testare la nuova versione del sistema operativo.

### <a name="multiple"></a>Più elementi

Più problemi influiscono sull'applicazione. Selezionare **query** per visualizzare i dettagli sui problemi rilevati da Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstalla l'applicazione dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma è necessario reinstallarla dopo l'aggiornamento di Windows. Il processo di aggiornamento rimuove l'applicazione. Per continuare l'aggiornamento, non è necessaria alcuna azione. Reinstallare l'applicazione nella nuova versione del sistema operativo.


## <a name="ready-for-windows"></a>Pronto per Windows

Il Catalogo applicazioni [pronto per Windows mette in](https://www.readyforwindows.com) correlazione le origini dati seguenti:

- Dati di diagnostica di altri clienti che segnalano le stesse app
- Ulteriori controlli da Microsoft, ad esempio i blocchi di compatibilità in un dispositivo

Le categorie possibili sono:

- **Elevata adozione**: almeno 100.000 dispositivi commerciali Windows 10 hanno installato questa app.  

- **Adottato**: almeno 10.000 dispositivi commerciali Windows 10 hanno installato questa app.  

- **Dati insufficienti**: un numero troppo basso di dispositivi Windows 10 commerciali condivide le informazioni per questa app per la categorizzazione dell'adozione da parte di Microsoft.

- **Contattare lo sviluppatore**: potrebbero essersi verificati problemi di compatibilità con questa versione dell'app. Microsoft consiglia di contattare il provider di software per ottenere ulteriori informazioni. Per ulteriori informazioni, vedere [Ready for Windows](https://www.readyforwindows.com/).  

- **Sconosciuto**: per questa versione di questa applicazione non sono disponibili informazioni pronte per Windows. Le informazioni potrebbero essere disponibili per le altre versioni dell'applicazione in [pronto per Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Istruzione support

Se il provider software supporta una o più versioni di questa applicazione in Windows 10, questa istruzione verrà visualizzata nel riquadro Proprietà app. Nella sezione fattori di rischio per la compatibilità esaminare l' **istruzione di supporto**.



## <a name="advanced-insights"></a>Informazioni dettagliate avanzate

Desktop Analytics può anche rilevare problemi usando le informazioni aggiuntive seguenti:

### <a name="adopted-version-available"></a>Versione adottata disponibile

È disponibile un'altra versione di questa app che è altamente adottata da altri clienti. Questo segnale usa i dati di Ready per Windows. Se sono presenti blocchi di aggiornamento con la versione corrente, è consigliabile distribuire invece la versione alternativa.

### <a name="driver-dependency"></a>Dipendenza driver

L'app dipende da un driver. Desktop Analytics consiglia all'app di eseguire test pilota per individuare eventuali regressioni. In caso di problemi, contattare l'autore per richiedere una versione conforme a Windows 10.

### <a name="additional-insights"></a>Informazioni aggiuntive

<!-- 4021225 -->
Quando si aggiorna il sito e i client di Configuration Manager alla versione 1906, i client segnalano anche queste informazioni aggiuntive, quando il livello dati di diagnostica è impostato su avanzato limitato:

> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Questo scenario non è funzionale finché la versione del client non è la più recente.

#### <a name="16-bit-apps"></a>app a 16 bit

Rimuovere tutti i componenti a 16 bit dalle applicazioni e sostituirli con equivalenti a 32 bit o a 64 bit. Per ulteriori informazioni, vedere la pagina relativa a [Windows Vista e Windows Server 2008 Developer Story: Cookbook per la compatibilità delle applicazioni](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)).

L'altra opzione consiste nell'abilitare la macchina DOS virtuale NT (NTVDM) per il supporto in Windows 10.

#### <a name="requires-admin-privileges"></a>Richiede privilegi di amministratore

L'app richiede che l'utente disponga dell'accesso amministrativo al dispositivo. Usare un manifesto dell'applicazione per queste app che richiedono le autorizzazioni di amministratore. Per altre informazioni, vedere [creare e incorporare un manifesto dell'applicazione](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics consiglia all'app di eseguire test pilota per individuare eventuali regressioni.

#### <a name="java-dependency"></a>Dipendenza Java

Molte applicazioni Java si basano su un Java Runtime Environment (JRE) installato separatamente. Sebbene le versioni precedenti di JRE possano continuare a funzionare in Windows 10, Oracle supporta solo le versioni più recenti di JRE. L'uso di un JRE non supportato precedente potrebbe avere vulnerabilità di sicurezza. Verificare che l'applicazione sia in esecuzione nelle versioni più recenti di JRE.

#### <a name="not-dpi-aware"></a>Non compatibile con DPI

È possibile che l'app includa problemi di visualizzazione con risoluzioni avanzate dello schermo in Windows 10. Usare un manifesto dell'applicazione per evitare problemi con risoluzioni DPI elevate. Per altre informazioni, vedere [manifesti dell'applicazione](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Desktop Analytics consiglia all'app di eseguire test pilota per individuare eventuali regressioni.

#### <a name="silverlight-framework"></a>Framework Silverlight

Microsoft consiglia di non usare Silverlight per le app non basate su browser. La data di fine del supporto per Silverlight 5 è il 2021 ottobre.

La maggior parte dei Web browser correnti non supporta Silverlight.

| Browser | Supporto |
|---------|---------|
| Google Chrome | Fine del supporto: settembre 2015 |
| Firefox | Fine del supporto: 2017 marzo |
| Microsoft Edge | Nessun plug-in disponibile |

Desktop Analytics consiglia all'app di eseguire test pilota per individuare eventuali regressioni.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

Il .NET Framework versione 1,0 non è supportato in Windows 10. La versione 1,1 non è compatibile con Windows 10. Se l'app è di un server di pubblicazione di terze parti, contattare il fornitore per richiedere una versione conforme a Windows 10. In caso contrario, risviluppare l'applicazione per usare una versione supportata di .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

I Framework .NET 2,0 e 3,5 sono supportati in Windows 10. Potrebbe essere necessario abilitare la funzionalità Windows. Per ulteriori informazioni, vedere [installare il .NET Framework 3,5 in Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Accesso all'interfaccia utente

Le applicazioni con accesso all'interfaccia utente possono ignorare i livelli di controllo dell'interfaccia utente per guidare l'input a finestre con privilegi più elevati sul desktop. Usare questa impostazione solo per le applicazioni di Assistive Technology dell'interfaccia utente.

Se non si usano le funzionalità di accessibilità nell'app, impostare il flag di accesso dell'interfaccia utente nel manifesto dell'app su false. Per altre informazioni, vedere [creare e incorporare un manifesto dell'applicazione](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics consiglia all'app di eseguire test pilota per individuare eventuali regressioni.


## <a name="driver-risk-assessment"></a>Valutazione del rischio del driver

In desktop Analytics sono inoltre elencati e raggruppati per disponibilità tutti i driver che non vengono migrati alla versione del sistema operativo.

È possibile trovare la valutazione sul driver in desktop Analytics. Nell'elenco di asset driver in un piano di distribuzione selezionare un singolo driver per aprire il riquadro a comparsa Proprietà. Verrà visualizzato un livello generale di raccomandazione e valutazione. La sezione **fattori di rischio** per la compatibilità Mostra i dettagli per queste valutazioni.

| Disponibilità driver | È necessario agire? | Significato | Guida |
|---------------------|------------------|---------------|----------|
| Disponibile in-box | No, solo per la consapevolezza | La versione attualmente installata di un'applicazione o di un driver non verrà migrata alla nuova versione del sistema operativo. Una versione compatibile viene installata con la nuova versione del sistema operativo. | Per continuare l'aggiornamento, non è necessaria alcuna azione. |
| Importa da Windows Update | Yes | La versione attualmente installata di un driver non verrà migrata alla nuova versione del sistema operativo. Una versione compatibile è disponibile dal Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, non è richiesta alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Disponibile in-box e da Windows Update | Yes | La versione attualmente installata di un driver non verrà migrata alla nuova versione del sistema operativo. Sebbene venga installato un nuovo driver durante l'aggiornamento, è disponibile una versione più recente da Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, non è richiesta alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Verifica con fornitore | Yes | Il driver non viene migrato alla nuova versione del sistema operativo e desktop Analytics non riesce a trovare una versione compatibile. | Per una soluzione, consultare il fornitore dell'hardware indipendente (IHV) che produce il driver o l'OEM (Original Equipment Manufacturer) che ha fornito il dispositivo. |


## <a name="see-also"></a>Vedere anche

Il vantaggio FastTrack Center per Windows 10 consente di accedere ad **app desktop assicura**. Questo vantaggio è un nuovo servizio progettato per risolvere i problemi relativi alla compatibilità delle app con Windows 10 e Office 365 ProPlus. Per altre informazioni, vedere [app desktop assicura](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
