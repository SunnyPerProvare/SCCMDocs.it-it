---
title: Console di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sull'esplorazione tramite la console di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f936cf1c1317940f28691863eafdb4aa883fc1cb
ms.sourcegitcommit: aa91f0d376de03b614b70d5fc513cb384ff58db4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2018
ms.locfileid: "50216915"
---
# <a name="using-the-system-center-configuration-manager-console"></a>Uso della console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli amministratori usano la console di System Center Configuration Manager per gestire l'ambiente di Configuration Manager. Questo articolo illustra le nozioni di base dell'esplorazione della console. I miglioramenti apportati alla console sono elencati per versione alla fine di questo articolo. 

## <a name="connect-the-console-to-a-site-server"></a>Connettere la console a un server del sito
La console si connette al server di sito di amministrazione centrale o ai server del sito primario. Non è tuttavia possibile connettere una console di Configuration Manager a un sito secondario. Se necessario, [installare la console di Configuration Manager](../deploy/install/install-consoles.md). Durante l'installazione, è stato specificato il nome di dominio completo (FQDN) del server del sito al quale si connette la console di Configuration Manager. Per connettersi a un server del sito diverso, usare le istruzioni seguenti: 

1. Fare clic sulla freccia nella parte superiore della barra multifunzione e selezionare **Connetti a un nuovo sito**.
    ![Connettere la console a un nuovo sito](media/connect-to-a-new-site.png)
2. Digitare il nome di dominio completo del server del sito. Se precedentemente ci si è connessi al server del sito, selezionare il server dall'elenco a discesa.  
    ![Digitare il nome di dominio completo del server del sito](media/site-server-fqdn.png)
3. Fare clic su **Connetti**. 

## <a name="navigate-the-console"></a>Esplorare la console
Alcune opzioni della console potrebbero non essere visibili a seconda del ruolo di sicurezza assegnato. Per altre informazioni sui ruoli, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](../../understand/fundamentals-of-role-based-administration.md). 

### <a name="workspaces"></a>Aree di lavoro
La console di Configuration Manager ha quattro **aree di lavoro**: 
   - **Asset e conformità**
   - **Raccolta software**
   - **Monitoraggio**
   - **Amministrazione**

 ![Aree di lavoro di Configuration Manager](media/configuration-manager-workspaces.png)

Riordinare i pulsanti delle aree di lavoro facendo clic sulla freccia verso il basso e selezionando **Opzioni Riquadro di spostamento**. Selezionare un elemento e fare clic su **Sposta su** o **Sposta giù**. Fare clic su **Reimposta** per ripristinare l'ordine predefinito dei pulsanti. 

 ![Riordinare le aree di lavoro di Configuration Manager](media/navigation-pane-options.png)

È possibile ridurre a icona il pulsante di un'area di lavoro selezionando **Mostra meno pulsanti**. Prima viene ridotta a icona l'ultima area di lavoro dell'elenco. Per ripristinare le dimensioni originali di un pulsante ridotto a icona, fare clic sul pulsante e selezionare **Mostra più pulsanti**.  

![Aree di lavoro di Configuration Manager](media/workspace-buttons.png)


### <a name="nodes"></a>Nodi
Le aree di lavoro sono una raccolta di **nodi**. Un esempio di nodo è il nodo **Gruppi di aggiornamenti software**. Quando si è in un nodo, è possibile fare clic sulla freccia per ridurre a icona il riquadro di spostamento. 

![Aree di lavoro di Configuration Manager](media/software-update-groups-node.png)

È possibile usare la **barra di spostamento** per muoversi nella console quando il riquadro di spostamento è ridotto a icona. 

![Riquadro di spostamento ridotto a icona di Configuration Manager](media/minimized-navigation-pane.png)

Nella console i nodi in alcuni casi sono organizzati in cartelle. Facendo clic sulla cartella, si accede in genere a un **indice di spostamento** o a un **dashboard**.

