---
title: Installare e configurare le estensioni SCAP
titleSuffix: Configuration Manager
description: Installare e configurare le estensioni SCAP (Security Content Automation Protocol) per Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c36f2380a93d6da27651f1aa3a4894e25b3bce39
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70890714"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Installare e configurare le estensioni SCAP per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver [preparato l'infrastruttura](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare), è possibile installare e configurare le estensioni SCAP per Configuration Manager nel computer dal quale si vuole eseguire questo processo.



## <a name="bkmk_install"></a> Installare le estensioni SCAP

Il file di installazione è disponibile nel percorso seguente della directory di installazione nel server del sito di Configuration Manager:  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. Copiare **ConfigMgrExtensionsforSCAP.msi** nel computer contenente la console di Configuration Manager in cui si vuole eseguire il processo.  

2. In Esplora risorse passare alla cartella in cui è stato copiato il file **ConfigMgrExtensionsforSCAP.msi**. Fare doppio clic sul file per aprirlo e avviare le estensioni SCAP per l'Installazione guidata di Configuration Manager.  

3. Esaminare il contratto di licenza. Fare clic su **Accetto i termini del contratto di licenza** e quindi fare clic su **Installa**.  

4. Al termine dell'installazione, fare clic su **Fine** per chiudere l'installazione guidata.  

L'installazione guidata installa le estensioni SCAP nella cartella di installazione della console di Configuration Manager. Per impostazione predefinita, la cartella di installazione della console è `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`.  



## <a name="bkmk_scap-data-stream-files"></a> Scaricare e installare i file di flusso dei dati SCAP

Prima di poter eseguire le estensioni SCAP, è necessario scaricare i file di flusso dei dati SCAP dalla [pagina di download](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline) di National Vulnerability Database (NVD) e quindi copiarli nella cartella in cui sono state installate le estensioni SCAP.

A seconda dell’ambiente, potrebbero non essere necessario tutti fi file di flusso dati SCAP elencati nella pagina di download.

### <a name="install-the-scap-data-streams"></a>Installare i flussi dei dati SCAP

