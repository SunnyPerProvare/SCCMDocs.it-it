---
title: Porte usate da Configuration Manager | Microsoft Docs
description: Informazioni sulle porte necessarie e personalizzabili usate da System Center Configuration Manager per le connessioni.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 41000b978f1add9ec6910bfa86f13e92bf93c4e4


---
# <a name="ports-used-in-system-center-configuration-manager"></a>Porte usate in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager è un sistema client/server distribuito. Per natura distribuita di Configuration Manager si intende la possibilità di stabilire connessioni tra server del sito, sistemi del sito e client. Alcune connessioni usano porte non configurabili e altre supportano porte personalizzate che vengono specificate. È necessario verificare che le porte richieste siano disponibili se si usa una qualsiasi tecnologia di filtro delle porte, ad esempio firewall, router, server proxy e IPsec.  

> [!NOTE]  
>  Se si supportano client basati su Internet tramite il bridging SSL, oltre ai requisiti delle porte è necessario consentire anche ad alcune intestazioni e alcuni verbi HTTP di superare il firewall. .  

 Le porte indicate di seguito vengono usate da Configuration Manager e non includono informazioni per servizi Windows standard, ad esempio impostazioni di criteri di gruppo per l'autenticazione Kerberos e per Active Directory Domain Services. Per informazioni sulle porte e sui servizi di Windows Server, vedere [Panoramica dei servizi e requisiti per le porte di rete per il sistema server Windows](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="a-namebkmkconfigurableportsa-ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Porte che è possibile configurare  
 Configuration Manager consente di configurare le porte per i tipi di comunicazione seguenti:  

-   Dal punto per siti Web del Catalogo applicazioni al punto per servizi Web del Catalogo applicazioni  

-   Dal punto proxy di registrazione al punto di registrazione  

-   Da client a sistemi del sito che eseguono IIS  

-   Da client a Internet (come impostazioni server proxy)  

-   Dal punto di aggiornamento software a Internet (come impostazioni server proxy)  

-   Dal punto di aggiornamento software al server WSUS  

-   Dal server del sito al server del database del sito  

-   Punti di Reporting Services  

    > [!NOTE]  
    >  Le porte in uso per il ruolo del sistema del sito del punto di Reporting Services vengono configurate in SQL Server Reporting Services. Queste porte vengono usate da Configuration Manager durante le comunicazioni al punto di Reporting Services. Assicurarsi di esaminare queste porte definendo le informazioni del filtro IP per i criteri IPsec o per la configurazione dei firewall.  

Per impostazione predefinita, la porta HTTP usata per la comunicazione dal client al sistema del sito è la porta 80 e la porta HTTPS predefinita è la porta 443. È possibile modificare le porte per la comunicazione di sistema "client/sito" su HTTP o HTTPS durante l'installazione o nelle proprietà Sito per il sito di Configuration Manager.  

Le porte in uso per il ruolo del sistema del sito del punto di Reporting Services vengono configurate in SQL Server Reporting Services. Queste porte vengono usate da Configuration Manager durante le comunicazioni al punto di Reporting Services. Assicurarsi di esaminare queste porte definendo le informazioni del filtro IP per i criteri IPsec o per la configurazione dei firewall.  

##  <a name="a-namebkmknonconfigurableportsa-non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Porte non configurabili  
Configuration Manager non consente di configurare le porte per i tipi di comunicazione seguenti:  

-   Da sito a sito  

-   Dal server del sito al sistema del sito  

-   Dalla console di Configuration Manager al provider SMS  

-   Dalla console di Configuration Manager a Internet  

-   Connessioni a servizi cloud, ad esempio Microsoft Intune e punti di distribuzione basati su cloud  

##  <a name="a-namebkmkcommunicationportsa-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Porte usate dai sistemi del sito e dai client di Configuration Manager  
Nelle sezioni seguenti vengono riportati i dettagli delle porte usate per la comunicazione in Configuration Manager. Le frecce nel titolo della sezione, tra i computer, rappresentano la direzione della comunicazione:  

-   -- > indica che un computer avvia la comunicazione e l'altro risponde sempre  

-   &lt; -- > indica che la comunicazione può essere avviata da uno dei due computer  

