---
title: 'Aggiornare i client macOS '
titleSuffix: Configuration Manager
description: Aggiornare i client di System Center Configuration Manager in computer Mac.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: 
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7ce260a4d93e58e31ec14219c317c793d4b9bb32
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Come aggiornare i client di System Center Configuration Manager in computer Mac

*Si applica a: System Center Configuration Manager (Current Branch)*

Seguire la procedura dettagliata descritta di seguito per aggiornare il client in computer Mac usando un'applicazione di System Center Configuration Manager. In alternativa, è anche possibile scaricare il file di installazione del client Mac, copiarlo in un percorso di rete condiviso o in una cartella locale del computer Mac, quindi fornire agli utenti le istruzioni per eseguire l'installazione manualmente.  

> [!NOTE]  
>  Prima di eseguire questi passaggi, assicurarsi che il computer Mac soddisfi i prerequisiti. Vedere [Supported operating systems for Mac computers](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers) (Sistemi operativi supportati per computer Mac).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Passaggio 1: scaricare il file di installazione del client Mac più recente da Area download Microsoft  
 Il client Mac per Configuration Manager non è disponibile sul supporto di installazione di Configuration Manager e deve essere scaricato da Area download Microsoft. I file di installazione del client Mac sono contenuti in un file Windows Installer denominato ConfigmgrMacClient.msi.  

 È possibile scaricare questo file dall' [Area download Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Passaggio 2: eseguire il file di installazione scaricato per creare il file di installazione del client Mac  
 Su un computer che esegue Windows, eseguire il file **ConfigmgrMacClient.msi** scaricato per decomprimere il file di installazione del client Mac, denominato **Macclient.dmg**. Per impostazione predefinita, questo file si trova nella cartella **C:\Programmi (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** del computer Windows dopo che i file sono stati decompressi.  

## <a name="step-3-extract-the-client-installation-files"></a>Passaggio 3: estrarre i file di installazione client  
 Copiare il file Macclient.dmg in una condivisione di rete o in una cartella locale su un computer Mac. Dal computer Mac, montare e quindi aprire il file Macclient.dmg e copiare i file in una cartella del computer Mac.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Passaggio 4: creare un file con estensione cmmac che può essere usato per creare un'applicazione  

1.  Usare lo strumento **CMAppUtil** (disponibile nella cartella **Strumenti** dei file di installazione del client Mac) per creare un file .cmmac dal pacchetto di installazione client. Questo file servirà per creare l'applicazione di Configuration Manager.  

2.  Copiare il nuovo file **CMClient.pkg.cmmac** in un percorso disponibile per il computer che esegue la console di Configuration Manager.  

 Per altre informazioni, vedere [Supplemental procedures to create and deploy applications for Mac computers](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers) (Procedure supplementari per creare e distribuire applicazioni per computer Mac).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Passaggio 5:** creare e distribuire un'applicazione contenente i file del client Mac  

1.  Nella console di Configuration Manager creare un'applicazione dal file **CMClient.pkg.cmmac** che contiene i file di installazione del client.  

2.  Distribuire l'applicazione nei computer Mac della gerarchia.  

 Per altre informazioni, vedere [Creating Mac computer applications with System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md) (Creazione di applicazioni per computer Mac con System Center Configuration Manager).  

## <a name="step-6-users-install-the-latest-client"></a>Passaggio 6: installare il client più recente  
 Gli utenti di client Mac saranno informati sulla disponibilità di un aggiornamento al client di Configuration Manager che dovrà essere installato. Al termine, è necessario riavviare il computer Mac.  

 Dopo il riavvio del computer, viene eseguita automaticamente la registrazione guidata computer per richiedere un nuovo certificato utente.  

 Se non si usa la registrazione di Configuration Manager, ma si installa il certificato client indipendentemente da Configuration Manager, vedere [Configurare il client aggiornato per usare un certificato esistente](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 Eseguire la procedura seguente per impedire che venga eseguita la registrazione guidata computer e per configurare il client aggiornato in modo da usare un certificato client esistente.  

-   Nella console di Configuration Manager creare un elemento di configurazione del tipo **Mac OS X**.  

-   Aggiungere un'impostazione a questo elemento di configurazione con il tipo di impostazione **Script**.  

-   Aggiungere il seguente script all'impostazione:  

    ```  
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

-   Aggiungere l'elemento di configurazione a una linea di base di configurazione, distribuire la linea di base di configurazione in tutti i computer Mac che installano un certificato indipendentemente da Configuration Manager.  

 Per altre informazioni su come creare e distribuire elementi di configurazione per computer Mac, vedere [How to create configuration items for Mac OS X devices managed with the System Center Configuration Manager client](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) (Come creare elementi di configurazione per dispositivi Mac OS X gestiti con il client di System Center Configuration Manager) e [How to deploy configuration baselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md) (Come distribuire le linee di base di configurazione in System Center Configuration Manager).  
