---
title: Gestire gli aggiornamenti di Office 365 ProPlus | Microsoft Docs
description: Configuration Manager sincronizza gli aggiornamenti del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito per rendere disponibili gli aggiornamenti per la distribuzione ai client.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 016580dc6ee3c5268833db941d42416a976d201c
ms.lasthandoff: 03/27/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gestire Office 365 ProPlus con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager sincronizza gli aggiornamenti client di Office 365 e li rende disponibili per la distribuzione ai client con Office 365 installato. A partire da Configuration Manager versione 1610, è possibile esaminare le informazioni sul client di Office 365 dal dashboard di gestione client di Office 365.

A partire dalla versione 1602, Configuration Manager consente di gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Quando pubblica un nuovo aggiornamento del client di Office 365 nella rete per la distribuzione di contenuti (CDN) di Office, Microsoft pubblica anche un pacchetto di aggiornamento per Windows Server Update Services (WSUS). Dopo che Configuration Manager ha sincronizzato l'aggiornamento del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito, l'aggiornamento è disponibile per la distribuzione ai client.

A partire dalla versione 1702, è possibile avviare il programma di installazione di Office 365 dal dashboard di gestione client di Office 365 per semplificare l'esperienza iniziale di installazione delle app di Office 365. La procedura guidata consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script con il contenuto.

## <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365  
A partire da Configuration Manager versione 1610, il dashboard di gestione client di Office 365 è disponibile nella console di Configuration Manager. Per visualizzare il dashboard, passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**.

Nel dashboard vengono visualizzati i grafici per:

