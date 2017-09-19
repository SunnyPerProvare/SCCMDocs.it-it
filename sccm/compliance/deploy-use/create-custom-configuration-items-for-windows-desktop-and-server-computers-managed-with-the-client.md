---
title: Creare elementi di configurazione per computer Windows gestiti da client - Configuration Manager | Microsoft Docs
description: "È possibile gestire le impostazioni per i computer e i server Windows usando un elemento di configurazione personalizzato per computer desktop e server Windows."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
caps.latest.revision: "9"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 9fe28782744a419acad9c1acec49ff8db6c0eaa6
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione personalizzati per computer desktop e server Windows gestiti con il client di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare l'elemento di configurazione **personalizzato per computer desktop e server Windows** di System Center Configuration Manager per gestire le impostazioni per i computer e server Windows gestiti dal client di Configuration Manager.  

## <a name="start-the-create-configuration-item-wizard"></a>Avviare la creazione guidata dell'elemento di configurazione

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

5.  In **Specificare il tipo di elemento di configurazione da creare**selezionare **Desktop e server di Windows (personalizzato)**.  

    > [!TIP]  
    >  Per specificare le impostazioni del metodo di rilevamento che consentono di controllare l'esistenza di un'applicazione, selezionare **Questo elemento di configurazione contiene le impostazioni dell'applicazione**.  

6.  Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  

## <a name="provide-detection-method-information"></a>Fornire informazioni sul metodo di rilevamento  
 Usare questa procedura per fornire informazioni sul metodo di rilevamento per l'elemento di configurazione.  

> [!NOTE]  
>  Si applica solo se si seleziona **questo elemento di configurazione contiene le impostazioni dell'applicazione** sul **Generale** pagina della procedura guidata.  

 Un metodo di rilevamento in Configuration Manager contiene regole che consentono di rilevare se un'applicazione viene installata in un computer. Questo rilevamento si verifica prima valutazione della conformità dell'elemento di configurazione. Per rilevare se un'applicazione è installata, è possibile rilevare la presenza di un file Windows Installer per l'applicazione, utilizzare uno script personalizzato o selezionare **presupporre sempre l'applicazione viene installata** per valutare l'elemento di configurazione per la conformità, anche se è installata l'applicazione.  

 Usare queste procedure per configurare i metodi di rilevamento in System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Per rilevare l'installazione di un'applicazione utilizzando il File Windows Installer  

1.  Nel **metodi di rilevamento** pagina del **Creazione guidata dell'elemento di configurazione**, selezionare il **il rilevamento di utilizzare Windows Installer** casella di controllo.  

2.  Fare clic su **Apri**, individuare il file Windows Installer (MSI) che si desidera rilevare, quindi fare clic su **Apri**.  

3.  Il **versione** è popolato automaticamente con il numero di versione del file di Windows Installer selezionato. È possibile immettere un nuovo numero di versione in questa casella se il valore visualizzato è corretto.  

4.  Selezionare la casella di controllo **Questa applicazione viene installata per uno o più utenti** se si vuole rilevare ogni profilo utente nel computer.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>Per rilevare un tipo specifico di applicazione e di distribuzione  

1.  Nella pagina **Metodi di rilevamento** della **Creazione guidata dell'elemento di configurazione**selezionare la casella di controllo **Rilevare un tipo di applicazione e distribuzione specifico** e quindi fare clic su **Seleziona**.  

2.  Nella finestra di dialogo **Specifica applicazione** selezionare l'applicazione e un tipo di distribuzione associato da rilevare.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Per rilevare l'installazione di un'applicazione con uno script personalizzato  

1.  Nel **metodi di rilevamento** pagina del **Creazione guidata dell'elemento di configurazione**, selezionare il **utilizzare uno script personalizzato per rilevare l'applicazione** casella di controllo.  

2.  Nell'elenco, selezionare la lingua dello script che si desidera aprire. Scegliere gli script seguenti:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Fare clic su **Apri**, selezionare lo script che si vuole usare e quindi fare clic su **Apri**.  

##  <a name="configure-settings"></a>Configurare le impostazioni  
 Usare questa procedura per configurare le impostazioni nell'elemento di configurazione.  

 Le impostazioni rappresentano le condizioni aziendali o tecniche usate per valutare la conformità nei dispositivi client. È possibile configurare una nuova impostazione o selezionare un'impostazione esistente in un computer di riferimento.  

