---
title: "Considerazioni sulla pianificazione per l'automazione delle attività"
titleSuffix: Configuration Manager
description: "Pianificare prima di automatizzare le attività in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: "13"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 5d044e7c7869faeb0b3ea24e24ff40674a63920e
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Considerazioni sulla pianificazione per l'automazione delle attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare sequenze di attività per automatizzare le attività nell'ambiente di System Center Configuration Manager. Queste attività vanno dall'acquisizione di un sistema operativo in un computer di riferimento alla distribuzione del sistema operativo in uno o più computer di destinazione. Le azioni della sequenza di attività sono definite nei singoli passaggi della sequenza. Quando si esegue la sequenza di attività, le azioni di ogni passaggio vengono eseguite a livello di riga di comando nel contesto Sistema locale senza l'intervento dell'utente. Per pianificare l'automatizzazione delle attività in Configuration Manager, vedere le sezioni seguenti.

##  <a name="BKMK_TSStepsActions"></a> Azioni e passaggi della sequenza di attività  
 I passaggi sono i componenti di base di una sequenza di attività. Possono contenere i comandi che configurano e acquisiscono il sistema operativo di un computer di riferimento oppure possono contenere i comandi che installano il sistema operativo, i driver, il client di Configuration Manager e il software nel computer di destinazione. I comandi di un passaggio della sequenza di attività vengono definiti tramite le azioni del passaggio. Esistono due tipi di azioni. Un'azione che viene definita usando una stringa della riga di comando viene definita azione personalizzata. Un'azione predefinita da Configuration Manager viene definita azione integrata. Una sequenza di attività è in grado di eseguire qualsiasi combinazione di azioni predefinite e personalizzate.  

 I passaggi della sequenza di attività possono anche includere condizioni che controllano il comportamento del passaggio, ad esempio interrompere o continuare la sequenza di attività in caso di errore. Le condizioni vengono aggiunte al passaggio includendo una variabile della sequenza di attività al passaggio. Ad esempio, è possibile usare la variabile **SMSTSLastActionRetCode** per verificare la condizione del passaggio precedente. È possibile aggiungere variabili a un singolo passaggio o a un gruppo di passaggi.  

 I passaggi della sequenza di attività vengono elaborati in sequenza, inclusa l'azione del passaggio e le condizioni che vengono assegnate al passaggio. Quando Configuration Manager inizia a elaborare un passaggio della sequenza di attività, il passaggio successivo non viene avviato finché non è stata completata l'azione precedente. Una sequenza di attività viene considerata completa quando tutti i passaggi sono stati completati o quando un passaggio non riuscito costringe Configuration Manager a interrompere l'esecuzione di una sequenza di attività prima del completamento di tutti i passaggi. Ad esempio, se il passaggio di una sequenza di attività non è in grado di individuare un'immagine o un pacchetto di riferimento in un punto di distribuzione, la sequenza di attività contiene un riferimento interrotto e Configuration Manager interrompe l'esecuzione della sequenza di attività a quel punto, a meno che il passaggio non riuscito non abbia la condizione "Continua in caso di errore" abilitata.  

> [!IMPORTANT]  
>  Per impostazione predefinita, una sequenza di attività non riesce dopo che un passaggio o un'azione ha esito negativo. Per fare in modo che la sequenza di attività continui anche quando un passaggio non riesce, modificare la sequenza di attività, fare clic sulla scheda **Opzioni** e selezionare **Continua in caso di errori**.  

 Per altre informazioni sui passaggi che possono essere aggiunti a una sequenza di attività, vedere [Passaggi della sequenze di attività](../understand/task-sequence-steps.md).  

##  <a name="BKMK_TSGroups"></a> Gruppi di sequenze di attività  
 I **gruppi** sono più passaggi all'interno di una sequenza di attività. Un gruppo di sequenze attività è composto da un nome, una descrizione facoltativa e qualsiasi condizione facoltativa valutata come un'unità prima che la sequenza di attività continui con il passaggio successivo. I gruppi possono essere nidificati uno nell'altro e un gruppo può contenere un insieme di passaggi e sottogruppi. I gruppi sono utili per combinare più passaggi che condividono una condizione comune.  

> [!IMPORTANT]  
>  Per impostazione predefinita, un gruppo di sequenze attività ha esito negativo quando si verifica un errore in un passaggio o in un gruppo incorporato all'interno del gruppo. Per fare in modo che la sequenza di attività continui quando un passaggio o un gruppo predefinito non riesce, fare clic sulla scheda **Opzioni** e selezionare **Continua in caso di errori**.  

 La tabella seguente illustra il funzionamento dell'opzione **Continua in caso di errore** quando si raggruppano i passaggi.  

 In questo esempio sono presenti due gruppi di sequenze attività e ognuno contiene tre passaggi di sequenza di attività.  

