---
title: Ridimensionamento e scala | Microsoft Docs
description: Identificare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi nell&quot;ambiente System Center Configuration Manager.
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9c43e26758d5171a6ef56e827b4b054ebc8a5e5
ms.openlocfilehash: c7ad33339e65e6e00e88f98d6e13baceb98dae77

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Numeri di ridimensionamento e scalabilità per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



Ogni distribuzione di System Center Configuration Manager ha un numero massimo di siti, di ruoli del sistema del sito e di dispositivi che può supportare. Questi numeri variano a seconda della struttura della gerarchia (i tipi e i numeri dei siti che vengono usati) e dei ruoli del sistema del sito che vengono distribuiti.  Le informazioni nelle aree seguenti consentono di identificare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi che si prevede di gestire con il proprio ambiente.

Usare le informazioni di questo argomento insieme a quelle contenute negli articoli seguenti:
-   [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato)
-   [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemi operativi supportati per client e dispositivi](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Prerequisiti del sito e del sistema del sito per System Center Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


I numeri del supporto riportati di seguito si basano sull'uso dell'hardware consigliato per Configuration Manager e delle impostazioni predefinite per tutte le funzionalità di Configuration Manager disponibili. Quando non si usa l'hardware consigliato oppure si usano impostazioni personalizzate più aggressive (come l'esecuzione dell'inventario hardware o software con maggiore frequenza rispetto all'impostazione predefinita pari a una volta ogni sette giorni), le prestazioni dei sistemi del sito possono peggiorare e non corrispondere ai livelli di supporto dichiarati.

##  <a name="a-namebkmksitesystemscalea-site-types"></a><a name="bkmk_SiteSystemScale"></a> Tipi di sito  
 **Sito di amministrazione centrale:**  

-   Un sito di amministrazione centrale supporta fino a 25 siti primari figlio.  

**Sito primario:**  

-   Ogni sito primario può supportare fino a 250 siti secondari.  

