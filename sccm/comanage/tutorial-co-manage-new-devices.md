---
title: Esercitazione&#58; Abilitare la co-gestione per nuovi dispositivi Windows 10 basati su Internet
titleSuffix: Configuration Manager
description: Configurare la co-gestione per dispositivi Windows 10 con Configuration Manager e Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/08/2019
ms.topic: tutorial
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: ''
ms.openlocfilehash: 61400d382a539efa495af99795e32fc1f2a517ab
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737355"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Esercitazione: Abilitare la co-gestione per nuovi dispositivi basati su Internet
Con la co-gestione è possibile mantenere i processi consolidati per l'uso di Configuration Manager per la gestione dei PC nell'organizzazione. Allo stesso tempo, è possibile investire nel cloud usando Intune per sicurezza e provisioning moderno. 

In questa esercitazione viene configurata la co-gestione di dispositivi Windows 10 in un ambiente in cui si usano sia Azure Active Directory (AD) sia Active Directory locale, ma non è presente [Azure Active Directory ibrido](https://docs.microsoft.com/azure/active-directory/devices/overview#hybrid-azure-ad-joined-devices). L'ambiente di Configuration Manager include un unico sito primario con tutti i ruoli del sistema del sito situati nello stesso server, il server del sito. Questa esercitazione parte dal presupposto che i dispositivi Windows 10 sono già registrati con Intune. 

Se è presente un'istanza di Azure AD ibrido che unisce Active Directory locale con Azure AD, è consigliabile seguire l'esercitazione complementare [Abilitare la co-gestione per i client di Configuration Manager](/sccm/comanage/tutorial-co-manage-clients). 
 
Usare questa esercitazione in questi casi:  
- Sono presenti dispositivi Windows 10 da includere nella co-gestione. Potrebbe essere stato effettuato il provisioning di questi dispositivi tramite Windows Autopilot o i dispositivi possono provenire dall'OEM hardware. 
- Sono presenti dispositivi Windows 10 in Internet attualmente gestiti con Intune cui si vuole aggiungere il client di Configuration Manager.


**In questa esercitazione verrà descritto come:**  
> [!div class="checklist"]  
> * Esaminare i prerequisiti per Azure e per l'ambiente locale
> * Richiedere un certificato SSL pubblico per Cloud Management Gateway
> * Abilitare i servizi di Azure in Configuration Manager
> * Distribuire e configurare Cloud Management Gateway  
> * Configurare il punto di gestione e i client per usare Cloud Management Gateway
> * Abilitare la co-gestione in Configuration Manager
> * Configurare Intune per installare il client di Configuration Manager
> * Assegnare la licenza per i servizi cloud



## <a name="prerequisites"></a>Prerequisiti  

### <a name="azure-services-and-environment"></a>Ambiente e servizi di Azure
- Sottoscrizione di Azure ([versione di valutazione gratuita](https://azure.microsoft.com/free)) 
- Azure Active Directory Premium 
- Sottoscrizione di Microsoft Intune 
  > [!TIP]  
  > Una sottoscrizione di Enterprise Mobility + Security (EMS) include sia Azure Active Directory Premium sia Microsoft Intune. Sottoscrizione di EMS ([versione di valutazione gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Agli utenti devono essere [assegnate le licenze](tutorial-co-manage-clients.md#assign-intune-licenses-to-users) per *Intune* e *Azure Active Directory Premium*
- Intune è configurato per la [registrazione automatica dei dispositivi](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  


### <a name="on-premises-infrastructure"></a>Infrastruttura locale
- System Center Configuration Manager Current Branch, versione 1810 o successive.  
  
  La versione 1810 introduce [HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http), che viene usato in questa esercitazione per evitare requisiti PKI più complessi. Tramite l'uso di HTTP avanzato, il sito primario usato per gestire i client deve essere configurato per l'uso di certificati generati da Configuration Manager per i sistemi del sito HTTP.  
   
  La versione 1810 introduce anche una riga di comando più semplice per l'installazione basata su Internet del client di Configuration Manager.

- L'[autorità MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) deve essere impostata su Intune  

### <a name="external-certificates"></a>Certificati esterni:
- Certificato di autenticazione server di Cloud Management Gateway. Si tratta di un certificato SSL rilasciato da un provider di certificati pubblico e attendibile a livello globale. Ad esempio, tra gli altri, DigiCert, Thawte, o VeriSign. È necessario esportare questo certificato come file PFX con chiave privata.  

- Più avanti in questa esercitazione vengono fornite indicazioni su come configurare la richiesta del certificato.

### <a name="permissions"></a>Autorizzazioni
In questa esercitazione usare le autorizzazioni seguenti per completare le attività:
- Un account che sia un *amministratore globale* in Azure  
- Un account che sia un *amministratore di dominio* nell'infrastruttura locale  
- Un account che sia un *amministratore completo* per *tutti* gli ambiti in Configuration Manager   


## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Richiedere un certificato pubblico per Cloud Management Gateway
Quando i dispositivi sono in Internet, per la co-gestione è necessario Cloud Management Gateway di Configuration Manager. Cloud Management Gateway permette ai dispositivi Windows 10 basati su Internet di comunicare con la distribuzione di Configuration Manager locale. Per stabilire una relazione di trust tra i dispositivi e l'ambiente di Configuration Manager, Cloud Management Gateway richiede un certificato SSL.

Questa esercitazione usa un certificato pubblico denominato **certificato di autenticazione server di Cloud Management Gateway** che deriva l'autorità da un provider di certificati attendibile a livello globale. Sebbene sia possibile configurare la co-gestione usando certificati che derivano l'autorità dall'autorità di certificazione Microsoft locale, l'uso di certificati autofirmati esula dall'ambito di questa esercitazione.

Il **certificato di autenticazione server di Cloud Management Gateway** viene usato per crittografare il traffico delle comunicazioni tra il client di Configuration Manager e Cloud Management Gateway. Il certificato riconduce a una radice attendibile per verificare l'identità del server per il client. Il certificato pubblico include una radice attendibile, ritenuta già attendibile dai client Windows.

Per quanto riguarda questo certificato: 

- È necessario identificare un nome univoco per il servizio Cloud Management Gateway in Azure e quindi specificare questo nome nella richiesta di certificato.  
- Generare la richiesta di certificato in un server specifico e quindi inviare la richiesta a un provider di certificati pubblici per ottenere il certificato SSL necessario.  
- Eseguire l'importazione nel sistema che ha generato la richiesta del certificato ricevuto di nuovo dal provider. Usare lo stesso computer per esportare il certificato per l'uso quando successivamente si distribuirà Cloud Management Gateway in Azure.  
- Quando Cloud Management Gateway viene installato, crea un servizio Cloud Management Gateway in Azure usando il nome specificato nel certificato.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identificare un nome univoco per il servizio Cloud Management Gateway in Azure
Nel richiedere il certificato di autenticazione server di Cloud Management Gateway, specificare un nome univoco per identificare il *servizio cloud (versione classica)* in Azure. Per impostazione predefinita, il cloud pubblico di Azure usa *cloudapp.net* e Cloud Management Gateway è ospitato all'interno del dominio cloudapp.net come *\<NomeDNSUnivoco >.cloudapp.net*.  

> [!TIP]  
> In questa esercitazione il **certificato di autenticazione server di Cloud Management Gateway** usa un FQDN che termina con *contoso.com*.  Dopo aver creato il servizio Cloud Management Gateway, verrà configurato un record di nome canonico (CNAME) nel DNS pubblico dell'organizzazione. Questo record crea un alias per Cloud Management Gateway di cui viene eseguito il mapping al nome usato nel certificato pubblico.  

Prima di richiedere il certificato pubblico, verificare che il nome che si vuole usare sia disponibile in Azure. Il servizio non viene creato direttamente in Azure. Al contrario, il nome specificato nel certificato pubblico richiesto viene usato da Configuration Manager per creare il servizio cloud quando si installa Cloud Management Gateway.  

1. Accedere al [portale di Microsoft Azure](https://portal.azure.com/).  

2. Selezionare **Crea una risorsa**, scegliere la categoria **Calcolo**, quindi selezionare **Servizio cloud**. Viene aperto il pannello Servizio cloud (versione classica).

3. Per **Nome DNS** specificare il nome del prefisso per il servizio cloud che verrà usato. Questo prefisso deve essere identico a quello usato in seguito quando si richiede un certificato pubblico per il certificato di autenticazione server di Cloud Management Gateway. Viene usato *MyCSG*, che crea lo spazio dei nomi *MyCSG.cloudapp.net*. L'interfaccia conferma se il nome è disponibile o già in uso in un altro servizio.  
 Dopo aver verificato che il nome che si vuole usare è disponibile, è possibile inviare la richiesta di firma del certificato.

### <a name="request-the-certificate"></a>Richiedere il certificato
Usare le informazioni seguenti per inviare un richiesta di firma del certificato per Cloud Management Gateway a un provider di certificati pubblici. Modificare i valori seguenti in base a quelli pertinenti per l'ambiente.  

- *MyCMG* per identificare il nome del servizio di Cloud Management Gateway
- *Contoso* come nome della società
- *Contoso.com* come dominio pubblico

È consigliabile usare il server del sito primario per generare richieste di firma del certificato. Quando si ottiene il certificato, è necessario registrarlo nello stesso server che ha generato la richiesta di firma del certificato o non sarà possibile esportare la chiave privata dei certificati, che è un'operazione obbligatoria.  

Richiedere un tipo di provider di chiavi versione 2 quando si genera una richiesta di firma del certificato. Sono supportati solo i certificati versione 2.  

> [!TIP]  
> Quando viene distribuito Cloud Management Gateway, viene installato contemporaneamente anche un punto di distribuzione cloud. Per impostazione predefinita, quando si distribuisce Cloud Management Gateway, l'opzione **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure** è selezionata. La condivisione del percorso del punto di distribuzione cloud nel server con Cloud Management Gateway elimina la necessità di configurazioni e certificati separati per supportare il punto di distribuzione cloud. Anche se il punto di distribuzione cloud non è necessario per l'uso della co-gestione, è utile nella maggior parte degli ambienti.  
>
> Se si intende usare altri punti di distribuzione cloud per la co-gestione, è necessario richiedere certificati separati per ogni server aggiuntivo. Per richiedere un certificato pubblico per il punto di distribuzione cloud, usare gli stessi dettagli usati per la richiesta di firma del certificato di Cloud Management Gateway. È necessario modificare solo il nome comune in modo che sia univoco per ogni punto di distribuzione cloud.  

**Dettagli per la richiesta di firma del certificato di Cloud Management Gateway**
- **Nome comune**: NomeServizioCloudCMG.NomeDominioPubblicoSocietà.com  
Esempio: MyCMG.contoso.com  
- **Nome alternativo soggetto**: identico al nome comune (CN)  
- **Organizzazione**:  nome dell'organizzazione  
- **Reparto**: in base all'organizzazione  
- **Città**: in base all'organizzazione  
- **Stato**: in base all'organizzazione  
- **Paese**: in base all'organizzazione  
- **Dimensione chiave: 2048**  
- **Provider: provider del servizio di crittografia Microsoft RSA SChannel**  

### <a name="import-the-certificate"></a>Importare il certificato
Dopo aver ricevuto il certificato pubblico, importarlo nell'archivio certificati locale del computer in cui è stata creata la richiesta di firma del certificato. Esportare quindi il certificato come file PFX in modo da poterlo usare per Cloud Management Gateway in Azure.  

I provider di certificati pubblici forniscono in genere istruzioni per l'importazione del certificato. Il processo di importazione del certificato dovrebbe essere simile alle linee guida seguenti:  

1. Nel computer in cui deve essere importato il certificato, individuare il file PFX del certificato.  

2. Fare clic con il pulsante destro del mouse sul file e quindi scegliere **Installa PFX**  

3. All'avvio dell'Importazione guidata certificati selezionare **Avanti**.  

4. Nella pagina **File da importare** selezionare **Avanti**. 

5. Nella pagina **Password** immettere la password per la chiave privata nella casella Password e quindi selezionare **Avanti**.  
  
   Selezionare l'opzione per rendere esportabile la chiave.

6. Nella pagina **Archivio certificati** scegliere **Seleziona automaticamente l'archivio certificati secondo il tipo di certificato** e quindi selezionare **Avanti**.  

7.  Selezionare **Fine**.

### <a name="export-the-certificate"></a>Esportare il certificato
Esportare il *certificato di autenticazione server di Cloud Management Gateway* dal server. La riesportazione del certificato ne permette l'utilizzo per Cloud Management Gateway in Azure.  

1. Nel server in cui è stato importato il certificato SSL pubblico, eseguire **certlm.msc** per aprire la console di Gestione certificati.  

2. Nella console di Gestione certificati selezionare **Personale > Certificati**. Quindi, fare clic con il pulsante destro del mouse sul *certificato di autenticazione server di Cloud Management Gateway* registrato nella procedura precedente e quindi selezionare **Tutte le attività > Esporta**.  

3. Nell'Esportazione guidata certificati selezionare **Avanti**, selezionare **Sì, esporta la chiave privata** e quindi scegliere **Avanti**.  

4. Nella pagina Formato file di esportazione selezionare **Personal Information Exchange - PKCS #12 (.PFX)**, selezionare **Avanti** e specificare una password. Per il nome del file specificare un nome simile a **C:\ConfigMgrCloudMGServer**. Si farà riferimento a questo file quando si creerà il servizio Cloud Management Gateway in Azure.  

5. Selezionare **Avanti** e quindi verificare le impostazioni seguenti prima di selezionare **Fine** per completare l'esportazione:  

   - Esporta chiavi = Sì  
   - Includi tutti i certificati nel percorso di certificazione = Sì  
   - Formato file = Personal Information Exchange (*.pfx)  

6. Dopo aver completato l'esportazione, individuare il file PFX e inserirne una copia in **C:\Certs** nel server del sito primario di Configuration Manager che gestirà i client basati su Internet. La cartella Certs è una cartella temporanea da usare per lo spostamento di certificati tra server. È possibile accedere al file di certificato dal server del sito primario quando si distribuisce Cloud Management Gateway in Azure.  

Dopo aver copiato il certificato nel server del sito primario, è possibile eliminare il certificato dall'archivio certificati personali nel server membro. 


## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Abilitare i servizi cloud di Azure in Configuration Manager
Per configurare i servizi di Azure dalla console di Configuration Manager, è necessario usare la procedura guidata Configura i servizi di Azure e creare due app in Azure Active Directory (Azure AD).  

- **App server**: *app Web* in Azure AD  
- **App client**: app *client nativa* in Azure AD  

Completare la procedura seguente dal server del sito primario.  

1. Dal server del sito primario aprire la console di Configuration Manager e passare a **Amministrazione > Servizi cloud > Servizi di Azure** e quindi selezionare **Configura i servizi di Azure**.  

   Nella pagina Configura i servizi di Azure specificare un nome descrittivo per il servizio di gestione cloud che si sta configurando. Ad esempio: *Servizio di gestione cloud*   

   Selezionare **Gestione cloud** e quindi **Avanti**.  
   
   > [!TIP]  
   > Per altre informazioni sulle configurazioni eseguite nella procedura guidata, vedere [Avviare la procedura guidata per i servizi di Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)


2. Nella pagina **Proprietà dell'app** per **App Web** selezionare **Sfoglia** per aprire la finestra di dialogo **App server** e quindi selezionare **Crea**. Configurare i campi seguenti:

   - **Nome applicazione**: Specificare un nome descrittivo per l'app, ad esempio *App Web gestione cloud*.  

   - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è obbligatorio per Azure AD. Per impostazione predefinita, questo valore è https://ConfigMgrService.  
   
   - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è https://ConfigMgrService.  

   Selezionare quindi **Accedi** e specificare un account amministratore globale di Azure. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure. 

   Dopo l'accesso, vengono visualizzati i risultati. Selezionare **OK** per chiudere la finestra di dialogo Crea un'applicazione server e tornare alla pagina Proprietà dell'app. 

3. Per **App client nativa** selezionare **Sfoglia** per aprire la finestra di dialogo **App client**. 

4. Selezionare **Crea** per aprire la finestra di dialogo **Crea un'applicazione client** e quindi configurare i campi seguenti:  

   - **Nome applicazione**: Specificare un nome descrittivo per l'app, ad esempio *App client nativa di gestione*.
   
   - **URL di risposta**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è https://ConfigMgrClient.
   Selezionare quindi **Accedi** e specificare un account amministratore globale di Azure. Come per l'app Web, queste credenziali non vengono salvate e non richiedono autorizzazioni in Configuration Manager.
   
   Dopo l'accesso, vengono visualizzati i risultati. Selezionare **OK** per chiudere la finestra di dialogo Crea un'applicazione client e tornare alla pagina Proprietà dell'app. Selezionare quindi **Avanti** per continuare.

5. Nella pagina **Configura le impostazioni di individuazione** selezionare la casella di controllo **Abilita l'individuazione utente di Azure Active Directory**, selezionare **Avanti**e quindi completare la configurazione delle finestre di dialogo di individuazione per l'ambiente.  

6. Continuare con le pagine Riepilogo, Avanzamento e Completamento e quindi chiudere la procedura guidata.  

   I servizi di Azure per l'individuazione utente di Azure AD sono ora abilitati in Configuration Manager.  Lasciare aperta la console a questo punto.  

7. Aprire un browser e accedere al [portale di Azure](https://portal.azure.com/).  

8. Selezionare **Tutti i servizi > Azure Active Directory > Registrazioni per l'app** e quindi:

   1. Selezionare l'app Web creata. 

   2. Passare a **Impostazioni > Autorizzazioni necessarie**, selezionare **Concedi autorizzazioni** e quindi **Sì**.  

   3. Selezionare l'app client nativa creata. 

   4. Passare a **Impostazioni > Autorizzazioni necessarie**, selezionare **Concedi autorizzazioni** e quindi **Sì**.  

9. Nella console di Configuration Manager passare a **Amministrazione > Panoramica > Servizi cloud > Servizi di Azure** e quindi selezionare il servizio di Azure. Fare clic con il pulsante destro del mouse su **Individuazione di utenti di Azure Active Directory** e scegliere **Esegui individuazione completa**. Selezionare **Sì** per confermare l'azione.  

10. Nel server del sito primario aprire il file **SMS_AZUREAD_DISCOVERY_AGENT.log** di Configuration Manager e cercare la voce seguente per verificare che l'individuazione funzioni correttamente:  *Successfully published UDX for Azure Active Directory users*  

    Per impostazione predefinita, il file di log si trova in *%Program_Files%\Microsoft Configuration Manager\Logs*.  


## <a name="create-the-cloud-services-in-azure"></a>Creare i servizi cloud in Azure
**In questa sezione dell'esercitazione si apprenderà come**:
- Creare il servizio cloud Cloud Management Gateway  
- Creare record CNAME DNS per entrambi i servizi  

### <a name="create-the-cmg"></a>Creare il servizio Cloud Management Gateway
Usare questa procedura per installare Cloud Management Gateway come servizio in Azure. Cloud Management Gateway viene installato nel sito di livello superiore della gerarchia. In questa esercitazione si continuerà a usare il sito primario in cui sono stati registrati ed esportati i certificati.

1. Nel server del sito primario aprire la console di Configuration Manager, passare a **Amministrazione > Panoramica > Servizi cloud > Cloud Management Gateway** e quindi selezionare **Crea un gateway di gestione cloud**.  

2. Nella pagina **Generale**:  

   1. Selezionare l'ambiente cloud per **Ambiente di Azure**. Questa esercitazione usa **AzurePublicCloud**.  
   
   2. Selezionare **Distribuzione di Azure Resource Manager**.  
  
   3. Fare clic su **Accedi** per accedere alla sottoscrizione di Azure. Configuration Manager immette informazioni aggiuntive in base ai dati configurati durante l'abilitazione dei servizi cloud di Azure per Configuration Manager.  

   Selezionare **Avanti** per continuare.  

3. Nella pagina **Impostazioni** individuare e selezionare il file denominato **ConfigMgrCloudMGServer.pfx**, che è il file esportato dopo l'importazione del certificato di autenticazione server di Cloud Management Gateway. Dopo aver specificato la password, i campi **Nome servizio** e **Nome distribuzione** verranno completati automaticamente in base ai dettagli inclusi nel file di certificato PFX. 

4. Specificare l'area in **Area**.

5. Per **Gruppo di risorse** usare un gruppo di risorse esistente o crearne uno nuovo con un nome descrittivo privo di spazi, ad esempio **ServiziCloudConfigMgr**. Se si sceglie di creare un gruppo, il gruppo viene aggiunto come gruppo di risorse in Azure.  

6. A meno che non si sia pronti per una configurazione su larga scala, usare uno (1) come numero di **istanze di macchina virtuale**. Il numero di istanze di macchina virtuale permette a un singolo servizio cloud Cloud Management Gateway di ampliare un livello di servizio per supportare più connessioni client. In seguito, sarà possibile usare la console di Configuration Manager per modificare il numero di istanze di macchina virtuale usate.  

7. Selezionare la casella di controllo **Verifica la revoca del certificato client**. 

8. Selezionare la casella di controllo **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure** se si vuole distribuire un punto di distribuzione cloud con Cloud Management Gateway.

9. Selezionare **Avanti** per continuare.

10. Esaminare i valori nella pagina **Avviso** e quindi selezionare **Avanti**.

11. Esaminare la pagina **Riepilogo** e fare clic su **Avanti** per creare il servizio cloud Cloud Management Gateway. Selezionare **Chiudi** per completare la procedura guidata.  

12. Nel nodo Cloud Management Gateway della console di Configuration Manager è ora possibile visualizzare il nuovo servizio.  

### <a name="create-dns-cname-records"></a>Creare record CNAME DNS

Quando si crea una voce DNS per Cloud Management Gateway, si consente ai dispositivi Windows 10 sia all'interno sia all'esterno della rete aziendale di usare la risoluzione dei nomi per trovare il servizio cloud Cloud Management Gateway in Azure.

L'esempio di record CNAME usa i dettagli seguenti:  

- Il nome della società è **Contoso** con uno spazio dei nomi DNS pubblico ***Contoso.com***.  

- Il nome del servizio Cloud Management Gateway è **MyCMG**, che diventa ***MyCMG.CloudApp.Net*** in Azure.  

Esempio di record CNAME: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configurare il punto di gestione e i client per usare Cloud Management Gateway
Configurare le impostazioni che permettono ai punti di gestione locali e ai client di usare Cloud Management Gateway. 

Poiché si usa HTTP avanzato per le comunicazioni client, non è necessario usare un punto di gestione HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Aggiungere il punto di connessione di Cloud Management Gateway
Configurare il sito per supportare HTTP avanzato.  

1. Nella console di Configuration Manager passare a **Amministrazione > Panoramica > Configurazione del sito > Siti** e aprire le proprietà del sito primario.  

2. Nella scheda **Comunicazione computer client** selezionare l'opzione *HTTPS o HTTP* per **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP** e quindi selezionare **OK** per salvare la configurazione. 

3. Passare ora a **Amministrazione > Panoramica > Configurazione del sito > Server e ruoli del sistema del sito** e selezionare il server con un punto di gestione in cui si vuole installare il punto di connessione di Cloud Management Gateway.  

4. Selezionare **Aggiungi ruoli del sistema del sito**e quindi **Avanti**> **Avanti**.  

5. Selezionare **Punto di connessione del gateway di gestione cloud** e quindi selezionare **Avanti** per continuare.  

6. Esaminare le opzioni predefinite nella pagina **Punto di connessione del gateway di gestione cloud** e assicurarsi che sia selezionato il servizio Cloud Management Gateway corretto. Se sono presenti più servizi Cloud Management Gateway, è possibile usare l'elenco a discesa per specificarne uno diverso. Dopo l'installazione, è anche possibile modificare il servizio Cloud Management Gateway in uso. Selezionare **Avanti** per continuare.

7. Selezionare **Avanti** per avviare l'installazione e quindi visualizzare i risultati nella pagina Completamento.  Selezionare **Chiudi** per completare l'installazione del punto di connessione. 

8. Passare ora a **Amministrazione > Panoramica > Configurazione del sito > Server e ruoli del sistema del sito** e aprire la pagina **Proprietà** per il punto di gestione in cui è stato installato il punto di connessione. Nella scheda **Generale**selezionare la casella di controllo accanto a **Consenti il traffico del gateway di gestione cloud di Configuration Manager** e quindi selezionare **OK** per salvare la configurazione. 
   > [!TIP]  
   > Benché non sia necessario per abilitare la co-gestione, è consigliabile apportare questa stessa modifica per qualsiasi punto di aggiornamento software. 

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Configurare le impostazioni client per indirizzare i client a usare Cloud Management Gateway
Usare le impostazioni client per configurare i client di Configuration Manager in modo da comunicare con Cloud Management Gateway.  

1. Aprire **Console di Configuration Manager > Amministrazione > Panoramica > Impostazioni client** e quindi modificare i valori in **Impostazioni client predefinite**.  

2. Selezionare **Servizi cloud**.

3. Nella pagina **Impostazioni predefinite** configurare le impostazioni seguenti su **Sì**  

   - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory**  

   - **Consenti ai client di usare un gateway di gestione cloud** 

   - **Consentire accesso al punto di distribuzione cloud** 

4. Nella pagina **Criteri client** impostare **Abilitare le richieste dei criteri utente dai client Internet** = **Sì** 

1. Selezionare **OK** per salvare la configurazione. 



## <a name="enable-co-management-in-configuration-manager"></a>Abilitare la co-gestione in Configuration Manager
Dopo aver predisposto le configurazioni di Azure, i ruoli del sistema del sito e le impostazioni client, è possibile configurare Configuration Manager per abilitare la co-gestione. Tuttavia, è ancora necessario eseguire alcune configurazioni in Intune dopo aver abilitato la co-gestione prima che questa esercitazione sia completa. Una di queste attività consiste nel configurare Intune per la distribuzione del client di Configuration Manager. Questa attività viene semplificata salvando la riga di comando per la distribuzione client disponibile nella Configurazione guidata della co-gestione. Ecco perché è necessario abilitare la co-gestione a questo punto, prima di completare le configurazioni per Intune. 

> [!TIP]  
>  Nel sesto passaggio della procedura seguente si assegnerà una raccolta come *gruppo pilota* per la co-gestione. Si tratta di un gruppo che contiene un numero ridotto di client per testare le configurazioni di co-gestione. È consigliabile creare una raccolta appropriata prima di avviare la procedura. È quindi possibile selezionare la raccolta senza chiudere la procedura a questo scopo.  
 
1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).

2. Nel gruppo Gestisci della scheda Home selezionare **Configura la co-gestione** per aprire la Configurazione guidata della co-gestione.

3. Nella pagina *Sottoscrizione* fare clic su **Accedi**, accedere al tenant di Intune e quindi selezionare **Avanti**.

4. Nella pagina *Abilitazione* selezionare una delle opzioni seguenti nell'elenco a discesa *Registrazione automatica in Intune*:  

   - **Pilota**  - *(scelta consigliata)* I membri della raccolta specificata vengono automaticamente registrati in Intune e possono quindi essere co-gestiti. La raccolta pilota viene specificata nella pagina *Gestione temporanea* di questa procedura guidata. Questa opzione permette di testare la co-gestione in un subset di client. È quindi possibile implementare la co-gestione in altri client usando un approccio in fasi.  

   - **Tutti** - La co-gestione è abilitata per tutti i client.  

   Prima di passare alla pagina successiva della procedura guidata, selezionare **Copia** e salvare la riga di comando CCMSetup fornita. La riga di comando verrà usata in seguito, per la configurazione di Intune per distribuire il client di Configuration Manager. Se non si salva la riga di comando a questo punto, sarà possibile esaminare la co-gestione in qualsiasi momento per ottenere la riga di comando. 

5. Nella pagina *Carichi di lavoro* è possibile spostare i carichi di lavoro da **Configuration Manager** a una delle destinazioni seguenti e quando si è pronti per continuare, selezionare **Avanti**.  
   
   - **Intune pilota** - Sposta un carico di lavoro solo per i dispositivi presenti nel gruppo pilota. È possibile assegnare una raccolta come gruppo pilota nella pagina successiva della procedura guidata.  
   
   - **Intune** - Sposta il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti.  

   Non è necessario spostare alcun carico di lavoro al momento dell'abilitazione della co-gestione. È possibile tornare a questa configurazione dalla console di Configuration Manager in seguito, dopo la configurazione della co-gestione.  

   Prima di spostare un carico di lavoro, assicurarsi che il carico di lavoro corrispondente in Intune sia stato configurato e distribuito. In questo modo, i carichi di lavoro vengono mantenuti gestiti.  

6. Nella pagina *Gestione temporanea* specificare una raccolta da usare per **Raccolta pilota** e quindi fare clic su **Avanti**. La raccolta specificata viene usata come parte dell'implementazione in fasi della co-gestione. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento dalle proprietà della co-gestione.  

7. Nella pagina *Riepilogo* selezionare **Avanti** e quindi **Chiudi** per completare la procedura guidata.  

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Usare Intune per distribuire il client di Configuration Manager
È possibile usare Intune per installare il client di Configuration Manager nei dispositivi Windows 10 che sono attualmente gestiti solo con Intune.  

Quindi, quando un dispositivo Windows 10 precedentemente non gestito viene registrato con Intune, installa automaticamente il client di Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Creare un'app di Intune per installare il client di Configuration Manager

1. Dal server del sito primario accedere al [portale di Azure](https://portal.azure.com/) e passare a **Intune > App client > App > Aggiungi**.

2. Per **Tipo di app**: selezionare **App line-of-business**.

3. Selezionare **File del pacchetto dell'app**, passare al percorso del file di Configuration Manager **ccmsetup.msi** e quindi selezionare **Apri > OK**.
Ad esempio, *C:\Programmi\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   

4. Selezionare **Informazioni sull'app** e quindi specificare i dettagli seguenti:
   - **Descrizione**: Configuration Manager Client  

   - **Editore**: Microsoft  

   - **Argomenti della riga di comando**:  *\<specificare la riga di comando **CCMSETUPCMD**. È possibile usare la riga di comando salvata dalla pagina* Abilitazione *della Configurazione guidata della co-gestione. Questa riga di comando include i nomi del servizio cloud e altri valori, che permettono ai dispositivi di installare il software client di Configuration Manager.>*  

     La struttura della riga di comando dovrebbe essere simile a questo esempio, usando solo i parametri CCMSETUPCMD e SMSSiteCode:  
 
         CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  

     > [!TIP]  
     > Se la riga di comando non è disponibile, è possibile visualizzare le proprietà di *CoMgmtSettingsProd* nella console di Configuration Manager per ottenere una copia della riga di comando.    

5. Selezionare **OK > Aggiungi**.  L'app viene creata ed è ora disponibile nella console di Intune. Quando l'app è disponibile, è possibile usare la sezione seguente per configurare Intune in modo da assegnarla ai dispositivi Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Assegnare l'app di Intune per installare il client di Configuration Manager
La procedura seguente distribuisce l'app per l'installazione del client di Configuration Manager creato nella procedura precedente. 

1. Accedere al [portale di Azure](https://portal.azure.com/).  Selezionare **Tutti i servizi > Intune > App client > App** e quindi selezionare **ConfigMgr Client Setup Bootstrap**, l'app creata per distribuire il client di Configuration Manager.  

2. Selezionare **Assegnazioni > Aggiungi gruppo**.  Impostare **Tipo di assegnazione** su **Richiesto**e quindi usare **Gruppi inclusi** e **Gruppi esclusi** per impostare i gruppi di Azure Active Directory (AD) che includono gli utenti e i dispositivi che dovranno partecipare alla co-gestione.  

3. Selezionare **OK** e quindi **Salva** per salvare la configurazione.
L'app viene ora richiesta dagli utenti e dai dispositivi cui è stata assegnata. Dopo che l'app installa il client di Configuration Manager in un dispositivo, questo viene gestito tramite la co-gestione.

## <a name="assign-intune-licenses-to-users"></a>Assegnare le licenze di Intune agli utenti   
Un'azione in genere trascurata ma cruciale è l'assegnazione di una licenza di Intune a ogni utente che usa un dispositivo co-gestito.  

Per assegnare licenze a gruppi di utenti, usare Azure Active Directory.  

1. Accedere al [portale di Azure](https://portal.azure.com/) con un account amministratore. Per gestire le licenze, l'account deve essere un ruolo Amministratore globale o un amministratore account utente.  

2. Selezionare **Tutti i servizi** nel riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**.  

3. Nel riquadro **Azure Active Directory** selezionare **Licenze** per aprire un riquadro in cui è possibile visualizzare e gestire tutti i prodotti soggetti a licenza nel tenant.  
 
4. In **Tutti i prodotti** selezionare l'opzione di prodotto che include la licenza di Intune e quindi selezionare **Assegna** nella parte superiore del riquadro.  

   Ad esempio, è possibile selezionare **Enterprise Mobility + Security E5** se è questo lo strumento tramite cui si ottiene Intune.  

5. Nel riquadro **Assegna licenza** fare clic su **Utenti e gruppi** per aprire il riquadro **Utenti e gruppi**. Selezionare i gruppi e i singoli utenti cui si vuole assegnare una licenza.  Fare quindi clic su **Seleziona** nella parte inferiore del riquadro per confermare la selezione.  

6. Nel riquadro **Assegna licenza** fare clic su **Opzioni di assegnazione** per visualizzare tutti i piani di servizio inclusi nel prodotto selezionato in precedenza. Se è stato selezionato un singolo prodotto come Intune, viene visualizzato solo tale prodotto.  
   - Impostare **Microsoft Intune** su **Attivato**.  
   - Assegnare a ogni utente una licenza per **Azure Active Directory Premium**.  

   Una volta assegnate le licenze applicabili, selezionare **OK**.  

7. Per completare l'assegnazione, nel riquadro **Assegna licenza** fare clic su **Assegna** nella parte inferiore del riquadro.  

8. Viene visualizzata una notifica nell'angolo superiore destro che mostra lo stato e il risultato del processo. Se non è stato possibile completare l'assegnazione al gruppo (ad esempio a causa di licenze già esistenti nel gruppo), fare clic sulla notifica per visualizzare i dettagli dell'errore. 


## <a name="summary"></a>Riepilogo 
Dopo aver completato i passaggi di configurazione di questa esercitazione, inclusa l'ultima operazione per garantire l'assegnazione delle licenze, i dispositivi possono essere co-gestiti. 

## <a name="next-steps"></a>Passaggi successivi
- Esaminare lo stato dei dispositivi co-gestiti con il [dashboard di co-gestione](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard)
- Usare [Windows Autopilot]() per effettuare il provisioning di nuovi dispositivi
- Usare l'[accesso condizionale](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access) e le regole di conformità di Intune per gestire l'accesso utente alle risorse aziendali
