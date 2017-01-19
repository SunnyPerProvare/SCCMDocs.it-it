---
title: Visualizzare dati di diagnostica | Microsoft Docs
description: "È possibile visualizzare i dati di diagnostica e di utilizzo per verificare che la gerarchia di System Center Configuration Manager non contenga informazioni riservate."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 5b5d6b6c176de8acbc1161f6820aa1cc3e9fca49


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Come visualizzare dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile visualizzare i dati di diagnostica e di utilizzo della gerarchia di System Center Configuration Manager per verificare che non siano incluse informazioni sensibili o personali. I dati di telemetria vengono riepilogati e archiviati nella tabella **TEL_TelemetryResults** del database del sito e sono formattati per essere utilizzabili ed efficienti a livello di programmazione. Anche se le opzioni seguenti offrono una visualizzazione dei dati esatti inviati a Microsoft, non sono progettate per l'uso per altri scopi, ad esempio per analisi dei dati.  

Il comando SQL seguente può essere usato per visualizzare il contenuto di questa tabella e mostra i dati esatti inviati (è anche possibile esportare questi dati in un file di testo):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Prima di installare la versione 1602, la tabella che archivia i dati di telemetria è **TelemetryResults**.  

Quando il punto di connessione del servizio è in modalità offline, è possibile usare lo strumento di connessione del servizio per esportare i dati di diagnostica e di utilizzo correnti in un file con valori delimitati da virgole (CSV). Eseguire lo strumento di connessione del servizio per il punto di connessione del servizio con il parametro **-Export**.  

##  <a name="a-namebkmkhashesa-one-way-hashes"></a><a name="bkmk_hashes"></a> Hash unidirezionali  
Alcuni dei dati sono costituiti da stringhe di caratteri alfanumerici casuali. Configuration Manager usa hash unidirezionali con l'algoritmo SHA-256 per verificare che non vengano raccolti dati potenzialmente sensibili, lasciandoli in uno stato in cui possono essere comunque usati per scopi di correlazione e confronto. Ad esempio, anziché raccogliere i nomi delle tabelle nel database del sito, viene acquisito un hash unidirezionale per ogni nome di tabella. Questo assicura che non siano visibili gli eventuali nomi di tabella personalizzati creati dall'utente o da componenti aggiuntivi del prodotto di terze parti. È quindi possibile procedere allo stesso modo per acquisire l'hash unidirezionale dei nomi delle tabelle SQL incluse per impostazione predefinita nel prodotto ed eseguire un confronto per determinare eventuali deviazioni dello schema del database rispetto a quello predefinito del prodotto. Queste informazioni possono poi essere usate per migliorare gli aggiornamenti che richiedono modifiche allo schema di SQL.  

Quando si visualizzano i dati non elaborati, viene visualizzato un valore hash comune in ogni riga di dati. Si tratta dell'ID gerarchia. Questo valore hash viene usato per assicurarsi che i dati siano correlati alla stessa gerarchia senza identificare il cliente o l'origine.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Per vedere come funziona l'hash unidirezionale  

1.  Ottenere l'ID gerarchia eseguendo l'istruzione SQL seguente in SQL Management Studio nel database di Configuration Manager: **select [dbo].[fnGetHierarchyID](\)**  

2.  Usare lo script di Windows PowerShell seguente per eseguire l'hash unidirezionale del GUID ottenuto dal database. A questo punto, è possibile confrontarlo all'ID gerarchia nei dati non elaborati per vedere come vengono nascosti questi dati.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
         #many of the values we hash are Guids  
         $bytesToHash = $guid.ToByteArray()  
    } else {  
         #otherwise hash as string (unicode)  
         $ue = New-Object System.Text.UnicodeEncoding  
         $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  



<!--HONumber=Dec16_HO3-->


