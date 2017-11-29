---
title: Creare ed eseguire script
titleSuffix: Configuration Manager
description: Creare ed eseguire script di PowerShell in dispositivi client.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 964f6d39c4c1afc82ff4336821740923d27cd569
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creare ed eseguire script di PowerShell dalla console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'esecuzione di script di PowerShell con System Center Configuration Manager è stata integrata in modo ancora migliore. Il vantaggio di PowerShell è che consente di creare script automatici sofisticati, intuitivi e condivisi con una vasta community. Gli script semplificano la creazione di strumenti personalizzati per amministrare il software e consentono di eseguire rapidamente attività pratiche, anche impegnative, in modo più semplice e uniforme.

Grazie a questa integrazione in System Center Configuration Manager, è possibile usare la funzionalità *Esegui script* per:

- Creare e modificare script da usare con Configuration Manager.
- Gestire l'utilizzo degli script tramite ruoli e ambiti di protezione  
- Eseguire gli script in raccolte o singoli PC Windows gestiti in locale.
- Ottenere rapidi risultati degli script aggregati dai dispositivi client.
- Monitorare l'esecuzione degli script e visualizzare i risultati restituiti dall'output degli script.

>[!IMPORTANT]
>Considerando la potenza degli script, è consigliabile usarli con attenzione e solo se intenzionalmente. Sono state integrate altre misure di sicurezza per supportare l'utente finale, come ruoli e ambiti segregati. Verificare l'accuratezza degli script prima di eseguirli e accertarsi che provengano da un'origine attendibile, per impedirne l'esecuzione accidentale. Prestare attenzione ai caratteri estesi o ad altri problemi di offuscamento e abituarsi a proteggere gli script.

>[!TIP]
>Introdotti con la versione 1706, gli script di PowerShell sono una funzionalità in versione non definitiva. Per abilitare gli script, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Prerequisiti

- Per eseguire script PowerShell, nel client deve essere in esecuzione PowerShell versione 3.0 o successiva. Tuttavia, se lo script eseguito contiene funzionalità di una versione successiva di PowerShell, nel client in cui viene eseguito lo script deve essere installata questa versione.
- Per eseguire gli script, i client Configuration Manager devono avere in esecuzione il client della versione 1706 o successiva.
- Per usare gli script, l'utente deve essere membro del ruolo di sicurezza appropriato di Configuration Manager.
- Per importare e creare script, l'account deve avere autorizzazioni **Crea** per **Script SMS** nel ruolo di sicurezza **Amministratore completo**.
- Per approvare o rifiutare script, l'account deve avere autorizzazioni **Approva** per **Script SMS** nel ruolo di sicurezza **Amministratore completo**.
- Per eseguire script: l'account deve avere autorizzazioni di **esecuzione script** per **Raccolte** nel ruolo di sicurezza **Gestione impostazioni di conformità**.

Per altre informazioni sui ruoli di sicurezza di Configuration Manager, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitazioni

La funzionalità Esegui script supporta attualmente:

- Linguaggi di scripting: PowerShell
- Tipi di parametro: intero e stringa

## <a name="run-script-authors-and-approvers"></a>Autori e responsabili dell'approvazione di script

La funzionalità Esegui script usa il concetto di *autore di script* e *responsabile dell'approvazione di script* come ruoli separati per l'implementazione e l'esecuzione di uno script. La separazione tra autori e responsabili dell'approvazione consente un'importante verifica dei processi per questo potente strumento.

### <a name="scripts-roles-control"></a>Controllo dei ruoli per gli script

Per impostazione predefinita, gli utenti non possono approvare uno script da loro stessi creato. Poiché gli script sono potenti e versatili e possono essere distribuiti in più dispositivi, è possibile separare i ruoli tra la persona che crea lo script e la persona che lo approva. Questi ruoli garantiscono un livello aggiuntivo di sicurezza, impedendo l'esecuzione di uno script senza supervisione. Per semplificare le attività di test, è possibile disattivare questa approvazione secondaria.

