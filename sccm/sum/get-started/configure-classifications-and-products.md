---
title: Configurare classificazioni e prodotti
titleSuffix: Configuration Manager
description: Seguire questi passaggi per configurare i prodotti e le classificazioni degli aggiornamenti software per la sincronizzazione nella console di Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/15/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1d984598288434aa1e81c6bd2c51a315edfa551
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405693"
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>configurare le classificazioni e i prodotti per la sincronizzazione  

*Si applica a: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  Attenersi alla procedura descritta in questa sezione solo nel sito di livello superiore.  

 I metadati degli aggiornamenti software vengono recuperati durante il processo di sincronizzazione in Configuration Manager in base alle impostazioni specificate nelle proprietà del componente punto di aggiornamento software. Dopo la sincronizzazione degli aggiornamenti software per la prima volta o al rilascio di nuovi prodotti e classificazioni, è necessario passare alle proprietà per selezionare i nuovi elementi. Utilizzare la procedura seguente per configurare le classificazioni e i prodotti per la sincronizzazione.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Per configurare le classificazioni e i prodotti per la sincronizzazione  

1.  Nella console di **Configuration Manager** passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.

2. Selezionare il sito di amministrazione centrale o il sito primario autonomo.  

3.  Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**.

4.  Nella scheda **Classificazioni** specificare le classificazioni degli aggiornamenti software per cui si desidera sincronizzare gli aggiornamenti software.  

    > [!NOTE]  
    >  Ogni aggiornamento software viene definito in base a una classificazione di aggiornamento che consente di organizzare i diversi tipi di aggiornamenti. Durante il processo di sincronizzazione, verranno sincronizzati i metadati degli aggiornamenti software per le classificazioni selezionate. Configuration Manager consente di sincronizzare gli aggiornamenti software con le classificazioni di aggiornamento seguenti:  
    >   
    > - **Aggiornamenti critici**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico, per un bug critico, non correlato alla sicurezza.  
    > - **Aggiornamenti delle definizioni**: specifica un aggiornamento software frequente rilasciato pubblicamente che contiene aggiunte al database che contiene la definizione del prodotto.  
    > - **Feature Pack**: specifica le nuove funzionalità del prodotto distribuite al di fuori di una versione del prodotto e che in genere sono incluse nella successiva versione completa del prodotto.  
    > - **Aggiornamenti della sicurezza**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico del prodotto, correlato alla sicurezza.  
    > - **Service Pack**: specifica un insieme cumulativo e testato di tutti gli aggiornamenti rapidi, gli aggiornamenti della sicurezza, gli aggiornamenti critici e gli aggiornamenti che vengono applicati a un prodotto. I Service Pack possono contenere anche aggiornamenti aggiuntivi per problemi rilevati internamente dopo il rilascio del prodotto.  
    > - **Strumenti**: specifica un'utilità o una funzionalità che consente di completare una o più attività.  
    > - **Aggiornamenti cumulativi**: specifica un insieme cumulativo e testato di aggiornamenti rapidi, aggiornamenti della sicurezza, aggiornamenti critici e aggiornamenti riuniti in un unico pacchetto per semplificarne la distribuzione. Un aggiornamento cumulativo interessa in genere un'area specifica, ad esempio la sicurezza o un componente del prodotto.  
    > - **Aggiornamenti**: specifica un aggiornamento rilasciato pubblicamente per un problema specifico. Un aggiornamento risolve un bug non critico, non correlato alla sicurezza.  
    > - **Aggiornamento**: specifica un aggiornamento per le caratteristiche e le funzionalità di Windows 10. Per ottenere la classificazione di [aggiornamento](https://support.microsoft.com/kb/3095113), i punti di aggiornamento software e i siti devono eseguire WSUS 4.0 con l'**hotfix 3095113**.    
    >       

    > [!NOTE]    
    > A partire da Configuration Manager versione 1706, è possibile selezionare la casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** per sincronizzare i driver di Microsoft Surface.<!--1098490--> Tutti i punti di aggiornamento software devono eseguire Windows Server 2016 per sincronizzare correttamente i driver di Surface. Se si abilita un punto di aggiornamento software in un computer che esegue Windows Server 2012 dopo aver abilitato i driver per Surface, i risultati dell'analisi per gli aggiornamenti dei driver non saranno accurati. Questo comportamento causa la visualizzazione di dati di conformità non corretti nella console di Configuration Manager e nei report di Configuration Manager.  
    >  
    > Questa funzionalità è stata introdotta per la prima volta nella versione 1706 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1710, questa funzionalità non è più in versione non definitiva.  
    >  
    > Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  Nella scheda **Prodotti** specificare i prodotti per cui si desidera sincronizzare gli aggiornamenti software e quindi fare clic su **Chiudi**.  

    > [!NOTE]  
    >  I metadati per ogni aggiornamento software definiscono i prodotti per i quali l'aggiornamento è applicabile. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione, ad esempio Windows Server 2012. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Windows, di cui Windows Server 2012 è membro. È possibile specificare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti. Il tempo necessario per sincronizzare gli aggiornamenti software è direttamente proporzionale al numero di prodotti selezionati.  
    >   
    >  Se gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è selezionato per la sincronizzazione, tutti i prodotti verranno visualizzati nella console di Configuration Manager, anche se alcuni non sono stati selezionati. Se, ad esempio, Windows Server 2012 è l'unico sistema operativo selezionato e se un aggiornamento software si applica a Windows 8 e a Windows Server 2012, entrambi i prodotti vengono visualizzati nella console di Configuration Manager.  

    > [!IMPORTANT]  
    >  Configuration Manager archivia un elenco di prodotti e di famiglie di prodotti tra cui è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. È possibile che i prodotti e le famiglie di prodotti pubblicati dopo il rilascio di Configuration Manager non siano disponibili per la selezione finché non si completa la sincronizzazione degli aggiornamenti software, che aggiorna l'elenco di prodotti e famiglie di prodotti disponibili tra cui è possibile scegliere.  

## <a name="next-steps"></a>Passaggi successivi
Avviare la sincronizzazione degli aggiornamenti software per recuperare gli aggiornamenti software in base ai nuovi criteri. Per informazioni dettagliate, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).
