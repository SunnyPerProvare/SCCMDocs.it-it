---
title: Prerequisiti per la distribuzione di client Windows
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per la distribuzione di client Configuration Manager a computer Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a830b36bec3d112c0b112d2df6887a84c837fa2
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418255"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Prerequisiti per la distribuzione dei client nei computer Windows in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La distribuzione di client di Configuration Manager nell'ambiente ha le dipendenze esterne e le dipendenze nel prodotto seguenti. Ogni metodo di distribuzione client presenta inoltre proprie dipendenze che devono essere soddisfatte per garantire la correttezza delle installazioni client.  

Per altre informazioni sui requisiti minimi per l'hardware e il sistema operativo per il client di Configuration Manager, vedere [Configurazioni supportate](/sccm/core/plan-design/configs/supported-configurations).  

> [!NOTE]  
>  I numeri delle versioni software elencati in questo articolo si riferiscono solo ai numeri delle versioni minime richieste.  



##  <a name="BKMK_prereqs_computers"></a> Prerequisiti per i client Windows  

Usare le informazioni seguenti per determinare i prerequisiti quando si installa il client di Configuration Manager in dispositivi Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Componente|Descrizione|  
|---|---|  
|Windows Installer versione 3.1.4000.2435|Necessario per supportare l'utilizzo di file di aggiornamento di Windows Installer (MSP) per pacchetti e aggiornamenti software.|  
|Microsoft Background Intelligent Transfer Service (BITS) versione 2.5|Necessario per consentire i trasferimenti di dati limitati tra il computer client e i sistemi del sito di Configuration Manager. BITS non viene scaricato automaticamente durante l'installazione del client. Quando BITS viene installato nei computer, in genere è necessario un riavvio per completare l'installazione.<br /><br /> La maggior parte dei sistemi operativi include BITS. In caso contrario, installare BITS prima di installare il client di Configuration Manager.|  
|Utilità di pianificazione di Microsoft|Per completare l'installazione del client, abilitare questo servizio nel client.|  


### <a name="bkmk_ExternalDependencies"></a> Dipendenze esterne a Configuration Manager e scaricate automaticamente durante l'installazione  

Il client di Configuration Manager presenta dipendenze esterne. Queste dipendenze variano a seconda della versione del sistema operativo e del software installato nel computer client.  

Se il client richiede queste dipendenze per completare l'installazione, le installa automaticamente.  

