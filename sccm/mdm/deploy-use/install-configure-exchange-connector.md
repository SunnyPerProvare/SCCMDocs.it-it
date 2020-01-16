---
title: Installare Exchange Connector
titleSuffix: Configuration Manager
description: Installare e configurare Exchange Connector per Configuration Manager per gestire i dispositivi mobili tramite ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d064b440922eb6994b2f761833f27a1d9590f34
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76037080"
---
# <a name="install-and-configure-the-exchange-connector"></a>Installare e configurare Exchange Connector

*Si applica a: Configuration Manager (Current Branch)*

Utilizzare questa procedura per installare e configurare un connettore Exchange Server per la gestione dei dispositivi mobili. Configuration Manager supporta un solo connettore in un'organizzazione Exchange.

Prima di installare il connettore Exchange Server per Configuration Manager, assicurarsi di disporre delle autorizzazioni e delle versioni necessarie. Per altre informazioni, vedere [gestione dei dispositivi con Exchange e Configuration Manager](/configmgr/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync#prerequisites).

## <a name="exchange-connection-account"></a>Account di connessione di Exchange

Stabilire quale account verrà connesso al server Accesso client di Exchange per gestire i dispositivi mobili. L'account può essere l'account computer del server del sito o un account utente di Windows.

Configurare quindi questo account in un gruppo di ruoli Exchange per eseguire i seguenti cmdlet di Exchange Server:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-User**  

- **Set-ActiveSyncOrganizationSettings**  

I seguenti ruoli di gestione di Exchange Server includono questi cmdlet:

- Gestione dei destinatari
- Gestione delle organizzazioni di sola visualizzazione
- Gestione del server

Per ulteriori informazioni, vedere informazioni sui [gruppi del ruolo di gestione](https://docs.microsoft.com/exchange/understanding-management-role-groups-exchange-2013-help) nella documentazione di Exchange Server 2013.

> [!TIP]  
> Se si tenta di installare o usare il connettore Exchange Server senza i cmdlet richiesti, verrà visualizzato l'errore seguente nel file EasDisc. log nel computer del server del sito: `Invoking cmdlet <cmdlet> failed`.

## <a name="install-the-connector"></a>Installare il connettore

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** , espandere **configurazione della gerarchia**e quindi selezionare **connettori Exchange Server**.

1. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** , selezionare **Aggiungi Exchange Server**.

1. Nella pagina **generale** della procedura guidata Aggiungi Exchange Server selezionare uno degli ambienti di Exchange Server:

    - **Exchange Server locale**: specificare un singolo server o un array del server Accesso client per ogni sito Active Directory.

        Se il server o l'array è offline, Configuration Manager cerca di trovare un server Accesso client da usare. Se questa operazione ha esito negativo, Client Access Server tenta di usare un server delle cassette postali per effettuare una connessione a un server Accesso client. Quando si ritenta la connessione, nel file EasDisc. log nel computer del server del sito vengono registrati gli avvisi seguenti: `Failed to open runspace for site <site_name>`.

    - **Exchange Server ospitato**: specificare l'indirizzo server dell'ambiente Exchange Online.

    Quindi selezionare il sito primario per l'esecuzione del connettore Exchange Server.

1. Nella pagina **account** specificare l'account per la connessione al server Exchange. Per ulteriori informazioni, vedere [account di connessione di Exchange](#exchange-connection-account).

1. Nella pagina **individuazione** configurare la pianificazione della sincronizzazione e le regole per la ricerca dei dispositivi.

1. Nella pagina **Impostazioni** configurare le impostazioni del dispositivo mobile nei gruppi seguenti:

    - **Generalee**
    - **Password**
    - **Gestione della posta elettronica**
    - **Security**
    - **Applicazione**

    Per ulteriori informazioni, vedere [Exchange Connector Settings](/configmgr/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync#policies).

    Se si registrano i dispositivi mobili anche usando Configuration Manager [MDM locale](/configmgr/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure), abilitare l'opzione per **consentire la gestione di dispositivi mobili esterni**. Questa impostazione consente ai dispositivi mobili di continuare a ricevere messaggi di posta elettronica da Exchange dopo la registrazione da Configuration Manager.

1. completare la procedura guidata.

## <a name="verify-and-monitor"></a>Verifica e monitoraggio

Verificare l'installazione del connettore Exchange Server con i messaggi di stato e i file di log:

- Verificare che Gestione componenti del sito installato correttamente il connettore Exchange Server. Cercare l'ID di stato del messaggio **1015** dal componente **SMS_EXCHANGE_CONNECTOR** .

    L'installazione può non riuscire se il server Accesso client specificato è offline. Se Configuration Manager non riesce a installare correttamente il connettore, Configuration Manager ritenta l'installazione ogni 60 minuti. Il tentativo continua fino a quando l'installazione non riesce o si rimuove il connettore Exchange Server.

- Nel computer del server del sito esaminare **SiteComp. log** per la voce seguente: `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Registra quindi l'installazione riuscita con il testo seguente: `STATMSG: ID=1015`.

Al termine dell'installazione, monitorare i dispositivi mobili rilevati e gestiti dal connettore. Visualizzare le raccolte di dispositivi mobili e usare i report per i dispositivi mobili.

> [!NOTE]  
> Configuration Manager genera nomi per i dispositivi mobili rilevati. Usa il formato *nome utente*_*tipo di dispositivo*. Ad esempio, **jdoe_WindowsPhone**. Se un utente ha più di un dispositivo mobile dello stesso tipo, Configuration Manager visualizzerà lo stesso nome per i dispositivi mobili nella console e nei report.  

## <a name="see-also"></a>Vedere anche

- [Porte usate dai sistemi del sito e dai client di configurazione](/configmgr/core/plan-design/hierarchy/ports#BKMK_PortsExchangeConnectorHosted)
- [Supporto dei server proxy](/configmgr/core/plan-design/network/proxy-server-support#site-system-roles-that-use-a-proxy)
- [Raccomandazioni sulla sicurezza per i dispositivi mobili](/configmgr/core/clients/deploy/plan/security-and-privacy-for-clients#bkmk_mobile)
- [Informazioni sulla privacy per i dispositivi mobili gestiti con il connettore Exchange Server](/configmgr/core/clients/deploy/plan/security-and-privacy-for-clients#BKMK_Privacy_ExchangeConnector)
