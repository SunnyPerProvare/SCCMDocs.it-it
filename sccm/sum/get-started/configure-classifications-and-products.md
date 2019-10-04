---
title: Configurare classificazioni e prodotti
titleSuffix: Configuration Manager
description: Seguire questi passaggi per configurare i prodotti e le classificazioni degli aggiornamenti software per la sincronizzazione nella console di Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/25/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7127229ceef948f4e88365255737fbe3844aa428
ms.sourcegitcommit: b9cc8e723c5d8c3be44edad24ad29d75c0cdd2b0
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826193"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>configurare le classificazioni e i prodotti per la sincronizzazione  

*Si applica a: System Center Configuration Manager (Current Branch)*

I metadati degli aggiornamenti software vengono recuperati durante il processo di sincronizzazione in Configuration Manager in base alle impostazioni specificate nelle proprietà del componente punto di aggiornamento software. Dopo la sincronizzazione degli aggiornamenti software per la prima volta o al rilascio di nuovi prodotti e classificazioni, è necessario passare alle proprietà per selezionare i nuovi elementi. Utilizzare la procedura seguente per configurare le classificazioni e i prodotti per la sincronizzazione.  

> [!NOTE]  
> Attenersi alla procedura descritta in questa sezione solo nel sito di livello superiore.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>Per configurare le classificazioni e i prodotti per la sincronizzazione  

1. Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.

2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  

3. Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.

