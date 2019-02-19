---
title: Ridimensionamento e scalabilità
titleSuffix: Configuration Manager
description: Determinare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi nell'ambiente.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 304fe88dd5ed8a37bf17dca390d95158d005bae3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125369"
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Numeri di ridimensionamento e scalabilità per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



Ogni distribuzione di Configuration Manager ha un numero massimo di siti, di ruoli del sistema del sito e di dispositivi che può supportare. Questi numeri variano a seconda della struttura della gerarchia: i tipi e i numeri dei siti che vengono usati e dei ruoli del sistema del sito che vengono distribuiti. Le informazioni in questo articolo consentono di determinare il numero di ruoli del sistema del sito e di siti necessari per supportare i dispositivi che si prevede di gestire.

Usare le informazioni di questo argomento insieme a quelle contenute negli articoli seguenti:
-   [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato)
-   [Sistemi operativi supportati per i server del sistema del sito di System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemi operativi supportati per client e dispositivi](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


I numeri del supporto si basano sull'uso dell'hardware consigliato per Configuration Manager. Si basano anche sulle impostazioni predefinite per tutte le funzionalità di Configuration Manager disponibili. Quando non si utilizza l'hardware consigliato o si adottano impostazioni personalizzate più aggressive, le prestazioni dei sistemi del sito possono peggiorare. I sistemi del sito potrebbero non soddisfare i livelli di supporto. Un esempio di impostazioni client più aggressive è eseguire l'inventario hardware o software più frequentemente di quanto definito dalle impostazioni predefinite, vale a dire una volta ogni sette giorni.

##  <a name="bkmk_SiteSystemScale"></a> Tipi di sito  

### <a name="central-administration-site"></a>Sito di amministrazione centrale  

-   Un sito di amministrazione centrale supporta fino a 25 siti primari figlio.  


### <a name="primary-site"></a>Sito primario  

- Ogni sito primario può supportare fino a 250 siti secondari.  

- Il numero di siti secondari per il sito primario si basa su connessioni WAN (Wide Area Network) continuamente connesse e affidabili. Per i percorsi contenenti meno di 500 client, considerare un punto di distribuzione anziché un sito secondario.  

  Per informazioni sul numero di client e di dispositivi che un sito primario può supportare, vedere la sezione [Numero di client per siti e gerarchie](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Sito secondario  

-   I siti secondari non supportano siti figlio.  



## <a name="bkmk_roles"></a> Site system roles    


### <a name="application-catalog-web-service-point"></a>Punto per servizi Web del Catalogo applicazioni  

-   È possibile installare più istanze del punto di servizio Web Catalogo applicazioni nei siti primari.  

    > [!TIP]  
    >  Come procedura consigliata, installare il punto di sito Web Catalogo applicazioni e il punto di servizio Web Catalogo applicazioni nello stesso sistema del sito quando offrono servizi ai client che si trovano nella intranet.  

    -   Per migliorare le prestazioni, prevedere di supportare fino a 50.000 client per ogni istanza.  

    -   Ogni istanza di questo ruolo del sistema del sito supporta il numero massimo di client supportati dalla gerarchia.  


### <a name="application-catalog-website-point"></a>Punto per siti Web del Catalogo applicazioni  

-   È possibile installare più istanze del punto di sito Web Catalogo applicazioni nei siti primari.  

    > [!TIP]  
    >  Come procedura consigliata, installare il punto di sito Web Catalogo applicazioni e il punto di servizio Web Catalogo applicazioni nello stesso sistema del sito quando offrono servizi ai client che si trovano nella intranet.  

    -   Per migliorare le prestazioni, prevedere di supportare fino a 50.000 client per ogni istanza.  

    -   Ogni istanza di questo ruolo del sistema del sito supporta il numero massimo di client supportati dalla gerarchia.  


### <a name="bkmk_cmg"></a>Gateway di gestione cloud

- È possibile installare più istanze del gateway di gestione cloud nei siti primari o del sito di amministrazione centrale.  

    > [!Tip]  
    > Nella gerarchia, creare il gateway di gestione cloud nel sito di amministrazione centrale.  

    - Un gateway di gestione cloud supporta da 1 a 16 istanze di macchina virtuale nel servizio cloud di Azure.  

    - Ogni istanza di macchina virtuale del gateway di gestione cloud supporta 6.000 connessioni client simultanee. Quando il gateway di gestione cloud ha un carico elevato a causa di un numero di client maggiore di quello supportato, le richieste continuano a essere gestite ma potrebbero verificarsi ritardi.  

Per altre informazioni, vedere [Prestazioni e scalabilità](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) del gateway di gestione cloud


### <a name="cloud-management-gateway-connection-point"></a>Punto di connessione del gateway di gestione cloud

- È possibile installare più istanze del punto di connessione del gateway di gestione cloud nei siti primari.  

- Un punto di connessione del gateway di gestione cloud può supportare un gateway con fino a quattro istanze di macchine virtuali. Se il gateway di gestione cloud ha di più di quattro istanze di macchine virtuali, aggiungere un secondo punto di connessione per il bilanciamento del carico. Un gateway di gestione cloud con 16 istanze di macchine virtuali deve essere collegato a quattro punti di connessione gateway di gestione cloud.

Per altre informazioni, vedere [Prestazioni e scalabilità](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) del gateway di gestione cloud


### <a name="distribution-point"></a>Punto di distribuzione  

-   Punti di distribuzione per sito:  

    -   Ogni sito primario e secondario supporta fino a 250 punti di distribuzione.  

    -   Ogni sito primario e secondario supporta fino a 2000 punti di distribuzione aggiuntivi configurati come punti di distribuzione pull. **Ad esempio**, un singolo sito primario supporta 2250 punti di distribuzione quando 2000 di questi punti di distribuzione sono configurati come punti di distribuzione pull.  

    -   Ogni punto di distribuzione supporta connessioni da massimo 4.000 client.  

    -   Un punto di distribuzione pull funziona come client durante l'accesso al contenuto da un punto di distribuzione di origine.  

-   Ogni sito primario e secondario supporta un totale combinato di massimo 5.000 punti di distribuzione. Tale totale include tutti i punti di distribuzione nel sito primario e tutti i punti di distribuzione che appartengono ai siti secondari figlio del sito primario.  

-   Ogni punto di distribuzione supporta un totale combinato di massimo 10.000 pacchetti e applicazioni.  

> [!WARNING]  
>  Il numero effettivo di client che un punto di distribuzione può supportare dipende dalla velocità della rete e dalla configurazione hardware del server.  
>   
>  Analogamente, il numero di punti di distribuzione pull che un punto di distribuzione di origine può supportare dipende dalla velocità della rete e dalla configurazione hardware del punto di distribuzione di origine. Ma questo numero dipende anche dalla quantità di contenuto che è stato distribuito. Questo accade perché, a differenza dei client che in genere accedono al contenuto in momenti diversi durante una distribuzione, tutti i punti di distribuzione pull richiedono contenuto nello stesso momento. I punti di distribuzione pull possono richiedere tutto il contenuto disponibile senza limitarsi al contenuto che è applicabile ad essi. Quando un punto di distribuzione di origine presenta un carico di elaborazione elevato, si possono verificare ritardi imprevisti nella distribuzione del contenuto ai punti di distribuzione di destinazione.  


### <a name="fallback-status-point"></a>Punto di stato di fallback  

-   Ogni punto di stato di fallback è in grado di supportare fino a 100.000 client.  


### <a name="management-point"></a>Punto di gestione  

- Ogni sito primario supporta fino a 15 punti di gestione.  

  > [!TIP]  
  >  Non installare punti di gestione in server che usano un collegamento lento dal server del sito primario o dal server di database del sito.  

- Ciascun sito secondario supporta un unico punto di gestione che deve essere installato nel server del sito secondario.  

  Per informazioni sul numero di client e dispositivi che un punto di gestione può supportare, vedere la sezione [Punti di gestione](#bkmk_mp).  


### <a name="software-update-point"></a>Punto di aggiornamento software  

-   Un punto di aggiornamento software installato nel server del sito può supportare fino a 25.000 client.   

-   Un punto di aggiornamento software installato in un computer remoto rispetto al server del sito può supportare fino a 150.000 client quando il computer remoto soddisfa i requisiti di Windows Server Update Services (WSUS) per il supporto di questo numero di client.  



##  <a name="bkmk_clientnumbers"></a> Numero di client per siti e gerarchie  
 Usare le informazioni seguenti per determinare quanti e quali tipi di client è possibile supportare in un sito o in una gerarchia.  


###  <a name="bkmk_cas"></a> Gerarchia con un sito di amministrazione centrale  
Un sito di amministrazione centrale supporta un numero totale di dispositivi che comprende fino al numero di dispositivi elencati per i tre gruppi seguenti:  

- 700.000 desktop (computer che eseguono Windows, Linux e UNIX). Vedere anche il supporto per i [dispositivi integrati](#embedded).

- 25.000 dispositivi che eseguono Mac e Windows CE 7.0  

- Uno dei gruppi seguenti, a seconda del modo in cui la distribuzione supporta la gestione di dispositivi mobili (MDM):  

  -   100.000 dispositivi gestiti con software MDM locale  

  -   300.000 dispositivi basati sul cloud  

  Ad esempio, in una gerarchia è possibile supportare 700.000 desktop, fino a 25.000 dispositivi Mac e Windows CE 7.0 e fino a 300.000 dispositivi basati su cloud quando si integra Microsoft Intune. Questa gerarchia supporta un totale di 1.025.000 dispositivi. Se si supportano dispositivi gestiti tramite software MDM locale, il totale per questa gerarchia è 825.000 dispositivi.  

> [!IMPORTANT]  
>  In una gerarchia in cui il sito di amministrazione centrale usa un'edizione Standard di SQL Server, la gerarchia supporta un massimo di 50.000 desktop e dispositivi. Per supportare più di 50.000 desktop e dispositivi è necessario usare un'edizione Enterprise di SQL Server. Questo requisito si applica solo a un sito di amministrazione centrale. Non si applica a un sito primario autonomo o un sito primario figlio. L'edizione di SQL Server in uso per un sito primario non limita la sua capacità di supportare il numero dichiarato di client.   


 L'edizione di SQL Server in uso in un sito primario autonomo non limita la capacità di tale sito di supportare fino al numero dichiarato di client.  


###  <a name="bkmk_chipri"></a> Sito primario figlio  
Ogni sito primario figlio in una gerarchia con un sito di amministrazione centrale supporta il numero di client seguente:  

-   Un totale di 150.000 client e dispositivi che non sono limitati a un gruppo o tipo specifico, a condizione di non superare il numero supportato per la gerarchia. Vedere anche il supporto per i [dispositivi integrati](#embedded).

Ad esempio, un sito primario supporta 25.000 dispositivi Mac e Windows CE 7.0. Tale numero è il limite per la gerarchia. Questo sito primario può quindi supportare 125.000 computer desktop aggiuntivi. raggiungendo un numero totale di dispositivi supportati per il sito figlio primario di 150.000.


###  <a name="bkmk_pri"></a> Sito primario autonomo  
Un sito primario autonomo supporta il numero seguente di dispositivi:  

-   Un totale di 175.000 client e dispositivi, senza superare:  

    -   150.000 desktop (computer che eseguono Windows, Linux e UNIX). Vedere anche il supporto per i [dispositivi integrati](#embedded).

    -   25.000 dispositivi che eseguono Mac e Windows CE 7.0

    -   Uno dei gruppi seguenti, a seconda del modo in cui la distribuzione supporta la gestione dei dispositivi mobili:  

        -   50.000 dispositivi gestiti con software MDM locale  

        -   150.000 dispositivi basati sul cloud  


Ad esempio, un sito primario autonomo che supporta 150.000 desktop e 10.000 Mac o Windows CE 7.0 può supportare solo 15.000 dispositivi aggiuntivi. Questi dispositivi possono essere basati sul cloud o gestiti con software MDM locale.  


### <a name="embedded"></a> Siti primari e dispositivi con Windows Embedded
I siti primari supportano i dispositivi con Windows Embedded in cui sono abilitati i filtri di scrittura basati su file (FBWF). Se nei dispositivi integrati non sono abilitati filtri di scrittura, un sito primario può supportare un numero di dispositivi integrati non superiore al numero di dispositivi consentito per il sito. Del numero totale di dispositivi supportati da un sito primario, un massimo di 10.000 dispositivi possono essere Windows Embedded. Questi dispositivi devono essere configurati per le eccezioni elencate nella nota importante in [Pianificazione della distribuzione del client in dispositivi con Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Un sito primario supporta solo 3.000 dispositivi con Windows Embedded in cui è abilitato EWF e che non sono configurati per le eccezioni.


###  <a name="bkmk_sec"></a> Siti secondari  
I siti secondari supportano il numero di dispositivi seguente:  

-   15.000 desktop (computer che eseguono Windows, Linux e UNIX)  


###  <a name="bkmk_mp"></a> Punti di gestione  
Ogni punto di gestione può supportare il numero di dispositivi seguente:  

-   Un totale di 25.000 client e dispositivi, senza superare:  

    -   25.000 desktop (computer che eseguono Windows, Linux e UNIX)  

    -   Uno dei gruppi seguenti (non entrambi):  

        -   10.000 dispositivi gestiti con software MDM locale  

        -   10.000 dispositivi che eseguono client Mac e Windows CE 7.0
