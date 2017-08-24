---
title: Pianificare i server e i ruoli del sistema | Documentazione Microsoft
description: Prendere in considerazione i server di sistema del sito e i ruoli di sistema del sito quando si pianifica la gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
caps.latest.revision: "11"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3704a2d3b75ed7e0a7f718b681448ab6fc078d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Pianificare i server e i ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Ogni sito di System Center Configuration Manager installato include un server del sito, ovvero un **server di sistema del sito**. Il sito può includere anche altri server del sistema del sito nei computer remoti rispetto al server del sito. I server del sistema del sito, ovvero il server del sito o un server del sistema del sito remoto, supportano i **ruoli del sistema del sito**.


##  <a name="bkmk_siteservers"></a> Server del sistema del sito  
 Quando si installa un ruolo del sistema del sito in un computer, il computer diventa un server del sistema del sito. In ogni sito è possibile installare uno o più server del sistema del sito aggiuntivi. Si può anche scegliere di non installare altri server del sistema del sito ed eseguire tutti i ruoli del sistema del sito direttamente nel computer del server del sito. Ogni server di sistema del sito supporta uno o più ruoli del sistema del sito. I server supplementari possono essere utili per espandere le funzionalità e la capacità di un sito condividendo il carico di elaborazione della CPU derivante dai ruoli del sistema del sito in un server.  

 Quando si valuta se aggiungere un server del sistema del sito, verificare che il server soddisfi i prerequisiti per l'uso previsto. È consigliabile aggiungere un percorso di rete con larghezza di banda sufficiente per comunicare con gli endpoint previsti, inclusi il server del sito, le risorse di dominio, un percorso basato sul cloud, i server del sistema del sito e i client.  

 Se si configura il server del sistema del sito con un proxy usato dai ruoli del sistema del sito, vedere [Ruoli del sistema del sito che possono usare un server proxy](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Site system roles  
 I ruoli del sistema del sito vengono installati in un computer per fornire altre funzionalità al sito. Alcuni esempi:  

-   Punti di gestione aggiuntivi in modo tale che il sito possa supportare più dispositivi, fino alla capacità supportata del sito.  

-   Punti di distribuzione aggiuntivi per espandere l'infrastruttura del contenuto, migliorando le prestazioni delle distribuzioni di contenuto a utenti e dispositivi.  

-   Uno o più ruoli del sistema del sito specifici per le funzionalità. Ad esempio, un punto di aggiornamento software consente di gestire gli aggiornamenti software per i dispositivi gestiti oppure un punto di Reporting Services consente di eseguire report per monitorare e comprendere o condividere le informazioni relative alla distribuzione.  


Vari siti di Configuration Manager possono supportare diversi set di ruoli di sistema del sito. Il set di ruoli del sistema del sito supportato dipende dal tipo di sito, ad esempio un sito di amministrazione centrale, un sito primario o un sito secondario. La topologia della gerarchia può limitare l'uso di alcuni ruoli a determinati tipi di sito. Ad esempio, il punto di connessione del servizio è supportato solo nel sito di livello superiore della gerarchia, che può essere un sito di amministrazione centrale o un sito primario autonomo. Questo ruolo non è supportato in un sito primario figlio o nei siti secondari.  

Dopo l'installazione di un sito, è possibile spostare la posizione di alcuni ruoli del sistema del sito dalla posizione predefinita nel server del sito a un altro server. Questo vale ad esempio per il punto di gestione o il punto di distribuzione installato per impostazione predefinita in un server del sito primario o secondario. È anche possibile installare altre istanze di alcuni ruoli del sistema del sito per espandere le funzionalità del sito, ovvero fornire altri servizi ai client, e per soddisfare i requisiti aziendali. Alcuni ruoli sono obbligatori, mentre altri sono facoltativi.  

-   **Server del sito di Configuration Manager.** Questo ruolo identifica il server in cui viene eseguito il programma di installazione di Configuration Manager per installare un sito oppure il server in cui viene installato un sito secondario. Questo ruolo non può essere spostato o disinstallato finché non viene disinstallato il sito.  

-   **Sistema del sito di Configuration Manager.** Questo ruolo viene assegnato a qualsiasi computer in cui si installa un sito o un ruolo del sistema del sito. Questo ruolo non può essere spostato o disinstallato finché l'ultimo ruolo del sistema del sito non viene rimosso dal computer.  

-   **Ruolo del sistema del sito del componente di Configuration Manager.** Questo ruolo identifica un sistema del sito che esegue un'istanza del servizio SMS Executive ed è necessario per supportare altri ruoli, ad esempio i punti di gestione. Questo ruolo non può essere spostato o disinstallato finché l'ultimo ruolo del sistema del sito applicabile non viene rimosso dal computer.  

-   **Server di database del sito di Configuration Manager.** Questo ruolo viene assegnato ai server di sistema del sito che mantengono un'istanza del database del sito per un sito. Questo ruolo può essere spostato solo in un nuovo server modificando il sito in modo che usi un'altra istanza di SQL Server per ospitare il database del sito.  

-   **Provider SMS.** Questo ruolo viene assegnato a ogni computer che ospita un'istanza del provider SMS, l'interfaccia tra una console di Configuration Manager e il database del sito. Per impostazione predefinita, questo ruolo viene installato automaticamente nel server del sito di un sito di amministrazione centrale e nei siti primari. È possibile installare altre istanze in ogni sito per fornire l'accesso ad altri utenti amministratori.  

     Per installare altri provider, è necessario eseguire il programma di installazione di Configuration Manager per [gestire il provider SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Quindi installare altri provider in computer aggiuntivi. È possibile installare solo un'istanza del provider SMS in un computer e tale computer deve essere nello stesso dominio del server del sito.  

-   **Punto per servizi Web del Catalogo applicazioni.** Ruolo del sistema del sito che fornisce informazioni sul software per il sito Web del Catalogo applicazioni dalla Raccolta software. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

-   **Punto per siti Web del Catalogo applicazioni.** Ruolo del sistema del sito che offre agli utenti un elenco dei software disponibili dal Catalogo applicazioni. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Quando il Catalogo applicazioni supporta computer client su Internet, installare il punto per siti Web del Catalogo applicazioni in una rete perimetrale e il punto per servizi Web del Catalogo applicazioni sulla Intranet come procedura di sicurezza consigliata.  

-   **Punto di sincronizzazione di Asset Intelligence.** Ruolo del sistema del sito che si connette a Microsoft per scaricare informazioni sul catalogo di Asset Intelligence. Questo ruolo carica anche i titoli senza categoria in modo che possano essere presi in considerazione per una futura inclusione nel catalogo. Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale.   Per altre informazioni, vedere [Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Punto di registrazione certificati.** Ruolo del sistema del sito che comunica con un server in cui è in esecuzione il servizio Registrazione dispositivi di rete. Questo ruolo gestisce le richieste di certificato del dispositivo che usano il protocollo Simple Certificate Enrollment Protocol (SCEP). Questo ruolo è supportato solo nei siti primari e nel sito di amministrazione centrale.

     Anche se un unico punto di registrazione certificati può fornire funzionalità a un'intera gerarchia, può essere opportuno installare più istanze di questo ruolo in uno o più siti della stessa gerarchia. Questo è utile per il bilanciamento del carico. Quando esistono più istanze in una gerarchia, i client vengono assegnati in modo casuale a uno dei punti di registrazione certificati.  

     Ogni punto di registrazione certificati richiede l'accesso a un'istanza separata di un servizio Registrazione dispositivi di rete. È possibile configurare due o più punti di registrazione certificati per usare lo stesso servizio Registrazione dispositivi di rete. Il punto di registrazione certificati non deve inoltre essere installato sullo stesso server che esegue il servizio Registrazione dispositivi di rete.  

- **Punto di connessione del gateway di gestione cloud.** Ruolo del sistema del sito per la comunicazione con il [gateway di gestione cloud](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Punto di distribuzione.** Ruolo del sistema del sito che contiene file di origine per i client da scaricare, come contenuto di applicazioni, pacchetti software, aggiornamenti software, immagini del sistema operativo e immagini d'avvio. Per impostazione predefinita, questo ruolo viene installato nel computer del server del sito dei nuovi siti primari e secondari quando viene installato il sito. Questo ruolo non è supportato in un sito di amministrazione centrale. È possibile installare più istanze di questo ruolo in un sito supportato e in più siti della stessa gerarchia. Per altre informazioni, vedere [Concetti di base per la gestione dei contenuti in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) e [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Punto di stato di fallback.** Ruolo del sistema del sito che consente di monitorare l'installazione client e di identificare i client che non sono gestiti perché non possono comunicare con il relativo punto di gestione. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito e in più siti della stessa gerarchia.     


-   **Punto di Endpoint Protection.** Ruolo del sistema del sito che Configuration Manager usa per accettare le condizioni di licenza di Endpoint Protection e per configurare l'appartenenza predefinita per Cloud Protection Service. Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale. Per altre informazioni, vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Punto di registrazione.** Ruolo del sistema del sito che usa i certificati PKI affinché Configuration Manager registri i dispositivi mobili e i computer Mac. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Se un utente registra dispositivi mobili tramite Configuration Manager e il relativo account di Active Directory si trova in una foresta considerata non attendibile dalla foresta del server del sito, è necessario installare un punto di registrazione nella foresta dell'utente. L'utente può quindi essere autenticato.  

-   **Punto proxy di registrazione.** Ruolo del sistema del sito che gestisce le richieste di registrazione di Configuration Manager provenienti da dispositivi mobili e computer Mac. Anche se questo ruolo è supportato solo nei siti primari, è possibile installarne più istanze in un sito o in più siti della stessa gerarchia.  

     Quando vengono supportati dispositivi mobili su Internet, installare il punto proxy di registrazione in una rete perimetrale per sicurezza e il punto di registrazione sulla Intranet.  

-   **Connettore Exchange Server.** Per altre informazioni su questo ruolo, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   **Punto di gestione.** Ruolo del sistema del sito che invia informazioni sui criteri e sulla posizione del servizio ai client e riceve da essi i dati di configurazione.  

    Per impostazione predefinita, questo ruolo viene installato nel computer del server del sito dei nuovi siti primari e secondari quando viene installato il sito. I siti primari supportano più istanze di questo ruolo. I siti secondari supportano un unico punto di gestione che invia ai client un punto di contatto locale per ottenere i criteri per computer e utenti. Un punto di gestione nel sito secondario viene chiamato punto di gestione proxy.  

     I punti di gestione possono essere configurati per supportare HTTP o HTTPS e i dispositivi mobili gestiti con la gestione dei dispositivi mobili locale di System Center Configuration Manager. È possibile usare [repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) per ridurre il carico della CPU sul server di database del sito derivante dai punti di gestione quando gestiscono le richieste provenienti dai client.  

-   **Punto di Reporting Services.** Ruolo del sistema del sito che si integra con SQL Server Reporting Services per creare e gestire rapporti per Configuration Manager. Questo ruolo è supportato nei siti primari e nel sito di amministrazione centrale ed è possibile installarne più istanze in un sito supportato. Per altre informazioni, vedere [Pianificazione per la creazione di report in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Punto di connessione del servizio.** Ruolo del sistema del sito usato per gestire i dispositivi mobili con Microsoft Intune e MDM locale. Questo ruolo carica anche i dati di utilizzo dal sito ed è necessario per rendere disponibili gli aggiornamenti per Configuration Manager nella console di Configuration Manager. Una gerarchia supporta una sola istanza di questo ruolo, che deve trovarsi nel sito di livello superiore della gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo. Se si espande il sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale. Per ulteriori informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Punto di aggiornamento software.** Ruolo del sistema del sito che si integra con Windows Server Update Services (WSUS) per fornire aggiornamenti software ai client di Configuration Manager. Questo ruolo è supportato in tutti i siti:  

    -   Installare questo sistema del sito nel sito di amministrazione centrale per la sincronizzazione con WSUS.  

    -   Configurare ogni istanza di questo ruolo nei siti primari figlio per la sincronizzazione con il sito di amministrazione centrale.  

    -   Valutare la possibilità di installare un punto di aggiornamento software nei siti secondari se il trasferimento dei dati nella rete risulta lento.  

    Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Punto di migrazione stato.** Ruolo del sistema del sito che memorizza i dati sullo stato utente quando viene eseguita la migrazione di un computer a un nuovo sistema operativo. Questo ruolo è supportato nei siti primari e nei siti secondari. È possibile installare più istanze di questo ruolo in un sito e in più siti della stessa gerarchia. Per altre informazioni sulla memorizzazione dello stato utente durante la distribuzione di sistemi operativi, vedere [Gestire lo stato utente in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Punto di Convalida integrità sistema.** Questo ruolo del sistema del sito non è più usato, anche se rimane visibile nella console di Configuration Manager.  

###  <a name="bkmk_proxy"></a> Ruoli del sistema del sito che possono usare un server proxy  
 Alcuni ruoli di sistema del sito di Configuration Manager richiedono connessioni a Internet e usano un server proxy se il server di sistema del sito che ospita il ruolo è configurato con questa opzione. In genere, questa connessione viene eseguita nel contesto del **sistema** del computer in cui è installato il ruolo del sistema del sito. La connessione non può usare una configurazione proxy per gli account utente tipici. Quando un server proxy è necessario per completare una connessione a Internet, il computer deve essere configurato per l'uso di un server proxy:  

-   È possibile configurare un server proxy quando si installa un ruolo del sistema del sito.  

-   È possibile aggiungere o modificare una configurazione del server proxy quando si usa la console di Configuration Manager.  

-   Viene usata la stessa configurazione del server proxy per tutti i ruoli del sistema del sito in un server del sistema del sito che può usare una configurazione del server proxy. Se sono richiesti ruoli del sistema del sito diversi per usare server proxy differenti, è necessario installare i ruoli del sistema del sito su computer del server del sistema del sito differenti.  

-   Se si modifica la configurazione del server proxy o si installa un nuovo ruolo del sistema del sito in un computer che ha già una configurazione del server proxy, la configurazione originale viene sovrascritta.  


Per le procedure di configurazione del server proxy per i ruoli del sistema del sito, vedere l'argomento [Aggiungere ruoli del sistema del sito per System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

I ruoli del sistema del sito seguenti possono usare un server proxy:  

-   **Punto di sincronizzazione di Asset Intelligence.** Questo ruolo del sistema del sito si connette a Microsoft e usa una configurazione del server proxy sul computer che ospita il punto di sincronizzazione di Asset Intelligence.  

-   **Punto di distribuzione basato sul cloud.** Quando si usa un punto di distribuzione basato sul cloud, il sito primario che lo gestisce deve potersi connettere a Microsoft Azure per effettuare il provisioning, il monitoraggio e la distribuzione del contenuto al punto di distribuzione. Se è necessario un server proxy per questa connessione, occorre configurarlo sul server del sito primario. Non è possibile configurare un server proxy nel punto di distribuzione basato sul cloud in Azure. Per altre informazioni, vedere la sezione [Configurare le impostazioni proxy per i siti primari che gestiscono servizi cloud](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) nell'argomento [Installare punti di distribuzione basati sul cloud in Microsoft Azure per System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Connettore Exchange Server.** questo ruolo del sistema del sito si connette a Exchange Server e usa una configurazione del server proxy nel computer che ospita il connettore Exchange Server.  

-   **Punto di aggiornamenti software.** Questo ruolo del sistema del sito può richiedere connessioni a Microsoft Update per scaricare le patch e sincronizzare le informazioni sugli aggiornamenti. In genere, quando si configura il server proxy, ogni ruolo del sistema del sito nel computer che supporta l'uso del server proxy usa il server proxy. Non è richiesta alcuna configurazione aggiuntiva. Un'eccezione al riguardo è rappresentata dal punto di aggiornamento software. Per impostazione predefinita, un punto di aggiornamento software non usa un server proxy disponibile a meno che non vengano abilitate anche le opzioni seguenti durante la configurazione di tale punto:  

    -   **Usa un server proxy durante la sincronizzazione degli aggiornamenti software**  

    -   **Usare un server proxy quando si scaricano contenuti tramite le regole di distribuzione automatica**  

    > [!TIP]  
    >  Prima di poter selezionare una delle due opzioni, è necessario che nel server del sistema del sito che ospita il punto di aggiornamento software sia configurato un server proxy. Il server proxy viene usato solo per le opzioni specifiche selezionate.  

 Per altre informazioni sui server proxy per i punti di aggiornamento software, vedere la sezione "Impostazioni del server proxy" nell'argomento [Installare e configurare un punto di aggiornamento software](../../../sum/get-started/install-a-software-update-point.md).  

-   **Punto di connessione del servizio.** quando è configurato per essere online (non offline), questo ruolo del sistema del sito si connette a Microsoft Intune e al servizio cloud Microsoft.  
