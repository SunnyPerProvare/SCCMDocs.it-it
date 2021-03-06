---
title: Installare i ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Le procedure guidate consentono di aggiungere ruoli del sistema del sito a un server del sistema del sito esistente nel sito.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4ec74f030dc216d85c9c9f52453d9c742a9abd39
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75798672"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Installare ruoli del sistema del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La console di Configuration Manager include due procedure guidate che è possibile usare per installare i ruoli del sistema del sito:  

-   **Aggiunta guidata ruoli del sistema del sito**: usare questa procedura guidata per aggiungere ruoli del sistema del sito a un server del sistema del sito esistente nel sito.  

-   **Creazione guidata server del sistema sito**: usare questa procedura guidata per specificare un nuovo server come server del sistema del sito, quindi installare uno o più ruoli del sistema del sito nel server. La procedura guidata è analoga alla procedura **Aggiunta guidata ruoli del sistema del sito**a eccezione della necessità di specificare nella prima pagina il nome del server da utilizzare e il sito in cui eseguire l'installazione.  

Quando un ruolo del sistema del sito viene installato in un computer remoto (compresa un'istanza del provider SMS), l'account computer del computer remoto viene aggiunto a un gruppo locale nel server del sito. Quando il sito viene installato in un controller di dominio, il gruppo nel server del sito è un gruppo di dominio anziché locale. In questo caso, il ruolo del sistema del sito remoto non è operativo fino al riavvio del computer del ruolo del sistema del sito o all'aggiornamento del ticket Kerberos per l'account del computer remoto. Per altre informazioni, vedere [Account usati](../../../../core/plan-design/hierarchy/accounts.md).  

Prima di installare il ruolo del sistema del sito Configuration Manager controlla il computer di destinazione per garantire che soddisfi i prerequisiti previsti per il ruolo del sistema del sito selezionato. Tenere presente quanto segue riguardo all'installazione dei ruoli del sistema del sito:  

-   Per impostazione predefinita, quando Configuration Manager installa un ruolo del sistema del sito, i file di installazione vengono installati nella prima unità disco NTFS con la maggiore quantità di spazio su disco disponibile. Per evitare che Configuration Manager venga installato in unità specifiche, creare un file vuoto denominato **no_sms_on_drive.sms** e copiarlo nella cartella radice dell'unità prima di installare il server del sistema del sito.  

-   Per installare i ruoli del sistema del sito Configuration Manager usa l'**account di installazione del sistema del sito**. È possibile specificare questo account quando si esegue la procedura guidata applicabile per creare un nuovo server del sistema del sito o aggiungere ruoli del sistema del sito a un server del sistema del sito esistente. Per impostazione predefinita, questo account è l'account del sistema locale del computer del server del sito, ma è possibile specificare un account utente di dominio da usare come l'account di installazione del sistema di sito. Per altre informazioni, vedere [Account usati](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="bkmk_Install"></a> Per installare i ruoli del sistema del sito in un server del sistema del sito esistente  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**e quindi fare clic su **Server e ruoli del sistema del sito**. Selezionare quindi il server che si vuole usare per i nuovi ruoli del sistema del sito.  

3.  Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Per accedere al ruolo del sistema del sito da Internet, assicurarsi di specificare un nome di dominio completo (FQDN) Internet.  

5.  Nella pagina **Proxy** specificare le impostazioni per un server proxy se i ruoli del sistema del sito in esecuzione nel server del sistema del sito richiedono un server proxy per la connessione ai percorsi Internet. Fare quindi clic su **Avanti**.  

6.  Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere, quindi fare clic su **Avanti**.  

7.  Completare la procedura guidata.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell, New-CMSiteSystemServer, esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](https://go.microsoft.com/fwlink/p/?LinkID=271414) nella documentazione di riferimento dei cmdlet di System Center Configuration Manager 2012 SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Per installare i ruoli del sistema del sito in un nuovo server del sistema del sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**e quindi fare clic su **Server e ruoli del sistema del sito**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Per accedere al nuovo ruolo del sistema del sito da Internet, assicurarsi di specificare un FQDN Internet.  

5.  Nella pagina **Proxy** specificare le impostazioni per un server proxy se i ruoli del sistema del sito in esecuzione nel server del sistema del sito richiedono un server proxy per la connessione ai percorsi Internet. Fare quindi clic su **Avanti**.  

6.  Nella pagina **Selezione ruolo del sistema** selezionare i ruoli del sistema del sito da aggiungere, quindi fare clic su **Avanti**.  

7.  Completare la procedura guidata.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell, New-CMSiteSystemServer, esegue la stessa funzione di questa procedura. Per altre informazioni, vedere [New-CMSiteSystemServer](https://go.microsoft.com/fwlink/p/?LinkID=271414) nella documentazione di riferimento dei cmdlet di System Center Configuration Manager 2012 SP1.  
