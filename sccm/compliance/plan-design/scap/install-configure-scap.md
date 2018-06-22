---
title: Installare e configurare estensioni SCAP (Security Content Automation Protocol)
titleSuffix: Configuraton Manager
description: Installare e configurare le estensioni SCAP (Security Content Automation Protocol)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 891d21b44ed6efca73413a46d0483519b76f9cae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336596"
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Installare e configurare le estensioni SCAP per Microsoft System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella Technical Preview versione 1803 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features). Questa versione non definitiva delle estensioni SCAP può essere installata in qualsiasi versione attualmente supportata di Configuration Manager Current Branch e LTSB 1606. A partire dalla Technical Preview 1803, il file di installazione si trova in cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi.   

Dopo aver preparato l'infrastruttura dei prerequisiti, è possibile installare e configurare le estensioni SCAP per Microsoft System Center Configuration Manager nel computer dal quale si vuole eseguire questo processo.

## <a name="install-scap-extensions-configuration-manager"></a>Installare SCAP Extensions Configuration Manager

1. Per installare lo strumento, eseguire ConfigMgr\_Extensions\_for\_SCAP.msi.
2. In Esplora risorse passare alla cartella in cui è stato scaricato il file **ConfigMgr\_Extensions\_for\_SCAP.msi** e quindi fare doppio clic sul file **ConfigMgr\_Extensions\_for\_SCAP.msi**. Verrà avviata l'installazione guidata delle estensioni SCAP per Microsoft System Center Configuration Manager.

Completare l'**Installazione guidata delle estensioni SCAP per Microsoft System Center Configuration Manager** usando le informazioni nella tabella seguente e accettando i valori predefiniti della procedura guidata, a meno che non sia necessario indicare valori specifici.

**Tabella 1.0** Processo di installazione guidata delle estensioni SCAP per Microsoft System Center Configuration Manager

| Nome della pagina della procedura guidata | Azione utente |
| --- | --- |
| Pagina iniziale e contratto di licenza con l'utente finale |1. Esaminare il contratto di licenza|
| Pagina iniziale e contratto di licenza con l'utente finale|2. Fare clic su **Accetto i termini del contratto di licenza**.|
| Pagina iniziale e contratto di licenza con l'utente finale|3. Fare clic su **Installa**.|
| La procedura di installazione guidata di SCAP Extensions for Microsoft System Center Configuration Manager è stata completata |4. Fare clic su **Fine**.|
 



Per impostazione predefinita, l'installazione guidata delle estensioni SCAP per Microsoft System Center Configuration Manager installa le estensioni nella cartella di installazione della console di Configuration Manager.



## <a name="download-and-install-the-scap-data-stream-files"></a>Scaricare e installare i file di flusso dei dati SCAP

