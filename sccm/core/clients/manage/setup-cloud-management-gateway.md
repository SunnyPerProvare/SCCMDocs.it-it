---
title: Configurare il gateway di gestione cloud | Documentazione Microsoft
description: 
author: nbigman
manager: angrobe
ms.author: nbigman
ms.date: 12/14/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
translationtype: Human Translation
ms.sourcegitcommit: 2bcc5d9dde1f1a2d9c33575d6c463e281ac818e8
ms.openlocfilehash: 61b8cd8458718b9a54edb129739c619f947ac380

---

# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurare il gateway di gestione cloud per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, il processo di configurazione del gateway di gestione cloud in Configuration Manager include i passaggi seguenti:

## <a name="step-1-create-a-custom-ssl-certificate"></a>Passaggio 1: Creare un certificato SSL personalizzato

È possibile creare un certificato SSL personalizzato per il gateway di gestione cloud esattamente come si farebbe per un punto di distribuzione basato su cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) procedendo in modo diverso per le operazioni seguenti:

-   Quando si configura il nuovo modello di certificato, assegnare le autorizzazioni **Lettura** e **Registrazione** al gruppo di protezione impostato per i server di Configuration Manager.

-  Quando si richiede un certificato del server Web personalizzato, per il nome comune del certificato specificare un nome di dominio completo che termina con **cloudapp.net** per usare il gateway di gestione cloud nel cloud pubblico di Azure o con **usgovcloudapp.net** per usarlo in Azure Government Cloud.

## <a name="step-2-export-the-client-certificates-root"></a>Passaggio 2: Esportare la radice del certificato client

Il modo più semplice per ottenere l'esportazione della radice dei certificati client utilizzati nella rete è aprire un certificato client in uno dei computer appartenenti a un dominio che ne abbia uno e copiarlo.

