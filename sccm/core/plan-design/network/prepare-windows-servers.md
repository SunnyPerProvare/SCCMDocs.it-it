---
title: Preparare i server Windows| System Center Configuration Manager
description: Assicurarsi che un computer soddisfi i prerequisiti per l'uso come server del sito o server di sistema del sito per System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f0a1cc32285fcb792c3f4cdec616668474708404
ms.openlocfilehash: acf8a401f1ce67a4d8c905c0126c031b97484271


---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Preparare i server di Windows per il supporto di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter usare un computer Windows come server di sistema del sito per System Center Configuration Manager, è necessario assicurarsi che il computer soddisfi i prerequisiti per l'uso previsto come server del sito o server di sistema del sito.  

-   Questi prerequisiti includono spesso uno o più ruoli o funzionalità di Windows, che vengono abilitati usando Server Manager del computer.  

-   Dal momento che il metodo per abilitare i ruoli e le funzionalità di Windows cambia in base ai diversi sistemi operativi, vedere la documentazione del sistema operativo in uso per informazioni dettagliate sulla configurazione.  

Le informazioni contenute in questo articolo offrono una panoramica dei tipi di configurazioni Windows necessari per il supporto dei sistemi del sito Configuration Manager. Per informazioni dettagliate sulla configurazione dei ruoli di sistema del sito specifico, vedere [Prerequisiti del sito e del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="a-namebkmkwinfeaturesa-windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Ruoli e funzionalità di Windows  
 Quando si configurano i ruoli e le funzionalità di Windows in un computer, potrebbe essere necessario riavviare il computer per completare la configurazione. È consigliabile quindi identificare i computer che ospiteranno i ruoli di sistema del sito prima di installare un sito o un server di sistema del sito di Configuration Manager.
### <a name="features"></a>Caratteristiche  
 le funzionalità di Windows seguenti sono richieste in alcuni server del sistema del sito e devono essere configurate prima di installare un ruolo del sistema del sito nel computer.  

-   **.NET Framework**: inclusi  

    -   ASP.NET  

    -   Attivazione HTTP  

    -   Attivazione non HTTP  

    -   Servizi WCF  

    Per i diversi ruoli del sistema del sito sono necessarie versioni specifiche di .NET Framework.  

    Dal momento che .NET Framework 4.0 e versioni successive non è compatibile con le versioni precedenti e non riesce a sostituire la versione 3.5 e precedenti, quando sono richieste versioni diverse, pianificare l'abilitazione di ogni versione nello stesso computer.  

-   **Servizio trasferimento intelligente in background (BITS)**: i punti di gestione richiedono BITS e le opzioni selezionate automaticamente per supportare la comunicazione con i dispositivi gestiti.  

-   **BranchCache**: i punti di distribuzione possono essere configurati con BranchCache per supportare i client che usano BranchCache.  

-   **Deduplicazione dati**: i punti di distribuzione possono essere configurati con la deduplicazione dei dati, che offre diversi vantaggi.  

-   **Compressione differenziale remota (RDC)**: ogni computer che ospita un server del sito o un punto di distribuzione richiede una compressione differenziale remota.   
    La compressione differenziale remota viene usata per generare le firme dei pacchetti ed eseguire confronti tra le firme.  

### <a name="roles"></a>Ruoli  
 i ruoli di Windows seguenti sono necessari per supportare specifiche funzionalità, ad esempio gli aggiornamenti software e le distribuzioni del sistema operativo, mentre IIS è richiesto per la maggior parte dei ruoli del sistema del sito più comuni.  

 -   **Servizio Registrazione dispositivi di rete** in Servizi certificati Active Directory: questo ruolo di Windows è un prerequisito per l'uso dei profili dei certificati in Configuration Manager.  

 -   **Server Web (IIS)**: includono:  

    -   Funzionalità HTTP comuni >  

        -   Reindirizzamento HTTP  

    -   Sviluppo di applicazioni >  

        -   Estendibilità .NET  

        -   ASP.NET  

        -   Estensioni ISAPI  

        -   Filtri ISAPI  

    -   Strumenti di gestione >  

        -   Compatibilità Gestione IIS 6  

        -   Compatibilità Metabase IIS 6  

        -   Compatibilità WMI IIS 6  

    -   Sicurezza >  

        -   Filtro richieste  

        -   Autenticazione di Windows  

 I ruoli del sistema del sito seguenti usano una o più delle configurazioni IIS elencate:  

    -   Punto per servizi Web del Catalogo applicazioni  

    -   Punto per siti Web del Catalogo applicazioni  

    -   Punto di distribuzione  

    -   Punto di registrazione  

    -   Punto proxy di registrazione  

    -   Punto di stato di fallback  

    -   Punto di gestione  

    -   Punto di aggiornamento software  

    -   Punto di migrazione stato  

    La versione minima di IIS richiesta è la versione fornita dal sistema operativo del server del sito.  

    Oltre a queste configurazioni IIS, potrebbe essere necessario configurare [Filtro richieste IIS per i punti di distribuzione](#BKMK_IISFiltering).  

-   **Servizi di distribuzione Windows**: questo ruolo viene usato con la distribuzione del sistema operativo.  

-   **Windows Server Update Services**: questo ruolo è richiesto quando si distribuiscono gli aggiornamenti software.  

##  <a name="a-namebkmkiisfilteringa-iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtro richieste IIS per i punti di distribuzione  
 Per impostazione predefinita, IIS usa il filtro richieste per bloccare l'accesso di diverse estensioni di file e percorsi di cartelle con la comunicazione HTTP o HTTPS. In un punto di distribuzione, questo impedisce ai client di scaricare i pacchetti che contengono estensioni bloccate o percorsi di cartelle.  

 Quando i file di origine del pacchetto contengono estensioni bloccate in IIS dalla configurazione del filtro richieste, è necessario configurare il filtro richieste per abilitarle. Per farlo, [modificare la funzionalità del filtro richieste](https://technet.microsoft.com/library/hh831621.aspx) in Gestione IIS nei computer del punto di distribuzione.  

 Le estensioni di file seguenti vengono usate da Configuration Manager per applicazioni e pacchetti. Verificare che le configurazioni del filtro richieste non blocchino queste estensioni di file:  

-   PCK  

-   PKG  

-   STA  

-   TAR  

Ad esempio, si possono avere file di origine per una distribuzione del software che includono una cartella denominata **bin**o che contengono un file con estensione **mdb** .  

-   Per impostazione predefinita, il filtro richieste IIS blocca l'accesso a questi elementi (**bin** è bloccato perché è un segmento nascosto e **mdb** è bloccato come estensione di file).  

-   Quando si usa la configurazione IIS predefinita in un punto di distribuzione, i client che usano BITS non riescono a scaricare questa distribuzione del software dal punto di distribuzione e indicano che sono in attesa del contenuto.  

-   Per abilitare il download del contenuto per i client, modificare il **filtro richieste** in Gestione IIS per ogni punto di distribuzione applicabile per consentire l'accesso alle estensioni di file e alle cartelle contenute nei pacchetti e nelle applicazioni distribuiti.  

> [!IMPORTANT]  
>  Le modifiche al filtro richieste possono aumentare la superficie di attacco del computer.  
>   
>  -   Le modifiche apportate a livello server si applicano a tutti i siti Web nel server  
> -   Le modifiche ai singoli siti Web si applicano solo al sito Web specificato  
>   
>  La procedura di sicurezza consigliata è l'esecuzione di Configuration Manager in un server Web dedicato. Se è necessario eseguire altre applicazioni nel server Web, usare un sito Web personalizzato per Configuration Manager. Per informazioni, vedere [Siti Web per i server del sistema del sito in System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Verbi HTTP
**Punti di gestione:** per assicurarsi che i client possano comunicare correttamente con un punto di gestione, verificare che i verbi HTTP seguenti siano consentiti nel server del punto di gestione:  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Punti di distribuzione:** i punti di distribuzione richiedono che i verbi HTTP seguenti siano consentiti:
 - GET
 - HEAD
 - PROFIND

Per informazioni sulla configurazione del filtro richieste, vedere [Configurare il filtro richieste in IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) su TechNet o in una documentazione simile che si applica alla versione di Windows Server che ospita il punto di gestione.



<!--HONumber=Nov16_HO1-->

