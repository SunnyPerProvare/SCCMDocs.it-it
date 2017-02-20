---
title: Gestire gli aggiornamenti di Office 365 ProPlus | Microsoft Docs
description: Configuration Manager sincronizza gli aggiornamenti del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito per rendere disponibili gli aggiornamenti per la distribuzione ai client.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 02/03/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 5ab49481a78eda044350addab86ee6f8ef1c0946
ms.openlocfilehash: fe8bf45970e34af0795a5a9a4c3aa985e446784d

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Gestire gli aggiornamenti di Office 365 ProPlus con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1602, Configuration Manager consente di gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Quando pubblica un nuovo aggiornamento del client di Office 365 nella rete per la distribuzione di contenuti (CDN) di Office, Microsoft pubblica anche un pacchetto di aggiornamento per Windows Server Update Services (WSUS). Dopo che Configuration Manager ha sincronizzato l'aggiornamento del client di Office 365 dal catalogo di Windows Server Update Services nel server del sito, l'aggiornamento è disponibile per la distribuzione ai client.

## <a name="office-365-client-management-dashboard"></a>Dashboard di Gestione client di Office 365  
A partire da Configuration Manager versione 1610, il dashboard di gestione client di Office 365 è disponibile nella console di Configuration Manager. Per visualizzare il dashboard, passare a **Raccolta software** > **Panoramica** > **Gestione client di Office 365**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

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

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

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

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Feb17_HO1-->