|Gruppo o passaggio di sequenza di attività|Impostazione Continua in caso di errore|  
|---------------------------------|-------------------------------|  
|**Gruppo di sequenze attività 1**|**Continua in caso di errori** selezionata.|  
|Passaggio sequenza di attività 1|**Continua in caso di errori** selezionata.|  
|Passaggio sequenza di attività 2|Non impostata.|  
|Passaggio sequenza di attività 3|Non impostata.|  
|**Gruppo di sequenze attività 2**|Non impostata.|  
|Passaggio sequenza di attività 4|Non impostata.|  
|Passaggio sequenza di attività 5|Non impostata.|  
|Passaggio sequenza di attività 6|Non impostata.|  

-   Se il passaggio sequenza di attività 1 non riesce, la sequenza di attività continua con il passaggio sequenza di attività 2.  

-   Se il passaggio sequenza di attività 2 non riesce, la sequenza di attività non esegue il passaggio sequenza di attività 3, ma continua a eseguire i passaggi sequenza di attività 4 e 5 che si trovano in un altro gruppo di sequenze di attività.  

-   Se il passaggio sequenza di attività 4 ha esito negativo, non vengono eseguiti altri passaggi e la sequenza di attività non riesce perché l'impostazione **Continua in caso di errore** non è stata configurata per il gruppo sequenza di attività 2.  

 È necessario assegnare un nome ai gruppi sequenza di attività, anche se non è necessario che il nome del gruppo sia univoco. È inoltre possibile fornire una descrizione facoltativa per il gruppo sequenza di attività.  

##  <a name="BKMK_TSVariables"></a> Variabili della sequenza di attività  
 Le variabili della sequenza di attività sono un set di coppie di nome e valore che specificano le impostazioni di configurazione e distribuzione del sistema operativo per le attività di configurazione di computer, sistema operativo e stato utente in un computer client di Configuration Manager. Le variabili della sequenza di attività forniscono un meccanismo per configurare e personalizzare i passaggi in una sequenza di attività.  

 Quando si esegue una sequenza di attività, molte impostazioni della sequenza di attività vengono archiviate come variabili di ambiente. È possibile visualizzare o modificare i valori delle variabili incorporate della sequenza di attività ed è possibile creare nuove variabili della sequenza di attività per personalizzare la modalità di esecuzione di una sequenza di attività in un computer di destinazione.  

 È possibile usare le variabili della sequenza di attività nell'ambiente della sequenza di attività per eseguire le azioni seguenti:  

-   Configurare le impostazioni per un'azione della sequenza di attività  

-   Fornire gli argomenti della riga di comando per un passaggio della sequenza di attività  

-   Valutare una condizione che determina se viene eseguito un passaggio o un gruppo della sequenza di attività  

-   Fornire valori per gli script personalizzati usati in una sequenza di attività  

 Ad esempio, si potrebbe avere una sequenza di attività che include un passaggio di sequenza di attività **Aggiunta a dominio o gruppo di lavoro**. La sequenza di attività può essere distribuita in più raccolte, in cui l'appartenenza della raccolta viene determinata dall'appartenenza al dominio. In questo caso è possibile specificare una variabile con ambito raccolta della sequenza di attività per ogni nome di dominio della raccolta e usare tale variabile della sequenza di attività per specificare il nome di dominio appropriato nella sequenza di attività.  

###  <a name="BKMK_TSCreateVariables"></a> Creare variabili della sequenza di attività  
 È possibile aggiungere nuove variabili della sequenza di attività per personalizzare e controllare i passaggi in una sequenza di attività. Ad esempio, è possibile creare una variabile della sequenza di attività per sostituire un'impostazione per un passaggio predefinito della sequenza di attività. È anche possibile creare una variabile personalizzata della sequenza di attività da usare con le condizioni, le righe di comando o i passaggi personalizzati nella sequenza di attività. Quando si crea una variabile della sequenza di attività, la variabile della sequenza di attività e il valore associato viene mantenuto nell'ambiente della sequenza di attività anche quando la sequenza riavvia il computer di destinazione. La variabile e il relativo valore possono essere usati all'interno della sequenza di attività in ambienti con sistemi operativi diversi. Ad esempio, possono essere usati in un sistema operativo Windows completo e in ambiente Windows PE.  

 Nella tabella seguente vengono descritti i metodi per creare una variabile della sequenza di attività e vengono fornite altre informazioni sull'utilizzo.  

