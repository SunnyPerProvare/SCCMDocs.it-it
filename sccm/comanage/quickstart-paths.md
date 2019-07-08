---
title: Percorsi per la co-gestione
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per i due metodi principali per configurare la co-gestione.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c34cf73133086f08cb390f39ab4fe715dfcefd2
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550678"
---
# <a name="paths-to-co-management"></a>Percorsi per la co-gestione

Esistono due modi principali per configurare la co-gestione. È importante conoscere i prerequisiti per ogni percorso. Ognuno di essi richiede una combinazione di Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune e Windows 10. 

1. [Registrare automaticamente i dispositivi gestiti da Configuration Manager esistenti in Intune](#bkmk_path1)  
2. [Eseguire il bootstrap del client di Configuration Manager con provisioning moderno](#bkmk_path2)  

![Diagramma dei percorsi di co-gestione](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Percorso 1: Registrare automaticamente i client esistenti

Scegliendo questo percorso è possibile registrare rapidamente i dispositivi gestiti da Configuration Manager esistenti in Intune. La gestione di questi dispositivi da Configuration Manager non è diversa rispetto a prima di abilitare la co-gestione. In questo modo si ottengono tutti i vantaggi del cloud. Questo percorso è trasparente per gli utenti.

Prerequisiti per la configurazione:
- Azure AD ibrido
    - Una delle [opzioni di identità ibrida di Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin) seguenti:  
       - [Sincronizzazione dell'hash delle password](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) con l'[accesso Single Sign-On facile](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Autenticazione pass-through](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) con l'[accesso Single Sign-On facile](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [SSO federato (con Active Directory Federation Services (AD FS))](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Licenza Azure AD Premium
    - Configurare l'aggiunta ad Azure AD ibrido (scegliere una delle opzioni):
        - Per i domini gestiti
        - Per i domini federati
- Impostazione dell'agente client per l'aggiunta ad Azure AD ibrido
- Configurare la registrazione automatica dei dispositivi in Intune
- Assegnare le licenze utente di Intune
- Abilitare la co-gestione in Configuration Manager

Per un'esercitazione dedicata a questo percorso, vedere [Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistenti](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Percorso 2: Eseguire il bootstrap con provisioning moderno

Prerequisiti per la configurazione:

1. [Configurare HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Creare i servizi cloud in Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurare il punto di gestione e i client per usare Cloud Management Gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Usare Intune per distribuire il client di Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Un'esercitazione per questo percorso sarà presto disponibile.

