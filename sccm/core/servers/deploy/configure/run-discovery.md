---
title: Eseguire l'individuazione | System Center Configuration Manager
description: Leggere la panoramica del processo di individuazione e dei record di dati dell'individuazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d73b493318b0a1938d42265ec03369015365addb


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Eseguire l'individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare uno o più metodi di individuazione in    
      System Center Configuration Manager per trovare risorse utente e di dispositivo che è possibile gestire. L'individuazione può essere usata anche per identificare l'infrastruttura di rete nel relativo ambiente.  Esistono diversi metodi di individuazione diversi che è possibile usare per trovare diversi componenti e ogni metodo presenta configurazioni e limitazioni specifiche.  

## <a name="overview-of-discovery"></a>Panoramica dell'individuazione  
 L'individuazione è il processo con cui Configuration Manager rileva ciò che è possibile gestire. Di seguito sono indicati i metodi di individuazione disponibili:  

-   Individuazione foresta Active Directory  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

-   Individuazione heartbeat  

-   Individuazione rete  

-   Individuazione server  

> [!TIP]  
>  Informazioni sui singoli metodi di individuazione sono disponibili nell'argomento [Informazioni sui metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Per assistenza nella scelta dei metodi da usare e dei siti della gerarchia, vedere l'argomento [Selezionare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Per usare la maggior parte dei metodi di individuazione, è necessario abilitare il metodo in un sito e configurarlo in modo da eseguire la ricerca di specifici percorsi di rete o di Active Directory. Durante l'esecuzione, vengono eseguite query nel percorso specificato per ottenere informazioni sui dispositivi o sugli utenti che Configuration Manager può gestire.  Quando un metodo di individuazione rileva correttamente un'informazione su una risorsa, questa viene inserita in un file denominato record dei dati di individuazione, che viene elaborato da un sito di amministrazione centrale o primario. L'elaborazione di un record dei dati di individuazione crea un nuovo record nel database del sito per le risorse appena individuate oppure aggiorna i record esistenti con le nuove informazioni.  

 Alcuni metodi di individuazione possono generare un grosso volume di traffico di rete e i record dei dati di individuazione risultanti possono causare un uso significativo di risorse della CPU durante l'elaborazione. Di conseguenza, pianificare l'uso solo dei metodi di individuazione necessari per soddisfare gli obiettivi. Si potrebbe iniziare a usare solo uno o due metodi di individuazione, quindi abilitare in seguito metodi aggiuntivi in modo controllato per estendere il livello di individuazione nel relativo ambiente.  

 Dopo che le informazioni di individuazione saranno state aggiunte al database del sito vengono quindi replicate in ogni sito della gerarchia, indipendentemente dal sito in cui sono state individuate o elaborate. Quindi, nonostante sia possibile configurare diverse pianificazioni e impostazioni per i metodi di individuazione nei diversi siti, si potrebbe eseguire un metodo di individuazione in un solo sito per ridurre l'uso della larghezza di banda attraverso azioni di individuazione duplicate e ridurre l'elaborazione dei dati di individuazione ridondanti in più siti.  

 È possibile usare i dati di individuazione per creare raccolte e query personalizzate che raggruppano in modo logico le risorse per attività di gestione come:  

-   Push o aggiornamento delle installazioni client  

-   Distribuzione del contenuto a utenti o dispositivi  

-   Distribuzione delle impostazioni client e delle configurazioni associate  

##  <a name="a-namebkmkddrsa-about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Informazioni sui record dei dati di individuazione  
 I record dei dati di individuazione (DDR) sono file creati da un metodo di individuazione e contengono informazioni su una risorsa che è possibile gestire in Configuration Manager. I DDR contengono informazioni sui computer, sugli utenti e, in alcuni casi, sull'infrastruttura di rete. Questi vengono elaborati nei siti primari o nei siti di amministrazione centrale. Dopo l'immissione nel database delle informazioni sulle risorse contenute nel DDR, il DDR viene eliminato e le informazioni vengono replicate come dati globali in tutti i siti della gerarchia.  

 Il sito in cui viene elaborato un DDR dipende dalle informazioni contenute:  

-   I DDR per le nuove risorse individuate non presenti nel database vengono elaborati nel sito di livello superiore della gerarchia. Il sito di livello superiore crea un nuovo record di risorse nel database e assegna al record un identificatore univoco. I DDR vengono trasferiti mediante replica basata su file fino a raggiungere il sito di livello superiore.  

-   I DDR per gli oggetti rilevati in precedenza vengono elaborati nei siti primari. I siti primari figlio non trasferiscono i DDR nel sito di amministrazione centrale se questi contengono informazioni su una risorsa già presente nel database.  

-   I siti secondari non elaborano i record dei dati di individuazione e li trasferiscono al relativo sito primario padre sempre con la replica basata su file.  

I file DDR si distinguono mediante l'estensione DDR e solitamente hanno una dimensione di circa 1 KB.  

## <a name="get-started-with-discovery"></a>Introduzione all'individuazione:  
 Prima di usare la console di Configuration Manager per configurare l'individuazione è necessario comprendere le differenze tra i metodi, le operazioni consentite e, per alcuni, le relative limitazioni.  
Gli argomenti seguenti aiutano a gettare le basi per l'uso corretto dei metodi di individuazione:  

-   [Informazioni sui metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Selezionare i metodi di individuazione da usare per System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Quindi, dopo aver stabilito quali metodi usare, vedere le informazioni relative alla configurazione di ogni metodo nell'argomento sulla [configurazione dei metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  



<!--HONumber=Nov16_HO1-->


