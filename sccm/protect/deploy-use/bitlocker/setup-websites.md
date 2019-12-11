---
title: Configurare i portali di BitLocker
titleSuffix: Configuration Manager
description: Installare i componenti di gestione di BitLocker per il portale self-service e il sito Web di Administration and Monitoring
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e2b0c71dfd93fd264e900b6a42952cf3c80374b1
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662349"
---
# <a name="set-up-bitlocker-portals"></a>Configurare i portali di BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Per utilizzare i componenti di gestione di BitLocker seguenti in Configuration Manager, è necessario prima installarli:

- Portale self-service degli utenti
- Sito Web di Administration and Monitoring (portale helpdesk)

È possibile installare i portali in un server del sito esistente con IIS oppure usare un server Web autonomo per ospitarli.

> [!NOTE]
> Nella versione 1910, installare solo il portale self-service e il sito Web di Administration and Monitoring con un database del sito primario. In una gerarchia installare questi siti Web per ogni sito primario.

Prima di iniziare, verificare i [prerequisiti](/configmgr/protect/plan-design/bitlocker-management#prerequisites) per questi componenti.

## <a name="script-usage"></a>Uso degli script

Questo processo usa uno script di PowerShell, MBAMWebSiteInstaller.ps1, per installare questi componenti nel server Web. I parametri accettati sono i seguenti:

- `-SqlServerName <ServerName>` (obbligatorio): nome di dominio completo del server di database del sito primario.

- `-SqlInstanceName <InstanceName>`: il nome dell'istanza di SQL Server per il database del sito primario. Questo parametro è facoltativo se SQL usa l'istanza predefinita.

- `-SqlDatabaseName <DatabaseName>` (obbligatorio): nome del database del sito primario, ad esempio `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: URL del servizio Web del punto di Reporting Services del sito primario. Si tratta del valore **URL servizio Web** in **Gestione configurazione Reporting Services**.

    > [!NOTE]
    > Questo parametro consente di installare il **report controllo ripristino** collegato dal sito Web di Administration and Monitoring. Per impostazione predefinita Configuration Manager include gli altri report di gestione di BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: ad esempio, `contoso\BitLocker help desk users`. Gruppo utenti di dominio i cui membri hanno accesso alle aree **Manage TPM** (Gestisci TPM) e **Drive Recovery** (Ripristino unità) nel sito Web di amministrazione e monitoraggio. Quando si usano queste opzioni, questo ruolo deve compilare tutti i campi, inclusi il dominio e il nome dell'account dell'utente.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: ad esempio, `contoso\BitLocker help desk admins`. Gruppo utenti di dominio i cui membri hanno accesso alle aree di ripristino del sito Web di amministrazione e monitoraggio. Per consentire agli utenti di ripristinare le unità, questo ruolo deve solo immettere la chiave di ripristino.

- `-MbamReportUsersGroupName <DomainUserGroup>`: ad esempio, `contoso\BitLocker report users`. Gruppo utenti di dominio i cui membri hanno accesso in sola lettura all'area **Report** del sito Web di amministrazione e monitoraggio.

- `-SiteInstall Both`: specificare quale componente installare. Le opzioni valide includono:
  - `Both`: installare entrambi i componenti
  - `HelpDesk`: installare solo il sito Web di amministrazione e monitoraggio
  - `SSP`: installare solo il portale self-service

- `IISWebSite`: il sito Web in cui lo script installa le applicazioni Web di MBAM. Per impostazione predefinita, usa il sito Web IIS predefinito.

- `InstallDirectory`: il percorso in cui lo script installa i file dell'applicazione Web. Per impostazione predefinita, il percorso è `C:\inetpub`.

## <a name="run-the-script"></a>Eseguire lo script

Nel server Web di destinazione eseguire le operazioni seguenti:

> [!NOTE]
> A seconda della progettazione del sito, potrebbe essere necessario eseguire lo script più volte. Ad esempio, eseguire lo script nel punto di gestione per installare il sito Web di Administration and Monitoring. Quindi eseguirlo di nuovo in un server Web autonomo per installare il portale self-service.

1. Copiare i file seguenti da `SMSSETUP\BIN\X64` nella cartella di installazione Configuration Manager sul server del sito in una cartella locale nel server di destinazione:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Eseguire PowerShell come amministratore e quindi eseguire lo script in modo simile alla riga di comando seguente:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Ad esempio,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

Una volta eseguita l'installazione, accedere ai portali tramite gli URL seguenti:

- Portale self-service: `https://webserver.contoso.com/SelfService`
- Sito Web di amministrazione e monitoraggio: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> L'uso di HTTPS è consigliato ma non obbligatorio. Per altre informazioni, vedere [Come configurare SSL in IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="verify"></a>Verifica

Per eseguire monitoraggio e risoluzione dei problemi usare i registri seguenti:

- Registri eventi di Windows in **Microsoft-Windows-mbam-Web**. Per ulteriori informazioni, vedere [informazioni sui registri eventi di BitLocker e sui](/configmgr/protect/tech-ref/bitlocker/about-event-logs) [registri eventi del server](/configmgr/protect/tech-ref/bitlocker/server-event-logs).

- I log di traccia per ogni componente si trovano nei percorsi predefiniti seguenti:

  - Portale self-service: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Sito Web di amministrazione e monitoraggio: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Per ulteriori informazioni sulla risoluzione dei problemi, vedere [Troubleshoot BitLocker](/configmgr/protect/tech-ref/bitlocker/troubleshoot).

## <a name="next-steps"></a>Passaggi successivi

[Personalizzare il portale self-service](/configmgr/protect/deploy-use/bitlocker/customize-self-service-portal)

Per ulteriori informazioni sull'utilizzo dei componenti installati, vedere gli articoli seguenti:

- [Sito Web di amministrazione e monitoraggio BitLocker](/configmgr/protect/deploy-use/bitlocker/helpdesk-portal)
- [Portale self-service BitLocker](/configmgr/protect/deploy-use/bitlocker/self-service-portal)