![Indice di spostamento degli aggiornamenti software per Configuration Manager](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>Barra multifunzione 
La barra multifunzione è nella parte superiore della console di Configuration Manager. La barra multifunzione può avere più di una scheda e può essere ridotta a icona con la freccia sulla destra. I pulsanti sulla barra multifunzione sono diversi a seconda del nodo. La maggior parte dei pulsanti della barra multifunzione è disponibile anche nei menu di scelta rapida. 
 
![Indice di spostamento degli aggiornamenti software per Configuration Manager](media/ribbon.png)

### <a name="details-pane"></a>Riquadro dettagli
È possibile ottenere informazioni aggiuntive sugli elementi esaminando il riquadro dei dettagli. Il riquadro dei dettagli può avere una o più schede. Le schede varieranno a seconda del nodo. 
![Riquadro dei dettagli di Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colonne 
È possibile aggiungere, rimuovere, riordinare e ridimensionare le colonne. Queste azioni consentono di visualizzare i dati che si preferisce. Le colonne disponibili varieranno a seconda del nodo. Fare clic con il pulsante destro del mouse su un'intestazione di colonna esistente, quindi scegliere un elemento da aggiungere o rimuovere dalla vista. Riordinare le colonne trascinando l'intestazione di colonna nella posizione desiderata. 
![Aggiungere colonne in Configuration Manager](media/add-columns.png)

Nella parte inferiore del menu di scelta rapida della colonna è possibile ordinare o raggruppare in base a una colonna. È anche possibile ordinare in base a una colonna facendo clic sull'intestazione. 

![Raggruppare per colonna in Configuration Manager](media/column-group-by.png)

##<a name="console-command-line-options"></a>Opzioni della riga di comando della console
La console di Microsoft System Center Configuration Manager include le seguenti opzioni della riga di comando.

|Opzione|Descrizione|  
|------------|-----------------|  
|**/sms:debugview=1**|Una DebugView viene inserita in tutte le ResultViews che specificano una visualizzazione. DebugView mostra le proprietà non elaborate (nomi e valori).|  
|**/sms:NamespaceView=1**|Mostra la visualizzazione dello spazio dei nomi nella console di System Center Configuration Manager.|  
|**/sms:ResetSettings**|La console di System Center Configuration Manager ignora la connessione permanente dell'utente e gli stati di visualizzazione (le dimensioni della finestra di Microsoft Management Console non vengono reimpostate).|  
|**/sms:IgnoreExtensions**|Disabilita tutte le estensioni di System Center Configuration Manager.|  
|**/sms:NoRestore**|La console di System Center Configuration Manager ignora la navigazione dei nodi persistente precedente.|  

## <a name="console-improvements-in-version-1806"></a>Miglioramenti della console nella versione 1806
In Configuration Manager versione 1806 sono stati aggiunti i miglioramenti della console seguenti:

- **Utente/i primario/i** è disponibile come colonna nel nodo del dispositivo. <!--1357280-->
- **Utente attualmente connesso** è disponibile come colonna nel nodo del dispositivo.<!--1358202-->
- Copiare le informazioni dal riquadro **Dettagli asset** per le viste di monitoraggio seguenti: <!--1357856-->
    - Stato distribuzione contenuto
    - Stato distribuzione 

    ![Copiare i dettagli degli asset in Configuration Manager](media/1810-deployment-status.PNG)

 - Inviare commenti e suggerimenti dalla console. È possibile salvare una copia da inviare in un secondo momento se non si ha accesso a Internet. <!--1357542-->
   
    - **Invia smile**: inviare commenti e suggerimenti su ciò che è stato apprezzato.
    - **Invia faccia imbronciata**: inviare commenti e suggerimenti su ciò che non è stato apprezzato. 
    - **Invia un suggerimento**: consente di accedere a UserVoice per condividere la propria opinione. 
 
       ![Inviare commenti e suggerimenti per Configuration Manager](media/1810-send-a-smile.PNG)
![Modulo di feedback di Configuration Manager](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Funzionalità di accessibilità](../../understand/accessibility-features.md)

