---
title: Preparare l'installazione di siti | System Center Configuration Manager
description: "Leggere queste informazioni dettagliate per risparmiare tempo durante l'installazione di più siti ed evitare errori."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6f240f1da4561c05bee974b78f43bfcdba591df6

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Preparare l'installazione di siti di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per prepararsi a una corretta distribuzione di uno o più siti di System Center Configuration Manager, acquisire familiarità con i dettagli in questo articolo. Questi passaggi possono aiutare a risparmiare tempo durante l'installazione di più siti ed evitare errori che potrebbero richiedere una nuova installazione di uno o più siti.
 > [!TIP]
 >  Gli scenari seguenti sono simili, ma non identici, all'installazione del sito di System Center Configuration Manager (Current Branch):
 > -  **Eseguire l'aggiornamento**: installare System Center Configuration Manager per **eseguire l'aggiornamento** da System Center 2012 Configuration Manager; vedere [Eseguire l'aggiornamento a System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)
 > -  **Eseguire l'aggiornamento**: usare gli aggiornamenti nella console per installare una nuova **versione di aggiornamento** in un sito esistente di System Center Configuration Manager; vedere [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/manage/updates.md)
 > -  **Eseguire la migrazione**: per **eseguire la migrazione dei dati** da un'altra gerarchia di Configuration Manager alla gerarchia corrente di System Center Configuration Manager, vedere [Pianificazione della migrazione a System Center Configuration Manager](../../../../core/migration/planning-for-migration.md)



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Opzioni per l'installazione di diversi tipi di siti
Quando si installa un nuovo Configuration Manager, la versione dei file di origine che è possibile usare dipende dalla versione dei siti che si trovano già nella gerarchia e i metodi di installazione disponibili dipendono dal tipo di sito che si vuole installare.  

Prima di installare i siti, assicurarsi di aver pianificato la gerarchia e di aver definito il tipo di sito che si vuole installare. Per altre informazioni, vedere [Progettare una gerarchia di siti](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Primo sito
Il primo sito da installare per una gerarchia è un sito di amministrazione centrale o un sito primario autonomo.

**Supporti di installazione**: per installare un sito di amministrazione centrale o un sito primario autonomo come primo sito di una nuova gerarchia, è necessario [usare una versione di base](../../../../core/servers/manage/updates.md#bkmk_Baselines) di Configuration Manager. Non installare il primo sito di una nuova gerarchia usando i file di origine aggiornati presenti nella [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) di qualsiasi sito.

**Metodo di installazione**: è possibile installare uno dei tipi di sito tramite l'[Installazione guidata di System Center Configuration Manager ](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) oppure è possibile configurare uno script da usare con un'[installazione dalla riga di comando con script](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Siti aggiuntivi
Dopo aver installato il sito iniziale, è possibile aggiungere altri siti in qualsiasi momento. Sono disponibili le opzioni seguenti per aggiungere altri siti (fino ai [limiti supportati ](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

Siti attualmente disponibili          |Siti aggiuntivi che è possibile installare  
---------                   |---------
Sito di amministrazione centrale |   Installare un sito primario figlio            
Sito primario figlio          |   Installare un sito secondario        
Sito primario autonomo    |   Installare un sito secondario<br />Espandere il sito primario, che converte il sito primario autonomo in un sito primario figlio

**Supporti di installazione**: quando si installa un sito di amministrazione centrale per espandere un sito primario autonomo o si installa un nuovo sito primario figlio in una gerarchia esistente, è necessario usare il supporto di installazione (file di origine) corrispondente alla versione del sito o dei siti esistenti.
> [!IMPORTANT]
> Se sono stati installati nella console aggiornamenti che hanno modificato la versione dei siti installati in precedenza, non usare il supporto di installazione originale, ma usare i file di origine della [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) di un sito aggiornato.  Configuration Manager richiede l'uso di file di origine corrispondenti alla versione del sito esistente a cui si connetterà il nuovo sito.


Un sito secondario deve essere installato dalla console di Configuration Manager, che esegue sempre installazioni usando i file di origine dal sito primario padre.

**Metodo di installazione**: il metodo usato per installare altri siti dipende dal tipo di sito che si vuole installare.
-   **Aggiunta di un sito di amministrazione centrale**:  
È possibile usare l'Installazione guidata di Configuration Manager o una riga di comando con script per installare il nuovo sito di amministrazione centrale come sito padre per il sito primario autonomo esistente.  Per altre informazioni, vedere [Espandere un sito primario autonomo](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Aggiunta di un sito primario figlio**:  
È possibile usare l'Installazione guidata di Configuration Manager o un'installazione da riga di comando per aggiungere un sito primario figlio sotto un sito di amministrazione centrale.
-   **Aggiunta di un sito secondario**:   
Per installare un sito secondario come sito figlio al di sotto del sito primario, usare la console di Configuration Manager. Altri metodi non sono supportati per i siti secondari.



## <a name="a-namebkmktasksa-common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a> Attività comuni da completare prima di avviare un'installazione
-   Capire la topologia della gerarchia che verrà usata per la distribuzione    
     (vedere [Progettare una gerarchia di siti per System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md))  

-   Preparare e configurare singoli server per soddisfare i prerequisiti e le configurazioni supportate per l'uso con Configuration Manager (vedere [Prerequisiti del sito e del sistema del sito](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md))  

-   Installare e configurare SQL Server per ospitare il database del sito (vedere    
    [Supporto per le versioni di SQL Server per System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md))  

-   Preparare l'ambiente di rete per il supporto di Configuration Manager (vedere [Configurare firewall, porte e domini per la preparazione di Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains))  

-   Se si usa una PKI, preparare l'infrastruttura e i certificati (vedere [Requisiti dei certificati PKI per Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md)

-   Installare gli ultimi aggiornamenti sulla sicurezza nei computer che verranno usati come server del sito o server di sistema del sito e avviarli quando è necessario.



## <a name="a-namebkmksitecodesa-about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Informazioni su nomi e codici dei siti
I codici e i nomi dei siti dei vengono usati per identificare e gestire i siti in una gerarchia di Configuration Manager. Nella console di Configuration Manager il codice e il nome del sito vengono visualizzati nel formato &lt;codice sito\> - &lt;nome sito\>. È necessario che ogni codice di sito usato nella gerarchia sia univoco. Se lo schema di Active Directory viene esteso a Configuration Manager e i siti pubblicano dati, i codici di sito usati in una foresta di Active Directory devono essere univoci, anche se vengono usati in una gerarchia diversa di Configuration Manager o sono stati usati in installazioni precedenti di Configuration Manager. Assicurarsi di pianificare con attenzione i codici e i nomi di sito prima della distribuzione della gerarchia.

### <a name="specify-a-site-code-and-site-name"></a>Specificare un codice e un nome del sito
Durante l'installazione di Configuration Manager vengono richiesti un codice e un nome di sito per il sito di amministrazione centrale e per ogni installazione di sito primario e secondario. Il codice del sito deve identificare in modo univoco ogni sito nella gerarchia. Poiché il codice del sito viene usato nei nomi di cartella, non usare mai i nomi seguenti per il codice del sito, che includono nomi riservati di Configuration Manager e di Windows:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Configuration Manager non verifica se il codice del sito specificato è già in uso.



Per specificare il codice per un sito durante l'installazione di Configuration Manager, è necessario immettere tre caratteri alfanumerici. Quando si specificano codici del sito, sono consentite solo le lettere dalla A alla Z, i numeri da 0 a 9 oppure combinazioni di tali numeri e lettere. La sequenza di lettere o numeri non ha alcun effetto sulla comunicazione tra siti. Ad esempio, non è necessario nominare un sito primario ABC e un sito secondario DEF.

Il nome del sito è un identificatore di nome descrittivo per il sito. Usare solo i caratteri standard dalla A alla Z, dalla a alla z, da 0 a 9 e il trattino (-) nei nomi sito.
> [!IMPORTANT]
> La modifica del codice del sito o del nome sito dopo l'installazione non è supportata.

### <a name="reuse-a-site-code"></a>Riutilizzare un codice del sito
I codici del sito non possono essere usati più di una volta in una gerarchia di Configuration Manager per un sito di amministrazione centrale o per siti primari, anche se il sito di origine e il codice del sito sono stati disinstallati. Se si usa di nuovo un codice del sito, si rischiano conflitti tra ID di oggetti nella gerarchia. È possibile riusare il codice del sito per un sito secondario se il sito secondario e il codice del sito non sono più in uso nella gerarchia di Configuration Manager o nella foresta di Active Directory.


## <a name="limits-and-restrictions-for-installed-sites"></a>Limiti e restrizioni per i siti installati
Prima di installare i siti, capire le limitazioni seguenti che si applicano a siti e gerarchie:
-   Al termine dell'installazione, non è possibile modificare le proprietà del sito seguenti senza disinstallare il sito e quindi reinstallarlo con i nuovi valori:  
    -   Directory di installazione dei programmi  
    -   Codice sito  
    -   Descrizione sito  
-   Se la gerarchia include un sito di amministrazione centrale:  
    -   Configuration Manager non consente di spostare un sito primario figlio da una gerarchia per creare un sito primario autonomo o aggiungerlo a un'altra gerarchia. Al contrario, disinstallare il sito primario figlio e reinstallarlo come nuovo sito primario autonomo o come figlio del sito di amministrazione centrale di un'altra gerarchia.  


## <a name="a-namebkmkoptionalstepsa-optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a> Procedura facoltativa da seguire prima di avviare il programma di installazione
**È possibile eseguire manualmente [Downloader di installazione](../../../../core/servers/deploy/install/setup-downloader.md)** per scaricare i file di installazione aggiornati per Configuration Manager.

Se il computer in cui si eseguirà l'installazione non è connesso a Internet o se si prevede di installare più server del sito, considerare di usare il Downloader di installazione per scaricare gli aggiornamenti necessari per i file di installazione:

-  Per impostazione predefinita, il programma di installazione si connetterà a Internet per scaricare i file di installazione aggiornati
-  Per impostazione predefinita, i file vengono archiviati in una cartella denominata Redist
-  È possibile indirizzare il programma di installazione a un percorso nella rete in cui è stata precedentemente memorizzata una copia di questi file


**È possibile eseguire manualmente [Controllo prerequisiti](../../../../core/servers/deploy/install/prerequisite-checker.md)** per identificare e risolvere i problemi prima di eseguire il programma di installazione. Prima di avviare l'installazione di un sito e di installare un ruolo di sistema del sito in un server, è possibile eseguire il Controllo prerequisiti per verificare che il computer soddisfi i requisiti per ospitare il sito o il ruolo di sistema del sito.
 -  Per impostazione predefinita, il programma di installazione esegue il Controllo prerequisiti.
 -  In caso di errori, il programma di installazione viene interrotto finché il problema non è risolto.


**Identificare le porte facoltative** da usare per i client e i sistemi del sito.
 -  Per impostazione predefinita, i client e i sistemi del sito usano porte predefinite per la comunicazione.
 -  Durante l'installazione è possibile configurare porte alternative.
 -  Per altre informazioni, vedere [Porte usate in System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md).



<!--HONumber=Nov16_HO1-->


