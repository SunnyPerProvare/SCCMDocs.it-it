---
title: Distribuire applicazioni | System Center Configuration Manager
description: Creare un tipo di distribuzione o simulare la distribuzione di un'applicazione usando System Center Configuration Manager.
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e608bcbadc82487018bb29c5e05660275d8fa275


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Distribuire le applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 Prima di distribuire un'applicazione di System Center Configuration Manager è necessario creare almeno un tipo di distribuzione per l'applicazione stessa. Per altre informazioni sulla creazione di applicazioni e tipi di distribuzione, vedere [Create applications ](../../apps/deploy-use/create-applications.md) (Creare applicazioni).  

> [!IMPORTANT]  
>  È possibile distribuire (installare o disinstallare) le applicazioni necessarie, ma non pacchetti o aggiornamenti software. I dispositivi mobili non supportano nemmeno le distribuzioni simulate.  
>   
>  I dispositivi mobili non supportano inoltre le impostazioni di pianificazione e di esperienza utente nella Distribuzione guidata del software.  

 È anche possibile simulare la distribuzione di un'applicazione. Questo tipo di distribuzione sottopone a test l'applicabilità di una distribuzione di applicazione nei computer senza installare o disinstallare l'applicazione. Una distribuzione simulata esegue una valutazione del metodo di rilevamento, dei requisiti e delle dipendenze per un tipo di distribuzione e segnala i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** . Per altre informazioni, vedere [Simulate application deployments ](../../apps/deploy-use/simulate-application-deployments.md) (Simulare le distribuzioni di applicazioni).  

## <a name="deploy-an-application"></a>Distribuire un'applicazione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nell'elenco **Applicazioni** selezionare l'applicazione che si desidera distribuire. Quindi, nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

4.  Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:  

    -   **Software** : visualizza l'applicazione da distribuire. È possibile fare clic su **Sfoglia** per selezionare un'altra applicazione.  

    -   **Raccolta** : fare clic su **Sfoglia** per selezionare la raccolta in cui distribuire l'applicazione.  

    -   **Usa gruppi di punti di distribuzione predefiniti associati a questa raccolta** : selezionare questa opzione se si desidera archiviare il contenuto dell'applicazione nel gruppo di punti di distribuzione predefinito della raccolta. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione non è disponibile.  

    -   **Distribuisci automaticamente contenuto per dipendenze** : se l'opzione è attivata e uno dei tipi di distribuzione dell'applicazione contiene dipendenze, anche il contenuto dell'applicazione dipendente verrà inviato ai punti di distribuzione.  

        > [!IMPORTANT]  
        >  Se l'applicazione dipendente viene aggiornata dopo la distribuzione dell'applicazione primaria, il nuovo contenuto per la dipendenza non verrà distribuito automaticamente.  

    -   **Commenti (facoltativo)** : immettere una descrizione facoltativa della distribuzione.  

5.  Nella pagina **Contenuto** fare clic su **Aggiungi** per aggiungere il contenuto associato a questa distribuzione ai punti di distribuzione o ai gruppi di punti di distribuzione. Se è stata selezionata l'opzione Use default distribution points associated to this collection (Usa gruppi di punti di distribuzione predefiniti associati a questa raccolta) nella pagina **Generale**, l'opzione verrà popolata automaticamente e potrà essere modificata solo da un membro del ruolo di sicurezza **Amministratore applicazione** .  

6.  Fare clic su **Avanti**.  

7.  Nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software specificare le informazioni seguenti:  

    -   **Azione** : dall'elenco a discesa scegliere se la distribuzione ha l'obiettivo **Installa** o **Disinstalla** relativo all'applicazione.  

        > [!NOTE]  
        >  Se un'applicazione viene distribuita due volte in un dispositivo, una volta con l'azione **Installa** e una volta con l'azione **Disinstalla**, avrà priorità la distribuzione dell'applicazione con l'azione **Installa** .  
        >   
        >  È impossibile modificare l'azione di una distribuzione dopo la relativa creazione.  

    -   **Scopo** : dall'elenco a discesa scegliere una delle seguenti opzioni:  

        -   **Disponibile** : se l'applicazione viene distribuita a un utente, l'utente visualizzerà l'applicazione pubblicata in Software Center e potrà installarla su richiesta.  

        -   **Richiesto** : l'applicazione viene distribuita automaticamente in base alla pianificazione configurata. Un utente può tuttavia tenere traccia dello stato della distribuzione dell'applicazione, a meno che non sia nascosto, e può installare l'applicazione da Software Center prima della scadenza.  

            > [!NOTE]  
            >  Quando l'azione di distribuzione è impostata su **Disinstalla**, lo scopo della distribuzione viene impostato automaticamente su **Richiesto** e non può essere modificato.  

    -   **Distribuisci automaticamente in base alla pianificazione con o senza accesso utente** : se la distribuzione è destinata a un utente, selezionare questa opzione per distribuire l'applicazione nei dispositivi primari dell'utente. Questa impostazione non richiede all'utente di accedere prima che venga eseguita la distribuzione. Non selezionare questa opzione se l'utente deve fornire input per completare l'installazione. Questa opzione è disponibile solo quando la distribuzione ha lo scopo **Richiesto**.  

    -   **Invia pacchetti di riattivazione** : se lo scopo della distribuzione è impostato su **Richiesto** e l'opzione è selezionata, ai computer viene inviato un pacchetto di riattivazione prima dell'installazione della distribuzione al fine di riattivare i computer da sospensione alla scadenza dell'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.  

    -   **Tutti i client devono usare una connessione di rete a consumo per scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo ulteriore** : questa opzione è disponibile solo per le distribuzioni con lo scopo **Richiesto**.  

    -   **Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione** : se l'opzione è selezionata, prima dell'installazione dell'applicazione l'amministratore deve approvare tutte le relative richieste degli utenti. Questa opzione non è disponibile quando lo scopo della distribuzione è **Richiesto** o quando l'applicazione viene distribuita in una raccolta dispositivi.  

        > [!NOTE]  
        >  Le richieste di approvazione dell'applicazione vengono visualizzate nel nodo **Richieste di approvazione** , in **Gestione applicazioni** , nell'area di lavoro **Raccolta software** . Se una richiesta di approvazione non viene approvata entro 45 giorni, verrà rimossa. La reinstallazione del client di Configuration Manager potrebbe anche annullare eventuali richieste di approvazione in sospeso.  

    -   **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione** : se l'opzione è selezionata, le versioni sostituite dell'applicazione verranno aggiornate con l'applicazione sostitutiva.  

