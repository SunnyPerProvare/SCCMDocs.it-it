---
title: "Funzionalità della versione Technical Preview 1704 per Configuration Manager"
description: "Informazioni sulle funzionalità disponibili nella versione Technical Preview 1704 per System Center Configuration Manager."
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: d7caee47ca74064630e09c1bdb94187af256d4b4
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Funzionalità della versione Technical Preview 1704 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo presenta le funzionalità disponibili nella versione Technical Preview 1704 per System Center Configuration Manager. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.    


**Di seguito sono riportate le nuove funzionalità disponibili con questa versione.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurare le app Android con i criteri di configurazione delle app
È possibile usare i criteri di configurazione delle app in System Center Configuration Manager (Configuration Manager) per distribuire impostazioni che potrebbero essere necessarie quando un utente esegue un'app in un dispositivo Android for Work. I criteri di configurazione delle app per Android sono disponibili solo nei dispositivi che eseguono Android for Work e riguardano le applicazioni approvate per lo store Play for Work.

### <a name="try-it-out"></a>Procedura                 

Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Criteri di configurazione dell'app**, quindi scegliere **Create App Configuration Policy** (Crea criteri di configurazione dell'app). Nella pagina **Generale** della procedura guidata scegliere **Select a configuration policy type** (Selezionare un tipo di criteri di configurazione). Specificare la piattaforma di destinazione per i criteri di configurazione dell'app: **Configuration policy for Android for Work apps** (Criteri di configurazione per app Android for Work). Quindi è possibile scegliere **Specify name and value pairs** (Specifica coppie di nome e valore) o **Browse to a property list JSON file** (Esplora file elenco proprietà JSON). I nuovi criteri di configurazione app vengono visualizzati nel nodo **Criteri di configurazione dell'app** dell'area di lavoro **Raccolta software**. Per associare criteri di configurazione delle app alla distribuzione di un'app per Android for Work, distribuire l'applicazione nel modo consueto con la procedura descritta nell'argomento [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications).

## <a name="hardware-inventory-collects-secure-boot-information"></a>L'inventario hardware raccoglie le informazioni di Avvio protetto
L'inventario hardware ora raccoglie informazioni sull'attivazione di Avvio protetto nei client. Queste informazioni sono archiviate nella classe **SMS_Firmware** (introdotta nella versione 1702) e abilitate nell'inventario hardware per impostazione predefinita. Per altre informazioni sull'inventario hardware, vedere [Come configurare l'inventario hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Aggiungere sequenze di attività figlio a una sequenza di attività
In questa versione è possibile aggiungere un nuovo passaggio della sequenza di attività che esegue un'altra sequenza di attività, la quale crea una relazione padre/figlio tra le sequenze di attività. In questo modo è possibile creare più sequenze di attività modulari riusabili.  

Quando si aggiunge una sequenza di attività figlio a una sequenza di attività, tenere presente quanto segue:

- Le sequenze di attività padre e figlio sono di fatto combinate in un unico criterio eseguito dal client.
- Non è supportata l'aggiunta di una sequenza di attività figlio che è la sequenza padre di un'altra sequenza di attività.
- L'ambiente è globale. Ad esempio, se una variabile viene impostata dalla sequenza di attività padre e quindi modificata dalla sequenza di attività figlio, la variabile resta modificata nelle fasi successive. Analogamente, se la sequenza di attività figlio crea una nuova variabile, la variabile è disponibile per i passaggi rimanenti della sequenza di attività padre.
- I messaggi di stato vengono inviati con la procedura normale per un'operazione sequenza di attività singola.
- Le sequenze di attività scrivono voci nel file smsts.log. Le nuove voci di registro evidenziano l'avvio di una sequenza di attività figlio.
- Nella versione Technical Preview 1704 per Configuration Manager, se la sequenza di attività figlio fa riferimento a qualsiasi pacchetto e si esegue la sequenza di attività padre da Software Center, quando viene eseguita la sequenza di attività figlio il client non trova il contenuto del pacchetto. In questo scenario, è necessario eseguire la sequenza di attività da un supporto (supporto di avvio, PXE e così via).  

    Se la sequenza di attività figlio usa passaggi quali **Esegui riga di comando** (senza riferimenti a pacchetti), **Format**, **BitLocker** e così via, la sequenza di attività viene eseguita correttamente da Software Center.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Per aggiungere una sequenza di attività figlio a una sequenza di attività
1. Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale**, quindi fare clic su **Run Task Sequence** (Esegui sequenza di attività).
2. Fare clic su **Sfoglia** per selezionare la sequenza di attività figlio.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Ricaricare immagini di avvio con la versione corrente di Windows PE
Quando si esegue **Aggiorna punti di distribuzione** su un'immagine d'avvio selezionata, ora è possibile scegliere di ricaricare nell'immagine d'avvio la versione più recente di Windows PE (dalla directory di installazione di Windows ADK). La pagina **Generale** della procedura guidata offre informazioni sulla versione di Windows ADK installata nel server del sito, sulla versione di Windows ADK dalla quale è stato usato Windows PE nell'immagine d'avvio e sulla versione del client di Configuration Manager. È possibile usare queste informazioni per decidere se ricaricare l'immagine d'avvio. Inoltre la nuova colonna **Versione client** aggiunta alla visualizzazione delle immagini d'avvio nel nodo **Immagini d'avvio** visualizza la versione del client di Configuration Manager usata da ogni immagine d'avvio.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Per ricaricare un'immagine d'avvio con la versione corrente di Windows PE

1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Immagini d'avvio**.
2. Selezionare un'immagine d'avvio e fare clic su **Aggiorna punti di distribuzione**.
3. Nella scheda **Generale** della procedura guidata, selezionare **Reload boot image using the current version of Windows PE from the installed Windows ADK** (Ricarica immagine d'avvio con la versione corrente di Windows PE da Windows ADK installato).

## <a name="improvements-to-operating-system-deployment"></a>Miglioramenti alla distribuzione del sistema operativo
Sono stati apportati i miglioramenti seguenti alla distribuzione del sistema operativo, molti dei quali sono il risultato del feedback degli utenti.

- [Nuova colonna **Versione SO** per le immagini del sistema operativo](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): la nuova colonna **Versione SO** è stata aggiunta per visualizzare la versione del sistema operativo dell'immagine quando si visualizzano informazioni nei nodi **Immagini del sistema operativo** e **Pacchetti di aggiornamento del sistema operativo**. Viene visualizzata solo la versione del primo indice del file .WIM. Per verificare le versioni del sistema operativo corrispondenti agli altri indici, aprire la scheda **Dettagli** dell'immagine.

- [Registrazione più efficiente in Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): a partire dalla versione corrente, nel file smsts.log non verranno più scritte voci per le informazioni CCM_CIVersionInfo.PolicyID. Prima di questa versione venivano spesso registrate molte voci con queste informazioni, che rendevano difficile la ricerca di informazioni più importanti nel file di registro.
