---
title: Cluster di SQL Server | Microsoft Docs
description: Usare un cluster di SQL Server per ospitare il database del sito di System Center Configuration Manager. Include informazioni sulle opzioni supportate.
ms.custom: na
ms.date: 2/28/2017
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
ms.sourcegitcommit: ce0d7fc5f3d1812c4d62e551661c0ef89707567b
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.lasthandoff: 02/28/2017


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Usare un cluster di SQL Server per il database del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 È possibile usare un cluster di SQL Server per ospitare il database del sito di System Center Configuration Manager. Il database del sito è l'unico ruolo del sistema del sito supportato in un cluster del server.  

> [!IMPORTANT]  
>  La configurazione corretta dei cluster di SQL Server si basa sulla documentazione e le procedure incluse nella libreria della documentazione di SQL Server.  

 Un cluster consente di garantire supporto per il failover e migliorare l'affidabilità del database del sito. Non offre tuttavia vantaggi aggiuntivi di elaborazione o bilanciamento del carico. Infatti, può verificarsi una riduzione delle prestazioni perché il server del sito deve trovare il nodo attivo del cluster di SQL Server prima di connettersi al database del sito.  

 Prima di installare Configuration Manager, è necessario preparare il cluster di SQL Server per il supporto di Configuration Manager. Vedere i prerequisiti descritti più avanti in questa sezione.  

 Durante l'installazione di Configuration Manager il writer del Servizio Copia Shadow del volume (VSS) viene installato su ogni nodo dei computer fisici del cluster di Microsoft Windows Server. Ciò supporta l'attività di manutenzione **Backup server sito**.  

 Dopo aver installato il sito, Configuration Manager controlla le modifiche al nodo del cluster ogni ora. Configuration Manager gestisce automaticamente tutte le modifiche trovate che possono interessare le installazioni dei componenti di Configuration Manager, ad esempio un failover del nodo o l'aggiunta di un nodo nuovo al cluster di SQL Server.  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opzioni supportate per l'uso di un cluster di failover di SQL Server

Le opzioni seguenti sono supportate per i cluster di failover di SQL Server usati come database del sito:

-   Cluster a istanza singola  

-   Configurazione a più istanze  

-   Più nodi attivi  

-   Istanza predefinita o denominata  

Tenere presente i prerequisiti seguenti:  

-   Il database del sito deve essere lontano dal server del sito. Il cluster non può includere il server di sistema del sito.  

-   È necessario aggiungere l'account del computer del server del sito al gruppo Administrators locale di ogni server nel cluster.  

-   Per supportare l'autenticazione Kerberos, il protocollo di comunicazione di rete **TCP/IP** deve essere abilitato per la connessione di rete di ogni nodo del cluster di SQL Server. **Named pipes** non è obbligatorio, ma può essere usato per risolvere i problemi relativi all'autenticazione Kerberos. Le impostazioni del protocollo di rete vengono configurate in **Gestione configurazione SQL Server** di **Configurazione di rete SQL Server**.  

-   Se si usa un certificato PKI, vedere Requisiti dei certificati PKI per Configuration Manager per i requisiti specifici dei certificati quando si usa un cluster di SQL Server per il database del sito.  

Tenere presente le limitazioni seguenti:  

-   **Installazione e configurazione:**  

    -   I siti secondari non possono usare un cluster di SQL Server.  

    -   L'opzione per specificare percorsi file non predefiniti per il database del sito non è disponibile quando si usa un cluster di SQL Server.  

-   **Provider SMS:**  

    -   L'installazione di un'istanza del provider SMS in un cluster di SQL Server o in un computer in cui è in esecuzione un nodo di SQL Server in cluster non è supportata.  

-   **Opzioni di replica dei dati:**  

    -   Se si usano **viste distribuite**, non è possibile usare un cluster di SQL Server per ospitare il database del sito.  

-   **Backup e ripristino:**  

    -   Configuration Manager non supporta backup di Data Protection Manager (DPM) per un cluster di SQL Server che usa un'istanza denominata. Supporta tuttavia backup di DPM in un cluster di SQL Server che usa l'istanza predefinita di SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Preparare un'istanza di SQL Server in cluster per il database del sito  

Queste sono le attività principali da completare per preparare il database del sito:

-   Creare il cluster di SQL Server virtuale per ospitare il database del sito in un ambiente cluster di Windows Server esistente. Per passaggi dettagliati sull'installazione e configurazione di un cluster di SQL Server, vedere la documentazione specifica della versione di SQL Server in uso. Ad esempio, se si sta utilizzando SQL Server 2008 R2, vedere [Installing a SQL Server 2008 R2 Failover Cluster (Installazione di un cluster di failover SQL Server 2008 R2)](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   In ogni computer del cluster di SQL Server è possibile inserire un file nella cartella radice di ogni unità in cui non si vuole che Configuration Manager installi i componenti del sito. Il file deve essere denominato **NO_SMS_ON_DRIVE.SMS**. Per impostazione predefinita, Configuration Manager installa alcuni componenti in ogni nodo fisico per supportare alcune operazioni, ad esempio il backup.  

-   Aggiungere l'account computer del server del sito al gruppo **Amministratori locali** di ciascun computer del nodo del cluster Windows Server.  

-   Nell'istanza virtuale di SQL Server assegnare il ruolo **sysadmin** di SQL Server all'account utente che esegue il programma di installazione di Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Per installare un nuovo sito usando un'istanza cluster di SQL Server  
 Per installare un sito che usa un database del sito in cluster, eseguire il programma di installazione di Configuration Manager seguendo la normale procedura per l'installazione di un sito con la modifica seguente:  

-   Nella pagina **Informazioni database** specificare il nome dell'istanza virtuale del cluster di SQL Server che ospita il database del sito. L'istanza virtuale sostituisce il nome del computer che esegue SQL Server.  

    > [!IMPORTANT]  
    >  Al momento dell'immissione del nome dell'istanza virtuale del cluster di SQL Server, non immettere il nome Windows Server virtuale creato dal cluster di Windows Server. Se si usa il nome virtuale di Windows Server, il database del sito viene installato nel disco rigido locale del nodo del cluster di Windows Server attivo. In questo modo, si impedisce il failover se il nodo non riesce.  

