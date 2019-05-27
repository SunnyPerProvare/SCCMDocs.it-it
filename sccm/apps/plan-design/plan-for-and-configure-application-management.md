---
title: Pianificare la gestione di applicazioni
titleSuffix: Configuration Manager
description: Implementare e configurare le dipendenze necessarie per la distribuzione di applicazioni in Configuration Manager.
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0c2808bd4fa9501c46012549427e2de4087eb9d
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083392"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Pianificare e configurare la gestione delle applicazioni in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni incluse in questo articolo per implementare le dipendenze necessarie per la distribuzione di applicazioni in Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

È necessario avere IIS nei server che eseguono i ruoli del sistema del sito seguenti:

- Punto per siti Web del Catalogo applicazioni  
- Punto per servizi Web del Catalogo applicazioni  
- Punto di gestione  
- Punto di distribuzione  

Per altre informazioni su questo requisito, vedere [Prerequisiti del sito e del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificati in applicazioni firmate dal codice per dispositivi mobili

Per firmare un'applicazione con codice per distribuirla nei dispositivi mobili, non usare un certificato generato tramite un modello della versione 3 (**Windows Server 2008, Enterprise Edition**). Questo modello di certificato crea un certificato non compatibile con le applicazioni di Configuration Manager per dispositivi mobili.

Se si usano i Servizi certificati Active Directory per firmare con codice applicazioni per dispositivi mobili, non usare un modello di certificato della versione 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Controllare gli eventi di accesso per l'affinità utente-dispositivo  

Se si vuole creare automaticamente le affinità utente-dispositivo, configurare i client per il controllo degli eventi di accesso.

Per determinare le affinità utente-dispositivo automatiche, il client di Configuration Manager legge gli eventi di accesso di tipo **Riuscito** dal registro eventi di sicurezza di Windows. Abilitare questi eventi con i due criteri di controllo seguenti:

- **Controlla eventi di accesso account**
- **Controlla eventi di accesso**

Per creare automaticamente relazioni tra utenti e dispositivi, verificare che queste due impostazioni siano attivate nei computer client. Per configurare queste impostazioni, è possibile usare i criteri di gruppo di Windows.

Per altre informazioni sull'affinità utente-dispositivo, vedere l'argomento [Collegare utenti e dispositivi mediante l'affinità utente-dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager


### <a name="management-point"></a>Punto di gestione

I client contattano un punto di gestione per scaricare i criteri client, individuare il contenuto e connettersi al Catalogo applicazioni. Se i client non possono accedere a un punto di gestione, non potranno usare il Catalogo applicazioni.

> [!Note]  
> A partire dalla versione 1806, i ruoli del Catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Per altre informazioni, vedere [Configurare Software Center](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).<!--1358309-->  
  

### <a name="distribution-point"></a>Punto di distribuzione

Prima di poter distribuire le applicazioni nei client, è necessario almeno un punto di distribuzione nella gerarchia. Per impostazione predefinita, durante un'installazione standard nel server del sito è attivato un ruolo del sito del punto di distribuzione. Il numero e la posizione dei punti di distribuzione variano in base ai requisiti specifici dell'ambiente.

Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="reporting-services-point"></a>Punto di Reporting Services

Per usare i report in Configuration Manager per la gestione delle applicazioni, prima installare e configurare un punto di Reporting Services.

Per altre informazioni, vedere [Creazione di report in Configuration Manager](/sccm/core/servers/manage/reporting).  


### <a name="client-settings"></a>Impostazioni client

Esistono numerose impostazioni client che controllano come il client installa le applicazioni e l'esperienza utente nel dispositivo. Queste impostazioni client includono i gruppi seguenti:

- Agente computer  
- Riavvio del computer  
- Software Center  
- Distribuzione software  
- Affinità utente-dispositivo  

Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulle impostazioni client](/sccm/core/clients/deploy/about-client-settings)  
- [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>Autorizzazioni di sicurezza per la gestione delle applicazioni

- Il ruolo di sicurezza **Autore applicazioni** include le autorizzazioni necessarie per creare, modificare e ritirare le applicazioni.  

- Il ruolo di sicurezza **Gestione distribuzione applicazioni** include le autorizzazioni necessarie per distribuire le applicazioni.  

- Il ruolo sicurezza **Amministratore applicazione** dispone di tutte le autorizzazioni da entrambi i ruoli sicurezza: **Autore applicazioni** e **Gestione distribuzione applicazioni**.  

Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1 o client successivo per l'esecuzione di applicazioni virtuali

Per creare applicazioni virtuali in Configuration Manager, installare App-V 4.6 SP1 o versione successiva nei dispositivi.

Prima di distribuire applicazioni virtuali, aggiornare anche il client App-V con l'aggiornamento rapido descritto nell'[articolo del supporto tecnico Microsoft 2645225](https://support.microsoft.com/help/2645225).  


### <a name="discovered-user-accounts-for-application-catalog"></a>Account utente individuati per il Catalogo applicazioni

Prima che gli utenti possano visualizzare e richiedere applicazioni dal Catalogo applicazioni, Configuration Manager deve individuare gli account utente. Per altre informazioni, vedere [Eseguire l'individuazione](/sccm/core/servers/deploy/configure/run-discovery).  


### <a name="application-catalog-web-service-point"></a>Punto per servizi Web del Catalogo applicazioni

Il punto per servizi Web del Catalogo applicazioni è un ruolo del sistema del sito che fornisce informazioni sul software disponibile nella raccolta software al sito Web del Catalogo applicazioni a cui accedono gli utenti.

Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Installare e configurare il Catalogo applicazioni](#bkmk_appcat).  

> [!Note]  
> A partire dalla versione 1806, il ruolo Punto per servizi Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*.<!--1358309-->  
>
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="application-catalog-website-point"></a>Punto per siti Web del Catalogo applicazioni

Il punto del sito Web del Catalogo applicazioni è un ruolo del sistema del sito che offre agli utenti un elenco del software disponibile.

Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Installare e configurare il Catalogo applicazioni](#bkmk_appcat).

> [!Note]  
> A partire dalla versione 1806, il ruolo Punto per siti Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*.<!--1358309-->  
>
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="bkmk_userex"></a> Configurare Software Center  

Per altre informazioni sulla configurazione e personalizzazione di Software Center, vedere [Pianificare Software Center](/sccm/apps/plan-design/plan-for-software-center).


## <a name="bkmk_appcat"></a> Installare e configurare il Catalogo applicazioni  

> [!Note]  
> A partire dalla versione 1806, i ruoli Punto per siti Web e Punto per servizi Web del Catalogo applicazioni non sono più *necessari*, ma sono ancora *supportati*. Per altre informazioni, vedere [Configurare Software Center](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  
>
> L'**esperienza utente di Silverlight** per il *punto per siti Web* del Catalogo applicazioni non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

> [!IMPORTANT]  
> Prima di eseguire questi passaggi, verificare che tutte le dipendenze siano implementate. Per altre informazioni, vedere le sezioni seguenti di questo articolo:
>
> - [Dipendenze esterne a Configuration Manager](#dependencies-external-to-configuration-manager)  
> - [Dipendenze di Configuration Manager](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>Passaggio 1: Certificato del server Web per HTTPS

Se si usano connessioni HTTPS, distribuire un certificato del server Web nei server di sistema del sito per il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni.

Se si vuole che i client usino il Catalogo Applicazioni da Internet, distribuire un certificato del server Web in almeno un punto di gestione. Configurarlo per le connessioni client da Internet.

Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Passaggio 2: Certificato di autenticazione client per HTTPS

Se si usa un certificato PKI client per le connessioni ai punti di gestione, distribuire un certificato di autenticazione client nei computer client. Anche se i client non usano un certificato PKI del client per connettersi al Catalogo applicazioni, è necessario che si connettano a un punto di gestione prima di poter usare il Catalogo applicazioni.

Distribuire un certificato di autenticazione client nei computer client negli scenari seguenti:

- Tutti i punti di gestione in Intranet accettano solo connessioni client HTTPS.
- I client eseguono la connessione al Catalogo applicazioni da Internet.

Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Passaggio 3: Installare e configurare i ruoli del Catalogo applicazioni

Installare entrambi i ruoli Punto per servizi Web del Catalogo applicazioni e Punto per siti Web del Catalogo applicazioni nello stesso sito. Non è necessario installarli nello stesso server o nella stessa foresta Active Directory. Il punto per servizi Web del Catalogo applicazioni deve trovarsi tuttavia nella stessa foresta del database del sito.

Per altre informazioni sulla selezione host per i server, vedere [Pianificare i server e i ruoli del sistema del sito](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

> [!NOTE]  
> Installare il Catalogo applicazioni in un sito primario. Non è possibile installarlo in un sito secondario o nel sito di amministrazione centrale.  

Installare il Catalogo applicazioni in nuovo server di sistema del sito o in un server esistente nel sito. Per altre informazioni sulla procedura generale, vedere [Installare i ruoli del sistema del sito](/sccm/core/servers/deploy/configure/install-site-system-roles). Nella procedura guidata per aggiungere un ruolo del sistema del sito o creare un server di sistema del sito, selezionare i ruoli seguenti nell'elenco:

- **Punto per servizi Web del Catalogo applicazioni**  
- **Punto per siti Web del Catalogo applicazioni**  

> [!TIP]  
> Se si vuole che i computer client usino il Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verificare l'installazione di questi ruoli del sistema del sito  

- Messaggi di stato: Utilizzare i componenti **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Ad esempio, l'ID stato **1015** per **SMS_PORTALWEB_CONTROL_MANAGER** conferma che Gestione componenti del sito ha completato l'installazione del punto per siti Web del Catalogo applicazioni.  

- File di log: cercare **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Per altre informazioni, cercare i file di log **awebsvcMSI.log** e **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Passaggio 4: Configurare le impostazioni client

Se si vuole che tutti gli utenti abbiano le stesse impostazioni, configurare le impostazioni client predefinite. In caso contrario, configurare le impostazioni client personalizzate per raccolte specifiche.

Per altre informazioni, vedere gli articoli seguenti:

- [Informazioni sulle impostazioni client](/sccm/core/clients/deploy/about-client-settings)  
    - Agente computer  
    - Riavvio del computer  
    - Software Center  
    - Distribuzione software  
    - Affinità utente-dispositivo  
- [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings)  

Il client di Configuration Manager configura i dispositivi con queste impostazioni durante il successivo download dei criteri client. Per attivare il recupero dei criteri per un singolo client, vedere [Come gestire i client](/sccm/core/clients/manage/manage-clients).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passaggio 5: Verificare che il Catalogo applicazioni sia operativo

Utilizzare le seguenti procedure per verificare che il Catalogo applicazioni sia operativo.

> [!NOTE]  
> L'esperienza utente con il Catalogo applicazioni richiede Microsoft Silverlight. Se si usa il Catalogo applicazioni direttamente da un browser, verificare prima di tutto che Microsoft Silverlight sia installato nel computer.  

> [!TIP]  
> La non aderenza ai prerequisiti è una delle più comuni cause di malfunzionamento del Catalogo applicazioni dopo l'installazione. Verificare i prerequisiti per i ruoli del sistema del sito del Catalogo applicazioni. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

In un browser immettere l'indirizzo del sito Web del Catalogo applicazioni. Verificare che nella pagina Web siano presenti tre schede: **Catalogo applicazioni**, **Richieste di applicazioni** e **Dispositivi personali**.  

Usare gli indirizzi appropriati per il Catalogo applicazioni tra quelli dell'elenco seguente, tenendo presente che &lt;server&gt; è il nome del computer, il nome di dominio completo Intranet o il nome di dominio completo Internet:  

- Connessioni client HTTPS e impostazioni predefinite del ruolo del sistema del sito: **https://&lt;server&gt;/CMApplicationCatalog**  

- Connessioni client HTTP e impostazioni predefinite del ruolo del sistema del sito: **http://&lt;server&gt;/CMApplicationCatalog**  

- Connessioni client HTTPS e impostazioni personalizzate del ruolo del sistema del sito: **https://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

- Connessioni client HTTP e impostazioni personalizzate del ruolo del sistema del sito: **http://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

> [!NOTE]  
> Se è stato eseguito l'accesso al dispositivo con un account amministratore di dominio, il client di Configuration Manager non visualizza messaggi di notifica, ad esempio messaggi indicanti che è disponibile nuovo software.  
