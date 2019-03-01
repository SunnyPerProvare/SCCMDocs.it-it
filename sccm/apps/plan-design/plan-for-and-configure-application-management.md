---
title: Pianificare la gestione di applicazioni
titleSuffix: Configuration Manager
description: Implementare e configurare le dipendenze necessarie per la distribuzione di applicazioni in Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 62d750a6ff711afc06ddbcec9b9ad98ecfab758e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124156"
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
> A partire dalla versione 1806, i ruoli del Catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Per altre informazioni, vedere [Configurare Software Center](#bkmk_userex).<!--1358309-->  
  

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

Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center](#bkmk_userex).  

> [!Note]  
> A partire dalla versione 1806, il ruolo Punto per servizi Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*.<!--1358309-->  
> 
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="application-catalog-website-point"></a>Punto per siti Web del Catalogo applicazioni

Il punto del sito Web del Catalogo applicazioni è un ruolo del sistema del sito che offre agli utenti un elenco del software disponibile.
Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center](#bkmk_userex).

> [!Note]  
> A partire dalla versione 1806, il ruolo Punto per siti Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*.<!--1358309-->  
> 
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="bkmk_userex"></a> Configurare Software Center  

Gli utenti modificano le impostazioni e cercano e installano applicazioni in Software Center. Quando si installa il client di Configuration Manager in un dispositivo Windows, viene automaticamente installato Software Center. Il nuovo Software Center ha un aspetto moderno. e le app che venivano visualizzate solo nel Catalogo applicazioni dipendente da Silverlight (app disponibili per gli utenti) vengono visualizzate ora in Software Center nella scheda **Applicazioni**. Per informazioni sulle altre funzionalità di Software Center, vedere il [Manuale dell'utente di Software Center](/sccm/core/understand/software-center).  

Di seguito sono elencati i miglioramenti apportati a Software Center: 

#### <a name="starting-in-version-1802"></a>A partire dalla versione 1802

- L'impostazione client **Usa il nuovo Software Center** nel gruppo **Agente computer** è abilitata per impostazione predefinita. La versione precedente di Software Center non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Gli utenti possono cercare e installare le applicazioni disponibili per gli utenti nei dispositivi aggiunti ad Azure Active Directory (Azure AD). Per altre informazioni, vedere [Deploy user-available applications on Azure AD-joined devices](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) (Distribuire applicazioni disponibili per l'utente in dispositivi aggiunti ad Azure AD).  

#### <a name="starting-in-version-1806"></a>A partire dalla versione 1806

- Specificare la visibilità del collegamento al sito Web del Catalogo applicazioni nella scheda **Stato dell'installazione** di Software Center. Per altre informazioni, vedere Impostazioni client di [Software Center](/sccm/core/clients/deploy/about-client-settings#software-center).  

- I ruoli del catalogo applicazioni non sono più necessari per visualizzare le applicazioni disponibili per gli utenti in Software Center. Questa modifica consente di ridurre l'infrastruttura server necessaria per distribuire le applicazioni agli utenti. Software Center ora si affida al punto di gestione per ottenere queste informazioni e questo consente una migliore scalabilità degli ambienti di grandi dimensioni, che vengono assegnati a [gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Se il Catalogo applicazioni è attualmente in uso, continua a funzionare anche se si aggiorna Configuration Manager alla versione 1806. I ruoli Punto per siti Web e Punto per servizi Web del Catalogo applicazioni non sono più *necessari*, ma sono ancora *supportati*. L'**esperienza utente di Silverlight** per il *punto per siti Web* del Catalogo applicazioni non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). 
    > 
    > Iniziare a pianificare la rimozione dei ruoli del Catalogo applicazioni dall'infrastruttura in futuro. Sfruttare i miglioramenti di Software Center per usare il punto di gestione e semplificare l'ambiente di Configuration Manager.  

Usare la tabella seguente per conoscere i requisiti di Software Center in base alla versione specifica di Configuration Manager:

| Tipo di dispositivo | Versione sito | Infrastruttura | 
|-----------------|--------------|----------------|
| Dispositivo aggiunto ad Azure AD</br>(o "aggiunto a un dominio cloud") | 1802 o 1806 | Punto di gestione per tutte le distribuzioni di app | 
| Dispositivo [aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) in Internet | 1802 o 1806 | Gateway di gestione cloud e punto di gestione per tutte le distribuzioni di app |
| Dispositivo aggiunto a un dominio di Active Directory locale | 1802 | Catalogo applicazioni necessario per le app disponibili per gli utenti in Software Center |
| Dispositivo aggiunto a un dominio di Active Directory locale | 1806 | Punto di gestione per tutte le distribuzioni di app |


> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.



## <a name="branding-software-center"></a>Personalizzazione di Software Center

Modificare l'aspetto di Software Center in modo che risponda ai requisiti di personalizzazione dell'organizzazione. Questa configurazione consente agli utenti di considerare attendibile Software Center. 

Configuration Manager applica la personalizzazione per Software Center in base alle priorità seguenti:  

- Se il Catalogo applicazioni non è stato installato (scelta consigliata):  

    1. Impostazioni client di **Software Center**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center) (Informazioni sulle impostazioni client).  

    2. Impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-agent) (Informazioni sulle impostazioni client).  

- Se il Catalogo applicazioni è stato installato:  

    1. Impostazioni client di **Software Center**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center) (Informazioni sulle impostazioni client).  

    2. Se si connette una sottoscrizione di Microsoft Intune a Configuration Manager, Software Center visualizza il *nome dell'organizzazione*, il *colore* e il *logo aziendale* specificati nelle proprietà della sottoscrizione di Intune. Per ulteriori informazioni, vedere [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. *Nome dell'organizzazione* e *colore* specificati nelle proprietà del punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Configuration options for Application Catalog website point](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website) (Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni).  

    4. Impostazione client **Nome organizzazione** nel gruppo **Agente computer**. Per altre informazioni, vedere [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-agent) (Informazioni sulle impostazioni client).  

#### <a name="configure-software-center-branding"></a>Configurare la personalizzazione di Software Center
<!-- 1351224 --> Personalizzare l'aspetto di Software Center aggiungendo gli elementi di personalizzazione dell'organizzazione e specificando la visibilità delle schede. 

Per altre informazioni, vedere gli articoli seguenti:
- Gruppo di impostazioni client di [Software Center](/sccm/core/clients/deploy/about-client-settings#software-center)  
- [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings)  



## <a name="bkmk_appcat"></a> Installare e configurare il Catalogo applicazioni  

> [!Note]  
> A partire dalla versione 1806, i ruoli Punto per siti Web e Punto per servizi Web del Catalogo applicazioni non sono più *necessari*, ma sono ancora *supportati*. Per altre informazioni, vedere [Configurare Software Center](#bkmk_userex).  
> 
> L'**esperienza utente di Silverlight** per il *punto per siti Web* del Catalogo applicazioni non è più supportata. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

> [!IMPORTANT]  
>  Prima di eseguire questi passaggi, verificare che tutte le dipendenze siano implementate. Per altre informazioni, vedere le sezioni seguenti di questo articolo:
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
>  Se si vuole che i computer client usino il Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Verificare l'installazione di questi ruoli del sistema del sito  

- Messaggi di stato: usare i componenti **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

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


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passaggio 5: verificare che il Catalogo applicazioni sia operativo

Utilizzare le seguenti procedure per verificare che il Catalogo applicazioni sia operativo. 

> [!NOTE]  
>  L'esperienza utente con il Catalogo applicazioni richiede Microsoft Silverlight. Se si usa il Catalogo applicazioni direttamente da un browser, verificare prima di tutto che Microsoft Silverlight sia installato nel computer.  

> [!TIP]  
>  La non aderenza ai prerequisiti è una delle più comuni cause di malfunzionamento del Catalogo applicazioni dopo l'installazione. Verificare i prerequisiti per i ruoli del sistema del sito del Catalogo applicazioni. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

In un browser immettere l'indirizzo del sito Web del Catalogo applicazioni. Verificare che nella pagina Web siano visualizzate tre schede: **Catalogo applicazioni**, **Richieste di applicazioni** e **Dispositivi personali**.  

Usare gli indirizzi appropriati per il Catalogo applicazioni tra quelli dell'elenco seguente, tenendo presente che &lt;server&gt; è il nome del computer, il nome di dominio completo Intranet o il nome di dominio completo Internet:  

- Connessioni client HTTPS e impostazioni predefinite del ruolo del sistema del sito: **https://&lt;server&gt;/CMApplicationCatalog**  

- Connessioni client HTTP e impostazioni predefinite del ruolo del sistema del sito: **http://&lt;server&gt;/CMApplicationCatalog**  

- Connessioni client HTTPS e impostazioni personalizzate del ruolo del sistema del sito: **https://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

- Connessioni client HTTP e impostazioni personalizzate del ruolo del sistema del sito: **http://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

> [!NOTE]  
>  Se è stato eseguito l'accesso al dispositivo con un account amministratore di dominio, il client di Configuration Manager non visualizza messaggi di notifica, ad esempio messaggi indicanti che è disponibile nuovo software.  

