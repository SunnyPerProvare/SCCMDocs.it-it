---
title: Dati di diagnostica per la versione 1610 | System Center Configuration Manager
description: Informazioni sui livelli dei dati di diagnostica e di utilizzo raccolti da System Center Configuration Manager versione 1610.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 6b4af705fa148261634d38dbb2df9988c5672180
ms.openlocfilehash: df8a4c84da8e73aae2455e5f5af26d097449cddd

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Livelli dei dati di diagnostica e di utilizzo raccolti da System Center Configuration Manager versione 1610

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager versione 1610 raccoglie tre livelli di dati di diagnostica e di utilizzo: **Di base**, **Avanzato** e **Completo**. Per impostazione predefinita, per questa funzionalità è impostato il livello avanzato. Le sezioni seguenti forniscono ulteriori dettagli sui dati raccolti per ogni livello.

Le modifiche rispetto alle versioni precedenti sono contrassegnate da ***[Nuovo]***, ***[Aggiornato]***, ***[Rimosso]*** o ***[Spostato]***.


> [!IMPORTANT]
>  Configuration Manager non raccoglie codici del sito o nomi di siti, indirizzi IP, nomi utente, nomi di computer, indirizzi fisici o indirizzi di posta elettronica per i livelli di base e avanzato. L'eventuale raccolta di tali informazioni per il livello completo non è intenzionale (dati potenzialmente inclusi nelle informazioni di diagnostica avanzate come file di log o snapshot di memoria) e le informazioni eventualmente raccolte non verranno usate da Microsoft per identificare l'utente, contattare l'utente o per fini pubblicitari.

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Come cambiare il livello
 Gli amministratori con ambito amministrativo basato sui ruoli che include le autorizzazioni **Modifica** per la classe di oggetti **Sito** possono modificare il livello dei dati raccolti nelle impostazioni dei dati di diagnostica e di utilizzo nella console di Configuration Manager.

A partire dalla versione 1610, è possibile modificare il livello di raccolta dati dall'interno della console, passando a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**. Aprire **Impostazioni gerarchia** e selezionare il livello di dati che si vuole usare.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Livello 1 - Di base
 Il livello di base include i dati sulla gerarchia ed è necessario per consentire il miglioramento dell'esperienza di installazione o aggiornamento, nonché per determinare quali aggiornamenti di Configuration Manager sono applicabili per la gerarchia.

 Per System Center Configuration Manager versione 1610, questo livello include:


 -   Informazioni sull'installazione:
      - Build, tipo di installazione, language pack, funzionalità abilitate  

      -   Stato di distribuzione ed errori del pacchetto di aggiornamento, avanzamento del download ed errori dei prerequisiti    

      -  Versione dello script post-aggiornamento

      -  Uso di Fast Ring di aggiornamento

    -  ***[Nuovo]*** Uso delle versioni non definitive, tipo di supporto di installazione, tipo Branch

    - ***[Nuovo]*** Data di scadenza Software Assurance


-   Metriche delle prestazioni del database (informazioni sull'elaborazione della replica, principali stored procedure di SQL Server per processore e utilizzo del disco)

-   Configurazione di base dei database (processori, configurazione del cluster, configurazione delle viste distribuite)

-   Schema del database di Configuration Manager (hash di tutte le definizioni di oggetti)

-   Numero delle versioni client di Configuration Manager e delle versioni del sistema operativo

-   Numero e sistema operativo dei dispositivi gestiti e dei criteri impostati da Exchange Connector

-   Numero delle lingue e delle impostazioni locali dei client

-   Numero dei dispositivi Windows 10 per ramo e build

-   Dati di base sulla gerarchia dei siti di Configuration Manager (elenco dei siti, tipo, versione, stato, numero di client e fuso orario)

-   Informazioni di base sul server del sistema del sito (ruoli del sistema del sito usati, stato di Internet e SSL, sistema operativo, processori, computer fisico o macchina virtuale)

-   Statistiche di base di individuazione degli utenti (numero di individuazioni di utenti, dimensioni minime/massime/medie dei gruppi)

-   Informazioni di base sulla protezione degli endpoint (versioni client antimalware)

-   Conteggi di base per applicazioni e tipi di distribuzione (totale app, totale app con più tipi di distribuzione, totale app con dipendenze, totale app sostituite, numero delle tecnologie di distribuzione in uso)

-   Conteggi di base OSD (immagini)

-   Tipi di punto di distribuzione e di punto di gestione e informazioni di base sulla configurazione (protetto, pre-installato, PXE, multicast, stato di SSL, punti di distribuzione pull/peer, abilitato per MDM, abilitato per SSL e così via)

-   Statistiche di telemetria (data/ora di esecuzione, runtime, errori)

-  Livello di telemetria configurato, modalità online o offline e configurazione di aggiornamento rapido

-  Uso di Network Discovery (abilitato o disabilitato)
-  Admin Console:

     -  Statistiche sulle connessioni della console (versione del sistema operativo, lingua, SKU e architettura; memoria di sistema, conteggio dei processori logici, ID del sito di connessione, versioni di .NET installate e Language Pack della console)    


- Versione SQL, livello Service Pack, edizione, ID regole di confronto, set di caratteri


##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Livello 2 - Avanzato
Il livello avanzato è quello predefinito dopo l'installazione. Questo livello include i dati raccolti per il livello di base, oltre a dati specifici per le funzionalità (frequenza e durata d'utilizzo), le impostazioni client di Configuration Manager (nome del componente, stato e alcune impostazioni come gli intervalli di polling) e le informazioni di base sugli aggiornamenti software.