###  <a name="a-namebkmkportsaia-asset-intelligence-synchronization-point-----microsoft"></a><a name="BKMK_PortsAI"></a> Punto di sincronizzazione di Asset Intelligence -- &gt; Microsoft  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsai-to-sqla-asset-intelligence-synchronization-point-----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a> Punto di sincronizzazione di Asset Intelligence -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsappcatalogservice-sqla-application-catalog-web-service-point-----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a> Punto per servizi Web del Catalogo applicazioni -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointappcatalogwebservicepointa-application-catalog-website-point-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Punto per siti Web del Catalogo applicazioni -- &gt; Punto per servizi Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsclient-appcatalogwebsitepointa-client-----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- &gt; Punto per siti Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsclient-clientwakeupa-client-----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- &gt; Client  
 Oltre alle porte riportate nella seguente tabella, il proxy di riattivazione usa anche i messaggi di richiesta echo di Internet Control Message Protocol (ICMP) da un client all'altro quando questi sono configurati per il proxy di riattivazione. Questo tipo di comunicazione viene usata per verificare se l'altro computer è attivo nella rete. ICMP viene talvolta indicato come comandi ping TCP/IP. ICMP non dispone di un numero di protocollo UDP o TCP e pertanto non è elencato nella seguente tabella. Tuttavia, qualsiasi firewall basato su host presente nei computer client o negli altri dispositivi di rete all'interno del sottoinsieme deve consentire il traffico ICMP affinché la comunicazione del proxy di riattivazione venga eseguita correttamente.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Riattivazione LAN|9 (vedere la nota 2, **Porta alternativa disponibile**)|--|  
|Proxy di riattivazione|25536 (vedere la nota 2, **Porta alternativa disponibile**)|--|  

###  <a name="a-namebkmkportsclient-policymodulea-client-----configuration-manager-policy-module-network-device-enrollment-service"></a><a name="BKMK_PortsClient-PolicyModule"></a> Client -- &gt; Modulo criteri di Configuration Manager (servizio Registrazione dispositivi di rete)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)||80|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-clouddpa-client-----cloud-based-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a> Client -- &gt; Punto di distribuzione basato su cloud  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsclient-dpa-client-----distribution-point"></a><a name="BKMK_PortsClient-DP"></a> Client -- &gt; Punto di distribuzione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsclient-dp2a-client-----distribution-point-configured-for-multicast"></a><a name="BKMK_PortsClient-DP2"></a> Client -- &gt; Punto di distribuzione configurato per multicast  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Protocollo multicast|63000-64000|--|  

###  <a name="a-namebkmkportsclient-dp3a-client-----distribution-point-configured-for-pxe"></a><a name="BKMK_PortsClient-DP3"></a> Client -- &gt; Punto di distribuzione configurato per PXE  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Dynamic Host Configuration Protocol (DHCP)|67 e 68|--|  
|Trivial File Transfer Protocol (TFTP)|69 (vedere la nota 4 **Daemon Trivial FTP (TFTP)**)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="a-namebkmkportsclient-fspa-client-----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a> Client -- &gt; Punto di stato di fallback  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsclient-gcdca-client-----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a> Client -- &gt; Controller di dominio catalogo globale  
 Un client di Configuration Manager non contatta un server di catalogo globale quando si tratta di un computer di un gruppo di lavoro o quando è configurato per la comunicazione solo con Internet.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Catalogo globale - LDAP|--|3268|  
|Catalogo globale - LDAP SSL|--|3269|  

###  <a name="a-namebkmkportsclient-mpa-client-----management-point"></a><a name="BKMK_PortsClient-MP"></a> Client -- &gt; Punto di gestione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Notifica client (comunicazione predefinita prima di eseguire il fallback su HTTP o HTTPS)|--|10123 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsclient-supa-client-----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a> Client -- &gt; Punto di aggiornamento software  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 o 8530 (vedere la nota 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 o 8531 (vedere la nota 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportsclient-smpa-client-----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a> Client -- &gt; Punto di migrazione stato  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="a-namebkmkportsconsole-clienta-configuration-manager-console-----client"></a><a name="BKMK_PortsConsole-Client"></a> Console di Configuration Manager -- &gt; Client  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Controllo remoto (controllo)|--|2701|  
|Assistenza remota (RDP e RTC)|--|3389|  

