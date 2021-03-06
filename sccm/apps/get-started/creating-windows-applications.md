---
title: Creare applicazioni Windows
titleSuffix: Configuration Manager
description: Altre informazioni sulla creazione e sulla distribuzione di applicazioni Windows in Configuration Manager.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 97b28f59308bf807bfaea577138fee4e4c17e8fb
ms.sourcegitcommit: fa806f4691befecc7f95a3213f709acfa520a132
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2020
ms.locfileid: "78289971"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Creare applicazioni Windows in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di Configuration Manager per la [creazione di un'applicazione](/sccm/apps/deploy-use/create-applications), quando si creano e si distribuiscono applicazioni per i dispositivi Windows è necessario tenere presente quanto segue.  



## <a name="bkmk_general"></a> Considerazioni generali  

Configuration Manager supporta la distribuzione dei formati pacchetto app Windows (con estensione appx) e bundle dell'app (con estensione appxbundle) per dispositivi Windows 8.1 e Windows 10.

Quando si crea un'applicazione nella console di Configuration Manager, come **Tipo** del file di installazione dell'applicazione selezionare **Pacchetto app Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** . Per altre informazioni sulla creazione di app in generale, vedere [Creare applicazioni](/sccm/apps/deploy-use/create-applications). Per altre informazioni sul formato MSIX, vedere [Supporto per il formato MSIX](#bkmk_msix). 

> [!Note]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Effettuare il provisioning dei pacchetti app Windows per tutti gli utenti in un dispositivo
<!--1358310-->
a partire dalla versione 1806, è possibile effettuare il provisioning di un'applicazione con un pacchetto dell'app di Windows per tutti gli utenti nel dispositivo. Un esempio comune di questo scenario è il provisioning di un'app da Microsoft Store per le aziende e la formazione, ad esempio Minecraft: Education Edition, in tutti i dispositivi usati dagli studenti di una scuola. In precedenza, Configuration Manager supportava solo l'installazione di queste applicazioni per ogni utente. Dopo aver eseguito l'accesso a un nuovo dispositivo, uno studente dovrebbe attendere prima di poter accedere a un'app. Ora quando viene eseguito il provisioning dell'app nel dispositivo per tutti gli utenti, tutti possono essere produttivi più rapidamente.

> [!Important]  
> Prestare attenzione con l'installazione, il provisioning e l'aggiornamento di versioni diverse dello stesso pacchetto di app di Windows in un dispositivo, poiché possono causare risultati imprevisti. Questo comportamento può verificarsi quando si usa Configuration Manager per eseguire il provisioning dell'app, ma dopo si consente agli utenti di aggiornare l'app dal Microsoft Store. Per altre informazioni, vedere le istruzioni del passaggio successivo quando si [gestiscono le app dal Microsoft Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Quando si esegue il provisioning di un'app con licenza offline Configuration Manager non consente a Windows di aggiornarla automaticamente dal Microsoft Store.  

Configuration Manager supporta il provisioning di app nelle versioni seguenti di Windows:<!--SCCMDocs-pr issue 2762-->
- Azione di installazione: Windows 10 versione 1607 e successive
- Azione di disinstallazione: Windows 10 versione 1703 e successive

Per configurare un tipo di distribuzione delle app Windows per questa funzionalità, abilitare l'opzione **Effettua il provisioning di questa applicazione per tutti gli utenti nel dispositivo**. Per altre informazioni, vedere [Create applications](/sccm/apps/deploy-use/create-applications) (Creare le applicazioni).


> [!Note]  
> Se è necessario disinstallare un'applicazione con provisioning dai dispositivi a cui gli utenti hanno già eseguito l'accesso, è necessario creare due distribuzioni di disinstallazione. Scegliere come destinazione della prima distribuzione di disinstallazione una raccolta di dispositivi che contenga i dispositivi. Scegliere come destinazione della seconda distribuzione di disinstallazione una raccolta di utenti che contenga gli utenti che hanno eseguito l'accesso ai dispositivi con l'applicazione con provisioning. Quando si disinstalla un'app con provisioning in un dispositivo, Windows attualmente non disinstalla l'app anche per gli utenti. 



## <a name="bkmk_msix"></a> Supporto per il formato MSIX
<!--1357427-->

A partire dalla versione 1806, Configuration Manager supporta i nuovi formati di pacchetto dell'app Windows 10 (con estensione msix) e bundle dell'app (con estensione msixbundle). Windows 10 versione 1809 o versioni successive supportano questi nuovi formati.  

- Per una panoramica di MSIX, vedere [A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/) (MSIX più da vicino).  

- Per informazioni su come creare una nuova app MSIX, vedere [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) (Introduzione del supporto di MSIX nella build di Insider 17682).  


### <a name="convert-applications-to-msix"></a>Convertire le applicazioni in MSIX
<!--3607729, fka 1359029-->

A partire dalla versione 1810, convertire le applicazioni Windows Installer (con estensione msi) esistenti nel formato MSIX. 

#### <a name="prerequisites"></a>Prerequisiti
- Un dispositivo di riferimento che esegue Windows 10 versione 1809 o versione successiva  

- Accedere a Windows su questo dispositivo come un utente con diritti amministrativi locali  

- Installare le app seguenti nel dispositivo:  

    - Console di Configuration Manager  

    - Installare [MSIX Packaging Tool](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) da Microsoft Store  

    - Installare il [driver dello strumento di creazione di pacchetti MSIX](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Non installare altri servizi o app in questo dispositivo. È il sistema di riferimento. 

#### <a name="process-to-convert-applications-to-msix-format"></a>Processo per convertire le applicazioni in formato MSIX
1. Nella console di Configuration Manager con privilegi elevati accedere all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Applicazioni**.  

2. Selezionare un'applicazione con tipo di distribuzione Windows Installer (.msi).  

    > [!Note]  
    > È necessario essere in grado di accedere al contenuto di origine dell'applicazione dal dispositivo di riferimento.  
    > 
    > Il nome dell'applicazione non può contenere caratteri speciali. Configuration Manager usa il nome dell'app come nome del file di output.  
    > 
    > Non installare questa applicazione nel dispositivo di riferimento in anticipo.  

3. Selezionare **Convert to .MSIX** (Converti in MSIX) nella barra multifunzione.

Al termine della procedura guidata, lo strumento MSIX Packaging Tool crea un file MSIX nella posizione specificata nella procedura guidata. Durante questo processo, Configuration Manager installa automaticamente l'applicazione nel dispositivo di riferimento.

Se il processo non riesce, la pagina di riepilogo punta al file di log con altre informazioni. Se si verifica un errore relativo all'acquisizione dello stato utente, disconnettersi da Windows. Il problema potrebbe risolversi eseguendo nuovamente l'accesso.

Per usare questa app MSIX, è prima necessario firmarla digitalmente in modo che i client la considerino attendibile. Per altre informazioni su questo processo, vedere gli articoli seguenti: 
- [MSIX – The MSIX Packaging Tool – signing the MSIX package](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/) (MSIX - MSIX Packaging Tool - Firma del pacchetto MSIX)
- [Come firmare un pacchetto di app con SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Dopo l'accesso all'app, creare un nuovo tipo di distribuzione nell'applicazione in Configuration Manager. Per altre informazioni, vedere [Creare tipi di distribuzione per l'applicazione](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).




## <a name="bkmk_uwp"></a> Supporto per app UWP (Universal Windows Platform)  

I dispositivi Windows 10 non richiedono una chiave di sideload per l'installazione di app line-of-business. Per abilitare il sideload in Windows, tuttavia, la chiave `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` del Registro di sistema deve avere un valore pari a **1**.  

Se non si configura questa chiave del Registro di sistema, Configuration Manager imposta automaticamente questo valore su **1** alla prima distribuzione di un'app nel dispositivo. Se questo valore è stato impostato su **0**, Configuration Manager non può modificare automaticamente il valore e non è possibile distribuire l'app line-of-business.  

Firmare digitalmente le app line-of-business UWP. Usare un certificato di firma codice ritenuto attendibile in ogni dispositivo in cui si distribuisce l'app. Usare certificati del PKI dell'organizzazione o acquistare un certificato da un fornitore di terze parti il cui certificato radice pubblico sia già ritenuto attendibile da Windows.  

Per firmare i pacchetti di app per dispositivi mobili, usare la tabella seguente per determinare il tipo di certificato di firma codice da usare:

| Pacchetto  | Symantec  | Non Symantec  |
|---------|---------|---------|
| Pacchetti universali con estensione **appx** nei dispositivi Windows 10 Mobile | Sì | Sì |
| Pacchetti con estensione **xap** | Sì | No | 
| Pacchetti con estensione **appx** creati per Windows Phone 8.1 per l'installazione in dispositivi Windows 10 Mobile | Sì | No | 



## <a name="bkmk_mdm-msi"></a> Distribuire app Windows Installer nei dispositivi Windows 10 registrati in MDM  

Il tipo di distribuzione **Windows Installer tramite MDM (\*.msi)** consente di creare e distribuire app basate su Windows Installer in dispositivi registrati in MDM che eseguono Windows 10.  

Quando si usa questo tipo di distribuzione, tenere presente quanto segue:    

-   Caricare solo un singolo file con estensione MSI.  

-   Configuration Manager usa il codice prodotto e la versione del prodotto del file per il rilevamento dell'app.  

-   Windows usa il comportamento di riavvio predefinito dell'app. Configuration Manager non controlla il comportamento di riavvio dell'app.  

-   I pacchetti MSI per utente vengono installati per un singolo utente.  

-   I pacchetti MSI per computer vengono installati per tutti gli utenti del dispositivo.  

-   Configuration Manager supporta gli aggiornamenti dell'app. Il codice prodotto di MSI per ogni versione deve essere uguale.  
