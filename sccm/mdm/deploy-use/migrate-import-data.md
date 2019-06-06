---
title: Importare i dati in Microsoft Intune
titleSuffix: Configuration Manager
description: Importare i dati di Configuration Manager in Microsoft Intune
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e7c9fde7298d4733c2f3abd9555edb989d7cb66
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66716200"
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importare i dati di Configuration Manager in Microsoft Intune 

*Si applica a: System Center Configuration Manager (Current Branch)*    

La prima fase consigliata nel processo di [migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune](migrate-hybridmdm-to-intunesa.md) in una configurazione solo cloud prevede l'uso dello strumento di importazione dati di Intune. Se si vuole, è possibile ignorare questa fase e passare alla fase di [preparazione di Intune per la migrazione degli utenti](migrate-prepare-intune.md). Questo strumento esegue però le attività seguenti, che possono consentire di risparmiare molto tempo nella fase successiva:  

1.  Raccoglie i dati relativi agli oggetti selezionati dalla gerarchia di Configuration Manager.  

2.  Fornisce informazioni dettagliate sugli oggetti che è possibile selezionare per l'importazione e informazioni sui motivi per cui non è possibile importare alcuni oggetti.  

3.  Importa gli oggetti selezionati nel tenant di Microsoft Intune.  

Lo strumento di importazione di dati non cambia in alcun modo l'ambiente di Configuration Manager. È possibile importare gli oggetti in Intune e verificare che tutto funzioni come previsto senza il rischio di lasciare i dispositivi MDM ibrida in uno stato non gestito. 


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
> L'importazione di distribuzioni è utile solo per altri tipi di oggetti da importare. Se, ad esempio, si importano le distribuzioni e i profili VPN, sarà possibile importare solo le distribuzioni per i profili VPN selezionati. Le distribuzioni in Intune vengono chiamate assegnazioni. Se si vuole importare una distribuzione per un oggetto importato in precedenza, è necessario importare di nuovo tale oggetto oppure creare manualmente l'assegnazione in Intune in Azure. Se, ad esempio, si importano i profili VPN e non le distribuzioni, sarà necessario eseguire di nuovo lo strumento e selezionare i profili VPN e le distribuzioni oppure creare manualmente l'assegnazione in Intune in Azure. Se si esegue di nuovo lo strumento, possono venire creati oggetti duplicati che è possibile eliminare successivamente in Intune in Azure.  

> [!Important]  
> Se la raccolta per una distribuzione è basata su un gruppo di Active Directory che è stato replicato in Azure Active Directory (Azure AD), lo strumento fa automaticamente riferimento agli oggetti migrati a gruppi, se si seleziona la distribuzione appropriata quando si esegue lo strumento. Quando si dispone di raccolte più complesse o raccolte di appartenenza diretta, è necessario ricreare manualmente in Azure AD e assegnarvi manualmente le assegnazioni degli oggetti ad essi in Intune in Azure.  


## <a name="things-to-know-before-you-run-the-tool"></a>Informazioni da sapere prima di eseguire lo strumento

- Eseguire lo strumento non verrà modificato in alcun modo l'ambiente di Configuration Manager.  

- Prima di tutto testare il processo di importazione di dati con un tenant di prova. Dopo aver verificato che i dati che previsti è stato importato, è possibile passare lo stesso processo con il tenant di Intune di produzione.  

- Lo strumento di importazione dati è progettato per importare i dati di Configuration Manager una sola volta. Non tenere traccia degli oggetti in Configuration Manager o Intune. Tuttavia, se si esegue l'utilità di importazione nuovamente nello stesso computer come prima, in cui viene indicato quali oggetti importati in precedenza. Lo strumento non sa se l'oggetto è ancora presente in Intune o se un oggetto è stato modificato. Se si importano i dati in Intune più di una volta, si potrebbero creare oggetti duplicati.  

- Non tutte le impostazioni del profilo possono essere importate. Ad esempio, è possibile importare la modalità tutto schermo o le impostazioni PFX.  

- Se si dispone di criteri di Configuration Manager con impostazioni che non sono applicabili alle piattaforme selezionate, lo strumento potrebbe ignorare queste impostazioni durante l'importazione. Ignorando le impostazioni è possibile assicurarsi che i criteri possano essere importati e siano supportati da Intune.  

