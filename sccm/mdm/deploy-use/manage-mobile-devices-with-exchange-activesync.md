---
title: Gestire i dispositivi mobili | Microsoft Docs
description: Gestire i dispositivi mobili usando il connettore Exchange Server in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44958bc35586f5e57ab3fb59681bfb018d2bd5da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare il connettore Exchange Server in System Center Configuration Manager quando si vuole gestire i dispositivi mobili che si connettono a Exchange Server, in locale oppure online, usando il protocollo Exchange ActiveSync e non è possibile registrarli usando Configuration Manager. È possibile configurare le funzionalità di gestione dei dispositivi mobili di Exchange, come la cancellazione remota dati nel dispositivo e il controllo delle impostazioni per più server Exchange, dalla console di Configuration Manager.  

 ![configmgr&#45;con&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-con-exchange")  

 Quando si gestiscono i dispositivi mobili usando il connettore Exchange Server, il connettore non installa il client di Configuration Manager nei dispositivi mobili. Pertanto, alcune funzioni di gestione sono limitate. È ad esempio impossibile installare il software in questi dispositivi o utilizzare gli elementi di configurazione per configurarli. Per altre informazioni sulle diverse funzioni di gestione che è possibile usare con Configuration Manager per i dispositivi mobili, vedere [Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

> [!IMPORTANT]  
>  Prima di installare il connettore Exchange Server, confermare il supporto della versione di Microsoft Exchange usata da parte di Configuration Manager. Per altre informazioni, vedere "Exchange Server connector" (Connettore Exchange Server) in [Supported operating systems for sites and clients for System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (Sistemi operativi supportati per siti e client per System Center Configuration Manager).  

 Quando si usa il connettore Exchange Server, i dispositivi mobili possono essere gestiti dalle impostazioni configurate in Configuration Manager invece di essere gestiti dai criteri cassetta postale predefiniti di Exchange ActiveSync. Definire le impostazioni da usare nelle impostazioni del gruppo seguenti: **Generale**, **Password**, **Gestione della posta elettronica**, **Sicurezza**e **Applicazione**. Ad esempio, nell'impostazione del gruppo **Password** , è possibile configurare se i dispositivi mobili richiedono una password, la lunghezza minima della password, la sua complessità e se ne è consentito il ripristino.  

 Quando si configura almeno un'impostazione nel gruppo, Configuration Manager gestisce tutte le impostazioni nel gruppo per i dispositivi mobili. Se non si configura alcuna impostazione in un gruppo, Exchange continua a gestire i dispositivi mobili per tali impostazioni. I criteri cassetta postale di Exchange ActiveSync configurati in Exchange Server e assegnati agli utenti verranno comunque applicati.  

 È inoltre possibile configurare il connettore Exchange Server per gestire le regole di accesso di Exchange e consentire, bloccare o mettere in quarantena i dispositivi mobili. È possibile cancellare i dati dei dispositivi mobili da remoto usando la console di Configuration Manager e gli utenti possono cancellare i dati dai loro dispositivi mobili usando il Catalogo applicazioni.  

 Un dispositivo mobile dell'utente viene visualizzato automaticamente nel Catalogo applicazioni quando viene gestito dal connettore Exchange Server ed Exchange Server si trova in locale. Quando si configura il connettore Exchange Server per Microsoft Exchange Online, è necessario configurare manualmente l'affinità utente-dispositivo in modo che il dispositivo mobile dell'utente venga visualizzato nel Catalogo applicazioni. Per altre informazioni sull'affinità utente-dispositivo, vedere [Collegare utenti e dispositivi mediante l'affinità utente-dispositivo in System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

> [!TIP]  
>  Se si gestisce un dispositivo mobile usando il connettore Exchange Server e il dispositivo mobile viene trasferito a un altro utente, eliminare il dispositivo mobile dalla console di Configuration Manager prima che il nuovo proprietario del dispositivo configuri l'account di Exchange nel dispositivo mobile trasferito.  

## <a name="required-security-permissions"></a>Autorizzazioni di sicurezza richieste  
 È necessario disporre delle seguenti autorizzazioni di sicurezza per configurare il connettore Exchange Server:  

-   Per aggiungere, modificare ed eliminare il connettore Exchange Server: autorizzazione di **Modifica** per l'oggetto **Sito** .  

-   Per configurare le impostazioni del dispositivo mobile: autorizzazione **ModifyConnectorPolicy** per l'oggetto **Sito** .  

 Il ruolo di sicurezza **Amministratore completo** include le autorizzazioni necessarie per configurare il connettore Exchange Server.  

 È necessario disporre delle seguenti autorizzazioni di sicurezza per gestire i dispositivi mobili:  

-   Per cancellare un dispositivo mobile: **Elimina risorsa** per l'oggetto **Raccolta** .  

-   Per annullare un comando di cancellazione: **Modifica risorsa** per l'oggetto **Raccolta** .  

-   Per consentire e bloccare i dispositivi mobili: **Modifica risorsa** per l'oggetto **Collection** .  

 Il ruolo di sicurezza **Amministratore operazioni** include le autorizzazioni necessarie per gestire i dispositivi mobili utilizzando il connettore Exchange Server.  

 Per altre informazioni su come configurare le autorizzazioni di sicurezza, vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Installare e configurare un connettore Exchange Server  
 Usare la seguente procedura per installare e configurare un connettore Exchange Server per gestire i dispositivi mobili. Configuration Manager supporta un solo connettore in un'organizzazione Exchange. Dopo aver completato questi passaggi, è possibile monitorare i dispositivi mobili rilevati e gestiti dal connettore quando si visualizzano le raccolte che mostrano i dispositivi mobili e utilizzando i report per dispositivi mobili.  

> [!NOTE]  
>  Configuration Manager generata i nomi per i dispositivi mobili rilevati usando il formato *NomeUtente*_*TipoDispositivo*. Se un utente ha più di un dispositivo mobile dello stesso tipo, Configuration Manager visualizzerà lo stesso nome per i dispositivi mobili nella console e nei report.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Per installare e configurare un connettore Exchange Server  

1.  Stabilire quale account verrà connesso al server Accesso client di Exchange per gestire i dispositivi mobili. L'account può essere l'account computer del server del sito o un account utente di Windows. Configurare quindi l'account per eseguire i seguenti cmdlet di Exchange Server:  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  

    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  

    > [!NOTE]  
    >  I ruoli di gestione di Exchange Server seguenti includono questi cmdlet: Gestione destinatari, Gestione organizzazione sola visualizzazione e Gestione server. Per ulteriori informazioni sui gruppi del ruolo di gestione in Microsoft Exchange Server 2010, vedere [Informazioni sui gruppi del ruolo di gestione](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Se si cerca di installare o utilizzare il connettore Exchange Server senza i cmdlet richiesti, verrà visualizzato un errore registrato con un messaggio del tipo `Invoking cmdlet <cmdlet> failed` nel file EasDisc.log sul computer del server del sito.  

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

3.  Nell'area di lavoro **Amministrazione** espandere **Configurazione della gerarchia**e quindi fare clic su **Connettori Exchange Server**.  

4.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi Exchange Server**.  

5.  Completare l'Aggiunta guidata Exchange Server:  

    -   Se si utilizza un'istanza locale di Exchange Server e si specifica un server Accesso client, è possibile specificare un singolo server o un array del server Accesso client per ciascun sito Active Directory. Se il server o l'array è offline, Configuration Manager cerca di trovare un server Accesso client da usare. Se questa operazione ha esito negativo, Client Access Server tenta di usare un server delle cassette postali per effettuare una connessione a un server Accesso client. I tentativi vengono registrati come avvisi nel file EasDisc.log nel computer del server del sito. Ad esempio, cercare `Failed to open runspace for site <site_name>`.  

    -   Come account connettore Exchange Server, specificare l'account configurato nel passaggio 1.  

    -   Se si registrano anche dispositivi mobili usando Configuration Manager, attivare l'opzione **Gestione dispositivi mobili esterni** per assicurarsi che i dispositivi continuino a ricevere messaggi di posta elettronica da Exchange dopo essere stati registrati da Configuration Manager.  

    -   Nella pagina **Account** della procedura guidata è possibile configurare l'account usato per inviare notifiche tramite posta elettronica ai client che vengono bloccati dall'accesso condizionale di Configuration Manager. L'account specificato deve disporre di una cassetta postale valida nel server Exchange.  

         Per altre informazioni, vedere [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  

6.  È possibile verificare l'installazione del connettore Exchange Server utilizzando i messaggi di stato e riesaminando i file di registro:  

    -   Per confermare che l'installazione del connettore Exchange Server da parte del servizio di gestione dei componenti del sito è avvenuta correttamente, cercare l'ID stato **1015** per il componente **SMS_EXCHANGE_CONNECTOR** . Se non è possibile installare correttamente il connettore, ad esempio perché il computer del server Accesso client specificato non è in linea), Configuration Manager tenterà di installarlo ogni 60 minuti fino alla riuscita dell'installazione o alla rimozione del connettore Exchange Server.  

    -   Sul computer del server del sito, cercare il file Sitecomp.log, e quindi cercare `Component SMS_EXCHANGE_CONNECTOR flagged for installation`all'interno del file di registro. Un'installazione eseguita correttamente viene quindi registrata con il seguente testo: `STATMSG: ID=1015`.  
