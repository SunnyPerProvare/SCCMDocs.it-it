---
title: Disponibilità elevata del server del sito
titleSuffix: Configuration Manager
description: Come configurare la disponibilità elevata per il server del sito di Configuration Manager aggiungendo un server del sito in modalità passiva.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be12cfe29ff470f2f577bab2c685695ae5770bae
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131422"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Disponibilità elevata del server del sito in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1128774-->

A partire da Configuration Manager versione 1806, la disponibilità elevata per il ruolo del server del sito è una soluzione di base di Configuration Manager per installare un server del sito aggiuntivo in modalità *passiva*. Il server del sito in modalità passiva è un'aggiunta al server del sito primario esistente in modalità *attiva*. Un server del sito in modalità passiva è disponibile per l'uso immediato, quando necessario. Includere questo server del sito aggiuntivo come parte della progettazione complessiva per rendere il servizio Configuration Manager a [disponibilità elevata](/sccm/core/servers/deploy/configure/high-availability-options).  

Un server del sito in modalità passiva:
- Usa lo stesso database del sito usato dal server del sito in modalità attiva.
- Non scrive dati nel database del sito quando si trova in modalità passiva.
- Usa la stessa raccolta contenuto usata dal server del sito in modalità attiva.

Per far diventare attivo il server del sito in modalità passiva, lo si *alza di livello* manualmente. Questa azione fa passare il server del sito dalla modalità passiva alla modalità attiva. I ruoli del sistema del sito che sono disponibili nel server in modalità Attivo originale rimangono disponibili fin a quando tale computer è accessibile. Solo il ruolo del server del sito viene commutato tra le modalità attiva e passiva.

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).



## <a name="prerequisites"></a>Prerequisiti

