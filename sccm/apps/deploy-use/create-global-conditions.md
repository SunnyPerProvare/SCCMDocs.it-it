---
title: Creare condizioni globali | System Center Configuration Manager
description: "È possibile creare condizioni globali per specificare la modalità in cui un'applicazione viene resa disponibile e distribuita nei dispositivi client."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4dfe52d5537d83d5ea17d1da4984e05d2a92cde


---
# <a name="how-to-create-global-conditions-in-system-center-configuration-manager"></a>Come creare condizioni globali in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le condizioni globali sono regole che rappresentano le condizioni tecniche o aziendali che l'utente può usare per specificare il modo in cui un'applicazione viene distribuita e resa disponibile per i dispositivi client. Le condizioni globali sono accessibili dalla pagina **Requisiti** della Creazione guidata tipo di distribuzione.  

> [!NOTE]  
>  È possibile modificare le condizioni globali solo dal sito in cui sono state create.  

 Usare le procedure seguenti per creare le condizioni globali di Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fornire informazioni di base sulla condizione globale  
 Sono disponibili diversi tipi di condizioni globali. Opzioni diverse sono associate a diversi tipi di condizione globale. Quando si seleziona un tipo specifico di condizione globale, Configuration Manager visualizza le opzioni che si applicano a quella selezione.  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Condizioni globali**.  

3.  Nella scheda **Home** del gruppo **Crea** , fare clic su **Crea condizione globale**.  

4.  Nella finestra di dialogo **Crea condizione globale** , fornire un nome e una descrizione opzionale per la condizione globale.  

5.  Nell'elenco a discesa **Tipo di dispositivo** scegliere se la condizione globale è per un computer **Windows** o un dispositivo **Windows Mobile**.  

6.  Nell'elenco a discesa **Tipo di condizione** , scegliere una delle seguenti opzioni:  

    -   **Impostazione** : questa opzione consente di controllare l'esistenza di uno o più elementi su dispositivi client. Ad esempio, è possibile controllare la presenza di un particolare file, cartella o valore della chiave del Registro di sistema su un dispositivo client.  

    -   **Espressione** : questa opzione consente di configurare regole più complesse per determinare se la condizione viene soddisfatta su dispositivi client. Ad esempio, è possibile determinare se la memoria fisica su un computer è tra i 2 e i 4 GB oppure per determinare se un dispositivo mobile utilizza un touch-screen per gli input.  

## <a name="configure-rules-for-the-global-condition"></a>Configurare le regole per la condizione globale  
 La procedura per la definizione delle regole delle condizioni globali è diversa a seconda della configurazione di un'impostazione o un'espressione. Utilizzare la procedura applicabile presentata di seguito per configurare un'impostazione o un'espressione per la condizione globale.  

### <a name="to-configure-a-setting-for-the-global-condition"></a>Per configurare un'impostazione per la condizione globale  

1.  Nell'elenco a discesa **Tipo di condizione** , scegliere **Impostazione**.  

