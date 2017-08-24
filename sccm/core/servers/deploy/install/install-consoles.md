---
title: Installare una console | Microsoft Docs
description: Informazioni sull'installazione della console di Configuration Manager per la connessione a un sito di amministrazione centrale o un sito primario.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installare la console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli amministratori usano la console di System Center Configuration Manager per gestire l'ambiente di Configuration Manager. Ogni console di Configuration Manager può connettersi a un sito di amministrazione centrale o a un sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario.

> [!NOTE]  
>  Gli oggetti visualizzati da un amministratore che sta eseguendo la console dipendono dalle autorizzazioni assegnate al relativo account utente. Per altre informazioni sull'amministrazione basata su ruoli, vedere [Fundamentals of role-based administration for System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md) (Nozioni di base sull'amministrazione basata su ruoli per System Center Configuration Manager).  

 È possibile installare la console di Configuration Manager durante l'installazione del server del sito tramite l'Installazione guidata oppure eseguire un'applicazione autonoma che usi l'Installazione guidata.  

 Usare la procedura seguente per installare una console di Configuration Manager tramite l'applicazione autonoma.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Per installare la console di Configuration Manager usando l'Installazione guidata  

1.  Verificare che siano soddisfatti i requisiti seguenti:  

    -  Si dispone di diritti di **amministratore locale** nel computer in cui verrà eseguita la console.  

    -   Si dispone di autorizzazioni di **lettura** per il percorso dei file di installazione della console di Configuration Manager.  

2.  Passare a una delle seguenti posizioni:  

    -   Nel server del sito passare a **<*percorso di installazione server del sito di Configuration Manager*>\Tools\ConsoleSetup**.  

    -   Dal supporto di origine di Configuration Manager passare a **<*file di origine di Configuration Manager*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Come procedura consigliata, avviare l'installazione della console di Configuration Manager da un server del sito piuttosto che dal supporto di installazione di System Center Configuration Manager. Il metodo di installazione del server del sito copia i file di installazione della console di Configuration Manager e i Language Pack supportati per il sito nella sottocartella **Tools\ConsoleSetup**. L'installazione della console di Configuration Manager dal supporto di installazione comporta sempre l'installazione della versione inglese, indipendentemente dalle lingue supportate nel server del sito o dalle impostazioni della lingua del sistema operativo in esecuzione nel computer. Facoltativamente, è possibile copiare la cartella **ConsoleSetup** in un percorso alternativo per avviare l'installazione.

3.  Per aprire l'Installazione guidata della console di Configuration Manager, fare doppio clic su **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installare sempre la console di Configuration Manager usando consolesetup.exe. Anche se è possibile installare la console di Configuration Manager eseguendo adminconsole.msi, questo metodo non esegue i controlli dei prerequisiti o delle dipendenze e l'installazione potrebbe non avere esito positivo.  

4.  Nella procedura guidata selezionare **Avanti**.  

5.  Nella pagina **Server del sito** immettere il nome di dominio completo (FQDN) del server del sito al quale si connetterà la console di Configuration Manager.  

6.  Nella pagina **Cartella di installazione** immettere la cartella di installazione per la console di Configuration Manager. Il percorso della cartella non deve contenere spazi o caratteri Unicode.  

7.  Nella pagina **Analisi utilizzo software** selezionare se partecipare all'Analisi utilizzo software.  

8.  Nella pagina **Inizio installazione** selezionare **Installa** per installare la console di Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Per installare la console di Configuration Manager da un prompt dei comandi  

1.  Nel server da cui si installa la console di Configuration Manager aprire una finestra del prompt dei comandi e passare a una delle posizioni seguenti:  

    -   **<*percorso di installazione server del sito di Configuration Manager*>\Tools\ConsoleSetup**  

    -   **<*supporto di installazione di Configuration Manager*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Quando si installa la console di Configuration Manager da un prompt dei comandi, viene sempre installata la versione inglese, indipendentemente dall'impostazione della lingua del sistema operativo in esecuzione nel computer. Per installare la console di Configuration Manager in una lingua diversa dall'inglese, è necessario [installare la console di Configuration Manager usando l'Installazione guidata](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Al prompt dei comandi digitare **consolesetup.exe**. Scegliere tra le opzioni della riga di comando seguenti.  

|  Opzione di riga di comando     | Descrizione     |
  | :------------- | :------------- |
  |/q|Installa la console di Configuration Manager in modalità automatica. Le opzioni **EnableSQM**, **TargetDir**e **DefaultSiteServerName** sono obbligatorie solo quando si usa questa opzione.|  
  |/uninstall|Disinstalla la console di Configuration Manager. È necessario specificare per prima questa opzione quando viene usata con l'opzione **/q** .|  
  |LangPackDir|Specifica il percorso alla cartella che contiene i file di lingua. È possibile usare il **Downloader di installazione** per scaricare i file di lingua. Se non si usa questa opzione, il programma di installazione ricerca la cartella della lingua nella cartella corrente. Se la cartella della lingua non viene trovata, il programma di installazione prosegue con l'installazione della sola versione in lingua inglese. Per altre informazioni, vedere [Downloader di installazione](setup-downloader.md).|  
  |TargetDir|Specifica la cartella di installazione per installare la console di Configuration Manager. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  
  |EnableSQM|Specifica se partecipare all'Analisi utilizzo software (CEIP). Usare un valore di **1** per partecipare all'Analisi utilizzo software e un valore di **0** per non partecipare a tale analisi. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  
  |DefaultSiteServerName|Specifica l'FQDN del server del sito a cui si connette la console all'apertura. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  


  **Esempi:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
