---
title: Prerequisiti per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Informazioni sui prerequisiti per gli aggiornamenti software in System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: ffe1546e3d7561a0bbda787ef6b1aaeac6e8d2e0
ms.sourcegitcommit: 2504617dc4db90e205327d06cab32f050e88dbf2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505126"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Prerequisiti per gli aggiornamenti software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo elenca i prerequisiti per gli aggiornamenti software in System Center Configuration Manager. Per ognuno di essi, le dipendenze esterne e interne sono elencate in tabelle separate.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dipendenze aggiornamenti software esterne a Configuration Manager  
 Le sezioni seguenti elencano le dipendenze esterne per gli aggiornamenti software.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) deve essere installato nei server di sistema del sito per eseguire il punto di aggiornamento software, il punto di gestione e il punto di distribuzione. Per altre informazioni, vedere [Prerequisiti per i ruoli di sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) è necessario per la sincronizzazione degli aggiornamenti software e per l'analisi dell'applicabilità degli aggiornamenti software nei client. È necessario installare il server WSUS prima di creare il ruolo del punto di aggiornamento software. Per un punto di aggiornamento software sono supportate le versioni di WSUS seguenti:  

-   WSUS 10.0 (ruolo in Windows Server 2016)
-   WSUS 6.2 e 6.3 (ruolo in Windows Server 2012 e Windows Server 2012 R2)

>[!NOTE]
>-   A partire dalla versione 1702, Windows Server 2008 R2 non è supportato per il ruolo del punto di aggiornamento software. Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).  

Quando esistono più punti di aggiornamento software in un sito, verificare che tutti eseguano la stessa versione di WSUS.  

