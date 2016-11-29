---
title: Siti Web per i sistemi del sito | System Center Configuration Manager
description: Questa sezione contiene informazioni sui siti Web predefiniti e personalizzati per i server del sistema del sito in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3f463aa804cb928b29fc26d9af8dede7f65222df


---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Siti Web per i server del sistema del sito in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Alcuni ruoli del sistema del sito di Configuration Manager richiedono Microsoft Internet Information Services (IIS) e usano il sito Web IIS predefinito per ospitare i servizi del sistema del sito. Quando è necessario eseguire altre applicazioni Web nello stesso server e le impostazioni non sono compatibili con Configuration Manager, provare a usare un sito Web personalizzato per Configuration Manager.  

> [!TIP]  
>  Come procedura di sicurezza consigliata, destinare un server ai sistemi del sito di Configuration Manager che richiedono IIS. Quando si eseguono altre applicazioni in un sistema del sito di Configuration Manager, si aumenta la superficie di attacco di tale computer.  




##  <a name="a-namebkmkwhat2knowa-what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a> Cosa è necessario sapere prima di scegliere di usare i siti Web personalizzati  
 Per impostazione predefinita, i ruoli del sistema del sito usano il **sito Web predefinito** in IIS. Ciò viene configurato automaticamente quando si installa il ruolo del sistema del sito. Tuttavia, nei siti primari è possibile scegliere di usare i siti Web personalizzati. Quando si usano siti Web personalizzati:  

-   I siti Web personalizzati sono abilitati per l'intero sito, non per i singoli server o ruoli del sistema del sito.  

-   Nei siti primari è necessario configurare ogni computer che ospiterà un ruolo del sistema del sito applicabile con un sito Web personalizzato denominato **SMSWEB**. Fino a quando non viene creato il sito Web e i ruoli del sistema del sito nel computer non vengono configurati per l'uso del sito Web personalizzato, è possibile che i client non siano in grado di comunicare con i ruoli del sistema del sito nel computer.  

-   Dal momento che i siti secondari vengono configurati automaticamente per l'uso di un sito Web personalizzato quando il sito primario padre è configurato a tale scopo, è necessario creare anche i siti Web personalizzati in IIS in ogni server del sistema del sito secondario che richiede IIS.  


  **Prerequisiti per l'uso di siti Web personalizzati:**  

 prima di abilitare l'opzione per usare i siti Web personalizzati in un sito, è necessario:  

-   Creare un sito Web personalizzato denominato **SMSWEB** in IIS in ogni server del sistema del sito che richiede IIS. Eseguire questa operazione nel sito primario e in tutti i siti secondari figlio.  

-   Configurare il sito Web personalizzato in modo che risponda alla stessa porta configurata per la comunicazione client di Configuration Manager (porta della richiesta del client).  

-   Per ogni sito Web personalizzato o predefinito che usa una cartella personalizzata, inserire una copia del tipo di documento predefinito da usare nella cartella radice che ospita il sito Web. Ad esempio, in un computer Windows Server 2008 R2 con configurazioni predefinite, **iisstart.htm** è uno dei diversi tipi di documenti predefiniti disponibili. È possibile trovare questo file nella directory principale del sito Web predefinito e quindi inserire una copia del file (o una copia del tipo di documento predefinito da usare) nella cartella radice che ospita il sito Web personalizzato SMSWEB. Per altre informazioni sui tipi di documento predefiniti, vedere [Documento predefinito &lt;defaultDocument\> per IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**Informazioni sui requisiti IIS:**
** i seguenti ruoli del sistema del sito richiedono IIS e un sito Web per ospitare i servizi del sistema del sito:**  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di distribuzione  

-   Punto di registrazione  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

Altre considerazioni:  

-   Quando un sito primario contiene siti Web personalizzati abilitati, i client assegnati a tale sito vengono indirizzati per comunicare con i siti Web personalizzati anziché con i siti Web predefiniti nei server del sistema del sito applicabili.  

-   Se si usano i siti Web personalizzati per un sito primario, provare a usare i siti Web personalizzati per tutti i siti primari nella gerarchia per assicurarsi che i client possano effettuare il roaming all'interno della gerarchia. Il roaming avviene quando un computer client si sposta in un nuovo segmento di rete gestito da un sito diverso. e può influire sulle risorse a cui il client può accedere localmente anziché con un collegamento WAN.  

-   Anche i ruoli del sistema del sito che usano IIS ma non accettano connessioni client, come ad esempio il punto di Reporting Services, usano il sito Web SMSWEB invece del sito Web predefinito.  

-   Ai siti Web personalizzati è necessario assegnare dei numeri di porta diversi da quelli usati dal sito Web predefinito del computer. Non è possibile eseguire contemporaneamente un sito Web predefinito e un sito Web personalizzato se entrambi provano a usare le stesse porte TCP/IP.  

-   Le porte TCP/IP configurate in IIS per il sito Web personalizzato devono corrispondere alle porte di richiesta client per il sito.  

## <a name="switching-between-default-and-custom-websites"></a>Passaggio da siti Web predefiniti a siti Web personalizzati  
Nonostante sia possibile in qualsiasi momento selezionare o deselezionare la casella di controllo per l'uso di siti Web personalizzati in un sito primario (si tratta di una casella di controllo nella scheda Generale delle proprietà dei siti), effettuare un'attenta pianificazione prima di apportare questa modifica. Quando si modifica questa configurazione, è necessario disinstallare e quindi reinstallare tutti i ruoli del sistema del sito applicabili nel sito primario e nei siti secondari figlio:  

I seguenti ruoli **vengono reinstallati automaticamente**:  

-   Punto di gestione  

-   Punto di distribuzione  

-   Punto di aggiornamento software  

-   Punto di stato di fallback  

-   Punto di migrazione stato  

I seguenti ruoli devono essere **reinstallati manualmente**:  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di registrazione  

-   Punto proxy di registrazione  

Inoltre:  

-   Quando si passa dall'uso del sito Web predefinito all'uso di un sito Web personalizzato, Configuration Manager non rimuove le vecchie directory virtuali. Se si decide di rimuovere i file usati da Configuration Manager, è necessario eliminare manualmente le directory virtuali create nel sito Web predefinito.  

-   Se si modifica il sito per usare i siti Web personalizzati, è necessario riconfigurare i client già assegnati al sito per usare le nuove porte di richiesta client per i siti Web personalizzati. Vedere [Come configurare porte di comunicazione client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md)  

## <a name="configure-custom-websites"></a>Configurare siti Web personalizzati  
Dal momento che la procedura per creare un sito Web personalizzato varia a seconda delle diverse versioni del sistema operativo, vedere la documentazione relativa alla versione del sistema operativo per la procedura esatta, ma usare le seguenti informazioni quando applicabile:  

-   Il nome del sito Web deve essere: **SMSWEB**  

-   Quando si configura il protocollo HTTPS, è necessario specificare un certificato SSL prima di poter salvare la configurazione.  

-   Dopo aver creato il sito Web personalizzato, rimuovere le porte del sito Web personalizzato usate da altri siti Web in IIS:  

    1.  Modificare le **associazioni** degli altri siti Web per rimuovere le porte che corrispondono a quelle assegnate al sito Web **SMSWEB** .  

    2.  Avviare il sito Web **SMSWEB** .  

    3.  Riavviare il servizio **SMS_SITE_COMPONENT_MANAGER** nel server del sito.  



<!--HONumber=Nov16_HO1-->


