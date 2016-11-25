---
title: Scegliere Intune autonomo o MDM per dispositivi ibridi | System Center Configuration Manager e Microsoft Intune
description: Scegliere se distribuire una gestione di dispositivi mobili ibridi con Intune e Configuration Manager o se eseguire Intune autonomamente.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Scegliere tra Microsoft Intune autonomo e la gestione di dispositivi mobili ibridi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Una delle domande più frequenti sulla Gestione di dispositivi mobili con Microsoft Intune è: "È consigliabile la Gestione di dispositivi mobili ibridi con Intune e Configuration Manager o eseguire Intune autonomo nella configurazione che prevede solo il cloud?" È una decisione importante poiché non è facilmente reversibile dopo l'implementazione.  

 La distribuzione di Intune autonomo non richiede infrastrutture locali e viene gestita tramite una console Web. Si tratta di una soluzione agile e leggera, diffuso tra le organizzazioni incentrate sul cloud.  

 Una distribuzione MDM per dispositivi ibridi include Intune e Configuration Manager e viene gestita tramite strumenti familiari agli amministratori esperti di Configuration Manager. Essa offre gestione tramite pannello di controllo unificato per MDM e client tradizionali, nonché scalabilità per ambienti di grandi dimensioni.  

##  <a name="what-does-intune-standalone-mean"></a>Che cosa significa Intune autonomo?  
 Intune è essenzialmente un servizio cloud. I data center di Intune sono ospitati in America del Nord, Europa e Asia e forniscono ai dispositivi mobili criteri di sicurezza, profili di posta elettronica e Wi-Fi, applicazioni, inventario e altro ancora.  

 L'implementazione di Intune autonomo non richiede alcuna infrastruttura locale. Configurazione, gestione, distribuzione e creazione di report vengono eseguiti tramite una console basata sul Web, accessibile da qualsiasi parte del mondo.  

 Per l'uso con applicazioni locali, ad esempio Microsoft Exchange e il servizio Registrazione dispositivi di rete (NDES), sono disponibili connettori locali per fornire connettività al servizio Intune.  

 Essendo un servizio cloud, Intune può essere compilato e distribuito in breve tempo.  

##  <a name="what-does-hybrid-mdm-mean"></a>Che cosa significa MDM per dispositivi ibridi?  
 Per le organizzazioni che desiderano ottimizzare l'investimento di Configuration Manager, per i clienti che necessitano di un controllo accurato o per i clienti che superano i limiti di scalabilità di Intune, è disponibile un'implementazione ibrida che si serve di Intune per gestire i dispositivi mobili.  

 Le distribuzioni ibride richiedono Microsoft System Center 2012 Configuration Manager SP1 o versione successiva.  

 Il servizio Intune è connesso a Configuration Manager con ruolo di sistema del sito del punto di connessione del servizio, formalmente noto come Microsoft Intune Connector, installato nel sito di amministrazione centrale o nel sito primario di una gerarchia di Configuration Manager. È possibile connettere un tenant di Intune solo a una gerarchia di Configuration Manager ed è possibile connettere una gerarchia di Configuration Manager solo a un tenant di Intune.  

 In una configurazione di MDM per dispositivi ibridi, alcuni degli overhead di archiviazione ed elaborazione vengono eseguiti dall'infrastruttura locale di Configuration Manager. Questo miglioramento dell'efficienza consente alla MDM per dispositivi ibridi di apportare scalabilità aggiuntiva a Intune autonomo.  

 La distribuzione ibrida consente di usare strumenti familiari agli amministratori di Configuration Manager. Le funzionalità avanzate, come il Controllo degli accessi in base al ruolo (RBAC), SQL Server Reporting Services (SSRS) e il raggruppamento complesso di utenti e dispositivi che usano query di appartenenza alla raccolta, diventano disponibili per i dispositivi mobili all'implementazione della MDM per dispositivi ibridi.  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>Opzioni di pianificazione e tempi per la distribuzione di Intune  
 Si assiste a una rapida evoluzione e innovazione di Intune, che comprende aggiornamenti mensili che offrono funzionalità nuove o migliorate, scalabilità avanzata, nuove esperienze per la console di amministrazione tramite il portale di Azure, gruppi dinamici tramite Azure Active Directory e altro ancora. Di conseguenza, le decisioni sulla progettazione devono tenere conto dell'orientamento futuro del prodotto.  

 Molte delle speciali funzionalità attualmente offerte dall'implementazione ibrida verranno funzionalmente replicate in Intune autonomo durante lo sviluppo del prodotto su breve, medio e lungo termine.  

 Se l'utente è in procinto di scegliere tra la distribuzione autonoma e la distribuzione ibrida, deve prendere in considerazione i tempi di distribuzione. Spesso si verifica che gli utenti debbano ripetere l'implementazione diverse volte. Ciò implica una nuova progettazione, compilazione, nuovi test di accettazione utente e nuove fasi pilota, che in genere richiedono numerosi mesi prima che possano essere distribuiti nell'ambiente di produzione. Per questo motivo, quando si sceglie la struttura della gerarchia Intune, è opportuno valutare il momento in cui procedere alla distribuzione effettiva e considerare le prospettive del servizio sul breve, medio e lungo termine.  

 Con l'evoluzione del servizio Intune, intendiamo semplificare la scelta della configurazione. In futuro, l'unico motivo per scegliere un ambiente MDM ibrido deve essere la necessità dei clienti di un'unica console di gestione per client tradizionali e dispositivi mobili.  Ci impegniamo molto per migliorare la scalabilità, aggiungendo accesso basato sui ruoli tramite il portale di Azure e gruppi dinamici tramite una maggiore integrazione di Azure Active Directory, distribuendoli con aggiornamenti del sito sul breve e medio termine.  

 Infine, stiamo anche lavorando per garantire che, indipendentemente dalla scelta di configurazione, l'utente sia in grado di spostarsi facilmente tra configurazione ibrida e autonoma senza difficoltà. Il cambiamento dell'autorità MDM oggi richiede l'intervento manuale dal supporto Microsoft e notevole impegno da parte del tenant. Per semplificare l'operazione, il nostro obiettivo è consentire la coesistenza di configurazione ibrida e Intune autonomo, che consenta agli utenti di spostarsi tra i due tipi di gestione, senza dover scegliere una delle due configurazioni.  Questa modifica rimuove anche la necessità attuale dell'intervento del supporto, nonché l'esigenza di annullare la registrazione e procedere a nuova registrazione dei dispositivi.  

