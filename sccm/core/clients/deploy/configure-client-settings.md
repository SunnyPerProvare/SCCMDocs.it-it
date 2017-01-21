---
title: Configurare le impostazioni client | Documentazione Microsoft
description: Selezionare le impostazioni client in System Center Configuration Manager.
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 809c7938968b4a6efce6ef37fe7b7baf2c9dd3e7
ms.openlocfilehash: 77e17786302c885052c8861107a49ff826accb65

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Come configurare le impostazioni client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile gestire tutte le impostazioni client in System Center Configuration Manager da **Amministrazione** > **Impostazioni client**. Modificare le impostazioni predefinite quando si desidera configurare le impostazioni per tutti gli utenti e i dispositivi nella gerarchia per cui non sono applicate impostazioni personalizzate. Se si desidera applicare impostazioni diverse solo alcuni utenti o dispositivi, creare delle impostazioni personalizzate e distribuirle alle raccolte.  

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

10. Visualizzare l'ordine dell'impostazione client personalizzata appena creata. Quando sono presenti più impostazioni client personalizzate, vengono applicate in base al numero d'ordine. Se sono presenti conflitti, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni. Per modificare il numero d'ordine, nel gruppo **Impostazioni client** della scheda **Home** scegliere **Sposta elemento in alto** o **Sposta elemento in basso**.  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione [Avviare il recupero criteri per un client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Come gestire i client in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="view-client-settings"></a>Visualizzare le impostazioni client  
 Una volta distribuite più impostazioni client allo stesso dispositivo, utente o gruppo degli utenti, la definizione delle priorità e la combinazione delle impostazioni possono essere complesse. Per visualizzare le impostazioni client:  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi** > **Utenti** o **Raccolte utenti**.  

3.  Selezionare un dispositivo, un utente o un gruppo di utenti e nel gruppo **Impostazioni client** , selezionare **Impostazioni del client risultanti**.  

4.  Selezionare un'impostazione client dal riquadro a sinistra: vengono visualizzate le impostazioni. In questa visualizzazione le impostazioni sono di sola lettura. 

    > [!NOTE]  
    >  Per visualizzare le impostazioni client, è necessario disporre dell'accesso in lettura a Impostazioni client.  

    


<!--HONumber=Dec16_HO3-->