Questo livello è consigliato perché offre a Microsoft i dati minimi necessari per apportare miglioramenti utili nelle versioni future di prodotti e servizi. Con questo livello non vengono raccolti i nomi degli oggetti (siti, utenti, computer o oggetti), dettagli sugli oggetti correlati alla sicurezza o informazioni sulle vulnerabilità come il numero di sistemi che richiedono aggiornamenti software.

Per System Center Configuration Manager versione 1610, questo livello include:

-   **Gestione delle applicazioni:**  

    -    Informazioni di base su utilizzo/destinazione per i tipi di distribuzione usati all'interno dell'organizzazione (utente e dispositivo di destinazione, richiesto o disponibile, app universali)  

    -   Informazioni sulla distribuzione delle applicazioni (installazione/disinstallazione, approvazione richiesta, interazione con l'utente abilitata o disabilitata, dipendenza, sostituzione)  

    -   Dati statistici sulle richieste di applicazioni disponibili  

    -   Numero di pacchetti per tipo  

    -   Numero di applicabilità delle applicazioni per sistema operativo  

    -   Numero di distribuzioni di pacchetti/programmi  

    -   Numero di ambienti e proprietà di distribuzione App-V  

    -   Numero di licenze per applicazioni con licenza Windows 10  

    -   Numero massimo/minimo/medio di distribuzioni di applicazioni per ogni utente o dispositivo per periodo

    -   Tipo e durata della finestra di manutenzione  

    -  Dimensioni criteri di applicazione e statistiche di complessità

    - ***[Aggiornato]*** Statistiche di sincronizzazione e delle app di Windows Store per le aziende, inclusi riepilogo dei tipi di app, stato delle app con licenza e numero di app con licenza online e offline  

    - Statistiche dei gruppi di limiti, compresi numero di veloci e lenti e conteggio per gruppo

    - Opzioni di configurazione MSI e conteggi

    - Requisiti delle app (conteggio delle condizioni predefinite con riferimento per tecnologia di distribuzione)

    - Sostituzione delle app, profondità massima della catena

    - Uso UDA, modalità di creazione

    - ***[Nuovo]*** Statistiche sull'approvazione applicazione e frequenza di utilizzo



-   **Client:**  

    -   Elenco/numero di agenti client abilitati  

    -   Numero di installazioni client da ogni tipo di posizione di origine  

    -   Numero di errori di installazioni client  

    -  ***[Aggiornato]*** Aggiornamento automatico del client: configurazione della distribuzione inclusi client pilota, utilizzo di esclusione (client a interoperabilità estesa)

    -  Statistiche dell'integrità dei client e riepilogo dei problemi principali

    - Età del BIOS in anni

    - Età del sistema operativo in mesi

    - Conteggio delle azioni di Software Center

    - Versione del client AMT (Active Management Technology)

    - Errori di download della distribuzione client

    - Stato dell'azione operazione di notifica client: numero di esecuzioni di ogni azione, numero massimo di client assegnati, frequenza media esecuzioni senza errori

    - Metodi di distribuzione usati per il client, numero di client per metodo di distribuzione

    - Configurazione della dimensione della cache del client

    - ***[Nuovo]*** Numero di classi di inventario hardware, regole dell'inventario software e regole di raccolta dei file




- **Servizi cloud:**

  - Conteggio delle raccolte sincronizzate in OMS

  -  Abilitazione del connettore cloud OMS

  - ***[Nuovo]*** Statistiche di utilizzo e configurazione del gateway di gestione cloud

  - ***[Nuovo]*** Conteggio dei connettori di analisi degli aggiornamenti




- **Raccolte:**

    -  Statistiche di valutazione raccolte (durata query, conteggi assegnati e non assegnati, conteggi per tipo, rollover degli ID e uso di regole)

    - Raccolte senza distribuzione

    - Uso ID raccolte (senza esaurimento degli ID)



-   **Impostazioni di conformità:**  

    -   Numero di elementi di configurazione per tipo  

    -   Informazioni di base sulla linea di base di configurazione (numero, numero di distribuzioni e numero di riferimenti)  

    -   Numero di distribuzioni che fanno riferimento a impostazioni predefinite (ora con acquisizione dell'impostazione di correzione)  

    -   Numero di regole e di distribuzioni create per le impostazioni personalizzate (ora con acquisizione dell'impostazione di correzione)  
    -   Conteggio di Simple Certificate Enrollment Protocol, VPN, WiFi, certificato (.pfx) e modelli dei criteri di conformità distribuiti

    -  Conteggio del certificato SCEP, VPN, Wifi, certificato (.pfx) e distribuzioni dei criteri di conformità per piattaforma

    - Criteri di Passport for Work (creati, distribuiti)



-   **Contenuto:**  

    -   Numero di limiti per tipo  

    -   Informazioni sui gruppi di limiti (numero di limiti e di sistemi del sito assegnati a ogni gruppo di limiti)  

    - ***[Nuovo]*** Relazioni di gruppo di limiti e configurazione del fallback

    -   Informazioni sui gruppi di punti di distribuzione (numero di pacchetti e punti di distribuzione assegnati a ogni gruppo di punti di distribuzione)  

    -   Informazioni di configurazione sui punti di distribuzione (uso di BranchCache, monitoraggio dei punti di distribuzione)  

    -   Informazioni di configurazione di Distribution Manager (thread, intervallo tra tentativi, numero di tentativi, impostazioni sui punti di distribuzione pull)  

    - ***[Nuovo]*** Numero di client peer cache e statistiche di utilizzo

    - ***[Nuovo]*** Statistiche di download dei contenuti client


-   **Endpoint Protection:**  

    -   Utilizzo dei criteri antimalware di EndPoint Protection e di Windows Firewall (numero di criteri univoci assegnati al gruppo; non sono incluse informazioni sulle impostazioni contenute nei criteri)  

    -   Errori di distribuzione di Endpoint Protection (numero di codici di errore di distribuzione dei criteri di Endpoint Protection)  

    -   Numero di raccolte selezionate per la visualizzazione nel dashboard di Endpoint Protection  

    -   Numero di avvisi configurati per funzionalità Endpoint Protection  

    - Criteri ATP (conteggio dei criteri, verifica della distribuzione)


- **Migrazione:**

  -   Numero di oggetti migrati (uso della procedura guidata di migrazione)



-   **Gestione di dispositivi mobili (MDM):**  

    -   ***[Aggiornato]*** Numero di comandi per azioni su dispositivi mobili: blocco, reimpostazione PIN, cancellazione, ritiro dati e Sincronizza ora  

    -   Numero di dispositivi mobili gestiti da Configuration Manager e Microsoft Intune e modalità di registrazione (in blocco, basata sull'utente)  

    -   Pianificazione del polling dei dispositivi mobili e durata dei controlli statistici dei dispositivi mobili  

    -   Numero di criteri per dispositivi mobili  

    -   Numero di utenti con più dispositivi mobili registrati  

-   **Risoluzione dei problemi di Microsoft Intune:**

    -   Numero e dimensioni dei messaggi relativi a stato, inventario, RDR, DDR, UDX, stato tenant, POL, LOG, Cert, CRP, risincronizzazione, CFD, RDO, BEX, ISM e conformità scaricati da Microsoft Intune

    -   Numero e dimensioni dei messaggi relativi ad azioni sui dispositivi (cancellazione, ritiro dati, blocco), telemetria e dati replicati in Microsoft Intune

    -   Statistiche della sincronizzazione degli utenti completa e differenziale per Microsoft Intune


-   **Gestione di dispositivi mobili (MDM) in locale:**  

    -   Statistiche di esito positivo o negativo della distribuzione per distribuzioni di applicazioni MDM in locale  

    -   Numero dei pacchetti e dei profili di registrazione in blocco di Windows 10  



-   **Distribuzione del sistema operativo:**  

    -   Numero di immagini di avvio, driver, pacchetti di driver, punti di distribuzione abilitati per il multicast, punti di distribuzione che supportano PXE e sequenze di attività  

    -   Numero uilizzi del passaggio della sequenza di attività

    - ***[Nuovo]*** Numero dei criteri di aggiornamento dell'edizione



-   **Aggiornamenti del sito:**

    - Versioni degli hotfix di Configuraton Manager installati




-   **Aggiornamenti del software:**  

    -   Numero totale/medio di raccolte con distribuzioni di aggiornamento del software e numero massimo/medio di aggiornamenti distribuiti  

    -   Numero di regole di distribuzione automatica associate alla sincronizzazione  

    -   Numero di regole di distribuzione automatica che aggiungono aggiornamenti o ne creano di nuovi in un gruppo esistente  

    -   Delta di disponibilità e scadenza usati nelle regole di distribuzione automatica  

    -   Numero medio e massimo di assegnazioni per ogni aggiornamento  

    -   Numero di aggiornamenti creati e distribuiti con System Center Update Publisher  

    -   Numero di gruppi e assegnazioni di aggiornamento  

    -   Numero di pacchetti di aggiornamento e numero massimo/minimo/medio dei punti di distribuzione assegnati con pacchetti  

    -   Numero di gruppi di aggiornamento e numero minimo/massimo/medio di aggiornamenti per ogni gruppo  

    -   Numero di aggiornamenti e percentuale di aggiornamenti distribuiti, scaduti, sostituiti, scaricati e contenenti EULA  

    -   Codici di errore e numero di computer per l'analisi per l'aggiornamento  

    -   Pianificazioni di valutazione e analisi per l'aggiornamento dei client  

    -   Pianificazione della sincronizzazione dei punti di aggiornamento software  

    -   Numero di regole di distribuzione automatica con più distribuzioni  

    -   Configurazioni usate per i piani di manutenzione attivi di Windows 10  

    -   Versioni del contenuto del dashboard di Windows 10  

    -   Numero di client Windows 10 che usano Windows Update per le aziende  

    -   Statistiche relative all'applicazione di patch al cluster  

    -   Numero di aggiornamenti di Office 365 distribuiti  

    -   Classificazioni sincronizzate dal punto di aggiornamento software

    -   Statistiche di bilanciamento del carico del punto di aggiornamento software

    -  ***[Nuovo]*** Configurazione degli aggiornamenti rapidi di Windows 10




-   **Dati SQL/prestazioni:**  

    -   Numero delle tabelle di database più grandi  

    -   ***[Aggiornato]*** Stato d'integrità, uso e informazioni sulla replica di SQL AlwaysOn

    -  Periodo di memorizzazione del rilevamento modifiche di SQL

    - Tipi di individuazione, abilitazione e pianificazione (completa, incrementale)

    - Statistiche operative di individuazione (numero di oggetti trovati)

    - Problemi di prestazioni del rilevamento modifiche di SQL, periodo di memorizzazione e stato di pulizia automatica



- **Varie**

    - Numero di siti con WOL

    - ***[Nuovo]*** Statistiche sull'utilizzo e sulle prestazioni della creazione di report  



##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Livello 3 - Completo
Il livello competo include tutti i dati dei livelli di base e avanzato. Include inoltre informazioni aggiuntive su Endpoint Protection, le percentuali di conformità degli aggiornamenti e informazioni sugli aggiornamenti software.  Questo livello può includere anche informazioni di diagnostica avanzate, come file di sistema e snapshot di memoria, che possono contenere informazioni personali presenti in memoria o nei file di log al momento dell'acquisizione.

Per System Center Configuration Manager versione 1610, questo livello include:

-   Statistiche di valutazione e aggiornamento delle raccolte

-   Riepilogo dell'integrità di Endpoint Protection (incluso il numero di client protetti, a rischio, sconosciuti e non supportati)

-   Configurazione dei criteri di Endpoint Protection

-   Informazioni sulla distribuzione degli aggiornamenti software (percentuale di distribuzioni assegnate ai client o  ora UTC, aggiornamento obbligatorio/facoltativo/invisibile all'utente, e facoltativi e invisibile all'utente, eliminazione del riavvio)

-   Conformità generale delle distribuzioni degli aggiornamenti software

-   Informazioni sulla pianificazione di valutazione delle regole di distribuzione automatiche

-   Codici e numero di errori di distribuzione degli aggiornamenti software

-   Numero minimo/massimo/medio dei client inattivi nelle raccolte di distribuzioni di aggiornamenti software

-   Numero di gruppi con aggiornamenti software scaduti

-   Numero minimo/massimo/medio di aggiornamenti software per ogni gruppo

-   Percentuali di analisi dell'aggiornamento software con esito positivo

-   Numero minimo/massimo/medio di ore dall'ultima analisi di aggiornamenti software

-    Prodotti di aggiornamento software sincronizzati dal punto di aggiornamento software
-    Impostazioni di conformità: SCEP, VPN, Wifi e dettagli di configurazione del modello dei criteri di conformità

-    Tipo di criteri di accesso condizionale EAS (blocco o quarantena) per i dispositivi gestiti da Intune

-   Prime 50 CPU dell'ambiente

-   Pacchetto di configurazione DCM per l'uso di SCCM

-   Codice prodotto MSI (app comuni distribuite dai clienti)

-   Riepilogo dell'integrità ATP

-   Errori di installazione della distribuzione client dettagliati

- ***[Nuovo]*** Dettagli delle applicazioni Windows Store per le aziende: elenco non aggregato di applicazioni sincronizzate, comprendente ID applicazione, stato online o offline, numero totale di licenze acquistate



<!--HONumber=Dec16_HO3-->


