---
title: Risoluzione dei problemi di Microsoft Deployment Toolkit
titleSuffix: Microsoft Deployment Toolkit
description: 'Riferimento per la risoluzione dei problemi di Microsoft Deployment Toolkit '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821015"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Riferimento per la risoluzione dei problemi di Microsoft Deployment Toolkit
 La distribuzione dei sistemi operativi e delle applicazioni, nonché la migrazione dello stato utente, possono rivelarsi attività complesse, anche quando sono disponibili linee guida e strumenti appropriati. Questo documento di riferimento, che fa parte di Microsoft® Deployment Toolkit (MDT) 2013, fornisce informazioni sui problemi noti correnti, possibili soluzioni alternative per tali problemi e informazioni aggiuntive per la risoluzione dei problemi.  

> [!NOTE]
>  In questo documento *Windows* si riferisce ai sistemi operativi Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, se non diversamente specificato. MDT non supporta le versioni di Windows basate su processore ARM. Analogamente, *MDT* si riferisce a MDT 2013, se non diversamente specificato.  

> [!NOTE]
>  Il Microsoft Diagnostics and Recovery Toolset (DaRT) contiene strumenti avanzati per il ripristino e la risoluzione dei problemi relativi a computer client che non si avviano o sono diventati instabili. È possibile utilizzare DaRT per determinare la causa di un arresto anomalo, ripristinare file persi e così via. È inoltre possibile utilizzare DaRT come strumento per la risoluzione dei problemi in fase di sviluppo e distribuzione di un sistema operativo Windows. Ad esempio, se un'immagine incorporata non viene avviata correttamente, è possibile avviare il computer client che contiene l'immagine utilizzando ERD Commander, ovvero un ambiente di diagnostica. Quindi, si può esplorare il disco rigido del computer client, visualizzare il registro eventi, rimuovere gli aggiornamenti, modificare le impostazioni del sistema operativo e così via. DaRT fa parte del Microsoft Desktop Optimization Pack per Software Assurance. Per ulteriori informazioni su DaRT, vedere [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Informazioni sui registri  
 Prima di poter iniziare una risoluzione dei problemi efficace di MDT, è necessario acquisire una comprensione approfondita dei numerosi file di log utilizzati durante la distribuzione del sistema operativo. Quando si sa in quali file di registro ricercare una data condizione di errore e si conosce l'ora in cui si è verificata, i problemi che sembravano misteriosi e difficili da comprendere possono diventare chiari e comprensibili.  

 Il formato dei file di log di MDT è progettato per essere letto da Trace32, parte di System Center Configuration Manager 2007 Toolkit V2 e disponibile per il download dal [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=9257). I registri possono essere letti anche dallo strumento Tracelog di Configuration Manager (CMTrace) disponibile con System Center 2012 Configuration Manager e versioni successive. Leggere i file di log utilizzando questi strumenti, quando possibile, in quanto rende molto più facile individuare gli errori.  

 Il resto di questa sezione descrive in dettaglio i file di log creati durante la distribuzione, nonché durante l'installazione di Windows. In questa sezione vengono inoltre forniti esempi di quando utilizzare i file per la risoluzione dei problemi.  

### <a name="mdt-logs"></a>Registri di MDT  
 Ogni script di MDT crea automaticamente i file di log durante l'esecuzione. I nomi dei file di log corrispondono al nome dello script, ad esempio, ZTIGather.wsf crea un file di log denominato *ZTIGather.log*. Ogni script aggiorna anche un file di log master comune (BDD.log) che aggrega il contenuto dei file di log creati dagli script di MDT. I file di log di MDT risiedono in C:\MININT\SMSOSD\OSDLOGS durante il processo di distribuzione. A seconda del tipo di distribuzione effettuata, al termine della distribuzione i file di log vengono spostati in %WINDIR%\SMSOSD o %WINDIR%\TEMP\SMSOSD. Per le distribuzioni Lite Touch Installation (LTI), i file di log iniziano in C:\MININT\SMSOSD\OSDLogs. Finiscono in %WINDIR%\TEMP\DeploymentLogs quando l'elaborazione della sequenza di attività è stata completata.  

 MDT crea i file di log seguenti:  

-   **BDD.log**. File di log di MDT aggregato che viene copiato in un percorso di rete al termine della distribuzione se si specifica la proprietà **SLShare** nel file CustomSettings.ini.  

-   **LiteTouch.log**. File creato durante le distribuzioni LTI. Risiede in %WINDIR%\TEMP\DeploymentLogs a meno che non sia stata specificata l'opzione **/debug:true**.  

-   **Nomescript*.log**. File creato da ogni script di MDT. *Nomescript* rappresenta il nome dello script in questione.  

-   **SMSTS.log**. File creato dal sequencer delle attività che descrive tutte le transazioni del sequencer delle attività. A seconda dello scenario di distribuzione, può trovarsi in %TEMP%, %WINDIR%\System32\ccm\logs, C:\\\_SMSTaskSequence oppure C:\SMSTSLog.  

-   **Wizard.log**. File creato e aggiornato dalle distribuzioni guidate.  

-   **WPEinit.log**. File creato durante il processo di inizializzazione di Windows PE utile per la risoluzione degli errori rilevati durante l'avvio di Windows PE.  

-   **DeploymentWorkbench_*id*.log**. File di log creato nella cartella % temp % quando si specifica **a /debug** all'avvio di Deployment Workbench.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Registri di distribuzione del sistema operativo di Configuration Manager  
 Per informazioni sui file di log di distribuzione del sistema operativo creati da Microsoft System Center 2012 R2 Configuration Manager, vedere [Guida tecnica per i file di log in Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Quando si esegue l'Utilità di migrazione stato utente Windows, MDT aggiunge automaticamente le opzioni di registrazione per salvare i file di log USMT nei percorsi dei file di log di MDT. I file di log e il momento della loro creazione sono i seguenti:  

-   **USMTEstimate.log**. Creato durante la stima dei requisiti di USMT  

-   **USMTCapture.log**. Creato da USMT durante l'acquisizione dei dati  

-   **USMTRestore.log**. Creato da USMT durante il ripristino dei dati  

 Lo script ZeroTouchInstallation.vbs analizza automaticamente i file di log dello stato di avanzamento USMT alla ricerca di errori e avvisi. Lo script genera l'ID evento 41010 in Microsoft System Center Operations Manager con il riepilogo seguente (dove *usmt_type* è **ESTIMATE**, **SCANSTATE** o **LOADSTATE**; *error_count* è il numero totale di errori rilevati e *warning_count* è il numero totale di avvisi rilevati):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Se il numero di errori è maggiore di 0, l'evento è di tipo Errore. Se il numero di avvisi è maggiore di 0 senza errori, l'evento è di tipo Avviso. In caso contrario, l'evento è di tipo Informativo.  

## <a name="identifying-error-codes"></a>Identificazione dei codici di errore  
Nella tabella 1 sono elencati i codici di errore che creano gli script di MDT e una descrizione di ogni codice. Questi codici di errore vengono registrati nel file BDD.log.  

### <a name="table-1-error-codes-and-their-description"></a>Tabella 1. Codici di errore con relativa descrizione  

|**Codice di errore**|**Descrizione**|  
|-|-|  
|5201|Impossibile stabilire una connessione alla condivisione di distribuzione. Non sarà possibile proseguire con la distribuzione.|  
|5203|Impossibile stabilire una connessione alla condivisione di distribuzione. Non sarà possibile proseguire con la distribuzione.|  
|5205|Impossibile stabilire una connessione alla condivisione di distribuzione. Non sarà possibile proseguire con la distribuzione.|  
|5206|La Distribuzione guidata è stata annullata o non è stata completata. Non sarà possibile proseguire con la distribuzione.|  
|5207|Impossibile stabilire una connessione alla condivisione di distribuzione. Non sarà possibile proseguire con la distribuzione.|  
|5208|**DeploymentType** non è impostato. È obbligatorio impostare un valore per **SkipWizard**.|  
|5208|Impossibile trovare il Sequencer delle attività SMS. Non sarà possibile proseguire con la distribuzione.|  
|5400|Creare l'oggetto: **Set *class_instance* = New *class_name***|  
|5490|Creare MSXML2.DOMDocument.|  
|5495|Creare MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Verificare che il guid sistema operativo %OSGUID% esista.|  
|5602|Aprire XML con OSGUID: %OSGUID%.|  
|5610|Verificare il file.|  
|5630|Verificare il file *ImagePath*.|  
|5640|Verificare il file *ImagePath*.|  
|5641|FindFile: ImageX.exe.|  
|5643|Trovare BootSect.exe.|  
|5650|Verificare la directory *SourcePath*.|  
|5651|Verificare la directory *SourcePath*\Platform.|  
|5652|FindFile: bootsect.exe.|  
|6001|Verificare l'unità.|  
|6002|Verificare l'unità.|  
|6010|Verificare TSGUID.|  
|6020|Robocopy ha restituito il valore *valore*.|  
|6021|Robocopy ha restituito il valore *valore*.|  
|6101|Verificare la presenza del file *DeployCab*.|  
|6102|Espandere i file Sysprep da DEPLOY.CAB.|  
|6111|Eseguire Sysprep.exe.|  
|6121|Eseguire Sysprep.|  
|6191|Verificare **CloneTag** nel registro di sistema per verificare che Sysprep sia stata completata.|  
|6192|Verificare **SystemSetupInProgress** nel registro di sistema per verificare che Sysprep sia stata completata.|  
|6401|Server DHCP autorizzato.|  
|6501|Impossibile eseguire il backup del computer, nessun percorso di rete (**BackupShare**, **BackupDir**) specificato.|  
|6502|ERRORE. Impossibile individuare IMAGEX, impossibile eseguire il backup.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Programmi di protezione configurati.|  
|6702|File di avvio spostati.|  
|6703|Creare la partizione BDE.|  
|6704|Deframmentare l'unità.|  
|6705|Compattare l'unità.|  
|6706|Verifica di più di 1 partizione.|  
|6707|Creare i file di avvio.|  
|6708|Crittografare il disco.|  
|6709|Connettersi al provider WMI MicrosoftVolumeEncryption.|  
|6710|Crittografia del disco in corso.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Salvare la chiave esterna su file.|  
|6715|Proteggere con chiave esterna.|  
|6716|Salvare la chiave esterna su file.|  
|6717|Proteggere la chiave con password numerica.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Salvare la password su file.|  
|6719|Aprire *PasswordFile*.|  
|6720|Crittografare l'unità.|  
|6721|Aprire *DiskPartFile*.|  
|6722|Creazione una partizione.|  
|6723|Ottenere l'unità BDE esistente.|  
|6724|Aprire *DiskPartFile*.|  
|6727|Tentare di aprire *DiskPartFile*.|  
|6729|Creare il file di testo *DiskPartFile*.|  
|6730|Eseguire **cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1**|  
|6731|Trovare bcdboot.exe.|  
|6732|Connettersi al provider di Microsoft TPM.|  
|6733|Ottenere un'istanza TPM nella classe provider.|  
|6734|Ottenere l'istanza TPM.|  
|6735|Verificare se TPM è abilitato.|  
|6736|Verificare se TPM è attivato.|  
|6737|Verificare se TPM è di proprietà.|  
|6738|Verificare se la proprietà di TPM è consentita.|  
|6739|Verificare se TPM è abilitato.|  
|6740|Verificare se TPM è attivato.|  
|6741|Verificare se TPM è di proprietà e la proprietà è consentita.|  
|6741|Password del proprietario del TPM impostata|  
|6742|P@ssword del proprietario del TPM impostata su **AdminP@ssword**.|  
|6743|Impostare un valore per la P@ssword del proprietario del TPM.|  
|6744|Verificare se TPM è abilitato.|  
|6745|Controllare il proprietario del TPM.|  
|6746|Controllare la coppia di chiavi di approvazione.|  
|6747|Verificare se TPM è attivato.|  
|6748|Verificare se la proprietà di TPM è consentita.|  
|6749|Convertire la p@ssword del proprietario in autorizzazione del proprietario.|  
|6750|Creare una coppia di chiavi di approvazione.|  
|6751|Cambiare l'autorizzazione del proprietario.|  
|6752|Eseguire **Cmd**.|  
|6753|Convalidare il TPM.|  
|6754|Ottenere l'istanza BDE.|  
|6755|Proteggere la chiave con il TPM.|  
|6756|Controllare se sono presenti supporti rimovibili da configurare. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Proteggere la chiave con il TPM e la chiave di avvio.|  
|6758|Cercare il pin BDE.|  
|6759|Proteggere la chiave con il TPM e il pin.|  
|6760|Trovare il supporto rimovibile di **BDEKeyLocation**.|  
|6761|Proteggere con chiave esterna.|  
|6762|P@ssword di ripristino salvata in *PasswordFile*.|  
|6764|Configurare il criterio BitLocker.|  
|7000|Impossibile individuare ZTIConfigure.xml. Interruzione in corso.|  
|7001|Ricerca di AnswerFile automatico.|  
|7100|ERRORE. Eseguire questo script solo nel sistema operativo completo.|  
|7101|ERRORE. Valori insufficienti specificati per la generazione del file di risposte DCPromo.|  
|7102|ERRORE. Le proprietà obbligatorie per la creazione di un nuovo controller di dominio di replica non sono state specificate.|  
|7103|ERRORE. Le proprietà obbligatorie per la creazione di un nuovo controller di dominio figlio non sono state specificate.|  
|7104|ERRORE. Le proprietà obbligatorie per la creazione di una nuova foresta non sono state specificate.|  
|7105|ERRORE. Le proprietà obbligatorie per la creazione di una nuova foresta non sono state specificate.|  
|7200|Impossibile configurare il server DHCP perché il servizio non è installato.|  
|7201|Impossibile leggere i dettagli relativi all'ambito. `GetScopeDetails()` non riuscita.|  
|7202|Non sono stati specificati valori sufficienti per la creazione di ambito.|  
|7203|Non sono stati forniti valori sufficienti per impostare l'intervallo IP per questo ambito.|  
|7204|Nessun valore specificato per l'intervallo di esclusione ambito.|  
|7300|Impossibile eseguire i comandi DNS.|  
|7700|Non è uno scenario di nuovo computer. Chiusura della partizione disco.|  
|7701|Disco non sufficientemente grande per il sistema e le partizioni BDE. Spazio richiesto = 1,5 GB.|  
|7702|Disco non sufficientemente grande per il sistema e le partizioni WinRE. Spazio richiesto = 10 GB.|  
|7703|DeployRoot è sul disco *DiskIndex*. Esecuzione di uno scenario OEM: ignorare.|  
|7704|Esecuzione di uno scenario OEM: ignorare.|  
|7704|Le partizioni estese e logiche non sono consentite con BitLocker.|  
|7712|Verificare che unità/*volume unità* sia presente. Formattare.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERRORE. L'attività di ripristino dello stato ZTITatoo deve essere in esecuzione nell'intero sistema operativo. Interruzione in corso.|  
|9701|Codice restituito dalla stima USMT diverso da zero, rc = *Error*.|  
|9702|Acquisizione dello stato utente impossibile. Spazio locale insufficiente e nessun percorso di rete (UDShare, UDDir) specificato.|  
|9703|Codice restituito dall'acquisizione USMT diverso da zero, rc = *Error*.|  
|9704|Non è stata specificata alcuna opzione riga di comando valida.|  
|9801|ERRORE. Tentativo di distribuire un sistema operativo client in un computer che esegue un sistema operativo server.|  
|9802|ERRORE. Tentativo di distribuire un sistema operativo server in un computer che esegue un sistema operativo client.|  
|9803|ERRORE. L'aggiornamento non è autorizzato nel computer (OSInstall=*OSInstall*). Interruzione in corso.|  
|9804|ERRORE: *Memory* MB di memoria sono insufficienti. Sono richiesti almeno *Memory* MB di memoria.|  
|9805|ERRORE. Velocità del processore *ProcessorSpeed* MHz insufficiente.  È richiesto almeno un processore da *ProcessorSpeed*.|  
|9806|ERRORE. Spazio insufficiente disponibile in *Drive*. Sono necessari altri *Size* MB.|  
|9807|ERRORE. Spazio insufficiente disponibile in *Drive*. Sono necessari altri *Size* MB.|  
|9901|Lo script ZTIWindowsUpdate non deve essere eseguito in Windows PE.|  
|9902|ZTIWindowsUpdate è stato eseguito e non è stato completato per troppe volte. Numero = *Count*.|  
|9903|Si è verificato un problema imprevisto installando la versione aggiornata di Windows Update Agent, rc = *Error*.|  
|9904|Impossibile creare l'oggetto: **Microsoft.Update.Session**.|  
|9905|Impossibile creare l'oggetto: **Microsoft.Update.UpdateColl**.|  
|9906|Il file critico *File* non è stato trovato. Interruzione in corso.|  
|10000|Creare l'oggetto: **Set oLTICleanup = New LTICleanup**.|  
|10201|Impossibile unire il dominio *Domain*. Interrompere l'installazione.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Eseguire il programma *LTISuspend*.|  
|41024|Eseguire ImageX.|  
|52012|Non sono impostati tutti i parametri della procedura guidata.|  

 L'elenco 1 contiene l'estratto di un file di log che illustra come trovare il codice di errore. In questo estratto il codice di errore segnalato è 5001.  

 **Elenco 1. Estratto del file SMSTS.log che contiene il codice di errore 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Conversione dei codici di errore  
 Molti codici di errore presentati nei file di log sembrano enigmatici e difficile da collegare a un'effettiva condizione di errore. Il processo seguente dimostra come convertire un codice di errore e ottenere informazioni significative che potrebbero rivelarsi utili per la risoluzione dei problemi.  

 **Problema**: l'acquisizione di un'immagine ha esito negativo con il codice di errore 0x80070040.  

 **Possibile soluzione 1**: il codice di errore presentato è in formato esadecimale e va convertito in formato decimale. A tale scopo, procurarsi una calcolatrice scientifica. La calcolatrice inclusa nei sistemi operativi Windows è adatta per questa attività.  

 **Per convertire un codice di errore**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Accessori**, quindi fare clic su **Calcolatrice**.  

2.  Nel menu **Visualizza**, fare clic su **Scientifica**.  

3.  Selezionare **Hex**, quindi immettere le ultime quattro cifre del codice, ovvero in questo caso, **0040**, come illustrato nella Figura 1.  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Figura 1. Conversione dell'errore  

     **Figura 1. Conversione dell'errore**  

     Si noti che quando la calcolatrice è in modalità esadecimale gli zeri iniziali non vengono visualizzati.  

4.  Selezionare **Dec**.  

     Il valore esadecimale *40* viene convertito in valore decimale *64*.  

5.  Aprire una finestra del prompt dei comandi, digitare **NET HELPMSG 64** e premere INVIO.  

     Il comando **NET HELPMSG** converte il codice di errore numerico in testo significativo. Nel caso di questo codice di errore, la conversione restituisce “Il nome di rete specificata non è più disponibile”.  

 Queste informazioni indicano che potrebbe essere presente un problema di rete nel computer di destinazione o tra il computer di destinazione e il server in cui risiede la condivisione di distribuzione. Questi problemi potrebbero indicare anche che i driver di rete non sono installati correttamente o una discordanza nelle impostazioni velocità e duplex.  

 **Possibile soluzione 2:** utilizzare l'utilità Error Code Look-up di Microsoft Exchange Server. Questa utilità della riga di comando è d'aiuto per la conversione dei codici di errore. È disponibile nel [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=985).  

### <a name="review-of-sample-logs"></a>Esaminare i registri di esempio  
 MDT crea file di log che è possibile utilizzare per risolvere problemi del processo di distribuzione di MDT. Nelle sezioni seguenti vengono forniti esempi di come utilizzare i file di log di MDT per risolvere i problemi del processo di distribuzione:  

-   Problemi relativi agli errori di accesso al database MDT (MDT DB) descritti in [Problemi di accesso al database](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Problemi di accesso al database  
 **Problema:** si verifica un errore durante una distribuzione per cui è stato utilizzato un file CustomSettings.ini contenente numerose sezioni e l'indicazione della priorità di ogni sezione da elaborare tramite la proprietà **Priority**. BDD.log contiene i messaggi di errore seguenti:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Per maggiore chiarezza, il contenuto del file di log è stato rappresentato come appare se visualizzato utilizzando il programma Trace32.  

 **Possibile soluzione:** il problema, come indicato nella prima riga del file di log di esempio, è che l'autorizzazione per l'accesso al database è stata negata. Pertanto, lo script non riesce a stabilire una connessione sicura al database, probabilmente perché non erano disponibili un ID utente e una password. Di conseguenza, l'accesso al database è stato tentato tramite l'account del computer. Il modo più semplice per risolvere questo problema è concedere a tutti gli utenti l'accesso in lettura al database.  

## <a name="troubleshooting"></a>Troubleshooting  
 Prima di imbarcarsi in complessi processi di risoluzione dei problemi, esaminare gli elementi seguenti per assicurarsi che tutti i requisiti associati siano stati soddisfatti:  

-   Se non sono stati soddisfatti tutti i prerequisiti software e hardware, possono verificarsi dei problemi di installazione.  

### <a name="application-installation"></a>Installazione dell'applicazione  
 Esaminare le soluzioni indicate per correggere i problemi relativi all'installazione dell'applicazione:  

-   I file di origine dell'installazione sono bloccati per motivi di sicurezza come descritto in [File eseguibili bloccati](#BlockedExecutables)  

-   Perdita della connettività di rete come descritto in [Perdita della connettività di rete](#LostNetworkConnections)  

-   Errore di installazione 30029 durante l'installazione dei file di Microsoft Office System 2007 o correlati come descritto in [Microsoft Office System 2007](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> File eseguibili bloccati  
 **Problema:** se i file di origine dell'installazione vengono scaricati da Internet, è probabile che vengano contrassegnati con uno o più flussi di dati del file system NTFS. Per ulteriori informazioni sui flussi di dati NTFS, vedere [File Streams](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx) (Flussi di file). L'esistenza di flussi di dati del file system NTFS potrebbe causare la visualizzazione dell'avviso **Apri file – Avviso di sicurezza**. L'installazione non verrà avviata fino a quando non si fa clic su **Esegui** al prompt.  

 Nella Figura 2 sono visualizzati i flussi di dati del file system NTFS utilizzando il comando **More** e l'[utilità Streams](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Figura 2. Flussi di dati NTFS  

 **Figura 2. Flussi di dati NTFS**  

 **Possibile soluzione 1:** fare clic con il pulsante destro del mouse sul file di origine dell'installazione e quindi su **Proprietà**. Fare clic su **Sblocca**, quindi fare clic su **OK** per rimuovere i flussi di dati del file system NTFS dal file. Ripetere questo processo per ogni file di origine dell'installazione bloccato dalla presenza di uno o più flussi di dati del file system NTFS.  

 **Possibile soluzione 2:** utilizzare l'utilità Streams, come illustra la REF \_Ref308173670 \\h Figura 2, per rimuovere i flussi di dati del file system NTFS dal file di origine dell'installazione. L'utilità Streams può rimuovere i flussi di dati del file system NTFS da uno o più file o cartelle in una sola volta.  

####  <a name="LostNetworkConnections"></a> Perdita della connettività di rete  
 **Problema:** un'installazione potrebbe non riuscire se installa driver dispositivo o modifica configurazioni di rete e dispositivo. Queste modifiche possono comportare una perdita della connettività di rete che, a sua volta, causa la non riuscita dell'installazione.  

 **Possibile soluzione:** implementare lo script ZTICacheUtil.vbs per abilitare il download e l'esecuzione per l'installazione. Questo script è progettato per perfezionare l'annuncio affinché il download e l'esecuzione vengano abilitati. Il download usa il servizio trasferimento intelligente in background \(BITS\) se il punto di distribuzione di Configuration Manager è WebDAV e BITS è attivo. Allo stesso tempo, modifica Configuration Manager affinché esegua prima lo script ZTICache.vbs, in modo che il programma non elimini se stesso durante il processo di distribuzione.  

####  <a name="MicrosoftOfficeSystem"></a> Microsoft Office System 2007  
 **Problema:** durante la distribuzione di Office System 2007 includendo un file \(MSP\) di patch di Windows Installer, l'installazione potrebbe non riuscire e generare il codice di errore 30029.  

 Ulteriori indagini nel ZTIApplications.log mostrano che sono presenti i messaggi seguenti:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Possibile soluzione 1:** spostare il file MSP nella directory Updates e quindi eseguire setup.exe senza specificare l'opzione **\/adminfile**. Per ulteriori informazioni sulla distribuzione degli aggiornamenti durante l'installazione, vedere [Distribuzione di Office System 2007](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Possibile soluzione 2:** verificare che nel file MSP la casella di controllo **Non visualizzare finestre modali** non sia selezionata. Per ulteriori informazioni sulla configurazione di questa impostazione, vedere [Panoramica della distribuzione di Office System 2007](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>Accesso automatico  
 Esaminare i problemi e le soluzioni ai problemi di accesso automatico:  

-   Interruzione dei processi di distribuzione di LTI e Zero Touch Installation \(ZTI\) a causa della presenza di intestazioni di sicurezza per l'accesso come descritto in [Intestazioni di sicurezza per l'accesso](#LogonSecutiryBanners)  

-   Interruzione dei processi di distribuzione LTI e ZTI a causa delle richieste di immissione delle credenziali utente come descritto in [Richieste di immissione delle credenziali utente](#PromtedforUserCredentials)  

####  <a name="LogonSecutiryBanners"></a> Intestazioni di sicurezza per l'accesso  
 **Problema:** le sequenze di attività di MDT vengono elaborate durante una sessione utente interattiva per la quale è necessario che il computer di destinazione sia autorizzato ad accedere automaticamente utilizzando un account amministratore specificato. Se è presente un oggetto Criteri di gruppo che applica un'intestazione di sicurezza per l'accesso, l'accesso automatico non può avvenire perché l'intestazione di sicurezza arresta il processo di accesso in attesa che l'utente accetti i criteri visualizzati.  

 **Possibile soluzione:** assicurarsi che l'oggetto Criteri di gruppo venga applicato ad unità organizzative specifiche e non incluso nell'oggetto Criteri di gruppo del dominio predefinito. Quando si aggiungono computer al dominio, specificare che devono essere aggiunti a un'unità organizzativa che non è interessata da un oggetto criteri di gruppo che applica un'intestazione di sicurezza per l'accesso. Includere nell'Editor della sequenza attività uno script che sposti l'account computer nell'unità organizzativa desiderata come uno degli ultimi passaggi della sequenza attività.  

> [!NOTE]
>  Se si riutilizzano account Servizi di dominio Active Directory \(AD DS\) esistenti, assicurarsi che prima della distribuzione al computer di destinazione, l'account del computer di destinazione sia stato spostato in un'unità organizzativa non interessata dall'oggetto Criteri di gruppo che applica l'intestazione di sicurezza per l'accesso.  

####  <a name="PromtedforUserCredentials"></a> Richieste di immissione delle credenziali utente  
 **Problema:** è stata creata l'immagine di un computer che è stato aggiunto al dominio. Durante la distribuzione della nuova immagine al computer di destinazione, il processo di distribuzione si interrompe perché l'accesso automatico non avviene e all'utente viene richiesto di immettere le credenziali appropriate. Il processo di distribuzione riprende quando l'utente fornisce le credenziali ed esegue l'accesso.  

 **Possibile soluzione:** durante l'acquisizione di immagini, il computer di origine non va aggiunto a un dominio. Se il computer è stato aggiunto a un dominio, aggiungere il computer a un gruppo di lavoro, acquisire nuovamente l'immagine e tentare la distribuzione a un computer di destinazione per determinare se il problema è stato risolto.  

### <a name="bios"></a>BIOS  
 **Problema:** durante la distribuzione a un computer di destinazione dotato di tecnologia Intel vPro, la distribuzione può arrestarsi con un errore irreversibile. Nonostante tutti i driver aggiornati siano stati inclusi come standard in Deployment Workbench, il computer di destinazione non si avvia.  

 Possibile soluzione: controllare le impostazioni BIOS del computer di destinazione per determinare se la modalità Serial ATA predefinita è configurata come AHCI \(Advanced Host Controller Interface\). Sfortunatamente, alcuni sistemi operativi Windows non supportano AHCI per impostazione predefinita.  

### <a name="database-problems"></a>Problemi di database  
 Esaminare i problemi e le soluzioni legati al database:  

-   Errori generati da una configurazione errata dei firewall nel server di database come descritto in [Richieste del browser a SQL Server bloccate](#BlockedSQLServerBrowserRequests)  

-   Errori generati in seguito a connessioni con il server di database interrotte, come descritto in [Connessioni named pipe](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Richieste del browser a SQL Server bloccate  
 **Problema:** durante il processo di distribuzione di MDT, è possibile recuperare informazioni dai database Microsoft SQL Server®. Tuttavia, possono sorgere errori generati da un'errata configurazione del firewall nel server di database.  

 **Possibile soluzione:** Windows Firewall in Windows Server consente di impedire l'accesso non autorizzato alle risorse del computer. Tuttavia, se il firewall è configurato in modo non corretto, i tentativi di connessione a un'istanza di SQL Server potrebbero essere bloccati. Per accedere a un'istanza di SQL Server protetta da firewall, configurare il firewall nel computer che esegue SQL Server. Per ulteriori informazioni sulla configurazione delle porte del firewall per SQL Server, vedere l'articolo del supporto tecnico Microsoft [Come aprire la porta del firewall per SQL Server su Windows Server 2008](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Connessioni named pipe  
 **Problema:** durante il processo di distribuzione di MDT, è possibile recuperare informazioni dai database SQL Server. Tuttavia, potrebbe essere generati errori causati da connessioni interrotte di SQL Server. Questi errori possono essere causati da una mancata abilitazione delle connessioni named pipe in Microsoft SQL Server.  

 **Possibile soluzione:** per risolvere questi problemi, abilitare le named pipe in SQL Server. Inoltre, specificare la proprietà **SQLShare** necessaria per stabilire una connessione a un database esterno utilizzando named pipe. Durante la connessione tramite named pipe, utilizzare la sicurezza integrata per stabilire la connessione al database. Nel caso di distribuzioni LTI, è l'account utente specificato che esegue la connessione al database. Per le distribuzioni ZTI che utilizzano Configuration Manager, è l'account di accesso alla rete che si connette al database. Poiché per impostazione predefinita Windows PE non dispone di alcun contesto di sicurezza, è necessario stabilire una connessione di rete al server di database per creare un contesto di sicurezza per l'utente che effettua la connessione.  

 La condivisione di rete che la proprietà **SQLShare** specifica rappresenta un mezzo per connettersi al server e ottenere un contesto di sicurezza appropriato. È necessario avere accesso in lettura alla condivisione. Una volta effettuata la connessione, è possibile stabilire la connessione named pipe al database. La proprietà **SQLShare** non è necessaria e non deve essere utilizzata quando si effettua una connessione TCP\/IP al database.  

 Abilitare le connessioni named pipe eseguendo le attività seguenti in base alla versione di SQL Server in uso:  

-   Abilitare le connessioni named pipe per SQL Server 2008 R2 come descritto in [Abilitare le connessioni named pipe in SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Abilitare le connessioni named pipe per SQL Server 2005 come descritto in [Abilitare le connessioni named pipe in SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Abilitare le connessioni named pipe in SQL Server 2008 R2  
 Per abilitare le connessioni named pipe in SQL Server 2008 R2, eseguire i passaggi seguenti:  

1.  Nel computer che esegue SQL Server 2008 R2 e che ospita il database su cui eseguire la query, fare clic su **Avvio**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft SQL Server 2008 R2**, quindi fare clic su **SQL Server Management Studio**.  

2.  Nella console di **Microsoft SQL Server Management Studio**, in **Esplora oggetti**, fare clic con il pulsante destro del mouse su ***sql\_server\_name***, quindi fare clic su **Proprietà** \(dove *sql\_server\_name* è il nome del computer che esegue SQL Server da configurare\).  

3.  Viene visualizzata la finestra di dialogo Proprietà server \- ***sql\_server\_name***.  

4.  Nella finestra di dialogo **Proprietà server** \- ***sql\_server\_name***, in **Seleziona una pagina**, fare clic su  **Connessioni**.  

5.  Nella pagina **Connessioni** verificare che la casella di controllo **Consenti connessioni remote a questo server** sia selezionata e fare clic su **OK**.  

6.  Chiudere la console di Microsoft SQL Server Management Studio.  

7.  Nel computer che esegue SQL Server 2008 R2 e che ospita il database su cui eseguire la query, fare clic su **Avvio**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft SQL Server 2008 R2**, quindi fare clic su **Strumenti di configurazione** e infine su **Gestione configurazione SQL Server**.  

8.  Nella console di **Gestione configurazione SQL Server**, passare a Gestione configurazione SQL Server \(locale\) \/ Configurazione di rete SQL Server \/ Protocolli per *sql\_instance* \(dove *sql\_instance* è il nome dell'istanza di SQL Server da configurare\).  

9. Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Named pipe**, quindi fare clic su **Abilita**.  

     La finestra di dialogo di avviso visualizzata informa che le modifiche verranno salvate ma che per renderle effettive è necessario arrestare e riavviare il servizio.  

10. Nella finestra di dialogo **Avviso** fare clic su **OK**.  

11. Nella console di **Gestione configurazione SQL Server** passare a Gestione configurazione SQL Server \(locale\) \/ Servizi di SQL Server.  

12. Nel riquadro dei dettagli, fare clic con il pulsante destro su**SQL Server*\(sql\_instance\)***, quindi fare clic su **Riavvia** \(dove *sql\_instance* è il nome dell'istanza di SQL Server configurata al passaggio 2\).  

     L'indicatore di avanzamento di Gestione configurazione SQL Server mostra lo stato di riavvio dei servizi. Dopo che il servizio è stato riavviato, l'indicatore di stato si chiude.  

13. Chiudere la console di SQL Configuration Manager.  

 Per ulteriori informazioni, vedere [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx) (Come abilitare le connessioni remote in SQL Server 2008).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Abilitare le connessioni named pipe in SQL Server 2005  
 Per abilitare le connessioni named pipe in SQL Server 2005, eseguire i passaggi seguenti:  

1.  Nel computer che esegue SQL Server 2005 e che ospita il database su cui eseguire la query, fare clic su **Avvio**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft SQL Server 2005**, quindi fare clic su **Strumenti di configurazione** e infine su **Configurazione superficie di attacco di Microsoft SQL Server**.  

2.  Nella finestra di dialogo **Configurazione superficie di attacco di Microsoft SQL Server 2005** fare clic su **Configurazione superficie di attacco per servizi e connessioni**.  

3.  Nella finestra di dialogo **Configurazione superficie di attacco per servizi e connessioni– *server\_name*** \(dove *server\_name* è il nome del computer che esegue SQL Server 2005\), in corrispondenza di **Selezionare un componente, quindi configurarne i servizi e le connessioni**, passare a MSSQLSERVER\\Motore di database e fare clic su **Connessioni remote**.  

4.  Fare clic su **Connessioni locali e remote**, fare clic su **Usa sia TCP\/IP che named pipe**, quindi fare clic su **Applica**.  

5.  Nella finestra di dialogo **Configurazione superficie di attacco per servizi e connessioni – *server\_name*** \(dove *server\_name* è il nome del computer che esegue SQL Server 2005\), in corrispondenza di **Selezionare un componente, quindi configurarne i servizi e le connessioni**, passare a MSSQLSERVER\\Motore di database e fare clic su **Servizio**.  

6.  Fare clic su **Arresta**.  

     Il servizio MSSQLSERVER si arresta.  

7.  Fare clic su **Avvia**.  

     Il servizio MSSQLSERVER si avvia.  

8.  Fare clic su **OK**.  

9. Chiudere Configurazione superficie di attacco di Microsoft SQL Server 2005.  

 Per ulteriori informazioni, vedere l'articolo del supporto tecnico Microsoft [Come configurare SQL Server 2005 per consentire le connessioni remote](http://support.microsoft.com/kb/914277)  

### <a name="deployment-scripts"></a>Script di distribuzione  
 Esaminare i problemi e le soluzioni legati a MDT:  

-   Sono state richieste le credenziali utente e viene visualizzato l'errore 0x80070035 come descritto in [Credentials_script](#Credentials_script)  

-   Viene visualizzato il messaggio di errore “Wuredist.cab non trovato” come descritto in [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Credentials\_script  
 **Problema:** durante l'ultimo avvio di un computer appena distribuito, all'utente viene richiesto di fornire le credenziali utente e può essere visualizzato l'errore 0x80070035, che indica che il percorso di rete non è stato trovato.  

 **Possibile soluzione:** assicurarsi che il file WIM non include una cartella MININT o \_SMSTaskSequence. Per eliminare queste cartelle, utilizzare innanzitutto l'utilità ImageX per montare il file WIM e quindi eliminare le cartelle.  

> [!NOTE]
>  Se quando si tenta di eliminare le cartelle dal file WIM si verifica un errore di accesso negato, aprire una finestra del prompt dei comandi, passare alla radice dell'immagine contenuta nel file WIM ed eseguire **RD MININT** e **RD \_SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problema:** se si usa lo script ZTIWindowsUpdate.wsf per applicare gli aggiornamenti software durante la distribuzione, tenere presente che questo script può comunicare direttamente con il sito Web Microsoft Update per scaricare e installare i file binari necessari per l'agente Windows Update, cercare aggiornamenti software applicabili, scaricare i file binari degli aggiornamenti software applicabili e installare i file binari scaricati. Questo processo richiede che l'infrastruttura di rete sia configurata in modo da consentire al computer di destinazione di poter accedere al sito Web Microsoft Update.  

 Se la condivisione di distribuzione non contiene i file di installazione dell'agente Windows Update e il computer di destinazione non ha accesso a Internet, nei file ZTIWindowsUpdate.log e BDD.log viene segnalato l'errore “Wuredist.cab non trovato”.  

 **Possibile soluzione:** seguire i passaggi illustrati nella sezione "ZTIWindowsUpdate.wsf" del documento di MDT *Informazioni di riferimento sul toolkit*.  

### <a name="deployment-shares"></a>Condivisioni di distribuzione  
 Esaminare i problemi e le soluzioni legati alle condivisioni di distribuzione:  

-   L'aggiornamento dei file WIM non viene eseguito durante l'aggiornamento di una condivisione di distribuzione, come descritto in [Impossibile aggiornare i file WIM](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Impossibile aggiornare i file WIM  
 In un ambiente "semplice":  

-   WIMGAPI.DLL viene generalmente prelevato da MDT da C:\\Windows\\system32 \(sempre nel percorso\). La versione di questa WIMGAPI.DLL deve corrispondere alla versione, cioè alla build, del sistema operativo.  

-   Nei sistemi operativi a 64 bit, MDT utilizza sempre il file WIMGAPI.DLL x64. Solo tale file deve essere presente nel percorso di sistema. Nei sistemi operativi a 32 bit, MDT utilizza sempre il file WIMGAPI.DLL x86. Solo tale file deve essere presente nel percorso di sistema. \(Altri prodotti, ad esempio Configuration Manager, utilizzano la versione a 32 bit di WIMGAPI.DLL anche sui sistemi operativi a 64 bit, ma gestiscono e installano tale versione.\)  

 **Problema:** durante il tentativo di aggiornare una condivisione di distribuzione, l'utente viene informato che il montaggio di uno o più file WIM non è riuscito.  

 **Possibile soluzione:** aprire una finestra del prompt dei comandi ed eseguire **where WIMGAPI.DLL**. Per la prima voce nell'elenco, cioè la prima posizione trovata dalla ricerca del percorso, verificare che la proprietà **Version** corrisponda alla build di Windows Assessment and Deployment Kit \(Windows ADK\) installata. Assicurarsi inoltre che la proprietà corrisponda al numero di build del sistema operativo.  

### <a name="the-windows-deployment-wizard"></a>Distribuzione guidata Windows  
 Esaminare i problemi e le soluzioni legati alla Distribuzione guidata Windows:  

-   Le pagine della Distribuzione guidata Windows sono visualizzate anche quando LTI è configurato per ignorare le pagine della procedura guidata, come descritto in [Le pagine della procedura guidata non vengono ignorate](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> Le pagine della procedura guidata non vengono ignorate  
 **Problema:** una pagina della procedura guidata viene visualizzata anche se il file CustomSettings.ini o MDT DB specificano che la procedura guidata deve essere ignorata.  

 **Possibile soluzione:** per evitare di visualizzare una pagina della procedura guidata, includere tutte le proprietà che verrebbero specificate in tale pagina nel file CustomSettings.ini o in MDT DB insieme ai valori appropriati. Se una proprietà è configurata in modo errato per una pagina della procedura guidata da ignorare, tale pagina verrà visualizzata. Per altre informazioni sulle proprietà che devono essere configurate per fare in modo che una pagina della procedura guidata venga ignorata, vedere la sezione relativa alle proprietà per le pagine ignorate della Distribuzione guidata nel documento di MDT *Informazioni di riferimento sul toolkit*.  

### <a name="disks-and-partitioning"></a>Dischi e partizionamento  
 Esaminare i problemi e le soluzioni legati al partizionamento del disco:  

-   Problemi di crittografia dell'unità BitLocker come descritto in [Crittografia unità BitLocker](#BitLockerDriveEncryption)  

-   Errori di partizionamento del disco come descritto in Errori di partizionamento del disco  

-   Errori durante gli scenari di distribuzione degli aggiornamenti al computer dovuti a dischi logici o dinamici, come descritto in [Supporto per i dischi logici e dinamici](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> Crittografia unità BitLocker  
 Per poter essere svolta correttamente, la distribuzione di BitLocker richiede una configurazione specifica. I seguenti potenziali problemi possono essere legati alla configurazione del computer di destinazione:  

-   Nelle distribuzioni ZTI e UDI, lo script ZTIBde.wsf non riesce con l'errore “Impossibile aprire la chiave del Registro di sistema ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ per la lettura”, come descritto in [Lo script ZTIBde.wsf non riesce con l'errore "Impossibile aprire la chiave del Registro di sistema ‘HKEY_CURRENT_USER\Control Panel\International\LocaleName’ per la lettura"](#ZTIBde.wsf).  

-   Dispositivi USB, unità CD, unità DVD o altri dispositivi multimediali rimovibili nel computer di destinazione che vengono visualizzati come più lettere di unità, come descritto in [I dispositivi vengono visualizzati come più lettere di unità](#DevicesAppearasMultipleDriveLetters)  

-   Compattazione dell'unità C del computer di destinazione per trovare sufficiente spazio non allocato del disco come descritto in [Problemi con la compattazione dei dischi](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> Lo script ZTIBde.wsf non riesce con l'errore “Impossibile aprire la chiave del Registro di sistema ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ per la lettura”  
 **Problema:** durante la distribuzione di BitLocker nel computer di destinazione in ZTI o UDI, lo script ZTIBde.wsf non riesce e genera l'errore “Impossibile aprire la chiave del Registro di sistema ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ per la lettura.”  

 **Possibile soluzione:** specificare le impostazioni locali nella proprietà **UILanguage**. In ZTI e UDI lo script ZTIBde.wsf viene eseguito nel controllo del sistema, quindi non viene caricato un profilo utente completo. Quando lo script ZTIBde.wsf tenta di leggere le informazioni sulle impostazioni locali non le trova nel registro di sistema, perché il registro di sistema, o profilo utente, non è stato caricato completamente. Come possibile soluzione si possono specificare le impostazioni locali nella proprietà **UILanguage**.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> I dispositivi vengono visualizzati come più lettere di unità  
 **Problema:** alcuni dispositivi possono essere visualizzati come più lettere di unità logiche, a seconda del modo in cui sono state partizionate. In alcuni casi, possono emulare un'unità disco floppy da 1,44 MB e un'unità di archiviazione di memoria. Di conseguenza, può accadere che Windows assegni le stesse lettere di unità A e B del dispositivo per l'emulazione del disco floppy e la lettera F per l'unità di archiviazione di memoria. Per impostazione predefinita, gli script di MDT utilizzano la lettera di unità più bassa, in questo esempio, la A.  

 **Possibile soluzione:** ignorare l'impostazione predefinita nella pagina **Specify the BitLocker recovery details** (Specificare i dettagli di ripristino di BitLocker) nella Distribuzione guidata Windows. Nella pagina di riepilogo della Distribuzione guidata Windows viene visualizzato un avviso per informare l'utente della lettera di unità selezionata per archiviare le informazioni di ripristino di BitLocker. Inoltre, nei file BDD.log e ZTIBDE.log vengono registrati i dispositivi multimediali rimovibili rilevati e quello scelto per archiviare le informazioni di ripristino di BitLocker.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problemi con la compattazione dei dischi  
 **Problema:** nel computer di destinazione non esiste spazio su disco non allocato sufficiente per abilitare BitLocker. Per la distribuzione di BitLocker in un computer di destinazione, sono necessari almeno 2 GB di spazio su disco non allocato per creare il volume di sistema. Il *volume di sistema* è il volume che contiene i file specifici dell'hardware necessari per caricare Windows dopo che il BIOS ha avviato il computer.  

 **Possibile soluzione 1:** nei computer esistenti utilizzare lo strumento Diskpart per compattare l'unità C in modo che si possa creare il volume di sistema. In alcuni casi, tuttavia, lo strumento Diskpart potrebbe non essere in grado di compattare l'unità C a sufficienza per liberare 2 GB di spazio su disco, probabilmente a causa della presenza di spazio frammentato nel disco nell'unità C.  

 Una possibile soluzione per questo problema è deframmentare l'unità C. A tale scopo, procedere come segue:  

1.  Eseguire il comando **shrink querymax** di Diskpart per identificare la quantità massima di spazio su disco che può essere liberata.  

2.  Se il valore restituito al passaggio 1 è inferiore a 2 GB, eliminare dall'unità C tutti i file non necessari e procedere con la deframmentazione.  

3.  Eseguire di nuovo il comando **shrink querymax** di Diskpart per verificare che sia possibile liberare più di 2 GB di spazio del disco.  

4.  Se il valore restituito al passaggio 3 è ancora inferiore a 2 GB, effettuare una delle attività seguenti:  

    -   Deframmentare l'unità C più volte per garantire che lo spazio sia totalmente ottimizzato.  

    -   Eseguire il backup dei dati nell'unità C, eliminare la partizione esistente, creare una nuova partizione e quindi ripristinare i dati nella nuova partizione.  

 **Possibile soluzione 2:** lo script ZTIBDE.wsf esegue lo strumento di preparazione del disco \(bdehdcfg.exe\) e configura la partizione del volume del sistema con una dimensione di 2 GB per impostazione predefinita. Se necessario, l'impostazione predefinita può essere personalizzata all'interno dello script ZTIBDE.wsf. Tuttavia, la modifica degli script di MDT non è un'operazione consigliata.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Supporto per i dischi logici e dinamici  
 **Problema:** durante uno scenario di distribuzione aggiornamento al computer, il processo di distribuzione potrebbe non riuscire se la distribuzione riguarda un computer di destinazione che utilizza unità logiche o dischi dinamici.  

 **Possibile soluzione:** MDT non supporta la distribuzione dei sistemi operativi in unità logiche o dischi dinamici.  

### <a name="domain-join"></a>Associazione del dominio  
 **Problema:** durante la distribuzione si utilizza Distribuzione guidata Windows per fornire tutte le informazioni necessarie sul computer di destinazione, incluse le credenziali, le informazioni per l'aggiunta al dominio e la configurazione con IP statico. Al termine dell'installazione, si nota che il sistema non è stato aggiunto al dominio ed è ancora incluso in un gruppo di lavoro.  

 **Possibile soluzione:** una distribuzione LTI di MDT consente di configurare le informazioni dell'IP statico quando il sistema operativo è in esecuzione. Se il computer di destinazione risiede in un segmento di rete senza protocollo DHCP, l'aggiunta automatica al dominio specificata nel file Unattend.xml ha esito negativo se DHCP non è presente.  

 Configurare Unattend.xml per l'aggiunta a un gruppo di lavoro. Quindi, usare il passaggio della sequenza di attività incorporata **Recover from domain** (Recupera dal dominio) per l'aggiunta al dominio dopo che l'indirizzo IP statico è stato applicato.  

### <a name="driver-installation"></a>Installazione dei driver  
 Per garantire la migliore esperienza utente possibile, l'installazione dei dispositivi hardware e dei driver software deve essere eseguita senza problemi con un intervento minimo o nessun intervento da parte dell'utente. Microsoft mette a disposizione strumenti e linee guida per facilitare la creazione di pacchetti di installazione che soddisfano questo obiettivo. Per informazioni generali sull'installazione dei driver, vedere [Device and Driver Installation](http://www.microsoft.com/whdc/driver/install/default.mspx) (Installazione di dispositivi e driver).  

 Esaminare i problemi e le soluzioni legate all'installazione dei driver di dispositivo:  

-   Problemi che si verificano quando si utilizzano i driver di archiviazione di massa $OEM$ con MDT come descritto in Combinare i driver di archiviazione di massa $OEM$ con logica di archiviazione di massa di MDT  

-   Risoluzione dei problemi di installazione dei driver di dispositivo usando SetupAPI.log come descritto in [Risoluzione dei problemi di installazione dei dispositivi con SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Risoluzione dei problemi di installazione dei dispositivi con SetupAPI.log  
 Il white paper [Troubleshooting Device Installation with the SetupAPI Log File](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) (Risoluzione dei problemi di installazione dei dispositivi con il file SetupAPI.log) fornisce informazioni su come eseguire il debug di installazioni di dispositivi Windows. In particolare, nel documento vengono fornite linee guida per gli sviluppatori e i tester di driver utili interpretare il file di log SetupAPI.  

 Uno dei file di log più utili per le attività di debug è il file SetupAPI.log. Questo file di testo mantiene aggiornate le informazioni che SetupAPI registra in merito all'installazione dei dispositivi, dei service pack e degli aggiornamenti. In particolare, il file tiene traccia delle modifiche ai dispositivi e ai driver, nonché delle principali modifiche apportate al sistema a partire dall'installazione di Windows più recente. Questo documento descrive l'utilizzo del file di log SetupAPI per risolvere i problemi di installazione dei dispositivi, ma non descrive le sezioni del file di log associate all'installazione di service pack e aggiornamenti.  

### <a name="new-computer-deployments"></a>Distribuzioni in nuovi computer  
 Esaminare i problemi e le soluzioni legati agli scenari di distribuzione in nuovi computer:  

-   Problemi di avvio del processo di distribuzione utilizzando Pre\-Boot Execution Environment \(PXE\) come descritto in [Avvio PXE](#PXEBoot)  

####  <a name="PXEBoot"></a> Avvio PXE  
 In breve, il protocollo PXE funziona nel modo seguente: il client avvia il protocollo trasmettendo un pacchetto di individuazione DHCP contenente un'estensione che identifica la richiesta come proveniente da un computer client che implementa il protocollo PXE. Supponendo che sia disponibile un server di avvio che implementa questo protocollo esteso, il server di avvio invia un'offerta che contiene l'indirizzo IP del server che interagirà con il client. Il client usa il Trivial File Transfer Protocol per scaricare il file eseguibile dal server di avvio. Infine, il computer client esegue il programma di avvio automatico scaricato.  

 La fase iniziale di questo protocollo si appoggia a un subset di messaggi DHCP per abilitare il client a individuare un server di avvio, ovvero un server che recapita i file eseguibili per l'installazione di nuovi computer. Il computer client può approfittarne per ottenere un indirizzo IP, il che rappresenta un comportamento previsto ma non necessario per eseguire questa operazione.  

 La seconda fase del protocollo avviene tra il computer client e un server di avvio e utilizza il comodo formato dei messaggi DHCP come forma di comunicazione. Sotto altri aspetti, questa seconda fase non è in alcun modo correlata ai servizi DHCP standard. Le pagine successive descrivono il processo dettagliato per l'inizializzazione del computer client PXE.  

 Per altre informazioni sulla risoluzione dei problemi relativi all'avvio PXE nei Servizi di distribuzione Windows eseguiti in modalità legacy o mista, vedere l'articolo del supporto tecnico Microsoft [Description of PXE Interaction Among PXE Client, DHCP, and RIS Server](http://support.microsoft.com/kb/244036) (Descrizione dell'interazione PXE tra client PXE, DHCP e server RIS).  

 Esaminare le seguenti soluzioni per i problemi di avvio PXE:  

-   Disabilitare la registrazione di Windows PE in SetupAPI.log come descritto in [Disabilitare la registrazione di Windows PE in Servizi di distribuzione Windows](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Assicurarsi che DHCP sia configurato correttamente, come descritto in [Verificare la corretta configurazione di DHCP](#EnsuretheProperDHCPConfiguration).  

-   Migliorare i tempi di risposta per l'assegnazione degli indirizzi IP ai computer client PXE come descritto in [Migliorare i tempi di risposta per l'assegnazione dell'indirizzo IP ai PXE](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Disabilitare la registrazione di Windows PE in Servizi di distribuzione Windows  
 La prima procedura consigliata consiste nell'accertarsi che la registrazione in SetupAPI.log sia stata disabilitata.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Verificare la corretta configurazione di DHCP  
 A seconda dei modelli di router in uso, la configurazione del router per l'inoltro broadcast DHCP potrebbe essere supportata su una subnet, o interfaccia router, o host specifico. Se il server DHCP e il computer che esegue i Servizi di distribuzione Windows sono due computer separati, assicurarsi che i router che inoltrano i broadcast DHCP siano progettati in modo che entrambi i server, DHCP e dei Servizi di distribuzione Windows, ricevano le trasmissioni client; in caso contrario, il computer client non riceverà una risposta alla richiesta di avvio remoto.  

 Tra il computer client e il server dell'installazione remota è presente un router che blocca le richieste o le risposte basate su DHCP? Quando il computer client di Servizi di distribuzione Windows e il server di Servizi di distribuzione Windows si trovano in subnet separate, configurare il router tra i due sistemi in modo che inoltri i pacchetti DHCP al server di Servizi di distribuzione Windows. Questo accorgimento è necessario perché i computer client di Servizi di distribuzione Windows individuino i server di Servizi di distribuzione Windows utilizzando un messaggio broadcast DHCP. Se l'inoltro DHCP non è stato configurato in un router, le trasmissioni DHCP dei computer client non possono raggiungere il server di Servizi di distribuzione Windows. Nei manuali di configurazione dei router, questo processo di inoltro DHCP è talvolta definito *proxy DHCP* oppure *indirizzo di helper IP*. Vedere le istruzioni del router per ottenere ulteriori informazioni sulla configurazione di inoltro DHCP su un router specifico.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Migliorare i tempi di risposta per l'assegnazione dell'indirizzo IP ai PXE  
 Se l'operazione di recupero di un indirizzo IP da parte del computer client PXE richiede molto tempo, 15-20 secondi, controllare gli elementi seguenti:  

-   La scheda di rete nel computer di destinazione e il commutatore o router sono impostati per la stessa velocità, cioè automatica, duplex, completo e così via  

-   L'indirizzo IP per il server di Servizi di distribuzione Windows nel file di helper IP si trova nel router attraverso il quale viene stabilita la connessione? Se l'elenco di indirizzi IP nel file di helper IP è lungo, è possibile spostare in cima l'indirizzo del server di Servizi di distribuzione Windows?  

### <a name="restarting-the-deployment-process"></a>Riavvio del processo di distribuzione  
 **Problema:** durante il test e la risoluzione dei problemi di una sequenza di attività nuova o modificata potrebbe essere necessario riavviare il computer di destinazione in modo che sia possibile riprendere dall'inizio il processo di distribuzione. Potrebbero verificarsi risultati imprevisti perché MDT tiene traccia del proprio stato di avanzamento mediante la scrittura di dati sul disco rigido. Un riavvio del computer di destinazione fa riprendere MDT dal punto in cui si era interrotto.  

 **Possibile soluzione:** per consentire al processo di distribuzione di essere ripreso dall'inizio, eliminare le cartelle C:\\MININT e C:\\\_SMSTaskSequence prima di riavviare il computer di destinazione.  

### <a name="sysprep"></a>Sysprep  
 Esaminare i problemi e le soluzioni legati a Sysprep:  

-   Il computer di destinazione non viene visualizzato nell'unità organizzativa Active Directory Domain Services corretta come descritto in [L'account del computer è nell'unità organizzativa errata](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> L'account del computer è nell'unità organizzativa errata  
 **Problema:** il computer di destinazione viene aggiunto correttamente al dominio, ma l'account del computer non è nell'unità organizzativa corretta.  

 **Possibile soluzione 1:** se per il computer di destinazione esiste un precedente account, l'account rimarrà nell'unità organizzativa originale. Per spostare l'account nell'unità organizzativa specificata, aggiungere un passaggio della sequenza di attività che utilizza uno strumento di automazione, ad esempio Visual Basic® Scripting Edition, per spostare l'account.  

 **Possibile soluzione 2:** verificare che l'unità organizzativa specificata esista e che sia nel formato corretto. Il formato corretto dell'unità organizzativa deve essere `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Configuration Manager  
 **Problema:** il messaggio di errore visualizzato nella REF \_Ref308174600 \\h Figura 3 viene visualizzato quando si tenta di creare un punto di servizio PXE di Configuration Manager usando l'opzione **Crea certificato autofirmato PXE**.  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
Figura SEQ Figura \\\* ARABO 3. Errore del punto di servizio PXE  

 \*Figura SEQ Figura **\\ ARABO 3. Errore del punto di servizio PXE**  

 **Possibile soluzione:** se nel server che si sta configurando esisteva già un punto di servizio PXE, è possibile che il punto di servizio PXE non abbia eliminato i certificati autocreati quando è stato disinstallato. Eliminare la cartella dei certificati PXE in C:\\Documents and Settings\\*nome\_utente*\\Application Data\\Microsoft\\Crypto\\RSA dove *nome\_utente* è il nome dell'utente che esegue la configurazione corrente o che ha eseguito la configurazione precedente. Dopo l'eliminazione della cartella, la creazione guidata del nuovo ruolo del sito nella console di Configuration Manager verrà completata correttamente.  

### <a name="task-sequences"></a>Sequenze di attività  
 Esaminare i problemi e le soluzioni legati alla sequenza di attività:  

-   La sequenza di attività non viene completata correttamente o presenta un comportamento imprevedibile, come descritto in [La sequenza di attività non viene completata correttamente](#TaskSequenceDoesNotFinishSuccessfully).  

-   In LTI le sequenze di attività OEM \(Original Equipment Manufacturer\) sono elencate nelle immagini di avvio con l'architettura del processore opposta, come descritto in [La sequenza di attività OEM per un'immagine di avvio creata per un'architettura del processore diversa viene visualizzata erroneamente](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   Distribuzione guidata Windows visualizza il messaggio di errore “Bad Task Sequence Item \(Invalid OS GUID\)” (Elemento sequenza di attività non valido - GUID del sistema operativo non valido) come descritto in [Messaggio Bad Task Sequence Item (Invalid OS GUID) (Elemento della sequenza di attività non valido - GUID del sistema operativo non valido) nella Distribuzione guidata Windows](#BadTaskSequenceItem).  

-   Quando si configura un nome per la connessione di rete, viene visualizzato il messaggio “Please enter a valid name for the network adapter” (Immettere un nome valido per la scheda di rete) come descritto in [Applica impostazioni di rete](#ApplyNetworkSettings).  

-   Problemi che possono verificarsi in seguito alla configurazione non corretta delle impostazioni di Continua in caso di errore nei passaggi della sequenza attività come descritto in [Usare Continua in caso di errore](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> La sequenza di attività non viene completata correttamente  
 **Problema:** la sequenza di attività non viene completata correttamente o presenta un comportamento imprevedibile.  

 **Possibile soluzione:** il passaggio della sequenza di attività **Installa sistema operativo** \(per LTI\) o il passaggio della sequenza di attività **Applica immagine del sistema operativo** \(per UDI e ZTI \) potrebbero essere stati modificati dopo la creazione del passaggio della sequenza di attività e causare risultati imprevisti. Ad esempio, se è stata creata una sequenza di attività per distribuire un'immagine Windows 8.1 a 32 bit e successivamente il passaggio della sequenza di attività **Installa sistema operativo** o il passaggio della sequenza di attività **Applica immagine del sistema operativo** è stato modificato per fare riferimento a un'immagine Windows 8.1 a 64 bit, la sequenza di attività potrebbe non essere eseguita correttamente.  

 È consigliabile creare una nuova sequenza di attività per distribuire un'immagine del sistema operativo diversa.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> La sequenza di attività OEM per un'immagine di avvio creata per un'architettura del processore diversa viene visualizzata erroneamente  
 **Problema:** viene visualizzata una sequenza di attività basata su un modello di sequenza di attività OEM LTI per un'immagine di avvio con un'architettura del processore diversa. Ad esempio, una sequenza di attività OEM che distribuisce un sistema operativo a 64 bit viene visualizzata in un'immagine di avvio a 32 bit.  

 **Possibile soluzione:** tale comportamento è normale in quanto le sequenze di attività OEM in LTI non sono considerate come specifiche per una data piattaforma e vengono sempre elencate, indipendentemente dall'architettura del processore dell'immagine di avvio.  

####  <a name="BadTaskSequenceItem"></a>Messaggio Bad Task Sequence Item \(Invalid OS GUID\) (Elemento della sequenza di attività non valido - GUID del sistema operativo non valido) nella Distribuzione guidata Windows  
 **Problema:** quando si esegue Distribuzione guidata Windows, la procedura guidata visualizza il messaggio di errore “Bad Task Sequence Item \(Invalid OS GUID\)” (Elemento della sequenza di attività non valido - GUID del sistema operativo non valido). Il sistema operativo è riportato nel file OperatingSystem.xml, tuttavia il sistema operativo non è visualizzato nella Deployment Workbench.  

 **Possibile soluzione:** l'origine del sistema operativo originale è associata a due o più file WIM. Una SKU associata a una sequenza di attività è stata eliminata, tuttavia, altre SKU dell'origine del sistema operativo sono ancora presenti. Quando la sequenza di attività che fa riferimento alla SKU eliminata è selezionata nella pagina **Select a task sequence to execute on this computer** (Seleziona una sequenza di attività da eseguire nel computer) della Distribuzione guidata Windows, viene visualizzato il messaggio di errore “Bad Task Sequence Item \(Invalid OS GUID\)" (Elemento della sequenza di attività non valido - GUID del sistema operativo non valido) quando si fa clic sul pulsante **Avanti** nella pagina della procedura guidata.  

 Per risolvere questo problema, eseguire una delle operazioni seguenti:  

-   Rimuovere tutte le SKU dall'origine del sistema operativo. Distribuzione guidata Windows si comporta normalmente e il messaggio di errore non viene visualizzato.  

-   Modificare la sequenza di attività per utilizzare un'immagine del sistema operativo diversa.  

####  <a name="ApplyNetworkSettings"></a> Applica impostazioni di rete  
 **Problema:** quando si configura il nome di connessione di rete in Deployment Workbench, un errore di convalida visualizza il messaggio “Please enter a valid name for the network adapter” (Immettere un nome valido per la scheda di rete).  

 **Possibile soluzione:** rimuovere eventuali spazi e caratteri non validi dal nome della connessione specificata.  

####  <a name="UseContinueonError"></a> Usare Continua in caso di errore  
 Se una sequenza di attività di MDT è configurata per non continuare in caso di errore e tale sequenza di attività restituisce un errore, tutte le sequenze di attività rimanenti di tale gruppo vengono ignorate. Tuttavia, i gruppi di sequenze di attività rimanenti vengono elaborati. Considerare quanto segue:  

 Sono stati creati due gruppi di sequenze di attività e un gruppo contiene più di un passaggio della sequenza di attività:  

-   Gruppo A  

    -   Passaggio A  

    -   Passaggio B  

-   Gruppo B  

    -   Passaggio A  

    -   Passaggio B  

 Se il passaggio A del gruppo A è configurato per non continuare in caso di errore, il passaggio B del gruppo A non verrà elaborato. Tuttavia, tutti i passaggi della sequenza di attività del gruppo B verranno elaborati.  

### <a name="the-user-state-migration-tool"></a>Utilità di migrazione stato utente  
 Esaminare i problemi e le soluzioni legati a USMT:  

-   I collegamenti che puntano a documenti archiviati in cartelle condivise in rete non sono ripristinati correttamente come descritto in [Collegamenti non presenti nel desktop](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Collegamenti non presenti nel desktop  
 **Problema:** quando si utilizza USMT per eseguire la migrazione dei dati utente, è possibile che i collegamenti che puntano a documenti di rete non possano essere ripristinati. I collegamenti vengono acquisiti durante Scanstate ma non vengono mai ripristinati nel computer di destinazione durante Loadstate.  

 **Possibile soluzione:** modificare il file MigUser.xml e commentare la riga seguente:  

 Riga originale:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Riga modificata:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>File di formato Windows Imaging  
 Esaminare i problemi e le soluzioni legati a WIM:  

-   Le distribuzioni LTI e ZTI hanno esito negativo registrando errori legati al file WIM nel file BDD.log come descritto in [File WIM danneggiato](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> File WIM danneggiato  
 **Problema:** quando si distribuisce un'immagine, la distribuzione ha esito negativo registrando le seguenti voci nel file BDD.log:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Esaminare il problema montando il file WIM usando i risultati ImageX nel messaggio di errore “I dati sono validi”. Ulteriori indagini dimostrano che l'indicatore di data del file WIM è di molti anni anteriore alla data attuale. È possibile che un altro processo, ad esempio un software antivirus, abbia tenuto aperto il file WIM dopo che era stato precedentemente chiuso al termine di un processo di lettura o scrittura.  

 **Possibile soluzione:** ripristinare il file WIM dai supporti di backup.  

### <a name="windows-pe"></a>Windows PE  
 Esaminare i problemi e le soluzioni legate a Windows PE:  

-   Il processo di distribuzione LTI o ZTI non è stato avviato a causa di RAM insufficiente o della presenza di schede di rete wireless come descritto in [Processo di distribuzione non avviato: RAM insufficiente o scheda di rete wireless](#LimitedRamorWirelessNetworkAdapter).  

-   Il processo di distribuzione LTI o ZTI non è stato avviato a causa della mancanza di componenti di Windows PE, come descritto in [Processo di distribuzione non avviato: componenti mancanti](#MissingComponents).  

-   Il processo di distribuzione LTI o ZTI non è stato avviato a causa di driver dispositivo mancanti o non corretti, come descritto in [Processo di distribuzione non avviato: driver mancanti o non corretti](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Processo di distribuzione non avviato: RAM insufficiente o scheda di rete wireless  
 **Problema:** durante la distribuzione di un'immagine in determinati computer di destinazione, Windows PE viene avviato, esegue **wpeinit**, apre una finestra del prompt dei comandi, ma non avvia davvero il processo di distribuzione. Se si tenta di risolvere il problema eseguendo il mapping di un'unità di rete dal computer di destinazione, si scopre che i driver della scheda di rete non sono caricati.  

 **Possibile soluzione 1:** la Distribuzione guidata non viene avviata perché la RAM è insufficiente. Verificare che il computer di destinazione disponga di almeno 512 MB di RAM e che non vi sia memoria video condivisa che utilizza più di 64 MB dei 512 MB.  

 Le versioni di Windows PE che MDT supporta non possono essere eseguite in un computer di destinazione che dispone di meno di 512 MB di RAM.  

 **Possibile soluzione 2:** non includere i driver wireless nell'immagine Windows PE.  

####  <a name="MissingComponents"></a> Processo di distribuzione non avviato: componenti mancanti  
 **Problema:** durante la risoluzione dei problemi di una distribuzione non riuscita, si trova la voce seguente nel file BDD.log:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Possibile soluzione:** questo errore può indicare che l'immagine Windows PE non è stata creata usando MDT. Se si utilizza Configuration Manager, non utilizzare una delle immagini di Windows PE create da Configuration Manager. Creare un'immagine utilizzando la procedura guidata Import Microsoft Deployment Task Sequence.  

> [!NOTE]
>  Le immagini di Windows PE che Configuration Manager crea contengono componenti che supportano script, XML e Strumentazione gestione Windows (WMI), ma non contengono componenti che supportano Microsoft ActiveX® Data Objects (ADO).  

####  <a name="MissingorIncorrectDrivers"></a> Processo di distribuzione non avviato: driver mancanti o non corretti  
 **Problema:** durante la distribuzione in determinati computer di destinazione, Windows PE viene avviato, esegue **wpeinit**, apre una finestra del prompt dei comandi, ma non avvia davvero il processo di distribuzione. Se si tenta di risolvere il problema eseguendo il mapping di un'unità di rete dal computer di destinazione, si scopre che i driver della scheda di rete non sono caricati. Un esame del file SetupAPI.log che si in trova *X*:\Windows\System32\Inf indica che Windows PE genera un errore quando sta configurando la scheda di rete. Un possibile errore è “This driver is not meant for this platform” (Questo driver non è destinato a questa piattaforma). I driver nell'elenco **Out-of-Box Drivers** sono stati inseriti nell'immagine.  

 **Possibile soluzione:** è possibile che sia presente un conflitto tra i driver di Windows PE e un altro driver. Quando si configurano le impostazioni per l'immagine Windows PE nel Deployment Workbench, creare un gruppo di driver di Windows PE che contiene solo i driver di archiviazione e della scheda di rete e quindi configurare la condivisione di distribuzione affinché utilizzi solo il gruppo di driver di Windows PE.  

## <a name="deployment-process-flow-charts"></a>Diagrammi di flusso del processo di distribuzione  
 In questa sezione vengono proposti due set di diagrammi di flusso MDT: uno per le distribuzioni LTI e uno per le distribuzioni ZTI con Configuration Manager. Ogni diagramma di flusso illustra le attività eseguite durante quel tipo di distribuzione.  

 Acquisire familiarità con i grafici di flusso del processo di distribuzione nei modi seguenti:  

-   Esaminando i diagrammi di flusso del processo di distribuzione LTI come descritto in [Diagrammi di flusso del processo di distribuzione LTI](#LTIDeploymentProcessFlowcharts)  

-   Esaminando i diagrammi di flusso del processo di distribuzione ZTI come descritto in [Diagrammi di flusso del processo di distribuzione ZTI](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Diagrammi di flusso del processo di distribuzione LTI  
 I diagrammi di flusso vengono forniti per le fasi seguenti:  

-   Convalida (Figura 4)  

-   Acquisizione dello stato (Figura 5 e Figura 6)  

-   Preinstallazione (Figura 7, Figura 8 e Figura 9)  

-   Installazione (Figura 10)  

-   Postinstallazione (Figura 11 e Figura 12)  

-   Ripristino dello stato (Figura 13, Figura 14, Figura 15 e Figura 16)  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
Figura 4. Diagramma di flusso per la fase di convalida  

 **Figura 4. Diagramma di flusso per la fase di convalida**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
Figura 5. Diagramma di flusso per la fase di acquisizione dello stato (1 di 2)  

 **Figura 5. Diagramma di flusso per la fase di acquisizione dello stato (1 di 2)**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
Figura 6. Diagramma di flusso per la fase di acquisizione dello stato (2 di 2)  

 **Figura 6. Diagramma di flusso per la fase di acquisizione dello stato (2 di 2)**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
Figura 7. Diagramma di flusso per la fase di preinstallazione (1 di 3)  

 **Figura 7. Diagramma di flusso per la fase di preinstallazione (1 di 3)**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
Figura 8. Diagramma di flusso per la fase di preinstallazione (2 di 3)  

 **Figura 8. Diagramma di flusso per la fase di preinstallazione (2 di 3)**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
Figura 9. Diagramma di flusso per la fase di preinstallazione (3 di 3)  

 **Figura 9. Diagramma di flusso per la fase di preinstallazione (3 di 3)**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
Figura 10. Diagramma di flusso per la fase di installazione  

 **Figura 10. Diagramma di flusso per la fase di installazione**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
Figura 11. Diagramma di flusso per la fase di postinstallazione (1 di 2)  

 **Figura 11. Diagramma di flusso per la fase di postinstallazione (1 di 2)**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
Figura 12 Diagramma di flusso per la fase di postinstallazione (2 di 2)  

 **Figura 12 Diagramma di flusso per la fase di postinstallazione (2 di 2)**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
Figura 13. Diagramma di flusso per la fase di ripristino dello stato (1 di 4)  

 **Figura 13. Diagramma di flusso per la fase di ripristino dello stato (1 di 4)**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
Figura 14. Diagramma di flusso per la fase di ripristino dello stato (2 di 4)  

 **Figura 14. Diagramma di flusso per la fase di ripristino dello stato (2 di 4)**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
Figura 15. Diagramma di flusso per la fase di ripristino dello stato (3 di 4)  

 **Figura 15. Diagramma di flusso per la fase di ripristino dello stato (3 di 4)**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
Figura 16. Diagramma di flusso per la fase di ripristino dello stato (4 di 4)  

 **Figura 16. Diagramma di flusso per la fase di ripristino dello stato (4 di 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Diagrammi di flusso del processo del processo di distribuzione ZTI  
 I diagrammi di flusso vengono forniti per le seguenti fasi della distribuzione ZTI con Configuration Manager:  

-   Inizializzazione (Figura 17)  

-   Convalida (Figura 18)  

-   Acquisizione stato (Figura 19)  

-   Preinstallazione (Figura 20)  

-   Installazione (Figura 21)  

-   Postinstallazione (Figura 22)  

-   Ripristino dello stato (Figura 23 e Figura 24)  

-   Acquisizione (Figura 25)  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
Figura 17. Diagramma di flusso per la fase di inizializzazione  

 **Figura 17. Diagramma di flusso per la fase di inizializzazione**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
Figura 18. Diagramma di flusso per la fase di convalida  

 **Figura 18. Diagramma di flusso per la fase di convalida**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
Figura 19. Diagramma di flusso per la fase di acquisizione dello stato  

 **Figura 19. Diagramma di flusso per la fase di acquisizione dello stato**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
Figura 20. Diagramma di flusso per la fase di preinstallazione  

 **Figura 20. Diagramma di flusso per la fase di preinstallazione**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
Figura 21. Diagramma di flusso per la fase di installazione  

 **Figura 21. Diagramma di flusso per la fase di installazione**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
Figura 22. Diagramma di flusso per la fase di postinstallazione  

 **Figura 22. Diagramma di flusso per la fase di postinstallazione**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
Figura 23. Diagramma di flusso per la fase di ripristino dello stato (1 di 2)  

 **Figura 23. Diagramma di flusso per la fase di ripristino dello stato (1 di 2)**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
Figura 24. Diagramma di flusso per la fase di ripristino dello stato (2 di 2)  

 **Figura 24. Diagramma di flusso per la fase di ripristino dello stato (2 di 2)**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
Figura 25. Diagramma di flusso per la fase di acquisizione dello stato  

 **Figura 25. Diagramma di flusso per la fase di acquisizione dello stato**  

## <a name="finding-additional-help"></a>Informazioni aggiuntive  
 È possibile reperire informazioni aggiuntive sulla risoluzione dei problemi di distribuzione di MDT nei modi seguenti:  

-   Contattando il supporto tecnico Microsoft, come descritto in [Supporto tecnico Microsoft](#MicrosoftSupport)  

-   Consultando i blog e altre risorse Internet come descritto in [Supporto Internet](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Supporto tecnico Microsoft  
 Microsoft fornisce supporto di livello Premier e professionale per il Microsoft Deployment Toolkit.  

 Supporto di livello professionale: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Supporto di livello Premier: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Quando si contatta il supporto, specificare che il problema riguarda MDT e indicare la versione esatta.  

###  <a name="InternetSupport"></a> Supporto Internet  
 Molte fonti online forniscono ulteriori informazioni sulla risoluzione dei problemi per MDT oltre a quelle illustrate in questo riferimento. Queste fonti online includono:  

-   Blog ospitati da Microsoft  

    -   [Blog del team MDT](http://blogs.technet.com/b/msdeployment/)  

    -   [Blog del team di Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blog di Michael Niehaus](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus scrive sulla distribuzione di Windows e Microsoft Office).  

-   Newsgroup e forum ospitati da Microsoft:  

     I seguenti newsgroup e forum offrono supporto da parte di dipendenti Microsoft, peer del settore e MVP:  

    -   [Configuration Manager: distribuzione del sistema operativo](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Installazione, configurazione e distribuzione di Windows 8](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Fonti di informazioni relative alle distribuzioni esterne a Microsoft:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
