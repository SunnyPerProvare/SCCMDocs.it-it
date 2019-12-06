---
title: Configurare il risparmio energia
titleSuffix: Configuration Manager
description: Configurare il risparmio energia in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f76cf68cc007a5cefb323828752186ded62ad5f
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "70902917"
---
# <a name="configure-power-management-in-configuration-manager"></a>Configurare il risparmio energia in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra come configurare il risparmio energia in Configuration Manager.

## <a name="enable-and-configure-client-settings"></a>Abilitare e configurare le impostazioni client

Questa procedura consente di configurare le *impostazioni client predefinite* per il risparmio energia. Si applica a tutti i computer nella gerarchia.

Per applicare queste impostazioni solo ad alcuni computer, creare un'*impostazione client di dispositivo personalizzata*. Assegnarla quindi a una raccolta che contiene i computer per il risparmio energia. Per altre informazioni, vedere [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings).  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, selezionare il nodo **Impostazioni client** e quindi selezionare **Impostazioni client predefinite**.

1. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

1. Selezionare il gruppo **Risparmio energia**.  

1. Abilitare l'impostazione client **Consentire il risparmio energia dei dispositivi**.

1. Configurare le ulteriori impostazioni client necessarie. Per altre informazioni, vedere [Informazioni sulle impostazioni client - Risparmio energia](/sccm/core/clients/deploy/about-client-settings#power-management).  

I client verranno configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Come gestire i client](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Escludere computer

È possibile evitare che raccolte di computer specifiche ricevano impostazioni di risparmio energia. Se un computer è membro di *qualsiasi* raccolta esclusa dalle impostazioni di risparmio energia, tale computer non applica le impostazioni di risparmio energia. Questo comportamento si applica anche se è un membro di un'altra raccolta che applica impostazioni di risparmio energia.  

Può essere necessario escludere i computer dal risparmio energia per i motivi seguenti:  

- Un requisito aziendale impone che i computer siano sempre attivi.  

- Esiste una raccolta di controllo di computer alla quale non si vogliono applicare le impostazioni di risparmio energia.  

- Alcuni computer non sono in grado di applicare impostazioni di risparmio energia.  

- Si vogliono escludere dalla funzionalità di risparmio energia i computer che eseguono Windows Server.  

> [!NOTE]  
> Se si configura l'impostazione client **Consentire agli utenti di escludere il dispositivo usato dal risparmio energia**, gli utenti possono escludere i propri computer dal risparmio energia tramite Software Center.  

Per individuare i computer esclusi dal risparmio energia, eseguire il report **Computer esclusi**. Per altre informazioni su questo report, vedere [Come monitorare e pianificare il risparmio energia](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management#BKMK_Excluded).  

> [!IMPORTANT]  
> L'esclusione di un computer dal risparmio energia causa il ripristino dei valori originali per tutte le impostazioni di risparmio energia. Non è possibile ripristinare i valori originali per singole impostazioni di risparmio energia.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Come escludere una raccolta di computer dal risparmio energia  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Raccolte dispositivi**.  

1. Selezionare la raccolta che si vuole escludere dal risparmio energia. Nella scheda **Home** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

1. Passare alla scheda **Risparmio energia** e selezionare **Non applicare mai le impostazioni di risparmio energia ai computer di questa raccolta**.  

## <a name="next-steps"></a>Passaggi successivi

[Come creare e applicare combinazioni per il risparmio di energia](/sccm/core/clients/manage/power/create-and-apply-power-plans)

[Come monitorare e pianificare il risparmio energia](/sccm/core/clients/manage/power/monitor-and-plan-for-power-management)
