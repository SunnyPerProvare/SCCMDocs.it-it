---
title: Controlli dei prerequisiti
titleSuffix: Configuration Manager
description: Informazioni di riferimento sugli specifici controlli dei prerequisiti per gli aggiornamenti di Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f17be653d206fd453cdafa4de159804f2fca816
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456686"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Elenco dei controlli dei prerequisiti per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra in dettaglio i controlli dei prerequisiti che vengono eseguiti quando si installa o si aggiorna Configuration Manager. Per altre informazioni, vedere [Controllo prerequisiti](/sccm/core/servers/deploy/install/prerequisite-checker).  



##  <a name="BKMK_Security"></a> Privilegi di protezione  


### <a name="security-rights-errors"></a>Privilegi di protezione: errori

#### <a name="administrator-rights-on-central-administration-site"></a>Diritti di amministratore per il sito di amministrazione centrale 
*Si applica a: sito primario*

L'account utente che esegue l'installazione di Configuration Manager ha privilegi di **amministratore** per il server del sito di amministrazione centrale.

#### <a name="administrative-rights-on-expand-primary-site"></a>Diritti amministrativi nel sito primario di espansione 
*Si applica a: sito di amministrazione centrale*

Quando un sito primario viene espanso in una gerarchia, l'account utente che esegue l'installazione ha privilegi di **amministratore** nel server del sito primario autonomo.

#### <a name="administrative-rights-on-site-system"></a>Diritti amministrativi sul sistema del sito 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

L'account utente che esegue l'installazione di Configuration Manager ha privilegi di **amministratore** per il server del sito.

#### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Privilegi di amministratore per il server del sito di amministrazione centrale su espansione sito primario 
*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, l'account computer del sito di amministrazione centrale ha privilegi di **amministratore** per il sito primario autonomo.

#### <a name="connection-to-sql-server-on-central-administration-site"></a>Connessione a SQL Server nel sito di amministrazione centrale 
*Si applica a: sito primario*

L'account utente che esegue l'installazione di Configuration Manager nel sito primario per l'aggiunta a una gerarchia esistente ha il ruolo **sysadmin** per l'istanza di SQL Server per il sito di amministrazione centrale.

#### <a name="site-server-computer-account-administrative-rights"></a>Diritti amministrativi dell'account computer del server di sito 
*Si applica a: sito primario, server di database del sito*

L'account computer del server del sito ha i privilegi di **amministratore** per SQL Server e il punto di gestione.

#### <a name="sql-server-sysadmin-rights"></a>Diritti di amministratore di sistema di SQL Server 
*Si applica a: server di database del sito*

L'account utente che esegue l'installazione di Configuration Manager ha il ruolo **sysadmin** per l'istanza di SQL Server selezionata per l'installazione del database del sito. Questo controllo ha esito negativo anche quando l'installazione non riesce ad accedere all'istanza di SQL Server per verificare le autorizzazioni.

#### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Diritti di amministratore di sistema SQL Server per sito di riferimento 
*Si applica a: server di database del sito*

L'account utente che esegue l'installazione di Configuration Manager ha il ruolo **sysadmin** per l'istanza del ruolo di SQL Server selezionata come database del sito di riferimento. Le autorizzazioni del ruolo **sysadmin** di SQL Server sono necessarie per modificare il database del sito.


### <a name="security-rights-warnings"></a>Privilegi di protezione: avvisi

#### <a name="site-system-to-sql-server-communication"></a>Comunicazione dal sistema del sito a SQL Server  
*Si applica a: sito secondario, punto di gestione*

L'account configurato per eseguire il servizio SQL Server per l'istanza di database del sito ha un nome dell'entità servizio (SPN, service principal name) valido in Active Directory Domain Services. Registrare un SPN valido in Active Directory Domain Services per supportare l'autenticazione Kerberos.

#### <a name="sql-server-security-mode"></a>Modalità di sicurezza di SQL Server 
*Si applica a: server di database del sito*

SQL Server è configurato per la sicurezza di autenticazione di Windows.