1.  Nel **impostazioni** pagina del **Creazione guidata dell'elemento di configurazione**, fare clic su **New**.  

2.  Nel **Generale** scheda il **Crea impostazione** finestra di dialogo immettere le informazioni seguenti:  

    -   **Nome:** Immettere un nome univoco per l'impostazione. È possibile usare un massimo di 256 caratteri.  

    -   **Descrizione:** Immettere una descrizione per l'impostazione. È possibile usare un massimo di 256 caratteri.  

    -   **Tipo di impostazione**: scegliere dall'elenco e configurare uno dei seguenti tipi di impostazione da usare per questa impostazione:  

        -   **Query Active Directory**  

             **Prefisso LDAP** - Specificare un prefisso valido per la query di Servizi di dominio Active Directory per valutare la conformità nei computer client. È possibile utilizzare **LDAP: / /** per una o **GC: / /** per eseguire una ricerca nel catalogo globale.  

             **Nome distinto (DN)** -specificare il nome distinto dell'oggetto servizi di dominio Active Directory che viene valutata per la conformità nei computer client.  

             Ad esempio, se si vuole valutare un valore correlato a un utente chiamato John Smith nel dominio corp.contoso.com, immettere quanto segue:  

            -   **Filtro di ricerca** : specificare un filtro LDAP opzionale per rifinire i risultati derivanti dalla query Servizi di dominio Active Directory per valutare la conformità nei computer client.  

                 Per restituire tutti i risultati della query, immettere **(objectclass=\*)**.  

            -   **Ambito di ricerca**: specificare l'ambito di ricerca in Servizi di dominio Active Directory/ È possibile scegliere tra:  

                -   **Base** -query solo nell'oggetto specificato.  

                -   **Un livello**: questa opzione non è usata in questa versione di Configuration Manager.  

                -   **Sottoalbero** -l'oggetto specificato e il relativo sottoalbero completo nella directory una query.  

            -   **Proprietà** -specificare la proprietà dell'oggetto servizi di dominio Active Directory che consente di valutare la conformità nei computer client.  

                 Ad esempio, se si desidera eseguire una query la proprietà di Active Directory **badPwdCount**, che archivia il numero di volte in cui un utente immette correttamente una password, immettere **badPwdCount** in questo campo.  

            -   **Query** -Visualizza la query creata dalle voci in **prefisso LDAP**, **nome distinto (DN)**, **filtro di ricerca** (se specificato), e **proprietà**, che vengono utilizzati per valutare la conformità nei computer client.  

             Per ulteriori informazioni sulla creazione di query LDAP, vedere la documentazione di Windows Server.  

        -   **Assembly**  

             Configurare i seguenti elementi per questo tipo di impostazione:  

            -   **Nome dell'assembly:** Specifica il nome dell'oggetto assembly che si desidera cercare. Il nome non può essere quella di altri oggetti assembly dello stesso tipo e deve essere registrato nella Global Assembly Cache. Il nome dell'assembly può essere composto al massimo da 256 caratteri.  

             Un assembly è una porzione di codice che può essere condivisa tra applicazioni. Le assembly possono avere come estensione del nome file .dll o .exe. Global Assembly Cache è una cartella denominata *%systemroot%\Assembly* sul client vengono archiviati i computer in tutti gli assembly condivisi.  

        -   **File system**  

            -   **Tipo** - Nell'elenco selezionare se si vuole effettuare la ricerca di un **File** o di una **Cartella**.  

            -   **Percorso** -specificare il percorso del file specificato o della cartella nei computer client. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel percorso.  

                > [!NOTE]  
                >  Se si usa la variabile di ambiente *% USERPROFILE %* nelle caselle **Percorso** o **Nome file o cartella** , la ricerca viene eseguita in tutti i profili utente nel computer client e ciò potrebbe portare all'individuazione di più istanze del file o della cartella.  
                >   
                >  Se le impostazioni di conformità non hanno accesso al percorso specificato, viene generato un errore di individuazione. Inoltre, se il file che si sta cercando è attualmente in uso, viene generato un errore di individuazione.  

            -   **Nome file o cartella** -specificare il nome dell'oggetto per la ricerca di file o cartella. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel nome file o cartella. È inoltre possibile usare i caratteri jolly * e ? nel nome di file.  

                > [!NOTE]  
                >  Se si specifica un nome di file o cartella con i caratteri jolly, questa combinazione potrebbe produrre un numero elevato di risultati e potrebbe causare un uso elevato delle risorse nel computer client e un traffico di rete elevato per la restituzione dei risultati a Configuration Manager.  

            -   **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

            -   **Cartella o il file è associato a un'applicazione a 64 bit** - se abilitato, solo i percorsi di file a 64 bit (ad esempio *% ProgramFiles %*) viene selezionata in computer a 64 bit. Se questa opzione non è abilitata, la ricerca verrà eseguita sia nei percorsi a 32 bit (ad esempio *%ProgramFiles(x86)%*) che in quelli a 64 bit.  

                > [!NOTE]  
                >  Se nel percorso dei file del sistema a 64 e 32 bit nello stesso computer a 64 bit esiste lo stesso file o cartella, la condizione globale individuerà più file.  

             Il tipo di impostazione **File system** non supporta l'indicazione di un percorso UNC di una condivisione di rete nella casella **Percorso** .  

        -   **Metabase IIS**  

            -   **Percorso metabase** - Specificare un percorso valido per la metabase di Internet Information Services (IIS).  

            -   **ID proprietà** : specificare la proprietà numerica dell'impostazione della metabase IIS.  

        -   **Chiave del Registro di sistema**  

            -   **Hive** - Nell'elenco a discesa selezionare l'hive del Registro di sistema in cui si vuole eseguire la ricerca.  

            -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Utilizzare il formato *key\subkey*.  

            -   **Questa chiave del Registro di sistema associato a un'applicazione a 64 bit** -specifica se le chiavi del Registro di sistema a 64 bit devono essere eseguite oltre le chiavi del Registro di sistema a 32 bit su client che eseguono una versione a 64 bit di Windows.  

                > [!NOTE]  
                >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individua entrambe le chiavi.  

        -   **Valore del Registro di sistema**  

            -   **Hive** - Nell'elenco a discesa selezionare l'hive del Registro di sistema in cui si vuole eseguire la ricerca.  

            -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Utilizzare il formato *key\subkey*.  

            -   **Valore** : specificare il valore che deve essere contenuto all'interno della chiave del Registro di sistema specificato.  

            -   **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit** - Consente di specificare se effettuare la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit su client che eseguono una versione a 64 bit di Windows.  

                > [!NOTE]  
                >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individua entrambe le chiavi.  

             È anche possibile fare clic su **Sfoglia** per selezionare un percorso del Registro di sistema nel computer o in un computer remoto. Per individuare un computer remoto, è necessario disporre dei diritti di amministratore sul computer remoto e il computer remoto deve essere in esecuzione il servizio Registro di sistema remoto.  

        -   **Script**  

            -   **Script di individuazione** - Fare clic su **Aggiungi** per immetterne uno oppure selezionare lo script da usare. È possibile utilizzare gli script Windows PowerShell, VBScript o Microsoft JScript.  

            -   **Esegui script utilizzando le credenziali dell'utente connesso** - Se si abilita questa opzione, lo script verrà eseguito nei computer client che usano le credenziali degli utenti connessi.  

                > [!NOTE]  
                >  Il valore restituito dallo script viene usato per valutare la conformità della condizione globale. Ad esempio, quando si usa VBScript, si può usare il comando **WScript.Echo Result** per restituire il valore della variabile *Result* alla condizione globale.  

        -   **Query SQL**  

            -   **Istanza SQL Server** : scegliere se si desidera che la query SQL venga eseguita sul nome dell'istanza predefinita, di tutte le istanze o dell'istanza di un database specifico.  

                > [!NOTE]  
                >  Il nome dell'istanza deve fare riferimento a un'istanza locale di SQL Server. Per fare riferimento a un'istanza di SQL server del cluster, è necessario utilizzare un'impostazione script.  

            -   **Database** -specificare il nome del database Microsoft SQL Server in cui si desidera eseguire la query SQL.  

            -   **Colonna** -specificare il nome della colonna restituito dall'istruzione Transact-SQL che consente di valutare la conformità della condizione globale.  

            -   **Istruzione Transact-SQL** : specificare la query SQL completa da utilizzare per la condizione globale. È inoltre possibile fare clic su **Apri** per aprire una query SQL esistente.  

                > [!IMPORTANT]  
                >  Le impostazioni Query SQL non supportano i comandi SQL che modificano il database. È possibile usare solo comandi SQL che leggono informazioni dal database.  

        -   **Query WQL**  

            -   **Dello spazio dei nomi** -specificare lo spazio dei nomi di Strumentazione gestione Windows (WMI) che viene utilizzato per costruire una query WQL che viene valutata per la conformità nei computer client. Il valore predefinito è Root\cimv2.  

            -   **Classe** -specifica la classe WMI che consente di compilare una query WQL che viene valutata per la conformità nei computer client.  

            -   **Proprietà** -specifica la proprietà WMI che consente di compilare una query WQL che viene valutata per la conformità nei computer client.  

            -   **Clausola WHERE della query WQL** : è possibile utilizzare l'elemento **Clausola WHERE della query WQL** per specificare una clausola WHERE da applicare allo spazio dei nomi, alla classe e alla proprietà specifici nei computer client.  

        -   **Query XPath**  

            -   **Percorso** - Specificare il percorso del file XML nei computer client che verrà usato per valutare la conformità. Configuration Manager supporta l'uso di tutte le variabili di ambiente di sistema Windows e la variabile utente *%USERPROFILE%* nel nome del percorso.  

            -   **Nome del file XML** -specificare il nome del file contenente la query XML utilizzato per valutare la conformità nei computer client.  

            -   **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

            -   **Il file è associato a un'applicazione a 64 bit**: scegliere se effettuare la ricerca anche nel percorso dei file del sistema a 64 bit (*%windir%*\System32), oltre al percorso dei file del sistema a 32 bit (*%windir%*\Syswow64) nei client di Configuration Manager che eseguono una versione a 64 bit di Windows.  

            -   **Query XPath** -specificare una valido XML path language (XPath) query completa che consente di valutare la conformità nei computer client.  

            -   **Spazi dei nomi** - Apre la finestra di dialogo **Spazi dei nomi XML** per individuare gli spazi dei nomi e i prefissi da usare durante la query XPath.  

             Se si tenta di individuare un file XML crittografato, le impostazioni di conformità trovano il file, ma la query XPath non genera alcun risultato e non viene generato alcun errore.  

             Se la query XPath non è valida, l'impostazione viene valutata come non conforme nei computer client.  

    -   **Tipo di dati:** nell'elenco scegliere il formato in cui la condizione restituisce i dati prima che vengano usati per valutare l'impostazione. Il **tipo di dati** elenco non viene visualizzata per tutti i tipi di impostazione.  

        > [!NOTE]  
        >  Il **a virgola mobile** tipo di dati supporta solo 3 cifre dopo il separatore decimale.  

3.  Configurare ulteriori dettagli su questa impostazione sotto il **impostazione tipo** elenco. Gli elementi che è possibile configurare variano a seconda del tipo di impostazione che è stata selezionata.  

    > [!NOTE]  
    >  Quando si creano le impostazioni del tipo **File system**, **chiave del Registro di sistema**, e **il valore del Registro di sistema**, è possibile fare clic **Sfoglia** per configurare l'impostazione di valori in un computer di riferimento. Per selezionare una chiave del Registro di sistema o un valore in un computer remoto, il computer remoto deve essere il servizio Registro di sistema remoto abilitato.  

4.  Fare clic su **OK** per salvare l'impostazione e chiudere la finestra di dialogo **Crea impostazione** .  

##  <a name="configure-compliance-rules"></a>Configurare le regole di conformità  
 Usare la procedura seguente per configurare le regole di conformità per l'elemento di configurazione.  

 Le regole di conformità consentono di specificare le condizioni che definiscono la conformità di un elemento di configurazione. Prima che sia possibile valutare la conformità di un'impostazione, è necessario che tale impostazione disponga almeno di una regola di conformità. Le impostazioni per WMI, Registro di sistema e script consentono di monitorare e aggiornare i valori che risultano non conformi. È possibile creare nuove regole o passare a un'impostazione esistente in qualsiasi elemento di configurazione per selezionare le regole in essa contenute.  

### <a name="to-create-a-compliance-rule"></a>Per creare una regola di conformità  

1.  Nel **le regole di conformità** pagina del **Creazione guidata dell'elemento di configurazione**, fare clic su **New**.  

2.  Nel **Create Rule** finestra di dialogo immettere le informazioni seguenti:  

    -   **Nome:** Immettere un nome per la regola di conformità.  

    -   **Descrizione:** Immettere una descrizione per la regola di conformità.  

    -   **Impostazione selezionata:** Fare clic su **Sfoglia** per aprire la **Select impostazione** nella finestra di dialogo. Selezionare l'impostazione che si desidera definire una regola per oppure fare clic su **nuova impostazione**. Al termine, fare clic su **selezionare**.  

        > [!NOTE]  
        >  È inoltre possibile fare clic su **proprietà** per visualizzare informazioni sull'impostazione attualmente selezionata.  

    -   **Tipo di regola:** Selezionare il tipo di regola di conformità che si desidera utilizzare:  

        -   **Valore** creare una regola che confronta il valore restituito dall'elemento di configurazione con un valore specificato dall'utente.  

        -   **Existential** creare una regola che restituisce l'impostazione a seconda se esistente in un dispositivo client o sul numero di volte in cui viene trovato.  

    -   Per un tipo di regola di **valore**, specificare le seguenti informazioni:  

        -   **L'impostazione deve essere conforme alle regole seguenti** : selezionare un operatore e un valore che viene valutato per la conformità con l'impostazione selezionata. È possibile utilizzare gli operatori seguenti:  

            |Operator|Altre informazioni|  
            |--------------|----------------------|  
            |Uguale a|Nessuna informazione aggiuntiva|  
            |Diverso da|Nessuna informazione aggiuntiva|  
            |Maggiore di|Nessuna informazione aggiuntiva|  
            |Minore di|Nessuna informazione aggiuntiva|  
            |Tra|Nessuna informazione aggiuntiva|  
            |Maggiore o uguale a|Nessuna informazione aggiuntiva|  
            |Minore o uguale a|Nessuna informazione aggiuntiva|  
            |Uno|Nella casella di testo, specificare una voce per ogni riga.|  
            |Nessuno|Nella casella di testo, specificare una voce per ogni riga.|  

        -   **Monitora e aggiorna le regole non conformi, se supportato** : selezionare questa opzione se si vuole monitorare e aggiornare automaticamente le regole non conformi mediante Configuration Manager. Configuration Manager consente di correggere automaticamente i tipi di regole seguenti:  

            -   **Il valore del Registro di sistema** – il valore del Registro di sistema è aggiornato, se è conforme e creato se non esiste.  

            -   **Script** (eseguendo automaticamente uno script di monitoraggio e aggiornamento).  

            -   **Query WQL**  

            > [!IMPORTANT]  
            >  È possibile correggere le regole non conformi solo quando l'operatore per la regola è impostato su **Uguale a**.  

        -   **Report non conformità, se questa istanza di impostazione non viene trovata** : l'elemento di configurazione segnala la non conformità, se questa impostazione non viene trovata nei computer client.  

        -   **Gravità della non conformità per i report:** specificare il livello di gravità che viene segnalato nei report di Configuration Manager se si verifica un errore di questa regola di conformità. I livelli di gravità disponibili sono i seguenti:  

            -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore.  

            -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni**.  

            -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Avviso**.  

            -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Critico**.  

            -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico**. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  

        -   Per il tipo di regola **Esistenziale**specificare le informazioni seguenti:  

            > [!NOTE]  
            >  Le opzioni visualizzate potrebbero variare a seconda del tipo di impostazione per cui si sta configurando una regola.  

            -   **L'impostazione deve esistere in dispositivi client**  

            -   **L'impostazione non deve esistere in dispositivi client**  

            -   **L'impostazione è presente il seguente numero di volte:**  

        -   **Gravità della non conformità per i report:** specificare il livello di gravità che viene segnalato nei report di Configuration Manager se si verifica un errore di questa regola di conformità. I livelli di gravità disponibili sono i seguenti:  

            -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore.  

            -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni**.  

            -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Avviso**.  

            -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Critico**.  

            -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico**. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  

3.  Fare clic su **OK** per chiudere la finestra di dialogo **Crea regola** .  

##  <a name="specify-supported-platforms"></a>Specificare le piattaforme supportate  
 Le piattaforme supportate sono i sistemi operativi in cui viene valutata la conformità di un elemento di configurazione.  

Nella pagina **Piattaforme supportate** della **Creazione guidata dell'elemento di configurazione**selezionare nell'elenco le versioni di Windows in cui si vuole valutare la conformità dell'elemento di configurazione oppure fare clic su **Seleziona tutto**.  

## <a name="complete-the-wizard"></a>Completare la procedura guidata  
 Nella pagina **Riepilogo** della procedura guidata verificare le azioni che verranno eseguite e quindi completare la procedura guidata. Nuovo elemento di configurazione viene visualizzato nel **gli elementi di configurazione** nodo il **asset e conformità** area di lavoro.  
