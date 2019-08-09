---
title: Come abilitare TLS 1.2
titleSuffix: Configuration Manager
description: Informazioni su come abilitare TLS 1.2 per Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b58f6d1441d338c121b67754989128944adcc923
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536565"
---
# <a name="how-to-enable-tls-12"></a>Come abilitare TLS 1.2

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive come abilitare TLS 1.2 per Configuration Manager e per i singoli componenti. In questo articolo sono descritti anche i requisiti di aggiornamento per le funzionalità usate comunemente e la risoluzione di alcuni problemi comuni.

Configuration Manager si basa su molti componenti diversi per proteggere le comunicazioni. Il protocollo usato per una determinata connessione dipende dalle funzionalità di tutti i componenti necessari. Se un componente non è aggiornato, la comunicazione potrebbe usare un protocollo meno recente e quindi meno sicuro.

Per la corretta abilitazione di Configuration Manager per supportare TLS 1.2, abilitare TLS 1.2 per tutti i componenti necessari. I componenti necessari variano a seconda dell'ambiente e dalle funzionalità di Configuration Manager in uso.

Avviare il processo con i client, in particolare con le versioni precedenti di Windows. Prima di abilitare TLS 1.2 nei server di Configuration Manager, assicurarsi che tutti i client supportino TLS 1.2. In caso contrario, i client non riusciranno a comunicare con i server e potranno restare orfani.


## <a name="tasks-for-features-and-scenarios"></a>Attività per funzionalità e scenari

Per abilitare TLS 1.2 per i componenti da cui Configuration Manager dipende per proteggere le comunicazioni, è necessario:

- [Abilitare il protocollo TLS 1.2 come provider di sicurezza](#enable-tls-12-protocol-as-a-security-provider)
- [Aggiornare .NET Framework per supportare TLS 1.2](#update-net-framework-to-support-tls-12)
- [Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components)
- [Aggiornare Windows e WinHTTP in Windows 8.0, Windows Server 2012 R2 e versioni precedenti](#update-windows-and-winhttp)
- [Aggiornare Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

Questa sezione descrive le dipendenze per funzionalità e scenari specifici di Configuration Manager. Per determinare i passaggi successivi, individuare gli elementi che si applicano all'ambiente.

|Scenario o funzionalità|Attività di aggiornamento|
|--- |--- |
|Server del sito (centrale, primario o secondario)| - [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verificare le impostazioni della crittografia complessa|
|Server di database del sito|[Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components)|
|Server del sito secondario|[Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components) a una versione conforme di SQL Express|
|Ruoli del sistema del sito| - [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa <br/> - [Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components) per i ruoli che lo richiedono, incluso [SQL Server Native Client](#sql-server-native-client)|
|Punto di Reporting Services|- [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) nel server del sito, nei server di SQL Reporting Services e nei computer con la console<br/> - Riavviare il servizio SMS_Executive in base alle esigenze|
|Punto di aggiornamento software|[Aggiornare WSUS](#update-windows-server-update-services-wsus)|
|Gateway di gestione cloud|[Applicare TLS 1.2](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway#bkmk_tls)|
|Console di Configuration Manager| - [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verificare le impostazioni della crittografia complessa|
|Client Configuration Manager con ruoli del sistema del sito HTTPS|[Aggiornare Windows per supportare TLS 1.2 per le comunicazioni client-server usando WinHTTP](#update-windows-and-winhttp)|
|Software Center| - [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Verificare le impostazioni della crittografia complessa|
|Client Windows 7| *Prima* di abilitare TLS 1.2 nei componenti server, [aggiornare Windows per supportare TLS 1.2 per le comunicazioni client-server usando WinHTTP](#update-windows-and-winhttp). Se prima si abilita TLS 1.2 nei componenti server, è possibile rendere orfane le versioni precedenti dei client.|


## <a name="enable-tls-12-protocol-as-a-security-provider"></a>Abilitare il protocollo TLS 1.2 come provider di sicurezza

Verificare l'impostazione della sottochiave del Registro di sistema `\SecurityProviders\SCHANNEL\Protocols`, come illustrato in [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

> [!NOTE]
> TLS 1.2 è abilitato per impostazione predefinita, quindi non è necessario apportare modifiche a queste chiavi per abilitarlo. È possibile apportare modifiche in Protocols per disabilitare TLS 1.0 e TLS 1.1 dopo aver eseguito il resto delle indicazioni fornite in questo articolo e aver verificato che l'ambiente funzioni solo con TLS 1.2 abilitato.


## <a name="update-net-framework-to-support-tls-12"></a>Aggiornare .NET Framework per supportare TLS 1.2

### <a name="determine-net-version"></a>Determinare la versione di .NET

In primo luogo, determinare il numero di versione di .NET. Per altre informazioni, vedere [Come determinare quali versioni e livelli di Service Pack di Microsoft.NET Framework sono installati](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Installare gli aggiornamenti di .NET

Alcune versioni di .NET Framework potrebbero richiedere aggiornamenti per abilitare la crittografia complessa. Usare queste linee guida:

- NET Framework 4.6.2 e versioni successive supportano TLS 1.1 e TLS 1.2. Confermare le impostazioni del Registro di sistema, ma non sono richieste modifiche aggiuntive.

- Aggiornare NET Framework 4.6 e versioni precedenti per supportare TLS 1.1 e TLS 1.2. Per altre informazioni, vedere [Versioni e dipendenze di .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Se si usa .NET Framework 4.5.1 o 4.5.2 in Windows 8.1 o Windows Server 2012, gli aggiornamenti pertinenti e i dettagli sono disponibili anche nell'[Area download](https://www.microsoft.com/download/details.aspx?id=42883).

### <a name="configure-for-strong-cryptography"></a>Configurare la crittografia complessa

Configurare .NET Framework per supportare la crittografia complessa. Configurare l'impostazione del Registro di sistema `SchUseStrongCrypto` su `DWORD:00000001`, che disabilita la crittografia a flusso RC4 e richiede un riavvio. Per altre informazioni su questa impostazione, vedere [Avviso di sicurezza Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Assicurarsi di impostare le chiavi del Registro di sistema seguenti in qualsiasi computer che comunica attraverso la rete con un sistema abilitato per TLS 1.2, ad esempio i client Configuration Manager o qualsiasi ruolo del sistema del sito remoto non installato nel server del sito.

Per le applicazioni a 32 bit in esecuzione su sistemi a 32 bit o per le applicazioni a 64 bit in esecuzione su sistemi a 64 bit, aggiornare il valore della sottochiave seguente:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Per le applicazioni a 32 bit in esecuzione su sistemi a 64 bit, aggiornare il valore della sottochiave seguente:

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> L'impostazione `SchUseStrongCrypto` consente a .NET di usare TLS 1.1 e TLS 1.2. L'impostazione `SystemDefaultTlsVersions` consente a .NET di usare la configurazione del sistema operativo. Per altre informazioni, vedere [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).


## <a name="update-sql-server-and-client-components"></a>Aggiornare SQL Server e i componenti client

Microsoft SQL Server 2016 e versioni successive supportano TLS 1.1 e TLS 1.2. Le versioni precedenti e le librerie dipendenti potrebbero richiedere aggiornamenti. Per altre informazioni, vedere [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Per i server del sito secondario è necessario usare almeno SQL Server 2016 Express con Service Pack 2 (13.2.50.26) o versione successiva.

### <a name="sql-server-native-client"></a>SQL Server Native Client

> [!NOTE]
> L'[articolo KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) descrive anche i requisiti per i componenti client di SQL Server.

Assicurarsi di aggiornare anche SQL Server Native Client almeno alla versione SQL 2012 SP4 (11.*.7001.0). A partire dalla versione 1810, questo requisito fa parte dei [controlli dei prerequisiti (avviso)](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client).

Configuration Manager usa SQL Server Native Client nei seguenti ruoli del sistema del sito:

- Server di database del sito
- Server del sito: sito di amministrazione centrale, sito primario o sito secondario
- Punto di gestione
- Punto di gestione dei dispositivi
- Punto di migrazione stato
- provider SMS
- Punto di aggiornamento software
- Punto di distribuzione abilitato per multicast
- Punto di servizio aggiornamento AI
- Punto di Reporting Services
- Servizio Web del Catalogo applicazioni
- Punto di registrazione
- Punto di Endpoint Protection
- punto di connessione del servizio
- Punto di registrazione certificati
- Punto di servizio del data warehouse


## <a name="update-windows-and-winhttp"></a>Aggiornare Windows e WinHTTP

Windows 8.1, Windows 2012 R2, Windows 10, Windows Server 2016 e le versioni successive di Windows supportano in modo nativo TLS 1.2 per le comunicazioni client-server tramite WinHTTP.

Le versioni precedenti di Windows, ad esempio Windows 7 o Windows Server 2012, non abilitano TLS 1.1 o 1.2 per impostazione predefinita per le comunicazioni client-server tramite HTTPS. Per queste versioni precedenti di Windows, installare l'[aggiornamento 3140245](https://support.microsoft.com/help/3140245) per abilitare TLS 1.1 e TLS 1.2 come protocolli sicuri predefiniti per WinHTTP in Windows. Impostare quindi i valori del Registro di sistema seguenti:

> [!IMPORTANT]
> Abilitare queste impostazioni in tutti i client *prima* di abilitare TLS 1.2 nei server di Configuration Manager. In caso contrario, è possibile renderli inavvertitamente orfani.

Verificare il valore dell'impostazione del Registro di sistema `DefaultSecureProtocols`, ad esempio:

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Se si modifica questo valore, riavviare il computer.

> [!Note]  
> L'esempio precedente illustra il valore di `0xAA0` per l'impostazione `DefaultSecureProtocols` di WinHTTP. L'articolo [KB 3140245: Eseguire l'aggiornamento per abilitare TLS 1.1 e 1.2 TLS come protocolli sicuri predefiniti in WinHTTP in Windows](https://support.microsoft.com/help/3140245) elenca il valore esadecimale per ogni protocollo. Per impostazione predefinita in Windows, questo valore è `0x0A0` per abilitare SSL 3.0 e TLS 1.0 per WinHTTP. L'esempio precedente mantiene queste impostazioni predefinite e abilita anche TLS 1.1 e TLS 1.2 per WinHTTP. Questa configurazione assicura che la modifica non interrompa altre applicazioni che potrebbe essere ancora basate su SSL 3.0 o TLS 1.0. È possibile usare il valore di `0xA00` per abilitare solo TLS 1.1 e TLS 1.2. Configuration Manager supporta il protocollo più sicuro negoziato da Windows tra entrambi i dispositivi.
>
> Per disabilitare completamente SSL 3.0 e TLS 1.0, usare l'impostazione dei protocolli disabilitati da SChannel in Windows. Per altre informazioni, vedere [Come limitare l'uso di determinati algoritmi di crittografia e protocolli in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).


## <a name="update-windows-server-update-services-wsus"></a>Aggiornare Windows Server Update Services (WSUS)

Per supportare TLS 1.2 per le comunicazioni client-server in WSUS in Windows Server 2012 e Windows Server 2012 R2, installare l'aggiornamento seguente nel server WSUS:

- Per il server WSUS che esegue Windows Server 2012, installare l'[aggiornamento 4022721](https://support.microsoft.com/help/4022721) o uno successivo.
- Per il server WSUS che esegue Windows Server 2012 R2, installare l'[aggiornamento 4022720](https://support.microsoft.com/help/4022720) o uno successivo.


## <a name="known-issues"></a>Problemi noti

Questa sezione fornisce suggerimenti per i problemi comuni che si verificano quando si abilita il supporto di TLS 1.2.

### <a name="unsupported-platforms"></a>Piattaforme non supportate

Le piattaforme client seguenti sono supportate da Configuration Manager, ma non sono supportate in un ambiente TLS 1.2:

- Windows Server 2008
- Windows CE
- Apple OS X
- Dispositivi Windows 10 gestiti con MDM locale

### <a name="reports-dont-show-in-the-console"></a>I report non vengono visualizzati nella console

Se i report non vengono visualizzati nella console di Configuration Manager, assicurarsi di aggiornare il computer in cui si esegue la console. È necessario [aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa.

### <a name="fips-security-policy-enabled"></a>Criteri di sicurezza FIPS abilitati

Se si abilita l'impostazione dei criteri di sicurezza FIPS per il client o un server, la negoziazione di Secure Channel (Schannel) può comportare l'uso di TLS 1.0. Questo comportamento si verifica anche se si disabilita il protocollo nel Registro di sistema.

Per analizzare il problema, abilitare la registrazione eventi del canale sicuro e quindi esaminare gli eventi Schannel nel registro di sistema. Per altre informazioni, vedere [Come limitare l'uso di determinati algoritmi di crittografia e protocolli in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Errore di comunicazione di SQL Server

Se la comunicazione di SQL Server non riesce e restituisce un errore **SslSecurityError**, verificare le impostazioni seguenti:

- [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in ogni computer
- [Aggiornare SQL Server](#update-sql-server-and-client-components) nel server host
- [Aggiornare i componenti client di SQL](#update-sql-server-and-client-components) in tutti i sistemi che comunicano con SQL, ad esempio i server del sito, il provider SMS e i server del ruolo del sito.

### <a name="configuration-manager-client-communication-failures"></a>Errori di comunicazione del client Configuration Manager

Se il client Configuration Manager non comunica con i ruoli del sito, verificare di aver [aggiornato Windows](#update-windows-and-winhttp) per supportare TLS 1.2 per la comunicazione client-server usando WinHTTP. I ruoli del sito comuni includono i punti di distribuzione, i punti di gestione e i punti di migrazione stato.

### <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Il punto di Reporting Services ha esito negativo e restituisce un errore previsto

Se il punto di Reporting Services non configura i report, cercare il messaggio di errore seguente in **SRSRP.log**:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Per risolvere questo problema, seguire questa procedura:

1. [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in tutti i computer pertinenti.

1. Dopo aver installato eventuali aggiornamenti, riavviare il servizio SMS_Executive.

### <a name="application-catalog-doesnt-initialize"></a>Il Catalogo applicazioni non viene inizializzato

> [!Important]  
> Il catalogo applicazioni è deprecato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Se il Catalogo applicazioni non viene inizializzato, cercare il messaggio di errore seguente nel file **ServicePortalWebSite.svclog**:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Per risolvere questo problema, seguire questa procedura:

1. [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in tutti i computer pertinenti.

1. Nella cartella `%WinDir%\System32\InetSrv` del server del Catalogo applicazioni creare un file **W2SP.exe.config** con il contenuto seguente:

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Questo è il file predefinito che viene creato se l'applicazione viene compilata usando .NET Framework 4.6.3.

1. Usare la sicurezza del trasporto HTTPS per i ruoli del Catalogo applicazioni.

    > [!Important]
    > Quando si usa la sicurezza del messaggio HTTP per i ruoli del Catalogo applicazioni, WCF è hardcoded in modo che sia possibile usare solo SSL 3.0 e TLS 1.0. Ciò impedisce l'uso di TLS 1.2.

1. Se sono state apportate modifiche, riavviare il computer.

### <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Software Center o il browser non comunica con il Catalogo applicazioni

> [!Important]  
> Il catalogo applicazioni è deprecato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Il metodo migliore per usare Software Center con le app disponibili per gli utenti in un sito abilitato per TLS 1.2 consiste nel rimuovere il ruolo del Catalogo applicazioni. Consentire quindi a Software Center di comunicare direttamente con un punto di gestione. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

Se è necessario risolvere gli errori di comunicazione tra il Catalogo applicazioni e Software Center, verificare le condizioni seguenti:

- [Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in ogni computer.

- Dopo aver apportato le modifiche, riavviare tutti i computer interessati.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### <a name="service-connection-point-upload-failures"></a>Errori di caricamento del punto di connessione del servizio

Se il punto di connessione del servizio non carica i dati in SCCMConnectedService, [aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in ogni computer. Ricordare di riavviare i computer dopo aver apportato le modifiche.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La console di Configuration Manager visualizza la finestra di dialogo di onboarding di Intune

Se la finestra di dialogo di onboarding di Intune viene visualizzata quando la console prova a connettersi al portale di Intune, [aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa in ogni computer. Ricordare di riavviare i computer dopo aver apportato le modifiche.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La console di Configuration Manager visualizza un errore di accesso ad Azure

Quando si prova a creare applicazioni di Azure AD (Azure AD), se la finestra di dialogo di onboarding dei servizi di Azure ha esito negativo subito dopo aver selezionato **Accedi**, [aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e abilitare la crittografia complessa. Ricordare di riavviare i computer dopo aver apportato le modifiche.

### <a name="configuration-manager-cloud-services-and-tls-12"></a>Servizi cloud di Configuration Manager e TLS 1.2

A partire dalla versione 1802, le macchine virtuali di Azure usate dal gateway di gestione cloud e dai punti di distribuzione cloud supportano TLS 1.2. I client supportati nella versione 1802 o successiva usano automaticamente TLS 1.2.

**SMSAdminui.log** può contenere un errore simile all'esempio seguente:

```
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

Nel registro eventi del sistema potrebbe essere registrato l'ID evento 36874 di SChannel con la descrizione seguente: `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->


## <a name="see-also"></a>Vedere anche

- [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)

- [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

- [Riferimento tecnico per i controlli crittografici](cryptographic-controls-technical-reference.md)