4. Nella scheda **Classificazioni** specificare le classificazioni degli aggiornamenti software per cui si desidera sincronizzare gli aggiornamenti software.  

    Ogni aggiornamento software viene definito in base a una classificazione di aggiornamento che consente di organizzare i diversi tipi di aggiornamenti. Durante il processo di sincronizzazione, verranno sincronizzati i metadati degli aggiornamenti software per le classificazioni selezionate. Configuration Manager consente di sincronizzare gli aggiornamenti software con le classificazioni di aggiornamento seguenti:  

     - **Aggiornamenti critici**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico che risolve un bug critico non correlato alla sicurezza.  
     - **Aggiornamenti delle definizioni**: specifica un aggiornamento software frequente rilasciato pubblicamente che contiene aggiunte al database delle definizioni di un prodotto.  
     - **Feature Pack**: specifica le nuove funzionalità del prodotto distribuite prima al di fuori di una versione del prodotto e che in genere sono incluse nella successiva versione completa del prodotto.  
     - **Aggiornamenti della sicurezza**: specifica un aggiornamento rilasciato pubblicamente per una vulnerabilità specifica del prodotto correlata alla sicurezza.  
     - **Service Pack**: specifica un set cumulativo e testato di tutti gli hotfix, gli aggiornamenti della sicurezza, gli aggiornamenti critici e gli aggiornamenti applicati a un prodotto. I Service Pack possono contenere anche aggiornamenti aggiuntivi per problemi rilevati internamente dopo il rilascio del prodotto.  
     - **Strumenti:** specifica un'utilità o una funzionalità che consente di completare una o più attività.  
     - **Aggiornamenti cumulativi**: specifica un set cumulativo e testato di hotfix, aggiornamenti della sicurezza, aggiornamenti critici e aggiornamenti riuniti in un unico pacchetto per semplificarne la distribuzione. Un aggiornamento cumulativo interessa in genere un'area specifica, ad esempio la sicurezza o un componente del prodotto.  
     - **Aggiornamenti**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico. Un aggiornamento risolve un bug non critico, non correlato alla sicurezza.  
     - **Aggiornamento**: specifica un aggiornamento per le caratteristiche e le funzionalità di Windows 10. Per ottenere la classificazione di [aggiornamento](https://support.microsoft.com/kb/3095113), i punti di aggiornamento software e i siti devono eseguire WSUS 6.2 con l'**hotfix 3095113**. Per ulteriori informazioni sull'installazione di questo aggiornamento e altri **aggiornamenti** per gli aggiornamenti, vedere [prerequisiti per gli aggiornamenti software](/sccm/sum/plan-design/prerequisites-for-software-updates#BKMK_wsus2012).

    > [!NOTE] 
    > 
    > A partire da Configuration Manager versione 1706, è possibile selezionare la casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** per sincronizzare i driver di Microsoft Surface.<!--1098490--> Tutti i punti di aggiornamento software devono eseguire Windows Server 2016 per sincronizzare correttamente i driver di Surface. Se si abilita un punto di aggiornamento software in un computer che esegue Windows Server 2012 dopo aver abilitato i driver per Surface, i risultati dell'analisi per gli aggiornamenti dei driver non saranno accurati. Questo comportamento causa la visualizzazione di dati di conformità non corretti nella console di Configuration Manager e nei report di Configuration Manager.  
    >  
    > - Questa funzionalità è stata introdotta per la prima volta nella versione 1706 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1710, questa funzionalità non è più in versione non definitiva.  
    >  
    > - Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

5. Nella scheda **Prodotti** specificare i prodotti per cui si desidera sincronizzare gli aggiornamenti software e quindi fare clic su **Chiudi**.  

    - Configuration Manager archivia un elenco di prodotti e di famiglie di prodotti tra cui è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. È possibile che i prodotti e le famiglie di prodotti pubblicati dopo il rilascio di Configuration Manager non siano disponibili per la selezione finché non si completa la sincronizzazione degli aggiornamenti software, che aggiorna l'elenco di prodotti e famiglie di prodotti disponibili tra cui è possibile scegliere.  

    - I metadati per ogni aggiornamento software definiscono i prodotti per i quali l'aggiornamento è applicabile. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione, ad esempio Windows Server 2012. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Windows, di cui Windows Server 2012 è membro. È possibile specificare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti. Il tempo necessario per sincronizzare gli aggiornamenti software è direttamente proporzionale al numero di prodotti selezionati.  

    - Quando gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è stato selezionato per la sincronizzazione, tutti i prodotti vengono visualizzati nella console di Configuration Manager, anche se alcuni non sono stati selezionati. Se, ad esempio, Windows Server 2012 è l'unico sistema operativo selezionato e se un aggiornamento software si applica a Windows 8 e a Windows Server 2012, entrambi i prodotti vengono visualizzati nella console di Configuration Manager.  

    > [!NOTE]  
    > **Windows 10 versione 1903 e successive** è stato aggiunto a Microsoft Update come prodotto a sé stante, anziché all'interno del prodotto **Windows 10** come le versioni precedenti. A causa di questa modifica è necessario eseguire una serie di passaggi manuali per assicurarsi che i client visualizzino questi aggiornamenti. È stato aiutato a ridurre il numero di passaggi manuali da eseguire per il nuovo prodotto nella versione Configuration Manager 1906. <!--4682946-->
    >
    > Quando si esegue l'aggiornamento a Configuration Manager versione 1906 e il prodotto **Windows 10** è selezionato per la sincronizzazione, vengono eseguite automaticamente le azioni seguenti:
    > - Il prodotto **Windows 10 versione 1903 e successive** viene aggiunto per la sincronizzazione.
    > - Le [regole di distribuzione automatica](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process) contenenti il prodotto **Windows 10** verranno aggiornate in modo da includere **Windows 10 versione 1903 e successive**.
    > - I [piani di manutenzione](/sccm/osd/deploy-use/manage-windows-as-a-service#servicing-plan-workflow) vengono aggiornati in modo che includano il prodotto **Windows 10 versione 1903 e successive**.

## <a name="bkmk_WIfB"></a>Programma Windows Insider
<!--3556023-->
A partire da settembre 2019, è possibile aggiornare i dispositivi che eseguono le build di Windows Insider Preview con Configuration Manager. Questa modifica significa che è possibile gestire questi dispositivi senza modificare i normali processi o abilitare Windows Update for business. È possibile scaricare gli aggiornamenti delle funzionalità e gli aggiornamenti cumulativi per le compilazioni di Windows Insider Preview in Configuration Manager esattamente come qualsiasi altro aggiornamento o aggiornamento di Windows 10. Per ulteriori informazioni, vedere il post di Blog sulla [pubblicazione di aggiornamenti delle funzionalità di Windows 10 in WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054) .

Per ulteriori informazioni sul supporto di Windows insider in Configuration Manager, vedere [supporto per Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#bkmk_WIfB-support).

### <a name="prerequisites"></a>Prerequisiti

- Configuration Manager versione 1906 o successiva, configurato per la [gestione degli aggiornamenti software](/sccm/sum/plan-design/plan-for-software-updates).
- Dispositivi Windows 10 che eseguono [Windows Insider Preview Build](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-get-started).
- Raccolta contenente i dispositivi Windows Insider.

### <a name="enable-windows-insider-upgrades-and-updates"></a>Abilita aggiornamenti e aggiornamenti di Windows Insider

È necessario abilitare i prodotti e le classificazioni per gli aggiornamenti e gli aggiornamenti di Windows Insider. Gli aggiornamenti delle funzionalità per Windows Insider si trovano nel prodotto **preliminare Windows Insider** . Gli aggiornamenti cumulativi e gli altri aggiornamenti per Windows Insider saranno tuttavia inclusi nel prodotto **Windows 10, versione 1903 e successive**.

1. Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.
2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  
3. Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.
4. Nella scheda **prodotti** assicurarsi che siano selezionati i seguenti prodotti per la sincronizzazione:
    - Versione preliminare di Windows Insider
    - Windows 10 versione 1903 e successive
5. Nella scheda **classificazioni** verificare che siano selezionate le classificazioni seguenti per la sincronizzazione:
    - Aggiornamenti
    - Aggiornamenti della sicurezza
    - Aggiornamenti (facoltativo)
6. Fare clic su **OK** per chiudere **Proprietà del componente del punto di aggiornamento software**.

### <a name="upgrading-windows-insider-devices"></a>Aggiornamento dei dispositivi Windows Insider

Una volta sincronizzati gli aggiornamenti per Windows Insider, è possibile visualizzarli dalla **raccolta** > software**Windows 10 manutenzione** > di**tutti gli aggiornamenti di Windows 10**.

![Aggiornamenti delle funzionalità di Windows Insider per la manutenzione di Windows 10](media/3556023-windows-insiders-pre-release-feature-update.png)

Distribuire gli aggiornamenti delle funzionalità per Windows Insider nella raccolta di destinazione in modo analogo a qualsiasi altro aggiornamento. Tuttavia, quando si distribuiscono gli aggiornamenti delle funzionalità, è opportuno tenere presenti gli elementi seguenti:

- Questi aggiornamenti saranno applicabili a tutti i client Windows 10 1903 o versioni precedenti, con architettura, edizione e linguaggio corrispondenti.
- Esistono condizioni di licenza. la distribuzione deve accettare le condizioni per l'installazione.
- Si consiglia di utilizzare la [priorità dei thread nelle impostazioni client](/sccm/core/clients/deploy/about-client-settings#bkmk_thread-priority).
- Aggiornamento dinamico installa automaticamente gli aggiornamenti critici, incluso l'aggiornamento cumulativo più recente, direttamente da Microsoft Update. Questo comportamento inizia con aggiornamenti delle funzionalità per Windows 10 versione 1903. 
  - È possibile disabilitare in modo esplicito l' [aggiornamento dinamico nelle impostazioni client](/sccm/core/clients/deploy/about-client-settings#bkmk_du) o con un [file setupconfig. ini](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options). 
  - Per altre informazioni, vedere il post di Blog relativo all' [aggiornamento dinamico di Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) .

Per altre informazioni su come distribuire gli aggiornamenti, vedere [gestire Windows come servizio](/sccm/osd/deploy-use/manage-windows-as-a-service).


### <a name="keeping-insider-devices-up-to-date"></a>Mantenere aggiornati i dispositivi Insider

Gli aggiornamenti cumulativi per Windows Insider saranno disponibili per WSUS e per estensione per Configuration Manager. Questi aggiornamenti cumulativi verranno rilasciati con una frequenza simile a quella degli aggiornamenti cumulativi di Windows 10 versione 1903. Gli aggiornamenti cumulativi di Windows Insider si trovano nella categoria di prodotti **Windows 10, versione 1903 e versioni successive** e sono classificati come **aggiornamenti di sicurezza** o **aggiornamenti**. È possibile distribuire gli aggiornamenti cumulativi per Windows Insider usando il normale processo di aggiornamento software come l'uso di [regole di distribuzione automatica](/sccm/sum/deploy-use/automatically-deploy-software-updates) o di [distribuzioni](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)in più fasi.


## <a name="next-steps"></a>Passaggi successivi

Avviare la sincronizzazione degli aggiornamenti software per recuperare gli aggiornamenti software in base ai nuovi criteri. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).
