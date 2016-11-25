---
title: Percorso di origine del contenuto | System Center Configuration Manager
description: Informazioni sulle impostazioni di System Center Configuration Manager che consentono ai client di individuare il contenuto in una rete lenta.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 667010fedb37770d4105fc30f098a231292969fd

---
# <a name="content-source-location-scenarios-in-system-center-configuration-manager"></a>Scenari del percorso di origine del contenuto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supporta diverse impostazioni che possono essere combinate per definire come e dove i client possono trovare il contenuto quando usano una rete lenta. Le combinazioni possibili incidono sui percorsi del contenuto usati dai client, e sulla possibilità di usare correttamente un percorso di fallback quando l'origine preferita del contenuto non è disponibile.  



**Le tre impostazioni seguenti definiscono il comportamento quando i client richiedono contenuti:**

-  **Consenti percorso origine di fallback per il contenuto** (opzione abilitata o non abilitata): questa opzione può essere abilitata nella scheda Gruppi limite di un punto di distribuzione.  L'opzione consente al client di usare un punto di distribuzione configurato come percorso di fallback quando non è disponibile contenuto in un punto di distribuzione preferito.  

 - **Comportamento di distribuzione per la velocità di connessione di rete**: ogni distribuzione è configurata con uno dei comportamenti seguenti da usare quando la connessione al punto di distribuzione è lenta:  

    -   **Scarica il contenuto dal punto di distribuzione ed esegui in locale**  

    -   **Non scaricare il contenuto**: questa opzione viene usata solo quando un client usa un percorso di fallback per ottenere il contenuto  

    La velocità di connessione per un punto di distribuzione è configurata nella scheda Riferimenti del gruppo di limiti ed è specifica per tale gruppo.  

 -  **Distribuzione di pacchetti su richiesta** (nei punti di distribuzione preferiti): questa opzione viene abilitata quando si seleziona l'opzione **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti** nella scheda Impostazioni distribuzione delle proprietà delle applicazioni o di un pacchetto. Quando è abilitata, questa opzione fa in modo che Configuration Manager copi automaticamente il contenuto in un punto di distribuzione preferito in cui ancora non è presente dopo che un client richiede tale contenuto da tale punto di distribuzione.  


 **I requisiti seguenti si applicano a tutti gli scenari:**


-   Il contenuto è disponibile in un punto di distribuzione di fallback  

-   I punti di distribuzione sono online e accessibili  


## <a name="scenario-1"></a>Scenario 1  
 Si applica in presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: opzione non abilitata  

-   **Comportamento di distribuzione per rete lenta**: qualsiasi configurazione  


**Dettagli**: la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-2"></a>Scenario 2  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli**: la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-3"></a>Scenario 3  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto è disponibile in un punto di distribuzione preferito**  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli**: la configurazione per la distribuzione di pacchetti su richiesta non è pertinente in questo scenario.  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto.  

3.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-4"></a>Scenario 4  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: opzione non abilitata  

-   **Comportamento di distribuzione per rete lenta**: qualsiasi configurazione  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Nell'elenco non sono disponibili punti di distribuzione preferiti.  

3.  Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Ogni ora viene avviata una nuova richiesta di contenuto  

## <a name="scenario-5"></a>Scenario 5  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma esiste almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto non viene scaricato perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Non scaricare il contenuto** (opzione usata quando i client eseguono il fallback per ottenere il contenuto). Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Il client effettua una nuova richiesta di contenuto ogni ora.  

## <a name="scenario-6"></a>Scenario 6  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione non abilitata  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono abilitati.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto viene scaricato da un punto di distribuzione di fallback nell'elenco perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Scarica e installa il contenuto**.  

## <a name="scenario-7"></a>Scenario 7  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: opzione non abilitata  

-   **Comportamento di distribuzione per rete lenta**: qualsiasi configurazione  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Non esistono punti di distribuzione preferiti con contenuto.  

3.  Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Ogni ora viene effettuata una nuova richiesta di contenuto.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti. Nella maggior parte dei casi il contenuto viene distribuito correttamente nei punti di distribuzione preferiti entro un'ora.  

6.  Una nuova richiesta di contenuto viene avviata dal client al punto di gestione.  

7.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto. Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-8"></a>Scenario 8  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Non scaricare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto non viene scaricato perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Non scaricare**. Il client genera il messaggio di errore **Contenuto non disponibile** e passa in modalità Riprova. Il client effettua una nuova richiesta di contenuto ogni ora.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti. Nella maggior parte dei casi il contenuto viene distribuito correttamente nei punti di distribuzione preferiti entro un'ora.  

6.  Una nuova richiesta di contenuto viene avviata dal client al punto di gestione.  

7.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti con contenuto.  

8.  Il client scarica il contenuto da un punto di distribuzione preferito nell'elenco.  

## <a name="scenario-9"></a>Scenario 9  
 In presenza delle configurazioni seguenti:  

-   **Il contenuto non è disponibile in un punto di distribuzione preferito**  

-   **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**: opzione abilitata  

-   **Consenti fallback**: opzione abilitata  

-   **Comportamento di distribuzione per rete lenta**: Scaricare e installare il contenuto  


**Dettagli:**  

1.  Il client invia una richiesta di contenuto al punto di gestione. Il client include un flag con la richiesta che indica che i punti di distribuzione di fallback sono consentiti.  

2.  Al client viene restituito un elenco di percorsi del contenuto dal punto di gestione con i punti di distribuzione preferiti e i punti di distribuzione di fallback con contenuto. Non esistono punti di distribuzione preferiti con contenuto, ma almeno un punto di distribuzione di fallback con contenuto.  

3.  Il contenuto viene scaricato da un punto di distribuzione di fallback nell'elenco perché la proprietà di distribuzione per quando il client usa un punto di distribuzione di fallback è impostata su **Scarica e installa il contenuto**. Questa impostazione di distribuzione consente a un client che deve usare un percorso dei contenuti di fallback di ottenere il contenuto da tale percorso.  

4.  Il punto di gestione crea un trigger per Distribution Manager per distribuire il contenuto in tutti i punti di distribuzione preferiti per il client che ha effettuato la richiesta di contenuto.  

5.  Distribution Manager distribuisce il contenuto in tutti i punti di distribuzione preferiti, consentendo ai client aggiuntivi di ottenere il contenuto senza usare un punto di distribuzione di fallback.  



<!--HONumber=Nov16_HO1-->