- Il server del sito in modalità passiva può essere locale o basato sul cloud in Azure.  
    > [!Note]  
    > Un server del sito basato sul cloud in modalità passiva usa l'infrastruttura distribuita come servizio (IaaS) di Azure. Per altre informazioni, vedere gli articoli seguenti:  
    > - [Macchine virtuali di Azure (per l'infrastruttura basata sul cloud)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Domande frequenti su Configuration Manager in Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Entrambi i server del sito devono appartenere allo stesso dominio di Active Directory.  

- Il sito è un sito primario autonomo. 

- Entrambi i server del sito devono usare lo stesso database del sito, che deve essere remoto per ogni server del sito.  

     - Entrambi i server del sito necessitano di autorizzazioni di **amministratore di sistema** per l'istanza di SQL Server che ospita il database del sito.

     - L'istanza di SQL Server che ospita il database del sito può usare un'istanza predefinita, un'istanza denominata, un [cluster di SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database) o un [gruppo di disponibilità Always On di SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - Il server del sito in modalità passiva è configurato per usare lo stesso database del sito del server del sito in modalità attiva. Il server del sito in modalità passiva legge solo dal database. Non scrive nel database finché non viene alzato di livello alla modalità attiva.  

- La raccolta contenuto del sito deve essere in una condivisione di rete remota. Entrambi i server del sito necessitano di autorizzazioni di controllo completo per la condivisione e i relativi contenuti. Per altre informazioni, vedere [Gestire la raccolta contenuto](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library).<!--1357525-->  

    - Il server del sito non può avere il ruolo di punto di distribuzione. Il punto di distribuzione usa anche la raccolta contenuto e questo ruolo non supporta una raccolta contenuto remota. Dopo aver spostato la raccolta contenuto, non è possibile aggiungere il ruolo di punto di distribuzione al server del sito.  

- Il server del sito in modalità passiva:  

     - Deve soddisfare i [prerequisiti per l'installazione di un sito primario](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Deve avere l'account computer nel gruppo di amministratori locale sul server del sito in modalità attiva.<!--516036-->

     - Esegue l'installazione usando file di origine che corrispondono alla versione del server del sito in modalità attiva.  

     - Non può avere un ruolo del sistema del sito da qualsiasi sito prima di installare il server del sito nel ruolo in modalità passiva.  

- Entrambi i server del sito possono eseguire versioni diverse del sistema operativo o del Service Pack, purché entrambe siano [supportate da Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## <a name="limitations"></a>Limitazioni
- Ciascun sito primario supporta un singolo server del sito in modalità Passivo.  

- Un server del sito in modalità passiva non è supportato in una gerarchia. Una gerarchia include un sito di amministrazione centrale e un sito primario figlio. Creare un server del sito in modalità passiva solo in un sito primario autonomo.<!--1358224-->

- Un server del sito in modalità passiva non è supportato in un sito secondario.<!--SCCMDocs issue 680-->  

- L'innalzamento di livello del server del sito in modalità passiva alla modalità attiva è manuale. Non si verificano failover automatici.  

- Non si possono installare ruoli del sistema del sito nel nuovo server prima di aggiungere il server del sito in modalità passiva.  

    > [!Note]  
    > Dopo l'installazione del server del sito in modalità passiva, è possibile aggiungere altri ruoli in base alle esigenze, ad esempio il provider SMS o un punto di gestione in un sito primario.  

- Per ruoli come il punto di reporting, che usano un database, ospitare il database in un server remoto rispetto a entrambi i server del sito.  

- Il provider SMS non viene installato nel server del sito in modalità passiva. Connettersi a un provider per consentire al sito di alzare manualmente di livello il server del sito in modalità passiva alla modalità attiva. Installare almeno un'istanza aggiuntiva del provider in un altro server. Per altre informazioni, vedere [Piano per il provider SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- La console di Configuration Manager non viene installata automaticamente nel server del sito in modalità passiva.  



## <a name="add-a-site-server-in-passive-mode"></a>Aggiungere un server del sito in modalità Passivo

Per altre informazioni sul processo generale di aggiunta dei ruoli, vedere [Installare i ruoli del sistema del sito](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito**, selezionare il nodo **Siti** e fare clic su **Crea server di sistema sito** nella barra multifunzione.   

2. Nella pagina **Generale** della Creazione guidata server del sistema sito specificare il server per ospitare il server del sito in modalità passiva. Il server specificato non può ospitare ruoli del sistema del sito prima di installare un server del sito in modalità passiva.  

3. Nella pagina **Selezione ruolo del sistema** selezionare solo **Server del sito in modalità passiva**.  

    > [!Note]  
    > La procedura guidata esegue i controlli dei prerequisiti iniziali seguenti in questa pagina:  
    > - Il server selezionato non è un server del sito secondario
    > - Il server selezionato non è già un server del sito in modalità passiva
    > - La raccolta contenuto del sito è in una posizione remota  
    >  
    > Se questi controlli dei prerequisiti iniziali hanno esito negativo, non è possibile proseguire oltre questa pagina della procedura guidata.  

4. Nella pagina **Server del sito in modalità passiva** fornire le informazioni seguenti che vengono usate per eseguire la configurazione e installare il ruolo del server del sito nel server specificato:

     - Scegliere una delle seguenti opzioni:  

         - **Copia i file di origine dell'installazione in rete dal server del sito in modalità attiva**: questa opzione crea un pacchetto compresso e lo invia al nuovo server del sito.  

         - **Usa i file di origine nel percorso seguente nel server del sito in modalità passiva**: ad esempio, un percorso locale in cui sono già stati copiati i file di origine. Assicurarsi che questo contenuto sia della stessa versione del server del sito in modalità attiva.  

         - (*Opzione consigliata*) **Utilizza i file di origine nel seguente percorso di rete**: specificare il percorso diretto al contenuto della cartella **CD.Latest** dal server del sito in modalità attiva. Ad esempio, `\\Server\SMS_ABC\CD.Latest`, dove "*Server*" è il nome del server del sito in modalità attiva e "*ABC*" è il codice del sito.  

     - Specificare il percorso locale in cui installare Configuration Manager nel nuovo server del sito. Ad esempio: `C:\Program Files\Configuration Manager`  

5. Completare la procedura guidata. Configuration Manager installa quindi il server del sito in modalità Passivo nel server specificato.

Per lo stato dettagliato dell'installazione, nella console andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. Lo stato del server del sito in modalità passiva viene visualizzato come **Installazione**. Per altre informazioni dettagliate, selezionare il server e fare clic su **Mostra stato**. Questa azione apre la finestra Stato dell'installazione del server del sito. Al termine del processo, lo stato viene visualizzato come **OK** per entrambi i server.   

Per altre informazioni sul processo di configurazione, vedere [Diagramma di flusso - Configurare un server del sito in modalità passiva](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

Dopo aver aggiunto un server del sito in modalità passiva, visualizzare entrambi i server del sito nella scheda **Nodi** nel nodo **Siti** della console. 

Tutti i componenti del server del sito di Configuration Manager sono in standby nel server del sito in modalità passiva. I servizi Windows sono ancora in esecuzione.



## <a name="site-server-promotion"></a>Innalzamento di livello dei server del sito  

Come per il backup e ripristino, pianificare e provare il processo per modificare i server del sito. Prendere in considerazione i punti seguenti nel piano di innalzamento di livello:  

- Provare un innalzamento di livello pianificato, in cui entrambi i server del sito sono online. Provare anche un failover non pianificato, disconnettendo o arrestando in modo forzato il server del sito in modalità attiva.  

- Determinare i processi operativi durante il failover e che cosa comunicare agli altri amministratori di Configuration Manager.  

- Prima di un innalzamento di livello pianificato:  

    - Controllare lo stato generale del sito e i componenti del sito. Assicurarsi che tutto sia integro come di consueto per l'ambiente.  

    - Controllare lo stato del contenuto per i pacchetti che eseguono la replica attiva tra siti.  

    - Non avviare nuovi processi distribuzione del contenuto. 

        > [!Note]  
        > Se la replica di file tra siti è in corso durante il failover, il nuovo server del sito potrebbe non ricevere il file replicato. In questo caso, ridistribuire il contenuto software una volta che il nuovo server del sito è attivo.<!--515436-->  


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processo per alzare di livello il server del sito in modalità passiva alla modalità attiva

Questa sezione descrive come far passare il server del sito in modalità passiva alla modalità attiva. Per accedere al sito e apportare questa modifica, è necessario poter accedere a un'istanza del provider SMS. Per altre informazioni, vedere [Usare più provider SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Important]  
> Per impostazione predefinita, solo il server del sito originale ha il ruolo Provider SMS. Se questo server è offline, non è possibile connettersi al sito perché non è disponibile alcun provider. Quando si aggiunge il server del sito in modalità passiva, il provider SMS non viene aggiunto automaticamente. Aggiungere almeno un altro ruolo Provider SMS al sito per un servizio a disponibilità elevata.  

> [!Tip]  
> La console di Configuration Manager richiede l'elenco dei provider SMS disponibili da WMI sul server del sito. Quando si installano più provider SMS in un sito, il sito assegna in modo casuale ogni nuova richiesta di connessione per usare un provider SMS installato. Non è possibile specificare la posizione del provider SMS da usare con una sessione di connessione specifica. Se la console non riesce a connettersi al sito perché il server del sito corrente è offline, specificare l'altro server del sito nella finestra Connessione al sito.  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Selezionare il sito e quindi passare alla scheda **Nodi**. Selezionare il server del sito in modalità passiva e quindi fare clic su **Alza di livello su attivo** nella barra multifunzione. Fare clic su **Sì** per confermare e continuare.   
  
2. Aggiornare il nodo della console. La colonna **Stato** per il server che si sta alzando di livello viene visualizzata nella scheda **Nodi** come **Innalzamento di livello**.  

3. Al termine dell'innalzamento di livello, nella colonna **Stato** viene visualizzato **OK** sia per il nuovo server del sito in modalità attiva che per il nuovo server del sito in modalità passiva. La colonna **Nome server** per il sito ora indica il nome del nuovo server del sito in modalità attiva.

Per lo stato dettagliato, andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. La colonna **Modalità** identifica quale server è *Attivo* o *Passivo*. Quando si alza di livello un server dalla modalità passiva alla modalità attiva, selezionare il server del sito che si sta alzando di livello alla modalità attiva e quindi scegliere **Mostra stato** dalla barra multifunzione. Questa azione apre la finestra Site Server Promotion Status (Stato innalzamento di livello server del sito) che mostra altri dettagli relativi al processo.

Quando un server del sito in modalità Attivo passa alla modalità Passivo, solo il ruolo del sistema del sito è reso passivo. Tutti gli altri ruoli del sistema del sito che vengono installati su quel computer restano attivi e accessibili ai client.

Per altre informazioni sul processo di innalzamento di livello *pianificato*, vedere [Diagramma di flusso - Alzare di livello il server del sito (con pianificazione)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### <a name="unplanned-failover"></a>Failover non pianificato

Se il server del sito corrente in modalità attiva è offline, il server del sito per l'innalzamento di livello prova a contattare il server del sito corrente in modalità attiva per 30 minuti. Se il server offline torna disponibile entro questo intervallo di tempo, viene inviata una notifica e la modifica procede normalmente. In caso contrario, il server del sito per l'innalzamento di livello aggiorna in modo forzato la configurazione del sito per renderla attiva. Se il server offline torna disponibile dopo questo intervallo di tempo, verifica prima di tutto lo stato corrente nel database del sito, quindi si abbassa di livello al server del sito in modalità passiva.

Durante questi 30 minuti di attesa, il sito non ha server del sito in modalità attiva. I client comunicano ugualmente con i ruoli destinati ai client, ad esempio i punti di gestione, i punti di aggiornamento software e i punti di distribuzione. Gli utenti possono installare il software che è già stato distribuito. L'amministrazione del sito non è consentita in questo periodo di tempo. Per altre informazioni, vedere [Impatto degli errori del sito](/sccm/core/servers/manage/site-failure-impacts).  

Se il server offline è danneggiato e non può tornare disponibile, eliminare questo server del sito dalla console, quindi creare un nuovo server del sito in modalità passiva per ripristinare un servizio a disponibilità elevata. 

Per altre informazioni sul processo di failover *non pianificato*, vedere [Diagramma di flusso - Alzare di livello il server del sito (senza pianificazione)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### <a name="additional-tasks-after-site-server-promotion"></a>Attività aggiuntive dopo l'innalzamento di livello server del sito  

Dopo aver commutato i server del sito, non c'è bisogno di eseguire la maggior parte delle altre attività necessarie quando [si ripristina un sito](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). Non è ad esempio necessario reimpostare le password o riconnettersi alla sottoscrizione di Microsoft Intune.

La procedura seguente potrebbe essere necessaria per l'ambiente specifico:  

- Se si importano i certificati PKI per i punti di distribuzione, reimportare il certificato per i server interessati. Per altre informazioni, vedere [Rigenerare i certificati per i punti di distribuzione](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- Se si integra Confguration Manager con Microsoft Store per le aziende, riconfigurare tale connessione. Per altre informazioni, vedere [Gestire le app da Microsoft Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).  



## <a name="daily-monitoring"></a>Monitoraggio giornaliero

Quando si ha un server del sito in modalità passiva, monitorarlo giornalmente. Assicurarsi che lo stato rimanga OK e che sia pronto per l'uso. Nella console di Configuration Manager andare all'area di lavoro **Monitoraggio** e selezionare il nodo **Stato del server del sito**. Visualizzare entrambi i server del sito e lo stato corrente. Visualizzare lo stato anche nell'area di lavoro **Amministrazione**. Espandere **Configurazione del sito** e selezionare il nodo **Siti**. Selezionare il sito e quindi passare alla scheda **Nodi**. 
