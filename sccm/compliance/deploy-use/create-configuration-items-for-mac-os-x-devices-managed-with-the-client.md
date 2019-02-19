---
title: 'Creare elementi di configurazione per i computer Mac gestiti tramite client '
titleSuffix: Configuration Manager
description: Usare l'elemento di configurazione Mac OS X di System Center Configuration Manager per gestire le impostazioni dei dispositivi Mac OS X.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf610c3310265f8b7dd6b467640617928a51258f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124054"
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Come creare elementi di configurazione per dispositivi Mac OS X gestiti con il client di System Center Configuration Manager
Usare l'elemento di configurazione **Mac OS X (personalizzato)** di System Center Configuration Manager per gestire le impostazioni dei dispositivi Mac OS X gestiti dal client di Configuration Manager.  
  
 Il sistema operativo Mac OS X usa i file elenco delle proprietà (o plist) per archiviare le impostazioni dell'applicazione. Usare le impostazioni di conformità per valutare e correggere le impostazioni in un file elenco delle proprietà. È anche possibile gestire le impostazioni di Mac OS X scrivendo uno script della shell che restituisce un valore che è possibile valutare e correggere in modo da renderlo conforme.  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>Per creare un elemento di configurazione personalizzato di Mac OS X  
  
1. Nella console di Configuration Manager fare clic su **Asset e conformità**.  
  
2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**e quindi fare clic su **Elementi di configurazione**.  
  
3. Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea elemento di configurazione**.  
  
4. Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione**specificare un nome e una descrizione facoltativa per l'elemento di configurazione.  
  
5. In **Specificare il tipo di elemento di configurazione da creare**selezionare **Mac OS X (personalizzato)**.  
  
6. Fare clic su **Categorie** se si vogliono creare e assegnare categorie per facilitare la ricerca e il filtraggio degli elementi di configurazione nella console di Configuration Manager.  
  
7. Nella pagina **Piattaforme supportate** della procedura guidata selezionare le versioni specifiche di Mac OS X che valuteranno l'elemento di configurazione.  
  
8. Nella pagina **impostazioni** della procedura guidata aggiungere le nuove impostazioni che verranno valutate a livello di conformità nei computer Mac. Fare clic su **Nuova** per aprire la finestra di dialogo **Crea impostazione** .  
  
9. Nella finestra di dialogo **Crea impostazione** immettere un nome univoco e una descrizione per l'impostazione.  
  
10. Scegliere il **tipo di impostazione** desiderato e quindi fornire le informazioni necessarie, come illustrato nella tabella seguente:  
  
    -   **Preferenze di Mac OS X** -  
  
        -   **ID applicazione** : specificare l'ID applicazione del file elenco delle proprietà in base al quale si vuole valutare la conformità di una chiave.  
  
             Ad esempio, se si desidera modificare le impostazioni per il browser Safari, è possibile utilizzare **com.apple.Safari.plist**.  
  
        -   **Chiave** : specificare il nome della chiave che si desidera valutare la conformità nei computer Mac. Usare la sintassi seguente: */<dizionario\>/<nomechiave\>*.  
  
            > [!IMPORTANT]  
            >  Il nome chiave fa distinzione tra maiuscole e minuscole e non verrà valutato se è diverso dal nome chiave sul computer Mac. Inoltre, non è possibile modificare il nome chiave dopo che è stato specificato. Se è necessario modificare il nome della chiave, eliminare e ricreare l'impostazione.  
  
    -   **Script** -  
  
        -   **Script di individuazione** : fare clic su **Aggiungi script**e quindi immettere uno script della shell per valutare la conformità delle impostazioni nel computer Mac. Usare il comando **echo** nello script della shell per restituire i valori conformi a Configuration Manager. Configuration Manager usa i risultati restituiti in **STDOUT** per valutare la conformità.  
  
            > [!IMPORTANT]  
            >  Non includere il comando **reboot** nello script di individuazione. Poiché lo script di individuazione viene eseguito a ogni riavvio del client, questo comando comporta il continuo riavvio del computer Mac.  
  
        -   **Script di monitoraggio e aggiornamento (facoltativo)** : facoltativamente, fare clic su **Aggiungi script** e quindi immettere uno script della shell che viene usato per monitorare e aggiornare le impostazioni non conformi rilevate nei computer client Mac.  
  
            > [!IMPORTANT]  
            >  Per evitare di introdurre caratteri di formattazione che il computer Mac non è in grado di interpretare, digitare lo script anziché copiarlo e incollarlo.  
  
11. Scegliere il **tipo di dati** che è il formato in cui la condizione restituisce i dati prima che vengano usati per valutare l'impostazione.  
  
    > [!NOTE]  
    >  Il **a virgola mobile** tipo di dati supporta solo 3 cifre dopo il separatore decimale.  
    >   
    >  Configuration Manager non supporta l'uso del tipo di dati **booleano** per le impostazioni script dell'elemento di configurazione Mac. Al contrario, impostare il tipo di dati su **Integer** e assicurarsi che lo script restituisca un valore intero.  
  
