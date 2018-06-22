---
title: Prerequisiti per la distribuzione di client Windows
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per la distribuzione di client Configuration Manager a computer Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf929e605a7d44ac2f29226177d3ab962eb8fba0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336851"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Prerequisiti per la distribuzione dei client nei computer Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La distribuzione di client di Configuration Manager nell'ambiente ha le dipendenze esterne e le dipendenze nel prodotto seguenti. Ogni metodo di distribuzione client presenta inoltre proprie dipendenze che devono essere soddisfatte per garantire la correttezza delle installazioni client.  

  Leggere anche [Configurazioni supportate](../../../core/plan-design/configs/supported-configurations.md) per verificare che i dispositivi soddisfino i requisiti minimi per l'hardware e il sistema operativo per il client Configuration Manager.  

 Per informazioni sui prerequisiti per il client Configuration Manager per Linux e UNIX, vedere [Pianificazione della distribuzione del client in computer Linux e UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

> [!NOTE]  
>  I numeri delle versioni software elencati in questo articolo si riferiscono solo ai numeri delle versioni minime richieste.  



##  <a name="BKMK_prereqs_computers"></a> Prerequisiti per computer client  
 Usare le informazioni seguenti per determinare i prerequisiti quando si installa il client di Configuration Manager in computer.  

### <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|||  
|-|-|  
|Windows Installer versione 3.1.4000.2435|Necessario per supportare l'utilizzo di file di aggiornamento di Windows Installer (MSP) per pacchetti e aggiornamenti software.|  
|[KB2552033](https://go.microsoft.com/fwlink/p/?LinkId=240048)|Installare questo hotfix nei server del sito che eseguono Windows Server 2008 R2 quando l'installazione push client è abilitata.|  
|Microsoft Background Intelligent Transfer Service (BITS) versione 2.5|Necessario per consentire i trasferimenti di dati limitati tra il computer client e i sistemi del sito di Configuration Manager. BITS non viene scaricato automaticamente durante l'installazione del client. Quando BITS viene installato nei computer, in genere è necessario un riavvio per completare l'installazione.<br /><br /> La maggior parte dei sistemi operativi include BITS, ma, in caso contrario (ad esempio, in Windows Server 2003 R2 SP2), è necessario installare BITS prima di installare il client di Configuration Manager.|  
|Utilità di pianificazione di Microsoft|Per completare l'installazione del client, abilitare questo servizio sul client stesso.|  

### <a name="bkmk_ExternalDependencies"></a> Dipendenze esterne a Configuration Manager e scaricate automaticamente durante l'installazione  
 Il client di Configuration Manager ha alcune potenziali relazioni esterne. Queste dipendenze variano a seconda del sistema operativo e del software installato nel computer client.  

 Se queste dipendenze sono necessarie per completare l'installazione del client, vengono installate automaticamente con il software client.  

|||  
|-|-|  
|Agente di Windows Update versione 7.0.6000.363|Richiesto da Windows per supportare il rilevamento e la distribuzione degli aggiornamenti.|  
|Microsoft Core XML Services (MSXML) versione 6.20.5002 o successiva|Necessario per supportare l'elaborazione di documenti XML in Windows.|  
|Compressione differenziale remota Microsoft (RDC)|Necessaria per ottimizzare la trasmissione dei dati attraverso la rete.|  
|Microsoft Visual C++ 2013 Redistributable versione 12.0.21005.1|Necessario per supportare le operazioni client. Quando questo aggiornamento viene installato nei computer client, potrebbe essere necessario un riavvio per completare l'installazione.|  
|Microsoft Visual C++ 2005 Redistributable versione 8.0.50727.42|Per la versione 1606 e precedenti, necessario per supportare le operazioni di Microsoft SQL Server Compact.|  
|API per Windows Imaging 6.0.6001.18000|Necessario per consentire a Configuration Manager di gestire i file di immagine Windows (wim).|  
|Microsoft Policy Platform 1.2.3514.0|Necessario per consentire ai client di valutare le impostazioni di conformità.|  
|Microsoft Silverlight 5.1.41212.0|Necessario per supportare l'esperienza utente del sito Web Catalogo applicazioni. A partire da Configuration Manager 1802, Silverlight non viene più installato automaticamente. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per il sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1° giugno 2018.<!--1356195-->|  
|Microsoft .NET Framework version 4.5.2|Necessario per supportare le operazioni client. Viene installato automaticamente nel computer client se Microsoft .NET Framework 4.5 o versione successiva non è installato in tale computer. Per altre informazioni, vedere [Informazioni aggiuntive su Microsoft .NET Framework versione 4.5.2](#dotNet).|  
|Componenti di Microsoft SQL Server Compact 3.5 SP2|Necessari per archiviare le informazioni relative alle operazioni client.|  
|Componenti di Microsoft Windows Imaging|Richiesti da Microsoft .NET Framework 4.0 per Windows Server 2003 o Windows XP SP2 per computer a 64 bit.|
|Client software PC di Microsoft Intune|Non è possibile eseguire il client software PC di Intune e il client di Configuration Manager sullo stesso PC. Prima di installare il client di Configuration Manager, verificare che il client di Intune sia stato rimosso.|

####  <a name="dotNet"></a> Informazioni dettagliate aggiuntive su Microsoft .NET Framework versione 4.5.2  

> [!NOTE]  
>  Il 12 gennaio 2016 il supporto per .NET 4.0, 4.5 e 4.5.1 è scaduto. Per altre informazioni, vedere le [domande frequenti sul ciclo di vita del supporto per Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  

 Per completare l'installazione potrebbe essere necessario un riavvio di Microsoft .NET Framework versione 4.5.2. L'utente riceve la notifica **Riavvio richiesto** sulla barra delle applicazioni. Scenari comuni che richiedono il riavvio dei computer client:  

-   Applicazioni o servizi .NET sono in esecuzione NEL computer.  

-   Mancano uno o più aggiornamenti software necessari per l'installazione di .NET.  

-   Il computer è in attesa di un riavvio dalla precedente installazione di aggiornamenti software di .NET Framework.  

 Dopo l'installazione di .NET Framework 4.5.2, i relativi aggiornamenti aggiuntivi potrebbero essere installati successivamente, operazione che potrebbe richiedere ulteriori riavvii del computer.  

### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  
 Per altre informazioni, vedere [Determinare i ruoli del sistema del sito per i client](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md)  

|||  
|-|-|  
|Punto di gestione|Anche se non è necessario un punto di gestione per distribuire un client di Configuration Manager, è invece necessario un punto di gestione per trasferire informazioni tra i computer client e i server di Configuration Manager. Senza un punto di gestione, non è possibile gestire i computer client.|  
|Punto di distribuzione|Il punto di distribuzione è un ruolo del sistema del sito facoltativo, ma consigliato per la distribuzione client. Tutti i punti di distribuzione ospitano i file di origine client che consentono ai computer di trovare il punto di distribuzione più vicino da cui scaricare i file di origine client durante la distribuzione client. Se il sito non dispone di un punto di distribuzione, i computer scaricano i file di origine client dal punto di gestione.|  
|Punto di stato di fallback|Il punto di stato di fallback è un ruolo del sistema del sito facoltativo, ma consigliato per la distribuzione client. Il punto di stato di fallback tiene traccia della distribuzione client e consente ai computer nel sito di Configuration Manager di inviare messaggi di stato quando non possono comunicare con un punto di gestione.|  
|Punto di Reporting Services|Il punto di Reporting Services è un ruolo del sistema del sito facoltativo, ma consigliato, in grado di visualizzare report correlati alla distribuzione e alla gestione di client. Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Dipendenze del metodo di installazione  
 I prerequisiti seguenti sono specifici dei diversi metodi di installazione client.  

#### <a name="client-push-installation"></a>Installazione push client  

   -   Gli account di installazione push client vengono usati per connettersi ai computer per installare il client e vengono specificati nella scheda **Account** della finestra di dialogo **Proprietà installazione push client** . L'account deve essere membro del gruppo Administrators locale nel computer di destinazione.  

         Se non si specifica un account di installazione push client, viene usato l'account del computer server del sito.  

   -   È necessario che il computer in cui si sta installando il client sia stato individuato da almeno un metodo di individuazione di Configuration Manager.  

   -   Il computer dispone di una condivisione ADMIN$.  

   -   L'opzione **Abilita installazione push client per le risorse assegnate** deve essere selezionata nella finestra di dialogo **Proprietà installazione push client** se si vuole eseguire il push automatico del client di Configuration Manager per le risorse individuate.  

   -   Il computer client deve essere in grado di contattare un punto di distribuzione o un punto di gestione per scaricare i file di supporto.  


È necessario avere le autorizzazioni di sicurezza seguenti per installare il client di Configuration Manager usando il push client:  

   -   Per configurare l'account di installazione push client: autorizzazione di **Modifica** e Lettura per l'oggetto **Site** .  

   -   Per usare il push client per installare il client in raccolte, dispositivi e query: autorizzazione di **Modifica risorsa** e **Lettura** per l'oggetto Collection.  


Il ruolo di sicurezza **Amministratore infrastruttura** include le autorizzazioni necessarie per gestire l'installazione push client.  


#### <a name="software-update-point-based-installation"></a>Installazione basata sul punto di aggiornamento software  

   -   Se lo schema di Active Directory non è stato esteso o si stanno installando client da un'altra foresta, è necessario effettuare il provisioning delle proprietà di installazione per CCMSetup.exe nel Registro di sistema del computer usando criteri di gruppo. Per altre informazioni, vedere [Come eseguire il provisioning delle proprietà di installazione client (criteri di gruppo e installazione client basata su aggiornamento software)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   Il client di Configuration Manager deve essere pubblicato al punto di aggiornamento software.  

   -   Il computer client deve essere in grado di contattare un punto di distribuzione o un punto di gestione per scaricare i file di supporto.  


Per le autorizzazioni di sicurezza necessarie per gestire gli aggiornamenti software di Configuration Manager, vedere [Prerequisiti per gli aggiornamenti software](../../../sum/plan-design/prerequisites-for-software-updates.md).  


#### <a name="group-policy-based-installation"></a>Installazione basata sui criteri di gruppo  

   -   Se lo schema di Active Directory non è stato esteso o si stanno installando client da un'altra foresta, è necessario effettuare il provisioning delle proprietà di installazione per CCMSetup.exe nel Registro di sistema del computer usando criteri di gruppo. Per altre informazioni, vedere [Come eseguire il provisioning delle proprietà di installazione client (criteri di gruppo e installazione client basata su aggiornamento software)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   Il computer client deve essere in grado di contattare un punto di gestione per scaricare i file di supporto.  


#### <a name="logon-script-based-installation"></a>Installazione basata su script di accesso  

Il computer client deve essere in grado di contattare un punto di distribuzione o un punto di gestione per scaricare i file di supporto. A meno che CCMSetup.exenon sia stato specificato con la proprietà della riga di comando **ccmsetup /source**.  


#### <a name="manual-installation"></a>Installazione manuale  

Il computer client deve essere in grado di contattare un punto di distribuzione o un punto di gestione per scaricare i file di supporto. A meno che CCMSetup.exenon sia stato specificato con la proprietà della riga di comando **ccmsetup /source**.  


#### <a name="microsoft-intune-mdm-installation"></a>Installazione MDM di Microsoft Intune

 - Richiede un abbonamento di Microsoft Intune e le licenze appropriate.  

 - Richiede che il dispositivo abbia accesso a Internet, anche se non è basato su Internet.  

 - A seconda del caso d'uso, può richiedere anche una o entrambe le tecnologie seguenti:  

     - Azure Active Directory  

     - Gateway di gestione cloud  


#### <a name="workgroup-computer-installation"></a>Installazione di computer del gruppo di lavoro  

Per accedere alle risorse nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso di rete per il sito.  

Per altre informazioni su come configurare l'account di accesso alla rete, vedere [Concetti di base per la gestione dei contenuti](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Installazione basata sulla distribuzione software (solo per aggiornamenti)  

   -   Se lo schema di Active Directory non è stato esteso o si stanno installando client da un'altra foresta, è necessario effettuare il provisioning delle proprietà di installazione per CCMSetup.exe nel Registro di sistema del computer usando criteri di gruppo. Per altre informazioni, vedere [Come eseguire il provisioning delle proprietà di installazione client (criteri di gruppo e installazione client basata su aggiornamento software)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

   -   Il computer client deve essere in grado di contattare un punto di distribuzione o un punto di gestione per scaricare i file di supporto.  


Per le autorizzazioni di sicurezza necessarie per eseguire l'aggiornamento client di Configuration Manager usando la gestione delle applicazioni, vedere [Sicurezza e privacy per la gestione delle applicazioni ](../../../apps/plan-design/security-and-privacy-for-application-management.md).  


#### <a name="automatic-client-upgrades"></a>Aggiornamenti automatici del client  

È necessario essere membro del ruolo di sicurezza **Amministratore completo** per configurare gli aggiornamenti client automatici.  


### <a name="firewall-requirements"></a>Requisiti del firewall  

Se esiste un firewall tra i server di sistema del sito e i computer in cui si vuole installare il client di Configuration Manager, vedere [Impostazioni di Windows Firewall e delle porte per i client](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Prerequisiti per i client di dispositivi mobili  

Quando si installa il client di Configuration Manager in dispositivi mobili e si esegue la registrazione, usare le informazioni seguenti per determinare i prerequisiti.  

### <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

-   Un'autorità di certificazione (CA) globale (enterprise) Microsoft con modelli di certificato per distribuire e gestire i certificati necessari per i dispositivi mobili.  

     La CA emittente deve approvare automaticamente le richieste di certificati degli utenti dei dispositivi mobili durante il processo di registrazione.  

     Per altre informazioni sui requisiti dei certificati, vedere [Sicurezza e privacy per i profili certificato](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

-   Un gruppo di sicurezza contenente gli utenti che possono registrare i propri dispositivi mobili.  

     Questo gruppo di sicurezza viene usato per configurare il modello di certificato usato durante la registrazione del dispositivo mobile.  

-   Facoltativo ma consigliato: un alias DNS (record CNAME) denominato **ConfigMgrEnroll**. Configurare l'alias per il nome del server del punto proxy di registrazione.  

     Questo alias DNS è necessario per supportare il rilevamento automatico per il servizio di registrazione. Se non si configura il record DNS, gli utenti devono specificare manualmente il nome del punto proxy di registrazione durante il processo di registrazione.  

-   Dipendenze di ruoli del sistema del sito per i computer che eseguono i ruoli del sistema del sito del punto di registrazione e del punto proxy di registrazione.  

     Vedere [Sistemi operativi supportati per i server del sistema del sito](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  
 Per altre informazioni, vedere [Determinare i ruoli del sistema del sito per i client](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

-   Punto di gestione configurato per le connessioni client HTTPS e abilitato per i dispositivi mobili  

     Per installare il client di Configuration Manager in dispositivi mobili è sempre necessario un punto di gestione. Oltre ai requisiti di configurazione di HTTPS e all'abilitazione per dispositivi mobili, il punto di gestione deve essere configurato con FQDN Internet e deve accettare connessioni client da Internet.  

-   Punto di registrazione e punto proxy di registrazione  

     Un punto proxy di registrazione gestisce le richieste di registrazione da parte di dispositivi mobili e il punto di registrazione completa il processo di registrazione. È necessario che il punto di registrazione si trovi nella stessa foresta Active Directory del server del sito, ma il punto proxy di registrazione può trovarsi in una foresta diversa.  

-   Impostazioni del client per la registrazione dei dispositivi portatili  

     Configurare le impostazioni del client per consentire agli utenti di registrare i dispositivi mobili e configurare almeno un profilo di registrazione.  

-   Punto di Reporting Services  

     Il punto di Reporting Services è un ruolo di sistema sito facoltativo ma consigliato, in grado di visualizzare report correlati alla registrazione di dispositivi mobili e alla gestione di client.  

     Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Per configurare la registrazione per dispositivi mobili, è necessario disporre delle autorizzazioni di sicurezza seguenti:  

    -   Per aggiungere, modificare ed eliminare i ruoli di sistema sito di registrazione: autorizzazione di **Modifica** per l'oggetto **Site** .  

    -   Per configurare le impostazioni del client per la registrazione: le impostazioni client predefinite necessitano dell'autorizzazione di **Modifica** per l'oggetto **Site** e le impostazioni client personalizzate necessitano di autorizzazioni di tipo **Agente client**  .  

     Il ruolo di sicurezza **Amministratore completo** include le autorizzazioni necessarie per configurare i ruoli di sistema sito di registrazione.  

     Per gestire i dispositivi mobili registrati, è necessario disporre delle autorizzazioni di sicurezza seguenti:  

    -   Per cancellare o ritirare un dispositivo mobile: **Elimina risorsa** per l'oggetto **Collection** .  

    -   Per annullare un comando di cancellazione o ritiro: **Elimina risorsa** per l'oggetto **Collection** .  

    -   Per consentire e bloccare i dispositivi mobili: **Modifica risorsa** per l'oggetto **Collection** .  

    -   Per il blocco remoto o la reimpostazione del passcode in un dispositivo mobile: **Modifica risorsa** per l'oggetto **Collection** .  

     Il ruolo di sicurezza **Amministratore operazioni** include le autorizzazioni necessarie per gestire i dispositivi portatili.  

     Per altre informazioni su come configurare le autorizzazioni di sicurezza, vedere [Nozioni fondamentali di amministrazione basata su ruoli](../../../core/understand/fundamentals-of-role-based-administration.md) e [Configurare l'amministrazione basata su ruoli](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Requisiti del firewall  
I dispositivi di rete interessati, ad esempio router e firewall e, se applicabile Windows Firewall, devono consentire il traffico associato alla registrazione dei dispositivi mobili:  

-   Tra i dispositivi mobili e il punto proxy di registrazione: HTTPS (per impostazione predefinita, TCP 443)  

-   Tra il punto proxy di registrazione e il punto di registrazione: HTTPS (per impostazione predefinita, TCP 443)  


Se si usa un server Web proxy, sarà necessario configurarlo per il tunneling SSL. Il bridging SSL non è supportato per i dispositivi mobili.  
