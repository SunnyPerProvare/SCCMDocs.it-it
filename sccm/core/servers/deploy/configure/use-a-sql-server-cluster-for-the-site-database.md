---
title: Cluster di SQL Server | Microsoft Docs
description: Usare un cluster di SQL Server per ospitare il database del sito di System Center Configuration Manager. Include informazioni sulle opzioni supportate.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: e5a001ee018e240396498d134c5e75e325eae275


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Usare un cluster di SQL Server per il database del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 È possibile usare un cluster di SQL Server per ospitare il database del sito di System Center Configuration Manager. Il database del sito è l'unico ruolo del sistema del sito supportato in un cluster del server.  

> [!NOTE]  
>  La corretta configurazione e i cluster di SQL Server richiedono che l'utente abbia una certa familiarità con la configurazione dei cluster di SQL Server e si basano sulla documentazione e sulle procedure fornite nella libreria della documentazione di SQL Server.  

 L'uso di un cluster consente di ottenere supporto per il failover e il miglioramento dell'affidabilità del database del sito. Tuttavia, l'uso di un database del sito in cluster, non fornisce ulteriori vantaggi in termini di elaborazione o bilanciamento del carico. Infatti, può verificarsi una riduzione delle prestazioni perché il server del sito deve trovare il nodo attivo del cluster di SQL Server prima che si connetta al database del sito.  

 Prima di installare Configuration Manager, è necessario preparare il cluster di SQL Server per il supporto di Configuration Manager. Vedere i prerequisiti descritti più avanti in questa sezione.  

 Durante l'installazione di Configuration Manager il writer del Servizio Copia Shadow del volume (VSS) viene installato su ogni nodo di computer fisico del cluster di Microsoft Windows Server per supportare l'attività di manutenzione **Backup server sito**.  

 Dopo aver installato il sito, Configuration Manager verifica ogni ora la presenza di modifiche al nodo del cluster e gestisce automaticamente le modifiche che interessano l'installazione del componente Configuration Manager, ad esempio un failover del nodo o l'aggiunta di un nuovo nodo al cluster di SQL Server.  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opzioni supportate per l'uso di un cluster di failover di SQL Server

-   Cluster a istanza singola  

-   Configurazione a più istanze  

-   Più nodi attivi  

-   Supporto per un'istanza predefinita o denominata  

**Prerequisiti:**  

-   Il database del sito deve essere lontano dal server del sito. Il cluster non può includere il server di sistema del sito.  

-   È necessario aggiungere l'account del computer server del sito al gruppo Amministratori locali di ciascun server nel cluster.  

-   Per supportare l'autenticazione Kerberos, il protocollo di comunicazione di rete **TCP/IP** deve essere abilitato per la connessione di rete di ogni nodo del cluster di SQL Server. **Named pipes** non è obbligatorio, ma può essere usato per risolvere i problemi relativi all'autenticazione Kerberos. Le impostazioni del protocollo di rete vengono configurate in **Gestione configurazione SQL Server** in **Configurazione di rete SQL Server**.  

-   Se si usa un certificato PKI, vedere i &lt;requisiti del certificato PKI per Configuration Manager, per informazioni sui requisiti specifici dei certificati quando si usa un cluster di SQL Server per il database del sito.  

**Limitazioni da considerare:**  

-   **Installazione e configurazione:**  

    -   I siti secondari non possono usare un cluster di SQL Server.  

    -   L'opzione per specificare percorsi file non predefiniti per il database del sito non è disponibile quando si usa un cluster di SQL Server.  

-   **Provider SMS:**  

    -   L'installazione di un'istanza del provider SMS su un cluster di SQL Server o un computer su cui è in esecuzione un nodo di SQL Server in cluster non è supportata.  

-   **Opzioni di replica dei dati:**  

    -   Se si usano le **viste distribuite**, non è possibile usare un cluster di SQL Server per ospitare il database del sito.  

-   **Backup e ripristino:**  

    -   Configuration Manager non supporta il backup DPM per un cluster SQL Server che usa un'istanza denominata ma supporta il backup DPM in un cluster SQL Server che usa l'istanza predefinita di SQL Server.  

## <a name="to-prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Per preparare un'istanza di SQL Server in cluster per il database del sito  

-   Creare il cluster di SQL Server virtuale per ospitare il database del sito in un ambiente cluster di Windows Server esistente. Per i passaggi dettagliati per installare e configurare un cluster di SQL Server, vedere la documentazione specifica per la relativa versione di SQL Server. Ad esempio, se si usa SQL Server 2008 R2, vedere l'argomento relativo all'  [installazione di un cluster di failover di SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkId=240231). Se si usa SQL Server 2014, vedere [Installazione del cluster di failover di SQL Server](https://technet.microsoft.com/library/hh231721\(v=sql.120\).aspx).  

-   Su ogni computer del cluster di SQL Server è possibile posizionare un file denominato **NO_SMS_ON_DRIVE.SMS** nella cartella radice di ogni unità in cui Configuration Manager non deve installare i componenti del sito. Per impostazione predefinita, Configuration Manager installa alcuni componenti su ogni nodo fisico a supporto di operazioni come il backup.  

-   Aggiungere l'account computer del server del sito al gruppo **Amministratori locali** di ciascun computer del nodo del cluster Windows Server.  

-   Nell'istanza virtuale di SQL Server assegnare il ruolo **sysadmin** di SQL Server all'account utente che esegue il programma di installazione di Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Per installare un nuovo sito usando un'istanza cluster di SQL Server  
 Per installare un sito che usa un database del sito in cluster, eseguire il programma di installazione di Configuration Manager seguendo la normale procedura per l'installazione di un sito con la modifica seguente:  

-   Nella pagina **Informazioni database** specificare il nome dell'istanza virtuale del cluster di SQL Server che ospita il database del sito.  L'istanza virtuale sostituisce il nome del computer che esegue SQL Server.  

    > [!IMPORTANT]  
    >  Al momento dell'immissione del nome dell'istanza virtuale del cluster di SQL Server, non immettere il nome Windows Server virtuale creato dal cluster di Windows Server. Se si usa il nome virtuale di Windows Server, il database del sito installa sul disco rigido locale del nodo del cluster di Windows Server attivo. In questo modo, si impedisce il failover se il nodo non riesce.  



<!--HONumber=Dec16_HO3-->


