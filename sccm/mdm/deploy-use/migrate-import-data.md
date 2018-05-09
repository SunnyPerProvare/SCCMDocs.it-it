---
title: Importare i dati in Microsoft Intune
titleSuffix: Configuration Manager
description: Importare i dati di Configuration Manager in Microsoft Intune
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: dcd84e484f55cb799953bea83be917055ca1292a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
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
- Ci sono alcuni profili che dipendono da altri oggetti. Se si vuole importare un profilo che dipende da un altro oggetto, ad esempio un profilo di posta elettronica che dipende da un certificato, è necessario importare entrambi gli oggetti contemporaneamente, a meno che l'altro oggetto non sia stato importato in precedenza dallo stesso computer con lo stesso utente.  
- Dopo aver eseguito lo strumento, potrebbe essere necessario eseguire altri passaggi manualmente. Ad esempio, indirizzare app e criteri ai gruppi di AAD. 

## <a name="prerequisites"></a>Prerequisiti
- Configuration Manager versione 1610 o successiva. È consigliabile specificare il sito principale ed eseguire lo strumento con un utente che abbia accesso a tutti gli oggetti nella gerarchia dei siti. Lo strumento individua solo gli oggetti accessibili dall'utente che lo esegue. 
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

1. Passare alla pagina delle [versioni di GitHub dello strumento di importazione dati di Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).
2. Per la versione più recente, fare clic su **Microsoft.Intune.Data.Importer.exe**.
3. Salvare ed eseguire (o semplicemente eseguire) l'EXE e quindi scegliere una cartella di destinazione in cui estrarre lo strumento di importazione dati di Intune.

## <a name="run-the-data-importer-tool"></a>Eseguire lo strumento di importazione dati
La procedura guidata per lo strumento di importazione dati può essere suddivisa in tre passaggi principali. Questa sezione fornisce informazioni utili per completare ogni sezione della procedura guidata e importare correttamente i dati di Configuration Manager in Intune. Ogni passaggio continua dal punto in cui termina il passaggio precedente.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornire allo strumento di importazione dati l'autorizzazione di accesso alle risorse
Prima di eseguire lo strumento di importazione dati, è necessario usare un account di amministratore globale per concedere allo strumento l'autorizzazione di accesso alle risorse in Azure. In seguito, è possibile eseguire lo strumento usando un account di amministratore globale o di amministratore di Intune.   

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

