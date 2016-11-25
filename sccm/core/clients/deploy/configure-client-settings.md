---
title: Configurare le impostazioni client | System Center Configuration Manager
description: Selezionare le impostazioni client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Come configurare le impostazioni client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile gestire tutte le impostazioni client in System Center Configuration Manager dal nodo **Impostazioni client** nell'area di lavoro **Amministrazione** della console di Configuration Manager. Modificare le impostazioni predefinite quando si desidera configurare le impostazioni per tutti gli utenti e i dispositivi nella gerarchia per cui non sono applicate impostazioni personalizzate. Se si desidera applicare impostazioni diverse solo alcuni utenti o dispositivi, creare delle impostazioni personalizzate e distribuirle alle raccolte.  

> [!NOTE]  
>  È inoltre possibile usare gli elementi di configurazione per gestire i client per la valutazione, il controllo e la correzione della conformità di configurazione dei dispositivi. Per altre informazioni, vedere [Garantire la conformità dei dispositivi con System Center Configuration Manage](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> Come configurare le impostazioni client predefinite  

 Usare la seguente procedura per configurare le impostazioni client predefinite per tutti i client nella gerarchia.  

#### <a name="to-configure-the-default-client-settings"></a>Per configurare le impostazioni client predefinite  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**e quindi selezionare **Impostazioni client predefinite**.  

3.  Nella scheda **Home** fare clic su **Proprietà**.  

4.  Visualizzare e configurare le impostazioni client per ogni gruppo di impostazioni nel riquadro di spostamento. Per altre informazioni su ogni impostazione, vedere [Informazioni sulle impostazioni client in Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

5.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni client predefinite** .  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione [Avviare il recupero criteri per un client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Come gestire i client in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> Come creare e distribuire le impostazioni client personalizzate  
 Usare la seguente procedura per configurare e distribuire le impostazioni personalizzate per una raccolta selezionata di utenti o dispositivi. Quando queste impostazioni personalizzate vengono distribuite, sostituiscono le impostazioni client predefinite.  

> [!NOTE]  
>  Prima di iniziare questa procedura, assicurarsi di disporre di una raccolta contenente gli utenti o i dispositivi che richiedono queste impostazioni client personalizzate.  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>Per configurare e distribuire le impostazioni client personalizzate  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea impostazioni client personalizzate**e quindi su una delle seguenti opzioni a seconda che si desideri creare impostazioni client personalizzate per i dispositivi o per gli utenti:  

    -   **Crea impostazioni dispositivo client personalizzate**  

    -   **Crea impostazioni utente client personalizzate**  

4.  Nella finestra di dialogo **Crea impostazioni dispositivo client personalizzate** o **Crea impostazioni utente client personalizzate** specificare un nome univoco per le impostazioni personalizzate e una descrizione facoltativa.  

5.  Selezionare una o più delle caselle di controllo disponibili che mostrano un gruppo di impostazioni.  

6.  Fare clic sulle impostazioni del primo gruppo dal riquadro di spostamento e quindi visualizzare e configurare le impostazioni personalizzate disponibili. Ripetere questo processo per le impostazioni dei gruppi rimanenti. Per informazioni su ogni impostazione client, vedere [Informazioni sulle impostazioni client in Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

7.  Fare clic su **OK** per chiudere la finestra di dialogo **Crea impostazioni dispositivo client personalizzate** o **Crea impostazioni utente client personalizzate** .  

8.  Selezionare l'impostazione client personalizzata appena creata. Nella scheda **Home** , nel gruppo **Impostazioni client** , fare clic su **Distribuisci**.  

9. Nella finestra di dialogo **Seleziona raccolta** selezionare la raccolta che contiene i dispositivi o gli utenti da configurare con le impostazioni personalizzate e quindi fare clic su **OK**. È possibile controllare la raccolta selezionata facendo clic sulla scheda **Distribuzioni** nel riquadro dei dettagli.  

10. Visualizzare l'ordine dell'impostazione client personalizzata appena creata. Quando sono presenti più impostazioni client personalizzate, vengono applicate in base al numero d'ordine. Se sono presenti conflitti, l'impostazione con il numero d'ordine più basso sostituisce le altre impostazioni. Per modificare il numero d'ordine, nel gruppo **Impostazioni client** della scheda **Home** fare clic su **Sposta elemento in alto** o **Sposta elemento in basso**.  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione [Avviare il recupero criteri per un client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) in [Come gestire i client in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> Come visualizzare le impostazioni client risultanti  
 Una volta distribuite più impostazioni client allo stesso dispositivo, utente o gruppo degli utenti, la definizione delle priorità e la combinazione delle impostazioni possono essere complesse. Usare la procedura seguente per visualizzare le impostazioni del client risultanti calcolate.  

#### <a name="to-view-the-resultant-client-settings"></a>Per visualizzare le impostazioni del client risultanti  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi**, **Utenti**o **Raccolte utenti**.  

3.  Selezionare un dispositivo, un utente o un gruppo di utenti e nel gruppo **Impostazioni client** , selezionare **Impostazioni del client risultanti**.  In alternativa, è possibile fare clic con il pulsante destro del mouse sul dispositivo, sull'utente o sul gruppo di utenti, selezionare **Impostazioni client**e fare clic su **Impostazioni del client risultanti**.  

4.  Selezionare un'impostazione client dal riquadro a sinistra e visualizzare le impostazioni risultanti.  

    > [!NOTE]  
    >  Per visualizzare le impostazioni del client risultante, l'utente connesso deve disporre dell'accesso in lettura alle impostazioni client.  

    > [!NOTE]  
    >  Le impostazioni risultanti visualizzate sono di sola lettura. Per modificare le impostazioni, usare le procedure descritte in precedenza.  



<!--HONumber=Nov16_HO1-->


