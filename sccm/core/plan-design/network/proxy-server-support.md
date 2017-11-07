---
title: Supporto dei server proxy
titleSuffix: Configuration Manager
description: Informazioni sul supporto di System Center Configuration Manager per i server proxy usato dai server di sistema del sito e dai client.
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 909c56f6087b6ed7b6600b6f3fc693dbd5b4d1b5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Supporto dei server proxy in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I client e i server del sistema del sito di System Center Configuration Manager possono usare un server proxy.  

## <a name="site-system-servers"></a>Server del sistema del sito  
Quando i ruoli del sistema del sito devono connettersi a Internet, è possibile configurarli per l'uso di un server proxy.  

-   Un computer che ospita un server del sistema del sito supporta una configurazione di server proxy singolo condivisa da tutti i ruoli del sistema del sito nello stesso computer. Se sono necessari server proxy separati per diversi ruoli o istanze di un ruolo, è necessario inserire i ruoli in server del sistema del sito separati.  

-   Quando si configurano nuove impostazioni del server proxy per un server del sistema del sito che ha già una configurazione del server proxy, la configurazione originale viene sovrascritta.  

-   Le connessioni al proxy usano l'account di **sistema** del computer che ospita il ruolo del sistema del sito.  

I ruoli del sistema del sito seguenti si connettono a Internet e possono richiedere un server proxy.  Con un'unica eccezione, i ruoli del sistema del sito che possono usare un proxy lo fanno senza bisogno di alcuna configurazione aggiuntiva. L'eccezione è rappresentata dal punto di aggiornamento software. L'elenco seguente riporta informazioni sulle configurazioni aggiuntive necessarie per un punto di aggiornamento software:  

**Punto di sincronizzazione di Asset Intelligence**: questo ruolo del sistema del sito si connette a Microsoft e usa una configurazione del server proxy nel computer che ospita il punto di sincronizzazione di Asset Intelligence.  

**Punto di distribuzione basato su cloud**: per configurare un server proxy per un punto di distribuzione basato su cloud, configurare il proxy nel sito primario che gestisce tale punto di distribuzione.  

Per questa configurazione, il server del sito primario:  

-   Deve riuscire a connettersi a Microsoft Azure per la configurazione, il monitoraggio e la distribuzione del contenuto al punto di distribuzione.  

-   Usa l'account di sistema del computer per effettuare la connessione.  

-   Usa il Web browser predefinito del computer.  

Non è possibile configurare un server proxy nel punto di distribuzione basato su cloud in Microsoft Azure.  

**Punto di connessione cloud**: questo ruolo del sistema del sito si connette al servizio cloud di Configuration Manager per scaricare gli aggiornamenti di versione per Configuration Manager e usa un server proxy configurato nel computer che ospita il punto di connessione del servizio.  

**Connettore Exchange Server**: questo ruolo del sistema del sito si connette a Exchange Server e usa una configurazione del server proxy nel computer che ospita il connettore Exchange Server.  

**Punto di connessione del servizio**: questo ruolo del sistema del sito si connette a Microsoft Intune e usa una configurazione del server proxy nel computer che ospita il punto di connessione del servizio.  

**Punto di aggiornamento software**: questo ruolo del sistema del sito può usare il proxy quando si connette a Microsoft Update per scaricare le patch e sincronizzare le informazioni sugli aggiornamenti. I punti di aggiornamento software usano un proxy solo per le opzioni seguenti, se abilitate durante la configurazione di tali punti:  

-   **Usa un server proxy durante la sincronizzazione degli aggiornamenti software**  

-   **Usare un server proxy quando si scaricano contenuti tramite le regole di distribuzione automatica**. Anche se disponibile, questa opzione non viene usata dai punti di aggiornamento software nei siti secondari.  

Configurare le impostazioni del server proxy nella pagina Punto di aggiornamento software attivo dell'Aggiunta guidata ruoli del sistema del sito oppure nella scheda **Generale** in **Proprietà del componente del punto di aggiornamento software**.  

-   Le impostazioni del server proxy sono associate solo al punto di aggiornamento software nel sito.  

-   Le opzioni del server proxy sono disponibili solo quando è presente un server proxy già configurato per il server del sistema del sito che ospita il punto di aggiornamento software.  

> [!NOTE]  
>  Per impostazione predefinita, l'account di **sistema** del server in cui è stata creata una regola di distribuzione automatica viene usato per connettersi a Internet e scaricare gli aggiornamenti software quando sono in esecuzione le regole di distribuzione automatica.  
>   
>  Quando l'account non ha accesso a Internet, non è possibile scaricare gli aggiornamenti software e in ruleengine.log viene registrata la voce seguente: **Failed to download the update from internet. Error = 12007** (Impossibile scaricare l'aggiornamento da Internet. Errore = 12007).  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Per configurare il server proxy per un server del sistema del sito  

1.  Nella console di Configuration Manager scegliere **Amministrazione**, espandere **Configurazione del sito** e quindi scegliere **Server e ruoli del sistema del sito**.  

2.  Scegliere il server del sistema del sito che si vuole modificare, quindi nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Sistema del sito** e scegliere **Proprietà**.  

3.  In Proprietà sistema del sito selezionare la scheda **Proxy** e quindi configurare le impostazioni proxy per il server del sito primario.  

4.  Scegliere **OK** per salvare la nuova configurazione del server proxy.  
