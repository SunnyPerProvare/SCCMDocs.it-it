---
title: Creare elementi di configurazione personalizzati
titleSuffix: Configuration Manager
description: È possibile gestire le impostazioni per i computer e i server Windows usando un elemento di configurazione personalizzato per computer desktop e server Windows
ms.date: 03/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c875c27698c02dff552c499b2c8ef63b5be209d
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75816497"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Creare elementi di configurazione personalizzati per computer desktop e server Windows gestiti con il client di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*


Usare l'elemento di configurazione **personalizzato per computer desktop e server Windows** di Configuration Manager per gestire le impostazioni per i computer e server Windows gestiti dal client di Configuration Manager.  



## <a name="start-the-wizard"></a>Avviare la procedura guidata

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il nodo **Elementi di configurazione**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Crea elemento di configurazione** nel gruppo **Crea**.  

3. Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  

4. In **Specificare il tipo di elemento di configurazione da creare**selezionare **Desktop e server di Windows (personalizzato)** .  

    > [!TIP]  
    > Per specificare le impostazioni del metodo di rilevamento che consentono di controllare l'esistenza di un'applicazione, selezionare **Questo elemento di configurazione contiene le impostazioni dell'applicazione**.  

5. Per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager, selezionare **Categorie** per creare e assegnare categorie.  



## <a name="detection-methods"></a>Metodi di rilevamento  

Usare questa procedura per fornire informazioni sul metodo di rilevamento per l'elemento di configurazione.  

> [!NOTE]  
> Queste informazioni si applicano solo se si seleziona **Questo elemento di configurazione contiene le impostazioni dell'applicazione** nella pagina **Generale** della procedura guidata.  

Un metodo di rilevamento in Configuration Manager contiene regole che consentono di rilevare se un'applicazione viene installata in un computer. Questo rilevamento si verifica prima che il client valuti la conformità per l'elemento di configurazione. Per rilevare se un'applicazione è installata, è possibile rilevare la presenza di un file Windows Installer per l'applicazione, utilizzare uno script personalizzato o selezionare **presupporre sempre l'applicazione viene installata** per valutare l'elemento di configurazione per la conformità, anche se è installata l'applicazione.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Per rilevare l'installazione di un'applicazione usando il file di Windows Installer  

1. Nella pagina **Metodi di rilevamento** della **Creazione guidata dell'elemento di configurazione** selezionare l'opzione **Utilizza rilevamento di Windows Installer**.  

2. Selezionare su **Apri**, individuare il file di Windows Installer (MSI) che si vuole rilevare e quindi selezionare **Apri**.  

3. Il campo della **versione** viene popolato automaticamente con il numero di versione del file di Windows Installer. Se il valore visualizzato non è corretto, immettere qui un nuovo numero di versione.  

4. Se si vuole rilevare ogni profilo utente nel computer, selezionare **Questa applicazione viene installata per uno o più utenti**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Per rilevare un tipo specifico di applicazione e di distribuzione  

1. Nella pagina **Metodi di rilevamento** della **Creazione guidata dell'elemento di configurazione** selezionare **Rilevare un tipo di applicazione e distribuzione specifico**. Scegliere **Seleziona**.   

2. Nella finestra di dialogo **Specifica applicazione** selezionare l'applicazione e un tipo di distribuzione associato da rilevare.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Per rilevare l'installazione di un'applicazione con uno script personalizzato  

1. Nella pagina **Metodi di rilevamento** della **Creazione guidata dell'elemento di configurazione** selezionare l'opzione **Utilizza script personalizzato per rilevare l'applicazione**.  

2. Nell'elenco selezionare la lingua dello script. Scegliere uno dei formati seguenti:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > A partire dalla versione 1810, quando si esegue uno script di Windows PowerShell come metodo di rilevamento, il client di Configuration Manager chiama PowerShell con il parametro `-NoProfile`. Questa opzione avvia PowerShell senza i profili. Un profilo di PowerShell è uno script che viene eseguito all'avvio di PowerShell. <!--3607762-->  

3. Selezionare **Apri**, selezionare lo script che si vuole usare e quindi selezionare **Apri**.  



##  <a name="specify-supported-platforms"></a>Specificare le piattaforme supportate  

Nella pagina **Piattaforme supportate** della **Creazione guidata dell'elemento di configurazione** selezionare le versioni di Windows in cui si vuole valutare la conformità dell'elemento di configurazione oppure scegliere **Seleziona tutto**. 

