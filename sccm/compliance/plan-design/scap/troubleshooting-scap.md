---
title: Risoluzione dei problemi relativi a SCAP
titleSuffix: System Center Configuration Manager
description: Importare le impostazioni di conformità SCAP come linee di base di configurazione ed esportare i risultati
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8270db5f0a43f1c94c876bdbd59e45ee2ca85ac6
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Risolvere i problemi delle estensioni SCAP per Microsoft System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella Technical Preview versione 1803 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features). Questa versione non definitiva delle estensioni SCAP può essere installata in qualsiasi versione attualmente supportata di Configuration Manager Current Branch e LTSB 1606. A partire dalla Technical Preview 1803, il file di installazione si trova in cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

SCAP Extensions per Microsoft System Center Configuration Manager è stato progettato per funzionare con i flussi di dati SCAP destinati allo strumento SCAP con funzionalità ACS per il supporto USGCB. In genere, non si verificano problemi con i flussi dei dati SCAP USGCB che vengono scaricati dal sito Web NIST.

È tuttavia possibile diagnosticare e risolvere eventuali problemi con i metodi seguenti:

- Verificare che i componenti client (scmdcm.msi) di SCAP Extensions vengano installati in tutti i computer di destinazione.
- Esaminare l'output del file di log dello strumento Microsoft.Sces.ScapToDcm.exe.
- Esaminare i problemi e le soluzioni comuni quando si usa SCAP Extensions.
- Per domande o commenti e suggerimenti su SCAP Extensions contattare Microsoft.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Esaminare il log dello strumento Microsoft.Sces.ScapToDcm.exe

Quando viene specificato il parametro -log, lo strumento Microsoft.Sces.ScapToDcm.exe crea un file di log denominato personalizzato. Il file di log contiene informazioni sui risultati dell'esecuzione dello strumento Microsoft.Sces.ScapToDcm.exe. Il file di log, ad esempio, contiene il numero degli elementi nel file di input XCCDF/DataStream che sono stati rimossi o ignorati durante l'esecuzione dello strumento Microsoft.Sces.ScapToDcm.exe.

Nella tabella seguente sono elencate alcune delle informazioni che vengono visualizzate nel file di log e una descrizione di ogni tipo di informazione.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Descrizione delle informazioni presenti nei file di log dello strumento Microsoft.Sces.ScapToDcm.exe

| Informazioni | Descrizione |
| --- | --- |
| Rimuovi | Un elemento potrebbe essere rimosso perché il tipo di test non è un tipo di test supportato. |
| Skip |L'ID definizione OVAL è per una piattaforma non valida. </br> </br> L'ID definizione OVAL non viene indicato con il file di input XCCDF/DataStream.</br> </br> L'ID test OVAL non viene indicato con il file di input XCCDF/DataStream. </br> </br> L'ID profilo XCCDF non contiene istruzioni @select uguali a 1. </br> </br> L'ID profilo XCCDF include un attributo abstract che è true. </br> </br> L'ID profilo XCCDF non contiene una regola valida.|

## <a name="common-problems-and-solutions"></a>Problemi comuni e soluzioni

Nella tabella seguente sono elencati alcuni problemi e soluzioni comuni per facilitare la risoluzione dei problemi.

Tabella 1.6 Problemi comuni e relative soluzioni

| Problema | Possibile soluzione |
| --- | --- |
| Se lo stato di una linea di base corrisponde a **Errore** o **Sconosciuto** e IE non è in grado di visualizzare il report. Internet Explorer visualizza il messaggio &quot;Il report è vuoto o non valido&quot; | Selezionare la linea di base e fare clic su **Valuta** per eseguire nuovamente la linea di base e quindi attendere per monitorare l'aggiornamento di **Stato di conformità**/**Ultima valutazione**. Dopo l'aggiornamento della data dell'ultima valutazione alla data/ora corrente (che significa che la valutazione è stata completata), selezionare la linea di base e visualizzare di nuovo il report. Se Internet Explorer non riesce ancora a visualizzare il report, potrebbe significare che la linea di base è troppo grande. Generare di nuovo il contenuto usando dimensioni inferiori per i batch per creare linee di base figlio più piccole. Se questo problema interessa le linee di base padre, provare a distribuire invece le linee di base figlio. |
| Sono stati creati oggetti Criteri di gruppo che includono le impostazioni USGCB prescritte. Questi oggetti sono stati collegati alle unità organizzative contenenti computer che eseguono Windows 7. I report di conformità, tuttavia, indicano che alcune impostazioni non sono configurate correttamente. | È possibile che le autorizzazioni di Criteri di gruppo non siano corrette o che non siano state collegate all'unità organizzativa corretta. Tuttavia, è più probabile che le nuove impostazioni non siano ancora state applicate. Per impostazione predefinita, nei computer client appartenenti a un dominio di Active Directory, vengono cercati aggiornamenti a Criteri di gruppo ogni 90 minuti. Questo potrebbe essere uno dei motivi del perché le impostazioni non sembrano essere state applicate, anche se i criteri sono stati configurati correttamente. Un altro fattore da ricordare è che molte impostazioni del computer richiedono un riavvio per essere effettive. L'impostazione denominata **Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma, ad esempio, richiede il riavvio del computer prima che Windows possa usare gli algoritmi di crittografia specificati. È possibile ignorare l'intervallo di aggiornamento di Criteri di gruppo immettendo il comando seguente al prompt dei comandi con privilegi di amministratore: gpupdate /force Al termine dell'aggiornamento di Criteri di gruppo, riavviare il computer per assicurarsi che tutte le impostazioni siano effettive. Per altre informazioni, vedere l'articolo della Knowledge Base 298444 [A Description of the Group Policy Update Utility](http://support.microsoft.com/kb/298444) (Descrizione dell'utilità di aggiornamento di Criteri di gruppo). |
| Si verifica un problema quando si forniscono le informazioni organizzative alla connessione database. | Per istruzioni su come configurare le informazioni di connessione del database, vedere l'articolo [Installare e configurare SCAP](/sccm/compliance/plan-design/scap/install-configure-scap). 

## <a name="next-step"></a>Passaggio successivo
> [!div class="nextstepaction"]
> [Installare e configurare le estensioni SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)