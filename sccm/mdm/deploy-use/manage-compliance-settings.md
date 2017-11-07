---
title: "Gestione della conformità nei dispositivi gestiti con Intune"
titleSuffix: Configuration Manager
description: "Informazioni sulle impostazioni di conformità di System Center Configuration Manager in alcuni scenari comuni."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 97f0ed47447dc5603a65563b0e87ec90bcc1fe42
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>Gestione della conformità nei dispositivi gestiti con Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questi scenari forniscono un'introduzione all'uso delle impostazioni di conformità di System Center Configuration Manager usando alcuni scenari comuni che potrebbero verificarsi.  

 Se si ha già familiarità con le impostazioni di conformità, la documentazione dettagliata su tutte le funzionalità disponibili è reperibile nella sezione [Elementi di configurazione per i dispositivi gestiti con Intune](#configuration-items-for-devices-managed-with-intune).  

 L'articolo [Introduzione alle impostazioni di conformità in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) contiene le nozioni di base sulle impostazioni di conformità e l'articolo [Pianificare e configurare le impostazioni di conformità in System Center Configuration Manager](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) consente di implementare i prerequisiti.  

## <a name="general-information-for-each-scenario"></a>Informazioni generali per ogni scenario  
 In ogni scenario verrà creato un elemento di configurazione che esegue un'attività specifica. Per aprire la Creazione guidata dell'elemento di configurazione, usare la procedura seguente:  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  

4.  Nella scheda **Generale** della Creazione guidata dell'elemento di configurazione mostrata sotto, specificare un nome e una descrizione per l'elemento di configurazione, quindi scegliere il tipo di elemento di configurazione appropriato per ogni scenario di questo argomento.  

     ![Mostra la pagina generale della creazione guidata dell'elemento di configurazione.](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>Scenari per dispositivi Windows 8.1 e Windows 10 gestiti con Intune  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Scenario: Limitare l'accesso all'App Store in tutti i PC Windows  
 In questo scenario si è l'amministratore IT per una società che gestisce informazioni estremamente riservate. Per questo motivo, si applicano restrizioni alle applicazioni che gli utenti possono installare. Si vuole impedire che gli utenti di tutti i PC Windows 10 scarichino app da Windows Store, quindi si intraprendono le azioni seguenti.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Windows 8.1 e Windows 10** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** selezionare tutte le piattaforme Windows 10.  

3.  Nella pagina **Impostazioni dispositivo** selezionare **Store**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Store** selezionare **Non consentito** come valore per **Store applicazioni**.  

5.  Selezionare **Monitora e aggiorna impostazioni non conformi** per assicurarsi che la modifica venga applicata a tutti i PC.  

6.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>Scenari per dispositivi Windows Phone gestiti con Intune  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Scenario: Disabilitare l'uso dell'acquisizione schermo in un dispositivo Windows Phone  
 Questo scenario prevede l'uso di dispositivi Windows Phone 8.1 nell'azienda. Questi dispositivi eseguono un'app di vendita che contiene informazioni riservate. Per proteggere l'azienda, si vuole disabilitare l'uso dell'acquisizione schermo nel dispositivo, che potrebbe essere usato per trasmettere informazioni sensibili all'esterno dell'azienda.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Windows Phone** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** selezionare le piattaforme **Tutti i sistemi operativi Windows Phone 8.1**.  

3.  Nella pagina **Impostazioni dispositivo** selezionare **Dispositivo**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Dispositivo** selezionare **Disabilitato** come valore per **Acquisizione schermo**.  

5.  Selezionare **Monitora e aggiorna impostazioni non conformi** per assicurarsi che la modifica venga applicata a tutti i dispositivi Windows Phone 8.1.  

6.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Scenari per dispositivi iOS e Mac OS X gestiti con Intune  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Scenario: Disabilitare la fotocamera sui dispositivi iOS  
 In questo scenario l'azienda produce disegni per nuovi progetti di prodotti, che contengono informazioni sensibili da non divulgare.  Considerato che la società fornisce iPhone o iPad a tutti i dipendenti, si vuole disabilitare l'uso della fotocamera su tali dispositivi per impedire che venga usata per fotografare i disegni.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **iOS e Mac OS X** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** selezionare le piattaforme per tutti i dispositivi iPhone e iPad.  

3.  Nella pagina **Impostazioni dispositivo** selezionare **Sicurezza**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Sicurezza** selezionare **Non consentito** come valore per **Fotocamera**.  

5.  Selezionare **Monitora e aggiorna impostazioni non conformi** per assicurarsi che la modifica venga applicata a tutti i dispositivi iOS.  

6.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione con System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Scenari per dispositivi Android e Samsung KNOX Standard gestiti con Intune  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Scenario: Richiedere una password per tutti i dispositivi Android 5  
 In questo scenario verrà creato un elemento di configurazione solo per i dispositivi Android 5 che richiede agli utenti di configurare una password di almeno 6 caratteri nei propri dispositivi. Inoltre, se un utente immette per 5 volte una password errata, i dati del dispositivo vengono cancellati.  

1.  Nella pagina **Generale** della Creazione guidata dell'elemento di configurazione selezionare il tipo di elemento di configurazione **Android e Samsung KNOX** , quindi fare clic su **Avanti**.  

2.  Nella pagina **Piattaforme supportate** selezionare solo **Android 5** per assicurarsi che le impostazioni vengano applicate solo a tale piattaforma.  

3.  Nella pagina **Impostazioni dispositivo** selezionare **Password**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Password** configurare le seguenti impostazioni:  

    -   **Richiedi impostazioni password nei dispositivi** > **Richiesta**  

    -   **Lunghezza minima password (caratteri)** > **6**  

    -   **Numero di tentativi di accesso non riusciti prima della cancellazione dei dati dal dispositivo** > **5**  

5.  Completare la procedura guidata per creare l'elemento di configurazione.  

 È ora possibile usare le informazioni contenute nell'argomento [Attività comuni per la creazione e la distribuzione di linee base di configurazione](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) per distribuire nei dispositivi la configurazione creata.  

## <a name="configuration-items-for-devices-managed-with-intune"></a>Elementi di configurazione per i dispositivi gestiti con Intune

I tipi di elementi di configurazione di System Center Configuration Manager elencati di seguito sono disponibili per i dispositivi non gestiti dal client di Configuration Manager, ad esempio i dispositivi registrati con Microsoft Intune.  

 -   [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti con Intune](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [Come creare elementi di configurazione per dispositivi Windows Phone gestiti con Intune ](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [Come creare elementi di configurazione per dispositivi iOS e Mac OS X gestiti con Intune](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [Come creare elementi di configurazione per dispositivi Android e Samsung KNOX Standard gestiti con Intune](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
