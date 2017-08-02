---
title: Prerequisiti per i siti | Microsoft Docs
description: Informazioni sui prerequisiti per l'installazione di diversi tipi di siti di System Center Configuration Manager.
ms.custom: na
ms.date: 7/31/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 5945abb49fe06c59355805aa94b04d0d445ecbc3
ms.openlocfilehash: d46a8b66ace45d25da9d86f2e91b19ae1d6875ab
ms.contentlocale: it-it
ms.lasthandoff: 07/24/2017

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Prerequisiti per l'installazione di siti di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di iniziare l'installazione di un sito, è consigliabile conoscere i prerequisiti per l'installazione di diversi tipi di siti di System Center Configuration Manager.

## <a name="primary-sites-and-the-central-administration-site"></a>Siti primari e sito di amministrazione centrale
I prerequisiti seguenti si applicano all'installazione di un sito di amministrazione centrale come primo sito di una gerarchia, di un sito primario autonomo o di un sito primario figlio. Se si installa un sito di amministrazione centrale come parte di un'espansione della gerarchia, vedere [Espansione di un sito primario autonomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) in questo argomento.

###  <a name="bkmk_PrereqPri"></a> Prerequisiti per l'installazione di un sito primario o un sito di amministrazione centrale  

-   L'account utente che installa il sito deve disporre dei diritti seguenti:  

    -   **Amministratore** nel computer server del sito  
    -   **Amministratore** in ogni computer che ospiterà il **database del sito** o un'istanza del **provider SMS** per il sito  
    -   **Amministratore di sistema** nell'istanza di SQL Server che ospita il database del sito  

        > [!IMPORTANT]  
        >  Al termine dell'installazione, sia l'account utente che esegue l'installazione che l'account computer server del sito devono mantenere i diritti di amministratore di sistema in SQL Server. Non rimuovere i diritti di amministratore di sistema da questi account.  

-   Quando si installa un sito primario, sono necessari i diritti aggiuntivi seguenti:  
    -  **Amministratore** in altri computer in cui verranno installati il punto di gestione iniziale e il punto di distribuzione, se non sono installati nel server del sito  

-   Se si installa un nuovo sito primario figlio all'interno di un sito di amministrazione centrale, sono necessari i diritti aggiuntivi seguenti:  

    -   **Amministratore** nel computer che ospita il sito di amministrazione centrale  

    -   Diritti di amministrazione basata su ruoli in Configuration Manager equivalenti al ruolo di sicurezza **Amministratore infrastruttura** o **Amministratore completo**  

