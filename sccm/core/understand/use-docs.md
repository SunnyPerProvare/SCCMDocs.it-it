---
title: Come usare la documentazione
titleSuffix: Configuration Manager
description: Suggerimenti sull'uso della di documentazione tecnica di Configuration Manager.
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 633827a8d4173c70f0d6180c8b2341c16246cb1b
ms.sourcegitcommit: fa806f4691befecc7f95a3213f709acfa520a132
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78290022"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Uso della documentazione di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo è suddiviso nelle sezioni elencate di seguito, in cui sono presentati suggerimenti e altre risorse utili per l'uso della libreria di documentazione di Configuration Manager:  

- [Come eseguire la ricerca](#bkmk_searchtips)  

- [Invio di segnalazioni di bug, miglioramenti, domande e nuove idee per la documentazione](#bkmk_docfeedback)  

- [Come ricevere notifiche relative alle modifiche](#bkmk_notifications)  

- [Come contribuire ai documenti](#bkmk_contribute)  


Per informazioni generali sul prodotto, vedere l'argomento sulla [consultazione della Guida](/sccm/core/understand/find-help).


##  <a name="bkmk_searchtips"></a> Ricerca   
 Per trovare le informazioni necessarie, usare i seguenti suggerimenti per la ricerca:  

-   Quando si usa il motore di ricerca preferito per individuare il contenuto per Configuration Manager, includere `SCCM` con le parole chiave della ricerca.  

    - Cercare i risultati in docs.microsoft.com per il branch corrente di Configuration Manager. I risultati reperibili in technet.microsoft.com o msdn.microsoft.com riguardano le versioni precedenti del prodotto.  

    - Per concentrare ulteriormente i risultati della ricerca sulla raccolta di contenuto corrente, includere `site:docs.microsoft.com` per definire l'ambito del motore di ricerca.  

-   Usare termini di ricerca che corrispondano alla terminologia nell'interfaccia utente e nella documentazione online. Evitare termini non ufficiali o abbreviazioni che possono trovarsi nei contenuti della community. Ad esempio, cercare "punto di gestione" anziché "PG", "tipo di distribuzione" anziché "TD" e "aggiornamenti software" anziché "AS".  

-   Per eseguire una ricerca all'interno di un articolo che si sta visualizzando, usare la funzionalità di **ricerca** del browser. Con i Web browser più recenti, premere **CTRL**+**F** e quindi immettere i termini di ricerca.  

-   Ogni articolo in docs.microsoft.com include i campi seguenti per agevolare la ricerca del contenuto:  

    - **Cerca** nell'angolo superiore destro. Per cercare in tutti gli articoli immettere i termini in questo campo. Gli articoli della libreria di Configuration Manager includono automaticamente l'ambito "ConfigMgr".  

    - **Filtra per titolo** sopra il sommario a sinistra. Per eseguire una ricerca nel sommario corrente, immettere i termini in questo campo. Il campo consente di individuare le corrispondenze solo con termini che appaiono nei titoli degli articoli per il nodo corrente. Ad esempio, Infrastruttura di base o Gestione applicazioni.  

- In caso di problemi durante la ricerca, [inviare un feedback](#bkmk_docfeedback). Quando si segnala il problema specificare il motore di ricerca in uso, le parole chiave che si è tentato di usare e l'articolo di destinazione. Questo feedback consente a Microsoft di ottimizzare il contenuto per migliorare la ricerca.  

> [!TIP] 
> A partire da Configuration Manager versione 1902, è disponibile il nodo **Documentazione** nella nuova area di lavoro **Community**. Questo nodo contiene informazioni aggiornate sulla documentazione di Configuration Manager e gli articoli del supporto tecnico. Per altre informazioni, vedere [Uso della console di Configuration Manager](/sccm/core/servers/manage/admin-console#bkmk_doc-dashboard)

## <a name="bkmk_docfeedback"></a> Commenti e suggerimenti

Per passare alla sezione Commenti e suggerimenti nella parte inferiore, fare clic sul collegamento **Commenti e suggerimenti** in alto a destra nell'articolo. Questa sezione è integrata con Problemi di GitHub. Per altre informazioni sull'integrazione con Problemi di GitHub, vedere il [post di blog sulla piattaforma di documentazione](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Per condividere commenti e suggerimenti sul prodotto Configuration Manager, fare clic su **Commenti e suggerimenti sul prodotto**. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback). 

Un [account GitHub](https://github.com/join) è un prerequisito per l'invio di un feedback sulla documentazione. Dopo aver effettuato l'accesso, viene richiesta un'autorizzazione monouso per MicrosoftDocs. Quando si fa clic su **Commenti sul contenuto** immettere un titolo e un commento e quindi scegliere **Invia commenti e suggerimenti**. Con questa azione si aggiunge un nuovo problema relativo all'articolo di destinazione al [repository SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Questa integrazione consente anche di visualizzare eventuali problemi chiusi o aperti esistenti per l'articolo di destinazione. Se esistono altri problemi, esaminarli prima di inviare un nuovo problema. Se si trova un problema correlato, fare clic sull'icona del viso per aggiungere una reazione o espanderla per aggiungere un commento. 

#### <a name="types-of-feedback"></a>Tipi di feedback
Usare Problemi di GitHub per inviare i seguenti tipi di commenti e suggerimenti:
- Bug della documentazione: il contenuto non è aggiornato, è poco chiaro, confuso o incompleto.
- Miglioramento della documentazione: suggerimenti per migliorare l'articolo.
- Domanda sulla documentazione: è necessario reperire documentazione esistente.
- Idea per la documentazione: suggerimenti per un nuovo articolo. Usare questo metodo anziché UserVoice per i suggerimenti sulla documentazione.
- Apprezzamenti: commenti positivi su un articolo utile o informativo.
- Localizzazione: commenti e suggerimenti sulla traduzione del contenuto.
- Ottimizzazione del motore di ricerca (SEO): commenti e suggerimenti sui problemi che si verificano durante la ricerca di contenuto. Includere il motore di ricerca, le parole chiave e l'articolo di destinazione nei commenti.

Se si segnalano problemi per argomenti non correlati alla documentazione, ad esempio [commenti e suggerimenti sui prodotti](/sccm/core/understand/find-help#product-feedback), [domande sui prodotti](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB) o [richieste di supporto](https://aka.ms/cmcbsupport), verranno chiusi e l'utente verrà reindirizzato al canale di feedback appropriato.

Per condividere commenti e suggerimenti sulla piattaforma docs.microsoft.com, vedere la sezione relativa al [feedback sulla documentazione](https://aka.ms/sitefeedback). La piattaforma include tutti i componenti di wrapping, ad esempio l'intestazione, il sommario e il menu a destra. Include anche indicazioni sull'esecuzione del rendering degli articoli nel browser, ad esempio il tipo di carattere, le finestre di avviso e gli ancoraggi delle pagine.



## <a name="bkmk_notifications"></a> Notifiche

Per ricevere notifiche quando viene modificato il contenuto nella libreria della documentazione, procedere come segue:

1. Usare la [ricerca nella documentazione](https://docs.microsoft.com/search/index?scope=ConfigMgr) per trovare un articolo o una serie di articoli. Ad esempio:
    - Cercare un singolo articolo in base al titolo, ad esempio ["File di log per la risoluzione dei problemi - Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)
    - Cercare qualsiasi articolo relativo a [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)
2. Nell'angolo superiore destro fare clic sul collegamento **RSS**. 
3. Usare questo feed in qualsiasi applicazione RSS per ricevere notifiche quando viene apportata una modifica a uno dei risultati della ricerca.


> [!Tip]  
> È anche possibile **consultare** il [repository SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) su GitHub. Questo metodo genera una grande quantità di notifiche. Non include inoltre le modifiche presenti in un repository privato usato da Microsoft.  



## <a name="bkmk_contribute"></a> Collaborazione

La libreria di documentazione di Configuration Manager, analogamente alla maggior parte del contenuto su docs.microsoft.com, è open source su GitHub. Questa raccolta accetta e incoraggia i contributi della community. Per altre informazioni su come iniziare, vedere la [guida per i collaboratori](https://docs.microsoft.com/contribute). Creare un [account GitHub](https://github.com/join) è l'unico prerequisito.

#### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Procedura di base per contribuire a SCCMdocs
1. Fare clic su **Modifica** nell'articolo di destinazione. Questa azione apre il file di origine in GitHub.  

2. Per modificare il file di origine, fare clic sull'icona a forma di matita.  

3. Apportare le modifiche nel markdown. Per altre informazioni, vedere [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/markdown-reference) (Come usare il markdown per scrivere documenti).  

4. Nella sezione di modifica del file immettere un commento di commit pubblico che descriva *cosa* è stato modificato. Quindi fare clic su **Propose file change** (Proponi modifica file).  

5. Scorrere verso il basso e verificare le modifiche apportate. Fare clic su **Crea richiesta pull** per aprire il modulo. Indicare *perché* è stata apportata la modifica. Assegnare un tag all'autore dell'articolo e richiedere la sua revisione. Fare clic su **Crea richiesta pull**.  


### <a name="what-to-contribute"></a>In che modo si contribuisce

Se si è interessati a collaborare, ma non si sa come iniziare, vedere i suggerimenti seguenti:  

- Cercare nell'elenco dei problemi le etichette assegnate alla community:  
  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)   
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Le etichette vengono assegnate dagli autori di Microsoft ai problemi per cui più facilmente si riceveranno contributi della community.  

- Esaminare un articolo per verificarne l'accuratezza. Aggiornare quindi i metadati **ms.date** usando il formato `mm/dd/yyyy`. Questo contributo consente di mantenere aggiornato il contenuto.  

- Aggiungere precisazioni, esempi o indicazioni in base alla propria esperienza. Questo contributo usa le risorse della community per condividere le informazioni.   

- Correggere le traduzioni in una lingua diversa dall'inglese. Questo contributo migliora l'usabilità del contenuto localizzato.  

> [!Note]  
> Chi non è un dipendente di Microsoft deve firmare un contratto di licenza per contributi per inviare contributi consistenti. GitHub richiede automaticamente di firmare questo contratto quando un contributo raggiunge la soglia.  


### <a name="tips"></a>Suggerimenti

Quando si contribuisce a documenti di Configuration Manager, seguire queste linee guida generali:

- Invece di inviare richieste pull di grandi dimensioni, [segnalare un problema](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_docfeedback) e avviare una discussione. Si eviterà così di perdere tempo e sarà possibile stabilire come procedere.  

- Leggere la [guida di stile Microsoft](https://aka.ms/MicrosoftStyle). Tenere presenti i [10 suggerimenti principali di Microsoft sullo stile e il tono](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).  

- Basare il proprio lavoro sul [modello di richiesta pull](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md).  

- Seguire il [flusso di lavoro di GitHub](https://guides.github.com/introduction/flow/).  

- Creare spesso blog e tweet (o quanto si ritiene idoneo) sui propri contributi.  

Questo elenco è stato tratto dalla [guida ai contributi su .NET](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts).
