---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità disponibili nella versione Technical Preview 1711 per System Center Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6353b765f769dfa57ea57926d12bf2b254ba8f68
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Funzionalità della versione Technical Preview 1711 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo presenta le funzionalità disponibili nella versione Technical Preview 1711 per System Center Configuration Manager. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemi noti di questa versione Technical Preview:**
-   **Supporto per Windows 10, versione 1709 (anche noto come Fall Creators Update)**.  A partire da questa versione di Windows, il supporto include più versioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento o di un'immagine del sistema operativo, assicurarsi di selezionare un'[edizione utilizzabile da Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **L'aggiornamento a una nuova versione di anteprima ha esito negativo se il server del sito è in modalità passiva**. Se si esegue una versione di anteprima con il [server del sito primario in modalità passiva](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), è necessario disinstallare il server del sito in modalità passiva prima di poter aggiornare il sito di anteprima alla nuova versione di anteprima. Sarà possibile reinstallare il server del sito in modalità passiva al termine dell'aggiornamento del sito.

  Per disinstallare il server del sito in modalità passiva:
  1. Nella console passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e quindi selezionare il server del sito in modalità passiva.
  2. Nel riquadro **Ruoli sistema del sito** fare clic con il pulsante destro del mouse sul ruolo **Server del sito** e quindi scegliere **Rimuovi ruolo**.
  3. Fare clic con il pulsante destro del mouse sul server del sito in modalità passiva e quindi scegliere **Elimina**.
  4. Dopo la disinstallazione del server del sito, nel server del sito primario attivo riavviare il servizio **CONFIGURATION_MANAGER_UPDATE**.

**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Miglioramenti apportati alla funzionalità Esegui la sequenza di attività
<!-- 1261338 -->

In questa anteprima tecnica è stato migliorato il passaggio Esegui la sequenza di attività. I miglioramenti comprendono:

 - Supporto per tutti gli scenari di distribuzione del sistema operativo da Software Center, PXE e dai supporti.
 - Miglioramenti apportati alle operazioni della console, come copia, importazione, esportazione e generazione di avvisi durante l'eliminazione di oggetti.
 - Supporto per la procedura guidata **Crea file di contenuto di pre-installazione**.
 - Integrazione con la verifica della distribuzione.
 - Il passaggio Esegui la sequenza di attività può ora essere usato a più livelli di sequenze di attività e non solo in un'unica relazione padre/figlio. Poiché le relazioni a più livelli aggiungono complessità, usarle con attenzione. Queste relazioni vengono comunque controllate per individuare i riferimenti circolari.

### <a name="try-it-out"></a>Verifica  

Provare a completare le attività seguenti e quindi inviare **Feedback** dalla scheda **Home** della barra multifunzione per comunicarci come è andata:

1. Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale**, quindi fare clic su **Run Task Sequence** (Esegui sequenza di attività).
2. Fare clic su **Sfoglia** per selezionare la sequenza di attività figlio.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Consentire l'interazione utente durante l'installazione di un'applicazione <!-- 1356976 -->

Con questa anteprima è possibile consentire a un utente finale di interagire con un'applicazione durante l'esecuzione della sequenza di attività. Ad esempio, è possibile eseguire un processo di installazione che chiede all'utente finale diverse opzioni. Nei programmi di installazione di alcune applicazioni non è possibile disattivare le richieste all'utente, in quanto il processo di installazione può richiedere valori di configurazione specifici noti solo all'utente. Questa funzionalità consente di gestire questi scenari di installazione.

### <a name="try-it-out"></a>Verifica

Provare a completare le attività seguenti e quindi usare **Commenti e suggerimenti** nella scheda **Home** della barra multifunzione per informare Microsoft sull'andamento della procedura:

1.  Creare o modificare un'applicazione. Per altre informazioni, vedere [Creare applicazioni con System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Scegliere la scheda **Esperienza utente** in **Proprietà Windows Installer (file \*msi)**.

    b. Selezionare **Installa per sistema** per **Comportamento di installazione**.

    c. Selezionare **Indipendentemente dalla connessione degli utenti** per **Requisiti di accesso**.

    d. Selezionare **Normale** per **Visibilità del programma di installazione**. È possibile scegliere tra tre opzioni: **Ridotta a icona**, **Normale** o **Ingrandita**.

    e. Selezionare la casella **Consenti agli utenti di visualizzare e interagire con il programma**.

2.  Creare o modificare una sequenza di attività per installare l'applicazione tramite il passaggio **Installa applicazione**. Per altre informazioni, vedere [Installa applicazione](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) in [Passaggi della sequenza di attività in System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Sequenza di attività di creazione dell'immagine dopo il passaggio Installa Windows e Configuration Manager.

    b. Sequenza di attività di aggiornamento sul posto nel gruppo Post-elaborazione.

3.  Distribuire la sequenza di attività in un client.
4.  Installare la sequenza di attività da Software Center.

Durante l'avanzamento della sequenza di attività, l'interfaccia di installazione dell'applicazione viene visualizzata nel dispositivo dell'utente finale di destinazione. L'avanzamento della sequenza di attività viene sospeso fino a quando l'utente finale non completa il flusso di lavoro di installazione dell'applicazione.

### <a name="install-using-the-wizard"></a>Installare l'applicazione tramite la procedura guidata

È anche possibile usare questa funzionalità per distribuire un'app tramite la procedura guidata.

1. Creare o modificare un'applicazione.
2. Distribuire l'applicazione in un client.
3. Installare l'applicazione da Software Center. Verrà visualizzata l'interfaccia di installazione dell'applicazione. L'utente finale deve seguire la procedura guidata di installazione dell'applicazione per installare correttamente l'applicazione.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sull'installazione o l'aggiornamento del ramo Technical Preview, vedere [Technical Preview per System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
