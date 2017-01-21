---
title: Installare scenari | Microsoft Docs
description: Informazioni sulle tecniche per installare una nuova gerarchia di Configuration Manager quando si esegue un aggiornamento.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 8333f9280f609c761ba5368b801d273f9a11ebb5


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Scenari per semplificare l'installazione di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il rilascio di versioni di aggiornamento per System Center Configuration Manager (Current Branch) offre nuovi scenari per semplificare l'installazione di una nuova gerarchia in una versione di aggiornamento, (ad esempio l'aggiornamento 1602), e per l'aggiornamento da Microsoft System Center 2012 Configuration Manager.  

Gli scenari supportati includono:  

**Installare una nuova gerarchia di System Center Configuration Manager (Current Branch)** che esegua una versione di aggiornamento:  

-   Si installa solo il sito di livello superiore, installando subito dopo un aggiornamento che porta il sito alla versione di aggiornamento che si userà. È quindi possibile installare altri siti direttamente con quella versione di aggiornamento.  

-   Questo scenario evita la necessità di installare altri siti a un livello di base e di doverli poi aggiornare alla versione di aggiornamento che si vuole usare.  

-   Questo scenario evita la necessità di installare i client a un livello di base per poi doverli reinstallare quando si esegue l'aggiornamento a una versione più recente.  

**Aggiornare l'infrastruttura di Microsoft System Center 2012 Configuration Manager** a una versione di System Center Configuration Manager:  

-   Prima di installare una versione di aggiornamento, ad esempio 1602, occorre aggiornare manualmente il sito di amministrazione centrale e ogni sito primario a una versione di base, ad esempio 1511.  

-   Non è possibile aggiornare siti secondari da Microsoft System Center 2012 Configuration Manager finché i siti primari non eseguono la versione di aggiornamento da usare.  

-   Non è possibile aggiornare i client da Microsoft System Center 2012 Configuration Manager finché i siti primari non eseguono la versione di aggiornamento da usare.  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>Scenario: installazione di una nuova gerarchia con una versione di aggiornamento  
In questo scenario di esempio si installa il primo sito di una gerarchia usando la versione di base 1511 di System Center Configuration Manager. Quindi si installa l'aggiornamento 1602 prima di distribuire altri siti o client.  

-   Dato che si prevede di usare una versione di aggiornamento, ad esempio 1602, invece della versione di base, ad esempio 1511, non è necessario installare altri siti o client e quindi aggiornarli.  

-   Non si installano siti secondari con la versione 1511 per poi aggiornarli alla versione 1602. Verranno invece installati quando i siti primari eseguono la versione 1602.  

**Usare la sequenza seguente:**  

1.  **Installare un sito principale per la nuova gerarchia** usando il supporto di base.  

    -   Si può usare solo il supporto di base per installare il primo sito di una nuova gerarchia.  

    -   Ad esempio, installare un sito principale usando la versione 1511. Vedere [Usare l'Installazione guidata per installare siti](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)  

    Dopo questo passaggio, il sito principale esegue la versione 1511.  

2.  **Usare gli aggiornamenti nella console per aggiornare il sito principale a una versione più recente.**  

    -   Prima di installare eventuali client o siti figlio, aggiornare il sito principale alla versione di aggiornamento che si intende usare.  

    -   Ad esempio, un sito principale che esegue la versione 1511 può essere aggiornato alla versione 1602. Vedere [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

    Dopo questo passaggio, il sito principale esegue la versione 1602.  

3.  **Installare nuovi siti primari figlio in un sito di amministrazione centrale.**  

    -   Usare il supporto di installazione disponibile nella cartella CD.Latest sul server del sito di amministrazione centrale per installare i siti primari figlio.  Vedere [Cartella CD.Latest per System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

        -   Questo supporto di origine è necessario per assicurare che i nuovi siti primari figlio corrispondano alla versione del sito di amministrazione centrale.  

    Dopo questo passaggio, i nuovi siti primari figlio eseguono la versione 1602.  

4.  **In ogni sito primario usare l'opzione nella console per installare nuovi siti secondari.**  

    -   Dato che i siti secondari non sono stati installati quando i siti primari eseguivano la versione 1511, non è necessario aggiornarli.  

    -   Si installano invece nuovi siti secondari che eseguono la versione 1602. Vedere *Installare un sito secondario* in [Usare l'Installazione guidata per installare siti](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

    Dopo questo passaggio, i nuovi siti secondari sono installati ed eseguono la versione 1602.  

5.  **Installare nuovi client nel sito primario.**  

    -   Dato che i client non sono stati installati quando i siti primari eseguivano la versione 1511, non è necessario aggiornarli dalla versione 1511 alla versione 1602.  

    -   Vengono invece installati nuovi client che eseguono la versione 1602. Vedere [Distribuire i client in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

    Dopo questo passaggio, i nuovi client sono installati ed eseguono la versione 1602.  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Scenario: aggiornamento di System Center 2012 Configuration Manager a una versione di aggiornamento di System Center Configuration Manager Current Branch  
In questo scenario di esempio, viene aggiornata l'infrastruttura di Microsoft System Center 2012 Configuration Manager a System Center Configuration Manager versione 1602.  

-   Il sito di amministrazione centrale e ciascun sito primario devono eseguire l'aggiornamento alla versione di base 1511 prima di installare l'aggiornamento per la versione 1602.  

-   I siti secondari e i client non vengono aggiornati o installati con la versione 1511. Al contrario, si spostano direttamente da Microsoft System Center 2012 Configuration Manager a System Center Configuration Manager versione 1602.  

**Usare la sequenza seguente:**  

1.  **Aggiornare il sito principale di Microsoft System Center 2012 Configuration Manager** alla versione di base Current Branch usando i supporti di origine per System Center Configuration Manager (ad esempio la versione 1511). Vedere [Eseguire l'aggiornamento a System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

    -   Come per gli scenari di aggiornamento tradizionali, si aggiorna sempre prima il sito principale della gerarchia e quindi i siti figlio.  

    Dopo questo passaggio, il sito principale esegue la versione 1511.  

2.  **Aggiornare ogni sito primario figlio nella gerarchia** alla stessa versione di base.  

    -   Quando si esegue l'aggiornamento da Microsoft System Center 2012 Configuration Manager, è necessario aggiornare manualmente ogni sito primario a una versione di base Current Branch.  

    -   In questa fase non si aggiornano i siti secondari.  

    Dopo questo passaggio, ogni sito primario esegue la versione 1511.  

3.  **Impostare le finestre di manutenzione nei siti primari figlio.** Dopo aver aggiornato tutti i siti primari alla versione di base, pianificare la configurazione di finestre di manutenzione per controllare quando quei siti installano aggiornamenti dell'infrastruttura. Vedere [Come usare le finestre di manutenzione in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  Le finestre di manutenzione sono dette intervalli di servizio nella versione 1511.  

    -   Un sito primario figlio installa gli stessi aggiornamenti installati in un sito di amministrazione centrale.  

    -   I siti secondari non installano automaticamente le nuove versioni e devono essere aggiornati manualmente dall'interno della console.  

    > [!NOTE]  
    >  Se si usa la versione 1511 e si vogliono usare gli intervalli di servizio, è necessario prima installare l'hotfix dall' [articolo 3142341 della Microsoft Knowledge Base](http://support.microsoft.com/kb/3142341). Questo problema viene risolto quando si installa l'aggiornamento 1602.  

    Dopo questo passaggio, quando si installano aggiornamenti nel sito di amministrazione centrale, verranno installati solo siti primari figlio che vengono aggiornati quando consentito dalla rispettiva finestra di manutenzione.  

4.  **Installare la versione di aggiornamento nel sito principale.** Il sito principale viene aggiornato. Dopo che un sito di amministrazione centrale installa la versione di aggiornamento, ogni sito primario figlio installa automaticamente l'aggiornamento a meno che non sia bloccato da una finestra di manutenzione.  

    -   Ad esempio, è possibile aggiornare un sito principale dalla versione 1511 alla versione 1602. Vedere [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

    Dopo questo passaggio, il sito di amministrazione centrale e ogni sito primario esegue la versione 1602.  

5.  **Aggiornare i siti secondari.** Dopo che un sito primario installa l'aggiornamento ed esegue la versione 1602, si può usare l'opzione nella console per aggiornare i siti secondari.  

    -   In questo modo i siti secondari vengono aggiornati da Microsoft System Center 2012 Configuration Manager alla versione di aggiornamento installata nel sito primario.  

    -   Per informazioni sull'aggiornamento di un sito secondario, vedere [Aggiornare i siti](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) in [Eseguire l'aggiornamento a System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6.  **Aggiornare i client.** Per informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

    -   In questo modo i client vengono aggiornati da Microsoft System Center 2012 Configuration Manager alla versione di aggiornamento installata nel sito primario.  

    Dopo questo passaggio, i client vengono aggiornati alla versione 1602 senza prima eseguire l'aggiornamento alla versione 1511.



<!--HONumber=Dec16_HO3-->


