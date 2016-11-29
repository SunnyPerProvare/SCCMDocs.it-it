---
title: Supporto Unicode e ASCII | System Center Configuration Manager
description: Informazioni sul supporto di caratteri Unicode e ASCII in oggetti di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 125cc72389f6dc95668c8a2f73a4c50597eb3186


---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Supporto Unicode e ASCII in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager crea la maggior parte degli oggetti usando i caratteri Unicode. Tuttavia, numerosi oggetti supportano solo caratteri ASCII o hanno altre limitazioni.  

 Nelle seguenti sezioni vengono elencati gli oggetti che devono utilizzare solo i caratteri del set ASCII o che presentano limitazioni aggiuntive.  

-   [Oggetti che usano i caratteri ASCII](#BKMK_ASCIIchar)  

-   [Limitazioni aggiuntive](#BKMK_OtherCharLimitations)  

-   [Oggetti di Configuration Manager non localizzati](#BKMK_LangNonLocalize)  

##  <a name="a-namebkmkasciichara-objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a> Oggetti che usano i caratteri ASCII  
 Configuration Manager supporta il set di caratteri ASCII solo quando vengono creati gli oggetti seguenti:  

-   Codice sito  

-   Tutti i nomi di computer del server di sistema del sito  

-   I seguenti account di Configuration Manager:  

    > [!NOTE]  
    >  Questi account supportano i caratteri ASCII e RUS in un sito eseguito in lingua russa.  

    -   Account di installazione push client  

    -   Account di pubblicazione riferimenti sullo stato di integrità  

    -   Account di query riferimenti sullo stato di integrità  

    -   Account di connessione database del punto di gestione  

    -   Account di accesso alla rete  

    -   Account di accesso al pacchetto  

    -   Account mittente standard  

    -   Account di installazione sistema del sito  

    -   Account di connessione al punto di aggiornamento software  

    -   Account del server proxy del punto di aggiornamento software  

    > [!NOTE]  
    >  L'account specificato per l'amministrazione basata su ruoli supporta Unicode.  
    >   
    >  L'account del punto di Reporting Services supporta Unicode, ad eccezione dei caratteri RUS.  

-   FQDN per server e sistemi del sito  

-   Percorso di installazione per Configuration Manager  

-   Nomi di istanza di SQL Server  

-   Il percorso per i seguenti ruoli di sistema del sito:  

    -   Punto per servizi Web del Catalogo applicazioni  

    -   Punto per siti Web del Catalogo applicazioni  

    -   Punto di registrazione  

    -   Punto proxy di registrazione  

    -   Punto di Reporting Services  

    -   Punto di migrazione stato  

-   Il percorso delle seguenti cartelle:  

    -   La cartella che archivia i dati di migrazione dello stato del client  

    -   La cartella che contiene i report di Configuration Manager  

    -   La cartella che archivia il backup di Configuration Manager  

    -   La cartella che contiene i file di installazione per la configurazione del sito.  

    -   La cartella che contiene i download prerequisiti per l'utilizzo da parte della configurazione  

-   Il percorso dei seguenti oggetti:  

    -   Sito Web IIS  

    -   Percorso di installazione dell'applicazione virtuale  

    -   Nome dell'applicazione virtuale  

-   I seguenti oggetti per AMT e gestione fuori banda:  

    -   FQDN del computer basato su AMT  

    -   Il nome del computer basato su AMT  

    -   Il nome NetBIOS del dominio  

    -   Nome del profilo wireless e SSID  

    -   Il nome dell'autorità di certificazione radice attendibile  

    -   Il nome dell'autorità di certificazione (CA) e i nomi dei modelli  

    -   Il nome e il percorso del file di immagine di reindirizzamento IDE  

    -   Il contenuto dell'archivio dati AMT  

-   Nomi file .ISO dei supporti di avvio  

##  <a name="a-namebkmkothercharlimitationsa-additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a> Limitazioni aggiuntive  
 Di seguito vengono riportate ulteriori limitazioni per i set di caratteri e le versioni delle lingue supportati:  

-   Configuration Manager non supporta la modifica delle impostazioni locali del computer del server del sito.  

-   Un'autorità di certificazione dell'organizzazione (enterprise) non supporta i nomi dei computer client che utilizzano set di caratteri DBCS. I nomi dei computer client che è possibile utilizzare sono limitati dalla limitazione PKI del set di caratteri IA5. Configuration Manager non supporta neppure i nomi di autorità di certificazione (CA) o i valori del nome oggetto che usano DBCS.  

##  <a name="a-namebkmklangnonlocalizea-configuration-manager-objects-that-are-not-localized"></a><a name="BKMK_LangNonLocalize"></a> Oggetti di Configuration Manager non localizzati  
 Il database di Configuration Manager supporta Unicode per la maggior parte degli oggetti archiviati e, se possibile, visualizza tali informazioni nella lingua del sistema operativo corrispondente alle impostazioni locali di un computer. Affinché l'interfaccia client o la console di Configuration Manager visualizzi le informazioni nella lingua del sistema operativo del computer, le impostazioni locali del computer devono corrispondere alla lingua di un client o di un server installato in un sito.  

 Diversi oggetti di Configuration Manager non supportano i caratteri Unicode, vengono quindi archiviati nel database usando caratteri ASCII oppure presentano limitazioni aggiuntive relative alla lingua. Queste informazioni vengono sempre visualizzate utilizzando il seti di caratteri ASCII o nella lingua in uso al momento della creazione dell'oggetto.  



<!--HONumber=Nov16_HO1-->


