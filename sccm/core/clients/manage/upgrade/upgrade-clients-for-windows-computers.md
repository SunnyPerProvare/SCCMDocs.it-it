---
title: Aggiornare i client | Windows | System Center Configuration Manager
description: Aggiornare i client di System Center Configuration Manager in computer Windows.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: 11
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2b1600e6f04095506f18f4c2cd0988a320fbb951


---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>Come aggiornare i client per i computer Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile aggiornare il client in computer Windows usando i metodi di installazione client o le funzionalità di aggiornamento client automatico di Configuration Manager. I metodi di installazione client seguenti sono validi per aggiornare il software client nei computer Windows:  

-   Installazione con Criteri di gruppo  

-   Installazione tramite script di accesso  

-   Installazione manuale  

-   Aggiornare l'installazione  

 Se si vuole aggiornare il client usando metodi di installazione client, sono disponibili altre informazioni sull'uso di tali metodi in [How to deploy clients to Windows computers in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md) (Come distribuire i client di System Center Configuration Manager in computer Windows)  

> [!TIP]  
>  Se si esegue l'aggiornamento dell'infrastruttura di server da una versione precedente di Configuration Manager \(ad esempio Configuration Manager 2007 o System Center 2012 Configuration Manager\), è consigliabile completare gli aggiornamenti dei server, tra cui l'installazione di tutti gli aggiornamenti del ramo corrente, prima dell'aggiornamento dei client di Configuration Manager.   L'aggiornamento più recente del ramo corrente contiene la versione più recente del client, quindi è consigliabile eseguire gli aggiornamenti dei client dopo aver installato tutti gli aggiornamenti di Configuration Manager che si vogliono usare.  

## <a name="use-automatic-client-upgrade"></a>Usare l'aggiornamento client automatico  
 È anche possibile configurare Configuration Manager per l'aggiornamento automatico del software client all'ultima versione client di Configuration Manager quando Configuration Manager rileva che la versione di un client assegnato alla gerarchia di Configuration Manager è precedente a quella usata nella gerarchia. Questo scenario include l'aggiornamento del client all'ultima versione durante il tentativo di assegnazione a un sito di Configuration Manager.  

 È possibile aggiornare automaticamente un client negli scenari seguenti:  

-   La versione client è inferiore a quella usata nella gerarchia.  

-   Nel client sul sito di amministrazione centrale è installato un Language Pack non presente nel client esistente.  

-   Un prerequisito client nella gerarchia prevede una versione differente rispetto a quella installata sul client.  

-   Uno o più file di installazione client hanno una versione diversa.  

> [!NOTE]  
>  È possibile eseguire il report **Conteggio dei client di Configuration Manager per versioni client** nella cartella report **Sito - Informazioni client** per individuare le diverse versioni del client di Configuration Manager nella gerarchia.  

 Per impostazione predefinita, Configuration Manager crea un pacchetto di aggiornamento che viene inviato automaticamente a tutti i punti di distribuzione nella gerarchia. In caso di modifiche al pacchetto client sul sito di amministrazione centrale, come l'aggiunta di un Language Pack client, Configuration Manager aggiorna automaticamente il pacchetto e lo distribuisce a tutti i punti di distribuzione nella gerarchia. Se l'aggiornamento client automatico è attivato, il nuovo Language Pack client sarà installato automaticamente su tutti i client.  

> [!NOTE]  
>  Configuration Manager non invia automaticamente il pacchetto di aggiornamento client ai punti di distribuzione di Configuration Manager basati sul cloud.  

 Gli aggiornamenti client automatici sono utili quando si desidera aggiornare un numero ridotto di computer client che potrebbero essere stati esclusi dal metodo di installazione client principale. Ad esempio, è stato completato un aggiornamento client iniziale, ma alcuni client erano offline durante la distribuzione dell'aggiornamento. È possibile quindi usare questo metodo per aggiornare il client su questi computer alla successiva attivazione.  

 Usare la procedura seguente per configurare l'aggiornamento client automatico. L'aggiornamento client automatico deve essere configurato in un sito di amministrazione centrale e tale configurazione viene applicata a tutti i client nella gerarchia.  

#### <a name="to-configure-automatic-client-upgrades"></a>Per configurare gli aggiornamenti automatici dei client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nella scheda **Home** , del gruppo **Siti** , fare clic su **Impostazioni gerarchia**.  

4.  Nella scheda **Aggiornamento client** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** verificare la versione e la data del client di produzione e assicurarsi che la versione corrisponda a quella che si vuole usare per l'aggiornamento dei computer Windows.  Se la versione del client non è quella prevista, potrebbe essere necessario alzare il livello del client di preproduzione a client di produzione. Per altre informazioni, vedere [How to test client upgrades in a preproduction collection in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md) (Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager).  

5.  Fare clic su **Aggiorna tutti i client nella gerarchia usando il client di produzione** , quindi fare clic su **OK** nella finestra di dialogo di conferma.  

6.  Se non si vuole che gli aggiornamenti client si applichino ai server, fare clic su **Non aggiornare i server**.  

7.  Specificare il numero di giorni entro i quali i computer client devono aggiornare il client dopo aver ricevuto i criteri client. Il client verrà aggiornato a un intervallo casuale entro tale periodo. In questo modo è possibile evitare che un numero elevato di computer client venga aggiornato simultaneamente.

    > [!NOTE]
    > Per eseguire l'aggiornamento del client, è necessario che un computer sia in esecuzione. Se invece il computer non è esecuzione nel momento in cui è pianificata la ricezione dell'aggiornamento, l'aggiornamento non sarà eseguito. Al riavvio del computer, verrà pianificato un altro aggiornamento in un momento casuale entro un numero di giorni consentiti. Se i giorni per eseguire l'aggiornamento sono scaduti, l'aggiornamento sarà pianificato per essere eseguito in un momento casuale entro 24 ore dal riavvio del computer.
    >     
    > Dato tale comportamento, è possibile che i computer che vengono regolarmente arrestati alla fine della giornata lavorativa impieghino più tempo del previsto per eseguire l'aggiornamento se il momento casuale dell'aggiornamento pianificato non rientra nelle normali ore lavorative.

8.  Se si vuole che il pacchetto di installazione venga copiato nei punti di distribuzione che sono stati abilitati per i contenuti in versione di preproduzione, fare clic su **Distribuisci automaticamente il pacchetto di installazione client nei punti di distribuzione abilitati per i contenuti in versione di preproduzione**.  

9. Fare clic su **OK** per salvare le impostazioni e chiudere la finestra di dialogo **Proprietà delle impostazioni di gerarchia** . I client ricevono queste impostazioni al successivo download dei criteri.  



<!--HONumber=Nov16_HO1-->

