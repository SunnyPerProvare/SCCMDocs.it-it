---
title: Importare i dati in Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: 4b5f788a611b9df7c12f788099d82fadbf1e4af9
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importare i dati di Configuration Manager in Microsoft Intune 

*Si applica a: System Center Configuration Manager (Current Branch)*    

La prima fase consigliata nel processo di [migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune](migrate-hybridmdm-to-intunesa.md) in una configurazione solo cloud prevede l'uso dello strumento di importazione dati di Intune. Se si vuole, è possibile ignorare questa fase e passare alla fase di [preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md). Questo strumento esegue però le attività seguenti, che possono consentire di risparmiare molto tempo nella fase successiva: 
1.  Raccoglie i dati relativi agli oggetti selezionati dalla gerarchia di Configuration Manager. 
2.  Fornisce informazioni dettagliate sugli oggetti che è possibile selezionare per l'importazione e informazioni sui motivi per cui non è possibile importare alcuni oggetti.
3.  Importa gli oggetti selezionati nel tenant di Microsoft Intune. 

Lo strumento di importazione dati non modifica in alcun modo l'ambiente di Configuration Manager e quindi è possibile importare gli oggetti in Intune e verificare che tutto funzioni come previsto senza il rischio di lasciare i dispositivi della soluzione MDM ibrida in uno stato non gestito. 

## <a name="what-objects-can-this-tool-import"></a>Quali oggetti può importare lo strumento?
Lo strumento di importazione può raccogliere informazioni sui tipi di oggetti seguenti in Configuration Manager e fornisce informazioni sulla possibilità di importare gli oggetti raccolti: 
- Elementi di configurazione
- Profili certificato
- Profili di posta elettronica
- Profili VPN
- Profili Wi-Fi
- Criteri di conformità
- App
- Distribuzioni

> [!Note]    
> L'importazione di distribuzioni è utile solo per altri tipi di oggetti da importare. Se, ad esempio, si importano le distribuzioni e i profili VPN, sarà possibile importare solo le distribuzioni per i profili VPN selezionati. Le distribuzioni in Intune vengono chiamate assegnazioni. Se si vuole importare una distribuzione per un oggetto importato in precedenza, è necessario importare di nuovo tale oggetto oppure creare manualmente l'assegnazione in Intune in Azure. Se, ad esempio, si importano i profili VPN e non le distribuzioni, sarà necessario eseguire di nuovo lo strumento e selezionare i profili VPN e le distribuzioni oppure creare manualmente l'assegnazione in Intune in Azure.  Se si esegue di nuovo lo strumento, possono venire creati oggetti duplicati che è possibile eliminare successivamente in Intune in Azure.  

> [!Important]    
> Se la raccolta per una distribuzione è basata su un gruppo di Active Directory che è stato replicato in Azure Active Directory (AAD), lo strumento invierà automaticamente gli oggetti di cui viene eseguita la migrazione nei gruppi se si seleziona la distribuzione appropriata quando si esegue lo strumento. In presenza di raccolte più complesse o raccolte di appartenenza diretta, è necessario ricreare manualmente le raccolte in AAD e assegnarvi manualmente le assegnazioni degli oggetti in Intune in Azure.


