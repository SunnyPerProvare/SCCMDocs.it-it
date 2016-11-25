---
title: "Funzionalità di Technical Preview 1610 per System Center Configuration Manager"
description: "Informazioni sulle funzionalità disponibili in Technical Preview per System Center Configuration Manager, versione 1610."
ms.custom: na
ms.date: 10/21/2016
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: article
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
caps.latest.revision: 2
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c9fe6961a63495d08a3e58e3ddf46c5d316e2613
ms.openlocfilehash: 865b5078282bf240aa6a2aef5cb2662f2471fb71

---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Funzionalità di Technical Preview 1610 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*



Questo articolo presenta le funzionalità disponibili in Technical Preview per System Center Configuration Manager, versione 1610. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager.      Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica
È ora possibile filtrare le dimensioni del contenuto per gli aggiornamenti software nelle regole di distribuzione automatica. Ad esempio, è possibile impostare il filtro **Dimensioni contenuto (KB)** su **< 2048** per scaricare solo gli aggiornamenti software inferiori a 2 MB. Questo filtro impedisce che vengano scaricati in automatico gli aggiornamenti software di grandi dimensioni al fine di migliorare il supporto della manutenzione Windows semplificata di livello inferiore quando la larghezza di banda è limitata. Per informazioni dettagliate, vedere [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/) (Configuration Manager e manutenzione Windows semplificata su sistemi operativi di livello inferiore).

#### <a name="to-configure-the-content-size-field"></a>Per configurare il campo Dimensioni contenuto
Per configurare il campo **Dimensioni contenuto (KB)**, accedere alla pagina **Aggiornamenti software** nella Creazione guidata delle regole di distribuzione automatica quando si crea un'ADR o accedere alla scheda **Aggiornamenti software** nelle proprietà di un'ADR esistente.

