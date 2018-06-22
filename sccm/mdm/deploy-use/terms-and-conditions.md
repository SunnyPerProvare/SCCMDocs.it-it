---
title: Termini e condizioni
titleSuffix: Configuration Manager
description: Distribuire le condizioni a gruppi di utenti in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cda5f01842f08ccc3e8dfbd17078fe157954d985
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353471"
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>Aggiungere termini e condizioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile distribuire le condizioni di System Center Configuration Manager a gruppi di utenti per spiegare in che modo la registrazione dei dispositivi, l'accesso alle risorse di lavoro e l'uso del Portale aziendale influiscono su dispositivi e utenti. Gli utenti dovranno quindi accettare i termini e le condizioni prima di poter usare il portale aziendale per registrare le app e accedere al lavoro.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Uso dei criteri di termini e condizioni in System Center Configuration Manager  
 È possibile creare e distribuire più set di criteri di termini e condizioni. È anche possibile creare versioni degli stessi termini e condizioni in lingue diverse e distribuirle ai gruppi appropriati.  

## <a name="to-create-a-terms-and-conditions"></a>Per creare termini e condizioni  

1.  Nella console di Configuration Manager passare a **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Termini e condizioni**.  

2.  Fare clic su **Crea termini e condizioni** per creare nuovi termini e condizioni.  

3.  Nella pagina **Generale** specificare le informazioni seguenti:  

    -   **Nome**: nome univoco visualizzato nella console di Configuration Manager  

    -   **Descrizione**: dettagli che consentono di identificare le condizioni nella console di Configuration Manager  

     Fare clic su **Avanti**.  

4.  Nella pagina **Condizioni** specificare le informazioni seguenti:  

    -   **Titolo** - Titolo visualizzato agli utenti nel portale aziendale  

    -   **Testo per le condizioni** - Termini e condizioni visualizzati agli utenti nel portale aziendale  

    -   **Testo in cui vengono spiegate le implicazioni dell'accettazione da parte dell'utente** : etichetta visualizzata agli utenti relativa all'accettazione. **Esempio**: "Accetto le condizioni".  

     Fare clic su **Avanti**.  

5.  Completare la procedura guidata per creare i nuovi termini e condizioni. I nuovi termini e condizioni vengono visualizzati nel nodo Termini e condizioni dell'area di lavoro Asset e conformità.  

## <a name="to-deploy-a-terms-and-conditions"></a>Per distribuire termini e condizioni  

1.  Nella console di Configuration Manager passare ad **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Termini e condizioni**.  

2.  Nell'elenco **Termini e condizioni** selezionare l'elemento da distribuire e quindi fare clic su **Distribuisci**.  

3.  Fare clic su**Sfoglia** per selezionare la **raccolta** in cui si vogliono distribuire i termini e le condizioni, quindi fare clic su **OK**.  

     Quando i dispositivi di destinazione accedono all'app Portale aziendale, verranno visualizzati i termini e le condizioni distribuiti. Gli utenti devono accettare questi termini prima di poter accedere alle risorse aziendali.  

    > [!NOTE]  
    >  Se si distribuisce un set di condizioni in più raccolte di utenti a cui appartiene un utente, tale utente visualizzerà più copie di condizioni identiche all'apertura dell'app Portale aziendale. Poiché gli utenti possono solo accettare o rifiutare tutte le condizioni, non vi è alcun rischio di trovarsi in uno stato di accettazione ambiguo in cui l'utente ha sia accettato che rifiutato le condizioni. Il report di accettazione di termini e condizioni includerà una sola riga per ogni set di condizioni per ogni utente, quindi nel report non possono esserci errori.  

## <a name="to-monitor-terms-and-conditions"></a>Per monitorare termini e condizioni  

1.  È possibile monitorare le distribuzioni di termini e condizioni nella console di Configuration Manager. Nel riquadro di spostamento della console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Distribuzioni**.  

2.  Selezionare la distribuzione di termini e condizioni dall'elenco delle distribuzioni.  

     L'area di riepilogo visualizza le statistiche seguenti:  

    -   **Conforme** : gli utenti hanno accettato la versione più recente di termini e condizioni  

    -   **Erroree**  

    -   **Non conforme** : gli utenti hanno accettato una versione precedente di termini e condizioni  

    -   **Sconosciuto** : gli utenti non hanno accettato termini e condizioni, inclusi quelli senza un dispositivo registrato  

3.  Selezionare una distribuzione di termini e condizioni, quindi scegliere **Esegui riepilogo** per visualizzare lo stato di distribuzione dei singoli utenti.  

     Nella schermata di stato della distribuzione è possibile selezionare le schede di stato per visualizzare gli utenti con lo stato specificato. È possibile fare clic su **Esegui riepilogo** per aggiornare i dati in tutta la gerarchia. Fare clic su **Aggiorna** per aggiornare i dati nella console  

## <a name="to-view--a-terms-and-conditions-report"></a>Per visualizzare un report Termini e condizioni  

1.  Nella console di Configuration Manager passare a **Monitoraggio** > **Panoramica** > **Creazione report** > **Report**.  

2.  Selezionare **Accettazione di termini e condizioni** , quindi fare clic su **Esegui**. Verrà aperto il report Accettazione di termini e condizioni. Il report visualizza ogni utente a cui sono stati distribuiti i termini e le condizioni. I campi includono:  

    -   Nome di termini e condizioni  

    -   Nome utente  

    -   Versione accettata  

    -   Data di accettazione  

    -   Ultima accettazione  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Aggiornamenti e controllo della versione per termini e condizioni  
 Quando si modificano termini e condizioni esistenti, è possibile scegliere il comportamento durante la distribuzione di termini e condizioni. Usare la procedura seguente per aggiornare i termini e le condizioni esistenti.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Come gestire più versioni di termini e condizioni  

1.  Nella console di Configuration Manager passare a **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Termini e condizioni**.  

2.  Selezionare l'istanza di termini e condizioni da modificare, quindi fare doppio clic per aprirla.  

3.  È possibile modificare il contenuto nella pagina **Generale** o **Condizioni** per apportare le necessarie modifiche.  

4.  Nella pagina **Condizioni** è possibile specificare se questa nuova versione dei termini e delle condizioni deve essere accettata da tutti gli utenti oppure se verrà visualizzata solo per i nuovi utenti.  

     È consigliabile incrementare il numero di versione e richiedere l'accettazione ogni volta che si apportano modifiche significative a termini e condizioni. Non modificare il numero di versione corrente se, ad esempio, si correggono errori di digitazione o si modifica la formattazione.

> [!div class="button"]
[< Passaggio precedente](configure-intune-subscription.md)  [Passaggio successivo >](create-service-connection-point.md)