|Componente|Descrizione|  
|---|---|  
|Agente di Windows Update versione 7.0.6000.363|Richiesto da Windows per supportare il rilevamento e la distribuzione degli aggiornamenti.|  
|Microsoft Core XML Services (MSXML) versione 6.20.5002 o successiva|Necessario per supportare l'elaborazione di documenti XML in Windows.|  
|Compressione differenziale remota Microsoft (RDC)|Necessaria per ottimizzare la trasmissione dei dati attraverso la rete.|  
|Microsoft Visual C++ 2013 Redistributable versione 12.0.21005.1|Necessario per supportare le operazioni client. Quando questo aggiornamento viene installato nei computer client, potrebbe essere necessario un riavvio per completare l'installazione.|  
|Microsoft Visual C++ 2005 Redistributable versione 8.0.50727.42|Per la versione 1606 e precedenti, necessario per supportare le operazioni di Microsoft SQL Server Compact.|  
|API per Windows Imaging 6.0.6001.18000|Necessario per consentire a Configuration Manager di gestire i file di immagine Windows (wim).|  
|Microsoft Policy Platform 1.2.3514.0|Necessario per consentire ai client di valutare le impostazioni di conformità.|  
|Microsoft Silverlight 5.1.41212.0|Necessario per supportare l'esperienza utente del sito Web Catalogo applicazioni. A partire da Configuration Manager 1802, Silverlight non viene più installato automaticamente. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per il sito Web del Catalogo applicazioni termina con la versione 1806.<!--1356195-->|  
|Microsoft .NET Framework version 4.5.2|Necessario per supportare le operazioni client. Viene installato automaticamente nel computer client se Microsoft .NET Framework 4.5 o versione successiva non è installato in tale computer. Per altre informazioni, vedere [Informazioni aggiuntive su Microsoft .NET Framework versione 4.5.2](#dotNet).|  
|Componenti di Microsoft SQL Server Compact 4.0 SP1|Necessari per archiviare le informazioni relative alle operazioni client.|  


####  <a name="dotNet"></a> Informazioni dettagliate aggiuntive su Microsoft .NET Framework versione 4.5.2  

> [!NOTE]  
>  Le versioni .NET 4.0, 4.5 e 4.5.1 non sono più supportate. Per altre informazioni, vedere le [domande frequenti sul ciclo di vita del supporto per Microsoft .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Per completare l'installazione di Microsoft .NET Framework versione 4.5.2 potrebbe essere necessario un riavvio. L'utente riceve la notifica **Riavvio richiesto** sulla barra delle applicazioni. Gli scenari comuni seguenti richiedono il riavvio dei computer client:  

-   Applicazioni o servizi .NET sono in esecuzione NEL computer.  

-   Mancano uno o più aggiornamenti software necessari per l'installazione di .NET.  

-   Il computer è in attesa di un riavvio dalla precedente installazione di aggiornamenti software di .NET Framework.  


Al termine dell'installazione di .NET Framework 4.5.2, potrebbero essere necessari ulteriori aggiornamenti. Tali aggiornamenti successivi, potrebbero richiedere un riavvio del computer.  


### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

Per altre informazioni, vedere [Determinare i ruoli del sistema del sito per i client](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

|Componente|Descrizione|  
|---|---|  
|Punto di gestione|Per distribuire il client di Configuration Manager, non è necessario un punto di gestione. I client richiedono un punto di gestione per trasferire le informazioni con il sito. Senza un punto di gestione, non è possibile gestire i computer client.|  
|Punto di distribuzione|Il punto di distribuzione è un ruolo del sistema del sito facoltativo, ma consigliato per la distribuzione e la gestione dei client. Tutti i punti di distribuzione ospitano i file di origine del client. I client trovano il punto di distribuzione più vicino da cui scaricare i file di origine durante la distribuzione o l'aggiornamento del client. Se il sito non dispone di un punto di distribuzione, i computer scaricano i file di origine client dal punto di gestione.|  
|Punto di stato di fallback|Il punto di stato di fallback è un ruolo del sistema del sito facoltativo, ma consigliato per la distribuzione client. Il punto di stato di fallback tiene traccia della distribuzione client e consente ai computer nel sito di Configuration Manager di inviare messaggi di stato quando non possono comunicare con un punto di gestione.|  
|Punto di Reporting Services|Il punto di Reporting Services è un ruolo del sistema del sito facoltativo, ma consigliato. Visualizza i report relativi alla gestione e alla distribuzione del client. Per altre informazioni, vedere [Creazione di report in Configuration Manager](/sccm/core/servers/manage/reporting).|  


### <a name="installation-method-dependencies"></a>Dipendenze del metodo di installazione  

I prerequisiti seguenti sono specifici dei diversi metodi di installazione client.  

#### <a name="client-push-installation"></a>Installazione push client  

   -   Il sito usa account di installazione push client per connettersi ai computer per installare il client. Specificare questi account nella scheda **Account** delle proprietà di installazione push client. L'account deve essere membro del gruppo Administrators locale nel computer di destinazione.  

         Se non si specifica un account di installazione push client, il server del sito usa il proprio account computer.  

   -   Il sito deve individuare il computer in cui verrà installato il client. È necessario almeno un metodo di individuazione di Configuration Manager.  

   -   Il computer dispone di una condivisione ADMIN$.  

   -   Per eseguire automaticamente il push del client di Configuration Manager nelle risorse individuate, selezionare l'opzione **Abilita installazione push client per le risorse assegnate** in Proprietà installazione push client.  

   -   Il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione per scaricare i file di origine.  

   -   A partire dalla versione 1806, quando si richiede l'autenticazione reciproca Kerberos, i client devono risiedere in una foresta Active Directory attendibile. Il protocollo Kerberos in Windows si basa su Active Directory per l'autenticazione reciproca.<!--1358204-->  


Per usare il push client, sono necessarie le autorizzazioni di sicurezza seguenti:  

   -   Per configurare l'account di installazione push client: autorizzazione **Modifica** e **Lettura** per l'oggetto **Sito**.  

   -   Per usare il push client per installare il client in raccolte, dispositivi e query: autorizzazione **Modifica risorsa** e **Lettura** per l'oggetto **Raccolta**.  


Il ruolo di sicurezza **Amministratore infrastruttura** predefinito include le autorizzazioni necessarie per gestire le installazioni push client.  


#### <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  

   -   Se lo schema di Active Directory non è stato esteso o se si installano i client da un'altra foresta, usare Criteri di gruppo per effettuare il provisioning dei parametri di installazione per CCMSetup.exe. Per altre informazioni, vedere [Come effettuare il provisioning delle proprietà di installazione client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Pubblicare il client di Configuration Manager nel punto di aggiornamento software.  

   -   Per scaricare i file di origine, il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione.  


Per le autorizzazioni di sicurezza necessarie per gestire gli aggiornamenti software di Configuration Manager, vedere [Prerequisiti per gli aggiornamenti software](/sccm/sum/plan-design/prerequisites-for-software-updates).  


#### <a name="group-policy-based-installation"></a>Installazione basata sui criteri di gruppo  

   -   Se lo schema di Active Directory non è stato esteso o se si installano i client da un'altra foresta, usare Criteri di gruppo per effettuare il provisioning dei parametri di installazione per CCMSetup.exe. Per altre informazioni, vedere [Come effettuare il provisioning delle proprietà di installazione client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Per scaricare i file di origine, il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione.  


#### <a name="logon-script-based-installation"></a>Installazione basata su script di accesso  

Per scaricare i file di origine, il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione. A meno che CCMSetup.exe non sia stato specificato con il parametro della riga di comando seguente: `ccmsetup /source`  


#### <a name="manual-installation"></a>Installazione manuale  

Per scaricare i file di origine, il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione. A meno che CCMSetup.exe non sia stato specificato con il parametro della riga di comando seguente: `ccmsetup /source`  


#### <a name="microsoft-intune-mdm-installation"></a>Installazione MDM di Microsoft Intune

 - Richiede un abbonamento di Microsoft Intune e le licenze appropriate.  

 - Richiede che il dispositivo abbia accesso a Internet, anche se non è basato su Internet.  

 - A seconda del caso d'uso, può richiedere anche una o entrambe delle tecnologie seguenti o entrambe:  

     - Azure Active Directory  

     - Gateway di gestione cloud  


#### <a name="workgroup-computer-installation"></a>Installazione di computer del gruppo di lavoro  

Per accedere alle risorse nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso alla rete per il sito.  

Per altre informazioni su come configurare l'account di accesso alla rete, vedere [Concetti di base per la gestione dei contenuti](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Installazione basata sulla distribuzione software (solo per aggiornamenti)  

   -   Se lo schema di Active Directory non è stato esteso o se si installano i client da un'altra foresta, usare Criteri di gruppo per effettuare il provisioning dei parametri di installazione per CCMSetup.exe. Per altre informazioni, vedere [Come effettuare il provisioning delle proprietà di installazione client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).   

   -   Per scaricare i file di origine, il computer client deve poter comunicare con un punto di distribuzione o un punto di gestione.  


Per le autorizzazioni di sicurezza necessarie per eseguire l'aggiornamento client di Configuration Manager usando la gestione delle applicazioni, vedere [Sicurezza e privacy per la gestione delle applicazioni ](/sccm/apps/plan-design/security-and-privacy-for-application-management).  


#### <a name="automatic-client-upgrades"></a>Aggiornamenti automatici del client  

È necessario essere membro del ruolo di sicurezza **Amministratore completo** per configurare gli aggiornamenti client automatici.  


### <a name="firewall-requirements"></a>Requisiti del firewall  

Se esiste un firewall tra i server di sistema del sito e i computer in cui si vuole installare il client di Configuration Manager, vedere [Impostazioni di Windows Firewall e delle porte per i client](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Prerequisiti per i client di dispositivi mobili  

Quando si installa il client di Configuration Manager in dispositivi mobili e si esegue la registrazione, usare le informazioni seguenti per determinare i prerequisiti.  

### <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

-   Un'autorità di certificazione (CA) globale (enterprise) Microsoft con modelli di certificato per distribuire e gestire i certificati necessari per i dispositivi mobili.  

     La CA emittente deve approvare automaticamente le richieste di certificati degli utenti dei dispositivi mobili durante il processo di registrazione.  

     Per altre informazioni sui requisiti dei certificati, vedere [Sicurezza e privacy per i profili certificato](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles).  

-   Un gruppo di sicurezza contenente gli utenti che possono registrare i propri dispositivi mobili.  

     Questo gruppo di sicurezza viene usato per configurare il modello di certificato usato durante la registrazione del dispositivo mobile.  

-   Facoltativo ma consigliato: un alias DNS (record CNAME) denominato **ConfigMgrEnroll**. Configurare l'alias per il nome del server del punto proxy di registrazione.  

     Questo alias DNS è necessario per supportare il rilevamento automatico per il servizio di registrazione. Se non si configura il record DNS, gli utenti devono specificare manualmente il nome del punto proxy di registrazione durante il processo di registrazione.  

-   Dipendenze di ruoli del sistema del sito per i computer che eseguono i ruoli del sistema del sito del punto di registrazione e del punto proxy di registrazione.  

     Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  


### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

Per altre informazioni, vedere [Determinare i ruoli del sistema del sito per i client](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

- Punto di gestione configurato per le connessioni client HTTPS e abilitato per i dispositivi mobili  

   Per installare il client di Configuration Manager in dispositivi mobili è sempre necessario un punto di gestione. Oltre ai requisiti di configurazione di HTTPS e all'abilitazione per dispositivi mobili, il punto di gestione deve essere configurato con FQDN Internet e deve accettare connessioni client da Internet.  

- Punto di registrazione e punto proxy di registrazione  

   Un punto proxy di registrazione gestisce le richieste di registrazione da parte di dispositivi mobili e il punto di registrazione completa il processo di registrazione. È necessario che il punto di registrazione si trovi nella stessa foresta Active Directory del server del sito, ma il punto proxy di registrazione può trovarsi in una foresta diversa.  

- Impostazioni del client per la registrazione dei dispositivi portatili  

   Configurare le impostazioni del client per consentire agli utenti di registrare i dispositivi mobili e configurare almeno un profilo di registrazione.  

- Punto di Reporting Services  

   Il punto di Reporting Services è un ruolo di sistema sito facoltativo ma consigliato, in grado di visualizzare report correlati alla registrazione di dispositivi mobili e alla gestione di client.  

   Per altre informazioni, vedere [Creazione di report in Configuration Manager](/sccm/core/servers/manage/reporting).  

- Per configurare la registrazione per dispositivi mobili, è necessario disporre delle autorizzazioni di sicurezza seguenti:  

  - Per aggiungere, modificare ed eliminare i ruoli di sistema sito di registrazione: autorizzazione **Modifica** per l'oggetto **Sito**.  

  - Per configurare le impostazioni del client per la registrazione: le impostazioni client predefinite necessitano dell'autorizzazione di **Modifica** per l'oggetto **Sito** e le impostazioni client personalizzate necessitano di autorizzazioni di tipo **Agente client**.  

    Il ruolo di sicurezza **Amministratore completo** include le autorizzazioni necessarie per configurare i ruoli del sistema del sito di registrazione.  

    Per gestire i dispositivi mobili registrati, è necessario disporre delle autorizzazioni di sicurezza seguenti:  

  - Per cancellare o ritirare un dispositivo mobile: **Elimina risorsa** per l'oggetto **Raccolta**.  

  - Per annullare un comando di cancellazione o ritiro: **Elimina risorsa** per l'oggetto **Raccolta**.  

  - Per consentire e bloccare i dispositivi mobili: **Modifica risorsa** per l'oggetto **Raccolta**.  

  - Per il blocco remoto o la reimpostazione del passcode in un dispositivo mobile: **Modifica risorsa** per l'oggetto **Raccolta**.  

    Il ruolo di sicurezza **Amministratore operazioni** include le autorizzazioni necessarie per gestire i dispositivi mobili.  

    Per altre informazioni su come configurare le autorizzazioni di sicurezza, vedere [Nozioni fondamentali di amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration) e [Configurare l'amministrazione basata su ruoli](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="firewall-requirements"></a>Requisiti del firewall  

I dispositivi di rete interessati, ad esempio router e firewall e, se applicabile Windows Firewall, devono consentire il traffico associato alla registrazione dei dispositivi mobili:  

-   Tra i dispositivi mobili e il punto proxy di registrazione: HTTPS (per impostazione predefinita, TCP 443)  

-   Tra il punto proxy di registrazione e il punto di registrazione: HTTPS (per impostazione predefinita, TCP 443)  


Se si usa un server Web proxy, deve essere configurato per il tunneling SSL. Il bridging SSL non è supportato per i dispositivi mobili.  