### <a name="manually-map-collections-to-azure-ad-groups"></a>Eseguire manualmente il mapping delle raccolte ai gruppi Azure AD
Quando si esegue lo strumento di importazione dati, viene estratto il nome del gruppo AD dalle raccolte con una singola regola destinata a un singolo gruppo AD. Quando le assegnazioni vengono create in Intune, lo strumento di importazione dati cerca un gruppo Azure AD con lo stesso nome del gruppo AD e, se esiste, assegna l'oggetto importato a tale gruppo Azure AD. È possibile sostituire il nome del gruppo AD trovato dallo strumento di importazione dati per una raccolta e specificare uno o più gruppi Azure AD da usare per la raccolta. L'uso del file di mapping delle raccolte consente di mappare le raccolte che in genere non possono essere importate con lo strumento di importazione dati a gruppi Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Trovare le raccolte non importabili
È possibile ottenere un elenco di tutte le raccolte che non possono essere importate, in modo da poterle aggiungere al file CSV di mapping delle raccolte. 
1. Eseguire lo strumento di importazione dati e selezionare gli oggetti da importare. Usare le procedure in [Fase 1: Individuare gli oggetti di Configuration Manager e raccogliere i dati](#phase-1:-discover-configuration-manager-objects-and-collect-data) e [Fase 2: Risolvere i problemi e selezionare gli oggetti da importare](#phase-2:-resolve-issues-and-select-the-objects-to-import) per individuare e scegliere gli oggetti. Nella pagina **Summary** (Riepilogo) scegliere quindi **Export Details** (Esporta dettagli) per creare un file CSV con i dettagli di tutti gli elementi selezionati per l'importazione, inclusi gli oggetti che non possono essere importati e le distribuzioni. 
2. Aprire il file CSV in Microsoft Excel e filtrare i dati in base a **Deployment** (Distribuzione) per la colonna **Type** (Tipo) e a **No** per la colonna **Importable** (Importabile). La colonna del nome delle raccolte mostra tutte le raccolte che devono essere aggiunte a un file di mapping delle raccolte per rendere importabili le distribuzioni.

#### <a name="create-the-collection-mapping-file"></a>Creare il file di mapping delle raccolte
Il file di mapping delle raccolte è un file con valori delimitati da virgole (CSV) in cui la prima colonna è il nome della raccolta di Configuration Manager e la seconda colonna è il nome del gruppo Azure AD da usare per la raccolta. Per specificare più di un gruppo Azure AD per una singola raccolta di Configuration Manager, creare più righe nel file CSV con lo stesso nome di raccolta. L'esempio seguente è un file CSV che contiene due raccolte. La prima raccolta è mappata a un singolo gruppo Azure AD e la seconda raccolta è mappata a due gruppi Azure AD.

![Esempio di file CSV di mapping delle raccolte](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Avviare lo strumento di importazione dati con il mapping delle raccolte
Per usare un file di mapping delle raccolte, è necessario avviare lo strumento di importazione dati tramite il parametro della riga di comando *-CollectionMappingFile* e il percorso completo del file CSV di mapping delle raccolte creato. Ad esempio:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> Lo strumento di importazione dati non visualizza alcuna indicazione in alcuna pagina della procedura guidata per segnalare il caricamento del file di mapping delle raccolte. Lo strumento visualizza tuttavia gli eventuali errori rilevati durante la lettura del file CSV. Nella pagina **Summary** (Riepilogo) della procedura guidata è inoltre possibile verificare i tipi di **Deployment** (Distribuzione). Lo strumento visualizza **Yes** (Sì) nella colonna Importable (Importabile) ed elenca i gruppi Azure AD che assegnerà agli oggetti nella colonna **Notes** (Note).

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Individuare gli oggetti di Configuration Manager e raccogliere i dati
Nella fase 1 si selezionano gli oggetti da individuare e lo strumento raccoglie informazioni sugli oggetti selezionati. 
1. Aprire lo strumento e fare clic su **Start** (Avvia).  
2. Aggiornare le informazioni e quindi fare clic su **Next** (Avanti). 
3. Scegliere se importare un set di dati esportato in precedenza o selezionare i tipi di oggetto da importare:
   - **Importare un set di dati esportato in precedenza**: scegliere **Import data set exported from a previous run of Intune Data Importer** (Importa set di dati esportato da un'esecuzione precedente dello strumento di importazione dati di Intune) e fare clic su **Browse** (Sfoglia) per **Exported data folder** (Cartella dati esportati) per selezionare un set di dati esportato in precedenza tramite lo strumento di importazione dati. L'utente che importa il set di dati deve essere lo stesso che ha esportato i dati. Dopo aver importato i dati, un riepilogo degli oggetti viene elencato nella pagina **Summary** (Riepilogo) della procedura guidata. Se il riepilogo è corretto, ignorare la [Fase 3: Importare gli oggetti selezionati in Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Dopo aver individuato e selezionato gli oggetti nel sito da importare, è possibile esportare gli oggetti in un set di dati nella pagina **Sign-in to Intune** (Accedi a Intune) della procedura guidata. È quindi possibile importare il set di dati in questa pagina. Il set di dati viene crittografato con le credenziali utente di Windows dell'utente connesso, pertanto solo l'utente che ha esportato il set di dati può importarlo nello strumento. 
   - **Selezionare i tipi di oggetto da importare**: scegliere **Select object types to import** (Selezionare i tipi di oggetto da importare) per selezionare i tipi di oggetto da importare e individuare gli oggetti nell'ambiente in uso. Specificare le informazioni seguenti sul sito e sugli oggetti da importare.
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
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  In ogni pagina di selezione degli elementi ordinare gli oggetti in base alla colonna Importable (Importabile) ed esaminare gli oggetti che non è possibile importare. Le informazioni nella colonna Notes (Note) forniscono dettagli sul motivo per cui lo strumento non può importare l'oggetto. 
7.  A questo punto è necessario decidere se provare a correggere i problemi per gli oggetti che non possono essere importati. Se si correggono uno o più problemi, fare clic su Previous (Indietro) fino a tornare alla pagina Select data from Configuration Manager (Seleziona dati da Configuration Manager) e raccogliere di nuovo i dati per verificare se il problema è stato risolto. È possibile continuare a correggere i problemi fino a ottenere il risultato desiderato in relazione agli oggetti importabili. 
8.  In ogni pagina di selezione degli elementi selezionare gli oggetti da importare. Sono disponibili le colonne seguenti:
    - **Name** (Nome): nome dell'oggetto di Configuration Manager. 
    - **Importable** (Importabile): specifica se un oggetto può essere importato. È possibile scegliere solo gli oggetti per i quali è indicato Yes (Sì) nella colonna Importable (Importabile). 
    - **Platform** (Piattaforma): specifica la piattaforma supportata dall'oggetto.
    - **Already imported** (Già importato): specifica se l'oggetto è già stato importato con lo strumento nel computer in uso. 
    - **Is superseded** (Sostituito) (per le app): specifica se l'app è stata sostituita da un'altra app. È necessario selezionare la casella di controllo **Show superseded apps** (Mostra app sostituite) nella parte superiore della pagina per visualizzare le app sostituite.
    - **Notes** (Note): fornisce informazioni sui motivi per cui non è possibile importare un oggetto. La colonna **Notes** (Note) visualizza anche informazioni sulle impostazioni che sono state ignorate (per alcuni tipi di oggetto), ma l'oggetto è ancora importabile senza tali impostazioni.
    - **Configuration baselines** (Linee di base di configurazione) (per gli elementi di configurazione): specifica le linee di base di configurazione associate a un elemento di configurazione.
    - **Required certificate** (Certificato richiesto) (per profili e criteri): specifica se all'oggetto è associato un certificato. Quando all'oggetto è associato un certificato, è necessario importare anche il certificato.
9.  Dopo aver scelto gli oggetti da importare, questi vengono elencati nella pagina di riepilogo. Sono disponibili le azioni seguenti: 
    - **Export details** (Esporta dettagli): crea un file CSV contenente le informazioni visualizzate sullo schermo. Mostra anche gli oggetti che non possono essere importati e il motivo per cui non sono importabili. È possibile conservare questo file come riferimento. 
    - **Export error data** (Esporta dati degli errori): esporta un file compresso contenente informazioni sui dati che lo strumento non è stato in grado di convertire o importare. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importare gli oggetti selezionati in Intune
Nella fase 3 si accede a Intune e si importano gli oggetti selezionati. 
10. Fare clic su **Next** (Avanti) e quindi su **Sign in to Intune** (Accedi a Intune) per accedere al tenant di Intune per l'importazione dei dati oppure scegliere di esportare i dati.

    - **Export** (Esporta): dopo aver individuato e selezionato gli oggetti nel sito da importare, è possibile esportare gli oggetti in un set di dati. Ciò consente di individuare gli oggetti da un computer che non ha accesso a Internet, esportare i dati e quindi importarli da un computer con accesso a Internet. Il set di dati viene crittografato con le credenziali utente di Windows dell'utente connesso, pertanto solo l'utente che ha esportato il set di dati può importarlo nello strumento. Quando si sceglie questa opzione, scegliere il percorso dei dati esportati. 
      1. Fare clic su **Export** (Esporta) nella pagina **Sign in to Intune** (Accedi a Intune). 
      2. Fare clic su **Browse** (Sfoglia) per selezionare la cartella di destinazione per l'esportazione. La cartella deve essere vuota. 
      3. Fare clic su **Start** (Avvia) per esportare i dati e al termine dell'esportazione fare clic su **Close** (Chiudi) per completare la procedura guidata e chiudere lo strumento di importazione dati.
      4. Avviare lo strumento di importazione dati da un altro computer con accesso a Internet usando le stesse credenziali e selezionare **Import previously exported data set** (Importa set di dati esportato in precedenza) nella seconda pagina della procedura guidata. Al termine dell'importazione dei dati, la procedura guidata visualizza la pagina **Sign in to Intune** (Accedi a Intune). 
    - **Sign in to Intune** (Accedi a Intune): è necessario accedere con un account di amministratore globale o di amministratore di Intune. Dopo l'accesso, viene avviato il processo di importazione.
    
      > [!Important]
      > È consigliabile testare prima il processo di importazione dei dati usando un tenant di prova. Quindi, dopo aver verificato che i dati previsti siano stati importati, è possibile eseguire lo stesso processo con il tenant di produzione di Intune.
12. Nella pagina relativa allo stato viene indicato lo stato di avanzamento man mano che gli oggetti vengono importati. Al termine dell'importazione, fare clic su **Next** (Avanti). 
13. Nella pagina di completamento sono elencati gli oggetti importati. Controllare lo stato di ogni oggetto per cui si è verificato un errore durante il processo di importazione. Sono disponibili le azioni seguenti: 
    - **Export details** (Esporta dettagli): crea un file CSV contenente le informazioni visualizzate sullo schermo. È possibile conservare questo file come riferimento. 
    - **Export error data** (Esporta dati degli errori): esporta un file compresso contenente informazioni sui dati che lo strumento non è stato in grado di convertire o importare.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere importato i dati in Intune, è necessario eseguire i passaggi per [preparare Intune per la migrazione degli utenti](migrate-prepare-intune.md). 