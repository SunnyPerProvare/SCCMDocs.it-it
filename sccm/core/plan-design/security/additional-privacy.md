---
title: Informativa sulla privacy per System Center Configuration Manager - Altre informazioni | Microsoft Docs
description: Informazioni su come Microsoft raccoglie e usa i dati da un'implementazione di System Center Configuration Manager.
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- en-gb
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
ms.openlocfilehash: ef7b3656f9b4a31e07227aa4e864448d0dd1fcdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Altre informazioni sulla privacy per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Aggiornamenti e manutenzione
System Center Configuration Manager introduce un nuovo modello di aggiornamento che consente di mantenere aggiornata la distribuzione di Configuration Manager con gli aggiornamenti e le funzionalità più recenti. Durante l'installazione, questa funzionalità aggiunge un nuovo ruolo del sistema del sito, chiamato punto di connessione del servizio, in un server del sito scelto dall'amministratore. Per approfondimenti sulle informazioni raccolte e sul loro uso, consultare la sezione Dati di utilizzo in questo articolo.


## <a name="usage-data"></a>Dati di utilizzo
System Center Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso, che Microsoft usa per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.
I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di System Center Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.

Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.

Gli amministratori possono modificare il livello dei dati che vengono raccolti andando alla sezione **Dati di utilizzo** della console di Configuration Manager.

Per altre informazioni, vedere gli articoli di approfondimento relativi alle impostazioni e ai livelli per i dati di utilizzo nell'articolo [Dati di diagnostica e di utilizzo per System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Analisi utilizzo software
Il programma Analisi utilizzo software raccoglie informazioni di base dalla console di Configuration Manager relative alla configurazione hardware e alla modalità di impiego del software e dei servizi per individuare tendenze e modelli di utilizzo. Vengono inoltre raccolte informazioni sul tipo e sul numero di errori rilevati, sulle prestazioni software e hardware e sulla velocità dei servizi. Non vengono raccolti nomi, indirizzi o altre informazioni che consentono l'identificazione personale degli utenti. Dai computer client non viene raccolta alcuna informazione per Analisi utilizzo software.

Microsoft usa le informazioni raccolte per migliorare la qualità, l'affidabilità e le prestazioni dei propri software e servizi.

