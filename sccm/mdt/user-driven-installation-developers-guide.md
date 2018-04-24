---
title: Installazione guidata dall'utente
titleSuffix: Microsoft Deployment Toolkit
description: "Guida per gli sviluppatori all'installazione guidata dall'utente di Microsoft Deployment Toolkit 2013. "
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2018
---
# <a name="user-driven-installation---developers-guide"></a>Installazione guidata dall'utente - Guida per gli sviluppatori
L'installazione guidata dall'utente (UDI, User Driven Installation) semplifica la distribuzione dei sistemi operativi client Windows®, quali Windows 8.1, a computer che usano la funzionalità di distribuzione del sistema operativo (OSD, Operating System Deployment) in Configuration Manager di Microsoft® System Center 2012 R2. L'UDI è inclusa nel Microsoft Deployment Toolkit (MDT).  

## <a name="introduction"></a>Introduzione  
 Quando si distribuiscono sistemi operativi con la funzionalità OSD è in genere necessario specificare tutte le informazioni per la distribuzione del sistema operativo. Le informazioni sono strutturate in file di configurazione o in database (ad esempio nel file CustomSettings.ini o nel database MDT [MDT DB]). È necessario specificare tutte le impostazioni di configurazione prima di poter avviare la distribuzione.  

 L'UDI offre un'interfaccia gestite da procedure guidate che consente di distribuire informazioni di configurazione immediatamente prima di eseguire la distribuzione. Questo comportamento consente di creare sequenze di attività di distribuzione del sistema operativo generiche e di specificare informazioni dettagliate per il computer al momento della distribuzione, per una flessibilità ottimale nel processo di distribuzione.  

### <a name="target-audience"></a>Destinatari  
 Questa guida è destinata agli sviluppatori che creano pagine personalizzate per la procedura guidata UDI ed editor di pagine personalizzate della procedura guidata per UDI Wizard Designer. Questa guida presuppone che l'utente conosca lo sviluppo di applicazioni Windows con:  

-   C++, che consente di creare pagine personalizzate della procedura guidata  

-   Microsoft .NET Framework, usato per la creazione di editor di pagine personalizzate della procedura guidata  

-   Windows Presentation Foundation (WPF), usato per la creazione di editor di pagine personalizzate della procedura guidata  

-   I linguaggi supportati da WPF, quali C#, C++ o Microsoft Visual Basic® .NET, usati per la creazione di editor di pagine personalizzate della procedura guidata  

### <a name="about-this-guide"></a>Informazioni su questa Guida  
 Questa guida specifica le informazioni di riferimento necessarie per la personalizzazione di UDI per l'organizzazione. Non illustra aspetti amministrativi o operativi come l'installazione di MDT (che include UDI), la configurazione di UDI per distribuire sistemi operativi e applicazioni o l'esecuzione di distribuzioni con la procedura guidata UDI. Per altre informazioni su questi argomenti, vedere gli argomenti UDI in *Uso di Microsoft Deployment Toolkit*, incluso in MDT.  

## <a name="udi-development-overview"></a>Panoramica sullo sviluppo dell'installazione guidata dall'utente (UDI)  
 Lo sviluppo dell'UDI consente di estendere le funzionalità dell'installazione guidata dall'utente. In genere, lo sviluppo dell'UDI è obbligatorio quando si vuole raccogliere informazioni aggiuntive necessarie per il processo di distribuzione dell'UDI. Queste informazioni aggiuntive vengono in genere salvate come variabili della sequenza di attività e vengono lette dai passaggi di una sequenza di attività UDI in Configuration Manager.  

### <a name="udi-architecture"></a>Architettura dell'installazione guidata dall'utente (UDI)  
 L'obiettivo principale dello sviluppo di UDI è la creazione di pagine personalizzate della procedura guidata, visualizzabili nella procedura guidata UDI. La creazione di pagine personalizzate della procedura guidata consente di estendere le funzionalità UDI esistenti per soddisfare i requisiti operativi e tecnici dell'organizzazione. Una pagina personalizzata della procedura guidata raccoglie informazioni in aggiunta o in sostituzione di quelle raccolte dalle pagine della procedura guidata UDI.  

 La figura 1 illustra la relazione tra UDI Wizard Designer e la procedura guidata UDI.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Figura 1. Relazione tra la procedura guidata UDI e UDI Wizard Designer  

 **Figura 1. Relazione tra la procedura guidata UDI e UDI Wizard Designer**  

 A livello concettuale, lo sviluppo dell'UDI include la creazione di:  

-   **Pagine personalizzate della procedura guidata**. Le pagine della procedura guidata vengono visualizzate nella procedura guidata UDI e raccolgono le informazioni necessarie per completare il processo di distribuzione. Per creare le pagine della procedura guidata si usa C++ in Microsoft Visual Studio®. Le pagine personalizzate della procedura guidata vengono implementate come DLL che vengono lette dalla procedura guidata UDI. Il Software Development Kit (SDK) dell'UDI include un esempio di creazione di pagine personalizzate della procedura guidata.  

-   **Editor di pagine personalizzate della procedura guidata**. Gli editor di pagine della procedura guidata consentono di configurare il comportamento delle pagine personalizzate della procedura guidata. Gli editor di pagine personalizzate della procedura guidata vengono implementati come DLL che vengono lette da UDI Wizard Designer. È possibile creare editor di pagine della procedura guidata usando:  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) versione 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) versione 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) versione 2.1  

     MDT include tutti gli assembly necessari per la creazione di un editor di pagine personalizzate della procedura guidata da usare in UDI Wizard Designer. Il SDK dell'UDI include un esempio di creazione di editor di pagine personalizzate della procedura guidata.  

 UDI Wizard Designer usa anche i file di supporto per la configurazione dell'editor di pagine della procedura guidata. I file di configurazione dell'editor di pagine della procedura guidata vengono creati nel processo di creazione delle pagine personalizzate della procedura guidata e degli editor di pagine personalizzate della procedura guidata. UDI Wizard Designer crea i dati XML necessari nel file di configurazione della procedura guidata UDI e nel file con estensione app corrispondente.  

### <a name="preparing-the-udi-development-environment"></a>Preparazione dell'ambiente di sviluppo dell'UDI  
 Prima di iniziare a creare pagine personalizzate della procedura guidata ed editor di pagine personalizzate della procedura guidata, seguire questa procedura per preparare l'ambiente di sviluppo dell'UDI:  

