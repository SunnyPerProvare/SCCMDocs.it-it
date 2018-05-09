---
title: Prerequisiti del sito
titleSuffix: Configuration Manager
description: Informazioni su come configurare un computer Windows come un server di sistema del sito di System Center Configuration Manager.
ms.date: 02/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c184bd66b90d53e87ea9b5fbd6dddeeec1e8994c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Prerequisiti del sito e del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 I computer basati su Windows richiedono configurazioni specifiche per supportare l'uso come server del sistema del sito di System Center Configuration Manager.  

 
 Per alcuni prodotti, come Windows Server Update Services (WSUS) per il punto di aggiornamento software, è necessario fare riferimento alla documentazione dei prodotti per identificare altri prerequisiti e limitazioni per l'uso. Qui sono incluse solo le configurazioni che si applicano direttamente all'uso con Configuration Manager.   

> [!NOTE]  
>  A gennaio 2016 è scaduto il supporto per .NET Framework 4.0, 4.5 e 4.5.1. Per altre informazioni, vedere le [domande frequenti sul ciclo di vita del supporto per Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) nel sito support.microsoft.com.  

## <a name="bkmk_generalprerewq"></a> Requisiti e limitazioni generali del server del sito
**Quanto segue si applica a tutti i server del sistema del sito:**

-   Ogni server del sistema del sito deve usare un sistema operativo a 64 bit. L'unica eccezione è il ruolo del sistema del sito del punto di distribuzione, che può essere installato in alcune versioni del sistema operativo a 32 bit.  

-   I sistemi del sito non sono supportati nelle installazioni Server Core per alcun sistema operativo. Un'eccezione è il fatto che le installazioni Server Core sono supportate per il ruolo del sistema del sito del punto di distribuzione, senza supporto per PXE o per il multicast.  

-   Dopo aver installato un server di sistema del sito, non è consentito modificare:  

    -   Il nome di dominio in cui si trova il computer del sistema del sito (operazione detta anche **ridenominazione del dominio**).  

    -   L'appartenenza del computer al dominio.  

    -   Nome del computer.  

  Se è necessario modificare uno di questi elementi, occorre prima di tutto rimuovere il ruolo del sistema del sito dal computer e quindi reinstallarlo al termine della modifica. Per le modifiche che influiscono sul computer server del sito, è necessario disinstallare il sito e quindi reinstallarlo dopo aver completato la modifica.  

-   I ruoli del sistema del sito non sono supportati in un'istanza di un cluster Windows Server. L'unica eccezione è il server del database del sito.  

-   La modifica delle impostazioni del tipo di avvio o di accesso per tutti i servizi di Configuration Manager non è supportata. Tale modifica potrebbe impedire il corretto funzionamento di servizi chiave.  

##  <a name="bkmk_2012Prereq"></a> Prerequisiti per Windows Server 2012 e sistemi operativi successivi  
###  <a name="bkmk_2012sspreq"></a> Server del sito: sito di amministrazione centrale e sito primario  
  **Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1
    - Per altre informazioni sulle versioni di .Net Framework, vedere [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)

-   Compressione differenziale remota  

**Windows ADK:**  

-   Prima di installare o aggiornare un sito di amministrazione centrale o un sito primario, è necessario installare la versione di Windows ADK (Windows Assessment and Deployment Kit) richiesta dalla versione di Configuration Manager che si intende installare o aggiornare. Vedere [Windows ADK 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) nell'articolo Supporto per Windows 10 come client.  

-   Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

-   I siti di amministrazione centrale e i siti primari richiedono entrambe le versioni x86 e x64 del file ridistribuibile applicabile.  

###  <a name="bkmk_2012secpreq"></a> Server del sito: sito secondario  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1
    - Per altre informazioni sulle versioni di .Net Framework, vedere [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)

-   Compressione differenziale remota  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

-   I siti secondari richiedono solo la versione x64.  

**Ruoli del sistema del sito predefiniti:**  

