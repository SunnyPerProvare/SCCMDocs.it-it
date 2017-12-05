---
title: Gestire le distribuzioni ad alto rischio
titleSuffix: Configuration Manager
description: Informazioni su come configurare le impostazioni del sito in System Center Configuration Manager per avvisare gli amministratori nel caso in cui creino una distribuzione ad alto rischio.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 96855503183c1f9a3b51c5861ca661089f3c2994
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Impostazioni per gestire le distribuzioni ad alto rischio per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Con System Center Configuration Manager è possibile configurare le impostazioni del sito in modo da avvisare gli amministratori se creano una distribuzione di sequenze di attività ad alto rischio. Una distribuzione ad alto rischio è:  

-   Una distribuzione che viene installata automaticamente  

-   Una distribuzione che può causare potenzialmente risultati indesiderati  

 Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** che distribuisce un sistema operativo viene considerata come distribuzione ad alto rischio.  

 Per ridurre l'incidenza di distribuzioni ad alto rischio indesiderate, è possibile configurare limiti di dimensioni nelle impostazioni di verifica della distribuzione seguenti:  

-   **Limiti delle dimensioni della raccolta**: nascondere raccolte che contengono più client del limite consentito quando si crea una distribuzione.  

    -   **Dimensioni predefinite**: per impostazione predefinita, questa impostazione nasconde le raccolte con più client rispetto al limite impostato in fase di creazione della distribuzione. È comunque possibile visualizzare queste raccolte durante la creazione della distribuzione, ma sono nascoste per impostazione predefinita. Il valore predefinito è 100. Immettere un valore pari a 0 per ignorare questa impostazione.  

    -   **Dimensioni massime**: questa impostazione nasconde sempre le raccolte con più client del limite definito in fase di creazione della distribuzione. Il valore predefinito è 0, che consente di ignorare l'impostazione. Il valore per **Dimensioni massime** deve essere superiore al valore per **Dimensione predefinita** .  

     Ad esempio, si imposta **Dimensioni predefinite** su 100 e **Dimensioni massime** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** verranno visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  

-   **Raccolte con i server del sistema del sito**: bloccare le distribuzioni o richiedere la verifica prima della creazione della distribuzione, quando la raccolta di destinazione contiene un computer con un ruolo del sistema del sito. Quando viene bloccata una distribuzione, è necessario selezionare una raccolta diversa che soddisfi i criteri di verifica della distribuzione.  

> [!NOTE]  
>  Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Per configurare la verifica della distribuzione per un sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** >**Configurazione del sito** > **Siti** e quindi selezionare il sito primario da configurare.  

2.  Nella scheda **Home** nel gruppo **Proprietà** fare clic su **Proprietà** e quindi sulla scheda **Verifica della distribuzione**.  

3.  Dopo aver impostato le configurazioni da usare, fare clic su **OK** per salvare la configurazione.  

### <a name="see-also"></a>Vedere anche  
 [Configure sites and hierarchies for System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md) (Configurare siti e gerarchie per System Center Configuration Manager)
