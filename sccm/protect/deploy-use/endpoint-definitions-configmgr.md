---
title: Definizioni di malware per Endpoint Protection | System Center Configuration Manager
description: Informazioni su come configurare gli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni ai computer client.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ead791ae0bf9d26ff02bea9a85973d7149b695a5


---

#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>Utilizzo degli aggiornamenti Software di Configuration Manager per distribuire gli aggiornamenti delle definizioni

*Si applica a: System Center Configuration Manager (Current Branch)*


 È possibile configurare gli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni ai computer client. A tale scopo, è necessario configurare regole di distribuzione automatica. Prima di iniziare a creare regole di distribuzione automatica, assicurarsi di aver configurato gli aggiornamenti software di Configuration Manager. Per altre informazioni, vedere [Introduzione agli aggiornamenti software in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).

> [!NOTE]
>  Questa procedura si applica solo agli elementi che devono essere configurati specificatamente per Endpoint Protection. Per altre informazioni sulla Creazione guidata delle regole di distribuzione automatica, vedere [Distribuire automaticamente gli aggiornamenti software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>Per configurare una regola di distribuzione automatica per distribuire aggiornamenti delle definizioni

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.

2.  Nell'area di lavoro **Raccolta software** espandere **Aggiornamenti software**e quindi fare clic su **Regole di distribuzione automatica**.

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea regola di distribuzione automatica**.

4.  Nella pagina **Generale** della **Creazione guidata delle regole di distribuzione automatica**specificare le informazioni seguenti:

    -   **Nome**: immettere un nome univoco per la regola di distribuzione automatica.

    -   **Raccolta**: selezionare la raccolta di computer client in cui distribuire gli aggiornamenti delle definizioni.

        > [!NOTE]
        >  Non è possibile distribuire aggiornamenti delle definizioni in una raccolta di utenti.

5.  Fare clic su **Aggiungi a un gruppo di aggiornamenti software**.

6.  Assicurarsi che la casella di controllo  **Attiva la distribuzione dopo l'esecuzione di questa regola** sia selezionata e quindi fare clic su **Avanti**.

7.  Nella pagina **Impostazioni distribuzione** della procedura guidata, nell'elenco **Livello dettaglio** selezionare **Minimo**e quindi fare clic su **Avanti**.

    > [!NOTE]
    >  Nell'elenco **Livello dettaglio** selezionare **Minimo** (Configuration Manager senza Service Pack) o **Solo messaggi di errore** (Configuration Manager). In questo modo, sarà possibile ridurre il numero di messaggi di stato restituiti dalla distribuzione delle definizioni. Questa configurazione consente di ridurre l'utilizzo dell'elaborazione CPU nei server di Configuration Manager.

8.  Nell'elenco **Filtri proprietà** selezionare la casella di controllo **Classificazione aggiornamento** .

9. Nell'elenco **Criteri di ricerca** fare clic su **<elementi da trovare\>**. Nella finestra di dialogo **Criteri di ricerca** selezionare quindi **Aggiornamenti delle definizioni** nell'elenco **Specificare il valore da cercare**.

10. Fare clic su **OK** per chiudere la finestra di dialogo **Criteri di ricerca** .

11. Nell'elenco **Filtri proprietà** selezionare la casella di controllo **Prodotto** .

12. Nell'elenco **Criteri di ricerca** fare clic su **<elementi da trovare\>**. Nella finestra di dialogo **Criteri di ricerca** selezionare quindi **Forefront Endpoint Protection 2010** , per Windows 8.1 e versioni precedenti, o **Windows Defender** , per Windows 10 e versioni successive, nell'elenco **Specificare il valore da cercare** .

13. Fare clic su **OK** per chiudere la finestra di dialogo **Criteri di ricerca** e quindi fare clic su **Avanti**.

14. Nell'elenco **Filtri proprietà** selezionare la casella di controllo **Sostituito** .

15. Nell'elenco **Criteri di ricerca** fare clic su **<elementi da trovare\>**. Nella finestra di dialogo **Criteri di ricerca** selezionare quindi **No** nell'elenco **Specificare il valore da cercare**.

16. Fare clic su **OK** per chiudere la finestra di dialogo **Criteri di ricerca** e quindi fare clic su **Avanti**.

17. Nella pagina **Pianificazione valutazione** della procedura guidata selezionare l'opzione ** **per consentire l'esecuzione della regola in base a una pianificazione e quindi configurare la pianificazione in base a cui scaricare gli aggiornamenti delle definizioni. Impostare la regola in modo che venga almeno eseguita due ore dopo ogni sincronizzazione del punto di aggiornamento software. Fare clic su **Avanti**.

18. Nella pagina **Pianificazione della distribuzione** della procedura guidata configurare le impostazioni seguenti:

    -   **Tempo basato su**: selezionare **UTC** per fare in modo che tutti i client nella gerarchia installino le definizioni più aggiornate contemporaneamente. Il tempo di installazione effettivo può variare all'interno di una finestra di due ore. Questa è l'impostazione consigliata.

    -   **Tempo disponibile software**: specificare il tempo disponibile per la distribuzione creata da questa regola. Il tempo specificato deve essere almeno un'ora dopo l'esecuzione della regola di distribuzione automatica. Ciò consente di assicurarsi che il contenuto abbia tempo sufficiente per la replica nei punti di distribuzione nella gerarchia. Alcuni aggiornamenti delle definizioni possono includere anche aggiornamenti del motore antimalware, che potrebbero richiedere più tempo per raggiungere i punti di distribuzione.

    -   **Scadenza installazione**: selezionare **Appena possibile**.

        > [!NOTE]
        >  Le scadenze degli aggiornamenti software variano all'interno di un periodo di due ore, per impedire che tutti i client richiedano un aggiornamento contemporaneamente.

19. Fare clic su **Avanti**.

20. Nella pagina **Esperienza utente** della procedura guidata selezionare **Nascondi in Software Center e nascondi tutte le notifiche** nell'elenco **Notifiche utente**.   In questo modo, gli aggiornamenti delle definizioni verranno installati in modo invisibile all'utente. Fare clic su **Avanti**.

21. Nella pagina **Avvisi** della procedura guidata non è necessario configurare avvisi. Endpoint Protection in Configuration Manager genera avvisi che potrebbero essere necessari. Fare clic su **Avanti**.

22. Nella pagina **Impostazioni download** della procedura guidata selezionare il comportamento di download degli aggiornamenti software necessario e quindi fare clic su **Avanti**.

23. Nella pagina **Pacchetto di distribuzione** della procedura guidata selezionare un pacchetto di distribuzione esistente o crearne uno nuovo per contenere i file degli aggiornamenti software associati alla regola.

    > [!NOTE]
    >  È consigliabile inserire gli aggiornamenti delle definizioni in un pacchetto che non contenga altri aggiornamenti software. In questo modo, le dimensioni del pacchetto di aggiornamenti delle definizioni resteranno contenute, consentendo una replica più veloce nei punti di distribuzione.

24. Nella pagina **Punti di distribuzione** della procedura guidata selezionare uno o più punti di distribuzione in cui verrà copiato il contenuto del pacchetto e quindi fare clic su **Avanti**.

25. Nella pagina **Percorso download** della procedura guidata selezionare **Scarica aggiornamenti software da Internet**e quindi fare clic su **Avanti**.

26. Nella pagina **Selezione lingua** della procedura guidata selezionare ogni versione linguistica degli aggiornamenti da scaricare e quindi fare clic su **Avanti**.

27. Completare la Creazione guidata delle regole di distribuzione automatica.

28. Verificare che la nuova regola venga visualizzata nel nodo **Regole di distribuzione automatica** della console di Configuration Manager.


> [!div class="button"]
[Passaggio successivo >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Indietro >](endpoint-configure-alerts.md)



<!--HONumber=Nov16_HO1-->

