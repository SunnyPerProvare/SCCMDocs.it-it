---
title: Co-gestione per dispositivi Windows 10
titleSuffix: Configuration Manager
description: Informazioni su come gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755370"
---
# <a name="what-is-co-management"></a>Informazioni sulla co-gestione

<!-- 1350871 --> CO-gestione è uno dei modi principali per collegare la distribuzione di Configuration Manager esistente nel cloud di Microsoft 365. Consente di sbloccare le funzionalità aggiuntive basate sul cloud, ad esempio l'accesso condizionale. 

CO-gestione consente di gestire i dispositivi Windows 10 contemporaneamente usando sia Configuration Manager e Microsoft Intune. Consente di collegare cloud l'investimento esistente in Configuration Manager mediante l'aggiunta di nuove funzionalità. Con CO-gestione, è possibile usare la soluzione di tecnologia più appropriata per l'organizzazione. 

Quando un dispositivo Windows 10 è il client di Configuration Manager e viene registrato in Intune, si ottengono i vantaggi di entrambi i servizi. Controllare quali carichi di lavoro, se presente, che si passa l'autorità da Configuration Manager a Intune. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro non passati a Intune e non supporta tutte le altre funzionalità di Configuration Manager che la co-gestione.

Si è in grado di eseguire la distribuzione pilota di un carico di lavoro con una raccolta separata di dispositivi. Avvio del progetto pilota consente di testare la funzionalità di Intune con un sottoinsieme di dispositivi prima di passare un gruppo più ampio. 

![Diagramma della panoramica di CO-gestione](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Percorsi per la co-gestione

I percorsi principali per realizzare la co-gestione sono due:  

- **I client di Configuration Manager esistenti**: Si hanno dispositivi Windows 10 che sono già client di Configuration Manager. Configurare ad Azure AD ibrido e registrarli in Intune.  

- **I nuovi dispositivi basati su internet**: Si dispongono di nuovi dispositivi Windows 10 aggiunti ad Azure AD e registrati automaticamente in Intune. Si installa il client di Configuration Manager per raggiungere uno stato di CO-gestione.  

Per altre informazioni sui percorsi, vedere [percorsi della co-gestione](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Vantaggi 

Quando si registrano i client di Configuration Manager esistenti in CO-gestione, è possibile ottenere il valore immediato seguente:  

- Accesso condizionale con conformità del dispositivo  

- Azioni di remoto basata su Intune, ad esempio: riavvio, il controllo remoto o reimpostazione di fabbrica

- Visibilità centralizzata dell'integrità dei dispositivi  

- Collegare gli utenti, dispositivi e App con Azure Active Directory (Azure AD)  

- Moderni il provisioning con Windows Autopilot  

- Azioni remote

Per altre informazioni su questo valore immediato dalla co-gestione, vedere la serie di guide introduttive per [Cloud connect con CO-gestione](/sccm/comanage/quickstarts).

CO-gestione consente anche di orchestrare con Intune per diversi carichi di lavoro. Per altre informazioni, vedere la [carichi di lavoro](#workloads) sezione. 



## <a name="prerequisites"></a>Prerequisiti

CO-gestione con questi prerequisiti nelle aree seguenti:

- [Gestione delle licenze](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Ruoli e autorizzazioni](#permissions-and-roles)  

### <a name="licensing"></a>Licenza

- Azure AD Premium 
- Licenza di EMS o Intune per tutti gli utenti  

    > [!Note]  
    > Un Enterprise Mobility + Security (EMS) sottoscrizione include Azure Active Directory Premium e Microsoft Intune.

> [!Tip]  
> Assicurarsi di assegnare una licenza di Intune per l'account usato per accedere al tenant. In caso contrario, l'accesso avrà esito negativo con messaggio di errore "L'utente non riconosciuto".  


### <a name="configuration-manager"></a>Configuration Manager

CO-gestione richiede Configuration Manager 1710 o versioni successive.

A partire da Configuration Manager versione 1806, è possibile connettere più istanze di Configuration Manager a un singolo tenant di Intune. <!--1357944-->  

Abilitare la co-gestione stessa non richiede di eseguire l'onboarding del sito con Azure AD. Per il [secondo scenario di percorso](#paths-to-co-management), i client di Configuration Manager basato su internet richiedono la [gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). Il cloud Management gateway è necessario il sito sia [caricata in Azure AD per la gestione cloud](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- I dispositivi Windows 10 devono essere aggiunti ad Azure AD. Possono essere di uno dei due tipi seguenti:  

    - [Aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), il dispositivo è aggiunto ad Active Directory locale e registrato in Azure Active Directory.  

    - [Aggiunto solo ad Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). Questo tipo è anche noto come "aggiunto a un dominio cloud".<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurare Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione. È tuttavia possibile avviare la migrazione degli utenti a Intune autonomo e quindi abilitare i dispositivi Windows 10 ad essi associati per la co-gestione. Per altre informazioni sulla migrazione a Intune autonomo, vedere [Avviare la migrazione da MDM ibrido a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Se si usa l'[autorità mista](/sccm/mdm/deploy-use/migrate-mixed-authority), completare prima la migrazione a Intune autonomo. Quindi impostare l'autorità MDM su Intune prima di impostare la co-gestione.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Aggiornare i dispositivi a Windows 10, versione 1709 o successiva. Per altre informazioni, vedere [adozione di Windows come servizio](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> I dispositivi mobili Windows 10 non supportano CO-gestione.


### <a name="permissions-and-roles"></a>Ruoli e autorizzazioni
<!--SCCMDocs issue #667-->

| Action | Ruolo necessario |
|----|----|
| Configurare un gateway di gestione cloud in Configuration Manager | Azure **gestione della sottoscrizione** |
| Creare app di Azure AD da Configuration Manager | Azure AD **amministratore globale** |
| Importa le app di Azure in Configuration Manager | Configuration Manager **amministratore completo**<br>Nessun altro ruolo di Azure Necessito |
| Abilitare la co-gestione in Configuration Manager | Un utente di Azure AD<br>Configuration Manager **amministratore completo** con **tutte** definire l'ambito dei diritti.<!--SCCMDoc issue 626--> | 

Per altre informazioni sui ruoli di Azure, vedere [Informazioni sui diversi ruoli](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Per altre informazioni sui ruoli di Configuration Manager, vedere [nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Carichi di lavoro 

Non è necessario passare i carichi di lavoro oppure è possibile eseguirli singolarmente quando sei pronto. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro non passati a Intune e non supporta tutte le altre funzionalità di Configuration Manager che la co-gestione.

CO-gestione supporta carichi di lavoro seguenti:

- Criteri di conformità  

- Criteri di Windows Update  

- Criteri di accesso alle risorse  

- Endpoint Protection  

- Configurazione del dispositivo  

- App A portata di clic di Office  

- App client  

Per altre informazioni, vedere [carichi di lavoro](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Monitorare la co-gestione

Il dashboard di CO-gestione consente di esaminare i computer CO-gestiti nell'ambiente in uso. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.

![Schermata del dashboard di CO-gestione](media/co-management-dashboard.png)

Per altre informazioni, vedere [come monitorare la co-gestione](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Passaggi successivi

- [Altre informazioni su un valore immediato e Guida introduttiva con CO-gestione](/sccm/comanage/quickstarts)  

- [Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistente](/sccm/comanage/tutorial-co-manage-clients)  