Per dettagli sulle informazioni che vengono raccolte, elaborate o trasmesse dal programma Analisi utilizzo software, vedere la relativa [informativa sulla privacy](http://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="operations-management-suite-connector"></a>Connettore Operations Management Suite
Il connettore Microsoft Operations Management Suite consente di sincronizzare dati, ad esempio le raccolte, da System Center Configuration Manager a Microsoft Operations Management Suite. L'ID sottoscrizione e la chiave privata di Microsoft Azure vengono memorizzati nel database di Configuration Manager quando l'amministratore configura la funzionalità. Sia la chiave privata del client di Azure Active Directory che la chiave condivisa dell'area di lavoro di Microsoft Operations Management Suite vengono archiviate nel database di System Center Configuration Manager in locale. Tutte le comunicazioni tra System Center Configuration Manager e Microsoft Operations Management Suite utilizzano HTTPS. A Microsoft non vengono fornite informazioni aggiuntive sulle raccolte, a parte dati di telemetria casuali. Per dettagli sulle informazioni raccolte da Microsoft Operations Management Suite, vedere [Sicurezza dei dati di Log Analytics](http://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Asset Intelligence consente agli amministratori IT di definire, tenere traccia e gestire in modo proattivo la conformità agli standard di configurazione. Il controllo e i report sulla distribuzione e l'utilizzo di applicazioni fisiche e virtuali consentono alle organizzazioni di prendere decisioni aziendali più efficaci relativamente alle licenze software, nonché di garantire la conformità rispetto ai contratti di licenza. Dopo aver raccolto i dati sull'utilizzo dai client di Configuration Manager, gli amministratori possono usare diverse funzionalità per visualizzare tali dati, ad esempio le raccolte, le query e i report.

Durante ogni sincronizzazione, viene scaricato un catalogo di software conosciuti dal sito Microsoft. Gli amministratori IT possono scegliere di inviare a Microsoft le informazioni relative ai titoli di software senza categoria rilevati nelle organizzazioni, al fine di cercarli e aggiungerli al catalogo. Prima di caricare queste informazioni, viene visualizzata una finestra di dialogo in cui sono mostrati i dati che si stanno per caricare. Non è possibile annullare il caricamento dei dati selezionati. Asset Intelligence non invia a Microsoft informazioni su utenti e computer o sull'utilizzo delle licenze.

Una volta caricato un titolo di software, i ricercatori Microsoft identificano, classificano e rendono le informazioni disponibili a tutti gli altri clienti che usano la funzionalità e a tutti gli utenti del catalogo. Tutti i titoli di software caricati diventano pubblici. Le informazioni su una determinata applicazione e la relativa classificazione diventano parte del catalogo e possono essere scaricate dagli altri utenti del catalogo. Prima di configurare la raccolta dei dati di Asset Intelligence e decidere se inviare informazioni a Microsoft, prendere in considerazione i requisiti sulla privacy della propria organizzazione.

Asset Intelligence non è abilitato in System Center Configuration Manager per impostazione predefinita. Il caricamento dei titoli senza categoria non avviene mai automaticamente e il sistema non è progettato per l'esecuzione automatica di questa attività. È necessario selezionare manualmente e approvare il caricamento di ogni titolo di software.

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service era precedentemente conosciuto come Microsoft Active Protection Service o MAPS.
I prodotti applicabili sono System Center Endpoint Protection e la funzionalità Endpoint Protection di System Center Configuration Manager (per la gestione di System Center Endpoint Protection e Windows Defender per Windows 10). Questa funzionalità non è implementata né per System Center Endpoint Protection per Linux né per System Center Endpoint Protection per Mac.

La community antimalware Microsoft Cloud Protection Service è una community antimalware online diffusa in tutto il mondo che comprende gli utenti di System Center Endpoint Protection. Se un utente entra a far parte di Microsoft Cloud Protection Service, System Center Endpoint Protection invierà automaticamente informazioni a Microsoft per consentire di individuare il software da analizzare alla ricerca di potenziali minacce e per migliorare l'efficacia di System Center Endpoint Protection. Questa community contribuisce ad arrestare la diffusione di nuove infezioni causate da software dannoso. Se un report di Microsoft Cloud Protection Service include informazioni su malware o software potenzialmente dannoso che il client di Endpoint Protection potrebbe rimuovere, Microsoft Cloud Protection Service esegue il download della firma più recente per risolvere il problema. Microsoft Cloud Protection Service può anche individuare "falsi positivi", ovvero elementi in origine identificati erroneamente come malware, e risolverli.

Le segnalazioni di Microsoft Cloud Protection Service includono dati relativi a potenziali file di malware, come i nomi dei file, l'hash crittografico, il fornitore, le dimensioni e gli indicatori di data. Microsoft Cloud Protection Service potrebbe inoltre raccogliere gli URL completi per indicare l'origine del file. Questi URL possono occasionalmente includere informazioni personali come termini di ricerca o dati immessi nei moduli. I report possono inoltre includere le azioni che sono state eseguite quando Endpoint Protection ha notificato software indesiderato. I report di Microsoft Cloud Protection Service includono queste informazioni per consentire a Microsoft di valutare l'efficacia di Endpoint Protection nel rilevare e rimuovere il malware e il software potenzialmente indesiderato e per tentare di identificare nuovo malware.

È possibile entrare a far parte di Microsoft Cloud Protection Service se si dispone di un'iscrizione base o avanzata. I report dei membri con iscrizione base includono le informazioni descritte in precedenza. I report dei membri con iscrizione avanzata sono più dettagliati e offrono altre informazioni relative al software rilevato da Endpoint Protection, come la posizione del software, i nomi file, le modalità di funzionamento del software e i suoi effetti sul computer. Tali report e quelli di altri utenti di Endpoint Protection che partecipano a Microsoft Cloud Protection Service aiutano i ricercatori Microsoft a scoprire più rapidamente le nuove minacce. Successivamente vengono create le definizioni dei malware per i programmi che soddisfano i criteri di analisi; le definizioni aggiornate sono messe a disposizione di tutti gli utenti attraverso Microsoft Update.

Per consentire di individuare e correggere alcuni tipi di infezioni malware, il prodotto invia regolarmente a Microsoft Cloud Protection Service informazioni sullo stato di protezione del PC. Queste informazioni includono indicazioni sulle impostazioni di protezione del PC e i file di log che descrivono i driver e altro software che viene caricato all'avvio del PC.
Viene inoltre inviato un numero che identifica in modo univoco il PC. Microsoft Cloud Protection Service può anche raccogliere gli indirizzi IP a cui i potenziali file malware si connettono.

I report Microsoft Cloud Protection Service vengono utilizzati per migliorare il software e i servizi Microsoft. Potrebbero essere usati anche per fini statistici, analitici o a scopo di prova e per generare definizioni. Solo i dipendenti, i collaboratori, i partner e i fornitori di Microsoft che abbiano una necessità commerciale di usare i report vi possono accedere.

Microsoft Cloud Protection Service non raccoglie intenzionalmente informazioni personali. Eventuali informazioni personali raccolte da Microsoft Cloud Protection Service non verranno utilizzate da Microsoft per identificare o contattare l'utente.

Altre informazioni relative ai dati raccolti sono disponibili nella documentazione del prodotto in [Endpoint Protection in System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Gerarchia dei siti: visualizzazione geografica con Bing Maps
Gerarchia siti - Vista geografica consente di usare le mappe fornite da Microsoft Bing Maps per visualizzare la topologia dei server fisici di Configuration Manager. Per abilitare questa funzionalità, le informazioni sulla posizione fornite dall'utente vengono inviate dal server al servizio Web di Bing Maps.

Microsoft usa le informazioni per il funzionamento e il miglioramento delle mappe di Microsoft Bing Maps e di altri siti e servizi Microsoft. Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](http://go.microsoft.com/fwlink/?LinkId=823548).
È possibile scegliere di non usare la visualizzazione geografica per la gerarchia dei siti. La vista Diagramma gerarchia consente di visualizzare la gerarchia e non usa il servizio Bing Maps.

## <a name="microsoft-intune-subscription"></a>Sottoscrizione di Microsoft Intune
I clienti che hanno acquistato una sottoscrizione a Microsoft Intune possono usare Configuration Manager per gestire i propri dispositivi mobili connessi tramite Microsoft Intune. L'[Informativa sulla privacy dei Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) si applica ai servizi online Microsoft, incluso Microsoft Intune. Se i clienti dispongono anche di una sottoscrizione Microsoft Intune, è necessario leggere l'[informativa sulla privacy di Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkId=262214) insieme alla presente informativa sulla privacy.

Tutte le comunicazioni con Microsoft utilizzano HTTPS. Per configurare la sottoscrizione a Microsoft Intune e scaricare la richiesta di firma del certificato (CSR) necessaria per la configurazione del supporto iOS, l'amministratore deve accedere a Microsoft Intune usando l'account e la password aziendali. Queste credenziali non vengono memorizzate in Configuration Manager. Tutte le altre comunicazioni con Microsoft Intune vengono autenticate mediante certificati PKI generati automaticamente da Microsoft Intune.

Per gestire i dispositivi collegati a Microsoft Intune, vengono scambiate alcune informazioni con Microsoft Intune. Queste informazioni includono il nome dell'entità utente (UPN) per tutti gli utenti assegnati al servizio e le informazioni di inventario per i dispositivi gestiti da Microsoft Intune. I metadati, come il nome dell'applicazione, l'editore e la versione, dei contenuti assegnati ai punti di distribuzione Manage.Microsoft.com vengono inviati a Microsoft Intune. Il contenuto binario effettivo assegnato a un punto di distribuzione Manage.Microsoft.com viene crittografato prima di essere caricato in Microsoft Intune.

Questa funzionalità non è configurata per impostazione predefinita. Gli amministratori controllano i contenuti che vengono trasferiti al punto di distribuzione Manage.Microsoft.com e gli utenti assegnati al servizio. La funzionalità può essere rimossa in qualsiasi momento.
