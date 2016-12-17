---
title: Installare ruoli del sistema del sito | System Center Configuration Manager
description: Le procedure guidate consentono di aggiungere ruoli del sistema del sito a un server del sistema del sito esistente nel sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 780ef516ddc641d53e1d2d4a5f559795cfd22cbb

---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Installare ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La console di System Center Configuration Manager include due procedure guidate che è possibile usare per installare i ruoli del sistema del sito:  

-   **Aggiunta guidata ruoli del sistema del sito**: Utilizzare questa procedura guidata per aggiungere ruoli del sistema del sito a un server del sistema del sito esistente nel sito.  

-   **Creazione guidata server del sistema sito**: Utilizzare questa procedura guidata per specificare un nuovo server come server del sistema del sito, quindi installare uno o più ruoli del sistema del sito nel server. La procedura guidata è analoga alla procedura **Aggiunta guidata ruoli del sistema del sito**a eccezione della necessità di specificare nella prima pagina il nome del server da utilizzare e il sito in cui eseguire l'installazione.  

Quando un ruolo del sistema del sito viene installato in un computer remoto (compresa un'istanza del provider SMS), l'account computer del computer remoto viene aggiunto a un gruppo locale nel server del sito. Quando il sito viene installato in un controller di dominio, il gruppo nel server del sito è un gruppo di dominio anziché un gruppo locale e il ruolo del sistema del sito remoto non è operativo fino al riavvio del computer del ruolo del sistema del sito o all'aggiornamento del ticket Kerberos per l'account computer remoti. Vedere [Accounts used in System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md) (Account usati in System Center Configuration Manager).  

Prima di installare il ruolo del sistema del sito Configuration Manager controlla il computer di destinazione per garantire che soddisfi i prerequisiti previsti per il ruolo del sistema del sito selezionato. Durante l'installazione dei ruoli del sistema del sito:  

-   Per impostazione predefinita, quando Configuration Manager installa un ruolo del sistema del sito, i file di installazione vengono installati nella prima unità disco NTFS con la maggiore quantità di spazio su disco disponibile. Per evitare l'installazione di Configuration Manager in unità specifiche, creare un file vuoto denominato **no_sms_on_drive.sms** e copiarlo nella cartella radice dell'unità prima dell'installazione del server del sistema del sito.  

-   Per installare i ruoli del sistema del sito Configuration Manager usa l'**account di installazione del sistema del sito**. È possibile specificare questo account quando si esegue la procedura guidata applicabile per creare un nuovo server del sistema del sito o aggiungere ruoli del sistema del sito a un server del sistema del sito esistente. Per impostazione predefinita, questo account è l'account del sistema locale del computer del server del sito, ma è possibile specificare un account utente di dominio da usare come l'account di installazione del sistema di sito. Per altre informazioni, vedere Site System Installation Account (Account di installazione del sistema del sito) nell'argomento [Accounts used in System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md) (Account usati in System Center Configuration Manager).  

##  <a name="a-namebkmkinstalla-to-install-site-system-roles-on-an-existing-site-system-server"></a><a name="bkmk_Install"></a> Per installare i ruoli del sistema del sito in un server del sistema del sito esistente  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, fare clic su **Server e ruoli del sistema del sito**, quindi selezionare il server che si desidera utilizzare per i nuovi ruoli del sistema del sito.  

3.  Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Per accedere al ruolo del sistema del sito da Internet, assicurarsi di specificare un FQDN Internet.  

5.  Nella pagina **Proxy** specificare le impostazioni per un server proxy se i ruoli del sistema del sito in esecuzione in questo server del sistema del sito richiedono un server proxy per la connessione ai percorsi in Internet, quindi fare clic su **Avanti**.  

6.  Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere, quindi fare clic su **Avanti**.  

7.  Completare la procedura guidata.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell, New-CMSiteSystemServer, esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) nella documentazione di riferimento dei cmdlet di System Center Configuration Manager 2012 SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Per installare i ruoli del sistema del sito in un nuovo server del sistema del sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**e quindi fare clic su **Server e ruoli del sistema del sito**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Per accedere al nuovo ruolo del sistema del sito da Internet, assicurarsi di specificare un FQDN Internet.  

5.  Nella pagina **Proxy** specificare le impostazioni per un server proxy se i ruoli del sistema del sito in esecuzione in questo server del sistema del sito richiedono un server proxy per la connessione ai percorsi in Internet, quindi fare clic su **Avanti**.  

6.  Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere, quindi fare clic su **Avanti**.  

7.  Completare la procedura guidata.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell, New-CMSiteSystemServer, esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) nella documentazione di riferimento dei cmdlet di System Center Configuration Manager 2012 SP1.  



<!--HONumber=Nov16_HO1-->

