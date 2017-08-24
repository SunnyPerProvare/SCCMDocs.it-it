---
title: Configurare i siti | Microsoft Docs
description: "Consultare questo elenco di controllo per verificare di aver tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurare siti e gerarchie per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver installato il primo sito di System Center Configuration Manager o avere aggiunto altri siti alla gerarchia, usare l'elenco di controllo seguente per verificare di avere tenuto in considerazione le configurazioni più comuni che interessano sia i siti che le gerarchie.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Elenco di controllo delle configurazioni comuni per i siti nuovi e aggiuntivi  
Tenere presenti le note sulla configurazione seguenti. Tali note sono valide per la maggior parte delle distribuzioni:

-   Alcune opzioni si basano su altre, ad esempio Individuazione foresta Active Directory, i limiti e i gruppi di limiti.  

-   Molte configurazioni presentano valori predefiniti che è possibile usare senza modifiche alla configurazione, almeno temporaneamente.  

-   Altre, come i gruppi di limiti e i gruppi di punti di distribuzione, devono essere configurate prima di poterle usare.  

|Azione|Dettagli|  
|------------|-------------|  
|Configurare l'amministrazione basata su ruoli|Separare le assegnazioni amministrative per controllare quali utenti amministratori possono visualizzare e gestire i diversi oggetti e dati nell'ambiente di Configuration Manager.<br /><br /> Le configurazioni per l'amministrazione basata su ruoli sono condivise con tutti i siti in una gerarchia.   <br/><br/>Per altre informazioni, vedere [Configurare l'amministrazione basata su ruoli per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Pubblicare i dati del sito in Active Directory Domain Services|Facilitare ai client l'individuazione dei servizi e l'uso efficiente delle risorse del sito.<br /><br /> È necessario innanzitutto [estendere lo schema di Active Directory per System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) e quindi configurare individualmente ogni sito per [pubblicare i dati del sito per System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md).|  
|Configurare un punto di connessione del servizio|Pianificare l'installazione e la configurazione di un punto di connessione del servizio nel sito di livello più alto della gerarchia. Per ulteriori informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Aggiungere ruoli del sistema del sito|Installare uno o più ruoli aggiuntivi del sistema del sito per singoli siti.  Per altre informazioni, vedere [Aggiungere ruoli del sistema del sito per System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurare i limiti e i gruppi di limiti del sito|Specificare i limiti che definiscono i percorsi di rete nella intranet in cui possono essere presenti i dispositivi da gestire. Configurare quindi gruppi di limiti in modo che i client in tali percorsi di rete possano trovare le risorse di Configuration Manager. Per altre informazioni, vedere [Definire i limiti del sito e i gruppi di limiti per System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurare gruppi di punti di distribuzione|Configurare gruppi logici di punti di distribuzione per semplificare la gestione delle distribuzioni. Per altre informazioni, vedere la sezione [Gestire i gruppi di punti di distribuzione](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) dell'argomento [Installare e configurare punti di distribuzione per System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Eseguire l'individuazione|Eseguire l'individuazione per trovare le risorse sulla rete, tra cui l'infrastruttura, i dispositivi e gli utenti della rete.<br /><br /> Per altre informazioni, vedere [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Aggiungere ridondanza e capacità per gli amministratori che si occupano della gestione dell'infrastruttura|Installare altri provider SMS e console di Configuration Manager per offrire agli amministratori capacità aggiuntive per la gestione dell'infrastruttura:<br /><br /> **Installare più provider SMS** per fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia. Per altre informazioni, vedere la sezione [Gestire il provider SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) dell'argomento [Modificare l'infrastruttura di System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Installare altre console di Configuration Manager** per fornire l'accesso ad altri utenti amministratori. Per altre informazioni, vedere [Installare la console di System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurare i componenti del sito|Configurare i componenti del sito per modificare il comportamento dei ruoli del sistema del sito e la creazione di report sullo stato del sito. Per altre informazioni, vedere [Componenti del sito per System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Creare raccolte personalizzate|Usando le informazioni sui dispositivi e gli utenti che sono state individuate, è possibile creare raccolte personalizzate di oggetti per semplificare le future attività di gestione. Per altre informazioni, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurare le impostazioni per gestire le distribuzioni ad alto rischio|Configurare le impostazioni in un sito in modo da avvisare gli utenti amministratori quando creano una distribuzione di sequenze di attività ad alto rischio.  Per altre informazioni, vedere [Impostazioni per gestire le distribuzioni ad alto rischio per System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurare le repliche di database per i punti di gestione|Configurare una replica di database per ridurre il carico della CPU determinato sul server di database del sito dai punti di gestione quando questi elaborano le richieste provenienti dai client. Per altre informazioni, vedere [Repliche di database per i punti di gestione per System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurare un gruppo di disponibilità SQL Server AlwaysOn per ospitare il database del sito|A partire dalla versione 1602, configurare i gruppi di disponibilità come soluzione a disponibilità elevata e ripristino di emergenza per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale. Per altre informazioni, vedere [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager).|  
|Modificare la replica tra siti|Vedere [Trasferimenti di dati tra siti in System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) per informazioni sugli argomenti seguenti:<br /><br /> Configurare la [replica basata su file](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) tra siti secondari<br /><br /> Configurare [collegamenti di replica di database](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurare [viste distribuite](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
