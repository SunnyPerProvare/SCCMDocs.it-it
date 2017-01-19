---
title: Gruppi di limiti per le versioni 1511, 1602 e 1606 | System Center Configuration Manager
description: Usare gruppi di limiti con Configuration Manager versioni 1511, 1602 e 1606.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b64f1f06af1ab4a255b6291b6eb5f85cff99ae63
ms.openlocfilehash: ef408041eb6d0d6716e244d34b9a2a4ebe5cb9cc


---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606

*Si applica a: System Center Configuration Manager (Current Branch)*

Le informazioni contenute in questo argomento si riferiscono specificamente all'uso di gruppi di limiti con le versioni 1511, 1602 e 1606 di System Center Configuration Manager.
Se si usa la versione 1610 o successiva, per informazioni sull'uso di gruppi di limiti riprogettati vedere [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-group/) (Gruppi di limiti) in *Define site boundaries and boundary groups for System Center Configuration Manager* (Definire limiti del sito e gruppi di limiti per System Center Configuration Manager).  


##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 I gruppi di limiti vengono creati per raggruppare logicamente i percorsi di rete correlati (limiti) e semplificare la gestione dell'infrastruttura. Prima di usare un gruppo di limiti è necessario assegnare i limiti ai gruppi di limiti. I client usano la configurazione del gruppo di limiti per:  

-   Assegnazione automatica del sito  

-   Percorso contenuto  

-   Punti di gestione preferiti. Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dalla configurazione del gruppo di limiti. Vedere la procedura seguente *Per abilitare l'uso dei punti di gestione preferiti*  

Quando si configurano i gruppi di limiti, si aggiungono uno o più limiti al gruppo di limiti e quindi si configurano le impostazioni aggiuntive per l'uso da parte dei client presenti in tali limiti.  

#### <a name="to-create-a-boundary-group"></a>Per creare un gruppo di limiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea gruppo di limiti**.  

3.  Nella finestra di dialogo **Crea gruppo di limiti** selezionare la scheda **Generale** e specificare un **Nome** per questo gruppo di limiti.  

4.  Fare clic su **OK** per salvare il nuovo gruppo di limiti.  

#### <a name="to-configure-a-boundary-group"></a>Per configurare un gruppo di limiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Selezionare il gruppo di limiti da modificare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Generale** per modificare i limiti appartenenti a questo gruppo di limiti:  

    -   Per aggiungere i limiti, fare clic su **Aggiungi**, selezionare la casella di controllo per uno o più limiti e quindi fare clic su **OK**.  

    -   Per rimuovere i limiti, selezionare il limite e fare clic su **Rimuovi**.  

5.  Selezionare la scheda **Riferimenti** per modificare l'assegnazione sito e la configurazione del server del sistema del sito associata:  

    -   Per consentire ai client di utilizzare questo gruppo di limiti per l'assegnazione sito, selezionare la casella di controllo **Utilizza questo gruppo limite per l'assegnazione sito**e quindi selezionare un sito dalla casella a discesa **Sito assegnato** .  

    -   Per configurare quali server del sistema del sito disponibili sono associati a questo gruppo di limiti:  

    1.  Fare clic su **Aggiungi**e quindi selezionare la casella di controllo per uno o più server. I server vengono aggiunti come server del sistema del sito associati per questo gruppo di limiti. Sono disponibili solo i server su cui è installato il ruolo del sistema del sito supportato.  

        > [!NOTE]  
        >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati vengono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente a questo gruppo di limiti.  

    2.  Per rimuovere un server da questo gruppo di limiti, selezionare il server e quindi fare clic su **Rimuovi**.  

        > [!NOTE]  
        >  Per interrompere l'utilizzo di questo gruppo di limiti per i sistemi del sito in fase di associazione, è necessario rimuovere tutti i server elencati come server del sistema del sito associati.  

    3.  Per modificare la velocità di connessione di rete per un server del sistema del sito per questo gruppo di limiti, selezionare il server e quindi fare clic su **Modifica connessione**.  

         Per impostazione predefinita, la velocità di connessione per ogni sistema del sito è impostata su **Veloce**, ma è possibile modificarla in **Lenta**. La velocità di connessione di rete e la configurazione di una distribuzione determinano se un client può scaricare il contenuto dal server.  

