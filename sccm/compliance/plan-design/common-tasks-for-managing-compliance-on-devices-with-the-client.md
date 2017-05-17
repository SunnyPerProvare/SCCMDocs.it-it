---
title: "Attività comuni di gestione della conformità per dispositivi gestiti da client - Configuration Manager | Microsoft Docs"
description: "Informazioni sulle impostazioni di conformità di System Center Configuration Manager in alcuni scenari comuni."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Attività comuni per la gestione della conformità nei dispositivi con il client System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli scenari presentati in questo argomento forniscono un'introduzione all'uso delle impostazioni di conformità di System Center Configuration Manager usando alcuni scenari comuni che potrebbero verificarsi.  

 Se si ha già familiarità con le impostazioni di conformità, la documentazione dettagliata su tutte le funzionalità disponibili è reperibile nella sezione [Configuration items for devices managed with the System Center Configuration Manager client](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md) (Elementi di configurazione per i dispositivi gestiti con il client di System Center Configuration Manager).  

 Prima di iniziare, leggere [Get started with compliance settings](../../compliance/get-started/get-started-with-compliance-settings.md) (Introduzione alle impostazioni di conformità) per apprendere alcune nozioni sulle impostazioni di conformità e [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità) per implementare i prerequisiti necessari.  

## <a name="general-information-for-each-scenario"></a>Informazioni generali per ogni scenario  
 In ogni scenario verrà creato un elemento di configurazione che esegue un'attività specifica. Per aprire la Creazione guidata dell'elemento di configurazione, usare la procedura seguente:  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella scheda **Generale** della Creazione guidata dell'elemento di configurazione mostrata sotto, specificare un nome e una descrizione per l'elemento di configurazione, quindi scegliere il tipo di elemento di configurazione appropriato per ogni scenario di questo argomento.  

     ![Mostra la pagina generale della creazione guidata dell'elemento di configurazione.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Scenari per dispositivi Windows 10 gestiti con il client di Configuration Manager  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Scenario: Disabilitare l'uso di Bluetooth in dispositivi Windows 10  
 In questo scenario il reparto di sicurezza ha identificato la funzionalità Bluetooth dei dispositivi quale mezzo che potrebbe essere usato per trasmettere informazioni aziendali riservate all'esterno dell'azienda. Di recente tutti i PC sono stati aggiornati a Windows 10 e si decide di disabilitare la funzionalità Bluetooth su questi dispositivi.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Windows 10** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** della procedura guidata, selezionare tutte le piattaforme Windows 10.  

3.  Nella pagina **Impostazioni dispositivo** selezionare **Dispositivo**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Dispositivo** selezionare **Non consentito** come valore per **Bluetooth**.  

5.  Selezionare **Monitora e aggiorna impostazioni non conformi** per assicurarsi che la modifica venga applicata a tutti i dispositivi Windows 10.  

6.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Scenari per computer desktop e server di Windows gestiti con il client di Configuration Manager  
 Nei computer Mac che eseguono il client di Configuration Manager è possibile eseguire la valutazione di conformità in due modi:  

-   Valutare un file di preferenze (plist) di Mac OS X.  

-   Usare uno script personalizzato e valutare i risultati restituiti dallo script.  

 Per altre informazioni, vedere [Come creare elementi di configurazione per dispositivi Mac OS X gestiti con il client di System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scenario: Correggere un valore non corretto del Registro di sistema nei computer desktop Windows  
 In questo scenario si scopre che un'importante app line-of-business non viene eseguita correttamente in alcuni computer gestiti che eseguono Windows 8.1. Dopo alcune indagini, si scopre che il problema è causato da una chiave del Registro di sistema denominata **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** , che in alcuni computer è impostata su un valore di **0** . Affinché l'app line-of-business venga eseguita correttamente, questo valore deve essere impostato su **1**.  

 In questa procedura verrà creato un elemento di configurazione che consente di monitorare e risolvere automaticamente i valori delle chiavi del Registro di sistema non corretti trovati.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Desktop e server di Windows (personalizzato)** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** della procedura guidata selezionare **Windows 8.1** (per verificare che l'elemento di configurazione si applichi solo ai computer interessati).  

3.  Nella pagina **Impostazioni** fare clic su **Nuova** per creare una nuova impostazione.  

4.  Nella scheda **Generale** della finestra di dialogo **Crea impostazione** configurare quanto segue:  

    -   **Nome** > **Impostazione di esempio**  

    -   **Tipo di impostazione** > **Valore del Registro di sistema**  

    -   **Tipo di dati** > **Numero intero** (perché il valore contiene solo un numero)  

    -   **Hive** > **HKEY_LOCAL_MACHINE**  

    -   **Chiave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **Valore** > **1** (il valore richiesto)  

5.  Nella scheda **Regole di conformità** della finestra di dialogo **Crea impostazione** fare clic su **Nuova**, quindi nella finestra di dialogo **Crea regola** configurare quanto segue:  

    -   **Nome** > **Regola di esempio**  

    -   **Impostazione selezionata** : verificare che l'impostazione selezionata sia **Impostazione di esempio**.  

    -   **Tipo di regola** > **Valore**  

    -   **L'impostazione deve essere conforme alla seguente regola** : verificare che il nome dell'impostazione sia corretto e configurare l'opzione per specificare che il valore dell'impostazione deve essere uguale **1**.  

    -   **Monitora e aggiorna le regole non conformi, se supportato**: selezionare questa casella per garantire che Configuration Manager reimposti il valore della chiave del Registro di sistema sul valore corretto nel caso in cui sia errato.  

6.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

