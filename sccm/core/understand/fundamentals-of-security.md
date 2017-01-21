---
title: Nozioni fondamentali sulla sicurezza | Microsoft Docs
description: Di seguito sono riportate informazioni sui livelli di protezione per System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: b4d12eaadaf0324515f6ae595a737f576bd5076c


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Nozioni fondamentali sulla sicurezza di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La sicurezza di System Center Configuration Manager è costituita da diversi livelli. Il primo livello è fornito dalle funzionalità di sicurezza di Windows per il sistema operativo e per la rete, incluse le seguenti:  

-   Condivisione di file per il trasferimento di file tra componenti di Configuration Manager  

-   Elenchi di controllo di accesso (ACL) per agevolare la protezione dei file e delle chiavi del Registro di sistema  

-   IPsec per proteggere le comunicazioni  

-   Criteri di gruppo per impostare criteri di protezione  

-   Autorizzazioni DCOM per applicazioni distribuite, ad esempio la console di Configuration Manager  

-   Servizi di dominio Active Directory per memorizzare le entità di protezione  

-   Protezione account di Windows, inclusi alcuni gruppi creati durante la configurazione di Configuration Manager  

Altri componenti di protezione aggiuntivi, ad esempio firewall e rilevamento intrusioni, aiutano a offrire una difesa approfondita per l'intero ambiente. I certificati emessi dalle implementazioni PKI standard per il settore consentono di offrire autenticazione, firma e crittografia.  

Oltre alla sicurezza fornita da Windows Server e dall'infrastruttura di rete, Configuration Manager controlla l'accesso alla console di Configuration Manager e alle relative risorse in diversi modi. Per impostazione predefinita, solo gli amministratori locali hanno i diritti per i file e per le chiavi del Registro di sistema necessari per l'esecuzione della console di Configuration Manager nei computer in cui è installata.  

Il livello successivo di protezione si basa sull'accesso con Windows Management Instrumentation (WMI), in particolare sul **provider SMS**. Il provider SMS è un componente di Configuration Manager che concede a un utente l'accesso per eseguire query nel database del sito per informazioni. Per impostazione predefinita, l'accesso al provider è limitato ai membri del gruppo **SMS Admins** locale. Questo gruppo contiene inizialmente solo l'utente che ha installato Configuration Manager. Per concedere altre autorizzazioni account al repository Common Information Model (CIM) e al provider SMS, aggiungere altri account al gruppo SMS Admins.  

Il livello di protezione finale si basa sulle autorizzazioni per gli oggetti nel database del sito. Per impostazione predefinita, l'account di sistema locale e l'account utente usato per l'installazione di Configuration Manager possono amministrare tutti gli oggetti nel database di sito. È possibile concedere e limitare le autorizzazioni per altri utenti amministrativi nella console di Configuration Manager usando l'**amministrazione basata su ruoli**.  

La parte rimanente di questo argomento tratta gli aspetti di sicurezza correlati a Configuration Manager.  

## <a name="role-based-administration"></a>Amministrazione basata su ruoli  
 Configuration Manager usa l'amministrazione basata su ruoli per consentire la protezione di oggetti quali raccolte, distribuzioni e siti. Questo modello di amministrazione definisce e gestisce centralmente le impostazioni di accesso di protezione a livello di gerarchia per tutti i siti e le impostazioni del sito. I ruoli di sicurezza vengono assegnati agli utenti amministrativi e le autorizzazioni di gruppo vengono assegnate a diversi tipi di oggetto di Configuration Manager, ad esempio le autorizzazioni per la creazione o la modifica delle impostazioni client. Gli ambiti di sicurezza raggruppano istanze specifiche di oggetti che un utente amministratore ha la responsabilità di gestire, ad esempio un'applicazione che installa Microsoft Office. La combinazione di ruoli di sicurezza, ambiti di protezione e raccolte consente di definire gli oggetti che possono essere visualizzati e gestiti da un utente amministrativo. Configuration Manager installa alcuni ruoli di sicurezza predefiniti per le attività di gestione comuni. Tuttavia, è possibile creare ruoli di sicurezza personalizzati per supportare requisiti aziendali specifici.  

 Per altre informazioni, vedere [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurare l'amministrazione basata su ruoli per System Center Configuration Manager)  

## <a name="securing-client-endpoints"></a>Protezione degli endpoint client  
 Le comunicazioni dei client con i ruoli del sistema del sito vengono protette tramite certificati autofirmati o tramite certificati PKI (Public Key Infrastructure). I computer client rilevati da Configuration Manager come presenti su Internet e i client di dispositivi mobili devono usare certificati PKI per consentire la protezione degli endpoint client con HTTPS. I ruoli del sistema del sito a cui si connettono i client possono essere configurati per la comunicazione client di tipo HTTPS o HTTP. I computer client comunicano sempre usando il metodo più sicuro disponibile e passano all'utilizzo del metodo di comunicazione meno sicuro, ovvero HTTP su Intranet solo se sono disponibili ruoli del sistema del sito che consentono le comunicazioni HTTP.  

 Per altre informazioni, vedere [Riferimento tecnico per i controlli crittografici per System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

## <a name="configuration-manager-accounts-and-groups"></a>Account e gruppi di Configuration Manager  
 Configuration Manager usa l'account di **sistema locale** per la maggior parte delle operazioni del sito. Tuttavia, alcune operazioni di gestione potrebbero richiedere creazione e la gestione di altri account. Durante l'installazione vengono creati diversi gruppi predefiniti e ruoli di SQL Server. Tuttavia, potrebbe essere necessario aggiungere manualmente gli account utente o computer a questi gruppi e ruoli predefiniti.  

 Per altre informazioni, vedere [Account usati in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Privacy  
 Benché i prodotti di gestione aziendale offrano molti vantaggi, grazie alla capacità effettiva di gestire un numero elevato di client, è necessario essere consapevoli del modo in cui tale software potrebbe influire sulla privacy degli utenti dell'organizzazione. System Center Configuration Manager include molti strumenti per la raccolta dei dati e il monitoraggio dei dispositivi, alcuni dei quali possono provocare problemi di privacy.  

 Ad esempio, quando si installa il client di Configuration Manager, vengono abilitate per impostazione predefinita molte impostazioni di gestione. Il software client invia pertanto informazioni al sito di Configuration Manager. Le informazioni sul client vengono archiviate nel database di Configuration Manager e non vengono inviate a Microsoft. Prima di implementare System Center Configuration Manager, considerare i requisiti relativi alla privacy.  



<!--HONumber=Dec16_HO3-->