###  <a name="a-namebkmkportsconsole-interneta-configuration-manager-console-----internet"></a><a name="BKMK_PortsConsole-Internet"></a> Console di Configuration Manager -- &gt; Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="a-namebkmkportsconsole-rspa-configuration-manager-console-----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a> Console di Configuration Manager -- &gt; Punto di Reporting Services  

||||  
|-|-|-|  
|Descrizione|UDP|TCP|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsconsole-sitea-configuration-manager-console-----site-server"></a><a name="BKMK_PortsConsole-Site"></a> Console di Configuration Manager -- &gt; Server del sito  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (connessione iniziale a WMI per individuare il sistema provider)|--|135|  

###  <a name="a-namebkmkportsconsole-providera-configuration-manager-console-----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a> Console di Configuration Manager -- &gt; Provider SMS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportscertificateregistationpointpolicymodulea-configuration-manager-policy-module-network-device-enrollment-service-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Modulo criteri di Configuration Manager (servizio Registrazione dispositivi di rete) - &gt; Punto di registrazione certificati  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsdistmpa-distribution-point-----management-point"></a><a name="BKMK_PortsDist_MP"></a> Punto di distribuzione -- &gt; Punto di gestione  
 Un punto di distribuzione comunica con il punto di gestione negli scenari seguenti:  

-   Per segnalare lo stato del contenuto pre-installato  

-   Per segnalare i dati di riepilogo sull'utilizzo  

-   Per segnalare la convalida del contenuto  

-   Un punto di distribuzione pull segnala lo stato di download del pacchetto  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 2, **Porta alternativa disponibile**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsendpointprotectioninterneta-endpoint-protection-point-----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a> Punto di Endpoint Protection -- &gt; Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80|  

###  <a name="a-namebkmkportsep-to-sqla-endpoint-protection-point-----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a> Punto di Endpoint Protection -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsenrollmentproxyenrollmentpointa-enrollment-proxy-point-----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Punto proxy di registrazione -- &gt; Punto di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsenrollmentenrollmentsqla-enrollment-point-----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Punto di registrazione -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsexchangeconnectorhosteda-exchange-server-connector-----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a> Connettore Exchange Server -- &gt; Exchange Online  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Gestione remota Windows su HTTPS|--|5986|  

###  <a name="a-namebkmkportsexchangeconnectoronprema-exchange-server-connector-----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a> Connettore Exchange Server -- &gt; Exchange Server locale  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Gestione remota Windows su HTTP|--|5985|  

###  <a name="a-namebkmkportsmacenrollmentproxypointa-mac-computer-----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Computer Mac -- &gt; Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmp-dca-management-point-----domain-controller"></a><a name="BKMK_PortsMP-DC"></a> Punto di gestione -- &gt; Controller di dominio  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|LDAP (connessione SSL [Secure Sockets Layer])|636|636|  
|Catalogo globale - LDAP|--|3268|  
|Catalogo globale - LDAP SSL|--|3269|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportsmp-sitea-management-point-lt-----site-server"></a><a name="BKMK_PortsMP-Site"></a> Punto di gestione&lt; -- > Server del sito  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|--|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  
|Server Message Block (SMB)|--|445|  

###  <a name="a-namebkmkportsmp-sqla-management-point-----sql-server"></a><a name="BKMK_PortsMP-SQL"></a> Punto di gestione -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

###  <a name="a-namebkmkportsmobiledeviceclient-enrollmentproxypointa-mobile-device-----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo mobile -- &gt; Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsmobiledeviceclient-windowsintunea-mobile-device-----microsoft-intune"></a><a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Dispositivo mobile -- &gt; Microsoft Intune  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportsrsp-sqla-reporting-services-point-----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a> Punto di Reporting Services -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, Porta alternativa disponibile)|  

###  <a name="a-namebkmkportsintuneconnector-windowsintunea-service-connection-point-----microsoft-intune"></a><a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Punto di connessione del servizio -- &gt; Microsoft Intune  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|
Per altre informazioni vedere i [requisiti di accesso Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) per il punto di connessione.

