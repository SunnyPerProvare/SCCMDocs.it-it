---
title: Pianificare il provider SMS | System Center Configuration Manager
description: Informazioni su come il provider SMS consente di gestire System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bdf7b9b4ab9e9da25bf32891381f61c94ef28285


---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Pianificare per il provider SMS per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per la gestione di System Center Configuration Manager, usare una console di Configuration Manager che si connette a un'istanza del **provider SMS**. Per impostazione predefinita, un provider SMS viene installato in un sito di amministrazione centrale o un sito primario, quando si installa il sito.  


##  <a name="a-namebkmkplansmsprova-about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Informazioni sul provider SMS  
 Il provider SMS è un provider di Strumentazione gestione Windows (WMI) che assegna l'accesso di **lettura** e **scrittura** del database di Configuration Manager a un sito:  

-   Il gruppo **SMS Admins**  fornisce l'accesso al provider SMS. Configuration Manager crea automaticamente questo gruppo di sicurezza nel server di sito e su ogni computer del provider SMS.  

-   Ogni sito di amministrazione centrale e sito primario richiede almeno un provider SMS.  È possibile installare altri provider in base alle esigenze.  

-   I siti secondari non supportano il provider SMS.  


Ogni console di Configuration Manager, Esplora inventario risorse, gli strumenti e gli script personalizzati usano un provider SMS per consentire agli utenti amministratori di Configuration Manager di accedere alle informazioni archiviate nel database. Il provider SMS non interagisce con i client di Configuration Manager. Quando una console di Configuration Manager si connette a un sito, esegue una query di WMI sul server del sito per individuare un'istanza del provider SMS da usare.  

 Il provider SMS consente di imporre la sicurezza di Configuration Manager. Restituisce solo le informazioni che l'utente amministratore che esegue la console di Configuration Manager è autorizzato a visualizzare.  

> [!IMPORTANT]  
>  Se tutti i computer che hanno un provider SMS per un sito sono offline, le console di Configuration Manager non possono connettersi al database di quel sito.  

 Per informazioni su come gestire il provider SMS, vedere [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) in [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md).  

 **Prerequisiti per installare il Provider SMS:**  

 Per supportare il provider SMS:  

-   Il computer deve trovarsi in un dominio con un trust bidirezionale con il server del sito e i sistemi del sito del database del sito.  

-   Il computer non può disporre di un ruolo del sistema del sito da un sito differente.  

-   Il computer non può disporre di un provider SMS da qualsiasi sito.  

-   Il computer deve eseguire un sistema operativo supportato per un server del sito.  

