---
title: Configurare il Cloud Management Gateway
titleSuffix: Configuraton Manager
description: Usare questa procedura dettagliata per configurare un Cloud Management Gateway (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 04c1b262704ec6458bd9773c28c43a50d8fc0840
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurare il gateway di gestione cloud per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*  

Questo processo include i passaggi necessari per configurare un Cloud Management Gateway (CMG). 

> [!Tip]
> Questa funzionalità è stata introdotta per la prima volta nella versione 1610 come [versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1802, questa funzionalità non è più in versione non definitiva.



## <a name="before-you-begin"></a>Prima di iniziare

Iniziare leggendo l'articolo [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Usare l'articolo per determinare la struttura del Cloud Management Gateway. 

Usare l'elenco di controllo seguente per assicurarsi di avere le informazioni e i prerequisiti necessari per la creazione di un Cloud Management Gateway:  

- Ambiente Azure da usare. Ad esempio il cloud pubblico di Azure o il cloud di Azure Governo degli Stati Uniti.  

- A seconda della struttura pianificata saranno necessari uno o più certificati per Cloud Management Gateway. Per altre informazioni, vedere [Certificati per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- A partire dalla versione 1802, scegliere se usare il metodo **Distribuzione di Azure Resource Manager** o **Distribuzione classica del servizio**. Per altre informazioni, vedere [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Per la distribuzione Azure Resource Manager del Cloud Management Gateway devono essere disponibili i requisiti seguenti:  

    - Integrazione con [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) per la **Gestione cloud**. L'individuazione utenti di Azure AD non è necessaria.  

    - Un amministratore della sottoscrizione deve effettuare l'accesso.  

- Per la distribuzione classica del servizio Cloud Management Gateway devono essere disponibili i requisiti seguenti:  

    - ID della sottoscrizione di Azure  

    - Certificato di gestione di Azure  

- Un nome univoco globale per il servizio. Il nome deriva dal [certificato di autenticazione server del Cloud Management Gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- Area di Azure per questa distribuzione Cloud Management Gateway.  

- Numero di istanze di macchina virtuale necessarie per la scalabilità e la ridondanza.  



## <a name="set-up-a-cmg"></a>Impostare un Cloud Management Gateway

Eseguire questa procedura nel sito di livello superiore. Tale sito è un sito primario autonomo o il sito di amministrazione centrale.

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Cloud Management Gateway**.  

2. Fare clic su **Crea un gateway di gestione cloud** sulla barra multifunzione.  

3. A partire dalla versione 1802, nella pagina Generale della procedura guidata, iniziare scegliendo il metodo di distribuzione di Cloud Management Gateway, **Distribuzione di Azure Resource Manager** o **Distribuzione classica del servizio**.  

    1. Per **Distribuzione di Azure Resource Manager**: fare clic su **Accedi** per eseguire l'autenticazione con un account amministratore della sottoscrizione di Azure. La procedura guidata compila automaticamente i campi rimanenti in base alle informazioni archiviate durante il prerequisito di integrazione di Azure AD. Se si hanno più sottoscrizioni, selezionare l'**ID sottoscrizione** di quella che si vuole usare.  

    2. Per **Distribuzione classica del servizio** *e le versioni di Configuration Manager 1706 e 1710*: immettere l'**ID sottoscrizione** di Azure. Quindi fare clic su **Sfoglia** e selezionare il file con estensione pfx del certificato di gestione di Azure. 

4. Specificare l'**ambiente di Azure** per il Cloud Management Gateway. Le opzioni nell'elenco a discesa possono variare a seconda del metodo di distribuzione.  

5. Fare clic su **Avanti**. Attendere che il sito completi il test della connessione ad Azure.  

4. Nella pagina Impostazioni della procedura guidata, fare clic su **Sfoglia** e selezionare il file con estensione pfx del certificato di autenticazione server per il Cloud Management Gateway. Il nome di questo certificato popola i campi obbligatori **FQDN servizio** e **Nome servizio**.  

   > [!NOTE]  
   > A partire dalla versione 1802, il certificato di autenticazione server del Cloud Management Gateway supporta i caratteri jolly. Se si usa un certificato con caratteri jolly, sostituire l'asterisco (\*) nel campo **FQDN servizio** con il nome desiderato per il Cloud Management Gateway.  
   <!--491233-->  

5. Fare clic sull'elenco a discesa **Area** per scegliere l'area di Azure per questo Cloud Management Gateway.  

6. Nella versione 1802 e con la distribuzione Azure Resource Manager, selezionare un'opzione per **Gruppo di risorse**. 
   1. Se si sceglie **Usa esistente** immettere il nome del nuovo gruppo di risorse o selezionare un gruppo di risorse esistente nell'elenco a discesa.
   2. Se si sceglie **Crea nuovo** immettere il nome del nuovo gruppo di risorse.

6. Nel campo **Istanza della macchina virtuale** immettere il numero di macchine virtuali per questo servizio. Il valore predefinito è uno, ma è possibile impostare fino a 16 macchine virtuali per Cloud Management Gateway.  

7. Fare clic su **Certificati** per aggiungere i certificati radice trusted del client. Aggiungere fino a due autorità di certificazione radice attendibili e quattro autorità intermedie (subordinate).  

8. Per impostazione predefinita, la procedura guidata abilita l'opzione **Verifica la revoca del certificato client**. Per il funzionamento di questa verifica è necessario pubblicare in modalità pubblica un elenco di revoche di certificati (CRL). Se non si pubblica un CRL, deselezionare questa opzione.  

9. Fare clic su **Avanti**.  

10. Per monitorare il traffico del Cloud Management Gateway con una soglia di 14 giorni, selezionare la casella di controllo per attivare l'avviso di soglia. Specificare quindi la soglia e le percentuali in corrispondenza delle quali verranno generati i diversi livelli di avviso. Al termine scegliere **Avanti**.  

11. Verificare le impostazioni e scegliere **Avanti**. Configuration Manager avvia la configurazione del servizio. Dopo l'esecuzione della procedura guidata saranno necessari da 5 a 15 minuti per completare il provisioning del servizio in Azure. Controllare la colonna **Stato** per la nuova istanza di Cloud Management Gateway per determinare quando il servizio è pronto.  

 > [!Note]  
 > Per la risoluzione dei problemi relativi alle distribuzioni di Cloud Management Gateway, usare **CloudMgr.log** e **CMGSetup.log**. Per altre informazioni, vedere [File di log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurare il sito primario per l'autenticazione del certificato client

Se si usano i [certificati di autenticazione client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) per l'autenticazione dei client con Cloud Management Gateway, seguire questa procedura per configurare ogni sito primario.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito primario al quale sono assegnati i client basati su Internet e scegliere **Proprietà**.  

3. Passare alla scheda **Comunicazioni computer client** della finestra delle proprietà del sito primario e selezionare **Utilizza certificato client PKI (funzionalità di autenticazione client) quando disponibile**.  

4. Se non si pubblica un elenco di revoche di certificati (CRL, Certificate Revocation List) deselezionare l'opzione **Controllo client dell'elenco di revoche di certificati (CRL) per i sistemi del sito**.  



## <a name="add-the-cmg-connection-point"></a>Aggiungere il punto di connessione del Cloud Management Gateway

Il punto di connessione del Cloud Management Gateway è il ruolo di sistema del sito per la comunicazione con il Cloud Management Gateway. Per aggiungere il punto di connessione del Cloud Management Gateway, seguire le istruzioni generali per [installare i ruoli del sistema del sito](/sccm/core/servers/deploy/configure/install-site-system-roles). Nella pagina Selezione ruolo del sistema dell'Aggiunta guidata ruoli del sistema del sito selezionare **Punto di connessione del gateway di gestione cloud**. Quindi selezionare il **Nome del gateway di gestione cloud** al quale si connette il server. La procedura guidata visualizza l'area per il Cloud Management Gateway selezionato. 

> [!Important]
> In determinati scenari il punto di connessione del Cloud Management Gateway deve avere un [certificato di autenticazione client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate). 

 > [!Note]  
 > Per la risoluzione dei problemi relativi all'integrità del Cloud Management Gateway, usare **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Per altre informazioni, vedere [File di log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurare i ruoli lato client per il traffico del Cloud Management Gateway

Configurare il punto di gestione e il punto di aggiornamento software per accettare il traffico del Cloud Management Gateway. Eseguire questa procedura nel sito primario, per tutti i punti di gestione e i punti di aggiornamento software che servono i client basati su Internet.  

1. Nella console di Configuration Manager, passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito**, fare clic con il pulsante destro del mouse su **Server e ruoli del sistema del sito** e selezionare **Punto di gestione** nell'elenco.  

2. Selezionare il server del sistema del sito da configurare per il traffico del Cloud Management Gateway. Selezionare il ruolo **Punto di gestione** nel riquadro dei dettagli e quindi fare clic su **Proprietà** nella barra multifunzione.  

3. Nel pannello Proprietà punto di gestione, in Connessioni client selezionare la casella accanto a **Consenti il traffico del gateway di gestione cloud di Configuration Manager**. 
    - A seconda della progettazione del Cloud Management Gateway e della versione di Configuration Manager, potrebbe essere necessario abilitare l'opzione **HTTPS**. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Fare clic su **OK**.   

Ripetere questi passaggi in base alle esigenze per i punti di gestione aggiuntivi e per gli eventuali punti di aggiornamento software. 



## <a name="configure-clients-for-cmg"></a>Configurare i client per il Cloud Management Gateway

Dopo che il Cloud Management Gateway e i ruoli del sistema del sito sono in esecuzione, i client recuperano automaticamente la posizione del servizio Cloud Management Gateway alla richiesta di posizione successiva. Per ricevere la posizione del servizio Cloud Management Gateway i client devono essere inclusi nell'intranet, salvo se si [installano e assegnano client Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Il ciclo di polling per le richieste di percorso è di 24 ore. Se non si vuole attendere la richiesta di percorso della normale pianificazione, è possibile forzare la richiesta riavviando il servizio host agenti di SMS (ccmexec.exe) nel computer.  

> [!Note]
> Per impostazione predefinita, tutti i client ricevono i criteri Cloud Management Gateway. È possibile controllare questo comportamento con l'impostazione client [Consenti ai client di usare un gateway di gestione cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).

Il client di Configuration Manager determina automaticamente se si trova sull'intranet o su Internet. Se il client riesce a contattare un controller di dominio o un punto di gestione locale, imposta il proprio tipo di connessione su **Ora intranet**. In caso contrario, passa all'impostazione **Ora Internet** e usa la posizione del servizio Cloud Management Gateway per comunicare con il sito.

>[!NOTE]
> È possibile forzare il client perché usi sempre il Cloud Management Gateway, sia che si trovi sull'intranet o su Internet. Questa configurazione è utile per l'esecuzione di test o per client in sedi nelle quali si vuole imporre l'uso del servizio Cloud Management Gateway. Impostare la seguente chiave del Registro di sistema nel client:
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> È anche possibile specificare questa impostazione durante l'installazione client usando la proprietà [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf).

Per verificare che i client dispongano della proprietà che specifica il Cloud Management Gateway, aprire un prompt dei comandi di Windows PowerShell come amministratore nel computer client ed eseguire il comando seguente: `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Questo comando visualizza tutti i punti di gestione basati su Internet rilevati dal client. Il Cloud Management Gateway non è tecnicamente un punto di gestione basato su Internet, ma i client lo rilevano come tale.

 > [!Note]  
 > Per la risoluzione dei problemi relativi al traffico client del Cloud Management Gateway, usare **CMGHttpHandler.log**, **CMGService.log** e **SMS_Cloud_ProxyConnector.log**. Per altre informazioni, vedere [File di log](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Modificare un Cloud Management Gateway

Dopo la creazione di un Cloud Management Gateway è possibile modificarne alcune impostazioni. Selezionare il Cloud Management Gateway nella console di Configuration Manager e fare clic su **Proprietà**. È possibile configurare le impostazioni seguenti:  

- **Generalee**  

    - **Certificato di gestione di Azure**: modificare il certificato di gestione di Azure per il Cloud Management Gateway. Questa opzione è utile quando si aggiorna il certificato prima della scadenza.  

- **Impostazioni**  

    - **File certificato**: cambiare il certificato di autenticazione server per il Cloud Management Gateway. Questa opzione è utile quando si aggiorna il certificato prima della scadenza.  

    - **Istanza della macchina virtuale**: modificare il numero di macchine virtuali che il servizio usa in Azure. Questa impostazione consente di modificare dinamicamente le dimensioni del servizio in base a considerazioni sui costi o sull'uso.  

    - **Certificati**: aggiungere o rimuovere certificati intermedi o certificati radice trusted dell'attività di certificazione (CA). Questa opzione è utile quando si aggiungono nuove autorità di certificazione o quando si ritirano i certificati scaduti.  

    - **Verifica la revoca del certificato client**: se questa impostazione non è stata abilitata al momento della creazione del Cloud Management Gateway, è possibile abilitarla in un secondo momento, dopo la pubblicazione dell'elenco CRL.  

- **Avvisi**: è possibile riconfigurare gli avvisi in qualsiasi momento dopo la creazione del Cloud Management Gateway. 

Altre modifiche significative, ad esempio le configurazioni seguenti, richiedono la ridistribuzione del servizio:
- Metodo di distribuzione classico ad Azure Resource Manager
- Sottoscrizione
- Nome del servizio
- PKI da privato a pubblico
- Area

Mantenere sempre almeno un Cloud Management Gateway per consentire ai client basati su Internet di ricevere i criteri aggiornati. I client basati su Internet non possono comunicare con un Cloud Management Gateway rimosso. Inoltre i client non rilevano un nuovo servizio Cloud Management Gateway fino a quando non effettuano nuovamente il roaming all'intranet. Quando si crea una seconda istanza del Cloud Management Gateway per eliminare la prima, è necessario creare anche un altro punto di connessione del Cloud Management Gateway.

Per impostazione predefinita i client aggiornano i criteri ogni 24 ore. Pertanto, dopo aver creato un nuovo Cloud Management Gateway, attendere almeno un giorno prima di eliminare quello precedente. Se i client sono disattivati o non dispongono di una connessione a Internet il tempo di attesa può essere superiore. 

A partire dalla versione 1802, se è presente un Cloud Management Gateway esistente con il metodo di distribuzione classico, è necessario distribuire un nuovo Cloud Management Gateway per usare il metodo di distribuzione Azure Resource Manager.<!--509753--> Sono disponibili due opzioni:
- Per riusare lo stesso nome di servizio:
    1. Eliminare la versione classica del Cloud Management Gateway, ricordando che è necessario avere almeno un Cloud Management Gateway sempre attivo per i client basati su Internet.
    2. Creare un nuovo Cloud Management Gateway usando una distribuzione di Gestione risorse. Riusare lo stesso certificato di autenticazione server.
    3. Riconfigurare il punto di connessione del Cloud Management Gateway in modo che usi la nuova istanza del Cloud Management Gateway.
- Per usare un nuovo nome del servizio:
    1. Creare un nuovo Cloud Management Gateway usando una distribuzione di Gestione risorse. Usare un nuovo certificato di autenticazione server.
    2. Creare un nuovo punto di connessione del Cloud Management Gateway e collegarlo al nuovo Cloud Management Gateway.
    3. Attendere almeno un giorno in modo che i client basati su Internet ricevano i criteri relativi al nuovo Cloud Management Gateway.
    4. Eliminare il Cloud Management Gateway versione classica.

Modificare il Cloud Management Gateway solo dalla console di Configuration Manager. L'apporto di modifiche al servizio o alle macchine virtuali sottostanti direttamente in Azure non è supportato. Tali modifiche possono andare perdute senza preavviso. Come con qualsiasi PaaS, il servizio può ricompilare le macchine virtuali in qualsiasi momento. Le ricompilazioni possono verificarsi per la manutenzione dell'hardware back-end o per l'applicazione di aggiornamenti al sistema operativo delle macchine virtuali.

Se è necessario eliminare il Cloud Management Gateway, eseguire questa operazione anche dalla console di Configuration Manager. La rimozione manuale di componenti in Azure crea incoerenze nel sistema. Questo stato produce dati orfani e può dare origine a comportamenti imprevisti. 



## <a name="next-steps"></a>Passaggi successivi

- [Monitorare i client per il gateway di gestione cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Domande frequenti sul gateway di gestione cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
