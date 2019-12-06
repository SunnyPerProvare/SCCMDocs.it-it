---
title: HTTP avanzato
titleSuffix: Configuration Manager
description: Usare l'autenticazione moderna per proteggere le comunicazioni client senza dover usare certificati PKI.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5634fb611d305fff196b7d6eb0b4ed97ff13d3e
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "70110074"
---
# <a name="enhanced-http"></a>HTTP avanzato

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1806 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1810, questa funzionalità non è più in versione non definitiva.  

Microsoft consiglia l'uso delle comunicazioni HTTPS per tutti i percorsi di comunicazione di Configuration Manager, ma alcuni clienti possono avere difficoltà a causa del sovraccarico di gestione dei certificati PKI.

Configuration Manager versione 1806 include miglioramenti per le modalità di comunicazione dei client con i sistemi del sito. Questi miglioramenti hanno due obiettivi principali:  

- Proteggere le comunicazioni client sensibili senza dover usare certificati di autenticazione server PKI.  

- I client possono accedere in modo sicuro al contenuto dai punti di distribuzione senza la necessità di un account di accesso alla rete, di un certificato PKI del client e dell'autenticazione di Windows.  

Tutte le altre comunicazioni client sono su HTTP. Usare HTTP avanzato non è come abilitare HTTPS per la comunicazione client o un sistema del sito.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> I certificati PKI rimangono un'opzione valida per i clienti con i requisiti seguenti:  
>
> - Tutte le comunicazioni client sono su HTTPS  
> - Controllo avanzato dell'infrastruttura di firma  


## <a name="bkmk_scenario"></a> Scenari

Gli scenari seguenti traggono vantaggio da questi miglioramenti:  

### <a name="bkmk_scenario1"></a> Scenario 1: Da client a punto di gestione

<!--1356889-->
[I dispositivi aggiunti ad Azure Active Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) possono comunicare usando un punto di gestione configurato per HTTP. Il server del sito genera un certificato per il punto di gestione in modo che possa comunicare tramite un canale sicuro.

> [!Note]  
> Questo comportamento è cambiato rispetto a Configuration Manager Current Branch versione 1802, che richiede un punto di gestione abilitato per HTTPS per i client aggiunti ad Azure AD che comunicano attraverso un gateway di gestione cloud. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

### <a name="bkmk_scenario2"></a> Scenario 2: Da client a punto di distribuzione

<!--1358228-->
Un gruppo di lavoro o un client aggiunto ad Azure AD può eseguire l'autenticazione e scaricare contenuto usando un canale sicuro da un punto di distribuzione configurato per HTTP. Questi tipi di dispositivi possono eseguire l'autenticazione e scaricare contenuto anche da un punto di distribuzione configurato per HTTPS senza richiedere un certificato PKI sul client. L'aggiunta di un certificato di autenticazione client a un gruppo di lavoro o un client aggiunto ad Azure AD è un'operazione complessa.

Questo comportamento comprende gli scenari di distribuzione del sistema operativo con una sequenza di attività eseguita da supporti di avvio, PXE o Software Center. Per altre informazioni, vedere [Account di accesso alla rete](/sccm/core/plan-design/hierarchy/accounts#network-access-account).<!--1358278-->

### <a name="bkmk_scenario3"></a> Scenario 3: Identità del dispositivo di Azure AD

<!--1358460-->
Un dispositivo aggiunto ad Azure AD o un [dispositivo di Azure AD ibrido](/azure/active-directory/devices/concept-azure-ad-join-hybrid) senza un utente di Azure AD connesso può comunicare in modo sicuro con il relativo sito assegnato. L'identità del dispositivo basata sul cloud è ora sufficiente per l'autenticazione con il gateway di gestione cloud e il punto di gestione negli scenari incentrati sui dispositivi. Un token utente è comunque necessario negli scenari incentrati sull'utente.  


## <a name="features"></a>Caratteristiche

Le seguenti funzionalità di Configuration Manager supportano o richiedono HTTP avanzato:

- [Gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Distribuzione del sistema operativo senza un account di accesso alla rete](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#enhanced-http)
- [Abilitare la co-gestione per nuovi dispositivi Windows 10 basati su Internet](/sccm/comanage/tutorial-co-manage-new-devices)
- [Approvazioni di app tramite posta elettronica](/sccm/apps/deploy-use/app-approval#bkmk_email-approve)
- [Servizio di amministrazione](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)
- [Visualizzare le console connesse di recente](/sccm/core/servers/manage/admin-console#bkmk_viewconnected)

> [!Note]  
> Il punto di aggiornamento software e gli scenari correlati hanno sempre supportato il traffico HTTP sicuro con i client, nonché con il gateway di gestione cloud. Usano un meccanismo con il punto di gestione diverso dall'autenticazione basata sui certificati o sui token.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Prerequisiti  

- Un punto di gestione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Generale** delle proprietà del ruolo del sistema del sito.  

- Un punto di distribuzione configurato per connessioni client HTTP. Impostare questa opzione nella scheda **Generale** delle proprietà del ruolo del sistema del sito. Non abilitare l'opzione **Consenti connessione anonima dei client**.  

- Eseguire l'onboarding del sito in Azure AD per la gestione del cloud.  

    - Se questo prerequisito per il sito è già soddisfatto, è necessario aggiornare l'applicazione Azure AD. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Tenant di Azure Active Directory**. Selezionare il tenant di Azure AD, selezionare l'applicazione Web nel riquadro **Applicazioni** e quindi selezionare **Aggiornare le impostazioni dell'applicazione** nella barra multifunzione.  

- *Solo per lo [scenario 3](#bkmk_scenario3)* : un client che esegue Windows 10 versione 1803 o successiva e aggiunto ad Azure AD. Il client richiede questa configurazione per l'autenticazione del dispositivo Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Configurare il sito

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**. Selezionare il sito e scegliere **Proprietà** nella barra multifunzione.  

2. Passare alla scheda **Comunicazione computer client**.

    > [!Note]
    > A partire dalla versione 1906, questa scheda è denominata **Communication Security** (Sicurezza comunicazione).<!-- SCCMDocs#1645 -->  

    Selezionare l'opzione **HTTPS o HTTP**. Quindi abilitare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**.

> [!Tip]
> Attendere fino a 30 minuti che il punto di gestione riceva e configuri il nuovo certificato del sito.

<!--3798957-->
A partire dalla versione 1902, è anche possibile abilitare HTTP avanzato per il sito di amministrazione centrale. Usare lo stesso processo e aprire le proprietà del sito di amministrazione centrale. Questa azione HTTP avanzato solo per i ruoli Provider SMS nel sito di amministrazione centrale. Non è un'impostazione globale valida per tutti i siti nella gerarchia.

È possibile visualizzare questi certificati nella console di Configuration Manager. Nell'area di lavoro **Amministrazione** espandere **Sicurezza** e selezionare il nodo **Certificati**. Cercare il certificato radice **Emissione SMS**, nonché i certificati di ruolo del server del sito emessi dalla radice di emissione SMS.

Per altre informazioni sul modo in cui il client comunica con il punto di gestione e il punto di distribuzione in questa configurazione, vedere [Comunicazioni da client a sistemi e servizi del sito](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System).


## <a name="see-also"></a>Vedere anche

- [Pianificare la sicurezza](/sccm/core/plan-design/security/plan-for-security)  

- [Sicurezza e privacy per i client di Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurare la sicurezza](/sccm/core/plan-design/security/configure-security)  

- [Comunicazioni tra gli endpoint](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  
