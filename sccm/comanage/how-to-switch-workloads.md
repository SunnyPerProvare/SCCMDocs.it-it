---
title: Passare i carichi di lavoro di CO-gestione
titleSuffix: Configuration Manager
description: Informazioni su come passare i carichi di lavoro attualmente gestiti da Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755441"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Viene illustrato come passare i carichi di lavoro di Configuration Manager a Intune

Uno dei vantaggi di CO-gestione è il passaggio dei carichi di lavoro da Configuration Manager a Microsoft Intune. Quando un dispositivo Windows 10 è il client di Configuration Manager e viene registrato in Intune, si ottengono i vantaggi di entrambi i servizi. Controllare quali carichi di lavoro, se presente, che si passa l'autorità da Configuration Manager a Intune. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro non passati a Intune e non supporta tutte le altre funzionalità di Configuration Manager che la co-gestione.

Per altre informazioni sui carichi di lavoro supportati, vedere [carichi di lavoro](/sccm/comanage/workloads).

È possibile passare i carichi di lavoro quando si abilita la co-gestione, o in seguito quando si è pronti. Se è già stata abilitata CO-gestione, eseguire prima di tutto. Per altre informazioni, vedere [come abilitare la co-gestione](/sccm/comanage/how-to-enable).


Dopo aver abilitato la co-gestione, modificare le impostazioni nelle proprietà della co-gestione. 

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Selezionare l'oggetto di CO-gestione e quindi scegliere **proprietà** nella barra multifunzione.  

3. Passare al **carichi di lavoro** scheda. Per impostazione predefinita, tutti i carichi di lavoro configurati per il **Configuration Manager** impostazione. Per passare un carico di lavoro, spostare il controllo dispositivo di scorrimento per tale carico di lavoro per l'impostazione desiderata.  

    ![Scheda screenshot di carichi di lavoro nella pagina delle proprietà di CO-gestione](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager continua a gestire questo carico di lavoro.  

    - **Avviare un programma pilota di Intune**: Passare questo carico di lavoro solo per i dispositivi nella raccolta pilota. È possibile modificare il **raccolta pilota** nel **Staging** scheda della pagina delle proprietà di CO-gestione.  

    - **Intune**: Passare questo carico di lavoro per tutti i dispositivi Windows 10 registrati in CO-gestione.  


> [!Important]  
> Prima di passare i carichi di lavoro, assicurarsi configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.  

<!--1357377--> A partire da Configuration Manager versione 1806, quando si passa a un altro carico di lavoro con co-gestione, i dispositivi in co-gestione sincronizzano automaticamente i criteri MDM da Microsoft Intune. La sincronizzazione si verifica anche quando si avvia l'azione **Scarica criteri computer** dalle notifiche client nella console di Configuration Manager. Per altre informazioni, vedere [Avviare il recupero dei criteri client usando la notifica client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


