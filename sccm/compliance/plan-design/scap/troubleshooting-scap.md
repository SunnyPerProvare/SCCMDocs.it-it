---
title: Risoluzione dei problemi relativi a SCAP
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi delle estensioni SCAP per Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f1dcfe872fceb6163bbe8893062bc8294dc9b2de
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75818146"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Risolvere i problemi delle estensioni SCAP per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le estensioni SCAP per Configuration Manager sono progettate per funzionare con i flussi dei dati SCAP destinati allo strumento di convalida SCAP con funzionalità di controllo di accesso per il supporto della conformità con l'iniziativa USGCB. In genere, non si verificano problemi con i flussi dei dati SCAP USGCB che vengono scaricati dal sito Web NIST.

Per diagnosticare e risolvere i problemi, usare i metodi seguenti:  

- Verificare che i componenti client (scmdcm.msi) delle estensioni SCAP siano installati in tutti i computer di destinazione.  

- Esaminare l'output del file di log dello strumento Microsoft.Sces.ScapToDcm.exe.  

- Esaminare i problemi e le soluzioni comuni durante l'utilizzo delle estensioni SCAP.  

- Per domande o commenti e suggerimenti sulle estensioni SCAP, contattare Microsoft.



## <a name="review-microsoftscesscaptodcmexe-log"></a>Esaminare il log dello strumento Microsoft.Sces.ScapToDcm.exe

Quando viene specificato il parametro `–log`, lo strumento Microsoft.Sces.ScapToDcm.exe crea un file di log con un nome personalizzato. Il file di log contiene informazioni sui risultati dell'esecuzione dello strumento Microsoft.Sces.ScapToDcm.exe. Il file di log, ad esempio, include il numero degli elementi nel file di input XCCDF/DataStream che sono stati rimossi o ignorati durante l'esecuzione dello strumento Microsoft.Sces.ScapToDcm.exe.

Nella tabella seguente sono elencate alcune delle informazioni visualizzate nel file di log e una descrizione di ogni tipo di informazione.

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Informazioni presenti nei file di log dello strumento Microsoft.Sces.ScapToDcm.exe

| Informazioni | Descrizione |
| --- | --- |
| **Rimuovi** | Un elemento potrebbe essere rimosso perché il tipo di test non è un tipo di test supportato. |
| **Ignora** | L'ID definizione OVAL è per una piattaforma non valida. </br> </br> L'ID definizione OVAL non viene indicato con il file di input XCCDF/DataStream.</br> </br> L'ID test OVAL non viene indicato con il file di input XCCDF/DataStream. </br> </br> L'ID profilo XCCDF non contiene istruzioni `@select` uguali a 1. </br> </br> L'ID profilo XCCDF include un attributo abstract che è true. </br> </br> L'ID profilo XCCDF non contiene una regola valida.|



## <a name="common-problems-and-solutions"></a>Problemi comuni e soluzioni

Di seguito sono elencati alcuni problemi e soluzioni comuni per facilitare la risoluzione dei problemi.

- Se viene visualizzato uno stato di **errore** o **sconosciuto** relativo a una linea di base e Internet Explorer non è in grado di visualizzare il report. L'errore del browser indica "Il report è vuoto o non è valido."  

     - Eseguire di nuovo la linea di base. Selezionare la linea di base e fare clic su **Evaluate** (Valuta). Attendere e monitorare **Compliant State**/**Last Evaluation update** (Stato conforme > Aggiornamento ultima valutazione). Dopo l'aggiornamento della data dell'ultima valutazione alla data/ora corrente (che significa che la valutazione è stata completata), selezionare la linea di base e visualizzare di nuovo il report.  

     - Se Internet Explorer non riesce ancora a visualizzare il report, potrebbe significare che la linea di base è troppo grande. Generare di nuovo il contenuto usando dimensioni inferiori per i batch per creare linee di base figlio più piccole.  

     - Se questo problema interessa le linee di base padre, provare a distribuire invece le linee di base figlio.  

- Sono stati creati oggetti Criteri di gruppo che includono le impostazioni USGCB indicate. Sono stati collegati alle unità organizzative contenenti i computer che eseguono Windows 7. I report di conformità indicano che alcune impostazioni non sono configurate correttamente.  

     - È possibile che le autorizzazioni di Criteri di gruppo non siano corrette o che i Criteri di gruppo non siano stati collegati all'unità organizzativa corretta.  

     - È più probabile che le nuove impostazioni non siano ancora diventate effettive. Per impostazione predefinita, i client Active Directory verificano la disponibilità di aggiornamento a Criteri di gruppo ogni 90 minuti. Questo ciclo potrebbe essere uno dei motivi per cui le impostazioni non sembrano essere effettive, anche se i criteri sono stati configurati correttamente.  

     - Molte impostazioni del computer richiedono un riavvio per diventare effettive. Ad esempio l'impostazione denominata **Crittografia sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma** richiede il riavvio del computer prima che Windows possa usare gli algoritmi di crittografia specificati. È possibile ignorare l'intervallo di aggiornamento di Criteri di gruppo immettendo il comando seguente nel prompt dei comandi con privilegi di amministratore: `gpupdate /force`. Dopo aver completato l'aggiornamento di Criteri di gruppo, riavviare il computer per assicurarsi che tutte le impostazioni vengano applicate. Per altre informazioni, vedere [Descrizione dell'utilità di aggiornamento di Criteri di gruppo](https://support.microsoft.com/help/298444).

- Si verifica un problema quando si specifica la connessione di database usando le informazioni aziendali.  

     - Per altre informazioni su come configurare la connessione di database, vedere [Installare e configurare SCAP](/sccm/compliance/plan-design/scap/install-configure-scap).  