-   Il numero di siti secondari per il sito primario si basa su connessioni WAN (Wide Area Network) continuamente connesse e affidabili. Per i percorsi contenenti meno di 500 client, considerare un punto di distribuzione anziché un sito secondario.  

 Per informazioni sul numero di client e di dispositivi che un sito primario può supportare, vedere la sezione [Numero di client per siti e gerarchie](#bkmk_clientnumbers) in questo argomento.  

**Sito secondario:**  

-   I siti secondari non supportano siti figlio.  

-   Un sito di amministrazione centrale supporta fino a 25 siti primari figlio.  

**Punto per siti Web del Catalogo applicazioni:**  

-   È possibile installare più istanze del punto di sito Web Catalogo applicazioni nei siti primari.  

    > [!TIP]  
    >  Come procedura consigliata, installare il punto di sito Web Catalogo applicazioni e il punto di servizio Web Catalogo applicazioni nello stesso sistema del sito quando offrono servizi ai client che si trovano nella intranet.  

    -   Per migliorare le prestazioni, prevedere di supportare fino a 50.000 client per ogni istanza.  

    -   Ogni istanza di questo ruolo del sistema del sito supporta il numero massimo di client supportati dalla gerarchia.  

## <a name="a-namebkmkrolesa-site-system-roles"></a><a name="bkmk_roles"></a> Site system roles    

**Punto per servizi Web del Catalogo applicazioni:**  

-   È possibile installare più istanze del punto di servizio Web Catalogo applicazioni nei siti primari.  

    > [!TIP]  
    >  Come procedura consigliata, installare il punto di sito Web Catalogo applicazioni e il punto di servizio Web Catalogo applicazioni nello stesso sistema del sito quando offrono servizi ai client che si trovano nella intranet.  

    -   Per migliorare le prestazioni, prevedere di supportare fino a 50.000 client per ogni istanza.  

    -   Ogni istanza di questo ruolo del sistema del sito supporta il numero massimo di client supportati dalla gerarchia.  

**Punto di distribuzione:**  

-   Punti di distribuzione per sito:  

    -   Ogni sito primario e secondario supporta fino a 250 punti di distribuzione.  

    -   Ogni sito primario e secondario supporta fino a 2000 punti di distribuzione aggiuntivi configurati come punti di distribuzione pull. **Ad esempio**, un singolo sito primario supporta 2250 punti di distribuzione quando 2000 di questi punti di distribuzione sono configurati come punti di distribuzione pull.  

    -   Ogni punto di distribuzione supporta connessioni da massimo 4.000 client.  

    -   Un punto di distribuzione pull funziona come client durante l'accesso al contenuto da un punto di distribuzione di origine.  

-   Ogni sito primario e secondario supporta un totale combinato di massimo 5.000 punti di distribuzione. Tale totale include tutti i punti di distribuzione nel sito primario e tutti i punti di distribuzione che appartengono ai siti secondari figlio del sito primario.  

-   Ogni punto di distribuzione supporta un totale combinato di massimo 10.000 pacchetti e applicazioni.  

> [!WARNING]  
>  Il numero effettivo di client che un punto di distribuzione può supportare dipende dalla velocità della rete e dalla configurazione hardware del computer del punto di distribuzione.  
>   
>  Analogamente, il numero di punti di distribuzione pull che un punto di distribuzione di origine può supportare dipende dalla velocità della rete e dalla configurazione hardware del computer del punto di distribuzione di origine. Ma questo numero dipende anche dalla quantità di contenuto che è stato distribuito. Infatti, a differenza dei client che in genere accedono al contenuto in momenti diversi nel corso di una distribuzione, tutti i punti di distribuzione pull richiedono il contenuto nello stesso momento e possono chiedere tutto il contenuto disponibile, non solo quello loro applicabile, come farebbe un client. Quando un punto di distribuzione di origine presenta un carico di elaborazione eccessivo, si possono verificare ritardi imprevisti nella distribuzione del contenuto ai punti di distribuzione previsti nell'ambiente in uso.  


**Punto di stato di fallback:**  

-   Ogni punto di stato di fallback è in grado di supportare fino a 100.000 client.  

**Punto di gestione:**  

-   Ogni sito primario supporta fino a 15 punti di gestione.  

    > [!TIP]  
    >  Non installare punti di gestione in server che usano un collegamento lento dal server del sito primario o dal server di database del sito.  

-   Ciascun sito secondario supporta un unico punto di gestione che deve essere installato nel server del sito secondario.  

 Per informazioni sul numero di client e dispositivi che un punto di gestione può supportare, vedere la sezione [Punti di gestione](#bkmk_mp) in questo argomento.  

**Punto di aggiornamento software:**  

-   Un punto di aggiornamento software installato nel server del sito può supportare fino a 25.000 client.  

-   Un punto di aggiornamento software installato in un computer remoto rispetto al server del sito può supportare fino a 150.000 client quando il computer remoto soddisfa i requisiti di Windows Server Update Services (WSUS) per il supporto di questo numero di client.  

-   Per impostazione predefinita, Configuration Manager non supporta la configurazione di punti di aggiornamento software come cluster di Bilanciamento carico di rete. È possibile tuttavia usare l'SDK di Configuration Manager per configurare fino a quattro punti di aggiornamento software in un cluster di Bilanciamento carico di rete.  

##  <a name="a-namebkmkclientnumbersa-client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a> Numero di client per siti e gerarchie  
 Usare le informazioni seguenti per determinare quanti e quali tipi di client è possibile supportare in un sito o in una gerarchia.  

###  <a name="a-namebkmkcasa-hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a> Gerarchia con un sito di amministrazione centrale  
Un sito di amministrazione centrale supporta un numero totale di dispositivi che comprende fino al numero di dispositivi elencati per i tre gruppi seguenti:  

-   700.000 desktop (computer che eseguono Windows, Linux e UNIX)  

-   25.000 dispositivi che eseguono Mac e Windows CE 7.0  

-   Uno dei gruppi seguenti, a seconda del modo in cui la distribuzione supporta la gestione di dispositivi mobili (MDM):  

    -   100.000 dispositivi gestiti con software MDM locale  

    -   300.000 dispositivi basati sul cloud  

 Ad esempio, in una gerarchia è possibile supportare 700.000 desktop, fino a 25.000 Mac e Windows CE 7.0 e fino a 300.000 dispositivi basati su cloud quando si integra Microsoft Intune, per un totale di 1.025.000 dispositivi. Se si supportano dispositivi gestiti tramite software MDM locale, il totale per la gerarchia è 825.000 dispositivi.  

> [!IMPORTANT]  
>  In una gerarchia in cui il sito di amministrazione centrale usa un'edizione Standard di SQL Server, la gerarchia supporta un massimo di 50.000 desktop e dispositivi. L'edizione di SQL Server in uso in un sito primario autonomo non limita la capacità di tale sito di supportare fino al numero dichiarato di client.  


###  <a name="a-namebkmkchipria-child-primary-site"></a><a name="bkmk_chipri"></a> Sito primario figlio  
Ogni sito primario figlio in una gerarchia con un sito di amministrazione centrale supporta le quantità seguenti:  

-   Un totale di&150;.000 client e dispositivi che non sono limitati a un gruppo o tipo specifico, a condizione di non superare il numero supportato per la gerarchia.  

Ad esempio, un sito primario che supporta 25.000 computer che eseguono Mac e Windows CE 7.0, vale a dire il limite per una gerarchia, può quindi supportare 125.000 computer desktop aggiuntivi, raggiungendo un numero totale di dispositivi supportati pari al limite massimo dei siti figlio primari, ovvero 150.000.

###  <a name="a-namebkmkpria-stand-alone-primary-site"></a><a name="bkmk_pri"></a> Sito primario autonomo  
Un sito primario autonomo supporta il numero seguente di dispositivi:  

-   Un totale di&175;.000 client e dispositivi, senza superare:  

    -   150.000 desktop (computer che eseguono Windows, Linux e UNIX)  

    -   25.000 dispositivi che eseguono Mac e Windows CE 7.0

    -   Uno dei gruppi seguenti, a seconda del modo in cui la distribuzione supporta la gestione dei dispositivi mobili:  

        -   50.000 dispositivi gestiti con software MDM locale  

        -   150.000 dispositivi basati sul cloud  

Ad esempio, un sito primario autonomo che supporta 150.000 desktop e 10.000 Mac o Windows CE 7.0 può supportare solo 15.000 dispositivi aggiuntivi. Questi dispositivi possono essere basati sul cloud o gestiti con software MDM locale.  

###  <a name="a-namebkmkseca-secondary-sites"></a><a name="bkmk_sec"></a> Siti secondari  
I siti secondari supportano le quantità seguenti:  

-   15.000 desktop (computer che eseguono Windows, Linux e UNIX)  

###  <a name="a-namebkmkmpa-management-points"></a><a name="bkmk_mp"></a> Punti di gestione  
Ogni punto di gestione può supportare il numero di dispositivi seguente:  

-   Un totale di&25;.000 client e dispositivi, senza superare:  

    -   25.000 desktop (computer che eseguono Windows, Linux e UNIX)  

    -   Uno dei gruppi seguenti (non entrambi):  

        -   10.000 dispositivi gestiti con software MDM locale  

        -   10.000 dispositivi che eseguono client Mac e Windows CE 7.0



<!--HONumber=Dec16_HO5-->


