---
title: Aggiornamenti
titleSuffix: Configuration Manager
description: Informazioni su un metodo di manutenzione nella console denominato **Aggiornamenti e manutenzione** che semplifica l'individuazione e l'installazione di aggiornamenti consigliati.
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: "51"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bca724f15dc18d7273bbca122b6428b4704a5d43
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="updates-for-system-center-configuration-manager"></a>Aggiornamenti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager usa un metodo di manutenzione nella console denominato **Aggiornamenti e manutenzione**. Questo metodo nella console semplifica l'individuazione e l'installazione degli aggiornamenti consigliati per l'infrastruttura di Configuration Manager. La manutenzione nella console è integrata dagli aggiornamenti fuori programma, ad esempio hotfix per i clienti che devono risolvere problemi che potrebbero essere specifici dell'ambiente in uso.  

> [!TIP]  
> Quando si gestisce l'infrastruttura del sito e della gerarchia di System Center Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti. Per informazioni su come viene usato ogni termine, vedere [Informazioni su upgrade, aggiornamento e installazione](/sccm/core/understand/upgrade-update-install).


 **Gli argomenti seguenti possono essere utili per capire come individuare e installare i diversi tipi di aggiornamento per System Center Configuration Manager:**  

-   [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) (Installare gli aggiornamenti nella console per System Center Configuration Manager)  

-   [Use the Service Connection Tool for System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) (Usare lo strumento di connessione del servizio per System Center Configuration Manager)  

