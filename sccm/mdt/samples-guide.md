---
title: Esempi di MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Esempi di Microsoft Deployment Toolkit. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915973"
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Guida agli esempi di Microsoft Deployment Toolkit  
 Questa guida fa parte di Microsoft® Deployment Toolkit (MDT) 2013 ed è destinata ai team specializzati che eseguono la distribuzione dei sistemi operativi Windows e di Microsoft Office. In particolare, la guida offre esempi di impostazioni di configurazione per scenari di distribuzione specifici.  

> [!NOTE]
>  In questo documento *Windows* si riferisce ai sistemi operativi Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2, se non diversamente specificato. MDT non supporta le versioni di Windows basate su processore ARM. Analogamente, *MDT* fa riferimento a MDT 2013 se non diversamente specificato.  

 **Per usare questa guida**  

 Esaminare l'elenco degli scenari nel sommario.  

1.  Selezionare lo scenario che meglio rappresenta gli obiettivi di distribuzione dell'organizzazione.  

2.  Verificare le impostazioni di configurazione di esempio per lo scenario selezionato.  

3.  Usare le impostazioni di configurazione di esempio come base per le impostazioni di configurazione nel proprio ambiente.  

4.  Personalizzare le impostazioni di configurazione di esempio per l'ambiente.  

 In molti casi può essere necessario completare le impostazioni di configurazione per l'ambiente per più di uno scenario.  

 Poiché questa guida contiene solo le impostazioni di configurazione di esempio, consultare le guide elencate nella tabella seguente può essere utile per personalizzare le impostazioni di configurazione nell'ambiente.  

 |Guida|Questa guida offre assistenza per|  
 |-|-|  
 |*Guida introduttiva per Microsoft System Center 2012 R2 Configuration Manager* |Usare System Center 2012 R2 Configuration Manager per installare il sistema operativo Windows 8.1 in uno scenario di distribuzione di tipo Nuovo computer.|  
 |*Guida introduttiva per l'installazione Lite Touch* |Installare il sistema operativo Windows 8.1 con Lite Touch Installation (LTI) usando i supporti di avvio in uno scenario di distribuzione di tipo Nuovo computer.|  
 |*Guida introduttiva per l'installazione guidata dall'utente* |Installare il sistema operativo Windows 8.1 con l'installazione guidata dall'utente e System Center 2012 R2 Configuration Manager in uno scenario di distribuzione di tipo Nuovo computer.|  
 |*Uso di Microsoft Deployment Toolkit* |Personalizzare ulteriormente i file di configurazione usati nelle distribuzioni con Zero Touch Installation (ZTI) e Light Touch Installation (LTI). Questa guida include anche informazioni generiche sulla configurazione e un riferimento tecnico per le impostazioni di configurazione.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Distribuzione di applicazioni Windows 8 con MDT  
 MDT è in grado di distribuire pacchetti di applicazioni Windows 8 con estensione APPX. Questi pacchetti di applicazioni sono una novità in Windows 8. Per altre informazioni su queste applicazioni, vedere la pagina relativa allo [sviluppo di applicazioni Windows Store.](http://msdn.microsoft.com/windows/apps)  

 Per distribuire le applicazioni Windows 8 usando MDT, attenersi alla procedura seguente:  

-   Distribuire le applicazioni Windows 8 usando l'installazione Light Touch come descritto in [Distribuzione di applicazioni Windows 8 con LTI](#DeployWin8LTI).  

-   Distribuire le applicazioni Windows 8 usando l'installazione guidata dall'utente (UDI, User-Driven Installation) come descritto in [Distribuzione di applicazioni Windows 8 con UDI](#DeployWin8UDI).  

###  <a name="DeployWin8LTI"></a> Distribuzione di applicazioni Windows 8 con LTI  
 È possibile distribuire le applicazioni Windows 8 usando LTI come qualsiasi altra applicazione che avvia il processo di installazione dalla riga di comando. È possibile aggiungere le applicazioni Windows 8 alle distribuzioni LTI nel nodo Applicazioni di Deployment Workbench.  

 **Per distribuire un'applicazione Windows 8 con LTI**  

1.  Creare una cartella di rete condivisa in cui archiviare l'applicazione.  

2.  Copiare l'applicazione Windows 8 nella cartella di rete condivisa creata nel passaggio precedente.  

     Assicurarsi di copiare il file APPX dell'applicazione Windows 8 e gli altri file necessari, ad esempio un file CER che contiene il certificato dell'applicazione.  

3.  Creare un elemento dell'applicazione LTI per l'applicazione Windows 8 nel nodo Applicazioni di Deployment Workbench usando la Creazione guidata nuova applicazione.  

     Mentre si esegue la Creazione guidata nuova applicazione, nella pagina dei **dettagli del comando** della procedura guidata, in **Riga di comando** digitare **nome_file_app** (dove *nome_file_app* è il nome dell'applicazione Windows 8).  

     Per altre informazioni su come completare la Creazione guidata nuova applicazione in Deployment Workbench, vedere le sezioni del documento *Uso di Microsoft Deployment Toolkit* relative agli argomenti seguenti:  

    -   Creazione di una nuova applicazione distribuita dalla condivisione di distribuzione  

    -   Creazione di una nuova applicazione distribuita da un'altra cartella condivisa della rete  

4.  Selezionare l'elemento dell'applicazione LTI creato nel passaggio precedente in una sequenza di attività LTI.  

###  <a name="DeployWin8UDI"></a> Distribuzione di applicazioni Windows 8 con UDI  
 È possibile distribuire le applicazioni Windows 8 usando UDI come qualsiasi altra applicazione che avvia il processo di installazione dalla riga di comando. È possibile aggiungere le applicazioni Windows 8 alle distribuzioni UDI nella pagina **ApplicationPage** della procedura guidata in UDI Wizard Designer.  

> [!NOTE]
>  La distribuzione di Windows 8 e delle applicazioni Windows 8 con UDI richiede System Center 2012 R2 Configuration Manager.  

 **Per distribuire un'applicazione Windows 8 con UDI**  

1.  Creare una cartella di rete condivisa in cui archiviare l'applicazione.  

     Questa cartella sarà la cartella di origine per l'applicazione di Configuration Manager creata in una fase successiva del processo.  

2.  Copiare l'applicazione Windows 8 nella cartella di rete condivisa creata nel passaggio precedente.  

     Assicurarsi di copiare il file APPX dell'applicazione Windows 8 e gli altri file necessari, ad esempio un file CER che contiene il certificato dell'applicazione.  

3.  Aggiungere l'applicazione Windows 8 come applicazione di Configuration Manager  

4.  Creare un elemento dell'applicazione di Configuration Manager per l'applicazione Windows 8 usando la Creazione guidata nuova applicazione nella console di Configuration Manager.  

     Durante il completamento della Creazione guidata nuova applicazione creare un tipo di distribuzione per distribuire l'applicazione Windows 8 usando la Creazione guidata tipo di distribuzione. Nella pagina **contenuto** della Creazione guidata tipo di distribuzione per il **programma di installazione** digitare **nome_file_app** (dove *nome_file_app* è il nome dell'applicazione Windows 8).  

     Per altre informazioni su come completare la Creazione guidata nuova applicazione nella console di Configuration Manager, vedere le sezioni seguenti nella libreria della documentazione per System Center 2012 Configuration Manager, acclusa a Configuration Manager:  

    -   [Come creare applicazioni in Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Come creare tipi di distribuzione in Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Come gestire le applicazioni e tipi di distribuzione di Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Verificare che la funzionalità di affinità utente-dispositivo di Configuration Manager sia configurata correttamente per supportare l'affinità tra utenti e dispositivi per la distribuzione delle applicazioni di Configuration Manager.  

     Per altre informazioni sulla configurazione dell'affinità utente-dispositivo a supporto della distribuzione delle applicazioni di Configuration Manager, vedere [Come gestire l'affinità utente dispositivo in Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Distribuire l'applicazione creata nel passaggio 4 agli utenti designati.  

     Per altre informazioni su come distribuire un'applicazione agli utenti, vedere [Come distribuire le applicazioni in Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Configurare la pagina **ApplicationPage** della procedura guidata in modo da includere l'applicazione di Configuration Manager creata nel passaggio 4 con UDI Wizard Designer.  

     Per altre informazioni su come configurare la pagina **ApplicationPage** della procedura guidata usando UDI Wizard Designer, vedere il passaggio 5-11 relativo alla personalizzazione del file di configurazione della procedura guidata UDI per il computer di destinazione nel documento di MDT *Guida introduttiva per l'installazione guidata dall'utente*.  

8.  Selezionare l'elemento dell'applicazione UDI creato nel passaggio precedente in una sequenza di attività UDI.  

    > [!NOTE]
    >  L'applicazione Windows 8 non viene istallata dalla sequenza di attività ma verrà installata la prima volta che l'utente accede al computer di destinazione, come definito dall'impostazione UDA configurata nel passaggio 5, usando il programma di installazione delle app incentrata sull'utente (AppInstall.exe) in UDI.  

     Per altre informazioni sulla funzionalità di programma di installazione di App incentrata sugli utenti in UDI, vedere la sezione relativa al programma di installazione delle app incentrata sull'utente nel documento di MDT *Informazioni di riferimento sul toolkit*.  

## <a name="managing-mdt-using-windows-powershell"></a>Gestione di MDT con Windows PowerShell  
 È possibile gestire condivisioni di distribuzione MDT usando Deployment Workbench e Windows PowerShell. MDT include uno snap-in di Windows PowerShell™, Microsoft.BDD.SnapIn, che deve essere caricato prima di usare le funzionalità specifiche di MDT in Windows PowerShell. Lo snap-in MDT di Windows PowerShell include:  

-   Un provider di Windows PowerShell, MDTProvider, che consente di accedere al contenuto di una condivisione di distribuzione  

-   Cmdlet che consentono di amministrare le condivisioni di distribuzione MDT  

 Gestire le condivisioni di distribuzione MDT con Windows PowerShell attenendosi alla procedura seguente:  

-   Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

-   Creare una condivisione di distribuzione usando Windows PowerShell come descritto in [Creazione di una condivisione di distribuzione con Windows PowerShell](#CreateDeployShare).  

-   Visualizzare le proprietà della condivisione di distribuzione usando Windows PowerShell come descritto in [Visualizzazione delle proprietà della condivisione di distribuzione con Windows PowerShell](#ViewDeployShareProp).  

-   Visualizzare l'elenco delle condivisioni di distribuzione usando Windows PowerShell come descritto in [Visualizzazione dell'elenco di condivisioni di distribuzione con Windows PowerShell](#ViewListDeployShare).  

-   Aggiornare una condivisione di distribuzione, che genera nuove immagini di avvio di Ambiente preinstallazione di Windows (Windows PE), come descritto in [Aggiornamento di una condivisione di distribuzione con Windows PowerShell](#UpdateDeployShare).  

-   Aggiornare una condivisione di distribuzione collegata, che replica il contenuto di una condivisione di distribuzione nella condivisione di distribuzione collegata, come descritto in [Aggiornamento di una condivisione di distribuzione collegata con Windows PowerShell](#UpdateLinkedDeployShare).  

-   Aggiornare i supporti di distribuzione, che replicano il contenuto di una condivisione di distribuzione nei supporti di distribuzione e quindi genera nuove immagini di avvio come descritto in [Aggiornamento dei supporti di distribuzione con Windows PowerShell](#UpdateDeployMedia).  

-   Gestire gli elementi in una condivisione di distribuzione, ad esempio sistemi operativi, pacchetti del sistema operativo, applicazioni e driver di dispositivo, come descritto in [Gestione di elementi in una condivisione di distribuzione con Windows PowerShell](#ManageItemDeployShare).  

-   Automatizzare il popolamento degli elementi in una condivisione di distribuzione, ad esempio sistemi operativi, pacchetti del sistema operativo, applicazioni e driver di dispositivo, come descritto in [Automazione del popolamento di una condivisione di distribuzione](#AutomatePopulateDeployShare).  

-   Gestire le cartelle in una condivisione di distribuzione usando Windows PowerShell come descritto in [Gestione delle cartelle di una condivisione di distribuzione con Windows PowerShell](#ManageDeployShareFolder).  

###  <a name="LoadMDTSnapIn"></a> Caricamento dello snap-in MDT di Windows PowerShell  
 I cmdlet di MDT sono disponibili in uno snap-in di Windows PowerShell, **Microsoft.BDD.SnapIn**, che deve essere caricato prima di usare i cmdlet di MDT. È possibile caricare lo snap-in MDT di Windows PowerShell usando uno dei metodi seguenti:  

-   Caricare lo snap-in MDT di Windows PowerShell usando la console dei moduli di Windows PowerShell come descritto in [Caricare lo snap-in MDT di Windows PowerShell usando l'attività Importa moduli di sistema](#LoadMDTSnapInImport).  

-   Caricare lo snap-in MDT di Windows PowerShell usando il cmdlet **Add-PSSnapIn** come descritto in [Caricare lo snap-in MDT di Windows PowerShell usando il cmdlet Add-PSSnapIn](#LoadMDTSnapInCmdlet).  

####  <a name="LoadMDTSnapInImport"></a> Caricare lo snap-in MDT di Windows PowerShell usando l'attività Importa moduli di sistema  
 L'attività Importa moduli di sistema include automaticamente tutti i moduli e gli snap-in di Windows PowerShell inclusi nei moduli presenti nella directory %Windir%\System32\WindowsPowerShell\1.0\Modules. MDT installa automaticamente lo snap-in MDT di Windows PowerShell **Microsoft.BDD.SnapIn** in tale cartella durante il processo di installazione di MDT.  

> [!NOTE]
>  L'attività Importa moduli di sistema è disponibile solo in Windows 7 e Windows Server 2008 R2 se Windows PowerShell 3.0 non è installato nel computer. A partire da Windows PowerShell 3.0, i moduli vengono importati automaticamente la prima volta che si usa un cmdlet nel modulo.  

 È possibile avviare una console di Windows PowerShell con l'attività Importa moduli di sistema effettuando una delle procedure riportate di seguito:  

-   Nella barra delle applicazioni fare clic con il pulsante destro del mouse sull'icona di **Windows PowerShell** e quindi fare clic su **Importa moduli di sistema**.  

-   Fare clic su **Start**, scegliere **Strumenti di amministrazione** e quindi fare clic su **Moduli di Windows PowerShell**.  

 Per altre informazioni sull'avvio di una console di Windows PowerShell con Importa moduli di sistema, vedere le istruzioni per l'[avvio di Windows PowerShell con l'importazione dei moduli di sistema](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Caricare lo snap-in MDT di Windows PowerShell usando il cmdlet Add-PSSnapIn  
 È possibile caricare lo snap-in MDT di Windows PowerShell **Microsoft.BDD.PSSnapIn** da qualsiasi ambiente di Windows PowerShell usando il cmdlet [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx), come illustrato nell'esempio seguente:  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Creazione di una condivisione di distribuzione con Windows PowerShell  
 È possibile creare condivisioni di distribuzione usando i cmdlet MDT di Windows PowerShell. La cartella radice per la condivisione di distribuzione viene creata e condivisa usando i cmdlet standard di Windows PowerShell e le chiamate ai comandi della classe Strumentazione gestione Windows (WMI). La condivisione di distribuzione viene popolata usando il provider MDTProvider Windows PowerShell e il cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx). L'unità Windows PowerShell MDTProvider viene resa persistente usando il cmdlet **Add-MDTPersistentDrive**.  

 **Per preparare una condivisione di distribuzione usando i cmdlet MDT di Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Creare la cartella che sarà la radice della nuova condivisione di distribuzione usando il cmdlet **New-Item**, come illustrato nell'esempio seguente e descritto nell'argomento relativo all'[uso del cmdlet New-Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     Il cmdlet visualizza l'esito positivo della creazione della cartella.  

3.  Condividere la cartella creata nel passaggio precedente usando la classe **WMI win32_share** come indicato nell'esempio seguente:  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     La chiamata alla classe **win32_share** restituisce i risultati della chiamata. Se il valore di **ReturnValue** è zero (0), la chiamata è riuscita.  

4.  Specificare la nuova cartella condivisa come condivisione di distribuzione usando il cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx), come illustrato nell'esempio seguente:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     Il cmdlet avvia automaticamente la creazione della condivisione di distribuzione e copia le informazioni del modello nella nuova condivisione di distribuzione. Al termine del processo di copia, il cmdlet visualizza le informazioni relative alla nuova condivisione di distribuzione.  

    > [!NOTE]
    >  Il valore specificato nel parametro *Name* (DS002) deve essere univoco e non può essere uguale a quello dell'unità Windows PowerShell di una condivisione di distribuzione esistente.  

5.  Verificare che per la condivisione di distribuzione siano state create le cartelle appropriate usando il comando **dir**, come illustrato nell'esempio seguente:  

    ```  
    dir ds002:  
    ```  

     Viene visualizzato l'elenco delle cartelle predefinite presenti nella radice della condivisione di distribuzione.  

6.  Aggiungere la nuova condivisione di distribuzione all'elenco delle condivisioni di distribuzione MDT persistenti usando il cmdlet **Add-MDTPersistentDrive** indicato nell'esempio seguente:  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     In questo esempio la variabile *$NewDS* viene usata per passare l'oggetto unità Windows PowerShell per la nuova condivisione di distribuzione al cmdlet.  

     In alternativa, è possibile combinare i cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) e **Add-MDTPersistentDrive**, come indicato nell'esempio che segue:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     Nell'esempio precedente la pipeline di Windows PowerShell specifica entrambi i parametri *Name* e *InputObject*.  

###  <a name="ViewDeployShareProp"></a> Visualizzazione delle proprietà della condivisione di distribuzione con Windows PowerShell  
 È possibile visualizzare le proprietà delle condivisioni di distribuzione MDT usando il cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) e il provider MDTProvider Windows PowerShell. Le stesse proprietà si possono visualizzare anche in Deployment Workbench.  

 **Per visualizzare le proprietà della condivisione di distribuzione usando i cmdlet MDT di Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Visualizzare le proprietà della condivisione di distribuzione usando il cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), come illustrato nell'esempio seguente:  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3. Il cmdlet restituisce le proprietà per la condivisione di distribuzione.  

###  <a name="ViewListDeployShare"></a> Visualizzazione dell'elenco di condivisioni di distribuzione con Windows PowerShell  
 È possibile visualizzare l'elenco di condivisioni di distribuzione MDT usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) e il provider MDTProvider Windows PowerShell. Lo stesso elenco di condivisioni di distribuzione può essere visualizzato anche in Deployment Workbench.  

 **Per visualizzare un elenco di condivisioni di distribuzione usando i cmdlet MDT di Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione.  

###  <a name="UpdateDeployShare"></a> Aggiornamento di una condivisione di distribuzione con Windows PowerShell  
 È possibile aggiornare le condivisioni di distribuzione usando il cmdlet **Update-MDTDeploymentShare** e il provider MDTProvider Windows PowerShell. L'aggiornamento di una condivisione di distribuzione consente di creare le immagini di avvio di Windows PE, ovvero file WIM e ISO (International Organization for Standardization) necessari per avviare la distribuzione LTI. È possibile eseguire lo stesso processo usando Deployment Workbench, come descritto nella sezione relativa all'aggiornamento di una condivisione di distribuzione in Deployment Workbench.  

 **Per aggiornare una condivisione di distribuzione con Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Aggiornare la condivisione di distribuzione usando il cmdlet **Update-MDTDeploymentShare**, come indicato nell'esempio seguente:  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

    > [!NOTE]
    >  L'aggiornamento della condivisione di distribuzione può richiedere molto tempo. Lo stato di avanzamento del cmdlet viene visualizzato nella parte superiore della console di Windows PowerShell.  

     Il cmdlet non restituisce alcun output se l'aggiornamento ha esito positivo.  

###  <a name="UpdateLinkedDeployShare"></a> Aggiornamento di una condivisione di distribuzione collegata con Windows PowerShell  
 È possibile aggiornare (replicare) le condivisioni di distribuzione collegate usando il cmdlet **Update-MDTLinkedDS** e il provider MDTProvider Windows PowerShell. L'aggiornamento di una condivisione di distribuzione collegata consente di replicare il contenuto della condivisione di distribuzione originale nella condivisione di distribuzione collegata. È possibile eseguire lo stesso processo usando Deployment Workbench, come descritto nella sezione relativa alla replica delle condivisioni di distribuzione collegate in Deployment Workbench.  

 **Per aggiornare una condivisione di distribuzione collegata con Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Aggiornare la condivisione di distribuzione usando il cmdlet **Update-MDTDeploymentShare**, come indicato nell'esempio seguente:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

    > [!NOTE]
    >  L'aggiornamento della condivisione di distribuzione collegata può richiedere molto tempo. Lo stato di avanzamento del cmdlet viene visualizzato nella parte superiore della console di Windows PowerShell.  

     Il cmdlet non restituisce alcun output se l'aggiornamento ha esito positivo.  

###  <a name="UpdateDeployMedia"></a> Aggiornamento dei supporti di distribuzione con Windows PowerShell  
 È possibile aggiornare (generare) i supporti di distribuzione usando il cmdlet **Update-MDTMedia** e il provider MDTProvider Windows PowerShell. L'aggiornamento di un supporto di distribuzione replica il contenuto della condivisione di distribuzione originale nella condivisione di distribuzione collegata e quindi genera file ISO e WIM. È possibile eseguire lo stesso processo usando Deployment Workbench, come descritto nella sezione relativa alla generazione di immagini di supporti in Deployment Workbench.  

 Al termine dell'esecuzione del cmdlet **Update-MDTMedia** vengono creati i file seguenti:  

-   Un file ISO nella cartella *cartella_supporti* (dove *cartella_supporti* è il nome della cartella specificata per il supporto)  

     La generazione del file ISO è un'opzione che può essere configurata:  

    -   Selezionando l'opzione che consente di **generare un'immagine ISO di avvio di Lite Touch** nella scheda **Generali** della finestra di dialogo **Proprietà** del supporto. Deselezionare questa opzione per ridurre il tempo necessario per generare il supporto, a meno che non sia necessario creare DVD di avvio o avviare macchine virtuali dal file ISO  

    -   Impostando la stessa proprietà usando il cmdlet [Set-ItemProperty](http://technet.microsoft.com/library/hh849844)  

-   File WIM nella cartella *cartella_supporti*\Content\Deploy\Boot (dove *cartella_supporti* è il nome della cartella specificata per il supporto)  

 **Per aggiornare una condivisione di distribuzione collegata con Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Aggiornare la condivisione di distribuzione usando il cmdlet **Update-MDTDeploymentShare**, come indicato nell'esempio seguente:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

    > [!NOTE]
    >  L'aggiornamento della condivisione di distribuzione collegata può richiedere molto tempo. Lo stato di avanzamento del cmdlet viene visualizzato nella parte superiore della console di Windows PowerShell.  

     Il cmdlet non restituisce alcun output se l'aggiornamento ha esito positivo.  

###  <a name="ManageItemDeployShare"></a> Gestione di elementi in una condivisione di distribuzione con Windows PowerShell  
 Una condivisione di distribuzione contiene gli elementi usati per eseguire le distribuzioni, ad esempio sistemi operativi, applicazioni, driver di dispositivo, pacchetti del sistema operativo e sequenze di attività. Questi elementi possono essere gestiti usando i cmdlet di Windows PowerShell e quelli acclusi a MDT.  

 Per altre informazioni sulla modifica degli elementi usando direttamente i cmdlet di Windows PowerShell, vedere [Manipolazione diretta di elementi](http://technet.microsoft.com/library/dd315266.aspx). La struttura di cartelle per una condivisione di distribuzione può essere gestita anche usando Windows PowerShell. Per altre informazioni, vedere [Gestione delle cartelle delle condivisioni di distribuzione con Windows PowerShell](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importare un elemento in una condivisione di distribuzione  
 È possibile importare ogni tipo di elemento, ad esempio sistemi operativi, applicazioni o driver di dispositivo, usando i cmdlet MDT. Per ogni tipo di elemento è disponibile un cmdlet specifico di MDT. Se si vogliono importare più elementi in una condivisione di distribuzione usando Windows PowerShell, vedere [Automazione del popolamento di una condivisione di distribuzione](#AutomatePopulateDeployShare).  

 Nella tabella seguente sono elencati i cmdlet MDT di Windows PowerShell usati per importare gli elementi in una condivisione di distribuzione, con una breve descrizione di ogni cmdlet. Gli esempi di utilizzo di ogni cmdlet sono riportati nella sezione corrispondente a ogni cmdlet.  

 |**Cmdlet** | **Descrizione** |  
 |-|-|  
 |**Import-MDTApplication** |Importa un'applicazione in una condivisione di distribuzione|  
 |**Import-MDTDriver** |Importa uno o più driver di dispositivo in una condivisione di distribuzione|  
 |**Import-MDTOperatingSystem** |Importa uno o più sistemi operativi in una condivisione di distribuzione|  
 |**Import-MDTPackage** |Importa uno o più pacchetti del sistema operativo in una condivisione di distribuzione|  
 |**Import-MDTTaskSequence** |Importa una sequenza di attività in una condivisione di distribuzione|  

####  <a name="ViewPropertyDeployShare"></a> Visualizzare le proprietà di un elemento in una condivisione di distribuzione  
 Ogni elemento in una condivisione di distribuzione ha un diverso set di proprietà. Per visualizzare le proprietà di un elemento di una condivisione di distribuzione, è possibile usare il cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx). Il cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) usa MDTProvider per visualizzare le proprietà di un elemento specifico, esattamente si possono visualizzare le proprietà in Deployment Workbench.  

 Per visualizzare le proprietà di più elementi di una condivisione di distribuzione usando Windows PowerShell, vedere [Automazione del popolamento di una condivisione di distribuzione](#AutomatePopulateDeployShare).  

 **Per visualizzare le proprietà di un elemento in una condivisione di distribuzione usando Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato nell'esempio seguente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Restituire un elenco di elementi per il tipo di elemento di cui si vogliono visualizzare le proprietà usando il cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788) come illustrato nell'esempio seguente:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Nell'esempio precedente viene visualizzato un elenco di tutti i sistemi operativi presenti nella condivisione di distribuzione. L'output viene inviato al cmdlet **Format-List** in modo che i nomi lunghi dei sistemi operativi possano essere visualizzati. Per altre informazioni sull'uso del cmdlet **Format-List**, vedere l'argomento relativo all'[uso del cmdlet Format-List](http://technet.microsoft.com/library/ee176830.aspx). Lo stesso processo può essere usato per restituire l'elenco di altri tipi di elementi, ad esempio driver di dispositivo o applicazioni.  

    > [!TIP]
    >  È anche possibile usare il comando **dir** per visualizzare l'elenco dei sistemi operativi anziché il cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Visualizzare le proprietà di uno degli elementi indicati nel passaggio precedente usando il cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), come illustrato nell'esempio seguente:  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     In questo esempio il valore del parametro *Path* è il percorso completo di Windows PowerShell all'elemento, che include il nome del file restituito nel passaggio precedente. È possibile usare lo stesso processo per visualizzare le proprietà di altri tipi di elementi, ad esempio driver di dispositivo o applicazioni.  

####  <a name="RemoveItemDeployShare"></a> Rimuovere un elemento da una condivisione di distribuzione  
 È possibile rimuovere un elemento da una condivisione di distribuzione usando il cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765). Il cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765) usa MDTProvider per rimuovere un elemento specifico, esattamente come si può rimuovere un elemento in Deployment Workbench. Se si vogliono rimuovere più elementi in una condivisione di distribuzione usando Windows PowerShell, vedere [Automazione del popolamento di una condivisione di distribuzione](#AutomatePopulateDeployShare).  

> [!NOTE]
>  La rimozione di un elemento usato da una sequenza di attività impedisce la riuscita della sequenza di attività. Prima di rimuovere un elemento, verificare che all'elemento non facciano riferimento altri elementi presenti nella condivisione di distribuzione. Se un elemento viene rimosso, non può essere recuperato.  

 **Per rimuovere un elemento da una condivisione di distribuzione usando Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente.  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate correttamente usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) come indicato nell'esempio seguente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider.  

4.  Restituire un elenco di elementi per il tipo di elemento di cui si vogliono visualizzare le proprietà usando il cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788) come illustrato nell'esempio seguente:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Nell'esempio precedente viene visualizzato un elenco di tutti i sistemi operativi presenti nella condivisione di distribuzione. L'output viene inviato al cmdlet **Format-List** in modo che i nomi lunghi dei sistemi operativi possano essere visualizzati. Per altre informazioni sull'uso del cmdlet **Format-List**, vedere l'argomento relativo all'[uso del cmdlet Format-List](http://technet.microsoft.com/library/ee176830.aspx). Si può usare lo stesso processo per restituire l'elenco di altri tipi di elementi, ad esempio driver di dispositivo o applicazioni.  

    > [!TIP]
    >  È anche possibile usare il comando **dir** per visualizzare l'elenco dei sistemi operativi anziché il cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Rimuovere uno degli elementi indicati nel passaggio precedente usando il cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), come illustrato nell'esempio seguente:  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     In questo esempio il valore del parametro *Path* è il percorso completo di Windows PowerShell all'elemento, che include il nome del file restituito nel passaggio precedente.  

     Si può usare lo stesso processo per rimuovere altri tipi di elementi, ad esempio driver di dispositivo o applicazioni.  

    > [!NOTE]
    >  La rimozione di un elemento usato da una sequenza di attività impedisce la riuscita della sequenza di attività. Prima di rimuovere un elemento, verificare che all'elemento non facciano riferimento altri elementi presenti nella condivisione di distribuzione.  

###  <a name="AutomatePopulateDeployShare"></a> Automazione del popolamento di una condivisione di distribuzione  
 I cmdlet MDT di Windows PowerShell consentono di gestire singoli elementi. Tuttavia, usando alcune delle funzionalità di scripting in Windows PowerShell, i cmdlet possono essere usati per automatizzare il popolamento di una condivisione di distribuzione.  

 Ad esempio, per un'organizzazione può essere necessario distribuire più condivisioni di distribuzione per diverse unità aziendali o un'organizzazione può offrire servizi di distribuzione del sistema operativo per altre organizzazioni. In entrambi questi esempi le organizzazioni devono essere in grado di creare e popolare condivisioni di distribuzione configurate in modo coerente.  

 Un metodo per gestire più elementi può essere usare un file con valori delimitati da virgole (CSV) contenente un elenco di tutti gli elementi che si prevede di gestire in una condivisione di distribuzione usando il cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx).  

 Di seguito è riportato un estratto di uno script di Windows PowerShell che consente di importare un elenco di applicazioni basato sulle informazioni contenute in un file CSV usando i cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731) e **Import-MDTApplication**:  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 In questo esempio il file C:\MDT\Import-MDT-Apps.csv contiene un campo per ogni variabile necessaria per importare un'applicazione. Per altre informazioni sulla creazione di un file CSV da usare con il cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vedere l'argomento relativo all'uso del [cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

 È possibile usare questo stesso metodo per importare sistemi operativi, driver di dispositivo e altri elementi in una condivisione di distribuzione effettuando le operazioni seguenti:  

1.  Creare un file CSV per ogni tipo di elemento della condivisione di distribuzione da popolare.  

2.  Per altre informazioni sulla creazione di un file CSV da usare con il cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vedere l'argomento relativo all'uso del [cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

3.  Creare un file di script di Windows PowerShell che verrà usato per automatizzare il popolamento della condivisione di distribuzione.  

     Per altre informazioni su come creare uno script di Windows PowerShell, vedere l'argomento relativo alla [creazione di script con Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Creare l'eventuale struttura di cartelle dei prerequisiti richiesta nella condivisione di distribuzione prima di importare gli elementi della condivisione di distribuzione.  

     Per altre informazioni, vedere [Gestione delle cartelle delle condivisioni di distribuzione con Windows PowerShell](#ManageDeployShareFolder).  

5.  Aggiungere la riga del cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) per uno dei file CSV creati nel passaggio 1.  

     Per altre informazioni sul cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vedere l'argomento relativo all'uso del [cmdlet Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

6.  Creare un ciclo di cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) che elabori ogni elemento del file CSV a cui si fa riferimento nel cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) nel passaggio precedente.  

     Per altre informazioni sul cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731), vedere l'argomento relativo all'[uso del cmdlet ForEach-Object](http://technet.microsoft.com/library/ee176828).  

7.  Aggiungere il cmdlet MDT corrispondente per importare gli elementi della condivisione di distribuzione nel ciclo di cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) creato nel passaggio precedente.  

     Per altre informazioni sui cmdlet MDT usati per importare elementi in una condivisione di distribuzione, vedere [Importare un elemento in una condivisione di distribuzione](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Gestione delle cartelle delle condivisioni di distribuzione con Windows PowerShell  
 È possibile gestire le cartelle in una condivisione di distribuzione usando gli strumenti da riga di comando, ad esempio il comando **mkdir**, o i cmdlet di Windows PowerShell, ad esempio [New-Item](http://technet.microsoft.com/library/hh849795), e il provider MDTProvider Windows PowerShell. La stessa struttura di cartelle di condivisioni di distribuzione può essere visualizzata e gestita anche in Deployment Workbench. Per altre informazioni sulla modifica degli elementi usando direttamente i cmdlet di Windows PowerShell, vedere [Manipolazione diretta di elementi](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Creare una cartella in una condivisione di distribuzione con Windows PowerShell  
 **Per creare una cartella in una condivisione di distribuzione usando Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione  

4.  Creare una cartella denominata *Windows_8* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il comando **mkdir**, come illustrato nell'esempio seguente:  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

5.  Verificare che la cartella venga creata correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Vengono visualizzate la cartella Windows_8 e tutte le cartelle esistenti nella cartella dei sistemi operativi.  

6.  Creare una cartella denominata *Windows_7* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il cmdlet [New-Item](http://technet.microsoft.com/library/hh849795), come illustrato nell'esempio seguente e descritto nell'argomento relativo all'uso del [cmdlet New-Item](http://technet.microsoft.com/library/ee176914.aspx):  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     Il cmdlet visualizza l'esito positivo della creazione della cartella.  

7.  Verificare che la cartella venga creata correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Vengono visualizzate la cartella Windows_7 e tutte le cartelle esistenti nella cartella dei sistemi operativi.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Eliminare una cartella in una condivisione di distribuzione con Windows PowerShell  
 **Per eliminare una cartella in una condivisione di distribuzione usando Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione.  

4.  Eliminare (rimuovere) una cartella denominata *Windows_8* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il comando **mkdir**, come illustrato nell'esempio seguente:  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

5.  Verificare che la cartella venga rimossa correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La cartella Windows_8 non è più visualizzata nell'elenco delle cartelle presenti nella cartella dei sistemi operativi  

6.  Eliminare (rimuovere) una cartella denominata *Windows_7* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), come illustrato nell'esempio seguente:  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     Il cmdlet visualizza l'esito positivo della rimozione della cartella.  

7.  Verificare che la cartella venga creata correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La cartella Windows_7 non è più visualizzata nell'elenco delle cartelle presenti nella cartella dei sistemi operativi.  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Rinominare una cartella in una condivisione di distribuzione con Windows PowerShell  
 **Per rinominare una cartella in una condivisione di distribuzione usando Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato di seguito:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione.  

4.  Rinominare una cartella denominata *Windows_8* in *Win_8* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il comando **ren**, come illustrato nell'esempio seguente:  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

5.  Verificare che la cartella venga rimossa correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La cartella Windows_8 è stata rinominata in *Win_8*.  

6.  Rinominare una cartella denominata *Windows_7* in *Win_7* nella cartella dei sistemi operativi di una condivisione di distribuzione usando il cmdlet [Rename-Item](http://technet.microsoft.com/library/hh849763), come illustrato nell'esempio seguente:  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     Il cmdlet visualizza l'esito positivo della ridenominazione della cartella.  

7.  Verificare che la cartella venga creata correttamente, digitando il comando seguente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La cartella Windows_7 è stata rinominata in *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automazione dell'applicazione dei Service Pack del sistema operativo nelle condivisioni di distribuzione  
 I Service Pack del sistema operativo sono una fase normale del ciclo di vita del software. I sistemi operativi esistenti nelle condivisioni di distribuzione devono essere aggiornati con i Service Pack al fine di garantire che i computer appena distribuiti o aggiornati siano allineati alle indicazioni di sicurezza e alle impostazioni di configurazione più recenti.  

 Se un'organizzazione ha molte condivisioni di distribuzione con più sistemi operativi in ogni condivisione, il processo di aggiornamento manuale dei sistemi operativi in ogni condivisione di distribuzione con i Service Pack può richiedere molto tempo. Esistono alcuni metodi per automatizzare l'applicazione dei Service Pack del sistema operativo nelle condivisioni di distribuzione, tra cui:  

-   Copia del contenuto di origine aggiornato che contiene già il Service Pack, ad esempio Windows 7 con supporto di SP1, nella cartella della condivisione di distribuzione in cui si trova il sistema operativo esistente, come descritto in [Automazione dell'applicazione di Service Pack del sistema operativo da un supporto di origine aggiornato](#AutomateAppFromUSM)  

-   Applicazione del Service Pack a un computer di riferimento e quindi acquisizione di un'immagine aggiornata da un computer di riferimento, come descritto in [Automazione dell'applicazione di Service Pack del sistema operativo usando un computer di riferimento e Windows PowerShell](#AutomateAppUsingRef)  

###  <a name="AutomateAppFromUSM"></a> Automazione dell'applicazione dei Service Pack del sistema operativo da un supporto di origine aggiornato  
 È possibile automatizzare il processo di aggiornamento dei Service Pack del sistema operativo con Windows PowerShell se i supporti di origine includono il Service Pack, ad esempio se è disponibile un DVD con Windows 7 con SP1 già integrato.  

 Per questo metodo, il supporto di origine del sistema operativo con il Service Pack viene copiato sui file del sistema operativo esistente senza Service Pack nella condivisione di distribuzione usando Windows PowerShell.  

 **Per automatizzare l'applicazione dei Service Pack del sistema operativo da un supporto di origine aggiornato con Windows PowerShell**  

1.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

2.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

3.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato nell'esempio che segue:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione.  

4.  Rimuovere la cartella per il sistema operativo esistente dalla condivisione di distribuzione usando i cmdlet [Get-ChildItem](http://technet.microsoft.com/library/hh849800) e [Remove-Item](http://technet.microsoft.com/library/hh849765), come illustrato nell'esempio seguente:  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     In questo esempio *DS002:* è il nome di un'unità Windows PowerShell restituita nel passaggio 3.  

5.  Copiare il contenuto dei file di origine del sistema operativo in cui è integrato il Service Pack usando il cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), come illustra l'esempio seguente:  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     In questo esempio i file di origine del sistema operativo sono sull'unità E e *DS002:* è il nome di un'unità di Windows PowerShell restituita nel passaggio 3.  

6.  Aggiornare eventuali supporti di distribuzione di MDT basati sulla condivisione di distribuzione usando il cmdlet **Update-MDTMedia**.  

 Per altre informazioni su come aggiornare i supporti di distribuzione di MDT basati sulla condivisione di distribuzione usando il cmdlet **Update-MDTMedia**, vedere [Aggiornamento dei supporti di distribuzione con Windows PowerShell](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automazione dell'applicazione di Service Pack del sistema operativo usando un computer di riferimento e Windows PowerShell  
 È possibile automatizzare il processo di aggiornamento dei Service Pack del sistema operativo con Windows PowerShell quando solo il Service Pack non è ancora integrato nel sistema operativo, ad esempio se SP1 per Windows 7 non è ancora integrato con un'immagine di Windows 7.  

 Per questo metodo, distribuire il sistema operativo senza il Service Pack a un computer di riferimento. Quindi, applicare il Service Pack nel computer di riferimento. Successivamente, acquisire un'immagine del sistema operativo dal computer di riferimento. Infine, copiare il file WIM acquisito sul file Install.wim del sistema operativo nella condivisione di distribuzione usando Windows PowerShell.  

 **Per automatizzare l'applicazione dei Service Pack del sistema operativo da un supporto di origine aggiornato con Windows PowerShell**  

1.  Distribuire il sistema operativo di destinazione a un computer di riferimento.  

     Per altre informazioni su come distribuire un computer di riferimento, vedere gli argomenti seguenti nel documento di MDT *Uso di Microsoft Deployment Toolkit*:  

    -   Preparazione per la distribuzione LTI al computer di riferimento  

    -   Distribuzione a e acquisizione di un'immagine del computer di riferimento in LTI  

2.  Installare il Service Pack nel computer di riferimento.  

     Per altre informazioni sull'installazione del Service Pack, vedere la documentazione acclusa al Service Pack.  

3.  Per acquisire un'immagine del computer di riferimento, creare e distribuire una sequenza di attività basata sul modello di sequenza **Sysprep e acquisizione**.  

     Per altre informazioni sulla creazione di una sequenza di attività basata sul modello **Sysprep e acquisizione**, vedere la sezione relativa alla creazione di una nuova sequenza di attività in Deployment Workbench.  

4.  Caricare lo snap-in MDT di Windows PowerShell come descritto in [Caricamento dello snap-in MDT di Windows PowerShell](#LoadMDTSnapIn).  

5.  Verificare che le distribuzioni MDT che condividono le unità Windows PowerShell vengano ripristinate usando il cmdlet **Restore-MDTPersistentDrive**, come illustrato nell'esempio seguente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Se le distribuzioni MDT che condividono le unità Windows PowerShell sono già state ripristinate, si riceverà un messaggio di avviso che indica che il cmdlet non è in grado di ripristinare l'unità.  

6.  Visualizzare l'elenco delle distribuzioni MDT che condividono le unità Windows PowerShell, una per ogni condivisione di distribuzione, usando il cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), come indicato nell'esempio che segue:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Viene visualizzato l'elenco delle unità Windows PowerShell specificate usando MDTProvider, una per ogni condivisione di distribuzione.  

7.  Copiare il file WIM acquisito nel passaggio 3 sul file Install.wim del sistema operativo nella condivisione di distribuzione usando il cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793) come illustrato nell'esempio seguente:  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     In questo esempio il file di immagine del sistema operativo acquisito (Win7SP1.wim) presente nella cartella delle acquisizioni della condivisione DS002: è il nome di un'unità di Windows PowerShell restituita nel passaggio 6 e il sistema operativo Windows 7 esistente viene archiviato nella cartella denominata *Windows 7*.  

8.  Aggiornare eventuali supporti di distribuzione di MDT basati sulla condivisione di distribuzione usando il cmdlet **Update-MDTMedia**.  

     Per altre informazioni su come aggiornare i supporti di distribuzione di MDT basati sulla condivisione di distribuzione usando il cmdlet **Update-MDTMedia**, vedere [Aggiornamento dei supporti di distribuzione con Windows PowerShell](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Personalizzazione della distribuzione basata sul tipo di chassis  
 È possibile personalizzare la distribuzione in base al tipo di chassis del computer. Gli script creano variabili locali che possono essere elaborate nel file CustomSettings.ini. Le variabili locali `IsLaptop`, `IsDesktop`, e `IsServer` indicano rispettivamente se il computer è un computer portatile, un computer desktop o un server.  

> [!NOTE]
>  Nelle versioni precedenti di Deployment Workbench il flag `IsServer` indica che il sistema operativo esistente è un sistema operativo server, ad esempio Windows Server 2003 Enterprise Edition. Questo flag è stato rinominato in `IsServerOS`.  

 **Per implementare le variabili locali nel file CustomSettings.ini**  

1.  Nella sezione `[Settings]`, riga `Priority`, aggiungere una sezione personalizzata per personalizzare la distribuzione in base al tipo di chassis (`ByChassisType` nell'esempio seguente, dove *Chassis* rappresenta il tipo di computer).  

2.  Creare la sezione personalizzata che corrisponde alla sezione personalizzata definita nel passaggio 1 (`ByChassisType` nell'esempio riportato di seguito, dove *Chassis* rappresenta il tipo di computer).  

3.  Definire una sottosezione per ogni tipo di chassis da rilevare (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` nell'esempio seguente).  

4.  Creare una sottosezione per ogni stato `True` e `False` di ogni sottosezione definita nel passaggio 3 (`[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` nell'esempio seguente).  

5.  In ogni sottosezione `True` e `False` aggiungere le impostazioni appropriate in base al tipo di chassis.  

 **Listato 1. Esempio di personalizzazione della distribuzione basata sul tipo di chassis nel file CustomSettings.ini**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Distribuzione di applicazioni basate su versioni precedenti delle applicazioni  
 Spesso, quando si installa un sistema operativo in un computer esistente, si installano le stesse applicazioni che in precedenza erano state installate nel computer. Per eseguire questa operazione, usare gli script di MDT, in particolare ZTIGather.wsf, per eseguire una query su due origini dati separate:  

-   **Funzionalità di inventario software di Configuration Manager** Contiene un record per ogni pacchetto di applicazioni, in questo caso i listati in Programmi e funzionalità in Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, installato l'ultima volta che Configuration Manager ha creato un inventario per il computer.  

-   **Una tabella di mapping.** Indica quale pacchetto e programma devono essere installati per ogni record, poiché i record di Programmi e funzionalità o Installazione applicazioni non specificano esattamente quale pacchetto ha installato l'applicazione, rendendo impossibile la selezione automatica del pacchetto solo in base all'inventario.  

 **Per eseguire un'installazione dinamica dell'applicazione specifica del computer**  

1.  Usare la tabella disponibile nel database MDT per connettere pacchetti specifici con le applicazioni indicate nel sistema operativo di destinazione.  

2.  Popolare la tabella con i dati che associano il pacchetto appropriato con l'applicazione indicata in Programmi e funzionalità o Installazione applicazioni.

     **Query SQL per popolare la tabella**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     La riga inserita connette qualsiasi computer con la voce `Office12.0` al pacchetto Microsoft Office 2010 Professional Plus.  

     Ciò significa che Microsoft Office 2010 Professional Plus verrà installato in qualsiasi computer che attualmente esegue il sistema Microsoft Office 2007 (Office 12.0). Aggiungere le voci simili per eventuali altri pacchetti. Gli elementi per cui non esistono voci vengono ignorati (non verrà installato alcun pacchetto).  

3.  Creare una stored procedure per semplificare l'aggiunta delle informazioni della nuova tabella ai dati di inventario.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     La stored procedure nell'esempio precedente presuppone che il database centrale del sito primario di Configuration Manager si trovi nel computer in cui viene eseguito SQL Server come database MDT. Se il database centrale del sito primario si trova in un altro computer, è necessario apportare le modifiche appropriate alla stored procedure. Inoltre, il nome del database (`CM_DB`) deve essere aggiornato. Considerare anche la possibilità di concedere ad altri account l'accesso in lettura alla visualizzazione **v_GS_ADD_REMOVE_PROGRAMS** nel database di Configuration Manager.  

4.  Configurare il file CustomSettings.ini in modo da eseguire una query su questa tabella di database specificando il nome di una sezione (`[DynamicPackages]` nell'elenco **Priority**) che punta alle informazioni del database.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Creare una sezione `[DynamicPackages]` per specificare il nome di una sezione del database.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Creare una sezione di database per specificare le informazioni sul database e i dettagli della query.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     Nell'esempio precedente viene eseguita una query sul database MDT denominato *MDTDB* nel computer che esegue l'istanza di SQL Server denominata *SERVER1*. Il database contiene una stored procedure denominata `RetrievePackages` (creata nel passaggio 3).  

 Quando è in esecuzione ZTIGather.wsf viene automaticamente generata un'istruzione SQL (Structured Query Language) `SELECT` e il valore della chiave personalizzata **MakeModelQuery** viene passato come parametro alla query:  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 Il valore effettivo della chiave personalizzata **MACAddress** verrà sostituito al valore "?" corrispondente.  Questa query restituisce un set di record con le righe specificate nel passaggio 2.  

 Un numero variabile di argomenti non può essere passato a una stored procedure. Di conseguenza, quando un computer ha più di un indirizzo MAC, non tutti gli indirizzi MAC possono essere passati alla stored procedure. In alternativa, sostituire la stored procedure con una visualizzazione che consente di eseguire query sulla visualizzazione con un'istruzione `SELECT` con una clausola `IN` per passare tutti i valori di indirizzo MAC.  

 In base allo scenario presentato qui, se il computer corrente ha il valore `Office12.0` inserito nella tabella (passaggio 2), viene restituita la riga `XXX0000F:Install Office 2010 Professional Plus`. Ciò indica che il pacchetto XXX0000f:Install Office 2001 Professional Plus verrà installato dal processo ZTI durante la fase di ripristino dello stato.  

## <a name="fully-automated-lti-deployment-scenario"></a>Scenario di distribuzione LTI completamente automatizzato  
 Lo scopo principale di LTI è quello di automatizzare il più possibile il processo di distribuzione. Benché ZTI offra l'automazione completa della distribuzione grazie agli script di MDT e a Servizi di distribuzione Windows, LTI è progettato in modo da funzionare con meno requisiti in termini di infrastruttura.  

 È possibile automatizzare la distribuzione guidata di Windows usata nel processo di distribuzione LTI per ridurre (o eliminare) le pagine della procedura guidata visualizzate. È possibile ignorare l'intera distribuzione guidata di Windows, specificando la proprietà **SkipWizard** in CustomSettings.ini. Per ignorare singole pagine della procedura guidata, usare le proprietà seguenti:  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Per altre informazioni sulle singole proprietà, vedere la proprietà corrispondente nel documento di MDT *Informazioni di riferimento sul toolkit*.  

Per ogni pagina della procedura guidata ignorata, specificare i valori per le proprietà corrispondenti che sono in genere raccolte nella pagina della procedura guidata nei file CustomSettings.ini e BootStrap.ini. Per altre informazioni sulle proprietà che devono essere configurate in questi file, vedere la sezione relativa alle proprietà per le pagine ignorate della distribuzione guidata nel documento di MDT *Informazioni di riferimento sul toolkit*.  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Distribuzione LTI completamente automatizzata per uno scenario di aggiornamento dei computer  
 Di seguito viene illustrato un file CustomSettings.ini usato in uno scenario di aggiornamento dei computer per ignorare tutte le pagine della distribuzione guidata di Windows. In questo esempio le proprietà da usare quando si ignora la pagina della procedura guidata sono immediatamente sotto la proprietà che ignora la pagina della procedura guidata.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Distribuzione LTI completamente automatizzata per uno scenario di nuovi computer  
 Di seguito viene illustrato un esempio di file CustomSettings.ini usato in uno scenario di creazione di nuovi computer per ignorare tutte le pagine della distribuzione guidata di Windows. In questo esempio le proprietà da usare quando si ignora la pagina della procedura guidata sono immediatamente sotto la proprietà che ignora la pagina della procedura guidata.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Chiamata dei servizi Web in MDT  
 Nelle versioni precedenti di MDT l'elaborazione delle regole è supportata con CustomSettings.ini e i database, da cui è possibile recuperare i valori del computer locale, in genere usando WMI, per prendere decisioni sulle operazioni da eseguire per ogni computer durante la distribuzione. Inoltre, è possibile fare in modo che le query SQL e le chiamate di stored procedure recuperino informazioni aggiuntive dai database esterni. Questo approccio tuttavia presenta delle difficoltà, in particolare quando si creano connessioni SQL protette.  

 Per risolvere questo problema, MDT offre la possibilità di eseguire chiamate ai servizi Web in base a semplici regole definite in CustomSettings.ini. Tali richieste di servizi Web non richiedono alcun contesto di sicurezza speciale e sono in grado di usare qualsiasi porta TCP/IP necessaria per semplificare le configurazioni dei firewall.  

 Di seguito viene illustrato come configurare CustomSettings.ini per chiamare un servizio Web specifico. In questo scenario il servizio Web viene scelto in modo casuale da una ricerca in Internet. Accetta un codice postale come input e restituisce città, provincia, indicativo di località e fuso orario (come lettera) per il codice postale specificato.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 L'esecuzione di questo codice genera un output simile al seguente:
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Esistono alcune piccole complicazioni da tenere sotto controllo quando si esegue un servizio Web:  

-   Non eseguire operazioni speciali con i server proxy. Se è presente un proxy anonimo, usarlo, ma l'autenticazione dei proxy può causare problemi. Nella maggior parte dei casi non verrà chiamato un servizio Web.  

-   CustomSettings.ini o ZTIGather.xml cerca le proprietà definite nel markup XML restituito in seguito alla chiamata del servizio Web (come accade con una query sul database o un'altra regola). Tuttavia, la ricerca XML non fa distinzione tra maiuscole e minuscole. Per fortuna, il servizio Web descritto di seguito restituisce tutti i nomi di proprietà in lettere maiuscole, che è quanto prevede ZTIGather.xml. È possibile modificare il mapping delle voci in lettere minuscole o maiuscole e minuscole per evitare il problema.  

-   Si consiglia di usare una richiesta `POST` al servizio Web, in modo che la chiamata del servizio Web sia in grado di supportare un `POST`.  

## <a name="connecting-to-network-resources"></a>Connessione alle risorse di rete  
 Durante i processi di distribuzione LTI e ZTI è possibile richiedere l'accesso a una risorsa di rete in un server diverso dal server che ospita la condivisione di distribuzione. L'utente deve essere autenticato nell'altro server in modo da poter accedere alle cartelle condivise o ai servizi presenti nello stesso. Ad esempio, è possibile installare un'applicazione da una cartella condivisa in un server diverso da quello che ospita la condivisione di distribuzione usata dagli script di MDT.  

> [!NOTE]
>  Per eseguire query sui database di SQL Server ospitati in un server diverso da quello che ospita la condivisione di distribuzione, vedere le proprietà **Database**, **DBID**, **DBPwd**, **Instance**, **NetLib**, **Order**, **Parameters**, **ParameterCondition**, **SQLServer**, **SQLShare** e **Table** nel documento di MDT *Informazioni di riferimento sul toolkit*.  

 Usando lo script ZTIConnect.wsf è possibile connettersi ad altri server e accedere alle relative risorse. La sintassi per lo script ZTIConnect.wsf è la seguente (dove *unc_path* è un percorso UNC per la connessione al server):  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 Nella maggior parte dei casi, si esegue lo script ZTIConnect.wsf come sequencer delle attività. Eseguire lo script ZTIConnect.wsf prima delle attività che richiedono l'accesso a un server diverso dal server che ospita la condivisione di distribuzione.  

 **Per aggiungere lo script ZTIConnect.wsf come attività alla sequenza di attività di una build**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro dei dettagli fare clic su ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività da modificare).  

4.  Nel riquadro Azioni fare clic su **Proprietà**.  

5.  Fare clic sulla scheda Sequenza di attività, passare a **gruppo** (dove *gruppo* è il gruppo in cui viene eseguito lo script ZTIConnec.wsf) e fare clic su **Aggiungi**. Fare clic su **Generali** e quindi fare clic su **Esegui riga di comando**.  

    > [!NOTE]
    >  Aggiungere l'attività prima di aggiungere eventuali attività che richiedono l'accesso alle risorse nel server di destinazione.  

6.  Completare la scheda **Proprietà** della nuova attività usando le informazioni seguenti:

    |**In questa casella** |**Eseguire questa operazione** |  
    |-|-|  
    |**Nome** |Digitare **Connect to server** (dove server è il nome del server a cui connettersi).|  
    |**Descrizione** |Digitare un testo che spiega perché deve essere stabilita la connessione.|  
    |**Comando** |Digitare **Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path** (dove *unc_path* è il percorso UNC a una cartella condivisa nel server).|  

7.  Completare la scheda **Opzioni** della nuova attività usando le informazioni seguenti. Se non diversamente specificato, accettare i valori predefiniti e quindi fare clic su **OK**.  

    |**In questa casella** |**Eseguire questa operazione** |  
    |-|-|  
    |**Codici di riuscita** |Digitare **0 3010**. (lo script ZTIConnect.wsf restituisce questi codici a completamento riuscito).|  
    |**Casella di riepilogo condizioni** |Aggiungere tutte le condizioni che possono essere necessarie (nella maggior parte dei casi questa attività non richiede condizioni).|  

 Dopo aver aggiunto l'attività che eseguirà lo script ZTIConnect.wsf, le attività successive possono accedere alle risorse di rete nel server specificato nell'opzione **/uncpath** dello script ZTIConnect.wsf.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Distribuzione dei driver di dispositivo corretti ai computer con gli stessi dispositivi hardware ma di marca e modello diversi  
 Possono esistere variazioni dei nomi e numeri di modello praticamente senza alcuna differenza nel set di driver. Le variazioni nei nomi e numeri di modello possono aumentare inutilmente il tempo impiegato per creare più voci di database per un determinato modello. La procedura seguente spiega come definire una nuova proprietà usando una chiamata di funzione User Exit che restituisce una sottostringa del numero di modello.  

 **Per creare gli alias di modello**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** scegliere la scheda **Regole**.  

5.  Creare gli alias per i tipi di hardware nelle sezioni di marca e modello del database MDT. Troncare il tipo di modello in corrispondenza della parentesi aperta "(" nel nome del modello. Ad esempio, *HP DL360 (G112)* diventa *HP DL360*.  

6.  Aggiungere la variabile personalizzata **ModelAlias** a ogni sezione.  

7.  Creare una nuova sezione `[SetModel]`.  

8.  Aggiungere la sezione `[SetModel]` alle impostazioni della **priorità** nella sezione `[Settings]`.  

9. Aggiungere una riga alla sezione `ModelAlias` per fare riferimento a uno script User Exit che tronca il nome del modello prima di "(".  

10. Creare una ricerca nel database **MMApplications** in cui **ModelAlias** è uguale a **Model**.  

11. Creare uno script User Exit e posizionarlo nella stessa directory del file CustomSettings.ini per troncare il nome del modello.  

    Di seguito sono riportati, nell'ordine, un file CustomSettings.ini e lo script User Exit.  

     **CustomSettings.ini**:  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Script User Exit**:  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Configurazione dei passaggi della sequenza di attività condizionale  
 In alcuni scenari è possibile eseguire un passaggio della sequenza di attività in modo condizionale in base a criteri definiti. È possibile aggiungere qualsiasi combinazione di queste condizioni per determinare se il passaggio della sequenza di attività deve essere eseguito. Ad esempio, usare il valore di una variabile della sequenza di attività e il valore di un'impostazione del Registro di sistema per determinare se si deve eseguire un passaggio della sequenza di attività.  

 Usando MDT, eseguire una sequenza di attività in modo condizionale in base a:  

-   Una o più istruzioni **IF**  

-   Una variabile della sequenza di attività  

-   La versione del sistema operativo di destinazione  

-   I risultati booleani di una query WMI  

-   Un'impostazione del Registro di sistema  

-   Il software installato nel computer di destinazione  

-   Le proprietà di una cartella  

-   Le proprietà di un file  

### <a name="configuring-a-conditional-task-sequence-step"></a>Configurazione di un passaggio della sequenza di attività condizionale  
 I passaggi di una sequenza di attività condizionale vengono configurati in Deployment Workbench, nella scheda **Opzioni** di un passaggio della sequenza di attività. È possibile aggiungere una o più condizioni al passaggio della sequenza di attività per creare la condizione appropriata per eseguire o meno il passaggio.  

> [!NOTE]
>  Ogni passaggio della sequenza di attività condizionale deve avere almeno un'istruzione **IF**.  

 **Per visualizzare la scheda Opzioni di un passaggio della sequenza di attività**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro dei dettagli fare clic su **sequenza_attività** (dove *sequenza_attività* è il nome della sequenza di attività da configurare).  

4.  Nel riquadro Azioni fare clic su **Proprietà**.  

5.  Nella scheda ***Sequenza attività*** della finestra di dialogo **Proprietà** di **sequenza_attività** fare clic su ***passaggio*** (dove *passaggio* è il nome del passaggio della sequenza di attività da configurare) e quindi fare clic sulla scheda **Opzioni**.  

 Nella scheda **Opzioni** del passaggio della sequenza di attività eseguire le azioni seguenti:  

-   **Aggiungi.** Fare clic su questo pulsante per aggiungere una condizione al passaggio della sequenza di attività.  

-   **Rimuovi.** Fare clic su questo pulsante per rimuovere una condizione esistente in un passaggio della sequenza di attività.  

-   **Modifica.** Fare clic su questo pulsante per modificare una condizione esistente in un passaggio della sequenza di attività.  

### <a name="if-statements-in-conditions"></a>Uso delle istruzioni IF nelle condizioni  
 Tutte le condizioni della sequenza di attività includono una o più istruzioni **IF**. Le istruzioni **IF** sono la base del processo di creazione dei passaggi di una sequenza di attività condizionale. Una condizione del passaggio della sequenza di attività può includere solo un'istruzione **IF**, ma si possono nidificare più istruzioni **IF** sotto l'istruzione **IF** di primo livello per creare condizioni più complesse.  

 Un'istruzione **IF** può essere basata sulle condizioni elencate nella tabella seguente, che vengono configurate nella finestra di dialogo **Proprietà dell'istruzione If**.  

 |**Condizione** |**Selezionare questa opzione per eseguire la sequenza di attività se** |  
 |-|-|  
 |**Tutte le condizioni** |Tutte le condizioni sotto questa istruzione **IF** devono essere true.|  
 |**Qualsiasi condizione** |Qualsiasi condizione sotto questa istruzione **IF** è true.|  
 |**Nessuno** |Nessuna delle condizioni sotto questa istruzione **IF** è true.|  

 Completare la condizione per eseguire il passaggio della sequenza di attività aggiungendo altri criteri alle condizioni, ad esempio le variabili della sequenza di attività o i valori in un'impostazione del Registro di sistema.  

 **Per aggiungere una condizione con istruzione IF a un passaggio della sequenza di attività**  

1.  Nella scheda ***Opzioni*** di **passaggio** (dove *passaggio* è il nome del passaggio della sequenza di attività da configurare) fare clic su **Aggiungi** e quindi su **Istruzione If**.  

2.  Nella finestra di dialogo **Proprietà dell'istruzione If** fare clic su **condizione** (dove *condizione* è una delle condizioni elencate nella tabella precedente), quindi fare clic su **OK**.  

### <a name="task-sequence-variables-in-conditions"></a>Condizione Variabile della sequenza di attività  
 Usare la condizione **Variabile della sequenza di attività** per valutare le variabili della sequenza di attività create da un'attività **Imposta variabile della sequenza di attività** o da qualsiasi attività della sequenza di attività. Si consideri ad esempio una rete che contiene computer client Windows XP che fanno parte di un dominio e altri che sono inclusi in un gruppo di lavoro. Sapendo che i criteri di dominio correnti impongono il salvataggio di tutte le impostazioni utente in rete, può essere necessario salvare le impostazioni utente solo per i computer che non fanno parte del dominio, ovvero i computer inclusi nel gruppo di lavoro. In questo caso, aggiungere una condizione all'attività **Acquisisci file utente e impostazioni** che faccia riferimento ai computer del gruppo di lavoro.  

 **Per aggiungere una condizione basata su una variabile della sequenza di attività**  

1.  Nella scheda ***Opzioni*** di **passaggio** (dove *passaggio* è il nome del passaggio della sequenza di attività da configurare) fare clic su **Aggiungi condizione** e quindi su **Variabile della sequenza di attività**.  

2.  Nella finestra di dialogo della condizione **Variabile della sequenza di attività** digitare **OSDJoinType** nella casella **Variabile**.  

    > [!NOTE]
    >  Questa variabile viene impostata su **0** per i computer aggiunti a un dominio e su **1** per quelli inclusi in un gruppo di lavoro.  

3.  Fare clic su **uguale a** nella casella **Condizione**.  

4.  Digitare **1** nella casella **Valore** e quindi fare clic su **OK**.  

### <a name="operating-system-version-in-conditions"></a>Condizione Versione del sistema operativo  
 Usare la condizione **Versione del sistema operativo** per verificare la versione del sistema operativo esistente di un computer di destinazione o del client esistente (durante l'acquisizione di un'immagine). Ad esempio, considerare una rete che contiene alcuni server che verranno aggiornati da Windows Server 2003 a Windows Server 2008. Le impostazioni di rete devono essere copiate e applicate solo ai server con Windows Server 2003. Tutti gli altri server useranno le impostazioni di rete predefinite usate da Windows Server 2008.  

 **Per aggiungere una condizione basata sulla versione del sistema operativo**  

1.  Fare clic sull'attività **Acquisisci impostazioni di rete** nell'editor delle sequenze di attività.  

2.  Fare clic su **Aggiungi condizione**, quindi su **Versione del sistema operativo**.  

3.  Fare clic sul server pertinente nella casella **Architettura**. Per questo esempio fare clic su **x86**.  

4.  Nella casella **Sistema operativo** scegliere il sistema operativo e la versione per cui si vuole impostare una condizione. Per questo esempio fare clic su **x86 Windows 2003**.  

5.  Nella casella **Condizione** selezionare la condizione pertinente e quindi fare clic su **OK**.  

### <a name="file-properties-in-conditions"></a>Condizione Proprietà file  
 Usare la condizione **Proprietà file** per verificare la versione e/o il timestamp di un determinato file per stabilire se è necessario eseguire un'attività o un gruppo di attività. In questo esempio l'ambiente di produzione contiene un'immagine di Windows Server 2003 che viene continuamente aggiornata e usata per ogni nuovo server aggiunto alla rete. Tutti i computer server nell'ambiente eseguono un'applicazione personalizzata che richiede l'API DAO (Digital Access Object) versione 3.60.6815.  

 Tutti i server esistenti funzionano correttamente. Tuttavia, ogni nuovo server aggiunto alla rete con l'immagine non è in grado di eseguire l'applicazione. Poiché è responsabilità di un altro gruppo gestire e aggiornare le immagini, si decide di modificare la sequenza di attività di distribuzione per installare la versione pertinente del DAO se la versione esistente del DAO distribuito con l'immagine non è corretta.  

 **Per aggiungere una condizione Proprietà file a un passaggio della sequenza di attività in Configuration Manager 2007 R3**  

1.  In Configuration Manager 2007 R3 creare un pacchetto per installare DAO 3.60.6815. Chiamare il pacchetto *DAO*, con un programma denominato *InstallDAO*. Per altre informazioni sulla creazione di pacchetti, vedere [Come creare un pacchetto](http://technet.microsoft.com/library/bb693627.aspx).  

2.  Creare un passaggio **Installa software** per distribuire il pacchetto DAO.  

3.  Fare clic sul passaggio **Installa software** della sequenza di attività creato nel passaggio 2 e quindi scegliere la scheda **Opzioni**.  

4.  Fare clic su **Aggiungi condizione**, quindi scegliere **Proprietà file**.  

5.  Nella casella **Percorso** digitare **C:\Programmi\Microsoft Shared\DAO\dao360.dll**.  

6.  Selezionare la casella di controllo **Controllare la versione** e quindi fare clic su **diverso da** per la condizione.  

7.  Nella casella **Versione** digitare **3.60.6815**.  

8.  In questo caso, deselezionare la casella di controllo **Controllare il timestamp** e quindi fare clic su **OK**.  

### <a name="folder-properties-in-conditions"></a>Condizione Proprietà cartella  
 Usare la condizione **Proprietà cartella** per verificare il timestamp di una determinata cartella per stabilire se è necessario eseguire un'attività o un gruppo di attività. Si consideri ad esempio una situazione in cui un'applicazione sviluppata internamente è stata aggiornata per funzionare con Windows 8. Tuttavia, la versione più recente dell'applicazione non è installata in tutti i computer nella rete ed è necessario eseguire un processo di conversione dei dati prima di aggiornare l'applicazione.  

 Se il timestamp della cartella in cui è installata l'applicazione è 12/31/2007 o precedente, la versione dell'applicazione eseguita nel computer di destinazione non è compatibile ed è necessario eseguire il processo di conversione dei dati in quel computer. Eseguire in modo condizionale un passaggio della sequenza di attività per eseguire il processo di conversione dei dati nei computer che usano una versione precedente dell'applicazione.  

 **Per aggiungere una condizione Proprietà cartella a un passaggio della sequenza di attività**  

1.  Nell'editor della sequenza di attività della console di Configuration Manager o di Deployment Workbench modificare ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività da modificare).  

2.  Creare un'attività **Riga di comando** per eseguire il processo di conversione dei dati.  

3.  Fare clic sull'attività creata nel passaggio 1.  

4.  Fare clic su **Aggiungi condizione**, quindi scegliere **Proprietà cartella**.  

5.  Nella casella **Percorso** digitare il percorso della cartella che contiene l'applicazione.  

6.  Selezionare la casella di controllo **Controllare il timestamp**.  

7.  Fare clic su **Minore o uguale a** per la condizione.  

8.  Nella casella **Data** fare clic su **12/31/2007**.  

9. Nella casella **Ora** fare clic su **12:00:00 AM** e quindi su **OK**.  

### <a name="registry-settings-in-conditions"></a>Condizione Impostazioni Registro di sistema  
 Usare la condizione **Impostazione Registro di sistema** per verificare l'esistenza di chiavi e valori nel registro e i dati corrispondenti archiviati nei valori del registro. Si consideri ad esempio un caso in cui un'applicazione attualmente usata in un piccolo set di computer non può essere eseguita in Windows 8 ed è in corso una distribuzione di Windows 8 al fine di aggiornare i computer che attualmente eseguono Windows XP. Creare una condizione nella prima attività di una sequenza per verificare se nel Registro di sistema è presente una voce per l'applicazione non compatibile e, se è presente, interrompere il processo di distribuzione per quel computer.  

 **Per aggiungere una condizione Proprietà Registro di sistema a un passaggio della sequenza di attività**  

1.  Nell'editor della sequenza di attività della console di Configuration Manager o di Deployment Workbench modificare ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività che distribuisce Windows 8).  

2.  Scegliere la prima attività della sequenza e quindi fare clic sulla scheda **Opzioni**.  

3.  Fare clic su **Aggiungi condizione**, quindi scegliere **Impostazione del Registro di sistema**.  

4.  Nell'elenco **Chiave radice** fare clic su **HKEY_LOCAL_MACHINE**.  

5.  Nella casella **Chiave** digitare **SOFTWARE\WOODGROVE**.  

6.  Fare clic su **non esiste** per la condizione. In questo caso, l'attività viene eseguita e la sequenza continua solo se la chiave non esiste.  

7.  Facoltativamente, la condizione può verificare la non esistenza di un valore se si digita il nome del valore nella casella **Nome valore**.  

8.  Se è stata usata una condizione diversa da **esiste/non esiste**, specificare un valore e un tipo di valore.  

9. Fare clic su **OK**.  

### <a name="wmi-queries-in-conditions"></a>Condizione Query WMI  
 Usare la condizione **Query WMI** per eseguire qualsiasi query WMI. La condizione viene valutata come True se la query restituisce almeno un risultato. Ad esempio, si consideri un team di distribuzione che deve aggiornare il sistema operativo di tutti i server il cui modello è Dell 1950. È possibile usare una query WMI per controllare il modello di ogni computer e procedere con la distribuzione solo se viene trovato il modello corretto.  

 **Per aggiungere una condizione Query WMI a un passaggio della sequenza di attività**  

1.  Nell'editor della sequenza di attività della console di Configuration Manager o di Deployment Workbench modificare ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività che eseguirà l'aggiornamento dei server).  

2.  Scegliere la prima attività della sequenza e quindi fare clic sulla scheda **Opzioni**.  

3.  Fare clic su **Aggiungi condizione**, quindi scegliere **Query WMI**.  

4.  Nella casella dello **spazio dei nomi WMI** digitare **root\cimv2**.  

5.  Nella casella **Query WQL** digitare **Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**. Fare clic su **OK**.  

### <a name="installed-software-in-conditions"></a>Condizione Software installato  
 Usare una condizione **Software installato** per verificare se una particolare parte del software è attualmente installata in un computer di destinazione. Questa condizione consente di valutare solo il software installato usando i file di Microsoft Installer (MSI). Ad esempio, si supponga di voler aggiornare il sistema operativo di tutti i server tranne quelli che eseguono Microsoft SQL Server 2012.  

 **Per aggiungere una condizione Software installato a un passaggio della sequenza di attività**  

1.  Nell'editor della sequenza di attività della console di Configuration Manager o di Deployment Workbench modificare ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività che eseguirà l'aggiornamento dei server).  

2.  Scegliere la prima attività della sequenza e quindi fare clic sulla scheda **Opzioni**.  

3.  Fare clic su **Aggiungi condizione**, quindi scegliere **Software installato**.  

4.  Fare clic su **Sfoglia** e quindi sul file MSI per SQL Server 2012.  

5.  Selezionare l'opzione che consente di indicare come computer di destinazione solo i computer che eseguono un **prodotto specifico**, in questo caso SQL Server 2012, e nessun'altra versione per il rilevamento da parte della query.  

6.  Fare clic su **OK**.  

### <a name="complex-conditions"></a>Condizioni complesse  
 È possibile raggruppare più condizioni usando le istruzioni **IF** per creare condizioni complesse. Si supponga ad esempio che un determinato passaggio debba essere eseguito solo per i computer Contoso 1950 con Windows Server 2003 o Windows Server 2008. Scritto come istruzione **IF** programmatica, il passaggio ha l'aspetto seguente:  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **Per aggiungere una condizione complessa**  

1.  Nell'editor della sequenza di attività della console di Configuration Manager o di Deployment Workbench modificare ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività che eseguirà l'aggiornamento dei server).  

2.  Fare clic sul passaggio della sequenza di attività a cui si aggiunge la condizione e quindi scegliere la scheda **Opzioni**.  

3.  Fare clic su **Aggiungi condizione**, su **Istruzione If**, quindi su **Tutte le condizioni**. Fare clic su **OK**.  

4.  Fare clic sull'istruzione condizionale, su **Aggiungi condizione** e quindi su **Query WMI**.  

5.  Verificare che sia specificato **root\cimv2** come spazio dei nomi WMI, quindi nella casella **Query WQL** digitare **SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**. Fare clic su **OK**.  

6.  Fare clic sull'istruzione **IF** e quindi scegliere **Aggiungi condizione**. Fare clic su **Istruzione If** e quindi su **Qualsiasi condizione**. Fare clic su **OK**.  

7.  Fare clic sulla seconda istruzione **IF**. Fare clic su **Aggiungi condizione**, quindi scegliere **Versione del sistema operativo**.  

8.  Nella casella **Architettura** scegliere l'architettura per i server. Per questo esempio fare clic su **x86**.  

9. Nella casella **Sistema operativo** scegliere il sistema operativo e la versione. Per questo esempio fare clic su **x86 Windows 2003 original release**. Fare clic su **OK**.  

10. Fare clic sulla seconda istruzione **IF**. Fare clic su **Aggiungi condizione**, quindi scegliere **Versione del sistema operativo**.  

11. Nella casella **Architettura** scegliere l'architettura per i server. Per questo esempio fare clic su **x86**.  

12. Nella casella **Sistema operativo** scegliere il sistema operativo e la versione. Per questo esempio fare clic su **x86 Windows 2008 original release**. Fare clic su **OK**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Creazione di un'infrastruttura di distribuzione LTI altamente scalabile  
 In questo scenario non è disponibile una distribuzione elettronica del software per l'infrastruttura di distribuzione, quindi si usa MDT per creare un'infrastruttura di distribuzione LTI completamente automatizzata. L'infrastruttura LTI scalabile usa le tecnologie di replica del file system distribuito (DFS) di SQL Server, Servizi di distribuzione Windows e Windows Server 2003.  

 Per ridimensionare l'infrastruttura LTI:  

-   Verificare che esista un'infrastruttura appropriata come descritto in [Verifica dell'esistenza di un'infrastruttura appropriata](#EnsureInfrastructure)  

-   Aggiungere contenuto a MDT come descritto in [Aggiunta di contenuto a MDT](#AddContent)  

-   Preparare Servizi di distribuzione Windows come descritto in [Preparazione di Servizi di distribuzione Windows](#PrepareDeployment)  

-   Configurare la replica del file system DFS come descritto in [Configurazione della replica del file system distribuito](#ConfigureFileReplication)  

-   Preparare la replica di SQL Server come descritto in [Preparazione per la replica di SQL Server](#PrepareSQLReplication)  

-   Configurare la replica di SQL Server come descritto in [Configurazione della replica di SQL Server](#ConfigureSQLReplication)  

 Questo scenario presuppone che MDT sia configurato in un server di distribuzione master e che la configurazione del database MDT sia già stata completata come descritto all'inizio di questo documento.  

###  <a name="EnsureInfrastructure"></a> Verifica dell'esistenza di un'infrastruttura appropriata  
 L'infrastruttura di distribuzione LTI altamente scalabile usa una topologia hub-and-spoke per la replica del contenuto. Di conseguenza, per prima cosa è necessario nominare nell'ambiente di produzione un server di distribuzione a cui assegnare il ruolo di server di distribuzione master.  Di seguito sono elencati i componenti necessari per il server di distribuzione master.  

 |**Componente obbligatorio** |**Scopo/commento** |  
 |-|-|  
 |Windows Server 2003 R2|Necessario per il supporto della replica del file system DFS|  
 |MDT |Contiene la copia master della condivisione di distribuzione|  
 |SQL Server 2005|Deve essere una versione completa per consentire la replica del database MDT|  
 |Replica del file system DFS |Necessaria per la replica della condivisione di distribuzione|  
 |Servizi di distribuzione Windows |Necessari per consentire l'avvio delle installazioni di rete basate su PXE|  

 Dopo aver selezionato il server di distribuzione master, eseguire il provisioning di server aggiuntivi in ogni sito per supportare le distribuzioni LTI.  Di seguito sono elencati i componenti obbligatori per il server di distribuzione figlio.  

 |**Componente obbligatorio** |**Scopo/commento** |  
 |-|-|  
 |Windows Server 2003 R2|Necessario per il supporto della replica del file system DFS|  
 |Microsoft SQL Server 2005 Express Edition |Riceve le copie replicate del database MDT|  
 |Replica del file system DFS |Richiesta per la replica della condivisione di distribuzione|  
 |Servizi di distribuzione Windows |Necessari per consentire l'avvio delle installazioni di rete basate su PXE|  

> [!NOTE]
>  Servizi di distribuzione Windows deve essere impostato e configurato in ogni server figlio, ma non è necessario aggiungere immagini di avvio o di installazione.  

###  <a name="AddContent"></a> Aggiunta di contenuto a MDT  
 Popolare il server di distribuzione master con contenuto usando Deployment Workbench e creare e popolare il database MDT, come descritto nelle sezioni seguenti. Per informazioni sul popolamento del database con:  

-   Applicazioni, vedere la sezione relativa alla configurazione delle applicazioni in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*  

-   Sistemi operativi, vedere la sezione relativa alla configurazione dei sistemi operativi in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*  

-   Pacchetti del sistema operativo, vedere la sezione relativa alla configurazione dei pacchetti in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*  

-   Driver di dispositivo, vedere la sezione relativa alla configurazione dei driver in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*  

-   Sequenze di attività, vedere la sezione relativa alla configurazione delle sequenze di attività in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*  

> [!NOTE]
>  Verificare che il file LiteTouchPE_x86.wim creato durante l'aggiornamento della condivisione di distribuzione sia stato aggiunto a Servizi di distribuzione Windows.  

###  <a name="PrepareDeployment"></a> Preparazione di Servizi di distribuzione Windows  
 Poiché il file LiteTouchPE_x86.wim viene periodicamente replicato attraverso il gruppo di replica del file system DFS, l'archivio dati di configurazione di avvio deve essere regolarmente aggiornato in modo da riflettere l'ambiente Windows PE appena replicato. Eseguire la procedura seguente per ogni server di distribuzione.  

 **Per preparare Servizi di distribuzione Windows**  

1.  Aprire una finestra del prompt dei comandi.  

2.  Digitare **WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60** e quindi premere INVIO.  

> [!NOTE]
>  Nell'esempio presentato qui il periodo di aggiornamento è impostato su 60 minuti. Tuttavia, è possibile configurare questo valore in modo che la replica abbia la stessa durata di quella del file system distribuito.  

###  <a name="ConfigureFileReplication"></a> Configurazione della replica del file system distribuito  
 Quando si ridimensiona l'architettura delle distribuzioni LTI, usare la replica del file system distribuito (DFS) come base per replicare il contenuto sia della condivisione di distribuzione MDT che dell'ambiente di avvio di Windows PE Lite Touch nonché dal server di distribuzione master ai server di distribuzione figlio.  

> [!NOTE]
>  Verificare che la replica del file system DFS sia installata prima di eseguire le operazioni riportate di seguito.  

 **Per configurare la replica del file system DFS per replicare il contenuto della distribuzione**  

1.  Aprire la console di gestione DFS.  

2.  Nella console di gestione DFS espandere Gestione DFS.  

3.  Fare clic con il pulsante destro del mouse su **Replica**, quindi scegliere **Nuovo gruppo di replica**.  

4.  Nella pagina **Tipo gruppo di replica** della Creazione guidata nuovo gruppo di replica selezionare il **gruppo di replica multifunzione**.  

5.  Fare clic su **Avanti**.  

6.  Nella pagina **Nome e dominio** digitare le informazioni seguenti:  

    -   Digitare un **nome per il gruppo di replica**, ad esempio **Gruppo di replica MDT 2010** nell'apposita casella.  

    -   Digitare una **descrizione facoltativa del gruppo di replica**, ad esempio **Gruppo per replica dati MDT 2010**, nell'apposita casella.  

    -   Verificare che la casella **Dominio** contenga il nome di dominio corretto.  

7.  Fare clic su **Avanti**.  

8.  Eseguire i passaggi seguenti nella pagina **Membri del gruppo di replica**:  

    1.  Fare clic su **Aggiungi**.  

    2.  Digitare i nomi di tutti i server che devono essere membri di questo gruppo di replica, ad esempio, tutti i server di distribuzione figlio e il server di distribuzione master.  

    3.  Fare clic su **OK**.  

9. Fare clic su **Avanti**.  

10. Nella pagina **Selezione topologia** fare clic su **Hub and Spoke** e quindi fare clic su **Avanti**.  

11. Nella pagina **Membri hub** fare clic sul server di distribuzione master e quindi scegliere **Aggiungi**.  

12. Fare clic su **Avanti**.  

13. Nella pagina delle **connessioni Hub and Spoke** verificare che per ogni server di distribuzione figlio sia indicato come server di distribuzione master il **membro hub obbligatorio**.  

14. Fare clic su **Avanti**.  

15. Nella pagina di **pianificazione e larghezza di banda del gruppo di replica** specificare una pianificazione per la replica del contenuto tra i server.  

16. Fare clic su **Avanti**.  

17. Nella casella **Membro primario** della pagina **Membro primario** fare clic sul server di distribuzione master.  

18. Fare clic su **Avanti**.  

19. Nella pagina **Folders to Replicate** (Cartelle da replicare) fare clic su **Aggiungi** ed eseguire le operazioni seguenti:  

    1.  Nella casella **Local Path of the folder to replicate** (Percorso locale della cartella da replicare) fare clic su **Sfoglia** per passare alla cartella *X:\\*Deployment (dove *X* è la lettera di unità nel server di distribuzione).  

    2.  Selezionare l'opzione che consente di **usare il nome basato sul percorso**.  

    3.  Fare clic su **OK**.  

    4.  Fare clic su **Aggiungi**.  

    5.  Nella finestra di dialogo **Add Folder to Replicate** (Aggiungi cartella da replicare) fare clic su **Sfoglia** per accedere alla cartella *X:* \RemoteInstall\Boot.  

    6.  Selezionare l'opzione che consente di **usare il nome basato sul percorso**.  

20. Fare clic su **Avanti**.  

21. Eseguire i passaggi seguenti nella pagina del **percorso di distribuzione locale per altri membri**:  

    1.  Selezionare tutti i membri del gruppo di distribuzione e quindi fare clic su **Modifica**.  

    2.  Nella finestra di dialogo **Edit Local Path** (Modifica percorso locale) fare clic su **Abilitato**.  

    3.  Digitare il percorso in cui deve essere archiviata la cartella della condivisione di distribuzione nel server di distribuzione figlio, ad esempio ***X:\Deployment*** (dove *X* è la lettera di unità nel server di distribuzione).  

    4.  Fare clic su **OK**.  

22. Fare clic su **Avanti**.  

23. Eseguire i passaggi seguenti nella pagina del **percorso di avvio locale per altri membri**:  

    1.  Selezionare tutti i membri del gruppo di distribuzione e quindi fare clic su **Modifica**.  

    2.  Nella finestra di dialogo **Edit Local Path** (Modifica percorso locale) fare clic su **Abilitato**.  

    3.  Digitare il percorso in cui deve essere archiviata la cartella di avvio nel server di distribuzione figlio, ad esempio ***X:\RemoteInstall\Boot*** (dove *X* è la lettera di unità nel server di distribuzione).  

    4.  Fare clic su **OK**.  

24. Fare clic su **Avanti**.  

25. Nella pagina **Remote Settings and Create Replication Group** (Impostazioni remote e creazione gruppo di replica) fare clic su **Crea** per completare la creazione guidata del gruppo di replica.  

26. Nella pagina **Conferma** fare clic su **Chiudi** per chiudere la procedura guidata.  

> [!NOTE]
>  Verificare che il nuovo gruppo di replica sia elencato sotto il nodo di replica.  

###  <a name="PrepareSQLReplication"></a> Preparazione per la replica di SQL Server  
 Per poter configurare la replica di SQL Server, è necessario completare alcuni passaggi di preconfigurazione per garantire che i server di distribuzione siano configurati correttamente.  

 **Per preparare la replica di SQL Server nel server di distribuzione master**  

1.  Creare una cartella per archiviare gli snapshot del database e quindi configurare la cartella come condivisione.  

    > [!NOTE]
    >  Per altre informazioni sulla protezione della cartella snapshot, vedere [Secure the Snapshot Folder](http://msdn2.microsoft.com/library/ms151151.aspx) (Proteggere la cartella snapshot).  

2.  Verificare che il servizio SQL Server Browser sia abilitato e impostato su Automatico.  

3.  Nella casella **Configurazione superficie di attacco di SQL Server** fare clic su **Local and Remote connections** (Connessioni locali e remote).  

 **Per preparare la replica di SQL Server nel server di distribuzione figlio**  

1.  Nella casella **Configurazione superficie di attacco di SQL Server** fare clic su **Local and Remote connections** (Connessioni locali e remote).  

2.  Facoltativamente, creare un database vuoto per ospitare il database MDT replicato.  

> [!NOTE]
>  Questo database deve avere lo stesso nome del database MDT nel server di distribuzione master. Ad esempio, se il database MDT nel server di distribuzione master è denominato *MDTDB*, creare un database vuoto denominato *MDTDB* nel server di distribuzione figlio.  

###  <a name="ConfigureSQLReplication"></a> Configurazione della replica di SQL Server  
 Dopo aver configurato la replica dei file e delle cartelle da usare per la compilazione dell'infrastruttura di distribuzione, configurare SQL Server per la replica del database MDT.  

> [!NOTE]
>  È anche possibile gestire un solo database centrale di MDT, se si gestisce una versione replicata del database MDT, si avrà un maggiore controllo sul trasferimento dei dati in tutta la rete WAN.  

 SQL Server 2005 usa un modello di replica simile al modello di distribuzione di una rivista:  

1.  Una *rivista* viene resa disponibile (pubblicata) da un *editore*.  

2.  Vengono usati dei *distributori* per distribuire la pubblicazione.  

3.  I *lettori* possono sottoscrivere una pubblicazione in modo che la pubblicazione venga periodicamente recapitata al sottoscrittore (una *sottoscrizione push*).  

 Questa terminologia viene usata nelle procedure guidate di impostazione e configurazione della replica di SQL Server.  

#### <a name="configure-a-sql-server-publisher"></a>Configurare un server di pubblicazione di SQL Server  
 Per configurare il server di distribuzione master come server di pubblicazione di SQL Server, eseguire questi passaggi:  

1.  Aprire SQL Server Management Studio.  

2.  Fare clic con il pulsante destro del mouse sul nodo **Replica** e quindi fare clic su **Configura distribuzione**.  

3.  Nella Configurazione guidata distribuzione fare clic su **Avanti**.  

4.  Nella pagina **Database di distribuzione** fare clic sull'opzione che consente di **impostare il server come database di distribuzione per se stesso e creare un database di distribuzione e un log in SQL Server**, quindi fare clic su **Avanti**.  

5.  Nella sezione **Preparazione per la replica di SQL Server** della pagina **Cartella snapshot** digitare il percorso UNC alla cartella snapshot creata.  

6.  Nella pagina **Database di distribuzione** fare clic su **Avanti**.  

7.  Nella pagina **Server di pubblicazione** fare clic sul server di distribuzione master per impostarlo come server di distribuzione e quindi fare clic su **Avanti**.  

8.  Nella pagina **Azioni procedura guidata** fare clic su **Configura distribuzione**, quindi scegliere **Avanti**.  

9. Fare clic su **Fine** e quindi fare clic su **Chiudi** al termine della procedura guidata.  

#### <a name="enable-the-mdt-db-for-replication"></a>Abilitare il database MDT per la replica  
 Per abilitare il database MDT per la replica nel server di distribuzione master, eseguire questi passaggi:  

1.  In SQL Server Management Studio fare clic con il pulsante destro del mouse sul nodo **Replica** e quindi fare clic su **Proprietà server di pubblicazione**.  

2.  Nella pagina **Proprietà server di pubblicazione** eseguire le operazioni riportate di seguito:  

    1.  Fare clic su **Database del server di pubblicazione**.  

    2.  Fare clic sul database MDT e quindi su **Transazionale**.  

    3.  Fare clic su **OK**.  

 Il database MDT è ora configurato per la replica transazionale e snapshot.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Creare una pubblicazione del database MDT  
 Per creare una pubblicazione del database MDT per cui i server di distribuzione figlio possono eseguire la sottoscrizione, attenersi a questa procedura:  

1.  In SQL Server Management Studio espandere Replica, fare clic con il pulsante destro del mouse su **Pubblicazioni locali** e quindi fare clic su **Nuova pubblicazione**.  

2.  Nella Creazione guidata nuova pubblicazione fare clic su **Avanti**.  

3.  Nella pagina **Database di pubblicazione** fare clic sul database MDT e quindi scegliere **Avanti**.  

4.  Nella pagina **Tipo di pubblicazione** fare clic su **Pubblicazione snapshot** e quindi su **Avanti**.  

5.  Nella pagina **Articoli** selezionare **Tabelle, Stored procedure** e **Visualizzazioni** e quindi fare clic su **Avanti**.  

6.  Nella pagina **Problemi articoli** fare clic su **Avanti**.  

7.  Nella pagina **Filtro righe tabella** fare clic su **Avanti**.  

8.  Nella pagina **Agente di snapshot** eseguire queste operazioni:  

    1.  Selezionare **Crea uno snapshot immediatamente e mantieni lo snapshot disponibile per l'inizializzazione delle sottoscrizioni**.  

    2.  Fare clic su **Usa la pianificazione seguente per l'esecuzione dell'agente snapshot**.  

    3.  Fare clic su **Cambia**.  

    > [!NOTE]
    >  Specificare una pianificazione che avrà luogo un'ora prima della replica del database.  

9. Fare clic su **Avanti**.  

10. Nella pagina **Sicurezza agente** fare clic sull'account in cui verrà eseguito l'agente di snapshot e quindi fare clic su **Avanti**.  

11. Nella pagina **Azioni procedura guidata** fare clic su **Crea la pubblicazione**, quindi scegliere **Avanti**.  

12. Nella pagina di **completamento della procedura guidata** digitare un nome descrittivo nella casella del **nome della pubblicazione**.  

13. Fare clic su **Fine** per completare la procedura guidata e quindi fare clic su **Chiudi** quando la procedura guidata ha creato la pubblicazione.  

    > [!NOTE]
    >  La pubblicazione ora sarà visibile sotto il nodo delle pubblicazioni locali in SQL Server Management Studio.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Sottoscrivere server di distribuzione figlio per il database MDT pubblicato  
 Ora che il database MDT è stato pubblicato, è possibile aggiungere i server di distribuzione figlio come sottoscrittori per questa pubblicazione. Ciò significa che riceveranno una copia del database in base a una pianificazione, in modo che durante una distribuzione i computer client siano in grado di eseguire query su un database locale per la rete anziché passare attraverso la rete WAN.  

 **Per sottoscrivere i server di distribuzione figlio per la pubblicazione del database MDT**  

1.  In SQL Server Management Studio andare Replica/Pubblicazioni locali.  

2.  Fare clic con il pulsante destro del mouse sulla pubblicazione creata nella sezione precedente e quindi fare clic su **nuove sottoscrizioni**.  

3.  Nella creazione guidata delle sottoscrizioni fare clic su **Avanti**.  

4.  Nella pagina **Pubblicazione** fare clic sulla pubblicazione creata nella sezione precedente.  

5.  Nella pagina **Posizione in cui eseguire l'agente di distribuzione** fare clic su **Esegui tutti gli agenti nel database di distribuzione NOMESERVER (sottoscrizioni push)** e quindi fare clic su **Avanti**.  

6.  Nella pagina **Sottoscrittori** aggiungere ogni server di distribuzione figlio attenendosi alla procedura seguente:  

    1.  Fare clic su **Aggiungi sottoscrittore**, e quindi fare clic su **Aggiungi sottoscrittore SQL Server**.  

    2.  Aggiungere ogni server di distribuzione figlio.  

    3.  Per ogni server di distribuzione figlio aggiunto, nella casella **Database di sottoscrizione** fare clic sul database MDT vuoto in quel server di distribuzione figlio.  

    > [!NOTE]
    >  Se il database MDT vuoto non è ancora stato creato, selezionare l'opzione che consente di creare un nuovo database nella casella **Database di sottoscrizione**.  

    > [!NOTE]
    >  Questo database deve avere lo stesso nome del database MDT nel server di distribuzione master. Ad esempio, se il database MDT nel server di distribuzione master è denominato *MDTDB*, creare un database vuoto denominato *MDTDB* nel server di distribuzione figlio.  

7.  Fare clic su **Avanti**.  

8.  Nella pagina **Sicurezza agente di distribuzione** fare clic su **...** per aprire la finestra di dialogo **Sicurezza agente di distribuzione**.  

9. Digitare i dettagli dell'account da usare per l'agente di distribuzione e quindi fare clic su **Avanti**.  

10. Eseguire le operazioni riportate di seguito nella pagina **Pianificazione della sincronizzazione**:  

    1.  Nella casella **Pianificazione agente** fare clic su **<Definizione pianificazione\>**.  

    2.  Specificare la pianificazione che deve essere usata per replicare il database tra i server di distribuzione master e figlio e quindi fare clic su **Avanti**.  

11. Nella pagina di **inizializzazione della sottoscrizione** fare clic su **Avanti**.  

12. Nella pagina **Azioni procedura guidata** fare clic su **Crea le sottoscrizioni**, quindi scegliere **Avanti**.  

13. Fare clic su **Fine** e quindi fare clic su **Chiudi** al termine della procedura guidata.  

 La replica di SQL Server è ora configurata e il database MDT verrà replicato dal server di distribuzione master in tutti i server di distribuzione figlio sottoscritti su base periodica.  

#### <a name="configure-customsettingsini"></a>Configurare CustomSettings.ini  
 L'infrastruttura di distribuzione LTI ora è stata creata correttamente e ogni posizione conterrà un server di distribuzione LTI, con una copia replicata di:  

-   Condivisione di distribuzione  

-   Database MDT  

-   Ambiente Windows PE LiteTouchPE_x86 che è stato aggiunto a Servizi di distribuzione Windows  

 A questo punto è possibile configurare il file CustomSettings.ini in modo che la condivisione di distribuzione usi il contenuto della distribuzione (condivisione di distribuzione e database) dal proprio server di distribuzione locale, il server che rende disponibile l'ambiente LiteTouchPE_x86.wim in Servizi di distribuzione Windows.  

 Quando il file LiteTouchPE_x86.wim viene recapitato da Servizi di distribuzione Windows, una chiave del Registro di sistema viene configurata con il nome del server di Servizi di distribuzione Windows in uso. MDT acquisisce il nome del server in una variabile (%WDSServer%) che è possibile usare per configurare CustomSettings.ini.  

 **Per usare sempre il server di distribuzione LTI locale**  

> [!NOTE]
>  La procedura seguente presuppone che la condivisione di distribuzione sia stata creata e impostata come condivisione Deployment$.  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Regole** e quindi modificare il file CustomSettings.ini per configurare le proprietà seguenti:  

    -   Per ogni sezione di SQL Server aggiunta, configurare **SQLServer** in modo che usi il nome del server **%WDSServer%**, ad esempio **SQLServer=%WDSServer%**.  

    -   Se si configura **DeployRoot**, configurare **DeployRoot** in modo che usi la variabile **%WDSServer%**, ad esempio **DeployRoot=\\\\%WDSServer%\Deployment$**.  

5.  Fare clic su **Edit Bootstrap.ini** (Modifica Bootstrap.ini).  

6.  Configurare BootStrap.ini in modo che usi la proprietà **%WDSServer%** aggiungendo o modificando il valore **DeployRoot** in **DeployRoot=\\\\%WDSServer%\Deployment$**.  

7.  Fare clic su **File**, quindi su **Salva** per salvare le modifiche apportate al file BootStrap.ini.  

8.  Fare clic su **OK**.  

     La condivisione di distribuzione e l'ambiente Windows PE LiteTouchPE_x86.wim devono essere aggiornati.  

9. Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

10. Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

11. Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

12. Fare clic su **Fine** nella pagina **Conferma**.  

 L'esempio seguente illustra CustomSettings.ini dopo l'esecuzione della procedura descritta in questa sezione.  

 **Esempio di CustomSettings.ini configurato per l'infrastruttura di distribuzione LTI scalabile**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Selezione di un server MDT locale quando sono presenti più server  
 In questo scenario vengono usati più server MDT per supportare un volume elevato di distribuzioni simultanee e distribuzioni in più siti. Quando una distribuzione LTI viene inizializzata, il comportamento predefinito è richiedere un percorso al server MDT per connettersi e accedere ai file necessari per iniziare il processo di distribuzione.  

 La distribuzione guidata di Windows è in grado di usare il file LocalServer.xml per presentare una scelta di server di distribuzione noti per ogni posizione.  

 Per usare il file LocationServer.xml:  

-   Comprendere le finalità e l'uso di LocationServer.xml come descritto in [Informazioni su LocationServer.xml](#UnderstandingLocationServer)  

-   Creare il file LocationServer.xml come descritto in [Creazione del file LocationServer.xml](#CreateLocationServer)  

-   Aggiungere il file LocationServer.xml alla directory dei file aggiuntivi, come descritto in Aggiunta del file LocationServer.xml alla directory dei file aggiuntivi  

-   Aggiornare il file BootStrap.ini come descritto in [Aggiornamento del file BootStrap.ini](#UpdateBootstrap)  

-   Aggiornare la condivisione di distribuzione come descritto in [Aggiornamento della condivisione di distribuzione](#UpdateDeploymentShare)  

 In questo scenario si presuppone che MDT sia configurato in un server di distribuzione.  

###  <a name="UnderstandingLocationServer"></a> Informazioni su LocationServer.xml  
 Per prima cosa è necessario comprendere in che modo MDT usa LocationServer.xml. Durante la distribuzione LTI, gli script MDT leggono ed elaborano il file BootStrap.ini per raccogliere le informazioni iniziali sulla distribuzione. Ciò si verifica prima che venga stabilita una connessione al server di distribuzione. Di conseguenza, normalmente si usa la proprietà **DeployRoot** per specificare nel file BootStrap.ini il server di distribuzione a cui si deve stabilire una connessione.  

 Se il file BootStrap.ini non contiene una proprietà **DeployRoot**, gli script MDT caricano una pagina della procedura guidata per richiedere all'utente un percorso al server di distribuzione. Durante l'inizializzazione della pagina **Applicazione HTML (HTA)** della procedura guidata, gli script MDT verificano l'esistenza del file LocationServer.xml e, se presente, usano LocationServer.xml per visualizzare i server di distribuzione disponibili.  

#### <a name="understand-when-to-use-locationserverxml"></a>Quando si deve usare LocationServer.xml  
 MDT offre diversi modi per determinare a quale server connettersi durante una distribuzione LTI. Alcuni metodi di individuazione del server di distribuzione sono più adatti a determinati scenari, quindi è importante capire quando usare LocationServer.xml.  

 In MDT sono disponibili diversi metodi per individuare e usare automaticamente il server di distribuzione più appropriato. Questi metodi sono elencati nella tabella seguente.

 |**Metodo** |**Informazioni dettagliate** |  
 |-|-|  
 |**%WDSServer%** |Questo metodo viene usato quando il server MDT è co-ospitato nel server di Servizi di distribuzione Windows.<br /><br /> Quando si avvia una distribuzione LTI da Servizi di distribuzione Windows, la variabile di ambiente %WDSServer% viene creata e popolata con il nome del server di Servizi di distribuzione Windows.<br /><br /> La variabile **DeployRoot** usa questa variabile per connettersi automaticamente a una condivisione di distribuzione nel server di Servizi di distribuzione Windows, ad esempio:<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Automazione basata sulla posizione** |MDT è in grado di usare l'automazione basata sulla posizione nel file BootStrap.ini per identificare il server per cui eseguire la distribuzione.<br /><br /> Usare la proprietà **Gateway predefinito** per distinguere posizioni diverse, ovvero per ogni **Gateway predefinito** viene specificato un diverso server MDT.<br /><br /> Per altre informazioni sull'uso dell'automazione basata sulla posizione, fare riferimento alla sezione relativa alla selezione dei metodi di applicazione delle impostazioni di configurazione.|  

 Ogni approccio elencato nella tabella precedente offre un modo per automatizzare la selezione del server di distribuzione in una posizione specifica per determinati scenari. Questi approcci sono destinati a scenari specifici, ad esempio quando il server MDT è co-ospitato con Servizi di distribuzione Windows.  

 Esistono altri scenari in cui questi approcci non sono adatti, ad esempio se sono presenti più server di distribuzione in un determinato percorso oppure la logica di automazione non è possibile (ad esempio, la rete non è abbastanza segmentata da consentire la determinazione della posizione o il server MDT è separato da Servizi di distribuzione Windows).  

 In questi scenari il file LocationServer.xml offre un modo flessibile per presentare le informazioni in fase di distribuzione senza richiedere la conoscenza dei nomi dei server e delle condivisioni di distribuzione.  

###  <a name="CreateLocationServer"></a> Creazione del file LocationServer.xml  
 Per presentare un elenco di server di distribuzione disponibili durante una distribuzione LTI, creare un file LocationServer.xml che contiene informazioni dettagliate su ogni server. Non esiste un file LocationServer.xml predefinito in MDT, creane uno usando le linee guida seguenti.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Creare un file LocationServer.xml per supportare più posizioni  
 Il metodo più semplice per creare e usare LocationServer.xml consiste nel creare un file LocationServer.xml e aggiungere le voci relative a ogni server di distribuzione nell'ambiente (nella stessa posizione o in posizioni diverse).  

 Per costruire il file LocationServer.xml, creare una nuova sezione per ogni server e aggiungere le informazioni seguenti:  

-   Un identificatore univoco  

-   Un nome di posizione, usato per presentare un nome facilmente identificabile per quella posizione  

-   Un percorso UNC al server MDT per quella posizione  

 Di seguito viene spiegato come si crea il file LocationServer.xml usando ognuna di queste proprietà e un file LocationServer.xml di esempio configurato per più posizioni.  

 **Esempio di file LocationServer.xml per supportare più posizioni**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Usando questo formato, specificare diverse voci di server per ogni posizione o per situazioni in cui sono presenti più server all'interno di un'unica posizione, specificando una voce di server diversa per ogni server in quella posizione, come illustrato nell'esempio seguente.   

 **Esempio di file LocationServer.xml per supportare più server in più posizioni**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Creare un file LocationServer.xml per bilanciare il carico di più server in posizioni diverse  
 Usando LocationServer.xml, specificare più server per ogni voce di posizione, quindi eseguire un bilanciamento del carico di base in modo che quando viene scelta una posizione, MDT seleziona automaticamente un server di distribuzione dall'elenco dei server disponibili. Per rendere disponibile questa funzionalità, il file LocationServer.xml supporta la definizione di una metrica di peso.  

 Di seguito viene illustrato un esempio di file LocationServer.xml configurato per più server in posizioni diverse.  

 **Esempio di file LocationServer.xml per posizioni diverse**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Specificare la metrica di peso usando il tag <server weight\>, che MDT usa nel processo di selezione dei server. La probabilità che un server venga selezionato viene calcolata in base a:  

 **Peso del server/somma di tutti i pesi dei server**  

 Nell'esempio precedente i tre server nella sede centrale di Contoso sono indicati come 1, 2 e 4. La probabilità che un server con peso 2 venga selezionato diventa 2 su 7. Di conseguenza, per usare il sistema di ponderazione, determinare la capacità dei server disponibili in una posizione e pesare ogni server in base alla capacità del server rispetto a ognuno degli altri server.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Aggiunta del file LocationServer.xml alla directory dei file aggiuntivi  
 Dopo aver creato il file LocationServer.xml, aggiungerlo alle immagini di avvio LiteTouch_x86 e LiteTouch_x64 di Windows PE nella cartella ***X:\\Deploy\Control***. Usando Deployment Workbench, aggiungere altri file e cartelle a tali immagini Windows PE specificando un'altra directory da aggiungere alle proprietà della condivisione di distribuzione.  

 **Per aggiungere LocationServer.xml alla condivisione di distribuzione**  

1.  Creare una cartella denominata *Extra Files* nella cartella della condivisione di distribuzione radice, ad esempio, D:\Production Share\Extra Files.  

2.  Creare una struttura di cartelle nella cartella Extra Files che rispecchi la posizione di Windows PE in cui deve trovarsi il file aggiuntivo.  

     Ad esempio, il file LocationServer.xml deve trovarsi nella cartella \Deploy\Control in Windows PE. Creare quindi la stessa struttura di cartelle in Extra Files, ad esempio D:\Production Deployment Share\Extra Files\Deploy\Control).  

3.  Copiare LocationServer.xml nella cartella *condivisione_distribuzione*\Extra Files\Deploy\Control (dove *condivisione_distribuzione* è il percorso completo alla cartella radice della condivisione di distribuzione).  

4.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

5.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

6.  Nel riquadro Azioni fare clic su **Proprietà**.  

7.  Nella finestra di dialogo ***Proprietà condivisione_distribuzione*** (dove condivisione_distribuzione è il nome della condivisione di distribuzione) eseguire questi passaggi:  

    1.  Fare clic sulla scheda **Impostazioni piattaforma Windows PE** (dove *piattaforma* è l'architettura dell'immagine Windows PE da configurare).  

    2.  Nella casella **personalizzazioni di Windows PE** nella sezione il **Extra directory to add** (Directory supplementare da aggiungere) digitare ***percorso*** (dove *percorso* è il percorso completo alla cartella Extra Files, ad esempio, D:\Production Deployment Share\Extra Files), quindi fare clic su **OK**.  

###  <a name="UpdateBootstrap"></a> Aggiornamento del file BootStrap.ini  
 Quando si crea una condivisione di distribuzione usando Deployment Workbench, una proprietà **DeployRoot** viene automaticamente creata e popolata nel file BootStrap.ini. Poiché il file LocationServer.xml viene usato per popolare la proprietà **DeployRoot**, è necessario rimuovere questo valore dal file BootStrap.ini.  

 **Per rimuovere la proprietà DeployRoot da BootStrap.ini**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Nella finestra di dialogo ***Proprietà condivisione_distribuzione*** (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione) fare clic sulla scheda **Regole** e quindi scegliere **BootStrap.ini**.  

5.  Rimuovere il valore **DeployRoot**, ad esempio **DeployRoot=\\\Server\Deployment$**.  

6.  Fare clic su **File**, quindi su **Salva** per salvare le modifiche apportate al file BootStrap.ini.  

7.  Fare clic su **OK** per inviare le modifiche.  

###  <a name="UpdateDeploymentShare"></a> Aggiornamento della condivisione di distribuzione  
 La condivisione di distribuzione deve essere aggiornata per generare un nuovo ambiente di avvio LiteTouch_x86 e LiteTouch_x64 che contiene il file LocationServer.xml e il file BootStrap.ini aggiornato.  

 **Per aggiornare la condivisione di distribuzione**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

4.  Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

5.  Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

6.  Fare clic su **Fine** nella pagina **Conferma**.  

> [!NOTE]
>  Al termine del processo di aggiornamento, aggiungere i nuovi ambienti LiteTouch_x86 e LiteTouch_x64 di Windows PE in Servizi di distribuzione Windows o masterizzarli sui supporti di avvio da usare durante la distribuzione.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Sostituzione di un computer esistente con un nuovo computer usando l'installazione Lite Touch  
 È possibile usare MDT per distribuire un'immagine in un nuovo computer che sostituisca un computer esistente nell'architettura aziendale. Questa situazione può verificarsi durante l'aggiornamento da un sistema operativo a un altro (un nuovo sistema operativo può richiedere nuovo hardware) o se l'organizzazione necessita di computer più nuovi e più veloci per le applicazioni esistenti.  

 Quando si sostituisce un computer esistente con un nuovo computer, è consigliabile prendere in considerazione tutte le impostazioni che verranno migrate da un computer all'altro, ad esempio gli account utente e i dati di stato utente. Inoltre è importante creare una soluzione di ripristino in caso la migrazione abbia esito negativo.  

 In questa distribuzione di esempio il computer esistente (WDG-EXIST-01) viene sostituito da un nuovo computer (WDG-NEW-02) nel dominio CORP attraverso l'acquisizione dei dati di stato utente da WDG-EXIST-01 e il salvataggio dei dati in una condivisione di rete. Quindi, si distribuisce un'immagine esistente in WDG-NEW-02 e infine si ripristinano i dati di stato utente acquisiti in WDG-NEW-02. La distribuzione verrà eseguita da un server di distribuzione (WDG-MDT-01).  

 In MDT usare il modello di sequenza di attività di sostituzione del client standard per creare una sequenza di attività che esegua tutte le attività di distribuzione necessarie.  

 In questa dimostrazione si presuppone che:  

-   MDT sia stato installato nel server di distribuzione (WDG MDT 01)  

-   La condivisione di distribuzione sia già stata creata e popolata, incluse le immagini del sistema operativo, le applicazioni e i driver di dispositivo  

-   Un'immagine di un computer di riferimento sia già stata acquisita e venga distribuita al nuovo computer (WDG NEW 02)  

-   Una cartella condivisa di rete (UserStateCapture$) sia stata creata e condivisa nel server di distribuzione (WDG MDT 01) con le autorizzazioni appropriate per la condivisione  

 Deve esistere una condivisione di distribuzione prima di iniziare questo esempio. Per altre informazioni sulla creazione di una condivisione di distribuzione, vedere la sezione relativa alla gestione delle condivisioni di distribuzione in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Passaggio 1: creare una sequenza di attività per acquisire lo stato utente  
 Creare sequenze di attività di MDT nel nodo delle sequenze di attività di Deployment Workbench usando la Creazione guidata sequenza di attività. Per eseguire la prima parte dello scenario di distribuzione Replace Computer (con acquisizione dello stato utente nel computer esistente), selezionare il modello Standard Client Replace Task Sequence nella Creazione guidata sequenza di attività.  

 **Per creare una sequenza di attività per acquisire lo stato utente nello scenario di distribuzione Replace Computer**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Nuova sequenza di attività**.  

     Viene avviata la Creazione guidata sequenza di attività.  

4.  Completare la Creazione guidata sequenza di attività usando le informazioni seguenti. Accettare i valori predefiniti se non diversamente specificato.  

    |**In questa pagina della procedura guidata** |**Eseguire questa operazione** |  
    |-|-|  
    |**Impostazioni generali** |1.  In **ID sequenza di attività** digitare **VISTA_EXIST**.<br />2.  Come **nome della sequenza di attività** digitare **Perform Replace Computer Scenario on Existing Computer** (Esegui scenario di sostituzione computer nel computer esistente).<br />3.  Fare clic su **Avanti**.|  
    |**Seleziona modello** |**Sono disponibili diversi modelli di sequenza di attività**. **Selezionare come modello da usare come punto di partenza** **Standard Client Replace Task Sequence** (Sequenza di attività di sostituzione client standard), quindi fare clic su **Avanti**.|  
    |**Riepilogo** |Verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.|  
    |**Conferma** |Fare clic su **Fine**.|  

 La creazione guidata sequenza di attività viene completata e la sequenza di attività **VISTA_EXIST** viene aggiunta all'elenco delle sequenze di attività.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Passaggio 2: creare una sequenza di attività per distribuire il sistema operativo e ripristinare lo stato utente  
 Creare sequenze di attività di MDT nel nodo delle sequenze di attività di Deployment Workbench usando la Creazione guidata sequenza di attività. Per eseguire la seconda parte dello scenario di distribuzione Replace Computer (distribuzione del sistema operativo e ripristino dello stato utente nel computer esistente), selezionare il modello Standard Client Task Sequence nella Creazione guidata sequenza di attività.  

 **Per creare una sequenza di attività per distribuire lo stato utente nello scenario di distribuzione Replace Computer**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Nuova sequenza di attività**.  

     Viene avviata la Creazione guidata sequenza di attività.  

4.  Completare la Creazione guidata sequenza di attività usando le informazioni seguenti. Accettare i valori predefiniti se non diversamente specificato.  

    |**In questa pagina della procedura guidata**|**Eseguire questa operazione**|  
    |-|-|  
    |**Impostazioni generali**|1.  In **ID sequenza di attività** digitare **VISTA_NEW**.<br />2.  Come **nome della sequenza di attività** digitare **Perform Replace Computer Scenario on New Computer** (Esegui scenario di sostituzione computer nel nuovo computer).<br />3.  Fare clic su **Avanti**.|  
    |**Seleziona modello**|**Sono disponibili diversi modelli di sequenza di attività**. **Selezionare come modello da usare come punto di partenza** **Standard Client Task Sequence** (Sequenza di attività client standard), quindi fare clic su **Avanti**.|  
    |**Seleziona immagine SO**|In quest'area sono elencate **le immagini del sistema operativo disponibili per la distribuzione con questa sequenza di attività**. Selezionare un'immagine, selezionare ***immagine_vista_acquisita*** (dove *imamgine_vista_acquisita* è l'immagine acquisita del computer di riferimento aggiunto al nodo Operating Systems in Deployment Workbench), quindi fare clic su *Avanti*.|  
    |**Specificare il codice Product Key**|Scegliere di **non specificare un codice Product Key in questo momento** e quindi fare clic su **Avanti**.|  
    |Impostazioni del sistema operativo|1.  In **Nome e cognome** digitare **Woodgrove Employee**.<br />2.  In **Organizzazione** digitare **Woodgrove Bank**.<br />3.  In **Home Page di Internet Explorer** digitare **http://www.woodgrovebank.com**.<br />4.  Fare clic su **Avanti**.|  
    |**Password amministratore**|Nei campi di **immissione della password dell'amministratore** e di **conferma della password dell'amministratore** digitare **P@ssw0rd**, quindi fare clic su **Fine**.|  
    |**Conferma**|Fare clic su **Fine**.|  

 La Creazione guidata sequenza di attività viene completata e la sequenza di attività **VISTA_NEW** viene aggiunta all'elenco delle sequenze di attività.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Passaggio 3: personalizzare i file di configurazione di MDT  
 Dopo aver creato la sequenza di attività di MDT, personalizzare i file di configurazione di MDT che specificano le impostazioni di configurazione per l'acquisizione delle informazioni sullo stato utente. In particolare, personalizzare il file CustomSettings.ini modificando il file nelle proprietà della condivisione di distribuzione creata in precedenza nel processo di distribuzione. In un passaggio successivo, la condivisione di distribuzione verrà aggiornata per garantire che il file di configurazione sia aggiornato nella condivisione di distribuzione.  

 **Per personalizzare i file di configurazione di MDT per l'acquisizione delle informazioni sullo stato utente**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

     Viene visualizzata la finestra di dialogo **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** scegliere la scheda **Regole**.  

5.  Nella scheda **Regole** modificare il file CustomSettings.ini in modo che rifletta le modifiche necessarie, come illustrato nell'esempio seguente. Apportare eventuali altre modifiche richieste dall'ambiente.  

     **File CustomSettings.ini personalizzato**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  Nella finestra di dialogo **Proprietà** fare clic su **OK**.  

7.  Chiudere tutte le finestre e finestre di dialogo aperte.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Passaggio 4: configurare le opzioni di Windows PE per la condivisione di distribuzione  
 Configurare le opzioni di Windows PE per la condivisione di distribuzione nel nodo delle condivisioni di distribuzione di Deployment Workbench.  

> [!NOTE]
>  Se i driver di dispositivo per il computer esistente (WDG-EXIST-01) e il nuovo computer (WDG-NEW-01) sono inclusi in Windows Vista, saltare questo passaggio e continuare con il passaggio seguente.  

 **Per configurare le opzioni di Windows PE per la condivisione di distribuzione**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

     Viene visualizzata la finestra di dialogo **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà**, nella scheda **Componenti *piattaforma* Windows PE** (dove *piattaforma* è l'architettura dell'immagine di Windows PE da configurare), in **Selection profile** (Profilo selezione) selezionare ***driver_dispositivo*** (dove *driver_dispositivo* corrisponde al nome del profilo di selezione dei driver di dispositivo), quindi fare clic su **OK**.  

### <a name="step-5-update-the-deployment-share"></a>Passaggio 5: aggiornare la condivisione di distribuzione  
 Dopo aver configurato le opzioni di Windows PE per la condivisione di distribuzione, aggiornare la condivisione di distribuzione. Aggiornando la condivisione di distribuzione si aggiornano tutti i file di configurazione di MDT e viene generata una versione personalizzata di Windows PE. La versione personalizzata di Windows PE viene usata per avviare il computer di riferimento e il processo di distribuzione LTI.  

 **Per aggiornare la condivisione di distribuzione in Deployment Workbench**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione) nel riquadro Azioni.  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

4.  Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

5.  Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

6.  Fare clic su **Fine** nella pagina **Conferma**.  

 Deployment Workbench avvia l'aggiornamento della condivisione di distribuzione. Deployment Workbench crea i file LiteTouchPE_x86.iso e LiteTouchPE_x86.wim (per i computer di destinazione a 32 bit) o i file LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (per i computer di destinazione a 64 bit) nella cartella *condivisione_distribuzione*\Boot (dove *condivisione_distribuzione* è la cartella condivisa usata come condivisione di distribuzione).  

### <a name="step-6-create-the-lti-bootable-media"></a>Passaggio 6: creare i supporti di avvio LTI  
 Specificare un metodo per l'avvio del computer con la versione personalizzata di Windows PE creata durante l'aggiornamento della condivisione di distribuzione. Deployment Workbench crea i file LiteTouchPE_x86.iso e LiteTouchPE_x86.wim (per i computer di destinazione a 32 bit) o i file LiteTouchPE_x64.iso e LiteTouchPE_x64.wim (per i computer di destinazione a 64 bit) nella cartella *condivisione_distribuzione*\Boot (dove *condivisione_distribuzione* è la cartella condivisa usata come condivisione di distribuzione). Creare i supporti di avvio LTI appropriati da una di queste immagini.  

 **Per creare i supporti di avvio LTI**  

1.  In Esplora risorse passare alla cartella *condivisione_distribuzione*\Boot (dove *condivisione_distribuzione* è la cartella condivisa usata come la condivisione di distribuzione).  

2.  In base al tipo di computer usato per il computer esistente (WDG-EXIST-01) e il nuovo computer (WDG-NEW-02), eseguire una delle attività seguenti:  

    -   Se il computer di riferimento è un computer fisico, creare un CD o DVD del file ISO.  

    -   Se il computer di riferimento è una macchina virtuale, avviare la macchina virtuale direttamente dal file ISO o da un CD o DVD del file ISO.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Passaggio 7: avviare il computer esistente con il supporto di avvio LTI  
 Avviare il computer esistente (WDG-EXIST-01) con il supporto di avvio LTI creato in precedenza nel processo. Questo CD consente di avviare Windows PE nel computer esistente e avvia il processo di distribuzione di MDT. Al termine del processo di distribuzione di MDT, le informazioni relative alla migrazione dello stato utente vengono archiviate nella cartella condivisa UserStateCapture$.  

> [!NOTE]
>  È anche possibile avviare il processo di MDT avviando il computer di destinazione da Servizi di distribuzione Windows. Per altre informazioni, vedere la sezione relativa alla preparazione di Servizi di distribuzione Windows nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

 **Per avviare il computer esistente con il supporto di avvio LTI**  

1.  Avviare il computer WDG-EXIST-01 con il supporto di avvio creato in precedenza nel processo.  

     Dopo l'avvio di Windows PE viene avviata anche distribuzione guidata di Windows.  

2.  Completare la distribuzione guidata di Windows usando le informazioni seguenti. Accettare i valori predefiniti se non diversamente specificato.  

    |**In questa pagina della procedura guidata**|**Eseguire questa operazione**|  
    |-|-|  
    |**Pagina iniziale della distribuzione**|Fare clic su **Run the Deployment Wizard** (Esegui distribuzione guidata) per installare un nuovo sistema operativo e quindi fare clic su **Avanti**.|  
    |**Specificare le credenziali per la connessione alle condivisioni di rete.**|1.  In **Nome utente** digitare **Amministratore**.<br />2.  In **Password** digitare **P@ssw0rd**.<br />3.  In **Dominio** digitare **CORP**.<br />4.  Fare clic su **OK**.|  
    |**Selezionare una sequenza di attività da eseguire in questo computer.**|Fare clic su *Perform Replace Computer Scenario on Existing Computer* (Esegui scenario di sostituzione computer nel computer esistente) e fare clic su **Avanti**.|  
    |**Specificare dove salvare i dati e le impostazioni**|Fare clic su **Avanti**.|  
    |**Specificare dove salvare un backup completo del computer**|Scegliere di **non eseguire il backup del computer esistente** e quindi fare clic su **Avanti**.|  
    |**Pronto a iniziare**|Fare clic su **Inizio**.|  

     Se si verificano errori o avvisi, consultare il documento di MDT *Informazioni di riferimento per la risoluzione dei problemi*.  

3.  Nella finestra di dialogo **Riepilogo distribuzione** fare clic su **Dettagli**.  

     Se si sono verificati errori o avvisi, esaminarli e registrare le informazioni di diagnostica.  

4.  Nella finestra di dialogo **Riepilogo distribuzione** fare clic su **Fine**.  

 Le informazioni sulla migrazione dello stato utente vengono acquisite e archiviate nella cartella condivisa di rete (UserStateCapture$) creata in precedenza nel processo.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Passaggio 8: avviare il nuovo computer con il supporto di avvio LTI  
 Avviare il nuovo computer (WDG-NEW-02) con il supporto di avvio LTI creato in precedenza nel processo. Questo CD consente di avviare Windows PE nel computer di riferimento e avvia il processo di distribuzione di MDT. Al termine del processo di distribuzione di MDT, Windows Vista viene distribuito nel nuovo computer e le informazioni acquisite sulla migrazione dello stato utente vengono ripristinate nel nuovo computer.  

> [!NOTE]
>  È anche possibile avviare il processo di MDT avviando il computer di destinazione da Servizi di distribuzione Windows. Per altre informazioni, vedere la sezione relativa alla preparazione di Servizi di distribuzione Windows nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

 **Per avviare il nuovo computer con il supporto di avvio LTI**  

1.  Avviare il computer WDG-NEW-02 con il supporto di avvio creato in precedenza nel processo.  

     Dopo l'avvio di Windows PE viene avviata anche distribuzione guidata di Windows.  

2.  Completare la distribuzione guidata di Windows usando le informazioni seguenti. Accettare i valori predefiniti se non diversamente specificato.  

    |**In questa pagina della procedura guidata**|**Eseguire questa operazione**|  
    |--|--|
    |**Pagina iniziale della distribuzione**|Fare clic su **Run the Deployment Wizard** (Esegui distribuzione guidata) per installare un nuovo sistema operativo e quindi fare clic su **Avanti**.|  
    |**Specificare le credenziali per la connessione alle condivisioni di rete.**|1.  In **Nome utente** digitare **Amministratore**.<br />2.  In **Password** digitare **P@ssw0rd**.<br />3.  In **Dominio** digitare **CORP**.<br />4.  Fare clic su **OK**.|  
    |**Selezionare una sequenza di attività da eseguire in questo computer.**|Fare clic su **Perform Replace Computer Scenario on New Computer** (Esegui scenario di sostituzione computer nel nuovo computer) e fare clic su **Avanti**.|  
    |**Configurare il nome del computer**|In **Nome computer** digitare **WDG-NEW-02** e quindi fare clic su **Avanti**.|  
    |**Aggiungere il computer a un dominio o un gruppo di lavoro**|Fare clic su **Avanti**.|  
    |**Specificare se devono essere ripristinati i dati utente**|1.  Fare clic su **Specify a location** (Specificare una posizione).<br />2.  In **Percorso** digitare **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Fare clic su **Avanti**.|  
    |**Selezione impostazioni locali**|Fare clic su **Avanti**.|  
    |**Impostare il fuso orario**|Fare clic su **Avanti**.|  
    |**Specificare se acquisire un'immagine**|Scegliere di **non acquisire un'immagine del computer**, quindi fare clic su **Avanti**.|  
    |**Specificare la configurazione di BitLocker**|Scegliere di **non abilitare BitLocker per il computer**, quindi fare clic su **Avanti**.|  
    |**Pronto a iniziare**|Fare clic su **Inizio**.|  

     Se si verificano errori o avvisi, consultare il documento di MDT *Informazioni di riferimento per la risoluzione dei problemi*.  

3.  Nella finestra di dialogo **Riepilogo distribuzione** fare clic su **Dettagli**.  

     Se si sono verificati errori o avvisi, esaminarli e registrare le informazioni di diagnostica.  

4.  Nella finestra di dialogo **Riepilogo distribuzione** fare clic su **Fine**.  

 Windows Vista è ora installato nel nuovo computer e sono state ripristinate le informazioni acquisite sulla migrazione dello stato utente.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Integrazione di codice di distribuzione personalizzato in MDT  
 È comune per un team di distribuzione avere requisiti complessi, specifici del proprio ambiente di destinazione, che non possono essere soddisfatti dalle azioni delle sequenze di attività predefinite di Deployment Workbench o dai file di configurazione predefiniti di MDT. In questo caso è necessario implementare codice personalizzato per soddisfare tali requisiti.  

 Per integrare codice di distribuzione personalizzato in MDT:  

-   Scegliere un linguaggio di scripting come descritto in [Scelta del linguaggio di scripting appropriato](#ChooseAppropLanguage)  

-   Usare ZTIUtility.vbs come descritto in [Modalità di utilizzo di ZTIUtility](#UnderstandLeverageZTI)  

-   Integrare il codice di distribuzione personalizzato come descritto in [Integrazione del codice di distribuzione personalizzato](#IntegrateCustomDeploy)  

 Nelle sezioni successive si presuppone che MDT sia configurato in un server di distribuzione.  

###  <a name="ChooseAppropLanguage"></a> Scelta del linguaggio di scripting appropriato  
 Benché qualsiasi codice eseguibile in Windows o Windows PE possa essere chiamato come installazione di un'applicazione o attraverso un passaggio di una sequenza di attività di MDT, Microsoft consiglia di usare gli script sotto forma di file VBS o WSF.  

 Il vantaggio offerto dall'uso dei file WSF è la registrazione integrata, oltre ad altre funzioni predefinite già in uso nei processi ZTI e LTI. Queste funzioni sono disponibili nello script ZTIUtility distribuito con MDT.  

 Quando viene fatto riferimento da uno script personalizzato, lo script ZTIUtility inizializza le classi di ambiente e configurazione di MDT. Sono disponibili le classi seguenti:  

-   **Logging**. Questa classe offre la funzionalità di registrazione usata da tutti gli script di MDT. Crea inoltre un singolo file di log per ogni script eseguito durante la distribuzione e un file di log consolidato di tutti gli script. Questi file di log vengono creati in un formato progettato per essere letto da TRACE32. Questo strumento è disponibile in [System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257).  

-   **Environment**. Questa classe configura le variabili di ambiente raccolte con l'elaborazione delle regole di WMI e MDT e consente di fare riferimento alle stesse direttamente dallo script. Ciò consente di leggere le proprietà di distribuzione e di accedere a tutte le informazioni di configurazione usate dai processi ZTI e LTI.  

-   **Utility**. Questa classe specifica utilità generali che vengono usate negli script ZTI e LTI. È consigliabile esaminare questa classe ogni volta che si sviluppa codice personalizzato per verificare se esiste del codice che si possa semplicemente riusare. Informazioni aggiuntive su alcune delle funzionalità proprie di questa classe sono disponibili più avanti in questa sezione.  

-   **Database**. Questa classe esegue alcune funzioni, tra cui la connessione ai database e la lettura delle informazioni dai database. In generale, l'accesso diretto alla classe database non è consigliato ed è invece opportuno elaborare le regole per eseguire ricerche nel database.  

-   **Strings**. Questa classe esegue normali routine di elaborazione delle stringhe, ad esempio la creazione di un elenco di elementi delimitato da virgole, la visualizzazione di un valore esadecimale, la rimozione di spazi vuoti da una stringa, l'allineamento a destra e a sinistra di una stringa, l'imposizione di un valore per un formato stringa o di matrice, la generazione di un identificatore univoco globale (GUID) casuale e le conversioni in Base64.  

-   **FileHandling**. Questa classe esegue diverse funzioni, tra cui la normalizzazione dei percorsi e la copia, lo spostamento e l'eliminazione di file e cartelle.  

-   **clsRegEx**. Questa classe esegue le funzioni di espressione regolare.  

 In MDT sono state implementate alcune modifiche all'architettura dello script per rendere il client Microsoft Visual Basic® Scripting Edition (VBScript) più efficace e affidabile. Queste modifiche comprendono:  

-   Apportate modifiche significative a ZTIUtility.vbs (libreria script principale), tra cui nuove API e una migliore gestione degli errori  

-   Nuovo aspetto per la struttura complessiva degli script ZTI_*xxx*.wsf  

 Modifica della struttura generale degli script di MDT. Gli script di MDT ora sono per la maggior parte incapsulati in oggetti **Class** di VBScript. La classe viene inizializzata e chiamata con la funzione **RunNewInstance**.  

> [!NOTE]
>  La maggior parte degli script di MDT 2008 Update 1 funzionerà così com'è in MDT, anche apportando modifiche significative a ZTIUtility.vbs, poiché la maggior parte degli script di MDT include ZTIUtility.vbs.  

###  <a name="UnderstandLeverageZTI"></a> Modalità di utilizzo di ZTIUtility  
 Il file ZTIUtility.vbs contiene classi di oggetti che possono essere usate nel codice personalizzato. Per integrare il codice personalizzato con MDT usare:  

-   La classe di registrazione definita in ZTIUtility.vbs come descritto in [Usare la classe di registrazione di ZTIUtility](#UseZTILogging)  

-   La classe di ambiente definita in ZTIUtility.vbs come descritto in [Usare la classe di ambiente di ZTIUtility](#UseZTIEnvironment)  

-   La classe di utilità definita in ZTIUtility.vbs come descritto in [Usare la classe di utilità di ZTIUtility](#UseZTIUtility)  

####  <a name="UseZTILogging"></a> Usare la classe di registrazione di ZTIUtility  
 La classe di registrazione di ZTIUtiliy.vbs offre un semplice meccanismo che consente al codice personalizzato di registrare informazioni sullo stato, avvisi ed errori analogamente agli altri script durante una distribuzione ZTI o LTI. Questa standardizzazione garantisce inoltre che nella finestra di dialogo **Riepilogo distribuzione LTI** sia indicato correttamente lo stato di qualsiasi codice personalizzato eseguito.  

 Di seguito è riportato un esempio di script di codice personalizzato che usa le funzioni **oLogging.CreateEntry** e **TestAndFail** per registrare diversi tipi di messaggi, in base ai risultati delle varie azioni di script.  

 **Esempio di script che usa la registrazione di ZTIUtility: ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  È comunque possibile continuare a usare gli script che chiamano **ZTIProcess()** con **ProcessResults()**. Tuttavia, alcune funzionalità avanzate di gestione degli errori non saranno abilitate.  

####  <a name="UseZTIEnvironment"></a> Usare la classe di ambiente di ZTIUtility  
 La classe di ambiente in ZTIUtiliy.vbs consente di accedere e, se necessario, di aggiornare le proprietà di MDT. Nell'esempio precedente **oEnvironment.Item("Memory")** consente di recuperare la quantità di RAM disponibile. Può essere usata anche per recuperare il valore di una delle proprietà descritte nel documento di MDT *Informazioni di riferimento sul toolkit* .  

####  <a name="UseZTIUtility"></a> Usare la classe di utilità di ZTIUtility  
 Lo script ZTIUtility.vbs contiene alcune utilità di uso comune che si possono impiegare in qualsiasi script di distribuzione personalizzato. È possibile aggiungere queste utilità a qualsiasi script esattamente come le classi **oLogging** e **oEnvironment**.  

Nella tabella seguente vengono descritte alcune funzioni utili disponibili con il relativo output. Per un elenco completo delle funzioni disponibili, vedere il file ZTIUtility.vbs.  

|**Funzione**|**Output**|  
|-|-|
|**oUtility.LocalRootPath**|Restituisce il percorso della cartella radice usata dal processo di distribuzione nel computer di destinazione, ad esempio C:\MININT|  
|**oUtility.BootDevice**|Restituisce il dispositivo di avvio del sistema, ad esempio MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|Restituisce il percorso alla cartella dei log usata durante la distribuzione, ad esempio C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|Restituisce il percorso dell'archivio stati attualmente configurato, ad esempio C:\MININT\StateStore|  
|**oUtility.ScriptName**|Restituisce il nome dello script che chiama la funzione, ad esempio Z-RAMTest|  
|**oUtility.ScriptDir**|Restituisce il percorso allo script che chiama la funzione, ad esempio \\\nome_server\Deployment$\Scripts|  
|**oUtility.ComputerName**|Determina il nome del computer che verrà usato durante il processo di compilazione, ad esempio nome_computer|  
|**oUtility.ReadIni(file, section, item)**|Consente la lettura dell'elemento specificato da un file INI|  
|**oUtility.WriteIni(file, section, item, value)**|Consente la scrittura dell'elemento specificato in un file INI|  
|**oUtility.Sections(file)**|Legge le sezioni di un file INI e le archivia in un oggetto di riferimento|  
|**oUtility.SectionContents(file, section)**|Legge il contenuto del file INI specificato e lo archivia in un oggetto|  
|**oUtility.RunWithHeartbeat(sCmd)**|Quando viene eseguito il comando, scrive informazioni di tipo heartbeat nei log ogni 0,5 secondi|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Cerca il file specificato nella cartella DeployRoot e nelle sottocartelle standard, tra cui Servicing, Tools, USMT, Templates, Scripts e Control|  
|**oUtility.findMappedDrive(sServerUNC)**|Verifica se un'unità è mappata al percorso UNC specificato e restituisce la lettera di unità|  
|**oUtility.ValidateConnection(sServerUNC)**|Verifica se esiste una connessione al server specificato e, se non esiste, tenta di crearne una|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Esegue il mapping di una lettera di unità al percorso UNC specificato come condivisione e restituisce la lettera di unità usata, in caso contrario restituisce un errore|  
|**VerifyPathExists(strPath)**|Verifica che il percorso specificato esista|  
|**oEnvironment.Substitute(sVal)**|Data una stringa, espande eventuali variabili o funzioni all'interno di tale stringa|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Legge o scrive una variabile in un archivio permanente|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Esegue un test per verificare se la variabile esiste|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Legge o scrive una variabile di tipo **array** in un archivio permanente|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Usata per eseguire una chiusura strutturata se viene rilevato un errore irreversibile|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|Scrive un messaggio nel file di log e invia l'evento a un server definito|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Scrive un messaggio nel file di log|  
|**TestAndFail(iRc, iError, sMessage)**|Esce dallo script con **iError** se **iRc** è False o Fail|  
|**TestAndLog(iRc , sMessage)**|Registra un avviso solo se **iRc** è False o Fail|  

###  <a name="IntegrateCustomDeploy"></a> Integrazione del codice di distribuzione personalizzato  
 Il codice di distribuzione personalizzato può essere integrato nel processo di MDT in diversi modi. Tuttavia, indipendentemente dal metodo usato, è necessario soddisfare le due regole seguenti:  

-   Il nome dello script del codice di distribuzione personalizzato deve sempre iniziare con la lettera Z.  

-   Il codice di distribuzione personalizzato deve essere inserito nella cartella Scripts della condivisione di distribuzione, ad esempio D:\Production Deployment Share\Scripts.  

 I metodi usati più frequentemente per integrare il codice personalizzato e che garantiscono una registrazione coerente sono:  

-   Distribuire il codice come applicazione MDT  

-   Avviare il codice come comando di una sequenza di attività di MDT  

-   Avviare il codice come script User Exit  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Distribuire il codice personalizzato come applicazione MDT  
 Il codice di distribuzione personalizzato può essere importato in Deployment Workbench e gestito come qualsiasi altra applicazione.  

 **Per creare una nuova applicazione per eseguire il codice di distribuzione personalizzato**  

1.  Copiare il codice di distribuzione personalizzato nella cartella *condivisione_distribuzione*\Scripts (dove *condivisione_distribuzione* è il percorso completo della condivisione di distribuzione).  

2.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

3.  Nell'albero della console di Deployment Workbench passare a Deployment Shares/*condivisione_distribuzione*/Applications (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

4.  Nel riquadro Azioni fare clic su **Nuova applicazione**.  

     Viene avviata la Creazione guidata nuova applicazione.  

5.  Completare la procedura guidata usando le informazioni seguenti. Accettare le impostazioni predefinite se non diversamente specificato.  

    |**In questa pagina della procedura guidata**|**Eseguire questa operazione**|  
    |-|-|  
    |**Tipo di applicazione**|Scegliere il tipo di **applicazione senza file di origine o in un'altra posizione nella rete**, quindi fare clic su **Avanti**.|  
    |**Informazioni dettagliate**|Completare questa pagina in base alle informazioni contenute nell'applicazione e quindi fare clic su **Avanti**.|  
    |**Dettagli del comando**|1.  Nella casella **Riga di comando** digitare **cscript.exe %SCRIPTROOT%\codice_personalizzato** (dove *codice_personalizzato* è il nome del codice personalizzato che è stato sviluppato).<br />2.  Nella casella **Directory di lavoro** digitare ***directory_lavoro*** (dove directory_lavoro è il nome della directory di lavoro del codice personalizzato, in genere la stessa cartella specificata nella casella **Riga di comando**).<br />3.  Fare clic su **Avanti**.|  
    |**Riepilogo**|Verificare che le impostazioni di configurazione siano corrette e quindi fare clic su **Avanti**.|  
    |**Conferma**|Fare clic su **Fine**.|  

 L'applicazione viene visualizzata nel nodo Applicazioni di Deployment Workbench.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Aggiungere il codice personalizzato come passaggio di una sequenza di attività  
 Il codice di distribuzione personalizzato può essere chiamato direttamente da qualsiasi punto di una sequenza di attività. Ciò consente di accedere alle normali opzioni e regole della sequenza di attività.  

 **Per aggiungere il codice di distribuzione personalizzato a una sequenza di attività esistente**  

1.  Copiare il codice di distribuzione personalizzato nella cartella *condivisione_distribuzione*\Scripts (dove *condivisione_distribuzione* è il percorso completo della condivisione di distribuzione).  

2.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

3.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

4.  Nel riquadro dei dettagli fare clic su ***sequenza_attività*** (dove *sequenza_attività* è il nome della sequenza di attività che esegue il codice personalizzato).  

5.  Nel riquadro Azioni fare clic su **Proprietà**.  

6.  Nella finestra di dialogo ***Proprietà sequenza_attività*** fare clic sulla scheda **Sequenza di attività**.  

7.  Nell'albero della console passare a *gruppo* (dove *gruppo* è il gruppo a cui aggiungere il passaggio della sequenza di attività).  

8.  Fare clic su **Aggiungi**, **Generali** e quindi scegliere **Esegui riga di comando**.  

9. Nell'albero della console fare clic su **Esegui riga di comando** e quindi sulla scheda **Proprietà**.  

10. Nella casella **Nome** digitare ***nome*** (dove *nome* è un nome descrittivo del codice personalizzato).  

11. Nella casella **Riga di comando** della scheda **Proprietà** digitare ***riga_comando*** (dove *riga_comando* è il comando di esecuzione del codice personalizzato, ad esempio **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. Nella casella **Da** digitare ***percorso*** (dove *percorso* è il percorso completo alla cartella di lavoro del codice personalizzato, in genere lo stesso percorso specificato nella casella **Riga di comando**) e quindi fare clic su **OK**.  

 Il passaggio della sequenza di attività appena creato appare nell'elenco dei passaggi della sequenza.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Eseguire il codice personalizzato come script User Exit  
 È anche possibile eseguire il codice personalizzato come script User Exit da CustomSettings.ini usando la direttiva **UserExit**. In questo modo si ha a disposizione un meccanismo che consente di passare le informazioni nel processo di convalida delle regole di CustomSettings.ini e ottenere un aggiornamento dinamico delle proprietà di MDT  

 Per altre informazioni sugli script User Exit e sulla direttiva **UserExit**, vedere la sezione relativa all'uso degli script User Exit nel file CustomSettings.ini File nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Installazione di driver di dispositivo usando vari metodi di installazione  
 In questo scenario si usa MDT per distribuire un sistema operativo in diversi tipi di hardware. Come parte del processo di distribuzione, identificare e installare i driver di dispositivo in modo che ogni tipo di hardware funzioni correttamente. Esistono due tipi principali di driver di dispositivo e ognuno deve essere gestito in modo diverso durante il processo di distribuzione:  

-   Driver di dispositivo che contengono un file INF che può essere usato per importare il driver di dispositivo in Deployment Workbench  

-   Driver di dispositivo che vengono inseriti in un pacchetto come un'applicazione e devono essere installati come un'applicazione  

 Con MDT è possibile gestire entrambi i tipi di driver come parte della distribuzione di un sistema operativo.  

 Per installare i driver di dispositivo:  

-   Determinare i metodi per installare ogni driver di dispositivo come descritto in [Determinazione del metodo da usare per installare un driver di dispositivo](#WhichMethodtoInstallDriver)  

-   Usare il metodo dei driver "non inclusi" come descritto in [Installazione dei driver di dispositivo usando driver non inclusi](#InstallOutofBoxDrivers)  

-   Installare i driver come applicazioni come descritto in [Installazione dei driver di dispositivo come applicazioni](#InstallDriversasApplications)  

 In questo scenario si presuppone che MDT sia eseguito in un server di distribuzione.  

###  <a name="WhichMethodtoInstallDriver"></a> Determinazione del metodo da usare per installare un driver di dispositivo  
 I produttori di hardware rilasciano i driver di dispositivo in uno di due formati:  

-   Come pacchetto che si può estrarre e che contiene i file INF usati per importare il driver in Deployment Workbench  

-   Come applicazione che deve essere installata usando i normali processi di installazione delle applicazioni  

 I pacchetti di driver di dispositivo che possono essere estratti per accedere ai file INF sono in grado di usare il processo di rilevamento e installazione automatico dei driver MDT importando il driver nel nodo Out-of-Box Drivers di Deployment Workbench.  

 I pacchetti di driver di dispositivo che non possono essere estratti per isolare i file INF o quelli che non funzionano correttamente se non vengono prima installati usando programma di installazione applicazione, ad esempio un file MSI o Setup.exe, possono usare la funzionalità Installa applicazione di MDT e installare il driver di dispositivo durante il processo di distribuzione come per qualsiasi applicazione normale.  

###  <a name="InstallOutofBoxDrivers"></a> Installazione dei driver di dispositivo usando driver non inclusi  
 È possibile importare pacchetti di driver di dispositivo che includono un file INF in Deployment Workbench e installarli automaticamente come parte del processo di distribuzione. Per implementare questo tipo di distribuzione dei driver di dispositivo, aggiungere prima il driver a Deployment Workbench.  

 **Per aggiungere il driver di dispositivo a Deployment Workbench**  

1.  Scaricare i driver di dispositivo richiesti per i tipi di hardware da distribuire ed estrarre il pacchetto di driver di dispositivo in un percorso temporaneo.  

2.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

3.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Out-of-Box Drivers (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

4.  Nel riquadro Azioni fare clic su **Import Drivers** (Importa driver).  

     Viene avviata l'importazione guidata dei driver di dispositivo.  

5.  Nella sezione **Origine driver** della pagina **Specificare directory** fare clic su **Sfoglia** per accedere alla cartella che contiene i nuovi driver di dispositivo, quindi fare clic su **Avanti**.  

    > [!NOTE]
    >  La creazione guidata nuovo driver di dispositivo eseguirà una ricerca in tutte le sottodirectory della directory di origine del driver. Se sono presenti più driver da installare, li estrae in cartelle all'interno della stessa directory radice e quindi imposta la directory di origine del driver come directory radice che contiene tutte le cartelle di origine dei driver.  

6.  Nella pagina **Riepilogo** verificare che le impostazioni siano corrette e quindi fare clic su **Avanti** per importare i driver in Deployment Workbench.  

7.  Fare clic su **Fine** nella pagina **Conferma**.  

 Se i driver di dispositivo contengono driver essenziali per l'avvio, ad esempio driver per l'archiviazione di massa o le classi di rete, la condivisione di distribuzione deve essere aggiornata in modo da generare un nuovo ambiente di avvio LiteTouch_x86 e LiteTouch_x64 che contiene i nuovi driver.  

 **Per aggiungere i driver di dispositivo alle immagini di Windows PE Lite Touch**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

4.  Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

5.  Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

6.  Fare clic su **Fine** nella pagina **Conferma**.  

###  <a name="InstallDriversasApplications"></a> Installazione dei driver di dispositivo come applicazioni  
 I driver di dispositivo che sono inclusi in pacchetti come applicazioni e non possono essere estratti in una cartella contenente un file INF, oltre ai file di driver, devono essere aggiunti a Deployment Workbench come applicazioni per l'installazione durante il processo di distribuzione.  

 Le applicazioni possono essere specificate come un passaggio della sequenza di attività o indicate in CustomSettings.ini. Tuttavia, le applicazioni di driver di dispositivo devono essere installate solo quando la sequenza di attività viene eseguita in un computer con i dispositivi. A tale scopo, eseguire il passaggio della sequenza di attività per distribuire le applicazioni di driver di dispositivo pertinenti come passaggio di una sequenza di attività condizionale. I criteri condizionali possono essere specificati per l'esecuzione del il passaggio della sequenza di attività usando le query WMI per il dispositivo nel computer di destinazione.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Aggiungere l'applicazione di driver di dispositivo a Deployment Workbench  
 Ogni applicazione di driver di dispositivo deve prima essere importata in Deployment Workbench.  

> [!NOTE]
>  Specificare se l'applicazione deve essere visibile durante la distribuzione nella finestra di dialogo **Proprietà** di qualsiasi applicazione, selezionando o deselezionando l'opzione che consente di **nascondere l'applicazione nella distribuzione guidata**. Ripetere questo processo per ogni applicazione di driver di dispositivo usata durante la distribuzione.  

 **Per aggiungere l'applicazione di driver di dispositivo a Deployment Workbench**  

1.  Scaricare l'applicazione di driver di dispositivo e salvarla in un percorso temporaneo.  

2.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

3.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Applications (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

4.  Nel riquadro Azioni fare clic su **Nuova applicazione**.  

     Viene avviata la Creazione guidata nuova applicazione.  

5.  Nella pagina **Tipo applicazione** scegliere l'**applicazione con file di origine** e quindi fare clic su **Avanti**.  

6.  Nella pagina **Dettagli** digitare le informazioni pertinenti sull'applicazione e quindi fare clic su **Avanti**.  

7.  Nella sezione **Directory di origine** della pagina **Origine** fare clic su **Sfoglia** per passare a e selezionare la cartella che contiene i file di origine dell'applicazione di driver di dispositivo. Fare clic su **OK**.  

8.  Fare clic su **Avanti**.  

9. Nella pagina **Destinazione** digitare un nome per la directory di destinazione e quindi fare clic su **Avanti**.  

10. Nella sezione **Riga di comando** della pagina **Dettagli del comando** digitare il comando che consente l'installazione invisibile all'utente dell'applicazione di driver di dispositivo.  

11. Nella pagina **Riepilogo** verificare che le impostazioni siano corrette e quindi fare clic su **Avanti** per importare l'applicazione di driver di dispositivo in Deployment Workbench.  

12. Fare clic su **Fine** nella pagina **Conferma**.  

 Dopo aver importato le applicazioni in Deployment Workbench, aggiungerle al processo di distribuzione usando la logica appropriata per garantire che l'applicazione venga installata solo se in esecuzione nel prodotto hardware corretto. Esistono diversi metodi per raggiungere questo obiettivo:  

-   Specificare l'applicazione di driver di dispositivo come parte di una sequenza di attività di distribuzione.  

-   Specificare l'applicazione di driver di dispositivo in CustomSettings.ini.  

-   Specificare l'applicazione di driver di dispositivo nel database MDT.  

 Ogni approccio è descritto più in dettaglio nelle sezioni seguenti.  

####  <a name="SpecifyDeviceAppTask"></a> Specificare l'applicazione di driver di dispositivo come parte di una sequenza di attività  
 Il primo metodo per aggiungere un'applicazione di driver di dispositivo al processo di distribuzione è usare una sequenza di attività per aggiungere i passaggi per ogni applicazione di driver di dispositivo.  

 Esistono due approcci principali per la gestione delle applicazioni di driver di dispositivo nella sequenza di attività:  

-   Creare un nuovo gruppo di sequenze di attività per ogni modello di hardware e quindi aggiungere una query per eseguire tale gruppo di azioni se il computer corrisponde a un tipo di hardware specifico.  

-   Creare un gruppo di sequenze di attività per le applicazioni specifiche dell'hardware e quindi aggiungere query per ogni azione della sequenza di attività in modo che ogni passaggio della sequenza di attività sia valutato in base al tipo di hardware e venga eseguito solo se viene trovata una corrispondenza.  

 **Per creare un nuovo gruppo di sequenze di attività per ogni tipo di hardware**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro dei dettagli fare clic su ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività di distribuzione che sarà richiesta per installare l'applicazione di driver di dispositivo).  

4.  Nel riquadro Azioni fare clic su **Proprietà**.  

5.  Nella finestra di dialogo ***Proprietà sequenza_attività***, nel riquadro dei dettagli della scheda **Sequenza di attività** passare a Ripristino stato/Windows Update (preinstallazione applicazione).  

6.  Nella scheda **Sequenza di attività** fare clic su **Aggiungi** e quindi su **Nuovo gruppo**.  

     Verrà creato un nuovo gruppo di sequenze di attività nella sequenza di attività. Usare questo nuovo gruppo di sequenze di attività per creare i passaggi per l'installazione delle applicazioni di driver di dispositivo specifiche dell'hardware.  

7.  Nel riquadro dei dettagli fare clic su **Nuovo gruppo**.  

8.  Nella casella **Nome** della scheda **Proprietà** digitare ***nome_gruppo*** (dove *nome_gruppo* è il nome del gruppo, ad esempio *Applicazioni specifiche hardware - Dell Computer Corporation*).  

9. Nella scheda **Opzioni** fare clic su **Aggiungi** e quindi su **Query WMI**.  

10. Nella finestra di dialogo **Task Sequence WMI Condition** (Condizione WMI sequenza di attività) digitare i dettagli seguenti:  

    -   Nella casella dello **spazio dei nomi WMI** digitare **root\cimv2**.  

    -   Nella casella **Query WQL** digitare una query WQL (WMI Query Language) usando la classe **Win32_ComputerSystem** per verificare che l'applicazione venga installata solo per un tipo specifico di applicazione, ad esempio:  

         **Select \* FROM Win32_ComputerSystem WHERE Model LIKE *%hardware_model%* AND Manufacturer LIKE *%hardware_manufacturer%***  

         In questo esempio *hardware_model* è il nome del modello di computer, ad esempio Latitudine D620, e *hardware_manufacturer* è il nome della marca del computer, ad esempio Dell Corporation.  

         Il simbolo **%** è un carattere jolly che viene incluso nei nomi per consentire agli amministratori di restituire eventuali modelli o marche di computer che contengono il valore specificato per ***hardware_model*** o ***hardware_manufacturer***.  

     Per altre informazioni sulle query WMI e WQL, vedere la sezione relativa all'aggiunta di query WMI alle condizioni dei passaggi di sequenza di attività nel documento di MDT *Uso di Microsoft Deployment Toolkit* e vedere [Querying with WQL](http://msdn.microsoft.com/library/aa392902.aspx) (Esecuzione di query con WQL).  

11. Fare clic su **OK** per inviare la query e quindi fare clic su **OK** per inviare le modifiche alla sequenza di attività.  

> [!NOTE]
>  Questo processo deve essere ripetuto per ogni tipo di hardware di ogni applicazione di driver di dispositivo da installare.  

 Dopo aver creato i gruppi di sequenze di attività specifiche dell'hardware, è possibile aggiungere le applicazioni di driver di dispositivo a ogni gruppo.  

 **Per aggiungere applicazioni di driver di dispositivo a gruppi di sequenze di attività specifiche dell'hardware**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro dei dettagli fare clic su ***sequenza_attività*** (dove *sequenza_attività* è la sequenza di attività di distribuzione che sarà richiesta per installare l'applicazione di driver di dispositivo).  

4.  Nel riquadro Azioni fare clic su **Proprietà**.  

5.  Nella finestra di dialogo ***Proprietà sequenza_attività*** fare clic sulla scheda **Sequenza di attività**.  

6.  Nel riquadro dei dettagli andare a Ripristino stato/*gruppo_specifico_hardware* (dove *gruppo_specifico_hardware* è il nome del gruppo specifico dell'hardware in cui verrà aggiunto il passaggio della sequenza di attività per installare l'applicazione di driver dispositivo).  

7.  Nella scheda **Sequenza di attività** fare clic su **Aggiungi**, **Generali** e quindi su **Installa applicazione**.  

     Il passaggio **Installa applicazione** della sequenza di attività appare nel riquadro dei dettagli.  

8.  Fare clic su **Installa applicazione** nel riquadro dei dettagli.  

9. Nella scheda **Proprietà** fare clic su **Install a single application** (Installa una sola applicazione) e nell'elenco delle **applicazioni da installare** selezionare ***applicazione_hardware*** (dove *applicazione_hardware* è l'applicazione per l'installazione dell'applicazione specifica dell'hardware).  

> [!NOTE]
>  Questo processo deve essere ripetuto per ogni applicazione di driver di dispositivo da usare durante una distribuzione.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Specificare l'applicazione di driver di dispositivo in CustomSettings.ini  
 Quando viene avviata una distribuzione LTI o ZTI, una delle prime operazioni da eseguire è l'elaborazione dei file di controllo BootStrap.ini e CustomSettings.ini. Entrambi questi file contengono regole che possono essere usate per personalizzare in modo dinamico la distribuzione.  

 A causa della modalità in cui MDT elabora il file CustomSettings.ini, è possibile usarlo per aggiungere applicazioni in base a condizioni specifiche. Questa logica verrà usata per aggiungere applicazioni specifiche del driver di dispositivo durante la distribuzione in base a tipi di hardware specifici. Alle applicazioni viene fatto riferimento nel file CustomSettings.ini dal GUID dell'applicazione, che si trova nel file Applications.xml nella condivisione di distribuzione.  

 **Per individuare il GUID di un'applicazione importata**  

1.  Nella condivisione di distribuzione del server di distribuzione aprire la cartella di controllo, ad esempio D:\Production Deployment Share\Control.  

2.  Individuare e aprire il file Applications.xml.  

3.  Individuare l'applicazione richiesta.  

4.  Individuare il GUID dell'applicazione cercando la riga racchiusa tra i tag `<guid>` dell'applicazione, ad esempio `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Nell'ambito del processo di inizializzazione, i processi LTI e ZTI raccolgono entrambi informazioni sul computer in cui sono in esecuzione. Come parte di questo processo, vengono eseguite query WMI e i valori della classe **Win32_ComputerSystem** per marca e produttore vengono popolati rispettivamente come variabili **%Make%** e **%Model%**.  

 Questi valori possono essere usati durante l'elaborazione del file CustomSettings.ini per leggere in modo dinamico le sezioni del file in base alla marca e al modello rilevati.  Di seguito è riportato un esempio di file CustomSettings.ini.  

 **Esempio di file CustomSettings.ini configurato per l'installazione di un'applicazione specifica dell'hardware**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Usare le proprietà seguenti per specificare applicazioni in CustomSettings.ini:  

-   **Applications**. Questa proprietà può essere usata quando gli amministratori della distribuzione non vogliono presentare la creazione guidata applicazioni come parte del processo di distribuzione, specificando **SkipApplications=YES** in CustomSettings.ini.  

-   **MandatoryApplications**. Questa proprietà può essere usata se gli amministratori della distribuzione vogliono presentare la creazione guidata applicazioni durante la distribuzione per consentire ai tecnici della distribuzione di selezionare altre applicazioni da installare durante la distribuzione.  

     Se la creazione guidata applicazioni viene usata senza la proprietà **MandatoryApplications**, ad esempio **SkipApplications=NO**, sovrascriverà le applicazioni specificate dalla proprietà **Applications**.  

     L'esempio precedente illustra come usare i valori di variabile Il sampole previousi viene illustrato come utilizzare i valori delle variabili **%Make%** e **%Model%** per modificare dinamicamente il modo in cui viene creato l'elenco delle applicazioni. I valori relativi a marca e modello di ogni tipo di hardware possono essere individuati usando uno dei metodi seguenti:  

-   **Lo strumento System Information**. Usare il nodo System Summary in questo strumento per identificare i valori di **System Manufacturer** (marca) e **System Model** (modello).  

-   **Windows PowerShell**. Usare il cmdlet **Get-WMIObject-class Win32_ComputerSystem** per determinare la marca e il modello del computer.  

-   **Riga di comando di Strumentazione gestione Windows**. Usare **CSProduct Get Name, Vendor** per restituire il nome (modello) e il fornitore (marca) del computer.  

 **Per modificare CustomSettings.ini in modo da aggiungere la logica specifica dell'hardware**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Regole**.  

5.  Le informazioni digitate in questa scheda vengono archiviate nel file CustomSettings.ini. Modificare le voci del file CustomSettings.ini per aggiungere la logica per ogni modello di hardware con un'applicazione specifica del driver di dispositivo, come descritto in [Specificare l'applicazione di driver di dispositivo come parte di una sequenza di attività](#SpecifyDeviceAppTask).  

6.  Fare clic su **OK** per inviare le modifiche.  

7.  Nel riquadro dei dettagli fare clic su *condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

8.  Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

9. Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

10. Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

11. Fare clic su **Fine** nella pagina **Conferma**.  

 Per impostazione predefinita, tutte le applicazioni disponibili vengono visualizzate nella distribuzione guidata di Windows durante una distribuzione LTI. Poiché le applicazioni specifiche del driver di dispositivo sono valide solo per determinati tipi di hardware, è preferibile non visualizzarle costantemente. Specificando il pacchetto di applicazioni specifiche del driver di dispositivo in CustomSettings.ini, è possibile nascondere un'applicazione usando l'opzione **Hide the application in the Deployment Wizard** (Nascondi l'applicazione nella distribuzione guidata) nella configurazione dell'applicazione.  

 **Per nascondere un'applicazione nella distribuzione guidata**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Applications (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro dei dettagli fare clic su ***applicazione_driver_dispositivo*** (dove *applicazione_driver_dispositivo* è l'applicazione da nascondere nella distribuzione guidata).  

4.  Nel riquadro Azioni fare clic su **Proprietà**.  

5.  Selezionare la casella di controllo **Hide the application in the Deployment Wizard** (Nascondi l'applicazione nella distribuzione guidata) nella scheda **Generali**.  

6.  Fare clic su **Applica** e quindi chiudere la finestra di dialogo **Proprietà**.  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Specificare l'applicazione di driver di dispositivo nel database MDT  
 Il database MDT è una versione database del file CustomSettings.ini che può essere sottoposta a query in fase di distribuzione per trovare le informazioni da usare durante la distribuzione. Per altre informazioni sull'uso del database MDT, vedere alla sezione relativa alla selezione dei metodi di applicazione delle impostazioni di configurazione.  

 Quando si eseguono query sul database MDT in fase di distribuzione, sono disponibili tre metodi per l'identificazione del computer di destinazione:  

-   Ricerca del singolo computer usando l'indirizzo MAC, il tag asset o simile.  

-   Ricerca del percorso del computer usando il gateway predefinito.  

-   Ricerca della marca e del modello del computer usando query WMI su produttore o marca e modello.  

 Per ogni voce del database creata è possibile specificare le proprietà della distribuzione, le applicazioni, se usare pacchetti di Configuration Manager e gli amministratori. Creando voci di marca e modello nel database, è possibile aggiungere le applicazioni di driver di dispositivo richieste per l'hardware specifico.  

 **Per creare le voci nel database MDT e consentire l'installazione delle applicazioni di driver del dispositivo**  

> [!NOTE]
>  Ripetere questo processo per ogni marca e modello di hardware che richiede un'applicazione di driver di dispositivo.  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/**condivisione_distribuzione**/Advanced Configuration/Database/Make and Model (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro delle azioni fare clic su **Nuovo**.  

4.  Nella scheda **Identità** della finestra di dialogo **Proprietà** digitare nella casella **Marca** ***nome_marca*** (dove *nome_marca* è un nome facilmente identificabile da associare alla marca del computer di destinazione).  

5.  Nel casella **Modello** digitare ***nome_modello*** (dove *nome_modello* è un nome facilmente identificabile da associare al modello del computer di destinazione).  

6.  Nella scheda **Applicazioni** aggiungere tutte le applicazioni di driver di dispositivo richieste per il modello di hardware.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Avvio di MDT usando Servizi di distribuzione Windows  
 Windows Server 2008 usa Servizi di distribuzione Windows come una versione aggiornata e riprogettata di Servizi di installazione remota, lo strumento di distribuzione predefinito in Windows Server 2003 con SP2. Con Servizi di distribuzione Windows è possibile distribuire i sistemi operativi Windows, in particolare i sistemi Windows 7, Windows Server 2008 o successivi, in una rete usando una scheda di rete abilitata per PXE o un supporto di avvio di un computer.  

 Prima di distribuire Servizi di distribuzione Windows, determinare quale delle seguenti opzioni di integrazione risulta più adatta all'ambiente:  

-   Opzione 1. Avviare i computer in PXE per avviare il processo LTI.  

-   Opzione 2. Distribuire un'immagine del sistema operativo dall'archivio immagini di Servizi di distribuzione Windows.  

-   Opzione 3. Usare la funzionalità multicast con MDT e il ruolo server Servizi di distribuzione Windows di Windows Server 2008.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Opzione 1: avviare i computer in PXE per avviare il processo LTI  
 Per ridurre al minimo i costi di gestione della distribuzione del sistema operativo, avviare il processo di distribuzione di MDT usando Servizi di distribuzione Windows in combinazione con Dynamic Host Configuration Protocol. In questo modo si evita di dover creare e distribuire supporti di avvio per ogni computer di destinazione.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Creare e importare l'immagine di Windows PE di Deployment Workbench in Servizi di distribuzione Windows  
 Quando si crea una nuova condivisione di distribuzione MDT o si modifica una condivisione di distribuzione MDT esistente, è possibile creare un'immagine di avvio Windows PE personalizzata. Quando la condivisione di distribuzione viene aggiornata, l'immagine di avvio di Windows PE viene automaticamente generata e aggiornata con le informazioni sulla condivisione di distribuzione e inserisce eventuali driver o componenti aggiuntivi specificati durante la configurazione della condivisione di distribuzione.  

 L'immagine di avvio di Windows PE viene generata sia come file di immagine ISO, che si può scrivere su un CD o DVD, sia come file WIM di avvio. È possibile importare il file WIM in Servizi di distribuzione Windows in modo che i computer che si possono avviare in PXE siano in grado di scaricare ed eseguire l'immagine di avvio LTI di Windows PE in una rete usata per inizializzare un'installazione.  

 **Per creare un'immagine di avvio di Windows PE in Deployment Workbench**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

     Nella finestra di dialogo ***Proprietà condivisione_distribuzione*** fare clic sulla scheda **Impostazioni *piattaforma* Windows PE** (dove piattaforma è l'architettura dell'immagine Windows PE da configurare).  

4.  Nelle **impostazioni delle immagini di avvio Lite Touch** selezionare la casella di controllo **Generate a Lite Touch bootable RAM disk ISO image** (Genera un'immagine ISO di disco RAM di avvio di Lite Touch).  

5.  Fare clic sulla scheda **Componenti *piattaforma* Windows PE** (dove *piattaforma* è l'architettura dell'immagine Windows PE da configurare).  

6.  Nella sezione **Aggiunta driver** scegliere i tipi di driver appropriati da includere.  

    > [!NOTE]
    >  Questo passaggio non è necessario se Windows PE include già i driver di dispositivo necessari.  

7.  Nell'elenco dei **profili di selezione** della sezione **Aggiunta driver** selezionare il profilo di selezione driver appropriato.  

8.  Nella finestra di dialogo **Proprietà** fare clic su **OK**.  

    > [!NOTE]
    >  Questo passaggio non è necessario se Windows PE include già i driver di dispositivo necessari.  

9. Nel riquadro dei dettagli fare clic su ***condivisione_distribuzione*** (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

10. Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

11. Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

12. Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

13. Fare clic su **Fine** nella pagina **Conferma**.  

     Al termine del processo la cartella di avvio nella condivisione di distribuzione conterrà alcune immagini di avvio, ad esempio:  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 È possibile scrivere i file ISO che sono stati generati direttamente su CD o DVD oppure usarli per inizializzare il processo LTI nel nuovo hardware. È anche possibile importare i file WIM di avvio in Servizi di distribuzione Windows, in modo che i nuovi computer siano in grado di inizializzare il processo di distribuzione LTI senza richiedere supporti fisici.  

 **Per importare l'immagine Windows PE in Servizi di distribuzione Windows**  

1.  Avviare la console di Servizi di distribuzione Windows e quindi connettersi a Servizi di distribuzione Windows.  

2.  Nell'albero della console fare clic con il pulsante destro del mouse su **Immagini d'avvio**, quindi su **Aggiungi immagine d'avvio**.  

3.  Scorrere fino all'immagine WIM da importare, ad esempio, D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim.  

4.  Il processo di importazione legge automaticamente i metadati dall'immagine di avvio, ma i valori di **Nome immagine** e **Descrizione immagine** possono essere modificati. **Nome immagine** riguarda le informazioni sulle opzioni di avvio visualizzate da Windows Boot Manager quando il client si avvia in PXE.  

5.  Se l'immagine di avvio è stata importata, qualsiasi computer che esegue l'avvio PXE e riceve una risposta da Servizi di distribuzione Windows sarà in grado di scaricare l'immagine di avvio LTI e di avviare un'installazione LTI.  

 L'installazione e la configurazione di Servizi di distribuzione Windows non sono trattate in questa guida. Per altre informazioni su Servizi di distribuzione Windows, vedere la [Guida di Servizi di distribuzione Windows](http://technet.microsoft.com/library/cc265612.aspx).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Usare Servizi di distribuzione Windows per rilevare automaticamente il server di distribuzione  
 Un'altra opzione è disponibile quando si usa Servizi di distribuzione Windows per ospitare le immagini d'avvio MDT quando la condivisione di distribuzione MDT è ospitata nello stesso server di Servizi di distribuzione Windows.  

 Quando un client PXE carica l'immagine di avvio MDT, il nome del server di Servizi di distribuzione Windows che ospita l'immagine di avvio viene acquisito e inserito nella proprietà **WDSServer** di MDT. È quindi possibile fare riferimento a questa proprietà nel file BootStrap.ini dell'immagine d'avvio e nel file CustomSettings.ini della condivisione di distribuzione dalla proprietà **DeployRoot**. In questo modo si ottiene un client che si avvia da Servizi di distribuzione Windows usando automaticamente la condivisione di distribuzione ospitata nel server di Servizi di distribuzione Windows. Questo elimina la necessità di specificare un nome di server in qualsiasi file di configurazione.  

 **Per impostare il server di Servizi di distribuzione Windows locale come server di distribuzione**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Advanced Configuration/Database (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Fare clic sulla scheda **Regole**.  

     Le informazioni digitate in questa scheda vengono archiviate nel file CustomSettings.ini.  

5.  Configurare la proprietà **DeployRoot** in modo che usi la variabile **%WDSServer%**, ad esempio **DeployRoot=\\\\%WDSServer%\Deployment$**.  

6.  Fare clic su **Edit Bootstrap.ini** (Modifica Bootstrap.ini).  

7.  Configurare BootStrap.ini in modo che usi la proprietà **%WDSServer%** aggiungendo o modificando il valore **DeployRoot** in **DeployRoot=\\\\%WDSServer%\Deployment$**.  

8.  Nel menu **File** fare clic su **Salva** per salvare le modifiche apportate al file BootStrap.ini.  

9. Fare clic su **OK**.  

     La condivisione di distribuzione deve essere aggiornata.  

10. Nel riquadro dei dettagli fare clic su **condivisione_distribuzione** (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

11. Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

12. Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

13. Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

14. Fare clic su **Fine** nella pagina **Conferma**.  

15. Importare il file WIM di avvio aggiornato in Servizi di distribuzione Windows.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Opzione 2: distribuire un'immagine del sistema operativo dall'archivio di Servizi di distribuzione Windows  
 Se si sta già usando Servizi di distribuzione Windows per la distribuzione del sistema operativo, estendere le funzionalità di MDT configurandole in modo da fare riferimento a immagini del sistema operativo di Servizi di distribuzione Windows già in uso anziché usare l'archivio e integrare nelle distribuzioni di Servizi di distribuzione Windows la gestione dei driver, la distribuzione delle applicazioni, l'installazione degli aggiornamenti, l'elaborazione delle regole e altre funzionalità di MDT. Quando MDT fa riferimento a un'immagine del sistema operativo di Servizi di distribuzione Windows è possibile trattare l'immagine come qualsiasi sistema operativo preparato per il commit in una condivisione di distribuzione MDT.  

 **Per fare riferimento a un'immagine del sistema operativo di Servizi di distribuzione Windows**  

> [!NOTE]
>  I passaggi seguenti richiedono che almeno un'immagine del sistema operativo sia già stata importata nel server di Servizi di distribuzione Windows.  

1.  Aggiornare MDT affinché sia in grado di accedere alle immagini di Servizi di distribuzione Windows copiando i file seguenti dalla cartella delle origini del supporto di Windows nella cartella C:\Programmi\Microsoft Deployment Toolkit\bin nel server di Servizi di distribuzione Windows:  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (applicabile solo se si esegue la copia dalle directory di origine di Windows Server 2008)  

    > [!NOTE]
    >  La directory di origine di Windows in uso deve corrispondere alla piattaforma del sistema operativo in esecuzione nel computer in cui è installato MDT.  

2.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

3.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Operating Systems (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

4.  Nel riquadro Azioni fare clic su **Import Operating System** (Importa sistema operativo).  

     Viene avviata la creazione guidata del sistema operativo.  

5.  Nella pagina **Tipo di sistema operativo** fare clic su **Immagini di Servizi di distribuzione Windows** e quindi fare clic su **Avanti**.  

6.  Nella pagina **Server WDS** digitare il nome del server di Servizi di distribuzione Windows a cui fare riferimento, ad esempio **WDSSvr001**, e quindi fare clic su **Avanti**.  

7.  Nella pagina **Riepilogo** verificare che le impostazioni siano corrette e quindi fare clic su **Avanti**.  

8.  Fare clic su **Fine** nella pagina **Conferma**.  

     Tutte le immagini disponibili nel server di Servizi di distribuzione Windows saranno ora disponibili per le sequenze di attività di MDT.  

> [!NOTE]
>  L'importazione delle immagini da Servizi di distribuzione Windows non implica la copia dei file di origine dal server di Servizi di distribuzione Windows nella condivisione di distribuzione. MDT continua a usare i file di origine dal percorso originale.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Opzione 3: usare la funzionalità multicast con MDT e il ruolo server Servizi di distribuzione Windows di Windows Server 2008  
 Con il rilascio di Windows Server 2008, Servizi di distribuzione Windows è stato migliorato per supportare la distribuzione di immagini usando le trasmissioni multicast. MDT include anche gli aggiornamenti per l'integrazione di MDT con il multicasting di Servizi di distribuzione Windows.  

 Inoltre, la versione 1.1 aggiornata di Windows Automated Installation Kit (Windows AIK) include Wdsmcast.exe. Ciò consente di aggiungere manualmente le sessioni multicast ai join e al client che avvia Wdsmcast.exe di copiare i file da una sessione multicast attiva.  

 Lo script LTIApply.wsf usa Wdsmcast.exe quando accede ai file di origine del sistema operativo dalla condivisione di distribuzione. LTIApply.wsf cerca Wdsmcast.exe nella condivisione di distribuzione nella cartella *condivisione_distribuzione*\Tools\x86 o *condivisione_distribuzione*\Tools\x64 (dove *condivisione_distribuzione* è il nome della cartella del file system che contiene la condivisione di distribuzione), a seconda della versione di Windows PE in esecuzione.  

 Quando LTIApply.wsf è in esecuzione tenta sempre di accedere e scaricare le immagini WIM da un flusso multicast esistente, ma esegue il fallback a un file standard se non esiste un flusso multicast.  

> [!NOTE]
>  Questo processo si applica solo ai file di immagine WIM.  

 I prerequisiti del server di distribuzione per la preparazione per il multicast di MDT sono:  

-   Il server di distribuzione deve eseguire Windows Server 2008 o versioni successive  

-   Il ruolo Servizi di distribuzione Windows deve essere installato dalla console di gestione del server  

-   Windows AIK 1.1 per Windows Server 2008 deve essere installato  

-   MDT deve essere installato  

-   Come con qualsiasi distribuzione in cui si usa MDT, deve essere stata importata almeno un'immagine WIM del sistema operativo, come set completo di file di origine o come immagine personalizzata con file di installazione  

> [!NOTE]
>  È importante usare la versione più recente di Windows AIK per il multicast. La copia di Windows PE inclusa nelle versioni precedenti di Windows AIK, ad esempio Windows AIK 1.0, non supporta il download da un server multicast.  

 **Per configurare MDT per il multicast da una condivisione di distribuzione esistente**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Nella scheda **Generali** selezionare l'opzione che consente di **abilitare il multicast per la condivisione di distribuzione** (richiede Servizi di distribuzione Windows di Windows Server 2008).  

5.  Fare clic su **OK**.  

6.  Fare clic su **Update Deployment Share** (Aggiorna condivisione di distribuzione).  

     Viene avviata la procedura guidata di aggiornamento della condivisione di distribuzione.  

7.  Nella pagina **Opzioni** selezionare le opzioni da usare per l'aggiornamento della condivisione di distribuzione e quindi fare clic su **Avanti**.  

8.  Nella pagina **Riepilogo** verificare che le informazioni siano corrette e quindi fare clic su **Avanti**.  

9. Fare clic su **Fine** nella pagina **Conferma**.  

 La condivisione di distribuzione è ora configurata per la trasmissione multicast di Servizi di distribuzione Windows.  

 Questo processo crea una trasmissione multicast di Servizi di distribuzione Windows di tipo automatico che usa direttamente la condivisione di distribuzione MDT esistente. MDT non crea trasmissioni multicast pianificate. Si noti inoltre che non vengono importate immagini aggiuntive in Servizi di distribuzione Windows e che non è possibile usare il multicast per le immagini di avvio, poiché il client multicast non può essere caricato finché Windows PE è in esecuzione.  

 **Per verificare che la trasmissione multicast sia stata generata in Servizi di distribuzione Windows**  

1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione** e quindi fare clic su **Servizi di distribuzione Windows**.  

2.  Nell'albero della console di Servizi di distribuzione Windows fare clic con il pulsante destro del mouse su **Server**, quindi fare clic su **Aggiungi server**.  

3.  Nella finestra di dialogo **Aggiungi server** fare clic su **Computer locale**, quindi scegliere **OK**.  

4.  Nell'albero della console di Servizi di distribuzione Windows fare clic su **Server**, quindi su ***nome_server*** (dove *nome_server* è il nome del computer che esegue Servizi di distribuzione Windows). Fare clic su **Trasmissioni multicast**.  

5.  Nel riquadro dei dettagli viene visualizzata una nuova trasmissione multicast automatica per la condivisione di distribuzione, ad esempio **BDD Share Deployments$**.  

6.  Verificare che lo stato della trasmissione multicast automatica **BDD Share Deployments$** sia impostato su **Attivo**.  

 Dopo la distribuzione di un computer, verificare che il sistema operativo sia stato scaricato da una trasmissione multicast esaminando il file BDD.log nella cartella \Windows\Temp\DeploymentLogs.  

 Nella cartella dei log saranno presenti due voci, che iniziano entrambe con **Multicast transfer**, controllarle per verificare che il trasferimento sia stato completato correttamente. Per altre informazioni sulle trasmissioni multicast con MDT e Servizi di distribuzione Windows, vedere la sezione relativa all'abilitazione della distribuzione multicast di Servizi di distribuzione Windows per le distribuzioni LTI nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Esecuzione di pre-distribuzioni con MDT (precaricamento OEM)  
 In molte organizzazioni i computer vengono caricati con l'immagine del sistema operativo prima della distribuzione nella rete di produzione. In alcuni casi il caricamento dell'immagine del sistema operativo viene eseguito da un team interno all'organizzazione responsabile per la configurazione dei computer in un ambiente di gestione temporanea. In altri casi il caricamento dell'immagine del sistema operativo viene eseguito dal fornitore dell'hardware del computer, noto anche come *OEM* (Original Equipment Manufacturer).  

> [!NOTE]
>  Il processo di precaricamento OEM è supportato in MDT solo per le distribuzioni eseguite con LTI. Per Configuration Manager, usare la funzionalità di supporto pre-installata.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Panoramica del processo di precaricamento OEM in MDT  
 Il processo di precaricamento OEM è suddiviso in tre fasi:  

-   **Fase 1**. Creare un'immagine basata su supporto del computer di riferimento da applicare nell'ambiente di gestione temporanea.  

-   **Fase2**. Applicare l'immagine del computer di riferimento al computer di destinazione in un ambiente di gestione temporanea.  

-   **Fase 3**. Effettuare una distribuzione completa del computer di destinazione nell'ambiente di produzione.  

 Le fasi 1 e 3 vengono in genere eseguite dall'organizzazione di distribuzione. In base all'uso del processo di precaricamento OEM nell'organizzazione, la fase 2 può essere eseguita dall'organizzazione o dal fornitore dell'hardware dei computer in uso. Se l'organizzazione esegue la fase 2, l'ambiente di gestione temporanea è interno all'organizzazione. Se un OEM esegue la fase 2, l'ambiente di gestione temporanea è nell'ambiente dell'OEM.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Panoramica dei file di configurazione di MDT nel processo di precaricamento OEM  
 I file di configurazione di MDT (CustomSettings.ini e bootstrap.ini) vengono usati separatamente dalle sequenze di attività eseguite durante la fase 1 e la fase 3 del processo di precaricamento OEM. Tuttavia, entrambi i file di configurazione sono presenti contemporaneamente in strutture di cartelle diverse.  

 Nella prima fase i file di configurazione vengono usati durante la creazione del computer di riferimento e vengono archiviati nella cartella specifica per la sequenza di attività usata in quella fase. I file di configurazione usati nella terza e ultima fase del processo di precaricamento OEM vengono archiviati nella cartella specifica della sequenza di attività usata in quella fase.  

 Quando si apportano modifiche ai file di configurazione, verificare che le modifiche apportate al file di configurazione corrispondano alla sequenza di attività appropriata in ogni fase del processo di precaricamento OEM.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Panoramica dei file di log di MDT nel processo di precaricamento OEM  
 Vengono generati file di log di MDT separati durante la fase 1 e la fase 3 del processo di precaricamento OEM:  

-   I file di log di MDT per la fase 1 vengono archiviati nelle cartelle C:\MININT e C:\SMSTSLog.  

-   I file di log di MDT per la fase 3 vengono archiviati nella cartella %WINDIR%\System32\CCM\Logs per le distribuzioni basate su x86 o nella cartella %WINDIR%\SysWow64\CCM\Logs per le distribuzioni basate su x64.  

 Usare la cartella appropriata per la diagnosi o la risoluzione dei problemi di distribuzione correlati a MDT.  

### <a name="staged-deployments-using-lti"></a>Pre-distribuzioni eseguite con LTI  
 Per le distribuzioni LTI, eseguire il processo di precaricamento OEM usando una condivisione di distribuzione di tipo *Supporto rimovibile*. Gli altri tipi di condivisione di distribuzione non sono supportati per il processo di precaricamento OEM.  

 Per eseguire il processo di precaricamento OEM, creare una sequenza di attività basata sul modello di sequenza di attività Litetouch OEM Task Sequence, oltre a eventuali sequenze di attività che verranno usate per distribuire il sistema operativo di destinazione. Creare quindi una condivisione di distribuzione di tipo *Supporto rimovibile* che consente di creare un file ISO del contenuto della condivisione di distribuzione, in particolare il file LiteTouchPE_x86.iso o il file LiteTouchPE_x64.iso (in base alla piattaforma del processore del computer di destinazione). Il processo di aggiornamento della condivisione di distribuzione crea inoltre una struttura di cartelle che possono essere usate per creare supporti Universal Disk Format.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>Processo di precaricamento OEM LTI - Fase 1: creare un'immagine basata su supporto  
 L'organizzazione di distribuzione esegue la prima fase del processo di precaricamento OEM. Il risultato finale di questa fase è un'immagine di avvio, ad esempio un file ISO, o un supporto, ad esempio un DVD, che viene inviato all'OEM o all'ambiente di gestione temporanea all'interno dell'organizzazione di distribuzione. La maggior parte di questi passaggi vengono eseguiti in Deployment Workbench.  

 **Per creare un'immagine basata su supporto per il recapito all'OEM o all'ambiente di gestione temporanea all'interno dell'organizzazione di distribuzione**  

1.  Popolare i seguenti nodi per la condivisione di distribuzione in Deployment Workbench:  

    -   Sistemi operativi  

    -   Applicazioni  

    -   Pacchetti  

    -   Driver non inclusi  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla gestione delle condivisioni di distribuzione in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

2.  Creare una nuova sequenza di attività basata sul modello di sequenza di attività Litetouch OEM Task Sequence di Deployment Workbench.  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla configurazione delle sequenze di attività in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

3.  Creare una o più sequenze di attività che verranno usate per distribuire il sistema operativo di destinazione nel computer di destinazione dopo la distribuzione nell'ambiente di produzione.  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla configurazione delle sequenze di attività in Deployment Workbench nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

4.  Creare un profilo di selezione che includa le applicazioni, i sistemi operativi, i driver, i pacchetti e le sequenze di attività necessari per la distribuzione OEM.  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla gestione dei profili di selezione nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

5.  Creare i supporti di distribuzione.  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla gestione dei supporti per la distribuzione LTI nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

6.  Aggiornare i supporti di distribuzione creati in Deployment Workbench nel passaggio precedente.  

     Quando si aggiorna il supporto di distribuzione, Deployment Workbench crea il file LiteTouchMedia.iso. Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa alla gestione dei supporti per la distribuzione LTI nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

7.  Creare un DVD del file LiteTouchMedia.iso creato nel passaggio precedente.  

    > [!NOTE]
    >  Se si invia il file ISO all'OEM o all'ambiente di gestione temporanea dell'organizzazione, questo passaggio non è necessario.  

8.  Inviare il file ISO o il DVD all'OEM o all'ambiente di gestione temporanea dell'organizzazione.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>Processo di precaricamento OEM LTI - Fase 2: applicare l'immagine al computer di destinazione  
 La seconda fase del processo di precaricamento OEM viene eseguita dall'OEM o dal team di distribuzione nell'ambiente di gestione temporanea dell'organizzazione di distribuzione. Durante questa fase del processo, il file ISO o DVD creato nella fase 1 viene applicato ai computer di destinazione. Il risultato finale di questa fase è l'immagine distribuita nei computer di destinazione in modo che siano pronti per la distribuzione nell'ambiente di produzione.  

 **Per applicare l'immagine ai computer di destinazione**  

1.  Avviare un computer di destinazione con il supporto creato nella fase 1.  

     Dopo l'avvio di Windows PE viene avviata anche la distribuzione guidata di Windows.  

2.  Nella distribuzione guidata di Windows fare clic sulla **sequenza di attività di preinstallazione OEM per l'ambiente di gestione temporanea**.  

     La sequenza di attività viene avviata e il contenuto del supporto di avvio viene copiato nel disco rigido locale del computer di destinazione.  

3.  Quando la distribuzione guidata di Windows viene completata per la **sequenza di attività di preinstallazione OEM per l'ambiente di gestione temporanea** il disco rigido è pronto per avviare il resto del processo di distribuzione eseguendo la procedura guidata di Windows per le altre sequenze di attività usate per distribuire il sistema operativo.  

     La **sequenza di attività di preinstallazione OEM per l'ambiente di gestione temporanea** è responsabile della distribuzione dell'immagine al computer di destinazione e dell'avvio del processo LTI. La distribuzione guidata di Windows viene avviata una seconda volta per eseguire le sequenze di attività usate per distribuire il sistema operativo nel computer di destinazione.  

4.  Clonare il contenuto del primo disco rigido per il numero necessario di computer di destinazione nell'ambiente di gestione temporanea.  

5.  I computer di destinazione vengono recapitati all'ambiente di produzione per la distribuzione.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>Processo di precaricamento OEM LTI - Fase 3: completare la distribuzione del computer di destinazione  
 La terza e ultima fase del processo di precaricamento OEM viene eseguita nell'ambiente di produzione dell'organizzazione di distribuzione. Durante questa fase del processo, viene avviato il computer di destinazione e l'immagine del supporto di avvio, situata nel disco rigido nell'ambiente di gestione temporanea, si avvia.  

 **Per completare la distribuzione del computer di destinazione nell'ambiente di produzione**  

1.  Avviare il computer di destinazione.  

     Dopo l'avvio di Windows PE viene avviata anche la distribuzione guidata di Windows.  

2.  Completare la distribuzione guidata di Windows usando le informazioni di configurazione specifiche per ogni computer di destinazione.  

     Per altre informazioni sull'esecuzione di questo passaggio, vedere la sezione relativa all'esecuzione della distribuzione guidata nel documento di MDT *Uso di Microsoft Deployment Toolkit*.  

 Al termine di questa fase, il computer di destinazione sarà pronto per l'uso nell'ambiente di produzione.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Uso di Windows PowerShell per eseguire attività comuni  
 Le attività di amministrazione di MDT vengono eseguite in Deployment Workbench dai cmdlet di Windows PowerShell sottostanti, che possono essere usati per automatizzare le attività di amministrazione, ad esempio quelle descritte nelle sezioni seguenti.  

 È possibile automatizzare l'amministrazione di MDT attenendosi alla procedura seguente:  

-   Creare una nuova condivisione di distribuzione come descritto in [Creazione di una nuova condivisione di distribuzione](#CreateNewDeployShare).  

-   Creare una cartella in una condivisione di distribuzione come descritto in [Creazione di una cartella](#CreateFolder).  

-   Eliminare una cartella da una condivisione di distribuzione come descritto in [Eliminazione di una cartella](#DeleteFolder).  

-   Importare un driver di dispositivo in una condivisione di distribuzione come descritto in [Importazione di un driver di dispositivo](#ImportDeviceDriver).  

-   Eliminare un driver di dispositivo da una condivisione di distribuzione come descritto in [Eliminazione di un driver di dispositivo](#DeleteDeviceDriver).  

-   Importare un pacchetto del sistema operativo in una condivisione di distribuzione come descritto in [Importazione di un pacchetto del sistema operativo](#ImportOpSysPackage).  

-   Eliminare un pacchetto del sistema operativo da una condivisione di distribuzione come descritto in [Eliminazione di un pacchetto del sistema operativo](#DeleteOpSysPackage).  

-   Importare un sistema operativo in una condivisione di distribuzione come descritto in [Importazione di un sistema operativo](#ImportOpSys).  

-   Eliminare un sistema operativo da una condivisione di distribuzione come descritto in [Eliminazione di un sistema operativo](#DeleteOpSys).  

-   Creare un'applicazione in una condivisione di distribuzione come descritto in [Creazione di un'applicazione](#CreateApplication).  

-   Eliminare un'applicazione da una condivisione di distribuzione come descritto in [Eliminazione di un'applicazione](#DeleteApplication).  

-   Creare una sequenza di attività in una condivisione di distribuzione come descritto in [Creazione di una sequenza di attività](#CreateTaskSequence).  

-   Eliminare una sequenza di attività da una condivisione di distribuzione come descritto in [Eliminazione di una sequenza di attività](#DeleteTaskSequence).  

-   Creare un database MDT come descritto in [Creazione di un database MDT](#CreateMDTDB).  

-   Creare un profilo di selezione come descritto in [Creazione di un profilo di selezione](#CreateSelectProfile).  

-   Aggiornare una condivisione di distribuzione come descritto in [Aggiornamento di una condivisione di distribuzione](#UpdatingDeployShare).  

-   Creare una condivisione di distribuzione collegata come descritto in [Creazione di una condivisione di distribuzione collegata](#CreateLinkedDeployShare).  

-   Aggiornare una condivisione di distribuzione collegata come descritto in [Aggiornamento di una condivisione di distribuzione collegata](#UpdatingLinkedDeployShare).  

-   Eliminare una condivisione di distribuzione collegata come descritto in [Eliminazione di una condivisione di distribuzione collegata](#DeleteLinkedDeployShare).  

-   Creare i supporti di distribuzione come descritto in [Creazione di supporti](#CreateMedia).  

-   Generare i supporti di distribuzione come descritto in [Generazione di supporti](#GenerateMedia).  

-   Eliminare i supporti di distribuzione come descritto in [Eliminazione di supporti](#DeleteMedia).  

###  <a name="CreateNewDeployShare"></a> Creazione di una nuova condivisione di distribuzione  
 I seguenti comandi di Windows PowerShell creano una nuova condivisione di distribuzione denominata *Production$* in D:\Production Deployment Share. La nuova condivisione di distribuzione verrà visualizzata in Deployment Workbench come Production.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Creazione di una cartella  
 I seguenti comandi di Windows PowerShell creano una cartella di Adobe nell'albero della console di Deployment Workbench in Deployment Workbench\/Deployment Shares\/Production\/Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  L'aggiunta di "`remove-psdrive`" allo script assicura che il processo in background termini prima di procedere.  

###  <a name="DeleteFolder"></a> Eliminazione di una cartella  
 I seguenti comandi di Windows PowerShell eliminano la cartella Deployment Workbench\/Deployment Shares\/Productions\/Applications\/Adobe.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  Lo script avrà esito negativo se la cartella non è vuota.  

###  <a name="ImportDeviceDriver"></a> Importazione di un driver di dispositivo  
 I seguenti comandi di Windows PowerShell importano il driver di dispositivo del monitor Dell 2407 WFP nella condivisione di distribuzione Production.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Eliminazione di un driver di dispositivo  
 I seguenti comandi di Windows PowerShell eliminano il driver del monitor Dell 2407 WFP dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importazione di un pacchetto del sistema operativo  
 I seguenti comandi di Windows PowerShell importano tutti i pacchetti del sistema operativo situati in D:\\Updates\\Microsoft\\Vista. Questi pacchetti del sistema operativo verranno archiviati nella condivisione di distribuzione Production, che si trova in D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Eliminazione di un pacchetto del sistema operativo  
 I seguenti comandi di Windows PowerShell eliminano il pacchetto del sistema operativo dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importazione di un sistema operativo  
 I seguenti comandi di Windows PowerShell importano il sistema operativo Windows Vista situato in D:\\Operating Systems\\Windows Vista x86. Il sistema operativo verrà archiviato nella condivisione di distribuzione Production, che si trova in D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Eliminazione di un sistema operativo  
 I seguenti comandi di Windows PowerShell eliminano il sistema operativo Windows Vista HOMEBASIC dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Creazione di un'applicazione  
 I seguenti comandi di Windows PowerShell creano l'applicazione Adobe Reader 9 usando i file di origine da D:\\Software\\Adobe\\Reader 9. L'applicazione verrà archiviata nella condivisione di distribuzione Production, che si trova in D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Eliminazione di un'applicazione  
 I seguenti comandi di Windows PowerShell eliminano l'applicazione Adobe Reader 9 dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Creazione di una sequenza di attività  
 I seguenti comandi di Windows PowerShell creano la sequenza di attività **Windows Vista Production Build** nella condivisione di distribuzione Production, che si trova nell'unità D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Eliminazione di una sequenza di attività  
 I seguenti comandi di Windows PowerShell eliminano la sequenza di attività **Windows Vista Production Build** dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Creazione di un database MDT  
 I seguenti comandi di Windows PowerShell creano un nuovo database MDT nel server *deployment\_server* dalla condivisione di distribuzione Production. Per la connessione al database viene usato il protocollo TCP\/IP.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Creazione di un profilo di selezione  
 I seguenti comandi di Windows PowerShell creano il nuovo profilo di selezione Applicazioni.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Aggiornamento di una condivisione di distribuzione  
 I seguenti comandi di Windows PowerShell aggiornano la condivisione di distribuzione Production situata in D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> Creazione di una condivisione di distribuzione collegata  
 I seguenti comandi di Windows PowerShell creano una condivisione di distribuzione collegata alla condivisione di distribuzione Production, che si trova nella condivisione \\\\*remote\_server\_name*\\Deployment$. Il profilo di selezione Everything viene usato per determinare il tipo di contenuto che verrà replicato nella condivisione di distribuzione collegata. Il contenuto della condivisione di distribuzione Production verrà unito al contenuto già esistente nella condivisione \\\\*remote\_server\_name*\\Deployment$.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Aggiornamento di una condivisione di distribuzione collegata  
 I seguenti comandi di Windows PowerShell aggiornano la condivisione di distribuzione LINKED001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Eliminazione di una condivisione di distribuzione collegata  
 I seguenti comandi di Windows PowerShell eliminano la condivisione di distribuzione LINKED001.  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Creazione di supporti  
 I seguenti comandi di Windows PowerShell creano una cartella di origine che contiene i contenuti usati per creare i supporti di avvio. La condivisione di distribuzione Production verrà usata come origine. Il profilo di selezione Everything determina quale contenuto viene inserito nella cartella del contenuto del supporto. Il file LiteTouchMedia.iso viene creato quando viene generato il supporto. Il supporto è compatibile con le piattaforme x86 e x64.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Generazione di supporti  
 I seguenti comandi di Windows PowerShell creano il file LiteTouchMedia.iso in D:\\Media, che userà il contenuto della cartella di origine del supporto MEDIA001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> Eliminazione di supporti  
 I seguenti comandi di Windows PowerShell eliminano il supporto MEDIA001 dalla condivisione di distribuzione Production.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Ritardo dell'aggiunta al dominio per evitare l'applicazione di oggetti Criteri di gruppo  
 Criteri di gruppo è una tecnologia avanzata e flessibile che consente di gestire in modo efficiente un numero elevato di oggetti computer e utente di Active Directory Domain Services (AD DS) usando un modello centralizzato uno-a-molti. Le impostazioni di Criteri di gruppo sono contenute in un oggetto Criteri di gruppo e collegate a uno o più contenitori di servizi AD DS, tra cui siti, domini e unità organizzative.  

 Alcune organizzazioni usano impostazioni restrittive di Criteri di gruppo che possono causare problemi durante le distribuzioni del sistema operativo. Ad esempio, le seguenti impostazioni di Criteri di gruppo possono interrompere un processo di accesso automatico:  

-   Restrizioni dell'accesso automatico  

-   Ridenominazione dell'account amministratore  

-   Didascalie e banner legali  

-   Criteri di sicurezza restrittivi, ad esempio Specialized Security – Limited Functionality (SSLF)  

 Un'opzione per risolvere i problemi che un oggetto Criteri di gruppo può causare durante la distribuzione è aggiungere il computer al dominio il più tardi possibile nel processo di distribuzione. L'aggiunta può essere effettuata usando una sequenza di attività personalizzata che esegue lo script ZTIDomainJoin.wsf.  

 Per aggiungere il computer di destinazione al dominio, lo script ZTIDomainJoin.wsf usa le proprietà **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**, **JoinDomain** e **MachineObjectOU**. È possibile dichiarare queste proprietà usando la distribuzione guidata di Windows, le regole di condivisione di distribuzione, il database MDT e le regole di computer e raccolta di Configuration Manager. L'account usato deve avere i diritti necessari per creare ed eliminare oggetti computer nel dominio.  

 In genere, lo script ZTIConfigure.wsf aggiorna il file Unattend.xml o Unattend.txt con i valori specificati da queste proprietà. Queste impostazioni vengono quindi analizzate dal programma di installazione di Windows e il sistema tenta di eseguire l'aggiunta al dominio nelle prime fasi del processo di distribuzione. In questo modo il computer di destinazione è soggetto alle impostazioni specificate negli oggetti Criteri di gruppo del dominio e il processo di distribuzione può avere esito negativo.  

 Per ritardare intenzionalmente l'aggiunta del computer di destinazione al dominio durante il processo di distribuzione, è possibile rimuovere determinati elementi dal file Unattend.xml. Lo script ZTIConfigure.wsf salterà la scrittura delle proprietà nel file Unattend.xml se l'elemento proprietà associato manca nel file.  

> [!NOTE]
>  Questo esempio di risoluzione è valido solo quando si distribuiscono i sistemi operativi Windows 7, Windows Server 2008 o Windows Server 2008 R2.  

 **Preparare il file unattend.xml in modo che il computer di destinazione non tenti di eseguire l'aggiunta al dominio durante l'installazione di Windows**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences/*sequenza_attività* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione e *sequenza_attività* è il nome della sequenza di attività da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Nella scheda delle **informazioni sul sistema operativo** fare clic su **Edit Unattend.xml** (Modifica Unattend.xml).  

     Viene avviato Windows System Image Manager.  

5.  Nel riquadro **File di risposte** accedere a **4 specialize/Identification/Credentials**. Fare clic con il pulsante destro del mouse su **Credentials** e quindi fare clic su **Elimina**.  

6.  Fare clic su **Sì**.  

7.  Salvare il file di risposte e quindi chiudere Windows System Image Manager.  

8.  Fare clic su **OK** nella finestra di dialogo **Proprietà** della sequenza di attività.  

 Con gli elementi `Credentials` mancanti nel file unattend.xml, lo script ZTIConfigure.wsf non è in grado di popolare le informazioni sull'aggiunta al dominio nel file Unattend.xml, che impediscono a Installazione di Windows di tentare l'aggiunta al dominio.  

 **Per aggiungere un passaggio della sequenza di attività che aggiunge il computer di destinazione al dominio**  

1.  Fare clic su **Start**, quindi scegliere **Tutti i programmi**. Scegliere **Microsoft Deployment Toolkit**, quindi fare clic su **Deployment Workbench**.  

2.  Nell'albero della console di Deployment Workbench passare a Deployment Workbench/Deployment Shares/*condivisione_distribuzione*/Task Sequences/*sequenza_attività* (dove *condivisione_distribuzione* è il nome della condivisione di distribuzione e *sequenza_attività* è il nome della sequenza di attività da configurare).  

3.  Nel riquadro Azioni fare clic su **Proprietà**.  

4.  Nella scheda **Sequenza di attività** selezionare ed espandere il nodo Ripristino stato.  

5.  Verificare che il passaggio **Recover From Domain** (Recupera da dominio) sia presente. In caso affermativo, andare al passaggio 9.  

6.  Nella finestra di dialogo **Proprietà** della sequenza di attività fare clic su **Aggiungi**, passare a **Impostazioni** e fare clic su **Recover From Domain** (Recupera da dominio).  

7.  Aggiungere il passaggio **Recover From Domain** (Recupera da dominio) della sequenza di attività all'editor delle sequenze di attività. Verificare che il passaggio sia nella posizione corretta nella sequenza di attività.  

8.  Verificare che le impostazioni per il passaggio **Recover From Domain** (Recupera da dominio) della sequenza di attività siano configurate in modo da soddisfare le proprie esigenze.  

9. Fare clic su **OK** nella finestra di dialogo **Proprietà** della sequenza di attività per salvare la sequenza di attività.
