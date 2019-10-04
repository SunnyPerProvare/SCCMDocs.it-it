---
title: Aggiornare i client macOS
titleSuffix: Configuration Manager
description: Aggiornare il client di Configuration Manager in computer Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33a956bf19a1b14a2190467b2148a3ef4b65e908
ms.sourcegitcommit: b9cc8e723c5d8c3be44edad24ad29d75c0cdd2b0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826130"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Come aggiornare i client nei computer Mac in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Seguire la procedura dettagliata descritta in questo articolo per aggiornare il client per i computer Mac usando un'applicazione di Configuration Manager. È anche possibile scaricare il file di installazione del client Mac, copiarlo in un percorso di rete condiviso o in una cartella locale del computer Mac, quindi fornire agli utenti le istruzioni per eseguire l'installazione manualmente.  

> [!NOTE]  
> Prima di eseguire questa procedura, assicurarsi che il computer Mac soddisfi i prerequisiti. Vedere [Supported operating systems for Mac computers](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers) (Sistemi operativi supportati per computer Mac).  

## <a name="download-the-latest-mac-client"></a>Scaricare il client Mac più recente

Il client Mac per Configuration Manager non è incluso nel supporto di installazione di Configuration Manager. Scaricarlo dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). I file di installazione del client Mac sono contenuti in un file di Windows Installer denominato **ConfigmgrMacClient.msi**.  

## <a name="create-the-mac-client-installation-file"></a>Creare il file di installazione del client Mac

In un computer Windows eseguire **ConfigmgrMacClient.msi**. Questo programma di installazione decomprime il file di installazione del client Mac, denominato **Macclient.dmg**. Questo file è disponibile nella cartella seguente per impostazione predefinita: **C:\Programmi (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client**.  

## <a name="extract-the-client-installation-files"></a>estrarre i file di installazione client

Copiare il file **Macclient.dmg** in un computer Mac. Montare il file Macclient.dmg in macOS e quindi copiare il contenuto in una cartella nel computer Mac.  

## <a name="create-a-cmmac-file"></a>Creare un file con estensione cmmac

1. Aprire la cartella **Tools** dei file di installazione del client Mac. Usare lo strumento **CMAppUtil** per creare un file con estensione cmmac dal pacchetto di installazione client. Questo file servirà per creare l'applicazione di Configuration Manager.  

2. Copiare il nuovo file **CMClient.pkg.cmmac** in un percorso di rete disponibile per il computer che esegue la console di Configuration Manager.  

    Per altre informazioni, vedere [Supplemental procedures to create and deploy applications for Mac computers](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers) (Procedure supplementari per creare e distribuire applicazioni per computer Mac).  

## <a name="create-and-deploy-the-app"></a>Creare e distribuire l’app

1. Nella console di Configuration Manager [creare un'applicazione](/sccm/apps/get-started/creating-mac-computer-applications) dal file **CMClient.pkg.cmmac**.  

2. [Distribuire l'applicazione](/sccm/apps/deploy-use/deploy-applications) nei computer Mac della gerarchia.  

## <a name="install-the-updated-client"></a>Installare il client aggiornato

Il client di Configuration Manager esistente nei computer Mac segnalerà all'utente che è disponibile un aggiornamento per l'installazione. Al termine, è necessario riavviare il computer Mac.  

Dopo il riavvio del computer, viene eseguita automaticamente la **registrazione guidata computer** per richiedere un nuovo certificato utente.

Se non si usa la registrazione di Configuration Manager, ma si installa il certificato client indipendentemente da Configuration Manager, vedere [Configurare i client per l'uso di un certificato esistente](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configurare i client per l'uso di un certificato esistente

Seguire questa procedura per impedire che venga eseguita la registrazione guidata computer e per configurare il client aggiornato in modo da usare un certificato client esistente.  

1. Nella console di Configuration Manager [creare un elemento di configurazione](/sccm/compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client) del tipo **Mac OS X**.  

1. Aggiungere un'impostazione a questo elemento di configurazione con il tipo di impostazione **Script**.  

1. Aggiungere il seguente script all'impostazione:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Aggiungere l'elemento di configurazione a una [linea di base di configurazione](/sccm/compliance/deploy-use/create-configuration-baselines). [Distribuire quindi la linea di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines) in tutti i computer Mac che installano un certificato indipendentemente da Configuration Manager.  