## <a name="things-to-know-before-you-run-the-tool"></a>Informazioni da sapere prima di eseguire lo strumento
- L'esecuzione dello strumento non modifica in alcun modo l'ambiente di Configuration Manager.
- È consigliabile testare prima il processo di importazione dei dati usando un tenant di prova. Quindi, dopo aver verificato che i dati previsti siano stati importati, è possibile eseguire lo stesso processo con il tenant di produzione di Intune.
- Lo strumento di importazione dati è progettato per importare i dati di Configuration Manager una sola volta. Non tiene traccia degli oggetti in Configuration Manager o in Intune. Se tuttavia si esegue lo strumento di importazione di nuovo nello stesso computer usato in precedenza, verranno indicati gli oggetti importati in precedenza. Lo strumento non sa se l'oggetto è ancora presente in Intune o se è stato modificato. Se si importano i dati in Intune più di una volta, si potrebbero creare oggetti duplicati.
- Non tutte le impostazioni del profilo possono essere importate. Non è ad esempio possibile importare la modalità tutto schermo o le impostazioni PFX. 
- Se ci sono criteri di Configuration Manager con impostazioni non applicabili alle piattaforme selezionate, lo strumento potrebbe ignorare tali impostazioni durante l'importazione. Ignorando le impostazioni è possibile assicurarsi che i criteri possano essere importati e siano supportati da Intune. 
- Lo strumento tenterà di indicare il motivo per cui non è possibile importare un oggetto. In alcuni casi, prima di importare gli oggetti in Intune, è possibile tornare alla console di Configuration Manager, risolvere il problema, avviare di nuovo l'operazione di individuazione degli oggetti di Configuration Manager e quindi importare gli oggetti. In alcuni casi potrebbe essere necessario o consigliabile ricreare questi oggetti manualmente in Intune.
- Ci sono alcuni profili che dipendono da altri oggetti. Se si vuole importare un profilo che dipende da un altro oggetto, ad esempio un profilo di posta elettronica che dipende da un certificato, è necessario importare entrambi gli oggetti contemporaneamente.
- Dopo aver eseguito lo strumento, potrebbe essere necessario eseguire altri passaggi manualmente. Ad esempio, indirizzare app e criteri ai gruppi di AAD. 

## <a name="prerequisites"></a>Prerequisiti
- Configuration Manager versione 1610 o successiva. È consigliabile specificare il sito principale ed eseguire lo strumento con un utente che abbia accesso a tutti gli oggetti nella gerarchia dei siti. Lo strumento individua solo gli oggetti accessibili dall'utente che lo esegue. 
- È necessario eseguire lo strumento da un computer che possa accedere al provider SMS (per raccogliere i dati di Configuration Manager) e a Internet (per importare gli oggetti in Intune).
- La prima volta lo strumento di importazione dati deve essere eseguito da un amministratore globale con il parametro ***intunedataimporter.exe -GlobalConsent***. In seguito, lo strumento può essere eseguito da un amministratore globale o un amministratore di Intune.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Scaricare lo strumento di importazione dati
Lo strumento di importazione dati è disponibile per il download dal repository ConfigMgrTools/Intune-Data-Importer in GitHub. Seguire questa procedura per scaricare lo strumento.

