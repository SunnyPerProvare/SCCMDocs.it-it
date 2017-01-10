---
title: Pianificare i server e i ruoli del sistema | Documentazione Microsoft
description: Prendere in considerazione i server di sistema del sito e i ruoli di sistema del sito quando si pianifica la gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2b00cfcec0959716d69a1605018f33d30287fee9
ms.openlocfilehash: a2e57aac01fff3c28b4acfcf58bcd786bd3e62c4


---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Pianificare i server e i ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Ogni sito di System Center Configuration Manager installato include un server del sito, ovvero un **server di sistema del sito**. Il sito può includere anche altri server del sistema del sito nei computer remoti rispetto al server del sito.   I server del sistema del sito, ovvero il server del sito o un server del sistema del sito remoto, supportano i **ruoli del sistema del sito**.


##  <a name="a-namebkmksiteserversa-site-system-servers"></a><a name="bkmk_siteservers"></a> Server del sistema del sito  
 Quando si installa un ruolo del sistema del sito in un computer, il computer diventa un server del sistema del sito. In ogni sito è possibile installare uno o più server del sistema del sito aggiuntivi. Si può anche scegliere di non installare altri server del sistema del sito ed eseguire tutti i ruoli del sistema del sito direttamente nel computer del server del sito.  Ogni server del sistema del sito supporta uno o più ruoli del sistema del sito e consente di espandere le funzionalità e la capacità di un sito condividendo il carico di elaborazione della CPU immesso dai ruoli del sistema del sito in un server.  

 Quando si valuta se aggiungere un server del sistema del sito, verificare che il server soddisfi i prerequisiti per l'uso previsto e che si trovi in un percorso di rete con larghezza di banda sufficiente per comunicare con gli endpoint previsti, inclusi il server del sito, le risorse di dominio, il percorso basato sul cloud, i server del sistema del sito e i client.  

 Se si configura il server del sistema del sito con un proxy usato dai ruoli del sistema del sito, vedere [Ruoli del sistema del sito che possono usare un server proxy](#bkmk_proxy)  

##  <a name="a-namebkmkplanrolesa-site-system-roles"></a><a name="bkmk_planroles"></a> Site system roles  
 I ruoli del sistema del sito vengono installati in un computer per fornire altre funzionalità al sito. Alcuni esempi:  

-   Punti di gestione aggiuntivi in modo tale che il sito sia in grado di supportare più dispositivi, fino alla capacità supportata dei siti  

-   Punti di distribuzione aggiuntivi per espandere l'infrastruttura del contenuto, migliorando le prestazioni delle distribuzioni di contenuto a utenti e dispositivi  

-   Uno o più ruoli del sistema del sito specifici delle funzionalità, come un punto di aggiornamento software che consenta di gestire gli aggiornamenti software per i dispositivi gestiti oppure un punto di Reporting Services che consenta di eseguire report per monitorare e comprendere o condividere le informazioni relative alla distribuzione  


Vari siti di Configuration Manager possono supportare diversi set di ruoli di sistema del sito. I ruoli del sistema del sito supportati dipendono dal tipo di sito, ad esempio un sito di amministrazione centrale, un sito primario o un sito secondario. La topologia della gerarchia può limitare l'uso di alcuni ruoli a determinati tipi di sito. Ad esempio, il punto di connessione del servizio è supportato solo nel sito di livello superiore della gerarchia, che può essere un sito di amministrazione centrale o un sito primario autonomo. Questo ruolo non è supportato in un sito primario figlio o nei siti secondari.  

Dopo l'installazione di un sito, è possibile spostare la posizione di alcuni ruoli del sistema del sito dalla posizione predefinita nel server del sito a un altro server, ad esempio il punto di gestione o il punto di distribuzione installato per impostazione predefinita in un server del sito primario o secondario. È anche possibile installare altre istanze di alcuni ruoli del sistema del sito per espandere le funzionalità del sito, ovvero fornire altri servizi ai client, e per soddisfare i requisiti aziendali. Alcuni ruoli sono obbligatori, mentre altri sono facoltativi:  

-   **Server del sito di Configuration Manager**: questo ruolo identifica il server in cui viene eseguito il programma di installazione di Configuration Manager per installare un sito oppure il server in cui installare un sito secondario. Questo ruolo non può essere spostato o disinstallato finché non viene disinstallato il sito.  

-   **Sistema del sito di Configuration Manager**: questo ruolo viene assegnato a qualsiasi computer in cui si installa un sito o un ruolo di sistema del sito.  Questo ruolo non può essere spostato o disinstallato finché l'ultimo ruolo del sistema del sito non viene rimosso dal computer.  

-   **Ruolo di sistema del sito del componente di Configuration Manager**: questo ruolo identifica un sistema del sito che esegue un'istanza del servizio SMS Executive ed è necessario per supportare altri ruoli, ad esempio i punti di gestione. Questo ruolo non può essere spostato o disinstallato finché l'ultimo ruolo del sistema del sito applicabile non viene rimosso dal computer.  

-   **Server di database del sito di Configuration Manager**: questo ruolo viene assegnato ai server di sistema del sito che mantengono un'istanza del database del sito per un sito.  Questo ruolo può essere spostato solo in un nuovo server modificando il sito in modo che usi un altro SQL Server per ospitare il database del sito.  

-   **Provider SMS**: questo ruolo viene assegnato a ogni computer che ospita un'istanza del provider SMS, l'interfaccia tra una console di Configuration Manager e il database del sito.  Per impostazione predefinita, questo ruolo viene installato automaticamente nel server del sito di un sito di amministrazione centrale e nei siti primari ed è possibile installare altre istanze in ogni sito per fornire l'accesso amministrativo a un sito ad altri utenti amministratori.  

     A differenza della maggior parte dei ruoli del sistema del sito che vengono installati dall'interno della console, per installare altri provider è necessario eseguire il programma di installazione di Configuration Manager per [gestire il provider SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) e quindi installare altri provider in computer aggiuntivi. È possibile installare solo un'istanza del provider SMS in un computer e tale computer deve essere nello stesso dominio del server del sito.  

-   **Punto per servizi Web del Catalogo applicazioni** : ruolo del sistema del sito che invia informazioni sul software al sito Web del Catalogo applicazioni dalla Libreria software. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

-   **Punto del sito Web del Catalogo applicazioni** : ruolo del sistema del sito che offre agli utenti un elenco del software disponibile nel Catalogo applicazioni. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Quando il Catalogo applicazioni supporta computer client su Internet, installare il punto per siti Web del Catalogo applicazioni in una rete perimetrale e il punto per servizi Web del Catalogo applicazioni sulla intranet come procedura di sicurezza consigliata.  

-   **Punto di sincronizzazione di Asset Intelligence** : ruolo del sistema del sito che si connette a Microsoft per scaricare informazioni sul catalogo di Asset Intelligence e caricare titoli senza categoria in modo che possano essere presi in considerazione per una futura inclusione nel catalogo.  Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale.   Per altre informazioni, vedere [Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Punto di registrazione certificati** : ruolo del sistema del sito che comunica con un server in cui è in esecuzione il servizio Registrazione dispositivi di rete per gestire le richieste di certificato del dispositivo che usano il protocollo Simple Certificate Enrollment Protocol (SCEP).  Questo ruolo è supportato solo nei siti primari e nel sito di amministrazione centrale.   Anche se un unico punto di registrazione certificati può fornire funzionalità a un'intera gerarchia, per consentire il bilanciamento del carico delle richieste di certificati è possibile installare più istanze di questo ruolo in uno o più siti della stessa gerarchia. Quando esistono più istanze in una gerarchia, i client vengono assegnati in modo casuale a uno dei punti di registrazione certificati.  

     Ogni punto di registrazione certificati richiede l'accesso a un'istanza separata di un servizio Registrazione dispositivi di rete. È possibile configurare due o più punti di registrazione certificati per usare lo stesso servizio Registrazione dispositivi di rete. Il punto di registrazione certificati non deve inoltre essere installato sullo stesso server che esegue il servizio Registrazione dispositivi di rete.  

- **Punto di connessione del gateway di gestione cloud**: ruolo del sistema del sito per la comunicazione con il [gateway di gestione cloud](/sccm/core/clients/manage/setup-cloud-management-gateway). 

-   **Punto di distribuzione** : ruolo del sistema del sito che contiene file di origine per i client da scaricare, come contenuto di applicazioni, pacchetti software, aggiornamenti software, immagini del sistema operativo e immagini d'avvio. Per impostazione predefinita, questo ruolo viene installato nel computer del server del sito dei nuovi siti primari e secondari quando viene installato il sito, ma non è supportato in un sito di amministrazione centrale.  È possibile installare più istanze di questo ruolo in un sito supportato e in più siti della stessa gerarchia.  Per altre informazioni, vedere [Concetti di base per la gestione dei contenuti in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Punto di stato di fallback** : ruolo del sistema del sito che consente di monitorare l'installazione client e di identificare i client che non sono gestiti perché non possono comunicare con il relativo punto di gestione.  Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito e in più siti della stessa gerarchia.  Per altre informazioni, vedere [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).


-   **Punto di Endpoint Protection**: ruolo di sistema del sito che Configuration Manager usa per accettare le condizioni di licenza di Endpoint Protection e per configurare l'appartenenza predefinita per Cloud Protection Service (precedentemente nota come Microsoft Active Protection Service). Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale. Per altre informazioni, vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Punto di registrazione**: ruolo di sistema del sito che usa i certificati PKI per Configuration Manager per registrare i dispositivi mobili e i computer Mac. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Se un utente registra dispositivi mobili tramite Configuration Manager e il relativo account di Active Directory si trova in una foresta considerata non attendibile dalla foresta del server del sito, è necessario installare un punto di registrazione nella foresta dell'utente che consenta l'autenticazione dell'utente.  

-   **Punto proxy di registrazione**: ruolo di sistema del sito che gestisce le richieste di registrazione di Configuration Manager provenienti da dispositivi mobili e computer Mac. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Quando vengono supportati dispositivi mobili su Internet, installare il punto proxy di registrazione in una rete perimetrale e il punto di registrazione sulla intranet come procedura di sicurezza consigliata.  

-   **Connettore Exchange Server**: per informazioni, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Punto di gestione** : ruolo del sistema del sito che invia informazioni sui criteri e sulla posizione del servizio ai client e riceve da essi i dati di configurazione.  
    Per impostazione predefinita, questo ruolo viene installato nel computer del server del sito dei nuovi siti primari e secondari quando viene installato il sito. I siti primari supportano più istanze di questo ruolo, mentre i siti secondari supportano un unico punto di gestione che invia ai client un punto di contatto locale per ottenere criteri per computer e utenti. Un punto di gestione nel sito secondario viene chiamato punto di gestione proxy.  

     I punti di gestione possono essere configurati per supportare HTTP o HTTPS e i dispositivi mobili gestiti con la gestione dei dispositivi mobili locale di System Center Configuration Manager. È possibile usare [repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) per ridurre il carico della CPU sul server di database del sito derivante dai punti di gestione quando gestiscono le richieste provenienti dai client.  

-   **Punto di Reporting Services**: ruolo di sistema del sito che si integra con SQL Server Reporting Services per creare e gestire report per Configuration Manager. Questo ruolo è supportato nei siti primari e nel sito di amministrazione centrale ed è possibile installarne più istanze in un sito supportato. Per altre informazioni, vedere [Pianificazione per la creazione di report in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Punto di connessione del servizio**: ruolo di sistema del sito usato per gestire i dispositivi mobili con Microsoft Intune e MDM locale. Questo ruolo carica anche i dati di utilizzo dal sito ed è necessario per rendere disponibili gli aggiornamenti per Configuration Manager nella console di Configuration Manager. Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Punto di aggiornamento software**: ruolo di sistema del sito che si integra con Windows Server Update Services (WSUS) per offrire aggiornamenti software ai client di Configuration Manager. Questo ruolo è supportato in tutti i siti:  

    -   Installare questo sistema del sito nel sito di amministrazione centrale per la sincronizzazione con Windows Server Update Services.  

    -   Configurare ogni istanza di questo ruolo nei siti primari figlio per la sincronizzazione con il sito di amministrazione centrale.  

    -   Valutare la possibilità di installare un punto di aggiornamento software nei siti secondari se il trasferimento dei dati nella rete risulta lento.  

    Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Punto di migrazione stato** : ruolo del sistema del sito che archivia i dati sullo stato dell'utente quando viene eseguita la migrazione di un computer in un nuovo sistema operativo. Questo ruolo è supportato nei siti primari e secondari ed è possibile installarne più istanze in un sito e in più siti della stessa gerarchia. Per altre informazioni sulla memorizzazione dello stato utente durante la distribuzione di sistemi operativi, vedere [Gestire lo stato utente in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Punto di Convalida integrità sistema**: questo ruolo di sistema del sito non è più usato con System Center Configuration Manager anche se rimane visibile nella console di Configuration Manager.  

##  <a name="a-namebkmkproxya-site-system-roles-that-can-use-a-proxy-server"></a><a name="bkmk_proxy"></a> Ruoli del sistema del sito che possono usare un server proxy  
 Alcuni ruoli di sistema del sito di Configuration Manager richiedono connessioni a Internet e usano un server proxy se il server di sistema del sito che ospita il ruolo è configurato con questa opzione. In genere, questa connessione viene eseguita nel contesto del **sistema** del computer in cui è installato il ruolo del sistema del sito e non può usare una configurazione proxy per gli account utente tipici. Quando un server proxy è necessario per completare una connessione a Internet, il computer deve essere configurato per l'utilizzo di un server proxy:  

-   È possibile configurare un server proxy quando si installa un ruolo del sistema del sito.  

-   È possibile aggiungere o modificare una configurazione del server proxy quando si usa la console di Configuration Manager.  

-   Tutti i ruoli del sistema del sito in un server del sistema del sito che può usare una configurazione del server proxy usano la stessa configurazione del server proxy. Se sono richiesti ruoli del sistema del sito diversi per usare server proxy differenti, è necessario installare i ruoli del sistema del sito in computer del server del sistema del sito distinti  

-   Se si modifica la configurazione del server proxy o si installa un nuovo ruolo del sistema del sito in un computer che ha già una configurazione del server proxy, la configurazione originale viene sovrascritta.  


Per le procedure di configurazione del server proxy per i ruoli del sistema del sito, vedere l'argomento [Aggiungere ruoli del sistema del sito per System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

I ruoli del sistema del sito seguenti possono usare un server proxy:  

-   **Punto di sincronizzazione di Asset Intelligence** : questo ruolo del sistema del sito si connette a Microsoft e usa una configurazione del server proxy nel computer che ospita il punto di sincronizzazione di Asset Intelligence.  

-   **Punto di distribuzione basato sul cloud** : quando si usa un punto di distribuzione basato sul cloud, il sito primario che lo gestisce deve potersi connettere a Microsoft Azure per eseguire il provisioning, il monitoraggio e la distribuzione del contenuto nel punto di distribuzione. Se è necessario un server proxy per questa connessione, occorre configurare il server proxy sul server del sito primario. Non è possibile configurare un server proxy nel punto di distribuzione basato su cloud in Windows Azure.  Per altre informazioni, vedere la sezione relativa alla [configurazione delle impostazioni proxy per i siti primari che gestiscono servizi cloud](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) nell'argomento sull'[installazione dei punti di distribuzione basati sul cloud in Microsoft Azure per System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Connettore Exchange Server** : questo ruolo del sistema del sito si connette a Exchange Server e usa una configurazione del server proxy nel computer che ospita il connettore Exchange Server.  

-   **Punto di aggiornamento software** : questo ruolo del sistema del sito può richiedere connessioni a Microsoft Update per scaricare le patch e sincronizzare le informazioni sugli aggiornamenti. In genere, quando si configura il server proxy, ogni ruolo del sistema del sito sul computer che supporta l'utilizzo del server proxy non richiederà alcuna configurazione aggiuntiva per tale utilizzo. Un'eccezione al riguardo è rappresentata dal punto di aggiornamento software. Per impostazione predefinita, un punto di aggiornamento software non usa un server proxy disponibile a meno che non vengano abilitate anche le seguenti opzioni durante la configurazione di tale punto:  

    -   **Usa un server proxy durante la sincronizzazione degli aggiornamenti software**  

    -   **Usare un server proxy quando si scaricano contenuti tramite le regole di distribuzione automatica**  

    > [!TIP]  
    >  Prima di poter selezionare una delle due opzioni, è necessario che un server proxy sia configurato nel server del sistema del sito che ospita il punto di aggiornamento software. Il server proxy viene usato solo per le opzioni specifiche selezionate.  

 Per altre informazioni sui server proxy per i punti di aggiornamento software, vedere la sezione Impostazioni del server proxy nell'argomento [Installare un punto di aggiornamento del software](../../../sum/get-started/install-a-software-update-point.md).  

-   **Punto di connessione del servizio**: se è configurato per essere online (non offline), questo ruolo di sistema del sito si connette a Microsoft Intune e al servizio cloud Microsoft.  



<!--HONumber=Dec16_HO3-->


