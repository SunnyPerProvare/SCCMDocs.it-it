---
title: Distribuire applicazioni | Microsoft Docs
description: Creare un tipo di distribuzione o simulare la distribuzione di un&quot;applicazione usando System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 23b1d24e908d04b64c3bbfa518793a44e696d468
ms.openlocfilehash: 0eaa1d13e9c273a6649f50d73fb357f04464d94c
ms.lasthandoff: 03/29/2017


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Distribuire le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 Prima di distribuire un'applicazione di System Center Configuration Manager è necessario creare almeno un tipo di distribuzione per l'applicazione stessa. Per altre informazioni sulla creazione di applicazioni e tipi di distribuzione, vedere [Create applications ](../../apps/deploy-use/create-applications.md) (Creare applicazioni).

 È anche possibile simulare la distribuzione di un'applicazione. Questo tipo di distribuzione sottopone a test l'applicabilità di una distribuzione di applicazione nei computer senza installare o disinstallare l'applicazione. Una distribuzione simulata esegue una valutazione del metodo di rilevamento, dei requisiti e delle dipendenze per un tipo di distribuzione e segnala i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Per altre informazioni, vedere [Simulate application deployments ](../../apps/deploy-use/simulate-application-deployments.md) (Simulare le distribuzioni di applicazioni).

> [!IMPORTANT]
>  È possibile distribuire (installare o disinstallare) le applicazioni necessarie, ma non pacchetti o aggiornamenti software. I dispositivi registrati con MDM non supportano nemmeno le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.

## <a name="deploy-an-application"></a>Distribuire un'applicazione

1.  Nella console di Configuration Manager accedere a **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.

2.  Nell'elenco **Applicazioni** selezionare l'applicazione che si desidera distribuire. Quindi, nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.

### <a name="specify-general-information-about-the-deployment"></a>Specificare le informazioni generali sulla distribuzione

Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:

- **Software**: visualizza l'applicazione da distribuire. È possibile fare clic su **Sfoglia** per selezionare un'altra applicazione.
- **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui distribuire l'applicazione.
- **Usa gruppi di punti di distribuzione predefiniti associati a questa raccolta**: selezionare questa opzione per archiviare il contenuto dell'applicazione nel gruppo di punti di distribuzione predefinito della raccolta. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione è disattivata.
- **Distribuisci automaticamente contenuto per dipendenze**: se l'opzione è attivata e uno dei tipi di distribuzione dell'applicazione contiene dipendenze, anche il contenuto dell'applicazione dipendente verrà inviato ai punti di distribuzione.

    >[!IMPORTANT]
    > Se l'applicazione dipendente viene aggiornata dopo la distribuzione dell'applicazione primaria, il nuovo contenuto per la dipendenza non verrà distribuito automaticamente.

- **Commenti (facoltativo)** : immettere una descrizione facoltativa della distribuzione.

### <a name="specify-content-options-for-the-deployment"></a>Specificare le opzioni di contenuto per la distribuzione

Nella pagina **Contenuto** fare clic su **Aggiungi** per aggiungere il contenuto associato a questa distribuzione ai punti di distribuzione o ai gruppi di punti di distribuzione. Se è stata selezionata l'opzione **Use default distribution points associated to this collection** (Usa gruppi di punti di distribuzione predefiniti associati a questa raccolta) nella pagina **Generale**, l'opzione verrà popolata automaticamente e potrà essere modificata solo da un membro del ruolo di sicurezza Amministratore applicazione.

### <a name="specify-deployment-settings"></a>Specificare le impostazioni di distribuzione

Nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software specificare le informazioni seguenti:

- **Azione**: dall'elenco a discesa scegliere se la distribuzione ha l'obiettivo di **installare** o **disinstallare** l'applicazione.

    > [!NOTE]
    >  Se un'applicazione viene distribuita due volte in un dispositivo, una volta con l'azione **Installa** e una volta con l'azione **Disinstalla**, avrà priorità la distribuzione dell'applicazione con l'azione **Installa** .

È impossibile modificare l'azione di una distribuzione dopo la relativa creazione.

