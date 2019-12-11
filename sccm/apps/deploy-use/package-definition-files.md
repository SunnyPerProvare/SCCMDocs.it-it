---
title: File di definizione del pacchetto
titleSuffix: Configuration Manager
description: Informazioni sull'utilizzo dei file di definizione del pacchetto per creare pacchetti e programmi in Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba927286e79d88a6e034fd7eb14f5190cb1f34d6
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "68537679"
---
# <a name="package-definition-files"></a>File di definizione del pacchetto

*Si applica a: System Center Configuration Manager (Current Branch)*

I file di definizione del pacchetto sono script che consentono di automatizzare la creazione di [pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs) in Configuration Manager. Specificano tutte le informazioni necessarie a Configuration Manager per creare un pacchetto e un programma, ad eccezione del percorso dei file origine del pacchetto.

## <a name="about-the-package-definition-file-format"></a>Informazioni sul formato di file definizioni del pacchetto

Ogni file di definizione del pacchetto è un file di testo ASCII o UTF-8 che usa il formato di file ini. Contiene le sezioni seguenti:  

### <a name="pdf"></a>[PDF]

Questa sezione identifica il file come file di definizione del pacchetto. Contiene le informazioni seguenti:  

- **Versione**: specificare la versione del formato di file di definizione del pacchetto usato dal file. Questa versione corrisponde alla versione di Configuration Manager per cui è stata scritta. Questa voce è necessaria.  

### <a name="package-definition"></a>[Package Definition]

Specificare le proprietà del pacchetto e del programma. Contiene le informazioni seguenti:  

- **Nome**: Il nome del pacchetto, fino a 50 caratteri.  

- **Versione** (facoltativo): la versione del pacchetto, con un massimo di 32 caratteri.  

- **Icona** (facoltativo): il file contenente l'icona da usare per il pacchetto. Se specificata, questa icona sostituisce quella del pacchetto predefinita nella console di Configuration Manager.

- **Publisher**: Il server di pubblicazione del pacchetto, un massimo di 32 caratteri.

- **Lingua**: La versione della lingua del pacchetto, un massimo di 32 caratteri.

- **Commento** (facoltativo): commento sul pacchetto, con un massimo di 127 caratteri.

- **ContainsNoFiles**: questa voce indica se il pacchetto contiene file di origine.  

- **Programmi**: i programmi definiti per il pacchetto. Ogni nome del programma corrisponde a un **[programma]** sezione in questo file di definizione del pacchetto.  

    Esempio:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: Il nome del file di formato MIF (Management Information) che contiene lo stato del pacchetto, fino a 50 caratteri.  

- **MIFName**: nome del pacchetto per la corrispondenza MIF, fino a 50 caratteri.  

- **MIFVersion**: numero di versione del pacchetto per la corrispondenza MIF, fino a 32 caratteri.  

- **MIFPublisher**: autore del software del pacchetto per la corrispondenza MIF, fino a 32 caratteri.  

### <a name="program"></a>[Program]

Includere una sezione [Program] per ogni programma specificato nella voce **Programs** nella sezione **[Package Definition]** . In questa sezione viene definito ogni programma. Ogni sezione Program offre le informazioni seguenti:  

- **Nome**: Il nome del programma, fino a 50 caratteri. Questa voce deve essere univoca all'interno di un pacchetto.  

- **Icona** (facoltativo): specificare il file contenente l'icona da usare per il programma. Questa icona sostituisce l'icona di programma predefinita nella console di Configuration Manager. Il client visualizza anche questa icona quando si distribuisce il programma in una raccolta.

- **Commento** (facoltativo): commento sul programma, con un massimo di 127 caratteri.

- **CommandLine**: specificare la riga di comando per il programma, con un massimo di 127 caratteri. Il comando è relativo alla cartella di origine del pacchetto.

- **StartIn**: specificare la cartella di lavoro per il programma, con un massimo di 127 caratteri. Questa voce può essere un percorso assoluto nel computer client o un percorso relativo della cartella di origine del pacchetto.

- **Esegui**: specificare la modalità in cui viene eseguito il programma. È possibile specificare **ridotta a icona**, **ingrandita**, o **Hidden**. Se non si include questa voce, il programma viene eseguito in modalità normale.  

- **AfterRunning**: specificare qualsiasi azione speciale che si verifica dopo il completamento del programma. Le opzioni disponibili sono **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Se non si include questa voce, il programma non esegue un'azione speciale.  