-   [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) (Usare lo strumento di registrazione dell'aggiornamento per importare hotfix in System Center Configuration Manager)  

-   [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md) (Usare il programma di installazione degli aggiornamenti rapidi per installare gli aggiornamenti per System Center Configuration Manager)  


Se si usa il ramo Technical Preview, vedere [Technical Preview per System Center Configuration Manager](/sccm/core/get-started/technical-preview) per informazioni aggiuntive specifiche relative a tale ramo.


##  <a name="bkmk_Baselines"></a> Versioni di base e di aggiornamento  
 La prima versione di System Center Configuration Manager Current Branch è la 1511, ossia una versione di base. Tra le versioni di base più recenti sono incluse la 1606 e la 1702:

-   Usare la versione di base più recente quando si installa un nuovo sito in una nuova gerarchia.  

-   Per eseguire l'aggiornamento da System Center 2012 Configuration Manager, si usa una versione baseline. Dopo l'aggiornamento a System Center Configuration Manager, non è più possibile usare le versioni baseline per restare aggiornati, ma solo gli [aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates) per l'aggiornamento alla versione più recente.  

-   Periodicamente vengono rilasciate altre versioni baseline. Quando si usa la versione baseline più recente per installare una nuova gerarchia, si evita di installare una versione non aggiornata di Configuration Manager, seguita da un aggiornamento aggiuntivo dell'infrastruttura per aggiornarla.  

Dopo avere installato una versione di base, altre versioni di Configuration Manager sono disponibili come aggiornamenti nella console. Gli aggiornamenti nella console aggiornano l'infrastruttura alla versione più recente di Configuration Manager.  

-   Installare gli aggiornamenti nella console per aggiornare la versione del sito principale.  

-   Gli aggiornamenti installati nel sito di amministrazione centrale vengono installati automaticamente nei siti primari figlio, a meno che non siano bloccati da una finestra di manutenzione configurata nel sito primario.  

-   Si aggiornano manualmente i siti secondari a una nuova versione di aggiornamento dalla console.  

Quando si installa un aggiornamento, questo archivia i file di installazione per la versione nel server del sito, in una cartella denominata CD.Latest. Per altre informazioni su questi file, vedere [Cartella CD.Latest per System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

-   I file nella cartella CD.Latest vengono usati durante il ripristino sito e per installare siti aggiuntivi in una gerarchia che non esegue più una versione baseline.  

-   Non è possibile usare i file di installazione della cartella CD.Latest per installare il primo sito di una nuova gerarchia oppure per aggiornare un sito da System Center 2012 Configuration Manager.  

Alcuni aggiornamenti per Configuration Manager sono disponibili sia come versione di aggiornamento nella console per l'infrastruttura esistente sia come nuova versione di base.  

Le versioni seguenti di Configuration Manager sono disponibili come versione di base, come aggiornamento oppure in entrambe le forme:  

|Versione |Data di disponibilità|[Data di fine supporto](/sccm/core/servers/manage/current-branch-versions-supported) |Versione di base|Aggiornamento nella console|  
|-------------|-----------|------------|--------------|------------------------|  
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|31 luglio 2017|31 luglio 2018|No|Sì|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|27 marzo 2017| 27 marzo 2018|Sì|Sì|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|18 novembre 2016| 18 novembre 2017|No|Sì|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|22 luglio 2016| 22 luglio 2017|No|Sì|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) con aggiornamento rapido cumulativo 1606 (KB3186654) </br></br>5.00.8412.1307 *(nota 1)* |12 ottobre 2016| 12 ottobre 2017|Sì|No|
| 1602<br /><br /> 5.00.8355.1000|11 marzo 2016| 11 marzo 2017|No|Sì| 
| 1511 <br /><br /> 5.00.8325.1000|8 dicembre 2015| 8 dicembre 2016|Sì|No|  


*(Nota 1)* Il supporto di base 1606 e 1702 è disponibile all'interno di Microsoft System Center 2016 o in System Center Configuration Manager (Current Branch e Long-Term Servicing Branch) in [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC). Ad esempio, in VLSC è possibile cercare *System Center Config Mgr (Current Branch e LTSB)*; entrambi i supporti di base delle versioni 1606 e 1702 vengono restituiti e sono disponibili per il download.

Per controllare la versione del sito di Configuration Manager, nella console passare a **Informazioni su System Center Configuration Manager** nell'angolo in alto a sinistra, dove è visualizzata la nuova versione del sito e della console.  

##  <a name="bkmk_inconsole"></a> Aggiornamenti e manutenzione nella console  
 Quando si usa un'installazione di System Center Configuration Manager pronta per l'ambiente di produzione, detta anche Current Branch, la maggior parte degli aggiornamenti da installare è disponibile mediante il canale Aggiornamenti e manutenzione. Questo metodo identifica, scarica e rende disponibili gli aggiornamenti applicabili alla versione e alla configurazione correnti dell'infrastruttura e include solo gli aggiornamenti consigliati da Microsoft a tutti i clienti.   
 Sono inclusi:  

-   Nuove versioni, ad esempio 1610, 1702 o 1706.  

-   Aggiornamenti, che includono nuove funzionalità per la versione corrente.

-   Hotfix, per la versione in uso di Configuration Manager e di cui è consigliata l'installazione a tutti i clienti.

Gli aggiornamenti nella console offrono maggiore stabilità e risolvono i problemi comuni. Sostituiscono i tipi di aggiornamento disponibili per le versioni precedenti del prodotto per quanto riguarda Service Pack, aggiornamenti cumulativi e hotfix applicabili a tutti i clienti, nonché l'estensione per Microsoft Intune. Questi aggiornamenti possono riguardare uno o più degli elementi seguenti:  

-   Server del sito di amministrazione centrale e dei siti primari  

-   Ruoli del sistema del sito e server di sistema del sito  

-   Istanze del provider SMS  

-   Console di Configuration Manager  

-   Client di Configuration Manager  

Configuration Manager individua nuovi aggiornamenti durante la sincronizzazione del ruolo del sistema del sito del punto di connessione del servizio con il servizio cloud di Microsoft e con l'Area download:  

-   Quando il punto di connessione del servizio è in modalità online, il sito si sincronizza con Microsoft ogni giorno per identificare automaticamente i nuovi aggiornamenti applicabili all'infrastruttura.  Per scaricare gli aggiornamenti e i file ridistribuibili per gli aggiornamenti, il computer che ospita il ruolo del sistema del sito Punto di connessione del servizio usa il contesto di **sistema** per accedere ai percorsi Internet seguenti: go.microsoft.com e download.microsoft.com. Per informazioni sui percorsi aggiuntivi ai quali si connette il punto di connessione del servizio, vedere [Internet access requirements](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) (Requisiti per l'accesso a Internet) in [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md) (Informazioni sul punto di connessione del servizio in System Center Configuration Manager).  