1. Visitare il [sito Web NVD](https://nvd.nist.gov/) per identificare i flussi di dati SCAP richiesti dall'organizzazione.
I flussi dei dati SCAP pubblicati da NIST sono organizzati in più bundle, detti anche _elenchi di controllo_.  

2. Scaricare i flussi dei dati SCAP dal [sito Web NVD](https://nvd.nist.gov/home.cfm). I flussi sono archiviati in file compressi con estensione zip o sono contrassegnati come file XML DataStream.  

    > [!IMPORTANT]  
    > Esistono molti file di flusso dati SCAP con estensione xml che è possibile scaricare dal NVD. Tuttavia, solo i file con estensione xml che includono contenuto XCCDF (SCAP 1.0 e 1.1)/DataStream (SCAP 1.2) sono appropriati per l'uso con le estensioni SCAP.  

3. Estrarre i file ZIP dei flussi di dati SCAP o il file XML DataStream scaricato nella stessa cartella in cui sono state installate le estensioni SCAP.  



## <a name="bkmk_convert-and-import"></a> Convertire e importare manualmente i file di flusso dei dati SCAP 

Dopo aver ottenuto i flussi dei dati SCAP, è possibile importare e convertire i flussi dei dati in linee di base di configurazione. I flussi di dati SCAP pubblicati da NIST sono organizzati in più bundle. Seguire le istruzioni di NIST per verificare quali bundle utilizzare nell'ambiente in uso. Ad esempio, esiste un bundle separato per ogni versione di Windows, un altro bundle specifico della versione per la configurazione del firewall e un bundle per Internet Explorer. Utilizzare le seguenti procedure per realizzare questa attività.  

> [!Note]  
> Questa sezione descrive il processo manuale per convertire e importare i file di flusso dei dati con la console di Configuration Manager. Per automatizzare questo processo, vedere la sezione successiva [Convertire e importare automaticamente i file di flusso dei dati SCAP](#bkmk_auto-convert-and-import).  

1. Fare clic sulla procedura guidata **Import SCAP Content** (Importa contenuto SCAP) dalla barra multifunzione della linea di base di configurazione.

     ![Pulsante Import SCAP Content (Importa contenuto SCAP) nella barra multifunzione della console](./media/import-scap-content.png)

2. Selezionare l'opzione SCAP content (Contenuto SCAP).

      ![Selezionare la pagina dell'opzione del contenuto SCAP dell'importazione guidata](./media/import-new-scap-content.png)

3. Selezionare il file di flusso dei dati SCAP, XCCDF e il file del dizionario CPE o il file di contenuto Oval.

     ![Selezionare il file di flusso dei dati SCAP](./media/select-datastream-file.png)

4. Con SCAP 1.2 selezionare il flusso dei dati. Selezionare quindi il profilo e il benchmark per SCAP 1.x. Selezionare **Avanti** per convertire il contenuto. 

      ![Selezionare il profilo e il benchmark per SCAP 1.2](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > Questa pagina della procedura guidata visualizza la riga di comando che si usa con lo strumento **ScapToDcm.exe** per automatizzare lo stesso processo.  

5. Confermare i dati di configurazione da importare.

      ![Confermare lo screenshot di configurazione](./media/confirm-configuration.png)

6. Fare clic su**Avanti** per importare i dati di configurazione.

      ![Completare l'importazione](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> Convertire e importare automaticamente i file di flusso dei dati SCAP 

### <a name="import-with-the-command-line-tool"></a>Importare con lo strumento da riga di comando

Dopo aver ottenuto i flussi dei dati SCAP, è possibile usare lo strumento **Microsoft.Sces.ScapToDcm.exe** per convertirli in file con estensione cab conformi alle impostazioni di conformità. Importare quindi i file con estensione cab in Configuration Manager. Lo strumento Microsoft.Sces.ScapToDcm.exe converte i flussi dei dati SCAP in elementi di configurazione e linee di base di configurazione che è possibile usare in Configuration Manager. Lo strumento Microsoft.Sces.ScapToDcm.exe converte i flussi dei dati SCAP in manifesti XML. Con questi ultimi crea quindi un pacchetto in un file con estensione cab che è possibile importare in Configuration Manager.

> [!Tip]  
> Il passaggio 4 del processo manuale nella sezione precedente mostra la pagina della procedura guidata che visualizza la riga di comando da usare con lo strumento **ScapToDcm.exe** per automatizzare lo stesso processo.  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Usare lo strumento Microsoft.Sces.ScapToDcm.exe per convertire i flussi dei dati SCAP in file CAB

Al prompt dei comandi passare alla cartella **AdminConsole\Bin** ed eseguire **Microsoft.Sces.ScapToDcm.exe**. Questo strumento genera un file CAB conforme alle impostazioni di conformità e lo importa nel sito di Configuration Manager.

   > [!NOTE]  
   > L'account deve avere autorizzazioni di lettura/scrittura per la cartella di output.

**Sintassi per IL contenuto SCAP 1.0/1.1 (file XML XCCDF, ad esempio contenuto USGCB e DISA):**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se non si specifica il benchmark/profilo mediante il parametro `–select`, lo strumento genererà un file con estensione CAB per ogni benchmark nel file di contenuto.  

**Sintassi per il contenuto SCAP 1.2 (file XML DataStream, ad esempio contenuto USGCB più recente):**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Se non si specifica il flusso dei dati/benchmark/profilo mediante il parametro `–select`, lo strumento genererà un file con estensione CAB per ogni benchmark nel file di contenuto.

**Sintassi per un singolo file OVAL con variabili esterne:**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > Se nel file delle variabili esterne sono presenti più valori per una variabile, lo strumento Microsoft.Sces.ScapToDcm.exe considererà i valori come una matrice di questa variabile.  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Parametri della riga di comando dello strumento Microsoft.Sces.ScapToDcm.exe

| Parametro | Utilizzo | Richiesto |
| --- | --- | --- |
| `-scap [scap data stream file]` | Specificare il file di flusso di dati SCAP | Sì (per il flusso dei dati SCAP 1.2, si escludono a vicenda con -xccdf e -oval / -variable) |
| `-xccdf [xccdf file]` | Specificare il file XCCDF | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| `-cpe [cpe file]` | Specificare il file CPE | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| `-oval [oval file]` | Specificare il file OVAL | Sì (per il file OVAL autonomo, si escludono a vicenda con -xccdf e -scap) |
| `-variable [oval external variable file]` | Specificare il file di variabili esterne OVAL | No (facoltativo per il file OVAL autonomo quando esiste un file di variabili esterne OVAL, si escludono a vicenda con -xccdf e -scap) |
| `-select [xccdf benchmark/profile]` | Selezionare il benchmark o il profilo XCCDF dal file di flusso dei dati SCAP o XCCDF | No (questo paramento non è obbligatorio, ma è consigliato. Se non specificato, lo strumento genererà un file con estensione cab per tutti i profili in tutti i flussi dei dati/benchmark incorporati) |
| `-out [output directory]` | Specificare dove eseguire l'output del file cab DCM | No (se non specificato, nello strumento verrà elencato solo il contenuto, senza conversione) |
| `-log [log file]` | Specificare il file di log | No (se non specificato, il log verrà scritto nel file Microsoft.Sces.ScapToDcm.log) |
| `-help` o `-?` | Utilizzo dello strumento di stampa | No |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Esempi dello strumento Microsoft.Sces.ScapToDcm.exe

**Contenuto SCAP 1.2:**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**Contenuto SCAP 1.0/1.1:**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**Contenuto SCAP OVAL:**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Output di esempio dello strumento Microsoft.Sces.ScapToDcm.exe

``` Output
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>Importare il file CAB

Il passaggio successivo del processo consiste nell'utilizzare la console di Configuration Manager per importare i file con estensione cab conformi alle impostazioni di conformità in Configuration Manager. Quando si importano i file con estensione cab creati in precedenza in questo processo, uno o più elementi di configurazione e linee di base di configurazione vengono creati nel database di Configuration Manager. Più avanti nella procedura sarà possibile distribuire le linee di base di configurazione alle raccolte di dispositivi. Per altre informazioni, vedere [Importare i dati di configurazione](/sccm/compliance/deploy-use/import-configuration-data).

Il percorso del file CAB creato in precedenza è costituito dalla cartella specificata dal parametro `–output` dello strumento Microsoft.Sces.ScapToDcm.exe.

> [!IMPORTANT]  
> Ripetere questa procedura per ogni file CAB creato in precedenza nel processo. È presente un file CAB per ogni profilo selezionato nel file XCCDF/XML DataStream scaricato dal sito Web NVD. Per elaborare questi file, eseguire lo strumento Microsoft.Sces.ScapToDcm.exe.  

La linea di base di configurazione importata è di sola lettura, è *Abilitata* e lo stato della distribuzione è impostato su *No*. La proprietà **Data modifica** indica l'ora di importazione della linea di base. Il nome della linea di base di configurazione deriva dalla sezione del nome visualizzato del file XCCDF/XML Datastream. Il nome viene creato tramite la convenzione `ABC[XYZ]`, dove **ABC** è l'ID benchmark XCCDF e **XYZ** è l'ID profilo XCCDF (se è selezionato un profilo).



## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Distribuire e monitorare la conformità SCAP ed esportare i risultati di conformità](/sccm/compliance/plan-design/scap/deploy-monitor-export)