##  <a name="BKMK_Dependencies"></a> Dipendenze

### <a name="dependencies-errors"></a>Dipendenze: errori

#### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mapping di migrazione attivi nel sito primario di destinazione 
*Si applica a: sito di amministrazione centrale*

Non sono presenti mapping di migrazione attivi nei siti primari.

#### <a name="active-replica-mp"></a>Replica di MP attiva 
*Si applica a: sito primario*

È presente una replica del punto di gestione attiva.

#### <a name="bits-enabled"></a>BITS attivato 
*Si applica a: punto di gestione*

Servizio trasferimento intelligente in background (BITS, Background Intelligent Transfert Service) è installato nel punto di gestione. Questo controllo può non riuscire per uno dei motivi seguenti: 
- BITS non è installato  
- Il componente di compatibilità WMI IIS 6.0 per IIS 7.0 non è installato nel server o nell'host IIS remoto  
- Non è stato possibile verificare le impostazioni IIS remote I componenti comuni IIS non sono installati nel server del sito.  

#### <a name="case-insensitive-collation-on-sql-server"></a>Regole di confronto senza distinzione tra maiuscole e minuscole nel server SQL 
*Si applica a: server di database del sito*

L'installazione di SQL Server usa regole di confronto senza distinzione tra maiuscole e minuscole, come ad esempio **SQL_Latin1_General_CP1_CI_AS**.

#### <a name="check-existing-stand-alone-primary-site-for-version-and-site-code"></a>Verificare la versione e il codice sito del sito primario autonomo esistente 
*Si applica a: sito di amministrazione centrale, sito primario*

Il sito primario che si intende espandere è un sito primario autonomo. Ha la stessa versione di Configuration Manager, ma un codice sito diverso rispetto al sito di amministrazione centrale da installare.

#### <a name="check-for-incompatible-collection-references"></a>Verifica la presenza di riferimenti a raccolte incompatibili 
*Si applica a: sito di amministrazione centrale*

Durante un aggiornamento le raccolte fanno riferimento solo ad altre raccolte dello stesso tipo.

#### <a name="client-version-on-management-point-computer"></a>Versione client nel computer del punto di gestione 
*Si applica a: punto di gestione*

Si sta installando il punto di gestione in un server che non ha una versione diversa del client di Configuration Manager installato.

#### <a name="dedicated-sql-server-instance"></a>Istanza di SQL Server dedicata 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

È stata configurata un'istanza dedicata di SQL Server per ospitare il database del sito di Configuration Manager. 

Se un altro sito usa l'istanza, è necessario selezionare un'istanza diversa per il nuovo sito. È anche possibile disinstallare l'altro sito o spostare il relativo database in un'istanza diversa di SQL Server.

#### <a name="existing-configuration-manager-server-components-on-server"></a>Componenti del server di Configuration Manager esistenti nel server 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

Un server del sito o un ruolo del sistema del sito non è installato nel server selezionato per l'installazione del sito.

#### <a name="firewall-exception-for-sql-server"></a>Eccezione firewall per SQL Server 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario, punto di gestione*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server. 

Consentire l'accesso remoto a Sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Server Service Broker (SSB) usa la porta TCP 4022.

#### <a name="iis-service-running"></a>Servizio IIS in esecuzione 
*Si applica a: punto di gestione, punto di distribuzione*

IIS è installato e in esecuzione nel server per il punto di gestione o il punto di distribuzione.

#### <a name="match-collation-of-expand-primary-site"></a>Creare corrispondenze con le regole di confronto del sito primario di espansione 
*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il sito del database per il sito primario autonomo usa le stesse regole di confronto del database del sito nel sito di amministrazione centrale.

#### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Libreria di Compressione differenziale remota Microsoft (RDC) registrata 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

La libreria Connessione Desktop remoto è registrata nel server del sito di Configuration Manager.

#### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

Verifica la versione di Windows Installer. 

Se questo controllo ha esito negativo, l'installazione non riesce a verificare la versione oppure la versione installata non soddisfa il requisito minimo di Windows Installer 4.5.

#### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Versione minima di .NET Framework per la console di Configuration Manager 
*Si applica a: console di Configuration Manager*

Microsoft .NET Framework 4.0 è installato nel computer della console di Configuration Manager. 

#### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Versione minima di .NET Framework per il server del sito di Configuration Manager 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

.NET Framework 3.5 è installato o abilitato nel server del sito di Configuration Manager. 

#### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Versione minima di .NET Framework per l'installazione di SQL Server Express per il sito secondario di Configuration Manager 
*Si applica a: sito secondario*

.NET Framework 4.0 è installato o abilitato nel server del sito secondario di Configuration Manager. Questa versione è necessaria per SQL Server Express.

#### <a name="parent-database-collation"></a>Regole di confronto database principale 
*Si applica a: sito primario, sito secondario*

Le regole di confronto del database del sito corrispondono a quelle del database del sito padre. Tutti i siti in una gerarchia devono usare le stesse regole di confronto del database.

#### <a name="primary-fqdn"></a>FQDN primario 
*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, server di database del sito*

Il nome NetBIOS del computer corrisponde al nome host locale nel nome di dominio completo (FQDN).

#### <a name="required-sql-server-collation"></a>Regole di confronto di SQL Server richieste 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

L'istanza di SQL Server è configurata per usare le regole di confronto **SQL_Latin1_General_CP1_CI_AS**. 

Se il database del sito di Configuration Manager è già installato, questo controllo si applica anche al database. Per informazioni su come modificare le regole di confronto del database e dell'istanza di SQL Server, vedere [Regole di confronto e supporto Unicode di SQL](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support). 

Se si usa un sistema operativo cinese ed è necessario il supporto GB18030, questo controllo non è applicabile. Per altre informazioni sull'attivazione del supporto GB18030, vedere [Supporto internazionale](/sccm/core/plan-design/hierarchy/international-support).

#### <a name="setup-source-folder"></a>Cartella di origine di installazione 
*Si applica a: sito secondario*

L'account computer per il sito secondario ha le autorizzazioni seguenti per accedere alla cartella origine di installazione e per la condivisione: 
- Autorizzazioni **Read** del file system NTFS
- Autorizzazioni **Read** di condivisione 

> [!Note]  
> Se si usano condivisioni amministrative, ad esempio C$ e D$, l'account computer del sito secondario deve essere un **amministratore** nel server.  

#### <a name="setup-source-version"></a>Versione dell'origine installazione 
*Si applica a: sito secondario*

La versione di Configuration Manager nella cartella di origine specificata per l'installazione del sito secondario corrisponde alla versione di Configuration Manager del sito primario.

#### <a name="site-code-in-use"></a>Codice del sito in uso 
*Si applica a: sito primario* Il codice sito specificato non è già in uso nella gerarchia di Configuration Manager. Specificare un codice univoco per questo sito.

#### <a name="sms-provider-in-same-domain-as-site-server"></a>Il provider SMS ha lo stesso dominio del server del sito 
*Si applica a: provider SMS*

Tutte le istanze del provider SMS sono nello stesso dominio del server del sito.

#### <a name="sql-server-edition"></a>Edizione di SQL Server 
*Si applica a: server di database del sito*

SQL Server nel sito non è SQL Server Express.

#### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express nel sito secondario 
*Si applica a: sito secondario*

SQL Server Express può essere installato correttamente nel server del sito secondario.

#### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server nel server del sito secondario 
*Si applica a: sito secondario*

SQL Server è installato nel server del sito secondario. Non è possibile installare SQL Server in un sistema del sito remoto per un sito secondario.

> [!Warning]  
> Il controllo viene eseguito solo quando si configura il programma di installazione in modo che usi un'istanza esistente di SQL Server.  

#### <a name="sql-server-service-running-account"></a>Account di esecuzione del servizio SQL Server 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

L'account di accesso per il servizio SQL Server non è un account utente locale o di tipo **LOCAL SERVICE**. 

È necessario configurare il servizio SQL Server per usare un account di dominio valido, di tipo **NETWORK SERVICE** o **LOCAL SYSTEM**.