12. Fare clic su **OK** per salvare le impostazioni e chiudere la finestra di dialogo **Crea impostazione** e quindi continuare ad aggiungere tutte le impostazioni necessarie.  
  
13. Nella pagina **Regole di conformità** della procedura guidata specificare le condizioni che definiscono la conformità di un elemento di configurazione. Prima che sia possibile valutare la conformità di un'impostazione, è necessario che tale impostazione disponga almeno di una regola di conformità. Fare clic su **Nuova** per aggiungere una nuova regola.  
  
14. Nel **Create Rule** finestra di dialogo immettere le informazioni seguenti:  
  
    -   **Nome:** immettere un nome per la regola di conformità.  
  
    -   **Descrizione:** immettere una descrizione per la regola di conformità.  
  
    -   **Impostazione selezionata:** fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona impostazione**. Selezionare l'impostazione che si desidera definire una regola per oppure fare clic su **nuova impostazione**. Al termine, fare clic su **selezionare**.  
  
        > [!TIP]  
        >  È inoltre possibile fare clic su **proprietà** per visualizzare informazioni sull'impostazione attualmente selezionata.  
  
    -   **Tipo di regola:** selezionare il tipo di regola di conformità che si vuole usare:  
  
        -   **Valore:** creare una regola che confronta il valore restituito dall'elemento di configurazione con un valore specificato dall'utente.  
  
        -   **Esistenziale** : creare una regola che valuta l'impostazione a seconda se esiste in un dispositivo.  
  
    -   Per il tipo di regola **Valore**specificare le informazioni seguenti:  
  
        -   L'impostazione deve essere conforme alla seguente regola - Selezionare un operatore e un valore la cui conformità viene valutata in base all'impostazione selezionata. È possibile utilizzare gli operatori seguenti:  
  
            -   **È uguale a**  
  
            -   **Diverso da**  
  
            -   **Maggiore di**  
  
            -   **Minore di**  
  
            -   **Tra**  
  
            -   **Maggiore o uguale a**  
  
            -   **Minore o uguale a**  
  
            -   **Uno** : nella casella di testo specificare una voce per ogni riga.  
  
            -   **Nessuno** : nella casella di testo specificare una voce per ogni riga.  
  
        -   **Monitora e aggiorna le regole non conformi, se supportato** : selezionare questa opzione se si vuole monitorare e aggiornare automaticamente le regole non conformi mediante Configuration Manager.  
  
            > [!IMPORTANT]  
            >  È possibile correggere le regole non conformi solo quando l'operatore per la regola è impostato su **Uguale a**.  
  
        -   **Segnalare la non conformità se questa istanza dell'impostazione non viene trovata** : l'elemento di configurazione segnala la mancata conformità se questa impostazione non viene trovata nel computer Mac.  
  
    -   **Gravità della non conformità per i report:** specificare il livello di gravità segnalato nel caso la regola di conformità non venga soddisfatta. I livelli di gravità disponibili sono i seguenti:  
  
        -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
        -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  
  
        -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  
  
        -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  
  
        -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato dal computer client Mac.  
  
    -   Per il tipo di regola **Esistenziale**specificare le informazioni seguenti:  
  
        -   Scegliere una delle opzioni seguenti:  
  
            -   **L'impostazione deve esistere nei dispositivi client**  
  
            -   **L'impostazione non deve esistere in dispositivi client**  
  
        -   **Gravità della non conformità per i report:** specificare il livello di gravità segnalato nel caso la regola di conformità non venga soddisfatta. I livelli di gravità disponibili sono i seguenti:  
  
            -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  
  
            -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Informazioni** per i report di Configuration Manager.  
  
            -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Avviso** per i report di Configuration Manager.  
  
            -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager.  
  
            -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore di tipo **Errore critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato dal computer client Mac.  
  
        > [!NOTE]  
        >  Le opzioni visualizzate potrebbero variare a seconda del tipo di impostazione per cui si sta configurando una regola.  
  
    -   Fare clic su **OK** per chiudere la finestra di dialogo **Crea regola** .  
  
15. Nella **Riepilogo** confermare le impostazioni del nuovo elemento di configurazione e quindi completare la procedura guidata.  
  
    Il nuovo elemento di configurazione viene visualizzato nel nodo **Elementi di configurazione** dell'area di lavoro **Asset e conformità** .  
  
    Se si vuole aggiungere l'elemento di configurazione a una linea di base di configurazione, vedere [Come creare linee di base di configurazione in System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi di configurazione per dispositivi gestiti con il client di System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
