---
title: Pubblicare i dati del sito | Microsoft Docs
description: Informazioni su come pubblicare i siti di Configuration Manager in Active Directory Domain Services.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: e7629fdf7fdf615fa27894158c3d101432c95a04
ms.openlocfilehash: bcfb002c503485f03ba27d7346acb61d0d3c6087
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Pubblicare i dati del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver esteso lo schema di Active Directory per System Center Configuration Manager, è possibile pubblicare i siti di Configuration Manager in Active Directory Domain Services. I computer di Active Directory possono così recuperare in modo sicuro le informazioni dei siti da una fonte attendibile. Anche se non è necessaria per la funzionalità di base di Configuration Manager, la pubblicazione delle informazioni del sito in Active Directory Domain Services può ridurre il carico amministrativo.  

-   **Quando un sito è configurato per la pubblicazione in Active Directory Domain Services**, i client di Configuration Manager possono trovare automaticamente i punti di gestione tramite la pubblicazione in Active Directory usando una query LDAP in un server di catalogo globale.  

-   **Quando un sito non viene pubblicato per Active Directory Domain Services**, i client devono avere un meccanismo alternativo per trovare il punto di gestione predefinito.  

Per informazioni su come i client trovano un punto di gestione, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurare i siti da pubblicare in Active Directory Domain Services  
 Di seguito sono indicati i passaggi generali:  

-   È necessario [estendere lo schema di Active Directory per System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) in ogni foresta in cui verranno pubblicati i dati del sito. Assicurarsi inoltre che sia presente il contenitore **System Management**.  

-   All'account computer di ogni sito primario che pubblicherà i dati è necessario concedere i diritti di tipo **Controllo completo** sul contenitore **System Management** e su tutti i relativi oggetti figlio.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Per abilitare la pubblicazione delle informazioni di un sito di Configuration Manager nella foresta Active Directory

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**e fare clic su **Siti**. Selezionare il sito per il quale si vuole abilitare la pubblicazione dei dati. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

3.  Nella scheda **Pubblicazione** delle proprietà del sito selezionare le foreste in cui verranno pubblicati i dati del sito.  

4.  Fare clic su **OK** per salvare la configurazione.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Per configurare le foreste Active Directory per la pubblicazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , fare clic su **Foreste Active Directory**. Se in precedenza è stato eseguito il metodo di individuazione foresta Active Directory, è possibile visualizzare ogni foresta rilevata nel riquadro dei risultati. La foresta locale e qualsiasi foresta trusted vengono individuate durante l'esecuzione del metodo di individuazione foresta Active Directory. È necessario aggiungere manualmente solo le foreste non trusted.  

    -   Per configurare una foresta individuata in precedenza, selezionarla nel riquadro dei risultati. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà** per aprire le proprietà della foresta. Procedere al passaggio 3.  

    -   Per configurare una nuova foresta non presente nell'elenco, nella scheda **Home**, nel gruppo **Crea**, fare clic su **Aggiungi foresta** per aprire la finestra di dialogo **Aggiungi foreste**. Procedere al passaggio 3.  

3.  Nella scheda **Generale** completare le configurazioni per la foresta che si vuole individuare e specificare un valore per **Account foresta Active Directory**.  

    > [!NOTE]  
    >  Il metodo di individuazione della foresta Active Directory richiede un account globale per l'individuazione e la pubblicazione in foreste non trusted. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

4.  Se si prevede di autorizzare i siti alla pubblicazione dei relativi dati in questa foresta, completare le configurazioni per la pubblicazione in questa foresta nella scheda **Pubblicazione** .  

    > [!NOTE]  
    >  Se si abilita la pubblicazione di siti in una foresta, è necessario estendere lo schema di Active Directory di tale foresta per Configuration Manager. L'account foresta Active Directory deve disporre delle autorizzazioni di tipo Controllo completo sul contenitore di sistema di tale foresta.  

5.  Dopo aver completato la configurazione di questa foresta per l'utilizzo con il metodo di individuazione della foresta Active Directory, fare clic su **OK** per salvare la configurazione.  