2.  Nell'elenco a discesa **Tipo di impostazione** , scegliere l'elemento da utilizzare come condizione per cui verranno controllati i requisiti. Sono disponibili i seguenti tipi di impostazione e configurazione.  

    -   **Query Active Directory**  

        -   **Prefisso LDAP** : specificare un prefisso LDAP valido per la query Servizi di dominio Active Directory per valutare la conformità nei computer client. È possibile usare **LDAP://** o **GC://**.  

        -   **Nome distinto (DN)** : specificare il nome distinto dell'oggetto Servizi di dominio Active Directory che sarà valutato per la conformità nei computer client.  

        -   **Filtro di ricerca** : specificare un filtro LDAP opzionale per rifinire i risultati derivanti dalla query Servizi di dominio Active Directory per valutare la conformità nei computer client.  

        -   **Ambito di ricerca** : specificare l'ambito di ricerca in Servizi di dominio Active Directory:  

            -   **Base** : esegue una query solo dell'oggetto specificato.  

            -   **Un livello**: questa opzione non è usata in questa versione di Configuration Manager.  

            -   **Sottoalbero** : esegue una query dell'oggetto specificato e il relativo sottoalbero completo nella directory.  

        -   **Proprietà** : specificare la proprietà dell'oggetto Servizi di dominio Active Directory che sarà utilizzato per valutare la conformità nei computer client.  

        -   **Query** : visualizza la query LDAP creata dalle voci in **Prefisso LDAP**, **Nome distinto (DN)**, **Filtro di ricerca** se specificati e **Proprietà**. Questa query verrà utilizzata per valutare la conformità nei computer client.  

    -   **Assembly**  

        -   **Nome assembly** : specifica il nome dell'oggetto assembly da cercare. Il nome non può essere lo stesso di qualsiasi altro oggetto assembly dello stesso tipo e deve essere registrato nella cache di assembly globale. Il nome dell'assembly può contenere un massimo di 256 caratteri.  

        > [!NOTE]  
        >  Un assembly è una porzione di codice che può essere condivisa tra applicazioni. Le assembly possono avere come estensione del nome file .dll o .exe. La cache di assembly globale è una cartella denominata *%systemroot%\assembly* nei computer client in cui sono memorizzati tutti gli assembly condivisi.  

    -   **File system**  

        -   **Tipo** : dall'elenco a discesa, selezionare se si desidera effettuare la ricerca di un **File** o di una **Cartella**.  

        -   **Percorso** : specificare il percorso al file o alla cartella specificati nei computer client. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel percorso.  

            > [!NOTE]  
            >  Se si utilizza la variabile di ambiente *%USERPROFILE%* nei campi **Percorso** o **Nome file o cartella** , verrà effettuata la ricerca di tutti i profili utente sui computer client. Ciò potrebbe causare l'individuazione di più istanze del file o della cartella.  

        -   **Nome file o cartella** : specificare il nome dell'oggetto file o cartella di cui verrà effettuata la ricerca. È possibile specificare le variabili di ambiente relative al sistema e la variabile di ambiente *%USERPROFILE%* nel nome file o cartella. È inoltre possibile usare i caratteri jolly * e ? nel nome file.  

            > [!NOTE]  
            >  Se si specifica un nome file o cartella e si utilizzano dei caratteri jolly, ciò potrebbe produrre un numero elevato di risultati. Questo potrebbe portare a un elevato utilizzo delle risorse nei computer client e anche a un elevato traffico di rete quando si segnalano i risultati a Configuration Manager.  

        -   **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

        -   **Il file o la cartella sono associati a un'applicazione a 64 bit**: scegliere se effettuare la ricerca anche nel percorso dei file del sistema a 64 bit (*%windir%*\system32), oltre al percorso dei file del sistema a 32 bit (*%windir%*\syswow64) nei client di Configuration Manager con una versione a 64 bit di Windows.  

            > [!NOTE]  
            >  Se nel percorso dei file del sistema a 64 e 32 bit sullo stesso computer a 64 bit esiste lo stesso file o cartella, la condizione globale individuerà più file.  

         Il tipo di impostazione **File system** non supporta la specificazione di un percorso UNC in una condivisione di rete nel campo **Percorso** .  

    -   **Metabase IIS**  

        -   **Percorso metabase** : specificare un percorso valido per la metabase IIS.  

        -   **ID proprietà** : specificare la proprietà numerica dell'impostazione della metabase IIS.  

    -   **Chiave del Registro di sistema**  

        -   **Hive** : dall'elenco a discesa, selezionare l'hive del Registro di sistema in cui si desidera effettuare la ricerca.  

        -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Il formato utilizzato deve essere *key\subkey*.  

        -   **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit** : consente di specificare se effettuare la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit su client con una versione a 64 bit di Windows.  

            > [!NOTE]  
            >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individuerà più chiavi del Registro di sistema.  

    -   **Valore del Registro di sistema**  

        -   **Hive** : dall'elenco a discesa, selezionare l'hive del Registro di sistema in cui si desidera effettuare la ricerca.  

        -   **Chiave** : specificare il nome della chiave del Registro di sistema in cui si desidera effettuare la ricerca. Il formato utilizzato deve essere *key\subkey*.  

        -   **Valore** : specificare il valore che deve essere contenuto all'interno della chiave del Registro di sistema specificato.  

        -   **Questa chiave del Registro di sistema è associata a un'applicazione a 64 bit** : consente di specificare se effettuare la ricerca anche tra le chiavi del Registro di sistema a 64 bit, oltre alle chiavi del Registro di sistema a 32 bit su client con una versione a 64 bit di Windows.  

            > [!NOTE]  
            >  Se la stessa chiave del Registro di sistema esiste nei percorsi dei Registri di sistema a 64 e 32 bit sullo stesso computer a 64 bit, la condizione globale individuerà più chiavi del Registro di sistema.  

    -   **Script**  

        -   **Script di individuazione** : fare clic su **Aggiungi** per immetterne uno oppure selezionare lo script da utilizzare. È possibile utilizzare gli script di Windows PowerShell, VBScript o JScript.  

        -   **Esegui script utilizzando le credenziali dell'utente connesso** : se si abilita questa opzione, lo script verrà eseguito nei computer client utilizzando le credenziali degli utenti connessi.  

            > [!NOTE]  
            >  Il valore restituito dallo script verrà utilizzato per valutare la conformità della condizione globale. Ad esempio, quando si utilizza VBScript, si può utilizzare il comando **Risultato WScript.Echo** per restituire il valore della variabile Risultato alla condizione globale.  
            >   
            >  Se lo script restituisce più valori, questi valori devono essere su una singola riga, separati da un punto e virgola. Se ogni valore si trova su una riga distinta, la valutazione avrà esito negativo.  

    -   **Query SQL**  

        -   **Istanza SQL Server** : scegliere se si desidera che la query SQL venga eseguita sul nome dell'istanza predefinita, di tutte le istanze o dell'istanza di un database specifico.  

            > [!NOTE]  
            >  Il nome dell'istanza deve fare riferimento a un'istanza locale di SQL Server. Per fare riferimento a un'istanza di SQL server del cluster, è necessario utilizzare un'impostazione script.  

        -   **Database** : specificare il nome del database di Microsoft SQL Server per cui verrà eseguita la query SQL.  

        -   **Colonna** : specificare il nome della colonna restituito dall'istruzione Transact-SQL da utilizzare per valutare la conformità della condizione globale.  

        -   **Istruzione Transact-SQL** : specificare la query SQL completa da utilizzare per la condizione globale. È inoltre possibile fare clic su **Apri** per aprire una query SQL esistente.  

    -   **Query WQL**  

        -   **Spazio dei nomi** : specificare lo spazio dei nomi WMI che sarà utilizzato per costruire una query WQL che verrà valutata per la conformità nei computer client. Il valore predefinito è Root\cimv2.  

        -   **Classe** : specificare la classe WMI che sarà utilizzata per costruire una query WQL che verrà valutata per la conformità nei computer client.  

        -   **Proprietà** : specificare la proprietà WMI che sarà utilizzata per costruire una query WQL che verrà valutata per la conformità nei computer client.  

        -   **Clausola WHERE della query WQL** : è possibile utilizzare l'elemento **Clausola WHERE della query WQL** per specificare una clausola WHERE da applicare allo spazio dei nomi, alla classe e alla proprietà specifici nei computer client.  

    -   **Query XPath**  

        -   **Percorso** : specificare il percorso del file XML nei computer client che verrà usato per valutare la conformità. Configuration Manager supporta l'uso di tutte le variabili di ambiente di sistema Windows e la variabile utente *%USERPROFILE%* nel nome del percorso.  

        -   **Nome file XML** : specificare il nome file contenente la query XML da utilizzare per valutare la conformità nei computer client.  

        -   **Includi sottocartelle** : abilitare questa opzione se si desidera effettuare la ricerca anche nelle sottocartelle nel percorso specificato.  

        -   **Il file è associato a un'applicazione a 64 bit**: scegliere se effettuare la ricerca anche nel percorso dei file del sistema a 64 bit (*%windir%*\system32), oltre al percorso dei file del sistema a 32 bit (*%windir%*\syswow64) nei client di Configuration Manager con una versione a 64 bit di Windows.  

        -   **Query XPath** : specificare una query XPath valida e completa da utilizzare per valutare la conformità nei computer client.  

        -   **Spazi dei nomi** : aprire la finestra di dialogo **Spazi dei nomi XML** per individuare gli spazi dei nomi e i prefissi da utilizzare durante la query XPath.  

