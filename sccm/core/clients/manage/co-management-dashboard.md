---
title: Dashboard di co-gestione
titleSuffix: System Center Configuration Manager
description: Esaminare le informazioni relative alla co-gestione usando il dashboard.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ca748921a806a0e5edf608a62e8a44edf4d84
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard di co-gestione in System Center Configuration Manager
*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1802, è possibile visualizzare un dashboard con informazioni sulla co-gestione. Il dashboard consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Aprire il dashboard di co-gestione
Per aprire il dashboard di co-gestione, procedere come segue: 

1. Aprire la console di Configuration Manager. 
2. Fare clic sul nodo **Monitoraggio**. 
3. Per caricare il dashboard, fare clic su **Co-gestione**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Verifica delle informazioni nel dashboard di co-gestione

Nel dashboard di co-gestione vengono visualizzati quattro grafici per l'ambiente. 

- **Dispositivi con co-gestione**: specifica la percentuale di dispositivi co-gestiti presenti in tutto l'ambiente.

    ![Grafico dei dispositivi co-gestiti](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribuzione del sistema operativo client**: visualizza il numero di dispositivi client per ogni versione di sistema operativo. Vengono usati i raggruppamenti seguenti: </br>
    - Windows 7 e 8.x
    - Windows 10, versioni precedenti alla 1709
    - Windows 10, versione 1709 e successive

         > [!NOTE] 
         > Windows 10, versione 1709 e successive, è un prerequisito per la co-gestione.

     Se si passa il mouse su una sezione del grafico, viene visualizzata la percentuale dei dispositivi nel raggruppamento di sistemi operativi selezionato.

     ![Grafico della distribuzione dei sistemi operativi dei client](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Stato della co-gestione**: la suddivisione dei dispositivi con esito positivo e negativo nelle categorie seguenti:
    - Esito positivo, aggiunto ad Azure AD ibrido
    - Esito positivo, aggiunto ad Azure AD
    - Esito negativo: registrazione automatica non riuscita
    
     Se si passa il mouse su una sezione del grafico, viene visualizzata la percentuale dei dispositivi nella categoria. 

     ![Grafico di stato per la co-gestione](media\co-management-dashboard\Co-management-status-graph.PNG)

     Se si fa clic su una sezione del grafico si passa all'elenco dei dispositivi per la categoria.
 
     ![Elenco di dispositivi con errore di registrazione](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transizione del carico di lavoro**: grafico a barre con il numero di dispositivi passati a Microsoft Intune per i quattro carichi di lavoro disponibili:
    - Criteri di conformità
    - Accesso alle risorse
    - Windows Update for Business
    - Endpoint Protection

     Se si passa il mouse su una sezione del grafico, viene visualizzato il numero di dispositivi di cui è stata eseguita la transizione per il carico di lavoro. 
     ![Grafico a barre della transizione dei carichi di lavoro](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla co-gestione, vedere:
 - [Co-gestione per dispositivi Windows 10](/sccm/core/clients/manage/co-management-overview.md)
 - [Preparare i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare.md)

    
