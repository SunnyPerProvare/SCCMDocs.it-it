---
title: Percorsi per la co-gestione
titleSuffix: Configuration Manager
description: Comprendere i prerequisiti per i due metodi principali per poter impostare la co-gestione.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755192"
---
# <a name="paths-to-co-management"></a>Percorsi per la co-gestione

Esistono due modi principali per poter configurare la co-gestione. È importante comprendere i prerequisiti per ogni percorso. Ognuna di esse richiede una combinazione di Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune e Windows 10. 

1. [Registrare automaticamente i dispositivi gestiti da Configuration Manager esistenti in Intune](#bkmk_path1)  
2. [Avviare il client di Configuration Manager con provisioning moderne](#bkmk_path2)  

![Diagramma dei percorsi di CO-gestione](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Percorso 1: Registrare automaticamente i client esistenti

Tenendo questo percorso, è possibile ottenere i dispositivi gestiti da Configuration Manager esistenti rapidamente registrati in Intune. La gestione dei dispositivi da Configuration Manager non è diversa dalla prima di abilitare la co-gestione. A questo punto si ottengono tutti i vantaggi e basato sul cloud. Questo percorso è trasparente per gli utenti.

Ecco cosa è necessario configurarlo:
- Azure AD ibrido
    - Active Directory Federation Services (ADFS) con l'autenticazione pass-through (PTA)
    - Azure AD Connect
    - Licenza di Azure AD Premium
    - Configurare ibrida di Azure AD join (scegliere una delle opzioni):
        - Per i domini gestiti
        - Per i domini federati
- Agente client l'impostazione per ibrida di Azure AD join
- Configurare la registrazione automatica dei dispositivi in Intune
- Assegnare le licenze utente di Intune
- Abilitare la co-gestione in Configuration Manager

Per un'esercitazione in questo percorso, vedere [esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistenti](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Percorso 2: Eseguire il bootstrap con provisioning moderne

Ecco cosa è necessario configurarlo:

1. [Il programma di installazione avanzata HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Creare i servizi cloud in Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurare il punto di gestione e ai client di usare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Usare Intune per distribuire il client di Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Un'esercitazione per questo percorso sarà presto disponibile.