3.  Nell'elenco a discesa **Tipo di dati** , scegliere il formato in cui i dati verranno restituiti dalla condizione prima di essere utilizzato per controllare i requisiti.  

    > [!NOTE]  
    >  L'elenco a discesa **Tipo di dati** non viene visualizzato per tutti i tipi di impostazioni.  

4.  Configurare ulteriori dettagli relativi a questa impostazione sotto l'elenco a discesa **Tipo di impostazione** . Gli elementi che è possibile configurare variano a seconda del tipo di impostazione che è stato selezionato.  

5.  Fare clic su **OK** per salvare la regola e chiudere la finestra di dialogo **Crea condizione globale** .  

### <a name="configure-an-expression-for-the-global-condition"></a>Configurare un'espressione per la condizione globale  

1.  Nell'elenco a discesa **Tipo di condizione** , scegliere **Espressione**.  

2.  Fare clic su **Aggiungi clausola** per aprire la finestra di dialogo **Aggiungi clausola** .  

3.  Dall'elenco a discesa **Seleziona categoria** , selezionare se l'espressione è per un utente o un dispositivo. In alternativa, selezionare **Personalizzata** per utilizzare una condizione globale configurata in precedenza.  

4.  Dall'elenco a discesa **Seleziona una condizione** , selezionare la condizione da utilizzare per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

5.  Dall'elenco a discesa **Scegli operatore** , scegliere l'operatore da utilizzare per confrontare la condizione selezionata con il valore specificato per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. Gli operatori disponibili variano a seconda della condizione selezionata.  

6.  Nel campo **Valore** , specificare i valori da utilizzare con la condizione e l'operatore selezionati per valutare se l'utente o il dispositivo soddisfano i requisiti della regola. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

7.  Fare clic su **OK** per salvare l'espressione e per chiudere la finestra di dialogo **Aggiungi clausola** .  

8.  Quando si è terminato di aggiungere clausole alla condizione globale, fare clic su **OK** per chiudere la finestra di dialogo **Crea condizione globale** e per salvare la condizione globale.  



<!--HONumber=Nov16_HO1-->