-   Il computer deve disporre di almeno 650 MB di spazio disponibile su disco per supportare i componenti di Windows Automated Deployment Kit (Windows ADK) installati con il provider SMS. Per altre informazioni su Windows ADK e sul provider SMS, vedere [Requisiti di distribuzione del sistema operativo per il provider SMS](#BKMK_WAIKforSMSProv) in questo argomento.  

##  <a name="a-namebkmklocationa-sms-provider-locations"></a><a name="bkmk_location"></a> Sedi dei provider SMS  
 Quando si installa un sito, viene installato automaticamente il primo provider SMS per il sito. È possibile specificare una delle seguenti sedi supportate per il provider SMS:  

-   Il computer del server del sito  

-   Il computer del database del sito  

-   Un computer di classe server che non dispone di un provider SMS o un ruolo del sistema del sito da un altro sito  


Per visualizzare le sedi di ciascun provider SMS installato in un sito, vedere la scheda **Generale** della finestra di dialogo **Proprietà** del sito.  

 Ogni provider SMS supporta connessioni simultanee da più richieste. Gli unici limiti su queste connessioni sono il numero di connessioni server e le risorse disponibili sul computer del provider SMS per rispondere alle richieste di connessione.  

 Dopo l'installazione di un sito, è possibile eseguire nuovamente il programma di installazione sul server del sito per modificare la sede di un provider°SMS esistente oppure per installare provider°SMS aggiuntivi in quel sito. È possibile installare un solo provider SMS su un computer e non è possibile installare un provider SMS da più di un sito su un computer.  

 Usare le informazioni seguenti per identificare i vantaggi e gli svantaggi dell'installazione di un provider SMS in ogni sede supportata:  


**Server del sito di Configuration Manager**  

-   **Vantaggi:**  

    -   Il provider SMS non usa le risorse del sistema del computer del database del sito.  

    -   Questa sede consente di garantire prestazioni migliori rispetto a un provider SMS situato su un computer diverso dal server del sito o dal computer del database del sito.  

-   **Svantaggi:**  

    -   Il provider SMS usa risorse di sistema e di rete che potrebbero essere dedicate alle operazioni del server del sito.  


**SQL Server che ospita il database del sito**  

-   **Vantaggi:**  

    -   Il provider SMS non usa risorse di sistema del sito sul server del sito.  

    -   Questa sede consente di offrire le migliori prestazioni, se sono disponibili sufficienti risorse server.  

-   **Svantaggi:**  

    -   Il provider SMS usa risorse di sistema e di rete che potrebbero essere dedicate alle operazioni del database del sito.  

    -   Questa sede non rientra nelle opzioni quando il database del sito è ospitato su un'istanza del cluster di SQL Server.  


**Computer diverso dal server del sito o dal computer del database del sito**  

-   **Vantaggi:**  

    -   Il provider SMS non usa il server del sito o le risorse del computer del database del sito.  

    -   Questo tipo di sede consente di distribuire altri provider SMS per garantire un'elevata disponibilità per le connessioni.  

-   **Svantaggi:**  

    -   Le prestazioni del provider SMS potrebbero risultare ridotte a causa del traffico di rete aggiuntivo richiesto per il coordinamento con il server del sito e il computer del database del sito.  

    -   Questo server deve essere sempre accessibile al computer del database del sito e a tutti i computer su cui è installata la console di Configuration Manager.  

    -   Questa sede consente di usare le risorse di sistema altrimenti dedicate ad altri servizi.  

##  <a name="a-namebkmksmsprovlanguagesa-about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> Lingue del provider SMS  
 Il provider SMS funziona indipendentemente dalla lingua di visualizzazione del computer su cui è installato.  

 Quando un utente amministratore o un processo di Configuration Manager richiede dei dati tramite il provider SMS, quest'ultimo prova a restituirli in un formato compatibile con la lingua del sistema operativo del computer richiedente. Il provider SMS non traduce le informazioni da una lingua all'altra. Al contrario, quando i dati vengono restituiti per la visualizzazione nella console di Configuration Manager, la relativa lingua di visualizzazione dipenderà dall'origine dell'oggetto e dal tipo di archiviazione.  

 Quando i dati relativi a un oggetto vengono memorizzati nel database, le lingue disponibili dipenderanno dagli elementi seguenti:  

-   Gli oggetti creati da Configuration Manager vengono memorizzati nel database usando il supporto per più lingue. L'oggetto viene memorizzato usando le lingue configurate nel sito in cui l'oggetto viene creato durante l'esecuzione del programma di installazione. Tali oggetti vengono visualizzati nella console di Configuration Manager nella lingua di visualizzazione del computer richiedente, se tale lingua è disponibile per l'oggetto. Se non è possibile visualizzare l'oggetto nella lingua di visualizzazione del computer richiedente, sarà visualizzato nella lingua predefinita, ovvero l'inglese.  

-   Gli oggetti creati da un utente amministratore vengono memorizzati nel database con la lingua usata per creare l'oggetto. Questi oggetti vengono visualizzati nella console di Configuration Manager in questa stessa lingua. Non possono essere tradotti dal provider SMS e non dispongono di opzioni multilingue.  

##  <a name="a-namebkmkmultismsprova-use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Usare più provider SMS  
 Al termine dell'installazione di un sito, è possibile installare altri provider SMS per il sito. Per installare altri provider SMS, eseguire il programma di installazione di Configuration Manager nel server del sito. Si consiglia di installare altri provider SMS in presenza di una delle seguenti condizioni:  

-   Molti utenti amministratori eseguiranno una console di Configuration Manager e si connetteranno contemporaneamente a un sito.  

-   Si userà l'SDK di Configuration Manager, o altri prodotti, e ciò potrebbe comportare chiamate frequenti al provider SMS.  

-   Si desidera garantire una disponibilità elevata per il provider SMS.  


Quando più provider°SMS sono installati in un sito e viene eseguita una richiesta di connessione, il sito assegna in modo non deterministico ciascuna nuova richiesta di connessione per usare un provider°SMS installato. Non è possibile specificare la sede del provider°SMS da usare con una sessione di connessione specifica.  

> [!NOTE]  
>  Considerare i vantaggi e gli svantaggi della sede di ciascun provider°SMS e ponderare queste considerazioni con le informazioni che non si è in grado di controllare, ad esempio quale provider°SMS sarà usato per ciascuna connessione.  

Ad esempio, quando si esegue la prima connessione di una console di Configuration Manager a un sito, la connessione esegue una query di WMI sul server del sito per identificare in modo non deterministico un'istanza del provider SMS che sarà usata dalla console. Questa istanza specifica del provider SMS viene usata dalla console di Configuration Manager fino al termine della sessione della console. Se la sessione viene interrotta perché il computer del provider SMS non è più disponibile sulla rete, alla successiva connessione della console di Configuration Manager il sito assegnerà in modo non deterministico un computer del provider SMS alla nuova sessione di connessione. È possibile che sia effettuata un'assegnazione al computer del provider°SMS non disponibile. In tal caso, provare a riconnettere la console di Configuration Manager fino all'assegnazione di un computer del provider SMS disponibile.  

##  <a name="a-namebkmkaboutsmsadminsa-about-the-sms-admins-group"></a><a name="BKMK_AboutSMSAdmins"></a> Gruppo SMS Admins  
 Il gruppo SMS Admins viene usato per fornire l'accesso al provider°SMS agli utenti amministratori. Il gruppo viene creato automaticamente sul server del sito quando si installa il sito e su ogni computer su cui è installato un provider°SMS. Altre informazioni relative al gruppo SMS Admins:  

-   Quando il computer è un server membro, il gruppo SMS Admins viene creato come gruppo locale.  

-   Quando il computer è un controller di dominio, il gruppo SMS Admins viene creato come gruppo locale di dominio.  

-   Quando il provider°SMS viene disinstallato da un computer, il gruppo SMS Admins non viene rimosso dal computer.  


Affinché un utente possa connettersi a un provider°SMS, il relativo account deve essere un membro del gruppo SMS Admins. Ogni utente amministratore configurato nella console di Configuration Manager viene automaticamente aggiunto al gruppo SMS Admins in ogni server del sito e a ogni computer del provider SMS nella gerarchia. Quando si elimina un utente amministratore dalla console di Configuration Manager, tale utente viene rimosso dal gruppo SMS Admins in ogni server del sito e in ogni computer del provider SMS nella gerarchia.  

Dopo che un utente ha stabilito una connessione con il provider SMS, l'amministrazione basata su ruoli determina a quali risorse di Configuration Manager tale utente potrà accedere o gestire.  

È possibile visualizzare e configurare i diritti e le autorizzazioni del gruppo SMS Admins usando lo snap-in MMC del controllo WMI. Per impostazione predefinita, **Tutti** dispone della autorizzazioni **Esegui metodi**, **Scrittura provider**, e **Abilita Account** . Dopo che l'utente si è connesso al provider SMS, potrà accedere ai dati nel database del sito in base ai privilegi di sicurezza amministrativi basati su ruoli, come definito nella console di Configuration Manager. Al gruppo SMS Admins vengono concesse in modo esplicito le autorizzazioni **Abilita account** e **Abilita remoto** sullo spazio dei nomi **Root\SMS** .  

> [!NOTE]  
>  Ogni utente amministratore che usa una console di Configuration Manager remota richiede autorizzazioni DCOM per l'attivazione remota sul computer del server del sito e sul computer del provider SMS. Sebbene sia possibile garantire questi privilegi a qualsiasi utente o gruppo, si consiglia di concederli al gruppo SMS Admins per semplificare l'amministrazione. Per ulteriori informazioni, vedere la sezione [Configure DCOM permissions for remote Configuration Manager consoles](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) nell'argomento [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  


##  <a name="a-namebkmksmsprovnamespacea-about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> Spazio dei nomi del provider SMS  
La struttura del provider°SMS è definita dallo schema WMI. Gli spazi dei nomi dello schema descrivono il percorso dei dati di Configuration Manager all'interno dello schema del provider SMS. Nella tabella seguente sono riportati alcuni degli spazi dei nomi comuni usati dal provider°SMS.  

|Spazio dei nomi|Descrizione|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;codice sito\>*|Provider SMS, usato largamente dalla console di Configuration Manager, da Esplora inventario risorse, dagli script e dagli strumenti di Configuration Manager.|  
|Root\SMS\SMS_ProviderLocation|Fornisce il percorso dei computer del provider SMS per un sito.|  
|Root\CIMv2|Percorso di inventario per le informazioni sullo spazio dei nomi WMI durante l'inventario hardware e software.|  
|Root\CCM|Criteri di configurazione del client di Configuration Manager e dati client.|  
|root\CIMv2\SMS|Percorso delle classi di report di inventario raccolte da Inventory Client Agent. Queste impostazioni vengono compilate dai client durante la valutazione dei criteri computer e si basano sulla configurazione delle impostazioni client per il computer.|  

##  <a name="a-namebkmkwaikforsmsprova-operating-system-deployment-requirements-for-the-sms-provider"></a><a name="BKMK_WAIKforSMSProv"></a> Requisiti di distribuzione del sistema operativo per il provider SMS  
Il provider SMS richiede l'installazione della dipendenza esterna seguente nel computer che esegue il provider SMS per consentire agli utenti di usare le funzioni di distribuzione del sistema operativo tramite la console di Configuration Manager:  

-   Windows Assessment and Deployment Kit 8.1  

 Quando si gestiscono le distribuzioni del sistema operativo, Windows ADK consente al provider SMS di completare varie attività, tra cui:  

-   Visualizzare i dettagli del file WIM  

-   Aggiungere file driver a immagini di avvio esistenti  

-   Creare file ISO di avvio  


L'installazione di Windows ADK può richiedere fino a 650 MB di spazio libero su disco in ogni computer che installa il provider SMS. Questo requisito di una grande quantità di spazio su disco è necessario affinché Configuration Manager installi le immagini di avvio di Windows PE.  



<!--HONumber=Nov16_HO1-->