###  <a name="a-namebkmkportsappcatalogwebservicepointsiteservera-site-server-lt-----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Server del sito &lt; -- > Punto dei servizi Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportsappcatalogwebsitepointsiteservera-site-server-lt-----application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Server del sito &lt; -- > Punto del sito Web del Catalogo applicazioni  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-aispa-site-server-lt-----asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a> Server del sito &lt; -- > Punto di sincronizzazione di Asset Intelligence  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-clienta-site-server-----client"></a><a name="BKMK_PortsSite-Client"></a> Server del sito -- &gt; Client  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Riattivazione LAN|9 (vedere la nota 2, **Porta alternativa disponibile**)|--|  

###  <a name="a-namebkmkportssiteserver-clouddpa-site-server-----cloud-based-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a> Server del sito -- &gt; Punto di distribuzione basato su cloud  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443|  

###  <a name="a-namebkmkportssite-dpa-site-server-----distribution-point"></a><a name="BKMK_PortsSite-DP"></a> Server del sito -- &gt; Punto di distribuzione  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-dca-site-server-----domain-controller"></a><a name="BKMK_PortsSite-DC"></a> Server del sito -- &gt; Controller di dominio  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|--|389|  
|LDAP (connessione SSL [Secure Sockets Layer])|636|636|  
|Catalogo globale - LDAP|--|3268|  
|Catalogo globale - LDAP SSL|--|3269|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportscertificateregistrationpointsiteservera-site-server-lt-----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Server del sito &lt; -- > Punto di registrazione certificati  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportsendpointprotectionsiteservera-site-server-lt-----endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a> Server del sito &lt; -- > Punto di Endpoint Protection  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkenrollmentpointsiteservera-site-server-lt-----enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a> Server del sito &lt; -- > Punto di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkenrollmentproxypointsiteservera-site-server-lt-----enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Server del sito &lt; -- > Punto proxy di registrazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-fspa-site-server-lt-----fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a> Server del sito &lt; -- > Punto di stato di fallback  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportsite-interneta-site-server-----internet"></a><a name="BKMK_PortSite-Internet"></a> Server del sito -- &gt; Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 1, **Porta server proxy**)|  

###  <a name="a-namebkmkportsissuingcasiteservera-site-server-lt-----issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a> Server del sito &lt; -- > Autorità di certificazione emittente (CA)  
 Questa comunicazione viene usata quando si distribuiscono i profili certificato usando il punto di registrazione del certificato. La comunicazione non viene usata per tutti i server del sito nella gerarchia, viene usata solo per il server del sito nel livello superiore della gerarchia.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Agente mapping endpoint RPC|135|135|  
|RPC (DCOM)|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-rspa-site-server-lt-----reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a> Server del sito &lt; -- > Punto di Reporting Services  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-sitea-site-server-lt-----site-server"></a><a name="BKMK_PortsSite-Site"></a> Server del sito &lt; -- > Server del sito  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="a-namebkmkportssite-sqla-site-server-----sql-server"></a><a name="BKMK_PortsSite-SQL"></a> Server del sito -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  

 Durante l'installazione di un sito che userà un SQL Server remoto per ospitare il database del sito, è necessario aprire le seguenti porte tra il server del sito e l'SQL Server:  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-providera-site-server-----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a> Server del sito -- &gt; Provider SMS  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  
|RPC|--|DINAMICHE (vedere la nota 6, **Porte dinamiche**)|  

###  <a name="a-namebkmkportssite-supa-site-server-lt-----software-update-point"></a><a name="BKMK_PortsSite-SUP"></a> Server del sito &lt; -- > Punto di aggiornamento software  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Hypertext Transfer Protocol (HTTP)|--|80 o 8530 (vedere la nota 3, Windows Server Update Services)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 o 8531 (vedere la nota 3, Windows Server Update Services)|  

###  <a name="a-namebkmkportssite-smpa-site-server-lt-----state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a> Server del sito &lt; -- > Punto di migrazione dello stato  
 (Vedere la nota 5, **Comunicazione tra server del sito e sistemi del sito**)  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Agente mapping endpoint RPC|135|135|  

