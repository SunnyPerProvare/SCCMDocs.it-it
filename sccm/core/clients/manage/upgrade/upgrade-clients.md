---
title: Aggiornare i client | Microsoft Docs
description: Informazioni su come aggiornare i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: c9794b9770e6fa5665af547d6b36559f85ade691


---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Aggiornare i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare diversi metodi per aggiornare il software client di System Center Configuration Manager in computer Windows, server UNIX e Linux e computer Mac all'interno dell'azienda. Le sezioni seguenti descrivono i vantaggi e gli svantaggi di ogni metodo di aggiornamento del client per aiutare l'utente a stabilire quale sia quello più appropriato per la propria organizzazione.  

> [!TIP]  
>  Se si esegue l'aggiornamento dell'infrastruttura di server da una versione precedente di Configuration Manager \(ad esempio Configuration Manager 2007 o System Center 2012 Configuration Manager\), è consigliabile completare gli aggiornamenti dei server, tra cui l'installazione di tutti gli aggiornamenti del ramo corrente, prima dell'aggiornamento dei client di Configuration Manager.   L'aggiornamento più recente del ramo corrente contiene la versione più recente del client, quindi è consigliabile eseguire gli aggiornamenti dei client dopo aver installato tutti gli aggiornamenti di Configuration Manager che si vogliono usare.  

## <a name="group-policy-installation"></a>Installazione tramite Criteri di gruppo  
 **Piattaforma client supportata:** Windows  

 **Vantaggi**  

-   Non richiede l'individuazione dei computer prima di poter aggiornare il client.  

-   Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

-   I computer possono leggere le proprietà di installazione client che sono state pubblicate in Servizi di dominio Active Directory.  

-   Non richiede la configurazione e il mantenimento di un account di installazione per il computer client previsto.  

 **Svantaggi**  

-   Può causare traffico di rete elevato se vengono aggiornati molti client.  

-   Se lo schema di Active Directory non è esteso per Configuration Manager, è necessario usare le impostazioni di Criteri di gruppo per aggiungere le proprietà di installazione del client ai computer presenti nel sito.  

 Per altre informazioni, vedere [Come installare i client di Configuration Manager usando i Criteri di gruppo](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP).  

## <a name="logon-script-installation"></a>Installazione tramite script di accesso  
 **Piattaforma client supportata:** Windows  

 **Vantaggi**  

-   Non richiede l'individuazione dei computer prima di poter installare il client.  

-   Può essere utilizzato per le nuove installazioni di client o per gli aggiornamenti.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

 **Svantaggi**  

-   Può causare traffico di rete elevato se vengono aggiornati molti client in un periodo di tempo breve.  

-   L'aggiornamento in tutti i computer client può richiedere molto tempo se gli utenti non accedono spesso alla rete.  

 Per altre informazioni, vedere [Come installare i client di Configuration Manager usando script di accesso](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Installazione manuale  
 **Piattaforma client supportata:** Windows, UNIX/Linux, Mac OS X  

 **Vantaggi**  

-   Non richiede l'individuazione dei computer prima di poter aggiornare il client.  

-   Può essere utile a scopo di test.  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

 **Svantaggi**  

-   Non prevede automazione, pertanto risulta dispendioso in termini di tempo.  

 Per altre informazioni, vedere i seguenti argomenti:  

-   [Come installare manualmente i client di Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Come aggiornare i client per i server Linux e UNIX in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

-   [Come aggiornare i client di System Center Configuration Manager in computer Mac](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Installazione aggiornamento (gestione applicazioni)  
 **Piattaforma client supportata:** Windows  

> [!NOTE]  
>  Non è possibile aggiornare i client di Configuration Manager 2007 con questo metodo. In questo scenario è possibile distribuire il client di Configuration Manager come pacchetto dal sito di Configuration Manager 2007 oppure è possibile usare l'aggiornamento automatico del client, che crea e distribuisce automaticamente un pacchetto contenente la versione più recente del client.  

 **Vantaggi**  

-   Supporta l'utilizzo di proprietà della riga di comando per CCMSetup.  

 **Svantaggi**  

-   Può causare elevato traffico di rete quando si esegue la distribuzione di client in raccolte di grandi dimensioni.  

-   Può essere utilizzato solo per aggiornare il software client nei computer che sono stati individuati e assegnati al sito.  

 Per altre informazioni, vedere [Come installare i client di Configuration Manager usando un pacchetto e un programma](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Aggiornamento automatico del client  

> [!NOTE]  
>  È possibile usare l'aggiornamento automatico per aggiornare i client di Configuration Manager 2007 a client di System Center Configuration Manager. Un client di Configuration Manager 2007 può eseguire l'assegnazione a un sito di Configuration Manager. Non può tuttavia eseguire altre azioni oltre all'aggiornamento automatico del client.  

 **Piattaforma client supportata:** Windows  

 **Vantaggi**  

-   Può essere utilizzato per mantenere automaticamente i client presenti nel sito aggiornati alla versione più recente.  

-   Richiede un livello di amministrazione minimo da parte dell'utente amministratore.  

 **Svantaggi**  

-   Può essere utilizzato solo per aggiornare il software client e non per installare un nuovo client.  

-   Non è adatto per l'aggiornamento di più client contemporaneamente.  

-   Si applica a tutti i client presenti nella gerarchia assegnati a un sito. Non può essere definito dalla raccolta.  

-   Opzioni di programmazione limitate.  

 Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Test di client  
 **Piattaforma client supportata:** Windows  

 **Vantaggi**  

-   Può essere usato per testare nuove versioni client in una raccolta di preproduzione più piccola.  

-   Al termine dei test, i client in pre-produzione vengono alzati di livello alla produzione e aggiornati automaticamente nel sito di Configuration Manager.  

 **Svantaggi**  

-   Può essere utilizzato solo per aggiornare il software client e non per installare un nuovo client.  

 [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  



<!--HONumber=Dec16_HO3-->


