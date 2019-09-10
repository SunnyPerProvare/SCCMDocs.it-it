---
title: Requisiti per l'accesso a Internet
titleSuffix: Configuration Manager
description: Informazioni sugli endpoint Internet a cui consentire l'accesso per usufruire delle funzionalità complete di Configuration Manager.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11241176abade1233a6fbdbe2ee3bdd0e3219e48
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243580"
---
# <a name="internet-access-requirements"></a>Requisiti per l'accesso a Internet

Alcune caratteristiche di Configuration Manager hanno bisogno della connettività Internet per funzionare completamente. Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, assicurarsi di consentire l'accesso a questi endpoint.

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a> Punto di connessione del servizio

Queste configurazioni si applicano al computer che ospita il punto di connessione del servizio e gli eventuali firewall posti tra il computer e Internet. Entrambe devono consentire le comunicazioni tramite la porta in uscita **TCP 443** per HTTPS e la porta in uscita **TCP 80** per HTTP ai percorsi Internet seguenti.

Il punto di connessione del servizio supporta l'uso di un proxy Web (con o senza autenticazione) per accedere a questi percorsi. Per altre informazioni, vedere [Supporto dei server proxy](/sccm/core/plan-design/network/proxy-server-support).

Per altre informazioni sul punto di connessione del servizio, vedere [Informazioni sul punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

Altre funzionalità di Configuration Manager possono richiedere endpoint aggiuntivi dal punto di connessione del servizio. Per altre informazioni, vedere le altre sezioni in questo articolo.

> [!TIP]  
> Il punto di connessione del servizio usa il servizio Microsoft Intune quando si connette a `go.microsoft.com` o a `manage.microsoft.com`. Esiste un problema noto per cui il connettore Intune riscontra problemi di connettività se il certificato radice Baltimore CyberTrust non è installato, è scaduto o è danneggiato nel punto di connessione del servizio. Per altre informazioni, vedere [KB 3187516: Il punto di connessione del servizio non scarica gli aggiornamenti](https://support.microsoft.com/help/3187516).  

### <a name="a-namebkmk_scp-updates-updates-and-servicing"></a><a name="bkmk_scp-updates"/> Aggiornamenti e manutenzione

Per altre informazioni su questa funzione, vedere [Aggiornamenti e manutenzione per Configuration Manager](/sccm/core/servers/manage/updates).

> [!Tip]  
> Abilitare questi endpoint per la regola delle [informazioni dettagliate sulla gestione](/sccm/core/servers/manage/management-insights), **connettere il sito al cloud Microsoft per gli aggiornamenti di Configuration Manager**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="microsoft-intune"></a>Microsoft Intune

Per altre informazioni su questa funzione, vedere [Soluzione MDM ibrida con Configuration Manager e Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### <a name="windows-10-servicing"></a>Manutenzione di Windows 10

Per altre informazioni su questa funzione, vedere [Gestire Windows come servizio](/sccm/osd/deploy-use/manage-windows-as-a-service).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Servizi di Azure

Per altre informazioni su questa funzione, vedere [Configurare i servizi di Azure da usare con Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).

- `management.azure.com`  


## <a name="co-management"></a>Co-gestione

Se si registrano dispositivi di Windows 10 in Microsoft Intune per la co-gestione, assicurarsi che questi dispositivi possano accedere agli endpoint richiesti da Intune. Per altre informazioni, vedere [Endpoint di rete per Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).


## <a name="microsoft-store-for-business"></a>Microsoft Store per le aziende

Se si integra Configuration Manager con [Microsoft Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business), assicurarsi che il punto di connessione del servizio e i dispositivi di destinazione siano in grado di accedere al servizio cloud. Per altre informazioni, vedere [Configurazione del proxy per Microsoft Store per le aziende](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).


## <a name="bkmk_cloud"></a> Servizi cloud

<!-- SCCMDocs-pr #3402 -->

Questa sezione illustra le funzionalità seguenti:

- Cloud Management Gateway
- Punto di distribuzione cloud
- Integrazione di Azure Active Directory (Azure AD)
- Individuazione basata su Azure AD

Per la distribuzione dei servizi Cloud Management Gateway/punto di distribuzione cloud, il **punto di connessione del servizio** deve avere accesso a:

- Gli endpoint di Azure specifici sono diversi per ogni ambiente a seconda della configurazione. Configuration Manager archivia gli endpoint nel database del sito. Eseguire una query nella tabella **AzureEnvironments** in SQL Server per un elenco degli endpoint di Azure.  

Il **punto di connessione di Cloud Management Gateway** deve avere accesso agli endpoint di servizio seguenti:

- ServiceManagementEndpoint: `https://management.core.windows.net/`  

- StorageEndpoint: `blob.core.windows.net` e `table.core.windows.net`

Per il recupero dei token di Azure AD da parte della **console di Configuration Manager** e del **client**:

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

Per l'individuazione utenti di Azure AD, il **punto di connessione del servizio** deve avere accesso a:

- Versione 1810 e precedenti: Endpoint di Azure AD Graph `https://graph.windows.net/`  

- Versione 1902 e successive: Endpoint di Microsoft Graph `https://graph.microsoft.com/`

Il sistema del sito del punto di connessione di Cloud Management Gateway supporta l'uso di un proxy Web. Per altre informazioni sulla configurazione di questo ruolo per un proxy, vedere le [informazioni di supporto per server proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Il punto di connessione di Cloud Management Gateway deve connettersi solo agli endpoint del servizio Cloud Management Gateway. Non ha bisogno dell'accesso ad altri endpoint di Azure.

Per altre informazioni su Cloud Management Gateway, vedere [Pianificare il gateway di gestione cloud in Configuration Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="bkmk_sum"></a> Aggiornamenti software

Consentire al punto di aggiornamento software attivo di accedere agli endpoint seguenti in modo che WSUS e Aggiornamenti automatici possano comunicare con il servizio cloud Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Per altre informazioni sugli aggiornamenti software, vedere [Pianificare gli aggiornamenti software](/sccm/sum/plan-design/plan-for-software-updates).

### <a name="intranet-firewall"></a>Firewall Intranet

Potrebbe essere necessario aggiungere endpoint a un firewall posto tra due sistemi del sito nei casi seguenti:

- Se i siti secondari hanno un punto di aggiornamento software
- Se è presente un punto di aggiornamento software basato su Internet attivo remoto in un sito

#### <a name="software-update-point-on-the-child-site"></a>Punto di aggiornamento software nel sito secondario

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## <a name="manage-office-365"></a>Gestire Office 365

Se si usa Configuration Manager per distribuire e aggiornare Office 365, abilitare gli endpoint seguenti:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` per sincronizzare il punto di aggiornamento software per gli aggiornamenti del client di Office 365

- `config.office.com` per creare configurazioni personalizzate per le distribuzioni di Office 365


## <a name="configuration-manager-console"></a>Console di Configuration Manager

I computer con la console di Configuration Manager richiedono l'accesso agli endpoint Internet seguenti per funzionalità specifiche:

### <a name="in-console-feedback"></a>Feedback nella console

- `http://petrol.office.microsoft.com`

Per altre informazioni su questa funzionalità, vedere [Commenti e suggerimenti sul prodotto](/sccm/core/understand/find-help#product-feedback).

### <a name="community-workspace-documentation-node"></a>Area di lavoro Community, nodo Documentazione

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Per altre informazioni su questo nodo della console, vedere [Uso della console di Configuration Manager](/sccm/core/servers/manage/admin-console).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Area di lavoro Monitoraggio, nodo Gerarchia siti

Se si usa la **vista geografica**, consentire l'accesso all'endpoint seguente:

- `http://maps.bing.com`


## <a name="desktop-analytics"></a>Desktop Analytics

Per altre informazioni sugli endpoint necessari per il servizio cloud Desktop Analytics, vedere [Abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing#endpoints).


## <a name="microsoft-public-ip-addresses"></a>Indirizzi IP pubblici Microsoft

Per altre informazioni sugli intervalli di indirizzi IP Microsoft, vedere [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). Questi indirizzi vengono aggiornati regolarmente. Non esiste alcuna granularità in base al servizio, è possibile usare qualsiasi indirizzo IP compreso in questi intervalli.


## <a name="see-also"></a>Vedere anche

- [Porte usate in Configuration Manager](/sccm/core/plan-design/hierarchy/ports)

- [Supporto dei server proxy in Configuration Manager](/sccm/core/plan-design/network/proxy-server-support)