- **EstimatedDiskSpace**: specificare la quantità di spazio su disco necessaria per l'esecuzione del programma software nel computer. Il valore predefinito è **Unknown**. È possibile impostare il valore su un numero intero maggiore o uguale a zero. Se si specifica un valore, includere anche le unità per il valore.  

    Esempio:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: specificare la durata stimata in minuti prevista per l'esecuzione del programma nel computer client. Il valore predefinito è **120**. È possibile impostare il valore su un numero intero maggiore di zero oppure su **Unknown**.  

    Esempio:  

    `EstimatedRunTime=25`  

- **SupportedClients**: specificare i processori e i sistemi operativi in cui viene eseguito il programma. Separare le piattaforme per virgole. Se non si include questa voce, il client non controlla le piattaforme supportate per questo programma.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: specificare l'intervallo tra i numeri di versione iniziali e quelli finali per i sistemi operativi specificati alla voce **SupportedClients**.  

    Esempio:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (facoltativo): specificare qualsiasi altro requisito o informazione per i computer client, con un massimo di 127 caratteri.

- **CanRunWhen**: specificare lo stato dell'utente necessario per l'esecuzione del programma nel computer client. I valori disponibili sono **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. Il valore predefinito è **UserLoggedOn**.  

- **UserInputRequired**: specificare se il programma richiede interazione con l'utente. I valori disponibili sono **True** o **False**. Il valore predefinito è **True**. Questa voce è impostata su **False** se **CanRunWhen** non è impostato su **UserLoggedOn**.  

- **AdminRightsRequired**: specificare se per l'esecuzione del programma è necessario immettere credenziali amministrative nel computer. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**. Questa voce è impostata su **True** se **CanRunWhen** non è impostato su **UserLoggedOn**.  

- **UseInstallAccount**: specificare se il programma usa l'account di installazione del software client durante l'esecuzione nei computer client. Per impostazione predefinita, questo valore è **False**. Questo valore corrisponde anche **False** se **CanRunWhen** è impostato su **UserLoggedOn**.  

- **DriveLetterConnection**: specificare se il programma richiede la connessione di una lettera di unità ai file del pacchetto nel punto di distribuzione. È possibile specificare **True** o **False**. Il valore predefinito è **False**, che consente al programma di usare una connessione UNC (Universal Naming Convention). Quando questo valore è impostato su **True**, il client usa la lettera di unità successiva disponibile, a partire da Z: e andando a ritroso.  

- **DriveLetterConnection**: specificare una lettera di unità necessaria al programma per connettersi ai file del pacchetto nel punto di distribuzione. Questa impostazione forza l'uso della lettera di unità specificata per le connessioni client ai punti di distribuzione.

- **ReconnectDriveAtLogon**: specificare se il computer si riconnette al punto di distribuzione quando l'utente esegue l'accesso. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  

- **DependentProgram**: specificare un programma nel pacchetto che deve essere eseguito prima del programma corrente. Questa voce usa il formato `DependentProgram=<ProgramName>`, dove `<ProgramName>` è la voce di **nome** per il programma nel file di definizione del pacchetto. Se non sono presenti programmi dipendenti, lasciare vuota questa voce.  

    Esempi:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Assignment**: specificare il modo in cui il programma viene assegnato agli utenti. Questo valore può essere:

    - **FirstUser**: solo il primo utente che accede al client esegue il programma
    - **EveryUser**: ogni utente che accede esegue il programma

    Quando **CanRunWhen** non è impostato su **UserLoggedOn**, questa voce è impostata su **FirstUser**.  

- **Disabled**: consente di specificare se è possibile distribuire il programma ai client. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  


## <a name="use-a-package-definition-file"></a>Usare un file di definizione del pacchetto  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Crea pacchetto da definizione**.  

3. Nella pagina **definizione pacchetto** della creazione **guidata pacchetto da definizione**scegliere un file di definizione del pacchetto esistente. Per aprire un nuovo file di definizione del pacchetto, scegliere **Sfoglia**. Dopo aver specificato un nuovo file di definizione del pacchetto, selezionarlo nell'elenco **definizione pacchetto** .

4. Nella pagina **File di origine** specificare le informazioni su tutti i file di origine necessari per il pacchetto e per il programma.  

5. Se il pacchetto richiede file di origine, nella pagina **cartella di origine** specificare il percorso da cui il sito può ottenere i file di origine.  

6. Completare la procedura guidata.  


## <a name="see-also"></a>Vedere anche

[Pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs)