- Lo strumento tenta di fornire un motivo per il motivo per cui non è possibile importare un oggetto. In alcuni casi, prima di importare gli oggetti in Intune, è possibile tornare alla console di Configuration Manager, risolvere il problema, avviare di nuovo l'operazione di individuazione degli oggetti di Configuration Manager e quindi importare gli oggetti. In alcuni casi potrebbe essere necessario o consigliabile ricreare questi oggetti manualmente in Intune.  

- Ci sono alcuni profili che dipendono da altri oggetti. Se si vuole importare un profilo che dipende da un altro oggetto, ad esempio un profilo di posta elettronica che dipende da un certificato, è necessario importare entrambi gli oggetti contemporaneamente, a meno che l'altro oggetto non sia stato importato in precedenza dallo stesso computer con lo stesso utente.  

- Dopo aver eseguito lo strumento, potrebbe essere necessario eseguire altri passaggi manualmente. Ad esempio, indirizzare App e criteri a gruppi Azure AD.  

- Se tutte le app web (operazione talvolta denominate webclips) sono state assegnate a utenti, è necessario rimuovere le app web prima della migrazione degli utenti. Quindi si riassegna le app web una volta completata la migrazione. Se si non esegue questa azione, la clip web diventa ingestibile dopo la migrazione.  


## <a name="prerequisites"></a>Prerequisiti

- Specificare il sito principale ed eseguire lo strumento con un utente che ha accesso a tutti gli oggetti nella gerarchia dei siti. Lo strumento individua solo gli oggetti accessibili dall'utente che lo esegue.  

- Un amministratore globale deve eseguire lo strumento di importazione dati la prima volta usando il parametro - GlobalConsent. Un amministratore globale o amministratore di Intune può quindi eseguire lo strumento. 

- Eseguire lo strumento di importazione di dati in Windows 10 o Windows Server 2016.


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->



## <a name="download-the-data-importer-tool"></a>Scaricare lo strumento di importazione dati

Scaricare lo strumento di importazione dati dal **repository ConfigMgrTools/Intune-Data-Importer** repository in GitHub. Seguire questa procedura per scaricare lo strumento.

1. Passare alla pagina delle [versioni di GitHub dello strumento di importazione dati di Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).  

2. Per la versione più recente, fare clic su **Microsoft.Intune.Data.Importer.exe**.  

3. Salvare ed eseguire il file eseguibile. Scegliere quindi una cartella di destinazione per estrarre lo strumento di importazione dati di Intune.  



## <a name="run-the-data-importer-tool"></a>Eseguire lo strumento di importazione dati

La procedura guidata per lo strumento di importazione dati può essere suddivisa in tre passaggi principali. Questa sezione fornisce informazioni utili per completare ogni sezione della procedura guidata e importare correttamente i dati di Configuration Manager in Intune. Ogni passaggio continua dal punto in cui termina il passaggio precedente.


### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornire allo strumento di importazione dati l'autorizzazione di accesso alle risorse

Prima di eseguire lo strumento di importazione dati, è necessario usare un account di amministratore globale per concedere allo strumento l'autorizzazione di accesso alle risorse in Azure. È quindi possibile eseguire lo strumento usando un account amministratore globale o amministratore di Intune.   

1.  Un amministratore globale deve eseguire lo strumento la prima volta usando il parametro seguente: `IntuneDataImporter.exe -GlobalConsent`  

2. Quando viene avviato lo strumento, accedere con un account con il ruolo di amministratore globale in Azure.  

3. Selezionare **Accept** per creare un'applicazione in Azure con i diritti appropriati in Microsoft Graph. Lo strumento di importazione dati necessita di questi diritti per importare gli oggetti in Microsoft Intune.  

    > [!Important]  
    > Quando si accetta questo prompt dei comandi, si concede allo strumento l'autorizzazione per eseguire le operazioni seguenti:  
    > - Leggere tutti i gruppi  
    > - Accedere e leggere il profilo utente  
    > - Leggere e scrivere criteri e configurazione dei dispositivi Intune  
    > - Leggere e scrivere app di Intune  
    > - Leggere e scrivere criteri di controllo di amministrazione basata su ruoli di Intune  
    > - Leggere e scrivere dispositivi di Intune  
    > - Leggere e scrivere la configurazione di Intune  

4. Dopo aver fornito il consenso, qualsiasi altro amministratore globale o amministratore di Intune può eseguire lo strumento per importare i dati da Configuration Manager in Intune in Azure.  