- Numero di client di Office 365
- Versioni dei client di Office 365
- Lingue dei client di Office 365
- Canali dei client di Office 365     
Per altre informazioni, vedere [Panoramica dei canali di aggiornamento per Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

Nella parte superiore del dashboard, usare l'impostazione a discesa **Raccolta** per filtrare i dati del dashboard in base ai membri di una raccolta specifica.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Visualizzare dati nel dashboard di gestione client di Office 365
I dati visualizzati nel dashboard di gestione client di Office 365 provengono dall'inventario hardware. L'inventario hardware deve essere abilitato ed è necessario selezionare la classe dell'inventario hardware **Office 365 ProPlus Configurations** prima che i dati vengano visualizzati nel dashboard.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Per visualizzare dati nel dashboard di gestione client di Office 365
1. Abilitare l'inventario hardware, se non è ancora stato fatto. Per altri dettagli, vedere [Configurare l'inventario hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. Nella console di Configuration Manager passare a **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  
3. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
4. Nel **Impostazioni Client predefinite** nella finestra di dialogo fare clic su **l'inventario Hardware**.  
5. Nel **le impostazioni del dispositivo** elenco, fare clic su **Imposta classi**.  
6. Nella finestra di dialogo **Classi di inventario hardware** selezionare **Office 365 ProPlus Configurations**.  
7.  Fare clic su **OK** per salvare le modifiche e chiudere il **classi di inventario Hardware** nella finestra di dialogo.  
Viene avviato il dashboard di gestione client di Office 365 che visualizza i dati in base all'inventario hardware.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Distribuire gli aggiornamenti di Office 365 con Configuration Manager
Eseguire i passaggi seguenti per distribuire gli aggiornamenti di Office 365 con Configuration Manager:

1.  [Verificare i requisiti](https://technet.microsoft.com/library/mt628083.aspx) per l'uso di Configuration Manager per la gestione degli aggiornamenti del client di Office 365 nella sezione **Requisiti necessari per gestire gli aggiornamenti client di Office 365 utilizzando Configuration Manager** dell'argomento.  

2.  [Configurare i punti di aggiornamento software](../get-started/configure-classifications-and-products.md) per sincronizzare gli aggiornamenti del client di Office 365. Impostare gli **aggiornamenti** per la classificazione e selezionare il **client di Office 365** per il prodotto. Potrebbe essere necessario sincronizzare gli aggiornamenti software almeno una volta prima che il client di Office 365 sia disponibile per la selezione. È necessario sincronizzare gli aggiornamenti software dopo aver configurato i punti di aggiornamento software per l'uso della classificazione **Aggiornamenti**.
3.  Abilitare i client di Office 365 per la ricezione di aggiornamenti da Configuration Manager. È possibile eseguire questa operazione usando le impostazioni client di Configuration Manager o i criteri di gruppo. Per abilitare il client usare uno dei metodi seguenti:  
    - Metodo 1: a partire dalla versione 1606 di Configuration Manager è possibile usare l'impostazione client di Configuration Manager per gestire l'agente client di Office 365. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager comunica con l'agente client di Office 365 al fine di scaricare gli aggiornamenti di Office 365 da un punto di distribuzione e installarli. Configuration Manager esegue l'inventario delle impostazioni client di Office 365 ProPlus.
      1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**.  

      2.  Aprire le impostazioni del dispositivo appropriato per abilitare l'agente client. Per altre informazioni sulle impostazioni client predefinite e personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

      3.  Fare clic su **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Abilita la gestione dell'agente client di Office 365**.  

    - Metodo 2: [Abilitare i client di Office 365 per la ricezione di aggiornamenti](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) da Configuration Manager usando lo strumento di distribuzione di Office o i criteri di gruppo.  

4. [Distribuire gli aggiornamenti di Office 365](deploy-software-updates.md) ai client.   

> [!Important]
> Se si dispone di un client Office 365 con più lingue e si scaricano gli aggiornamenti per un numero minore di lingue, l'installazione di tali aggiornamenti avrà esito negativo. Si supponga, ad esempio, di avere un client Office 365 con le lingue en-us e de-de. Si supponga quindi di scaricare e distribuire nel server del sito solo il contenuto en-us di un aggiornamento di Office 365. Quando l'utente avvia l'installazione di questo aggiornamento da Software Center, l'operazione si blocca durante il download del contenuto. È necessario scaricare e distribuire gli aggiornamenti nelle stesse lingue dei client Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Aggiungere altre lingue per i download degli aggiornamenti di Office 365
A partire da Configuration Manager versione 1610, è possibile aggiungere il supporto per Configuration Manager per scaricare gli aggiornamenti in qualsiasi lingua supportata da Office 365, indipendentemente dal fatto che tali lingue siano supportate in Configuration Manager.
> [!IMPORTANT]  
> La configurazione di lingue aggiuntive per l'aggiornamento di Office 365 è un'impostazione a livello di sito. Dopo l'aggiunta delle lingue in base alla procedura seguente, tutti gli aggiornamenti di Office 365 verranno scaricati in tali lingue, oltre che nelle lingue selezionate nella pagina Selezione lingua del Download guidato degli aggiornamenti software o della Distribuzione guidata degli aggiornamenti software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Per aggiungere il supporto per il download degli aggiornamenti in altre lingue
Seguire questa procedura nel sito di amministrazione centrale, o in un sito primario autonomo, in cui è installato il ruolo del sistema del sito del punto di aggiornamento software.
1. Da un prompt dei comandi digitare *wbemtest* come utente amministratore per aprire il Tester di Strumentazione gestione Windows.
2. Fare clic su **Connetti** e quindi digitare *root\sms\site_&lt;CodiceSito&gt;*.
3. Fare clic su **Query** e quindi eseguire la query seguente: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![query WMI](..\media\1-wmiquery.png)
4. Nel riquadro dei risultati fare doppio clic sull'oggetto con il codice corrispondente al sito di amministrazione centrale o al sito primario autonomo.
5. Selezionare la proprietà **Props**, fare clic su **Modifica proprietà** e quindi su **Visualizza ogg. incorporati**.
![Editor di proprietà](..\media\2-propeditor.png)
6. A partire dal primo risultato della query, aprire tutti gli oggetti fino a individuare quello con **AdditionalUpdateLanguagesForO365** per la proprietà **PropertyName**.
7. Selezionare **Value2** e fare clic su **Modifica proprietà**.  
![Modificare la proprietà Value2](..\media\3-queryresult.png)
8. Aggiungere altre lingue alla proprietà **Value2** e fare clic su **Salva proprietà**.  
Ad esempio, pt-pt (per Portoghese - Portogallo), af-za (per Afrikaans - Sudafrica), nn-no (per Norvegese Nynorsk - Norvegia) e così via.  
![Aggiungere lingue in Editor di proprietà](..\media\4-props.png)  
9. Fare clic su **Chiudi**, fare di nuovo clic su **Chiudi**, quindi fare clic su **Salva proprietà**, su **Salva oggetto** (se si fa clic su **Chiudi** qui, i valori verranno rimossi), su **Chiudi** e infine su **Esci** per chiudere il Tester di Strumentazione gestione Windows.
10. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management (Gestione client di Office 365)** > **Office 365 Updates (Aggiornamenti di Office 365)**.
11. Gli aggiornamenti di Office 365 verranno scaricati nella lingua selezionata nella procedura guidata e nelle lingue configurate in questa procedura. Per verificare che gli aggiornamenti vengano effettivamente scaricati in tali lingue, passare all'origine pacchetto per gli aggiornamenti e cercare i file con il codice lingua nel nome.  
![Nomi di file con altre lingue](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Modificare il canale di aggiornamento dopo aver abilitato i client di Office 365 alla ricezione degli aggiornamenti da Configuration Manager
Per modificare il canale di aggiornamento dopo aver abilitato i client di Office 365 alla ricezione degli aggiornamenti da Configuration Manager, è possibile usare Criteri di gruppo per distribuire una modifica del valore della chiave del Registro di sistema ai client di Office 365. Modificare la chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** in modo che usi uno dei valori seguenti:

- Current Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release per Current Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release per Deferred Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Distribuire app di Office 365  
A partire dalla versione 1702, è possibile avviare il programma di installazione di Office 365 dal dashboard di gestione client di Office 365 per semplificare l'esperienza iniziale di installazione delle app di Office 365. La procedura guidata consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script per i file.

Questo è particolarmente utile perché gli aggiornamenti di Office 365 non sono applicabili per i client senza Office 365 installato. Nelle versioni precedenti la 1702, per installare per la prima volta app di Office 365 nei computer client è necessario scaricare manualmente Office 365 Deployment Tool (ODT) e i file di origine dell'installazione di Office 365, inclusi tutti i Language Pack necessari, e generare il file Configuration.xml che specifica il canale e la versione di Office corretti. Per eseguire l'installazione di app di Office 365 nei client, è quindi necessario creare e distribuire un pacchetto legacy oppure un'applicazione script.

> [!NOTE]
> - Il computer che esegue il programma di installazione di Office 365 deve avere accesso a Internet.  
> - L'utente che esegue il programma di installazione di Office 365 deve avere accesso in **lettura** e **scrittura** al percorso dei contenuti specificato nella procedura guidata.
> - Se si riceve l'errore di download 404, copiare i file seguenti nella cartella %temp% dell'utente:
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Dopo la creazione e la distribuzione di applicazioni di Office 365 mediante il programma di installazione di Office 365, Configuration Manager non gestirà gli aggiornamenti di Office per impostazione predefinita. Per consentire ai client Office 365 di ricevere gli aggiornamenti da Configuration Manager, vedere [Distribuire gli aggiornamenti di Office 365 con Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Per distribuire app di Office 365 ai client dal dashboard di gestione client di Office 365
1. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
2. Fare clic su **Office 365 Installer** (Programma di installazione di Office 365) nel riquadro in alto a destro. Si apre l'installazione guidata dei client di Office 365.
3. Nella pagina **Impostazioni applicazione** specificare il nome e la descrizione per l'app, immettere il percorso di download per i file e quindi fare clic su **Avanti**. Si noti che è necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*share*.
4. Nella pagina **Import Client Settings** (Importa impostazioni client) scegliere se importare le impostazioni del client di Office 365 da un file di configurazione XML esistente o se specificare manualmente le impostazioni, quindi fare clic su **Avanti**.  

    Se già si dispone di un file di configurazione, immettere il percorso del file e andare al passaggio 7. Si noti che è necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*share*&#92;*nomedelfile*.XML.
5. Nella pagina **Client Products** (Prodotti client) selezionare la suite Office 365 in uso, selezionare le applicazioni da includere, selezionare eventuali prodotti aggiuntivi di Office da includere e quindi fare clic su **Avanti**.
6. Nella pagina **Impostazioni client** scegliere le impostazioni da includere e fare clic su **Avanti**.
7. Nella pagina **Distribuzione** scegliere se distribuire l'applicazione, quindi fare clic su pagina **Avanti**.  
Se si sceglie di non distribuire il pacchetto nella procedura guidata, andare al passaggio 9.
8. Configurare il resto delle pagine della procedura guidata come si farebbe per la distribuzione di un'applicazione comune. Per i dettagli, vedere [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application) (Creare e distribuire un'applicazione).
9. Completare la procedura guidata.
10. È possibile distribuire o modificare l'applicazione esattamente come si farebbe con qualsiasi altra applicazione in Configuration Manager da **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**.   

> [!IMPORTANT]
> L'app di Office 365 creata e distribuita mediante la Creazione guidata dell'applicazione di Office 365 in Configuration Manager non viene gestita automaticamente da Configuration Manager fino a quando non si abilita l'impostazione dell'agente client degli aggiornamenti software **Enable management of the Office 365 Client Again** (Abilita di nuovo la gestione del client Office 365). Per altre informazioni, vedere [Informazioni sulle impostazioni client](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Dopo la distribuzione delle applicazioni di Office 365, è possibile creare regole di distribuzione automatica per le applicazioni. Per creare una regola di distribuzione automatica per le applicazioni di Office 365, fare clic su **Crea un ADR** nel dashboard di gestione client di Office 365 e selezionare **Office 365 Client** quando si sceglie il prodotto. Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

