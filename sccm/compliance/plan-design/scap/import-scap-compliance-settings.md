---
title: Importare le impostazioni di conformità SCAP
titleSuffix: Configuraton Manager
description: Importare le impostazioni di conformità SCAP come linee di base di configurazione ed esportare i risultati
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importare i file con estensione cab conformi a Impostazioni di compatibilità in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella Technical Preview versione 1803 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features). Questa versione non definitiva delle estensioni SCAP può essere installata in qualsiasi versione attualmente supportata di Configuration Manager Current Branch e LTSB 1606. A partire dalla Technical Preview 1803, il file di installazione si trova in cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

Il passaggio successivo del processo consiste nell'utilizzare la console di Configuration Manager per importare i file con estensione cab conformi a Impostazioni di compatibilità in Configuration Manager. Quando si importano i file con estensione cab creati in precedenza in questo processo, uno o più elementi di configurazione e linee di base di configurazione vengono creati nel database di Configuration Manager. In seguito, nel processo, è possibile assegnare ciascuna delle linee di base di configurazione a una raccolta di computer in Configuration Manager.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>Importare i file con estensione cab conformi a Impostazioni di compatibilità in Configuration Manager

1. Aprire la **console di Configuration Manager**.
2. Nel riquadro di spostamento della **console di Configuration Manager passare ad **Asset e conformità**> **Impostazioni di conformità** > **Linee di base di configurazione**.

3. Nel riquadro Azioni fare clic su **Importa dati di configurazione** per avviare l'Importazione guidata dei dati di configurazione.

1. Completare l'**Importazione guidata dei dati di configurazione** usando le informazioni nella tabella seguente e accettando i valori predefiniti se non diversamente specificato.



Processo dell'Importazione guidata dei dati di configurazione

| Nome della pagina della procedura guidata | Azione utente |
| --- | --- |
| **Scegliere i file** |1. Fare clic su **Aggiungi**. </br>Viene visualizzata la finestra di dialogo Apri.|
||2. Nella finestra di dialogo **Apri** passare alla cartella **&lt;compliant cab output\_folder&gt;**. Fare clic sul file con estensione cab **&lt;compliant\_cab&gt;**, dove _compliant cab **output\_folder** è la cartella specificata dopo l'opzione -output quando è stato eseguito lo strumento Sces.ScapToDcm.exe. **compliant\_file** è il nome di un file con estensione cab creato in precedenza durante il processo. Quindi, fare clic su **Apri**. </br> Viene visualizzata la finestra di dialogo Console di Configuration Manager – Avviso di protezione.|
||3. Nella finestra di dialogo **Console di Configuration Manager - Avviso di protezione** fare clic su **Esegui**. Nella pagina Scegli file, i dati di configurazione vengono visualizzati nell'elenco delle linee di base per l'importazione.|
||3. Fare clic su **Avanti**.|
| **Riepilogo** |5. Fare clic su **Avanti**. |
| **Completamento dell'Importazione guidata dei dati di configurazione** |6. Fare clic su **Chiudi**. |

La nuova linea di base di configurazione viene visualizzata nel riquadro informazioni della Console di Configuration Manager.

>[!IMPORTANT]
> È necessario ripetere questa procedura per ogni file con estensione cab creato in precedenza nel processo. Esiste un file con estensione cab per ogni profilo selezionato nel file XCCDF/XML DataStream scaricato dal sito Web NVD. È possibile elaborare tale file con estensione cab eseguendo lo strumento Microsoft.Sces.ScapToDcm.exe.

La linea di base di configurazione importata è di sola lettura, lo stato corrisponde ad &#39;Abilitata&#39; e il valore iniziale di Distribuito corrisponde a &#39;No&#39;.  La proprietà &#39;Data di modifica&#39; indica l'ora di importazione della linea di base.  Il nome della linea di base di configurazione è tratto dalla sezione del nome visualizzato del file XCCDF/XML DataStream e viene costruito tramite la convenzione seguente:

ABC[XYZ], dove ABC è l'ID benchmark XCCDF e XYZ è l'ID profilo XCCDF (se è selezionato un profilo).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Assegnare linee di base di configurazione alle raccolte di computer

Dopo aver creato le raccolte di computer appropriate per i computer a cui si vuole accedere per valutare la conformità SCAP, è possibile assegnare le linee di base di configurazione importate per l'associazione alle raccolte di computer. Questa sezione fornisce informazioni per assegnare una linea di base di configurazione a una raccolta di computer utilizzando la Console di Configuration Manager.

Per assegnare una linea di base di configurazione a una raccolta di computer:

1. Aprire la **console** di **Configuration Manager**.

2. Nel riquadro di spostamento della **console di Configuration Manager passare ad **Asset e conformità** > **Impostazioni di conformità** >** Linee di base di configurazione**.
3. Nel riquadro di spostamento fare clic su &lt; **configuration\_baseline >, dove &lt;_configuration\_baseline&gt;_ è il nome della linea di base di configurazione che si vuole assegnare a una raccolta di computer.

    L'elenco di elementi di configurazione per la linea di base di configurazione viene visualizzato nel riquadro delle informazioni di Configuration Manager.

4. Nel riquadro delle azioni fare clic su **Distribuisci**.

5. Completare la finestra di **dialogo** **Linea di base** **configurazione distribuzione** usando le informazioni nella tabella seguente e accettando i valori predefiniti se non diversamente specificato.

### <a name="deploy-configuration-baseline-dialog-process"></a>Processo della finestra di dialogo Linea di base di configurazione

| Nome della pagina della procedura guidata | Azione utente |
| --- | --- |
| **Scegliere una raccolta** | 1. Fare clic su **Sfoglia**.|
||2. Nella finestra di dialogo **Seleziona raccolta** selezionare **Raccolte di dispositivi**, quindi fare clic su  **&lt;computer\_collection&gt;**, dove &lt; _computer\_collection&gt;_  è il nome del raccolta di computer creata in precedenza durante il processo. Fare clic su **OK**.|
| **Impostare la pianificazione** |3. Selezionare la pianificazione appropriata per l'organizzazione.|
 
>[!IMPORTANT]
> Ripetere questo processo per ogni raccolta di computer che si desidera assegnare a ciascuna linea di base di configurazione. Come minimo, assegnare ogni linea di base di configurazione almeno a una raccolta di computer.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Verificare che i dati di conformità siano stati raccolti

Prima di esportare i dati di conformità nuovamente al formato SCAP, è necessario verificare che i dati siano stati raccolti. Dopo aver assegnato una linea di base di configurazione a una raccolta di computer, il client di Configuration Manager in ogni computer nella raccolta raccoglie automaticamente le informazioni sulla conformità. Le informazioni sulla conformità vengono quindi archiviate sul client nel database di Configuration Manager.

Lo stato della distribuzione della linea di base di configurazione viene visualizzato in Configuration Manager per garantire che i dati appropriati siano stati raccolti dal client di Configuration Manager. È importante verificare che i dati di conformità appropriati siano stati raccolti in Configuration Manager, perché ciò consente di convalidare i file di risultati XCCDF/DataStream creati in un secondo momento nel processo.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Verificare che i dati di conformità siano stati raccolti

1. Aprire la console di Configuration Manager.
2. Nel riquadro di spostamento della Console di Configuration Manager passare a **Monitoraggio** > **Distribuzioni**.
3. Fare clic su **Tipo di funzionalità** per ordinare il tipo di distribuzione e trovare gli elementi di tipo **Linea di base** nell'elenco.
4. Fare clic con il pulsante destro del mouse su &lt;configuration\_baseline&gt; nell'elenco appena distribuito nella raccolta e fare clic su **Visualizza stato**.
5. Passare quindi al nodo &lt;configuration\_baseline&gt; per visualizzare lo stato di conformità. Se un computer ha stato sconosciuto, significa che per tale computer la raccolta dei dati di conformità non è stata ancora completata.