#### <a name="sql-server-tcp-port"></a>Porta TCP di SQL Server 
*Si applica a: server di database del sito*

Il protocollo TCP è abilitato per l'istanza di SQL Server ed è impostato per usare una porta statica.

#### <a name="sql-server-version"></a>Versione di SQL Server 
*Si applica a: server di database del sito*

Una versione supportata di SQL Server è installata nel server di database del sito specificato. 

Per altre informazioni, vedere [Supporto per le versioni di SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).

#### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Punto di sincronizzazione di Asset Intelligence nel sito primario espanso 
*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del punto di sincronizzazione di Asset Intelligence non è installato nel sito primario autonomo.

#### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Punto di Endpoint Protection nel sito primario espanso 
*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del punto di Endpoint Protection non è installato nel sito primario autonomo.

#### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Connettore Microsoft Intune nel sito primario espanso 
*Si applica a: sito di amministrazione centrale*

Quando si espande un sito primario in una gerarchia, il ruolo del connettore Microsoft Intune non è installato nel sito primario autonomo.

#### <a name="usmt-installed"></a>USMT non installata 
*Si applica a: sito di amministrazione centrale, sito primario (solo autonomo)*

Il componente Utilità di migrazione stato utente (USMT) di Windows Assessment and Deployment Kit (ADK) per Windows è installato.

#### <a name="validate-fqdn-of-sql-server"></a>Convalida del nome di dominio completo di SQL Server 
*Si applica a: server di database del sito*

È stato specificato un nome di dominio completo valido per il computer SQL Server.

#### <a name="verify-central-administration-site-version"></a>Verificare la versione del sito di amministrazione centrale 
*Si applica a: sito primario*

La versione del sito di amministrazione centrale è la stessa di Configuration Manager.

#### <a name="windows-deployment-tools-installed"></a>Strumenti di distribuzione Windows installati 
*Si applica a: provider SMS*

Il componente Strumenti di distribuzione Windows di Windows ADK è installato.

#### <a name="windows-failover-cluster"></a>Cluster di failover Windows 
*Si applica a: server del sito, punto di gestione, punto di distribuzione*

Server con i ruoli del server del sito, del punto di gestione o del punto di distribuzione che non fanno parte di un cluster Windows.

