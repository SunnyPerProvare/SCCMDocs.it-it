---
title: Estendere l'inventario hardware | Microsoft Docs
description: Informazioni su come estendere l'inventario hardware in System Center Configuration Manager.
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: "10"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 3e5517e1710d0d12e51fba58efda5dc5edd08544
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Come estendere l'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'inventario hardware legge le informazioni dai PC Windows usando Strumentazione gestione Windows (WMI). WMI è l'implementazione Microsoft di Web-Based Enterprise Management (WBEM), uno standard del settore per l'accesso alle informazioni di gestione in ambiente aziendale. Nelle versioni precedenti di Configuration Manager era possibile estendere l'inventario hardware modificando il file sms_def.mof nel server del sito. Questo file contiene un elenco di classi WMI che può essere letto dall'inventario hardware. Se si modifica questo file, è possibile abilitare e disabilitare classi esistenti e creare anche nuove classi nell'inventario.  

Il file Configuration.mof, usato per definire le classi di dati da inserire nell'inventario hardware nel client, è rimasto lo stesso da Configuration Manager 2012. È possibile creare classi di dati per effettuare un inventario di classi di dati di repository WMI esistenti o personalizzate o chiavi del Registro di sistema presenti nei sistemi client.  

 Il file Configuration.mof definisce e registra anche i provider WMI che accedono alle informazioni durante l'inventario hardware. Registrazione dei provider definisce il tipo di provider da utilizzare e le classi supportate dal provider.  

 Quando sono necessari criteri per i client di Configuration Manager, ad esempio durante l'intervallo di polling dei criteri client standard, il file Configuration.mof viene collegato al corpo dei criteri. Questo file viene quindi scaricato e compilato dai client. Quando si aggiungere, modificare o eliminano classi di dati dal file MOF, i client compilare automaticamente le modifiche apportate alle classi di dati correlati al magazzino. Non sono necessarie altre azioni per eseguire l'inventario di classi di dati nuove o modificate nei client di Configuration Manager. Questo file si trova in **<PercorsoInstallazioneCM\>\Inboxes\clifiles.src\hinv\\** sui server del sito primario.  

 In Configuration Manager non è più possibile modificare il file sms_def.mof come in Configuration Manager 2007. È invece possibile abilitare e disabilitare le classi WMI e aggiungere nuove classi che dovranno essere raccolte dall'inventario hardware usando le impostazioni client. Configuration Manager mette a disposizione i metodi seguenti per estendere l'inventario hardware.  

> [!NOTE]  
>  Se è stato modificato manualmente il file Configuration.mof per aggiungere le classi di inventario personalizzate, queste modifiche verranno sovrascritte quando si aggiorna alla versione 1602. Per continuare a usare le classi personalizzate dopo l'aggiornamento, è necessario aggiungerle alla sezione relativa alle estensioni aggiunte del file Configuration.mof dopo l'aggiornamento alla versione 1602.  
> Tuttavia è necessario evitare di modificare le sezioni che precedono questa, perché sono riservate alle modifiche da parte di Configuration Manager. Un backup del file Configuration.mof personalizzato è disponibile in:  
> **<Directory installazione CM\>\data\hinvarchive\\**.  

