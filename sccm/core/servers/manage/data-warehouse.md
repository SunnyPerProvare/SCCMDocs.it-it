---
title: Data warehouse | Microsoft Docs
description: Punto di servizio e database del data warehouse per System Center Configuration Manager
ms.custom: na
ms.date: 5/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: f11a53bbc85b40077b3909568db5ae5552b0456c
ms.contentlocale: it-it
ms.lasthandoff: 06/01/2017


---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>Punto di servizio del data warehouse per System Center Configuration Manager
*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1702 è possibile usare il punto di servizio del data warehouse per archiviare e creare report di dati cronologici a lungo termine per la distribuzione di Configuration Manager.

> [!TIP]  
> Introdotto con la versione 1702, il punto di servizio del data warehouse è una funzionalità di versione non definitiva. Per abilitarla, vedere [Usare le funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features).

Il data warehouse supporta fino a 2 TB di dati, con timestamp per il rilevamento delle modifiche. L'archiviazione dei dati viene eseguita tramite sincronizzazioni automatizzate dal database del sito di Configuration Manager al database del data warehouse. Queste informazioni diventano quindi accessibili dal punto di Reporting Services.


Tra i dati sincronizzati sono inclusi i dati seguenti dai gruppi di dati globali e del sito:
- Integrità dell'infrastruttura
- Sicurezza
- Conformità
- Malware   
- Distribuzioni software
- Dettagli relativi all'inventario. La cronologia dell'inventario, tuttavia, non è sincronizzata

Quando viene installato, il ruolo del sistema del sito installa e configura il database del data warehouse. Vengono inoltre installati alcuni report che semplificano le attività di ricerca dei dati e di creazione dei report.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Prerequisiti per il punto di servizio del data warehouse
- Il computer in cui si installa il ruolo del sistema del sito richiede .NET Framework 4.5.2 o versioni successive.
- L'account del computer in cui si installa il ruolo del sistema del sito viene usato per sincronizzare i dati con il database del data warehouse. L'account richiede le autorizzazioni seguenti:  
  - **Amministratore** nel computer che ospiterà il database del data warehouse.
  - **DB_owner** per il database del data warehouse.
  - **DB_reader** ed **execute** per il database del sito dei siti di livello superiore.
-    Il database del data warehouse è supportato in un'istanza predefinita o denominata di SQL Server 2012 o versioni successive. L'edizione deve essere Enterprise o Datacenter.
  - Gruppo di disponibilità AlwaysOn di SQL Server: questa configurazione non è supportata.
  - Cluster di SQL Server: i cluster di failover di SQL Server non sono supportati. Questo supporto non è disponibile perché il database del data warehouse non è stato testato in profondità nei cluster di failover di SQL Server.
  - Quando il database del data warehouse è remoto rispetto al database del server del sito, è necessario avere una licenza separata per l'istanza di SQL Server che ospita il database.

> [!IMPORTANT]  
> Il data warehouse non è supportato se il computer che esegue il punto di servizio del data warehouse o che ospita il database del data warehouse esegue una delle lingue seguenti:
> - JPN - Giapponese
> - KOR - Coreano
> - CHS - Cinese semplificato
> - CHT - Cinese tradizionale. Il problema verrà risolto in una versione successiva.


## <a name="install-the-data-warehouse"></a>Installare il data warehouse
È possibile installare il ruolo del sistema del sito del data warehouse solo nel sito di livello superiore nella gerarchia, ovvero un sito di amministrazione centrale o il sito primario autonomo.

Ogni gerarchia supporta una singola istanza di questo ruolo e può trovarsi in qualsiasi sistema del sito di livello superiore. L'istanza di SQL Server che ospita il database del data warehouse può essere locale nel ruolo del sistema del sito o remota. Anche se il data warehouse funziona con il punto di Reporting Services installato nello stesso sito, non è necessario che i due ruoli del sistema del sito siano installati nello stesso server.   

Per installare il ruolo, usare l'**Aggiunta guidata ruoli del sistema del sito** o la **Creazione guidata server del sistema sito**. Per altre informazioni, vedere [Installare ruoli del sistema del sito](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Quando si installa il ruolo, Configuration Manager crea il database del data warehouse nell'istanza di SQL Server specificata dall'utente. Se si specifica il nome di un database esistente, come si farebbe se si [spostasse il database del data warehouse in un nuovo SQL Server](#move-the-data-warehouse-database), Configuration Manager non crea un nuovo database, ma usa invece quello specificato dall'utente.

### <a name="configurations-used-during-installation"></a>Configurazioni usate durante l'installazione
Pagina **Selezione ruolo del sistema**:  

