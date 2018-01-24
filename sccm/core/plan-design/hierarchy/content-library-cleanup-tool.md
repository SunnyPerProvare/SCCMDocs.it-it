---
title: Strumento di pulizia della raccolta contenuto
titleSuffix: Configuration Manager
description: "Usare lo strumento di pulizia della raccolta contenuto per rimuovere contenuto orfano non più associato a una distribuzione di System Center Configuration Manager."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 334b79e675ea7804128b0feb9678de4ad06dbc93
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>Strumento di pulizia della raccolta contenuto per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 A partire dalla versione 1702, è possibile usare uno strumento da riga di comando (**ContentLibraryCleanup.exe**) per rimuovere contenuto non più associato a un pacchetto o a un'applicazione da un punto di distribuzione (contenuto orfano). Questo strumento, denominato strumento di pulizia della raccolta contenuto, sostituisce le versioni precedenti di strumenti simili rilasciati per i prodotti Configuration Manager precedenti.  

Lo strumento interessa solo il contenuto presente nel punto di distribuzione che viene specificato quando si esegue lo strumento stesso. Quest'ultimo non può rimuovere contenuto dalla raccolta contenuto nel server del sito.

Lo strumento **ContentLibraryCleanup.exe** è disponibile nella cartella \*%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* nel server del sito in un sito di amministrazione centrale o in un sito primario.

## <a name="requirements"></a>requisiti  
 Lo strumento può essere eseguito solo in un singolo punto di distribuzione alla volta.  
 - È possibile eseguire lo strumento direttamente nel computer che ospita il punto di distribuzione da pulire oppure in remoto da un altro server.
 - L'account utente che esegue lo strumento deve disporre di autorizzazioni di amministrazione dirette basate sui ruoli equivalenti a quelle di amministratore completo nella gerarchia di Configuration Manager. Lo strumento non funziona se all'account sono state concesse queste autorizzazioni in quanto membro di un gruppo di sicurezza di Windows con autorizzazioni di amministratore completo.

## <a name="modes-of-operation"></a>Modalità di funzionamento
È possibile eseguire lo strumento nelle due modalità seguenti. È consigliabile eseguire lo strumento in modalità *di simulazione*, in modo che sia possibile esaminare i risultati prima di eseguirlo in *modalità di eliminazione*:
  1.    **Modalità di simulazione**:   
      Se non si specifica l'opzione **/delete**, lo strumento viene eseguito in modalità di simulazione e identifica il contenuto da eliminare dal punto di distribuzione.
   - Quando viene eseguito in questa modalità, lo strumento non elimina alcun dato.
   - Le informazioni sul contenuto da eliminare vengono scritte nel file di log dello strumento e non viene chiesto di confermare ogni potenziale eliminazione.  
      </br>   

  2. **Modalità di eliminazione**:   
    Se si attiva l'opzione **/delete**, lo strumento viene eseguito in modalità di eliminazione.

     - Se si esegue lo strumento in questa modalità, il contenuto orfano rilevato nel punto di distribuzione specificato può essere eliminato dalla raccolta contenuto del punto di distribuzione stesso.
     -  Prima di eliminare ciascun file, è necessario confermare l'operazione.  È possibile selezionare **S** per Sì, **N** per No o **Sì a tutti** per ignorare le altre richieste di conferma ed eliminare tutto il contenuto orfano.  
     </br>

Quando si esegue lo strumento, indipendentemente dalla modalità, viene creato automaticamente un log il cui nome è composto dalla modalità in cui viene eseguito lo strumento, dal nome del punto di distribuzione e dalla data e dall'ora dell'operazione. Il file di log si apre automaticamente al termine dell'esecuzione dello strumento.

Per impostazione predefinita, il file di log viene scritto nella cartella temp dell'account utente che esegue lo strumento, sul computer in cui quest'ultimo viene eseguito. È tuttavia possibile usare l'opzione **/log** per reindirizzare il file di log a un'altra posizione, compresa una condivisione di rete.


## <a name="run-the-tool"></a>Eseguire lo strumento
Per eseguire lo strumento:
1. Aprire un prompt dei comandi amministrativo in una cartella contenente **ContentLibraryCleanup.exe**.  
2. Immettere quindi una riga di comando che includa le opzioni della riga di comando obbligatorie e le opzioni facoltative che si vogliono usare.

**Problema noto** Quando si esegue lo strumento, se un pacchetto o una distribuzione ha esito negativo o è in corso, è possibile che venga restituito un errore simile al seguente:
-  *System.InvalidOperationException: non è possibile eseguire la pulizia della raccolta contenuto perché il pacchetto <packageID> non è installato completamente*.

**Soluzione temporanea:** Nessuna. Lo strumento non è in grado di identificare in modo affidabile i file orfani quando il contenuto è in corso o la sua distribuzione ha avuto esito negativo. Di conseguenza, lo strumento non consente di eseguire la pulizia del contenuto fino a quando il problema non viene risolto.

### <a name="command-line-switches"></a>Opzioni della riga di comando  
È possibile usare le opzioni della riga di comando seguenti in qualsiasi ordine.   

|Opzione|Dettagli|
|---------|-------|
|**/delete**  |**Facoltativa** </br> Usare questa opzione se si desidera eliminare contenuto dal punto di distribuzione. Prima dell'eliminazione viene richiesta la conferma. </br></br> Se questa opzione non viene usata, lo strumento registra i risultati relativi al contenuto da eliminare, ma non elimina contenuto dal punto di distribuzione. </br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Facoltativa** </br> Questa opzione consente di eseguire lo strumento in modalità non interattiva. Tutte le richieste di conferma, ad esempio in caso di eliminazione di contenuto, vengono soppresse e il file di log non viene aperto automaticamente. </br></br> Esempio: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN punto di distribuzione>**  | **Richiesto** </br> Specificare il nome di dominio completo (FQDN) del punto di distribuzione che si desidera pulire. </br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN sito primario>**       | **Facoltativa** per la pulizia del contenuto di un punto di distribuzione in un sito primario.</br>**Obbligatoria** per la pulizia del contenuto di un punto di distribuzione in un sito secondario. </br></br>Lo strumento si connette al sito primario padre per eseguire query su SMS_Provider. Queste query consentono allo strumento di determinare il tipo di contenuto che deve essere disponibile nel punto di distribuzione, in modo da poter identificare il contenuto isolato e che può essere rimosso. La connessione al sito primario padre deve essere eseguita per i punti di distribuzione in un sito secondario, perché i dettagli necessari non sono disponibili direttamente dal sito secondario.</br></br> Specificare il nome FQDN del sito primario a cui appartiene il punto di distribuzione oppure il nome del padre primario se il punto di distribuzione si trova in un sito secondario. </br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;codice del sito primario>**  | **Facoltativa** per la pulizia del contenuto di un punto di distribuzione in un sito primario.</br>**Obbligatoria** per la pulizia del contenuto di un punto di distribuzione in un sito secondario. </br></br> Specificare il codice del sito primario a cui appartiene il punto di distribuzione o del sito primario padre se il punto di distribuzione si trova in un sito secondario.</br></br> Esempio: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Facoltativa** </br> Specificare il percorso in cui lo strumento scrive il file di log. Può trattarsi di un'unità locale o di una condivisione di rete.</br></br> Quando questa opzione non viene usata, il file di log viene scritto nella cartella temp dell'utente, sul computer in cui viene eseguito lo strumento.</br></br> Esempio di unità locale: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Esempio di condivisione di rete: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;condivisione>\&lt;cartella>***|
