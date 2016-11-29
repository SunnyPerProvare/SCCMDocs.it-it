---
title: Installare le console | System Center Configuration Manager
description: Informazioni sull'installazione di console di Configuration Manager per la connessione a un sito di amministrazione centrale o un sito primario.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1483e35a397667a340605c0454c1835ec6067d9e

---
# <a name="install-system-center-configuration-manager-consoles"></a>Installare le console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Gli utenti amministratori usano la console di System Center Configuration Manager per gestire l'ambiente di Configuration Manager. Ogni console di Configuration Manager può connettersi a un sito di amministrazione centrale o a un sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario.


> [!NOTE]  
>  Gli oggetti visualizzati per l'utente amministratore che sta eseguendo la console dipendono dai privilegi assegnati a tale utente. Per altre informazioni sull'amministrazione basata su ruoli, vedere [Fundamentals of role-based administration for System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md) (Nozioni di base sull'amministrazione basata su ruoli per System Center Configuration Manager).  

 È possibile installare la console di Configuration Manager durante l'installazione del server del sito durante l'installazione guidata oppure eseguire l'applicazione autonoma.  

 Usare la procedura seguente per installare una console di Configuration Manager tramite l'applicazione autonoma.  

## <a name="to-install-a-configuration-manager-console"></a>Per installare una console di Configuration Manager  

1.  Verificare che l'utente amministratore che esegue l'applicazione della console di Configuration Manager disponga dei seguenti diritti di sicurezza:  

    -   Diritti di**amministratore locale** sul computer su cui verrà eseguita la console.  

    -   Autorizzazione di **lettura** per il percorso dei file di installazione della console di Configuration Manager.  

2.  Passare a una delle seguenti posizioni:  

    -   Dal supporto di origine di Configuration Manager passare a **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386**  

    -   Nel server del sito passare a **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    > [!TIP]  
    >  Come procedura consigliata, avviare l'installazione della console di Configuration Manager da un server del sito piuttosto che dal supporto di installazione di System Center Configuration Manager. Il metodo di installazione del server del sito copia i file di installazione della console di Configuration Manager e i Language Pack supportati per il sito nella sottocartella **Tools\ConsoleSetup**. Se si installa la console di Configuration Manager dal supporto di installazione, sarà sempre installata la versione inglese, indipendentemente dalle lingue supportate nel server del sito o dalle impostazioni della lingua per il sistema operativo in esecuzione nel computer. Facoltativamente, è possibile copiare la cartella **ConsoleSetup** in un percorso alternativo per avviare l'installazione.  

3.  Fare doppio clic su **consolesetup.exe**. Si aprirà la finestra dell'Installazione guidata della console di Configuration Manager.  

    > [!IMPORTANT]  
    >  Installare sempre la console di Configuration Manager usando consolesetup.exe. Anche se è possibile installare la console di Configuration Manager eseguendo AdminConsole.msi, questo metodo non esegue i controlli dei prerequisiti o delle dipendenze e l'installazione potrebbe non avere esito positivo.  

4.  Nella pagina di apertura fare clic su **Avanti**.  

5.  Nella pagina **Server del sito** specificare il nome di dominio completo (FQDN) del server del sito al quale si connetterà la console di Configuration Manager.  

6.  Nella pagina **Cartella di installazione** specificare la cartella di installazione per la console di Configuration Manager. Il percorso della cartella non deve contenere spazi o caratteri Unicode.  

7.  Nella pagina **Analisi utilizzo software** scegliere se partecipare all'Analisi utilizzo software.  

8.  Nella pagina **Inizio installazione** fare clic su **Installa** per installare la console di Configuration Manager.  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>Per installare una console di Configuration Manager da un prompt dei comandi  

1.  Nel server da cui si installa la console di Configuration Manager aprire una finestra del prompt dei comandi e passare a una delle posizioni seguenti:  

    -   **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quando si installa una console di Configuration Manager al prompt dei comandi, viene sempre installata la versione inglese, indipendentemente dall'impostazione della lingua per il sistema operativo in esecuzione nel computer. Per installare la console di Configuration Manager in un'altra lingua, è necessario usare la procedura precedente.  

2.  Digitare **consolesetup.exe** e scegliere tra le opzioni di riga di comando seguenti.  

|  Opzione di riga di comando     | Descrizione     |
  | :------------- | :------------- |
  |/q|Installa la console di Configuration Manager in modalità automatica. Le opzioni **EnableSQM**, **TargetDir**e **DefaultSiteServerName** sono obbligatorie solo quando si usa questa opzione.|  
  |/uninstall|Disinstalla la console di Configuration Manager. È necessario specificare per prima questa opzione quando viene usata con l'opzione **/q** .|  
  |LangPackDir|Specifica il percorso alla cartella che contiene i file di lingua. È possibile usare il **Downloader di installazione** per scaricare i file di lingua. Se non si usa questa opzione, il programma di installazione ricerca la cartella della lingua nella cartella corrente. Se la cartella della lingua non viene trovata, il programma di installazione prosegue con l'installazione della sola versione in lingua inglese. Per altre informazioni, vedere [Downloader di installazione](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Specifica la cartella di installazione per installare la console di Configuration Manager. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  
  |EnableSQM|Specifica se partecipare all'Analisi utilizzo software (CEIP). Usare un valore di 1 per partecipare all'Analisi utilizzo software e un valore di 0 per non partecipare a tale analisi. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  
  |DefaultSiteServerName|Specifica l'FQDN del server del sito a cui si connette la console all'apertura. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  


  **Esempi di utilizzo:**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Nov16_HO1-->