Pagina **Generale**:
-     **Impostazioni di connessione del database del data warehouse di Configuration Manager**:
 - **Nome di dominio completo di SQL**:  
 Specificare il nome di dominio completo (FQDN, Full Qualified Domain Name) del server che ospita il database del punto di servizio del data warehouse.
 - **Nome istanza di SQL Server, se applicabile**:   
 Se non si usa un'istanza predefinita di SQL Server, è necessario specificare l'istanza.
 - **Nome database**:   
 Specificare il nome del database del data warehouse.  Configuration Manager creerà il database del data warehouse con questo nome. Se si specifica un nome di database già esistente nell'istanza di SQL Server, Configuration Manager userà il database corrispondente.
 - **Porta di SQL Server usata per la connessione**:   
 Specificare il numero di porta TCP/IP configurato per l'istanza di SQL Server che ospita il database del data warehouse. Questa porta viene usata dal servizio di sincronizzazione del data warehouse per la connessione al database del data warehouse.  

Pagina **Pianificazione della sincronizzazione**:   
- **Pianificazione della sincronizzazione**:
 - **Ora di inizio**:  
 Specificare l'ora in cui si vuole avviare la sincronizzazione del data warehouse.
 - **Criterio ricorrenza**:
    - **Ogni giorno**: specificare che la sincronizzazione viene eseguita ogni giorno.
    - **Ogni settimana**: specificare un solo giorno alla settimana e la ricorrenza settimanale per la sincronizzazione.

## <a name="reporting"></a>Reporting
Dopo aver installato un punto di servizio del data warehouse, diversi report diventano disponibili nel punto di Reporting Services installato nello stesso sito. Se si installa il punto di servizio del data warehouse prima di installare un punto di Reporting Services, i report verranno aggiunti automaticamente quando in seguito si installerà il punto di Reporting Services.

Il ruolo del sistema del sito del data warehouse include i report seguenti, che hanno una categoria di **Data Warehouse**:
 - **Application Deployment - Historical** (Distribuzione applicazioni - Cronologia):   
 Visualizza i dettagli per la distribuzione di applicazioni per un'applicazione e un computer specifici.
 - **Endpoint Protection and Software Update Compliance - Historical** (Endpoint Protection e Conformità dell'aggiornamento software - Cronologia): visualizza i computer in cui mancano aggiornamenti software.  
 - **General Hardware Inventory - Historical** (Inventario generale hardware - Cronologia):      
 Visualizza tutto l'inventario dell'hardware per un computer specifico.
 - **General Software Inventory - Historical** (Inventario generale software - Cronologia):      
 Visualizza tutto l'inventario del software per un computer specifico.
 - **Infrastructure Health Overview - Historical** (Panoramica integrità infrastruttura - Cronologia):     
 Visualizza una panoramica dell'integrità dell'infrastruttura di Configuration Manager
 - **List of Malware Detected - Historical** (Elenco di malware rilevato - Cronologia):     
 Visualizza il malware che è stato rilevato nell'organizzazione.
 - **Software Distribution Summary - Historical** (Riepilogo distribuzione software - Cronologia):     
 Riepilogo della distribuzione del software per un annuncio e un computer specifici.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Espandere un sito primario autonomo esistente in una gerarchia
Prima di installare un sito di amministrazione centrale per espandere un sito primario autonomo esistente, è necessario disinstallare il ruolo del punto di servizio del data warehouse. Dopo aver installato il sito di amministrazione centrale, è possibile installare il ruolo del sistema del sito nel sito di amministrazione centrale.  

A differenza di uno spostamento del database del data warehouse, questa modifica comporta la perdita dei dati cronologici sincronizzati in precedenza nel sito primario. Le operazioni di backup del database dal sito primario e di ripristino nel sito di amministrazione centrale non sono supportate.




## <a name="move-the-data-warehouse-database"></a>Spostare il database del data warehouse
Per spostare il database del data warehouse in un nuovo SQL Server, procedere come segue:

1.    Usare SQL Server Management Studio per eseguire il backup del database del data warehouse e quindi ripristinare il database in un'istanza di SQL Server nel nuovo computer che ospiterà il data warehouse.   
> [!NOTE]     
> Dopo aver ripristinato il database nel nuovo server, assicurarsi che le autorizzazioni di accesso al database per il nuovo database del data warehouse siano le stesse del data warehouse originale.  

2.    Usare la console di Configuration Manager per rimuovere il ruolo del sistema del sito del punto di servizio del data warehouse dal server corrente.
3.    Reinstallare il punto di servizio del data warehouse e specificare il nome della nuova istanza di SQL Server e dell'istanza che ospita il database del data warehouse appena ripristinato.
4.    Dopo l'installazione del ruolo del sistema del sito, lo spostamento è completato.

## <a name="troubleshooting-data-warehouse-issues"></a>Risoluzione dei problemi del data warehouse
**File di log**:  
Usare i log seguenti per analizzare i problemi dell'installazione del punto di servizio del data warehouse o della sincronizzazione dei dati:
 - *DWSSMSI.log* e *DWSSSetup.log*: questi log consentono di analizzare gli errori che si verificano durante l'installazione del punto di servizio del data warehouse.
 - *Microsoft.ConfigMgrDataWarehouse.log*: questo log consente di analizzare la sincronizzazione dei dati tra il database del sito e il database del data warehouse.

**Errore di installazione**  
 L'installazione del punto di servizio del data Warehouse non riesce nel server di sistema di un sito remoto quando il data warehouse è il primo ruolo del sistema del sito installato in tale computer.  
  - **Soluzione**:   
    Verificare che il computer in cui si installa il punto di servizio del data warehouse ospiti già almeno un altro ruolo del sistema del sito.  


**Problemi di sincronizzazione noti**:   
La sincronizzazione non riesce e restituisce il messaggio seguente nel file *Microsoft.ConfigMgrDataWarehouse.log*: **"failed to populate schema objects"** (non è stato possibile popolare gli oggetti dello schema)  
 - **Soluzione**:  
    Verificare che l'account del computer che ospita il ruolo del sistema del sito sia un **db_owner** nel database del data warehouse.

Non è possibile aprire i report del data warehouse quando il database del data warehouse e il punto di Reporting Services si trovano in sistemi del sito diversi.  

 - **Soluzione**:  
    Concedere ad **Account punto di Reporting Services** l'autorizzazione **db_datareader** per il database del data warehouse.

Quando si apre un report del data warehouse, viene restituito l'errore seguente:

*Errore durante l'elaborazione del report. (rsProcessingAborted) Non è possibile creare una connessione all'origine dati 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) La connessione con il server è stata stabilita correttamente, ma poi si è verificato un errore durante l'handshake pre-login. (provider: Provider SSL, errore: 0 - La catena di certificati è stata emessa da un'autorità non disponibile nell'elenco locale.)*

