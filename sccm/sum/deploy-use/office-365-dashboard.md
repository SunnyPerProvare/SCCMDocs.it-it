---
title: Dashboard di Gestione client di Office 365
titleSuffix: Configuration Manager
description: Esaminare le informazioni sul client Office 365 dal dashboard di Gestione client di Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf13e3389ec610ffacb06f56278113eb84a6089b
ms.sourcegitcommit: edc7a5ad6a2eb72d0448d4689b9534f7e6f4d2b7
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73623098"
---
# <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365

A partire da Configuration Manager versione 1802, è possibile esaminare le informazioni sul client Office 365 dal dashboard di Gestione client di Office 365. Il dashboard di Gestione client di Office 365 visualizza un elenco di dispositivi rilevanti quando vengono selezionate le sezioni del grafico. <!--1357281 -->

## <a name="prerequisites"></a>Prerequisiti

### <a name="enable-hardware-inventory"></a>Abilitare l'inventario hardware

I dati visualizzati nel dashboard di gestione client di Office 365 provengono dall'inventario hardware. Abilitare l'inventario hardware e selezionare la classe **Configurazioni di Office 365 ProPlus** di tale inventario per visualizzare i dati nel dashboard.
 
1. Abilitare l'inventario hardware, se non è ancora stato fatto. Per altri dettagli, vedere [Configurare l'inventario hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. Nella console di Configuration Manager passare a **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  
3. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
4. Nel **Impostazioni Client predefinite** nella finestra di dialogo fare clic su **l'inventario Hardware**.  
5. Nel **le impostazioni del dispositivo** elenco, fare clic su **Imposta classi**.  
6. Nella finestra di dialogo **Classi di inventario hardware** selezionare **Office 365 ProPlus Configurations**.  
7. Fare clic su **OK** per salvare le modifiche e chiudere il **classi di inventario Hardware** nella finestra di dialogo.

Il dashboard di Gestione client di Office 365 inizia a visualizzare i dati in base all'inventario hardware.

### <a name="internet-connectivity-for-clients"></a>Connettività Internet per i client

*(Introdotta nella versione 1906 come prerequisito)*

A partire dalla versione 1906, i dispositivi in cui è installato Office necessitano di connettività Internet per popolare le informazioni sul componente aggiuntivo per il dashboard di conformità per l' [aggiornamento di office 365 ProPlus](#bkmk_readiness-dash). I dispositivi scaricano un file di conformità del componente aggiuntivo dalla rete per la [distribuzione di contenuti di Office](https://docs.microsoft.com/office365/enterprise/content-delivery-networks#the-office-365-cdn). Questo file contiene l'elenco completo dei componenti aggiuntivi noti a Microsoft e i dettagli delle prestazioni previste in Office 365 ProPlus. Ogni dispositivo utilizza le informazioni del file per determinare la compatibilità dei componenti aggiuntivi. Se un dispositivo non è in grado di scaricare il file, avrà lo stato di conformità dei componenti aggiuntivi della **revisione delle esigenze**.

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualizzazione del dashboard di Gestione client di Office 365

Per visualizzare il dashboard di Gestione client di Office 365, nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**. Nella parte superiore del dashboard, usare l'impostazione a discesa **Raccolta** per filtrare i dati del dashboard in base ai membri di una raccolta specifica. A partire da Configuration Manager versione 1802, il dashboard di gestione client di Office 365 visualizza un elenco di dispositivi pertinenti quando vengono selezionate le sezioni del grafico.

Il dashboard di Gestione client di Office 365 presenta sotto forma di grafico le informazioni seguenti:

- Numero di client di Office 365
- Versioni dei client di Office 365
- Lingue dei client di Office 365
- Canali client di Office 365 Per altre informazioni, vedere [Panoramica dei canali di aggiornamento per Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="bkmk_o365_readiness"></a> Integrazione per l'idoneità per Office 365 ProPlus
<!--3735402-->
A partire da Configuration Manager versione 1902 è possibile usare il dashboard per identificare in modo attendibile i dispositivi pronti per l'aggiornamento a Office 365 ProPlus. Questa integrazione offre informazioni dettagliate sui problemi di compatibilità potenziali con i componenti aggiuntivi e le macro di Office nell'ambiente. Quindi è possibile usare Configuration Manager per distribuire Office nei dispositivi pronti.

Il dashboard di Gestione client di Office 365 include un nuovo riquadro, **Preparazione aggiornamenti di Office 365 ProPlus**. Questo riquadro è un grafico a barre dei dispositivi negli stati seguenti:
- Valutazione non eseguita
- Pronto per l'aggiornamento
- Revisione necessaria

Selezionare uno stato per eseguire il drill-through a un elenco di dispositivi. Questo report di conformità visualizza altri dettagli sui dispositivi. Include colonne per lo stato di compatibilità di componenti aggiuntivi e macro per Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Prerequisiti per l'integrazione con la preparazione per Office 365 ProPlus

- Attivare l'inventario hardware nelle impostazioni client. Per altre informazioni, vedere la sezione [Prerequisiti](#prerequisites).  

- Il dispositivo richiede la connettività alla rete per la distribuzione di contenuti (CDN, Content Delivery Network) di Office per scaricare un file di conformità dei componenti aggiuntivi. Per altre informazioni, vedere [Reti per la distribuzione di contenuti](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Se il dispositivo non riesce a scaricare questo file, lo stato dei componenti aggiuntivi è *Revisione necessaria*.  

    > [!Note]  
    > Per questa funzionalità non viene inviato nessun dato a Microsoft.  

### <a name="bkmk_ort"></a> Conformità dettagliata per le macro

Per impostazione predefinita l'agente di analisi esamina l'elenco dei file usati di recente (MRU) in ogni dispositivo. Quindi conteggia i file di questo elenco che supportano le macro. I file possono essere dei tipi seguenti:
- Formati di file Office con attivazione macro, quali cartelle di lavoro di Excel con attivazione macro (file con estensione xlsm) o documenti di Word con attivazione macro (file con estensione docm)  
- Formati di Office meno recenti che non indicano se è presente contenuto con macro. Ad esempio una cartella di lavoro di Excel 97-2003 (file con estensione xls).

Se sono necessarie informazioni più dettagliate sulla compatibilità delle macro, distribuire il **Toolkit di conformità per Office** per analizzare il codice all'interno dei file di macro. Controlla se sono presenti potenziali problemi di compatibilità. Ad esempio, il file potrebbe usare una funzione che è stata modificata in una versione più recente di Office. Dopo l'esecuzione di Readiness Toolkit per Office, i risultati ottenuti possono essere usati da Configuration Manager. Questi dati aggiuntivi migliorano i calcoli di conformità dei dispositivi. Per altre informazioni, vedere [Valutare la compatibilità delle applicazioni per Office 365 ProPlus tramite Readiness Toolkit](https://aka.ms/readinesstoolkit).

## <a name="bkmk_readiness-dash"></a> Dashboard Preparazione aggiornamenti per Office 365 ProPlus

*(Funzionalità introdotta nella versione 1906)*

<!--4021125-->
Per individuare i dispositivi pronti per l'aggiornamento a Office 365 ProPlus, a partire dalla versione 1906 è disponibile un dashboard di preparazione. Include il riquadro **Preparazione aggiornamenti di Office 365 ProPlus** rilasciato in Configuration Manager Current Branch versione 1902. I nuovi riquadri seguenti di questo dashboard consentono di valutare l'idoneità di componenti aggiuntivi e macro di Office:

- Distribuzione
- Idoneità del dispositivo
- Idoneità dei componenti aggiuntivi
- Dichiarazioni di supporto dei componenti aggiuntivi
- Componenti aggiuntivi principali in base al numero di versione
- Number of devices that have macros (Numero di dispositivi con macro)
- Idoneità delle macro
- Avvisi di macro

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Uso del dashboard Preparazione aggiornamenti per Office 365 ProPlus

Dopo aver verificato i [prerequisiti](#prerequisites), usare le istruzioni seguenti per usare il Dashboard:
 
1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software** ed espandere **Gestione client di Office 365**.
1. Selezionare il nodo **Office 365 ProPlus preparazione aggiornamenti** .
1. Modificare la **raccolta** e l' **architettura di Office di destinazione** per modificare le informazioni inoltrate nel dashboard.

![Dashboard Preparazione aggiornamenti per Office 365 ProPlus](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Dashboard Preparazione aggiornamenti per Office 365 ProPlus](./media/4021125-office-365-to-add-ins.png)

![Dashboard Preparazione aggiornamenti per Office 365 ProPlus](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>Informazioni sulla conformità dei dispositivi

Una volta valutato il componente aggiuntivo e l'inventario delle macro in ogni dispositivo, i dispositivi vengono raggruppati in base alle informazioni. I dispositivi il cui stato è elencato come **pronto per l'aggiornamento** non hanno probabilmente problemi di compatibilità.

Selezionando la categoria **pronto per l'aggiornamento** nel grafico vengono visualizzati altri dettagli sui dispositivi nella raccolta di limitazione. È possibile esaminare l'elenco dei dispositivi, effettuare selezioni in base ai requisiti aziendali e creare una nuova raccolta di dispositivi dalla selezione. Usare la nuova raccolta per distribuire Office 365 ProPlus con Configuration Manager.

I dispositivi che potrebbero essere a rischio di problemi di compatibilità sono contrassegnati come **revisione delle esigenze**. Questi dispositivi possono richiedere un'azione da intraprendere prima di aggiornarli a Office 365 ProPlus. Ad esempio, è possibile aggiornare i componenti aggiuntivi critici a una versione più recente.

### <a name="add-in-information"></a>Informazioni sul componente aggiuntivo

 In ogni dispositivo viene raccolto un inventario di tutti i componenti aggiuntivi installati. L'inventario viene quindi confrontato con le informazioni fornite da Microsoft sulle prestazioni dei componenti aggiuntivi in Office 365 ProPlus. Se viene individuato un componente aggiuntivo che probabilmente causa problemi dopo l'aggiornamento, tutti i dispositivi con il componente aggiuntivo vengono contrassegnati per la revisione.

### <a name="macro-information"></a>Informazioni macro

Configuration Manager esamina i file usati più di recente in ogni dispositivo. Conta i file in questo elenco che supportano le macro, inclusi i tipi seguenti:

- Formati di file di Office abilitati per macro.
- Formati di Office meno recenti, che non indicano se il contenuto della macro è presente.

Se sono necessarie informazioni più dettagliate sulla compatibilità delle macro, distribuire il **Toolkit di conformità per Office** per analizzare il codice all'interno dei file di macro. I risultati possono essere prelevati dall'agente di inventario hardware di Configuration Manager quando si seleziona l'opzione per i **documenti di Office usati più di recente e i componenti aggiuntivi installati nel computer**. I dati aggiuntivi possono migliorare il calcolo della conformità dei dispositivi. Per altre informazioni, vedere [Valutare la compatibilità delle applicazioni per Office 365 ProPlus tramite Readiness Toolkit](https://aka.ms/readinesstoolkit).


## <a name="next-steps"></a>Passaggi successivi

[Gestire Office 365 ProPlus con Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates)