### <a name="approve-or-deny-a-script"></a>Approvare o rifiutare uno script

Gli script devono essere approvati dal ruolo *responsabile dell'approvazione di script* prima di poter essere eseguiti. Per approvare uno script:

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nell'elenco **Script** scegliere lo script che si desidera approvare o rifiutare e quindi scegliere la scheda **Home** nel gruppo **Script**, quindi fare clic su **Approve/Deny** (Approva/Rifiuta).
4. Nella finestra di dialogo **Approva o rifiuta script** selezionare **Approva** o **Rifiuta** per lo script e, facoltativamente, immettere un commento sulla decisione.  Se si rifiuta uno script, questo non può essere eseguito sui dispositivi client. <br>
![Script - Approvazione](./media/run-scripts/RS-approval.png)
5. Completare la procedura guidata. Nell'elenco **Script** la colonna **Stato dell'approvazione** cambia a seconda dell'azione eseguita.

### <a name="allow-users-to-approve-their-own-scripts"></a>Consentire agli utenti di approvare i propri script

Questa approvazione viene usata principalmente per la fase di test dello sviluppo di script.

1. Nella console di Configuration Manager fare clic su **Amministrazione**.
2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.
3. Nell'elenco dei siti selezionare il sito e quindi scegliere la scheda **Home** nel gruppo **Siti** e fare clic su **Impostazioni gerarchia**.
4. Nella scheda **Generale** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** deselezionare la casella di controllo **Do not allow script authors to approve their own scripts** (Non consentire agli autori di script di approvare i propri script).

>[!IMPORTANT]
>Come procedura consigliata, non consentire a un autore di script di approvare i propri script. Questa operazione deve essere consentita solo in un ambiente di prova. Valutare con attenzione il potenziale impatto della modifica di questa impostazione in un ambiente di produzione.

## <a name="security-scopes"></a>ambiti di protezione
*Introdotti con la versione 1710*  
La funzionalità Esegui script usa gli ambiti di protezione, una caratteristica esistente di Configuration Manager, per controllare la creazione e l'esecuzione di script tramite l'assegnazione di tag che rappresentano gruppi di utenti. Per altre informazioni sull'uso degli ambiti di protezione, vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-a-script"></a>Creare uno script

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea gruppo**.
4. Nella pagina **Script** della procedura guidata **Crea script** configurare le impostazioni seguenti:
    - In **Nome script** inserire il nome dello script. Anche se è possibile creare più script con lo stesso nome, l'uso di nomi duplicati rende più difficile individuare lo script necessario nella console di Configuration Manager.
    - **Lingua script**: attualmente sono supportati solo script di PowerShell.
    - **Importa**: importare uno script di PowerShell nella console. Lo script viene visualizzato nel campo **Script**.
    - **Cancella**: rimuove lo script corrente dal campo Script.
    - **Script**: visualizza lo script attualmente importato. È possibile modificare lo script in questo campo in base alle esigenze.
1. Completare la procedura guidata. Il nuovo script viene visualizzato nell'elenco **Script** con stato **In attesa di approvazione** . Prima di poter eseguire questo script nei dispositivi client, è necessario approvarlo.

## <a name="script-parameters"></a>Parametri di script
*Introdotti con la versione 1710*  
L'aggiunta di parametri a uno script offre maggiore flessibilità per ogni attività. La sezione seguente descrive le attuali caratteristiche della funzionalità Esegui script con i parametri di script per tipi di dati *String* e *Integer*. Sono disponibili anche gli elenchi dei valori preimpostati. Se lo script ha tipi di dati non supportati, verrà generato un avviso.

Nella finestra di dialogo **Crea script** fare clic su **Parametri script** in **Script**.

Ognuno dei parametri di script è associato a una finestra di dialogo per l'aggiunta di altri dettagli e la convalida.

### <a name="parameter-validation"></a>Convalida dei parametri

Ogni parametro nello script ha una finestra di dialogo **Proprietà parametri script**, in cui è possibile aggiungere la convalida per il parametro. Dopo aver aggiunto la convalida, verranno restituiti errori quando si immette un valore che non soddisfa i requisiti di convalida per il parametro.

