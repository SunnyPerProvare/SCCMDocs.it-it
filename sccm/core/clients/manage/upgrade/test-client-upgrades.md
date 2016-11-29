---
title: Testare gli aggiornamenti client in una raccolta di pre-produzione | System Center Configuration Manager
description: Testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e648b94a475bda2b35d69ff0a8863d2e0d248fb


---
# <a name="how-to-test-client-upgrades-in-a-preproduction-collection-in-system-center-configuration-manager"></a>Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per l'aggiornamento del client di Configuration Manager nei PC e nei dispositivi Windows è possibile testare una nuova versione del client in una raccolta di pre-produzione prima di aggiornare il resto del sito.  In questo caso, solo i dispositivi che fanno parte della raccolta di pre-produzione vengono aggiornati al nuovo client. Dopo aver testato il client in questa raccolta di pre-produzione, è possibile alzare di livello il client. In questo modo la nuova versione del software client viene resa disponibile al resto del sito.  

 Per testare i client in modalità di pre-produzione sono previsti 3 passaggi di base  

1.  [Per configurare gli aggiornamenti automatici del client per l'uso di una raccolta di pre-produzione](#BKMK_config) per usare una raccolta di pre-produzione.  

2.  [Per installare un aggiornamento di Configuration Manager che include una nuova versione del client](#BKMK_install) che include una nuova versione del client. Durante l'installazione, specificare l'uso di una raccolta di pre-produzione per il nuovo software client.  

3.  [Per alzare di livello il nuovo client al livello di produzione](#BKMK_promote) dopo aver testato sufficientemente il nuovo client in modalità di pre-produzione.  

> [!TIP]  
>  Se si esegue l'aggiornamento dell'infrastruttura di server da una versione precedente di Configuration Manager \(ad esempio Configuration Manager 2007 o System Center 2012 Configuration Manager\), è consigliabile completare gli aggiornamenti dei server, tra cui l'installazione di tutti gli aggiornamenti del ramo corrente, prima dell'aggiornamento dei client di Configuration Manager.   L'aggiornamento più recente del ramo corrente contiene la versione più recente del client, quindi è consigliabile eseguire gli aggiornamenti dei client dopo aver installato tutti gli aggiornamenti di Configuration Manager che si vogliono usare.  

##  <a name="a-namebkmkconfiga-to-configure-automatic-client-upgrades-to-use-a-preproduction-collection"></a><a name="BKMK_config"></a> Per configurare gli aggiornamenti client automatici per l'uso di una raccolta di pre-produzione  

1. Impostare una raccolta che contiene i computer nei quali si vuole distribuire il client di pre-produzione. Per altre informazioni su questo passo, vedere [How to create collections](..\collections\create-collections.md) (Come creare raccolte).

> [!NOTE]
> Non includere i computer del gruppo lavoro nelle raccolte di pre-produzione. I computer del gruppo di lavoro non possono usare l'autenticazione richiesta per il punto di distribuzione per accedere al pacchetto client di pre-produzione.   

1.  Nella console di Configuration Manage aprire **Amministrazione** > **Configurazione del sito** > **Siti** e fare clic su **Impostazioni gerarchia**.  

     Nella scheda **Aggiornamento client** di **Proprietà impostazioni gerarchia**, eseguite le seguenti operazioni:  

    -   Selezionare **Aggiornare tutti i client della raccolta di preproduzione automaticamente utilizzando il client preproduzione**  

    -   Immettere il nome di una raccolta da utilizzare come raccolta preproduzione  

2.  Fare clic su **OK** per salvare le impostazioni di aggiornamento client.  

##  <a name="a-namebkmkinstalla-to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a><a name="BKMK_install"></a> Per installare un aggiornamento di Configuration Manager che include una nuova versione del client  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**, selezionare un aggiornamento **Disponibile** e fare clic su **Installa pacchetto di aggiornamento**  

     Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante l'installazione dell'aggiornamento, nella pagina **Opzioni client** della procedura guidata selezionare **Testa in una raccolta di pre-produzione**e fare clic su **Avanti**.  

3.  Completare il resto della procedura guidata e installare il pacchetto di aggiornamento.  

     Dopo aver completato la procedura guidata, i client nella raccolta di pre-produzione inizieranno a distribuire il client aggiornato. È possibile monitorare la distribuzione dei client aggiornati passando a **Monitoraggio** > **Stato del client** > **Distribuzione client di pre-produzione**. Per altre informazioni, vedere [Come monitorare lo stato di distribuzione dei client in System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Lo stato della distribuzione nei computer che ospitano i ruoli del sistema del sito in una raccolta di pre-produzione può essere indicato come **non avviato** anche quando il client è stato distribuito correttamente. Quando si promuove il client al livello di produzione, lo stato della distribuzione è segnalato in modo corretto.

##  <a name="a-namebkmkpromotea-to-promote-the-new-client-to-production"></a><a name="BKMK_promote"></a> Per alzare di livello il nuovo client al livello di produzione  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**e fare clic su **Alza di livello il client di pre-produzione**.

    > [!TIP]
    > Il pulsante **Alza di livello il client di pre-produzione** è disponibile anche durante il monitoraggio delle distribuzioni dei client nella console da **Monitoraggio** > **Stato del client** > **Distribuzione client di pre-produzione**.

2.  Nella finestra di dialogo esaminare le versioni dei client in produzione e pre-produzione, verificare che sia specificata la raccolta di pre-produzione corretta e quindi fare clic su **Alza di livello**. Fare clic su **Sì**nella finestra di dialogo di conferma.  

3.  Quando si chiude la finestra di dialogo, la versione aggiornata del client sostituisce quella attualmente in uso nella gerarchia. Sarà quindi possibile aggiornare i client per l'intero sito. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  



<!--HONumber=Nov16_HO1-->