È anche possibile **specificare manualmente la versione di Windows**. Selezionare **Aggiungi** e specificare ogni parte del numero di build di Windows. 



##  <a name="configure-settings"></a>Configurare le impostazioni  

Usare questa procedura per configurare le impostazioni nell'elemento di configurazione.  

Le impostazioni rappresentano le condizioni aziendali o tecniche usate per valutare la conformità nei dispositivi client. È possibile configurare una nuova impostazione o selezionare un'impostazione esistente in un computer di riferimento.  

1. Nella pagina **Impostazioni** della **Creazione guidata dell'elemento di configurazione** selezionare **Nuovo**.  

2. Nel **Generale** scheda il **Crea impostazione** finestra di dialogo immettere le informazioni seguenti:  

    - **Nome**: immettere un nome univoco per l'impostazione. È possibile usare un massimo di 256 caratteri.  

    - **Descrizione**: immettere una descrizione per l'impostazione. È possibile usare un massimo di 256 caratteri.  

    - **Tipo di impostazione**: scegliere dall'elenco e configurare uno dei seguenti tipi di impostazione da usare per questa impostazione:  
        - [Query Active Directory](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [File system](#bkmk_file)
        - [Metabase IIS](#bkmk_iis)
        - [Chiave del Registro di sistema](#bkmk_regkey)
        - [Valore del Registro di sistema](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Query SQL](#bkmk_sql)
        - [Query WQL](#bkmk_wql)
        - [Query XPath](#bkmk_xpath)

    - **Tipo di dati**: nell'elenco scegliere il formato in cui la condizione restituisce i dati prima che vengano usati per valutare l'impostazione. L'elenco **Tipo di dati** non viene visualizzato per tutti i tipi di impostazioni.  

        > [!Tip]  
        > Il tipo di dati **Virgola mobile** supporta solo tre cifre dopo il separatore decimale.  

3. Configurare ulteriori dettagli su questa impostazione sotto il **impostazione tipo** elenco. Gli elementi che è possibile configurare variano a seconda del tipo di impostazione selezionata.  

4. Selezionare **OK** per salvare l'impostazione e chiudere la finestra di dialogo **Crea impostazione**.  


### <a name="bkmk_adquery"></a> Query Active Directory

- **Prefisso LDAP**: specificare un prefisso valido per la query di Active Directory Domain Services per valutare la conformità nei computer client. Per eseguire una ricerca nel catalogo globale, usare `LDAP://` o `GC://`.  

- **Nome distinto (DN)** : specificare il nome distinto dell'oggetto Active Directory Domain Services che viene valutato per la conformità nei computer client.  

- **Filtro di ricerca**: specificare un filtro LDAP facoltativo per rifinire i risultati derivanti dalla query Active Directory Domain Services per valutare la conformità nei computer client. Per restituire tutti i risultati della query, immettere `(objectclass=*)`.  

- **Ambito di ricerca**: specificare l'ambito di ricerca in Active Directory Domain Services  

    - **Base**: esegue una query solo dell'oggetto specificato  

    - **Un livello**: questa opzione non è usata in questa versione di Configuration Manager  

    - **Sottoalbero**: esegue una query dell'oggetto specificato e il relativo sottoalbero completo nella directory  

- **Proprietà**: specificare la proprietà dell'oggetto Active Directory Domain Services che consente di valutare la conformità nei computer client.  

    Ad esempio, se si vuole eseguire una query per la proprietà di Active Directory che archivia il numero di volte in cui un utente digita una password in modo non corretto, immettere `badPwdCount` in questo campo.  

- **Query**: visualizza la query creata dalle voci in **Prefisso LDAP**, **Nome distinto (DN)** , **Filtro di ricerca** (se specificato) e **Proprietà**.  


### <a name="bkmk_assembly"></a> Assembly

Un assembly è una porzione di codice che può essere condivisa tra applicazioni. Le assembly possono avere come estensione del nome file .dll o .exe. Il Global Assembly Cache è la cartella `%SystemRoot%\Assembly` nei computer client. Questa cache è il punto in cui Windows archivia tutti gli assembly condivisi.  

- **Nome dell'assembly:** specifica il nome dell'oggetto assembly che si vuole cercare. Il nome non può essere uguale ad altri oggetti assembly dello stesso tipo. Prima di tutto, registrarlo nel Global Assembly Cache. Il nome dell'assembly può essere composto al massimo da 256 caratteri.  


### <a name="bkmk_file"></a> File system

- **Tipo**: nell'elenco selezionare se si vuole eseguire la ricerca di un **File** o di una **Cartella**.  

- **Percorso**: specificare il percorso del file o della cartella specificati nei computer client. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente `%USERPROFILE%` nel percorso.  

    > [!NOTE]  
    > Se si usa la variabile di ambiente `%USERPROFILE%` nelle caselle **percorso** o **nome file o cartella** , il client di Configuration Manager Cerca tutti i profili utente nel computer client. Questo comportamento potrebbe determinare la ricerca di più istanze del file o della cartella.  
    >   
    > Se le impostazioni di conformità non hanno accesso al percorso specificato, viene generato un errore di individuazione. Inoltre, se il file che si sta cercando è attualmente in uso, viene generato un errore di individuazione.  

    > [!Tip]  
    > Selezionare **Sfoglia** per configurare l'impostazione dai valori in un computer di riferimento.   

- **Nome file o cartella**: specificare il nome dell'oggetto file o cartella per la ricerca. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente `%USERPROFILE%` nel nome di file o cartella. È anche possibile usare i caratteri jolly `*` e `?` nel nome file.  

    > [!NOTE]  
    > Se si specifica un nome di file o cartella e si usano caratteri jolly, questa combinazione potrebbe produrre un numero elevato di risultati. Potrebbe anche portare a un uso elevato delle risorse nei computer client e a un intenso traffico di rete per la restituzione dei risultati a Configuration Manager.  

- **Includi sottocartelle**: Cerca anche le sottocartelle nel percorso specificato.  

- **Il file o la cartella sono associati a un'applicazione a 64 bit**: se abilitata, Cerca solo i percorsi dei file a 64 bit, ad esempio `%ProgramFiles%` nei computer a 64 bit. Se questa opzione non è abilitata, cercare i percorsi a 64 bit e a 32 bit, ad esempio `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Se nel percorso dei file del sistema a 64 e 32 bit nello stesso computer a 64 bit esiste lo stesso file o cartella, la condizione globale individuerà più file.  

    Il tipo di impostazione **File system** non supporta l'indicazione di un percorso UNC di una condivisione di rete nel campo **Percorso**.  


### <a name="bkmk_iis"></a> Metabase IIS

- **Percorso metabase**: specificare un percorso valido per la metabase di Internet Information Services (IIS). Ad esempio, `/LM/W3SVC/`  

- **ID proprietà**: specificare la proprietà numerica dell'impostazione della metabase IIS.  


### <a name="bkmk_regkey"></a> Chiave del Registro di sistema

- **Hive**: selezionare l'hive del registro di sistema in cui si vuole eseguire la ricerca

    > [!Tip]  
    > Selezionare **Sfoglia** per configurare l'impostazione dai valori in un computer di riferimento. Per passare a una chiave del registro di sistema in un computer remoto, abilitare il servizio **Registro di sistema remoto** nel computer remoto.  

- **Chiave**: specificare il nome della chiave del Registro di sistema che si vuole cercare. Usare il formato `key\subkey`.  

- **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit**: consente di eseguire la ricerca anche nelle chiavi del Registro di sistema a 64 bit, oltre che nelle chiavi del Registro di sistema a 32 bit, nei client che eseguono una versione a 64 bit di Windows.  

    > [!NOTE]  
    > Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individua entrambe le chiavi.  


### <a name="bkmk_regval"></a> Valore del Registro di sistema

- **Hive**: selezionare l'hive del registro di sistema in cui eseguire la ricerca.  

    > [!Tip]  
    > Selezionare **Sfoglia** per configurare l'impostazione dai valori in un computer di riferimento. Per passare a un valore del registro di sistema in un computer remoto, abilitare il servizio **Registro di sistema remoto** nel computer remoto. Sono inoltre necessarie le autorizzazioni di amministratore per accedere al computer remoto.  

- **Chiave**: specificare il nome della chiave del registro di sistema da cercare. Usare il formato `key\subkey`.  

- **Valore**: specificare il valore che deve essere contenuto nella chiave del Registro di sistema specificata.  

- **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit**: consente di eseguire la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit, nei client che eseguono una versione a 64 bit di Windows.  

    > [!NOTE]  
    > Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individua entrambe le chiavi.  


### <a name="bkmk_script"></a> Script

Il valore restituito dallo script viene usato per valutare la conformità della condizione globale. Ad esempio, quando si usa VBScript, si può usare il comando **WScript.Echo Result** per restituire il valore della variabile *Result* alla condizione globale.  

- **Script di individuazione**: selezionare **Aggiungi script**e immettere o selezionare uno script. Questo script viene usato per trovare il valore. È possibile utilizzare gli script Windows PowerShell, VBScript o Microsoft JScript.  

- **Script di monitoraggio e aggiornamento (facoltativo)** : selezionare **Aggiungi script**e immettere o selezionare uno script. Questo script viene usato per monitorare e aggiornare i valori delle impostazioni non conformi. È possibile utilizzare gli script Windows PowerShell, VBScript o Microsoft JScript.  

- **Esegui script utilizzando le credenziali dell'utente connesso**: se si abilita questa opzione, lo script viene eseguito nei computer client che usano le credenziali dell'utente connesso.  

> [!Note]  
> A partire dalla versione 1810, quando si usa Windows PowerShell come uno script di individuazione o monitoraggio e aggiornamento, il client Configuration Manager chiama PowerShell con il parametro `-NoProfile`. Questa opzione avvia PowerShell senza i profili. Un profilo di PowerShell è uno script che viene eseguito all'avvio di PowerShell. <!--3607762-->  


### <a name="bkmk_sql"></a> Query SQL

- **Istanza SQL Server**: scegliere se si vuole che la query SQL venga eseguita nell'istanza predefinita, in tutte le istanze o nell'istanza di database specificata.  

    > [!NOTE]  
    > Il nome dell'istanza deve fare riferimento a un'istanza locale di SQL Server. Per fare riferimento a un'istanza di SQL server del cluster, è necessario utilizzare un'impostazione script.  

- **Database**: specificare il nome del database Microsoft SQL Server in cui si vuole eseguire la query SQL.  

- **Column** (Colonna): specificare il nome della colonna restituito dall'istruzione Transact-SQL usata per valutare la conformità della condizione globale.  

- **Istruzione Transact-SQL**: specificare la query SQL completa da usare per la condizione globale. Per usare una query SQL esistente, selezionare **Apri**.  

    > [!IMPORTANT]  
    > Le impostazioni Query SQL non supportano i comandi SQL che modificano il database. È possibile usare solo comandi SQL che leggono informazioni dal database.  


### <a name="bkmk_wql"></a> Query WQL

- **Spazio dei nomi**: specificare lo spazio dei nomi WMI che viene valutato per la conformità nei computer client. Il valore predefinito è `root\cimv2`.  

- **Classe**: specificare la classe WMI di destinazione nello spazio dei nomi sopra riportato.  

- **Proprietà**: specificare la proprietà WMI di destinazione nella classe precedente.  

- **Clausola WHERE della query WQL**: specificare una clausola di qualificazione per ridurre i risultati. Ad esempio, per eseguire una query solo sul servizio DHCP nella classe Win32_Service, è possibile `Name = 'DHCP' and StartMode = 'Auto'`la clausola WHERE.   


### <a name="bkmk_xpath"></a> Query XPath

- **Percorso**: specificare il percorso del file XML nei computer client che viene usato per valutare la conformità. Configuration Manager supporta l'uso di tutte le variabili di ambiente di sistema Windows e della variabile utente `%USERPROFILE%` nel nome del percorso.  

- **Nome file XML**: specificare il nome file contenente la query XML nel percorso precedente.  

- **Includi sottocartelle**: abilitare questa opzione per eseguire la ricerca anche nelle eventuali sottocartelle nel percorso specificato.  

- **Questo file è associato a un'applicazione a 64 bit**: eseguire una ricerca nel percorso dei file di sistema a 64 bit `%Windir%\System32` oltre al percorso dei file del sistema a 32 bit `%Windir%\Syswow64` nei client Configuration Manager che eseguono una versione di Windows a 64 bit.  

- **Query XPath**: specificare una query XPath (XML Path Language) valida.  

- **Spazi dei nomi**: identificare gli spazi dei nomi e i prefissi da utilizzare durante la query XPath.  

Se si tenta di individuare un file XML crittografato, le impostazioni di conformità trovano il file, ma la query XPath non genera alcun risultato. Il client Configuration Manager non genera un errore.  

Se la query XPath non è valida, l'impostazione viene valutata come non conforme nei computer client.  



##  <a name="configure-compliance-rules"></a>Configurare le regole di conformità  

Le regole di conformità consentono di specificare le condizioni che definiscono la conformità di un elemento di configurazione. Prima che sia possibile valutare la conformità di un'impostazione, è necessario che tale impostazione disponga almeno di una regola di conformità. Le impostazioni per WMI, Registro di sistema e script consentono di monitorare e aggiornare i valori che risultano non conformi. È possibile creare nuove regole o passare a un'impostazione esistente in qualsiasi elemento di configurazione per selezionare le regole in essa contenute.  


### <a name="to-create-a-compliance-rule"></a>Per creare una regola di conformità  

1. Nella pagina **Regole di conformità** della **Creazione guidata dell'elemento di configurazione** selezionare **Nuovo**.  

2. Nel **Create Rule** finestra di dialogo immettere le informazioni seguenti:  

    - **Nome**: immettere un nome per la regola di conformità.  

    - **Descrizione**: immettere una descrizione per la regola di conformità.  

    - **Impostazione selezionata**: selezionare **Sfoglia** per aprire la finestra di dialogo **Seleziona impostazione**. Selezionare l'impostazione per cui si vuole definire una regola o selezionare **Nuova impostazione**. Al termine, scegliere **Seleziona**.  

        > [!Tip]  
        > Per visualizzare informazioni sull'impostazione attualmente selezionata, selezionare **Proprietà**.  

    - **Tipo di regola**: selezionare il tipo di regola di conformità che si vuole usare:  

        - **Valore**: creare una regola che confronta il valore restituito dall'elemento di configurazione con un valore specificato dall'utente. Per ulteriori informazioni sulle impostazioni aggiuntive, vedere [regole relative ai valori](#bkmk_value).  

        - **Esistenziale**: creare una regola che valuta l'impostazione a seconda che esista in un dispositivo client oppure a seconda del numero di occorrenze trovate. Per ulteriori informazioni sulle impostazioni aggiuntive, vedere [regole esistenziali](#bkmk_exist).  

3. Selezionare **OK** per chiudere la finestra di dialogo **Crea regola**.  




### <a name="bkmk_value"></a>Regole relative ai valori  

- **Property**: la proprietà dell'oggetto da controllare varia in base all'impostazione selezionata. Le proprietà disponibili variano in base al tipo di impostazione. 

- **L'impostazione deve essere conforme alle seguenti...** : le regole o le autorizzazioni disponibili variano in base al tipo di impostazione.

- **Monitora e aggiorna le regole non conformi, se supportato**: selezionare questa opzione se si vuole monitorare e aggiornare automaticamente le regole non conformi tramite Configuration Manager. Configuration Manager supporta questa azione con i tipi di regole seguenti:  

    - **Valore del registro di sistema**: se non è conforme, il client imposta il valore del registro di sistema. Se non esiste, il client crea il valore.  

    - **Script**: il client usa lo script di monitoraggio e aggiornamento specificato con l'impostazione.  

    - **Query WQL**  

    > [!IMPORTANT]  
    > È possibile correggere le regole non conformi solo quando l'operatore per la regola è impostato su **Uguale a**.  

- Segnala la mancata **conformità se questa istanza dell'impostazione non viene trovata**: se questa impostazione non viene trovata nei computer client, abilitare questa opzione per l'elemento di configurazione per segnalare la mancata conformità.  

- **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato nei report di Configuration Manager se si verifica un errore di questa regola di conformità. Sono disponibili i livelli di gravità seguenti:  
    - **Nessuno**  
    - **Informazioni**  
    - **Avviso**  
    - **Errore critico**  
    - **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Critico**. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  


### <a name="bkmk_exist"></a>Regole esistenziali 

> [!NOTE]  
> Le opzioni visualizzate potrebbero variare a seconda del tipo di impostazione per cui si sta configurando una regola.  

- **L'impostazione deve esistere in dispositivi client**  

- **L'impostazione non deve esistere in dispositivi client**  

- **L'impostazione è presente il seguente numero di volte:**  

- **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato nei report di Configuration Manager se si verifica un errore di questa regola di conformità. Sono disponibili i livelli di gravità seguenti:  
    - **Nessuno**  
    - **Informazioni**  
    - **Avviso**  
    - **Errore critico**  
    - **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità errore del tipo **Critico**. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  



## <a name="next-steps"></a>Passaggi successivi

[Creare linee di base di configurazione](/sccm/compliance/deploy-use/create-configuration-baselines)
