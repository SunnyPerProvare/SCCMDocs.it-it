---
title: Monitorare lo stato di distribuzione dei client
titleSuffix: Configuration Manager
description: Monitorare lo stato di distribuzione dei client in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
caps.latest.revision: "11"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: f5ea535b47b7b9061282a1aadcaa6ed7492f08b4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>Come monitorare lo stato di distribuzione dei client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La distribuzione client nel sito richiede tempo e alcune installazioni non riescono la prima volta. La console di System Center Configuration Manager offre un modo per tenere d'occhio le distribuzioni client in una raccolta attraverso la segnalazione dello stato di distribuzione client in tempo reale.  

> [!NOTE]  
>  Il modo migliore e più affidabile per monitorare la distribuzione client consiste nell'usare la console di Configuration Manager, come descritto in questo articolo. La sezione **Stato del client** dell'area di lavoro **Monitoraggio** nella console indica lo stato di distribuzione del client con precisione e in tempo reale. È possibile monitorare le distribuzioni client con altri strumenti, ad esempio Server Manager in Windows Server o System Center Operations Manager, ma è possibile ricevere avvisi da normali attività di installazione del client. A causa della modalità di esecuzione del programma di installazione del client (CCMSetup.exe) in vari ambienti, gli altri strumenti potrebbero generare falsi allarmi e avvisi che non riflettono accuratamente lo stato delle distribuzioni client.  

 Nell'area di lavoro **Monitoraggio** della console è possibile monitorare i seguenti stati delle distribuzioni client che avvengono all'interno di una raccolta specificata:  

-   Conforme  

-   In corso  

-   Non conforme  

-   Operazione non riuscita  

-   Sconosciuto  

 Configuration Manager segnala le distribuzioni client di produzione o di pre-produzione. La console di Configuration Manager offre anche un grafico delle distribuzioni client non riuscite in uno specifico periodo di tempo, per determinare se le azioni intraprese per la risoluzione dei problemi di distribuzione stanno migliorando la percentuale di distribuzione senza errori nel tempo.  

## <a name="to-monitor-client-deployments"></a>Per monitorare le distribuzioni client  

-   Nella console di Configuration Manager fare clic su **Monitoraggio** > **Stato client**.  

-   Fare clic su **Distribuzione client di produzione** oppure su **Distribuzione client di pre-produzione** a seconda della versione del client da monitorare.  

-   Esaminare i grafici di stato della distribuzione client e di errore di distribuzione client.  

-   Per modificare l'ambito del report, fare clic su **Sfoglia…** e scegliere una raccolta diversa.  

 Per altre informazioni sulle distribuzioni client di pre-produzione, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).

 > [!NOTE]
 > Lo stato della distribuzione nei computer che ospitano i ruoli del sistema del sito in una raccolta di pre-produzione può essere indicato come **Non conforme** anche quando il client è stato distribuito correttamente. Quando si promuove il client al livello di produzione, lo stato della distribuzione è segnalato in modo corretto.   

 Per monitorare lo stato dei client distribuiti, vedere [Come monitorare i client in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md)  

 È possibile usare i report di Configuration Manager per ottenere altre informazioni sullo stato dei client nel proprio sito. Per altre informazioni sull'esecuzione dei report, vedere [Creazione di report in System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
