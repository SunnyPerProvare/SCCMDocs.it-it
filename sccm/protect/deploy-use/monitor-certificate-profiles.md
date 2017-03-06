---
title: Monitorare i profili certificato | Microsoft Docs
description: "Informazioni su come monitorare lo stato di conformità dei profili certificato di System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: 74a0a4274965891869caf838550cd9465b46fd51
ms.lasthandoff: 12/30/2016


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Come monitorare i profili certificato in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visualizzare i risultati di conformità nella console di Configuration Manager  

Per monitorare la conformità dei certificati SCEP, usare i [report](#view-compliance-results-by-using-reports) invece della console. 

1.  Nella console di Configuration Manager scegliere **Monitoraggio**>  **Distribuzioni**.  

3.  Selezionare la distribuzione del profilo certificato desiderata.  

4.  Controllare le informazioni di riepilogo sulla conformità del certificato nella pagina principale. Per informazioni più dettagliate, selezionare il profilo certificato, quindi nella scheda **Home**, nel gruppo **Distribuzione**, scegliere **Visualizza stato** per aprire la pagina **Stato distribuzione** .  

     La pagina **Stato distribuzione** contiene le seguenti schede:  

    -   **Conforme**: visualizza la conformità del profilo certificato in base al numero degli asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che sono conformi al profilo del certificato. Il riquadro **Dettagli asset** visualizza anche gli utenti che sono conformi a questo profilo. Fare doppio clic su un utente nell'elenco per visualizzare altre informazioni.  

        > [!IMPORTANT]  
        >  Un profilo certificato non viene valutato se non è applicabile a un dispositivo client. Tuttavia, viene restituito come conforme.  

    -   **Errore**: visualizza un elenco di tutti gli errori per la distribuzione del profilo certificato selezionata in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che hanno generato errori con questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare altre informazioni.  

    -   **Non conforme**: visualizza un elenco di tutte le regole non conformi nel profilo certificato in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti gli utenti che non sono conformi a questo profilo. Quando si seleziona un utente, il riquadro **Dettagli asset** visualizza gli utenti interessati dal problema selezionato. Fare doppio clic su un utente nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Sconosciuto**: visualizza un elenco di tutti gli utenti che non sono conformi alla distribuzione del profilo certificato selezionata insieme allo stato client corrente dei dispositivi.  

5.  Nella pagina **Stato distribuzione** esaminare le informazioni dettagliate sulla conformità del profilo certificato distribuito. Viene creato un nodo temporaneo nel nodo **Distribuzioni** che consente di ritrovare rapidamente queste informazioni.  

     Lo stato di registrazione del certificato viene visualizzato come un numero. Utilizzare la tabella seguente per comprendere il significato di ciascun numero:  

    |Stato registrazione|Descrizione|  
    |-----------------------|-----------------|  
    |0x00000001|La registrazione ha avuto esito positivo e il certificato è stato rilasciato.|  
    |0x00000002|La richiesta è stata inviata e la registrazione è in sospeso o la richiesta è stata emessa fuori banda.|  
    |0x00000004|La registrazione deve essere rinviata.|  
    |0x00000010|Si è verificato un errore.|  
    |0x00000020|Lo stato di registrazione è sconosciuto.|  
    |0x00000040|Le informazioni sullo stato sono state ignorate. Ciò può verificarsi se un'autorità di certificazione  (collegamento ipertestuale: http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly) non è valida o non è stata selezionata per il monitoraggio.|  
    |0x00000100|La registrazione è stata negata.|  

##  <a name="view-compliance-results-by-using-reports"></a>Visualizzare i risultati di conformità usando i report

 Le impostazioni di conformità in System Center Configuration Manager includono report incorporati che è possibile usare per monitorare le informazioni sui profili certificato. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
>  È necessario utilizzare un carattere jolly (%) quando si utilizzano i parametri **Filtro dispositivo** e **Filtro utente** nei report per le impostazioni di conformità.  

Per monitorare la conformità dei certificati SCEP, usare questi report sui certificati disponibili nel nodo dei report **Accesso risorse aziendali**:  

 -   Cronologia di rilascio dei certificati  
 -   Elenco degli asset con certificati prossimi alla scadenza  
 -   Elenco degli asset per stato di rilascio del certificato  



 Per altre informazioni sulle modalità di configurazione dei report in System Center Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