A partire dalla versione 1810, il programma di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. Poiché SQL Always On richiede questo ruolo, non era possibile in precedenza inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando SQL Always On e un server del sito in modalità passiva. Per altre informazioni, vedere [Opzioni di disponibilità elevata](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

#### <a name="windows-pe-installed"></a>Windows PE installato 
*Si applica a: provider SMS*

Il componente Ambiente preinstallazione di Windows di Windows ADK è installato.


### <a name="dependencies-warnings"></a>Dipendenze: avvisi

#### <a name="administrative-rights-on-distribution-point"></a>Diritti amministrativi sul punto di distribuzione 
*Si applica a: punto di distribuzione*

L'account utente che esegue il programma di installazione ha i privilegi di **amministratore** per il punto di distribuzione.

#### <a name="administrative-rights-on-management-point"></a>Diritti amministrativi sul punto di gestione 
*Si applica a: punto di gestione, punto di distribuzione*

L'account computer del server del sito ha i privilegi di **amministratore** per il punto di gestione e il punto di distribuzione.

#### <a name="administrative-share-site-system"></a>Condivisione amministrativa (sistema del sito) 
*Si applica a: punto di gestione*

Le condivisioni amministrative necessarie sono presenti nel computer del sistema del sito.

#### <a name="application-compatibility"></a>Compatibilità delle applicazioni 
*Si applica a: sito di amministrazione centrale, sito primario*

Le applicazioni correnti sono compatibili con lo schema dell'applicazione.

#### <a name="bits-installed"></a>BITS installato 
*Si applica a: punto di gestione*

Servizio trasferimento intelligente in background (BITS, Background Intelligent Transfert Service) è installato e abilitato in IIS.

#### <a name="configuration-for-sql-server-memory-usage"></a>Configurazione per l'utilizzo della memoria di SQL Server 
*Si applica a: server di database del sito*

SQL Server è configurato per un uso illimitato della memoria. Configurare la memoria di SQL Server impostando un limite massimo.

#### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Eccezione firewall per SQL Server (sito primario autonomo) 
*Si applica a: sito primario (solo autonomo)*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server. 

Consentire l'accesso remoto a Sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Server Service Broker usa la porta TCP 4022.

#### <a name="firewall-exception-for-sql-server-for-management-point"></a>Eccezione del firewall di SQL Server per il punto di gestione 
*Si applica a: punto di gestione*

Windows Firewall è disattivato o è stata generata un'eccezione rilevante di Windows Firewall per SQL Server.

#### <a name="iis-https-configuration"></a>Configurazione HTTPS di IIS 
*Si applica a: punto di gestione, punto di distribuzione*

Binding del sito Web IIS per il protocollo di comunicazione HTTPS. 

Quando si installano ruoli del sito che richiedono HTTPS, configurare i binding del sito IIS nel server specificato con un certificato di infrastruttura a chiave pubblica (PKI) valido.

#### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60) 
*Si applica a sito di amministrazione centrale, sito primario, sito secondario, console di Configuration Manager, punto di gestione, punto di distribuzione*

Verifica che sia installato MSXML 6.0 o versione successiva.

#### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 nel server di sito 
*Si applica a: sito primario con Exchange Connector*

Windows PowerShell 2.0 o versione successiva è installato nel server del sito per Configuration Manager Exchange Connector. 

#### <a name="remote-connection-to-wmi-on-secondary-site"></a>Connessione remota a WMI nel sito secondario 
*Si applica a: sito secondario*

Il programma di installazione può stabilire una connessione remota a WMI nel server del sito secondario.

#### <a name="sql-server-process-memory-allocation"></a>Allocazione di memoria per il processo di SQL Server 
*Si applica a: server di database del sito* 

SQL Server riserva almeno 8 GB di memoria per il sito di amministrazione centrale e per il sito primario e almeno 4 GB di memoria per il sito secondario.

Per altre informazioni, vedere [Come configurare le opzioni di memoria tramite SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd).

> [!NOTE]  
> Questo controllo non è applicabile a SQL Server Express in un sito secondario. In questa edizione la memoria riservata è limitata a 1 GB.  

#### <a name="unsupported-site-system-os-version-for-upgrade"></a>Versione del sistema operativo non supportata per l'aggiornamento 
*Si applica a: sito primario, sito secondario*

Ruoli del sistema del sito diversi dai punti di distribuzione sono installati nei server che eseguono Windows Server 2012 o versione successiva.

Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> Questo controllo non può risolvere lo stato dei ruoli del sistema del sito installati in Azure o per l'archiviazione nel cloud usata da Microsoft Intune. Ignorare gli avvisi per questi ruoli come falsi positivi.

#### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Verificare le autorizzazioni del server del sito da pubblicare in Active Directory Domain Services 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

L'account computer per il server del sito dispone di autorizzazioni di tipo **Controllo completo** per il contenitore **System Management** nel dominio di Active Directory. 

Per altre informazioni, vedere [Preparare Active Directory per la pubblicazione di siti](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> È possibile ignorare questo avviso se si verificano manualmente le autorizzazioni.

#### <a name="windows-remote-management-winrm-v11"></a>Gestione remota Windows (WinRM) v1.1 
*Si applica a: sito primario, console di Configuration Manager*

WinRM 1.1 è installato nel server del sito primario o nel computer della console di Configuration Manager per l'esecuzione della console di gestione fuori banda. 

Per altre informazioni su come scaricare WinRM 1.1, vedere l'[articolo del supporto tecnico 936059](https://support.microsoft.com/help/936059).

#### <a name="wsus-on-site-server"></a>WSUS nel server di sito 
*Si applica a: sito di amministrazione centrale, sito primario*

Una versione supportata di Windows Server Update Services (WSUS) è installata nel server del sito. 

Quando si usa un punto di aggiornamento software in un server diverso rispetto al server del sito, è necessario installare la console di amministrazione WSUS nel server del sito. Per altre informazioni su WSUS, vedere [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).

#### <a name="pending-configuration-item-policy-updates"></a>Aggiornamenti dei criteri per elementi di configurazione in sospeso 
<!--SCCMDocs-pr issue 2814-->
*Si applica a: sito primario*

A partire dalla versione 1806, se si esegue l'aggiornamento dalla versione 1706 o successiva, potrebbe essere visualizzato questo avviso se sono presenti molte distribuzioni di applicazioni e almeno una di esse richiede l'approvazione. 

Sono disponibili due opzioni:  

- Ignorare l'avviso e continuare l'aggiornamento. Questa azione comporta una maggiore elaborazione sul server del sito durante l'aggiornamento a causa dell'elaborazione dei criteri. È inoltre possibile osservare un aumento del carico del processore nel punto di gestione dopo l'aggiornamento.  

- Modificare una delle applicazioni che non prevedono requisiti o che ne prevedono uno per un sistema operativo specifico. Eseguire la pre-elaborazione di parte del carico nel server del sito in questa fase. Esaminare **objreplmgr.log** e quindi monitorare il processore nel punto di gestione. Dopo aver completato l'elaborazione, aggiornare il sito. Sarà ancora presente un certo livello di elaborazione aggiuntiva dopo l'aggiornamento, ma sarà inferiore a quella che si verifica ignorando l'avviso con la prima opzione.  



##  <a name="BKMK_Requirements"></a> Requisiti di sistema  

### <a name="system-requirements-errors"></a>Requisiti di sistema: errori

#### <a name="server-service-is-running"></a>Il servizio Server è in esecuzione 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

Il servizio Server è avviato e in esecuzione.

#### <a name="domain-membership"></a>Appartenenza al dominio 
*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, provider SMS, SQL Server*

Il computer di Configuration Manager è membro di un dominio di Windows.

#### <a name="free-disk-space-on-site-server"></a>Spazio su disco disponibile nel server di sito 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

Per installare il server del sito, il computer deve avere almeno 15 GB di spazio libero su disco. Se si installa il provider SMS nello stesso server, è necessario 1 GB di spazio libero aggiuntivo.

#### <a name="pending-system-restart"></a>Riavvio del sistema in sospeso 
*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, console di Configuration Manager, provider SMS, SQL Server, punto di gestione, punto di distribuzione*

Prima di eseguire l'installazione, un altro programma necessita del riavvio del server.

A partire dalla versione 1810, questo controllo è più resiliente. Per verificare se il computer è in uno stato di riavvio in sospeso, controlla le posizioni del Registro di sistema seguenti:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="read-only-domain-controller"></a>Controller di dominio di sola lettura 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

I server di database del sito e i server dei siti secondari non sono supportati in un controller di dominio di sola lettura. 

Per altre informazioni, vedere l'articolo del supporto tecnico Microsoft relativo ai [problemi riscontrati durante l'installazione di SQL Server in un controller di dominio](https://support.microsoft.com/help/2032911).

#### <a name="site-server-fqdn-length"></a>Lunghezza del nome di dominio completo del server del sito 
*Si applica a: sito di amministrazione centrale, sito primario,sito secondario*

Lunghezza del nome di dominio completo del server del sito.

#### <a name="unsupported-os-for-configuration-manager-console"></a>Sistemi operativi non supportati per la console di Configuration Manager
*Si applica a: console di Configuration Manager*

Installare la console di Configuration Manager in computer che eseguono una versione del sistema operativo supportata. 

Per altre informazioni, vedere [Sistemi operativi supportati per le console di Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

#### <a name="unsupported-os-for-site-server"></a>Sistema operativo non supportato per il server del sito 
*Si applica a: sito di amministrazione centrale, sito primario, sito secondario, console di Configuration Manager, punto di gestione, punto di distribuzione*

Il server esegue una versione supportata del sistema operativo. 

Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

#### <a name="verify-database-consistency"></a>Verificare la coerenza del database 
*Si applica a: sito di amministrazione centrale, sito primario*

Verifica la coerenza del database del sito in SQL Server.  


### <a name="system-requirements-warnings"></a>Requisiti di sistema: avvisi

#### <a name="active-directory-domain-functional-level"></a>Livello di funzionalità del dominio di Active Directory 
*Si applica a: sito di amministrazione centrale, sito primario*

Il livello funzionale del dominio di Active Directory è almeno Windows Server 2008 R2.

#### <a name="domain-membership"></a>Appartenenza al dominio 
*Si applica a: punto di gestione, punto di distribuzione*

Il computer di Configuration Manager è membro di un dominio di Windows.

#### <a name="ntfs-drive-on-site-server"></a>Unità NTFS nel server del sito 
*Si applica a: sito primario*

L'unità disco deve essere formattata con il file system NTFS. Per una protezione migliore, installare i componenti del server del sito in unità disco formattate con il file system NTFS.

#### <a name="schema-extensions"></a>Estensioni dello schema 
*Si applica a: sito di amministrazione centrale, sito primario*

Lo schema di Active Directory è stato esteso. Se è esteso, il controllo verifica la versione delle estensioni dello schema usate. 

Configuration Manager non richiede le estensioni dello schema di Active Directory per l'installazione del server del sito. Microsoft le consiglia per l'uso completo di tutte le funzionalità di Configuration Manager. Per altre informazioni sui vantaggi offerti dall'estensione dello schema, vedere [Preparare Active Directory per la pubblicazione di siti](/sccm/core/plan-design/network/extend-the-active-directory-schema).

#### <a name="bkmk_changetracking"></a> Pulizia rilevamento modifiche SQL
*Si applica a: server di database del sito*

A partire dalla versione 1810, è presente un controllo che verifica se il database del sito ha un backlog di dati di rilevamento modifiche di SQL.<!--SCCMDocs-pr issue 3023-->  

Eseguire manualmente il controllo tramite una stored procedure nel database del sito. Creare prima di tutto una [connessione di diagnostica](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) al database del sito. Il metodo più semplice è usare l'editor di query di SQL Server Management Studio e connettersi a `admin:<instance name>`. 

In una finestra di query di connessione amministrativa dedicata, eseguire i comandi seguenti:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

A seconda delle dimensioni del database e del backlog, l'esecuzione della stored procedure può richiedere alcuni minuti o diverse ore. Al termine della query, vengono visualizzate due sezioni di dati correlati al backlog. Esaminare per prima cosa **CT_Days_Old**. Questo valore indica il numero di giorni trascorsi da quando è stata immessa la prima voce nella tabella syscommittab. Dovrebbe essere pari a cinque giorni, il valore predefinito di Configuration Manager. Non modificare questo valore predefinito. In caso di elaborazione dati o repliche di dimensioni molto elevate, la prima voce nella tabella syscommittab potrebbe essere stata immessa più di cinque giorni prima. Se il valore supera i sette giorni, eseguire una pulizia manuale dei dati di rilevamento delle modifiche.  

Per eseguire la pulizia dei dati di rilevamento delle modifiche, eseguire il comando seguente nella connessione amministrativa dedicata: 

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Questo comando avvia una pulizia di syscommittab e di tutte le tabelle laterali associate. L'esecuzione del comando può richiedere da alcuni minuti a diverse ore. Per monitorarne l'avanzamento, eseguire una query sulla vista **vLogs**. Per visualizzare lo stato di avanzamento corrente, eseguire la query seguente: 

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

<!-- #### SQL Native Client
<!--SCCMDocs-pr issue 3094->
*Applies to: Central administration site, primary site, secondary site*

A supported version of the SQL Native Client. Starting in version 1810, the minimum version is 11.4.7001.0. 

This SQL Native Client version supports TLS 1.2. For more information, see the following articles:
- [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  
- [How to enable TLS 1.2 for Configuration Manager](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager)  
 -->