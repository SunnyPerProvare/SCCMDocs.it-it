---
title: Distribuire applicazioni
titleSuffix: Configuration Manager
description: Creare o simulare la distribuzione di un'applicazione a una raccolta di utenti o dispositivi
ms.custom: na
ms.date: 03/22/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0101ba0eade5775577f52920f301a782afd7bbda
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Distribuire le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Creare o simulare la distribuzione di un'applicazione a una raccolta di utenti o dispositivi in Configuration Manager. La distribuzione specifica istruzioni per il client di Configuration Manager su come e quando installare il software. 

Prima di distribuire un'applicazione, creare almeno un tipo di distribuzione per l'applicazione. Per altre informazioni, vedere [Create applications](/sccm/apps/deploy-use/create-applications) (Creare le applicazioni).

 È anche possibile simulare la distribuzione di un'applicazione. La simulazione verifica l'applicabilità di una distribuzione senza installare o disinstallare l'applicazione. Una distribuzione simulata esegue una valutazione del metodo di rilevamento, dei requisiti e delle dipendenze per un tipo di distribuzione e segnala i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Per altre informazioni, vedere [Simulare distribuzioni di applicazioni ](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  È possibile simulare la distribuzione di applicazioni necessarie, ma non di pacchetti o aggiornamenti software.   
>  I dispositivi registrati con MDM non supportano le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.



## <a name="deploy-an-application"></a>Distribuire un'applicazione

1.  Nella console di Configuration Manager accedere a **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.

2.  Nell'elenco **Applicazioni** selezionare l'applicazione che si desidera distribuire. Quindi, nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.

### <a name="specify-general-information-about-the-deployment"></a>Specificare le informazioni generali sulla distribuzione

Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:

- **Software**: visualizza l'applicazione da distribuire. Fare clic su **Sfoglia** per selezionare un'altra applicazione.
- **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui distribuire l'applicazione.
- **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**: consente di archiviare il contenuto dell'applicazione nel gruppo di punti di distribuzione predefinito della raccolta. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione è disattivata.
- **Distribuisci automaticamente contenuto per dipendenze**: se uno dei tipi di distribuzione dell'applicazione contiene dipendenze, il sito invia anche il contenuto dell'applicazione dipendente ai punti di distribuzione.

    >[!IMPORTANT]
    > Se l'applicazione dipendente viene aggiornata dopo la distribuzione dell'applicazione primaria, il sito non distribuisce automaticamente il nuovo contenuto per la dipendenza.

- **Commenti (facoltativo)**: immettere una descrizione facoltativa della distribuzione.

### <a name="specify-content-options-for-the-deployment"></a>Specificare le opzioni di contenuto per la distribuzione

Nella pagina **Contenuto** fare clic su **Aggiungi** per aggiungere il contenuto associato a questa distribuzione ai punti di distribuzione o ai gruppi di punti di distribuzione. Se si seleziona **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta** nella pagina **Generale**, questa opzione viene popolata automaticamente. Solo un membro del ruolo di sicurezza Amministratore applicazione può modificarlo.

### <a name="specify-deployment-settings"></a>Specificare le impostazioni di distribuzione

Nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software specificare le informazioni seguenti:

- **Azione**: dall'elenco a discesa scegliere **Installa** o **Disinstalla** perché la distribuzione installi o disinstalli l'applicazione.

    > [!NOTE]
    >  Se un'applicazione viene distribuita due volte in un dispositivo, una volta con l'azione **Installa** e una volta con l'azione **Disinstalla**, ha priorità la distribuzione dell'applicazione con l'azione **Installa**.

  Non è possibile modificare l'azione di una distribuzione dopo averla creata.

- **Scopo**: dall'elenco a discesa scegliere una delle opzioni seguenti:  
    - **Disponibile**: se l'applicazione viene distribuita a un utente, l'utente visualizza l'applicazione pubblicata in Software Center e può installarla su richiesta.
    - **Richiesto**: l'applicazione viene distribuita automaticamente in base alla pianificazione. Se lo stato della distribuzione dell'applicazione non è nascosto, chiunque usi l'applicazione può tenere traccia dello stato della distribuzione e installare l'applicazione da Software Center prima della scadenza.

    > [!NOTE]   
    >  Quando l'azione di distribuzione è impostata su **Disinstalla**, lo scopo della distribuzione viene impostato automaticamente su **Richiesto**. Non è possibile modificare questo comportamento.  

- **Deploy automatically according to schedule whether or not a user is logged on** (Distribuisci automaticamente in base alla pianificazione con o senza accesso utente): se la distribuzione è destinata a un utente, selezionare questa opzione per distribuire l'applicazione nei dispositivi primari dell'utente. Questa impostazione non richiede all'utente di accedere prima che venga eseguita la distribuzione. Non selezionare questa opzione se l'utente deve interagire con l'installazione. Questa opzione è disponibile solo quando la distribuzione ha lo scopo **Richiesto**.

