---
title: Configurare le impostazioni client
titleSuffix: Configuration Manager
description: Selezionare le impostazioni client in System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0405769d3cfc7f77c4ab639ddc0f9ed0cd561366
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334039"
---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Come configurare le impostazioni client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile gestire tutte le impostazioni client in System Center Configuration Manager da **Amministrazione** > **Impostazioni client**. Modificare le impostazioni predefinite quando si desidera configurare le impostazioni per tutti gli utenti e i dispositivi nella gerarchia per cui non sono applicate impostazioni personalizzate. Per applicare impostazioni diverse solo ad alcuni utenti o dispositivi, creare impostazioni personalizzate e distribuirle alle raccolte.  

Per informazioni su ogni impostazione client, vedere [Informazioni sulle impostazioni client in Configuration Manager](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  È inoltre possibile usare gli elementi di configurazione per gestire i client per la valutazione, il controllo e la correzione della conformità di configurazione dei dispositivi. Per altre informazioni, vedere [Garantire la conformità dei dispositivi con System Center Configuration Manage](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configurare le impostazioni client predefinite    

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

3.  Nella scheda **Home** scegliere **Proprietà**.  

4.  Visualizzare e configurare le impostazioni client per ogni gruppo di impostazioni nel riquadro di spostamento.  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione [Avviare il recupero criteri per un client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Come gestire i client in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Creare e distribuire impostazioni client personalizzate  
Quando queste impostazioni personalizzate vengono distribuite, sostituiscono le impostazioni client predefinite. Prima di iniziare questa procedura, assicurarsi di disporre di una raccolta contenente gli utenti o i dispositivi che richiedono queste impostazioni client personalizzate.  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.  

3.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea impostazioni dispositivo client personalizzate** e quindi scegliere una delle opzioni seguenti:  

    -   **Crea impostazioni dispositivo client personalizzate**  

    -   **Crea impostazioni utente client personalizzate**  

4.  Specificare un nome univoco e una descrizione dell'opzione.  

5.  Selezionare una o più delle caselle di controllo che mostrano un gruppo di impostazioni.  

6.  Scegliere ciascun gruppo di impostazioni dal riquadro di spostamento, configurare le impostazioni disponibili e quindi fare clic su **OK**.   

8.  Selezionare l'impostazione client personalizzata creata. Nella scheda **Home**, nel gruppo **Impostazioni client**, scegliere **Distribuisci**.  

9. Nella finestra di dialogo **Seleziona raccolta** selezionare la raccolta appropriata e quindi scegliere **OK**. È possibile controllare la raccolta selezionata facendo clic sulla scheda **Distribuzioni** nel riquadro dei dettagli.  

10. Visualizzare l'ordine dell'impostazione client personalizzata creata. Quando sono presenti più impostazioni client personalizzate, vengono applicate in base al numero d'ordine. Se sono presenti conflitti, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni. Per modificare il numero d'ordine, nel gruppo **Impostazioni client** della scheda **Home** scegliere **Sposta elemento in alto** o **Sposta elemento in basso**.  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione [Avviare il recupero criteri per un client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Come gestire i client in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  



##  <a name="view-client-settings"></a>Visualizzare le impostazioni client  
 Quando vengono distribuite più impostazioni client allo stesso dispositivo, utente o gruppo di utenti, la definizione delle priorità e la combinazione delle impostazioni risultano complesse. Per visualizzare le impostazioni client:  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi** > **Utenti** o **Raccolte utenti**.  

3.  Selezionare un dispositivo, un utente o un gruppo di utenti e nel gruppo **Impostazioni client** , selezionare **Impostazioni del client risultanti**.  

4.  Selezionare un'impostazione client dal riquadro a sinistra: vengono visualizzate le impostazioni. In questa visualizzazione le impostazioni sono di sola lettura. 

    > [!NOTE]  
    >  Per visualizzare le impostazioni client, è necessario disporre dell'accesso in lettura a Impostazioni client.  

    