6.  Fare clic su **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Per associare un server di distribuzione del contenuto o un punto di gestione a un gruppo di limiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Selezionare il gruppo di limiti da modificare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Riferimenti** .  

5.  In **Seleziona server del sistema del sito**fare clic su **Aggiungi**, selezionare la casella di controllo per i server del sistema del sito da associare a questo gruppo di limiti, quindi fare clic su **OK**.  

6.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione del gruppo di limiti.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Per abilitare l'uso dei punti di gestione preferiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**, quindi nella scheda **Home** selezionare **Impostazioni gerarchia**.  

2.  Nella scheda **Generale** di Impostazioni gerarchia selezionare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

3.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Per configurare un sito di fallback per l'assegnazione sito automatica  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** >  **Siti**.  

2.  Nella scheda **Home** , del gruppo **Siti** , fare clic su **Impostazioni gerarchia**.  

3.  Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback**e quindi selezionare un sito dall'elenco a discesa **Sito di fallback** .  

4.  Fare clic su **OK** per salvare la configurazione.  

 Le sezioni seguenti forniscono dettagli aggiuntivi sulle configurazioni del gruppo di limiti.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informazioni sull'assegnazione del sito  
 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica del sito verrà aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  

-   Dopo l'assegnazione a un sito, il client non modificherà la propria assegnazione del sito quando cambia il percorso di rete. Se il client ad esempio si sposta in un nuovo percorso di rete rappresentato da un limite in un gruppo di limiti con un'assegnazione sito diversa, il sito assegnato a tale client non verrà modificato.  

-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  

-   Quando un limite è un membro di più gruppi di limiti con diversi siti assegnati, i client selezioneranno uno di questi siti in modo casuale.  

-   Le modifiche a un sito assegnato dei gruppi di limiti si applicano solo alle nuove azioni di assegnazione del sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione del sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione dei siti per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informazioni sul percorso del contenuto  
 È possibile configurare ogni gruppo di limiti con uno o più punti di distribuzione e punti di migrazione stato che possono poi essere associati a più gruppi di limiti.  

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione. Configuration Manager invia al client un elenco dei punti di distribuzione associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

-   **Durante la distribuzione del sistema operativo, i client** richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato. Configuration Manager invia al client un elenco dei punti di migrazione dello stato associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informazioni sui punti di gestione preferiti  
 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usare un punto di gestione dal sito assegnato che non è configurato come preferito.  

-   Per usare questa opzione è necessario abilitarla per la gerarchia e configurare i gruppi di limiti nei singoli siti primari per includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti  

-   Se sono configurati i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio dell'elenco dei punti di gestione assegnati (che include tutti i punti di gestione dal sito assegnato del client)  

> [!NOTE]  
>  Quando un client esegue il roaming (ossia, modifica i percorsi di rete, ad esempio quando un computer portatile viene spostato in un percorso di ufficio remoto), può usare un punto di gestione (o un punto di gestione proxy) dal sito locale nella nuova posizione prima di provare a usare un punto di gestione del sito assegnato (che include i punti di gestione preferiti).  Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informazioni sui limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto:  

-   **Quando un client richiede un contenuto** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno il contenuto.  

-   **Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Informazioni sulla velocità di connessione di rete  
 È possibile impostare la velocità di connessione di rete per ogni server del sistema del sito in un gruppo di limiti. Questa impostazione si applica ai client che si connettono a un sistema del sito basato su questa configurazione dei gruppi di limiti. Lo stesso server del sistema del sito può avere una velocità di connessione impostata nei diversi gruppi di limiti.  

 Per impostazione predefinita, la velocità di connessione di rete è configurata come **Veloce**, ma è possibile configurarla anche come **Lenta**. La velocità di connessione di rete e la configurazione della distribuzione determinano se per un client incluso in un gruppo di limiti associato è possibile scaricare contenuto da un punto di distribuzione.  

 Per altre informazioni sul modo in cui la configurazione della velocità di connessione di rete influisce sulle modalità di recupero del contenuto da parte dei client, vedere [Scenari del percorso di origine del contenuto](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  



<!--HONumber=Dec16_HO3-->


