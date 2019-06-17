---
title: Valutazione della compatibilità
titleSuffix: Configuration Manager
description: Informazioni sulla valutazione della compatibilità per le app di Windows e i driver in Desktop Analitica.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bef2c11732177dfb842f0961dc2d5d5a69edd55e
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148098"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Valutazione della compatibilità nel Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Aggiornamento delle valutazioni in Analitica di Windows sono state generiche, ad esempio: Attenzione necessita o correzione disponibile. Non fornisce alcun indicatore visivo sull'assegnazione di priorità le app o i driver con problemi o eseguire l'aggiornamento di insights. Desktop Analitica sostituisce questa funzionalità con **rischi relativi alla compatibilità**. Analitica desktop Mostra la valutazione per le app solo nella visualizzazione della distribuzione per uno scenario di pre-aggiornamento. Vengono suddivisi le app basate su informazioni dettagliate che ottiene Microsoft dai computer inclusi in un piano di distribuzione corrente.

Analitica desktop utilizza le seguenti categorie di valutazione della compatibilità:

- **Bassa**: Trovare il servizio non segnali per mettere l'app a rischio per un Windows esegue l'aggiornamento. È probabile che funzionerà su sistema operativo di destinazione come-è.  

- **Medium**: Analitica indica che l'applicazione potrebbe avere compromesse la funzionalità, sebbene correzione è probabilmente possibile.  

- **Elevata**: L'applicazione è quasi sicuramente esito negativo durante o dopo l'aggiornamento. Potrebbe essere necessario un monitoraggio e aggiornamento.  

- **Sconosciuto**: La valutazione non è stata eseguita l'app. Non esistono, ad esempio nessun altro insights *problemi noti di MS* oppure *pronto per Windows*.  

Nell'elenco di app o il driver asset in un piano di distribuzione, si noterà questo valore per ogni asset nel **rischi relativi alla compatibilità** colonna.


## <a name="app-risk-assessment"></a>Valutazione dei rischi di App

Esistono varie fonti che Analitica Desktop Usa per generare la valutazione di valutazione per le applicazioni:

- [Problemi noti di Microsoft](#microsoft-known-issues)
- [Pronto per il catalogo di Windows](#ready-for-windows)
- [Informazioni dettagliate avanzate](#advanced-insights)

È possibile trovare la valutazione per ogni origine dell'app nel Desktop Analitica. Nell'elenco degli asset di app in un piano di distribuzione, selezionare una singola app per aprire il riquadro di menu a comparsa di proprietà. Verrà visualizzato un livello di valutazione e indicazione generale. Il **fattori di rischio compatibilità** sezione mostra i dettagli per queste valutazioni.


## <a name="microsoft-known-issues"></a>Problemi noti di Microsoft

Desktop Analitica esamina il database di compatibilità delle app di Microsoft per problemi noti. Usa questo database per determinare eventuali blocchi di compatibilità esistenti per le applicazioni disponibili pubblicamente da Microsoft o altri server di pubblicazione. Questo controllo si applica solo al sistema operativo di destinazione per il piano di distribuzione selezionato.

Si noterà quanto segue nel riquadro delle proprietà app come **problemi noti MS**:

### <a name="application-is-removed-during-upgrade"></a>Rimozione dell'applicazione durante l'aggiornamento

Windows ha rilevato problemi di compatibilità. L'applicazione non eseguire la migrazione alla nuova versione del sistema operativo. Non sono richiesti interventi per continuare l'aggiornamento.

### <a name="blocking-upgrade"></a>Il blocco di aggiornamento

Windows ha rilevato problemi di blocco e non è possibile rimuovere l'applicazione durante l'aggiornamento. Potrebbe non funzionare nella nuova versione del sistema operativo. Prima dell'aggiornamento, rimuovere l'applicazione. Reinstallare ed eseguirne il test sulla nuova versione del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Il blocco di aggiornamento, ma può essere reinstallato dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma non eseguire la migrazione. Rimuovere l'applicazione prima dell'aggiornamento di Windows. Reinstallare il programma per la nuova versione del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Il blocco di aggiornamento, aggiornare l'applicazione alla versione più recente

La versione esistente dell'applicazione non è compatibile con la nuova versione del sistema operativo e non eseguire la migrazione. È disponibile una versione compatibile dell'applicazione. Aggiornare l'applicazione prima dell'aggiornamento.

### <a name="disk-encryption-blocking-upgrade"></a>Aggiornamento blocco crittografia del disco

Le funzionalità di crittografia dell'applicazione blocca l'aggiornamento. Disabilitare la funzionalità di crittografia prima di eseguire l'aggiornamento di Windows e abilitarlo dopo l'aggiornamento.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Non funziona con il nuovo sistema operativo, ma non bloccherà l'aggiornamento

L'applicazione non è compatibile con la nuova versione del sistema operativo, ma non bloccherà l'aggiornamento. Non sono richiesti interventi per continuare l'aggiornamento. Installare una versione compatibile dell'applicazione per la nuova versione del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Non funziona con il nuovo sistema operativo e l'aggiornamento verrà bloccato

L'applicazione non è compatibile con la nuova versione del sistema operativo e l'aggiornamento verrà bloccato. Rimuovere l'applicazione prima dell'aggiornamento. Una versione compatibile dell'applicazione potrebbe essere disponibile.

### <a name="evaluate-application-on-new-os"></a>Valutare l'applicazione nel nuovo sistema operativo

Windows verrà eseguita la migrazione dell'applicazione, ma rilevati problemi che potrebbero compromettere le prestazioni dell'app per la nuova versione del sistema operativo. Non sono richiesti interventi per continuare l'aggiornamento. Testare l'applicazione nella nuova versione del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Potrebbe bloccare l'aggiornamento, applicazione di test

Windows ha rilevato problemi che potrebbero interferire con l'aggiornamento, ma richiedono ulteriori indagini. Testare il comportamento dell'applicazione durante l'aggiornamento. Se si blocca l'aggiornamento, rimuoverlo prima dell'aggiornamento. Quindi reinstallarlo e testare la nuova versione del sistema operativo.

### <a name="multiple"></a>Più elementi

I problemi più rendere l'applicazione. Selezionare **Query** per visualizzare i dettagli sui problemi rilevati da Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstallare l'applicazione dopo l'aggiornamento

L'applicazione è compatibile con la nuova versione del sistema operativo, ma è necessario reinstallarlo dopo l'aggiornamento di Windows. Il processo di aggiornamento rimuove l'applicazione. Non sono richiesti interventi per continuare l'aggiornamento. Reinstallare l'applicazione nella nuova versione del sistema operativo.


## <a name="ready-for-windows"></a>Pronto per Windows

Il [pronto per Windows](https://www.readyforwindows.com) catalogo applicazioni mette in correlazione le origini dati seguenti:

- Dati di diagnostica da altri clienti che sono subordinati stesse App
- Controlli aggiuntivi da parte di Microsoft, ad esempio i blocchi di compatibilità su un dispositivo

Le categorie possibili sono:

- **Ampiamente adottate**: Almeno 100.000 dispositivi commerciali di Windows 10 sono installato l'app.  

- **Adottato**: Almeno 10.000 dispositivi commerciali di Windows 10 sono installato l'app.  

- **Dati insufficienti**: Un numero troppo ridotto i dispositivi Windows 10 commerciali condividono informazioni per l'app a Microsoft di categorizzare la sua adozione.

- **Contattare lo sviluppatore**: Potrebbero esserci problemi di compatibilità con questa versione dell'app. Microsoft consiglia di contattare il provider di software per altre informazioni. Per altre informazioni, vedere [pronto per Windows](https://www.readyforwindows.com/).  

- **Sconosciuto**: Nessuna informazione pronti per Windows è disponibile per questa versione di questa applicazione. Le informazioni potrebbero essere disponibili per le altre versioni dell'applicazione in [pronto per Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Informativa sul supporto

Se il provider di software supporta uno o più versioni dell'applicazione in Windows 10, si noterà l'istruzione seguente nel riquadro delle proprietà app. Nella sezione compatibilità fattori di rischio, esaminare i **supporta istruzione**.



## <a name="advanced-insights"></a>Informazioni dettagliate avanzate

Desktop Analitica consente inoltre di rilevare i problemi usando le informazioni dettagliate aggiuntive seguenti:

### <a name="adopted-version-available"></a>Versione adottata disponibile

È disponibile un'altra versione dell'app che è ampiamente adottate da altri clienti. Questo segnale utilizza i dati di pronto per Windows. Se sono presenti eventuali blocchi di aggiornamento con la versione corrente, è possibile distribuire la versione alternativa invece.

### <a name="driver-dependency"></a>Dipendenze di driver

L'app è dipendente da un driver. Desktop Analitica consiglia l'app per attività di test. Dovrebbe funzionare correttamente per la fase pilota, ma sono disponibili eventuali regressioni. Se si verificano problemi, contattare l'editore per richiedere una versione compatibile con Windows 10.



## <a name="driver-risk-assessment"></a>Valutazione dei rischi di driver

Elenca inoltre desktop Analitica e gruppi in base alla disponibilità di eventuali driver di non eseguire la migrazione alla versione del sistema operativo.

È possibile trovare la valutazione sul driver in Desktop Analitica. Nell'elenco degli asset di driver in un piano di distribuzione, selezionare un singolo driver per aprire il riquadro di menu a comparsa di proprietà. Verrà visualizzato un livello di valutazione e indicazione generale. Il **fattori di rischio compatibilità** sezione mostra i dettagli per queste valutazioni.

| Disponibilità driver | Azione necessaria? | Che cosa significa | Linee guida |
|---------------------|------------------|---------------|----------|
| Preinstallati disponibili | No, per il riconoscimento solo | La versione attualmente installata di un'applicazione o il driver non eseguire la migrazione alla nuova versione del sistema operativo. È installata una versione compatibile con la nuova versione del sistema operativo. | Non sono richiesti interventi per continuare l'aggiornamento. |
| Importa da Windows Update | Yes | La versione attualmente installata di un driver non eseguire la migrazione alla nuova versione del sistema operativo. Una versione compatibile è disponibile da Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, è necessaria alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Disponibile in arrivo e da Windows Update | Yes | La versione attualmente installata di un driver non eseguire la migrazione alla nuova versione del sistema operativo. Anche se è installato un nuovo driver durante l'aggiornamento, una versione più recente è disponibile da Windows Update. | Se il computer riceve automaticamente gli aggiornamenti da Windows Update, è necessaria alcuna azione. In caso contrario, importare un nuovo driver da Windows Update dopo l'aggiornamento di Windows. |
| Contattare il fornitore | Yes | Il driver non eseguire la migrazione alla nuova versione del sistema operativo e Analitica Desktop non è possibile individuare una versione compatibile. | Per una soluzione, contattare il fornitore di hardware indipendente (IHV) che produce il driver o OEM (OEM) che ha fornito il dispositivo. |


## <a name="see-also"></a>Vedere anche

FastTrack Center Benefit per Windows 10 consente di accedervi **garantire App Desktop**. Questo vantaggio è un nuovo servizio progettato per risolvere i problemi con Windows 10 e Office 365 ProPlus compatibilità dell'applicazione. Per altre informazioni, vedere [garantire App Desktop](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
