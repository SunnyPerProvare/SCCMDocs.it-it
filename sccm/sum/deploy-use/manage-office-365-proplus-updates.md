---
title: Gestire gli aggiornamenti di Office 365 ProPlus
titleSuffix: Configuration Manager
description: Configuration Manager sincronizza gli aggiornamenti del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito per rendere disponibili gli aggiornamenti per la distribuzione ai client.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/26/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 4fbbe4b6792c51cd7adeeae3a96f81927153362c
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gestire Office 365 ProPlus con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager consente di gestire le app di Office 365 ProPlus nei modi seguenti:

- [Dashboard di gestione client di Office 365](#office-365-client-management-dashboard): è possibile esaminare le informazioni sul client di Office 365 dal dashboard di gestione client di Office 365. A partire da Configuration Manager versione 1802, il dashboard di gestione client di Office 365 visualizza un elenco di dispositivi pertinenti quando vengono selezionate le sezioni del grafico. <!--1357281 -->

- [Distribuire app di Office 365](#deploy-office-365-apps): a partire dalla versione 1702, è possibile avviare il programma di installazione di Office 365 dal dashboard di Gestione client di Office 365. In questo modo, viene semplificata l'esperienza iniziale di installazione delle app di Office 365. La procedura guidata consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script con il contenuto.    

- [Distribuzione di aggiornamenti di Office 365](#deploy-office-365-updates): è possibile gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Quando pubblica un nuovo aggiornamento del client di Office 365 nella rete per la distribuzione di contenuti (CDN) di Office, Microsoft pubblica anche un pacchetto di aggiornamento per Windows Server Update Services (WSUS). Dopo che Configuration Manager ha sincronizzato l'aggiornamento del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito, l'aggiornamento è disponibile per la distribuzione ai client.    

- [Aggiungere lingue per i download di aggiornamento di Office 365](#add-languages-for-office-365-update-downloads): è possibile aggiungere il supporto per Configuration Manager per scaricare gli aggiornamenti in tutte le lingue supportate da Office 365. Non è necessario che Configuration Manager supporti la lingua se è supportata da Office 365. Prima di Configuration Manager versione 1610, è necessario scaricare e distribuire gli aggiornamenti nelle stesse lingue configurate nei client Office 365. 

- [Modificare il canale di aggiornamento](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): è possibile usare Criteri di gruppo per distribuire ai client di Office 365 la modifica del valore della chiave del Registro di sistema relativa al canale di aggiornamento.


## <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365  
Il dashboard di Gestione client di Office 365 presenta sotto forma di grafico le informazioni seguenti:

- Numero di client di Office 365
- Versioni dei client di Office 365
- Lingue dei client di Office 365
- Canali dei client di Office 365     
  Per altre informazioni, vedere [Panoramica dei canali di aggiornamento per Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).

Per visualizzare il dashboard di Gestione client di Office 365, nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**. Nella parte superiore del dashboard, usare l'impostazione a discesa **Raccolta** per filtrare i dati del dashboard in base ai membri di una raccolta specifica. A partire da Configuration Manager versione 1802, il dashboard di gestione client di Office 365 visualizza un elenco di dispositivi pertinenti quando vengono selezionate le sezioni del grafico.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Visualizzare dati nel dashboard di gestione client di Office 365
I dati visualizzati nel dashboard di gestione client di Office 365 provengono dall'inventario hardware. Abilitare l'inventario hardware e selezionare la classe **Configurazioni di Office 365 ProPlus** di tale inventario per visualizzare i dati nel dashboard. 
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Per visualizzare dati nel dashboard di gestione client di Office 365
1. Abilitare l'inventario hardware, se non è ancora stato fatto. Per altri dettagli, vedere [Configurare l'inventario hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. Nella console di Configuration Manager passare a **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  
3. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
4. Nel **Impostazioni Client predefinite** nella finestra di dialogo fare clic su **l'inventario Hardware**.  
5. Nel **le impostazioni del dispositivo** elenco, fare clic su **Imposta classi**.  
6. Nella finestra di dialogo **Classi di inventario hardware** selezionare **Office 365 ProPlus Configurations**.  
7.  Fare clic su **OK** per salvare le modifiche e chiudere il **classi di inventario Hardware** nella finestra di dialogo. <br/>Il dashboard di Gestione client di Office 365 inizia a visualizzare i dati in base all'inventario hardware.

## <a name="deploy-office-365-apps"></a>Distribuire app di Office 365  
A partire dalla versione 1702, per l'installazione iniziale delle app di Office 365 è possibile avviare il programma di installazione di Office 365 dal dashboard di Gestione client di Office 365. La procedura guidata consente di configurare le impostazioni di installazione di Office 365, scaricare file dalle reti di distribuzione del contenuto (CDN) e creare e distribuire un'applicazione script per i file. Finché Office 365 non viene installato nei client, gli aggiornamenti di Office 365 non sono applicabili.

Per le versioni di Configuration Manager precedenti, è necessario eseguire la procedura seguente per installare le app di Office 365 nei client per la prima volta:
- Scaricare lo Strumento di distribuzione di Office 365 (ODT)
- Scaricare i file di origine dell'installazione di Office 365, inclusi tutti i Language Pack necessari.
- Generare il file Configuration.xml che specifica la versione e il canale corretti di Office.
- Per eseguire l'installazione di app di Office 365 nei client, creare e distribuire un pacchetto legacy oppure un'applicazione script.

### <a name="requirements"></a>requisiti
- Il computer che esegue il programma di installazione di Office 365 deve avere accesso a Internet.  
- L'utente che esegue il programma di installazione di Office 365 deve avere accesso in **lettura** e **scrittura** al percorso dei contenuti specificato nella procedura guidata.
- Se si riceve l'errore di download 404, copiare i file seguenti nella cartella %temp% dell'utente:
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  


### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Per distribuire app di Office 365 ai client dal dashboard di gestione client di Office 365
1. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management** (Gestione Client di Office 365).
2. Fare clic su **Office 365 Installer** (Programma di installazione di Office 365) nel riquadro in alto a destro. Si apre l'installazione guidata dei client di Office 365.
3. Nella pagina **Impostazioni applicazione** specificare il nome e la descrizione per l'app, immettere il percorso di download per i file e quindi fare clic su **Avanti**. Il percorso deve essere specificato nel formato &#92;&#92;*server*&#92;*condivisione*.
4. Nella pagina **Importa le impostazioni del client** scegliere se importare le impostazioni del client di Office 365 da un file di configurazione XML esistente o se specificare manualmente le impostazioni. Al termine, fare clic su **Avanti**.  

    Se già si dispone di un file di configurazione, immettere il percorso del file e andare al passaggio 7. È necessario specificare il percorso nel formato &#92;&#92;*server*&#92;*condivisione*&#92;*nomefile*.XML.
    > [!IMPORTANT]    
    > Il file di configurazione XML deve contenere solo [lingue supportate dal client Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).

5. Nella pagina **Prodotti client** selezionare la famiglia di prodotti Office 365 in uso. Selezionare le applicazioni da includere. Selezionare i prodotti Office aggiuntivi che devono essere inclusi e fare clic su **Avanti**.
6. Nella pagina **Impostazioni client** scegliere le impostazioni da includere e fare clic su **Avanti**.
7. Nella pagina **Distribuzione** scegliere se distribuire l'applicazione, quindi fare clic su pagina **Avanti**. <br/>Se si sceglie di non distribuire il pacchetto nella procedura guidata, andare al passaggio 9.
8. Configurare il resto delle pagine della procedura guidata come si farebbe per la distribuzione di un'applicazione comune. Per i dettagli, vedere [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application) (Creare e distribuire un'applicazione).
9. Completare la procedura guidata.
10. È possibile distribuire o modificare l'applicazione da **Raccolta software** > **Panoramica** > **Gestione applicazioni** > **Applicazioni**.    

Dopo la creazione e la distribuzione di applicazioni di Office 365 mediante il programma di installazione di Office 365, Configuration Manager non gestirà gli aggiornamenti di Office per impostazione predefinita. Per consentire ai client Office 365 di ricevere gli aggiornamenti da Configuration Manager, vedere [Distribuire gli aggiornamenti di Office 365 con Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

>[!NOTE]
>Dopo la distribuzione delle applicazioni di Office 365, è possibile creare regole di distribuzione automatica per le applicazioni. Per creare una regola di distribuzione automatica per le app di Office 365, fare clic su **Crea una regola di distribuzione automatica** in Dashboard di gestione client di Office 365. Selezionare **Client Office 365** quando si sceglie il prodotto. Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## <a name="deploy-office-365-updates"></a>Distribuire aggiornamenti di Office 365
A partire da Configuration Manager versione 1706, gli aggiornamenti del client di Office 365 sono stati spostati nel nodo **Gestione client di Office 365** >**Aggiornamenti di Office 365**.  Lo spostamento non avrà impatto sulla configurazione delle regole di distribuzione automatica. 

Eseguire i passaggi seguenti per distribuire gli aggiornamenti di Office 365 con Configuration Manager:

1.  [Verificare i requisiti](https://technet.microsoft.com/library/mt628083.aspx) per l'uso di Configuration Manager per la gestione degli aggiornamenti del client di Office 365 nella sezione **Requisiti necessari per gestire gli aggiornamenti client di Office 365 usando Configuration Manager** dell'articolo.  

2.  [Configurare i punti di aggiornamento software](../get-started/configure-classifications-and-products.md) per sincronizzare gli aggiornamenti del client di Office 365. Impostare gli **aggiornamenti** per la classificazione e selezionare il **client di Office 365** per il prodotto. Sincronizzare gli aggiornamenti software dopo aver configurato i punti di aggiornamento software per l'uso della classificazione **Aggiornamenti**.
3.  Abilitare i client di Office 365 per la ricezione di aggiornamenti da Configuration Manager. Usare le impostazioni client di Configuration Manager o Criteri di gruppo per abilitare il client.   

    **Metodo 1**: a partire dalla versione 1606 di Configuration Manager è possibile usare l'impostazione del client di Configuration Manager per la gestione dell'agente client di Office 365. Dopo aver configurato questa impostazione e distribuito gli aggiornamenti di Office 365, l'agente client di Configuration Manager comunica con l'agente client di Office 365 al fine di scaricare gli aggiornamenti da un punto di distribuzione e installarli. Configuration Manager esegue l'inventario delle impostazioni client di Office 365 ProPlus.    

      1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**.  

      2.  Aprire le impostazioni del dispositivo appropriato per abilitare l'agente client. Per altre informazioni sulle impostazioni client predefinite e personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

      3.  Fare clic su **Aggiornamenti software** e selezionare **Sì** per l'impostazione **Abilita la gestione dell'agente client di Office 365**.  

    **Metodo 2**: [Abilitare i client di Office 365 per la ricezione di aggiornamenti](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) da Configuration Manager usando lo Strumento di distribuzione di Office o Criteri di gruppo.  

4. [Distribuire gli aggiornamenti di Office 365](deploy-software-updates.md) ai client.   

> [!Important]
> Prima di Configuration Manager versione 1610, è necessario scaricare e distribuire gli aggiornamenti nelle stesse lingue configurate nei client Office 365. Si supponga, ad esempio, di avere un client Office 365 configurato con le lingue en-us e de-de. Si supponga quindi di scaricare e distribuire nel server del sito solo il contenuto en-us di un aggiornamento di Office 365. Quando l'utente avvia l'installazione di questo aggiornamento da Software Center, l'operazione si blocca durante il download del contenuto per de-de.   

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Comportamento di riavvio e notifiche client per gli aggiornamenti di Office 365
Quando si distribuisce un aggiornamento a un client di Office 365, il comportamento di riavvio e le notifiche client sono diversi a seconda della versione di Configuration Manager. La tabella seguente fornisce informazioni sull'esperienza dell'utente finale quando il client riceve un aggiornamento di Office 365:

|Versione di Configuration Manager |Esperienza utente finale|  
|----------------|---------------------|
|Precedente alla 1610|Viene impostato un flag di riavvio e l'aggiornamento viene installato dopo il riavvio del computer.|
|1610|Le app di Office 365 vengono chiuse senza preavviso prima dell'installazione dell'aggiornamento|
|1610 con aggiornamento <br/>1702|Viene impostato un flag di riavvio e l'aggiornamento viene installato dopo il riavvio del computer.|
|1706|Il client riceve notifiche popup e in-app, nonché una finestra di dialogo con il conto alla rovescia prima dell'installazione dell'aggiornamento.|
|1802| Il client riceve notifiche popup e in-app, nonché una finestra di dialogo con il conto alla rovescia prima dell'installazione dell'aggiornamento. </br>Se sono in esecuzione applicazioni di Office 365 durante l'imposizione di un aggiornamento client di Office 365, le applicazioni di Office non verranno chiuse. Al contrario, l'installazione dell'aggiornamento restituisce una richiesta di riavvio del sistema <!--510006-->|

> [!Important]
>
>In Configuration Manager versione 1706 si noti quanto segue:
>
>- Viene visualizzata un'icona di notifica nell'area di notifica sulla barra delle applicazioni per le app obbligatorie la cui scadenza è entro 48 ore e per cui il contenuto dell'aggiornamento è stato scaricato. 
>- Viene visualizzata una finestra di dialogo con un conto alla rovescia per le app obbligatorie la cui scadenza è entro 7,5 ore e per cui l'aggiornamento è stato scaricato. L'utente può posticipare la finestra di dialogo del conto alla rovescia fino a tre volte prima della scadenza. Se viene posticipato, il conto alla rovescia viene visualizzato di nuovo dopo due ore. Se non viene posticipato, viene eseguito un conto alla rovescia di 30 minuti e, al termine, l'aggiornamento viene installato.
>- Potrebbe non venire visualizzata una notifica popup fino a quando l'utente non fa clic sull'icona nell'area di notifica. Inoltre, se nell'area di notifica c'è poco spazio, l'icona di notifica potrebbe non essere visibile a meno che l'utente non apra o espanda l'area. 
>- La finestra di dialogo di notifica e conto alla rovescia può essere avviata mentre l'utente non usa attivamente il dispositivo. Ad esempio, quando il dispositivo è bloccato durante la notte è possibile che le app di Office in esecuzione nel dispositivo vengano chiuse per installare l'aggiornamento. Prima di chiudere l'app, Office salva i relativi dati per evitarne la perdita. 
>- Se la scadenza è nel passato o se l'impostazione prevede l'avvio il prima possibile, è possibile che venga forzata la chiusura delle app di Office in esecuzione senza alcuna notifica. 
>- Se l'utente installa un aggiornamento di Office prima della scadenza, quando viene raggiunta la scadenza Configuration Manager verifica che l'aggiornamento sia installato. Se l'aggiornamento non viene rilevato nel dispositivo, viene installato. 
>- La barra di notifica in-app non viene visualizzata in un'app di Office che è in esecuzione prima del download dell'aggiornamento. Dopo il download dell'aggiornamento, la notifica in-app viene visualizzata solo per le app aperte successivamente.
>- Per gli aggiornamenti di Office attivati da un intervallo di servizio o pianificati per l'orario non di ufficio, è possibile che venga forzata la chiusura delle app di Office in esecuzione senza alcuna notifica. 



## <a name="add-languages-for-office-365-update-downloads"></a>Aggiungere lingue per i download degli aggiornamenti di Office 365
È possibile aggiungere il supporto per Configuration Manager per scaricare gli aggiornamenti in qualsiasi lingua supportata da Office 365, indipendentemente dal fatto che la lingua sia supportata in Configuration Manager.    

> [!IMPORTANT]  
> La configurazione di lingue aggiuntive per l'aggiornamento di Office 365 è un'impostazione a livello di sito. Dopo l'aggiunta delle lingue in base alla procedura seguente, tutti gli aggiornamenti di Office 365 vengono scaricati in queste lingue, oltre che nelle lingue selezionate nella pagina **Selezione lingua** del Download guidato degli aggiornamenti software o della Distribuzione guidata degli aggiornamenti software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Per aggiungere il supporto per il download degli aggiornamenti in altre lingue
Seguire questa procedura per il punto di aggiornamento software presso il sito di amministrazione centrale o presso il sito primario autonomo.
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
8. Aggiungere altre lingue alla proprietà **Value2** e fare clic su **Salva proprietà**. <br/> Ad esempio, pt-pt (per Portoghese - Portogallo), af-za (per Afrikaans - Sudafrica), nn-no (per Norvegese Nynorsk - Norvegia) e così via.  
![Aggiungere lingue in Editor di proprietà](..\media\4-props.png)  
9. Fare clic su **Chiudi**, **Chiudi**, **Salva proprietà** e **Salva oggetto** (se si fa clic su **Chiudi**, i valori vengono ignorati). Fare clic su **Chiudi** e quindi su **Esci** per chiudere il tester di Strumentazione gestione Windows.
10. Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Office 365 Client Management (Gestione client di Office 365)** > **Office 365 Updates (Aggiornamenti di Office 365)**.
11. Ora gli aggiornamenti di Office 365 vengono scaricati nelle lingue selezionate nella procedura guidata e configurati in questa procedura. Per verificare che gli aggiornamenti vengano effettivamente scaricati nelle lingue corrette, passare all'origine pacchetto per gli aggiornamenti e cercare i file con il codice lingua nel nome.  
![Nomi di file con altre lingue](..\media\5-verification.png)

## <a name="updating-office-365-during-task-sequences-when-office-365-is-installed-in-the-base-image"></a>Aggiornamento di Office 365 durante le sequenze di attività quando Office 365 è installato nell'immagine di base
Quando si installa un sistema operativo in cui Office 365 è già installato nell'immagine, è possibile che il valore della chiave del Registro di sistema per il canale aggiornamento sia il percorso di installazione originale. In questo caso, l'analisi aggiornamenti non visualizzerà alcun aggiornamento del client di Office 365 come applicabile. Esiste un'attività pianificata degli aggiornamenti automatici di Office che viene eseguita più volte a settimana. Dopo l'esecuzione di questa attività, il canale di aggiornamento punterà all'URL configurato per la rete di distribuzione dei contenuti di Office e l'analisi visualizzerà quindi questi aggiornamenti come applicabili. <!--510452-->

Per impostare il canale di aggiornamento in modo da rilevare gli aggiornamenti applicabili, seguire questa procedura:
1. In un computer con la stessa versione di Office 365 di quella contenuta nell'immagine di base del sistema operativo aprire l'Utilità di pianificazione (taskschd.msc) e individuare l'attività degli aggiornamenti automatici di Office 365. Questa attività si trova in genere in **Libreria Utilità di pianificazione** >**Microsoft**>**Office**.
2. Fare clic con il pulsante destro del mouse sull'attività e selezionare **Proprietà**.
3. Passare alla scheda **Azioni** e fare clic su **Modifica**. Copiare il comando e gli eventuali argomenti. 
4. Nella console di Configuration Manager modificare la sequenza di attività.
5. Aggiungere un nuovo passaggio **Esegui riga di comando** prima del passaggio **Installa aggiornamenti** nella sequenza di attività. 
6. Inserire il comando e gli argomenti raccolti dall'attività pianificata degli aggiornamenti automatici di Office. 
7. Fare clic su **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Modificare il canale di aggiornamento dopo aver abilitato i client di Office 365 alla ricezione degli aggiornamenti da Configuration Manager
Per modificare il canale di aggiornamento dopo aver abilitato i client di Office 365 alla ricezione degli aggiornamenti da Configuration Manager, usare Criteri di gruppo per distribuire una modifica del valore della chiave del Registro di sistema ai client di Office 365. Modificare la chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** in modo che usi uno dei valori seguenti:

- Canale mensile <br/>
<i>( in precedenza Current Channel)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canale semestrale <br/>
<i>( in precedenza Deferred Channel</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Canale mensile (mirato)<Br/>
 <i>(in precedenza First Release per Current Channel</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Canale semestrale (mirato) <br/>
<i>(in precedenza First Release per Deferred Channel</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
<!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US>


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