-   Per impostazione predefinita, un sito secondario installa un **punto di gestione** e un **punto di distribuzione**.  

-   Assicurarsi che il server del sito secondario soddisfi i prerequisiti per questi ruoli del sistema del sito.  

###  <a name="bkmk_2012dbpreq"></a> Server di database  
**Servizio Registro di sistema remoto:**  

-   Durante l'installazione del sito di Configuration Manager, è necessario abilitare il servizio Registro di sistema remoto nel computer che ospita il database del sito.  

**SQL Server:**  

-   Prima di installare un sito di amministrazione centrale o un sito primario, è necessario installare una versione supportata di SQL Server per ospitare il database del sito.  

-   Prima di installare un sito secondario, è possibile installare una versione supportata di SQL Server.  

-   Se si sceglie di lasciare che Configuration Manager installi SQL Server Express come parte dell'installazione del sito secondario, assicurarsi che il computer soddisfi i requisiti per l'esecuzione di SQL Server Express.  

###  <a name="bkmk_2012smsprovpreq"></a> Server del provider SMS  
**Windows ADK:**  

-   Nel computer in cui si installa un'istanza del provider SMS deve essere installata la versione di Windows ADK richiesta dalla versione di Configuration Manager che si intende installare o aggiornare. Vedere [Windows ADK 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) nell'articolo Supporto per Windows 10 come client.

-   Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2012acwspreq"></a> Punto per siti Web del Catalogo applicazioni  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1
    - ASP.NET 4.5 

    - Per altre informazioni sulle versioni di .Net Framework, vedere [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)  

    

**Configurazione di IIS:**  

-   Funzionalità HTTP comuni:  

    -   Documento predefinito  

    -   Contenuto statico  

-   Sviluppo di applicazioni:  

    -   ASP.NET 3.5 (e le opzioni selezionate automaticamente)   

    -   ASP.NET 4.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 3.5  

    -   Estendibilità .NET 4.5  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

###  <a name="bkmk_2012ACwsitepreq"></a> Punto per servizi Web del Catalogo applicazioni  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1:  

    -   ASP.NET 4.5:  

        -   Attivazione ASP.NET (e le opzioni selezionate automaticamente)  

**Configurazione di IIS:**  

-   Funzionalità HTTP comuni:  

    -   Documento predefinito  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

-   Sviluppo di applicazioni:  

    -   ASP.NET 3.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 3.5  

    -   ASP.NET 4.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 4.5  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2012AIpreq"></a> Punto di sincronizzazione di Asset Intelligence  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

###  <a name="bkmk_2012crppreq"></a> Punto di registrazione certificati  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1:  

    -   Attivazione HTTP  

**Configurazione di IIS:**  

-   Sviluppo di applicazioni:  

    -   ASP.NET 3.5 (e le opzioni selezionate automaticamente)   

    -   ASP.NET 4.5 (e le opzioni selezionate automaticamente)   

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  

###  <a name="bkmk_2012dppreq"></a> Punto di distribuzione  
**Funzionalità e ruoli di Windows Server:**  

-   Compressione differenziale remota  

**Configurazione di IIS:**  

-   Sviluppo di applicazioni:  

    -   Estensioni ISAPI  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  

**PowerShell:**  

-   In Windows Server 2012 o versioni successive è necessario PowerShell 3.0 o 4.0 prima di installare il punto di distribuzione.  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

-   La versione installata dipende dalla piattaforma del computer (x86 o x64).  

**Microsoft Azure:**  

-   È possibile usare un servizio cloud in Microsoft Azure per ospitare un punto di distribuzione.  

**Per il supporto di PXE o del multicast:**  

