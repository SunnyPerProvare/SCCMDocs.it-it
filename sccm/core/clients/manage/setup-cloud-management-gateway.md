---
title: Configurare il gateway di gestione cloud | Documentazione Microsoft
description: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 05/01/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 84b617b3e83636ab4578174ef40e786dcf1178cd
ms.sourcegitcommit: 06aef618f72c700f8a716a43fb8eedf97c62a72b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2017
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurare il gateway di gestione cloud per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, il processo di configurazione del gateway di gestione cloud in Configuration Manager include i passaggi seguenti:

## <a name="step-1-configure-required-certificates"></a>Passaggio 1: Configurare i certificati richiesti

> [!TIP]  
> Prima di richiedere un certificato, verificare che il nome di dominio di Azure desiderato, ad esempio GraniteFalls.CloudApp.Net, sia univoco. A tale scopo, accedere al [portale di Microsoft Azure](https://manage.windowsazure.com), fare clic su **Nuovo**, selezionare **Servizio cloud** e quindi **Creazione personalizzata**. Nel campo **URL** digitare il nome di dominio desiderato assicurandosi di non fare clic sul segno di spunta per creare il servizio. Il portale verificherà se il nome di dominio è disponibile o se è già in uso in un altro servizio.

## <a name="option-1-preferred---use-the-server-authentication-certificate-from-a-public-and-globally-trusted-certificate-provider-like-verisign"></a>Opzione 1 (consigliata): Usare il certificato di autenticazione server di un provider di certificati pubblico e globalmente attendibile, ad esempio VeriSign

Quando si usa questo metodo, i client considereranno automaticamente attendibile il certificato e non è necessario creare manualmente un certificato SSL personalizzato.

1. Creare un record di nome canonico (CNAME) nel DNS (Domain Name Service) pubblico dell'organizzazione per creare un alias per il servizio gateway di gestione cloud con un nome descrittivo che verrà usato nel certificato pubblico.
Ad esempio, Contoso denomina il proprio servizio gateway di gestione cloud **GraniteFalls**, che in Azure diventerà **GraniteFalls.CloudApp.Net**. Nello spazio dei nomi contoso.com del DNS pubblico di Contoso l'amministratore DNS crea un nuovo record CNAME **GraniteFalls.Contoso.com** per il nome host effettivo, **GraniteFalls.CloudApp.net**.
2. Richiede quindi un certificato di autenticazione server da un provider pubblico usando il nome comune dell'alias CNAME.
Ad esempio, Contoso usa **GraniteFalls.Contoso.com** per il nome comune del certificato.
3. Creare il servizio gateway di gestione cloud nella console di Configuration Manager usando questo certificato.
    - Nella pagina **Impostazioni** della Creazione guidata gateway di gestione cloud, quando si aggiunge il certificato server per il servizio cloud (dal **file Certificate**), la procedura guidata estrae il nome host dal nome comune del certificato come nome del servizio e quindi lo aggiunge a **cloudapp.net** (o **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti) come nome di dominio completo del servizio per creare il servizio in Azure.
Ad esempio, quando si crea il gateway di gestione cloud di Contoso, il nome host **GraniteFalls** viene estratto dal nome comune del certificato, così che il servizio effettivo viene creato in Azure come **GraniteFalls.CloudApp.net**.

### <a name="option-2---create-a-custom-ssl-certificate-for-cloud-management-gateway-in-the-same-way-as-for-a-cloud-based-distribution-point"></a>Opzione 2: È possibile creare un certificato SSL personalizzato per il gateway di gestione cloud esattamente come si farebbe per un punto di distribuzione basato su cloud

È possibile creare un certificato SSL personalizzato per il gateway di gestione cloud esattamente come si farebbe per un punto di distribuzione basato su cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates) procedendo in modo diverso per le operazioni seguenti:

- Quando si richiede un certificato del server Web personalizzato, per il nome comune del certificato specificare un nome di dominio completo che termina con **cloudapp.net** per usare il gateway di gestione cloud nel cloud pubblico di Azure o con **usgovcloudapp.net** per usarlo in Azure Government Cloud.


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

>[!NOTE]
>Se il certificato client è stato rilasciato da un'autorità di certificazione subordinata, sarà necessario ripetere questo passaggio per ogni certificato presente nella catena.

## <a name="step-3-upload-the-management-certificate-to-azure"></a>Passaggio 3: Caricare il certificato di gestione in Azure

Per consentire a Configuration Manager di accedere all'API di Azure e configurare il gateway di gestione cloud, è necessario un certificato di gestione di Azure. Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:

- [Panoramica sui certificati per i servizi cloud di Azure](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Caricare un certificato di gestione dell'API di gestione di Azure](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Sarà necessario per configurare il gateway di gestione cloud nella console di Configuration Manager nel [passaggio successivo](#step-4-set-up-cloud-management-gateway).



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

    - Specificare il certificato radice e gli eventuali certificati subordinati esportati dal certificato client. La procedura guidata accetta un massimo di due certificati radice e di quattro certificati subordinati.

    -   Specificare lo stesso FQDN del nome del servizio utilizzato per creare il nuovo modello di certificato. Per il nome del servizio FQDN basato sul cloud di Azure in uso, è necessario specificare uno dei suffissi seguenti:

    Cloud di Azure | Prefisso FQDN
    --------------|-------------
    Cloud pubblico (commerciale) | .cloudapp.net    
    Cloud pubblica amministrazione | .usgovcloudapp.net

  - Deselezionare la casella accanto a **Verifica la revoca di certificato client**  (a meno che non si intenda pubblicare le informazioni di CRL).

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

L'ultimo passaggio della configurazione del gateway di gestione cloud consiste nel configurare i ruoli del sistema del sito per accettare il traffico del gateway di gestione cloud. Per Cloud Management Gateway sono supportati solo i ruoli punto di aggiornamento software e punto di gestione. È necessario configurare separatamente ogni ruolo.

1. Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Server e ruoli di sistema del sito**.

2. Scegliere il server di sistema del sito per il ruolo che si vuole configurare per il traffico del gateway di gestione cloud.

3. Scegliere il ruolo e quindi scegliere **Proprietà**.

4. Nel pannello Proprietà del ruolo, in Connessioni client selezionare la casella accanto a **Consenti il traffico del gateway di gestione cloud di Configuration Manager** e quindi scegliere **OK**. Ripetere questi passaggi per i ruoli rimanenti. L'abilitazione dell'opzione **HTTPS** è una procedura consigliata per la sicurezza, ma non è obbligatoria.

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