1.  Impostare i prerequisiti per l'ambiente di sviluppo dell'UDI come descritto in [Preparare i prerequisiti per l'ambiente di sviluppo dell'UDI](#PrepareUDIDevelopmentEnvironmentPrerequisites).  

2.  Configurare l'ambiente di sviluppo dell'UDI come descritto in [Configurare l'ambiente di sviluppo dell'UDI](#ConfigureUDIDevelopmentEnvironment).  

3.  Verificare che l'ambiente di sviluppo dell'UDI sia configurato correttamente, come descritto in [Verificare l'ambiente di sviluppo dell'UDI](#VerifyUDIDeploymentEnvironment).  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> Preparare i prerequisiti per l'ambiente di sviluppo dell'UDI  
 Per preparare i prerequisiti per l'ambiente di sviluppo dell'UDI, seguire questa procedura:  

1.  Impostare i prerequisiti hardware per l'ambiente di sviluppo dell'UDI come descritto in [Preparare i prerequisiti hardware per l'ambiente di sviluppo dell'UDI](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites).  

2.  Impostare i prerequisiti software per l'ambiente di sviluppo dell'UDI come descritto in [Preparare i prerequisiti software per l'ambiente di sviluppo dell'UDI](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites).  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> Preparare i prerequisiti hardware per l'ambiente di sviluppo dell'UDI  
 I prerequisiti hardware per l'ambiente di sviluppo dell'UDI sono gli stessi requisiti hardware validi per l'edizione di Microsoft Visual Studio 2010 in uso. Per altre informazioni su questi requisiti, vedere i requisiti di sistema per ogni edizione in [Prodotti Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> Preparare i prerequisiti software per l'ambiente di sviluppo dell'UDI  
 L'ambiente di sviluppo dell'UDI prevede i prerequisiti software seguenti:  

-   Qualsiasi sistema operativo che supporta Visual Studio 2010 (consigliato Windows 7 o Windows Server® 2008 R2).  

     È necessario un sistema operativo Windows che supporti l'architettura del processore per il quale si vuole sviluppare l'UDI. È possibile eseguire lo sviluppo dell'UDI a 32 bit e a 64 bit con un sistema operativo a 64 bit. Per lo sviluppo dell'UDI a 32 bit è necessario un sistema operativo a 32 bit. Per questo motivo è consigliabile usare un sistema operativo a 64 bit.  

    > [!NOTE]
    >  Le versioni IntelItanium (IA-64) del sistema operativo Windows non sono supportate per gli ambienti di sviluppo dell'UDI.  

     Per altre informazioni sui sistemi operativi che supportano Visual Studio 2010, vedere i requisiti di sistema per ogni edizione in [Prodotti Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework versione 4.0 (richiesto da Visual Studio 2010)  

-   Linguaggio C++ (usato per l'estensione delle pagine della procedura guidata UDI)  

-   Altri linguaggi supportati da WPF, ad esempio C#, Visual Basic .NET o C++/ Common Language Infrastructure, usati per l'estensione degli editor di pagine della procedura guidata di UDI Wizard Designer  

    > [!NOTE]
    >  Il codice sorgente di esempio per gli editor di pagine della procedura guidata di UDI Wizard Designer è scritto nel linguaggio C#. Per usare l'esempio di codice sorgente, installare il linguaggio C#.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> Configurare l'ambiente di sviluppo dell'UDI  
 Quando i prerequisiti dell'ambiente di sviluppo dell'UDI sono soddisfatti, seguire questa procedura per configurare l'ambiente di sviluppo dell'UDI:  

1.  Installare Visual Studio 2010.  

     Assicurarsi di installare il linguaggio C++ e qualsiasi altro linguaggio supportato da WPF.  

    > [!NOTE]
    >  Il codice sorgente di esempio per le pagine dell'editor di UDI Wizard Designer è scritto nel linguaggio C#. Per usare l'esempio di codice sorgente, installare il linguaggio C#.  

     Per altre informazioni sull'installazione di Visual Studio 2010, vedere [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx) (Installazione di Visual Studio).  

2.  Installare MDT.  

     Per altre informazioni su come installare MDT, vedere la sezione "Installing or Upgrading to MDT" (Installazione o aggiornamento a MDT) in *Uso di Microsoft Deployment Toolkit*.  

3.  In Esplora risorse creare *cartella_locale* (*cartella_locale* corrisponde a qualsiasi cartella su un'unità locale del computer di sviluppo).  

4.  Copiare la cartella *cartella_installazione*\SDK in *cartella_locale* (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *cartella_locale* è qualsiasi cartella su un'unità locale del computer di sviluppo).  

     La cartella SDK viene copiata in un'altra posizione perché MDT è installato nella cartella Programmi, in cui è possibile scrivere solo con autorizzazioni di accesso elevate. Copiando la cartella SDK in un'altra posizione è possibile modificare i file della cartella SDK anche senza avere autorizzazioni elevate.  

5.  Copiare la cartella *cartella_installazione*\Templates\Distribution\Tools in *cartella_locale* (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *cartella_locale* è la cartella creata in precedenza nel processo).  

6.  Rinominare la cartella *cartella_locale*\Tools come *cartella_locale*\OSDSetupWizard (dove *cartella_locale* è la cartella creata in precedenza nel processo).  

     Al termine, la struttura di cartelle sotto *cartella_locale* sarà simile a quella illustrata nella Figura 2 (dove *cartella_locale* è la cartella creata in precedenza nel processo e visualizzata come *UDIDevelopment* nella figura).  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Figura 2. Struttura di cartelle per lo sviluppo dell'UDI  

     **Figura 2. Struttura di cartelle per lo sviluppo dell'UDI**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> Verificare l'ambiente di sviluppo dell'UDI  
 Dopo aver configurato l'ambiente di sviluppo dell'UDI, confermare che l'ambiente sia configurato correttamente verificando che i progetti di esempio vengano compilati correttamente in Visual Studio 2010.  

 Verificare che l'ambiente di sviluppo dell'UDI sia configurato correttamente, confermando che:  

-   Il progetto SamplePage venga compilato correttamente, come descritto in [Verificare che il progetto SamplePage venga compilato correttamente](#VerifySamplePageProjectBuildsCorrectly)  

-   Il progetto SampleEditor venga compilato correttamente, come descritto in [Verificare che il progetto SampleEditor venga compilato correttamente](#VerifySampleEditorProjectBuildsCorrectly)  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> Verificare che il progetto SamplePage venga compilato correttamente  
 Il progetto SamplePage è un esempio di creazione di pagina personalizzata della procedura guidata per la procedura guidata UDI. Per altre informazioni sul progetto SamplePage, vedere [Esaminare la soluzione SamplePage di Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **Per verificare che il progetto SamplePage venga compilato correttamente**  

1.  Avviare Visual Studio 2010.  

2.  Aprire il progetto SamplePage.  

     Il progetto SamplePage si trova nel percorso *cartella_locale*\SDK\UDI\SamplePage (dove *cartella_locale* è la cartella creata in precedenza nel processo).  

3.  In Visual Studio 2010, in Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto SamplePage e quindi fare clic su **proprietà**.  

     Viene visualizzata la finestra di dialogo **Pagine delle proprietà SamplePage**.  

4.  Nella finestra di dialogo **Pagine delle proprietà SamplePage** accedere a Proprietà di configurazione/Debug.  

5.  Nell'area **Configurazione** delle proprietà Debug selezionare **Tutte le configurazioni**.  

6.  Nell'area **Comando** delle proprietà Debug digitare **$(TargetDir)\OSDSetupWizard.exe.**  

7.  Nell'area **Directory di lavoro** delle proprietà Debug digitare **$(TargetDir)**.  

8.  Nella finestra di dialogo **Pagine delle proprietà SamplePage** accedere a Proprietà di configurazione/Eventi di compilazione/Evento di post-compilazione.  

9. Nelle proprietà Evento di post-compilazione sotto **Riga di comando**, digitare quanto segue:  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. Nella finestra di dialogo **Pagine delle proprietà SamplePage** fare clic su **OK**.  

11. Salvare il progetto.  

12. Nel menu **Debug** fare clic su **Avvia debug**.  

     La finestra di dialogo **Microsoft Visual Studio** visualizzata indica che l'origine non è aggiornata e richiede se si vuole compilare il progetto.  

13. Nella finestra di dialogo **Microsoft Visual Studio** fare clic su **Sì**.  

     Viene visualizzata la finestra di dialogo **No Debugging Information** (Nessuna informazione di debug) indicante che non sono disponibili informazioni di debug per OSDSetupWizard.exe.  

14. Nella finestra di dialogo **No Debugging Information** (Nessuna informazione di debug), fare clic su **Sì**.  

     Viene visualizzata la procedura guidata UDI con la pagina personalizzata della procedura guidata.  

15. Verificare che sia possibile selezionare un valore in **Choose your location** (Scegli il percorso).  

16. Nel modulo **Wizard with sample page** (Procedura guidata con pagina di esempio) fare clic su **Annulla**.  

     Viene visualizzata la finestra di dialogo **Annulla procedura guidata**.  

17. Nella finestra di dialogo **Annulla procedura guidata** fare clic su **Sì**.  

18. Chiudere Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> Verificare che il progetto SampleEditor venga compilato correttamente  
 Il progetto SampleEditor è un esempio di creazione di editor di pagine personalizzate della procedura guidata per UDI Wizard Designer. Per altre informazioni sul progetto SampleEditor, vedere [Esaminare la soluzione SampleEditor di Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **Per verificare che il progetto SampleEditor venga compilato correttamente**  

1.  Avviare Visual Studio 2010.  

2.  Aprire il progetto SampleEditor.  

     Il progetto SampleEditor si trova nel percorso *cartella_locale*\SDK\UDI\SampleEditor (dove *cartella_locale* è la cartella creata in precedenza nel processo).  

3.  In Visual Studio 2010 aprire Esplora soluzioni e selezionare il progetto SampleEditor.  

4.  Nel menu **Progetto** fare clic su **Aggiungi riferimento**.  

     Viene visualizzata la finestra di dialogo **Aggiungi riferimento**.  

5.  Nella finestra di dialogo **Aggiungi riferimento** fare clic sulla scheda **Sfoglia**.  

6.  Nella scheda **Sfoglia** passare a *cartella_installazione*\Bin (dove *cartella_installazione* è la cartella in cui è stato installato MDT). Selezionare i file seguenti e fare clic su **OK**:  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  È possibile selezionare più file nella scheda **Sfoglia** tenendo premuto CTRL mentre si fa clic sui file.  

7.  In Esplora soluzioni accedere a SampleEditor/Riferimenti.  

8.  Verificare che nessun riferimento presenti avvisi o errori.  

9. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto SampleEditor e quindi fare clic su **Proprietà**.  

     Viene visualizzata la finestra di dialogo **Pagine delle proprietà SampleEditor**.  

10. Nella finestra di dialogo **Pagine delle proprietà SampleEditor** fare clic sulla scheda **Debug**.  

11. Nella scheda **Debug** fare clic su **Avvia programma esterno**.  

12. In **Avvia programma esterno** digitare ***cartella_installazione\Bin\UDIDesigner.exe*** (dove *cartella_installazione* è la cartella in cui è stato installato MDT), quindi fare clic su **OK**.  

    > [!TIP]
    >  È possibile fare clic sui punti di sospensione (...) per trovare la cartella e selezionare UDIDesigner.exe.  

13. Nel menu **File** fare clic su **Salva tutto**.  

14. Copiare il file *cartella_locale*\SDK\SamplePage\SamplePage.dll.config in *cartella_installazione*\Bin\Config (dove *cartella_locale* è la cartella creata nel computer di sviluppo in una sfase precedente del processo di configurazione e *cartella_installazione* è la cartella in cui è stato installato MDT).  

15. Nel menu **Debug** di Visual Studio 2010 fare clic su **Avvia debug**.  

     Viene visualizzato UDI Wizard Designer.  

16. Nella barra multifunzione di UDI Wizard Designer fare clic su **Apri**.  

     Viene visualizzata la finestra di dialogo **Apri**.  

17. Nella finestra di dialogo **Apri** aprire il file *cartella_locale*\SDK\SamplePage\SamplePage\Config.xml file (dove *cartella_locale* è la cartella creata nel computer di sviluppo in una fase precedente del processo di configurazione).  

     Il file Config.xml viene aperto e l'oggetto personalizzato [StageGroup](#StageGroup) viene visualizzato nel riquadro dei dettagli.  

18. Nel riquadro dei dettagli fare clic sulla scheda **Configura**.  

19. Esaminare le informazioni di configurazione per la casella **Posizione**, che includono quanto segue:  

    -   Pulsante **Sbloccato** che attiva o disattiva la casella **Posizione**  

    -   Casella **Valore predefinito** nella quale si immette il valore predefinito da visualizzare nella casella **Posizione**  

    -   **Friendly display name visible in summary page** (Nome visualizzato descrittivo visibile nella pagina di riepilogo), in cui si immette la didascalia per le informazioni visualizzate nella pagina **Riepilogo**  

    -   Casella di riepilogo **Posizione** che include un elenco di posizioni possibili  

20. Chiudere UDI Wizard Designer.  

21. Chiudere Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Esame degli esempi di SDK dell'UDI  
 Prima di iniziare lo sviluppo, vedere gli esempi disponibili nell'SDK dell'UDI. Usare le informazioni di questa guida e il codice sorgente degli esempi per creare le pagine personalizzate della procedura guidata e gli editor di pagine personalizzate della procedura guidata dell'UDI.  

 Esaminare gli esempi di SDK dell'UDI per visualizzare:  

-   Contenuto della cartella SDK copiato in precedenza nel processo di installazione, come descritto in [Esaminare il contenuto della cartella SDK](#ReviewContentsofSDKFolder)  

-   Esempio di pagina personalizzata della procedura guidata UDI, come descritto in [Esaminare la soluzione SamplePage di Visual Studio](#ReviewSamplePageVisualStudioSolution)  

-   Esempio di editor di pagine personalizzate della procedura guidata visualizzato in [Esaminare la soluzione SampleEditor di Visual Studio](#ReviewSampleEditorVisualStudioSolution)  

###  <a name="ReviewContentsofSDKFolder"></a> Esaminare il contenuto della cartella SDK  
 Durante la configurazione dell'ambiente di sviluppo dell'UDI, la cartella SDK è stata copiata dalla cartella di installazione di MDT a un'altra cartella creata. La tabella 1 elenca le cartelle sotto la cartella SDK e offre una breve descrizione.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tabella 1. Cartelle nel SDK dell'UDI  

|**Cartella**|**Contenuto della cartella**|  
|-|-|  
|Includes|File di intestazione di C++ necessari per la creazione di pagine personalizzate della procedura guidata per la procedura guidata UDI|  
|Libs|File di libreria di C++ che vengono collegati alla pagina personalizzata. Sono presenti versioni a 32 e 64 bit di librerie di collegamento statico. **Nota:** le versioni delle librerie per Itanium (IA-64) non sono disponibili.|  
|SampleEditor|Progetto di Visual Studio per la compilazione di un editor personalizzato destinato alla modifica della pagina SamplePage (scritta in C#) in UDI Wizard Designer|  
|SamplePage|Progetto di Visual Studio per la compilazione di una pagina personalizzata della procedura guidata UDI, creata in Visual C++|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> Esaminare la soluzione SamplePage di Visual Studio  
 Prima di iniziare a creare pagine personalizzate della procedura guidata ed editor di pagine personalizzate della procedura guidata, eseguire le attività seguenti per preparare l'ambiente di sviluppo dell'UDI:  

-   Esaminare le fasi del ciclo di vita di una pagina della procedura guidata UDI, come descritto in [Esaminare il ciclo di vita di una pagina della procedura guidata](#ReviewWizardPageLifeCycle).  

-   Esaminare la soluzione di Visual Studio per l'esempio SamplePage nel SDK dell'UDI, come descritto in [Esaminare l'esempio SamplePage](#ReviewSamplePageExample).  

####  <a name="ReviewWizardPageLifeCycle"></a> Esaminare il ciclo di vita della pagina della procedura guidata  
 Una pagina della procedura guidata UDI dispone di metodi che corrispondono a ogni fase del ciclo di vita della pagina. Per creare la pagina personalizzata della procedura guidata è necessario eseguire l'override di questi metodi con il codice. La Tabella 2 elenca i metodi da sottoporre a override e offre una breve descrizione di ogni metodo, che specifica quando usare il metodo nel ciclo di vita della pagina della procedura guidata.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tabella 2. Metodi nel ciclo di vita di una pagina della procedura guidata  

|**Metodo**|**Descrizione**|  
|-|-|  
|**OnWindowCreated**|Questo metodo viene chiamato una sola volta dopo la creazione della finestra della pagina.<br /><br /> Per questo metodo, scrivere codice che inizializza la pagina per la prima volta e viene eseguito una sola volta. Ad esempio usare questo metodo per inizializzare campi o per leggere informazioni di configurazione dagli elementi **Setter** del file di configurazione della procedura guidata UDI.|  
|**OnWindowShown**|Questo metodo viene chiamato ogni volta che la pagina viene visualizzata nella procedura guidata UDI. Viene chiamato quando la pagina viene visualizzata per la prima volta pagina e poi ogni volta che si passa alla pagina facendo clic su **Avanti** o su **Indietro** nella procedura guidata.<br /><br /> Per questo metodo scrivere codice che prepara la pagina alla visualizzazione, ad esempio codice che legge le variabili di memoria, le variabili della sequenza di attività o le variabili di ambiente e quindi aggiorna la pagina in base alle modifiche apportate a tali variabili.|  
|**OnCommonControlEvent**|Questo metodo può essere chiamato ogni volta che la pagina della procedura guidata viene visualizzata e riceve un messaggio WM_NOTIFY da un elemento figlio (in genere un controllo comune).<br /><br /> Per questo metodo scrivere codice che gestisce WM_NOTIFY in base al messaggio di notifica. Ad esempio può risultare necessario rispondere agli eventi di un controllo comune, come eventi clic o doppio clic per un controllo **TreeView**.|  
|**OnUnhandledEvent**|Questo metodo viene chiamato ogni volta che appare un messaggio della finestra non gestito nella pagina della procedura guidata. Questo metodo consente di intercettare e gestire questi messaggi della finestra che in caso contrario non verrebbero gestiti.<br /><br /> Per questo metodo scrivere codice che gestisce i messaggi della finestra relativi alla pagina della procedura guidata. In genere non è necessario eseguire l'override di questo metodo.|  
|**OnNextClicked**|Questo metodo viene chiamato quando si fa clic su **Avanti** nella procedura guidata.<br /><br /> Per questo metodo scrivere codice che esegue le azioni necessarie prima di passare alla pagina successiva della procedura guidata, ad esempio l'esecuzione di una convalida che può richiedere molto tempo. Se la convalida non riesce, è possibile annullare la richiesta **Avanti** e visualizzare un messaggio.|  
|**OnWindowHidden**|Questo metodo viene chiamato ogni volta che la pagina viene nascosta, quando viene visualizzata la pagina precedente o successiva della procedura guidata.<br /><br /> Per questo metodo scrivere codice che esegue le azioni desiderate prima che la pagina venga nascosta e venga visualizzata un'altra pagina. In genere non è necessario eseguire l'override di questo metodo.|  

####  <a name="ReviewSamplePageExample"></a> Esaminare l'esempio SamplePage  
 Esaminare l'esempio SamplePage usando l'elenco seguente, che rappresenta la sequenza di eventi del ciclo di vita della pagina della procedura guidata dell'esempio SamplePage:  

1.  La procedura guidata UDI, OSDSetupWizard.exe, legge le informazioni di configurazione dal file di configurazione della procedura guidata UDI dell'esempio (file Config.xml) come descritto in [Passaggio 1: La procedura guidata UDI (OSDSetupWizard.exe) legge il file Config.xml](#UDIWizardReadstheConfigFile).  

2.  La procedura guidata UDI carica le DLL necessarie per ogni pagina della procedura guidata elencata nel file di configurazione della procedura guidata UDI, come descritto in [Passaggio 2: La procedura guidata UDI carica la DLL per la pagina personalizzata della procedura guidata](#UDIWizardLoadstheDLLforCustomWizardPage).  

3.  La procedura guidata UDI visualizza la pagina personalizzata della procedura guidata e consente l'interazione di controllo desiderata come descritto in [Passaggio 3: La procedura guidata UDI visualizza la pagina personalizzata della procedura guidata](#UDIWizardDisplaysCustomWizardPage).  

4.  Quando la pagina personalizzata della procedura guidata ha raccolto le informazioni, eseguire le attività necessarie prima di fare clic su **Avanti** per passare alla pagina seguente della procedura guidata, come descritto in [Passaggio 4: Clic sul pulsante Avanti nella pagina personalizzata della procedura guidata](#TheNextButtonisClickedinCustomWizardPage).  

#####  <a name="UDIWizardReadstheConfigFile"></a> Passaggio 1: La procedura guidata UDI (OSDSetupWizard.exe) legge il file Config.xml  
 Quando viene avviata la procedura guidata UDI (OSDSetupWizard.exe), per impostazione predefinita viene letto il file di configurazione della procedura guidata UDI, ovvero il file UDIWizard_Config.xml (file di configurazione principale per la procedura guidata UDI).  

> [!NOTE]
>  L'esempio usa come file di configurazione il file Config.xml. In MDT il file di configurazione predefinito è UDIWizard_Config.xml, che si trova nella cartella Scripts nel pacchetto Files di MDT per la configurazione.  

 È possibile eseguire l'override del file di configurazione predefinito usato dalla procedura guidata UDI modificando il passaggio della sequenza di attività della procedura guidata UDI in modo che usi il parametro **/definition**. Per altre informazioni sull'override del file di configurazione predefinito usato dalla procedura guidata UDI, vedere "Override the Configuration File That the UDI Wizard Uses" (Eseguire l'override del file di configurazione predefinito usato dalla procedura guidata UDI).  

 Gli elementi di livello superiore nel file Config.xml sono:  

-   Elemento [DLLs](#DLLs)  

-   Elemento [Style](#Style)  

-   Elemento [Pages](#Pages)  

-   Elemento [StageGroups](#StageGroups)  

 Per altre informazioni sullo schema del file di configurazione della procedura guidata UDI e su ognuno di questi elementi, vedere [Riferimento per lo schema del file di configurazione della procedura guidata UDI](#UDIWizardConfigurationFileSchemaReference).  

 La procedura guidata UDI analizza l'elemento **DLLs** cercando i file con estensione dll da caricare. Nell'esempio vengono elencati due file con estensione dll: SamplePage.dll e SharedPages.dll. Questi file con estensione dll devono trovarsi nella stessa cartella di OSDSetupWizard.exe, ovvero la cartella Tools\\*piattaforma* (dove *piattaforma* è x86 per la versione a 32 bit x64 per la versione a 64 bit).  

 La procedura guidata UDI esamina l'elemento **Pages** cercando le pagine definite. Nell'esempio sono definite due pagine: **Custom** e **SummaryPage**. L'attributo **Type** dell'elemento **Page** viene definito nel file PageClassIDs.h e definisce in modo univoco il tipo della pagina personalizzata.  

 Nell'esempio il tipo definito è **Microsoft.SamplePage.LocationPage**. Per la pagina personalizzata sostituire il codice seguente, per evitare potenziali conflitti con altre pagine create in un secondo momento:  

-   Sostituire **Microsoft** con il nome dell'organizzazione.  

-   Sostituire **SamplePage** con il nome del progetto.  

-   Sostituire **LocationPage** con il nome della pagina personalizzata della procedura guidata.  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> Passaggio 2: La procedura guidata UDI carica la DLL per la pagina personalizzata della procedura guidata  
 Quando la procedura guidata UDI carica la DLL, chiama la funzione **RegisterFactories**, che deve essere implementata nel file con estensione dll. Nell'esempio questa funzione è implementata nel file dllmain.ccp. Ogni pagina della procedura guidata che viene creata deve implementare la funzione **RegisterFactories**.  

 La funzione **RegisterFactories** viene usata per registrare la classe factory della pagina della procedura guidata nel registro class factory per la procedura guidata UDI. Le *class factory* sono classi che possono creare un'istanza di un'altra classe. La funzione **RegisterFactories** crea una nuova istanza di una classe factory e passa la classe al registro class factory della procedura guidata UDI, che rende tale classe factory disponibile alla procedura guidata. La procedura guidata UDI cerca una classe factory registrata con un ID che corrisponde all'attributo **Type** dell'elemento **Page** per la pagina personalizzata della procedura guidata.  

 Nell'esempio l'ID è definito come **ID_Location** nel file PageClassIds.h come **Microsoft.SamplePage.LocationPage**, che corrisponde all'attributo **Type** dell'elemento **Page** nel file Config.xml. **ID_Location** viene passato come parametro nella funzione **RegisterFactories** implementata nel file dllmain.ccp.  

 È possibile creare una funzione usando il modello di funzione Register_*nome* per semplificare la creazione di una nuova istanza di factory e registrare l'istanza appena creata. Il valore **nome** incluso con il modello di funzione Register deve implementare l'interfaccia **iClassFactory**. La [classe ClassFactoryImpl](#ClassFactoryImplClass) gestisce la maggior parte dei dettagli dell'implementazione di una class factory.  

 È anche possibile usare la funzione **RegisterFactories** per registrare i tipi di attività e tipi di validator. Per altre informazioni, vedere  

-   [Creazione di attività UDI personalizzate](#CreatingCustomUDITasks)  

-   [Creazione di validator personalizzati dell'UDI](#CreatingCustomUDIValidators)  

> [!NOTE]
>  L'esempio contiene e registra solo una pagina personalizzata della procedura guidata. L'esempio non include attività personalizzate o validator personalizzati e pertanto non registra attività personalizzate o validator personalizzati.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> Passaggio 3: La procedura guidata UDI visualizza la pagina personalizzata della procedura guidata  
 La pagina personalizzata della procedura guidata nell'esempio è definita nel file LocationPage.cpp. Le pagine della procedura guidata derivano dalle classi modello, che specificano gran parte delle funzionalità presenti in una pagina. Tutte le pagine della procedura guidata dovrebbero derivare dalla [classe modello WizardPageImpl](#WizardPageImplTemplateClass), che implementa l'[interfaccia IWizardPage](#IWizardPageInterface). Ogni pagina della procedura guidata può implementare altre classi modello facoltative e le interfacce corrispondenti in base alle esigenze della pagina.  

 La [classe modello WizardPageImpl](#WizardPageImplTemplateClass) include varie interfacce utili che facilitano la creazione di pagine personalizzate della procedura guidata. Implementare la [classe modello WizardPageImpl](#WizardPageImplTemplateClass) come classe base per la pagina personalizzata della procedura guidata.  

 Per un elenco di:  

-   Classi modello per le pagine della procedura guidata, vedere [Wizard Page Helper Classes](#WizardPageHelperClasses) (Classi helper della pagina della procedura guidata)  

-   Interfacce per le classi modello della pagina della procedura guidata, vedere [Wizard Page Interfaces](#WizardPageInterfaces) (Interfacce della pagina della procedura guidata)  

 La pagina personalizzata della procedura guidata dell'esempio deriva dalla [classe modello WizardPageImpl](#WizardPageImplTemplateClass) e implementa l'[interfaccia IWizardPage](#IWizardPageInterface). La pagina personalizzata della procedura guidata implementa anche l'interfaccia **IFieldCallback**. Entrambi gli elementi sono implementati nel file LocationPage.cpp.  

 La pagina personalizzata della procedura guidata di esempio esegue l'override dei metodi seguenti:  

-   **OnWindowCreated**. Il metodo **OnWindowCreated** nella pagina della procedura guidata di esempio chiama i metodi seguenti:  

    -   [AddField](#AddField). Questo metodo associa il controllo della casella **IDC_COMBO_LOCATION** nella risorsa **IDD_LOCATION_PAGE** all'elemento [Data](#Data) con nome **Location** nel file Config.xml.  

         Oltre al metodo **AddField** è possibile usare i metodi [AddRadioGroup](#AddRadioGroup) e [AddToGroup](#AddToGroup) per supportare altri controlli e comportamenti.  

        > [!NOTE]
        >  Verificare di chiamare il metodo [AddField](#AddField), [AddRadioGroup](#AddRadioGroup) o [AddToGroup](#AddToGroup) prima di chiamare il metodo [InitFields](#InitFields).  

    -   [InitFields](#InitFields). Usare questo metodo per inizializzare i campi (controlli) aggiunti al modulo. Il puntatore della pagina è un parametro. Nell'esempio viene passato il puntatore **this** che fa riferimento alla pagina corrente.  

        > [!NOTE]
        >  Per supportare l'uso del puntatore **this** è necessario implementare l'interfaccia **IFieldCallback** oltre alle interfacce supportate dalla [classe modello WizardPageImpl](#WizardPageImplTemplateClass).  

         L'interfaccia **IFieldCallback** chiama il metodo **SetFieldDefault**, che viene usato per impostare i valori predefiniti per i controlli diversi dalle caselle di testo e dalle caselle di controllo. Nell'esempio il metodo **SetFieldDefault** imposta l'indice iniziale del controllo casella combinata sul valore predefinito specificato nell'elemento **Default** dell'elemento [Field](#Field) nel file Config.xml.  

     Il metodo **OnWindowCreated** configura il controller del modulo usando l'[interfaccia IFormController](#IFormController-Interface). Per altre informazioni sulla configurazione del controller di modulo, vedere [Impostazione del modulo](#SettingUptheForm).  

-   **InitLocations**. Questo metodo popola la casella combinata dall'elenco di percorsi nel file Config.xml. L'elemento [Data](#Data) e gli elementi figlio [DataItem](#DataItem) del file Config.xml specificano l'elenco dei valori possibili.  

-   **OnNextClicked**. Questo metodo esegue le attività seguenti:  

    -   Aggiorna la variabile della sequenza di attività **TSLocation** con il valore selezionato nella casella combinata usando il metodo **SaveFields**  

    -   Aggiunge informazioni che verranno visualizzate nella pagina **Riepilogo** usando il metodo **SaveFields**  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> Passaggio 4: Clic sul pulsante Avanti nella pagina personalizzata della procedura guidata  
 Dopo aver completato i campi nella pagina personalizzata della procedura guidata, l'utente fa clic su **Avanti**. Questa azione chiama il metodo **OnNextClicked**. Prima di passare alla pagina successiva della procedura guidata, il metodo **OnNextClicked** esegue le attività necessarie, ad esempi la registrazione delle modifiche alla configurazione apportate nella pagina personalizzata della procedura guidata.  

 Per la pagina personalizzata della procedura guidata di esempio, l'override associato al metodo **OnNextClicked** viene implementato nel file LocationPage.ccp. Nel metodo **OnNextClicked** della pagina personalizzata della procedura guidata di esempio vengono chiamati i seguenti metodi:  

1.  [InitSection](#InitSection). Questo metodo inizializza l'intestazione (didascalia dell'etichetta) per i dati di riepilogo della pagina **Riepilogo**. In genere è possibile impostare questo valore usando la funzione **DisplayName()**. I dati associati alla didascalia vengono salvati usando il metodo [SaveFields](#SaveFields).  

2.  [SaveFields](#SaveFields). Questo metodo consente di salvare i valori dei campi in variabili della sequenza di attività e nei dati visualizzati nella pagina **Riepilogo**.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> Esaminare la soluzione SampleEditor di Visual Studio  
 Prima di iniziare a creare pagine personalizzate della procedura guidata ed editor di pagine personalizzate della procedura guidata, seguire questa procedura per preparare l'ambiente di sviluppo dell'UDI:  

-   Esaminare l'architettura di UDI Wizard Designer, come descritto in [Esaminare l'architettura di UDI Wizard Designer](#ReviewUDIWizardDesignerArchitecture).  

-   Esaminare i componenti di una pagina della procedura guidata UDI che possono essere personalizzati usando il file di configurazione della procedura guidata UDI, come descritto in [Esaminare i componenti configurabili di una pagina della procedura guidata UDI](#ReviewConfigurableComponentsofUDIWizardPage).  

-   Esaminare l'esempio EditorPage disponibile nel SDK dell'UDI, come descritto in [Esaminare l'esempio EditorPage](#ReviewEditorPageExample).  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> Esaminare l'architettura di UDI Wizard Designer  
 UDI Wizard Designer è stato sviluppato con WPF, Prism e Unity. UDI Wizard Designer viene usato per modificare il file di configurazione della procedura guidata UDI (UDIWizard_Config.xml), che la procedura guidata UDI (OSDSetupWizard.exe) legge in fase di runtime. L'elemento [Pages](#Pages) nel file di configurazione della procedura guidata UDI contiene un elenco di pagine con un elemento [Page](#Page) per ogni pagina della procedura guidata.  

 Quando si modificano le impostazioni di configurazione per una pagina della procedura guidata, UDI Wizard Designer carica l'editor di pagine personalizzate corrispondente al tipo di pagina della procedura guidata. Gli editor di pagine personalizzate della procedura guidata vengono sviluppati come controlli utente WPF. Le pagine dell'editor di pagine personalizzate della procedura guidata usano lo schema progettuale [Model-View-ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) (MVVM) per WPF.  

 Lo schema progettuale MVVM consente di separare l'interfaccia utente (UI, presentazione) dai dati presentati. I dati sono la parte visibile dell'elemento [Page](#Page) nel file di configurazione della procedura guidata UDI (il file Config.xml nell'esempio), al quale si accede mediante la proprietà [CurrentPage](#CurrentPage) dell'interfaccia [IDataService](#IDataService).  

 UDI Wizard Designer usa **DependencyAttribute** per ottenere l'accesso alla classe **DataService** basata sul framework Dependency Injection in Unity. Per altre informazioni sul framework Dependency Interjection in Unity, vedere [Inject Some Life into Your Applications-Getting to Know the Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx) (Un nuovo approccio alle applicazioni: il blocco applicazione Unity).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> Esaminare i componenti configurabili di una pagina della procedura guidata UDI  
 Durante la creazione della pagina personalizzata della procedura guidata, alcune impostazioni di configurazione potrebbero essere definite nel codice e non essere modificabili dopo la compilazione della pagina. Nel caso di altre impostazioni di configurazione sarà necessario consentire la modifica di tali impostazioni mediante UDI Wizard Designer.  

 In genere le impostazioni di configurazione che si vuole configurare con UDI Wizard Designer vengono salvate nel file di configurazione della procedura guidata UDI (il file Config.xml nell'esempio). Se necessario, è anche possibile creare un file di configurazione personalizzato separato. Un esempio dell'uso di un file di configurazione separato è il file UDIWizard_Config.xml.app, usato dall'attività **Individuazione applicazioni** e dal tipo di pagina della procedura guidata **ApplicationPage**.  

 Di seguito è riportato un elenco delle impostazioni di configurazione comuni gestibili con UDI Wizard Designer:  

-   **Field**. I campi d'uso consentono agli utenti di specificare input. I campi appaiono come elementi [Field](#Field) nel file di configurazione della procedura guidata UDI (UDIWizard_Config.xml), che contiene le impostazioni di configurazione per ogni campo. L'editor di pagine della procedura guidata corrispondente deve specificare un metodo per la modifica delle impostazioni di configurazione per il campo mediante [FieldElementControl](#FieldElementControl).  

-   **Proprietà**. I setter consentono di creare proprietà per le entità nella pagina, ad esempio pagine nell'elemento [Page](#Page), campi nell'elemento [Field](#Field) o dati negli elementi [Data](#Data) o [DataItem](#DataItem). È possibile configurare le proprietà negli elementi [Setter](). Aggiungere un elemento [Setter]() separato per ogni proprietà che si vuole definire. Per modificare le proprietà si usa [SetterControl](#SetterControl) e si configurano altri elementi [Setter]() usando altri controlli.  

-   **Dati**. I dati vengono usati per archiviare le informazioni usate dalla pagina della procedura guidata e da altri componenti. È possibile definire dati per le pagine o i campi usando gli elementi [Data](#Data) o [DataItem](#DataItem). I dati possono essere definiti in una struttura semplice o gerarchica, usando in modo appropriato gli elementi [Data](#Data) o [DataItem](#DataItem). Il file Config.xml nell'esempio del SDK visualizza come compilare strutture di dati semplici.  

 L'editor di pagine personalizzate della procedura guidata che viene creato deve essere in grado di gestire queste impostazioni di configurazione.  

####  <a name="ReviewEditorPageExample"></a> Esaminare l'esempio EditorPage  
 L'esempio EditorPage viene usato per definire le impostazioni di configurazione per la pagina **SamplePage** della procedura guidata nel file di configurazione della procedura guidata UDI. L'esempio EditorPage include i componenti principali seguenti:  

-   Interfaccia utente per configurare le impostazioni della casella combinata **Location**  

-   Interfaccia utente per aggiungere o modificare una posizione nell'elenco delle posizioni possibili, riportate nella casella combinata **Location**  

-   Impostazioni di configurazione lette e salvate nel file di configurazione della procedura guidata UDI  

-   Codice di supporto per gli altri componenti  

 Esaminare l'esempio EditorPage in Visual Studio eseguendo la procedura seguente:  

1.  Esaminare le modalità di caricamento e inizializzazione dell'editor di pagine della procedura guidata **SampleEditor** in UDI Wizard Designer, descritte in [Esaminare il caricamento e l'inizializzazione dell'editor di pagine della procedura guidata](#ReviewWizardPageEditorLoadingInitialization).  

2.  Esaminare l'interfaccia utente usata per modificare la casella combinata **Location** nei file LocationPageEditor.xaml e LocationPageEditor.xaml.cs, come descritto in [Esaminare l'interfaccia utente usata per configurare la casella combinata Location](#ReviewUserInterfaceUsedtoConfigureLocationComboBox).  

3.  Esaminare l'interfaccia utente usata per aggiungere o modificare posizioni dell'elenco nei file AddEditLocationView.xaml e AddEditLocationView.xaml.cs, come descritto in [Esaminare l'interfaccia utente usata per modificare l'elenco di posizioni possibili](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations).  

4.  Esaminare il codice usato per gestire le informazioni di configurazione salvate nel file di configurazione della procedura guidata UDI, come descritto in [Esaminare il codice usato per gestire le informazioni di configurazione](#ReviewCodeUsedtoManageConfigurationInformation).  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> Esaminare il caricamento e l'inizializzazione dell'editor di pagine della procedura guidata  
 Gli editor di pagine personalizzate della procedura guidata vengono caricati se richiesti da UDI Wizard Designer. I file di configurazione della procedura guidata UDI vengono caricati all'avvio di UDI Wizard Designer. UDI Wizard Designer esegue la scansione della cartella *cartella_installazione*\Bin\Config (dove *cartella_installazione* è il nome della cartella in cui è installato MDT) per rilevare file con estensione config.  

 Durante la configurazione dell'ambiente di sviluppo UDI, il file SamplePage.dll.confg è stato copiato nella cartella *cartella_installazione*\Bin\Config. Quando si avvia UDI Wizard Designer, viene trovato e caricato il file SamplePage.dll.confg.  

 UDI Wizard Designer usa i seguenti attributi dell'elemento [Page](#Page) nel file SamplePage.dll.confg per caricare e inizializzare l'esempio EditorPage:  

-   **DesignerAssembly**. Questo attributo determina il nome della DLL da caricare. Questa DLL deve trovarsi nella stessa cartella del file UDIDesigner.exe, ovvero in *cartella_installazione*\Bin (dove *cartella_installazione* è il nome della cartella in cui è installato MDT).  

-   **DesignerType**. Questo attributo è il nome del tipo Microsoft .NET della classe che contiene il controllo utente WPF.  

-   **Tipo**. Usare questo attributo per configurare il tipo della pagina personalizzata della procedura guidata, che viene caricata dalla procedura guidata UDI. UDI Wizard Designer usa questo attributo per trovare l'elemento [Page](#Page) appropriato nel file di configurazione della procedura guidata UDI.  

-   **Dll**. Usare questo attributo per configurare l'elemento [DLL](#DLL) nel file di configurazione della procedura guidata UDI creato da UDI Wizard Designer.  

-   **Descrizione**. Usare questo attributo per specificare informazioni sull'editor di pagine della procedura guidata. Il valore di questo attributo viene visualizzato nella finestra di dialogo **Aggiungi nuova pagina** di UDI Wizard Designer, che consente di aggiungere la pagina della procedura guidata alla "Page Library".  

-   **DisplayName**. Usare questo attributo per specificare il nome della pagina personalizzata della procedura guidata che viene visualizzata in UDI Wizard Designer. Il valore di questo attributo viene visualizzato nella finestra di dialogo **Aggiungi nuova pagina** di UDI Wizard Designer, che consente di aggiungere la pagina della procedura guidata alla "Page Library".  

     Nell'esempio il tipo della pagina personalizzata della procedura guidata **SamplePage** è **Microsoft.SamplePage.LocationPage**, che viene salvato nel file Config.xml. Il file Config.xml si trova nel percorso *cartella_locale*\SDK\SamplePage\SamplePage (dove *cartella_locale* è la cartella creata nel computer di sviluppo in una fase precedente del processo di configurazione).  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> Esaminare l'interfaccia utente usata per configurare la casella combinata Location  
 Quando l'editor di pagine della procedura guidata è caricato e inizializzato, l'editor di pagine della procedura guidata SampleEditor viene caricato quando viene modificata una pagina di tipo **Microsoft.SamplePage.LocationPage**. L'interfaccia utente per l'editor di pagine è archiviata nel file LocationPageEditor.xaml.  

 Se si esamina l'interfaccia utente nella scheda **Design** e il codice nella scheda **XAML** è possibile visualizzare la relazione tra l'interfaccia utente grafica e gli elementi e attributi XAML (Extensible Application Markup Language).  

 Ad esempio, se si esamina l'elemento **Controls:FieldElementControl** in XAML è possibile vederne la relazione con il layout dell'interfaccia utente corrispondente. Usare l'elemento **Controls:FieldElementControl** per definire il controllo [FieldElementControl](#FieldElementControl).  

 I parametri **Binding** del file XAML associano i campi nell'editor di pagine di esempio con le informazioni nel file di configurazione della procedura guidata UDI. Ad esempio il codice seguente associa la casella di testo **Default value** all'elemento [Default](#Default) nel file di configurazione della procedura guidata UDI (il file Config.xml nell'esempio):  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Per altre informazioni, vedere [How to: Make Data Available for Binding in XAML](http://msdn.microsoft.com/library/ms748857.aspx) (Procedura: Rendere i dati disponibili per il binding in XAML).  

 Usare l'elemento**Views:CollectionTControl.ColumnCollectionView** nel codice XAML per modificare l'elenco delle posizioni disponibili nella visualizzazione griglia. Usare il controllo [CollectionTControl](#CollectionTControl) per rendere visibile la visualizzazione griglia e associarla all'elemento [Data](#Data) con nome **Location** nel file di configurazione UDI.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> Esaminare l'interfaccia utente usata per modificare l'elenco di posizioni possibili  
 L'interfaccia utente per la modifica dell'elenco di possibili posizioni è costituita da:  

-   Un menu sensibile al contesto e pulsanti della barra multifunzione che consentono di aggiungere, modificare, rimuovere o modificare l'ordine degli elementi nell'elenco di posizioni, come descritto in [Esaminare il menu sensibile al contesto e i pulsanti della barra multifunzione per la modifica dell'elenco di posizioni](#ReviewContextSensitiveMenuandRibbonButtons)  

-   Una finestra di dialogo che viene aperta quando si sceglie di aggiungere o modificare un elemento nell'elenco delle posizioni, come descritto in [Esaminare la finestra di dialogo per l'aggiunta o la modifica di posizioni](#ReviewDialogBoxforAddingEditingLocations)  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> Esaminare il menu sensibile al contesto e i pulsanti della barra multifunzione per la modifica dell'elenco di posizioni  
 Quando si fa clic con il pulsante destro del mouse sulla casella di riepilogo che contiene l'elenco di posizioni viene visualizzato un menu sensibile al contesto. La barra multifunzione include pulsanti corrispondenti, che consentono di eseguire le stesse attività. L'elemento di controllo **Views:CollectionsTControl** nel file LocationPageEditor.xaml definisce i metodi chiamati in base all'operazione eseguita e le proprietà impostate nel modo seguente:  

-   **SelectedItem**. Questa proprietà associata a dati viene attivata quando l'utente seleziona un elemento nell'elenco. Questa proprietà è associata alla proprietà **CurrentLocation** nel modello di visualizzazione che si trova nel file LocationPageEditorViewModel.cs e viene usata dal controllo [CollectionTControl](#CollectionTControl) per passare l'elemento selezionato quando si modifica o si rimuove un elemento esistente.  

-   **AddItemAction**. Questa azione viene eseguita quando l'utente fa clic sull'opzione **Aggiungi elemento** nel menu sensibile al contesto o sui pulsanti corrispondenti della barra multifunzione. È presente un'associazione dati a una proprietà nel modello di visualizzazione che restituisce l'oggetto **AddLocationAction**. Questo oggetto è il metodo **AddLocationCallback**, che si trova nel file LocationPageEditorViewModel.cs e visualizza la finestra di dialogo nel file AddEditLocationView.xaml.  

-   **EditItemAction**. Questa azione viene eseguita quando l'utente fa clic sull'opzione **Modifica elemento** nel menu sensibile al contesto. È presente un'associazione dati a una proprietà nel modello di visualizzazione che restituisce l'oggetto **EditLocationAction**. Questo oggetto è il metodo **EditLocationCallback**, che si trova nel file LocationPageEditorViewModel.cs e visualizza la finestra di dialogo nel file AddEditLocationView.xaml.  

-   **RemoveAction**. Questa azione viene eseguita quando l'utente fa clic sull'opzione **Rimuovi elemento** nel menu sensibile al contesto. È presente un'associazione dati a una proprietà nel modello di visualizzazione che restituisce l'oggetto **RemoveAction**. Questo oggetto è il metodo **EditLocationCallback**, che si trova nel file LocationPageEditorViewModel.cs e visualizza un messaggio che conferma l'eliminazione della posizione.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> Esaminare la finestra di dialogo per l'aggiunta o la modifica di posizioni  
 Se si aggiunge una nuova posizione all'elenco di posizioni o si modifica una posizione esistente, viene visualizzato un messaggio che si trova nel file AddEditLocationView.xaml. Il messaggio viene visualizzato mediante il metodo della finestra [ShowDialogWindow](#ShowDialogWindow) nel file LocationPageEditorViewModel.cs.  

 L'interfaccia utente nel file AddEditLocationView.xaml è costituita da:  

-   Una cornice di finestra di dialogo denominata **DialogFrame**, che include gli elementi seguenti:  

    -   Un titolo, configurabile mediante l'attributo **DialogTitle** della cornice della finestra di dialogo  

    -   Un pulsante **OK** che imposta lo stato di restituzione della proprietà **Approved** su **True**. Lo stato di restituzione viene verificato nel metodo **AddLocationCallback** nel file LocationPageEditorViewModel.cs per determinare se l'utente ha fatto clic su **OK**.  

    -   Un pulsante **Cancel** (Annulla) che imposta lo stato di restituzione della proprietà **Approved** su **False**. Lo stato di restituzione viene verificato nel metodo **AddLocationCallback** nel file LocationPageEditorViewModel.cs per determinare se l'utente ha fatto clic su **Cancel**.  

-   Un elemento WPF che contiene:  

    -   Un'etichetta, configurabile mediante l'attributo **Content**  

    -   Una casella di testo che è associata all'elemento [Data](#Data) con nome **Location** nel file di configurazione UDI (il file Config.xml nell'esempio)  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> Esaminare il codice usato per gestire le informazioni di configurazione  
 Le informazioni di configurazione per la pagina personalizzata della procedura guidata vengono archiviate nel file di configurazione della procedura guidata UDI, ovvero:  

-   File Config.xml nell'esempio reso disponibile con il SDK dell'UDI (il file contiene solo le impostazioni di configurazione per l'esempio).  

-   File UDIWizard_Config.xml reso disponibile con MDT, archiviato in *cartella_installazione*\Templates\Distribution\Scripts (dove *cartella_installazione* è la cartella in cui è stato installato MDT). Questo file contiene le impostazioni di configurazione per tutte le pagine e le fasi incorporate della procedura guidata  

 Nell'esempio SampleEditor, la routine **Locations** consente di gestire le informazioni di configurazione e si trova nel file LocationPageEditorViewModel.cs. La routine **Locations** restituisce un elenco di posizioni dal file di configurazione della procedura guidata UDI. In particolare l'elenco restituito contiene un elemento per ogni elemento [DataItem](#DataItem) nel file di configurazione della procedura guidata UDI.  

## <a name="creating-custom-udi-wizard-pages"></a>Creazione di pagine personalizzate della procedura guidata UDI  
 Il processo generale per la creazione di pagine personalizzate della procedura guidata UDI è il seguente:  

1.  Creare una copia della soluzione SamplePage come punto di partenza.  

2.  Posizionare i controlli (campi) desiderati nel modulo.  

3.  Scrivere codice per eseguire le attività appropriate quando viene caricata la pagina della procedura guidata (override per il metodo **OnWindowCreated**), inclusi i passaggi seguenti:  

    1.  Inizializzare il modulo.  

    2.  Leggere variabili della memoria, variabili della sequenza di attività, variabili di ambiente o informazioni di file con estensione xml (ad esempio le proprietà **Setter**).  

4.  Scrivere il codice necessario per eseguire le attività appropriate quando viene visualizzata la pagina (override per il metodo **OnWindowShown**), inclusi i passaggi seguenti:  

    1.  Abilitare o disabilitare i controlli in base alle informazioni lette al caricamento della pagina nel passaggio 3.  

    2.  Aggiornare i controlli in base alle informazioni lette al caricamento della pagina nel passaggio 3, ad esempio il popolamento dei controlli sulla base delle informazioni lette.  

5.  Scrivere codice per l'esecuzione delle attività appropriate quando l'utente interagisce con la pagina della procedura guidata.  

6.  Scrivere codice per eseguire le attività appropriate quando l'utente fa clic su **Avanti** nella procedura guidata UDI (override per il metodo **OnNextClicked**), inclusi i passaggi seguenti:  

    1.  Aggiornare variabili della memoria, variabili della sequenza di attività, variabili di ambiente o informazioni di file con estensione xml.  

    2.  Aggiornare le informazioni della pagina di riepilogo (se l'operazione non viene eseguita dai campi della pagina).  

7.  Compilare la soluzione.  

     Verificare che la versione della DLL creata abbia la stessa piattaforma del processore usata dall'installazione di MDT, ovvero la piattaforma del processore per Ambiente preinstallazione di Windows (Windows PE). La procedura guidata UDI può essere eseguita nei seguenti ambienti:  

    -   **Il sistema operativo esistente nel computer di destinazione**. Le versioni a 32 bit della pagina della procedura guidata possono essere eseguite nei sistemi operativi Windows a 32 bit o a 64 bit. Tuttavia le versioni a 64 bit della pagina della procedura guidata possono essere eseguite solo nei sistemi operativi Windows a 64 bit.  

    -   **Windows PE nel computer di destinazione**. Windows PE non supporta l'esecuzione di applicazioni a 32 bit in una versione di Windows PE a 64 bit. In tal caso, è necessario avere una versione della pagina procedura guidata compilata per ogni architettura del processore di Windows PE che si intende usare.  

8.  Copiare la DLL per la pagina personalizzata della procedura guidata in *cartella_installazione*\Templates\Distribution\Tools\piattaforma (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma* è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit).  

9. Completare i passaggi per la creazione dell'editor di pagine personalizzate.  

## <a name="creating-custom-wizard-page-editors"></a>Creazione di editor di pagine personalizzate della procedura guidata  
 Il processo generale per la creazione di editor di pagine personalizzate della procedura guidata è il seguente:  

1.  Creare una copia della soluzione SampleEditor come punto di partenza.  

2.  Creare l'interfaccia utente dell'editor della pagina principale in un file con estensione xaml.  

3.  Aggiungere istanze del controllo [FieldElementControl](#FieldElementControl) in base alle esigenze della pagina della procedura guidata da configurare (se richiesto).  

4.  Aggiungere istanze del controllo [SetterControl](#SetterControl) in base alle esigenze della pagina della procedura guidata da configurare (se richiesto).  

5.  Aggiungere istanze del controllo [CollectionTControl](#CollectionTControl) in base alle esigenze della pagina della procedura guidata da configurare (se richiesto).  

6.  Aggiungere l'interfaccia [IDataService](#IDataService).  

7.  Creare il codice appropriato per aggiornare il file di configurazione della procedura guidata UDI in base alle impostazioni da configurare mediante l'editor di pagine personalizzate della procedura guidata.  

8.  Creare finestre di dialogo figlio in un file con estensione xaml e chiamarle dall'editor della pagina primaria usando l'interfaccia [IMessageBoxService](#IMessageBoxService) in base alle esigenze della pagina della procedura guidata da configurare.  

9. Aggiungere le interfacce appropriate alla barra multifunzione di UDI Wizard Designer in base ai requisiti della pagina della procedura guidata da configurare.  

10. Compilare la soluzione.  

    > [!NOTE]
    >  Verificare che la versione della DLL creata supporti la stessa piattaforma di processore usata dall'installazione di MDT. Se ad esempio si installa la versione a 64 bit di MDT, compilare una versione a 64 bit dell'editor di pagine personalizzate.  

11. Creare un file di configurazione di UDI Wizard Designer per caricare le DLL necessarie ed eseguire il mapping dell'editor di pagine della procedura guidata con la pagina della procedura guidata corrispondente (il file SamplePage.dll.config nell'esempio).  

     Per altre informazioni relative agli elementi necessari per il mapping tra la pagina della procedura guidata e l'editor di pagine della procedura guidata, vedere l'elemento [DesignerMappings](#DesignerMappings), gli elementi figlio e gli attributi corrispondenti.  

12. Copiare il file di configurazione di UDI Wizard Designer creato nel passaggio precedente in *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stata installata la versione di MDT).  

13. Copiare la DLL dell'editor di pagine personalizzate della procedura guidata in *cartella_installazione*\Bin (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

##  <a name="CreatingCustomUDITasks"></a> Creazione di attività UDI personalizzate  
 Le *attività UDI* sono DLL scritte in C++ che implementano l'[interfaccia ITask](#ITaskinterface). È possibile registrare la DLL con la libreria di attività UDI Wizard Designer creando un file di configurazione di UDI Wizard Designer (con estensione config) e posizionandolo in *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

> [!NOTE]
>  È possibile creare una DLL che contiene pagine della procedura guidata, attività e validator nello stesso file con estensione dll. È anche possibile creare un singolo file di configurazione di UDI Wizard Designer (con estensione config) che contiene le impostazioni di configurazione per le pagine della procedura guidata, le attività e i validator della DLL.  

 **Per creare attività UDI personalizzate**  

1.  Scrivere codice che implementa l'[interfaccia ITask](#ITaskinterface) e i metodi seguenti:  

    -   [Init](#Init). Questo metodo viene chiamato per inizializzare l'attività.  

    -   [Execute](#Execute). Questo metodo viene chiamato per eseguire l'attività.  

2.  Scrivere codice che registra la class factory dell'attività personalizzata con il registro factory.  

3.  Compilare la soluzione per l'attività personalizzata.  

    > [!NOTE]
    >  Verificare che la versione della DLL creata supporti la stessa piattaforma di processore usata dall'installazione di MDT. Se ad esempio si installa la versione di MDT a 64 bit, compilare una versione a 64 bit dell'attività UDI personalizzata.  

4.  Creare un elemento [Task](#Task) sotto l'elemento [TaskLibrary](#TaskLibrary) nel file di configurazione di UDI Wizard Designer, come nell'esempio seguente:  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Tutti gli elementi [Task](#Task) devono includere il parametro **BitmapFilename**. Specificare tutti gli altri parametri necessari per l'attività. Ad esempio nel codice precedente il parametro **log** viene usato per specificare un parametro per il percorso di un file di log.  

5.  Copiare il file di configurazione di UDI Wizard Designer creato nel passaggio precedente in *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

6.  Copiare la DLL per l'attività personalizzata in *cartella_installazione*\Templates\Distribution\Tools\piattaforma (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma* è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit).  

##  <a name="CreatingCustomUDIValidators"></a> Creazione di validator personalizzati dell'UDI  
 I *validator UDI* sono DLL scritte in C++ che implementano l'interfaccia **IValidator**. È possibile registrare la DLL con la libreria validator di UDI Wizard Designer creando un file di configurazione di UDI Wizard Designer (con estensione config) e posizionandolo in *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

 **Per creare validator personalizzati dell'UDI**  

1.  Scrivere codice che crea una sottoclasse della classe **BaseValidator** e implementa i metodi seguenti:  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. Il controller del modulo chiama il membro **Init** per inizializzare il validator. Questo metodo deve chiamare il metodo **Init** per la classe **BaseValidator**. In genere legge le proprietà impostate per il validator dal file di configurazione della procedura guidata UDI. Ad esempio il validator **InvalidCharactersValidator** recupera il valore della proprietà **InvalidChars** usando questo metodo.  

    -   **IsValid**. Il controller del modulo chiama questo metodo per verificare se il controllo contiene testo valido. L'esempio seguente del metodo **IsValid** visualizza un validator che verifica che il campo non sia vuoto:  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR message)**. Il controller del modulo chiama questo membro per ogni sequenza di tasti e per altri eventi, in modo che il validator convalidi il contenuto del controllo e i messaggi aggiornati nella parte inferiore della pagina della procedura guidata (o li cancelli).  

     In genere questi sono gli unici metodi dei quali è necessario eseguire l'override. Tuttavia, a seconda del validator, potrebbe essere necessario eseguire l'override di altri metodi nella sottoclasse della classe **BaseValidator** creata. Per altre informazioni sugli altri metodi, vedere la classe **BaseValidator**.  

2.  Scrivere codice che registra la classe dell'attività personalizzata con la factory registro.  

3.  Compilare la soluzione per l'attività personalizzata.  

    > [!NOTE]
    >  Verificare che la versione della DLL creata supporti la stessa piattaforma di processore usata dall'installazione di MDT. Se ad esempio si installa la versione di MDT a 64 bit, compilare una versione a 64 bit dell'attività UDI personalizzata.  

4.  Creare un elemento [Validator](#Validator) sotto l'elemento **ValidatorLibrary** nel file di configurazione di UDI Wizard Designer, come nell'esempio seguente:  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Tutti gli elementi [Validator](#Validator) devono includere il parametro **Message**. Specificare tutti gli altri parametri richiesti dal validator. Ad esempio, nell'estratto precedente, il parametro **NamedPattern** viene usato per specificare un parametro per il nome di un criterio di espressione regolare predefinito.  

5.  Copiare il file di configurazione di UDI Wizard Designer creato nel passaggio precedente in *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

6.  Copiare la DLL per l'attività personalizzata in *cartella_installazione*\Templates\Distribution\Tools\piattaforma (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma* è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit).  

## <a name="udi-wizard-reference"></a>Riferimento per la procedura guidata UDI  

### <a name="wizard-page-components"></a>Componenti della pagina della procedura guidata  
 Per compilare le pagine personalizzate è possibile usare uno dei componenti precompilati.  

#### <a name="creating-component-instances"></a>Creazione di istanze del componente  
 La procedura guidata UDI usa le class factory per creare nuove istanze di oggetti per l'utente. Queste factory vengono registrate in un registro factory usando una stringa come chiave per la factory. Ad esempio il componente **WmiRepository** è identificato dalla stringa "Microsoft.Wizard.WmiRepository", che è disponibile nel file di intestazione IWmiRepository come **ID_WmiRepository**.  

 Supponendo che la pagina sia stata scritta come sottoclasse di **WizardPageImpl**, è possibile creare una nuova istanza di un **WmiRepository** come segue:  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 La funzione **CreateInstance** è una funzione di modello indipendente dai tipi per la creazione di nuove istanze dei componenti. **PWmiRepository** è un puntatore intelligente che gestisce il conteggio automatico dei riferimenti.  

#### <a name="creatable-components"></a>Componenti creabili  
 È presente un set di componenti registrabili nel registro. Il primo set di componenti viene sempre registrato, perché è reso disponibile dal file eseguibile principale della procedura guidata UDI. Gli altri due set di componenti vengono resi disponibili in DLL "facoltative". Perché questi componenti siano disponibili, la DLL deve essere elencata nella sezione **DLLs** del file XML con estensione config. Non è necessario che il codice determini quale eseguibile contiene un componente specifico.  

 L'elenco degli ID componente per i componenti (il nome del componente è uguale all'ID senza il prefisso *ID_*) registrati nel registro factory (definito in OSDSetupWizard) è visualizzato nella tabella 3.  

### <a name="table-3-component-ids"></a>Tabella 3. ID componente  

|**ID**|**Descrizione**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) Attività preliminare che garantisce che il computer non sia alimentato solo a batteria|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) Attività specializzata per trovare gli elementi software installati nel computer in uso|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) Può essere usato per eseguire un'attività in un altro thread|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) Attività per la copia di uno o più file|  
|**ID_FormController**|(**IFormController**) Probabilmente non sarà necessario creare un'istanza, dato che la pagina riceve un'istanza propria|  
|**ID_InvalidCharactersValidator**|(**IValidator**) Verifica che nessun campo di testo contenga caratteri inclusi in un elenco reso disponibile al validator|  
|**ID_Logger**|(**ILogger**) Probabilmente non sarà necessario creare un'istanza, dato che la pagina riceve un puntatore all'istanza condivisa|  
|**ID_NonEmptyValidator**|(**IValidator**) Validator che verifica che nessun campo sia vuoto|  
|**ID_PasswordValidator**|(**IValidator**) Validator che verifica che non siano presenti due campi di testo con lo stesso contenuto|  
|**ID_Regex**|(**IRegEx**) Valuta le espressioni regolari verificando la presenza di corrispondenze|  
|**ID_RegExValidator**|(**IValidator**) Validator che esegue la convalida rispetto a un'espressione regolare o uno schema noto|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) Metodo semplice per inviare proprietà alle attività senza usare XML|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) Eseguire un programma esterno|  
|**ID_SummaryBag**|(**ISummaryBag**) Disponibile indirettamente dalla pagina tramite il metodo Form|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) Gestisce l'esecuzione di un set di attività e dell'interfaccia utente|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) Consente di eseguire query di Strumentazione gestione Windows (WMI)|  
|**ID_IXmlDocument**|(**IXmlDocument**) Specifica un ambiente per la lettura e la scrittura di documenti XML|  

 Il file OSDRefreshWizard.dll, le pagine condivise e gli altri componenti di controllo definiti sono visualizzati nella Tabella 4 e nella Tabella 5.  

### <a name="table-4-directory-controls"></a>Tabella 4. Controlli di directory  

|**ID**|**Descrizione**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) Ambiente per ottenere informazioni sulle directory dal file system|  

### <a name="table-5-defined-sharedpagesdll"></a>Tabella 5. File SharedPages.dll definito  

|**ID**|**Descrizione**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Specifica un ambiente per un set limitato di funzionalità in Active Directory® Domain Services (AD DS)|  
|**ID_CpuInfo**|(**ICpuInfo**) Determina se la CPU è a 32 bit o a 64 bit|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) Include alcuni metodi per verificare se un set di credenziali è autorizzato per l'aggiunta a un dominio|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) Usa WMI per ottenere un elenco di unità nel computer in uso|  
|**ID_WiredNetworkTask**|(**ITask**) Attività che verifica se si è connessi alla rete con una scheda di rete con cavo (anziché wireless)|  

#### <a name="control-components"></a>Componenti di controllo  
 È possibile interagire con i controlli della pagina tramite la funzione del modello **GetControlWrapper**, che offre l'accesso a uno dei tipi di componenti elencati nella Tabella 6.  

### <a name="table-6-components"></a>Tabella 6. Componenti  

|**Tipi di controlli della finestra di dialogo**|**Descrizione**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) Ambiente per l'uso di controlli casella di controllo|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) Ambiente per i controlli casella combinata|  
|**CONTROL_GENERIC**|(**IControl**) Consente di lavorare con la maggior parte dei tipi di controllo per gestire gli stati attivo e visibile|  
|**CONTROL_LIST_VIEW**|(**IListView**) Ambiente per l'accesso alle funzionalità di un controllo visualizzazione elenco|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) Ambiente per la gestione della posizione di un controllo indicatore di stato|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) Ambiente per la gestione dei controlli pulsante di opzione|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) Ambiente che offre autorizzazioni di lettura/scrittura per il testo di un controllo, ad esempio una casella di testo o un'etichetta|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) Ambiente per la gestione di un controllo di visualizzazione albero|  

#### <a name="image-list-component"></a>Componente ImageList  
 Questo componente è un ambiente per un controllo **ImageList** nella pagina. È possibile creare un elenco immagini tramite l'interfaccia **IListView** o **ITreeView**.  

#### <a name="formcontroller-component"></a>Componente FormController  
 La procedura guidata crea automaticamente questo componente e lo passa alla pagina in uso. È possibile accedere al componente dalla pagina tramite il metodo **Form**, implementato dalla classe base **WizardPageImpl**.  

#### <a name="invalidcharactervalidator-component"></a>Componente InvalidCharacterValidator  
 Tipo di validator che è possibile includere in una pagina. L'ID è **ID_InvalidCharactersValidator** (definito in IValidator.h), che ha il valore di testo "Microsoft.Wizard.Validation.InvalidChars".  

 Questo validator cerca una proprietà singola (un elemento **Setter** nel file con estensione config) denominato **InvalidChars**, che è un elenco di caratteri non consentiti. L'elemento controlla i caratteri in una casella di testo. Se il testo contiene uno dei caratteri presenti nell'elenco, il componente segnala un errore.  

#### <a name="nonemptyvalidator-component"></a>Componente NonEmptyValidator  
 Tipo di validator che è possibile includere in una pagina. L'ID è **ID_NonEmptyValidator** (definito in IValidator.h), che ha il valore di testo "Microsoft.Wizard.Validation.NonEmpty".  

 Questo validator segnala un errore se la casella di testo (o qualsiasi altro controllo che supporta **IStaticText**) ha un valore stringa vuoto.  

#### <a name="passwordvalidator-component"></a>Componente PasswordValidator  
 Tipo di validator che è possibile includere in una pagina. L'ID è **ID_PasswordValidator** (definito in IValidator.h), che ha il valore di testo "Microsoft.Wizard.Validation.Password".  

 Questo validator funziona con due controlli di testo diversi (controlli che supportano **IStaticText**) e segnala un errore se i controlli non contengono gli stessi valori. In altre parole segnala un errore se il valore delle caselle di testo **Password** e **Conferma Password** non corrisponde.  

 Poiché include due controlli, questo validator richiede un'installazione più estesa rispetto ad altri validator. L'installazione può avere un aspetto simile al seguente:  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 In primo luogo si definisce il controllo **Conferma password** come controllo "figlio" del controllo **Password**. In questo modo, se il controller del modulo disabilita il controllo **Password** viene disabilitato anche il controllo **Conferma password**. Quindi si aggiunge un validator della password al modulo. Infine si offre al validator della password l'interfaccia per il controllo **Conferma password**.  

 Dato che sono richiesti due controlli, per impostare questo validator è necessario usare il codice anziché il file XML con estensione config.  

#### <a name="regexvalidator-component"></a>Componente RegExValidator  
 Tipo di validator che è possibile includere in una pagina. L'ID è **ID_RegExValidator** (definito in IValidator.h), che ha il valore di testo "Microsoft.Wizard.Validation.RegEx".  

 Questo validator confronta il contenuto di un controllo di testo (che supporta **IStaticText**) con un'espressione regolare e restituisce un errore se il testo non corrisponde all'espressione regolare.  

 In alternativa è possibile usare questo validator con un criterio denominato predefinito. Per l'uso di un'espressione regolare, il codice XML deve contenere una proprietà setter denominata **Pattern**. Se invece si vuole usare un criterio denominato, usare un setter **NamedPattern** impostato su uno dei valori nella tabella 7.  

### <a name="table-7-named-pattern-setters"></a>Tabella 7. Setter del criterio denominato  

|**Criterio**|**Descrizione**|  
|-|-|  
|Nome utente|Verifica che il testo abbia la forma dominio\utente o user@domain|  
|ComputerName|Il nome deve essere compreso tra 1 e 15 caratteri e non può includere un determinato set di caratteri (ad esempio : e ?)|  
|Gruppo di lavoro|Il nome deve essere compreso tra 1 e 15 caratteri e non può includere un determinato set di caratteri (ad esempio =, + e ?)|  

#### <a name="factoryregistry-component"></a>Componente FactoryRegistry  
 Questo componente tiene traccia di tutte le class factory e i servizi. Implementa l'interfaccia **IFactoryRegistry** ed è disponibile indirettamente tramite il metodo **Container** della pagina. Il registro carica anche DLL di estensione. Dopo il caricamento di una DLL il registro cerca la funzione esportata **RegisterFactories**. È necessario implementare questa funzione e registrare al suo interno class factory per le pagine, le attività e i validator (e le altre class factory che si vuole registrare). Il codice seguente è tratto dal progetto di esempio:  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Componente logger  
 Questo componente è disponibile per la pagina tramite il metodo **Logger** (implementato da **WizardPageImpl**). Questo metodo consente di scrivere voci nel file di log. Il contenuto del file di log è utile per la diagnosi degli eventuali problemi riscontrati dagli utenti nell'esecuzione della procedura guidata UDI.  

#### <a name="propertybag-component"></a>Componente PropertyBag  
 L'*elenco proprietà* è un contenitore per le variabili di memoria. È disponibile nella pagina mediante **Container()->Properties()**. Le variabili di memoria sono utili per il passaggio di dati temporanei tra pagine diverse.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>Componenti TSVariableBag e TSRepository  
 Il componente **TSVariableBag** consente di leggere e scrivere variabili della sequenza di attività. I valori restano in memoria finché l'utente non fa clic su **Fine** (per impostazione predefinita). È possibile accedere all'elenco**TSVariable** tramite il metodo **TSVariables** (implementato dalla classe di base **WizardPageImpl**). Questi componenti registrano tutte le letture e scritture di variabili della sequenza di attività.  

#### <a name="wmirepository-component"></a>Componente WmiRepository  
 Questo componente offre un ambiente per la gestione delle query WMI. È possibile chiamare la funzione di supporto **CreateInstance** con **ID_WmiRepository** per ottenere un'istanza di questo componente, che supporta l'interfaccia **IWmiRepository**. Questo componente restituisce record di risultato mediante l'interfaccia **IWmiIterator**.  

###  <a name="WizardPageHelperClasses"></a> Classi helper della pagina della procedura guidata  
 È possibile creare pagine personalizzate della procedura guidata UDI usando le classi helper predefinite specificate con il SDK dell'UDI. La tabella 8 elenca le classi helper che è possibile usare per creare pagine personalizzate della procedura guidata.  

### <a name="table-8-helper-classes"></a>Tabella 8. Classi helper  

|**Classe helper**|**Descrizione**|  
|-|-|  
|[Classe ClassFactoryImpl](#ClassFactoryImplClass)|Classe di base utile per la creazione di una class factory che può quindi essere registrata con il registro factory.|  
|[Classe modello Interface](#InterfaceTemplateClass)|Usare questa classe modello quando si vuole compilare un componente che implementa più interfacce.|  
|[Classe helper Path](#PathHelperClass)|Specifica operazioni comuni per file e directory.|  
|[Classe modello Pointer](#PointerTemplateClass)|Specifica il conteggio dei riferimenti per la gestione del ciclo di vita nei componenti COM. È importante rilasciare le interfacce dopo averne completato l'elaborazione. Questa classe modello gestisce automaticamente la durata.|  
|[Classe PUnknown](#PUnkownClass)|Questa classe è un puntatore intelligente specifico per l'interfaccia IUnknown. Per tutte le altre interfacce, usare la classe modello Pointer.|  
|[Classe helper StringUtil](#StringUtilHelperClass)|Questa classe offre metodi helper che rendono più facile lavorare con le stringhe.|  
|[Classe modello SubInterface](#SubInterfaceTemplateClass)|Questa classe di base semplifica l'implementazione di un componente che supporta un'interfaccia, la quale a sua volta eredita da un'altra interfaccia.|  
|[Classe modello UnknownImpl](#UnknownImplTemplateClass)|Questa classe gestisce la maggior parte dei dettagli della creazione di un componente COM.|  
|[Classe modello WizardComponent](#WizardComponentTemplateClass)|Questa classe di base viene usata per la creazione di componenti che richiedono l'accesso ai servizi della procedura guidata, quali la creazione e la registrazione di componenti.|  
|[Classe modello WizardPageImpl](#WizardPageImplTemplateClass)|Questa classe di base deve essere usata come classe di base per tutte le pagine personalizzate della procedura guidata.|  

####  <a name="ClassFactoryImplClass"></a> Classe ClassFactoryImpl  
 Classe di base utile per la creazione di una class factory che può quindi essere registrata con il registro factory.  

 L'esempio seguente per la definizione della classe **ClassFactoryImpl** è tratto dal file LocationPage.h nel progetto di esempio.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 L'esempio seguente è tratto dal file LocationPage.cpp nella pagina della procedura guidata di esempio usata per definire la class factory per la pagina.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Classe modello Interface  
 Usare questa classe modello per compilare un componente che implementa più interfacce, ad esempio:  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Questo codice crea una catena di classi di base che supporta sia **IFieldCalback** sia le interfacce supportate da **WizardPageImpl** (in questo caso **IWizardPage**).  

####  <a name="PathHelperClass"></a> Classe helper Path  
 Specifica operazioni comuni per file e directory:  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 Restituisce anche il percorso completo del file con estensione dll o exe con l'handle dell'istanza reso disponibile a questo metodo:  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 La classe restituisce il percorso completo e il nome dei file con estensione exe e dll con l'handle dell'istanza reso disponibile a questo metodo:  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . oppure offre solo il percorso e rimuove il nome del file:  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 Se è specificato un percorso con un nome file, la classe helper Path restituisce solo il nome del file:  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Infine la classe restituisce una nuova stringa con la combinazione di percorso combinato e nome file (oppure con un altro percorso).  

####  <a name="PointerTemplateClass"></a> Classe modello Pointer  
 Questa classe è definita in Pointer.h. Dato che i componenti COM usano il conteggio dei riferimenti per la gestione del ciclo di vita, è importante rilasciare le interfacce dopo averne completato l'elaborazione. Microsoft offre una classe modello che gestisce automaticamente la durata. Se ad esempio si vuole avere un puntatore intelligente per un'interfaccia XML, è possibile scrivere codice simile al seguente:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 La prima riga definisce il puntatore intelligente. La seconda riga illustra il recupero di un puntatore intelligente tramite un'altra chiamata. L'operatore **&** rilascia sempre un'interfaccia esistente se ne contiene una e restituisce l'indirizzo del puntatore interno. Dopo il recupero di un puntatore di questo tipo, l'istanza **Pointer** chiama automaticamente **Release** quando la variabile esce dall'ambito. Microsoft consiglia di usare puntatori intelligenti invece di chiamare manualmente **AddRef** e **Release**.  

 La classe del puntatore intelligente **Pointer** chiama anche **QueryInterface** per il recupero automatico di altre interfacce. Quando ad esempio il registro factory crea una nuova istanza di un componente, il codice è simile al seguente:  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 La prima riga chiama **QueryInterface** in background per richiedere l'interfaccia **IWizardComponent**. Il puntatore intelligente risultante sarà uguale a **nullptr** se il componente non supporta tale interfaccia.  

####  <a name="PUnkownClass"></a> Classe PUnknown  
 Questa classe è un puntatore intelligente specifico per l'interfaccia **IUnknown**. Per tutte le altre interfacce, usare la classe modello **Pointer**.  

####  <a name="StringUtilHelperClass"></a> Classe helper StringUtil  
 Questa classe è definita in Utilities.h e offre metodi helper che rendono più facile lavorare con le stringhe:  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Questo metodo confronta due stringhe ignorando la distinzione tra maiuscole e minuscole (vedere la tabella 9).  

### <a name="table-9-stringutil-helper-class"></a>Tabella 9. Classe helper StringUtil  

|**Valori restituiti**|**Descrizione**|  
|-|-|  
|**0**|Corrispondenza di stringhe, ignorando le maiuscole/minuscole|  
|**<0**|Prima < seconda|  
|**>0**|Prima > seconda|  

 Di seguito è riportato un esempio:  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Questi metodi sono simili ai metodi **Format** di Microsoft .NET perché i parametri hanno il formato **{0}**. Tuttavia non eseguono nessuna formattazione dell'input, solo la sostituzione:  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Si tratta di wrapper per **StringCchPrintf** che restituiscono un valore **wstring** evitando l'allocazione manuale di memoria per le stringhe o i buffer.  

####  <a name="SubInterfaceTemplateClass"></a> Classe modello SubInterface  
 Questa classe di base semplifica l'implementazione di un componente che supporta un'interfaccia, la quale a sua volta eredita da un'altra interfaccia. Ad esempio l'interfaccia **ICheckBox** eredita da **IControl**. Ecco come questa classe viene usata per definire **CheckBoxWrapper**:  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 L'interfaccia di base è il primo parametro, mentre l'interfaccia derivata è il secondo parametro.  

####  <a name="UnknownImplTemplateClass"></a> Classe modello UnknownImpl  
 Questa classe è definita in UnknownImpl.h e gestisce la maggior parte dei dettagli della creazione di un componente COM. Di seguito è riportato un esempio d'uso di questa classe di base:  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 Questo codice definisce una classe che supporta l'interfaccia **IDirectory**.  

####  <a name="WizardComponentTemplateClass"></a> Classe modello WizardComponent  
 Questa classe di base è definita in IWizardComponent.h ed è una classe base utile per la creazione di componenti che richiedono l'accesso ai servizi della procedura guidata, quali la creazione e la registrazione di componenti.  

 Ad esempio, ecco come viene definito il componente **CopyFilesTask**:  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 Il parametro per questa classe modello è l'interfaccia "principale" che si vuole usare per il componente, ad esempio **ITask** nel caso delle attività. L'uso di **WizardComponent** significa che il componente supporta sia l'interfaccia specificata (in questo caso **ITask**) sia **IWizardComponent**.  

 Quando si usa il registro class factory per creare un nuovo componente, il registro chiama il metodo **IWizardComponent->SetContainer** del componente per consentire al componente stesso di accedere ai servizi della procedura guidata.  

####  <a name="WizardPageImplTemplateClass"></a> Classe modello WizardPageImpl  
 Usare questa classe come classe base per le pagine personalizzate, ad esempio:  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 Il parametro è l'ID risorsa per il modello di finestra di dialogo.  

###  <a name="WizardPageInterfaces"></a> Interfacce di pagina della procedura guidata  
 La procedura guidata UDI Usa le interfacce per accedere ai diversi controlli della pagina. All'interno della pagina è possibile usare la funzione **GetControlWrapper** per recuperare un wrapper del controllo. Di seguito è riportato un esempio:  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 In questo caso **PStaticText** è un puntatore intelligente per l'interfaccia **IStaticText**. I puntatori intelligenti chiamano automaticamente il metodo COM **Release()** quando escono dall'ambito o quando si passa l'indirizzo di una variabile (ad esempio **&pFormat**) a un metodo.  

#### <a name="iadhelper-interface"></a>Interfaccia IADHelper  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Inizializzare il componente passandolo al logger per fare in modo che possa registrare informazioni.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 Questo metodo verifica se un set di credenziali è valido, come illustrato nella tabella 10.  

### <a name="table-10-hresultvalidlogon"></a>Tabella 10. HResultValidLogon  

|**HResult**|**Descrizione**|  
|-|-|  
|S_OK|Le credenziali sono valide|  
|S_FALSE|Le credenziali non sono valide|  
|E_FAIL|Non è stato possibile trovare il controller di dominio. Controllare i log per informazioni dettagliate.|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Questo metodo verifica se un set di credenziali ha accesso in lettura/scrittura all'oggetto computer in AD DS, come illustrato nella tabella 11.  

### <a name="table-11-hresult-hasaccess"></a>Tabella 11. HResult HasAccess  

|**HRESULT**|**Descrizione**|  
|-|-|  
|S_OK|L'utente dispone dell'accesso.|  
|E_FAIL|L'utente non dispone dell'accesso. Per altre informazioni, verificare il file di log.|  

#### <a name="ibackgroundtask-interface"></a>Interfaccia IBackgroundTask  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Panoramica  
 La pagina **Progress** usa questa classe per eseguire attività in un thread separato. È anche possibile usare questa classe ogni volta che si vuole eseguire delle operazioni su un thread separato. Le *attività* sono qualsiasi classe che supporta l'interfaccia **ITask**.  

 Questa interfaccia viene implementata dal componente **ID_BackgroundTask** ("Microsoft.Wizard.BackgroundTask"), definito nell'interfaccia IBackgroundTask.h.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Questa interfaccia inizializza il componente, come illustrato nella tabella 12.  

### <a name="table-12-hresult-init"></a>Tabella 12. HRESULT Init  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pTask**|Puntatore alla classe contenente il codice che si vuole eseguire in un altro thread|  
|**Id**|Numero che è possibile usare nel metodo **Finished** del callback per indicare quale attività ha terminato l'esecuzione. È utile quando si avviano diverse attività con lo stesso metodo di callback.|  
|**pCallback**|Classe che implementa il metodo **Finished**, chiamato ogni volta che termina l'esecuzione di un'attività. La chiamata del metodo **Finished** viene eseguita sul thread in background e non sul thread dell'interfaccia utente.|  

##### <a name="void-startvoid"></a>void Start(void)  
 Questo metodo avvia l'attività su un thread in background e restituisce gli elementi visualizzati nella tabella 13.  

### <a name="table-13-return-background-thread"></a>Tabella 13. Valori restituiti nel thread in background  

|**Valori restituiti**|**Descrizione**|  
|-|-|  
|**E_INVALIDARG**|L'attività è già in esecuzione, pertanto non può essere avviata ora.|  
|**E_FAIL**|Si è verificato un problema all'avvio del thread.|  
|**S_OK**|Il thread è stato avviato.|  

##### <a name="bool-running"></a>BOOL Running()  
 Questo metodo restituisce TRUE se l'attività in background è in esecuzione e FALSE se non è in esecuzione.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Questo metodo attende fino a quando l'esecuzione del thread termina o per il numero di millisecondi specificato.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Questo metodo termina il thread in esecuzione (vedere le tabelle 14 e 15). Il completamento del processo può richiedere un certo tempo dopo il completamento del metodo.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tabella 14. Codice di uscita HRESULT Terminate  

|**Parametro**|**Descrizione**|  
|-|-|  
|**exitCode**|Codice di uscita che viene inviato al metodo di callback Finished ed è disponibile anche nel metodo **GetExitCode**.|  

### <a name="table-15-termination-codes"></a>Tabella 15. Codici di terminazione  

|**Valori restituiti**|**Descrizione**|  
|-|-|  
|**E_FAIL**|Chiamata di terminazione non riuscita.|  
|**S_OK**|La richiesta di terminare il thread è stata completata.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Usare questo metodo per ottenere i risultati dell'esecuzione dell'attività nel thread in background (vedere la tabella 16).  

### <a name="table-16-result-codes"></a>Tabella 16. Codici di risultato  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pCode**|Puntatore a un elemento **DWORD** che viene impostato in fase di restituzione o **nullptr** se il valore restituito non è necessario. All'uscita il parametro viene impostato su **STILL_ACTIVE** se il thread è in esecuzione, sul codice restituito dal metodo **Execute** dell'attività o sul valore passato al metodo **Terminate** se è stato chiamato tale metodo.|  
|**pHresult**|Puntatore a un elemento **HRESULT** che viene impostato in fase di restituzione o **nullptr** se il valore **HRESULT** restituito non è necessario.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Questo metodo rilascia il thread in background. Restituisce **E_INVALIDARG** se il thread è in esecuzione e **S_OK** negli altri casi.  

#### <a name="icheckbox-interface"></a>Interfaccia ICheckBox  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 Imposta lo stato di selezione della casella di controllo. Quando il metodo è TRUE la casella di controllo è selezionata; quando il metodo è FALSE la casella di controllo è deselezionata.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Questo metodo segnala lo stato di selezione corrente di una casella di controllo.  

#### <a name="icombobox-interface"></a>Interfaccia IComboBox  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **CheckBoxWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_COMBO_BOX**.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Usare questo metodo quando è presente un'origine dati che implementa l'interfaccia **IBindableList**. La casella di riepilogo inizializza il contenuto con le didascalie presenti in questo elenco.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Selezionare l'elemento nella casella combinata in corrispondenza dell'indice.  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 Questo metodo restituisce l'indice dell'elemento selezionato oppure **-1** se non è selezionato nessun elemento.  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 Consente di aggiungere manualmente un elemento alla casella combinata.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Recupera la stringa della voce attualmente selezionata della casella combinata.  

##### <a name="void-clear"></a>void Clear()  
 Rimuove tutti gli elementi dalla casella combinata.  

#### <a name="icontrol-interface"></a>Interfaccia IControl  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **ControlWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_GENERIC**.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Abilita o disabilita il controllo.  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 Restituisce TRUE se il controllo è abilitato, FALSE in caso contrario.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Visualizza o nasconde il controllo.  

#### <a name="icpuinfo-interface"></a>Interfaccia ICpuInfo  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia si ottiene creando un nuovo componente **ID_CpuInfo**. Il metodo single segnala se la CPU è a 32 bit o a 64 bit. Si noti che se si ha un sistema operativo a 32 bit in un computer a 64 bit questo metodo restituisce TRUE, perché registra solo la capacità della CPU (non quella del sistema operativo).  

##### <a name="idirectory-interface"></a>Interfaccia IDirectory  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Panoramica  
 Il componente **Directory**, creato usando **ID_Directory**, offre un ambiente per lavorare con le directory del file system.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Questo metodo restituisce TRUE se esiste un file con il nome specificato.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Questo metodo trova la prima corrispondenza per il nome specificato. Supporta i caratteri jolly e restituisce sia nomi file che directory. Il metodo restituisce TRUE se viene trovata una corrispondenza, FALSE in caso contrario.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Questo metodo recupera il nome del file trovato con una chiamata a **FindFirst** o **FindNext**.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Questo metodo restituisce l'attributo del file trovato o della directory trovata più di recente. È possibile usare il codice come indicato di seguito per verificare se si tratta di una directory:  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Trova l'occorrenza successiva. Il metodo restituisce TRUE se viene trovata un'altra corrispondenza, FALSE in caso contrario.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Questo metodo rilascia le risorse usate per l'operazione di ricerca.  

#### <a name="idomainjoinvalidator-interface"></a>Interfaccia IDomainJoinValidator  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Panoramica  
 È possibile ottenere un'istanza di questa interfaccia mediante il valore **ID_DomainJoinValidator** della funzione di modello **CreateInstance**.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Inizializza l'istanza, come illustrato nella tabella 17.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tabella 17. HRESULT Init - Inizializzazione dell'istanza  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pLogger**|Istanza del logger, disponibile per la pagina tramite il metodo **Logger** della pagina stessa|  
|**pContainer**|Passa i risultati del metodo **Container** della pagina|  
|**pUsername**|Casella di testo che contiene il nome utente da convalidare|  
|**pPassword**|Casella di testo che contiene la password da convalidare|  
|**PComputerName**|Casella di testo contenente il nome del computer che verrà aggiunto al dominio|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Questo metodo usa il metodo **IADHelper->ValidLogon** per eseguire l'operazione. Vedere il metodo per informazioni dettagliate.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Verifica se l'utente dispone dei diritti per modificare la voce computer. La maggior parte delle operazioni viene eseguita da **IADHelper->HasAccess**. Se questo metodo restituisce FALSE, controllare il file di log per informazioni dettagliate.  

#### <a name="idrivelist-interface"></a>Interfaccia IDriveList  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Chiamare questo metodo prima di chiamare qualsiasi altro componente. È necessario creare un nuovo **WmiRepository** prima di chiamare questo metodo.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Questo metodo consente di aggiungere il testo che viene visualizzato come una clausola "where" nella query. Ad esempio la riga seguente restituisce solo le unità USB:  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 Imposta le dimensioni minime dell'unità disco, in byte, per le unità che verranno restituite dalla query.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Esegue la query. L'elenco di unità disponibile dopo la chiamata di questo metodo viene ordinato per lettera di unità.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Questo metodo aggiunge i nomi delle proprietà aggiuntive che si vuole rendere disponibili nei risultati della query. Chiamare questo metodo prima di chiamare **Update**. La tabella 18 visualizza tre proprietà utili.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tabella 18. HRESULT AddProperty: proprietà utili  

|**Sezione**|**Proprietà**|**Descrizione**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|Dimensioni in byte rappresentate come stringa|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|Numero del disco come valore intero a partire da 0|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|Etichetta del volume|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Numero di record restituiti dalla query. Chiamare **Update** prima di chiamare questo metodo.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value)  
 Questo metodo recupera il valore di una proprietà dai risultati della query, come illustrato nella tabella 19.  

### <a name="table-19-hresult-getproperty"></a>Tabella 19. HRESULT GetProperty  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Index**|Indice in base zero per il record del risultato|  
|**propName**|Nome della proprietà, ad esempio "Size"|  
|**Valore**|In fase di restituzione, questo parametro contiene un valore Variant della proprietà|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index,  LPBSTR pCaption)  
 Questo metodo recupera la didascalia per un record che corrisponde alla proprietà **Caption**.  

#### <a name="iimagelist-interface"></a>Interfaccia IImageList  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **ImageList**. È possibile recuperare un'istanza di questo componente dall'interfaccia **IListView**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crea un nuovo elenco di immagini, gestito da questo componente. Chiamare questo metodo solo una volta.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Questo metodo restituisce l'handle dell'elenco di immagini, utile quando è necessario eseguire altre operazioni sull'elenco di immagini.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 Aggiunge una nuova immagine all'elenco di immagini da una risorsa, come illustrato nella tabella 20.  

### <a name="table-20-hresult-iimagelist-interface"></a>Tabella 20. Interfaccia HRESULT IImageList  

|**Parametro**|**Descrizione**|  
|-|-|  
|**hInstance**|Handle dell'istanza del modulo che contiene la risorsa bitmap|  
|**resourceId**|ID della risorsa da caricare nell'elenco di immagini|  

#### <a name="ilistview-interface"></a>Interfaccia IListView  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **ControlWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_LIST_VIEW**.  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 Aggiunge una nuova riga alla casella di riepilogo. Il metodo restituisce l'indice dell'elemento appena aggiunto.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 Aggiunge una nuova colonna alla visualizzazione elenco.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Imposta il testo in una colonna diversa dalla prima colonna della casella di riepilogo, come illustrato nella tabella 21.  

### <a name="table-21-hresult-setsubitem"></a>Tabella 21. HRESULT SetSubItem  

|**Parametro**|**Descrizione**|  
|-|-|  
|**index**|Indice dell'elemento elenco da modificare|  
|**column**|Indice della colonna che si vuole aggiornare; la prima colonna viene impostata con **AddItem**, mentre la seconda e le colonne successive vengono impostate con questo metodo|  
|**text**|Stringa da visualizzare nella colonna|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 Questo metodo restituisce la larghezza dell'intera casella di testo.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Questo metodo consente di impostare stili estesi nella casella di riepilogo, ad esempio:  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 Questo metodo restituisce l'indice dell'elemento della visualizzazione elenco attualmente selezionato.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Impostare l'elemento selezionato nell'elenco su questo indice.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Questo metodo restituisce TRUE se un elemento dell'elenco è selezionato. Questo metodo richiede la chiamata di **SetExtendedStyle** per impostare lo stile della casella di controllo.  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 Questo metodo restituisce il numero di elementi dell'elenco di visualizzazione.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crea un nuovo elenco di immagini e lo associa alla visualizzazione elenco.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Aggiunge un'immagine all'elenco di immagini della visualizzazione elenco. In primo luogo è necessario chiamare **CreateImageList**.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Imposta l'immagine che verrà visualizzata a sinistra per un elemento specifico della visualizzazione elenco.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Rimuove tutti gli elementi dalla visualizzazione elenco.  

#### <a name="iprogressbar-interface"></a>Interfaccia IProgressBar  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **ProgressBarWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_PROGRESS_BAR**.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 Imposta la posizione dell'indicatore di stato su un numero compreso tra 0 e 100. Per impostazione predefinita i nuovi indicatori di stato Win32® hanno un intervallo massimo pari a 100.  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 Questo metodo restituisce la posizione corrente dell'indicatore di stato.  

#### <a name="iradiobutton-interface"></a>Interfaccia IRadioButton  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **RadioButtonWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_RADIO_BUTTON**.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 Specifica il wrapper con l'intervallo di pulsanti di opzione che vanno considerati come un gruppo. Chiamare questo metodo prima di **CheckRadio**.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Imposta il pulsante di opzione specifico come pulsante singolo nel gruppo di pulsanti di opzione selezionato. Chiamare **SetGroup** prima di chiamare questo metodo.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Questo metodo restituisce TRUE se il pulsante di opzione è selezionato, FALSE in caso contrario.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 Questo metodo abilita o disabilita un pulsante di opzione.  

#### <a name="istatictext-interface"></a>Interfaccia IStaticText  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **StaticTextWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_STATIC_TEXT**.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Imposta il testo per il controllo.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Questo metodo restituisce il valore corrente del testo per il controllo.  

####  <a name="ITaskinterface"></a> Interfaccia ITask  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Implementare questa interfaccia se si vuole che il componente sia disponibile come attività nella pagina preliminare o se si vuole usare il componente **BackgroundTask** per eseguire operazioni su un thread in background.  

 I componenti che implementano l'interfaccia **ITask** sono i seguenti:  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Init  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Se si sta scrivendo un'attività per la pagina preliminare, chiamare questo metodo per inizializzare l'attività. Il file con estensione config contiene codice XML che può essere simile al seguente:  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 Il parametro **pProperties** offre l'accesso ai tre valori setter, mentre il parametro **pTaskSettings** consente l'accesso all'elemento **Task** e agli elementi figli. Per la maggior parte delle attività è sufficiente leggere i dati dal parametro **pProperties**.  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 In questo metodo si scrive il codice che esegue l'attività. Il metodo deve restituire **S_OK** se non è presente nessun errore e può restituire un altro **HRESULT** se durante l'esecuzione dell'attività si è verificato un errore. I valori diversi da **S_OK** restituiti da questo metodo vengono confrontati con gli elementi <Error\> nella sezione <ExitCodes\> se si sta usando la pagina preliminare.  

 Il parametro **pReturnCode** deve essere aggiornato con un numero che specifica lo stato dell'attività. Questi valori vengono confrontati con elementi <ExitCode\> dalla pagina preliminare.  

#### <a name="itreeview-interface"></a>Interfaccia ITreeView  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata dal componente **TreeViewWrapper**. È possibile recuperare un'istanza di questo componente usando la funzione helper **GetControlWrapper** con il tipo **CONTROL_TREE_VIEW**.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Questo metodo attiva le caselle di controllo nel controllo di visualizzazione albero impostando lo stile **TVS_CHECKBOXES**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Aggiunge un nuovo elenco di immagini per il controllo di visualizzazione albero. Il parametro **flags** viene passato nella chiamata alla funzione Win32 **ImageList_Create**.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Aggiunge un'immagine all'elenco di immagini da una risorsa (**resourceId**) nel modulo con l'handle di istanza **hInstance**.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Aggiunge un nodo alla visualizzazione struttura ad albero. Il nuovo nodo viene aggiunto al livello superiore se **hParent** è NULL. In caso contrario specificare l'handle dell'elemento padre al quale si vuole aggiungere il nuovo elemento. Questo metodo restituisce l'handle per il nuovo elemento.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 Impostare l'immagine da usare per un elemento della visualizzazione struttura ad albero. È possibile impostare sia l'immagine normale sia l'immagine espansa.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Rimuove tutti gli elementi dalla visualizzazione struttura ad albero.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Verifica che l'elemento della visualizzazione struttura ad albero sia visibile. Se necessario, la visualizzazione struttura ad albero scorre per rendere visibile l'elemento.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Imposta l'elemento attualmente selezionato sull'elemento specificato. È possibile chiamare **SetFirstVisible** dopo questo metodo per garantire che l'elemento appena selezionato sia visibile.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 Il metodo imposta l'immagine che verrà visualizzata per la casella di controllo nella visualizzazione struttura ad albero. Queste immagini si trovano in un controllo **ImageList** specifico gestito dalla visualizzazione struttura ad albero. Per impostazione predefinita, questo elenco di immagini contiene tre immagini, illustrate nella tabella 22.  

### <a name="table-22void-checkitem-image-list-default"></a>Tabella 22. Elenco di immagini predefinite void CheckItem  

|**checkState**|**Descrizione**|  
|-|-|  
|**0**|Vuoto|  
|**1**|Deselezionato|  
|**2**|Selezionato|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Questo metodo restituisce l'handle dell'elemento della visualizzazione struttura ad albero attualmente selezionato.  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 Questo metodo imposta l'altezza in pixel di tutti gli elementi nel controllo di visualizzazione struttura ad albero. Restituisce l'altezza precedente in pixel.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Questo metodo abilita o disabilita un singolo elemento nell'albero. Se si disabilita un elemento con elementi figlio, gli elementi figlio non vengono disabilitati.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 Questo metodo espande o comprime un nodo dell'albero.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Questo metodo restituisce il primo elemento figlio di un elemento della visualizzazione struttura ad albero o NULL se non sono presenti elementi figlio.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Questo metodo restituisce l'handle dell'elemento padre per un nodo nella visualizzazione struttura ad albero o NULL se il nodo è in corrispondenza del livello superiore.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 È possibile chiamare questo metodo con un handle restituito da **GetChild** per eseguire l'iterazione su tutti gli elementi figlio di un nodo. Questo metodo restituisce il successivo elemento di pari livello nell'albero che condivide lo stesso elemento padre.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Questo metodo restituisce **0** se il nodo della visualizzazione struttura ad albero non è selezionato e **1** se è selezionato.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Questo metodo restituisce TRUE se il nodo della visualizzazione struttura ad albero è abilitato, FALSE in caso contrario.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 Questo metodo è solo per uso interno.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Chiamare questo metodo se si vuole ricevere una notifica quando l'elemento selezionato viene modificato o quando l'utente modifica lo stato di selezione di un elemento della visualizzazione struttura ad albero. Per ricevere i callback corrispondenti è necessario implementare **ITreeViewEvent** nel componente.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Imposta il colore del tema usato per l'elemento selezionato.  

#### <a name="iwmiiteration-interface"></a>Interfaccia IWmiIteration  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia viene in genere usata insieme a **IWmiRepository** quando si lavora con le chiamate WMI. L'interfaccia **IWmiIteration** consente di scorrere i valori restituiti da una query.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Consente di passare all'elemento successivo nei risultati della query, come illustrato nella tabella 23.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tabella 23. Risultati restituiti dalla query HRESULT Next(void)  

|**HRRESULT**|**Descrizione**|  
|-|-|  
|**S_OK**|Passa al risultato successivo; è possibile usare **GetProperty** per recuperare le proprietà di tale risultato.|  
|**S_FALSE**|Non sono presenti altri elementi nell'elenco.|  
|**E_NOT_SET**|Nessun risultato della query.|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Questo metodo recupera il valore di una proprietà dal record dei risultati corrente, come illustrato nelle tabelle 24 e 25.  

### <a name="table-24-hresult-getproperty"></a>Tabella 24. HRESULT GetProperty  

|**Parametro**|**Descrizione**|  
|-|-|  
|**propertyName**|Nome della proprietà da recuperare|  
|**pValue**|Punta a una struttura VARIANT che in fase di restituzione contiene il valore della proprietà|  

### <a name="table-25-hresult-getproperty-result"></a>Tabella 25. Risultato di HRESULT GetProperty  

|**HRESULT**|**Descrizione**|  
|-|-|  
|**S_OK**|Il valore della proprietà è stato recuperato.|  
|**WBEM_E_NOT_FOUND**|Non è presente nessuna proprietà con questo nome.|  
|**E_NOT_VALID_STATE**|Non è presente nessun record corrente.|  

> [!NOTE]
>  Il metodo **GetProperty** può restituire codici di errore WMI diversi da quelli elencati nella tabella 25. I valori elencati sono i risultati comuni che vengono restituiti.  

#### <a name="iwmirepository-interface"></a>Interfaccia IWmiRepository  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia viene implementata per il componente **WmiRepository** (**ID_WmiRepository**).  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Questo metodo imposta lo spazio dei nomi WMI che viene usato per la query. Chiamare questo metodo prima di **ExecQuery**. Se non si chiama questo metodo, lo spazio dei nomi sarà root\cimv2. Questo metodo restituisce sempre **S_OK**.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 Esegue una query sul set dello spazio dei nomi WMI con una chiamata a **SetNamespace**, come illustrato nelle tabelle 26 e 27.  

### <a name="table-26-hresult-execquery"></a>Tabella 26. HRESULT ExecQuery  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Query**|Stringa della query WMI da eseguire|  
|**ppIterator**|Passa un puntatore a un puntatore di interfaccia che in fase di restituzione viene compilato con un'interfaccia, fornendo l'accesso ai risultati della query|  

### <a name="table-27-hresult-query-result"></a>Tabella 27. Risultati query HRESULT  

|**HRESULT**|**Descrizione**|  
|-|-|  
|**S_OK**|Query completata|  
|**Other**|Se la query ha esito negativo, restituisce un **HRESULT** WMI|  

#### <a name="iformcontroller-interface"></a>Interfaccia IFormController  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Panoramica  
 Ogni pagina della procedura guidata UDI ha un proprio controller del modulo che implementa questa interfaccia. Questo controller consente di connettere i dati dei campi nel file XML con estensione config ai controlli della pagina. Il controller del modulo gestisce automaticamente vari dettagli.  

#####  <a name="SettingUptheForm"></a> Impostazione del modulo  
 In generale si imposta il controller del modulo nel metodo **OnWindowCreated** della pagina. Questo approccio richiede la chiamata dei metodi illustrati nella tabella 28.  

### <a name="table-28-onwindowcreated-method"></a>Tabella 28. Metodo OnWindowCreated  

|**Metodo**|**Descrizione**|  
|-|-|  
|**Init**|Inizializza il controller del modulo|  
|**AddField**|Specifica una connessione tra un campo nel file XML con estensione config (un nome di stringa) e un controllo nella finestra di dialogo della pagina che corrisponde a un ID|  
|**AddRadioGroup**|Consente di connettere un pulsante di opzione a un gruppo e a un controllo nella finestra di dialogo|  
|**AddToGroup**|Consente controlli "figlio" che vengono abilitati o disabilitati insieme al controllo padre o in base al pulsante di opzione selezionato|  
|**InitFields**|Chiamare questo elemento dopo aver chiamato tutti i metodi **Add** per impostare il modulo|  
|**Validate**|Esegue la convalida iniziale|  

##### <a name="processing-form-events"></a>Elaborazione degli eventi del modulo  
 Aggiungere la chiamata seguente al metodo **OnControlEvent**:  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Questa chiamata passa gli eventi al controller del modulo che può così elaborare gli eventi associati al modulo.  

##### <a name="save-form-data"></a>Salvare i dati del modulo  
 Nel metodo **OnNextClicked** chiamare i metodi del modulo illustrati nella tabella 29.  

### <a name="table-29-onnextclicked-method"></a>Tabella 29. Metodo OnNextClicked  

|**Metodo**|**Descrizione**|  
|-|-|  
|**InitSection**|Specifica il nome della sezione che verrà visualizzata nella pagina **Riepilogo** per questa pagina|  
|**SaveFields**|Consente di salvare i valori di campo in variabili della sequenza di attività e nella pagina **Riepilogo**|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 In genere questo metodo viene chiamato in prossimità dell'inizio del metodo **OnWindowCreated** della pagina. Il comando dovrebbe essere simile al seguente:  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Questo metodo viene chiamato internamente e non è necessario chiamarlo manualmente. Specifica il codice XML della pagina al controller del modulo.  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 Questo metodo esegue tutti i validator associati a controlli. Se un validator non viene passato, il controller di modulo visualizza un messaggio di avviso e disabilita il pulsante **Avanti**, quindi arresta l'elaborazione dei validator. In genere è sufficiente chiamare questo metodo al termine del metodo **OnWindowCreated**. Il valore restituito è sempre**S_OK**.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Questo metodo aggiunge un controllo come "figlio" di una casella di controllo o di un pulsante di opzione, come illustrato nella tabella 30. Tutti i controlli figlio di questo tipo vengono disabilitati quando il controllo padre non è selezionato. Il metodo restituisce sempre **S_OK**.  

### <a name="table-30-addtogroup"></a>Tabella 30. AddToGroup  

|**Parametro**|**Descrizione**|  
|-|-|  
|**groupControlId**|ID della casella di controllo o del pulsante di opzione che controlla lo stato di abilitazione del controllo figlio|  
|**Controlld**|ID del controllo che si vuole aggiungere come figlio|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Questo metodo aggiorna lo stato abilitato o disabilitato dei controlli figlio di un gruppo in base allo stato del controllo padre. In genere non è necessario chiamare direttamente questo metodo, perché il controller del modulo lo chiama automaticamente.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Chiamare questo metodo solo se si vuole creare un validator nel codice anziché con il linguaggio XML. Questo metodo restituisce sempre **S_OK**.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Chiamare questo metodo solo se si vuole creare un validator nel codice anziché con il linguaggio XML.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Chiamare questo metodo per disabilitare esplicitamente il validator per un controllo o per ripristinare la convalida normale, come illustrato nella tabella 31. Questo metodo è utile ad esempio quando sono presenti regole di abilitazione/disabilitazione per controlli non inclusi nella convalida del modulo ed è necessario disabilitare la convalida per un controllo. In altre parole, in genere non è necessario chiamare direttamente questo metodo. Questo metodo restituisce sempre **S_OK**.  

### <a name="table-31-hresult-disablevalidation"></a>Tabella 31. HRESULT DisableValidation  

|**Parametro**|**Descrizione**|  
|-|-|  
|**controlId**|Controllo per il quale si vuole abilitare o disabilitare la convalida|  
|**Disabilitato**|Impostare su TRUE per disabilitare la convalida e su FALSE per ripristinare la convalida normale|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Consente di aggiungere un mapping di controllo tra il nome di un elemento **Field** del file XML con estensione config e l'ID controllo nella finestra di dialogo della pagina, come illustrato nella tabella 32. È necessario chiamare questo metodo prima della chiamata di **InitFields**, perché **InitFields** usa queste informazioni. Questo metodo restituisce sempre **S_OK**.  

### <a name="table-32-hresult-addfield"></a>Tabella 32. HRESULT AddField  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Fieldname**|Nome del campo come appare nel codice XML della pagina|  
|**controlId**|ID del controllo nel modello di finestra di dialogo della pagina|  
|**suppressLog**|Impostare questo parametro su TRUE se non si vuole che i valori del campo vengano scritti nel file di log. Impostare sempre questo parametro su TRUE per i campi di password o PIN|  
|**Tipo**|Tipo di controllo, uno dei seguenti:<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Questo metodo aggiunge un controllo a un gruppo di pulsanti di opzione con nome, come illustrato nella tabella 33. È necessario chiamare questo metodo prima del metodo **InitFields**, perché tale metodo usa gli attributi dell'elemento **RadioGroup** per controllare le impostazioni per tutti i controlli pulsante di opzione del gruppo. Ad esempio è possibile che i gruppi di pulsanti di opzione siano bloccati e di conseguenza che tutti i pulsanti di opzione siano disabilitati, ma i controlli figlio sono abilitati o disabilitati solo in base al pulsante di opzione che è selezionato. Questo metodo restituisce sempre **S_OK**.  

### <a name="table-33-hresult-addradiogroup"></a>Tabella 33. HRESULT AddRadioGroup  

|**Parametro**|**Descrizione**|  
|-|-|  
|**groupName**|Stringa che definisce un gruppo di pulsanti di opzione in questa pagina|  
|**radioControlId**|ID di un singolo pulsante di opzione da aggiungere a questo gruppo|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Questo metodo consente di abilitare o disabilitare un intero gruppo di pulsanti di opzione. Quando si disabilita un gruppo di pulsanti opzione vengono disabilitati tutti i controlli pulsante di opzione del gruppo e gli eventuali elementi figlio di questi pulsanti di opzione che sono stati aggiunti con **AddToGroup**. Vedere la tabella 34 e la tabella 35.  

### <a name="table-34-enableradiogroup"></a>Tabella 34. EnableRadioGroup  

|**Parametro**|**Descrizione**|  
|-|-|  
|**groupName**|Nome di un gruppo di pulsanti di opzione già definito con una chiamata a **AddRadioGroup**|  
|**Attiva**|Impostare su TRUE per abilitare il gruppo di pulsanti di opzione e su FALSE per disabilitare il gruppo|  

### <a name="table-35-hresult-enableradiogroup"></a>Tabella 35. HRESULT EnableRadioGroup  

|**HRESULT**|**Descrizione**|  
|-|-|  
|**S_OK**|Il gruppo è abilitato o disabilitato|  
|**E_INVALIDARG**|Non è presente alcun gruppo di pulsanti di opzione con il nome specificato|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Prima di chiamare questo metodo, chiamare **AddField** per ogni campo che il codice XML può controllare. Questo metodo restituisce sempre **S_OK**.  

 Il parametro **pFieldCallback** è facoltativo. Se viene reso disponibile, il controller del modulo chiama **SetFieldDefault** per i controlli che non sono **CONTROL_STATIC_TEXT** né **CONTROL_CHECK_BOX**. Questo comportamento consente di recuperare un valore predefinito dal codice XML e di impostarlo direttamente nel controllo.  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Questo metodo consente di salvare i valori dei campi in variabili della sequenza di attività e nei dati di riepilogo che vengono visualizzati nella pagina **Riepilogo**. Se si specifica un puntatore in **pFieldCallback** è possibile gestire il salvataggio di valori per i controlli che non supportano **CONTROL_STATIC_TEXT**.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Questo metodo consente di determinare se un campo è stato disabilitato nel codice XML.  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Questo metodo inizializza i dati di riepilogo che vengono visualizzati nella pagina **Riepilogo**, come illustrato nella tabella 36. Chiamare questo metodo nel metodo **OnNextClicked** prima di chiamare **SaveFields**. Questo metodo restituisce sempre **S_OK**.  

### <a name="table-36-hresult-initsection"></a>Tabella 36. HRESULT InitSection  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Key**|Questo parametro deve essere univoco per la pagina. Viene usato per garantire che ogni pagina disponga delle proprie informazioni di riepilogo.|  
|**sectionCaption**|Intestazione che viene visualizzata nella pagina **Riepilogo** per le informazioni di riepilogo di questa pagina. In genere si usa **DisplayName()** come valore di questo parametro.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Questo metodo consente di aggiungere elementi di riepilogo alla pagina **Riepilogo** prima e dopo gli elementi impostati con il codice XML. Vedere la tabella 37.  

### <a name="table-37-hresult-addsummaryitem"></a>Tabella 37. HRESULT AddSummaryItem  

|**Parametro**|**Descrizione**|  
|-|-|  
|**First**|Didascalia dell'elemento di riepilogo, visualizzata sul lato sinistro|  
|**Second**|Valore che verrà visualizzato a destra|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Chiamare questo metodo per le variabili della sequenza di attività di cui non si vuole che i valori vengano scritti nel file di log. Chiamare questo metodo per le variabili della sequenza di attività che archiviano password, PIN o altri valori riservati che possono essere immessi da un utente.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Questo metodo salva il valore di un controllo di testo sia in una variabile della sequenza di attività sia nella sezione di riepilogo. In genere non è necessario chiamare direttamente questo metodo, perché il controller del modulo lo chiama per tutti i campi. Vedere la tabella 38.  

### <a name="table-38-hresult-savetext"></a>Tabella 38. HRESULT SaveText  

|**Parametro**|**Descrizione**|  
|-|-|  
|**controlId**|ID della casella di testo che contiene il valore che si vuole salvare (o qualsiasi altro controllo che può restituire testo)|  
|**tsVariableName**|Nome della variabile della sequenza di attività che si vuole modificare|  
|**summaryCaption**|Didascalia per questo valore nella pagina **Riepilogo**|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Questo metodo legge il valore di una variabile della sequenza di attività e imposta la casella di testo su questo valore.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Chiamare questo metodo sul metodo **OnControlEvent** per garantire che il controller di modulo possa elaborare eventi di controllo, operazione necessaria per il funzionamento corretto. I valori passati a questo metodo sono gli stessi valori passati al metodo **OnControlEvent**.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Questo metodo restituisce lo stato della convalida più recente del modulo. Se uno dei validator del controllo ha segnalato un errore, questo metodo restituisce FALSE. In altre parole, il metodo restituisce TRUE solo se tutti i controlli nella pagina sono validi.  

#### <a name="ivalidator-interface"></a>Interfaccia IValidator  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Panoramica  
 I *validator* sono componenti che possono convalidare un singolo controllo nella pagina. Il modo più semplice per implementare un validator è impostarlo come sottoclasse della classe **BaseValidator**, definita nel file di intestazione BaseValidator.h.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Se si crea un validator nel codice, è possibile chiamare questo metodo per inizializzare il validator. Vedere la tabella 39.  

### <a name="table-39-hresult-init"></a>Tabella 39. HRESULT Init  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pControl**|Controllo che il validator deve convalidare|  
|**Message**|Messaggio da visualizzare nella pagina se il controllo non è valido|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 Il controller del modulo chiama questo metodo per inizializzare i validator che crea in base al codice XML della pagina. Vedere la tabella 40.  

### <a name="table-40-hresult-init-method"></a>Tabella 40. Metodo HRESULT Init  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pControl**|Controllo che il validator deve convalidare|  
|**pContainer**|Utile se il validator richiede l'accesso al logger o deve creare altri componenti|  
|**pProperties**|Specifica l'accesso alle proprietà (elementi setter) per il validator|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 Questo metodo restituisce TRUE se il controllo è valido o FALSE se il controllo non è valido. Nell'output restituito, **pMessage** viene popolato da un nuovo **BSTR** contenente il messaggio da visualizzare quando il controllo non è valido.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 È possibile implementare questo metodo se sono necessari valori aggiuntivi non disponibili nel codice XML.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 È possibile implementare questo metodo se sono necessari valori aggiuntivi non disponibili nel codice XML.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 È possibile implementare questo metodo se sono necessari valori aggiuntivi non disponibili nel codice XML.  

#### <a name="iregex-interface"></a>Interfaccia IRegEx  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Questo metodo viene implementato dal componente **ID_Regex** (IRegex.h) e offre il supporto per l'elaborazione delle espressioni regolari.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Questo metodo confronta l'espressione regolare con il testo di input. Usa la funzione **regex_match** della libreria C++ standard per l'operazione. Il metodo restituisce TRUE se vengono trovate corrispondenze, FALSE in caso contrario.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Questo metodo consente di recuperare le corrispondenze della chiamata più recente di **MatchesRegex**. Si noti che questo metodo non include l'elaborazione degli errori e restituisce **S_OK** o genera un'eccezione.  

#### <a name="isummaryinfo-interface"></a>Interfaccia ISummaryInfo  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 Non è necessario usare direttamente questa interfaccia. Usare invece **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 Non è necessario usare direttamente questa interfaccia. Usare invece **IFormController**.  

#### <a name="itsvariablebag-interface"></a>Interfaccia ITSVariableBag  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Questa interfaccia offre l'accesso alle variabili della sequenza di attività. È possibile accedere all'interfaccia tramite il metodo **TSVariables()** della pagina.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 Questo metodo legge il valore di una variabile della sequenza di attività.  

> [!NOTE]
>  I valori vengono memorizzati nella cache dopo la prima lettura.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 Questo metodo imposta il valore di una variabile della sequenza di attività. Questo valore viene salvato in memoria. I valori della sequenza di attività vengono scritti dopo che si fa clic su **Fine** nella procedura guidata UDI.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Questo metodo rimuove tutti i valori della sequenza di attività che sono stati salvati in memoria.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Questo metodo rimuove dalla memoria un valore specifico della sequenza di attività. Quando si chiama di nuovo **GetValue** con lo stesso nome di sequenza di attività, il metodo prova a recuperare il valore dalla sequenza di attività.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Ogni volta che vengono scritte le variabili della sequenza di attività, ad esempio quando si fa clic su **Fine** nella procedura guidata UDI, i nomi e i valori vengono scritti nel file di log. Chiamare questo metodo per annullare la registrazione di valori sensibili, ad esempio password o PIN, per una variabile della sequenza di attività specifica.  

##### <a name="void-savevoid"></a>void Save(void)  
 Questo metodo consente di salvare tutti i valori della sequenza di attività che sono stati impostati con chiamate a **SetValue**.  

#### <a name="itsvariablerepository-interface"></a>Interfaccia ITSVariableRepository  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Questa interfaccia è destinata all'uso interno da parte di **TSVariableBag** per leggere e scrivere variabili della sequenza di attività.  

#### <a name="iwizardfinish-interface"></a>Interfaccia IWizardFinish  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Questa interfaccia è utile in scenari avanzati in cui si intende eseguire operazioni aggiuntive quando si fa clic su **Fine** o su **Annulla** nella procedura guidata UDI. La procedura guidata UDI contiene un'attività **Finish** che salva le variabili della sequenza di attività quando si fa clic su **Fine**. Se si annulla la procedura guidata, l'attività imposta solo la variabile della sequenza di attività **OSDSetupWizCancelled** su TRUE e non salva le modifiche apportate alle altre variabili della sequenza di attività.  

 Se si crea un proprio componente Finish è necessario registrarlo con codice simile al seguente:  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>Interfaccia IBindableList  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implementare questa interfaccia se è presente un componente origine dati che si vuole associare a una casella combinata chiamando il relativo metodo **Bind**.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Questo metodo restituisce il numero di elementi dell'elenco.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Questo metodo restituisce la didascalia dell'elemento in corrispondenza di un indice specifico.  

#### <a name="idatanodes-interface"></a>Interfaccia IDataNodes  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Questa interfaccia offre l'accesso ai dati gerarchici che possono essere salvati in una pagina. Questa interfaccia si ottiene tramite i metodi dell'interfaccia **ISettingsProperties**, disponibile per la pagina tramite il metodo **Settings**.  

 I dati nel codice XML di una pagina possono avere un aspetto simile al seguente  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 La chiamata di **Settings()->GetDataNode(L"Network", &pData)** produce un'istanza **IDataNodes** con due elementi di dati (ognuno dei quali a sua volta ha due proprietà).  

##### <a name="sizet-count"></a>size_t Count()  
 Questo metodo restituisce il numero di elementi **DataItem**.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 Il componente che supporta questa interfaccia supporta anche **IBindableList**, che rende più facile popolare una casella combinata con i dati del codice XML della pagina. Questo metodo controlla quale proprietà (setter) di ogni elemento **DataItem** viene usata per questa associazione. Ad esempio è possibile chiamare questo metodo con **DisplayName** e il metodo userà tale proprietà setter per l'associazione dei dati. La casella combinata risultante conterrà gli elementi **Public** e **Dev Team**.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Questo metodo ottiene una proprietà da uno degli elementi **DataItem**. Vedere la tabella 41 e la tabella 42.  

### <a name="table-41-dataitem-getproperty"></a>Tabella 41. DataItem GetProperty  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Index**|Valore di indice (a partire da 0) del **DataItem** per il quale si vuole recuperare un valore della proprietà|  
|**propertyName**|Nome della proprietà del setter per la quale si vuole recuperare un valore|  
|**propertyValue**|In fase di restituzione, contiene il valore stringa di una proprietà|  

### <a name="table-42-hresult-getproperty"></a>Tabella 42. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Descrizione**|  
|**S_OK**|La proprietà è stata recuperata.|  
|**E_INVALIDARG**|L'indice è oltre la fine della matrice.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Questo metodo è simile a **GetProperty**, ma anziché restituire un valore da un **DataItem** restituisce l'intero **DataItem** sottoposto a wrapping in un'interfaccia **ISettingsProperties**. Vedere la tabella 43 e la tabella 44.  

### <a name="table-43-hresult-getnode"></a>Tabella 43. HRESULT GetNode  

|**Parametro**|**Descrizione**|  
|-|-|  
|Indice|Valore di indice (a partire da 0) del **DataItem** per il quale si vuole recuperare un valore della proprietà|  
|**ppNode**|All'uscita, l'interfaccia **ISettingsProperties** che esegue il wrapping del nodo **DataItem**|  

### <a name="table-44-hresult-getnode-results"></a>Tabella 44. Risultati di HRESULT GetNode  

|**HRESULT**|**Descrizione**|  
|-|-|  
|**S_OK**|Il nodo è stato recuperato.|  
|**E_INVALIDARG**|L'indice è oltre la fine della matrice.|  

#### <a name="ifactoryregistry-interface"></a>Interfaccia IFactoryRegistry  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Quando si crea una nuova pagina personalizzata, è necessario creare come minimo una *page factory*, ovvero una classe che implementa **IClassFactory**. È possibile usare **ClassFactoryImpl** come classe base per la factory.  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type, IClassFactory \*pFactory)  
 Questo metodo registra una class factory nel registro. Vedere la tabella 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tabella 45. IClassFactory void Register  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Tipo**|Stringa che identifica la factory che si sta registrando; in genere la stringa di questo parametro deve includere il nome della società per garantire che sia univoco|  
|**pFactory**|Puntatore all'istanza della class factory|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Questo metodo è solo per uso interno.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 In genere questo metodo è solo per uso interno. Verifica se una class factory è stata registrata per un tipo.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type, IClassFactory **ppFactory)  
 Questo metodo consente di recuperare la class factory. In genere viene chiamata **CreateInstance**. Se tuttavia si vuole creare un numero elevato di istanze dello stesso componente, è più efficiente recuperare la factory e quindi impostarla per la creazione delle istanze.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, IUnknown **ppInstance)  
 Questo metodo crea una nuova istanza di un componente, dato il tipo del componente. Usare come alternativa il metodo del modello **CreateInstance**, che consente la creazione di oggetti indipendenti dai tipi.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Questo metodo è solo per uso interno.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 I *servizi* sono singole istanze di un componente che possono essere usati in diverse posizioni. È possibile usare questo metodo per registrare un servizio in una pagina e quindi recuperare la stessa istanza da un'altra pagina.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid, IUnknown **ppService)  
 Questo metodo recupera un servizio che è stato registrato in precedenza con una chiamata a RegisterService.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Questo metodo imposta la lingua della procedura guidata UDI sull'identificatore di lingua specificato nel parametro **languageId**.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Questo metodo restituisce il valore dell'identificatore di lingua reso disponibile con il parametro della riga di comando **/locale** per la procedura guidata UDI. Il metodo restituisce uno dei valori seguenti:  

-   Valore dell'identificatore di lingua reso disponibile con il parametro della riga di comando **/locale**  

-   0 se non è stato specificato il parametro della riga di comando **/locale**  

#### <a name="ilogger-interface"></a>Interfaccia ILogger  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Panoramica  
 La procedura guidata UDI registra le informazioni in un file di log, che semplifica la risoluzione dei problemi rilevati nel campo. La registrazione di informazioni nelle pagine è una procedura consigliata. È possibile ottenere un puntatore a questa interfaccia dall'interno della pagina tramite il metodo **Logger()** della pagina. Le righe del file di log contengono un numero di "livello", che rappresenta messaggi di errore, normali, dettagliati o di debug.  

> [!NOTE]
>  I messaggi di debug vengono salvati nel file di log solo se è abilitato il supporto del debug. È possibile attivare il supporto del debug aggiungendo la riga seguente all'elemento **Style** nel file con estensione config:  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Init  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="log"></a>Registro  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="error"></a>Errore  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Chiamare questo metodo per registrare informazioni su un errore. Vedere la tabella 46.  

### <a name="table-46-hresult-error"></a>Tabella 46. HRESULT Error  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Errore**|Codice di errore restituito da una chiamata (questo codice verrà visualizzato nella voce di registro come un numero).|  
|**Componente**|Stringa che identifica l'origine dell'errore, in genere la pagina o il componente che è stato creato|  
|**Message**|Messaggio che descrive la causa dell'errore|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Questo metodo è simile al metodo **Error** ma consente di visualizzare un messaggio in due parti. Il messaggio finale includerà "message" e quindi "message2" nel file di output. Il metodo viene reso disponibile per comodità.  

##### <a name="normal"></a>Normale  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Questo metodo registra un messaggio normale. Per i parametri, vedere la descrizione del metodo [Error](#Error).  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Questo metodo registra un messaggio normale. Per i parametri, vedere la descrizione del metodo [Error2](#Error2).  

##### <a name="verbose"></a>Dettagliato  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Questo metodo registra un messaggio dettagliato. Per i parametri, vedere la descrizione del metodo [Error](#Error).  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Questo metodo registra un messaggio dettagliato. Per i parametri, vedere la descrizione del metodo [Error2](#Error2).  

##### <a name="debug"></a>Debug  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Questo metodo registra un messaggio di debug. Per i parametri, vedere la descrizione del metodo [Error](#Error). I messaggi di debug vengono salvati nel file solo se il debug è abilitato. Per altre informazioni, vedere la sezione Panoramica.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="close"></a>Chiusura  

```  
HRESULT Close(void)  
```  

 Questo metodo è solo per uso interno.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Questo metodo recupera il nome del file di log.  

#### <a name="iorientation-interface"></a>Interfaccia IOrientation  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Questa interfaccia è solo per uso interno.  

#### <a name="isettings-interface"></a>Interfaccia ISettings  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Questa interfaccia è solo per uso interno.  

#### <a name="isettingsproperties-interface"></a>Interfaccia ISettingsProperties  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia offre l'accesso ai dati della pagina. Per ottenere il livello superiore dei dati della pagina, usare il metodo **Settings()** della pagina.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName, LPBSTR attributeValue)  
 Questo metodo consente di recuperare i valori degli attributi sul nodo principale, ovvero il nodo **Page** quando si usa il metodo **Settings()** della pagina.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Questo metodo offre l'accesso ai valori delle proprietà del setter sotto il nodo principale. Per una pagina, queste sono le proprietà di livello superiore.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath, IXMLDOMNodeList **ppList)  
 Chiamare questo metodo per ottenere direttamente un elenco di nodi XML usando un'espressione XPath. È preferibile usare uno degli altri metodi, se possibile. Usare questo metodo solo se non è possibile ottenere i nodi con altre modalità.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath, IXMLDOMNode **ppNode)  
 Chiamare questo metodo se si vuole ottenere direttamente un nodo XML singolo usando un'espressione XPath. È preferibile usare uno degli altri metodi, se possibile. Usare questo metodo solo se non è possibile ottenere un nodo con altre modalità.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name, ISettingsProperties **ppNode)  
 Consente di recuperare un elemento **Data** in base all'attributo **Name** dell'elemento.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Questo metodo recupera un elenco di elementi **DataItem** sotto il nodo corrente. Dal livello della pagina, chiamare **GetDataNode** per recuperare un'interfaccia **ISettingsProperty** per i dati. Quindi su questa istanza chiamare **GetDataNodes** per recuperare l'elenco di record. Considerare ad esempio il codice XML seguente:  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName, IDataNodes **ppNodes)  
 Questo metodo offre un modo rapido per ottenere il set di nodi **DataItem** in un nodo **Data** specifico. Sulla base del codice XML dell'esempio **GetDataNodes**, il codice seguente esegue esattamente le stesse operazioni delle quattro righe di codice dell'esempio sotto **GetDataNodes**, ma con il controllo errori:  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>Interfaccia ISimpleStringProperties  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 Di per sé questa interfaccia può risultare poco utile. Tuttavia è implementata dal componente **ID_SimpleStringProperties**, che implementa anche l'interfaccia **IStringProperties**. È possibile usare questo componente nei casi in cui è necessario passare un set di proprietà a un altro componente, ad esempio un'attività, ma si vuole aggiungere valori a livello di programmazione anziché usare valori dal codice XML. Di seguito è riportato un esempio d'uso di questa interfaccia:  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Questa interfaccia offre l'accesso diretto a un gruppo di elementi setter provenienti dal codice XML. È disponibile per le proprietà di una pagina mediante **Settings()->Properties()**.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Questo metodo consente recuperare un singolo valore proprietà. Vedere la tabella 47 e la tabella 48.  

### <a name="table-47-ihresult-get-property-value"></a>Tabella 47. IHRESULT Get Property Value  

|**Parametro**|**Descrizione**|  
|-|-|  
|**propertyName**|Nome della proprietà da leggere|  
|**pPropValue**|All'uscita contiene il valore della proprietà sotto forma di stringa (il valore sarà **nullptr** se la proprietà non è presente).|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tabella 48. Risultati di IHRESULT Get Property Value  

|||  
|-|-|  
|**HRESULT**|**Descrizione**|  
|**S_OK**|Il valore della proprietà è stato recuperato.|  
|**E_INVALIDARG**|Non è presente nessuna proprietà con il nome specificato.|  

#### <a name="itaskmanager-interface"></a>Interfaccia ITaskManager  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Questa interfaccia è implementata dal componente **TaskManager** (**ID_TaskManager** in ITaskManager.h), ovvero il componente che esegue le attività nella pagina preliminare. È possibile usare direttamente la pagina preliminare (opzione usata nella maggior parte dei casi) o creare una pagina propria e lasciare al componente la maggior parte del lavoro.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 È necessario chiamare questo metodo prima di qualsiasi altro metodo. Il metodo inizializza il componente **TaskManager**. Vedere la tabella 49.  

### <a name="table-49-hresult-init"></a>Tabella 49. HRESULT Init  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pPageView**|Consente di accedere alla pagina che esegue le attività (la pagina deve avere un set specifico di controlli, descritti nei parametri seguenti).|  
|**idListView**|ID di controllo di un controllo **ListView** che visualizza l'elenco delle attività e lo stato di tali attività|  
|**idMessage**|ID di controllo di una casella di testo usata per visualizzare un messaggio per l'attività selezionata|  
|**idRetryButton**|ID di controllo di un pulsante sul quale è possibile fare clic per eseguire di nuovo le attività|  
|**pPageInfo**|Wrapper del codice XML della pagina (**TaskManager** carica il set di attività per l'esecuzione da questo codice XML).|  
|**pCallback**|Può essere null (se il parametro non è null, **TaskManager** chiama il metodo **Started** quando avvia un'attività e il metodo **Finished** per ogni attività che completa l'esecuzione).|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Questo metodo imposta il messaggio che viene visualizzato se una o più attività hanno esito negativo.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Questo metodo avvia tutte le attività. Ogni attività viene avviata in un thread separato.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Questo metodo è solo per uso interno. Recupera il messaggio corrente per un'attività in base all'indice corrispondente nell'elenco delle attività.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType(size_t index, LPBSTR type)  
 Questo metodo recupera il "tipo" corrente per un'attività. I tipi disponibili sono visualizzati nella tabella 50.  

### <a name="table-50-hresult-getresulttype"></a>Tabella 50. HRESULT GetResultType  

|**Tipo**|**Descrizione**|  
|-|-|  
|**0**|Rappresenta un'attività che ha avuto esito positivo|  
|**1**|Rappresenta un'attività che ha restituito un avviso|  
|**-1**|Rappresenta un'attività non riuscita|  

 Il tipo viene recuperato esaminando il codice di uscita o il codice di errore dell'attività e trovando una corrispondenza nell'elemento XML <ExitCodes\> dell'attività.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Questo metodo è usato dalla pagina di stato e dalla pagina preliminare per recuperare la proprietà setter **BitmapFilename** e visualizzare un'immagine accanto al messaggio per l'attività evidenziata. In altre parole è possibile aggiungere un setter personalizzato al codice XML dell'attività e quindi recuperarlo con questo metodo.  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 Questo metodo recupera l'indice dell'attività attualmente selezionata, che risulta utile per recuperare informazioni aggiuntive sull'attività (vedere il metodo **GetProperty**) da visualizzare per l'attività selezionata. La pagina di stato e la pagina preliminare usano questo metodo per visualizzare un'immagine per l'attività selezionata.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Questo metodo opera principalmente con gli unit test in modo che il test garantisca il completamento delle attività prima del completamento dell'unit test. In genere questo metodo non viene chiamato direttamente. Viene restituito al completamento di tutte le attività in esecuzione o quando viene superato il tempo di attesa.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Questo metodo restituisce il numero di attività attualmente contrassegnate come non riuscite.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Questo metodo restituisce il numero di attività attualmente contrassegnate con un avviso.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Questo metodo restituisce il numero di attività attualmente contrassegnate come riuscite.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Questo metodo restituisce il numero di attività attualmente in esecuzione.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 Chiamare questo metodo dall'elemento **OnCommonControlEvent** della pagina, in modo che **TaskManager** possa elaborare gli eventi necessari.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 Chiamare questo metodo dall'elemento **OnControlEvent** della pagina, in modo che **TaskManager** possa elaborare gli eventi necessari.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Questo metodo è solo per uso interno.  

#### <a name="iwizardcomponent-interface"></a>Interfaccia IWizardComponent  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Panoramica  
 In genere questa interfaccia non viene implementata direttamente, ma tramite la classe modello **WizardComponent**. Se il componente implementa questa interfaccia ed è stata registrata una class factory con il registro, il componente riceve un puntatore all'istanza **IWizardPageContainer** al momento della creazione. Ciò facilita ad esempio l'accesso al logger o al registro per la creazione di altri componenti che potrebbero essere necessari per questo componente.  

#### <a name="iwizarddialogcontroller-interface"></a>Interfaccia IWizardDialogController  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Questa interfaccia è solo per uso interno.  

#### <a name="iwizarddialogview-interface"></a>Interfaccia IWizardDialogView  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Questa interfaccia è solo per uso interno.  

####  <a name="IWizardPageInterface"></a> Interfaccia IWizardPage  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è implementata da **WizardPageImpl**, quindi in genere non è necessario implementarla direttamente. La procedura guidata chiama tutti questi metodi quando interagisce con le pagine personalizzate.  

#### <a name="iwizardpagecontainer-interface"></a>Interfaccia IWizardPageContainer  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia è disponibile per la pagina tramite il metodo **Container** (implementato dal **WizardPageImpl**) e consente l'accesso a vari servizi della procedura guidata.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Usare questo metodo per scrivere messaggi nel file di log, ad esempio:  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Questo metodo offre l'accesso alle variabili "memory", proprietà che restano in memoria solo durante l'esecuzione della procedura guidata UDI. Queste proprietà sono disponibili per altre pagine nel codice o in XML tramite la sintassi **$memoryVarName$**.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>CreateInstance(LPCTSTR type, IUnknown **ppInstance)  
 Questo metodo consente di creare una nuova istanza di qualsiasi componente che è stato registrato. È tuttavia preferibile usare la funzione di modello **CreateInstance**, perché è fortemente tipizzata.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Questo metodo consente di recuperare un servizio che è stato registrato. È tuttavia preferibile chiamare la funzione di modello **GetService**, che è fortemente tipizzata (invece di usare **IUnknown**).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Questo metodo gestisce l'uso di variabili all'interno di valori stringa. Supporta i formati visualizzati nella tabella 51 e nella tabella 52.  

### <a name="table-51-hresult-replacevariables"></a>Tabella 51. HRESULT ReplaceVariables  

|**Formato**|**Descrizione**|  
|-|-|  
|**$Name$**|Sostituisce il valore di una variabile di memoria con questo nome (se non è presente nessuna variabile di memoria con il nome, il "token" viene rimosso).|  
|**%Name%**|Variabile della sequenza di attività o variabile di ambiente. L'ordine è il seguente:<br /><br /> 1.  Usare il valore di una variabile della sequenza di attività, se disponibile.<br />2.  Usare il valore di una variabile di ambiente, se disponibile.<br />3.  In caso contrario, rimuovere il testo dalla stringa.|  

### <a name="table-52-hresult-parameter"></a>Tabella 52. Parametro HRESULT  

|**Parametro**|**Descrizione**|  
|-|-|  
|**Origine**|Stringa di input che può contenere qualsiasi combinazione di variabili **$** e **%** o nessuna variabile|  
|**pDest**|In fase di restituzione, contiene una nuova stringa in cui tutti i token sono stati sostituiti in base alla tabella 51|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Questo metodo non è stato testato completamente. Consente di passare direttamente a una pagina specifica in base al nome della pagina, definito nel file XML con estensione config. Se si chiama questo metodo, il metodo **OnNextClicked** nella pagina viene ignorato. Il comportamento di questo metodo è soggetto a modifiche, pertanto il suo uso è a rischio dell'utente.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 Questo metodo visualizza una finestra di messaggio con il testo e la didascalia specificati. Il parametro **uType** è un valore che è possibile aggiungere alla funzione Win32 **MessageBox**.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Questo metodo restituisce TRUE se la procedura guidata è stata avviata in modalità "anteprima" fornendo l'opzione **/preview**. In modalità di anteprima il pulsante **Avanti** non è mai disabilitato. Questo metodo consente ad esempio di ignorare il codice in modalità di anteprima che potrebbe causare problemi quando non sono presenti dati validi nella pagina.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Questo metodo restituisce l'elemento **HWND** per la finestra di dialogo principale. Usare questo metodo con cautela. In genere l'API dell'applicazione guidata UDI è progettata in modo tale per cui l'utente non lavora mai direttamente con i punti di controllo della finestra.  

#### <a name="iwizardpageview-interface"></a>Interfaccia IWizardPageView  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Questa interfaccia è disponibile per il codice della pagina tramite il metodo **View**, implementato da **WizardPageImpl**.  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 La procedura guidata UDI usa i *wrapper*, che sono in realtà ambienti per l'interazione con i controlli della pagina. L'uso di tali ambienti invece dei controlli rende molto più semplice la scrittura di test per la pagina, perché è possibile specificare ambienti fittizi dai test.  

 Invece di usare direttamente questo metodo è preferibile usare il metodo del modello **GetControlWrapper** che è fortemente tipizzato, ad esempio:  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Questo metodo restituisce l'handle della finestra per la pagina. In genere non è necessario avere accesso a questo handle della finestra.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Solo se necessario, è possibile chiamare questo metodo per ottenere l'handle della finestra per un controllo della pagina. È preferibile chiamare la funzione di modello **GetControlWrapper**.  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 Questo metodo è solo per uso interno.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Questo metodo è solo per uso interno.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Imposta lo stato attivo per l'input a un controllo specifico.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Questo metodo è solo per uso interno.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Questo metodo è solo per uso interno.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Imposta lo stato attivo su uno dei pulsanti della procedura guidata. **WizardButtons** dispone di due valori: **BackButton** e **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Richiede che uno dei pulsanti della procedura guidata sia abilitato o disabilitato. Lo stato del pulsante potrebbe non corrispondere allo stato richiesto. Se ad esempio si esegue la procedura guidata UDI con l'opzione **/preview** i pulsanti sono sempre abilitati. **WizardButtons** ha due valori: **BackButton** e **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Questo metodo consente di visualizzare un messaggio di avviso nella parte inferiore dell'area del contenuto della pagina. Il testo del messaggio può essere personalizzato dall'utente.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Consente di nascondere un messaggio di avviso visualizzato con una chiamata a **ShowWarningMessage**.  

#### <a name="ixmldocument-interface"></a>Interfaccia IXmlDocument  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Panoramica  
 Questa interfaccia viene implementata dal componente **ID_IXmlDocument**, un ambiente progettato per semplificare il lavoro con i documenti XML in C++.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Questo metodo carica un documento XML da un file esterno. Restituisce **S_OK** se il file viene caricato senza errori o **S_FALSE** se si verifica un errore. Quando si verifica un errore è possibile ottenere il messaggio di errore chiamando **GetParseErrorMessage**.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Questo metodo carica un documento XML da una stringa anziché da un file esterno. Il comportamento è identico a quello del metodo **Load**, salvo per l'origine dalla quale viene letto il documento XML.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Questo metodo salva il documento XML presente in memoria in un file esterno.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Questo metodo restituisce una nuova stringa con il messaggio di errore associato al caricamento del documento XML, se presente. Restituisce sempre **S_OK**.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Questo metodo consente di usare un'espressione XPath per recuperare una raccolta di nodi dal documento. Restituisce sempre **S_OK**.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Questo metodo consente di usare un'espressione XPath per recuperare un nodo dal documento. Restituisce sempre **S_OK**.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Questo metodo aggiunge il nome di un file di schema esterno che viene usato per convalidare lo schema del documento XML quando viene caricato. Lo spazio dei nomi specificato è la stringa usabile nelle query XPath, anche se questa funzionalità non è stata sottoposta a test.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Questo metodo aggiunge un nuovo attributo a un nodo esistente nel documento XML. Vedere la tabella 53.  

### <a name="table-53-hresult-addattribute"></a>Tabella 53. HRESULT AddAttribute  

|**Parametro**|**Descrizione**|  
|-|-|  
|**pNode**|Nodo al quale si vuole aggiungere un attributo|  
|**Nome**|Nome del nuovo attributo|  
|**Valore**|Valore del nuovo attributo|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Chiamare questo metodo per creare un nuovo nodo:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Dopo aver creato un nuovo nodo, è possibile aggiungerlo come elemento figlio a un altro nodo chiamando il metodo **appendChild** del nodo padre.  

### <a name="helper-functions"></a>Funzioni helper  

#### <a name="createinstance-template-function"></a>Funzione di modello CreateInstance  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Questa funzione è definita in IWizardPageContainer.h e specifica un wrapper indipendente dai tipi tramite il metodo **IWizardPageContainer->CreateInstance**, ad esempio:  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Questo codice crea un nuovo componente **ID_Directory** per recuperare l'interfaccia **IDirectory** di tale componente.  

#### <a name="getservice-template-function"></a>Funzione di modello GetService  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Questa funzione è definita in IWizardPageContainer.h e specifica un wrapper indipendente dai tipi tramite il metodo **IWizardPageContainer->GetService**, ad esempio:  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Questa funzione recupera il componente sequenza di attività che supporta l'interfaccia **ITSVariableBag**. In alternativa, per **ITSVariableBag** è possibile usare il metodo TSVariables della classe **WizardPageImpl**.  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Riferimento per lo schema del file di configurazione di UDI Wizard Designer  
 Questo file viene usato da UDI Wizard Designer. Viene creato un file separato per ogni file con estensione dll personalizzato, che può contenere editor di pagine personalizzate della procedura guidata, attività personalizzate o validator personalizzati. Il file deve avere l'estensione *config* e trovarsi nella cartella *cartella_installazione*\Bin\Config (dove *cartella_installazione* è la cartella in cui è stato installato MDT).  

  La tabella 54 elenca gli elementi nel file di configurazione di UDI Wizard Designer e le relative descrizioni. L'elemento **DesignerConfig** è il nodo radice per questo riferimento.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>Tabella 54. Elementi del file di configurazione di UDI Wizard Designer e relative descrizioni  

|**Nome elemento**|**Descrizione**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Specifica la radice per tutti gli altri elementi|  
|[DesignerMappings](#DesignerMappings)|Raggruppa un set d elementi [Page](#Page)|  
|[Page](#Page)|Specifica un editor di pagine della procedura guidata da caricare in UDI Wizard Designer, usato per modificare le impostazioni di configurazione di una pagina della procedura guidata|  
|[Param](#Param)|Specifica un parametro che viene passato all'elemento padre [Task](#Task) o [Validator](#Validator) e corrisponde a un elemento [Setter]() nel file di configurazione della procedura guidata UDI. **Nota:** gli attributi per questo elemento sono diversi a seconda che l'elemento padre sia [Task](#Task) o [Validator](#Validator).|  
|[Task](#Task)|Specifica un'attività nella libreria di attività|  
|[TaskItem](#TaskItem)|Specifica un gruppo di parametri che vengono passati all'attività|  
|[TaskLibrary](#TaskLibrary)|Raggruppa un set d elementi [Task](#Task)|  
|[Validator](#Validator)|Specifica un validator all'interno della libreria di validator|  
|[ValidatorLibrary](#ValidatorLibrary)|Raggruppa un set di elementi [Validator](#Validator)|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 Specifica la radice per tutti gli altri elementi.  

##### <a name="element-information"></a>Informazioni sull'elemento  
  La tabella 55 visualizza informazioni sull'elemento [DesignerConfig](#DesignerConfig).  

### <a name="table-55-designerconfig-element-information"></a>Tabella 55. Informazioni sull'elemento DesignerConfig  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una: questo elemento è obbligatorio.|  
|Elementi padre|Nessuno|  
|Contenuti|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 Questo elemento raggruppa un set di elementi [Page](#Page).  

##### <a name="element-information"></a>Informazioni sull'elemento  
  La tabella 56 visualizza informazioni sull'elemento [DesignerMappings](#DesignerMappings).  

### <a name="table-56-designermappings-element-information"></a>Tabella 56. Informazioni sull'elemento DesignerMappings  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o una nell'elemento [DesignerConfig](#DesignerConfig). Questo elemento è facoltativo se nella DLL non è presente nessuna pagina personalizzata della procedura guidata corrispondente a questo file di configurazione di UDI Wizard Designer.|  
|Elementi padre|**DesignerConfig**|  
|Contenuti|**Page**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 Questo elemento specifica un editor di pagine della procedura guidata da caricare in UDI Wizard Designer, che a sua volta viene usato per modificare le impostazioni di configurazione di una pagina della procedura guidata.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 57 visualizza informazioni sull'elemento [Page](#Page).  

### <a name="table-57-page-element-information"></a>Tabella 57. Informazioni sull'elemento Page  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più per ogni pagina della procedura guidata definita nell'elemento [DesignerMappings](#DesignerMappings)|  
|Elementi padre|**DesignerMappings**|  
|Contenuti|Qualsiasi contenuto XML ben formato|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 58 elenca gli attributi dell'elemento [Page](#Page) e include una descrizione per ogni attributo.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>Tabella 58. Attributi e valori corrispondenti per l'elemento Page  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Descrizione**|Specifica testo che offre informazioni sul parametro e viene visualizzato in UDI Wizard Designer|  
|**DesignerAssembly**|Specifica il nome del file con estensione dll associato all'editor di pagine della procedura guidata (il file con estensione dll deve trovarsi nella cartella *cartella_installazione*\Bin (dove *cartella_installazione* è la cartella in cui è stato installato MDT).|  
|**DesignerType**|Specifica il nome dell'editor di pagine della procedura guidata incluso nel file con estensione dll specificato nell'attributo **DesignerAssembly** (questo è il tipo Microsoft .NET dell'editor di pagine della procedura guidata, con il nome completo dello spazio dei nomi Microsoft .NET).|  
|**DisplayName**|Specifica il nome descrittivo dell'editor di pagine, visualizzato in UDI Wizard Designer|  
|**DLL**|Specifica il nome del file con estensione dll associato alla pagina della procedura guidata (il file con estensione dll deve trovarsi nella cartella *cartella_installazione*\Templates\Distribution\Tools\\*piattaforma* (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma*  è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit). **Nota:** assicurarsi che l'architettura del processore DLL corrisponda all'architettura del processore MDT installato. Se ad esempio è stata installata una versione di MDT a 32 bit, assicurarsi di usare una DLL a 32 bit per la pagina della procedura guidata.|  
|**Image**|Specifica il nome di un'immagine della pagina in formato Portable Network Graphics (PNG) (il file con estensione png deve trovarsi nella cartella *cartella_installazione*\Bin\Images (dove *cartella_installazione* è la cartella in cui è stato installato MDT).|  
|**Tipo**|Specifica l'editor di pagine della procedura guidata e deve corrispondere al nome usato per la registrazione della pagina personalizzata.|  

##### <a name="remarks"></a>Note  
 UDI Wizard Designer usa l'elemento [Page](#Page) come modello per creare il codice XML iniziale per una nuova procedura guidata. UDI Wizard Designer esegue la convalida dello schema per garantire che l'elemento [Page](#Page) e gli elementi figlio abbiano un formato valido. Questo elemento offre un mapping tra il tipo di pagina della procedura guidata UDI e le informazioni richieste da UDI Wizard Designer per la modifica e la creazione di pagine di questo tipo mediante un editor di pagine personalizzate.  

##### <a name="example"></a>Esempio  
 Nessuno.  

####  <a name="Param"></a> Param  
 Questo elemento specifica un parametro che viene passato all'elemento padre [Task](#Task) o [Validator](#Validator) e corrisponde a un elemento [Setter]() nel file di configurazione della procedura guidata UDI.  

> [!NOTE]
>  Gli attributi per questo elemento sono diversi a seconda che l'elemento padre sia [Task](#Task) o [Validator](#Validator).  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 59 visualizza informazioni sull'elemento [Param](#Param).  

### <a name="table-59-param-element-information"></a>Tabella 59. Informazioni sull'elemento Param  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più per ogni elemento padre [TaskItem](#TaskItem) o [Validator](#Validator)|  
|Elementi padre|**TaskItem**, **Validator**|  
|Contenuti|Qualsiasi contenuto XML ben formato|  

##### <a name="element-attributes"></a>Attributi elemento  
  La tabella 60 elenca gli attributi dell'elemento [Param](#Param) e include una descrizione per ogni attributo.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>Tabella 60. Attributi e valori corrispondenti per l'elemento Param  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Descrizione**|Specifica testo che offre informazioni sul parametro e viene visualizzato in UDI Wizard Designer **Nota:** questo attributo è valido solo per l'elemento [Validator](#Validator).|  
|**DisplayName**|Specifica il nome descrittivo del parametro di convalida, visualizzato per la pagina della procedura guidata UDI appropriata in UDI Wizard Designer (tale nome è in genere più descrittivo rispetto all'attributo **Name**). **Nota:** questo attributo è valido solo per l'elemento [Validator](#Validator).|  
|**Nome**|Specifica il nome del parametro che viene passato all'attività o al validator, a seconda dell'elemento padre (questo attributo diventerà l'attributo **Property** di un elemento [Setter]() nel file di configurazione della procedura guidata UDI). **Nota:** questo parametro viene usato per entrambi gli elementi padre [TaskItem](#TaskItem) e [Validator](#Validator).|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Task"></a> Task  
 Questo elemento specifica un'attività nella libreria di attività.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 61 visualizza informazioni sull'elemento [Task](#Task).  

### <a name="table-61-task-element-information"></a>Tabella 61. Informazioni sull'elemento Task  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più all'interno dell'elemento [TaskLibrary](#TaskLibrary) (questo elemento non è facoltativo se è specificato l'elemento **TaskLibrary**).|  
|Elementi padre|**TaskLibrary**|  
|Contenuti|**TaskItem**|  

##### <a name="element-attributes"></a>Attributi elemento  
  La tabella 62 elenca gli attributi dell'elemento [Task](#Task) e include una descrizione per ogni attributo.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>Tabella 62. Attributi e valori corrispondenti per l'elemento Task  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Descrizione**|Specifica testo che offre informazioni sull'attività e viene visualizzato in UDI Wizard Designer|  
|**DLL**|Specifica il nome del file con estensione dll associato all'attività (il file con estensione dll deve trovarsi nella cartella *cartella_installazione*\Templates\Distribution\Tools\\*platform* (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma* è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit).|  
|**Nome**|Specifica il nome dell'attività, che viene visualizzato nella pagina della procedura guidata UDI appropriata e in UDI Wizard Designer|  
|**Tipo**|Specifica il tipo di attività, che viene registrato con il registro factory e consente di chiamare un'attività specifica in un file con estensione dll|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="TaskItem"></a> TaskItem  
 Questo elemento specifica un gruppo di parametri che vengono passati all'attività.  

##### <a name="element-information"></a>Informazioni sull'elemento  
  La tabella 63 visualizza informazioni sull'elemento [TaskItem](#TaskItem).  

### <a name="table-63-taskitem-element-information"></a>Tabella 63. Informazioni sull'elemento TaskItem  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più per ogni elemento **Task**|  
|Elementi padre|**Task**|  
|Contenuti|**Param**|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 64 elenca gli attributi dell'elemento [TaskItem](#TaskItem) e include una descrizione per ogni attributo.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tabella 64. Attributi e valori corrispondenti per l'elemento TaskItem  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Tipo**|Specifica il tipo di elemento che verrà creato nel file di configurazione della procedura guidata UDI. Viene creato un elemento XML che corrisponde al valore di questo attributo. Se ad esempio il valore di questo attributo è [File](#File), nel file di configurazione della procedura guidata UDI verrà creato un elemento **File**.<br /><br /> Attualmente, gli unici valori supportati sono:<br /><br /> -   **File**, che richiede due elementi figlio [Param](#Param) (un elemento figlio **Param** con l'attributo **Name** impostato su **Source** e un altro elemento figlio **Param** con l'attributo **Name** impostato su **Dest**)<br />-   [Setter](), che richiede un elemento figlio **Param**|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="TaskLibrary"></a> TaskLibrary  
 Questo elemento raggruppa un set di elementi [Task](#Task).  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 65 visualizza informazioni sull'elemento [TaskLibrary](#TaskLibrary).  

### <a name="table-65-tasklibrary-element-information"></a>Tabella 65. Informazioni sull'elemento TaskLibrary  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o una nell'elemento [DesignerConfig](#DesignerConfig). Questo elemento è facoltativo se nella DLL non è presente nessuna attività corrispondente a questo file di configurazione di UDI Wizard Designer.|  
|Elementi padre|**DesignerConfig**|  
|Contenuti|**Task**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 Questo elemento specifica un validator all'interno della libreria di validator.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 66 visualizza informazioni sull'elemento [Validator](#Validator).  

### <a name="table-66-validator-element-information"></a>Tabella 66. Informazioni sull'elemento Validator  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno dell'elemento [ValidatorLibrary](#ValidatorLibrary) (questo elemento è facoltativo).|  
|Elementi padre|**ValidatorLibrary**|  
|Contenuti|**Param**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 67 elenca gli attributi dell'elemento [Validator](#Validator) e include una descrizione per ogni attributo.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tabella 67. Attributi e valori corrispondenti per l'elemento Validator  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Descrizione**|Specifica testo che offre informazioni sul validator e viene visualizzato in UDI Wizard Designer|  
|**DisplayName**|Specifica il nome descrittivo del validator, visualizzato in UDI Wizard Designer (tale nome è in genere più descrittivo rispetto all'attributo **Name**).|  
|**DLL**|Specifica il nome del file con estensione dll associato al validator (il file con estensione dll deve trovarsi nella cartella *cartella_installazione*\Templates\Distribution\Tools\\*piattaforma* (dove *cartella_installazione* è la cartella in cui è stato installato MDT e *piattaforma*  è **x86** per la versione a 32 bit o **x64** per la versione a 64 bit).|  
|**Nome**|Specifica il nome del validator che viene visualizzato nella pagina della procedura guidata UDI appropriata e in UDI Wizard Designer|  
|**Tipo**|Specifica il tipo di validator che viene registrato con il registro factory e consente di chiamare un validator specifico in un file con estensione dll|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 Questo elemento raggruppa un set di elementi [Validator](#Validator).  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 68 visualizza informazioni sull'elemento [ValidatorLibrary](#ValidatorLibrary).  

### <a name="table-68-validatorlibrary-element-information"></a>Tabella 68. Informazioni sull'elemento ValidatorLibrary  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o uno nell'elemento [DesignerConfig](#DesignerConfig). Questo elemento è facoltativo se nella DLL non è presente nessun validator corrispondente a questo file di configurazione di UDI Wizard Designer.|  
|Elementi padre|**DesignerConfig**|  
|Contenuti|**Validator**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Richiede testo in un campo" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Non consente la presenza di determinati caratteri in un campo" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Deve seguire un motivo predefinito" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Richiede che il contenuto corrisponda a un'espressione regolare" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Riferimento per UDI Wizard Designer  

### <a name="controls"></a>Controlli  
 I controlli usati per creare editor di pagine personalizzate della procedura guidata da usare in UDI Wizard Designer sono istanze **UserControl** di WPF. La tabella 69 elenca i controlli che è possibile usare per creare editor di pagine personalizzate della procedura guidata.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabella 69. Controlli per la creazione di editor di pagine personalizzate della procedura guidata  

|Controllo|Descrizione|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Questo controllo consente di modificare i dati archiviati nell'elemento [Data](#Data) all'interno di un elemento [Page](#Page).|  
|[FieldElementControl](#FieldElementControl)|Questo controllo viene usato per modificare un campo, in genere collegato a un controllo TextBox nella pagina con estensione xaml.|  
|[SetterControl](#SetterControl)|Questo controllo viene usato per modificare il valore di un elemento [setter]() nel file di configurazione della procedura guidata UDI.|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 Questo controllo offre molte funzionalità per la modifica dei dati. Il modo migliore per imparare a usare questo controllo è l'esame dell'esempio, che illustra come modificare i dati nell'elemento **Data** di una pagina. In particolare l'esempio illustra come aggiungere, rimuovere e modificare elementi in questo controllo.  

####  <a name="FieldElementControl"></a> FieldElementControl  
 Usare questo controllo per modificare un campo che in genere è collegato a un controllo **TextBox** nella pagina con estensione xaml.  

##### <a name="example"></a>Esempio  
 Nel seguente codice estratto da un file con estensione xaml viene illustrato l'uso di **FieldElementControl** per configurare il valore predefinito per un campo in una pagina della procedura guidata usando un controllo **TextBox** figlio:  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Proprietà  

###### <a name="fielddata"></a>FieldData  
 Questa proprietà della stringa contiene informazioni per la connessione di **FieldElementControl** al codice XML sottostante per il campo. La connessione viene stabilita a una proprietà dell'interfaccia dell'editor di pagine. Nel seguente codice estratto da un file con estensione xaml viene illustrato l'uso della proprietà **FieldData**:  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 In questo codice l'interfaccia dell'editor di pagine è denominata **ControlRoot** ed è specificata nel parametro **ElementName**. L'associazione viene eseguita alla proprietà **DataContext.Location** dell'interfaccia dell'editor di pagine **ControlRoot**. **DataContext** è un modello di visualizzazione che punta all'elemento [Page](#Page) nel file di configurazione della procedura guidata UDI. **Location** è una proprietà della visualizzazione che restituisce un elenco delle posizioni possibili e viene definita mediante un elemento [Data](#Data) nel file di configurazione della procedura guidata UDI. Ogni posizione è definita da un elemento [DataItem](#DataItem) nel file di configurazione della procedura guidata UDI.  

###### <a name="headertext"></a>HeaderText  
 Questa proprietà della stringa consente di specificare un'intestazione per il controllo [FieldElementControl](#FieldElementControl). L'intestazione funge da titolo per il controllo e viene formattata come testo arancione in grassetto, visualizzato immediatamente sopra il controllo.  

###### <a name="instructiontext"></a>InstructionText  
 Questa proprietà della stringa consente di specificare testo informativo per il controllo [FieldElementControl](#FieldElementControl). In genere il testo viene usato per visualizzare una breve descrizione del campo e illustrare gli effetti della configurazione del campo sulla pagina della procedura guidata corrispondente.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Questa proprietà booleana consente di controllare la visibilità del pulsante che alterna lo stato tra **Unlocked** e **Locked** (abilitato o disabilitato). Se impostata su:  

-   **True** il pulsante non è visibile  

-   **False** il pulsante è visibile (questo è il valore predefinito).  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Questa proprietà booleana consente di controllare la visibilità della sezione che contiene il controllo usato per impostare il valore predefinito. Anche se la proprietà fa riferimento a una scheda, l'elemento [FieldElementControl](#FieldElementControl) non include alcuna scheda, bensì una sezione che può essere nascosta. Se impostata su:  

-   **True** la sezione non è visibile  

-   **False** la sezione è visibile (questo è il valore predefinito).  

###### <a name="hideborder"></a>HideBorder  
 Questa proprietà booleana consente di controllare la visibilità del bordo intorno al controllo del campo. Se impostata su:  

-   **True** il bordo non è visibile  

-   **False** il bordo è visibile (questo è il valore predefinito).  

###### <a name="hideimage"></a>HideImage  
 Questa proprietà booleana consente di controllare la visibilità dell'immagine configurata dalla proprietà **FieldImageSource**. Se impostata su:  

-   **True** l'immagine non è visibile  

-   **False** l'immagine è visibile (questo è il valore predefinito).  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Questa proprietà booleana consente di controllare la visibilità della sezione in cui viene gestito l'elenco di validator. Anche se la proprietà fa riferimento a una scheda, l'elemento [FieldElementControl](#FieldElementControl) non include alcuna scheda, bensì una sezione che può essere nascosta. Se impostata su:  

-   **True** la sezione non è visibile  

-   **False** la sezione è visibile (questo è il valore predefinito).  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Questa proprietà booleana consente di controllare la visibilità della sezione in cui è possibile configurare la didascalia di riepilogo del campo. La didascalia e il valore del campo corrispondente vengono visualizzati in un tipo pagina di procedura guidata **SummaryPage** in un flusso di fase. Anche se la proprietà fa riferimento a una scheda, l'elemento [FieldElementControl](#FieldElementControl) non include alcuna scheda, bensì una sezione che può essere nascosta. Se impostata su:  

-   **True** la sezione non è visibile  

-   **False** la sezione è visibile (questo è il valore predefinito).  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Questa proprietà booleana consente di controllare la visibilità della sezione in cui è possibile configurare la variabile della sequenza di attività corrispondente al campo. Anche se la proprietà fa riferimento a una scheda, l'elemento [FieldElementControl](#FieldElementControl) non include alcuna scheda, bensì una sezione che può essere nascosta. Se impostata su:  

-   **True** la sezione non è visibile  

-   **False** la sezione è visibile (questo è il valore predefinito).  


####  <a name="SetterControl"></a> SetterControl  
 Usare questo controllo per modificare il valore di un elemento [Setter]() nel file di configurazione della procedura guidata UDI. Questo controllo contiene un controllo figlio usato per modificare il valore dell'elemento **setter**.  

##### <a name="example"></a>Esempio  
 Il codice seguente, estratto da un file con estensione xaml, illustra l'uso di **SetterControl** per modificare un elemento [Setter]() con nome **KeyLocationSetter** usando un controllo **TextBox** figlio.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Proprietà  

###### <a name="setterdata"></a>SetterData  
 È necessario associare questo elemento a una proprietà della visualizzazione o del modello di visualizzazione che si connette al setter. La procedura è simile a quella di associazione a un campo, descritta per l'elemento **FieldElementControl**.  

###### <a name="headertext"></a>HeaderText  
 Questa proprietà consente di impostare il testo che viene visualizzato nell'intestazione del controllo. Può essere considerata come un titolo per il controllo e per impostazione predefinita viene visualizzata con testo arancione in grassetto.  

###### <a name="instructiontext"></a>InstructionText  
 Impostare questa proprietà con il testo da visualizzare sotto l'intestazione, in genere testo di istruzioni che indica all'utente dell'editor personalizzato quando e perché è utile modificare il comportamento del campo.  

### <a name="interfaces"></a>Interfacce  
La tabella 70 elenca le interfacce che è possibile usare per creare editor di pagine personalizzate della procedura guidata.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabella 70. Interfacce per la creazione di editor di pagine personalizzate della procedura guidata  

|**Interfaccia**|**Descrizione**|  
|-|-|  
|[IDataService](#IDataService)|Usare questa interfaccia per connettere i campi agli elementi **Data** nel file di configurazione della procedura guidata UDI.|  
|[IMessageBoxService](#IMessageBoxService)|Questa interfaccia offre l'accesso ai metodi che è possibile usare per visualizzare le finestre di messaggio.|  

####  <a name="IDataService"></a> IDataService  
 Questa interfaccia contiene molte proprietà e metodi, ma è probabile che sia necessario usare una sola proprietà. Questa proprietà è l'unica documentata qui.  

 È possibile usare l'inserimento di dipendenze per ottenere un puntatore a questa interfaccia, usando codice simile al seguente nella classe:  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Proprietà  
 La tabella 71 elenca le proprietà per l'interfaccia **IDataService**.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>Tabella 71. Proprietà per l'interfaccia IDataService  

|**Interfaccia**|**Descrizione**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Questa proprietà offre l'accesso agli elementi XML, agli attributi e ai valori sottostanti al contesto della pagina corrente in corso di modifica nel file di configurazione della procedura guidata UDI.|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Questa proprietà offre l'accesso al codice XML per la pagina corrente. Questa proprietà non va impostata, ma è possibile modificare il codice XML per la pagina. L'editor di pagine di esempio illustra esempi di modifica del codice XML. Questa proprietà viene usata soprattutto quando sono presenti dati personalizzati. Per i campi e le proprietà (setter) è possibile usare i controlli predefiniti che gestiscono tutti i dettagli.  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 Questa interfaccia offre l'accesso ai metodi che è possibile usare per visualizzare le finestre di messaggio. Ci si potrebbe chiedere perché è necessaria un'interfaccia per visualizzare una finestra di messaggio. In realtà l'interfaccia non è necessaria: Microsoft la usa nel codice, perché facilita la scrittura di test automatizzati per le pagine della finestra di progettazione.  

 Tuttavia l'uso di questi metodi offre un vantaggio: l'impostazione "owner" per le finestre di dialogo è sempre la procedura guidata UDI, pertanto la finestra di dialogo viene raggruppata correttamente con la finestra principale.  

 È possibile usare l'inserimento di dipendenze per ottenere un puntatore a questa interfaccia, usando codice simile al seguente nella classe:  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Metodi  
 La tabella 72 elenca i metodi per l'interfaccia **IMessageBoxService**.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>Tabella 72. Metodi per l'interfaccia IMessageBoxService  

|**Metodo**|**Descrizione**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Questo metodo con overload viene usato per visualizzare una finestra di messaggio con i membri seguenti:<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Usare questo metodo per creare una nuova finestra di dialogo.|  
|[ShowWizardWindow](#ShowWizardWindow)|Usare questo metodo per visualizzare un editor personalizzato all'interno di una finestra di dialogo che include i pulsanti **Avanti** e **Indietro** per la navigazione.|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 Questo metodo visualizza una casella di messaggio che è un elemento figlio dell'editor di pagine personalizzate della procedura guidata. Questo membro è in rapporto di overload: la tabella 73 contiene un elenco dei membri e una breve descrizione di ognuno. Per informazioni complete su ogni membro (che includono la sintassi, l'uso ed esempi), vedere le sezioni corrispondenti ai singoli membri.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>Tabella 73. Membri con overload per il metodo ShowMessagBox  

|Membro|Descrizione|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Visualizza una finestra di messaggio con un'icona e un pulsante **OK**|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Visualizza una finestra di messaggio con un'icona e diverse combinazioni possibili di pulsanti|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|Visualizza una finestra di messaggio che offre informazioni su un'eccezione e dispone di un pulsante **OK**|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Questo metodo visualizza una finestra di messaggio con un pulsante **OK**. Vedere la tabella 74.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>Tabella 74. Parametri per il metodo ShowMessageBox(String message, String caption, MessageBoxImage icon)  

|**Parametro**|**Descrizione**|  
|-|-|  
|**message**|Messaggio da visualizzare nell'area del contenuto della finestra di messaggio|  
|**caption**|Testo da visualizzare nella barra del titolo della finestra di dialogo|  
|**icon**|Tipo di icona da visualizzare nella finestra di messaggio|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Questo metodo visualizza una finestra di messaggio con il set di pulsanti che si vuole visualizzare e segnala il pulsante sul quale è stato fatto clic. Vedere la tabella 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>Tabella 75. Parametri per il metodo ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

|**Parametro**|**Descrizione**|  
|-|-|  
|**message**|Messaggio da visualizzare nell'area del contenuto della finestra di messaggio|  
|**caption**|Testo da visualizzare nella barra del titolo della finestra di dialogo|  
|**button**|Pulsanti da visualizzare|  
|**icon**|Tipo di icona da visualizzare nella finestra di messaggio|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 Questo metodo visualizza una finestra di messaggio che restituisce informazioni su un'eccezione. Questa finestra di messaggio ha un singolo pulsante **OK**. Vedere la tabella 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tabella 76. Parametri per il metodo ShowMessageBox(Exception exception)  

|**Parametro**|**Descrizione**|  
|-|-|  
|**exception**|Eccezione che si vuole segnalare (la finestra di dialogo usa come contenuto **exception.Message**).|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Questo metodo crea una nuova finestra di dialogo contenente il testo che l'utente specifica nel parametro **viewType**. La finestra di progettazione UDI crea una nuova istanza di questo tipo e ne esegue il wrapping in una finestra di dialogo che dispone di pulsanti **OK** e **Annulla**.  

 È possibile passare dati al controllo usando il parametro dialogPayload. La soluzione **SampleEditor** nella directory SDK include un esempio d'uso di questa funzionalità.  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Questo metodo consente di visualizzare un editor personalizzato all'interno di una finestra di dialogo che include i pulsanti **Avanti** e **Indietro** per la navigazione. Microsoft non ha reso disponibile un esempio d'uso di questo metodo.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> Riferimento per lo schema del file di configurazione della procedura guidata UDI  
 Questo file è consumato dalla procedura guidata UDI e configurato da UDI Wizard Designer. Il file viene usato per configurare:  

-   Pagine della procedura guidata visualizzate nella procedura guidata UDI  

-   Sequenza delle pagine della procedura guidata per la procedura guidata UDI  

-   Impostazioni per i campi in ogni pagina della procedura guidata  

-   Elementi StageGroups disponibili in UDI Wizard Designer  

-   Fasi disponibili all'interno di ogni procedura guidata di distribuzione in UDI Wizard Designer  

  La tabella 77 elenca gli elementi nel file di configurazione della procedura guidata UDI e le relative descrizioni. L'elemento **Wizard** è il nodo radice per questo riferimento.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>Tabella 77. Elementi nel file di configurazione della procedura guidata UDI e relative descrizioni  

|**Nome elemento**|**Descrizione**|  
|-|-|  
|[Data](#Data)|Raggruppa i singoli elementi [DataItem](#DataItem) all'interno di un elemento [Page](#Page) ed è denominato dall'attributo **Name**.|  
|[DataItem](#DataItem)|Raggruppa i singoli elementi [Setter]() all'interno di un elemento [Page](#Page). È possibile creare dati gerarchici includendo uno o più elementi [Data](#Data) in un elemento [DataItem](#DataItem). Ogni elemento **DataItem** rappresenta un elemento singolo. Ad esempio, un elenco di unità disponibili può avere un elemento **DataItem** per il nome visualizzato e un altro elemento **DataItem** per la lettera di unità corrispondente.|  
|[Impostazione predefinita](#Default)|Specifica un valore predefinito per il campo specificato nell'elemento padre [Field](#Field) o [RadioGroup](#RadioGroup). L'impostazione predefinita è il valore racchiuso in questo elemento.|  
|[DLL](#DLL)|Specifica una DLL che deve essere caricata e alla quale fanno riferimento la procedura guidata UDI e UDI Wizard Designer.|  
|[DLLs](#DLLs)|Raggruppa i singoli elementi [DLL](#DLL).|  
|[Error](#Error)|Specifica un codice di errore che può essere restituito da un'attività. Il valore del codice di errore viene restituito tramite **HRESULT** per l'attività e viene intercettato da questo elemento per visualizzare informazioni più specifiche sull'errore.|  
|[ExitCode](#ExitCode)|Specifica un possibile codice di uscita per un'attività. I codici di uscita sono codici restituiti previsti dall'attività. Creare un elemento **ExitCode** per ogni codice di uscita possibile. In alternativa è possibile specificare un asterisco (\*) nell'attributo **Value** per gestire i codici restituiti non elencati in altri elementi **ExitCode**.|  
|[ExitCodes](#ExitCodes)|Raggruppa un set di elementi [ExitCode](#ExitCode) ed [Error](#Error) per un elemento [Task](#Task) o un elemento **Error**.|  
|[Field](#Field)|Specifica un'istanza di un controllo in un elemento [Page](#Page) che viene usata per specificare la personalizzazione con XML. Solo i controlli che usano l'elemento [Field](#Field) consentono la personalizzazione con XML.|  
|[Fields](#Fields)|Raggruppa i singoli elementi [Field](#Field) all'interno di un elemento [Page](#Page).|  
|[File](#File)|Specifica l'origine e la destinazione di un'operazione di copia file usando il tipo di attività **Microsoft.Wizard.CopyFilesTask**. È possibile includere un elemento **File** separato per copiare più file in una singola attività.|  
|[Page](#Page)|Specifica un'istanza di una pagina e include tutte le impostazioni di configurazione per la pagina.|  
|[PageRef](#PageRef)|Specifica un riferimento a un'istanza di una pagina all'interno di un elemento [Stage](#Stage) incluso in un elemento [StageGroup](#StageGroup).|  
|[Pages](#Pages)|Raggruppa i singoli elementi [Page](#Page).|  
|[RadioGroup](#RadioGroup)|Specifica un gruppo di pulsanti di opzione all'interno di un elemento [Field](#Field).|  
|[StageGroup](#StageGroup)|Specifica un gruppo costituito da una o più fasi.|  
|[StageGroups](#StageGroups)|Raggruppa un set di gruppi di fasi in un file di configurazione della procedura guidata UDI.|  
|[Setter]()|Specifica un'impostazione di proprietà di un valore per una proprietà denominata nella proprietà **Property**.|  
|[Stage](#Stage)|Specifica una fase all'interno di un elemento [StageGroup](#StageGroup) e contiene uno o più elementi [PageRef](#PageRef).|  
|[Style](#Style)|Raggruppa i singoli elementi [setter]() che configurano l'aspetto della procedura guidata UDI, tra cui il titolo visualizzato in alto nella procedura guidata e l'immagine del banner visualizzata nella procedura guidata UDI.|  
|[Task](#Task)|Specifica un'attività che deve essere eseguita nella pagina specificata nell'elemento padre [Page](#Page).|  
|[Attività](#Tasks)|Raggruppa un set di attività per un elemento [Page](#Page).|  
|[Validator](#Validator)|Specifica un validator per il controllo campo specificato nell'elemento padre [Field](#Field).|  
|[Wizard](#Wizard)|Specifica la radice per tutti gli altri elementi.|  

####  <a name="Data"></a> Data  
 Questo elemento raggruppa i singoli elementi [DataItem](#DataItem) all'interno di un elemento [Page](#Page) ed è denominato dall'attributo **Name**.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 78 visualizza informazioni sull'elemento [Data](#Data).  

### <a name="table-78-data-element-information"></a>Tabella 78. Informazioni sull'elemento Data  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [Page](#Page) (questo elemento è facoltativo).|  
|Elementi padre|**Page**, **DataItem**|  
|Contenuti|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 79 elenca gli attributi dell'elemento [Data](#Data) e include una descrizione per ogni attributo.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>Tabella 79. Attributi e valori corrispondenti per l'elemento Data  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Nome**|Specifica il nome dell'elemento [Data](#Data)|  

##### <a name="remarks"></a>Note  
 L'attributo **Name** consente al codice di recuperare un set di dati specifico.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="DataItem"></a> DataItem  
 Questo elemento raggruppa i singoli elementi [Setter]() all'interno di un elemento [Page](#Page). È possibile creare dati gerarchici includendo uno o più elementi [Data](#Data) in un elemento [DataItem](#DataItem). Ogni elemento **DataItem** rappresenta un elemento singolo. Ad esempio, un elenco di unità disponibili può avere un elemento **DataItem** per il nome visualizzato e un altro elemento **DataItem** per la lettera di unità corrispondente.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 80 visualizza informazioni sull'elemento [DataItem](#DataItem).  

### <a name="table-80-dataitem-element-information"></a>Tabella 80. Informazioni sull'elemento DataItem  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [Data](#Data) (questo elemento è facoltativo).|  
|Elementi padre|**Data**|  
|Contenuti|**Data**, **Setter**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

#### <a name="default"></a>Predefinito  
 Questo elemento specifica un valore predefinito per il campo specificato nell'elemento padre [Field](#Field) o [RadioGroup](#RadioGroup). L'impostazione predefinita è il valore racchiuso in questo elemento.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 81 visualizza informazioni sull'elemento [Default](#Default).  

### <a name="table-81-default-element-information"></a>Tabella 81. Informazioni sull'elemento Default  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze |Zero o più all'interno di ogni elemento [Field](#Field) o [RadioGroup](#RadioGroup) (questo elemento è facoltativo).|  
|Elementi padre|**Field**, **RadioGroup**|  
|Contenuti|Può essere qualsiasi contenuto XML ben formato, ma in genere è testo standard|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nell'esempio seguente il valore predefinito per il campo **TimeZone** viene impostato su "Pacific Standard Time" (Ora solare Pacifico):  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 Questo elemento specifica una DLL che la procedura guidata UDI e UDI Wizard Designer possono caricare e usare come riferimento.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 82 visualizza informazioni sull'elemento [DLL](#DLL).  

### <a name="table-82-dll-element-information"></a>Tabella 82. Informazioni sull'elemento DLL  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più all'interno dell'elemento [DLLs](#DLLs)|  
|Elemento padre|**DLLs**|  
|Contenuti|Nessun contenuto consentito per questo elemento|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 83 elenca gli attributi dell'elemento [DLL](#DLL) e include una descrizione per ogni attributo.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>Tabella 83. Attributi e valori corrispondenti per l'elemento DLL  

|**Attributo**|**Descrizione**|  
|-|-|  
|Name|Specifica il nome della DLL che viene usata come riferimento dalla procedura guidata UDI e da UDI Wizard Designer|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 Questo elemento raggruppa i singoli elementi [DLL](#DLL).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 84 visualizza informazioni sull'elemento [DLLs](#DLLs).  

### <a name="table-84-dlls-element-information"></a>Tabella 84. Informazioni sull'elemento DLLs  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Uno|  
|Elementi padre|**Wizard**|  
|Contenuti|**DLL**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 Questo elemento specifica un codice di errore che può essere restituito da un'attività. Il valore del codice di errore viene restituito e intercettato tramite **HRESULT** per l'attività, allo scopo di offrire informazioni più specifiche sull'errore.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 85 visualizza informazioni sull'elemento [Error](#Error).  

### <a name="table-85-error-element-information"></a>Tabella 85. Informazioni sull'elemento Error  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [ExitCode](#ExitCode) (questo elemento è facoltativo).|  
|Elementi padre|**ExitCodes**|  
|Contenuti|Qualsiasi contenuto XML ben formato|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 86 elenca gli attributi dell'elemento [Error](#Error) e include una descrizione per ogni attributo.  

###  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Stato**|Specifica lo stato di restituzione di un'attività che ha rilevato un errore. In genere il valore di questo attributo è impostato su Error. Il valore viene visualizzato nella colonna **State** della pagina della procedura guidata nella procedura guidata UDI.|  
|**Text**|Specifica il testo descrittivo per la condizione di errore rilevata dall'attività.|  
|**Tipo**|Specifica se questo elemento rappresenta un errore, un avviso o un'operazione completata. Il valore specificato in **Type** deve essere univoco all'interno di un elemento [ExitCodes](#ExitCodes). I valori validi per questo elemento sono i seguenti:<br /><br /> -   **0.** L'elemento rappresenta un'operazione completata.<br />-   **1.** L'elemento rappresenta un avviso.<br />-   **-1.** L'elemento rappresenta un errore.|  
|**Valore**|Specifica il valore del codice restituito dall'attività come valore numerico. La specificazione di un asterisco (*) indica l'elemento predefinito per i codici di restituzione non presenti in altri elementi [Error](#Error).|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="ExitCode"></a> ExitCode  
 Questo elemento specifica un possibile codice di uscita per un'attività. I codici di uscita sono codici restituiti previsti dall'attività. Creare un elemento **ExitCode** per ogni codice di uscita possibile. In alternativa è possibile specificare un asterisco (\*) nell'attributo **Value** per gestire i codici restituiti non elencati in altri elementi **ExitCode**.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 87 visualizza informazioni sull'elemento [ExitCode](#ExitCode).  

### <a name="table-87-exitcode-element-information"></a>Tabella 87. Informazioni sull'elemento ExitCode  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [ExitCodes](#ExitCodes) (questo elemento è facoltativo).|  
|Elementi padre|**ExitCodes**|  
|Contenuti|Almeno un elemento [ExitCode](#ExitCode) e zero o più elementi [Error](#Error)|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 88 elenca gli attributi dell'elemento [ExitCode](#ExitCode) e include una descrizione per ogni attributo.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>Tabella 88. Attributi e valori corrispondenti per l'elemento ExitCode  

|**Attributo**|Descrizione|  
|-|-|  
|**Stato**|Specifica lo stato restituito da un'attività. Il valore dell'attributo viene visualizzato nella colonna **State** della pagina della procedura guidata corrispondente nella procedura guidata UDI. È possibile usare tutti i valori per questo attributo significativi per l'attività. I valori seguenti sono quelli tipici usati per questo attributo:<br /><br /> -   Success<br />-   Warning<br />-   Error|  
|**Text**|Specifica il testo descrittivo per il codice esistente dell'attività.|  
|**Tipo**|Specifica se questo elemento rappresenta un errore, un avviso o un'operazione completata. Il valore specificato per il tipo deve essere univoco all'interno di un elemento [ExitCodes](#ExitCodes). I valori validi per questo elemento sono i seguenti:<br /><br /> -   **0.** L'elemento rappresenta un'operazione completata.<br />-   **1.** L'elemento rappresenta un avviso.<br />-   **-1.** L'elemento rappresenta un errore.|  
|**Valore**|Specifica il valore del codice restituito dall'attività come valore numerico. La specificazione di un asterisco (*) indica l'elemento predefinito per i codici di restituzione non presenti in altri elementi [ExitCode](#ExitCode).|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="ExitCodes"></a> ExitCodes  
 Questo elemento raggruppa un set di elementi [ExitCode](#ExitCode) e [Error](#Error) per un elemento [Task](#Task) o un elemento **Error**.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 89 visualizza informazioni sull'elemento [ExitCodes](#ExitCodes).  

### <a name="table-89-exitcodes-element-information"></a>Tabella 89. Informazioni sull'elemento ExitCodes  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una all'interno di ogni elemento [Task](#Task)|  
|Elementi padre|**Task**|  
|Contenuti|**Error**, **ExitCode**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Field"></a> Field  
 Questo elemento specifica un'istanza di un controllo in un elemento [Page](#Page) che viene usata per definire la personalizzazione con XML. Solo i controlli che usano l'elemento [Field](#Field) consentono la personalizzazione con XML.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 90 visualizza informazioni sull'elemento [Field](#Field).  

### <a name="table-90-field-element-information"></a>Tabella 90. Informazioni sull'elemento Field  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [Field](#Field) (questo elemento è facoltativo).|  
|Elementi padre|**Fields**|  
|Contenuti|**Default**, **Validator**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 91 elenca gli attributi dell'elemento [Field](#Field) e include una descrizione per ogni attributo.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tabella 91. Attributi e valori corrispondenti per l'elemento Field  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Enabled**|Specifica se il campo è abilitato per l'input utente (l'attributo può essere impostato su True o False).|  
|**Nome**|Specifica il nome del campo|  
|**Riepilogo**|Specifica il testo descrittivo visualizzato nella pagina **Riepilogo** della procedura guidata per il valore impostato da questo campo|  
|**VarName**|Specifica il nome variabile della sequenza di attività letto o configurato tramite il campo nell'elemento padre [Field](#Field)|  

##### <a name="remarks"></a>Note  
 Questo elemento può contenere zero o più elementi [Default](#Default) e zero o più elementi [Validator](#Validator).  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Fields"></a> Fields  
 Questo elemento raggruppa i singoli elementi [Field](#Field) all'interno di un elemento [Page](#Page).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 92 visualizza informazioni sull'elemento [Fields](#Fields).  

### <a name="table-92-fields-element-information"></a>Tabella 92. Informazioni sull'elemento Fields  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento [Page](#Page) (questo elemento è facoltativo).|  
|Elementi padre|**Page**|  
|Contenuti|**Field**, **RadioGroup**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="File"></a> File  
 Questo elemento specifica l'origine e la destinazione di un'operazione di copia file usando il tipo di attività **Microsoft.Wizard.CopyFilesTask**. È possibile includere un elemento [File](#File) separato per copiare più file in una singola attività.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 93 visualizza informazioni sull'elemento [File](#File).  

### <a name="table-93-file-element-information"></a>Tabella 93. Informazioni sull'elemento File  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più occorrenze per ogni attività di tipo **Microsoft.Wizard.CopyFilesTask**|  
|Elementi padre|**Task**|  
|Contenuti|Nessuno|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 94 elenca gli attributi dell'elemento [File](#File) e include una descrizione per ogni attributo.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>Tabella 94. Attributi e valori corrispondenti per l'elemento File  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Dest**|Specifica il percorso completo o relativo alla cartella di destinazione per il file specificato nell'attributo **Source**. Le variabili di ambiente sono consentite come parte del percorso.|  
|**Origine**|Specifica il percorso completo o relativo al file di origine copiato dal tipo di attività **Microsoft.Wizard.CopyFilesTask**. Questo attributo supporta i caratteri jolly, pertanto è possibile copiare più file usando un singolo elemento [File](#File). Le variabili di ambiente sono consentite come parte del percorso.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="PageElement"></a> Page  
 Questo elemento specifica un'istanza di una pagina e include tutte le impostazioni di configurazione per la pagina.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 95 visualizza informazioni sull'elemento [Page](#Page).  

### <a name="table-95-page-element-information"></a>Tabella 95. Informazioni sull'elemento Page  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più all'interno di ogni elemento [Pages](#Pages)|  
|Elementi padre|**Pages**|  
|Contenuti|**Data**, **Fields**, **Setter**, **Tasks**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 96 elenca gli attributi dell'elemento [Page](#Page) e include una descrizione per ogni attributo.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>Tabella 96. Attributi e valori corrispondenti per l'elemento Page  

|**Attributo**|**Descrizione**|  
|-|-|  
|**DisplayName**|Specifica il nome descrittivo della pagina della procedura guidata visualizzata in UDI Wizard Designer. Questo nome è in genere più descrittivo rispetto all'attributo **Name**.|  
|**Nome**|Specifica il nome della pagina della procedura guidata visualizzata in UDI Wizard Designer.|  
|**Tipo**|Specifica il tipo di pagina della procedura guidata che è direttamente correlata a una pagina della procedura guidata specifica in una DLL.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="PageRef"></a> PageRef  
 Questo elemento specifica un riferimento a un'istanza di una pagina all'interno di un elemento [Stage](#Stage) incluso in un elemento [StageGroup](#StageGroup).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 97 visualizza informazioni sull'elemento [PageRef](#PageRef).  

### <a name="table-97-pageref-element-information"></a>Tabella 97. Informazioni sull'elemento PageRef  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più in un elemento [Stage](#Stage)|  
|Elementi padre|**Stage**|  
|Contenuti|Nessuno|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 98 elenca l'attributo dell'elemento [PageRef](#PageRef) e include una descrizione dell'attributo.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tabella 98. Attributi e valori corrispondenti per l'elemento PageRef  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Page**|Specifica l'istanza di una pagina all'interno di un elemento [Stage](#Stage) incluso in un elemento [StageGroup](#StageGroup). Impostare questo valore sull'attributo Name di un elemento [Page](#Page).|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Pages"></a> Pages  
 Questo elemento raggruppa i singoli elementi [Page](#Page).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 99 visualizza informazioni sull'elemento [Pages](#Pages).  

### <a name="table-99-pages-element-information"></a>Tabella 99. Informazioni sull'elemento Pages  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Uno|  
|Elementi padre|**Wizard**|  
|Contenuti|**Page**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 Questo elemento specifica un gruppo di pulsanti di opzione all'interno di un elemento [Field](#Field).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 100 visualizza informazioni sull'elemento [RadioGroup](#RadioGroup).  

### <a name="table-100-radiogroup-element-information"></a>Tabella 100. Informazioni sull'elemento RadioGroup  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di un elemento [Fields](#Fields) (questo elemento è facoltativo).|  
|Elementi padre|**Fields**|  
|Contenuti|**Impostazione predefinita**|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 101 elenca gli attributi dell'elemento [RadioGroup](#RadioGroup) e include una descrizione per ogni attributo.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>Tabella 101. Attributi e valori corrispondenti per l'elemento RadioGroup  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Locked**|Specifica se il gruppo di pulsanti di opzione è abilitato per l'input utente. L'attributo può essere impostato su:<br /><br /> -   **True**. Specifica che i pulsanti di opzione sono disabilitati e gli utenti non possono selezionare un pulsante di opzione nel gruppo.<br />-   **False**. Specifica che i pulsanti di opzione sono abilitati e gli utenti possono selezionare un pulsante di opzione nel gruppo.|  
|**Nome**|Specifica il nome del gruppo di pulsanti di opzione.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="StageGroup"></a> StageGroup  
 Questo elemento specifica un gruppo di fasi di distribuzione.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 102 visualizza informazioni sull'elemento [StageGroup](#StageGroup).  

### <a name="table-102-stagegroup-element-information"></a>Tabella 102. Informazioni sull'elemento StageGroup  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più in un elemento [StageGroups](#StageGroups)|  
|Elementi padre|**StageGroups**|  
|Contenuti|**Stage**|  

##### <a name="element-attributes"></a>Attributi elemento  
 La tabella 103 elenca gli attributi dell'elemento [StageGroup](#StageGroup) e include una descrizione per ogni attributo.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>Tabella 103. Attributi e valori corrispondenti per l'elemento StageGroup  

|**Attributo**|**Descrizione**|  
|-|-|  
|**DisplayName**|Specifica il nome descrittivo del gruppo di fasi visualizzato in UDI Wizard Designer. Questo nome è in genere più descrittivo rispetto all'attributo **Name**.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="StageGroups"></a> StageGroups  
 Questo elemento raggruppa un set di gruppi di fasi in un file di configurazione della procedura guidata UDI.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 104 visualizza informazioni sull'elemento [StageGroups](#StageGroups).  

### <a name="table-104-stagegroups-element-information"></a>Tabella 104. Informazioni sull'elemento StageGroups  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o una all'interno di un elemento [Wizard](#Wizard)|  
|Elementi padre|**Wizard**|  
|Contenuti|**StageGroup**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Setter"></a> Setter  
 Questo elemento specifica un'impostazione per il valore di una proprietà denominata nella proprietà **Property**.  

##### <a name="element-information"></a>Informazioni sull'elemento  
 La tabella 105 visualizza informazioni sull'elemento [Setter]().  

### <a name="table-105-setter-element-information"></a>Tabella 105. Informazioni sull'elemento Setter  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o più all'interno di ogni elemento padre (questo elemento è facoltativo).|  
|Elementi padre|**Data**, **DataItem**, **Page**, **Style**, **Task**, **Validator**|  
|Contenuti|Contiene un valore stringa nell'attributo **Property**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 106 elenca l'attributo dell'elemento [Setter]() e include una descrizione dell'attributo.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>Tabella 106. Attributi e valori corrispondenti per l'elemento Setter  

|**Attributo**|**Descrizione**|  
|-|-|  
|**Proprietà**|Specifica il nome della proprietà da impostare. Il nome della proprietà è impostato sul valore che questo attributo racchiude tra parentesi quadre.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

#### <a name="stage"></a>Fase  
 Questo elemento specifica un elemento [Stage](#Stage) all'interno di un elemento [StageGroup](#StageGroup) e contiene uno o più elementi [PageRef](#PageRef).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 107 visualizza informazioni sull'elemento [Stage](#Stage).  

### <a name="table-107-stage-element-information"></a>Tabella 107. Informazioni sull'elemento Stage  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più in un elemento [StageGroup](#StageGroup)|  
|Elementi padre|**StageGroup**|  
|Contenuti|**PageRef**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 108 elenca gli attributi dell'elemento [Stage](#Stage) e include una descrizione per ogni attributo.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>Tabella 108. Attributi e valori corrispondenti per l'elemento Stage  

|**Attributo**|**Descrizione**|  
|-|-|  
|**DisplayName**|Specifica il nome descrittivo della pagina della procedura guidata visualizzata in UDI Wizard Designer. Questo nome è in genere più descrittivo rispetto all'attributo **Name**.|  
|**Nome**|Specifica il nome della fase. Il valore di questo elemento viene usato quando si avvia la procedura guidata UDI con il parametro della riga di comando **/stage: name**.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Style"></a> Style  
 Questo elemento raggruppa i singoli elementi [Setter]() che configurano l'aspetto della procedura guidata UDI, tra cui il titolo visualizzato in alto nella procedura guidata e l'immagine del banner visualizzata nella procedura guidata UDI.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 109 visualizza informazioni sull'elemento Style.  

### <a name="table-109-style-element-information"></a>Tabella 109. Informazioni sull'elemento Style  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Uno|  
|Elementi padre|**Wizard**|  
|Contenuti|**Setter**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 Questo elemento specifica un'attività che deve essere eseguita nella pagina specificata nell'elemento padre [Page](#Page).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 110 visualizza informazioni sull'elemento [Task](#Task).  

### <a name="table-110-task-element-information"></a>Tabella 110. Informazioni sull'elemento Task  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Una o più in un elemento [Task](#Tasks)|  
|Elementi padre|**Attività**|  
|Contenuti|**ExitCodes**, **File**, **Setter**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 111 elenca gli attributi dell'elemento [Task](#Task) e include una descrizione per ogni attributo.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>Tabella 111. Attributi e valori corrispondenti per l'elemento Task  

|**Attributo**|**Descrizione**|  
|-|-|  
|**DependsOn**|Specifica se l'attività è dipendente da un'altra attività. Il valore di questo attributo è impostato sull'attributo **Name** di un altro elemento [Task](#Task). **Nota:** questo attributo non può essere configurato con UDI Wizard Designer. È tuttavia possibile aggiungere manualmente l'attributo a un elemento [Task](#Task) modificando direttamente il file con estensione xml.|  
|**DisplayName**|Specifica il nome descrittivo dell'attività visualizzata in UDI Wizard Designer. Questo nome è in genere più descrittivo rispetto all'attributo **Name**.|  
|**Nome**|Specifica il nome dell'attività. Il nome deve essere univoco.|  
|Type|Specifica il tipo di attività per l'attività da eseguire, che viene definito nella DLL contenente l'attività.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Tasks"></a> Tasks  
 Questo elemento raggruppa un set di attività per un elemento [Page](#Page).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 112 visualizza informazioni sull'elemento [Tasks](#Tasks).  

### <a name="table-112-tasks-element-information"></a>Tabella 112. Informazioni sull'elemento Tasks  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o una all'interno di ogni elemento [Page](#Page) (questo elemento è facoltativo).|  
|Elementi padre|**Page**|  
|Contenuti|**Task**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 113 elenca gli attributi dell'elemento [Tasks](#Tasks) e include una descrizione per ogni attributo.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>Tabella 113. Attributi e valori corrispondenti per l'elemento Tasks  

|**Attributo**|**Descrizione**|  
|-|-|  
|**NameTitle**|Specifica la didascalia visualizzata in alto nella colonna che contiene il nome delle attività nella pagina della procedura guidata appropriata.|  
|**StatusTitle**|Specifica la didascalia visualizzata in alto nella colonna che contiene lo stato delle attività nella pagina della procedura guidata appropriata.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="ValidatorElement"></a> Validator  
 Questo elemento specifica un validator per il controllo campo specificato nell'elemento padre [Field](#Field).  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 114 visualizza informazioni sull'elemento [Validator](#Validator).  

### <a name="table-114-validator-element-information"></a>Tabella 114. Informazioni sull'elemento Validator  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Zero o una all'interno di un elemento [Field](#Field)|  
|Elementi padre|**Field**|  
|Contenuti|**Setter**|  

##### <a name="element-attributes"></a>Attributi elemento  
La tabella 115 elenca l'attributo dell'elemento [Validator](#Validator) e include una descrizione dell'attributo.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>Tabella 115. Attributi e valori corrispondenti per l'elemento Validator  

|**Attributo**|**Descrizione**|  
|-|-|  
|Type|Specifica il tipo del validator, che viene definito nella DLL contenente il validator stesso.|  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  
 Nessuna.  

####  <a name="Wizard"></a> Wizard  
 Specifica la radice per tutti gli altri elementi.  

##### <a name="element-information"></a>Informazioni sull'elemento  
La tabella 116 visualizza informazioni sull'elemento [Wizard](#Wizard).  

### <a name="table-116-wizard-element-information"></a>Tabella 116. Informazioni sull'elemento Wizard  

|**Attributo**|**Valore**|  
|-|-|  
|Numero di occorrenze|Uno|  
|Elementi padre|Nessuno|  
|Contenuti|**DLLs**, **Pages**, **StageGroups**, **Style**|  

##### <a name="element-attributes"></a>Attributi elemento  
 Questo elemento non ha attributi.  

##### <a name="remarks"></a>Note  
 Nessuna.  

##### <a name="example"></a>Esempio  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
