---
title: Gestire computer Windows in remoto | Microsoft Docs
description: Amministrare un computer client Windows da posizione remota tramite System Center Configuration Manager.
ms.custom: na
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: aecc4ccfec98932f3988f1ca1fcdc898cd417933
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Come amministrare un computer client Windows in remoto mediante System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di iniziare a usare il controllo remoto, assicurarsi di aver esaminato le informazioni contenute negli argomenti seguenti:  

-   [Prerequisiti per il controllo remoto in System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configurazione del controllo remoto in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Di seguito vengono elencati tre modi per avviare il visualizzatore controllo remoto:  

-   Dalla console di Configuration Manager.  

-   A un prompt dei comandi di Windows.  

-   Dal menu **Start** di Windows in un computer che esegue la console di Configuration Manager dal gruppo di programmi **Microsoft System Center**.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Per amministrare un computer client in remoto dalla console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi** oppure **Raccolte di dispositivi**.  

3.  Selezionare il computer che si vuole gestire in remoto e quindi nel gruppo **Dispositivo** della scheda **Home** selezionare **Avvia** > **Controllo remoto**.  

    > [!IMPORTANT]  
    >  Se l'impostazione client **Richiedere all'utente l'autorizzazione di controllo remoto** è impostata su **True**, la connessione si avvia solo quando l'utente del computer remoto risponde affermativamente alla richiesta del controllo remoto. Per altre informazioni, vedere [Configurazione del controllo remoto in System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Quando la finestra **Controllo remoto di Configuration Manager** si apre, è possibile amministrare il computer client in remoto. Per configurare la connessione, usare le opzioni seguenti.  

    > [!NOTE]  
    >  Se il computer a cui ci si connette ha diversi monitor, nella finestra del controllo remoto viene visualizzato ciò che compare su tutti i monitor.  

    -   **File - Connetti**: esegue la connessione a un altro computer. Questa opzione non è disponibile quando è attiva una sessione di controllo remoto.  

    -   **File - Disconnetti**: disconnette la sessione di controllo remoto attiva ma non chiude la finestra **Controllo remoto di Configuration Manager**.  

    -   **File - Esci**: disconnette la sessione di controllo remoto attiva e chiude la finestra **Controllo remoto di Configuration Manager**.  

        > [!NOTE]  
        >  Quando si disconnette una sessione di controllo remoto, il contenuto degli Appunti di Windows nel computer che si sta visualizzando viene eliminato.  

    -   **Visualizza - Schermo intero**: ingrandisce la finestra **Controllo remoto di Configuration Manager**.  

        > [!NOTE]  
        >  Per uscire dalla modalità schermo intero, premere CTRL+ALT+INTERR.  

    -   **Visualizza - Adatta**: ridimensiona la visualizzazione del computer remoto in modo da adattarla alle dimensioni della finestra **Controllo remoto di Configuration Manager**.  

    -   **Visualizza - Barra di stato**: attiva e disattiva la visualizzazione della barra di stato della finestra **Controllo remoto di Configuration Manager**.  

    -   **Azione - Invia CTRL+ALT+CANC**: invia la combinazione di tasti CTRL+ALT+CANC al computer remoto.  

    -   **Azione - Abilita condivisione Appunti**: consente di copiare e incollare elementi nel e dal computer remoto. Se si modifica questo valore, per rendere effettiva la modifica è necessario riavviare la sessione di controllo remoto.  

        > [!NOTE]  
        >  Se non si vuole abilitare la condivisione degli Appunti nella console di Configuration Manager, impostare il valore della chiave del Registro di sistema **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** a **0** nel computer che esegue la console.  

    -   **Azione - Blocca tastiera e mouse remoti**: blocca la tastiera e il mouse remoti per impedire all'utente di eseguire operazioni nel computer remoto.  

    -   **Guida - Informazioni su Controllo remoto**: visualizza la versione corrente del visualizzatore.  

5.  Gli utenti del computer remoto possono visualizzare altre informazioni sulla sessione di controllo remoto facendo clic sull'icona **Controllo remoto** di Configuration Manager nell'area di notifica di Windows o sull'icona della barra della sessione di controllo remoto.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Per avviare il visualizzatore controllo remoto dalla riga di comando di Windows  

-   Al prompt dei comandi di Windows, digitare *<cartella di installazione di Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe supporta le opzioni da riga di comando seguenti:  

- *Indirizzo*: specifica il nome NetBIOS, il nome di dominio completo (FQDN) o l'indirizzo IP del computer client a cui ci si vuole connettere.
- *Nome del server del sito*: specifica il nome del server del sito di System Center Configuration Manager al quale si vogliono inviare messaggi di stato relativi alla sessione di controllo remoto.
- **/?** : visualizza le opzioni da riga di comando per il visualizzatore controllo remoto.  
     
**Esempio: CmRcViewer.exe** *<Indirizzo\>* *<\\\nome del server del sito>*  