##  <a name="pros-and-cons-of-intune-standalone"></a>Vantaggi e svantaggi di Intune autonomo  

|Vantaggi|Svantaggi|  
|----------|----------|  
|Distribuzione e compilazione rapide<br /><br /> Infrastruttura non in locale<br /><br /> Aggiornamenti e versioni di funzionalità con rilascio più frequente<br /><br /> Curva di apprendimento lenta<br /><br /> Console di amministrazione disponibile esternamente|Funzionalità di reporting limitate<br /><br /> Restrizione sul ruolo di sicurezza<br /><br /> Nessuno strumento esterno (ad esempio PowerShell, ecc.)<br /><br /> Inventario app limitato<br /><br /> Funzionalità di base per il raggruppamento di utenti e dispositivi<br /><br /> Silverlight obbligatorio|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>Vantaggi e svantaggi della MDM per dispositivi ibridi  

|Vantaggi|Svantaggi|  
|----------|----------|  
|Funzionalità di scalabilità<br /><br /> Strumenti avanzati (ad esempio, console di Configuration Manager, PowerShell, registrazione, ecc.)<br /><br /> Controllo dell'accesso basato sui ruoli (RBAC)<br /><br /> Report avanzati<br /><br /> Gestione da pannello di controllo unificato per MDM + client tradizionali<br /><br /> Inventario app esteso<br /><br /> Raggruppamento avanzato per utenti e dispositivi<br /><br /> Supporto di un numero maggiore di connettori Exchange locali e online<br /><br /> Supporto di un numero maggiore di ruoli NDES/CRP<br /><br /> Possibilità di contrassegnare i dispositivi come "di proprietà dell'azienda"<br /><br /> Maggiori capacità di risoluzione dei problemi<br /><br /> Licenze CAL per utenti di Configuration Manager incluse nella sottoscrizione|Complessità locale (configurazione e gestione)<br /><br /> Curva di apprendimento ripida<br /><br /> Manutenzione necessaria per gli aggiornamenti e le nuove funzionalità<br /><br /> Requisiti di licenza aggiuntivi (ad esempio Windows, SQL Server, ecc.)|  

