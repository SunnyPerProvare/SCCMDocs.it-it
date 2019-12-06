---
title: Distribuire e monitorare la conformità SCAP
titleSuffix: Configuration Manager
description: Distribuire le impostazioni di conformità SCAP come linee di base di configurazione, monitorare la conformità ed esportare i risultati.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3280edbe900e96cf97af8e59578ceab5322ee2a
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62204961"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Distribuire e monitorare la conformità SCAP in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver [convertito e importato](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) i file di flusso dei dati SCAP, vedere i passaggi successivi seguenti:  

- [Distribuire](#bkmk_deploy) le linee di base di configurazione alle raccolte per valutare la conformità SCAP dei dispositivi  

- [Monitorare](#bkmk_monitor) i dati di conformità restituiti dai client di destinazione  

- [Esportare](#bkmk_export) i risultati di conformità in formato SCAP  



## <a name="bkmk_deploy"></a> Distribuire le linee di base di configurazione SCAP

Creare prima di tutto le raccolte di dispositivi per i computer di cui si vuole valutare la conformità SCAP. Per altre informazioni, vedere [Creare raccolte](/sccm/core/clients/manage/collections/create-collections).  

Ora è tutto pronto per distribuire le linee di base di configurazione importate in queste raccolte di dispositivi. Per altre informazioni, vedere [Come distribuire linee di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Ripetere questo processo per ogni linea di base di configurazione che si vuole distribuire in ogni raccolta di dispositivi. Come minimo, distribuire ogni linea di base di configurazione almeno a una raccolta di dispositivi.



## <a name="bkmk_monitor"></a> Monitorare i dati di conformità SCAP 

Prima di esportare i dati di conformità nuovamente al formato SCAP, è necessario verificare che il sito abbia raccolto i dati. Dopo aver distribuito una linea di base di configurazione a una raccolta di dispositivi, il client di Configuration Manager in ogni computer nella raccolta raccoglie automaticamente le informazioni sulla conformità. Le informazioni sulla conformità vengono quindi archiviate sul client nel database di Configuration Manager.

Visualizzare lo stato della distribuzione della linea di base di configurazione in Configuration Manager per garantire che i dati appropriati siano stati raccolti dal client di Configuration Manager. È importante verificare che i dati di conformità appropriati siano stati raccolti in Configuration Manager, perché ciò consente di convalidare i file di risultati XCCDF/DataStream creati in un secondo momento nel processo.

Per altre informazioni, vedere [Monitorare le impostazioni di conformità](/sccm/compliance/deploy-use/monitor-compliance-settings).


### <a name="validate-the-xccdfdatastream-results"></a>Convalidare i risultati XCCDF/DataStream

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare il **dashboard SCAP**.  

2. Selezionare linea di base di configurazione, l'assegnazione, il file SCAP, il flusso dei dati, il benchmark e il profilo (se applicabile).  

3. Fare clic su **Show Report** (Visualizza report)
 ![Report SCAP di esempio](./media/scap-report.png)



## <a name="bkmk_export"></a> Esportare i risultati di conformità in formato SCAP

Il passaggio successivo del processo consiste nell'esportare i dati di conformità nel formato SCAP, ovvero un file di report ARF in formato XML/leggibile. L'Esportazione guidata estensioni SCAP e lo strumento da riga di comando Microsoft.Sces.DcmToScap.exe esportano un file di risultati XCCDF/DataStreamARF per ogni linea di base di configurazione. Questi file corrispondono ognuno a uno dei file di input XCCDF/DataStream usato dallo strumento Microsoft.Sces.ScapToDcm.exe per creare ogni linea di base di configurazione.


### <a name="manually-export-with-the-console-wizard"></a>Esportazione manuale con la procedura guidata della console

> [!Note]  
> Questa sezione descrive il processo manuale di esportazione dei risultati di conformità con la console di Configuration Manager. Per automatizzare questo processo, vedere la sezione successiva [Esportazione automatica con lo strumento da riga di comando](#bkmk_auto-export).  


1. Avviare l'**Esportazione guidata report SCAP** facendo clic con il pulsante destro del mouse sul nodo **SCAP Dashboard** (Dashboard SCAP).  
![Avviare l'Esportazione guidata report SCAP dal dashboard SCAP](./media/import-from-scap-dashboard.png)

2. Selezionare la linea di base di configurazione, l'assegnazione e il tipo di contenuto SCAP.  
![Selezionare la linea di base](./media/select-ci-baseline.png)

3. Scegliere la posizione per il file di flusso dei dati SCAP, per il file XCCDF/CPE o per i file di contenuto e delle variabili Oval.  
![Scegliere il flusso dei dati](./media/export-scap-report-datastream.png)

4. Specificare il nome dell'organizzazione e scegliere la cartella in cui esportare il report SCAP.  
 ![Scegliere il flusso dei dati](./media/specify-org-export.png)
   > [!Tip]  
   > Questa pagina della procedura guidata visualizza la riga di comando che si usa con lo strumento **DcmToScap.exe** per automatizzare lo stesso processo.  

5. Confermare le impostazioni.  
 ![Scegliere il flusso dei dati](./media/confirm-export.png)

6. Scegliere **Avanti** per esportare il report. Completare la procedura guidata.  
 ![Completare l'esportazione](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> Esportazione automatica con lo strumento da riga di comando

Aprire il prompt dei comandi e andare alla cartella **AdminConsole\Bin** di Configuration Manager. Usare uno degli esempi di riga di comando seguenti:  

> [!NOTE]  
> L'account deve avere le autorizzazioni di lettura per il provider di Configuration Manager. Sono necessarie anche le autorizzazioni di scrittura per la cartella specificata nel parametro `–out` della riga di comando.

**Per contenuto SCAP 1.0/1.1 (ad esempio contenuto USGCB e DISA):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > In presenza di più benchmark/profili nel contenuto, usare il parametro `–select` per specificare il benchmark/profilo valutato dai client.  

**Per contenuto SCAP 1.2 (ad esempio, il contenuto USGCB più recente):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > In presenza di più flussi di dati/benchmark/profili nel contenuto, usare il parametro `–select` per specificare il flusso di dati/benchmark/profilo valutato dai client.  

**Per un singolo file OVAL con variabili esterne:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > Microsoft.Sces.DcmToScap.exe genera solo il report dei risultati di definizione OVAL per ogni computer di destinazione. Il report ARF non viene generato.  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>Come ottenere BaselineCIID e AssignmentID

Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità** e selezionare **Linee di base di configurazione**. `BaselineCIID` è l'identificatore (ID) della linea di base di configurazione.  
![Ottenere l'ID integrazione continua e l'ID assegnazione](./media/get-to-baselines.png)

Selezionare la linea di base di configurazione desiderata e fare clic sulla scheda **Distribuzioni**. `AssignmentID` è l'identificatore (ID) della distribuzione della linea di base di configurazione in una raccolta di dispositivi. Se l'ID assegnazione non viene visualizzato, fare clic con il pulsante destro del mouse sull'intestazione della colonna e scegliere **ID assegnazione**.  
![Ottenere l'ID integrazione continua e l'ID assegnazione](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Parametri della riga di comando dello strumento Microsoft.Sces.DcmToScap.exe

| Parametro | Utilizzo | Richiesto |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Specificare la linea di base di configurazione | Sì |
| `-assignment [Assignment ID]` | Specificare la distribuzione della linea di base di configurazione | Sì |
| `-organization [organization name]` | Specificare il nome dell'organizzazione, che verrà visualizzato nel report. Può essere separato da `;` per specificare un nome di organizzazione su più righe. | No |
| `-type [thin/full/fullnosc]` | Specificare il tipo di risultato OVAL: risultato thin, risultato completo o risultato completo senza caratteristica del sistema. | No (se non specificato, il valore predefinito è completo) |
| `-scap [scap data stream file]` | Specificare il file di flusso di dati SCAP | Sì (per il flusso dei dati SCAP 1.2, si escludono a vicenda con -xccdf e -oval / -variable) |
| `-xccdf [xccdf file]` | Specificare il file XCCDF | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| `-cpe [cpe file]` | Specificare il file CPE | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| `-oval [oval file]` | Specificare il file OVAL | Sì (per il file OVAL autonomo, si escludono a vicenda con -xccdf e -scap) |
| `-variable [oval external variable file]` | Specificare il file di variabili esterne OVAL | No (facoltativo per il file OVAL autonomo quando esiste un file di variabili esterne OVAL, si escludono a vicenda con -xccdf e -scap) |
| `-select [xccdf benchmark/profile]` | Selezionare il benchmark o il profilo XCCDF dal file di flusso dei dati SCAP o XCCDF | Sì (è necessario eseguire una selezione per generare un report in modo da associare la linea di base DCM corrispondente nel database di Configuration Manager) |
| `-out [output directory]` | Specificare dove eseguire l'output del file con estensione cab di Impostazioni di conformità | No (se non specificato, nello strumento viene elencato solo il contenuto, senza conversione) |
| `-log [log file]` | Specificare il file di log | No (se non specificato, il log viene scritto nel file Microsoft.Sces.DcmToScap.log) |
| `-help` o `-?` | Utilizzo dello strumento di stampa | No |

 > [!TIP]  
 > È possibile specificare il parametro `-?`, `–h` o `–help` per visualizzare la sintassi dello strumento Microsoft.Sces.DcmToScap.exe e un elenco di parametri.

Per impostazione predefinita, lo strumento Microsoft.Sces.DcmToScap.exe accede al database di Configuration Manager usando le credenziali dell'utente. Lo strumento Microsoft.Sces.DcmToScap.exe richiede minimo l'autorizzazione di accesso in lettura al database di Configuration Manager.

Dopo aver eseguito lo strumento, verificare che esistano i file seguenti: 
- Report **ARF**: `_ARF_xxxx.xml_` e/o report **in formato leggibile**: `xxx.txt`
- Report **Cyberscope**: `LASR_xxx.xml`
- Report **ConsumedOval**: `xx-oval-<machineName>.xml`
- Report dei **risultati XCCDF Benchmark**: `xccdf_xxx.xml` 



## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Risoluzione dei problemi](/sccm/compliance/plan-design/scap/troubleshooting-scap)
