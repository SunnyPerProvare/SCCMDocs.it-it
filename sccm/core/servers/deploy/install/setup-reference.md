---
title: Informazioni di riferimento | System Center Configuration Manager
description: Esaminare le informazioni di riferimento seguenti che consentono di preparare l'installazione di un sito o di una gerarchia di Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 06bab7e01fee2c0b030a2879fa67fd455bf668fe


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Informazioni di riferimento per l'installazione di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il programma di installazione di System Center Configuration Manager fa riferimento a diversi argomenti descritti in dettaglio nelle sezioni seguenti. Le informazioni nelle sezioni seguenti possono essere utili per preparare l'installazione di un sito o di una gerarchia di Configuration Manager e per prendere alcune delle decisioni necessarie durante l'installazione:  

-   [Prima di iniziare](#bkmk_start)  

-   [Valutare la conformità dei server](#bkmk_assess)  

-   [Client per altri sistemi operativi](#bkmk_Addclients)  

-   [Diagnostica e dati di utilizzo per System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

##  <a name="a-namebkmkstarta-before-you-begin"></a><a name="bkmk_start"></a> Prima di iniziare  
 Prima di installare nuovi siti di Configuration Manager, assicurarsi di avere esaminato le informazioni seguenti, utili per garantire una buona riuscita della distribuzione:  

-   [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md) (Nozioni fondamentali su System Center Configuration Manager)  

-   [Plan for System Center Configuration Manager infrastructure](../../../plan-design/network/configure-firewalls-ports-domains.md) (Pianificare l'infrastruttura di System Center Configuration Manager)  

-   [Prepare to install System Center Configuration Manager sites](prepare-to-install-sites.md) (Preparare l'installazione di siti di System Center Configuration Manager)  

##  <a name="a-namebkmkassessa-assess-server-readiness"></a><a name="bkmk_assess"></a> Valutare la conformità dei server  
 Prima di iniziare l'installazione di un nuovo sito, verificare che il server del sito e i server di sistema del sito remoti da usare per il sito (ad esempio il server che ospita il database del sito) soddisfino tutte le configurazioni dei prerequisiti. Gli argomenti seguenti nella raccolta di documentazione possono essere utili:  

-   [Configurazioni supportate per System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  

-   [Controllo prerequisiti](https://technet.microsoft.com/library/mt590813.aspx#bkmk_PreqChk)  

##  <a name="a-namebkmkaddclientsa-clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> Client per altri sistemi operativi  
 È possibile scaricare il software client per Configuration Manager dall'Area download Microsoft per i sistemi operativi seguenti:  

-   Mac   (Apple)  

-   UNIX  

-   Linux  

**Usare i collegamenti seguenti per scaricare i client per la versione di Configuration Manager in uso:**  

-   [System Center Configuration Manager (Current Branch)](http://www.microsoft.com/download/details.aspx?id=47719)  

-   [System Center 2012 R2 Configuration Manager SP1 e System Center 2012 Configuration Manager SP2](http://go.microsoft.com/fwlink/?LinkID=626550)  

-   [System Center 2012 R2 Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=316448)  

-   [System Center 2012 Configuration Manager SP1](http://www.microsoft.com/en-pk/download/details.aspx?id=36212)  

##  <a name="a-namebkmkusagea-usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Impostazioni e livelli per i dati di utilizzo  
Quando si installa il primo sito di System Center Configuration Manager, nel server del sito viene installato e configurato automaticamente un nuovo ruolo del sistema del sito, ovvero il **punto di connessione del servizio**, con le impostazioni predefinite seguenti:  

-   Modalità**Online** (è supportata anche una modalità offline)  

-   Livello di raccolta dati **Avanzato** (sono supportati altri due livelli di raccolta dati, Base e Completo)  

Quando questo ruolo è online, consente a Microsoft di raccogliere automaticamente informazioni di utilizzo e di diagnostica in Internet. Le informazioni raccolte sono utili per:  

-   Identificare e risolvere i problemi  

-   Migliorare i prodotti e il servizio  

-   Identificare gli aggiornamenti per Configuration Manager applicabili alla versione in uso  

I tre livelli di raccolta dati includono:  

-   **Base** : include i dati su installazione e aggiornamento, come il numero di siti e le funzionalità di Configuration Manager abilitate. Non vengono trasmesse informazioni personali.  

-   **Avanzato** : include i dati contenuti nell'impostazione Base e trasmette i dati sulla gerarchia, come vengono usate le singole funzionalità, ad esempio frequenza e durata, e informazioni di diagnostica avanzata, come lo stato della memoria del server quando si verifica un arresto anomalo di un sistema o un'app. Non vengono trasmessi dati riservati.  

-   **Completo** : include i dati contenuti nelle impostazioni Base e Avanzato e invia anche informazioni di diagnostica avanzate, ad esempio file di sistema e snapshot di memoria. Questa opzione può includere informazioni personali, che tuttavia non verranno usate per identificare o contattare l'utente o a fini pubblicitari.  

Per altre informazioni, tra cui la divulgazione dei dettagli raccolti da ogni livello, vedere [Diagnostics and usage data for System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md) (Dati di diagnostica e di uso per System Center Configuration Manager).  

[Informativa sulla privacy di System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527)



<!--HONumber=Nov16_HO1-->