-   È necessario usare il supporto di installazione corretto (file di origine) ed eseguire il programma di installazione da tale percorso. Per informazioni sui file di origine corretti da usare per installare i diversi tipi di siti, vedere [Opzioni per l'installazione di diversi tipi di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) nell'argomento [Preparare l'installazione di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   Il computer server del sito deve avere accesso ai file di installazione aggiornati offerti da Microsoft in uno dei modi seguenti:
    -  Prima di iniziare l'installazione, è possibile scaricare e archiviare una copia di questi file nella rete locale usando il [downloader di installazione](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Se non è disponibile una copia locale di questi file, il server del sito deve avere accesso a Internet in modo da poter scaricare i file dal sito Microsoft durante l'installazione.

- Prima di espandere un sito primario autonomo in cui è installato un ruolo del sistema del sito relativo al punto di connessione del servizio, è necessario disinstallare il punto di connessione del servizio. In una gerarchia è consentita solo un'istanza di questo ruolo ed è consentita solo nel sito di livello superiore della gerarchia. Sarà possibile reinstallare il ruolo durante l'installazione del sito di amministrazione centrale.
- Il server del sito e i computer del database del sito devono soddisfare tutte le configurazioni dei prerequisiti. Prima di avviare il programma di installazione, è possibile [eseguire manualmente Controllo prerequisiti](../../../../core/servers/deploy/install/prerequisite-checker.md) per identificare e risolvere eventuali problemi.  


### <a name="bkmk_expand"></a> Prerequisiti per l'espansione di un sito primario autonomo
Un sito primario autonomo deve soddisfare i seguenti prerequisiti ai fini dell'espansione in una gerarchia con un sito di amministrazione centrale:

-   **È necessario installare il nuovo sito di amministrazione centrale usando i file inclusi nella cartella CD.Latest (contenente i file di origine), che corrispondono alla versione del sito primario autonomo**

 Per assicurarsi che la versione corrisponda, usare i file di origine presenti nella [cartella CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) del sito primario autonomo.

 Per altre informazioni sui file di origine corretti da usare per installare i diversi siti, vedere [Opzioni per l'installazione di diversi tipi di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) nell'argomento [Preparare l'installazione di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **Non è possibile configurare il sito primario autonomo per eseguire la migrazione dei dati da un'altra gerarchia di Configuration Manager**  

     È necessario interrompere la migrazione attiva al sito primario autonomo da altre gerarchie di Configuration Manager e rimuovere tutte le configurazioni per la migrazione, inclusi i processi di migrazione che non sono stati completati, la raccolta dati e la configurazione della gerarchia di origine attiva.  

     Ciò è necessario perché le operazioni di migrazione sono eseguite dal sito superiore della gerarchia e le configurazioni per la migrazione non vengono trasferite al sito di amministrazione centrale quando si espande un sito primario autonomo.  

     Se si riconfigura la migrazione nel sito primario dopo l'espansione del sito primario autonomo, le operazioni correlate alla migrazione vengono eseguite dal sito di amministrazione centrale. Per altre informazioni sulla configurazione della migrazione, vedere [Configurare gerarchie di origine e siti di origine per la migrazione a System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **L'account del computer che ospiterà il nuovo sito di amministrazione centrale deve essere un membro del gruppo utenti Amministratore nel sito primario autonomo**  

     Per espandere correttamente il sito primario autonomo, l'account computer del nuovo sito di amministrazione centrale deve avere diritti di **Amministratore** nel sito primario autonomo. Ciò è richiesto solo durante l'espansione del sito. L'account può essere rimosso dal gruppo utenti nel sito primario al termine dell'espansione del sito.  

-   **L'account utente che esegue il programma di installazione per installare il nuovo sito di amministrazione centrale deve avere i diritti di amministrazione basata su ruoli nel sito primario autonomo**  

     Per installare un sito di amministrazione centrale come parte di un'espansione del sito, l'account utente che esegue il programma di installazione per installare il sito di amministrazione centrale deve essere definito nell'amministrazione basata su ruoli nel sito primario autonomo come **Amministratore completo** o **Amministratore infrastruttura**.  

-   **Per espandere il sito, è necessario prima disinstallare i ruoli seguenti di sistema del sito dal sito primario autonomo:**  

    -   Punto di sincronizzazione di Asset Intelligence  
    -   Punto di Endpoint Protection  
    -   punto di connessione del servizio  

   Questi ruoli del sistema del sito sono supportati solo nel sito di livello superiore della gerarchia. È necessario pertanto disinstallare questi ruoli di sistema del sito prima di espandere il sito primario autonomo. Al termine dell'espansione, è possibile reinstallare questi ruoli del sistema del sito nel sito di amministrazione centrale.  

    Tutti gli altri ruoli del sistema del sito possono rimanere installati nel sito primario.  

-   **La porta per SQL Server Service Broker tra il sito primario autonomo e il computer che installerà il sito di amministrazione centrale deve essere aperta**  

     Per replicare correttamente i dati tra un sito di amministrazione centrale e un sito primario, Configuration Manager richiede una porta aperta tra i due siti per SSB. Quando si installa un sito di amministrazione centrale e si espande un sito primario autonomo, il controllo dei prerequisiti non verifica che la porta specificata per SSB sia aperta nel sito primario.  

**Problemi noti dopo la configurazione dei servizi di Azure:**  
Quando si usa uno dei seguenti servizi di Azure con Configuration Manager e si prevede di espandere un sito, dopo l'espansione del sito è necessario rimuovere e quindi ricreare la connessione al servizio.

Servizi:  
-       [Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS)
-       [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)
-       [Windows Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

Attenersi a questa procedura per risolvere il problema:
 1.    Nella console di Configuration Manager eliminare il servizio di Azure dal nodo dei servizi di Azure.
 2.    Nel portale di Azure eliminare il tenant associato al servizio dal nodo dei tenant di Azure Active Directory.  Questa procedura elimina anche l'app Web di Azure AD associata al servizio.  
 3.   Riconfigurare la connessione al servizio di Azure per l'uso con Configuration Manager.


## <a name="bkmk_secondary"></a> Siti secondari
Di seguito vengono elencati i prerequisiti per l'installazione di siti secondari:
-   L'amministratore che configura l'installazione del sito secondario nella console di Configuration Manager deve avere i diritti di amministrazione basata su ruoli equivalenti al ruolo di sicurezza di **Amministratore infrastruttura** o **Amministratore completo**.  
-   L'account computer del sito primario padre deve essere un **amministratore** nel computer server del sito secondario.  
-   Quando il sito secondario usa un'istanza di SQL Server installata in precedenza per ospitare il database del sito secondario:  

    -   L' **account computer** del sito primario padre deve avere i diritti di **amministratore di sistema** sull'istanza di SQL Server sul computer server del sito secondario.  

    -   L'account di **sistema locale** del computer server del sito secondario deve avere i diritti di **amministratore di sistema** sull'istanza di SQL Server sul computer server del sito secondario.  

        > [!IMPORTANT]  
        >  Al termine dell'installazione, entrambi gli account devono mantenere diritti di amministratore di sistema per SQL Server. Non rimuovere i diritti di amministratore di sistema da questi account.  

-   Il computer server del sito secondario deve soddisfare tutte le configurazioni richieste, inclusi SQL Server e i ruoli del sistema del sito predefiniti del punto di gestione e del punto di distribuzione.  

