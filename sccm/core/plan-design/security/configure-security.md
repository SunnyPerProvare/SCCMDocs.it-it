---
title: Configurare la sicurezza in System Center Configuration Manager
description: Configurare le opzioni relative alla sicurezza per System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e43979e1c5cdf9559b8a9f11c8f8de4008ae406


---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurare la sicurezza in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni contenute in questo argomento per configurare le seguenti opzioni relative alla sicurezza per System Center Configuration Manager:  

-   [Configure Settings for Client PKI Certificates](#BKMK_ConfigureClientPKI)  

-   [Configurare la firma e la crittografia](#BKMK_ConfigureSigningEncryption)  

-   [Configure Role-Based Administration](#BKMK_ConfigureRBA)  

-   [Manage Accounts that are Used by Configuration Manager](#BKMK_ManageAccounts)  

##  <a name="a-namebkmkconfigureclientpkia-configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Configurare le impostazioni per i certificati PKI client  
Se si desidera utilizzare i certificati di infrastruttura a chiave pubblica (PKI) per le connessioni client con i sistemi del sito che utilizzano IIS (Internet Information Services), utilizzare la seguente procedura per configurare le impostazioni relative ai certificati.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Per configurare le impostazioni dei certificati PKI client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione sito**, fare clic su **Siti**e quindi sul sito primario da configurare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**e quindi sulla scheda **Comunicazione computer client** .  

    Questa scheda è disponibile solo in un sito primario. Se la scheda **Comunicazione computer client** non viene visualizzata, verificare di non essere connessi a un sito di amministrazione centrale o a un sito secondario.  

4.  Fare clic su **Solo HTTPS** per fare in modo che i client assegnati al sito utilizzino sempre un certificato PKI client durante la connessione ai sistemi del sito che utilizzano IIS. In alternativa, fare clic su **HTTPS o HTTP** se non è necessario che i client utilizzino i certificati PKI.  

5.  Se è stata selezionata l'opzione **HTTPS o HTTP**, fare clic su **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile** per utilizzare un certificato PKI client per le connessioni HTTP. Il client utilizza questo certificato anziché un certificato autofirmato per l'autenticazione nei sistemi del sito. Questa opzione viene selezionata automaticamente se si seleziona **Solo HTTPS**.  

    Se i client vengono rilevati in Internet o vengono configurati solo per la gestione client Internet, essi utilizzano sempre un certificato PKI client.  

6.  Fare clic su **Modifica** per configurare il metodo di selezione client scelto nel caso in cui in un client sia disponibile più di un certificato client PKI valido, quindi fare clic su **OK**.  

    Per altre informazioni sul metodo di selezione del certificato client, vedere l'argomento [Pianificazione della selezione del certificato client PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Selezionare o deselezionare la casella di controllo relativa al controllo dell'elenco di revoche di certificati (CRL) da parte dei client.  

    Per altre informazioni sul controllo CRL da parte dei client, vedere [Pianificazione di revoche di certificati PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Se è necessario specificare i certificati dell'autorità di certificazione radice attendibile (CA) per i client, fare clic su **Imposta**, importare i file di certificato della CA radice, quindi fare clic su **OK**.  

    Per altre informazioni su questa impostazione, vedere [Pianificazione di certificati radice trusted PKI e dell'elenco di autorità emittenti di certificati](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà per il sito.  

Ripetere questa procedura per tutti i siti primari nella gerarchia.  

##  <a name="a-namebkmkconfiguresigningencryptiona-configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Configurare la firma e la crittografia  
Configurare le impostazioni di firma e crittografia più sicure per i sistemi del sito supportate da tutti i client del sito. Queste impostazioni sono particolarmente importanti quando si consente ai client di comunicare con i sistemi del sito utilizzando i certificati autofirmati tramite HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Per configurare la firma e la crittografia per un sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione sito**, fare clic su **Siti**e quindi sul sito primario da configurare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**e quindi sulla scheda **Firma e crittografia** .  

    Questa scheda è disponibile solo in un sito primario. Se la scheda **Firma e crittografia** non viene visualizzata, verificare di non essere connessi a un sito di amministrazione centrale o a un sito secondario.  

4.  Configurare le opzioni di firma e crittografia desiderate e quindi fare clic su **OK**.  

    > [!WARNING]  
    >  Non selezionare **Richiedi SHA-256** prima di aver verificato che tutti i client che è possibile assegnare al sito siano in grado di supportare questo algoritmo hash o che dispongano di un certificato di autenticazione client PKI valido. Potrebbe essere necessario installare aggiornamenti o hotfix nei client per il supporto di SHA-256. Ad esempio, i computer che eseguono Windows Server 2003 SP2 devono installare un hotfix a cui si fa riferimento nell' [articolo della Knowledge Base 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Se questa opzione viene selezionata e i client non sono in grado di supportare SHA-256 ma usano certificati autofirmati, questi client vengono rifiutati da Configuration Manager. In questo scenario, il componente SMS_MP_CONTROL_MANAGER registra l'ID messaggio 5443.  

5.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà** per il sito.  

Ripetere questa procedura per tutti i siti primari nella gerarchia.  

##  <a name="a-namebkmkconfigurerbaa-configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Configurare l'amministrazione basata su ruoli  
L'amministrazione basata su ruoli combina ruoli di sicurezza, ambiti di protezione e raccolte assegnate per definire l'ambito amministrativo per ogni utente amministratore. L'ambito amministrativo comprende gli oggetti che possono essere visualizzati da un utente amministratore nella console di Configuration Manager, nonché le attività relative a tali oggetti eseguibili dall'utente amministratore. Le configurazioni dell'amministrazione basata su ruoli vengono applicate a tutti i siti della gerarchia.  

Di seguito sono riportati collegamenti alle sezioni pertinenti dell'argomento [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md):  

-   [Creare ruoli di sicurezza personalizzati](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurare i ruoli di sicurezza](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurare gli ambiti di protezione per un oggetto](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurare le raccolte per la gestione della sicurezza](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Creare un nuovo utente amministratore](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modificare l'ambito amministrativo di un utente amministratore](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  L'ambito amministrativo consente di definire gli oggetti e le impostazioni che è possibile assegnare quando si configura l'amministrazione basata su ruoli per un altro utente amministratore. Per informazioni sulla pianificazione dell'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="a-namebkmkmanageaccountsa-manage-accounts-that-are-used-by-configuration-manager"></a><a name="BKMK_ManageAccounts"></a> Gestire gli account usati da Configuration Manager  
Configuration Manager supporta gli account di Windows per diverse attività e usi.  

Usare la procedura seguente per visualizzare gli account configurati per le diverse attività e per gestire la password usata da Configuration Manager per ogni account.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Per gestire gli account usati da Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e quindi fare clic su **Account** per visualizzare gli account configurati per Configuration Manager.  

3.  Per modificare la password per un account configurato per Configuration Manager, selezionare l'account.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic su **Imposta** per aprire la finestra di dialogo **Account utente di Windows** e specificare la nuova password che Configuration Manager userà per l'account.  

    > [!NOTE]  
    >  La password specificata deve corrispondere alla password specificata per l'account in Utenti e computer di Active Directory.  

6.  Fare clic su **OK** per completare la procedura.  



<!--HONumber=Nov16_HO1-->