- **Invia pacchetti di riattivazione**: se lo scopo della distribuzione è impostato su **Richiesto**, ai computer viene inviato un pacchetto di riattivazione prima che il client esegua la distribuzione. Il pacchetto attiva i computer nel momento in cui scade l'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per la riattivazione LAN.
- **Consente a tutti i client che utilizzano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**: questa opzione è disponibile solo per le distribuzioni con scopo **Richiesto**.
- **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**: per altre informazioni, vedere [Come controllare l'esecuzione di file eseguibili prima di installare un'applicazione](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione**: per la versione 1710 e versioni precedenti, l'amministratore approva tutte le richieste degli utenti per l'applicazione prima che l'utente la installi. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando l'applicazione viene distribuita in una raccolta di dispositivi.  

    > [!NOTE]
    >  Le richieste di approvazione dell'applicazione vengono visualizzate nel nodo **Richieste di approvazione** , in **Gestione applicazioni** , nell'area di lavoro **Raccolta software** . Se una richiesta non viene approvata entro 45 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  
    >  Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Questa azione non comporta la disinstallazione dell'applicazione dai dispositivi da parte del client, ma impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.

- **Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo**: a partire dalla versione 1802, l'amministratore approva tutte le richieste utente per l'applicazione prima che l'utente la installi nel dispositivo richiesto. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando l'applicazione viene distribuita in una raccolta di dispositivi. <!--1357015-->  

    Si tratta di una funzionalità facoltativa. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti). Se questa funzionalità non è abilitata, sarà valida l'opzione precedente.  

    > [!Important]  
    > Anche la versione del client di Configuration Manager deve essere la 1802. È necessario anche usare il nuovo Software Center.  

    > [!Note]  
    > Nell'area di lavoro **Raccolta software** della console di Configuration Manager visualizzare **Richieste di approvazione** in **Gestione applicazioni**. Nell'elenco è ora presente una colonna **Dispositivo** per ogni richiesta. Quando si intraprende un'azione sulla richiesta, la finestra di dialogo Richiesta di applicazioni include anche il nome del dispositivo da cui l'utente ha inviato la richiesta.  
    >  Se una richiesta non viene approvata entro 45 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  
    >  Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Questa azione non comporta la disinstallazione dell'applicazione dai dispositivi da parte del client, ma impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.

- **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione**: il client aggiorna le versioni sostituite dell'applicazione con l'applicazione sostitutiva.    

    > [!NOTE]  
    > A partire dalla versione 1802, per lo scopo di installazione **Disponibile** oppure **Richiesto**, è possibile abilitare o disabilitare questa opzione. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Specificare le impostazioni di pianificazione per la distribuzione

Nella pagina **Pianificazione** della Distribuzione guidata del software configurare il momento in cui l'applicazione deve essere distribuita o resa disponibile per i dispositivi client.
Le opzioni presenti in questa pagina variano in base all'impostazione dell'azione di distribuzione, che può essere **Disponibile** o **Richiesta**.

In alcuni casi, è possibile concedere agli utenti più tempo per l'installazione di distribuzioni di applicazioni o aggiornamenti del software obbligatori, anche oltre eventuali scadenze impostate. Questo comportamento è in genere necessario quando un computer è stato disattivato per molto tempo ed è necessario installare molte applicazioni. Ad esempio, quando un utente torna da una vacanza, potrebbe dover attendere parecchio tempo mentre vengono installate le distribuzioni delle applicazioni scadute. Per risolvere il problema ora è possibile definire un periodo di tolleranza di imposizione distribuendo le impostazioni del client di Configuration Manager a una raccolta.

Per configurare il periodo di tolleranza eseguire le operazioni seguenti:

- Nella pagina **Agente computer** delle impostazioni del client configurare la nuova proprietà **Periodo di tolleranza per l'imposizione dopo la scadenza della distribuzione (ore)** con un valore compreso tra **1** e **120** ore.
- Nella pagina **Pianificazione** di una distribuzione richiesta dell'applicazione scegliere l'opzione **Ritardare l'imposizione di questa distribuzione in base alle preferenze dell'utente, fino al periodo di tolleranza massimo definito nelle impostazioni del client**. Tale periodo di tolleranza si applica a tutte le distribuzioni con questa opzione abilitata e destinate a dispositivi in cui è stata distribuita anche l'impostazione del client.

Alla scadenza dell'installazione, il client installa l'applicazione nella prima finestra non aziendale, configurata dall'utente, fino alla scadenza del periodo di tolleranza. Tuttavia l'utente può comunque aprire Software Center e installare l'applicazione in qualsiasi momento. Una volta scaduto il periodo di tolleranza, le distribuzioni scadute torneranno al normale comportamento.

