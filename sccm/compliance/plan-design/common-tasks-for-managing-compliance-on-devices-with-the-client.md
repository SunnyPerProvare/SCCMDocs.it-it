---
title: Attività comuni di gestione della conformità
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni di conformità di Configuration Manager in alcuni scenari comuni.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: da92506d291ca24af807db7b4f4b73473359e12f
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "70890654"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Attività comuni per la gestione della conformità nei dispositivi con il client di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo fornisce un'introduzione all'uso di System Center Configuration Manager impostazioni di conformità grazie ad alcuni scenari comuni che è possibile riscontrare.  

 Se si ha già familiarità con le impostazioni di conformità, è possibile trovare informazioni dettagliate su tutte le funzionalità usate in [Elementi di configurazione per dispositivi gestiti con il client di System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Prima di iniziare, vedere [Introduzione alle impostazioni di conformità](../../compliance/get-started/get-started-with-compliance-settings.md) per apprendere alcune nozioni di base sulle impostazioni di conformità. Per informazioni sui prerequisiti necessari, vedere [pianificare e configurare le impostazioni di conformità](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) .  

## <a name="general-information-for-each-scenario"></a>Informazioni generali per ogni scenario  
 In ogni scenario verrà creato un elemento di configurazione che esegue un'attività specifica. Per aprire la creazione guidata dell'elemento di configurazione e iniziare, seguire questa procedura:  

1.  Nella console di Configuration Manager selezionare **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

1.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea elemento di configurazione**.  

1.  Nella pagina **generale** della creazione guidata dell'elemento di configurazione, come illustrato nella schermata seguente, specificare un nome e una descrizione per l'elemento di configurazione. Quindi scegliere il tipo di elemento di configurazione appropriato per ogni scenario di questo articolo.  

     ![Pagina generale della Creazione guidata dell'elemento di configurazione](/sccm/mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Scenario: disabilitare il Bluetooth nei dispositivi Windows 10

 In questo scenario il reparto responsabile della sicurezza ha stabilito che la funzionalità Bluetooth dei dispositivi potrebbe essere usata per trasmettere informazioni aziendali riservate all'esterno dell'azienda. Tutti i computer sono stati aggiornati di recente a Windows 10. Si decide di disabilitare Bluetooth su questi dispositivi.  

1. Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Windows 10** e quindi selezionare **Avanti**.  

2. Nella pagina **Piattaforme supportate** della procedura guidata, selezionare tutte le piattaforme Windows 10.  

3. Nella pagina **Impostazioni dispositivo** selezionare **dispositivo**, quindi fare clic su **Avanti**.  

4. Nella pagina **Dispositivo** selezionare **Non consentito** come valore per **Bluetooth**.  

5. Selezionare **Monitora e aggiorna impostazioni non conformi** per assicurarsi che la modifica venga applicata a tutti i dispositivi Windows 10.  

6. Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'articolo [Attività comuni per la creazione e la distribuzione di linee base di configurazione con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scenario: Correggere un valore non corretto del Registro di sistema nei computer desktop Windows

> [!NOTE] 
> Nei computer Mac che eseguono il client di Configuration Manager è possibile eseguire la valutazione di conformità in due modi:  
> - Valutare un file di preferenze (plist) di Mac OS X.
> - Usare uno script personalizzato e valutare i risultati restituiti dallo script.  
>
>Per altre informazioni, vedere [Come creare elementi di configurazione per dispositivi Mac OS X gestiti con il client di System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 In questo scenario si scopre che un'importante app line-of-business non viene eseguita correttamente in alcuni computer Windows 8.1 gestiti. Si scopre che il problema è causato da una chiave del Registro di sistema denominata **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**, che in alcuni computer è impostata sul valore **0**. Affinché l'app line-of-business venga eseguita correttamente, questo valore deve essere impostato su **1**.  

 In questa procedura verrà creato un elemento di configurazione che consente di monitorare e risolvere automaticamente i valori delle chiavi del Registro di sistema non corretti trovati.  

1. Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Desktop e server di Windows (personalizzato)** e quindi selezionare **Avanti**.  

2. Nella pagina **Piattaforme supportate** della procedura guidata selezionare **Windows 8.1** (per assicurarsi che l'elemento di configurazione venga applicato solo ai computer interessati).  

3. Nella pagina **Impostazioni** selezionare **Nuova** per creare una nuova impostazione.  

4. Nella scheda **Generale** della finestra di dialogo **Crea impostazione** configurare queste impostazioni:  

   -   **Nome** > **Impostazione di esempio**  

   -   **Tipo di impostazione** > **Valore del Registro di sistema**  

   -   **Tipo di dati** > **Numero intero** (perché il valore contiene solo un numero)  

   -   **Hive** > **HKEY_LOCAL_MACHINE**  

   -   **Chiave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valore** > **1** (il valore richiesto)  

5. Nella scheda **regole di conformità** della finestra di dialogo **Crea impostazione** Selezionare **nuovo**. Nella finestra di dialogo **Crea regola** configurare le impostazioni seguenti:  

   -   **Nome** > **Regola di esempio**  

   -   **Impostazione selezionata** > Verificare che l'impostazione selezionata sia **Impostazione di esempio**.

   -   **Tipo di regola** > **Valore**  

   -   **L'impostazione deve essere conforme alla seguente regola** > Verificare che il nome dell'impostazione sia corretto e configurare l'opzione per specificare che il valore dell'impostazione deve essere uguale **1**.  

   -   **Monitora e aggiorna le regole non conformi, se supportato** > Selezionare questa casella di controllo per assicurarsi che Configuration Manager reimposti il valore della chiave del Registro di sistema sul valore corretto nel caso in cui sia errato.  

6. Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'articolo [Attività comuni per la creazione e la distribuzione di linee base di configurazione](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="next-steps"></a>Passaggi successivi

[Creare e distribuire linee di base di configurazione](/sccm/compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines)
