---
title: Controllare l'uso del controllo remoto | Microsoft Docs
description: Controllare l'uso di controllo remoto in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4259ecfca48ccdffa83247e9ab5a65b3f006c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>Come controllare l'uso di controllo remoto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare i report di System Center Configuration Manager per visualizzare le informazioni di controllo per il controllo remoto.  

 Per altre informazioni sulle modalità di configurazione dei report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

 I due report seguenti sono disponibili con la categoria **Messaggi di stato - Controllo**:  

-   **Controllo remoto - Tutti i computer sotto controllo remoto da un utente specifico**: visualizza un riepilogo delle attività di controllo remoto avviate da un utente specifico.  

-   **Controllo remoto - Tutte le informazioni sul controllo remoto**: visualizza un riepilogo dei messaggi di stato relativi al controllo remoto dei computer client.  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>Per eseguire il report Controllo remoto - Tutti i computer sotto controllo remoto da un utente specifico  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report**.  

3.  Nel nodo **Report** fare clic sulla colonna **Categoria** per ordinare i report in modo da poter trovare più facilmente quelli nella categoria **Messaggi di stato - Controllo**.  

4.  Selezionare il report **Controllo remoto - Tutti i computer sotto controllo remoto da un utente specifico**e quindi in **Gruppo Report** nella scheda **Home**fare clic su **Esegui**.  

5.  Nell'elenco **Nome utente** in **Controllo remoto - Tutti i computer sotto controllo remoto da un utente specifico**specificare l'utente per il quale si vuole visualizzare le informazioni di controllo e quindi fare clic su **Visualizza report**.  

6.  Dopo aver visualizzato i dati nel report, chiudere la finestra del report.  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>Per eseguire il report Controllo remoto - Tutte le informazioni sul controllo remoto  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report**.  

3.  Nel nodo **Report** fare clic sulla colonna **Categoria** per ordinare i report in modo da poter trovare più facilmente quelli nella categoria **Messaggi di stato - Controllo**.  

4.  Selezionare il report **Controllo remoto - Tutte le informazioni sul controllo remoto**e quindi in **Gruppo Report** nella scheda **Home**fare clic su **Esegui** per aprire la finestra **Controllo remoto - Tutte le informazioni sul controllo remoto** .  

5.  Dopo aver visualizzato i dati nel report, chiudere la finestra del report.  