> [!WARNING]  
>  La classificazione degli aggiornamenti software **Aggiornamenti** è supportata solo a partire da WSUS 4.0. Prima di sincronizzare questa nuova classificazione e avere la possibilità di valutare i computer Windows 10 in un piano di manutenzione di Windows 10, è fondamentale installare l'[hotfix 3095113](https://support.microsoft.com/kb/3095113) per WSUS nei punti di aggiornamento software e nei server del sito. Questo hotfix consente a WSUS in un server basato su Windows Server 2012 o su Windows Server 2012 R2 di sincronizzare e distribuire gli aggiornamenti di funzionalità per Windows 10. Per altre informazioni, vedere [Gestire Windows come servizio](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Se si sincronizzano gli aggiornamenti software con la classificazione di **Aggiornamenti** prima di installare l' [hotfix 3095113](https://support.microsoft.com/kb/3095113), vedere [Per ripristinare la sincronizzazione della classificazione Aggiornamenti prima di installare KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Console di amministrazione di WSUS  
 È necessaria la console di amministrazione di WSUS nel server del sito di Configuration Manager se il punto di aggiornamento software si trova in un server di sistema del sito remoto e WSUS non è ancora stato installato nel server del sito.  

> [!IMPORTANT]  
> La versione di WSUS nel server del sito deve corrispondere alla versione di WSUS in esecuzione nei punti di aggiornamento software.
>
> Non usare la console di amministrazione di WSUS per configurare le impostazioni WSUS. Configuration Manager si connette all'istanza di WSUS in esecuzione nel punto di aggiornamento software e configura le impostazioni appropriate.  



### <a name="windows-update-agent"></a>Agente di Windows Update  
 È necessario che il client dell'agente di Windows Update (WUA) sia presente nei client in modo che questi possano connettersi al server WSUS. WUA recupera l'elenco di aggiornamenti software che devono essere esaminati per verificare la conformità.  

 Quando si installa Configuration Manager, viene scaricata la versione più recente di dell'agente di Windows Update. Quando viene installato il client di Configuration Manager, l'agente di Windows Update viene aggiornato se necessario. Tuttavia, se l'installazione non riesce, è necessario usare un metodo diverso per eseguire l'aggiornamento dell'agente di Windows Update.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dipendenze aggiornamenti software interne a Configuration Manager  
 Le sezioni seguenti elencano le dipendenze interne per gli aggiornamenti software in Configuration Manager.  

### <a name="management-points"></a>Punti di gestione  
 I punti di gestione trasferiscono le informazioni tra i computer client e il sito di Configuration Manager. I punti di gestione sono necessari per gli aggiornamenti software.  

### <a name="software-update-points"></a>Punti di aggiornamento software  
 È necessario installare un punto di aggiornamento software nel server WSUS per poter distribuire gli aggiornamenti software in Configuration Manager. Per altre informazioni, vedere [Installare e configurare un punto di aggiornamento software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Punti di distribuzione  
 I punti di distribuzione sono necessari per archiviare il contenuto per gli aggiornamenti software. Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Impostazioni client per gli aggiornamenti software  
 Per impostazione predefinita, gli aggiornamenti software sono abilitati per i client. Tuttavia, sono disponibili altre impostazioni che controllano come e quando i client valutano la conformità per gli aggiornamenti software e la relativa modalità di installazione.  

 Per altre informazioni, vedere gli articoli seguenti:  

-   [Impostazioni client per gli aggiornamenti software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [Informazioni sulle impostazioni client per gli aggiornamenti software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Punti di Reporting Services  
 Il ruolo del sistema del sito del punto di Reporting Services può visualizzare i report per gli aggiornamenti software. Questo ruolo è facoltativo ma consigliato. Per altre informazioni su come creare un punto di Reporting Services, vedere [Configurazione della creazione di report](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Ripristinare la sincronizzazione della categoria Aggiornamenti prima di installare KB 3095113  
 È necessario l' [hotfix 3095113](https://support.microsoft.com/kb/3095113) per WSUS nei punti di aggiornamento software e sui server del sito prima della sincronizzazione della classificazione **Aggiornamenti** . Se l'hotfix non viene installato quando si abilita la classificazione **Aggiornamenti**, WSUS rileva l'aggiornamento delle funzionalità della build 1511 di Windows 10 anche se non riesce a scaricare e distribuire correttamente i pacchetti associati. 
 
 Se si sincronizzano gli eventuali aggiornamenti senza avere prima installato l'[hotfix 3095113](https://support.microsoft.com/kb/3095113), nel database WSUS (SUSDB) vengono inseriti dati inutilizzabili. Tali dati devono essere cancellati prima di poter distribuire correttamente gli aggiornamenti. Per risolvere questo problema, seguire la procedura riportata di seguito.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Per ripristinare la sincronizzazione della classificazione Aggiornamenti prima di installare KB 3095113  

1.  Eliminare gli aggiornamenti software con la classificazione **Aggiornamenti**. È possibile usare uno script di PowerShell simile allo script di esempio riportato di seguito:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Prima di procedere con il passaggio successivo, è necessario eseguire lo script in tutti i punti di aggiornamento software nella gerarchia di Configuration Manager.  

     Per eliminare in blocco gli aggiornamenti software con la classificazione **Aggiornamenti**, è possibile modificare lo script di PowerShell in modo da leggere più GUID da un file di testo.  

2.  Deselezionare la classificazione **Aggiornamenti** nelle proprietà del componente del punto di aggiornamento software. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti](../get-started/configure-classifications-and-products.md). A questo punto avviare la sincronizzazione degli aggiornamenti software. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](../get-started/synchronize-software-updates.md).  

3.  Installare l'are l' [hotfix 3095113](https://support.microsoft.com/kb/3095113) per WSUS nei punti di aggiornamento software e nei server del sito.  

4.  Selezionare la classificazione **Aggiornamenti** nelle proprietà del componente del punto di aggiornamento software. Per altre informazioni, vedere [Configurare le classificazioni e i prodotti](../get-started/configure-classifications-and-products.md). A questo punto avviare la sincronizzazione degli aggiornamenti software. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](../get-started/synchronize-software-updates.md).  

## <a name="next-steps"></a>Passaggi successivi
[Preparare la gestione degli aggiornamenti software](../get-started/prepare-for-software-updates-management.md)