|Metodo di creazione|Utilizzo|  
|-------------------|-----------|  
|Impostazione dei campi nei passaggi della sequenza di attività usando l'editor della sequenza di attività|Specifica i valori predefiniti per il passaggio della sequenza di attività. La variabile e il valore sono accessibili solo quando il passaggio viene eseguito nella sequenza di attività. Non fanno parte dell'ambiente generale della sequenza e non sono accessibili da altri passaggi della sequenza di attività nella sequenza di attività.<br /><br /> Per un elenco delle variabili predefinite e delle relative azioni associate, vedere [Variabili di azione della sequenza di attività](../understand/task-sequence-action-variables.md).|  
|Aggiunta di un determinato passaggio della sequenza di attività in una sequenza di attività|Specifica la variabile della sequenza di attività e il valore nell'ambiente della sequenza di attività quando il passaggio della sequenza di attività viene eseguito come parte della sequenza di attività. Tutti i passaggi successivi della sequenza di attività possono accedere alla variabile di ambiente e al relativo valore.|  
|Definizione di una variabile con ambito raccolta|Specifica le variabili della sequenza di attività e i valori per una raccolta di computer. Tutte le sequenze attività assegnate alla raccolta possono accedere alle variabili della sequenza di attività e ai relativi valori.|  
|Definizione di una variabile con ambito computer|Specifica le variabili della sequenza di attività e i valori per un determinato computer. Tutte le sequenze attività assegnate al computer possono accedere alle variabili della sequenza di attività e ai relativi valori.|  
|Aggiunta di una variabile della sequenza di attività nella pagina **Personalizzazione** della Creazione guidata del supporto per la sequenza di attività|Specifica le variabili della sequenza di attività e i valori per la sequenza di attività che viene eseguita dal supporto che può accedere alla variabile della sequenza di attività e al relativo valore.|  

 Per sostituire il valore predefinito per una variabile predefinita della sequenza di attività, è necessario definire una variabile della sequenza di attività con lo stesso nome della variabile predefinita della sequenza di attività. Per un elenco delle variabili predefinite delle sequenze di attività con le azioni associate e il relativo uso, vedere [Variabili predefinite della sequenza di attività](../understand/task-sequence-built-in-variables.md).  

 È possibile eliminare una variabile della sequenza di attività nell'ambiente della sequenza di attività usando gli stessi metodi di creazione di una variabile della sequenza di attività. In tal caso, per eliminare una variabile dall'ambiente della sequenza di attività, impostare il valore della variabile della sequenza di attività su una stringa vuota.  

 È possibile combinare metodi per impostare una variabile della sequenza di attività dell'ambiente su valori diversi per la stessa sequenza. In uno scenario avanzato potrebbe essere possibile impostare i valori predefiniti per i passaggi in una sequenza usando l'editor della sequenza di attività e quindi impostare un valore della variabile personalizzata usando i vari metodi di creazione. Nell'elenco seguente vengono descritte le regole che determinano il valore che viene usato quando una variabile della sequenza di attività viene creata usando più di un metodo.  

1.  Il passaggio **Imposta variabile della sequenza di attività** sostituisce tutti gli altri metodi di creazione.  

2.  Le variabili con ambito computer hanno la precedenza sulle variabili con ambito raccolta. Se si specifica lo stesso nome della variabile della sequenza di attività per una variabile con ambito computer e una variabile con ambito raccolta, il valore della variabile con ambito computer viene usato quando il computer di destinazione esegue la sequenza di attività distribuita.  

3.  È possibile eseguire le sequenze attività dal supporto. Usare le variabili con ambito supporto anziché le variabili con ambito raccolta o computer. Se la sequenza di attività viene eseguita dal supporto, le variabili con ambito computer e raccolta non sono valide e non vengono usate. Al contrario, le variabili della sequenza di attività definite nella pagina **Personalizzazione** della Creazione guidata del supporto vengono usate per impostare valori specifici per una sequenza di attività eseguita a partire dal supporto.  

4.  Se un valore della variabile della sequenza di attività non è impostato nell'ambiente generale della sequenza, le azioni predefinite usano il valore predefinito per il passaggio, come impostato nell'editor della sequenza di attività.  

 Oltre a sostituire i valori per le impostazioni predefinite del passaggio della sequenza di attività, è possibile creare una nuova variabile di ambiente da usare in un passaggio della sequenza di attività, uno script, una riga di comando o una condizione. Quando si specifica un nome per una nuova variabile della sequenza di attività, usare le seguenti linee guida:  

-   Il nome della variabile della sequenza di attività specificato può contenere lettere, numeri, il carattere di sottolineatura (_) e un trattino (-).  

-   I nomi delle variabili della sequenza di attività hanno una lunghezza minima di 1 carattere e una lunghezza massima di 256 caratteri.  

-   Le variabili definite dall'utente devono iniziare con una lettera (A-Z o a-z).  

-   I nomi delle variabili definite dall'utente non possono iniziare con il carattere di sottolineatura. Solo le variabili della sequenza di attività di sola lettura sono precedute dal carattere di sottolineatura  

    > [!NOTE]  
    >  Le variabili della sequenza di attività di sola lettura possono essere lette dai passaggi della sequenza di attività in una sequenza di attività, ma non possono essere impostate. Ad esempio, è possibile usare una variabile della sequenza di attività di sola lettura come parte della riga di comando per una variabile azione della sequenza di attività **Esegui riga di comando**, ma non è possibile impostare una variabile di sola lettura usando la variabile azione **Imposta variabile della sequenza di attività**.  

-   Ai nomi delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Ad esempio, OSDVAR e osdvar rappresentano la stessa variabile della sequenza di attività.  

