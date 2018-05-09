---
title: Sincronizzare i dati in OMS
titleSuffix: Configuration Manager
description: Sincronizzazione dei dati da System Center Configuration Manager a Microsoft Operations Management Suite.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a01c5534367ad66314afc563cff41adeb2b88dc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1258052-->
È possibile usare la **Procedura guidata Servizi di Azure** per configurare la connessione da Configuration Manager al servizio cloud Operations Management Suite (OMS). A partire dalla versione 1706, la procedura guidata sostituisce i precedenti flussi di lavoro per la configurazione della connessione. Per le versioni precedenti, vedere [Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite (versione 1702 e precedenti)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   La procedura guidata viene usata per configurare i servizi cloud per Configuration Manager, come ad esempio OMS, Microsoft Store per le aziende e Azure Active Directory (Azure AD).  

-   Configuration Manager si connette a OMS per funzionalità quali [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) o [Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade/upgrade-analytics).


> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## <a name="prerequisites-for-the-oms-connector"></a>Prerequisiti per il connettore OMS
I prerequisiti per configurare una connessione a OMS sono identici a quelli [indicati per la versione Current Branch 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Tali informazioni viene ripetute di seguito:  

-   Prima di installare OMS Connector in Configuration Manager, è necessario fornire a Configuration Manager le autorizzazioni per OMS. In particolare, è necessario concedere l'*accesso di tipo Collaboratore* al *gruppo di risorse* di Azure che contiene l'area di lavoro OMS Log Analytics. Le procedure per eseguire questa operazione sono documentate nel contenuto di Log Analytics. Vedere [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) nella documentazione relativa a OMS.

-   OMS Connector deve essere installato nel computer che ospita un [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) che si trova in [modalità online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Nel punto di connessione del servizio, insieme a OMS Connector è necessario installare Microsoft Monitoring Agent per OMS. L'agente e OMS Connector devono essere configurati per l'uso della stessa **area di lavoro OMS**. Per installare l'agente, vedere [Scaricare e installare l'agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) nella documentazione relativa a OMS.
-   Dopo aver installato l'agente e OMS Connector, è necessario configurare OMS per l'uso dei dati di Configuration Manager. A questo scopo, [importare le raccolte di Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections) nel portale di OMS.

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Usare la Procedura guidata Servizi di Azure per configurare la connessione a OMS

1.  Nella console andare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure**. Scegliere **Configura i servizi di Azure** dalla scheda **Home** della barra multifunzione per avviare la **procedura guidata per i servizi di Azure**.

2.  Nella pagina **Servizi di Azure** selezionare il servizio cloud Operations Management Suite. Specificare un nome descrittivo per **Nome del servizio Azure** e una descrizione facoltativa, quindi fare clic su **Avanti**.

3.  Nella pagina **App** specificare l'ambiente Azure (la versione Technical Preview supporta solo cloud pubblici). Fare clic su **Sfoglia** per aprire la finestra dell'app server.

4.  Selezionare un'app Web:

    -   **Importa**: per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant. Indicare l'ID tenant, l'ID client e la chiave privata per l'app Web di Azure che si vuole usare con Configuration Manager. Dopo aver fatto clic su **Verifica** per verificare le informazioni, fare clic su **OK** per continuare.   

    > [!NOTE]   
    > Quando si configura OMS con questa versione di anteprima, OMS supporta solo la funzione di *importazione*  di un'app Web. La creazione di una nuova app Web non è supportata. Analogamente, non è possibile usare di nuovo un'app esistente per OMS.

5.  Se tutte le altre procedure sono state eseguite correttamente, le informazioni della schermata di **configurazione della connessione OMS** vengono automaticamente visualizzate. Le informazioni relative alle impostazioni di connessione vengono visualizzate in **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.

6.  La procedura guidata esegue la connessione al servizio OMS usando le informazioni immesse dall'utente. Selezionare le raccolte di dispositivi da sincronizzare con OMS e quindi fare clic su **Aggiungi**.

7.  Verificare le impostazioni di connessione nella schermata **Riepilogo** e selezionare **Avanti**. Nella schermata **Avanzamento** viene visualizzato lo stato della connessione e quindi **Completata**.

8.  Al termine della procedura guidata, nella console di Configuration Manager viene indicato che **Operation Management Suite** è stato configurato come **Tipo di servizio cloud**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite (versione 1702 e precedenti)


*Si applica a: System Center Configuration Manager (versione 1702 e precedenti)*

È possibile usare Microsoft Operations Management Suite (OMS) Connector per sincronizzare i dati, ad esempio le raccolte, da System Center Configuration Manager a OMS Log Analytics in Microsoft Azure. Il connettore rende visibili in OMS i dati della distribuzione di Configuration Manager.
> [!TIP]
> A partire da Configuration Manager 1802, OMS Connector non è più una funzionalità di versione non definitiva. Per altre informazioni, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/pre-release-features).

A partire dalla versione 1702, è possibile usare OMS Connector per la connessione a un'area di lavoro OMS che si trova sul cloud di Microsoft Azure per enti pubblici. A questo scopo, prima di installare OMS Connector è necessario modificare un file di configurazione. Vedere la sezione [Usare OMS Connector con il cloud di Azure per enti pubblici](#fairfaxconfig) di questo articolo.

### <a name="prerequisites"></a>Prerequisiti
- Prima di installare OMS Connector in Configuration Manager, è necessario fornire a Configuration Manager le autorizzazioni per OMS. In particolare, è necessario concedere l'*accesso di tipo Collaboratore* al *gruppo di risorse* di Azure che contiene l'area di lavoro OMS Log Analytics. Le procedure per eseguire questa operazione sono documentate nel contenuto di Log Analytics. Vedere [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) nella documentazione relativa a OMS.

- OMS Connector deve essere installato nel computer che ospita un [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) che si trova in [modalità online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Se OMS è stato connesso a un sito primario autonomo e si pianifica di aggiungere all'ambiente un sito di amministrazione centrale, è necessario eliminare la connessione corrente e quindi riconfigurare il connettore nel nuovo sito di amministrazione centrale.

- Nel punto di connessione del servizio, insieme a OMS Connector è necessario installare Microsoft Monitoring Agent per OMS.  L'agente e OMS Connector devono essere configurati per l'uso della stessa **area di lavoro OMS**. Per installare l'agente, vedere [Scaricare e installare l'agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) nella documentazione relativa a OMS.

- Dopo aver installato l'agente e OMS Connector, è necessario configurare OMS per l'uso dei dati di Configuration Manager.  A questo scopo, [importare le raccolte di Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections) nel portale di OMS.



### <a name="install-the-oms-connector"></a>Installare OMS Connector  
1. Nella console di Configuration Manager configurare la [gerarchia per l'uso di funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features) e quindi abilitare l'uso di OMS Connector.  
0
2. Passare quindi ad **Amministrazione** > **Servizi cloud** > **OMS Connector**. Sulla barra multifunzione fare clic su "Creare una connessione a Operations Management Suite". Questo passaggio apre la **Connessione guidata a Operations Management Suite**. Selezionare **Avanti**.  


3.  Nella pagina **Generale** verificare di avere le informazioni seguenti e quindi scegliere **Avanti**.  
  - Configuration Manager registrato come uno strumento di gestione "Applicazione Web e/o API Web" e di avere [l'ID client della registrazione](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Una chiave client creata per lo strumento di gestione registrato in Azure Active Directory.  

  - Nel portale di Azure fornire all'app Web registrata l'autorizzazione per accedere a OMS, come descritto in [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  Nella pagina di **Azure Active Directory** configurare le impostazioni di connessione a OMS specificando **Tenant**, **ID client** e **Chiave privata del client**, quindi scegliere **Avanti**.  

5.  Nella pagina **OMS Connection Configuration** (Configurazione connessione OMS) specificare le impostazioni di connessione in **Sottoscrizione di Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.  L'area di lavoro deve corrispondere a quella configurata per Microsoft Management Agent, installato nel punto di connessione del servizio.  

6.  Verificare le impostazioni di connessione nella pagina **Riepilogo** e scegliere **Avanti**. Nella pagina **Avanzamento** verrà visualizzato lo stato della connessione, quindi **Operazione completata**.

Dopo aver collegato Configuration Manager a OMS, è possibile aggiungere o rimuovere raccolte e visualizzare le proprietà della connessione OMS.

### <a name="verify-the-oms-connector-properties"></a>Verificare le proprietà di OMS Connector
1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Servizi cloud** e quindi selezionare **OMS Connector** per aprire la pagina **Connessione OMS**.
2.  In questa pagina sono disponibili due schede:
  - **Azure Active Directory:** 
  
     Questa scheda include le informazioni relative a **Tenant**, **ID client** e **Scadenza della chiave privata del client** e consente inoltre di verificare se la chiave privata del client è scaduta.

  - **Proprietà della connessione OMS:**  

     Questa scheda include le informazioni relative a **Sottoscrizione di Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**, nonché un elenco di **raccolte di dispositivi per cui OMS può recuperare i dati**. Usare i pulsanti **Aggiungi** e **Rimuovi** per modificare le raccolte consentite.

### <a name="fairfaxconfig"> </a> Usare OMS Connector con il cloud di Azure per enti pubblici


1.  In un computer in cui è installata la console di Configuration Manager modificare il file di configurazione seguente in modo che punti al cloud per enti pubblici:  ***&lt;percorso installazione CM>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Modifiche:**

    Modificare il valore del nome dell'impostazione *FairFaxArmResourceID* in modo che sia uguale a "https://management.usgovcloudapi.net/"

   - **Originale:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Modificato:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Modificare il valore del nome dell'impostazione *FairFaxAuthorityResource* in modo che sia uguale a "https://login.microsoftonline.us/"

  - **Originale:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Modificato:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.us/&lt;/value>

2.  Dopo aver salvato il file con le due modifiche, riavviare la console di Configuration Manager nello stesso computer e quindi usare la console per installare il connettore OMS. Per installare il connettore, usare le informazioni in [Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) e selezionare l'**Area di lavoro di Operations Management Suite** che si trova nel cloud di Microsoft Azure per enti pubblici.

3.  Dopo aver installato il connettore OMS, la connessione al cloud per enti pubblici sarà disponibile quando si usa qualsiasi console che si connette al sito.
