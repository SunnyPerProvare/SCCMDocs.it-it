---
title: Creare linee di base di configurazione
titleSuffix: Configuration Manager
description: Creare linee di base di configurazione in System Center Configuration Manager da distribuire in una raccolta.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 10b7d0c026ab7af0f5b1964539a70f74f13c079e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421536"
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Creare linee di base di configurazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Le linee di base di configurazioni in System Center Configuration Manager contengono elementi di configurazione predefiniti e, facoltativamente, altre linee di base di configurazione. Dopo aver creato una linea di base di configurazione, è possibile distribuirla in una raccolta in modo che i dispositivi in tale raccolta la scarichino e valutino la propria conformità in base a essa.  

 Le linee di base di configurazione in Configuration Manager possono contenere revisioni specifiche degli elementi di configurazione o possono essere configurate in modo da usare sempre la versione più recente di un elemento di configurazione. Per altre informazioni sulle revisioni dell'elemento di configurazione, vedere [Attività di gestione per i dati di configurazione](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Esistono due metodi che è possibile usare per creare le linee di base di configurazione:  

-   Importare i dati di configurazione da un file. Per avviare l' **Importazione guidata dei dati di configurazione**, nel nodo **Elementi di configurazione** o **Linee di base di configurazione** nell'area di lavoro **Asset e conformità** fare clic su **Importa dati di configurazione**.  

-   Usare la finestra di dialogo **Crea linea di base di configurazione** per creare una nuova linea di base di configurazione.  

Per creare una linea di base di configurazione mediante la finestra di dialogo **Crea linea di base di configurazione**, usare la procedura seguente:  

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

2. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea linea di base di configurazione**.  

3. Nella finestra di dialogo **Crea linea di base di configurazione** immettere un nome univoco e una descrizione per la linea di base di configurazione. È possibile usare un massimo di 255 caratteri per il nome e 512 caratteri per la descrizione.  

4. L'elenco **Dati configurazione** visualizza tutti gli elementi di configurazione o le linee di base di configurazione incluse in questa linea di base di configurazione. Fare clic su **Aggiungi** per aggiungere un nuovo elemento di configurazione o una nuova linea di base di configurazione all'elenco. È possibile scegliere uno degli elementi seguenti:  

   - **Elementi di configurazione**  

   - **Aggiornamenti software**  

   - **Linee di base di configurazione**  
     > [!IMPORTANT]
     > È necessario limitare ogni linea di base di configurazione a non più di 1000 aggiornamenti software.
5. Usare l'elenco **Modifica scopo** per specificare il comportamento di un elemento di configurazione selezionato nell'elenco **Dati di configurazione**. È possibile selezionare uno degli elemento seguenti:  

   -   **Richiesto**: la linea di base di configurazione viene valutata come non conforme se l'elemento di configurazione non viene rilevato in un dispositivo client. Se viene rilevato, viene valutata come conforme  

   -   **Facoltativo**: l'elemento di configurazione viene valutato solo a livello di conformità se l'applicazione a cui fa riferimento viene trovata nei computer client. Se l'applicazione non viene trovata, la linea di base di configurazione non viene contrassegnata come non conforme (applicabile solo agli elementi di configurazione dell'applicazione).  

   -   **Non consentito**: la linea di base di configurazione viene valutata come non conforme se l'elemento di configurazione viene rilevato nei computer client (applicabile solo agli elementi di configurazione dell'applicazione).  

   > [!NOTE]
   >  L'elenco **Modifica scopo** è disponibile solo se è stata selezionata l'opzione **Questo elemento di configurazione contiene le impostazioni dell'applicazione** nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**.  

6. Usare l'elenco **Modifica revisione** per selezionare un oggetto specifico o l'ultima revisione dell'elemento di configurazione per valutare la conformità nei dispositivi client o selezionare **Utilizza sempre più recente** per usare sempre l'ultima revisione. Per altre informazioni sulle revisioni dell'elemento di configurazione, vedere [Attività di gestione per i dati di configurazione](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Per rimuovere un elemento di configurazione dalla linea di base di configurazione, selezionare un elemento di configurazione e quindi fare clic su **Rimuovi**.  

8. A partire dalla versione 1806, è possibile selezionare l'opzione **Applica sempre questa baseline per client con co-gestione**. Quando è selezionata, la linea di base verrà applicata anche ai client gestiti da Intune.  Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune. 

9. Facoltativamente, fare clic su **Categorie** per assegnare alla linea di base le categorie per la ricerca e il filtro. 

10. Fare clic su **OK** per chiudere la finestra di dialogo **Crea linea di base di configurazione** e creare una nuova linea di base di configurazione.  

>[!NOTE]
> Se si modifica una linea di base esistente, ad esempio impostando l'opzione **Applica sempre questa baseline per client con co-gestione**, incrementerà la versione del contenuto della linea di base. I client dovranno valutare la nuova versione per aggiornare il report della linea di base. 