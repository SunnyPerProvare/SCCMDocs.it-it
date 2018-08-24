---
title: Distribuire i client in Windows
titleSuffix: Configuration Manager
description: Informazioni su come distribuire il client di Configuration Manager in computer Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6eaac644b876fa3adfa1a2c79e7c4c5810942d9f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385576"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Come distribuire i client nei computer Windows in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo fornisce informazioni dettagliate su come distribuire il client di Configuration Manager in computer Windows. Per altre informazioni su come pianificare e preparare la distribuzione dei client, vedere gli articoli seguenti:
- [Metodi di installazione client](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Prerequisiti per la distribuzione dei client nei computer Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Sicurezza e privacy per i client di Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [Procedure consigliate per la distribuzione di client](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> Installazione push client 

Sono disponibili tre modi principali per usare il push client:  

- Quando si configura l'installazione push client per un sito, l'installazione client viene eseguita automaticamente nei computer individuati dal sito. Questo metodo è circoscritto ai limiti configurati del sito quando tali limiti sono configurati come un gruppo di limiti.  

- Per avviare l'installazione push client, eseguire l'Installazione guidata push client per una raccolta specifica o una risorsa all'interno di una raccolta.  

- Usare l'Installazione guidata push client per installare il client di Configuration Manager nei risultati ottenuti da una [query](/sccm/core/servers/manage/queries-technical-reference). Affinché l'installazione abbia esito positivo, uno degli elementi restituiti dalla query deve essere l'attributo **ResourceID** dalla classe **Risorse di sistema**.   

Se il server del sito non può contattare il computer client o avviare il processo di installazione, ripete automaticamente il tentativo di installazione ogni ora, per sette giorni.  

Per tenere traccia del processo di installazione client, installare un punto di stato di fallback prima di installare i client. Quando viene installato un punto di stato di fallback, esso viene assegnato automaticamente ai client quando vengono installati con il metodo di installazione push client. Per tenere traccia dello stato di installazione client, visualizzare i report di assegnazione e distribuzione client. 

I file di log del client contengono informazioni più dettagliate per la risoluzione dei problemi e non richiedono un punto di stato di fallback. Ad esempio, nel file **CCM.log** nel server del sito vengono registrati tutti i problemi riscontrati dal server del sito durante la connessione al computer. Nel file **CCMSetup** nel client viene registrato il processo di installazione.  

> [!IMPORTANT]  
>  Affinché il push client venga eseguito correttamente, assicurarsi che siano presenti tutti i prerequisiti. Per altre informazioni, vedere [Dipendenze del metodo di installazione](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurare il sito per l'uso automatico del push client per i computer individuati

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Selezionare il sito per cui si vuole configurare l'installazione push client automatica a livello di sito.  

3.  Nella scheda **Home** della barra multifunzione, nel gruppo **Impostazioni** scegliere **Impostazioni di installazione client** e selezionare **Installazione push client**.  

4.  Nella scheda **Generale** della finestra Proprietà installazione push client selezionare **Abilita installazione push client automatica a livello di sito**.   

5. A partire dalla versione 1806, quando si aggiorna il sito viene abilitato un controllo Kerberos per il push client. L'opzione **Consenti il fallback connessione in NTLM** è abilitata per impostazione predefinita, coerentemente con il comportamento precedente. Se il sito non può autenticare il client tramite Kerberos, tenta di eseguire la connessione mediante NTLM. La configurazione consigliata per migliorare la sicurezza consiste nel disabilitare questa impostazione, che richiede l'autenticazione Kerberos senza fallback in NTLM.<!--1358204-->  

    > [!Note]  
    > Quando si usa il metodo di installazione push client per il client di Configuration Manager, il server del sito crea una connessione remota al client. A partire dalla versione 1806, il sito può richiedere l'autenticazione reciproca Kerberos non consentendo il fallback in NTLM prima di stabilire la connessione. Questo miglioramento consente di proteggere la comunicazione tra il server e il client.  
    > 
    > A seconda dei criteri di sicurezza, l'ambiente può già preferire o richiedere l'autenticazione Kerberos rispetto all'autenticazione NTLM meno recente. Per altre informazioni sulle considerazioni relative alla sicurezza per questi protocolli di autenticazione, vedere l'[impostazione dei criteri di sicurezza di Windows per limitare NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    > 
    > Per usare questa funzionalità, i client devono essere in una foresta di Active Directory trusted. Il protocollo Kerberos in Windows si basa su Active Directory per l'autenticazione reciproca.  

6.  Selezionare i tipi di sistema in cui Configuration Manager deve eseguire il push del software client. Specificare se si vuole installare il client nei controller di dominio.  

7.  Nella scheda **Account** specificare uno o più account affinché Configuration Manager li usi durante la connessione al computer di destinazione. Fare clic sull'icona **Crea**, immettere **Nome utente** e **Password** (non più di 38 caratteri), confermare la password e quindi fare clic su **OK**. Specificare almeno un account di installazione push client. Per installare il client, è necessario che questo account abbia i diritti di amministratore locale nel computer di destinazione. Se non si specifica un account di installazione push client, Configuration Manager prova a usare l'account computer di sistema del sito. L'installazione push client tra domini ha esito negativo quando si usa l'account del computer del sistema del sito.  

    > [!NOTE]  
    >  Per usare l'installazione push client da un sito secondario, specificare l'account del sito secondario che avvia l'installazione push client.  
    >   
    >  Per altre informazioni sull'account di installazione push client, vedere la procedura [Usare l'installazione guidata push client](#use-the-client-push-installation-wizard) riportata di seguito.  

8.  Completare la scheda **Proprietà di installazione**.

     Se lo schema di Active Directory è stato esteso per Configuration Manager, il sito pubblica le [proprietà di installazione client](/sccm/core/clients/deploy/about-client-installation-properties) specificate in Active Directory Domain Services. Se CCMSetup viene eseguito senza le proprietà di installazione, esegue la lettura di tali proprietà da Active Directory.  

    > [!NOTE]  
    >  Se si abilita l'installazione push client in un sito secondario, assicurarsi che la proprietà **SMSSITECODE** sia impostata sul codice del sito di Configuration Manager del relativo sito primario padre. Se lo schema di Active Directory è stato esteso per Configuration Manager, impostare questa proprietà su **AUTO** per individuare automaticamente la corretta assegnazione del sito.  


### <a name="use-the-client-push-installation-wizard"></a>Usare l'Installazione guidata push client

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Selezionare il sito per cui si vuole configurare l'installazione push client automatica a livello di sito.  

3.  Nella scheda **Home** della barra multifunzione, nel gruppo **Impostazioni** scegliere **Impostazioni di installazione client** e selezionare **Installazione push client**.  

4.  Completare la scheda **Proprietà di installazione**.  

    Se lo schema di Active Directory è stato esteso per Configuration Manager, il sito pubblica le [proprietà di installazione client](/sccm/core/clients/deploy/about-client-installation-properties) specificate in Active Directory Domain Services. Se CCMSetup viene eseguito senza le proprietà di installazione, esegue la lettura di tali proprietà da Active Directory.   

5.  Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**.  

6.  Nel nodo **Dispositivi** selezionare uno o più computer. In alternativa, selezionare una raccolta di computer nel nodo **Raccolte dispositivi**.  

7.  Nella scheda **Home** della barra multifunzione scegliere una delle opzioni seguenti:  

    -   Per eseguire il push del client in uno o più dispositivi, nel gruppo **Dispositivo** scegliere **Installa client**.  

    -   Per eseguire il push del client in una raccolta di dispositivi, nel gruppo **Raccolta** scegliere **Installa client**.  

8. Nella pagina **Prima di iniziare** dell'Installazione guidata client verificare le informazioni e quindi scegliere **Avanti**.  

9. Completare la pagina **Opzioni di installazione**.  

10. Verificare le impostazioni di installazione, quindi completare la procedura guidata.  

> [!NOTE]  
> È possibile usare la procedura guidata per installare i client anche se il sito non è configurato per il push client.  



##  <a name="BKMK_ClientSUP"></a> Installazione basata sull'aggiornamento software  

L'Installazione client basata sull'aggiornamento software pubblica il client in un punto di aggiornamento software come aggiornamento software. Usare questo metodo per una nuova installazione o un aggiornamento.  

Se in un computer è installato il client di Configuration Manager, tale computer riceve i criteri client dal sito. I criteri includono il nome del server del punto di aggiornamento software e la porta dalla quale ricevere gli aggiornamenti.   

> [!IMPORTANT]  
>  Per usare l'installazione basata sull'aggiornamento software, è necessario usare lo stesso server di Windows Server Update Services (WSUS) per l'installazione client e gli aggiornamenti software. Questo server deve essere il punto di aggiornamento software attivo in un sito primario. Per altre informazioni, vedere [Install a software update point](/sccm/sum/get-started/install-a-software-update-point) (Installare un punto di aggiornamento software).  

Se in un computer non è installato il client di Configuration Manager, configurare e assegnare un oggetto Criteri di gruppo. I Criteri di gruppo specificano il nome del server del punto di aggiornamento software.  

Non è possibile aggiungere proprietà della riga di comando a un'installazione client basata sull'aggiornamento software. Se lo schema di Active Directory è stato esteso a Configuration Manager, l'installazione client esegue automaticamente una query sulle proprietà di installazione in Active Directory Domain Services.  

Se lo schema di Active Directory non è stato esteso, usare Criteri di gruppo per effettuare il provisioning delle impostazioni dell'installazione client. Queste impostazioni vengono applicate automaticamente a tutte le installazioni client basate sull'aggiornamento software. Per altre informazioni, vedere la sezione [Come effettuare il provisioning delle proprietà di installazione client](#BKMK_Provision) e l'articolo [Come assegnare i client a un sito](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Usare le procedure seguenti per configurare i computer senza un client di Configuration Manager per l'uso del punto di aggiornamento software. È inoltre disponibile una procedura per pubblicare il software client nel punto di aggiornamento software.  

> [!Tip]  
>  Se i computer sono in uno stato di riavvio in sospeso in seguito a una precedente installazione software, un'installazione client basata sull'aggiornamento potrebbe causare il riavvio del computer.  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configurare un oggetto Criteri di gruppo per specificare il punto di aggiornamento software  

1.  Usare la **Console Gestione Criteri di gruppo** per aprire un oggetto Criteri di gruppo nuovo o esistente.  

2.  Espandere **Configurazione computer**, **Modelli amministrativi**, **Componenti di Windows** e quindi scegliere **Windows Update**.  

3.  Aprire le proprietà dell'impostazione **Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet** e quindi scegliere **Attivato**.  

4.  **Impostare il servizio di aggiornamento nella rete Intranet per il rilevamento degli aggiornamenti**: specificare il nome e la porta del server del punto di aggiornamento software.  

    -   Se il sistema del sito di Configuration Manager è stato configurato per usare un nome di dominio completo (FQDN), usare questo formato.  

    -   Se il sistema del sito di Configuration Manager non è stato configurato per usare un nome FQDN, usare il formato di nome breve.   

    > [!Tip]  
    >  Per determinare il numero della porta, vedere [Come determinare le impostazioni della porta usate da WSUS](/sccm/sum/plan-design/plan-for-software-updates).  

     Esempio con il formato FQDN: `http://server1.contoso.com:8530`  

5.  **Impostare il server per le statistiche nella rete Intranet**: questa impostazione corrisponde in genere al nome del server.   

6.  Assegnare l'oggetto Criteri di gruppo ai computer in cui si vuole installare il client e ricevere gli aggiornamenti software.  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Pubblicare il client di Configuration Manager nel punto di aggiornamento software  

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Selezionare il sito per cui si vuole configurare l'installazione client basata sull'aggiornamento software.  

3.  Nella scheda **Home** della barra multifunzione, nel gruppo **Impostazioni** scegliere **Impostazioni di installazione client** e quindi scegliere **Installazione client basata sull'aggiornamento software**.  

4.  Selezionare **Abilita installazione client basata su aggiornamento software**.  

5.  Se la versione client del sito è successiva alla versione client del punto di aggiornamento software, verrà visualizzata la finestra di dialogo **Versione più recente del pacchetto client rilevata**. Fare clic su **Sì** per pubblicare la versione più recente.  

    > [!NOTE]  
    >  Se il software client non è già stato pubblicato nel punto di aggiornamento software, questa casella è vuota.  

L'aggiornamento software per il client di Configuration Manager non viene automaticamente aggiornato quando esiste una nuova versione. Quando si aggiorna il sito, ripetere questa procedura per aggiornare il client.  



##  <a name="BKMK_ClientGP"></a> Installazione tramite Criteri di gruppo 

Usare Criteri di gruppo in Active Directory Domain Services per pubblicare o assegnare il client di Configuration Manager. Il client viene installato all'avvio del computer. Quando si usa Criteri di gruppo, il client viene visualizzato in **Installazione applicazioni** nel Pannello di controllo a disposizione dell'utente per eseguire l'installazione.  

Usare il pacchetto di Windows Installer **CCMSetup.ms** per le installazioni basate su Criteri di gruppo. Il file si trova nella cartella `<ConfigMgr installation directory>\bin\i386` nel server del sito. Non è possibile aggiungere proprietà a questo file per modificare il comportamento di installazione.  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client, è necessario disporre delle autorizzazioni di **amministratore**.  

-   Se lo schema di Active Directory è stato esteso per Configuration Manager ed è stata selezionata l'opzione **Publish this site in Active Directory Domain Services** (Pubblica questo sito in Active Directory Domain Services) nella scheda **Avanzate** della finestra di dialogo **Proprietà sito**, i computer client eseguono automaticamente una ricerca in Active Directory Domain Services per individuare le proprietà di installazione. Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  

-   Se lo schema di Active Directory non è stato esteso, per archiviare le proprietà di installazione nel Registro di sistema Windows dei computer, vedere la sezione [Come effettuare il provisioning delle proprietà di installazione client](#BKMK_Provision). Durante l'installazione, il client usa queste proprietà di installazione.  

Per altre informazioni su come usare Criteri di gruppo in Active Directory Domain Services per l'installazione del software, vedere [Utilizzo dei Criteri di gruppo per l'installazione remota del software](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  



##  <a name="BKMK_Manual"></a> Installazione manuale

Installare manualmente il software client nei computer tramite **CCMSetup.exe**. Il programma e i relativi file di supporto si trovano nel server del sito, nella sottocartella **Client** della cartella di installazione di Configuration Manager. Il sito condivide questa cartella con la rete come:  

 `\\<Site Server Name>\SMS_<Site Code>\Client\`  

 dove `<Site Server Name>` è il nome del server del sito primario e `<Site Code>` è il codice del sito primario a cui è assegnato il client. Per eseguire CCMSetup.exe dalla riga di comando nel client, è necessario connettersi a questo percorso di rete e quindi eseguire il comando.  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client, è necessario disporre delle autorizzazioni di **amministratore**.  

CCMSetup.exe copia tutti i prerequisiti necessari nel computer client e chiama il pacchetto di Windows Installer (Client.msi) per installare il client. Non è possibile eseguire Client.msi direttamente.  

Per modificare il comportamento dell'installazione client, specificare le opzioni della riga di comando per CCMSetup.exe e Client.msi. Verificare di aver specificato i parametri di CCMSetup che iniziano con `/` prima di specificare le proprietà di Client.msi. Ad esempio:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

In questo esempio l'installazione client viene eseguita con le opzioni seguenti:  

|Opzione|Descrizione|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Questo parametro di CCMSetup specifica il punto di gestione SMSMP01 per scaricare i file di installazione client richiesti.|  
|`/logon`|Questo parametro di CCMSetup specifica che l'installazione deve essere arrestata se nel computer viene rilevato un client di Configuration Manager esistente.|  
|`SMSSITECODE=AUTO`|Questa proprietà di Client.msi specifica che il client cerca di individuare il codice del sito di Configuration Manager da usare, ad esempio usando Active Directory Domain Services.|  
|`FSP=SMSFP01`|La proprietà Client.msi specifica che il punto di stato di fallback denominato SMSFP01 viene usato per ricevere i messaggi di stato inviati dal computer client.|  

 Per altre informazioni vedere [Proprietà e parametri di installazione client](/sccm/core/clients/deploy/about-client-installation-properties).  

> [!Tip]  
> Per conoscere la procedura di installazione del client di Configuration Manager in un dispositivo Windows 10 moderno usando un'identità di Azure AD, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Tale procedura è riservata ai client sulla Intranet o su Internet.  


### <a name="manual-installation-examples"></a>Esempi di installazione manuale

Questi esempi sono specifici per client aggiunti ad Active Directory sulla Intranet. Usano i valori seguenti:  

- **MPSERVER**: server che ospita il punto di gestione   
- **FSPSERVER**: server che ospita il punto di stato di fallback  
- **ABC**: codice del sito  
- **contoso.com**: nome di dominio  

Tutti i server del sistema del sito sono stati configurati con un FQDN Intranet. Le informazioni del sito sono state pubblicate in Active Directory.  

Eseguire queste procedure nel computer client:  
1. Eseguire l'accesso come amministratore locale  
2. Eseguire il mapping dell'unità Z: a `\\MPSERVER\SMS_ABC\Client`  
3. Nel prompt dei comandi passare all'unità Z:  

Eseguire quindi uno di questi comandi:  


#### <a name="manual-example-1"></a>Esempio manuale 1  

`CCMSetup.exe`  

Questo esempio mostra come installare il client senza parametri o proprietà aggiuntive. Il client viene configurato automaticamente con le proprietà di installazione client pubblicate in Active Directory Domain Services, incluse le impostazioni seguenti:  

- Codice del sito: per questa impostazione è necessario includere il percorso di rete del client in un gruppo di limiti configurato per l'assegnazione del client.  
- Punto di gestione
- Punto di stato di fallback
- Comunicare solo tramite HTTPS  

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  


#### <a name="manual-example-2"></a>Esempio manuale 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
In questo esempio viene eseguito l'overrride della configurazione automatica disponibile in Active Directory Domain Services. In questo caso non è necessario includere il percorso di rete del client in un gruppo di limiti configurato per l'assegnazione del client. Al contrario, è l'installazione a specificare le impostazioni seguenti:
- Codice sito
- Punto di gestione Intranet 
- Punto di gestione basato su Internet
- Punto di stato di fallback che accetta connessioni Internet
- Usare un certificato client PKI con il periodo di validità più lungo  



##  <a name="BKMK_ClientLogonScript"></a> Installazione tramite script di accesso

Configuration Manager supporta gli script di accesso per installare il software client di Configuration Manager. Usare il file di programma **CCMSetup.exe** in uno script di accesso per attivare l'installazione client.  

L'installazione con script di accesso usa gli stessi metodi dell'installazione client manuale. Specificare il parametro di installazione `/logon` per CCMSsetup.exe. Se nel computer esiste già una versione del client, questo parametro impedisce l'installazione del client. In questo modo è possibile evitare la reinstallazione del client ogni volta che viene eseguito lo script di accesso.  

Se non viene specificata un'origine dell'installazione con il parametro `/Source` né viene specificato un punto di gestione da cui ottenere l'installazione usando il parametro `/MP`, CCMSetup.exe individua il punto di gestione eseguendo una ricerca in Active Directory Domain Services. Questo comportamento si verifica solo se lo schema è stato esteso per Configuration Manager e il sito è pubblicato in Active Directory Domain Services. In alternativa, il client può usare DNS o WINS per individuare un punto di gestione.  



##  <a name="BKMK_ClientApp"></a> Installazione di pacchetto e programma  

Usare Configuration Manager per creare e distribuire un pacchetto e un programma di aggiornamento per il software client per i dispositivi selezionati. Con Configuration Manager viene fornito un file di definizione del pacchetto che popola le proprietà del pacchetto con i valori tipici. Per personalizzare il comportamento dell'installazione del client, specificare i parametri e le proprietà della riga di comando aggiuntivi.  

> [!NOTE]  
>  Non è possibile aggiornare i client di Configuration Manager 2007 con questo metodo. Usare invece l'aggiornamento automatico del client, che crea e distribuisce automaticamente un pacchetto contenente la versione più recente del client. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients).  
>   
>  Per altre informazioni sulla migrazione da versioni precedenti del client di Configuration Manager, vedere [Pianificare una strategia di migrazione client](/sccm/core/migration/planning-a-client-migration-strategy).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Creare un pacchetto e un programma per il software client  

Usare la procedura seguente per creare un pacchetto e un programma di Configuration Manager che possa essere distribuito nei computer client di Configuration Manager per aggiornare il software client.  

1.  Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2.  Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Crea pacchetto da definizione**.  

3.  Nella pagina **Definizione pacchetto** della creazione guidata selezionare **Microsoft** nell'elenco a discesa **Autore** e selezionare **Aggiornamento client di Configuration Manager** nell'elenco **Definizione pacchetto**.  

4.  Nella pagina **File di origine** selezionare **Reperisci sempre i file di origine da una cartella di origine**.  

5.  Nella pagina **Cartella di origine** selezionare **Percorso di rete (nome UNC)**. A questo punto immettere il percorso di rete del server e della condivisione che contiene i file di installazione del client.  

    > [!NOTE]  
    >  Il computer in cui è in esecuzione la distribuzione di Configuration Manager deve avere accesso alla cartella di rete specificata. In caso contrario, l'installazione del client ha esito negativo.  

    Per cambiare una proprietà di installazione client, è possibile modificare la riga di comando CCMSetup.exe nella scheda **Generale** della finestra di dialogo del programma **Aggiornamento automatico dell'agente di Configuration Manager - Proprietà**. Le proprietà di installazione predefinite sono `/noservice SMSSITECODE=AUTO`.  

6. Distribuire il pacchetto a tutti i punti di distribuzione in cui si desidera venga ospitato il pacchetto di aggiornamento client. Distribuire quindi il pacchetto nelle raccolte di dispositivi contenenti i client da aggiornare.  



## <a name="bkmk_mdm"></a> Dispositivi Windows gestiti da MDM Intune

Distribuire il client di Configuration Manager nei dispositivi registrati con Microsoft Intune. 

Questa procedura è valida per un client tradizionale connesso alla Intranet. Usa i metodi di autenticazione client tradizionali. Per garantire che il dispositivo rimanga in uno stato gestito dopo l'installazione del client, il dispositivo deve essere nella rete Intranet e all'interno di un limite del sito di Configuration Manager.  

Per conoscere la procedura di installazione del client di Configuration Manager in un dispositivo Windows 10 moderno usando un'identità di Azure AD, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]  
> Per impostazione predefinita, dopo l'installazione del software client, la registrazione del dispositivo con Intune viene annullata.
> 
> A partire dalla versione 1710, la registrazione dei client con Intune non viene annullata. È possibile avere sia il client di Configuration Manager sia la registrazione MDM nello stesso momento. Per altre informazioni, vedere la [panoramica di co-gestione](/sccm/core/clients/manage/co-management-overview).  


###  <a name="install-clients-with-intune"></a>Installare i client con Intune  

1. In Intune [aggiungere un'app line-of-business di Windows](https://docs.microsoft.com/intune/lob-apps-windows) contenente il file di installazione client di Configuration Manager **ccmsetup.msi**. Il file è disponibile nella cartella seguente nel server del sito: `<ConfigMgr installation directory>\bin\i386`  

2. In Autore del software Microsoft Intune immettere i parametri della riga di comando. Ad esempio, usare la riga di comando seguente con un client tradizionale sulla Intranet:  

  `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<Your site code> DNSSUFFIX=<DNS Suffix of management point>"`  

   > [!Note]  
   > Per una riga di comando di esempio da usare con un client Windows 10 moderno che usa l'autenticazione di Azure AD, vedere [Preparare i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).  

3. [Assegnare l'app](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune) a un gruppo di computer Windows registrati.  



##  <a name="BKMK_ClientImage"></a> Installazione dell'immagine del sistema operativo

Preinstallare il client di Configuration Manager in un computer di riferimento da usare per creare un'immagine del sistema operativo.   

> [!Important]  
> Quando si usa la sequenza di attività di Configuration Manager per distribuire l'immagine del sistema operativo, il passaggio [Prepara Client ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) rimuove completamente il client di Configuration Manager.  


### <a name="prepare-the-client-computer-for-imaging"></a>Preparare il computer client per la creazione dell'immagine  

1.  Installare manualmente il software client di Configuration Manager nel computer di riferimento. Per altre informazioni, vedere [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Non specificare un codice sito di Configuration Manager per il client nelle proprietà della riga di comando CCMSetup.exe.  

2.  In un prompt dei comandi digitare `net stop ccmexec` per arrestare il servizio **Host agenti di SMS** (Ccmexec.exe) nel computer di riferimento.  

3.  Eliminare il file **SMSCFG.INI** dalla cartella **Windows** nel computer di riferimento.  

4.  Rimuovere i certificati memorizzati nell'archivio del computer locale nel computer di riferimento. Ad esempio, se si usano certificati di infrastruttura a chiave pubblica (PKI), è necessario rimuovere i certificati nell'archivio **Personale** per **Computer** e **Utente** prima di creare l'immagine del computer.  

5.  Se i client sono installati in una gerarchia di Configuration Manager diversa rispetto al computer di riferimento, rimuovere la chiave radice attendibile dal computer di riferimento.  

    > [!NOTE]  
    >  Se i client non possono eseguire query in Active Directory Domain Services per individuare un punto di gestione, usano la chiave radice attendibile per determinare i punti di gestione attendibili. Se tutti i client creati da un'immagine vengono distribuiti nella stessa gerarchia del computer master, non rimuovere la chiave radice attendibile. 
    > 
    > Se i client vengono distribuiti in gerarchie diverse, rimuovere la chiave radice attendibile. Effettuare anche il provisionig di questi client con la nuova chiave radice attendibile. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

6.  Usare il software di creazione delle immagini per acquisire un'immagine del computer di riferimento.  

7.  Distribuire l'immagine ai computer di destinazione.  



##  <a name="BKMK_ClientWorkgroup"></a> Computer del gruppo di lavoro  

Configuration Manager supporta l'installazione di client per i computer nei gruppi di lavoro. Installare il client nei computer del gruppo di lavoro usando il metodo specificato in [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  


### <a name="prerequisites"></a>Prerequisiti  

-   Installare manualmente il client in ogni computer del gruppo di lavoro. Durante l'installazione, l'utente interattivo deve disporre dei diritti di amministratore locale.  

-   Per accedere alle risorse nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso alla rete per il sito. Specificare questo account nel componente del sito di distribuzione software. Per altre informazioni, vedere [Componenti del sito](/sccm/core/servers/deploy/configure/site-components).  


### <a name="limitations"></a>Limitazioni  

-   I client del gruppo di lavoro non possono individuare i punti di gestione da Active Directory Domain Services. Usano invece i servizi DNS, WINS o un altro punto di gestione.  

-   Il roaming globale non è supportato. I client del gruppo di lavoro non possono eseguire query in Active Directory Domain Services per acquisire informazioni sul sito.  

-   I metodi di individuazione di Active Directory non sono in grado di individuare i computer nei gruppi di lavoro.  

-   Non è possibile distribuire software agli utenti dei computer del gruppo di lavoro.  

-   Non è possibile usare il metodo di installazione push client per installare il client nei computer del gruppo di lavoro.  

-   I client del gruppo di lavoro non possono usare l'autenticazione Kerberos e potrebbero richiedere l'approvazione manuale.  

-   Non è possibile configurare il client di un gruppo di lavoro come un punto di distribuzione. Configuration Manager richiede che i computer del punto di distribuzione siano membri di un dominio.  


### <a name="install-the-client-on-workgroup-computers"></a>Installare il client nei computer del gruppo di lavoro  

Controllare i prerequisiti e seguire le istruzioni della sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  


#### <a name="workgroup-example-1"></a>Gruppo di lavoro - Esempio 1

Questo esempio esegue le azioni seguenti: 
- Installa il client per la gestione del client Intranet
- Specifica il codice del sito 
- Specifica il suffisso DNS per individuare un punto di gestione  

   `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>Gruppo di lavoro - Esempio 2

In questo esempio è necessario che il client si trovi in un percorso di rete configurato in un gruppo di limiti, affinché l'assegnazione automatica del sito sia completata correttamente. Il comando include un punto di stato di fallback nel server FSPSERVER. Questa proprietà consente di tenere traccia della distribuzione client e di identificare eventuali problemi di comunicazione con il client. 

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Gestione client basata su Internet  
 
> [!Note]  
> Questa sezione non si applica ai client che usano un [gateway di gestione cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Per installare i client basati su Internet che usano un gateway di gestione cloud, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

Quando il sito di Configuration Manager supporta la [gestione client basata su Internet](/sccm/core/clients/manage/plan-internet-based-client-management) per client che si trovano a volte sulla Intranet e a volte su Internet, sono disponibili due opzioni per l'installazione dei client sulla Intranet:  

-   Quando si installa il client, includere la proprietà Client.msi `CCMHOSTNAME=<internet FQDN of the internet-based management point>`. Ad esempio, usando l'installazione manuale o il push client. Quando si usa questo metodo, assegnare direttamente il client al sito. Non è possibile usare l'assegnazione sito automatica. Vedere la sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual) che illustra un esempio di questo metodo di configurazione.  

-   Installare il client per la gestione del client Intranet, quindi assegnare un punto di gestione client basato su Internet al client. Modificare il punto di gestione usando le proprietà client di Configuration Manager nel Pannello di controllo oppure usando uno script. Questo metodo consente di usare l'assegnazione client automatica. Per altre informazioni, vedere la sezione [ Configurare i client per la gestione client basata su Internet dopo l'installazione](#BKMK_ConfigureIBCM_MP).  

Per installare i client Internet, scegliere uno dei metodi supportati seguenti:  

-   Predisporre un meccanismo per questi client affinché possano temporaneamente connettersi alla Intranet tramite VPN. Installare quindi il client usando un metodo di installazione client appropriato.  

-   Usare un metodo di installazione indipendente da Configuration Manager. Ad esempio, creare un pacchetto dei file di origine dell'installazione client su un supporto rimovibile e inviarlo agli utenti per l'installazione. I file di origine dell'installazione client sono disponibili nella cartella `<InstallationPath>\Client` nel server del sito di Configuration Manager. Includere nel supporto uno script per eseguire la copia manuale nella cartella del client. Da questa cartella, installare il client usando CCMSetup.exe e tutte le proprietà della riga di comando CCMSetup appropriate.  

> [!NOTE]  
>  Configuration Manager non supporta l'installazione di un client direttamente dal punto di gestione basato su Internet o dal punto di aggiornamento software basato su Internet.  

I client gestiti su Internet devono comunicare con sistemi del sito basati su Internet. Assicurarsi che questi client abbiano anche i certificati per un'infrastruttura a chiave pubblica (PKI) prima di installare il client. Installare tali certificati in modo indipendente da Configuration Manager. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Istallare i client su Internet specificando le proprietà della riga di comando CCMSetup  

1.  Seguire le istruzioni fornite nella sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual). Includere sempre le opzioni seguenti:  

    -   Parametro della riga di comando CCMSetup `/source:<local path to the copied Client folder>`  

    -   Parametro della riga di comando CCMSetup `/UsePKICert`  

    -   Proprietà Client.msi `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Proprietà Client.msi `SMSSIGNCERT=<local path to exported site server signing certificate>`  

    -   Proprietà Client.msi `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  Se il sito ha più di un punto di gestione basato su Internet, non ha importanza quale punto di gestione basato su Internet viene specificato per la proprietà CCMHOSTNAME. Quando un client di Configuration Manager si connette al punto di gestione basato su Internet specificato, questo invia al client un elenco di punti di gestione basati su Internet disponibili nel sito e il client ne seleziona uno in modo casuale.  

2.  Se non si vuole che il client controlli l'elenco di revoche di certificati (CRL), specificare il parametro della riga di comando CCMSetup `/NoCRLCheck`.  

3.  Se si sta usando un punto di stato di fallback basato su Internet, specificare la proprietà Client.msi `FSP=<internet FQDN of the internet-based fallback status point>`.  

4.  Se si sta installando il client per la gestione client Internet esclusiva, specificare la proprietà Client.msi `CCMALWAYSINF=1`.  

5.  Verificare se è necessario specificare parametri della riga di comando CCMSetup aggiuntivi. Ad esempio, se il client dispone di più di un certificato PKI valido, potrebbe essere necessario specificare un criterio di selezione del certificato. Per un elenco delle proprietà disponibili, vedere [Informazioni su proprietà e parametri di installazione client](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="internet-based-example"></a>Esempio per il client basato su Internet:  

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

In questo esempio il client viene installato con i comportamenti seguenti:
  - Usare i file di origine da una cartella sull'unità D
  - Usare un certificato PKI del client 
  - Selezionare il certificato con il periodo di validità più esteso 
  - Gestione client Internet esclusiva
  - Assegnare il client per usare il punto di gestione basato su Internet denominato SERVER1
  - Assegnare il punto di stato di fallback basato su Internet nel dominio contoso.com
  - Assegnare il client al sito ABC  


###  <a name="BKMK_ConfigureIBCM_MP"></a> Configurare i client per la gestione client basata su Internet dopo l'installazione  

Per assegnare il punto di gestione basato su Internet dopo l'installazione del client, usare una delle procedure seguenti. La prima richiede la configurazione manuale ed è appropriata per configurare pochi client. La seconda è più appropriata per la configurazione di molti client.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Per configurare i client per la gestione client basata su Internet dopo l'installazione dal pannello di controllo di Configuration Manager  

1.  Aprire il pannello di controllo di **Configuration Manager** nel client.  

2.  Nella scheda **Internet** immettere il nome di dominio completo del punto di gestione basato su Internet in **FQDN Internet**.  

    > [!NOTE]  
    >  La scheda **Internet** è disponibile solo per i client che dispongono di un certificato PKI.  

3.  Se il client accede a Internet tramite un server proxy, immettere le impostazioni di tale server.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurare i client per la gestione client basata su Internet dopo l'installazione usando uno script  

1.  Aprire un editor di testo, come Blocco note.  

2.  Copiare e inserire l'esempio di VBScript seguente nel file. Sostituire *mp.contoso.com* con l'FQDN Internet del punto di gestione basato su Internet.  

    ``` VBScript 
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Per eliminare il punto di gestione basato su Internet specificato, rimuovere il valore del nome di dominio completo del server racchiuso tra virgolette. La riga avrà l'aspetto seguente: `newInternetBasedManagementPointFQDN = ""`  

4.  Salvare il file con un'estensione .vbs.  

5.  Usare cscript.exe per eseguire lo script nei computer client, ricorrendo a uno dei metodi seguenti:  

    -   Distribuire il file ai client di Configuration Manager esistenti usando un pacchetto e un programma.  

    -   Eseguire il file localmente sui client di Configuration Manager esistenti facendo doppio clic sul file di script in Esplora risorse.  

Potrebbe essere necessario riavviare il client per rendere effettive le modifiche.  



##  <a name="BKMK_Provision"></a> Effettuare il provisioning delle proprietà di installazione client per le installazioni client basate su Criteri di gruppo e aggiornamento software

Usare Criteri di gruppo di Windows per effettuare il provisioning dei computer con le proprietà di installazione client di Configuration Manager. Queste proprietà sono archiviate nel Registro di sistema del computer. Il client ne esegue la lettura al momento dell'installazione. Questa procedura normalmente non è richiesta, ma potrebbe essere necessaria in alcuni scenari di installazione client, come i seguenti:  

-   Si usano le impostazioni di Criteri di gruppo o i metodi di installazione client basata sull'aggiornamento software. Lo schema di Active Directory non è stato esteso a Configuration Manager.  

-   Si desidera sostituire le proprietà di installazione client su computer specifici.  

> [!NOTE]  
>  Se nella riga di comando CCMSetup.exe vengono specificate le proprietà di installazione, le proprietà di cui viene effettuato il provisioning nei computer non vengono usate.  

Il supporto di installazione di Configuration Manager offre un modello amministrativo di Criteri di gruppo denominato **ConfigMgrInstallation.adm** da usare per effettuare il provisioning dei computer client con le proprietà di installazione.   


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurare e assegnare le proprietà di installazione client tramite un oggetto Criteri di gruppo  

1.  Importare il modello amministrativo **ConfigMgrInstallation.adm** in un oggetto Criteri di gruppo nuovo o esistente usando un editor, ad esempio l'Editor oggetti Criteri di gruppo di Windows. Questo file è disponibile nella cartella `TOOLS\ConfigMgrADMTemplates` del supporto di installazione di Configuration Manager.  

2.  Aprire le proprietà dell'impostazione importata **Configurare le impostazioni di distribuzione client**.  

3.  Scegliere **Abilitato**.  

4.  Nella casella **CCMSetup** immettere le proprietà necessarie della riga di comando di CCMSetup. Per un elenco di tutte le proprietà della riga di comando di CCMSetup con i relativi esempi di utilizzo, vedere [Informazioni su parametri e proprietà di installazione del client](/sccm/core/clients/deploy/about-client-installation-properties).  

5.  Assegnare l'oggetto Criteri di gruppo ai computer per i quali si vuole effettuare il provisioning delle proprietà di installazione client di Configuration Manager.  
