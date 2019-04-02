---
title: Percorsi per la co-gestione
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per i due metodi principali per configurare la co-gestione.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803f05dd14da8d280f08f2bcf3608865f384d273
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755192"
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
    - Active Directory Federation Services (AD FS) con l'autenticazione pass-through (PTA)
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

