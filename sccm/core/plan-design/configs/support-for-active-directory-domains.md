---
title: Supporto per i domini di AD | System Center Configuration Manager
description: Requisiti per l'appartenenza di un sistema del sito di System Center Configuration Manager a un dominio di Active Directory.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fdcd1b3b59dbe2b5bd82499e8d29230b3d8ca5cd


---
# <a name="support-for-active-directory-domains-for-system-center-configuration-manager"></a>Supporto per i domini Active Directory per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Tutti i sistemi del sito di System Center Configuration Manager devono essere membri di un dominio Windows Active Directory supportato. I computer client Configuration Manager possono essere membri del dominio o membri del gruppo di lavoro.  

 **Requisiti e limitazioni:**  

-   L'appartenenza al dominio si applica ai sistemi del sito che supportano la gestione client basata su Internet in una rete perimetrale (detta anche subnet schermata).  

-   Non è supportata per modificare gli elementi seguenti per un computer che ospita un ruolo del sistema del sito:  

    -   Appartenenza al dominio  

    -   Nome di dominio  

    -   Nome computer  

Prima di apportare queste modifiche, è necessario disinstallare il ruolo del sistema del sito (incluso il sito se si tratta di un server del sito).  

**Sono supportati i domini con i livelli funzionali del dominio seguenti:**  

-   Windows Server 2008  

-   Windows Server 2008 R2  

-   Windows Server 2012  

-   Windows Server 2012 R2  

##  <a name="a-namebkmkdisjointa-disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Spazio dei nomi non contiguo  
Configuration Manager supporta l'installazione di client e sistemi del sito in un dominio che contiene uno spazio dei nomi non contiguo.  

In uno scenario di spazio dei nomi non contiguo il suffisso Domain Name System (DNS) primario di un computer non corrisponde al nome di dominio DNS di Active Directory in cui risiede il computer. Il computer che usa il suffisso DNS primario non corrispondente è detto non contiguo. Un altro scenario di spazio dei nomi non contiguo si ottiene quando il nome di dominio NetBIOS di un controller di dominio non corrisponde al nome di dominio DNS di Active Directory.  

La tabella seguente identifica gli scenari supportati per uno spazio dei nomi non contiguo.  

|Scenario|Altre informazioni|  
|--------------|----------------------|  
|**Scenario 1:**<br /><br /> Il suffisso DNS primario del controller di dominio è diverso dal nome di dominio DNS di Active Directory. I computer membri del dominio possono essere contigui o non contigui.|In questo scenario, il suffisso DNS primario del controller di dominio è diverso dal nome di dominio DNS di Active Directory. Il controller di dominio è non contiguo in questo scenario. I computer membri del dominio, ad esempio computer e server del sito, possono avere un suffisso DNS primario che corrisponde al suffisso DNS primario del controller di dominio o al nome di dominio DNS di Active Directory.|  
|**Scenario 2:**<br /><br /> Un computer membro in un dominio Active Directory è non contiguo, anche se il controller di dominio è contiguo.|In questo scenario, il suffisso DNS primario di un computer membro in cui è installato un sistema del sito è diverso dal nome di dominio DNS di Active Directory, anche se il suffisso DNS primario del controller di dominio corrisponde la nome di dominio DNS di Active Directory. In questo scenario sono presenti un controller di dominio contiguo e un computer membro non contiguo. I computer membri che eseguono il client di Configuration Manager possono avere un suffisso DNS primario che corrisponde al suffisso DNS primario del server di sistema del sito non contiguo o al nome di dominio DNS di Active Directory.|  

 Per consentire a un computer di accedere ai controller di dominio non contigui, è necessario modificare l’attributo **msDS-AllowedDNSSuffixes** di Active Directory nel contenitore dell'oggetto dominio. È necessario aggiungere entrambi i suffissi DNS all'attributo.  

 Inoltre, per assicurarsi che l'elenco di ricerca suffissi DNS contenga tutti gli spazi dei nomi DNS distribuiti all'interno dell'organizzazione, è necessario configurare l'elenco di ricerca per ogni computer nel dominio non contiguo. Includere nell'elenco degli spazi dei nomi il suffisso DNS primario del controller di dominio, il nome di dominio DNS ed eventuali spazi dei nomi aggiuntivi per altri server con cui Configuration Manager potrebbe interagire. È possibile usare la console Gestione criteri di gruppo per configurare l'elenco di **ricerca suffisso Domain Name System (DNS)** .  

> [!IMPORTANT]  
>  Quando si fa riferimento a un computer in Configuration Manager, immettere il computer usando il suffisso DNS primario. Questo suffisso deve corrispondere al nome di dominio completo registrato come attributo **dnsHostName** nel dominio di Active Directory e nome dell'entità servizio associata al sistema.  

##  <a name="a-namebkmkslda-single-label-domains"></a><a name="bkmk_SLD"></a> Domini con etichetta singola  
 Configuration Manager supporta client e sistemi del sito in un nome di dominio con etichetta singola quando vengono soddisfatti i criteri seguenti:  

-   Il dominio con etichetta singola in Servizi di dominio Active Directory deve essere configurato con uno spazio dei nomi DNS non contiguo che dispone di un dominio di livello superiore valido.  

     **Ad esempio:** il dominio con etichetta singola di Contoso è configurato per contenere uno spazio dei nomi non contiguo contoso.com in DNS. Pertanto, quando si specifica il suffisso DNS in Configuration Manager per un computer nel dominio Contoso, specificare Contoso.com e non Contoso.  

-   Le connessioni DCOM tra i server del sito nel contesto del sistema devono essere stabilite usando l'autenticazione Kerberos.  



<!--HONumber=Nov16_HO1-->

