---
title: Configurare i siti | Microsoft Docs
description: "Consultare questo elenco di controllo per verificare di aver tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: a6936dac2159118b192a930eecb4595b0f4d4a59


---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurare siti e gerarchie per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver installato il primo sito di System Center Configuration Manager o avere aggiunto altri siti alla gerarchia, usare l'elenco di controllo seguente per verificare di avere tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Elenco di controllo delle configurazioni comuni per i siti nuovi e aggiuntivi  
 Nella maggior parte delle distribuzioni non è necessario configurare le opzioni seguenti in un ordine specifico:  

-   Alcune opzioni si basano su altre, ad esempio Individuazione foresta Active Directory, i limiti e i gruppi di limiti.  

-   Molte configurazioni presentano valori predefiniti che è possibile usare senza modifiche alla configurazione, almeno temporaneamente.  

-   Altre, come i gruppi di limiti e i gruppi di punti di distribuzione, devono essere configurate prima di poterle usare.  

|Azione|Dettagli|  
|------------|-------------|  
|Configurare l'amministrazione basata su ruoli|L'amministrazione basata su ruoli è il modo in cui vengono suddivise le assegnazioni amministrative per controllare quali utenti amministratori possono visualizzare e gestire i vari oggetti e dati nell'ambiente di Configuration Manager.<br /><br /> Le configurazioni per l'amministrazione basata su ruoli sono condivise con tutti i siti in una gerarchia.   <br />Vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|  
|Pubblicare i dati del sito in Servizi di dominio Active Directory|Quando si pubblicano i dati del sito in Servizi di dominio Active Directory, i client possono trovare facilmente i servizi e usare le risorse del sito in modo efficiente.<br /><br /> È necessario innanzitutto [Estendere lo schema di Active Directory per System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), quindi configurare ogni sito per [Pubblicare i dati del sito per System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) individualmente.|  
|Configurare un punto di connessione del servizio|Nel sito di livello superiore della gerarchia è consigliabile pianificare l'installazione e la configurazione di un punto di connessione del servizio. Per informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Aggiungere ruoli del sistema del sito|Installare uno o più ruoli del sistema del sito aggiuntivi nei singoli siti.  Vedere [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurare i limiti e i gruppi di limiti del sito|Specificare i limiti che definiscono i percorsi di rete sulla Intranet che possono contenere i dispositivi che si vuole gestire, quindi configurare gruppi di limiti in modo che i client in tali percorsi di rete possano trovare le risorse dei servizi di Configuration Manager. Vedere [Definire i limiti del sito e i gruppi di limiti per System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)|  
|Configurare gruppi di punti di distribuzione|Configurare gruppi logici di punti di distribuzione per semplificare la gestione delle distribuzioni. Vedere [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) (Gestire i gruppi di punti di distribuzione) in [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Installare e configurare i punti di distribuzione per System Center Configuration Manager).|  
|Eseguire l'individuazione|Eseguire l'individuazione per trovare le risorse sulla rete, tra cui l'infrastruttura, i dispositivi e gli utenti della rete.<br /><br /> Vedere [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Aggiungere ridondanza e capacità per chi si occupa della gestione dell'infrastruttura|È possibile installare ulteriori provider SMS e console di Configuration Manager per offrire capacità aggiuntive agli amministratori per la gestione dell'infrastruttura:<br /><br /> **Installare più provider SMS** per fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia. Vedere [Manage the SMS Provider](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) in [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md)<br /><br /> **Installare altre console di Configuration Manager** per fornire l'accesso simultaneo ad altri utenti amministratori. Vedere [Install Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md) (Installare le console di Configuration Manager)|  
|Configurare i componenti del sito|In ogni sito è possibile configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Vedere [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Creare raccolte personalizzate|Con le informazioni sui dispositivi e gli utenti che sono state individuate è possibile creare raccolte personalizzate di oggetti per semplificare le future attività di gestione. Vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|Configurare le impostazioni per gestire le distribuzioni ad alto rischio|Configurare le impostazioni in un sito in modo da avvisare gli utenti amministratori quando creano una distribuzione di sequenze di attività ad alto rischio.  Vedere [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurare le repliche di database per i punti di gestione|Configurare una replica di database per ridurre il carico della CPU sul server di database del sito derivante dai punti di gestione quando gestiscono le richieste provenienti dai client. Vedere [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurare un gruppo di disponibilità SQL Server AlwaysOn per ospitare il database del sito|A partire dalla versione 1602, è possibile configurare i gruppi di disponibilità come soluzione a disponibilità elevata e ripristino di emergenza per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale. Vedere [SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)|  
|Modificare la replica tra siti|Vedere [Trasferimenti di dati tra siti in System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) per informazioni sugli argomenti seguenti:<br /><br /> Configurare [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) tra siti secondari<br /><br /> Configurare [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurare [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  



<!--HONumber=Dec16_HO3-->