-   I nomi delle variabili della sequenza di attività non possono iniziare o finire con uno spazio o contenere spazi. Gli spazi lasciati all'inizio o alla fine di un nome della variabile della sequenza di attività vengono ignorati.  

 La tabella seguente contiene esempi di variabili della sequenza di attività specificate dall'utente valide e non valide.  

|Esempi di nNomi di variabili specificate dall'utente valide|Esempi di nomi di variabili specificate dall'utente non valide|  
|-------------------------------------------------------|----------------------------------------------------------|  
|Variabile|1Variable<br /><br /> Le variabili della sequenza di attività specificate dall'utente non possono iniziare con un numero.|  
|My_Variable|MyV@riable<br /><br /> Le variabili della sequenza di attività specificate dall'utente non possono contenere il simbolo @.|  
|My_Variable_2|_MyVariable<br /><br /> Le variabili della sequenza di attività specificate dall'utente non possono iniziare con un carattere di sottolineatura.|  

 Limitazioni generali per le variabili della sequenza di attività:  

-   I valori delle variabili della sequenza di attività non possono superare i 4.000 caratteri.  

-   Non è possibile creare o sostituire una variabile della sequenza di attività di sola lettura. Le variabili di sola lettura sono contraddistinte da nomi che iniziano con un carattere di sottolineatura (_). È possibile accedere al valore delle variabili di sola lettura nella sequenza di attività. Tuttavia, non è possibile modificare i relativi valori associati.  

-   I valori delle variabili della sequenza di attività possono applicare la distinzione tra maiuscole e minuscole a seconda dell'uso del valore. Nella maggior parte dei casi, ai valori delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Tuttavia, alcuni valori possono essere maiuscole e minuscole, ad esempio una variabile contenente una password.  

-   Non è previsto un limite massimo di variabili della sequenza di attività che possono essere create. Tuttavia, il numero di variabili è limitato dalle dimensioni dell'ambiente della sequenza di attività. Il limite di dimensione totale per l'ambiente della sequenza di attività è 32 MB.  

###  <a name="BKMK_TSEnvironmentVariables"></a> Accedere alle variabili di ambiente  
 Dopo aver specificato la variabile della sequenza di attività e il relativo valore tramite uno dei metodi descritti nella sezione precedente, è possibile usare il valore della variabile di ambiente nelle proprie sequenze attività. È possibile accedere ai valori predefiniti per le variabili della sequenza di attività predefinite, specificare un nuovo valore per una variabile predefinita oppure usare una variabile della sequenza di attività personalizzata in uno script o una riga di comando.  

 Nella tabella seguente vengono descritte le operazioni della sequenza di attività eseguibili accedendo alle variabili di ambiente della sequenza di attività.  

|Operazione sequenza di attività|Utilizzo|  
|-----------------------------|-----------|  
|Configurare le impostazioni dell'azione|È possibile specificare che un'impostazione di un passaggio della sequenza di attività sia fornita da un valore della variabile quando viene eseguita la sequenza.<br /><br /> Per fornire un'impostazione del passaggio della sequenza di attività usando una variabile di ambiente di tale sequenza, usare l'editor della sequenza di attività per modificare il passaggio e specificare il nome della variabile come valore del campo. Il nome della variabile deve essere racchiuso tra simboli di percentuale (%) per indicare che si tratta di una variabile di ambiente.|  
|Fornire gli argomenti della riga di comando|È possibile specificare parzialmente o totalmente una riga di comando personalizzata usando un valore della variabile di ambiente.<br /><br /> Per specificare un'impostazione della riga di comando tramite una variabile di ambiente, usare il nome della variabile come parte del campo **Riga di comando** del passaggio della sequenza di attività **Esegui riga di comando**. Il nome della variabile deve essere racchiuso tra simboli di percentuale (%).<br /><br /> La seguente riga di comando, ad esempio, usa una variabile di ambiente predefinita per scrivere il nome del computer in C:\File.txt.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Valutare una condizione del passaggio|È possibile usare variabili di ambiente della sequenza di attività personalizzate o predefinite come parte di una condizione del gruppo o del passaggio della sequenza di attività. Il valore della variabile di ambiente verrà valutato prima dell'esecuzione del gruppo o del passaggio della sequenza di attività.<br /><br /> Per aggiungere una condizione che valuti un valore della variabile, effettuare le seguenti operazioni:<br /><br /> 1.  Selezionare il passaggio o il gruppo a cui si desidera aggiungere la condizione.<br />2.  Nella scheda **Opzioni** del passaggio o del gruppo, scegliere **Variabile sequenza attività** dal menu a discesa **Aggiungi condizione**.<br />3.  Nella finestra di dialogo **Variabile della sequenza di attività** specificare il nome della variabile, la condizione in corso di verifica e il valore della variabile.|  
|Fornire informazioni per uno script personalizzato|Le variabili della sequenza di attività possono essere lette e scritte usando l'oggetto COM Microsoft.SMS.TSEnvironment durante l'esecuzione della sequenza di attività.<br /><br /> L'esempio seguente illustra un file script di Visual Basic che esegue una query della variabile della sequenza di attività **_SMSTSLogPath** per ottenere la posizione corrente del registro. Lo script imposta inoltre una variabile personalizzata.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' È possibile eseguire una query sull'ambiente per ottenere una variabile esistente.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' È anche possibile impostare una variabile nell'ambiente OSD.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Per altre informazioni su come usare le variabili della sequenza di attività negli script, consultare la documentazione dell'SDK|  

