---
title: Creare ed eseguire script
titleSuffix: Configuration Manager
description: Creare ed eseguire script di PowerShell in dispositivi client.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b9699b2f4bd1f18890d25582be9a8d20778b64be
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creare ed eseguire gli script di PowerShell dalla console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1236459-->
La funzionalità di esecuzione degli script di Powershell è integrata in System Center Configuration Manager. Il vantaggio di PowerShell è che consente di creare script automatici sofisticati, intuitivi e condivisi con una vasta community. Gli script semplificano la creazione di strumenti personalizzati per amministrare il software e consentono di eseguire rapidamente attività pratiche, anche impegnative, in modo più semplice e coerente.  

> [!TIP]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1706 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1802, questa funzionalità non è più in versione non definitiva.  


> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Grazie a questa integrazione in System Center Configuration Manager, è possibile usare la funzionalità *Esegui script* per:

- Creare e modificare script da usare con System Center Configuration Manager.
- Gestire l'utilizzo degli script tramite ruoli e ambiti di protezione. 
- Eseguire gli script in raccolte o singoli PC Windows gestiti in locale.
- Ottenere rapidi risultati degli script aggregati dai dispositivi client.
- Monitorare l'esecuzione degli script e visualizzare i risultati restituiti dall'output degli script.

>[!WARNING]
>Considerando la potenza degli script, è consigliabile usarli con attenzione e solo se intenzionalmente. Sono state integrate altre misure di sicurezza per supportare l'utente finale, come ruoli e ambiti segregati. Verificare l'accuratezza degli script prima di eseguirli e accertarsi che provengano da un'origine attendibile, per impedirne l'esecuzione accidentale. Prestare attenzione ai caratteri estesi o ad altri problemi di offuscamento e abituarsi a proteggere gli script. [Informazioni sulla sicurezza degli script PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Prerequisiti

- Per eseguire script PowerShell, nel client deve essere in esecuzione PowerShell versione 3.0 o successiva. Tuttavia, se lo script eseguito contiene funzionalità di una versione successiva di PowerShell, nel client in cui viene eseguito lo script deve essere installata questa versione.
- Per eseguire gli script, i client Configuration Manager devono avere in esecuzione il client della versione 1706 o successiva.
- Per usare gli script, l'utente deve essere membro del ruolo di sicurezza appropriato di Configuration Manager.
- Per importare e creare script, l'account deve avere autorizzazioni **Crea** per **Script SMS**.
- Per approvare o rifiutare script, l'account deve avere autorizzazioni **Approva** per **Script SMS**.
- Per eseguire gli script, l'account deve avere autorizzazioni **Esegui script** per **Raccolte**.

Per altre informazioni sui ruoli di sicurezza di Configuration Manager:</br>
[Ambiti di protezione per l'esecuzione di script](#BKMK_Scopes)</br>
[Ruoli di sicurezza per l'esecuzione di script](#BKMK_ScriptRoles)</br>
[Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration)

## <a name="limitations"></a>Limitazioni

La funzionalità Esegui script supporta attualmente:

- Linguaggi di scripting: PowerShell
- Tipi di parametro: intero, stringa ed elenco.


>[!WARNING]
>Tenere presente che quando si usano i parametri si apre una superficie di attacco con il rischio potenziale di attacchi PowerShell injection. Per ovviare al problema, esistono vari modi e soluzioni alternative, ad esempio l'uso di espressioni regolari per convalidare l'input del parametro o l'uso di parametri predefiniti. Una procedura consigliata comune consiste nel non includere segreti negli script di PowerShell, ad esempio password e altro. [Informazioni sulla sicurezza degli script PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Autori e responsabili dell'approvazione di script

La funzionalità Esegui script usa il concetto di *autore di script* e *responsabile dell'approvazione di script* come ruoli separati per l'implementazione e l'esecuzione di uno script. La separazione tra autori e responsabili dell'approvazione consente un'importante verifica dei processi per questo potente strumento. Un altro ruolo, *esecutori di script*, consente l'esecuzione di script, ma non la creazione o l'approvazione. Vedere [Creare ruoli di sicurezza per gli script](#BKMK_ScriptRoles).

### <a name="scripts-roles-control"></a>Controllo dei ruoli per gli script

Per impostazione predefinita, gli utenti non possono approvare uno script da loro stessi creato. Poiché gli script sono potenti e versatili e vengono potenzialmente distribuiti a molti dispositivi, è possibile separare i ruoli tra la persona che crea lo script e la persona che lo approva. Questi ruoli garantiscono un livello aggiuntivo di sicurezza, impedendo l'esecuzione di uno script senza supervisione. Per semplificare le attività di test, è possibile disattivare l'approvazione secondaria.

### <a name="approve-or-deny-a-script"></a>Approvare o rifiutare uno script

Gli script devono essere approvati dal ruolo *responsabile dell'approvazione di script* prima di poter essere eseguiti. Per approvare uno script:

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nell'elenco **Script** scegliere lo script che si desidera approvare o rifiutare e quindi scegliere la scheda **Home** nel gruppo **Script**, quindi fare clic su **Approve/Deny** (Approva/Rifiuta).
4. Nella finestra di dialogo **Approva o rifiuta script** selezionare **Approva** o **Nega** per lo script. Facoltativamente, immettere un commento sulla decisione.  Se si rifiuta uno script, questo non può essere eseguito sui dispositivi client. <br>
![Script - Approvazione](./media/run-scripts/RS-approval.png)
1. Completare la procedura guidata. Nell'elenco **Script** la colonna **Stato dell'approvazione** cambia a seconda dell'azione eseguita.

### <a name="allow-users-to-approve-their-own-scripts"></a>Consentire agli utenti di approvare i propri script

Questa approvazione viene usata principalmente per la fase di test dello sviluppo di script.

1. Nella console di Configuration Manager fare clic su **Amministrazione**.
2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.
3. Nell'elenco dei siti selezionare il sito e quindi scegliere la scheda **Home** nel gruppo **Siti** e fare clic su **Impostazioni gerarchia**.
4. Nella scheda **Generale** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** deselezionare la casella di controllo **Do not allow script authors to approve their own scripts** (Non consentire agli autori di script di approvare i propri script).

>[!IMPORTANT]
>Come procedura consigliata, non consentire a un autore di script di approvare i propri script. Ciò deve essere consentito solo in un ambiente di prova. Valutare con attenzione il potenziale impatto della modifica di questa impostazione in un ambiente di produzione.

## <a name="security-scopes"></a>ambiti di protezione
*Introdotti con la versione 1710*  
La funzionalità Esegui script usa gli ambiti di protezione, una caratteristica esistente di Configuration Manager, per controllare la creazione e l'esecuzione di script tramite l'assegnazione di tag che rappresentano gruppi di utenti. Per altre informazioni sull'uso degli ambiti di protezione, vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Creare ruoli di sicurezza per gli script
I tre ruoli di sicurezza usati per l'esecuzione di script non vengono creati per impostazione predefinita in Configuration Manager. Per creare i ruoli di esecutori di script, autori di script e responsabili dell'approvazione di script seguire i passaggi descritti.

1. Nella console di Configuration Manager passare a **Amministrazione** >**Protezione** >**Ruoli di protezione**
2. Fare clic con il pulsante destro del mouse su un ruolo e selezionare **Copia**. Il ruolo copiato ha le autorizzazioni già assegnate. Verificare di includere solo le autorizzazioni desiderate. 
3. Assegnare al ruolo personalizzato un **nome** e una **descrizione**. 
4. Assegnare al ruolo di sicurezza le autorizzazioni indicate di seguito. 

    ### <a name="security-role-permissions"></a>**Autorizzazioni del ruolo di sicurezza**

     **Nome del ruolo**: esecutori di script
    - **Descrizione**: queste autorizzazioni consentono a questo ruolo solo di eseguire script precedentemente creati e approvati da altri ruoli. 
    - **Autorizzazioni:** verificare che le autorizzazioni seguenti siano impostate su **Sì**.
         |**Categoria**|**Autorizzazione**|**Stato**|
         |---|---|---|
         |Raccolta|Esegui script|Sì|
         |Script SMS|Creazione|Sì|
         |Script SMS|Lettura|Sì|

     **Nome del ruolo**: autori di script
    - **Descrizione**: queste autorizzazioni consentono a questo ruolo di creare script, ma non di approvarli o eseguirli. 
    - **Autorizzazioni**: verificare che siano impostate le autorizzazioni seguenti.
    - 
         |**Categoria**|**Autorizzazione**|**Stato**|
         |---|---|---|
         |Raccolta|Esegui script|No|
         |Script SMS|Creazione|Sì|
         |Script SMS|Lettura|Sì|
         |Script SMS|Elimina|Sì|
         |Script SMS|Modifica|Sì|

    **Nome del ruolo**: autori di script
    - **Descrizione**: queste autorizzazioni consentono a questo ruolo di approvare script, ma non di crearli o eseguirli. 
    - **Autorizzazioni:** verificare che siano impostate le autorizzazioni seguenti.

         |**Categoria**|**Autorizzazione**|**Stato**|
         |---|---|---|
         |Raccolta|Esegui script|No|
         |Script SMS|Lettura|Sì|
         |Script SMS|Approva|Sì|
         |Script SMS|Modifica|Sì|
     
**Esempio di autorizzazioni Script SMS per il ruolo di autori di script**

 ![Esempio di autorizzazioni Script SMS per il ruolo di autori di script](./media/run-scripts/script_authors_permissions.png)

   

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
5. Completare la procedura guidata. Il nuovo script viene visualizzato nell'elenco **Script** con stato **In attesa di approvazione** . Prima di poter eseguire questo script nei dispositivi client, è necessario approvarlo. 

> [!IMPORTANT]
    >Evitare di creare uno script per il riavvio del dispositivo o il riavvio dell'agente di Configuration Manager quando si usa la funzionalità Esegui script. Questa operazione potrebbe causare uno stato di riavvio continuo. Se necessario, sono disponibili miglioramenti delle funzionalità di notifica client che supportano il riavvio dei dispositivi, a partire da Configuration Manager versione 1710. La [colonna Riavvio in sospeso](/sccm/core/clients/manage/manage-clients#Restart-clients) può essere utile per identificare i dispositivi che richiedono un riavvio. 
<!--SMS503978  -->

## <a name="script-parameters"></a>Parametri di script
*Introdotti con la versione 1710*  
L'aggiunta di parametri a uno script offre maggiore flessibilità per ogni attività. La sezione seguente descrive le attuali caratteristiche della funzionalità Esegui script con i parametri di script per tipi di dati *String* e *Integer*. Sono disponibili anche gli elenchi dei valori preimpostati. Se lo script ha tipi di dati non supportati, verrà generato un avviso.

Nella finestra di dialogo **Crea script** fare clic su **Parametri script** in **Script**.

Ognuno dei parametri di script è associato a una finestra di dialogo per l'aggiunta di altri dettagli e la convalida.

>[!IMPORTANT]
> Nei valori dei parametri non è consentito l'apostrofo. 


### <a name="parameter-validation"></a>Convalida dei parametri

Ogni parametro nello script ha una finestra di dialogo **Proprietà parametri script**, in cui è possibile aggiungere la convalida per il parametro. Dopo aver aggiunto la convalida, verranno restituiti errori quando si immette un valore che non soddisfa i requisiti di convalida per il parametro.

#### <a name="example-firstname"></a>Esempio: *FirstName*

In questo esempio è possibile impostare le proprietà del parametro stringa *FirstName*.

![Parametri di script - Stringa](./media/run-scripts/RS-parameters-string.png)


La sezione di convalida della finestra di dialogo **Proprietà dei parametri dello script** contiene i campi seguenti:

- **Lunghezza minima** - Numero minimo di caratteri del campo *FirstName*.
- **Lunghezza massima** - Numero massimo di caratteri del campo *FirstName*.
- **RegEx** - abbreviazione di *Espressione regolare*. Per altre informazioni sull'uso di espressioni regolari, vedere la sezione successiva *Uso della convalida con espressioni regolari*.
- **Errore personalizzato** - Utile per aggiungere un messaggio di errore personalizzato che sostituirà qualsiasi messaggio di errore di convalida del sistema.

#### <a name="using-regular-expression-validation"></a>Uso della convalida con espressioni regolari

Un'espressione regolare è una forma di programmazione compatta per controllare una stringa di caratteri rispetto a una convalida codificata. Ad esempio, si potrebbe verificare se manca un carattere alfabetico maiuscolo nel campo *FirstName* inserendo `[^A-Z]` nel campo *RegEx*.

L'elaborazione delle espressioni regolari per questa finestra di dialogo è supportata da .NET Framework. Per informazioni sull'uso delle espressioni regolari, vedere [Espressioni regolari di .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Esempi di script

Ecco alcuni esempi che mostrano gli script che è possibile usare con questa funzionalità.

### <a name="create-a-new-folder-and-file"></a>Creare una nuova cartella e un file

Questo script crea una nuova cartella e un file all'interno della cartella in base ai nomi specificati.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName,
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Recuperare la versione del sistema operativo

Questo script usa WMI per richiedere la versione del sistema operativo al computer.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Esegui uno script

Dopo l'approvazione, uno script può essere eseguito su un singolo dispositivo o su una raccolta. Una volta avviata l'esecuzione, lo script viene eseguito rapidamente in un sistema ad alta priorità con timeout di un'ora. I risultati dello script vengono quindi restituiti tramite un sistema di messaggi di stato.

Per selezionare una raccolta di destinazioni per lo script:

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro Asset e conformità fare clic su **Raccolte dispositivi**.
3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta di dispositivi in cui si desidera eseguire lo script.
4. Selezionare una raccolta a scelta e fare clic su **Esegui script**.
5. Nella pagina **Script** della procedura guidata **Esegui Script** scegliere uno script dall'elenco. Vengono visualizzati solo gli script approvati.
6. Fare clic su **Avanti** e completare la procedura guidata.

>[!IMPORTANT]
>Se lo script non viene eseguito, ad esempio perché il client di destinazione è spento entro il periodo di tempo di un'ora, è necessario eseguirlo di nuovo.

### <a name="target-machine-execution"></a>Esecuzione nel computer di destinazione

Lo script viene eseguito come account di *sistema* o *computer* nei client di destinazione. Questo account ha accesso di rete limitato. L'accesso dello script a posizioni e sistemi remoti deve essere eseguito di conseguenza.

## <a name="script-monitoring"></a>Monitoraggio dello script

Dopo aver avviato l'esecuzione di uno script in una raccolta di dispositivi, usare la procedura seguente per monitorare l'operazione. A partire dalla versione 1710, è possibile monitorare uno script in tempo reale durante la sua esecuzione ed è anche possibile restituire un report per un'esecuzione della funzionalità Esegui script specifica. <br>

![Monitoraggio dello script - Stato di esecuzione dello script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** fare clic su **Stato script**.
3. Nell'elenco **Stato script** sono visualizzati i risultati per ogni script eseguito nei dispositivi client. Un codice di uscita dello script uguale a **0** indica in genere che lo script è stato eseguito correttamente.
    - A partire da Configuration Manager 1802, l'output dello script viene troncato in corrispondenza di 4 KB per consentire una migliore esperienza di visualizzazione.  <!--510013-->
      ![Monitoraggio script - Script troncato](./media/run-scripts/Script-monitoring-truncated.png) 

## <a name="script-output"></a>Output dello script

- A partire da Configuration Manager versione 1802, l'output dello script viene restituito con la formattazione JSON. Questo formato restituisce in modo coerente un output dello script leggibile. 
- Gli script con un risultato sconosciuto o dove il client era offline, non vengono visualizzati nei grafici o nel set di dati. <!--507179-->
- Evitare di restituire un output troppo grande poiché verrà troncato in corrispondenza di 4 KB. <!--508488-->
- Alcune funzionalità con la formattazione dell'output dello script non sono disponibili quando si esegue Configuration Manager versione 1802 o successiva con una versione di livello inferiore del client. <!--508487-->
    - Con un client di Configuration Manager precedente alla versione 1802 viene restituito un output di stringhe.
    -  Con un client di Configuration Manager versione 1802 e successive viene restituita la formattazione JSON.
        - Ad esempio, si può ottenere il risultato TEXT in una versione del client e "TEXT", ovvero con l'output racchiuso tra virgolette doppie, in un'altra versione. Questi risultati verranno inseriti nel grafico come due categorie diverse.
        - Se questo comportamento costituisce un problema, prendere in considerazione l'esecuzione dello script su due raccolte diverse. Una con i client precedenti alla versione 1802 e un'altra con i client 1802 e versioni successive. In alternativa, è possibile convertire un oggetto enum in un valore stringa negli script in modo da visualizzarlo correttamente nella formattazione JSON. 
- Convertire un oggetto enum in un valore stringa negli script in modo da visualizzarlo correttamente nella formattazione JSON. <!--508377--> ![Convertire un oggetto enum in un valore stringa](./media/run-scripts/enum-tostring-JSON.png)



## <a name="see-also"></a>Vedere anche

- [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration)