### <a name="validate-the-xccdfdatastream-results"></a>Convalidare i risultati XCCDF/DataStream

1. Aprire la console di Configuration Manager.
2. Nel riquadro di spostamento della console di Configuration Manager passare a **Impostazioni di conformità** > **SCAP Dashboard** (Dashboard SCAP).
3. Selezionare linea di base di configurazione, assegnazione, file SCAP, flusso dei dati, benchmark e profilo (se applicabile).
4. Fare clic su **Mostra report**
 ![Report SCAP](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>Esportare i risultati di conformità in formato SCAP

L'attività successiva del processo consiste nell'esportazione dei dati di conformità di Impostazioni di conformità in formato SCAP, ovvero in un file ARFreport in formato XML/leggibile. L'Esportazione guidata estensioni SCAP e lo strumento Microsoft.Sces.DcmToScap.exe esportano un file di risultati XCCDF/ARF DataStream per ogni linea di base di configurazione di Impostazioni di conformità. Questi file corrispondono ognuno a uno dei file di input XCCDF/DataStream usato dallo strumento Microsoft.Sces.ScapToDcm.exe per creare ogni linea di base di configurazione di Impostazioni di conformità.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Esportare i dati di conformità di impostazioni di conformità usando l'Esportazione guidata report SCAP

1. Avviare l'Esportazione guidata report SCAP dal menu visualizzato facendo clic con il pulsante destro del mouse nel dashboard SCAP.
![Importare dal dashboard SCAP](./media/import-from-scap-dashboard.png)

2. Selezionare la linea di base di configurazione e l'assegnazione ![Selezionare la linea di base](./media/select-ci-baseline.png)

3. Scegliere la posizione per il file di flusso dei dati SCAP, per il file XCCDF/CPE o per i file di contenuto e delle variabili Oval.
![Scegliere il flusso dei dati](./media/export-scap-report-datastream.png)

4. Specificare il nome dell'organizzazione e scegliere la cartella in cui esportare il report SCAP.
 ![Scegliere il flusso dei dati](./media/specify-org-export.png)

5. Confermare le impostazioni.
 ![Scegliere il flusso dei dati](./media/confirm-export.png)

6. Scegliere **Avanti per esportare il report.  Verrà visualizzato un indicatore di stato e quindi una pagina di completamento.
 ![Completare l'esportazione](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Metodo alternativo) Esportare i dati di conformità di Impostazioni di conformità tramite lo strumento Microsoft.Sces.DcmToScap.exe

1. Al prompt dei comandi passare alla cartella AdminConsole\Bin, digitare i parametri della riga di comando elencati nella tabella seguente e quindi premere **INVIO:

    >[!NOTE] 
    >L'account deve avere autorizzazioni di lettura per il provider di Configuration Manager e autorizzazioni di scrittura per la cartella di output specificata nel parametro -out della riga di comando.

**Per contenuto SCAP 1.0/1.1 (ad esempio contenuto USGCB e DISA):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -select &lt;xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt; [-log logFileName]

  >[!NOTE] 
    >È consigliabile usare il parametro -select per specificare il benchmark/profilo valutato nei client in presenza di più benchmark/profili nel contenuto.

**Per contenuto SCAP 1.2 (ad esempio, il contenuto USGCB più recente):**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt; [-log logFileName]

   >[!NOTE] 
   >È consigliabile usare il parametro -select per specificare il flusso dei dati/benchmark/profilo valutato nei client in presenza di più flussi dei dati/benchmark/profili nel contenuto.

**Per un singolo file OVAL con variabili esterne:**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputResultFolder&gt; [-log logFileName]

   >[!NOTE] 
    >Microsoft.Sces.DcmToScap.exe genererà solo il report dei risultati di definizione OVAL per ogni computer di destinazione, il report ARF non verrà generato.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Come ottenere l'ID integrazione continua della linea di base e l'ID assegnazione

In Admin Console passare ad **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**. L'ID integrazione continua è l'ID integrazione continua della linea di base di configurazione.

![Ottenere l'ID integrazione continua e l'ID assegnazione](./media/get-to-baselines.png)

Selezionare la linea di base di configurazione desiderata e fare clic sulla scheda Distribuzioni. se l'ID assegnazione non è visualizzato, fare clic con il pulsante destro del mouse sull'intestazione di colonna e fare clic sull'ID assegnazione per abilitarlo.
![Ottenere l'ID integrazione continua e l'ID assegnazione](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parametri della riga di comando dello strumento Microsoft.Sces.DcmToScap.exe

| **Parametro** | **Utilizzo** | **Richiesto** |
| --- | --- | --- |
| -baseline [Baseline CI ID] | Specificare la linea di base di configurazione | Sì |
| -assignment [Assignment ID] | Specificare la distribuzione della linea di base di configurazione | Sì |
| -organization [organization name] | Specificare il nome dell'organizzazione, che verrà visualizzato nel report. Può essere separato da &#39;;&#39; per specificare un nome di organizzazione su più righe. | No |
| -type [thin/full/fullnosc] | Specificare il tipo di risultato OVAL: risultato thin, risultato completo o risultato completo senza caratteristica del sistema. | No (se non specificato, il valore predefinito è completo) |
| -scap [scap data stream file] | Specificare il file di flusso di dati SCAP | Sì (per il flusso dei dati SCAP 1.2, si escludono a vicenda con -xccdf e -oval / -variable) |
| -xccdf [xccdf file] | Specificare il file XCCDF | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| -cpe [cpe file] | Specificare il file CPE | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| -oval [oval file] | Specificare il file OVAL | Sì (per il file OVAL autonomo, si escludono a vicenda con -xccdf e -scap) |
| -variable [oval external variable file] | Specificare il file di variabili esterne OVAL | No (facoltativo per il file OVAL autonomo quando esiste un file di variabili esterne OVAL, si escludono a vicenda con -xccdf e -scap) |
| -select [xccdf benchmark/profile] | Selezionare il benchmark o il profilo XCCDF dal file di flusso dei dati SCAP o XCCDF | Sì (è necessario eseguire una selezione per generare un report in modo da associare la linea di base DCM corrispondente nel database di Configuration Manager) |
| -out [output directory] | Specificare dove eseguire l'output del file con estensione cab di Impostazioni di conformità | No (se non specificato, nello strumento viene elencato solo il contenuto, senza conversione) |
| -log [log file] | Specificare il file di log | No (se non specificato, il log viene scritto nel file Microsoft.Sces.DcmToScap.log) |
| -help / -? | Utilizzo dello strumento di stampa | No |



 >[!TIP] 
 >È possibile specificare il parametro -? Parametro -h o -help per visualizzare la sintassi dello strumento Microsoft.Sces.DcmToScap.exe e un elenco di parametri.

Per impostazione predefinita, lo strumento Microsoft.Sces.DcmToScap.exe accede al database di Configuration Manager usando le credenziali dell'utente. Lo strumento Microsoft.Sces.DcmToScap.exe richiede minimo l'autorizzazione di accesso in lettura al database di Configuration Manager.

Dopo aver verificato l'esistenza del report **ARF** appropriato: _ARF\_xxxx.xml_ e/o **del report** leggibile: xxx.txt, **del report**Cyberscope: LASR\_xxx.xml, **del report** ConsumedOval: xx-oval-&lt;nomeComputer&gt;.xml, del report dei **risultati del benchmark XCCDF**: xccdf\_xxx.xml, alla riga di comando digitare exit e quindi premere **INVIO** per uscire dal prompt dei comandi.

## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Risoluzione dei problemi](/sccm/compliance/plan-design/scap/troubleshooting-scap)
