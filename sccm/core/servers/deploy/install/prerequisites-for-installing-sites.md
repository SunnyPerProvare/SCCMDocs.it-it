---
title: Prerequisiti per i siti | Microsoft Docs
description: Informazioni sui vari prerequisiti necessari per installare i diversi tipi di siti di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: d39c8acca79c97c3979020c284616038b897d7cf

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Prerequisiti per l'installazione di siti di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Le sezioni seguenti offrono informazioni dettagliate sui diversi prerequisiti necessari per installare i vari tipi di siti di System Center Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Siti primari e sito di amministrazione centrale
I prerequisiti seguenti si applicano all'installazione di un sito di amministrazione centrale come primo sito di una gerarchia, primario autonomo o sito primario figlio. Se si installa un sito di amministrazione centrale come parte di uno scenario di espansione della gerarchia, vedere [Espansione di un sito primario autonomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
) in questo argomento.

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Prerequisiti per l'installazione di un sito primario o un sito di amministrazione centrale  

-   L'utente che installa il sito deve avere le autorizzazioni seguenti:  

    -   **Amministratore locale** sul computer server del sito  

    -   **Amministratore locale** su ogni computer che ospiterà il **database del sito** o un'istanza di **SMS_Provider** per il sito  

    -   **Amministratore di sistema** nell'istanza di SQL Server che ospita il database del sito  

        > [!IMPORTANT]  
        >  Al termine dell'installazione, sia l'account utente che esegue l'installazione che l'account computer server del sito devono mantenere diritti di amministratore di sistema su SQL Server. Non è possibile rimuovere diritti di amministratore di sistema da questi account.  

-   Quando si installa un sito primario, sono necessarie le autorizzazioni aggiuntive seguenti:  
    -  **Amministratore locale** su altri computer in cui si installeranno il punto di gestione iniziale e il punto di distribuzione, se non vengono installati nel server del sito.  

-   Se si installa un nuovo sito primario figlio all'interno di un sito di amministrazione centrale, sono necessarie le autorizzazioni aggiuntive seguenti:  

    -   **Amministratore locale** sul computer che ospita il sito di amministrazione centrale.  

    -   Autorizzazioni di amministrazione basata su ruoli in Configuration Manager equivalenti al ruolo di sicurezza di tipo **Amministratore infrastruttura** o **Amministratore completo**.  

