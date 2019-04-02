---
title: Abilitare la co-gestione
titleSuffix: Configuration Manager
description: Abilitare rapidamente la co-gestione in Configuration Manager per ottenere valore immediato.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755417"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Come abilitare la co-gestione in Configuration Manager

Quando si abilita la co-gestione, è possibile ottenere valore immediato. Quando si è pronti, è possibile avviare la transizione dei carichi di lavoro in base alle necessità del proprio ambiente.

Assicurarsi che i prerequisiti per la co-gestione siano configurati prima di avviare il processo. Per altre informazioni, vedere [Prerequisiti](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Processo

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Fare clic su **Configura la co-gestione** nella barra multifunzione per aprire **Co-management Onboarding Wizard** (Caricamento guidato della co-gestione).  

2. Nella pagina **Sottoscrizione** della procedura guidata fare clic su **Accedi**. Accedere al tenant di Intune e quindi selezionare **Avanti**.  

3. Nella pagina **Abilitazione** scegliere l'impostazione **Registrazione automatica in Intune**: **Pilota** o **Tutti**.   

    Questa azione abilita la registrazione automatica dei client in Intune per i client di Configuration Manager esistenti. Quando si sceglie **Pilota**, vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri della raccolta pilota. Questa opzione consente di abilitare la co-gestione su un subset di client per iniziare a testarla e implementarla mediante un approccio per fasi.  

    > [!Note]  
    > A partire dalla versione 1806, la registrazione automatica non è immediata per tutti i client. Questo comportamento consente una migliore scalabilità della registrazione per gli ambienti di grandi dimensioni. Configuration Manager sceglie in modo casuale la registrazione in base al numero di client. Se l'ambiente include 100.000 client, ad esempio, quando si abilita questa impostazione, la registrazione viene eseguita in più giorni.<!--1358003-->  

    In presenza di dispositivi basati su Internet già registrati in Intune, copiare la riga di comando in questa pagina. È possibile usare questa riga di comando per installare il client di Configuration Manager come app in Intune.

4. Nella pagina **Carichi di lavoro** per ogni carico di lavoro scegliere il gruppo di dispositivi da spostare per la gestione con Intune. Per altre informazioni, vedere [Carichi di lavoro](/sccm/comanage/workloads).  

    Se si vuole solo abilitare la co-gestione, non è necessario trasferire i carichi di lavoro in questo momento. È possibile trasferirli in seguito. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](/sccm/comanage/how-to-switch-workloads).  

    L'impostazione **Intune pilota** trasferisce il carico di lavoro associato solo per i dispositivi nella raccolta pilota. L'impostazione **Intune** trasferisce il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti.  

    > [!Important] 
    > Prima di trasferire eventuali carichi di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.  

5. Nella pagina **Gestione temporanea** configurare le impostazioni seguenti:  

    - **Pilota**: il gruppo pilota contiene una o più raccolte selezionate. Usare il gruppo come parte dell'implementazione a fasi della co-gestione. Iniziare con una raccolta di test di piccole dimensioni e quindi aggiungere più raccolte al gruppo pilota durante l'implementazione della co-gestione per più utenti e dispositivi. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento.  

    - **Production**: Configurare **Exclusion group** (Gruppo di esclusione) con una o più raccolte. I dispositivi che sono membri di una raccolta nel gruppo vengono esclusi dalla co-gestione.  

6. Per abilitare la co-gestione, completare la procedura guidata.  



## <a name="next-steps"></a>Passaggi successivi

Dopo avere abilitato la co-gestione, esaminare gli articoli seguenti per scoprire il valore immediato che è possibile ottenere nell'ambiente:

- [Accesso condizionale](/sccm/comanage/quickstart-conditional-access)  

- [Azioni remote da Intune](/sccm/comanage/quickstart-remote-actions)  

- [Integrità del client](/sccm/comanage/quickstart-client-health)  
