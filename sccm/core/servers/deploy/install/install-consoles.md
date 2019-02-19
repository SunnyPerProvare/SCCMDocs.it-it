---
title: Installare la console
titleSuffix: Configuration Manager
description: Installare la console di Configuration Manager per la connessione a un sito di amministrazione centrale o a un sito primario.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35bfd908864ee77c19821ce02ab62c03523fae37
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126947"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installare la console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli amministratori usano la console di Configuration Manager per gestire l'ambiente di Configuration Manager. Ogni console di Configuration Manager può connettersi a un sito di amministrazione centrale o a un sito primario. Non è possibile connettere una console di Configuration Manager a un sito secondario.

> [!NOTE]  
>  Gli amministratori possono visualizzare gli oggetti nella console in base alle autorizzazioni assegnate al proprio account utente. Per altre informazioni sull'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Quando si installa il server del sito, è possibile installare la console di Configuration Manager nello stesso momento. Per installare la console in un momento diverso rispetto all'installazione del server del sito, eseguire il programma di installazione autonomo.  

 Usare la procedura seguente per installare la console di Configuration Manager tramite il programma di installazione autonomo.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Per installare la console di Configuration Manager usando l'Installazione guidata  

1.  Verificare che siano soddisfatti i requisiti seguenti:  

    -  Avere i diritti di **Amministratore** locale nel computer in cui verrà installata la console.  

    -   Si dispone di autorizzazioni di **lettura** per il percorso dei file di installazione della console di Configuration Manager.  

2.  Passare a una delle seguenti posizioni:  

    -   Dal server del sito, accedere a: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   Dal supporto di origine di Configuration Manager, accedere a: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Come procedura consigliata, avviare il programma di installazione della console di Configuration Manager da un server del sito piuttosto che dal supporto di installazione di System Center Configuration Manager. Quando si installa un server del sito, questo copia i file di installazione della console di Configuration Manager e i Language Pack supportati per il sito nella sottocartella **Tools\ConsoleSetup**. Quando si installa la console di Configuration Manager dai supporti di installazione viene sempre installata la versione in lingua inglese. Questo comportamento si verifica anche se il server del sito supporta diverse lingue o il sistema operativo del computer di destinazione è impostato su una lingua diversa. Facoltativamente, è possibile copiare la cartella **ConsoleSetup** in un percorso alternativo per avviare l'installazione.

3.  Per aprire l'Installazione guidata della console di Configuration Manager, fare doppio clic su **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installare sempre la console di Configuration Manager usando **consolesetup.exe**. Anche se è possibile installare la console di Configuration Manager eseguendo adminconsole.msi, con questo metodo non viene eseguita la verifica delle dipendenze o dei prerequisiti. L'installazione potrebbe non essere completata correttamente.  

4.  Nella procedura guidata selezionare **Avanti**.  

5.  Nella pagina **Server del sito** immettere il nome di dominio completo (FQDN) del server del sito al quale si connette la console di Configuration Manager.  

6.  Nella pagina **Cartella di installazione** immettere la cartella di installazione per la console di Configuration Manager. Il percorso della cartella non deve contenere spazi o caratteri Unicode.  

7.  Nella pagina **Analisi utilizzo software** selezionare se partecipare all'Analisi utilizzo software.  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

8.  Nella pagina **Inizio installazione** selezionare **Installa** per installare la console di Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Per installare la console di Configuration Manager da un prompt dei comandi  

1.  Nel server da cui si installa la console di Configuration Manager aprire una finestra del prompt dei comandi e accedere a uno dei percorsi seguenti:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Quando si installa la console di Configuration Manager da un prompt dei comandi viene sempre installata la versione in lingua inglese. Questo comportamento si verifica anche se il sistema operativo del computer di destinazione è impostato su una lingua diversa. Per installare la console di Configuration Manager in una lingua diversa dall'inglese, è necessario [installare la console di Configuration Manager usando l'Installazione guidata](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  Al prompt dei comandi digitare **consolesetup.exe**. Scegliere tra le opzioni della riga di comando seguenti:  

|  Opzione di riga di comando     | Descrizione     |
  |-------------|-------------|
  |/q|Installa la console di Configuration Manager in modalità automatica. Le opzioni **EnableSQM**, **TargetDir**e **DefaultSiteServerName** sono obbligatorie solo quando si usa questa opzione.|  
  |/uninstall|Disinstalla la console di Configuration Manager. Specificare per prima questa opzione quando viene usata con l'opzione **/q**.|  
  |LangPackDir|Specifica il percorso alla cartella che contiene i file di lingua. È possibile usare il **Downloader di installazione** per scaricare i file di lingua. Se non si usa questa opzione, il programma di installazione ricerca la cartella della lingua nella cartella corrente. Se la cartella della lingua non viene trovata, il programma di installazione prosegue con l'installazione della sola versione in lingua inglese. Per altre informazioni, vedere [Downloader di installazione](setup-downloader.md).|  
  |TargetDir|Specifica la cartella di installazione per installare la console di Configuration Manager. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  
  |EnableSQM|Specifica se partecipare all'Analisi utilizzo software (CEIP). Usare un valore di **1** per partecipare all'Analisi utilizzo software e un valore di **0** per non partecipare a tale analisi. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .</br></br>Nota: A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.  Se si usa il parametro, l'installazione non riuscirà.|  
  |DefaultSiteServerName|Specifica l'FQDN del server del sito a cui si connette la console all'apertura. Questa opzione è obbligatoria solo quando si usa l'opzione **/q** .|  


  ### <a name="examples"></a>Esempi
  **Per le versioni 1802 e successive NON includere il parametro EnableSQM**
  -  `ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

  -  `ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com EnableSQM=1  LangPackDir=C:\Downloads\ConfigMgr`  

  -  `ConsoleSetup.exe /uninstall /q`  