Prima di poter eseguire le estensioni SCAP per convertire i file di flusso dei dati SCAP e quindi importarli nella funzionalità Impostazioni di conformità, è necessario scaricare i file di flusso dei dati SCAP dal sito Web della [pagina di download](http://nvd.nist.gov/fdcc/download_fdcc.cfm) del database NVD (National Vulnerability Database) e quindi copiarli nella cartella in cui sono installate le estensioni SCAP

A seconda dell’ambiente, potrebbero non essere necessario tutti fi file di flusso dati SCAP elencati nella pagina di download.

Per installare i flussi dei dati SCAP

1. Visitare il [sito Web NVD](http://nvd.nist.gov/) per identificare i flussi di dati SCAP richiesti dall'organizzazione.
I flussi dei dati SCAP pubblicati da NIST sono organizzati in più bundle, detti anche _elenchi di controllo_.

2. Scaricare i flussi dei dati SCAP dal [sito Web NVD](http://nvd.nist.gov/home.cfm). I flussi sono archiviati in file compressi con estensione zip o sono contrassegnati come file XML DataStream.

    >[!IMPORTANT] 
    >Esistono molti file di flusso dati SCAP con estensione xml che è possibile scaricare dal NVD. Tuttavia, solo i file con estensione xml che includono contenuto XCCDF (SCAP 1.0 e 1.1)/DataStream (SCAP 1.2) sono appropriati per l'uso con le estensioni SCAP.

3. Estrarre i file con estensione zip dei flussi di dati SCAP o il file XML DataStream scaricato nella stessa cartella in cui è stato installato SCAP Extensions.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Convertire e importare i file di flusso dei dati SCAP tramite l'importazione guidata contenuto SCAP

Dopo aver ottenuto i flussi dei dati SCAP, è possibile importare e convertire i flussi dei dati in linee di base di configurazione. I flussi di dati SCAP pubblicati da NIST sono organizzati in più bundle. Seguire le istruzioni di NIST per verificare quali bundle usare nell'ambiente in uso. Ad esempio, esiste un bundle separato per ogni versione di Windows, un altro bundle specifico della versione per la configurazione del firewall e un bundle per Internet Explorer 8.0. Utilizzare le seguenti procedure per realizzare questa attività.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Per importare i flussi di dati SCAP in Configuration Manager

1. Avviare l'Importazione guidata contenuto SCAP dalla barra multifunzione della linea di base di configurazione.

     ![Avviare l'Importazione guidata contenuto SCAP dalla barra multifunzione della linea di base di integrazione continua](./media/import-scap-content.png)

2. Selezionare il tipo di contenuto.

      ![Selezionare il tipo di contenuto](./media/import-new-scap-content.png)

3. Selezionare il file di flusso dei dati SCAP, XCCDF e il file del dizionario CPE o il file di contenuto Oval.

     ![Selezionare il file di flusso dei dati SCAP](./media/select-datastream-file.png)

4. Con SCAP 1.2 selezionare il flusso dei dati. Selezionare quindi il profilo e il benchmark per SCAP 1.x.  Selezionare **Avanti** per convertire il contenuto. Verrà visualizzato un indicatore di stato.

      ![Selezionare il profilo e il benchmark per SCAP 1.2](./media/select-benchmark-and-profile.png)

5. Confermare i dati di configurazione da importare.

      ![Confermare lo screenshot di configurazione](./media/confirm-configuration.png)

6. Fare clic su**Avanti** per importare i dati di configurazione.

      ![Completare l'importazione](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Metodo alternativo) Convertire e importare i file di flusso dei dati SCAP tramite lo strumento da riga di comando

Dopo aver ottenuto i flussi dei dati SCAP, è possibile usare lo strumento Microsoft.Sces.ScapToDcm.exe per convertirli in file con estensione cab conformi a Impostazioni di conformità. Importare quindi i file con estensione cab in Configuration Manager. Lo strumento Microsoft.Sces.ScapToDcm.exe converte i flussi dei dati SCAP in elementi di configurazione e linee di base di configurazione cui è possibile accedere usando la funzionalità Impostazioni di conformità in Configuration Manager. Lo strumento Microsoft.Sces.ScapToDcm.exe converte i flussi dei dati SCAP in manifesti XML. Con questi ultimi crea quindi un pacchetto in un file con estensione cab che è possibile importare in Configuration Manager.

I flussi di dati SCAP pubblicati da NIST sono organizzati in più bundle. Seguire le istruzioni di NIST per verificare quali bundle usare nell'ambiente in uso. Ad esempio, esiste un bundle separato per ogni versione di Windows, un altro bundle specifico della versione per la configurazione del firewall e un bundle per Internet Explorer 8.0. Utilizzare le seguenti procedure per realizzare questa attività.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Per importare i flussi di dati SCAP in Configuration Manager

1. Convertire i flussi di dati SCAP in un file con estensione cab conformi a Impostazioni di conformità.
2. Importare il file con estensione cab in Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Convertire i flussi dei dati SCAP in file con estensione cab conformi a Impostazioni di conformità

Prima di poter analizzare e valutare la conformità dei sistemi, è necessario convertire i flussi di dati SCAP in formato XML in manifesti XML conformi agli elementi di configurazione di Impostazioni di conformità e alle linee di base di configurazione. Lo strumento Microsoft.Sces.ScapToDcm.exe converte i flussi dei dati SCAP in manifesti XML. Con questi ultimi crea quindi un pacchetto in un file con estensione cab che in seguito è possibile importare in Configuration Manager.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Per convertire i flussi dei dati SCAP in file con estensione cab conformi a Impostazioni di conformità tramite lo strumento Microsoft.Sces.ScapToDcm.exe**

Al prompt dei comandi passare alla cartella AdminConsole\Bin, eseguire Microsoft.Sces.ScapToDcm.exe per generare un file con estensione cab conforme a Impostazioni di conformità e importarlo nel sito di Configuration Manager.

   >[!NOTE] 
   > L'account deve avere autorizzazioni di lettura/scrittura per la cartella di output

**Per contenuto SCAP 1.0/1.1 (file XML XCCDF, ad esempio contenuto USGCB e DISA):**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >Se non si specifica il benchmark o il profilo mediante il parametro -select, lo strumento genererà un file con estensione cab DCM per ogni benchmark nel file di contenuto.

**Per contenuto SCAP 1.2 (file XML DataStream, ad esempio contenuto USGCB più recente):**

Microsoft.Sces.ScapToDcm.exe -scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > Se non si specifica il flusso di dati, il benchmark o il profilo tramite il parametro -select, lo strumento genererà un file con estensione cab DCM per ogni benchmark nel file di contenuto.

**Per un singolo file OVAL con variabili esterne:**

Microsoft.Sces.ScapToDcm.exe -oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > Se nel file delle variabili esterne sono presenti più valori per una variabile, lo strumento Microsoft.Sces.ScapToDcm.exe considererà i valori come una matrice di questa variabile.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Parametri della riga di comando

| **Parametro** | **Utilizzo** | **Richiesto** |
| --- | --- | --- |
| -scap [scap data stream file] | Specificare il file di flusso di dati SCAP | Sì (per il flusso dei dati SCAP 1.2, si escludono a vicenda con -xccdf e -oval / -variable) |
| -xccdf [xccdf file] | Specificare il file XCCDF | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| -cpe [cpe file] | Specificare il file CPE | Sì (per SCAP 1.0/1.1 XCCDF, si escludono a vicenda con -scap e -oval / -variable) |
| -oval [oval file] | Specificare il file OVAL | Sì (per il file OVAL autonomo, si escludono a vicenda con -xccdf e -scap) |
| -variable [oval external variable file] | Specificare il file di variabili esterne OVAL | No (facoltativo per il file OVAL autonomo quando esiste un file di variabili esterne OVAL, si escludono a vicenda con -xccdf e -scap) |
| -select [xccdf benchmark/profile] | Selezionare il benchmark o il profilo XCCDF dal file di flusso dei dati SCAP o XCCDF. | No (è consigliabile specificare questa opzione). Se non specificata, lo strumento genererà un file con estensione cab per tutti i profili in tutti i flussi di dati/benchmark incorporati) |
| -out [output directory] | Specificare dove eseguire l'output del file cab DCM | No (se non specificato, nello strumento verrà elencato solo il contenuto, senza conversione) |
| -log [log file] | Specificare il file di log | No (se non specificato, il log verrà scritto nel file Microsoft.Sces.ScapToDcm.log) |
| -help / -? | Utilizzo dello strumento di stampa | No |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>Le righe di comando seguenti sono esempi per lo strumento Microsoft.Sces.ScapToDcm.exe:

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**L'output seguente è un esempio dallo strumento Microsoft.Sces.ScapToDcm.exe:**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Importare le impostazioni di conformità SCAP ed esportare i risultati di conformità](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