-   Installare e configurare il ruolo Servizi di distribuzione Windows di Windows Server.  

    > [!NOTE]  
    >  Servizi di distribuzione Windows viene installato e configurato automaticamente quando si configura un punto di distribuzione per il supporto di PXE o del multicast in un server che esegue Windows Server 2012 o versioni successive.  

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando il punto di distribuzione trasferisce il contenuto, il trasferimento viene eseguito tramite il **Servizio trasferimento intelligente in background** (BITS) incluso nel sistema operativo Windows. Il ruolo del punto di distribuzione non richiede l'installazione della funzionalità facoltativa di estensione del server IIS BITS, perché il client non carica informazioni in tale server.  

###  <a name="bkmk_2012EPPpreq"></a> Punto di Endpoint Protection  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

###  <a name="bkmk_2012Enrollpreq"></a> Punto di registrazione  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1:  

     Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

    -   Attivazione ASP.NET (e le opzioni selezionate automaticamente)  

    -   ASP.NET 4.5  


**Configurazione di IIS:**  

-   Funzionalità HTTP comuni:  

    -   Documento predefinito  

-   Sviluppo di applicazioni:  

    -   ASP.NET 3.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 3.5  

    -   ASP.NET 4.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 4.5  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2012EnrollProxpreq"></a> Punto proxy di registrazione  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

     Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

**Configurazione di IIS:**  

-   Funzionalità HTTP comuni:  

    -   Documento predefinito  

    -   Contenuto statico  

-   Sviluppo di applicazioni:  

    -   ASP.NET 3.5 (e le opzioni selezionate automaticamente)   

    -   ASP.NET 4.5 (e le opzioni selezionate automaticamente)   

    -   Estendibilità .NET 3.5  

    -   Estendibilità .NET 4.5  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2012FSPpreq"></a> Punto di stato di fallback  
È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

###  <a name="bkmk_2012MPpreq"></a> Punto di gestione  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

-   Estensioni del server BITS (e le opzioni selezionate automaticamente) o Servizio trasferimento intelligente in background (BITS) (e le opzioni selezionate automaticamente)  

**Configurazione di IIS:**  

-   Sviluppo di applicazioni:  

    -   Estensioni ISAPI  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  

###  <a name="bkmk_2012RSpoint"></a> Punto di Reporting Services  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**SQL Server Reporting Services:**  

-   Prima di installare il punto di Reporting Services, installare e configurare almeno un'istanza di SQL Server per supportare SQL Server Reporting Services.  

-   L'istanza usata per SQL Server Reporting Services può essere la stessa usata per il database del sito.  

-   Inoltre, l'istanza usata può essere condivisa con altri prodotti System Center purché per tali prodotti non siano previste limitazioni per la condivisione dell'istanza di SQL Server.  

###  <a name="bkmk_SCPpreq"></a> Punto di connessione del servizio  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

     Quando viene installato questo ruolo del sistema del sito, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

-   Il ruolo del sistema del sito richiede la versione x64.  

###  <a name="bkmk_2012SUPpreq"></a> Punto di aggiornamento software  
**Funzionalità e ruoli di Windows Server:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

È necessaria la configurazione predefinita di IIS.

**Windows Server Update Services:**  

-   È necessario installare il ruolo del server di Windows Windows Server Update Services in un computer prima di installare un punto di aggiornamento software.  

-   Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Punto di migrazione stato  
È necessaria la configurazione predefinita di IIS.  