> [!NOTE] 
>
> I certificati client sono richiesti su qualsiasi computer che si intende gestire con il gateway di gestione cloud e sul server di sistema del sito che ospita il punto di connessione del gateway di gestione. Se è necessario aggiungere un certificato client a uno di tali computer, vedere [Distribuzione del certificato client per computer Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

1.  Nella finestra Esegui digitare **mmc** e premere INVIO.

2.  Nel menu File fare scegliere **Aggiungi/Rimuovi snap-in**.

3.  Nella finestra di dialogo Aggiungi/Rimuovi snap-in scegliere **Certificati** > **Aggiungi &gt;** > **Account computer** > **Avanti** > **Computer locale** > **Fine**. 

4.  Passare a **Certificati** &gt; **Personale** &gt; **Certificati**.

5.  Fare doppio clic sul certificato per l'autenticazione client nel computer, fare clic sulla scheda Percorso certificazione e fare doppio clic sull'autorità radice (nella parte superiore del percorso).

6.  Nella scheda Dettagli scegliere **Copia su file**.

7.  Completare l'Esportazione guidata certificati utilizzando il formato di certificato predefinito. Prendere nota del nome e percorso del certificato radice creato. Sarà necessario configurare il gateway di gestione cloud in un [passaggio successivo](#step-4-set-up-cloud-management-gateway).

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Passaggio 3: Caricare il certificato di gestione in Azure

Per consentire a Configuration Manager di accedere all'API di Azure e configurare il gateway di gestione cloud, è necessario un certificato di gestione di Azure. Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:

- [Panoramica sui certificati per i servizi cloud di Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Caricare un certificato di gestione dell'API di gestione di Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Sarà necessario per configurare il gateway di gestione cloud nella console di Configuration Manager nel [passaggio successivo](#step-4-set-up-cloud-management-gateway).

### <a name="subordinate-ca-certificates-and-azure"></a>Certificati di una CA subordinata e Azure

Se il certificato viene emesso da una CA subordinata (subCA) e l'infrastruttura PKI dell'azienda non è presente su Internet, per caricare il certificato in Azure seguire questa procedura. 

1. Nel portale di Azure, dopo aver configurato un gateway di gestione cloud, individuare il servizio del gateway di gestione cloud e passare alla scheda **Certificato**. Caricare i certificati subCA in tale posizione. Se sono presenti più certificati subCA, è necessario caricarli tutti. 
2. Dopo aver caricato un certificato, registrarne l'identificazione personale. 
3. Aggiungere l'identificazione personale al database del sito usando questo script:
    
```

    DIM serviceCName
    DIM subCAThumbprints

    ' Verify arguments
    IF WScript.Arguments.Count <> 2 THEN
    WScript.StdOut.WriteLine "Usage: CScript UpdateSubCAThumbprints.vbs <ServiceCName> <SubCA cert thumbprints, separated by ;>"
    WScript.Quit 1
    END IF

    'Get arguments
    serviceCName = WScript.Arguments.Item(0)
    subCAThumbprints = WScript.Arguments.Item(1)

    'Find SMS Provider
    WScript.StdOut.WriteLine "Searching for SMS Provider for local site..."
    SET objSMSNamespace = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms")
    SET results = objSMSNamespace.ExecQuery("SELECT * From SMS_ProviderLocation WHERE ProviderForLocalSite = true")

    'Process the results
    FOR EACH var in results
    siteCode = var.SiteCode
    NEXT

    IF siteCode = "" THEN
    WScript.StdOut.WriteLine "Failed to locate SMS provider."
    WScript.Quit 1
    END IF

    WScript.StdOut.WriteLine "SiteCode = " & siteCode 

    ' Connect to the SMS namespace
    SET objWMIService = GetObject("winmgmts:{impersonationLevel=impersonate}!\\.\root\sms\site_" & siteCode)

    'Get instance of SMS_AzureService
    DIM query
    query = "SELECT * From SMS_AzureService WHERE ServiceType = 'CloudProxyService' AND ServiceCName = '" & serviceCName & "'"
    WScript.StdOut.WriteLine "Run WQL query: " &  query
    SET objInstances = objWMIService.ExecQuery(query)

    IF IsNull(objInstances) OR (objInstances.Count = 0) THEN
    WScript.StdOut.WriteLine "Failed to get Azure_Service instance."
    WScript.Quit 1
    END IF

    FOR EACH var IN objInstances
    SET azService = var
    NEXT

    WScript.StdOut.WriteLine "Update [SubCACertThumbprint] to " & subCAThumbprints

    'Update SubCA cert thumbprints
    azService.Properties_.item("SubCACertThumbprint") = subCAThumbprints

    'Save data back to provider
    azService.Put_

    WScript.StdOut.WriteLine "[SubCACertThumbprint] is updated successfully."
```


## <a name="step-4-set-up-cloud-management-gateway"></a>Passaggio 4: Configurare il gateway di gestione cloud

>[!NOTE]
>Nella versione 1610 il gateway di gestione cloud è una funzionalità di versione non definitiva. Per abilitarla, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Servizi cloud** > **Gateway di gestione cloud**.
2. Scegliere **Crea un gateway di gestione cloud**.

3. Nella Creazione guidata del gateway di gestione cloud immettere l'ID sottoscrizione di Azure (copiato dal portale di gestione di Azure) e passare al file di certificato caricato come certificato di gestione di Azure. Scegliere **Avanti** e attendere qualche secondo per consentire alla console di connettersi ad Azure.

4. Compilare i dettagli aggiuntivi nella procedura guidata:

    - Specificare il nome del servizio che verrà eseguito in Azure. Il nome del servizio deve essere costituito soltanto da caratteri alfanumerici e avere una lunghezza compresa tra 3 e 24 caratteri.

    - Scegliere l'area di Azure in cui si vuole eseguire il servizio.

    - Specificare il numero di macchine virtuali da usare per il servizio. Il valore predefinito è 1, ma è possibile eseguire fino a 16 macchine virtuali per il servizio.

    >[!NOTE]
    >Se si usa un proxy Internet come punto di connessione del gateway di gestione cloud, è necessario aumentare il numero di porte sul proxy aggiungendone tante quante sono le macchine virtuali usate, a partire dalla porta 10124.

    - Specificare la chiave privata (file con estensione .pfx) esportato dal certificato SSL personalizzato.

    - Specificare il certificato radice esportato dal certificato client.

    -   Specificare lo stesso FQDN del nome del servizio utilizzato per creare il nuovo modello di certificato. Per il nome del servizio FQDN basato sul cloud di Azure in uso, è necessario specificare uno dei suffissi seguenti:

    Cloud di Azure | Prefisso FQDN
    --------------|-------------
    Cloud pubblico (commerciale) | .cloudapp.net    
    Cloud pubblica amministrazione | .usgovcloudapp.net

  - Deselezionare la casella accanto a **Verifica la revoca di certificato client ** (a meno che non si intenda pubblicare le informazioni di CRL).

  - Al termine scegliere **Avanti**.

5. Se si intende monitorare il traffico del gateway di gestione cloud con una soglia di 14 giorni, selezionare la casella di controllo per attivare l'avviso di soglia. Specificare quindi la soglia e le percentuali in corrispondenza delle quali verranno generati i diversi livelli di avviso. Al termine scegliere **Avanti**.

6. Verificare le impostazioni e scegliere **Avanti**. Configuration Manager avvia la configurazione del servizio. Una volta eseguita la procedura guidata, saranno necessari da 5 a 15 minuti per completare il provisioning del servizio in Azure. Controllare la colonna **Stato** per il nuovo gateway di gestione cloud configurato per determinare quando il servizio è pronto.

## <a name="step-5-configure-primary-site-for-client-certification-authentication"></a>Passaggio 5: Configurare il sito primario per l'autenticazione con certificati client

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Siti**.

2. Selezionare il sito primario per i client che si vogliono gestire tramite il server di gestione cloud e scegliere **Proprietà**.

3. Nella scheda Comunicazioni computer client della finestra delle proprietà del sito primario selezionare **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile**.

4. Verificare di aver deselezionato **Controllo client dell'elenco di revoche di certificati (CRL) per i sistemi del sito**. Questa opzione è necessaria solo quando si pubblicano i CRL.


## <a name="step-6-add-the-cloud-management-gateway-connector-point"></a>Passaggio 6: Aggiungere il punto di connessione del gateway di gestione cloud

Il punto di connessione del gateway di gestione cloud è un nuovo ruolo del sistema del sito per la comunicazione con il gateway di gestione cloud. Per aggiungere il punto di connessione del gateway di gestione cloud, seguire le istruzioni riportate in [Add site system roles for System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles) (Aggiungere ruoli del sistema del sito per System Center Configuration Manager).

## <a name="step-7-configure-roles-for-cloud-management-gateway-traffic"></a>Passaggio 7: Configurare i ruoli per il traffico del gateway di gestione cloud

L'ultimo passaggio della configurazione del gateway di gestione cloud consiste nel configurare i ruoli del sistema del sito per accettare il traffico del gateway di gestione cloud. Con la versione Technical Preview 1606 sono supportati per il gateway di gestione cloud solo i ruoli punto di gestione, punto di distribuzione e aggiornamento del software. È necessario configurare separatamente ogni ruolo.

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Server e ruoli di sistema del sito**.

2. Scegliere il server di sistema del sito per il ruolo che si vuole configurare per il traffico del gateway di gestione cloud.

3. Scegliere il ruolo e quindi scegliere **Proprietà**.

4. Nella finestra delle proprietà del ruolo, sotto Connessioni client, scegliere **HTTPS**, selezionare la casella accanto a **Consenti il traffico del gateway di gestione cloud di Configuration Manager** e quindi scegliere **OK**. Ripetere questi passaggi per i ruoli rimanenti.

## <a name="step-8-configure-clients-for-cloud-management-gateway"></a>Passaggio 8: Configurare i client per il gateway di gestione cloud

Quando il gateway di gestione cloud e i ruoli del sistema del sito sono configurati completamente e in esecuzione, i client ottengono automaticamente la posizione del servizio gateway di gestione cloud alla successiva richiesta di percorso. Per ricevere la posizione del servizio gateway di gestione cloud, i client devono trovarsi nella rete aziendale. Il ciclo di polling per le richieste di percorso è di 24 ore. Se non si vuole attendere la richiesta di percorso della normale pianificazione, è possibile forzare la richiesta riavviando il servizio host agenti di SMS (ccmexec.exe) nel computer.

Dopo che la posizione del servizio gateway di gestione cloud è stata configurata sul client, il servizio è in grado di determinare automaticamente se si trova sulla intranet o in Internet. Se il client può contattare il controller di dominio o il punto di gestione locale, userà tale elemento per la comunicazione con Configuration Manager. In caso contrario, riterrà che Configuration Manager si trova in Internet e per comunicare userà la posizione del servizio gateway di gestione cloud.

>[!NOTE]
> È possibile forzare il client perché usi sempre il gateway di gestione cloud indipendentemente dal fatto che si trovi nella intranet o in Internet. A questo scopo, impostare nel computer client la chiave del Registro di sistema seguente:\
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`

Per verificare che il client sia in grado di contattare Configuration Manager, è possibile eseguire sul computer client il comando PowerShell seguente:

`gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate`

Questo comando visualizza i punti di gestione che il client può contattare, incluso il servizio gateway di gestione cloud.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i client per il gateway di gestione cloud](monitor-clients-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


