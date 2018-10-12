---
title: Domande frequenti su Cloud Management Gateway
description: Questo articolo contiene le risposte alle domande frequenti sul gateway di gestione cloud
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 16cb80efe5ad082d8624452c01dcd54a5eca27f2
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2018
ms.locfileid: "45600940"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Domande frequenti sul gateway di gestione cloud

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo contiene le risposte alle domande frequenti sul gateway di gestione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="what-certificates-do-i-need"></a>Quali certificati sono necessari?

Per informazioni più dettagliate, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>È necessario Microsoft Azure ExpressRoute?

[Microsoft Azure ExpressRoute](/azure/expressroute/expressroute-introduction) consente di estendere la rete locale nel cloud Microsoft. Microsoft Azure ExpressRoute o altre connessioni di rete virtuale simili non sono necessari per il gateway di gestione cloud di Configuration Manager. La progettazione del gateway di gestione cloud consente ai client basati su Internet di comunicare tramite il servizio di Azure con i sistemi del sito locale senza alcuna configurazione di rete aggiuntiva. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

Se l'organizzazione usa Microsoft Azure ExpressRoute, una procedura ottimale di protezione consiste nell'isolare la sottoscrizione di Azure per il gateway di gestione cloud. Questa configurazione assicura che il gateway di gestione cloud non sia connesso accidentalmente in questo modo. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>È necessario gestire le macchine virtuali di Azure?

Non è necessaria alcuna manutenzione. La progettazione del gateway di gestione cloud usa una piattaforma come servizio (PaaS) di Azure. Tramite la sottoscrizione offerta dall'utente, Configuration Manager crea le macchine virtuali (VM), le risorse di archiviazione e la rete necessari. Azure protegge e aggiorna la macchina virtuale. Queste macchine virtuali non fanno parte dell'ambiente locale, come accade con l'infrastruttura come servizio (IaaS). Il gateway di gestione cloud è un PaaS che estende l'ambiente di Configuration Manager nel cloud. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Sto già usando IBCM. Se aggiungo Cloud Management Gateway, come si comportano i client?

Se è già stata distribuita la [gestione client basata su Internet](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), è possibile anche distribuire il gateway di gestione cloud. I client ricevono criteri per entrambi i servizi. Quando effettuano il roaming su Internet, essi selezionano in modo casuale e usano uno di questi servizi basati su Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>Gli account utente devono trovarsi nella sottoscrizione di Azure che ospita il servizio cloud CMG?
<!--SCCMDocs-pr issue #2873--> Se l'ambiente ha più di una sottoscrizione, è possibile distribuire CMG in qualsiasi sottoscrizione in grado di ospitare i servizi cloud di Azure. 

Questa domanda è comune negli scenari seguenti:  

- Quando si usano ambienti di test e produzione distinti per Active Directory e Azure AD, ma un'unica sottoscrizione di hosting centralizzata di Azure  

- L'uso di Azure è cresciuto organicamente in team diversi  

Quando si usa una distribuzione di Resource Manager, eseguire l'onboarding del tenant di Azure AD associato. Questa connessione consente a Configuration Manager di eseguire l'autenticazione ad Azure per creare, distribuire e gestire il CMG.  

Se si usa l'autenticazione di Azure AD per gli utenti e i dispositivi gestiti con il CMG, eseguire l'onboarding del tenant di Azure AD. Per altre informazioni sui servizi di Azure per la gestione cloud, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Quando si carica ogni tenant di Azure AD, un singolo CMG può specificare l'autenticazione di Azure AD per più tenant, indipendentemente dalla posizione di hosting.



## <a name="next-steps"></a>Passaggi successivi

- [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificati per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sicurezza e privacy per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Numeri di ridimensionamento e scalabilità del gateway di gestione cloud](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)