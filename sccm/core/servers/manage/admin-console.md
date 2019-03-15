---
title: Console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sull'esplorazione tramite la console di Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f9c06f40af1134055d4038fd23954b3f4c59682
ms.sourcegitcommit: 544f335cfd1bfd0a1d4973439780e9f5e9ee8bed
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562109"
---
# <a name="using-the-configuration-manager-console"></a>Uso della console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli amministratori usano la console di Configuration Manager per gestire l'ambiente di Configuration Manager. Questo articolo illustra le nozioni di base dell'esplorazione della console.  



## <a name="connect-to-a-site-server"></a>Connettersi a un server del sito

La console si connette al server di sito di amministrazione centrale o ai server del sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario. È possibile [installare la console di Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Durante l'installazione, è stato specificato il nome di dominio completo (FQDN) del server del sito a cui si connette la console. 

Per connettersi a un server del sito diverso, eseguire questa procedura: 

1. Selezionare la freccia nella parte superiore della [barra multifunzione](#ribbon) e scegliere **Connetti a un nuovo sito**.  

    ![Connettere la console a un nuovo sito](media/connect-to-a-new-site.png)  

2. Digitare il nome di dominio completo del server del sito. Se precedentemente ci si è connessi al server del sito, selezionare il server dall'elenco a discesa.  

    ![Nella finestra Connessione al sito immettere il nome di dominio completo del server del sito](media/site-server-fqdn.png)  

3. Selezionare **Connetti**.  


A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Per altre informazioni, vedere [Piano per il provider SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="navigation"></a>Navigazione

Alcune aree della console potrebbero non essere visibili a seconda del ruolo di sicurezza assegnato. Per altre informazioni sui ruoli, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration). 


### <a name="workspaces"></a>Aree di lavoro

La console di Configuration Manager ha quattro **aree di lavoro**:  

- **Asset e conformità**  

- **Raccolta software**  

- **Monitoraggio**  

- **Amministrazione**  

![Aree di lavoro di Configuration Manager con menu di scelta rapida](media/configuration-manager-workspaces.png)  

Riordinare i pulsanti delle aree di lavoro selezionando la freccia giù e scegliendo **Opzioni riquadro di spostamento**. Selezionare un elemento e fare clic su **Sposta su** o **Sposta giù**. Selezionare **Reimposta** per ripristinare l'ordine predefinito dei pulsanti.  

 ![Finestra Opzioni riquadro di spostamento per riordinare le aree di lavoro](media/navigation-pane-options.png)  

Ridurre a icona il pulsante di un'area di lavoro selezionando **Mostra meno pulsanti**. Prima viene ridotta a icona l'ultima area di lavoro dell'elenco. Selezionare un pulsante ridotto a icona e scegliere **Mostra più pulsanti** per ripristinare le dimensioni originali del pulsante.   

![Aree di lavoro ridotte a icona nella console di Configuration Manager](media/workspace-buttons.png)  


### <a name="nodes"></a>Nodi

Le aree di lavoro sono una raccolta di **nodi**. Un esempio di nodo è il nodo **Gruppi di aggiornamenti software** nell'area di lavoro **Raccolta software**. 

All'interno del nodo, è possibile selezionare la freccia per ridurre il riquadro di spostamento.  

![Nodo di esempio e freccia di riduzione evidenziata](media/software-update-groups-node.png)  

Usare la **barra di spostamento** per muoversi nella console quando si riduce a icona il riquadro di spostamento.  

![Riquadro di spostamento ridotto a icona di Configuration Manager](media/minimized-navigation-pane.png)  

Nella console i nodi in alcuni casi sono organizzati in cartelle. Facendo clic sulla cartella, si accede in genere a un **indice di spostamento** o a un **dashboard**.  

![Indice di spostamento degli aggiornamenti software per Configuration Manager](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>Barra multifunzione 

La barra multifunzione è nella parte superiore della console di Configuration Manager. La barra multifunzione può avere più di una scheda e può essere ridotta a icona con la freccia sulla destra. I pulsanti sulla barra multifunzione sono diversi a seconda del nodo. La maggior parte dei pulsanti della barra multifunzione è disponibile anche nei menu di scelta rapida.  

![Barra multifunzione di esempio, evidenziazione di più schede e freccia di riduzione](media/ribbon.png)   


### <a name="details-pane"></a>Riquadro dettagli

È possibile ottenere informazioni aggiuntive sugli elementi esaminando il riquadro dei dettagli. Il riquadro dei dettagli può avere una o più schede. Le schede variano a seconda del nodo.  

![Riquadro dei dettagli di esempio di Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Colonne 

È possibile aggiungere, rimuovere, riordinare e ridimensionare le colonne. Queste azioni consentono di visualizzare i dati che si preferisce. Le colonne disponibili variano a seconda del nodo. Per aggiungere o rimuovere una colonna dalla visualizzazione, fare clic con il pulsante destro del mouse sull'intestazione di una colonna esistente e selezionare un elemento. Riordinare le colonne trascinando l'intestazione di colonna nella posizione desiderata.  

![Aggiungere colonne in Configuration Manager](media/add-columns.png)  

Nella parte inferiore del menu di scelta rapida della colonna è possibile ordinare o raggruppare in base a una colonna. È anche possibile ordinare in base a una colonna selezionandone l'intestazione.  

![Raggruppare per colonna in Configuration Manager](media/column-group-by.png)  



## <a name="command-line-options"></a>Opzioni della riga di comando

La console di Configuration Manager include le seguenti opzioni della riga di comando:

|Opzione|Descrizione|  
|------------|-----------------|  
|`/sms:debugview=1`|Una DebugView viene inserita in tutte le ResultViews che specificano una visualizzazione. DebugView mostra le proprietà non elaborate (nomi e valori).|  
|`/sms:NamespaceView=1`|Mostra la visualizzazione dello spazio dei nomi nella console.|  
|`/sms:ResetSettings`|La console ignora la connessione permanente dell'utente e gli stati della visualizzazione. Le dimensioni della finestra non vengono reimpostate.|  
|`/sms:IgnoreExtensions`|Disabilita tutte le estensioni di Configuration Manager.|  
|`/sms:NoRestore`|La console ignora lo spostamento del nodo permanente precedente.|  



## <a name="tips"></a>Suggerimenti

### <a name="send-feedback"></a>Inviare un feedback
<!--1357542-->

A partire dalla versione 1806, inviare un feedback sul prodotto dalla console.  

- **Invia smile**: inviare commenti e suggerimenti su ciò che si è apprezzato  

- **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non si è apprezzato  

- **Invia un suggerimento**: consente di accedere a UserVoice per condividere la propria opinione  
 
Per altre informazioni, vedere [Commenti e suggerimenti sul prodotto](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Area di lavoro Asset e conformità

#### <a name="view-users-for-a-device"></a>Visualizzare gli utenti per un dispositivo
A partire dalla versione 1806, le colonne seguenti sono disponibili nel nodo **Dispositivi**:  

- **Utente/i primario/i** <!--1357280-->  

- **Utente attualmente connesso** <!--1358202-->  
    > [!NOTE]  
    > La visualizzazione dell'utente attualmente connesso richiede l'[individuazione dell'utente](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) e l'[affinità utente-dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Per altre informazioni su come visualizzare una colonna non predefinita, vedere [Colonne](#columns).

#### <a name="improvement-to-device-search-performance"></a>Miglioramento delle prestazioni di ricerca dei dispositivi
<!-- 3614690 --> A partire dalla versione 1806, quando si esegue la ricerca in una raccolta di dispositivi, non viene eseguita la ricerca della parola chiave in tutte le proprietà degli oggetti. Quando non si specifica cosa cercare, la ricerca viene eseguita nelle quattro proprietà seguenti:
- Name
- Utente/i primario/i
- Utente attualmente connesso
- Nome utente ultimo accesso

Questo comportamento migliora significativamente il tempo necessario per le ricerche in base al nome, in particolare in un ambiente di grandi dimensioni. Le ricerche personalizzate in base a criteri specifici non sono interessate da questa modifica. 


### <a name="monitoring-workspace"></a>Area di lavoro di monitoraggio

#### <a name="copy-details-in-monitoring-views"></a>Copiare i dettagli nelle viste monitoraggio
<!--1357856--> A partire dalla versione 1806, copiare le informazioni dal riquadro **Dettagli asset** per i nodi di monitoraggio seguenti:  

- **Stato distribuzione contenuto**  

- **Stato distribuzione**  

![Vista Stato distribuzione, copiare i dettagli degli asset](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Passaggi successivi

[Funzionalità di accesso facilitato](/sccm/core/understand/accessibility-features)

