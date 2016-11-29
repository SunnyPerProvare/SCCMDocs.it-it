---
title: Installare punti di distribuzione basati sul cloud | System Center Configuration Manager
description: Informazioni su cosa occorre fare per iniziare a usare punti di distribuzione basati sul cloud in Microsoft Azure.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1dafd0b61a61a0fd2f2c597b89dea7cd6ac715a8

---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Installare punti di distribuzione basati sul cloud in Microsoft Azure per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile installare punti di distribuzione basati sul cloud in Microsoft Azure per System Center Configuration Manager. Se non si ha familiarità con i punti di distribuzione basati sul cloud, vedere [Usare un punto di distribuzione basato sul cloud](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) prima di continuare.

 Prima di iniziare l'installazione, assicurarsi di disporre dei file di certificato richiesti:  

-   Un certificato di gestione Microsoft Azure esportato in un file CER e in un file PFX.  

-   Un certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager esportato in un file con estensione pfx.  

    > [!TIP]
    >   Per altre informazioni su questi certificati, vedere la sezione relativa ai punti di distribuzione basati sul cloud nell'argomento [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager). Per una distribuzione di esempio per un certificato di servizio del punto di distribuzione, vedere la sezione *Deploying the Custom Web Server Certificate for Cloud-Based Distribution Points* (Distribuzione del certificato di servizio per i punti di distribuzione basati sul cloud) nell'argomento [Step-by-Step Example Deployment of the PKI Certificates for Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) (Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008).  


 Al termine dell'installazione del punto di distribuzione basato sul cloud, Microsoft Azure genera automaticamente un GUID per il servizio e lo aggiunge al suffisso DNS di **cloudapp.net**. Se si usa questo GUID, è necessario configurare DNS con un alias DNS (record CNAME) per effettuare il mapping del nome servizio definito nel certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager al GUID generato automaticamente.  

 Se si utilizza un server Web proxy, potrebbe essere necessario configurare le impostazioni proxy per abilitare la comunicazione con il servizio cloud che ospita il punto di distribuzione.  

##  <a name="a-namebkmkconfigwindowsazureandinstalldpa-configure-microsoft-azure-and-install-cloud-based-distribution-points"></a><a name="BKMK_ConfigWindowsAzureandInstallDP"></a>Configurare Microsoft Azure e installare punti di distribuzione basati sul cloud  
 Usare le procedure seguenti per configurare Microsoft Azure per il supporto dei punti di distribuzione, quindi installare il punto di distribuzione basato sul cloud in Configuration Manager.  

#### <a name="to-configure-a-cloud-service-in-microsoft-azure-for-a-distribution-point"></a>Per configurare un servizio cloud in Microsoft Azure per un punto di distribuzione  

1.  Aprire un Web browser e passare al portale di gestione di Microsoft Azure all'indirizzo https://manage.windowsazure.com e accedere all'account Microsoft Azure.  

2.  Fare clic su **Servizi ospitati, account di archiviazione e CDN** e quindi selezionare **Certificati di gestione**.  

3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione, quindi selezionare **Aggiungi certificato**.  

4.  Relativamente a **File di certificato**, specificare il file CER contenente il certificato di gestione di Microsoft Azure esportato da usare per questo servizio cloud, quindi fare clic su **OK**.  

 Quando il certificato di gestione viene caricato in Microsoft Azure è possibile installare un punto di distribuzione basato sul cloud.  

#### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Per installare un punto di distribuzione basato sul cloud per Configuration Manager  

1.  Completare i passaggi della procedura precedente per configurare un servizio cloud in Microsoft Azure con un certificato di gestione.  

2.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager, espandere **Servizi cloud**, selezionare **Punti di distribuzione del cloud** e quindi nella scheda **Home** fare clic su** Crea punto di distribuzione cloud**.  

3.  Nella pagina **Generale** della procedura guidata per la crezione del punto di distribuzione cloud, configurare quanto segue:  

    -   Specificare l' **ID sottoscrizione** per l'account Microsoft Azure.  

        > [!TIP]  
        >  È possibile trovare l'ID sottoscrizione di Microsoft Azure nel portale di gestione di Microsoft Azure.  

    -   Specificare il **Certificato di gestione**. Fare clic su **Sfoglia** per specificare il file PFX contenente il certificato di gestione di Microsoft Azure esportato, quindi immettere la password per il certificato. Facoltativamente, è possibile specificare un file .publishsettings versione 1 di Microsoft Azure SDK 1.7  

4.  Fare clic su **Avanti**in modo che Configuration Manager si connetta a Microsoft Azure per la convalida del certificato di gestione.  

5.  Nella pagina **Impostazioni** specificare le seguenti configurazioni e quindi fare clic su **Avanti**:  

    -   Relativamente ad **Area**, selezionare l'area di Microsoft Azure in cui si desidera creare il servizio cloud che ospita il punto di distribuzione.  

    -   Per **File di certificato** specificare il file PFX contenente il certificato di servizio del punto di distribuzione basato sul cloud esportato di Configuration Manager, quindi immettere la password.  

        > [!NOTE]  
        >  La casella **FQDN servizio** viene compilata automaticamente con il nome oggetto del certificato e, nella maggior parte dei casi, non è necessario modificarla. L'eccezione si verifica in caso di utilizzo di un certificato con caratteri jolly in un ambiente di testing, in cui il nome host non è specificato e più computer con lo stesso suffisso DNS possono utilizzare il certificato. In questo scenario, l'oggetto del certificato contiene un valore simile a **CN=\*.contoso.com** e Configuration Manager visualizza un messaggio per indicare che è necessario specificare l'FQDN corretto. Fare clic su **OK** per chiudere il messaggio, quindi immettere un nome specifico prima del suffisso DNS per fornire un FQDN completo. È ad esempio possibile aggiungere **clouddp1** per specificare l'FQDN servizio completo di **clouddp1.contoso.com**. L'FQDN del servizio deve essere univoco nel dominio e non corrispondere a qualsiasi dispositivo aggiunto al dominio.  
        >   
        >  I certificati con caratteri jolly sono supportati solo per ambienti di testing.  