8.  Nella pagina **Pianificazione** Distribuzione guidata del software configurare il momento in cui l'applicazione verrà distribuita o sarà disponibile nei dispositivi client.  
    Le opzioni presenti in questa pagina varieranno in base all'impostazione dell'azione di distribuzione, che può essere **Disponibile** o **Richiesto**.  

9. Se l'applicazione che si desidera distribuire sostituisce un'altra applicazione, è possibile configurare la scadenza dell'installazione nel momento in cui gli utenti ricevono la nuova applicazione. A tale scopo usare l'impostazione **Scadenza dell'installazione per l'aggiornamento di utenti o dispositivi con l'applicazione sostituita installata** .  

10. Nella pagina **Esperienza utente** della Distribuzione guidata del software specificare le informazioni sulle modalità di interazione degli utenti con l'installazione dell'applicazione.
    Quando si distribuiscono applicazioni in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'applicazione nella sovrapposizione temporanea e confermare le modifiche in seguito oppure confermarle alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  
   > [!NOTE]  
   >  Quando si distribuisce un'applicazione in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata. Per altre informazioni sull'uso delle finestre di manutenzione quando si distribuiscono applicazioni in dispositivi con Windows Embedded, vedere [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md) (Creare applicazioni Windows Embedded).  
   >  Le opzioni **Installazione software** e **Riavvio del sistema (se richiesto per completare l'installazione)** non vengono usate se lo scopo della distribuzione è impostato su **Disponibile**. È inoltre possibile configurare il livello di notifica visualizzato dall'utente durante l'installazione dell'applicazione.  
11. Nella pagina **Avvisi** della Distribuzione guidata del software configurare la modalità in cui Configuration Manager e System Center Operations Manager dovranno generare gli avvisi relativi alla distribuzione. È possibile configurare le soglie di reporting degli avvisi e disattivare il reporting per tutta la durata della distribuzione.  

12. (solo per app iOS): fare clic su **Nuovo** nella pagina **Criteri di configurazione dell'app** per associare questa distribuzione a un criterio di configurazione dell'app iOS, se ne è stato creato uno. Per altre informazioni su questo tipo di criteri, vedere [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurare le app iOS con i criteri di configurazione delle app).  

13. Nella pagina **Riepilogo** della Distribuzione guidata del software esaminare le azioni che verranno eseguite dalla distribuzione e quindi fare clic su **Avanti** per completare la procedura guidata.  

 La nuova distribuzione verrà visualizzata nell'elenco **Distribuzioni** del nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** . È possibile modificare le proprietà di questa distribuzione o eliminare la distribuzione dalla scheda **Distribuzioni** del riquadro dettagli dell'applicazione.  

## <a name="delete-an-application-deployment"></a>Eliminare la distribuzione di un'applicazione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nell'elenco **Applicazioni** selezionare l'applicazione per cui si desidera eliminare la distribuzione.  

4.  Nella scheda **Distribuzioni** dell'elenco *<nome applicazione\>* selezionare la distribuzione dell'applicazione da eliminare. Quindi, nella scheda **Distribuzione** , nel gruppo **Distribuzione** , fare clic su **Elimina**.  

 Quando si elimina la distribuzione di un'applicazione, tutte le istanze dell'applicazione già installate non vengono rimosse. Per rimuovere queste applicazioni, è necessario distribuire l'applicazione nei computer con l'azione **Disinstalla**. Se si elimina la distribuzione di un'applicazione o si rimuove una risorsa dalla raccolta in cui si vuole eseguire la distribuzione, l'applicazione non sarà più visibile in Software Center.  



<!--HONumber=Nov16_HO1-->


