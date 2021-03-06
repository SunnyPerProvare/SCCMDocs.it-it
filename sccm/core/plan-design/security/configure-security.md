---
title: Configurare la sicurezza
titleSuffix: Configuration Manager
description: Configurare le opzioni relative alla sicurezza per Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8bdfaa89bec2c935d344d4fe63f2405b4b49554
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80593078"
---
# <a name="configure-security-in-configuration-manager"></a>Configurare la sicurezza in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni contenute in questo articolo per configurare le opzioni relative alla sicurezza per Configuration Manager. L'articolo descrive le opzioni di sicurezza seguenti:
- [Comunicazione computer client](#BKMK_ConfigureClientPKI) per i certificati PKI dei client  
- [Firma e crittografia](#BKMK_ConfigureSigningEncryption)  
- [Amministrazione basata su ruoli](#BKMK_ConfigureRBA)  
- [Gestisci account](#BKMK_ManageAccounts)  
- [Configura Azure Active Directory](#bkmk_azuread)  
- [Configurare l'autenticazione del provider SMS](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Configurare le impostazioni per i certificati PKI client  

Se si desidera utilizzare i certificati di infrastruttura a chiave pubblica (PKI) per le connessioni client con i sistemi del sito che utilizzano IIS (Internet Information Services), utilizzare la seguente procedura per configurare le impostazioni relative ai certificati.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Per configurare le impostazioni dei certificati PKI client  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito primario da configurare.  

2.  Nella barra multifunzione scegliere **Proprietà**. Quindi passare alla scheda **Comunicazione computer client**.  

    > [!Note]
    > A partire dalla versione 1906, questa scheda è denominata **Communication Security** (Sicurezza comunicazione).<!-- SCCMDocs#1645 -->  

3.  Selezionare le impostazioni per i sistemi del sito che usano IIS.  

    - **Solo HTTPS**: i client assegnati al sito usano sempre un certificato PKI client durante la connessione ai sistemi del sito che usano IIS.  

    - **HTTPS o HTTP**: non viene richiesto l'uso dei certificati PKI da parte dei client.  

    - **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**: Per altre informazioni su questa impostazione, vedere [HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http).  

4.  Selezionare le impostazioni per i computer client.  

    - **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile**: se si sceglie l'impostazione del server del sito **HTTPS o HTTP**, selezionare questa opzione per usare un certificato PKI client per le connessioni HTTP. Il client utilizza questo certificato anziché un certificato autofirmato per l'autenticazione nei sistemi del sito. Se si sceglie **Solo HTTPS**, questa opzione viene selezionata automaticamente.  

    Quando è disponibile più di un certificato client PKI valido in un client, scegliere **Modifica** per configurare i metodi di selezione del certificato client.  

    Per altre informazioni sul metodo di selezione del certificato client, vedere l'argomento [Pianificazione della selezione del certificato client PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection).  

    - **Controllo client dell'elenco di revoche di certificati (CRL) per i sistemi del sito**: abilitare questa impostazione perché i client controllino l'elenco di revoche di certificati dell'organizzazione.  

    Per altre informazioni sul controllo CRL da parte dei client, vedere [Pianificazione di revoche di certificati PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).  

5.  Per importare, visualizzare ed eliminare i certificati per le autorità di certificazione radice attendibili, scegliere **Imposta**.  

    Per altre informazioni, vedere [Pianificare certificati radice trusted PKI e l'elenco di autorità di certificazione](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs).  


Ripetere questa procedura per tutti i siti primari nella gerarchia.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Configurare la firma e la crittografia  

Configurare le impostazioni di firma e crittografia più sicure per i sistemi del sito supportate da tutti i client del sito. Queste impostazioni sono particolarmente importanti quando si consente ai client di comunicare con i sistemi del sito utilizzando i certificati autofirmati tramite HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Per configurare la firma e la crittografia per un sito  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito primario da configurare.  

2.  Nella barra multifunzione selezionare **Proprietà** e quindi passare alla scheda **Firma e crittografia**.  

    Questa scheda è disponibile solo in un sito primario. Se la scheda **Firma e crittografia** non viene visualizzata, verificare di non essere connessi a un sito di amministrazione centrale o a un sito secondario.  

3.  Configurare le opzioni di firma e crittografia per i client per comunicare con il sito.  

    - **Richiedi firma**: i client firmano i dati prima dell'invio al punto di gestione.  

    - **Richiedi SHA-256**: i client usano l'algoritmo SHA-256 per la firma dei dati.  

    > [!WARNING]  
    >  Non selezionare **Richiedi SHA-256** senza aver prima verificato che tutti i client supportino questo algoritmo hash. Questi client includono i client che potrebbero essere assegnati al sito in futuro.  
    >   
    >  Se si sceglie questa opzione e i client con certificati autofirmati non sono supportano SHA-256, questi client vengono rifiutati da Configuration Manager. Il componente SMS_MP_CONTROL_MANAGER registra l'ID messaggio 5443.  

    - **Utilizza crittografia**: i client eseguono la crittografia dei dati di inventario e dei messaggi di stato prima dell'invio al punto di gestione. I client usano l'algoritmo 3DES.  

Ripetere questa procedura per tutti i siti primari nella gerarchia.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Configurare l'amministrazione basata su ruoli  

L'amministrazione basata su ruoli combina ruoli di sicurezza, ambiti di protezione e raccolte assegnate per definire l'ambito amministrativo per ogni utente amministratore. Un ambito comprende gli oggetti che possono essere visualizzati da un utente nella console, nonché le attività correlate agli oggetti eseguibili dall'utente. Le configurazioni dell'amministrazione basata su ruoli vengono applicate a tutti i siti della gerarchia.  

Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](/sccm/core/servers/deploy/configure/configure-role-based-administration). Questo articolo illustra nel dettaglio le azioni seguenti:  

- Creare ruoli di sicurezza personalizzati  

- Configurare i ruoli di sicurezza  

- Configurare gli ambiti di protezione per un oggetto  

- Configurare le raccolte per la gestione della sicurezza  

- Creare un nuovo utente amministratore  

- Modificare l'ambito amministrativo di un utente amministratore  

> [!IMPORTANT]  
>  L'ambito amministrativo consente di definire gli oggetti e le impostazioni che è possibile assegnare quando si configura l'amministrazione basata su ruoli per un altro utente amministratore. Per informazioni sulla pianificazione dell'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a> Gestire gli account usati da Configuration Manager  

Configuration Manager supporta gli account di Windows per diverse attività e usi. Per visualizzare gli account configurati per le diverse attività e per gestire la password usata da Configuration Manager per ogni account, usare la procedura seguente:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Per gestire gli account usati da Configuration Manager  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Sicurezza** e quindi scegliere il nodo **Account**.  

2.  Per modificare la password per un account, selezionare l'account nell'elenco. Quindi scegliere **Proprietà** nella barra multifunzione.  

3.  Scegliere **Imposta** per aprire la finestra di dialogo **Account utente di Windows**. Specificare la nuova password per Configuration Manager da usare per questo account.  

    > [!NOTE]  
    >  La password specificata deve corrispondere alla password dell'account in Active Directory.  

Per altre informazioni, vedere [Account usati in Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a> Configurare Azure Active Directory

Integrare Configuration Manager con Azure Active Directory (Azure AD) per semplificare e abilitare per il cloud l'ambiente. Abilitare il sito e i client per l'autenticazione tramite Azure AD. Per altre informazioni, vedere il servizio **Gestione cloud** in [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a> Configurare l'autenticazione del provider SMS

A partire dalla versione 1810 è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Per altre informazioni, vedere [Piano per il provider SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Vedere anche

- [Pianificare la sicurezza](/sccm/core/plan-design/security/plan-for-security)  

- [Sicurezza e privacy per i client di Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Comunicazioni tra gli endpoint](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Riferimento tecnico per i controlli crittografici](/sccm/core/plan-design/security/cryptographic-controls-technical-reference)  

- [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  