6.  Nella pagina **Avvisi** configurare le quote di archiviazione, le quote di trasferimento e la percentuale delle quote necessaria affinché Configuration Manager generi gli avvisi, quindi fare clic su **Avanti**.  

7.  Completare la procedura guidata.  

 Questa procedura guidata consente di creare un nuovo servizio ospitato per il punto di distribuzione basato sul cloud. Al termine della procedura guidata è possibile monitorare lo stato dell'installazione del punto di distribuzione basato sul cloud nella console di Configuration Manager oppure monitorando il file **CloudMgr.log** nel server del sito primario. È anche possibile monitorare il provisioning del servizio cloud nel portale di gestione di Microsoft Azure.  

> [!NOTE]  
>  Il provisioning di un nuovo punto di distribuzione in Microsoft Azure può richiedere fino a 30 minuti. Fino a quando non viene eseguito il provisioning dell'account di archiviazione, nel file **CloudMgr.log** viene ripetuto il messaggio seguente: **Waiting for check if container exists (In attesa della verifica dell'esistenza del contenitore). Nuova verifica tra 10 secondi**. Il servizio viene quindi creato e configurato.  

 È possibile verificare il completamento dell'installazione del punto di distribuzione basato sul cloud utilizzando i seguenti metodi:  

-   Nel portale di gestione di Microsoft Azure la **Distribuzione** per il punto di distribuzione basato sul cloud visualizza lo stato **Pronto**.  

-   Nell'area di lavoro **Amministrazione**, **Configurazione della gerarchia**, nodo **Cloud** della console di Configuration Manager, il punto di distribuzione basato sul cloud visualizza lo stato **Pronto**.  

-   Configuration Manager visualizza l'ID messaggio di stato **9409** per il componente SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="a-namebkmkconfigdnsforclouddpsa-configure-name-resolution-for-cloud-based-distribution-points"></a><a name="BKMK_ConfigDNSforCloudDPs"></a> Configurare la risoluzione dei nomi per i punti di distribuzione basati sul cloud  
 Prima che i client possano accedere al punto di distribuzione basato su cloud, devono essere in grado di risolverne il nome in un indirizzo IP gestito da Microsoft Azure. I client effettuano questa operazione in due fasi:  

1.  Eseguono il mapping del nome del servizio fornito con il certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager nell'FQDN del servizio Microsoft Azure. Questo FQDN contiene un GUID e il suffisso DNS di **cloudapp.net**. Il GUID viene generato automaticamente dopo l'installazione del punto di distribuzione basato su cloud. È possibile visualizzare l'FQDN completo nel portale di gestione di Microsoft Azure, facendo riferimento all' **URL SITO** nel dashboard del servizio cloud. Un esempio di URL del sito è **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Risolvono l'FQDN del servizio Microsoft Azure nell'indirizzo IP allocato da Microsoft Azure. Questo indirizzo IP può essere anche individuato nel dashboard per il servizio cloud nel portale di Microsoft Azure ed è denominato **INDIRIZZO IP VIRTUALE (VIP) PUBBLICO**.  

Per eseguire il mapping del nome del servizio fornito con il certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager (ad esempio **clouddp1.contoso.com**) nell'FQDN del servizio Microsoft Azure (ad esempio **d1594d4527614a09b934d470.cloudapp.net**), i server DNS su Internet devono disporre di un alias DNS (record CNAME). I client possono quindi risolvere l'FQDN del servizio Microsoft Azure nell'indirizzo IP usando i server DNS su Internet.  

##  <a name="a-namebkmkconfigproxyforclouda-configure-proxy-settings-for-primary-sites-that-manage-cloud-services"></a><a name="BKMK_ConfigProxyforCloud"></a>Configurare le impostazioni proxy per i siti primari che gestiscono servizi cloud  
 Quando si usano servizi cloud con Configuration Manager, il sito primario che gestisce il punto di distribuzione basato sul cloud deve essere in grado di connettersi al portale di gestione di Microsoft Azure usando l'account **di sistema** del computer del sito primario. Questa connessione viene effettuata utilizzando il browser Web predefinito sul computer del server del sito primario.  

 Potrebbe essere necessario configurare le impostazioni proxy sul server del sito primario che gestisce il punto di distribuzione basato su cloud per consentire al sito primario di accedere a Internet e Microsoft Azure.  

 Usare la procedura seguente per configurare le impostazioni proxy per il server del sito primario nella console di Configuration Manager.  

> [!TIP]  
>  È possibile inoltre configurare il server proxy quando si installano dei nuovi ruoli del sistema del sito sul server del sito primario utilizzando l' **Aggiunta guidata ruoli del sistema del sito**.  

#### <a name="to-configure-proxy-settings-for-the-primary-site-server"></a>Per configurare le impostazioni proxy per il server del sito primario  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, fare clic su **Server e ruoli del sistema del sito**, quindi selezionare il server del sito primario che gestisce il punto di distribuzione basato su cloud.  

3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Sistema del sito**, quindi fare clic su **Proprietà**.  

4.  In **Proprietà sistema del sito** selezionare la scheda **Proxy**, quindi configurare le impostazioni proxy per il server del sito primario.  

5.  Fare clic su **OK** per salvare la nuova configurazione del server proxy.  



<!--HONumber=Nov16_HO1-->