##  <a name="bkmk_2008"></a> Prerequisiti per Windows Server 2008 R2 e Windows Server 2008  
Windows Server 2008 e Windows Server 2008 R2 sono ora in modalità di supporto "Extended" e non più in modalità di supporto Mainstream, come descritto nel sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle). Per altre informazioni sul supporto disponibile in futuro per questi sistemi operativi come server di sistema del sito con Configuration Manager, vedere [Sistemi operativi del server rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

**Le indicazioni seguenti sono valide per tutti i requisiti di .NET Framework:**  

-   Installare la versione completa di .NET Framework prima di installare i ruoli del sistema del sito. Ad esempio, vedere [Microsoft .NET Framework 4 (programma di installazione autonomo)](http://go.microsoft.com/fwlink/p/?LinkId=193048). .NET Framework 4 Client Profile è insufficiente per questo requisito.  

**Le indicazioni seguenti sono valide per tutti i requisiti di attivazione di Windows Communication Foundation (WCF):**  

-   È possibile configurare l'attivazione di WCF come parte della funzionalità .NET Framework di Windows nel server del sistema del sito. Ad esempio, in Windows Server 2008 R2, eseguire **Aggiunta guidata funzionalità** per installare funzionalità aggiuntive nel server. Nella pagina **Seleziona caratteristiche** espandere **Funzionalità di .NET Framework 3.5.1** e quindi **Attivazione WCF**. Selezionare le caselle di controllo per **Attivazione HTTP** e **Attivazione non HTTP** per abilitare queste opzioni.  

###  <a name="bkmk_2008sspreq"></a> Server del sito: sito di amministrazione centrale e sito primario  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**Funzionalità di Windows:**  

-   Compressione differenziale remota  

**Windows ADK:**  

-   Prima di installare o aggiornare un sito di amministrazione centrale o un sito primario, è necessario installare la versione di Windows ADK richiesta dalla versione di Configuration Manager che si intende installare o aggiornare.  Vedere [Windows ADK 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) nell'articolo Supporto per Windows 10 come client.  

-   Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

-   I siti di amministrazione centrale e i siti primari richiedono entrambe le versioni x86 e x64 del file ridistribuibile applicabile.  

###  <a name="bkmk_2008secpreq"></a> Server del sito: sito secondario  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer in cui viene installato un server del sito.  

-   I siti secondari richiedono solo la versione x64.  

**Ruoli del sistema del sito predefiniti:**  

-   Per impostazione predefinita, un sito secondario installa un **punto di gestione** e un **punto di distribuzione**.  

-   Assicurarsi che il server del sito secondario soddisfi i prerequisiti per questi ruoli del sistema del sito.  

###  <a name="bkmk_2008dbpreq"></a> Server di database  
**Servizio Registro di sistema remoto:**  

-   Durante l'installazione del sito di Configuration Manager, è necessario abilitare il servizio Registro di sistema remoto nel computer che ospita il database del sito.  

**SQL Server:**  

-   Prima di installare un sito di amministrazione centrale o un sito primario, è necessario installare una versione supportata di SQL Server per ospitare il database del sito.  

-   Prima di installare un sito secondario, è possibile installare una versione supportata di SQL Server.  

-   Se si sceglie di lasciare che Configuration Manager installi SQL Server Express come parte dell'installazione del sito secondario, assicurarsi che il computer soddisfi i requisiti per l'esecuzione di SQL Server Express.  

###  <a name="bkmk_2008smsprovpreq"></a> Server del provider SMS  
**Windows ADK:**  

-   Nel computer in cui si installa un'istanza del provider SMS deve essere installata la versione di Windows ADK richiesta dalla versione di Configuration Manager che si intende installare o aggiornare. Vedere [Windows ADK 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) nell'articolo Supporto per Windows 10 come client.  

-   Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2008acwspreq"></a> Punto per siti Web del Catalogo applicazioni  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Funzionalità HTTP comuni:  

    -   Contenuto statico  

    -   Documento predefinito  

-   Sviluppo di applicazioni:  

    -   ASP.NET (e le opzioni selezionate automaticamente)  

         In alcuni scenari, ad esempio quando IIS viene installato o riconfigurato dopo l'installazione di .NET Framework versione 4.5.2, è necessario abilitare esplicitamente ASP.NET versione 4.5. Ad esempio, in un computer a 64 bit che esegue .NET Framework versione 4.0.30319 eseguire il comando seguente: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

###  <a name="bkmk_2008ACwsitepreq"></a> Punto per servizi Web del Catalogo applicazioni  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**Attivazione di Windows Communication Foundation (WCF):**  

-   Attivazione HTTP  

-   Attivazione non HTTP  

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Sviluppo di applicazioni:  

    -   ASP.NET (e le opzioni selezionate automaticamente)  

         In alcuni scenari, ad esempio quando IIS viene installato o riconfigurato dopo l'installazione di .NET Framework versione 4.5.2, è necessario abilitare esplicitamente ASP.NET versione 4.5. Ad esempio, in un computer a 64 bit che esegue .NET Framework versione 4.0.30319 eseguire il comando seguente: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2008AIpreq"></a> Punto di sincronizzazione di Asset Intelligence  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1

###  <a name="bkmk_2008crppreq"></a> Punto di registrazione certificati  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

-   Attivazione HTTP  

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  

###  <a name="bkmk_2008dppreq"></a> Punto di distribuzione  
**Configurazione di IIS:**

È possibile usare la configurazione predefinita di IIS o una configurazione personalizzata. Per usare una configurazione personalizzata di IIS, è necessario abilitare le opzioni seguenti per IIS:  

-   Sviluppo di applicazioni:  

    -   Estensioni ISAPI  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  

Quando si usa una configurazione personalizzata di IIS, è possibile rimuovere le opzioni non necessarie, ad esempio:  

-   Funzionalità HTTP comuni:  

    -   Reindirizzamento HTTP  

-   Strumenti e script di gestione IIS  

**Funzionalità di Windows:**  

-   Compressione differenziale remota  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

-   La versione installata dipende dalla piattaforma del computer (x86 o x64).  

**Microsoft Azure:**  

-   È possibile usare un servizio cloud in Azure per ospitare un punto di distribuzione.  

**Per il supporto di PXE o del multicast:**  

-   Installare e configurare il ruolo Servizi di distribuzione Windows di Windows Server.  

    > [!NOTE]  
    >  Servizi di distribuzione Windows viene installato e configurato automaticamente quando si configura un punto di distribuzione per il supporto di PXE o del multicast in un server che esegue Windows Server 2012 o versioni successive.  

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando il punto di distribuzione trasferisce il contenuto, il trasferimento viene eseguito tramite il **Servizio trasferimento intelligente in background** (BITS) incluso nel sistema operativo Windows. Il ruolo di punto di distribuzione non richiede l'installazione della funzionalità facoltativa di estensione del server IIS BITS, perché il client non carica informazioni in tale server.   


###  <a name="bkmk_2008EPPpreq"></a> Punto di Endpoint Protection  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

###  <a name="bkmk_2008Enrollpreq"></a> Punto di registrazione  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

     Se quando viene installato questo ruolo del sistema del sito nel server non è già installata una versione supportata di .NET Framework, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

**Attivazione di Windows Communication Foundation (WCF):**  

-   Attivazione HTTP  

-   Attivazione non HTTP  

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Sviluppo di applicazioni:  

    -   ASP.NET (e le opzioni selezionate automaticamente)  

         In alcuni scenari, ad esempio quando IIS viene installato o riconfigurato dopo l'installazione di .NET Framework versione 4.5.2, è necessario abilitare esplicitamente ASP.NET versione 4.5. Ad esempio, in un computer a 64 bit che esegue .NET Framework versione 4.0.30319 eseguire il comando seguente: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2008EnrollProxpreq"></a> Punto proxy di registrazione  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1

     Se quando viene installato questo ruolo del sistema del sito nel server non è già installata una versione supportata di .NET Framework, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Quando un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

**Attivazione di Windows Communication Foundation (WCF):**  

-   Attivazione HTTP  

-   Attivazione non HTTP  

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Sviluppo di applicazioni:  

    -   ASP.NET (e le opzioni selezionate automaticamente)  

         In alcuni scenari, ad esempio quando IIS viene installato o riconfigurato dopo l'installazione di .NET Framework versione 4.5.2, è necessario abilitare esplicitamente ASP.NET versione 4.5. Ad esempio, in un computer a 64 bit che esegue .NET Framework versione 4.0.30319 eseguire il comando seguente: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Memoria del computer:**  

-   Il computer che ospita questo ruolo del sistema del sito deve avere almeno il 5% di memoria libera disponibile per permettere al ruolo del sistema del sito di elaborare le richieste.  

-   Quando questo ruolo del sistema del sito condivide il percorso con un altro ruolo del sistema del sito con lo stesso requisito, questo requisito di memoria per il computer non aumenta, ma rimane almeno pari al 5%.  

###  <a name="bkmk_2008FSPpreq"></a> Punto di stato di fallback  
**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS con le aggiunte seguenti:  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

###  <a name="bkmk_2008MPpreq"></a> Punto di gestione  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1

**Configurazione di IIS:**

È possibile usare la configurazione predefinita di IIS o una configurazione personalizzata. Ogni punto di gestione abilitato per supportare i dispositivi mobili richiede la configurazione aggiuntiva di IIS per ASP.NET (e le relative opzioni selezionate automaticamente).

In alcuni scenari, ad esempio quando IIS viene installato o riconfigurato dopo l'installazione di .NET Framework versione 4.5.2, è necessario abilitare esplicitamente ASP.NET versione 4.5. Ad esempio, in un computer a 64 bit che esegue .NET Framework versione 4.0.30319 eseguire il comando seguente: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


Per usare una configurazione personalizzata di IIS, è necessario abilitare le opzioni seguenti per IIS:  

-   Sviluppo di applicazioni:  

    -   Estensioni ISAPI  

-   Protezione:  

    -   Autenticazione di Windows  

-   Compatibilità Gestione IIS 6:  

    -   Compatibilità Metabase IIS 6  

    -   Compatibilità WMI IIS 6  


Quando si usa una configurazione personalizzata di IIS, è possibile rimuovere le opzioni non necessarie, ad esempio:  

-   Funzionalità HTTP comuni:  

    -   Reindirizzamento HTTP  

-   Strumenti e script di gestione IIS  

**Funzionalità di Windows:**  

-   Le estensioni del Server BITS (e le opzioni selezionate automaticamente), o i servizi di trasferimento intelligente in background (BITS) (e le opzioni selezionate automaticamente)  

###  <a name="bkmk_2008RSpoint"></a> Punto di Reporting Services  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**SQL Server Reporting Services:**  

-   Prima di installare il punto di Reporting Services, installare e configurare almeno un'istanza di SQL Server per supportare SQL Server Reporting Services.  

-   L'istanza usata per SQL Server Reporting Services può essere la stessa usata per il database del sito.  

-   Inoltre, l'istanza usata può essere condivisa con altri prodotti System Center purché per tali prodotti non siano previste limitazioni per la condivisione dell'istanza di SQL Server.  

###  <a name="bkmk_2008SCPpreq"></a> Punto di connessione del servizio  
**.NET Framework:**  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

     Se quando viene installato questo ruolo del sistema del sito nel server non è già installata una versione supportata di .NET Framework, Configuration Manager installa automaticamente .NET Framework 4.5.2. Questa installazione può far sì che il server passi a uno stato di riavvio in sospeso. Se un riavvio è in sospeso per .NET Framework, le applicazioni .NET possono restituire un errore finché il server non viene riavviato e l'installazione non viene completata.  

**Visual C++ Redistributable:**  

-   Configuration Manager installa Microsoft Visual C++ 2013 Redistributable Package in ogni computer che ospita un punto di distribuzione.  

-   Il ruolo del sistema del sito richiede la versione x64.  

###  <a name="bkmk_2008SUPpreq"></a> Punto di aggiornamento software  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (o versioni successive)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7 o 4.7.1 

**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS.  

**Windows Server Update Services:**  

-   È necessario installare il ruolo del server di Windows Windows Server Update Services in un computer prima di installare un punto di aggiornamento software.  

-   Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="bkmk_2008SMPpreq"></a> Punto di migrazione stato  
**Configurazione di IIS:**

È necessaria la configurazione predefinita di IIS.  