###  <a name="BKMK_ComputerCollectionVariables"></a> Variabili di computer e raccolta  
 È possibile configurare le sequenze attività da eseguire contemporaneamente su più computer o raccolte. È possibile specificare informazioni con ambito computer o raccolta univoche, come specificare un codice Product Key per il sistema operativo univoco oppure associare tutti i membri di una raccolta a un dominio specificato.  

 È possibile assegnare variabili della sequenza di attività a un singolo computer o una singola raccolta. Quando si avvia l'esecuzione della sequenza di attività sul computer o sulla raccolta di destinazione, i valori specificati vengono applicati a tale computer o raccolta.  

 È possibile specificare variabili della sequenza di attività per un singolo computer o una singola raccolta. Quando si avvia l'esecuzione della sequenza di attività sul computer o sulla raccolta di destinazione, le variabili specificate vengono aggiunte all'ambiente e i valori sono disponibili per tutti i passaggi nella sequenza di attività.  

> [!WARNING]  
>  Se si usa lo stesso nome della variabile per una variabile con ambito computer e una variabile con ambito raccolta, il valore della variabile del computer prevale sulla variabile della raccolta. Le variabili della sequenza di attività assegnate alle raccolte hanno la priorità sulle variabili della sequenza di attività predefinite.  

 Per altre informazioni sulla creazione delle variabili della sequenza di attività per computer e raccolte, vedere [Creare variabili della sequenza di attività per computer e raccolte](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="BKMK_TSMediaVariables"></a> Variabili dei supporti per sequenza di attività  
 È possibile specificare variabili per le sequenze attività che vengono eseguite dal supporto. Quando si usa un supporto per la distribuzione del sistema operativo, al momento della creazione del supporto devono essere aggiunte le variabili della sequenza di attività e specificati i relativi valori. Le variabili e i valori correlati vengono memorizzati nel supporto.  

> [!NOTE]  
>  Le sequenze attività vengono memorizzate su un supporto autonomo. Tutti gli altri tipi di supporto, ad esempio i supporti pre-installati, recuperano invece la sequenza di attività da un punto di gestione.  

 È possibile specificare le variabili della sequenza di attività nella pagina **Personalizzazione** della Creazione guidata del supporto per la sequenza di attività. Per informazioni su come creare i supporti, vedere [Creare il supporto per la sequenza di attività](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  La sequenza di attività scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file di log CreateTSMedia.log nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

##  <a name="BKMK_TSCreate"></a> Creare una sequenza di attività  
 È possibile creare sequenze attività usando la Creazione guidata della sequenza di attività. La procedura guidata consente di creare sequenze attività predefinite che eseguono attività specifiche o sequenze attività personalizzate che possono eseguire molte attività differenti.  

 Ad esempio, è possibile creare sequenze attività che generano e acquisiscono un'immagine del sistema operativo di un computer di riferimento, installano un'immagine del sistema operativo esistente su un computer di destinazione oppure creano una sequenza di attività personalizzata che esegue un'attività personalizzata. È possibile usare sequenze attività personalizzate per eseguire distribuzioni del sistema operativo specializzate.  

 Per altre informazioni su come creare sequenze di attività, vedere [Creare sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="BKMK_TSEdit"></a> Modificare una sequenza di attività  
 È possibile modificare la sequenza di attività tramite l'**editor delle sequenze di attività**. L'editor può apportare le seguenti modifiche alla sequenza di attività:  

-   È possibile aggiungere o rimuovere i passaggi della sequenza di attività.  

-   È possibile modificare l'ordine dei passaggi della sequenza di attività.  

-   È possibile aggiungere o rimuovere gruppi di passaggi.  

-   È possibile specificare se la sequenza di attività continua quando si verifica un errore.  

-   È possibile aggiungere condizioni ai passaggi e ai gruppi di una sequenza di attività.  

> [!IMPORTANT]  
>  Se la sequenza di attività ha dei riferimenti non associati a un pacchetto o un programma come risultato della modifica, è necessario correggere il riferimento, eliminare il programma privo di riferimenti dalla sequenza di attività oppure disabilitare il passaggio della sequenza di attività non riuscito fino alla correzione o rimozione del riferimento interrotto.  

 Per altre informazioni su come modificare una sequenza di attività, vedere [Modificare una sequenza di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="BKMK_TSDeploy"></a> Distribuire una sequenza di attività  
 È possibile distribuire una sequenza di attività nei computer di destinazione che si trovano in qualsiasi raccolta di Configuration Manager. Ciò include la raccolta **Tutti i computer sconosciuti** usata per distribuire i sistemi operativi per computer sconosciuti. Tuttavia, non è possibile distribuire una sequenza di attività alle raccolte di utenti.  

> [!IMPORTANT]  
>  Non distribuire sequenze di attività che installano i sistemi operativi nelle raccolte inappropriate, come la raccolta **Tutti i sistemi** . Accertarsi che la raccolta in cui viene distribuita la sequenza di attività contenga solo i computer in cui si desidera installare il sistema operativo. Per prevenire una distribuzione accidentale del sistema operativo, è possibile gestire le impostazioni di distribuzione. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Ciascun computer di destinazione che riceve la sequenza di attività la esegue in base alle impostazioni specificate nella distribuzione. La sequenza di attività stessa non contiene file o programmi associati. Qualsiasi file a cui fa riferimento una sequenza di attività deve essere già presente nel computer di destinazione oppure deve risiedere in un punto di distribuzione accessibile ai client. Inoltre, la sequenza di attività installa i pacchetti a cui fanno riferimento i programmi, anche se il programma o il pacchetto è già installato sul computer di destinazione.  

> [!NOTE]  
>  A differenza dei pacchetti e dei programmi, la sequenza di attività installa un'applicazione solo se le regole relative ai requisiti per tale applicazione sono soddisfatte e l'applicazione non è già installata, in base al metodo di rilevamento specificato per l'applicazione.  

 Il client di Configuration Manager esegue una distribuzione della sequenza di attività durante il download dei criteri del client. Per avviare l'azione anziché attendere fino al successivo ciclo di polling, vedere [Avviare il recupero criteri per un client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Quando si distribuiscono sequenze di attività in dispositivi con Windows Embedded abilitati ai filtri di scrittura, è possibile specificare se disabilitare il filtro di scrittura sul dispositivo durante la distribuzione e riavviare il dispositivo al termine dell'operazione. Se il filtro di scrittura non è disabilitato, la sequenza di attività viene distribuita in una sovrapposizione temporanea e non sarà disponibile al riavvio del dispositivo.  

> [!NOTE]  
>  Quando si distribuisce una sequenza di attività in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata. Ciò consente di decidere quando abilitare o disabilitare il filtro di scrittura nonché quando riavviare il dispositivo.  
>   
>  Se i client scaricano sequenze attività al di fuori di una finestra di manutenzione, la sequenza di attività viene scaricata due volte. In questo scenario i client scaricheranno la sequenza di attività, disabiliteranno i filtri di scrittura, riavvieranno il computer e scaricheranno nuovamente la sequenza di attività perché quest'ultima era stata scaricata nella sovrapposizione temporanea che viene cancellata al riavvio del dispositivo.  

 Per altre informazioni su come distribuire sequenze di attività, vedere [Distribuire una sequenza di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_TSExportImport"></a> Esportare e importare sequenze di attività  
 Configuration Manager consente di esportare e importare le sequenze di attività. Quando si esporta una sequenza di attività, è possibile includere gli oggetti cui fa riferimento tale sequenza. Questi includono un'immagine del sistema operativo, un'immagine di avvio, un pacchetto dell'agente client, un pacchetto driver e applicazioni con dipendenze.  

> [!NOTE]  
>  Il processo di esportazione e importazione delle sequenze di attività è molto simile allo stesso tipo di processo per le applicazioni in Configuration Manager.  

 Per altre informazioni sull'esportazione e importazione delle sequenze attività, vedere [Esportare e importare sequenze di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="BKMK_TSRun"></a> Eseguire una sequenza di attività  
 Per impostazione predefinita, le sequenze attività sono sempre eseguite usando l'account di sistema locale. Il passaggio della riga di comando della sequenza di attività consente di eseguire la sequenza di attività come un account diverso. Quando si esegue la sequenza di attività, il client di Configuration Manager controlla la presenza di pacchetti con riferimenti prima di avviare i passaggi della sequenza di attività. Se un pacchetto con riferimenti non è convalidato o non è disponibile in un punto di distribuzione, la sequenza di attività restituisce un errore per il passaggio della sequenza di attività associato.  

 Se una sequenza di attività distribuita viene configurata per il download e l'esecuzione, tutti i pacchetti e le applicazioni dipendenti vengono scaricati nella cache client di Configuration Manager. I pacchetti e le applicazioni necessari vengono ottenuti dai punti di distribuzione e, se la dimensione della cache client di Configuration Manager è eccessivamente ridotta oppure non è possibile individuare il pacchetto o l'applicazione, la sequenza di attività ha esito negativo e viene generato un messaggio di stato. È anche possibile specificare che il client scaricherà il contenuto solo quando richiesto quando si seleziona **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**. Si può anche usare l'opzione **Esegui programma dal punto di distribuzione** per specificare che il client installerà i file direttamente dal punto di distribuzione, senza scaricarli prima nella cache. L'opzione **Esegui programma dal punto di distribuzione** è disponibile solo se l'impostazione **Copia il contenuto del pacchetto in una condivisione pacchetto nei punti di distribuzione** dei pacchetti con riferimenti è abilitata nella scheda **Accesso dati** delle proprietà **Pacchetto**.  

 Se il client su cui è in esecuzione la sequenza di attività non è in grado di individuare un'applicazione o un pacchetto dipendente, invia immediatamente un messaggio di errore non appena la distribuzione viene configurata come **Disponibile**. Se tuttavia la distribuzione è configurata come **Richiesta**, il client di Configuration Manager attende e riprova a scaricare il contenuto fino alla scadenza, nel caso in cui quest'ultimo non sia già replicato in un punto di distribuzione accessibile al client.  

 Quando una sequenza di attività viene completata correttamente o non riesce, Configuration Manager registra l'evento nella cronologia client di Configuration Manager. Non è possibile annullare o interrompere una sequenza di attività dopo l'inizializzazione su un computer.  

> [!IMPORTANT]  
>  Se un passaggio di una sequenza di attività richiede il riavvio del computer client, il client deve essere in grado di eseguire l'avvio di una partizione del disco formattato. In caso contrario, la sequenza di attività non riesce indipendentemente dalla gestione degli errori specificata dalla sequenza di attività.  

 Quando un oggetto dipendente di una sequenza di attività, ad esempio un pacchetto di distribuzione software, viene aggiornato a una nuova versione, le sequenze attività che fanno riferimento al pacchetto vengono automaticamente aggiornate e fanno riferimento alla versione più recente, indipendentemente dal numero di aggiornamenti distribuiti.  

> [!NOTE]  
>  Prima di eseguire una sequenza di attività, un client di Configuration Manager verifica la presenza di possibili dipendenze in tutte le sequenze di attività e la disponibilità di tali dipendenze in un punto di distribuzione. Se il client trova un oggetto eliminato da cui dipende la sequenza di attività, il client genera un errore e non esegue la sequenza di attività.  

###  <a name="BKMK_RunProgram"></a> Eseguire un programma prima dell'esecuzione della sequenza di attività  
 È possibile selezionare un programma che viene eseguito prima dell'esecuzione della sequenza di attività. Per specificare un programma da eseguire prima, aprire la finestra di dialogo **Proprietà** per la sequenza di attività e selezionare la scheda **Avanzate** per impostare le opzioni seguenti:  

> [!IMPORTANT]  
>  Per eseguire un programma prima dell'esecuzione della sequenza di attività, tutto il contenuto per la sequenza di attività e il programma devono essere disponibili in una condivisione per il pacchetto. Configurare la condivisione pacchetto nella scheda **Accesso dati** nelle proprietà del pacchetto.  

-   **Esegui prima un altro programma**: specifica di eseguire un altro programma prima dell'esecuzione della sequenza di attività.  

    > [!IMPORTANT]  
    >  Questa impostazione si applica solo alle sequenze di attività che vengono eseguite nel sistema operativo completo. Configuration Manager ignora questa impostazione se la sequenza di attività viene avviata tramite PXE o il supporto di avvio.  

-   **Pacchetto**: specifica il pacchetto che contiene il programma.  

-   **Programma**: specifica il programma da eseguire.  

-   **Esegui sempre prima questo programma**: specifica che Configuration Manager deve eseguire questo programma ogni volta che esegue la sequenza di attività nello stesso client. Per impostazione predefinita, dopo che un programma è stato eseguito correttamente, non viene più eseguito se la sequenza di attività non viene rieseguita sullo stesso client.  

 Se l'esecuzione su un client del programma selezionato non riesce, la sequenza di attività non viene eseguita.  

##  <a name="BKMK_TSMaintenanceWindow"></a> Usare una finestra di manutenzione per specificare quando è possibile eseguire una sequenza di attività  
 È possibile specificare quando la sequenza di attività può essere eseguita definendo una finestra di manutenzione per la raccolta contenente i computer di destinazione. Le finestre di manutenzione vengono configurate con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. Inoltre, quando si imposta la pianificazione della finestra di manutenzione, è possibile specificare che la finestra di manutenzione si applica solo alle sequenze attività. Per altre informazioni, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  Quando si configura una finestra di manutenzione per l'esecuzione di una sequenza di attività, dopo l'avvio la sequenza di attività continua a essere eseguita anche se la finestra di manutenzione viene chiusa. La sequenza di attività verrà completata correttamente oppure avrà esito negativo.  

##  <a name="BKMK_TSNetworkAccessAccount"></a> Sequenze di attività e account di accesso alla rete  
 Anche se le sequenze di attività vengono eseguite solo nel contesto dell'account di sistema locale, potrebbe essere necessario configurare l'account di accesso alla rete nelle circostanze seguenti:  

-   Se l'account di accesso alla rete non viene configurato correttamente, la sequenza di attività avrà esito negativo se prova ad accedere ai pacchetti di Configuration Manager nei punti di distribuzione per completare l'attività. Per altre informazioni sull'account di accesso alla rete, vedere [Account di accesso alla rete](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

    > [!NOTE]  
    >  L'account di accesso alla rete non viene mai usato come contesto di sicurezza per eseguire programmi, installare applicazioni, installare aggiornamenti oppure eseguire sequenze attività. L'account di accesso alla rete viene tuttavia usato per l'accesso alle risorse associate in rete.  

-   Quando si usa un'immagine di avvio per iniziare una distribuzione di un sistema operativo, Configuration Manager usa l'ambiente Windows PE, che non è un sistema operativo completo. L'ambiente Windows PE usa un nome casuale generato automaticamente che non è membro di nessun dominio. Se non si configura correttamente l'account di accesso alla rete, è possibile che il computer non abbia le autorizzazioni obbligatorie per accedere ai pacchetti di Configuration Manager necessari per completare la sequenza di attività.  

##  <a name="BKMK_TSCreateMedia"></a> Creare supporti per le sequenze di attività  
 È possibile scrivere le sequenze attività e le dipendenze e i file correlati in diversi tipi di supporto. È inclusa la scrittura su supporti rimovibili, ad esempio un set di DVD o CD o una unità flash USB per i supporti di acquisizione, autonomi e di avvio, o la scrittura in un file di formato Windows Imaging (WIM) per i supporti pre-installati.  

 È possibile creare i tipi di supporto seguenti:  

-   **Supporti di acquisizione**. I supporti di acquisizione ottengono un'immagine del sistema operativo configurata e creata al di fuori dell'infrastruttura di Configuration Manager. I supporti di acquisizione possono contenere programmi personalizzati eseguibili prima dell'esecuzione di una sequenza di attività. Il programma personalizzato può interagire con il desktop, richiedere valori di input all'utente o creare variabili che verranno usate dalla sequenza di attività.  

     Per altre informazioni, vedere [Creare supporti di acquisizione](../deploy-use/create-capture-media.md).  

-   **Supporti autonomo**. I supporti autonomi contengono la sequenza di attività e tutti gli oggetti associati necessari per l'esecuzione della sequenza di attività. Le sequenze di attività dei supporti autonomi possono essere eseguite quando Configuration Manager ha limitata o nessuna connettività alla rete. I supporti autonomi possono essere eseguiti nei modi seguenti:  

    -   Se il computer di destinazione non viene avviato, viene usata l'immagine di Windows PE associata alla sequenza di attività a partire dal supporto autonomo e la sequenza di attività ha inizio.  

    -   Il supporto autonomo può essere avviato manualmente se un utente è connesso alla rete e avvia l'installazione.  

    > [!IMPORTANT]  
    >  I passaggi di una sequenza di attività di un supporto autonomo devono poter essere eseguiti senza recuperare nessun dato dalla rete. In caso contrario, il passaggio della sequenza di attività che cerca di recuperare i dati ha esito negativo. Un passaggio di una sequenza di attività, ad esempio, che richiede un punto di distribuzione per ottenere un pacchetto ha esito negativo. Se tuttavia il pacchetto necessario è contenuto nel supporto autonomo, il passaggio della sequenza di attività viene completato correttamente.  

     Per altre informazioni, vedere [Creare supporti autonomi](../deploy-use/create-stand-alone-media.md).  

-   **Supporti di avvio**. I supporti di avvio contengono i file necessari per avviare un computer di destinazione in modo che possa connettersi all'infrastruttura di Configuration Manager per determinare quali sequenze di attività eseguire in base all'appartenenza a una raccolta. La sequenza di attività e gli oggetti dipendenti non sono contenuti nel supporto, ma vengono ottenuti in rete dal client di Configuration Manager. Questo metodo è utile per i nuovi computer o per le distribuzioni bare metal oppure quando nel computer di destinazione non è presente nessun client di Configuration Manager o sistema operativo.  

     Per altre informazioni, vedere [Creare supporti di avvio](../deploy-use/create-bootable-media.md).  

-   **Supporti preinstallati**. I supporti pre-installati distribuiscono un'immagine del sistema operativo in un computer di destinazione di cui non viene effettuato il provisioning. I supporti preinstallati sono archiviati come file WIM (Windows Imaging Format), i quali può essere installati in un computer bare metal dal produttore o in un centro di gestione temporanea aziendale non connesso all'ambiente di Configuration Manager.  

     Per altre informazioni, vedere [Creare supporti preinstallati](../deploy-use/create-prestaged-media.md).  

 Quando si crea il supporto, specificare una password per consentire al supporto di controllare l'accesso ai file contenuti nel supporto. Se si specifica una password, deve essere presente un utente che immetta la password nel computer di destinazione quando viene eseguita la sequenza di attività.  

 Quando si esegue una sequenza di attività usando il supporto, l'architettura chip del computer specificata, contenuta nel supporto, non verrà riconosciuta e l'esecuzione della sequenza di attività verrà tentata anche se l'architettura specificata non corrisponde a quella effettivamente installata nel computer di destinazione. Se l'architettura chip contenuta nel supporto non corrisponde all'architettura chip installata nel computer di destinazione, l'installazione non riesce.  

 Per altre informazioni su come distribuire sistemi operativi usando i supporti, vedere [Creare supporti per le sequenze di attività](../deploy-use/create-task-sequence-media.md).  
