---
title: Come abilitare TLS 1.2
titleSuffix: Configuration Manager
description: Informazioni su come abilitare TLS 1.2 per Microsoft Configuration Manager.
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3641c3a9adce23f24a80135d996da03e12e78907
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355608"
---
# <a name="how-to-enable-tls-12-for-configuration-manager"></a>Come abilitare TLS 1.2 per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive come abilitare TLS 1.2 per Configuration Manager e per i singoli componenti. In questo articolo sono descritti anche i requisiti di aggiornamento per le funzionalità usate comunemente e la risoluzione di alcuni problemi comuni.

Configuration Manager si basa su molti componenti diversi per proteggere le comunicazioni. Il protocollo usato per una determinata connessione dipende dalle funzionalità di tutti i componenti necessari. Se un componente non è aggiornato, la comunicazione potrebbe usare un protocollo meno recente e quindi meno sicuro.

Per la corretta abilitazione di Configuration Manager per supportare TLS 1.2, è necessario abilitare TLS 1.2 per tutti i componenti necessari. I componenti necessari dipendono dall'ambiente e dalle funzionalità di Configuration Manager in uso.


## <a name="to-enable-tls-12"></a>Per abilitare TLS 1.2

Per abilitare TLS 1.2, è prima di tutto necessario abilitare TLS 1.2 come provider di sicurezza per ogni computer che esegue o interagisce con Configuration Manager. Abilitare quindi TLS 1.2 per i componenti da cui Configuration Manager dipende per proteggere le comunicazioni.

### <a name="enable-the-tls-12-protocol-as-a-security-provider"></a>Abilitare il protocollo TLS 1.2 come provider di sicurezza

Verificare l'impostazione della sottochiave del Registro di sistema "\SecurityProviders\SCHANNEL\Protocols", come illustrato in [Procedure consigliate per Transport Layer Security (TLS) con .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?).

> [!NOTE]
> TLS 1.2 è abilitato per impostazione predefinita, quindi non è necessario apportare modifiche a queste chiavi per abilitarlo. È possibile apportare modifiche in Protocols per disabilitare TLS 1.0 e TLS 1.1 dopo aver eseguito il resto delle indicazioni fornite in questo articolo e aver verificato che l'ambiente funzioni solo con TLS 1.2 abilitato.

### <a name="enable-tls-12-for-dependent-components"></a>Abilitare TLS 1.2 per i componenti dipendenti
Per abilitare TLS 1.2 per i componenti dipendenti da cui Configuration Manager dipende per proteggere le comunicazioni, è necessario:

- [Aggiornare .NET Framework per supportare TLS 1.2](#update-net-framework-to-support-tls-12)
- [Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components)
- [Aggiornare Windows e WinHTTP in Windows 8.0, Windows Server 2012 R2 e versioni precedenti](#update-windows-and-winhttp)
- [Aggiornare Windows Server Update Services (WSUS)](#update-windows-server-update-services)

#### <a name="update-net-framework-to-support-tls-12"></a>Aggiornare .NET Framework per supportare TLS 1.2
Per aggiornare .NET Framework per supportare TLS 1.2, determinare prima il numero di versione di .NET. Per informazioni, vedere [Come determinare quali versioni e livelli di service pack di Microsoft.NET Framework sono installati](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

Le versioni precedenti di .NET Framework potrebbero richiedere aggiornamenti o modifiche al Registro di sistema per abilitare la crittografia complessa. Usare queste linee guida:

- NET Framework 4.6.2 supporta TLS 1.1 e TLS 1.2.  Non occorre alcuna modifica aggiuntiva.
- NET Framework 4.6 e versioni precedenti [devono essere aggiornati](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) per supportare TLS 1.1 e TLS 1.2.

Se si usa .NET Framework 4.5.1 o 4.5.2 in Windows 8.1, Windows RT 8.1 o Windows Server 2012, gli aggiornamenti pertinenti e i dettagli sono disponibili anche nell'[Area download](https://www.microsoft.com/download/details.aspx?id=42883).
-  .NET Framework deve essere configurato per supportare la crittografia complessa. Configurare l'impostazione del Registro di sistema `SchUseStrongCrypto` su `DWORD:00000001`, che disabilita la crittografia a flusso RC4 e richiede un riavvio. Per altre informazioni su questa impostazione, vedere [Microsoft Security Advisory 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358) (Avviso di sicurezza Microsoft 296038).

Per le applicazioni a 32 bit in esecuzione su sistemi a 32 bit o per le applicazioni a 64 bit in esecuzione su sistemi a 64 bit, aggiornare il valore della sottochiave seguente:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
Per le applicazioni a 32 bit in esecuzione su sistemi a 64 bit, aggiornare il valore della sottochiave seguente:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### <a name="update-sql-server-and-client-components"></a>Aggiornare SQL Server e i componenti client

Microsoft SQL Server 2016 supporta TLS 1.1 e TLS 1.2.
Le versioni precedenti e le librerie dipendenti potrebbero richiedere aggiornamenti. Per altre informazioni, vedere [KB 3135244: Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> L'articolo KB 3135244 descrive anche i requisiti per i componenti client di SQL Server. Aggiornare ogni componente usato nell'ambiente.

#### <a name="update-windows-and-winhttp"></a>Aggiornare Windows e WinHTTP

Windows 10, Windows 8.1, Windows Server 2016 e Windows Server 2012 R2 supportano TLS 1.2 per le comunicazioni client-server tramite WinHTTP per impostazione predefinita.

Windows 8.0, Windows Server 2012 e le versioni precedenti di Windows non abilitano TLS 1.1 o 1.2 per impostazione predefinita per le comunicazioni client-server tramite HTTPS. Per queste versioni precedenti di Windows, è consigliabile installare l'[aggiornamento 3140245](https://support.microsoft.com/help/3140245) per abilitare TLS 1.1 e TLS 1.2 come protocolli sicuri predefiniti in WinHTTP in Windows e impostare i valori del Registro di sistema seguenti.

> [!IMPORTANT]
> Questa operazione deve essere eseguita in tutti i client di livello inferiore **prima** di abilitare TLS 1.2 per evitare di isolarli inavvertitamente.

Verificare che l'impostazione del Registro di sistema `DefaultSecureProtocols` sia `0xAA0`, come segue:

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> Questa modifica richiede un riavvio.

#### <a name="update-windows-server-update-services"></a>Aggiornare Windows Server Update Services

Per supportare TLS 1.2 per le comunicazioni client-server in WSUS in Windows Server 2012 e Windows Server 2012 R2, è necessario applicare l'aggiornamento seguente nel server WSUS:
- Per il server WSUS che esegue Windows Server 2012, applicare l'[aggiornamento 4022721](https://support.microsoft.com/help/4022721) o uno successivo.
- Per il server WSUS che esegue Windows Server 2012 R2, applicare l'[aggiornamento 4022720](https://support.microsoft.com/help/4022720) o uno successivo.

## <a name="tasks-required-for-configuration-manager-features-and-scenarios"></a>Attività necessarie per le funzionalità e gli scenari di Configuration Manager
Questa sezione descrive le dipendenze per funzionalità e scenari specifici di Configuration Manager. Per determinare i passaggi successivi, individuare gli elementi che si applicano all'ambiente e quindi verificare le dipendenze eseguendo i passaggi elencati in precedenza in [Abilitare TLS 1.2 per i componenti dipendenti](#enable-tls-12-for-dependent-components).

|Scenario o funzionalità|Attività di aggiornamento|
|--- |--- |
|Server del sito (centrale, primario o secondario)|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa.|
|provider SMS|[Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components) in modo appropriato per ogni provider SMS.|
|Ruoli del sistema del sito|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa. [Aggiornare SQL Server e i componenti client](#update-sql-server-and-client-components).|
|Catalogo applicazioni del punto di connessione del servizio|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa.|
|Punto di reporting SRS|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) nel server del sito e nei server SRS. Riavviare il servizio SMS_Executive in base alle esigenze.|
|Console di Configuration Manager|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa.|
|Client SCCM con ruoli del sistema del sito HTTPS|[Aggiornare Windows per supportare TLS 1.2 per le comunicazioni client-server usando WinHTTP](#update-windows-and-winhttp).|
|Software Center|[Aggiornare .NET Framework](#update-net-framework-to-support-tls-12) e verificare le impostazioni della crittografia complessa.|
|Punto di aggiornamento software|[Aggiornare WSUS](#update-windows-server-update-services).|
|Punti di gestione|Eseguire l'aggiornamento al client nativo di SQL Server più recente per consentire a Configuration Manager di comunicare con i componenti più recenti di SQL Server abilitati per TLS 1.2. Vedere la tabella "Download di componenti client" in [Supporto di TLS 1.2 per Microsoft SQL Server](https://support.microsoft.com/help/3135244).|

## <a name="known-issues"></a>Problemi noti

Questa sezione fornisce suggerimenti per i problemi comuni che si verificano quando si abilita il supporto di TLS 1.2.

### <a name="fips-security-policy-enabled"></a>Criteri di sicurezza FIPS abilitati

Se l'impostazione dei criteri di sicurezza FIPS è abilitata per il client o un server, la negoziazione tramite canale sicuro (Schannel) può causare l'uso di TLS 1.0 anche se il protocollo viene disabilitato usando il Registro di sistema.

Per analizzare il problema, abilitare la registrazione eventi del canale sicuro e quindi esaminare gli eventi Schannel nel registro di sistema. Per informazioni correlate, vedere [Come limitare l'uso di determinati algoritmi di crittografia e protocolli in Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Errore di comunicazione di SQL Server

Se la comunicazione di SQL Server non riesce e restituisce un errore **SslSecurityError**, verificare quanto segue:
- .NET Framework è aggiornato e ha la crittografia complessa abilitata in ogni computer.
- SQL Server è aggiornato nel server host.
- I componenti client di SQL sono aggiornati nei server del sito, nel provider SMS, nei server del ruolo del sito e in tutti gli altri sistemi che comunicano con SQL server.

### <a name="configuration-manager-client-communication-failures"></a>Errori di comunicazione del client Configuration Manager

Se il client Configuration Manager non comunica con gli endpoint dei ruoli del sito, ad esempio i punti di distribuzione, i punti di gestione e i punti di migrazione stato, verificare che Windows sia stato aggiornato per supportare TLS 1.2 per la comunicazione client-server con WinHTTP.

### <a name="srs-reporting-point-fails-and-returns-an-expected-error"></a>Il punto di reporting SRS ha esito negativo e restituisce un errore previsto

Se il punto di reporting SRS non configura i report, cercare il messaggio di errore seguente in *SRSRP.log*:

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Per risolvere questo problema, seguire questa procedura:

1. Verificare che .NET Framework sia aggiornato e abbia la crittografia complessa abilitata in tutti i computer pertinenti.
1. Verificare che il servizio SMS_Executive sia stato riavviato dopo l'installazione di ogni aggiornamento.

### <a name="application-catalog-doesnt-initialize"></a>Il Catalogo applicazioni non viene inizializzato

Se il Catalogo applicazioni non viene inizializzato, cercare il messaggio di errore seguente nel file *ServicePortalWebSite.svclog*:

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Per risolvere questo problema, seguire questa procedura:
1. Verificare che .NET Framework sia aggiornato e abbia la crittografia complessa abilitata in tutti i computer pertinenti.
1. Nella cartella C:\Windows\System32\InetSrv del server del Catalogo applicazioni creare un file *W2SP.exe.config* eseguendo lo script seguente: 

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <configuration>
     <runtime>
     <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
     </runtime>
   </configuration>
   ```
   > [!NOTE]
   > Questo è il file predefinito che verrà creato se l'applicazione viene compilata usando .NET Framework 4.6.3.
1. Usare la sicurezza del trasporto HTTPS per i ruoli del Catalogo applicazioni.

   > [!NOTE]
   > Quando si usa la sicurezza del messaggio HTTP per i ruoli del Catalogo applicazioni, WCF è hardcoded in modo che sia possibile usare solo SSL 3.0 e TLS 1.0. Ciò impedisce l'uso di TLS 1.2.
1. Se sono state apportate modifiche, riavviare il computer.


### <a name="software-center-or-browser-doesnt-communicate-with-application-catalog"></a>Software Center o il browser non comunica con il Catalogo applicazioni

Per risolvere gli errori di comunicazione tra il Catalogo applicazioni e Software Center o il browser, verificare le condizioni seguenti:

- .NET Framework è aggiornato e ha la crittografia complessa abilitata in ogni computer.
- Il browser è configurato per supportare TLS 1. Prima di Windows 10, questa opzione era disabilitata per impostazione predefinita.
- Tutti i computer sono stati riavviati dopo che sono state apportate le modifiche.

   > [!NOTE]
   > Per fare in modo che Software Center usi il server imposto da TLS 1.2 per le app disponibili per gli utenti, è consigliabile rimuovere i ruoli del Catalogo app e consentire a Software Center di comunicare con il punto di gestione. Per altre informazioni, vedere [Rimuovere il catalogo applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

### <a name="service-connection-point-upload-failures"></a>Errori di caricamento del punto di connessione del servizio

Se il punto di connessione del servizio non carica i dati in SCCMConnectedService, verificare che .NET Framework sia aggiornato e abbia la crittografia complessa abilitata in ogni computer. Ricordare di riavviare i computer dopo aver apportato le modifiche.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La console di Configuration Manager visualizza la finestra di dialogo di onboarding di Intune

Se la finestra di dialogo di onboarding di Intune viene visualizzata quando la console prova a connettersi al portale di Intune, verificare che .NET Framework sia aggiornato e abbia la crittografia complessa abilitata in ogni computer.  Ricordare di riavviare i computer dopo aver apportato le modifiche.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La console di Configuration Manager visualizza un errore di accesso ad Azure

Se la finestra di dialogo di onboarding dei servizi di Azure ha esito negativo subito dopo aver selezionato **Accedi** quando si prova a creare applicazioni di Azure AD, verificare che .NET Framework sia aggiornato e che la crittografia complessa sia abilitata. È necessario eseguire il riavvio per rendere effettive le modifiche.

## <a name="see-also"></a>Vedere anche

[Riferimento tecnico per i controlli crittografici](cryptographic-controls-technical-reference.md)