-   È necessario usare il supporto di installazione corretto (file di origine) ed eseguire il programma di installazione da tale percorso. Per informazioni sui file di origine corretta da usare per installare diversi siti, vedere [Opzioni per l'installazione di diversi tipi di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) nell'argomento [Preparare l'installazione di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   Il computer del server del sito deve avere accesso ai file di installazione aggiornati forniti da Microsoft:
    -  Prima di iniziare l'installazione, è possibile scaricare e archiviare una copia di questi file nella rete locale tramite [Downloader di installazione](../../../../core/servers/deploy/install/setup-downloader.md)
    -  Se una copia locale di questi file non è disponibile, il server del sito deve avere accesso a Internet in modo da poter scaricare i file dal sito Microsoft durante l'installazione

  - Prima di espandere un sito primario autonomo in cui è installato un ruolo del sistema del sito relativo al punto di connessione del servizio, è necessario disinstallare il punto di connessione del servizio. In una gerarchia è consentita solo un'istanza di questo ruolo ed è consentita solo nel sito di livello superiore della gerarchia. Sarà possibile reinstallare il ruolo durante l'installazione del sito di amministrazione centrale.
  - Il server del sito e i computer del database del sito devono soddisfare tutte le configurazioni dei prerequisiti. Prima di avviare il programma di installazione, è possibile [eseguire manualmente Controllo prerequisiti](../../../../core/servers/deploy/install/prerequisite-checker.md) per identificare e risolvere eventuali problemi.  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Espansione di un sito primario autonomo
Un sito primario autonomo deve soddisfare i seguenti prerequisiti ai fini dell'espansione in una gerarchia con un sito di amministrazione centrale:


-   **È necessario installare il supporto di installazione del sito di amministrazione centrale nuovo (file di origine) che corrisponde alla versione del sito primario autonomo:**  
     Per assicurarsi che la versione corrisponda, installare il nuovo sito usando i file di origine presenti nella [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) del sito primario autonomo.

     Per altre informazioni sui file di origine corretta da usare per installare diversi siti, vedere [Opzioni per l'installazione di diversi tipi di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) nell'argomento [Preparare l'installazione di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **Non è possibile configurare il sito primario autonomo per eseguire la migrazione dei dati da un'altra gerarchia di Configuration Manager:**  

     È necessario interrompere la migrazione attiva al sito primario autonomo da altre gerarchie di Configuration Manager e rimuovere tutte le configurazioni per la migrazione. Ciò include i processi di migrazione che non sono stati completati, la raccolta dati e la configurazione della gerarchia di origine attiva.  

     Ciò è necessario perché le operazioni di migrazione sono eseguite dal sito superiore della gerarchia e le configurazioni per la migrazione non vengono trasferite al sito di amministrazione centrale quando si espande un sito primario autonomo.  

     Se si riconfigura la migrazione al sito primario dopo l'espansione del sito primario autonomo, le operazioni correlate alla migrazione saranno eseguite dal sito di amministrazione centrale. Per altre informazioni sulla configurazione della migrazione, vedere [Configurazione delle gerarchie di origine e dei siti di origine per la migrazione a System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **L'account del computer che ospiterà il nuovo sito di amministrazione centrale deve essere un membro del gruppo Amministratori nel sito primario autonomo:**  

     Per espandere correttamente il sito primario autonomo, l'account computer del nuovo sito di amministrazione centrale deve essere un membro del gruppo **Amministratori** dei siti primari autonomi. Ciò è richiesto solo durante l'espansione del sito e, al termine di tale operazione, è possibile rimuovere l'account dal gruppo sul sito primario.  

-   **All'account utente che esegue l'installazione del nuovo sito di amministrazione centrale devono essere concesse autorizzazioni per l'amministrazione basata su ruoli nel sito primario autonomo:**  

     Per installare un sito di amministrazione centrale come parte di uno scenario di espansione del sito, l'account utente che esegue la procedura per l'installazione del sito di amministrazione centrale deve essere definita nell'amministrazione basata sul ruolo nel sito primario autonomo come **Amministratore completo** o come **Amministratore infrastruttura**.  

-   **Per espandere il sito, è necessario prima disinstallare i ruoli seguenti di sistema del sito dal sito primario autonomo:**  

    -   Punto di sincronizzazione di Asset Intelligence  

    -   Punto di Endpoint Protection  

    -   punto di connessione del servizio  

     Questi ruoli del sistema del sito sono supportati solo nel sito di livello superiore della gerarchia. È necessario pertanto disinstallare questi ruoli di sistema del sito prima di espandere il sito primario autonomo. Al termine dell'espansione, è possibile reinstallare questi ruoli del sistema del sito nel sito di amministrazione centrale.  

    Tutti gli altri ruoli del sistema del sito possono rimanere installati nel sito primario.  

-   **La porta per SQL Server Service Broker deve essere aperta tra il sito primario autonomo e il computer che installa il sito di amministrazione centrale:**  

     Per replicare correttamente i dati tra un sito di amministrazione centrale e un sito primario, Configuration Manager richiede l'apertura della porta che deve essere usata da SQL Server Service Broker tra i due siti. Quando si installa un sito di amministrazione centrale e si espande un sito primario autonomo, il controllo dei prerequisiti non stabilisce che la porta specificata per SQL Server Service Broker è aperta sul sito primario.  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> Siti secondari
Di seguito vengono elencati i prerequisiti per l'installazione di siti secondari:
-   L'utente amministratore che configura l'installazione del sito secondario nella console di Configuration Manager deve avere i diritti di amministrazione basata su ruoli equivalenti al ruolo di sicurezza di **Amministratore infrastruttura** o **Amministratore completo**.  

-   L'account computer del sito primario padre deve essere un **amministratore locale** sul computer server del sito secondario.  

-   Quando il sito secondario usa un'istanza di SQL Server installata in precedenza per ospitare il database del sito secondario:  

    -   L' **account computer** del sito primario padre deve avere i diritti di **amministratore di sistema** sull'istanza di SQL Server sul computer server del sito secondario.  

    -   L'account di **sistema locale** del computer server del sito secondario deve avere i diritti di **amministratore di sistema** sull'istanza di SQL Server sul computer server del sito secondario.  

        > [!IMPORTANT]  
        >  Al termine dell'installazione, entrambi gli account devono mantenere diritti di amministratore di sistema su SQL Server. Non è possibile rimuovere diritti di amministratore di sistema da questi account.  

-   Il computer server del sito secondario deve soddisfare tutte le configurazioni richieste, inclusi SQL Server e i ruoli del sistema del sito predefiniti del punto di gestione e del punto di distribuzione.  



<!--HONumber=Dec16_HO3-->