###  <a name="a-namebkmkportsprovider-sqla-sms-provider-----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a> Provider SMS -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, Porta alternativa disponibile)|  

###  <a name="a-namebkmkportssup-interneta-software-update-point-----internet"></a><a name="BKMK_PortsSUP-Internet"></a> Punto di aggiornamento software -- &gt; Internet  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 (vedere la nota 1, **Porta server proxy**)|  

###  <a name="a-namebkmkportssup-wsusa-software-update-point-----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a> Punto di aggiornamento software -- &gt; Server WSUS upstream  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Hypertext Transfer Protocol (HTTP)|--|80 o 8530 (vedere la nota 3, **Windows Server Update Services**)|  
|Secure Hypertext Transfer Protocol (HTTPS)|--|443 o 8531 (vedere la nota 3, **Windows Server Update Services**)|  

###  <a name="a-namebkmkportssql-sqla-sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 La replica di database tra siti richiede SQL Server in un sito per comunicare direttamente con SQL Server del sito padre o del sito figlio.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Servizio SQL Server|--|1433 (vedere la nota 2, Porta alternativa disponibile)|  
|SQL Server Service Broker|--|4022 (vedere la nota 2, Porta alternativa disponibile)|  

> [!TIP]  
>  Configuration Manager non richiede SQL Server Browser, che usa la porta UDP 1434.  

###  <a name="a-namebkmkportsstatemigrationpoint-to-sqla-state-migration-point-----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Punto di migrazione stato -- &gt; SQL Server  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SQL su TCP|--|1433 (vedere la nota 2, **Porta alternativa disponibile**)|  



###  <a name="a-namebkmyportnotesa-notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Note per le porte usate dai sistemi del sito e dai client di Configuration Manager  

1.  **Porta server proxy**: questa porta non può essere configurata, ma può essere instradata attraverso un server proxy configurato.  

2.  **Porta alternativa disponibile**: è possibile definire una porta alternativa con Configuration Manager per questo valore. Se è stata definita una porta personalizzata, sostituirla durante la definizione delle informazioni sul filtro IP per i criteri IPsec o per la configurazione dei firewall.  

3.  **Windows Server Update Services**: WSUS può essere installato nel sito Web predefinito (porta 80) o in un sito Web personalizzato (porta 8530).  

     Al termine dell'installazione è possibile modificare la porta. Non è necessario usare lo stesso numero di porta per tutta la gerarchia del sito.  

    -   Se la porta HTTP è la porta 80, la porta HTTPS deve essere la porta 443.  

    -   Se la porta HTTP è diversa, la porta HTTPS deve essere maggiore di 1. Ad esempio, 8530 e 8531.  

    > [!NOTE]  
    >  Quando si configura il punto di aggiornamento software per l'uso di HTTPS, deve essere aperta anche la porta HTTP. I dati non crittografati, ad esempio il contratto di licenza per aggiornamenti specifici, usano la porta HTTP.  

4.  **Daemon Trivial FTP (TFTP)**: il servizio del sistema Daemon Trivial FTP (TFTP) non richiede un nome utente o una password ed è parte integrante di Servizi di distribuzione Windows (WDS). Il servizio Daemon Trivial FTP implementa il supporto per il protocollo TFTP definito nei seguenti RFC:  

    -   RFC 350 - TFTP  

    -   RFC 2347 - Estensione opzione  

    -   RFC 2348 - Opzione dimensione blocco  

    -   RFC 2349 - Intervallo di timeout e opzioni dimensione trasferimento  

     Trivial File Transfer Protocol è progettato per supportare ambienti di avvio privi di dischi. I daemon TFTP sono in ascolto sulla porta UDP 69 ma rispondono da una porta elevata allocata in modo dinamico. Pertanto, l'abilitazione di questa porta consente al servizio TFTP di ricevere richieste TFTP in ingresso ma non consentirà al server selezionato di rispondere. Non è possibile consentire al server selezionato di rispondere alle richieste TFTP in entrata a meno che il server TFTP non sia configurato per rispondere dalla porta 69.  