Se l'applicazione distribuita sostituisce un'altra applicazione, è possibile impostare la scadenza dell'installazione in corrispondenza del momento in cui gli utenti ricevono la nuova applicazione. Per aggiornare gli utenti con l'applicazione sostituita, impostare la **Scadenza installazione**.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Specificare le impostazioni dell'esperienza utente per la distribuzione

Nella pagina **Esperienza utente** della Distribuzione guidata del software specificare le informazioni sulle modalità di interazione degli utenti con l'installazione dell'applicazione.

Quando si distribuiscono applicazioni in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'applicazione nella sovrimpressione temporanea ed eseguire il commit delle modifiche in un secondo momento. È anche possibile specificare di eseguire il commit delle modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Se si esegue il commit delle modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario riavviare il dispositivo. Le modifiche vengono mantenute nel dispositivo.

>[!NOTE]
    >  Quando si distribuisce un'applicazione in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione e sui dispositivi con Windows Embedded, vedere [Creare applicazioni Windows Embedded con System Center Configuration Manager](../../apps/get-started/creating-windows-embedded-applications.md).
    > Le opzioni **Installazione software** e **Riavvio del sistema (se richiesto per completare l'installazione)** non vengono usate se lo scopo della distribuzione è impostato su **Disponibile**. È inoltre possibile configurare il livello di notifica visualizzato dall'utente durante l'installazione dell'applicazione.

### <a name="specify-alert-options-for-the-deployment"></a>Specificare le opzioni di avviso per la distribuzione

Nella pagina **Avvisi** della Distribuzione guidata del software impostare la modalità in cui Configuration Manager e System Center Operations Manager devono generare gli avvisi relativi alla distribuzione. È possibile configurare le soglie di reporting degli avvisi e disattivare il reporting per tutta la durata della distribuzione.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associare la distribuzione a un criterio di configurazione dell'app iOS

Nella pagina **Criteri di configurazione dell'app** fare clic su **Nuovo** per associare questa distribuzione a un criterio di configurazione dell'app iOS, se ne è stato creato uno. Per altre informazioni su questo tipo di criteri, vedere [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurare le app iOS con i criteri di configurazione delle app).

### <a name="deployment-properties"></a>Proprietà di distribuzione

Individuare la nuova distribuzione nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. È possibile modificare le proprietà di questa distribuzione o eliminare la distribuzione dalla scheda **Distribuzioni** del riquadro dettagli dell'applicazione.



## <a name="delete-an-application-deployment"></a>Eliminare la distribuzione di un'applicazione

1.  Nella console di Configuration Manager accedere a **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.
3.  Nell'elenco **Applicazioni** selezionare l'applicazione che include la distribuzione da eliminare.
4.  Nella scheda **Distribuzioni** dell'elenco *<nome applicazione\>* selezionare la distribuzione dell'applicazione da eliminare. Quindi, fare clic su **Elimina** nel gruppo **Distribuzione** della scheda **Distribuzione**.

Quando si elimina la distribuzione di un'applicazione, tutte le istanze dell'applicazione già installate non vengono rimosse. Per rimuovere queste applicazioni, è necessario distribuire l'applicazione nei computer con **Disinstalla**. Se si elimina la distribuzione di un'applicazione o si rimuove una risorsa dalla raccolta in cui si vuole eseguire la distribuzione, l'applicazione non è più visibile in Software Center.



## <a name="user-notifications-for-required-deployments"></a>Notifiche utente per le distribuzioni richieste
Quando si riceve il software necessario, dall'impostazione **Posponi e ricorda tra:** è possibile selezionare un'opzione dall'elenco di valori a discesa seguente:
- **In seguito**: specifica che le notifiche vengono programmate in base alle impostazioni di notifica configurate nelle impostazioni del client.
- **Fixed time** (Orario fisso): specifica che la notifica venga pianificata per una nuova visualizzazione dopo l'ora selezionata. Ad esempio, se si seleziona un periodo di 30 minuti, la notifica viene visualizzata di nuovo dopo 30 minuti.

![Gruppo Agente computer nelle impostazioni client predefinite](media/ComputerAgentSettings.png)

Il tempo di posticipo massimo è sempre basato sui valori di notifica configurati nelle impostazioni del client su ogni orario presente lungo la cronologia di distribuzione. Ad esempio:
- Viene configurata l'impostazione **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** nella pagina **Agente computer** per 10 ore.
- Il client visualizza la finestra di dialogo di notifica più di 24 ore prima della scadenza di distribuzione.
- La finestra di dialogo visualizza opzioni di posposizione fino a 10 ore ma mai superiori. 
- Quando la scadenza di distribuzione di avvicina, nella finestra di dialogo vengono visualizzate meno opzioni. Tali opzioni sono coerenti con le impostazioni del client pertinenti per ogni componente della scadenza di distribuzione.

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente è più invasiva. Anziché una notifica temporanea sulla barra delle applicazioni, viene visualizzata una finestra di dialogo simile alla seguente ogni volta che è necessaria una manutenzione critica del software:

![Finestra di dialogo software che notifica la necessità di una manutenzione critica del software](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Come controllare l'esecuzione di file eseguibili prima di installare un'applicazione

Nella finestra di dialogo **Proprietà** di un tipo di distribuzione specificare uno o più file eseguibili nella scheda **Comportamento di installazione**. Se uno di questi file eseguibili è in esecuzione nel client, l'installazione del tipo di distribuzione si blocca. L'utente deve chiudere il file eseguibile in esecuzione prima che il client installi il tipo di distribuzione. Per le distribuzioni con scopo Richiesto, il client può chiudere automaticamente il file eseguibile in esecuzione.

1. Aprire la finestra di dialogo **Proprietà** per qualsiasi tipo di distribuzione.
2. Nella scheda **Comportamento di installazione** della finestra di dialogo *<deployment type name>* **Proprietà** fare clic su **Aggiungi**.
3. Nella finestra di dialogo **Aggiungi un file eseguibile/Modifica il file eseguibile** immettere il nome del file eseguibile che, se in esecuzione, blocca l'installazione dell'applicazione. Facoltativamente, è anche possibile immettere un nome descrittivo per l'applicazione in modo da identificarla più facilmente nell'elenco.
4. Fare clic su **OK** e chiudere la finestra di dialogo *<deployment type name>* **Proprietà**.
5. Quando si distribuisce l'applicazione, nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software selezionare **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**.

Dopo che i client ricevono la distribuzione, si applica il comportamento seguente:

- Se l'applicazione è stata distribuita come **Disponibile** e un utente finale prova a installarla, il client chiede all'utente di chiudere tutti i file eseguibili in esecuzione specificati prima di procedere con l'installazione.

- Se l'applicazione è stata distribuita come **Richiesta** ed è stata specificata l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**, viene visualizzata una finestra di dialogo che informa che i file eseguibili specificati verranno chiusi automaticamente quando verrà raggiunta la scadenza dell'installazione dell'applicazione. È possibile pianificare queste finestre di dialogo in **Impostazioni client** > **Agente computer**. Se non si vuole che l'utente finale visualizzi questi messaggi, selezionare **Nascondi in Software Center e nascondi tutte le notifiche** nella scheda **Esperienza utente** delle proprietà di distribuzione.

- Se l'applicazione è stata distribuita come **Richiesta** e non è stata specificata l'opzione **Chiudi automaticamente eventuali file eseguibili in esecuzione specificati nella scheda Comportamento di installazione della finestra di dialogo relativa alle proprietà del tipo di distribuzione**, l'installazione dell'applicazione ha esito negativo se sono in esecuzione una o più applicazioni tra quelle specificate.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD
<!-- 1322613 -->
Se si distribuiscono applicazioni come disponibili agli utenti, a partire dalla versione 1802 questi possono esplorarle e installarle tramite Software Center nei dispositivi Azure Active Directory (Azure AD).  

#### <a name="prerequisites"></a>Prerequisiti

- Abilitare HTTPS nel punto di gestione  

- Integrare il sito con [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) per la **Gestione cloud**  

    - Configurare [l'individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Distribuire un'applicazione come disponibile a una raccolta di utenti da Azure AD  

- Distribuire il contenuto dell'applicazione a un [punto di distribuzione cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Abilitare l'impostazione client **Usa il nuovo Software Center** nel gruppo [Agente computer](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Il sistema operativo del client deve essere Windows 10 e il client deve essere aggiunto ad Azure AD, solo al dominio cloud o ibrido aggiunto ad Azure AD.  

- Per supportare i client basati su Internet:  

    - [Gateway di gestione cloud](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Abilitare l'impostazione client **Abilitare le richieste dei criteri utente dai client Internet** nel gruppo [Criteri client](/sccm/core/clients/deploy/about-client-settings#client-policy)  

- Per supportare i client su Intranet:  

    - Aggiungere il punto di distribuzione cloud a un gruppo di limiti usato dai client  

    - I client devono essere in grado di risolvere il nome di dominio completo (FQDN) del punto di gestione abilitato per HTTPS  



## <a name="next-steps"></a>Passaggi successivi

   -  [Impostazioni per gestire le distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md)
   -  [Manuale dell'utente di Software Center](/sccm/core/understand/software-center)