- **Scopo**: dall'elenco a discesa scegliere una delle seguenti opzioni:
    - **Disponibile**: se l'applicazione viene distribuita a un utente, l'utente visualizza l'applicazione pubblicata in Software Center e può installarla su richiesta.
    - **Richiesto**: l'applicazione viene distribuita automaticamente in base alla pianificazione. Se lo stato della distribuzione dell'applicazione non è nascosto, chiunque usi l'applicazione può tenere traccia dello stato della distribuzione e installare l'applicazione da Software Center prima della scadenza.

    > [!NOTE]   
    >  Quando l'azione di distribuzione è impostata su **Disinstalla**, lo scopo della distribuzione viene impostato automaticamente su **Richiesto** e non può essere modificato.  

- **Distribuisci automaticamente in base alla pianificazione con o senza accesso utente**: se la distribuzione è destinata a un utente, selezionare questa opzione per distribuire l'applicazione nei dispositivi primari dell'utente. Questa impostazione non richiede all'utente di accedere prima che venga eseguita la distribuzione. Non selezionare questa opzione se l'utente deve fornire input per completare l'installazione. Questa opzione è disponibile solo quando la distribuzione ha lo scopo **Richiesto**.


- **Invia pacchetti di riattivazione**: se lo scopo della distribuzione è impostato su **Richiesto** e l'opzione è selezionata, ai computer viene inviato un pacchetto di riattivazione prima dell'installazione della distribuzione. Il pacchetto attiva i computer nel momento in cui scade l'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.
- **Tutti i client devono usare una connessione di rete a consumo per scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo ulteriore**: questa opzione è disponibile solo per le distribuzioni con lo scopo **Richiesto**.
- **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**: per altre informazioni su come configurare un elenco di file eseguibili che impediscano l'installazione di un'applicazione, vedere **Come controllare l'esecuzione di file eseguibili prima di installare un'applicazione** più avanti in questo argomento.
- **Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione**: se l'opzione è selezionata, prima dell'installazione dell'applicazione l'amministratore deve approvare tutte le relative richieste degli utenti. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando l'applicazione viene distribuita in una raccolta dispositivi.

    > [!NOTE]
    >  Le richieste di approvazione dell'applicazione vengono visualizzate nel nodo **Richieste di approvazione** , in **Gestione applicazioni** , nell'area di lavoro **Raccolta software** . Se una richiesta non viene approvata entro 45 giorni, verrà rimossa. La reinstallazione del client di Configuration Manager potrebbe anche annullare eventuali richieste di approvazione in sospeso.
    >  Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager (in precedenza questo pulsante era disabilitato dopo l'approvazione).
    >  Questa azione non comporta la disinstallazione dell'applicazione dai dispositivi, ma impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.



- **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione**: se l'opzione è selezionata, le versioni sostituite dell'applicazione verranno aggiornate con l'applicazione sostitutiva.

### <a name="specify-scheduling-settings-for-the-deployment"></a>Specificare le impostazioni di pianificazione per la distribuzione

Nella pagina **Pianificazione** della Distribuzione guidata del software configurare il momento in cui l'applicazione verrà distribuita o sarà disponibile per i dispositivi client.
Le opzioni presenti in questa pagina varieranno in base all'impostazione dell'azione di distribuzione, che può essere **Disponibile** o **Richiesto**.

In alcuni casi, è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti del software obbligatori, anche oltre eventuali scadenze impostate. In genere questo è necessario quando un computer è stato disattivato per un lungo periodo di tempo ed è necessario installare un numero elevato di aggiornamenti o distribuzioni di applicazioni. Ad esempio, se un utente è appena tornato da una vacanza, potrebbe dover attendere parecchio tempo mentre vengono installate le distribuzioni delle applicazioni scadute. Per risolvere il problema ora è possibile definire un periodo di tolleranza di imposizione distribuendo le impostazioni del client di Configuration Manager a una raccolta.

Per configurare il periodo di tolleranza eseguire le operazioni seguenti:

- Nella pagina **Agente computer** delle impostazioni del client configurare la nuova proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** con un valore compreso tra **1** e **120** ore.
- Nella pagina **Pianificazione** di una nuova distribuzione richiesta dell'applicazione o nelle proprietà di una distribuzione esistente selezionare l'opzione che consente di **ritardare l'imposizione della distribuzione in base alle preferenze dell'utente fino al periodo di tolleranza definito nelle impostazioni client**. Tale periodo di tolleranza viene usato per tutte le distribuzioni con questa opzione selezionata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client.

Alla scadenza dell'installazione, l'applicazione verrà installata nella prima finestra non aziendale che l'utente ha configurato fino alla scadenza del periodo di tolleranza specificato. Tuttavia l'utente può comunque aprire Software Center e installare l'applicazione in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.

Se l'applicazione distribuita sostituisce un'altra applicazione, è possibile impostare la scadenza dell'installazione nel momento in cui gli utenti ricevono la nuova applicazione. A tale scopo usare l'impostazione **Scadenza installazione** per aggiornare gli utenti con l'applicazione sostituita.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Specificare le impostazioni dell'esperienza utente per la distribuzione


Nella pagina **Esperienza utente** della Distribuzione guidata del software specificare le informazioni sulle modalità di interazione degli utenti con l'installazione dell'applicazione.

Quando si distribuiscono applicazioni in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'applicazione nella sovrapposizione temporanea e confermare le modifiche in seguito oppure confermarle alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario riavviare il dispositivo. Le modifiche vengono mantenute nel dispositivo.

>[!NOTE]
    >  Quando si distribuisce un'applicazione in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata. Per altre informazioni sull'uso delle finestre di manutenzione quando si distribuiscono applicazioni in dispositivi con Windows Embedded, vedere [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md) (Creare applicazioni Windows Embedded).
    > Le opzioni **Installazione software** e **Riavvio del sistema (se richiesto per completare l'installazione)** non vengono usate se lo scopo della distribuzione è impostato su **Disponibile**. È inoltre possibile configurare il livello di notifica visualizzato dall'utente durante l'installazione dell'applicazione.

### <a name="specify-alert-options-for-the-deployment"></a>Specificare le opzioni di avviso per la distribuzione

Nella pagina **Avvisi** della Distribuzione guidata del software impostare la modalità in cui Configuration Manager e System Center Operations Manager dovranno generare gli avvisi relativi alla distribuzione. È possibile configurare le soglie di reporting degli avvisi e disattivare il reporting per tutta la durata della distribuzione.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associare la distribuzione a un criterio di configurazione dell'app iOS

Nella pagina **Criteri di configurazione dell'app** fare clic su **Nuovo** per associare questa distribuzione a un criterio di configurazione dell'app iOS, se ne è stato creato uno. Per altre informazioni su questo tipo di criteri, vedere [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurare le app iOS con i criteri di configurazione delle app).

### <a name="finish-up"></a>Terminare

Nella pagina **Riepilogo** della Distribuzione guidata del software esaminare le azioni che verranno eseguite dalla distribuzione e quindi fare clic su **Avanti** per terminare la procedura guidata.

La nuova distribuzione verrà visualizzata nell'elenco **Distribuzioni** del nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** . È possibile modificare le proprietà di questa distribuzione o eliminare la distribuzione dalla scheda **Distribuzioni** del riquadro dettagli dell'applicazione.

## <a name="delete-an-application-deployment"></a>Eliminare la distribuzione di un'applicazione

1.  Nella console di Configuration Manager accedere a **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.

3.  Nell'elenco **Applicazioni** selezionare l'applicazione che include la distribuzione da eliminare.

4.  Nella scheda **Distribuzioni** dell'elenco *<nome applicazione\>* selezionare la distribuzione dell'applicazione da eliminare. Quindi, fare clic su **Elimina** nel gruppo **Distribuzione** della scheda **Distribuzione**.

 Quando si elimina la distribuzione di un'applicazione, tutte le istanze dell'applicazione già installate non vengono rimosse. Per rimuovere queste applicazioni, è necessario distribuire l'applicazione nei computer con **Disinstalla**. Se si elimina la distribuzione di un'applicazione o si rimuove una risorsa dalla raccolta in cui si vuole eseguire la distribuzione, l'applicazione non sarà più visibile in Software Center.

## <a name="user-notifications-for-required-deployments"></a>Notifiche utente per le distribuzioni richieste
Quando si riceve il software necessario, dall'impostazione **Posponi e ricorda tra:** è possibile selezionare un'opzione dall'elenco di valori a discesa seguente:
- **In seguito**: specifica che le notifiche sono programmate in base alle impostazioni di notifica configurate nelle impostazioni dell'agente client.
- **Orario fisso**: specifica che è programmata una nuova visualizzazione della notifica dopo l'orario selezionato. Ad esempio, se si seleziona 30 minuti, la notifica verrà visualizzata di nuovo dopo 30 minuti.

![Pagina dell'agente computer nelle impostazioni dell'agente client](media/ComputerAgentSettings.png)

Il tempo di posticipo massimo è sempre basato sui valori di notifica configurati nelle impostazioni dell'agente client su ogni orario presente lungo la cronologia di distribuzione. Ad esempio, se l'impostazione **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** della pagina **Agente computer** è configurata per 10 ore e alla scadenza mancano più di 24 ore, all'avvio della finestra di dialogo viene visualizzato un gruppo di opzioni di posticipo mai superiori a 10 ore. Man mano che si avvicina la scadenza, la finestra di dialogo mostra un numero minore di opzioni coerente con le impostazioni dell'agente client pertinente per ogni componente della cronologia di distribuzione.

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente è ora più invasiva. Ogni volta che si riceve una notifica in relazione alla necessità di manutenzione critica del software, anziché una notifica temporanea sulla barra delle applicazioni viene visualizzata nel computer una finestra di dialogo simile alla seguente:

![Finestra di dialogo del software richiesto](media/client-toast-notification.png)

## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Come controllare l'esecuzione di file eseguibili prima di installare un'applicazione

>[!Tip]
>Introdotta con la versione 1702, è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](https://docs.microsoft.com/sccm/core/servers/manage/pre-release-features).

Nella finestra di dialogo **Proprietà** di un tipo di distribuzione, nella scheda **Comportamento installazione**, è possibile specificare uno o più file eseguibili che, se in esecuzione, bloccano l'installazione del tipo di distribuzione. L'utente deve chiudere il file eseguibile in esecuzione, che in alternativa può essere chiuso automaticamente per le distribuzioni con scopo richiesto, prima dell'installazione del tipo di distribuzione. Per configurare questa impostazione:

1. Aprire la finestra di dialogo **Proprietà** per qualsiasi tipo di distribuzione.
2. Nella scheda **Comportamento di installazione** della finestra di dialogo *<deployment type name>* **Proprietà** fare clic su **Aggiungi**.
3. Nella finestra di dialogo **Aggiungi un file eseguibile/Modifica il file eseguibile** immettere il nome del file eseguibile che, se in esecuzione, bloccherà l'installazione dell'applicazione. Facoltativamente, è anche possibile immettere un nome descrittivo per l'applicazione in modo da identificarla più facilmente nell'elenco.
4. Fare clic su **OK** e chiudere la finestra di dialogo *<deployment type name>* **Proprietà**.
5. Se si distribuisce un'applicazione, nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software selezionare **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** e continuare la procedura di distribuzione dell'applicazione.

Quando l'applicazione raggiunge i PC client, si verifica il comportamento seguente:

- Se l'applicazione è stata distribuita come **Disponibile** e un utente finale prova a installarla, verrà chiesto di chiudere tutti i file eseguibili in esecuzione specificati, prima di poter procedere con l'installazione.

- Se l'applicazione è stata distribuita come **Richiesta** e l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** è selezionata, verrà visualizzata una finestra di dialogo che informa che i file eseguibili specificati verranno chiusi automaticamente quando viene raggiunta la scadenza dell'installazione dell'applicazione. È possibile pianificare queste finestre di dialogo in **Impostazioni client** > **Agente computer**. Se non si vuole che l'utente finale visualizzi questi messaggi, selezionare **Nascondi in Software Center e nascondi tutte le notifiche** nella scheda **Esperienza utente** delle proprietà di distribuzione.

- Se l'applicazione è stata distribuita come **Richiesta** e l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione** non è selezionata, l'installazione dell'applicazione avrà esito negativo se sono in esecuzione una o più applicazioni tra quelle specificate.

## <a name="for-more-information"></a>Per ulteriori informazioni:
- [Impostazioni per gestire le distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md)