> [!Note]  
> Se un amministratore globale prima di tutto non ha accettato il consenso, lo strumento potrebbe essere visualizzato l'errore seguente per un amministratore di Intune: **È possibile accedere a questa applicazione**.  


### <a name="manually-map-collections-to-azure-ad-groups"></a>Eseguire manualmente il mapping delle raccolte ai gruppi Azure AD

Quando si esegue lo strumento di importazione di dati, estrae il nome del gruppo Active Directory dalle raccolte con una singola regola destinata a un singolo gruppo di Active Directory. Quando le assegnazioni vengono create in Intune, l'utilità di importazione dati Cerca un gruppo di Azure AD con lo stesso nome del gruppo di Active Directory. Se esiste, lo strumento assegna l'oggetto importato a tale gruppo Azure AD. 

È possibile sostituire il nome del gruppo Active Directory che consente di trovare l'utilità di importazione di dati per una raccolta e specificare uno o più gruppi di Azure AD da usare per la raccolta. L'uso del file di mapping delle raccolte consente di mappare le raccolte che in genere non possono essere importate con lo strumento di importazione dati a gruppi Azure AD. 

#### <a name="find-the-collections-that-cant-be-imported"></a>Trovare le raccolte non importabili
È possibile ottenere un elenco di tutte le raccolte che non possono essere importate, in modo da poterle aggiungere al file CSV di mapping delle raccolte. 