1. Passare alla [pagina di GitHub dello strumento di importazione dati di Intune](https://go.microsoft.com/fwlink/?linkid=858194).
2. Fare clic su **Clone or download** (Clona o scarica), fare clic su **Download ZIP** (Scarica ZIP) e salvare il file ZIP compresso. 
3. Estrarre il contenuto del file ZIP.

## <a name="run-the-data-importer-tool"></a>Eseguire lo strumento di importazione dati
Prima di eseguire lo strumento di importazione dati, è necessario usare un account di amministratore globale per concedere allo strumento l'autorizzazione di accesso alle risorse in Azure. In seguito, è possibile eseguire lo strumento usando un account di amministratore globale o di amministratore di Intune.     

La procedura guidata per lo strumento di importazione dati può essere suddivisa in tre passaggi principali. Questa sezione fornisce informazioni utili per completare ogni sezione della procedura guidata e importare correttamente i dati di Configuration Manager in Intune. Ogni passaggio continua dal punto in cui termina il passaggio precedente.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornire allo strumento di importazione dati l'autorizzazione di accesso alle risorse
1.  La prima volta lo strumento di importazione dati deve essere eseguito da un amministratore globale con il parametro ***intunedataimporter.exe -GlobalConsent*** 
2. All'avvio dello strumento, viene visualizzata una schermata di accesso in cui è necessario usare un account con il ruolo di amministratore globale in Azure per accedere. 
3. Fare clic su **Accept** (Accetta) per creare un'applicazione in Azure con i diritti appropriati in Microsoft Graph. Lo strumento di importazione dati necessita di questi diritti per importare gli oggetti in Microsoft Intune.   

   > [!Important]
   > Facendo clic su **Accept** (Accetta), si assegna allo strumento l'autorizzazione per eseguire le operazioni seguenti:
   > - Leggere tutti i gruppi
   > - Accedere e leggere il profilo utente
   > - Leggere e scrivere criteri e configurazione dei dispositivi Intune
   > - Leggere e scrivere app di Intune
   > - Leggere e scrivere criteri di controllo di amministrazione basata su ruoli di Intune
   > - Leggere e scrivere dispositivi di Intune
   > - Leggere e scrivere la configurazione di Intune
1. Dopo aver fornito il consenso, qualsiasi altro amministratore globale o amministratore di Intune può eseguire lo strumento per importare i dati da Configuration Manager in Intune in Azure.    
        
    > [!Note]
    > Se il consenso non viene prima fornito da un amministratore globale, potrebbe venire visualizzato il messaggio **Impossibile accedere all'applicazione** quando un amministratore di Intune esegue lo strumento di importazione dati e accede alla sottoscrizione di Intune.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Individuare gli oggetti di Configuration Manager e raccogliere i dati
Nella fase 1 si selezionano gli oggetti da individuare e lo strumento raccoglie informazioni sugli oggetti selezionati. 
1. Aprire lo strumento e fare clic su **Start** (Avvia).  
2. Aggiornare le informazioni e quindi fare clic su **Next** (Avanti). 
3. Fornire le informazioni seguenti sul sito e sugli oggetti nel sito da importare. 
    - **Site server name** (Nome del server del sito): specificare il nome di dominio completo del server del sito per l'importazione degli oggetti. Lo strumento individua solo gli oggetti accessibili dall'utente che lo esegue. In genere, è consigliabile specificare il sito principale ed eseguire lo strumento con un utente che abbia accesso a tutti gli oggetti nella gerarchia dei siti.
    - **Site code** (Codice del sito): specificare il codice del sito per il server del sito. È possibile trovare il codice di tre lettere nella parte superiore della console di Configuration Manager.
    - **Object types to import** (Tipi di oggetti da importare): scegliere gli oggetti che si vuole raccogliere tramite lo strumento. È possibile scegliere **Select all** (Seleziona tutto) per scegliere tutti gli oggetti oppure selezionare singoli tipi di oggetti. 
4.  Fare clic su **Next** (Avanti) per avviare l'individuazione degli oggetti nel sito. Lo strumento visualizza lo stato di avanzamento per ogni tipo di oggetto. 
    - Quando lo strumento non individua dati per un tipo di oggetto selezionato, l'indicatore di stato indica immediatamente che l'operazione è stata completata per quel tipo di oggetto.
    - Gli oggetti non selezionati non vengono visualizzati nella pagina **Collect** (Raccogli). 
    - È possibile eseguire di nuovo lo strumento per gli oggetti che non sono stati raccolti o che sono stati annullati durante il processo di raccolta.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Risolvere i problemi e selezionare gli oggetti da importare  
Nella fase 2 si esaminano gli oggetti trovati dallo strumento, si risolvono i problemi che impediscono l'importazione dell'oggetto in Intune e si selezionano gli oggetti da importare. Se si correggono i problemi, tornare alla pagina **Discover environment** (Individua ambiente) della procedura guidata per eseguire di nuovo l'individuazione degli oggetti. 
5.  Fare clic su **Next** (Avanti) per esaminare gli oggetti raccolti. È disponibile una pagina di selezione degli elementi per ogni tipo di oggetto raccolto. 

    > [!Tip]     
    > In ogni pagina di selezione degli elementi è possibile creare un filtro per trovare gli oggetti da importare. Tenere tuttavia presente quanto segue:
    > - Quando è aperta una pagina di selezione degli elementi e la vista è filtrata, le caselle di controllo Select all (Seleziona tutto) si applicano solo agli elementi visualizzati. Eventuali oggetti nascosti a causa dell'applicazione di un filtro non vengono inclusi quando si usano le caselle di controllo.
    > - Gli oggetti vengono sempre raggruppati sotto il relativo elemento padre, anche quando si ordinano o si filtrano.


6.  In ogni pagina di selezione degli elementi ordinare gli oggetti in base alla colonna Importable (Importabile) ed esaminare gli oggetti che non è possibile importare. Le informazioni nella colonna Notes (Note) forniscono dettagli sul motivo per cui lo strumento non può importare l'oggetto. 
7.  A questo punto è necessario decidere se provare a correggere i problemi per gli oggetti che non possono essere importati. Se si correggono uno o più problemi, fare clic su Previous (Indietro) fino a tornare alla pagina Select data from Configuration Manager (Seleziona dati da Configuration Manager) e raccogliere di nuovo i dati per verificare se il problema è stato risolto. È possibile continuare a correggere i problemi fino a ottenere il risultato desiderato in relazione agli oggetti importabili. 
8.  In ogni pagina di selezione degli elementi selezionare gli oggetti da importare. Sono disponibili le colonne seguenti:
    - **Name** (Nome): nome dell'oggetto di Configuration Manager. 
    - **Importable** (Importabile): specifica se un oggetto può essere importato. È possibile scegliere solo gli oggetti per i quali è indicato Yes (Sì) nella colonna Importable (Importabile). 
    - **Platform** (Piattaforma): specifica la piattaforma supportata dall'oggetto.
    - **Already imported** (Già importato): specifica se l'oggetto è già stato importato con lo strumento nel computer in uso. 
    - **Notes** (Note): fornisce informazioni sui motivi per cui non è possibile importare un oggetto.
    - **Configuration baselines** (Linee di base di configurazione) (per gli elementi di configurazione): specifica le linee di base di configurazione associate a un elemento di configurazione.
    - **Required certificate** (Certificato richiesto) (per profili e criteri): specifica se all'oggetto è associato un certificato. Quando all'oggetto è associato un certificato, è necessario importare anche il certificato.
9.  Dopo aver scelto gli oggetti da importare, questi vengono elencati nella pagina di riepilogo. Sono disponibili le azioni seguenti: 
    - **Export details** (Esporta dettagli): crea un file CSV contenente le informazioni visualizzate sullo schermo. È possibile conservare questo file come riferimento. 
    - **Export error data** (Esporta dati degli errori): esporta un file compresso contenente informazioni sui dati che lo strumento non è stato in grado di convertire o importare. 

### <a name="phase-3-import-selected-object-to-intune"></a>Fase 3: Importare l'oggetto selezionato in Intune
Nella fase 3 si accede a Intune e si importano gli oggetti selezionati. 
10. Fare clic su **Next** (Avanti) e quindi su **Sign in to Intune** (Accedi a Intune) per accedere al tenant di Intune per l'importazione dei dati. È necessario accedere con un account di amministratore globale o di amministratore di Intune. Dopo l'accesso, viene avviato il processo di importazione.

    > [!Important]
    > È consigliabile testare prima il processo di importazione dei dati usando un tenant di prova. Quindi, dopo aver verificato che i dati previsti siano stati importati, è possibile eseguire lo stesso processo con il tenant di produzione di Intune.

12. Nella pagina relativa allo stato viene indicato lo stato di avanzamento man mano che gli oggetti vengono importati. Al termine dell'importazione, fare clic su **Next** (Avanti). 
13. Nella pagina di completamento sono elencati gli oggetti importati. Controllare lo stato di ogni oggetto per cui si è verificato un errore durante il processo di importazione. Sono disponibili le azioni seguenti: 
    - **Export details** (Esporta dettagli): crea un file CSV contenente le informazioni visualizzate sullo schermo. È possibile conservare questo file come riferimento. 
    - **Export error data** (Esporta dati degli errori): esporta un file compresso contenente informazioni sui dati che lo strumento non è stato in grado di convertire o importare.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere importato i dati in Intune, è necessario eseguire i passaggi per [preparare Intune per la migrazione degli utenti](migrate-prepare-intune.md). 