#### <a name="example-firstname"></a>Esempio: FirstName

In questo esempio è possibile impostare le proprietà del parametro stringa *FirstName*. Notare il campo facoltativo per **Errore personalizzato**. Questo campo è utile per l'aggiunta di indicazioni per l'utente riguardo al campo specifico e di indicazioni per l'utente riguardo all'interazione con il parametro di stringa *FirstName* in questo caso.

![Parametri di script - Stringa](./media/run-scripts/RS-parameters-string.png)

## <a name="script-examples"></a>Esempi di script

Ecco alcuni esempi che mostrano gli script che è possibile usare con questa funzionalità.

### <a name="create-a-folder"></a>Crea una cartella

``` powershell
New-Item "c:\scripts" -type folder name
```

### <a name="create-a-file"></a>Creare un file

```powershell
New-Item "c:\scripts\new_file.txt" -type file name
```

### <a name="ping-a-given-computer"></a>Effettuare il ping di un computer specifico

Questo script usa una stringa come parametro per un'operazione di *ping*.

``` powershell
Param
(
 [String][Parameter(Mandatory=$True, Position=1)] $Computername
)

Ping $Computername
```

### <a name="get-battery-status"></a>Ottenere lo stato della batteria

Questo script usa WMI per eseguire query sul computer in modo da determinarne lo stato della batteria.

``` powershell
Write-Output (Get-WmiObject -Class Win32_Battery).BatteryStatus

```

## <a name="run-a-script"></a>Esegui uno script

Dopo che uno script è stato approvato, può essere eseguito su una raccolta a scelta dell'utente. Una volta avviata l'esecuzione, lo script viene eseguito rapidamente in un sistema ad alta priorità e viene completato entro un'ora. I risultati dello script vengono restituiti tramite un sistema di messaggi di stato più lento.

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro Asset e conformità fare clic su **Raccolte dispositivi**.
3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta di dispositivi in cui si desidera eseguire lo script.
4. Nella scheda **Home** nel gruppo **Tutti i sistemi** fare clic su **Esegui script**.
5. Nella pagina **Script** della procedura guidata **Esegui Script** scegliere uno script dall'elenco. Vengono visualizzati solo gli script approvati.
6. Fare clic su **Avanti** e completare la procedura guidata.

>[!IMPORTANT]
>Se lo script non viene eseguito entro il periodo di tempo di un'ora, ad esempio perché il client di destinazione è spento, è necessario eseguirlo di nuovo.

### <a name="target-machine-execution"></a>Esecuzione nel computer di destinazione
Lo script viene eseguito come account di *sistema* o *computer* nei client di destinazione. Questo account ha accesso di rete limitato. L'accesso dello script a posizioni e sistemi remoti deve essere eseguito di conseguenza.

## <a name="work-flow-and-monitoring"></a>Flusso di lavoro e monitoraggio

Ecco l'aspetto della funzionalità Esegui script come flusso di lavoro di creazione, approvazione, esecuzione e monitoraggio.

![Esegui script - Flusso di lavoro](./media/run-scripts/RS-run-scripts-work-flow.png)

### <a name="script-monitoring"></a>Monitoraggio dello script

Dopo aver avviato l'esecuzione di uno script in una raccolta di dispositivi, usare la procedura seguente per monitorare l'operazione. A partire dalla versione 1710, è possibile monitorare uno script in tempo reale durante la sua esecuzione ed è anche possibile restituire un report per un'esecuzione della funzionalità Esegui script specifica.

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** fare clic su **Stato script**. ![Monitoraggio dello script - Stato di esecuzione dello script](./media/run-scripts/RS-monitoring-three-bar.png)
3. Nell'elenco **Stato script** sono visualizzati i risultati per ogni script eseguito nei dispositivi client. Un codice di uscita dello script uguale a **0** indica in genere che lo script è stato eseguito correttamente.

## <a name="see-also"></a>Vedere anche

- [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration)