1. Eseguire lo strumento di importazione dati e selezionare gli oggetti da importare. Utilizzare le procedure in [fase 1: Individuare gli oggetti di Configuration Manager e raccogliere dati di](#phase-1-discover-configuration-manager-objects-and-collect-data) e [fase 2: Risolvere i problemi e selezionare gli oggetti da importare](#phase-2-resolve-issues-and-select-the-objects-to-import) per individuare e scegliere gli oggetti. Nella pagina **Summary** (Riepilogo) scegliere quindi **Export Details** (Esporta dettagli) per creare un file CSV con i dettagli di tutti gli elementi selezionati per l'importazione, inclusi gli oggetti che non possono essere importati e le distribuzioni.  

2. Aprire il file CSV in Microsoft Excel e filtrare i dati in base a **Deployment** (Distribuzione) per la colonna **Type** (Tipo) e a **No** per la colonna **Importable** (Importabile). La colonna del nome delle raccolte mostra tutte le raccolte che devono essere aggiunte a un file di mapping delle raccolte per rendere importabili le distribuzioni.  

#### <a name="create-the-collection-mapping-file"></a>Creare il file di mapping delle raccolte
Il file di mapping delle raccolte è un file con valori delimitati da virgole (CSV) in cui la prima colonna è il nome della raccolta di Configuration Manager e la seconda colonna è il nome del gruppo Azure AD da usare per la raccolta. Per specificare più di un gruppo Azure AD per una singola raccolta di Configuration Manager, creare più righe nel file CSV con lo stesso nome di raccolta. L'esempio seguente è un file CSV che contiene due raccolte. La prima raccolta è mappata a un singolo gruppo Azure AD e la seconda raccolta è mappata a due gruppi Azure AD.

![Esempio di file CSV di mapping delle raccolte](../media/migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Avviare lo strumento di importazione dati con il mapping delle raccolte
Per usare un file di mapping delle raccolte, è necessario avviare lo strumento di importazione dati tramite il parametro della riga di comando **-CollectionMappingFile** e il percorso completo del file CSV di mapping delle raccolte creato. Ad esempio:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]  
> L'utilità di importazione di dati non visualizza alcuna indicazione in qualsiasi pagina della procedura guidata per indicare che è stato caricato il file di mapping raccolta. Lo strumento visualizza tuttavia gli eventuali errori rilevati durante la lettura del file CSV. 
> 
> Nella pagina **Summary** (Riepilogo) della procedura guidata è inoltre possibile verificare i tipi di **Deployment** (Distribuzione). Lo strumento visualizza **Yes** (Sì) nella colonna Importable (Importabile) ed elenca i gruppi Azure AD che assegnerà agli oggetti nella colonna **Notes** (Note).  


### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Individuare gli oggetti di Configuration Manager e raccogliere i dati

Nella fase 1 si selezionano gli oggetti da individuare e lo strumento raccoglie informazioni sugli oggetti selezionati. 

1. Aprire lo strumento e selezionare **avviare**.  

2. Leggere le informazioni e quindi selezionare **successivo**.  

3. Scegliere se importare un set di dati esportato in precedenza o selezionare i tipi di oggetto da importare:  

    - **Importa set di dati esportato da un'esecuzione precedente di importazione dati di Intune**: Selezionare **esplorare** per **cartella di dati esportato**. Selezionare un set di dati esportato in precedenza tramite lo strumento di importazione dei dati. L'utente che importa il set di dati deve essere lo stesso che ha esportato i dati. Dopo aver importato i dati, un riepilogo degli oggetti viene elencato nella pagina **Summary** (Riepilogo) della procedura guidata. Se il riepilogo è corretto, ignorare il [fase 3: Importare gli oggetti selezionati in Intune](#phase-3-import-selected-objects-to-intune).  

        > [!Note]  
        > Dopo aver individuato e selezionato gli oggetti nel sito da importare, è possibile esportare gli oggetti in un set di dati nella pagina **Sign-in to Intune** (Accedi a Intune) della procedura guidata. È quindi possibile importare il set di dati in questa pagina. Il set di dati vengono crittografato usando le credenziali utente di Windows dell'utente connesso, pertanto solo l'utente che ha esportato il set di dati è possibile importare il set di dati nello strumento.  

    - **Selezionare i tipi di oggetto da importare**: Fornire le informazioni seguenti sul sito e gli oggetti da importare:  

        - **Nome server sito**: Specificare il nome di dominio completo del server del sito per importare gli oggetti. Lo strumento individua solo gli oggetti accessibili dall'utente che lo esegue. In genere, è consigliabile specificare il sito principale ed eseguire lo strumento con un utente che abbia accesso a tutti gli oggetti nella gerarchia dei siti.  

        - **Codice del sito**: Fornire il codice del sito per il server del sito. È possibile trovare il codice di tre lettere nella parte superiore della console di Configuration Manager.  

        - **Tipi di oggetto per importare**: Scegliere gli oggetti che si desidera che lo strumento per raccogliere. È possibile scegliere **Select all** (Seleziona tutto) per scegliere tutti gli oggetti oppure selezionare singoli tipi di oggetti.  

4.  Selezionare **successivo** per avviare l'individuazione di oggetti nel sito. Lo strumento visualizza lo stato di avanzamento per ogni tipo di oggetto.  

    - Quando lo strumento non individua dati per un tipo di oggetto selezionato, l'indicatore di stato indica immediatamente che l'operazione è stata completata per quel tipo di oggetto.  

    - Gli oggetti che non è stato selezionato non vengono visualizzati nei **raccogliere** pagina di dati.  

    - È possibile eseguire di nuovo lo strumento per gli oggetti che non sono stati raccolti o che viene annullato durante il processo di raccolta.  


### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Risolvere i problemi e selezionare gli oggetti da importare  

Nella fase 2 si esaminano gli oggetti trovati dallo strumento, si risolvono i problemi che impediscono l'importazione dell'oggetto in Intune e si selezionano gli oggetti da importare. Se si correggono i problemi, tornare al **Discover ambiente** pagina della procedura guidata per individuare gli oggetti di nuovo. 

1. Fare clic su **Next** (Avanti) per esaminare gli oggetti raccolti. È disponibile una pagina di selezione degli elementi per ogni tipo di oggetto raccolto.  
   <!--   > [!Tip]     
   > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
   > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
   > - Objects are always grouped under their parent item even when you sort or filter the objects.
   -->
2. In ogni pagina di selezione di elementi, ordinare gli oggetti per il **Importable** colonna ed esaminare gli oggetti che non possono essere importati. Le informazioni contenute nel **Notes** colonna fornisce dettagli sul motivo per cui lo strumento non è possibile importare l'oggetto.  

3. Decidere se si desidera risolvere i problemi per gli oggetti non possono essere importati. Se si correggono uno o più problemi, selezionare **Previous** finché non viene visualizzata selezionare dati dalla pagina Configuration Manager. Quindi raccogliere i dati nuovamente per verificare se è stato risolto il problema. È possibile continuare a correggere i problemi fino a quando non si è soddisfatti con gli oggetti che sono importabili.  

4. In ogni pagina di selezione degli elementi selezionare gli oggetti da importare. Sono disponibili le colonne seguenti:  

    - **Nome**: Nome dell'oggetto di Configuration Manager.  

    - **Importable (importabile)** : Specifica se un oggetto può essere importato. È possibile scegliere solo gli oggetti per i quali è indicato Yes (Sì) nella colonna Importable (Importabile).  

    - **Piattaforma**: Specifica la piattaforma supportata dall'oggetto.  

    - **Già importato**: Specifica se l'oggetto è già stato importato tramite lo strumento nel computer.  

    - **È stato sostituito** (per le App): Specifica se l'app è stata sostituita da un'altra app. Selezionare il **Show sostituiti app** opzione nella parte superiore della pagina per le app sostituite da visualizzare.  

    - **Note sulla**: Vengono fornite informazioni sui motivi per cui non è possibile importare un oggetto. La colonna **Notes** (Note) visualizza anche informazioni sulle impostazioni che sono state ignorate (per alcuni tipi di oggetto), ma l'oggetto è ancora importabile senza tali impostazioni.  

    - **Linee di base di configurazione** (per gli elementi di configurazione): Specifica le linee di base di configurazione che sono associati a un elemento di configurazione.  

    - **Certificato obbligatorio** (per profili e criteri): Specifica se un certificato è associato l'oggetto. Quando all'oggetto è associato un certificato, è necessario importare anche il certificato.  

5. Dopo aver scelto gli oggetti da importare, elencate nella pagina di riepilogo. Sono disponibili le azioni seguenti:  

    - **Esportare i dettagli**: Crea un file con estensione csv che contiene le informazioni visualizzate sullo schermo. Indica inoltre gli oggetti che non possono essere importati e il motivo per cui non può essere importato. È possibile conservare questo file come riferimento.  

    - **Esportare i dati a errore**: Esporta un file compresso che contiene informazioni sui dati che lo strumento non è stato in grado di convertire o importare.  


### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importare gli oggetti selezionati in Intune

Nella fase 3 si accede a Intune e importano gli oggetti selezionati. 

1. Selezionare **successivo**, quindi selezionare una delle opzioni seguenti:  

    - **Esportare**: Dopo aver individuato e selezionato gli oggetti nel sito da importare, è possibile esportare gli oggetti in un set di dati. Ciò consente di individuare gli oggetti da un computer che non ha accesso a internet, esportare i dati e quindi importare i dati da un computer che abbia accesso a internet. Il set di dati vengono crittografato usando le credenziali utente di Windows dell'utente connesso, pertanto solo l'utente che ha esportato il set di dati è possibile importare il set di dati nello strumento. Quando si sceglie questa opzione, scegliere il percorso dei dati esportati.  

        1. Selezionare **esportare** nel **accedere a Intune** pagina.  

        2. Selezionare **esplorare** per selezionare la cartella di destinazione per l'esportazione. La cartella deve essere vuota.  

        3. Selezionare **avviare** per esportare i dati. Al termine dell'esportazione, selezionare **chiudere** per completare la procedura guidata e chiudere l'utilità di importazione di dati.  

        4. Avviare l'utilità di importazione di dati da un altro computer con accesso a internet usando le stesse credenziali. Selezionare **importazione esportato in precedenza set di dati** nella seconda pagina della procedura guidata. Al termine dell'importazione dei dati, la procedura guidata visualizza la pagina **Sign in to Intune** (Accedi a Intune).  

    - **Accedere a Intune**: Accedere con un account amministratore globale o amministratore di Intune. Dopo l'accesso, viene avviato il processo di importazione.  

        > [!Important]  
        > Prima di tutto testare il processo di importazione di dati con un tenant di prova. Dopo aver verificato che i dati che previsti è stato importato, è possibile passare lo stesso processo con il tenant di Intune di produzione.  

2. Nella pagina relativa allo stato viene indicato lo stato di avanzamento man mano che gli oggetti vengono importati. Al termine dell'importazione, fare clic su **Next** (Avanti).  

3. Nella pagina di completamento sono elencati gli oggetti importati. Controllare lo stato di ogni oggetto per cui si è verificato un errore durante il processo di importazione. Sono disponibili le azioni seguenti:  

    - **Esportare i dettagli**: Crea un file con estensione csv che contiene le informazioni visualizzate sullo schermo. È possibile conservare questo file come riferimento.  

    - **Esportare i dati a errore**: Esporta un file compresso che contiene informazioni sui dati che lo strumento non è stato in grado di convertire o importare.  



## <a name="next-steps"></a>Passaggi successivi

Dopo aver importato i dati in Intune [preparare Intune per la migrazione degli utenti](migrate-prepare-intune.md). 
