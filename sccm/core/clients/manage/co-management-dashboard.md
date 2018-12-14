---
title: Dashboard di co-gestione
titleSuffix: Configuration Manager
description: Usare il dashboard di co-gestione per esaminare le informazioni sui dispositivi con co-gestione.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad76140285df1c0125fcd2efab0f4794ed4881bf
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455946"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Dashboard di co-gestione in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1802, è possibile visualizzare un dashboard con informazioni sulla co-gestione. Il dashboard consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.<!--1356648-->

Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Co-gestione**.

A partire dalla versione 1810, il dashboard di co-gestione è stata migliorato con l'aggiunta di informazioni più dettagliate. <!--1358980-->



## <a name="dashboard-tiles"></a>Riquadri del dashboard 

I riquadri presenti nel dashboard di co-gestione variano a seconda della versione del sito. 


### <a name="co-managed-devices"></a>Dispositivi con co-gestione

*Si applica alla versione 1802 e 1806*

Specifica la percentuale di dispositivi co-gestiti presenti in tutto l'ambiente.
 ![Riquadro dei dispositivi co-gestiti](media\co-management-dashboard\Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribuzione del sistema operativo client

*Si applica a tutte le versioni* 

Specifica il numero di dispositivi client per ogni versione di sistema operativo. Gli elementi sono raggruppati nei modi seguenti:  
- Windows 7 e 8.x  
- Windows 10, versioni precedenti alla 1709  
- Windows 10, versione 1709 e successive  

    > [!Tip]  
    > Windows 10, versione 1709 e successive, è un prerequisito per la co-gestione.  

Passare il mouse su una sezione del grafico per visualizzare la percentuale dei dispositivi nello specifico gruppo di sistemi operativi.
 ![Riquadro Distribuzione del sistema operativo client](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Stato della co-gestione (anello)

*Si applica alla versione 1802 e 1806*

Specifica la suddivisione dei dispositivi con esito positivo e negativo nelle categorie seguenti:
- Esito positivo, aggiunto ad Azure AD ibrido  
- Esito positivo, aggiunto ad Azure AD  
- Esito negativo: registrazione automatica non riuscita  

Passare il mouse su una sezione del grafico per visualizzare la percentuale dei dispositivi nella categoria. 
 ![Riquadro Stato della co-gestione (anello)](media\co-management-dashboard\Co-management-status-graph.PNG)

Selezionare una sezione del grafico per visualizzare l'elenco dei dispositivi presenti in tale categoria.
 ![Elenco di dispositivi con errore di registrazione](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Stato della co-gestione (imbuto)

*Si applica alla versione 1810 e successive*

Un grafico a imbuto che mostra il numero di dispositivi che presentano i seguenti stati del processo di registrazione:  
- Dispositivi idonei  
- Scheduled  
- La registrazione è stata avviata  
- Registrazione eseguita  

![Riquadro Stato della co-gestione (imbuto)](media\co-management-dashboard\1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Stato di registrazione della co-gestione

*Si applica alla versione 1810 e successive*

Specifica la suddivisione degli stati dei dispositivi nelle categorie seguenti:
- Esito positivo, aggiunto ad Azure AD ibrido  
- Esito positivo, aggiunto ad Azure AD  
- Registrazione, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD ibrido  
- Operazione non riuscita, aggiunta ad Azure AD  
- Accesso utente in sospeso  

Selezionare uno stato nel riquadro per visualizzare un elenco dei dispositivi con tale stato.  

![Riquadro Stato di registrazione della co-gestione](media\co-management-dashboard\1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>Errori di registrazione

*Si applica alla versione 1810 e successive*

Una tabella che mostra il numero di errori di registrazione dei dispositivi.  


### <a name="workload-transition"></a>Transizione del carico di lavoro

*Si applica a tutte le versioni*

Grafico a barre con il numero di dispositivi passati a Microsoft Intune per i carichi di lavoro disponibili. (L'elenco dei carichi di lavoro varia in base alla versione di Configuration Manager. Per altre informazioni, vedere [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune).)

Passare il mouse su una sezione del grafico per visualizzare il numero di dispositivi di cui è stata eseguita la transizione per il carico di lavoro. 
 ![Grafico a barre della transizione dei carichi di lavoro](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla co-gestione, vedere:
 - [Co-gestione per dispositivi Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Preparare i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare)

    