##  <a name="planning-decisions"></a>Decisioni relative alla pianificazione  
 ![ibridi&#45;decisioni](../../mdm/understand/media/hybrid-decisions.png)  

|Passaggio|Decisione|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**Quanti dispositivi si prevede di gestire?**<br /><br /> Intune autonomo supporta fino a 50.000 dispositivi. MDM per dispositivi ibridi supporta fino a 300.000 dispositivi.<br /><br /> Per le distribuzioni di grandi dimensioni, autonome o MDM per dispositivi ibridi, è consigliabile contattare il team degli account Microsoft. Il team degli account Microsoft può mettere l'utente in contatto con gli specialisti Intune, i quali sono in grado di spiegare nel dettaglio le questioni relative a scalabilità e limitazioni.|  
|![ibridi&#45;2](../../mdm/understand/media/hybrid-2.png)|**È necessario il controllo granulare degli accessi? (RBAC)**<br /><br /> Il Controllo degli accessi in base al ruolo (RBCA) è stato aggiunto a System Center 2012 Configuration Manager. RBAC consente agli amministratori di Configuration Manager di progettare e distribuire set di autorizzazioni complessi per limitare l'accesso amministrativo alle funzioni e agli oggetti di Configuration Manager.<br /><br /> Intune autonomo fornisce solo due ruoli di amministratore: accesso completo e accesso in sola lettura.<br /><br /> Se l'organizzazione deve definire l'ambito di alcuni amministratori su determinati utenti, dispositivi, funzioni o oggetti, è necessario Configuration Manager con RBAC.<br /><br /> Se l'organizzazione dispone di un piccolo team di amministrazione e non necessita della complessità del controllo di accesso granulare, la soluzione ottimale è Intune con ruoli di sicurezza incorporati.|  
|![ibridi&#45;3](../../mdm/understand/media/hybrid-3.png)|**Sono necessarie le funzionalità avanzate di reporting?**<br /><br /> MDM per dispositivi ibridi con Configuration Manager include funzionalità di reporting avanzate tramite SQL Server Reporting Services (SSRS). Configuration Manager include 34 report MDM incorporati e oltre 400 report standard di Configuration Manager. SSRS consente anche agli amministratori e ai business analyst di scrivere report personalizzati. Il database di Configuration Manager può anche ricevere query da strumenti esterni, ad esempio strumenti di orchestrazione, per fornire funzioni specifiche, come gli avvisi personalizzati. Tutti i report eseguiti da Configuration Manager possono includere anche dati non MDM, ad esempio inventari PC tradizionali affiancati a inventari di dispositivi mobili.<br /><br /> Intune autonomo fornisce 9 report. Questi report non sono personalizzabili e offrono variabili di input limitate. I report possono essere stampati o esportati in formato CSV o HTML.<br /><br /> Se l'organizzazione richiede funzioni avanzate per la creazione di report e dispone di larghezza di banda e competenza per gestire SSRS, la soluzione ottimale è MDM per dispositivi ibridi.<br /><br /> Se l'organizzazione desidera un motore di creazione di report semplice da usare e report predefiniti, la funzionalità di creazione di report di Intune autonomo dovrebbe risultare sufficiente.|  
|![ibridi&#45;4](../../mdm/understand/media/hybrid-4.png)|**Vengono gestiti dispositivi Windows 10 senza accesso a Internet?**<br /><br /> In Configuration Manager (ramo corrente), i dispositivi Windows 10 possono essere gestiti tramite il canale MDM usando solo l'infrastruttura locale.<br /><br /> La funzionalità Gestione di dispositivi mobili locale è progettata per consentire la gestione MDM per i client che non dispongono di accesso a Internet ed è principalmente destinata a dispositivi monouso, ad esempio i dispositivi kiosk, e dispositivi IoT.<br /><br /> A causa dell'approccio esclusivamente cloud di Intune autonomo, tutti i dispositivi gestiti devono avere accesso a Internet. Se l'organizzazione desidera gestire i dispositivi Windows 10 tramite Gestione di dispositivi mobili locale, è necessaria una configurazione MDM per dispositivi ibridi. Si noti che Gestione di dispositivi mobili locale non supporta la gestione simultanea di dispositivi mobili Internet e intranet.|  
|![ibridi&#45;5](../../mdm/understand/media/hybrid-5.png)|**È necessario l'inventario completo delle app?**<br /><br /> Per impostazione predefinita, Intune autonomo raccoglie solo l'inventario delle app per le applicazioni gestite e distribuite da Intune. Questo significa che i report di inventario non conterranno informazioni sulle applicazioni sottoposte a sideload e installate da utenti esterni al portale aziendale di Intune.<br /><br /> MDM per dispositivi ibridi con Configuration Manager consente agli amministratori di designare alcuni dispositivi come "di proprietà dell'azienda". Quando un dispositivo viene impostato come dispositivo "di proprietà dell'azienda", viene raccolto un inventario app esteso, che fornisce accesso all'elenco completo di app dei dispositivi.<br /><br /> Se l'organizzazione richiede informazioni sulle applicazioni installate personalmente dai dispositivi gestiti, è necessari la MDM per dispositivi ibridi. Prima di prendere una decisione a riguardo, considerare l'impatto sulla privacy dell'utente finale.|  
|![ibridi&#45;6](../../mdm/understand/media/hybrid-6.png)|**Si desidera gestire i PC nel modo tradizionale Fat Client?**<br /><br /> Un vantaggio offerto dalla MDM per dispositivi ibridi rispetto alla configurazione autonoma è la gestione tramite pannello di controllo unificato. Ciò significa che un'organizzazione può gestire tutti i computer desktop, server e dispositivi mobili da un solo strumento di gestione, la console di Configuration Manager. Con il client di Configuration Manager sono disponibili per i dispositivi mobili funzioni avanzate di gestione, ad esempio l'inventario hardware e software, la gestione degli aggiornamenti software, la distribuzione del software e la distribuzione del sistema operativo.<br /><br /> Se l'organizzazione desidera gestire client Windows, Linux/UNIX e Mac tradizionali, Configuration Manager è la piattaforma di gestione ideale.<br /><br /> Intune autonomo offre anche la gestione dei PC tradizionali (Windows 7, 8.1 e 10) tramite il client di gestione del PC Intune. Esso offre gestione di base dei PC, inventario hardware, aggiornamenti di Windows, Endpoint Protection e semplice distribuzione del software. Il client non funziona con Configuration Manager, pertanto può essere usato nelle distribuzioni sia di Intune autonomo che di MDM ibrida.|  
|![ibridi&#45;7](../../mdm/understand/media/hybrid-7.png)|**Si desidera gestire l'infrastruttura locale?**<br /><br /> Qualsiasi infrastruttura locale implica un certo livello di overhead e complessità di gestione. Configuration Manager è un prodotto che richiede notevoli conoscenze, esperienza e investimenti per gestire e mantenere la propria infrastruttura.<br /><br /> Come requisito minimo, la MDM ibrida richiede un singolo sito primario di Configuration Manager, con ruolo del database, ruolo di Reporting Services e ruolo di punto di connessione del servizio. Se è necessaria la gestione dei PC tradizionale, potrebbero essere necessari il punto di gestione, il punto di distribuzione, il punto di aggiornamento software e i ruoli del catalogo applicazioni. Le funzioni avanzate, ad esempio la distribuzione di certificati, la gestione Mac ed Endpoint Protection aggiungono un numero maggiore di ruoli e una complessità superiore.<br /><br /> La gerarchia di Configuration Manager richiede notevoli azioni di gestione e manutenzione per garantire l'integrità e la funzionalità richieste.<br /><br /> Se si desidera evitare il sovraccarico di una gerarchia di Configuration Manager, la soluzione ideale è la distribuzione di Intune autonomo.|  
|![ibridi&#45;8](../../mdm/understand/media/hybrid-8.png)|**L'utente necessita di strumenti esterni?**<br /><br /> Configuration Manager è un prodotto di livello enterprise solido che offre molti modi per interagire con il servizio senza usare la console. Una distribuzione MDM ibrida consente agli amministratori di usare l'SDK di Configuration Manager o PowerShell per gestire i dispositivi mobili a livello di codice. Essa consente anche agli amministratori di usare strumenti quali System Center Orchestrator, Power BI e vari componenti aggiuntivi di terze parti.<br /><br /> In una distribuzione di Intune autonomo, tutta l'amministrazione deve essere eseguita tramite la console di Silverlight e non sono disponibili strumenti esterni.|  
|![ibridi&#45;9](../../mdm/understand/media/hybrid-9.png)|**Si desiderano gli aggiornamenti rapidi delle funzioni MDM?**<br /><br /> Anche se Configuration Manager (ramo corrente) offre manutenzione rapida per gli aggiornamenti e le funzionalità, lo sviluppo di servizi cloud, come Intune, si presta bene a una distribuzione ancora più rapida nell'ambiente di produzione.<br /><br /> Intune autonomo potrà ricevere nuove funzionalità prima della distribuzione MDM ibrida.<br /><br /> Per le organizzazioni all'avanguardia, Intune autonomo offre le più recenti funzionalità MDM nei tempi più rapidi.|



<!--HONumber=Nov16_HO1-->


