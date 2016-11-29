---
title: Configurare gli avvisi di Endpoint Protection | System Center Configuration Manager
description: Informazioni su come configurare gli avvisi di Endpoint Protection in Microsoft System Center 2012 Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 38abfd1823972f8fea9966d74ae7c00a48baeb8b


---

#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurare gli avvisi di Endpoint Protection in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 È possibile configurare gli avvisi di Endpoint Protection in Microsoft System Center Configuration Manager per notificare agli utenti amministratori se si verificano eventi specifici nella gerarchia, ad esempio un'infezione da malware. Le notifiche vengono visualizzate nel dashboard di Endpoint Protection della console di Configuration Manager nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** o possono essere inviate tramite posta elettronica agli utenti specificati.

 Seguire i passaggi e le procedure supplementari seguenti di questo argomento per configurare gli avvisi per Endpoint Protection in Configuration Manager.

> [!IMPORTANT]
>  Per configurare gli avvisi per Endpoint Protection, è necessario avere l'autorizzazione **Applicazione protezione** per le raccolte.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Procedura per configurare gli avvisi per Endpoint Protection in Configuration Manager

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.

3.  Nell'elenco **Raccolte dispositivi** selezionare la raccolta per cui configurare gli avvisi e quindi nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà**.

    > [!NOTE]
    >  Non è possibile configurare avvisi per raccolte di utenti.

4.  Nella scheda **Avvisi** della finestra di dialogo **Proprietà***<Nome raccolta\>* selezionare **Visualizza questa raccolta nel dashboard di Endpoint Protection** se si vogliono visualizzare i dettagli sulle operazioni antimalware per questa raccolta nell'area di lavoro **Monitoraggio** della console di Configuration Manager console.

    > [!NOTE]
    >  Questa opzione non è disponibile per la raccolta **Tutti i sistemi** .

5.  Nella scheda **Avvisi** della finestra di dialogo **Proprietà***<Nome raccolta\>* fare clic su **Aggiungi**.

6.  Nella sezione **Genera un avviso quando si applicano queste condizioni** della finestra di dialogo **Aggiungi avvisi nuova raccolta**, selezionare gli avvisi che devono essere generati da Configuration Manager se si verificano gli eventi di Endpoint Protection specificati e fare clic su **OK**.

7.  Nell'elenco  **Condizioni** della scheda **Avvisi** selezionare ogni avviso di Endpoint Protection e specificare le informazioni seguenti:

    -   **Nome avviso**: accettare il nome predefinito o immettere un nome nuovo per l'avviso.

    -   **Gravità avviso**: selezionare nell'elenco il livello di avviso da visualizzare nella console di Configuration Manager.

8.  A seconda dell'avviso selezionato, specificare le informazioni aggiuntive seguenti:

    -   **Rilevamento malware**: questo avviso viene generato se viene rilevato un malware in un computer della raccolta monitorata. **Soglia di rilevamento malware**: specifica i livelli di rilevamento di malware in base al quale viene generato questo avviso:

        -   **Alto - Tutti i rilevamenti**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware, indipendentemente dall'azione eseguita dal client di Endpoint Protection.

        -   **Medio - Rilevato, azione in sospeso**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware ed è necessario rimuovere il malware manualmente.

        -   **Basso - Rilevato, ancora attivo**: l'avviso viene generato quando ci sono uno o più computer nella raccolta specificata in cui viene rilevato malware ancora attivo.

    -   **Attacco malware**: questo avviso viene generato se viene rilevato malware specificato su una percentuale determinata di computer nella raccolta monitorata.

        -   **Percentuale di computer con rilevamento malware**: l'avviso viene generato quando la percentuale di computer della raccolta in cui viene rilevato malware supera la percentuale specificata. Specificare una percentuale compresa tra **1** e **99**.

            > [!NOTE]
            >  Il valore di percentuale è basato sul numero di computer nella raccolta, ma esclude i computer in cui non è installato un client di Configuration Manager. Include i computer in cui non è ancora installato il client di Endpoint Protection.

    -   **Rilevamento malware ripetuto**: questo avviso viene generato se viene rilevato un malware specifico un numero di volte superiore al numero specificato durante il numero di ore nei computer della raccolta monitorata. Per configurare questo avviso, specificare le informazioni seguenti:

        -   **Numero di rilevamenti malware** : l'avviso viene generato quando lo stesso malware viene rilevato nei computer nella raccolta per un numero di volte maggiore di quello specificato. Specificare un numero compreso tra **2** e **32**.

        -   **Intervallo per rilevamento (ore)** : specificare l'intervallo di rilevamento (in ore) in cui deve essere raggiunto il numero di rilevamenti di malware. Specificare un numero compreso tra **1** e **168**.

    -   **Rilevamento di più malware**: questo avviso viene generato se più di un numero specificato di tipi di malware viene rilevato durante un numero determinato di ore nei computer della raccolta monitorata. Per configurare questo avviso, specificare le informazioni seguenti:

        -   **Numero di tipi di malware rilevati** : l'avviso viene generato quando viene rilevato il numero specificato di tipi diversi di malware nei computer nella raccolta. Specificare un numero compreso tra **2** e **32**.

        -   **Intervallo per rilevamento (ore)** : specificare l'intervallo di rilevamento, in ore, in cui deve essere raggiunto il numero di rilevamenti di malware. Specificare un numero compreso tra **1** e **168**.

9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà***<Nome raccolta\>*.  

> [!div class="button"]
[Passaggio successivo >](endpoint-definition-updates.md)

> [!div class="button"]
[Indietro >](endpoint-protection-site-role.md)



<!--HONumber=Nov16_HO1-->

