---
title: Come usare le variabili della sequenza di attività
titleSuffix: Configuration Manager
description: Informazioni su come usare le variabili in una sequenza di attività di Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd2e95a82ab01c760ea14158f164e930a77db894
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748136"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Come usare le variabili della sequenza di attività in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 Il motore di esecuzione della sequenza di attività nella funzionalità di distribuzione del sistema operativo di Configuration Manager usa numerose variabili per controllarne i comportamenti. Usare queste variabili per: 
 - Impostare le condizioni sui passaggi  
 - Cambiare i comportamenti per passaggi specifici  
 - Creare azioni più complesse con gli script  


 Per informazioni di riferimento su tutte le variabili della sequenza di attività disponibili, vedere [Task sequence variables](/sccm/osd/understand/task-sequence-variables) (Variabili della sequenza di attività).



## <a name="bkmk_types"></a> Tipi di variabili

 Sono disponibili diversi tipi di variabili:  
 - [Predefinite](#bkmk_built-in)  
 - [Azione](#bkmk_action)  
 - [Personalizzato](#bkmk_custom)  
 - [Di sola lettura](#bkmk_read-only)  
 - [Di matrice](#bkmk_array)  


### <a name="bkmk_built-in"></a> Variabili predefinite

 Le variabili predefinite forniscono informazioni sull'ambiente in cui viene eseguita la sequenza di attività. I relativi valori sono disponibili nell'intera sequenza di attività. In genere il motore di esecuzione della sequenza di attività inizializza le variabili predefinite prima di eseguire qualsiasi passaggio. 

 Ad esempio, **\_SMSTSLogPath** è una variabile di ambiente che specifica il percorso in cui i componenti di Configuration Manager scrivono i file di log. Qualsiasi passaggio della sequenza di attività può accedere a questa variabile di ambiente. 

 La sequenza di attività valuta alcune variabili prima di ogni passaggio. Ad esempio, **\_SMSTSCurrentActionName** elenca il nome del passaggio corrente. 

### <a name="bkmk_action"></a> Variabili di azione

 Le variabili di azione della sequenza di attività specificano le impostazioni di configurazione usate da un singolo passaggio della sequenza di attività. Per impostazione predefinita, il passaggio inizializza le proprie impostazioni prima dell'esecuzione. Queste impostazioni sono disponibili solo mentre il passaggio della sequenza di attività associato è in esecuzione. La sequenza di attività aggiunge la variabile di azione all'ambiente prima di eseguire il passaggio. Rimuove quindi il valore dall'ambiente dopo l'esecuzione del passaggio.

 Ad esempio, aggiungere il passaggio **Esegui riga di comando** a una sequenza di attività. Questo passaggio include una proprietà **Da**. La sequenza di attività archivia un valore predefinito per questa proprietà come variabile **WorkingDirectory**. La sequenza di attività inizializza questo valore prima di eseguire il passaggio **Esegui riga di comando**. Durante l'esecuzione di questo passaggio, accedere al valore della proprietà **Da** dal valore **WorkingDirectory**. Dopo il completamento del passaggio, la sequenza di attività rimuove il valore della variabile **WorkingDirectory** dall'ambiente. Se la sequenza di attività include un altro passaggio **Esegui riga di comando**, inizializza una nuova variabile **WorkingDirectory**. A questo punto la sequenza di attività imposta la variabile sul valore iniziale del passaggio corrente. Per altre informazioni, vedere [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory).  

 Il valore *predefinito* per una variabile di azione è presente quando il passaggio viene eseguito. Se si imposta un *nuovo* valore, questo è disponibile per più passaggi della sequenza di attività. Se si esegue l'override di un valore predefinito, il nuovo valore rimane nell'ambiente. Questo nuovo valore esegue l'override del valore predefinito per altri passaggi della sequenza di attività. Supponiamo ad esempio di aggiungere un passaggio **Imposta variabile della sequenza di attività** come primo passaggio della sequenza di attività. Questo passaggio imposta la variabile **WorkingDirectory** su `C:\`. Qualsiasi passaggio **Esegui riga di comando** nella sequenza di attività usa il nuovo valore della directory iniziale.  

 Alcuni passaggi della sequenza di attività contrassegnano determinate variabili di azione come *output*. I passaggi successivi della sequenza di attività leggono queste variabili di output.

 > [!Note]  
 > Non tutti i passaggi della sequenza di attività contengono variabili di azione. Ad esempio, anche se ci sono variabili associate all'azione **Attiva BitLocker**, non ci sono variabili associate all'azione **Disattiva BitLocker**.  


### <a name="bkmk_custom"></a> Variabili personalizzate

 Le variabili personalizzate sono tutte le variabili non create da Configuration Manager. Inizializzare le variabili personalizzate da usare come condizioni, in righe di comando o in script. 

 Quando si specifica un nome per una nuova variabile della sequenza di attività, usare le seguenti linee guida:  

 - Il nome della variabile della sequenza di attività può contenere lettere, numeri, il carattere di sottolineatura (`_`) e un trattino (`-`).  

 - I nomi delle variabili della sequenza di attività hanno una lunghezza minima di un carattere e una lunghezza massima di 256 caratteri.  

 - Le variabili definite dall'utente devono iniziare con una lettera (`A-Z` o `a-z`).  

 - I nomi delle variabili definite dall'utente non possono iniziare con il carattere di sottolineatura. Solo le variabili della sequenza di attività di sola lettura sono precedute dal carattere di sottolineatura.  

 - Ai nomi delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Ad esempio, `OSDVAR` e `osdvar` sono la stessa variabile della sequenza di attività.  

 - I nomi delle variabili della sequenza di attività non possono iniziare o finire con uno spazio né contenere spazi. Gli spazi lasciati all'inizio o alla fine di un nome di variabile vengono ignorati dalla sequenza di attività.  


 Non è previsto un limite massimo di variabili della sequenza di attività che possono essere create. Tuttavia, il numero di variabili è limitato dalle dimensioni dell'ambiente della sequenza di attività. Il limite di dimensione totale per l'ambiente della sequenza di attività è 32 MB.  


### <a name="bkmk_read-only"></a> Variabili di sola lettura

 Le variabili di sola lettura sono variabili di cui non è possibile cambiare il valore. In genere il nome inizia con un carattere di sottolineatura (\_). La sequenza di attività usa queste variabili per le sue operazioni. Le variabili di sola lettura sono visibili nell'ambiente della sequenza di attività. 

 Queste variabili sono utili negli script o nelle righe di comando. Ad esempio, è possibile eseguire una riga di comando e inviare pipe dell'output a un file di log in **\_SMSTSLogPath** con gli altri file di log.

 > [!NOTE]  
 >  Le variabili della sequenza di attività di sola lettura possono essere lette dai passaggi di una sequenza di attività, ma non possono essere impostate. Ad esempio, usare una variabile di sola lettura come parte della riga di comando di un passaggio **Esegui riga di comando**. Non è possibile impostare una variabile di sola lettura usando il passaggio **Imposta variabile della sequenza di attività**.  



### <a name="bkmk_array"></a> Variabili di matrice

 La sequenza di attività archivia alcune variabili come matrice. Ogni elemento della matrice rappresenta le impostazioni per un singolo oggetto. Usare queste variabili quando un dispositivo ha più oggetti da configurare. I passaggi seguenti della sequenza di attività usano variabili di matrice:

 - [Applica impostazioni di rete](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Formato e disco partizione](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> Come impostare le variabili

 Sono disponibili diversi metodi che consentono di inizializzare e impostare il valore delle variabili personalizzate o non di sola lettura:  

 - [Imposta variabile della sequenza di attività](#bkmk_set-ts-step)  
 - [Imposta variabili dinamiche](#bkmk_set-dyn-step)  
 - [Variabili di raccolta e dispositivo](#bkmk_set-coll-var)  
 - [Oggetto COM TSEnvironment](#bkmk_set-com)  
 - [Comando di preavvio](#bkmk_set-prestart)  
 - [Creazione guidata del supporto per la sequenza di attività](#bkmk_set-media)  


 Eliminare una variabile dall'ambiente usando gli stessi metodi usati per crearla. Per eliminare una variabile, impostarne il valore su una stringa vuota.  

 È possibile combinare metodi per impostare una variabile della sequenza di attività su valori diversi per la stessa sequenza. Ad esempio, impostare i valori predefiniti usando l'editor delle sequenze di attività e i valori personalizzati usando uno script. 

 Se si imposta la stessa variabile con metodi diversi, il motore di esecuzione della sequenza di attività usa l'ordine seguente:  

 1. Prima di tutto valuta le variabili di raccolta.  

 2. Le variabili specifiche del dispositivo eseguono l'override dello stesso set di variabili in una raccolta.  

 3. Le variabili impostate da un qualsiasi metodo durante la sequenza di attività hanno la precedenza sulle variabili di raccolta o dispositivo.  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitazioni generali per i valori delle variabili della sequenza di attività  

 - I valori delle variabili della sequenza di attività non possono superare i 4.000 caratteri.  

 - Non è possibile modificare una variabile della sequenza di attività di sola lettura. Le variabili di sola lettura hanno nomi che iniziano con un carattere di sottolineatura (`_`).  

 - I valori delle variabili della sequenza di attività possono applicare la distinzione tra maiuscole e minuscole a seconda dell'uso del valore. Nella maggior parte dei casi, ai valori delle variabili della sequenza di attività non viene applicata la distinzione tra maiuscole e minuscole. Viene invece applicata alle variabili che includono una password.  


### <a name="bkmk_set-ts-step"></a> Imposta variabile della sequenza di attività

 Usare questo passaggio nella sequenza di attività per impostare una singola variabile su un singolo valore. 

 Per altre informazioni, vedere [Imposta variabile della sequenza di attività](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Imposta variabili dinamiche

 Usare questo passaggio nella sequenza di attività per impostare una o più variabili della sequenza di attività. Occorre definire le regole in questo passaggio per determinare quali variabili e valori usare. 

 Per altre informazioni, vedere [Imposta variabili dinamiche](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a> Variabili di raccolta e dispositivo

 Impostare le variabili sulle proprietà di una raccolta o di un dispositivo specifico. 

 Per altre informazioni, vedere [Creare le variabili della sequenza di attività per computer e raccolte](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a> Oggetto COM TSEnvironment

 Per lavorare con le variabili da uno script, usare l'oggetto **TSEnvironment**. 

 Per altre informazioni, vedere [How to use variables in a running task sequence](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) (Come usare le variabili in una sequenza di attività in esecuzione) in Configuration Manager SDK.


### <a name="bkmk_set-prestart"></a> Comando di preavvio

 Il comando di preavvio è uno script o un file eseguibile che viene eseguito in Windows PE prima che l'utente selezioni la sequenza di attività. Può eseguire query su una variabile o richiedere informazioni all'utente e quindi salvarle nell'ambiente. Usare l'oggetto COM [TSEnvironment](#bkmk_set-com) per leggere e scrivere variabili dal comando di preavvio. 

 Per altre informazioni vedere [Comandi di preavvio del supporto per sequenza attività](/sccm/osd/understand/prestart-commands-for-task-sequence-media).


### <a name="bkmk_set-media"></a> Creazione guidata del supporto per la sequenza di attività

 Specificare le variabili per le sequenze di attività che vengono eseguite da supporti. Quando si usa un supporto per la distribuzione del sistema operativo, al momento della creazione del supporto occorre aggiungere le variabili della sequenza di attività e specificarne i valori. Le variabili e i loro valori vengono memorizzati nel supporto.  

 > [!NOTE]  
 >  Le sequenze attività vengono memorizzate su un supporto autonomo. Tutti gli altri tipi di supporto, ad esempio i supporti pre-installati, recuperano invece la sequenza di attività da un punto di gestione.  

 Quando si esegue una sequenza di attività da un supporto, è possibile aggiungere una variabile nella pagina **Personalizzazione** della procedura guidata. 

 Usare le variabili con ambito supporto anziché le variabili con ambito raccolta o computer. Se la sequenza di attività viene eseguita dal supporto, le variabili con ambito computer e raccolta non sono valide e non vengono usate.  

 > [!TIP]  
 >  La sequenza di attività scrive l'ID del pacchetto e la riga di comando di preavvio nel file di log **CreateTSMedia.log** nel computer che esegue la console di Configuration Manager. Questo file di log include il valore di tutte le variabili della sequenza di attività. Rivedere questo file di log per verificare il valore per le variabili della sequenza di attività.  

 Per altre informazioni, vedere [Creare supporti per sequenza di attività](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a> Come accedere alle variabili

 Dopo aver specificato la variabile e il relativo valore tramite uno dei metodi descritti nella sezione precedente, usarla nelle sequenze di attività. Ad esempio, accedere ai valori predefiniti delle variabili delle sequenze di attività predefinite o rendere un passaggio condizionale in base al valore della variabile.  

 Usare i metodi seguenti per accedere ai valori delle variabili nell'ambiente della sequenza di attività:
 - [Uso in un passaggio](#bkmk_access-step)  
 - [Condizione del passaggio](#bkmk_access-condition)  
 - [Script personalizzato](#bkmk_access-script)  
 - [File di risposte del programma di installazione di Windows](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> Uso in un passaggio

 Specificare un valore di variabile per un'impostazione in un passaggio della sequenza di attività. Nell'editor di testo delle sequenze di attività modificare il passaggio e specificare il nome della variabile come valore del campo. Racchiudere il nome della variabile tra simboli di percentuale (`%`). 

 Ad esempio, usare il nome della variabile come parte del campo **Riga di comando** del passaggio **Esegui riga di comando**. La riga di comando seguente scrive il nome computer in un file di testo. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> Condizione del passaggio

 Usare variabili della sequenza di attività predefinite o personalizzate come parte di una condizione per un passaggio o un gruppo. La sequenza di attività valuta il valore della variabile prima di eseguire il passaggio o il gruppo.

 Per aggiungere una condizione che valuti un valore della variabile, eseguire i passaggi seguenti:  

 1. Nell'editor delle sequenze di attività selezionare il passaggio o il gruppo a cui si vuole aggiungere la condizione.  

 2. Passare alla scheda **Opzioni** relativa al passaggio o al gruppo. Fare clic su **Aggiungi condizione** e selezionare **Variabile della sequenza di attività**.  

 3. Nella finestra di dialogo **Variabile della sequenza di attività** specificare le impostazioni seguenti:  

    - **Variabile**: nome della variabile. Ad esempio, `_SMSTSInWinPE`.  

    - **Condizione**: condizione in base a cui valutare il valore della variabile. Ad esempio, **uguale a**.  

    - **Valore**: valore della variabile da controllare. Ad esempio, `false`.  


 I tre esempi riportati sopra formano una condizione in base a cui verificare se la sequenza di attività è in esecuzione da un'immagine d'avvio in Windows PE: 

 > **Variabile della sequenza di attività** `_SMSTSInWinPE equals "false"`

 Vedere questa condizione nel gruppo **Acquisisci file e impostazioni** del modello di sequenza di attività predefinita per installare un'immagine del sistema operativo esistente.


### <a name="bkmk_access-script"></a> Script personalizzato

 Le variabili possono essere lette e scritte usando l'oggetto COM **Microsoft.SMS.TSEnvironment** durante l'esecuzione della sequenza di attività.

 L'esempio di Windows PowerShell seguente esegue una query sulla variabile **_SMSTSLogPath** per ottenere il percorso del log corrente. Lo script imposta inoltre una variabile personalizzata.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> File di risposte del programma di installazione di Windows

Il file di risposte del programma di installazione di Windows che si specifica può contenere variabili della sequenza di attività incorporate. Usare il formato `%varname%`, dove *varname* è il nome della variabile. Il passaggio **Imposta Windows e ConfigMgr** sostituisce la stringa del nome della variabile con il valore effettivo della variabile. Queste variabili incorporate della sequenza di attività non possono essere usate in campi di tipo solo numerico in un file di risposte unattend.xml.

Per altre informazioni, vedere [Impostare Windows e Configuration Manager](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).



## <a name="see-also"></a>Vedere anche

- [Passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps)
- [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables)
- [Considerazioni sulla pianificazione dell'automazione delle attività](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