5.  **Comunicazione tra il server del sito e i sistemi del sito**: per impostazione predefinita, la comunicazione tra il server del sito e i sistemi del sito è bidirezionale. Il server del sito avvia la comunicazione per configurare il sistema del sito, quindi la maggior parte dei sistemi del sito si riconnette al server del sito per inviare le informazioni sullo stato. I punti di distribuzione e i punti di Reporting Services non inviano informazioni sullo stato. Se si seleziona **Richiedi al server del sito di avviare le connessioni al sistema del sito** nelle proprietà del sistema del sito, dopo la relativa installazione il sistema del sito non avvierà la comunicazione al server del sito. Il server del sito avvia le connessioni e usa l'account di installazione sistema del sito per l'autenticazione al server di sistema del sito.  

6.  **Porte dinamiche**: le porte dinamiche (dette anche porte temporanee) usano un intervallo di numeri di porta definito dalla versione del sistema operativo. Per informazioni sugli intervalli di porta predefiniti, vedere [Panoramica dei servizi e requisiti per le porte di rete per Windows](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="a-namebkmkadditionalportsa-additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Altri elenchi di porte  
 Nelle seguenti sezioni vengono fornite ulteriori informazioni sulle porte usate da Configuration Manager.  

###  <a name="a-namebkmkclientsharesa-client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Da client a condivisioni server  
 I client usano Server Message Block (SMB) ogni volta che si connettono alle condivisioni UNC. Ad esempio:  

-   Installazione client manuale che specifica la proprietà della riga di comando di **/source:** CCMSetup.exe.  

-   Client di Endpoint Protection che scarica i file di definizione da un percorso UNC.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

###  <a name="a-namebkmksqlportsa-connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Connessioni a Microsoft SQL Server  
 Per la comunicazione al motore di database di SQL Server e per la replica tra siti, è possibile usare la porta di SQL Server predefinita o specificare porte personalizzate:  

-   Le comunicazioni intrasito usano:  

    -   SQL Server Service Broker, che usa per impostazione predefinita la porta TCP 4022.  

    -   SQL Server Service, che usa per impostazione predefinita la porta TCP 1433.  

-   La comunicazione all'interno del sito tra il motore di database di SQL Server e i diversi ruoli di sistema del sito di Configuration Manager usa la porta TCP 1433 per impostazione predefinita.  

> [!WARNING]  
>  Configuration Manager non supporta le porte dinamiche. Poiché per impostazione predefinita le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database, quando si usa un'istanza denominata è necessario configurare manualmente la porta statica da usare per la comunicazione tra siti.  

 I ruoli del sistema del sito seguenti comunicano direttamente con il database di SQL Server:  

-   Punto per servizi Web del Catalogo applicazioni  

-   Ruolo del punto di registrazione certificati  

-   Ruolo del punto di registrazione  

-   Punto di gestione  

-   Server del sito  

-   Punto di Reporting Services  

-   provider SMS  

-   SQL Server --> SQL Server  

Se SQL Server ospita un database da più di un sito, ogni database deve usare un'istanza separata di SQL Server e ogni istanza deve essere configurata con un set univoco di porte.  

Se si dispone di un firewall abilitato nel computer SQL Server, assicurarsi che sia configurato per consentire le porte in uso dalla distribuzione e in tutti i percorsi della rete tra i computer che comunicano con SQL Server.  

Per un esempio di come configurare SQL Server per l'uso di una porta specifica, vedere [Procedura: Configurazione di un server per l'attesa su una porta TCP specifica (Gestione configurazione SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) nella libreria TechNet di SQL Server.  


### <a name="bkmk_discovery"> </a> Individuazione e pubblicazione
Le porte seguenti vengono usate per l'individuazione e la pubblicazione delle informazioni del sito:
 - Lightweight Directory Access Protocol (LDAP)  - 389
 - LDAP (connessione Secure Sockets Layer [SSL])  - 636


 - Catalogo globale LDAP - 3268
 - Catalogo globale LDAP SSL -3269


 - Mapper di Endpoint RPC - 135
 - RPC - porte TCP elevate allocate dinamicamente


 - TCP: 1024 - 5000
 - TCP:  49152 - 65535


###  <a name="a-namebkmkexternala-external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Connessioni esterne stabilite da Configuration Manager  
 I sistemi del sito o i client di Configuration Manager possono eseguire le connessioni esterne seguenti:  

-   [Punto di sincronizzazione di Asset Intelligence -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Punto di Endpoint Protection -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client -- &gt; Controller di dominio catalogo globale](#BKMK_PortsClient-GCDC)  

-   [Console di Configuration Manager -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Punto di gestione -- &gt; Controller di dominio](#BKMK_PortsMP-DC)  

-   [Server del sito -- &gt; Controller di dominio](#BKMK_PortsSite-DC)  

-   [Server del sito &lt; -- &gt; Autorità di certificazione emittente (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Punto di aggiornamento software -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Punto di aggiornamento software -- &gt;Server upstream di WSUS](#BKMK_PortsSUP-WSUS)  

-   [Punto di connessione del servizio -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="a-namebkmkibcmportsa-installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a> Requisiti di installazione per sistemi del sito che supportano client basati su Internet  
 I punti di gestione e di distribuzione che supportano i client basati su Internet, il punto di aggiornamento software e il punto di stato fallback usano le seguenti porte per l'installazione e il ripristino:  

-   Server del sito --> sistema del sito: mapper di endpoint RPC con la porta 135 TCP e UDP.  

-   Server del sito --> sistema del sito: porte TCP dinamiche RPC.  

-   Server del sito &lt; --> sistema del sito: Server Message Block (SMB) tramite la porta TCP 445.  

Le installazioni di applicazioni e pacchetti nei punti di distribuzione richiedono le seguenti porte RPC:  

-   Server del sito --> punto di distribuzione: mapper di endpoint RPC con la porta 135 TCP e UDP.  

-   Server del sito --> punto di distribuzione: porte TCP dinamiche RPC  

Usare IPsec per proteggere il traffico tra il server del sito e i sistemi del sito. Se è necessario limitare le porte dinamiche usate con RPC, è possibile usare lo strumento di configurazione RPC di Microsoft (rpccfg.exe) per configurare un intervallo limitato di porte per tali pacchetti RPC. Per altre informazioni sullo strumento di configurazione RPC, vedere [Come configurare RPC per l'utilizzo di determinate porte e come proteggere tali porte tramite IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Prima di installare questi sistemi del sito, assicurarsi che il servizio Registro di sistema remoto sia in esecuzione nel server di sistema del sito e di aver specificato un account di installazione sistema del sito se il sistema del sito si trova in una foresta Active Directory diversa senza una relazione di trust.  

###  <a name="a-namebkmkportsclientinstalla-ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Porte usate dall'installazione client di Configuration Manager  
Le porte usate durante l'installazione del client dipendono dal metodo di distribuzione client. Vedere **Porte usate durante la distribuzione client di Configuration Manager** nell'argomento [Impostazioni di Windows Firewall e della porta per i computer client in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) per un elenco di porte per ogni metodo di distribuzione client. Per informazioni su come configurare Windows Firewall nel client per la comunicazione durante e dopo l'installazione del client, vedere [Impostazioni di Windows Firewall e della porta per i client in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="a-namebkmkmigrationportsa-ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Porte usate dalla migrazione  
Il server del sito che esegue la migrazione usa diverse porte per connettersi ai siti applicabili nella gerarchia di origine per raccogliere i dati dal database di SQL Server dei siti di origine e per condividere i punti di distribuzione condivisi.  

 Per informazioni su queste porte, vedere la sezione [Configurazioni necessarie per la migrazione](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) nell'argomento [Prerequisiti per la migrazione in System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md).  

###  <a name="a-namebkmkserverportsa-ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Porte usate da Windows Server  
 Nella tabella seguente vengono elencate alcune porte chiave che usa Windows Server e le rispettive funzioni. Per un elenco completo dei requisiti delle porte di rete e dei servizi di Windows Server, vedere [Panoramica dei servizi e requisiti per le porte di rete per il sistema server Windows](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Domain Name System (DNS)|53|53|  
|Dynamic Host Configuration Protocol (DHCP)|67 e 68|--|  
|Risoluzione nomi NetBIOS|137|--|  
|Servizio datagrammi NetBIOS|138|--|  
|Servizio di sessione NetBIOS|--|139|  



<!--HONumber=Dec16_HO3-->


