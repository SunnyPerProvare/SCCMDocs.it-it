---
title: Domande frequenti su Cloud Management Gateway
titleSuffix: Configuration Manager
description: Questo articolo contiene le risposte alle domande frequenti sul gateway di gestione cloud
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 8d139986ba665c8db2a26b5991c0e113efca9dd9
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75824589"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Domande frequenti sul gateway di gestione cloud

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo contiene le risposte alle domande frequenti sul gateway di gestione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Domande frequenti

### <a name="what-certificates-do-i-need"></a>Quali certificati sono necessari?

Per informazioni più dettagliate, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>È necessario Microsoft Azure ExpressRoute?

No. [Microsoft Azure ExpressRoute](/azure/expressroute/expressroute-introduction) consente di estendere la rete locale nel cloud Microsoft. Microsoft Azure ExpressRoute o altre connessioni di rete virtuale simili non sono necessari per il gateway di gestione cloud di Configuration Manager. La progettazione del gateway di gestione cloud consente ai client basati su Internet di comunicare tramite il servizio di Azure con i sistemi del sito locale senza alcuna configurazione di rete aggiuntiva. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>È necessario gestire le macchine virtuali di Azure?

Non è necessaria alcuna manutenzione. La progettazione del gateway di gestione cloud usa una piattaforma come servizio (PaaS) di Azure. Tramite la sottoscrizione offerta dall'utente, Configuration Manager crea le macchine virtuali (VM), le risorse di archiviazione e la rete necessari. Azure protegge e aggiorna la macchina virtuale. Queste macchine virtuali non fanno parte dell'ambiente locale, come accade con l'infrastruttura come servizio (IaaS). Il gateway di gestione cloud è un PaaS che estende l'ambiente di Configuration Manager nel cloud. Per altre informazioni, vedere [Protezione delle distribuzioni PaaS](/azure/security/security-paas-deployments).


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Come è possibile garantire la continuità del servizio durante gli aggiornamenti del servizio?

Grazie alla scalabilità di Cloud Management Gateway che permette di includere due o più istanze, è possibile usare automaticamente i domini di aggiornamento in Azure. Vedere [Come aggiornare un servizio cloud](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Sto già usando IBCM. Se aggiungo Cloud Management Gateway, come si comportano i client?

Se è già stata distribuita la [gestione client basata su Internet](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), è possibile anche distribuire il gateway di gestione cloud. I client ricevono criteri per entrambi i servizi. Quando effettuano il roaming su Internet, essi selezionano in modo casuale e usano uno di questi servizi basati su Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>Gli account utente devono trovarsi nella sottoscrizione di Azure che ospita il servizio cloud CMG?
<!--SCCMDocs-pr issue #2873-->
Se l'ambiente ha più di una sottoscrizione, è possibile distribuire CMG in qualsiasi sottoscrizione in grado di ospitare i servizi cloud di Azure. 

Questa domanda è comune negli scenari seguenti:  

- Quando si usano ambienti di test e produzione distinti per Active Directory e Azure AD, ma un'unica sottoscrizione di hosting centralizzata di Azure  

- L'uso di Azure è cresciuto organicamente in team diversi  

Quando si usa una distribuzione di Resource Manager, eseguire l'onboarding del tenant di Azure AD associato. Questa connessione consente a Configuration Manager di eseguire l'autenticazione ad Azure per creare, distribuire e gestire il CMG.  

Se si usa l'autenticazione di Azure AD per gli utenti e i dispositivi gestiti con il CMG, eseguire l'onboarding del tenant di Azure AD. Per altre informazioni sui servizi di Azure per la gestione cloud, vedere [Configurare i servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Quando si carica ogni tenant di Azure AD, un singolo CMG può specificare l'autenticazione di Azure AD per più tenant, indipendentemente dalla posizione di hosting.

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Come influisce CMG sui client connessi tramite VPN?

I client mobili che si connettono all'ambiente tramite VPN vengono comunemente rilevati come se usassero una connessione Intranet. Tentano di connettersi all'infrastruttura locale, ad esempio a punti di gestione e punti di distribuzione. Alcuni clienti preferiscono che questi client mobili siano gestiti da servizi cloud anche quando si connettono tramite VPN. A partire dalla versione 1902, CMG viene associato a un gruppo di limiti. In questo modo i client non possono usare i sistemi del sito locali. Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Se si abilita CMG, i client si connetteranno solo al punto di gestione abilitato per CMG quando sono connessi alla rete Intranet?

Per proteggere il traffico di dati sensibili inviati tramite CMG, configurare un punto di gestione HTTPS oppure usare HTTP migliorato.

Se si sceglie di implementare un CMG e usare certificati PKI per la comunicazione HTTPS nel punto di gestione abilitato per CMG, selezionare l'opzione **Consenti solo connessione client Internet** nelle proprietà del punto di gestione. Questa impostazione assicura che i client interni continueranno a usare i punti di gestione HTTP nell'ambiente.

Se si usa HTTP migliorato, non è necessario configurare questa impostazione. I client continueranno a usare HTTP quando comunicano direttamente con il punto di gestione abilitato per CMG. Per altre informazioni, vedere [HTTP migliorato](/sccm/core/plan-design/hierarchy/enhanced-http).

## <a name="next-steps"></a>Passaggi successivi

- [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificati per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sicurezza e privacy per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Numeri di ridimensionamento e scalabilità del gateway di gestione cloud](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