|Metodo|Altre informazioni|  
|------------|----------------------|  
|Abilitare o disabilitare le classi di inventario|Abilitare o disabilitare le classi di inventario predefinite o creare impostazioni che consentono di raccogliere classi di inventario hardware diverse dalle raccolte di client specificate. Vedere la procedura [Per abilitare o disabilitare classi di inventario esistenti](#BKMK_Enable) in questo argomento.|  
|Aggiungere una nuova classe di inventario|Aggiungere una nuova classe di inventario dello spazio dei nomi WMI di un altro dispositivo. Vedere la procedura [Per aggiungere una nuova classe di inventario](#BKMK_Add) in questo argomento.|  
|Importazione ed esportazione di classi di inventario hardware|Importare ed esportare file Managed Object Format (MOF) che contengono classi di inventario dalla console di Configuration Manager. Vedere le procedure [Per importare classi di inventario hardware](#BKMK_Import) e [Per esportare classi di inventario hardware](#BKMK_Export) in questo argomento.|  
|Creare file NOIDMIF|Usare file NOIDMIF per raccogliere informazioni sui dispositivi client che non possono essere inclusi nell'inventario da Configuration Manager. È ad esempio raccogliere informazioni sul numeri dispositivo asset che esiste solo come un'etichetta sul dispositivo. Inventario NOIDMIF viene associato automaticamente al dispositivo raccolti dai client. Vedere la sezione [Per creare file NOIDMIF](#BKMK_NOIDMIF) in questo argomento.|  
|Creare i file IDMIF|Usare i file IDMIF per raccogliere informazioni sulle risorse dell'organizzazione non associate a un client di Configuration Manager, ad esempio proiettori, fotocopiatrici e stampanti di rete. Vedere [Per creare file IDMIF](#BKMK_IDMIF) in questo argomento.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedure per estendere l'inventario hardware  
Queste procedure consentono di configurare le impostazioni client predefinite per l'inventario hardware e si applicano a tutti i client nella gerarchia. Per applicare queste impostazioni solo ad alcuni client, creare un'impostazione di dispositivo client personalizzata e assegnarla a una raccolta di client specifici. Vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Per abilitare o disabilitare classi di inventario esistenti  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

6.  Nel **le impostazioni del dispositivo** elenco, fare clic su **Imposta classi**.  

7.  Nel **classi di inventario Hardware** finestra di dialogo selezionare o deselezionare le classi e proprietà della classe deve essere raccolto dall'inventario hardware. È possibile espandere le classi per selezionare o deselezionare le singole proprietà di tale classe. Utilizzare il **ricerca di classi di inventario** campo per la ricerca di singole classi.  

    > [!IMPORTANT]  
    >  Quando si aggiungono nuove classi all'inventario hardware di Configuration Manager, le dimensioni del file di inventario raccolto e inviato al server del sito aumentano. Ciò potrebbe influire negativamente sulle prestazioni della rete e del sito di Configuration Manager. Abilitare solo le classi di inventario che si desidera raccogliere.  


###  <a name="BKMK_Add"></a> Per aggiungere una nuova classe di inventario  

È possibile aggiungere classi di inventario solo dal server di livello superiore nella gerarchia e modificando le impostazioni client predefinite. Questa opzione non è disponibile quando si creano impostazioni dispositivo personalizzati.

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

6.  Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

7.  Nella finestra di dialogo **Classi di inventario hardware** scegliere **Aggiungi**.  

8.  Nel **aggiungere classe di inventario Hardware** nella finestra di dialogo fare clic su **Connect**.  

9. Nel **connessione a Strumentazione gestione Windows (WMI)** finestra di dialogo, specificare il nome del computer da cui si recupererà le classi WMI e lo spazio dei nomi WMI da utilizzare per recuperare le classi. Se si desidera recuperare tutte le classi sotto lo spazio dei nomi WMI specificato, fare clic su **ricorsiva**. Se il computer che si è connessi non è il computer locale, fornire le credenziali di accesso per un account che dispone dell'autorizzazione per accedere a WMI sul computer remoto.  

10. Scegliere **Connetti**.  

11. Nell'elenco **Classi di inventario hardware** nella finestra di dialogo **Aggiungi classe di inventario hardware** selezionare le classi WMI da aggiungere all'inventario hardware di Configuration Manager.  

12. Se si vogliono modificare le informazioni sulla classe WMI selezionata, scegliere **Modifica** e immettere le informazioni seguenti nella finestra di dialogo **Qualificatori di classe**:  

    -   **Nome visualizzato**: questo nome verrà visualizzato in Esplora risorse.  

    -   **Proprietà**: specificare le unità in cui verrà visualizzata ogni proprietà della classe WMI.  

     È inoltre possibile specificare proprietà come proprietà chiave per identificare in modo univoco ogni istanza della classe. Se è stata definita alcuna chiave per la classe e più istanze della classe vengono segnalate dal client, viene archiviata solo l'istanza più recente viene trovata nel database.  

     Dopo aver configurato le proprietà, fare clic su **OK** per chiudere la finestra di dialogo **Qualificatori di classe** e le altre finestre di dialogo aperte. 


###  <a name="BKMK_Import"></a> Per importare classi di inventario hardware  

Quando si modificano le impostazioni client predefinite, è possibile importare solo le classi di inventario. Tuttavia, è possibile utilizzare le impostazioni client personalizzate per importare le informazioni che non contengono una modifica dello schema, ad esempio la modifica della proprietà di una classe esistente da **True** a **False**.  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

6.  Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

7.  Nella finestra di dialogo **Classi di inventario hardware** scegliere **Importa**.  

8.  Nella finestra di dialogo **Importa** selezionare il file Managed Object Format (MOF) che si vuole importare e quindi scegliere **OK**. Controllare gli elementi che verranno importati e quindi fare clic su **Importa**.  

###  <a name="BKMK_Export"></a> Per esportare classi di inventario hardware  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, scegliere **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni client predefinite** scegliere **Inventario hardware**.  

6.  Nell'elenco **Impostazioni del dispositivo** scegliere **Imposta classi**.  

7.  Nella finestra di dialogo **Classi di inventario hardware** scegliere **Esporta**.  

    > [!NOTE]  
    >  Quando si esportano le classi, verranno esportate tutte le classi attualmente selezionate.  

8.  Nella finestra di dialogo **Esporta** selezionare il file Managed Object Format (MOF) in cui esportare le classi e quindi scegliere **Salva**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Come usare file MIF per estendere l'inventario hardware  
 Usare file MIF per estendere le informazioni dell'inventario hardware che Configuration Manager ha raccolto dai client. Durante l'inventario hardware, le informazioni archiviate nel file MIF viene aggiunto al report di inventario client e archiviate nel database del sito, dove è possibile utilizzare i dati nello stesso modo di utilizzare dati di inventario client predefinito. Esistono due tipi di file MIF, NOIDMIF e IDMIF.

> [!IMPORTANT]  
>  Prima di aggiungere al database di Configuration Manager informazioni dei file MIF, è necessario creare o importare informazioni relative alla classe per tali informazioni. Per altre informazioni, vedere le sezioni [Per aggiungere una nuova classe di inventario](#BKMK_Add) e [Per importare classi di inventario hardware](#BKMK_Import) in questo argomento.  

###  <a name="BKMK_NOIDMIF"></a> Per creare file NOIDMIF  
 I file NOIDMIF possono essere usati per aggiungere a un inventario hardware client informazioni che normalmente Configuration Manager non riesce a raccogliere. Questi file sono associati a dispositivi client specifici. Ad esempio, molte società etichettano ogni computer dell'organizzazione con un numero di asset e quindi li catalogano manualmente. Quando si crea un file NOIDMIF, è possibile aggiungere queste informazioni al database di Configuration Manager e usarle per le query e la creazione di report. Per informazioni sulla creazione di file NOIDMIF, vedere la documentazione di Configuration Manager SDK.  

> [!IMPORTANT]  
>  Quando si crea un file NOIDMIF, il file deve essere salvato in un formato con codifica ANSI. I file NOIDMIF salvati in formato con codifica UTF-8 non sono leggibili per Configuration Manager.  

 Dopo aver creato un file NOIDMIF, archiviarlo nella cartella *%Windir%***\CCM\Inventory\Noidmifs** di ogni client. Configuration Manager raccoglierà informazioni dai file NODMIF in questa cartella durante il successivo ciclo di inventario hardware pianificato.  

###  <a name="BKMK_IDMIF"></a> Per creare file IDMIF  
 I file IDMIF possono essere usati per aggiungere al database di Configuration Manager informazioni sugli asset di cui Configuration Manager non può normalmente eseguire l'inventario e che non sono associati a un dispositivo client specifico. È possibile, ad esempio, usare file IDMIF per raccogliere informazioni su proiettori, lettori DVD, fotocopiatrici o altri dispositivi che non contengono un client Configuration Manager. Per informazioni sulla creazione di file IDMIF, vedere la documentazione di Configuration Manager SDK.  

 Dopo aver creato un file IDMIF, archiviarlo nella cartella *%Windir%***\CCM\Inventory\Idmifs** dei computer client. Configuration Manager raccoglierà informazioni da questo file durante il successivo ciclo di inventario hardware pianificato. È necessario dichiarare nuove classi per le informazioni contenute nel file aggiungendo o importarli.  

> [!NOTE]
> I file MIF potrebbero contenere grandi quantità di dati e la raccolta di tali dati potrebbe influire negativamente sulle prestazioni del sito. Abilitare la raccolta di file MIF solo quando necessario e configurare l'opzione **Dimensioni massime file MIF personalizzate (KB)** nelle impostazioni relative all'inventario hardware. Per altre informazioni, vedere [Introduzione all'inventario hardware in System Center Configuration Manager](introduction-to-hardware-inventory.md).