- **Soluzione**: attenersi alla procedura seguente per configurare i certificati:

  1. Nel computer che ospita il database del data warehouse:

    1. Aprire IIS, fare clic su **Certificati del server**, fare clic con il pulsante destro del mouse su **Crea certificato autofirmato** e quindi specificare il "nome descrittivo" del nome del certificato come **Certificato di identificazione SQL Server del data warehouse**. Selezionare l'archivio certificati come **Personale**.
    2. Aprire **Gestione configurazione SQL Server** in **Configurazione di rete SQL Server**, fare clic con il pulsante destro del mouse per selezionare **Proprietà** in **Protocolli per MSSQLSERVERR**. Quindi, nella scheda **Certificato** selezionare **Certificato di identificazione SQL Server del data warehouse** come certificato e salvare le modifiche.  
    3. Aprire **Gestione configurazione SQL Server** in **Servizi di SQL Server**, riavviare **Servizio SQL Server** e **Servizio di creazione report**.
    4.    Aprire Microsoft Management Console (MMC), aggiungere lo snap-in per **Certificati** e quindi selezionare **Account del computer** per gestire il certificato per l'account del computer locale. Quindi, in MMC espandere la cartella **Personale** > **Certificati** ed esportare **Certificato di identificazione SQL Server del data warehouse** come file **Binario codificato DER x.509 (.CER)**.    
  2.    Nel computer che ospita SQL Server Reporting Services, aprire MMC, aggiungere lo snap-in per **Certificati** e quindi selezionare **Account del computer** per gestire il certificato per l'account del computer locale. Nella cartella **Autorità di certificazione principale attendibili** importare **Certificato di identificazione SQL Server del data warehouse**.


## <a name="data-warehouse-dataflow"></a>Flusso dei dati del data warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

**Sincronizzazione e archiviazione dei dati**

| Passaggio   | Dettagli  |
|:------:|-----------|  
| **1**  |     Il server del sito trasferisce e archivia i dati nel database del sito.  |  
| **2**  |      In base alla pianificazione e alla configurazione, il punto di servizio del data warehouse recupera dati dal database del sito.  |  
| **3**  |  Il punto di servizio del data warehouse trasferisce e archivia una copia dei dati sincronizzati nel database del data warehouse. |  
**Creazione di report**

| Passaggio   | Dettagli  |
|:------:|-----------|  
| **A**  |  Un utente richiede i dati usando i report predefiniti. Questa richiesta viene passata al punto di Reporting Services tramite SQL Server Reporting Services. |  
| **B**  |      La maggior parte dei report sono usati per informazioni correnti e queste richieste vengono eseguite tramite il database del sito. |  
| **C**  | Se un report richiede dati cronologici, tramite un report con *Categoria* corrispondente a **Data warehouse** la richiesta viene eseguita tramite il database del data warehouse.   |  