-   Quando il punto di connessione del servizio è in modalità offline, è necessario usare lo strumento di connessione del servizio per eseguire manualmente la sincronizzazione con il cloud Microsoft. Per altre informazioni, vedere [Usare lo strumento di connessione del servizio per System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   Grazie agli aggiornamenti nella console non è necessario individuare e installare i singoli aggiornamenti, Service Pack e nuove funzionalità in modo indipendente.  

-   Vengono installati solo gli aggiornamenti nella console scelti e durante l'installazione di alcuni aggiornamenti è possibile selezionare le singole funzionalità da abilitare e usare. Per altre informazioni, vedere [Enable optional features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).  

Quando si installa un aggiornamento nella console:  

-   Viene eseguito automaticamente un controllo dei prerequisiti. È anche possibile eseguire questo controllo prima dell'avvio dell'installazione.  

-   L'installazione viene eseguita automaticamente nel sito di amministrazione centrale, se presente, e nei siti primari. È possibile controllare quando ogni server del sito primario può aggiornare l'infrastruttura usando gli [intervalli di servizio per i server del sito](../../../core/servers/manage/service-windows.md).  

-   Dopo l'aggiornamento di un server del sito, tutti i ruoli del sistema del sito interessati (incluse le istanze del provider SMS) vengono aggiornati automaticamente. Le console di Configuration Manager chiedono all'utente di aggiornare anche la console stessa dopo l'installazione dell'aggiornamento nel sito.  

-   Se un aggiornamento include il client di Configuration Manager, è possibile scegliere se testare l'aggiornamento in pre-produzione oppure applicare immediatamente l'aggiornamento a tutti i client.  

-   Dopo l'aggiornamento di un sito primario, i siti secondari non vengono aggiornati automaticamente. È invece necessario avviare l'aggiornamento del sito secondario.  

> [!NOTE]  
>  La versione per la produzione di Center Configuration Manager (Current Branch), Long Term Servicing Branch e la Technical Preview di System Center Configuration Manager sono versioni diverse. Di conseguenza, gli aggiornamenti relativi a un ramo non sono disponibili come aggiornamenti nella console per gli altri rami. Per altre informazioni sui rami disponibili, vedere [Which branch of Configuration Manager should I use?](/sccm/core/understand/which-branch-should-i-use) (Scelta del ramo di Configuration Manager da usare)

##  <a name="bkmk_outofband"></a> Hotfix fuori programma  
Alcuni hotfix vengono rilasciati con disponibilità limitata per risolvere problemi specifici oppure sono applicabili a tutti i clienti, ma non possono essere installati usando il metodo nella console. Questi aggiornamenti sono rilasciati fuori programma e non vengono individuati dal servizio cloud Microsoft.  

Se si sta tentando di risolvere o correggere un problema relativo alla distribuzione di Configuration Manager, in genere è possibile trovare informazioni sugli hotfix fuori programma nei servizi di assistenza clienti Microsoft, in un articolo della Knowledge Base o nel [blog del team di System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam).  

Installare questi aggiornamenti manualmente, usando uno dei due metodi seguenti:  

-   **Strumento di registrazione dell'aggiornamento:** questo strumento importa manualmente l'hotfix nella console di Configuration Manager da cui è poi possibile installare l'aggiornamento come si farebbe con gli aggiornamenti nella console individuati automaticamente. Questo metodo è usato per gli aggiornamenti con la struttura di nome file seguente: **.update.exe**.  Il nome file completo per questo tipo di hotfix è simile a: **&lt;Prodotto\>-&lt;versione prodotto\>-&lt;ID articolo KB\>-ConfigMgr.Update.exe**.  

     Per altre informazioni, vedere [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) (Usare lo strumento di registrazione dell'aggiornamento per importare hotfix in System Center Configuration Manager).  

-   **Strumento di installazione di hotfix:** questo strumento consente di installare manualmente un hotfix che non è possibile installare usando il metodo nella console. Questo metodo è usato per gli aggiornamenti che hanno la struttura di nome file seguente: **&lt;Prodotto\>-&lt; versione prodotto\>-&lt;ID articolo KB\>-&lt;piattaforma\>-&lt;lingua\>.exe**.

     Per altre informazioni, vedere [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md) (Usare il programma di installazione di hotfix per installare gli aggiornamenti per System Center Configuration Manager).
