---
title: Gestire le distribuzioni ad alto rischio
titleSuffix: Configuration Manager
description: Informazioni su come configurare le impostazioni del sito di verifica della distribuzione in Configuration Manager per avvisare gli amministratori nel caso in cui creino una distribuzione ad alto rischio.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4d617bdea9c63010c96cef6f91e5123b27641e9
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62250546"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Impostazioni per gestire le distribuzioni ad alto rischio per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Con Configuration Manager è possibile configurare le impostazioni del sito di verifica della distribuzione. Queste impostazioni avvisano gli amministratori se creano una distribuzione di sequenza di attività ad alto rischio. Una distribuzione ad alto rischio è:  

-   Una distribuzione che viene installata automaticamente  

-   Una distribuzione che può causare potenzialmente risultati indesiderati  

Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** che distribuisce un sistema operativo viene considerata come distribuzione ad alto rischio.  

Per ridurre l'incidenza di distribuzioni ad alto rischio indesiderate, è possibile configurare limiti di dimensioni nelle impostazioni di verifica della distribuzione seguenti:  

- **Limiti delle dimensioni della raccolta**: quando si crea una distribuzione, nascondere le raccolte che includono più client del limite consentito.  

  - **Dimensioni predefinite**: quando si crea una distribuzione, per impostazione predefinita, questa impostazione nasconde le raccolte che includono più client rispetto a questo limite. È comunque possibile visualizzare queste raccolte durante la creazione della distribuzione, ma sono nascoste per impostazione predefinita. Il valore predefinito è **100**. Per ignorare questa impostazione, immettere un valore pari a **0**.  

  - **Dimensioni massime**: quando si crea una distribuzione, questa impostazione nasconde sempre le raccolte con più client rispetto a questo limite. Il valore predefinito è **0**, che consente di ignorare l'impostazione. Il valore per **Dimensioni massime** deve essere superiore al valore per **Dimensione predefinita** .  

    Ad esempio, si imposta **Dimensioni predefinite** su 100 e **Dimensioni massime** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** vengono visualizzate solo le raccolte che includono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  

- **Raccolte con i server del sistema del sito**: quando la raccolta di destinazione contiene un computer con un ruolo del sistema del sito, bloccare le distribuzioni o richiedere la verifica prima della creazione della distribuzione. Quando viene bloccata una distribuzione, selezionare una raccolta diversa che soddisfi i criteri di verifica della distribuzione per continuare a creare la distribuzione.  

> [!NOTE]  
>  Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**.  

### <a name="configure-deployment-verification-for-a-site"></a>Configurare la verifica della distribuzione per un sito  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito**, selezionare **Siti** e quindi selezionare il sito primario da configurare.  

2.  Fare clic su **Proprietà** nella barra multifunzione e quindi passare alla scheda **Verifica della distribuzione**.  

3.  Dopo aver impostato le configurazioni da usare, fare clic su **OK** per salvare la configurazione.  


### <a name="see-also"></a>Vedere anche  
 [Configurare siti e gerarchie](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)