![Campo Dimensione contenuto](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Funzionalità migliorate per le finestre di dialogo del software richieste
Quando si riceve il software necessario, dall'impostazione **Posponi e ricorda tra:** è possibile selezionare un'opzione dall'elenco di valori a discesa seguente:
- In seguito: specifica che le notifiche vengono programmate in base alle impostazioni di notifica configurate nelle impostazioni dell'agente client.
- Orario fisso: specifica che la notifica verrà pianificata per una nuova visualizzazione dopo l'ora selezionata. Ad esempio, se un utente seleziona 30 minuti, la notifica verrà visualizzata nuovamente dopo 30 minuti.

![Pagina dell'agente computer nelle impostazioni dell'agente client](media/computeragentsettings.png)

Il tempo di posticipo massimo è sempre basato sui valori di notifica configurati nelle impostazioni dell'agente client su ogni orario presente lungo la cronologia di distribuzione. Ad esempio, se l'impostazione nella pagina dell'agente computer **Più di 24 ore alla scadenza di distribuzione. Avvisare l'utente ogni (ore)** è configurata per 10 ore e alla scadenza mancano più di 24 ore, all'avvio della finestra di dialogo l'utente visualizzerà un set di opzioni di posticipo mai superiori a 10 ore. Man mano che si avvicina la scadenza, la finestra di dialogo mostra un numero minore di opzioni coerente con le impostazioni dell'agente client pertinente per ogni componente della cronologia di distribuzione.

Per una distribuzione ad alto rischio, ad esempio una sequenza di attività che distribuisce un sistema operativo, l'esperienza di notifica dell'utente finale è ora più invasiva. Ogni volta che l'utente viene informato della necessità di manutenzione critica del software, invece di una notifica temporanea sulla barra delle applicazioni, nel computer dell'utente viene visualizzata una finestra di dialogo simile alla seguente:

![Finestra di dialogo del software richiesto](media/requiredsoftwaredialog.png)


Per ulteriori informazioni:
- [Impostazioni per gestire le distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Come configurare le impostazioni client](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Negare richieste di applicazioni approvate in precedenza

In qualità di amministratore l'utente è ora in grado di negare una richiesta di applicazioni approvate in precedenza. Per installare un'applicazione negata, gli utenti successivi dovranno inviare una nuova richiesta. La negazione non disinstalla l'applicazione, ma impone che qualsiasi nuova richiesta dell'utente per l'applicazione specifica venga riapprovata. In precedenza era possibile negare soltanto richieste di applicazioni non approvate.

#### <a name="try-it-out"></a>Procedura
Per negare la richiesta di un'applicazione approvata:

1.  Nella console di Configuration Manager [creare e distribuire un'applicazione](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/create-applications) che richiede l'approvazione.
2.  In un computer client aprire Software Center e inviare una richiesta per l'applicazione.
3.  Nella console di Configuration Manager approvare la richiesta per l'applicazione.
4.  Negare la richiesta di un'applicazione approvata: nella console di Configuration Manager passare a**Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Richieste di approvazione** e selezionare la richiesta di applicazione che si desidera negare.  Nella barra multifunzione fare clic su **Nega**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Impedire l'aggiornamento automatico dei client
Tecnichal Preview 1610 presenta una nuova impostazione che consente di impedire che una raccolta di client installi automaticamente le versioni client aggiornate.  Questa funzione si applica sia all'aggiornamento automatico sia ad altri metodi, ad esempio all'aggiornamento basato sull'aggiornamento software, agli script di accesso e ai criteri di gruppo. Questa opzione può essere utile per una raccolta di computer che richiede particolare attenzione durante l'aggiornamento del client. I client che appartengono a una raccolta esclusa ignorano le richieste di aggiornamento del software client.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurare l'esclusione dall'aggiornamento automatico
Per configurare le esclusioni dall'aggiornamento automatico:
1.  Nella console di Configuration Manager aprire **Impostazioni gerarchia** in **Amministrazione > Configurazione del sito > Siti** e quindi selezionare la scheda **Aggiornamento client**.
2.  Selezionare la casella di controllo **Exclude specified clients from upgrade** (Escludi dall'aggiornamento i client specificati) e **Exclusion collection** (Raccolta di esclusione), quindi selezionare la raccolta da escludere. È possibile selezionare per l'esclusione solo una singola raccolta.
3.  Fare clic su **OK** per chiudere e salvare la configurazione. Dopo che i client avranno aggiornato i criteri, i client appartenenti alla raccolta esclusa non installeranno più automaticamente gli aggiornamenti per il software client.

  ![Impostazioni per l'esclusione dall'aggiornamento automatico](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Anche se l'interfaccia utente indica che i client non verranno aggiornati, esistono due metodi che è possibile usare per sostituire queste impostazioni. L'installazione push del client e l'installazione manuale del client consentono di sostituire questa configurazione. Per altre informazioni, vedere la sezione seguente.


### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Come aggiornare un client in una raccolta esclusa
Se una raccolta è configurata per l'esclusione, i membri di tale raccolta possono aggiornare il software client solo tramite uno dei due metodi che sostituiscono l'esclusione:
 - **Installazione push client**: è possibile usare l'installazione push del client per eseguire l'aggiornamento di un client che appartiene a una raccolta esclusa. Questa operazione è consentita in quanto richiesta dall'amministratore e permette di aggiornare i client lasciando invariata l'esclusione dell'intera raccolta.       
 - **Installazione client manuale**: è possibile aggiornare manualmente i client che appartengono a una raccolta esclusa usando la seguente opzione della riga di comando con ccmsetup: ***/ignoreskipupgrade***.

  Se si tenta di aggiornare manualmente un client che fa parte della raccolta esclusa senza usare questa opzione, il client non installa il nuovo software client. Per altre informazioni, vedere [Come installare manualmente i client di Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

Per altre informazioni su questi metodi di installazione del client, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).


## <a name="see-also"></a>Vedere anche
[Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->


