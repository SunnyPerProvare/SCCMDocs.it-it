---
title: Configurare le classificazioni e i prodotti per la sincronizzazione | Microsoft Docs
description: Seguire questi passaggi per configurare le classificazioni e i prodotti per la sincronizzazione nella console di Configuration Manager.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.translationtype: HT
ms.sourcegitcommit: afe0ecc4230733fa76e41bf08df5ccfb221da7c8
ms.openlocfilehash: 2da61e6e06850b36543b9fd41bd9a7d2368006fb
ms.contentlocale: it-it
ms.lasthandoff: 08/04/2017

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
    > - **Aggiornamenti critici:** specifica un aggiornamento rilasciato su vasta scala per un problema specifico, che risolve un bug critico, non correlato alla sicurezza.  
    > - **Aggiornamenti delle definizioni:** specifica un aggiornamento a un virus o ad altri file di definizione.  
    > - **Feature Pack**: specifica le nuove funzionalità del prodotto distribuite al di fuori di una versione del prodotto e che in genere sono incluse nella versione successiva completa del prodotto.  
    > - **Aggiornamenti della sicurezza:** specifica un aggiornamento rilasciato su vasta scala per un problema specifico del prodotto e correlato alla sicurezza.  
    > - **Service Pack:** specifica un set cumulativo di aggiornamenti rapidi applicati a un'applicazione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti software e così via.  
    > - **Strumenti:** specifica un'utilità o una funzionalità che consente di completare una o più attività.  
    > - **Aggiornamenti cumulativi:** specifica un set cumulativo di aggiornamenti rapidi inclusi nello stesso pacchetto per facilitarne la distribuzione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti e così via. Un aggiornamento cumulativo è relativo in genere a un'area specifica, ad esempio la sicurezza o un componente del prodotto.  
    > - **Aggiornamenti:** specifica un aggiornamento di un'applicazione o un file attualmente installato.  
    > - **Aggiornamento**: specifica un aggiornamento per le caratteristiche e le funzionalità di Windows 10. Per ottenere la classificazione di [aggiornamento](https://support.microsoft.com/kb/3095113), i punti di aggiornamento software e i siti devono eseguire WSUS 4.0 con l'**hotfix 3095113**.    
    >       

    > [!NOTE]    
    > A partire da Configuration Manager versione 1706, è anche possibile selezionare la casella di controllo **Includi i driver di Microsoft Surface e gli aggiornamenti del firmware** per sincronizzare i driver di Microsoft Surface. Tutti i punti di aggiornamento software devono eseguire Windows Server 2016 per sincronizzare correttamente i driver di Surface.     
    >    
    > Si tratta di una funzionalità di versione non definitiva. Le funzionalità di versioni non definitive sono incluse nel prodotto a scopo di test preliminare in un ambiente di produzione, ma non devono essere considerate pronte per l'ambiente di produzione. Per rendere disponibile questa funzionalità è necessario attivarla. Per altre informazioni, vedere la sezione relativa all'[abilitazione delle funzionalità facoltative dagli aggiornamenti](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

5.  Nella scheda **Prodotti** specificare i prodotti per cui si desidera sincronizzare gli aggiornamenti software e quindi fare clic su **Chiudi**.  

    > [!NOTE]  
    >  I metadati per ogni aggiornamento software definiscono i prodotti per i quali l'aggiornamento è applicabile. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione, ad esempio Windows Server 2012. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Windows, di cui Windows Server 2012 è membro. È possibile specificare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti. Il tempo necessario per sincronizzare gli aggiornamenti software è direttamente proporzionale al numero di prodotti selezionati.  
    >   
    >  Se gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è selezionato per la sincronizzazione, tutti i prodotti verranno visualizzati nella console di Configuration Manager, anche se alcuni prodotti non sono stati selezionati. Se, ad esempio, Windows Server 2012 è l'unico sistema operativo selezionato e se un aggiornamento software si applica a Windows 8 e a Windows Server 2012, entrambi i prodotti verranno visualizzati nella console di Configuration Manager.  

    > [!IMPORTANT]  
    >  Configuration Manager archivia un elenco di prodotti e di famiglie di prodotti tra cui è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. È possibile che i prodotti e le famiglie di prodotti pubblicati dopo il rilascio di Configuration Manager non siano disponibili per la selezione finché non si completa la sincronizzazione degli aggiornamenti software, che aggiorna l'elenco di prodotti e famiglie di prodotti disponibili tra cui è possibile scegliere.  

## <a name="next-steps"></a>Passaggi successivi
Avviare la sincronizzazione degli aggiornamenti software per recuperare gli aggiornamenti software in base ai nuovi criteri. Per informazioni dettagliate, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).

