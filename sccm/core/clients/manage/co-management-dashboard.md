---
title: Dashboard di co-gestione
titleSuffix: Configuraton Manager
description: Esaminare le informazioni relative alla co-gestione usando il dashboard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3d4cbbf78639a135e9e36e3402f9920a6ef71ed
ms.sourcegitcommit: 78d2dce465e3500653b252583a6903a006784c26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/19/2018
ms.locfileid: "46448787"
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
 - [Co-gestione per dispositivi Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparare i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare)

    
