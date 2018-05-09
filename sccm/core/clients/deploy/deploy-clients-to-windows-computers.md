---
title: Distribuire i client in Windows
titleSuffix: Configuration Manager
description: Informazioni su come distribuire il client di Configuration Manager in computer Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Come distribuire i client nei computer Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di installare i client di Configuration Manager, assicurarsi che siano presenti tutti i [prerequisiti](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) e che siano state completate tutte le configurazioni di distribuzione necessarie.   



##  <a name="BKMK_ClientPush"></a> Come installare i client con l'installazione push client  

È possibile configurare l'installazione push client per un sito. L'installazione client viene eseguita automaticamente nei computer individuati all'interno dei limiti configurati del sito quando tali limiti sono configurati come gruppo di limiti. In alternativa, è possibile avviare un'installazione push client eseguendo l'Installazione guidata push client per una raccolta specifica o una risorsa all'interno di una raccolta.  

È anche possibile usare l'Installazione guidata push client per installare il client di Configuration Manager nei risultati ottenuti da una [query](../../../core/servers/manage/queries-technical-reference.md). Affinché l'installazione abbia esito positivo, uno degli elementi restituiti dalla query deve essere l'attributo **ResourceID** dalla classe **Risorse di sistema**.   

Se il server del sito non può contattare il computer client o avviare il processo di installazione, ripete automaticamente il tentativo di installazione ogni ora, per sette giorni.  

Per tenere traccia del processo di installazione client, installare un punto di stato di fallback prima di installare i client. Quando viene installato un punto di stato di fallback, esso viene assegnato automaticamente ai client quando vengono installati con il metodo di installazione push client. Per tenere traccia dello stato di installazione client, visualizzare i report di assegnazione e distribuzione client. 

I file di log del client contengono informazioni più dettagliate per la risoluzione dei problemi e non richiedono un punto di stato di fallback. Ad esempio, nel file **CCM.log** nel server del sito vengono registrati tutti i problemi riscontrati dal server del sito durante la connessione al computer. Nel file **CCMSetup** nel client viene registrato il processo di installazione.  

> [!IMPORTANT]  
>  Affinché il push client venga eseguito correttamente, assicurarsi che siano presenti tutti i prerequisiti. Per altre informazioni, vedere [Dipendenze del metodo di installazione](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurare il sito per l'uso automatico del push client per i computer individuati

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti**.  

3.  Selezionare il sito per cui si vuole configurare l'installazione push client automatica a livello di sito.  

4.  Nella scheda **Home** del gruppo **Impostazioni** scegliere **Impostazioni di installazione client** > **Installazione push client**.  

5.  Nella scheda **Generale** della finestra di dialogo **Proprietà installazione push client** selezionare **Abilita installazione push client automatica a livello di sito**. Selezionare i tipi di sistema in cui Configuration Manager deve eseguire il push del software client.  

6.  Specificare se si vuole installare il client nei controller di dominio.  

7.  Nella scheda **Account** specificare uno o più account affinché Configuration Manager li usi durante la connessione al computer di destinazione. Fare clic sull'icona **Crea**, immettere **Nome utente** e **Password** (non più di 38 caratteri), confermare la password e quindi fare clic su **OK**. Specificare almeno un account di installazione push client. Per installare il client, è necessario che questo account abbia i diritti di amministratore locale nel computer di destinazione. Se non si specifica un account di installazione push client, Configuration Manager prova a usare l'account del computer del sistema del sito. L'installazione push client tra domini ha esito negativo quando si usa l'account del computer del sistema del sito.  
    > [!NOTE]  
    >  Per usare l'installazione push client da un sito secondario, specificare l'account del sito secondario che avvia l'installazione push client.  
    >   
    >  Per altre informazioni sull'account di installazione push client, vedere la procedura [Usare l'installazione guidata push client](#use-the-client-push-installation-wizard) riportata di seguito.  

8.  Completare la scheda **Proprietà di installazione**.

     Se lo schema è esteso a Configuration Manager, il sito pubblica in Active Directory Domain Services le [proprietà di installazione client](../../../core/clients/deploy/about-client-installation-properties.md) specificate in questa scheda. Queste proprietà vengono lette dalle installazioni client quando CCMSetup viene eseguito senza proprietà di installazione.  

    > [!NOTE]  
    >  Se si abilita l'installazione push client in un sito secondario, assicurarsi che la proprietà **SMSSITECODE** sia impostata sul nome del sito di Configuration Manager del relativo sito primario padre. Se lo schema di Active Directory è esteso a Configuration Manager, è anche possibile impostare questa proprietà su AUTO per individuare automaticamente la corretta assegnazione del sito.  

### <a name="use-the-client-push-installation-wizard"></a>Usare l'installazione guidata push client

1.  Nella console di Configuration Manager scegliere **Amministrazione** >  **Configurazione del sito** > **Siti**.  

3.  Selezionare il sito per cui si vuole configurare l'installazione push client automatica a livello di sito.  

4.  Nella scheda **Home** > gruppo **Impostazioni** scegliere **Impostazioni di installazione client** > **Installazione push client**.  

5.  Completare la scheda **Proprietà di installazione**.  

     Se lo schema è esteso a Configuration Manager, il sito pubblica in Active Directory Domain Services le [proprietà di installazione client](../../../core/clients/deploy/about-client-installation-properties.md) specificate in questa scheda. Queste proprietà vengono lette dalle installazioni client quando CCMSetup viene eseguito senza proprietà di installazione.   

6.  Nella console di Configuration Manager scegliere **Asset e conformità**.  

7.  Nell'area di lavoro **Asset e conformità** , selezionare uno o più computer o una raccolta di computer.  

8.  Nella scheda **Home** scegliere una delle opzioni seguenti:  

    -   Se si vuole installare il client in uno o più computer, nel gruppo **Dispositivo** scegliere **Installa client**.  

    -   Se si vuole installare il client in una raccolta di computer, nel gruppo **Raccolta** scegliere **Installa client**.  

9. Nella pagina **Prima di iniziare** dell'**Installazione guidata client** riesaminare le informazioni e quindi scegliere **Avanti**.  

10. Completare la pagina **Opzioni di installazione**.  

11. Esaminare le impostazioni di installazione, quindi chiudere la procedura guidata.  

> [!NOTE]  
>  È possibile usare la procedura guidata per installare i client, anche se il sito non è configurato per il push client.  



##  <a name="BKMK_ClientSUP"></a> Come installare i client con l'installazione basata sull'aggiornamento software  
 L'Installazione client basata sull'aggiornamento software pubblica il client in un punto di aggiornamento software come aggiornamento software. Usare questo metodo per una nuova installazione o un aggiornamento.  

 Se in un computer è installato il client di Configuration Manager, tale computer riceve i criteri client dal sito. I criteri includono il nome del server del punto di aggiornamento software e la porta dalla quale ricevere gli aggiornamenti.   

> [!IMPORTANT]  
>  Per usare l'installazione basata sull'aggiornamento software, è necessario usare lo stesso server di Windows Server Update Services (WSUS) per l'installazione client e gli aggiornamenti software. Questo server deve essere il punto di aggiornamento software attivo in un sito primario. Per altre informazioni, vedere [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) (Installare un punto di aggiornamento software).  

Se un computer non ha installato il client di Configuration Manager, è necessario configurare e assegnare un oggetto Criteri di gruppo in Active Directory Domain Services per specificare il nome del server del punto di aggiornamento software.  

Non è possibile aggiungere proprietà della riga di comando a un'installazione client basata sull'aggiornamento software. Se lo schema di Active Directory è stato esteso a Configuration Manager, i computer client inviano automaticamente la query delle proprietà di installazione ad Active Directory Domain Services durante l'installazione.  

Se lo schema di Active Directory non è stato esteso, è necessario usare Criteri di gruppo per effettuare il provisioning delle impostazioni dell'installazione client nei computer presenti nel sito. Queste impostazioni vengono applicate automaticamente a tutte le installazioni basate sull'aggiornamento software. Per altre informazioni, vedere [Come effettuare il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software)](#BKMK_Provision) e [Come assegnare i client a un sito](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Usare le procedure seguenti per configurare i computer senza un client di Configuration Manager per l'uso del punto di aggiornamento software per l'installazione client e gli aggiornamenti software e per la pubblicazione del software client nel punto di aggiornamento software.  

> [!NOTE]  
>  Se i computer sono in uno stato di riavvio in sospeso in seguito a una precedente installazione software, un'installazione client basata sull'aggiornamento potrebbe causare il riavvio del computer.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configurare un oggetto Criteri di gruppo in Active Directory Domain Services per specificare il punto di aggiornamento software per l'installazione client e gli aggiornamenti software:  

1.  Usare la Console Gestione Criteri di gruppo per aprire un oggetto Criteri di gruppo nuovo o esistente.  

2.  Nella console espandere **Configurazione computer**, **Modelli amministrativi**, **Componenti di Windows** e quindi scegliere **Windows Update**.  

3.  Aprire le proprietà dell'impostazione **Specifica il percorso del servizio di aggiornamento Microsoft nella rete Intranet** e quindi scegliere **Attivato**.  

4.  Nella casella **Impostare il servizio di aggiornamento nella rete Intranet per il rilevamento degli aggiornamenti** specificare il nome e la porta del server del punto di aggiornamento software:  

    -   Se il sistema del sito di Configuration Manager è configurato per usare un nome di dominio completo (FQDN), usare il formato FQDN.  

    -   Se il sistema del sito di Configuration Manager non è configurato per usare un nome FQDN, usare il formato di nome breve.  

    > [!NOTE]  
    >  Per determinare il numero della porta, vedere [Come determinare le impostazioni della porta usate da WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Esempio: **http://server1.contoso.com:8530**  

5.  Nella casella **Impostare il server per le statistiche nella rete Intranet** specificare il nome del server delle statistiche Intranet. Non deve essere lo stesso server del punto di aggiornamento software. Se si tratta dello stesso server, il formato deve essere diverso.  

6.  Assegnare l'oggetto Criteri di gruppo ai computer in cui si vuole installare il client e ricevere gli aggiornamenti software.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Pubblicare il client di Configuration Manager nel punto di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**.  

3.  Selezionare il sito per cui si vuole configurare l'installazione client basata sull'aggiornamento software.  

4.  Nella scheda **Home** del gruppo **Impostazioni** scegliere **Impostazioni di installazione client** e quindi scegliere **Installazione client basata sull'aggiornamento software**.  

5.  Selezionare **Abilita installazione client basata su aggiornamento software**.  

6.  Se il software client nel server del sito di Configuration Manager è una versione successiva a quella disponibile nel punto di aggiornamento software, viene visualizzata la finestra di dialogo **Versione più recente del pacchetto client rilevata**. Fare clic su **Sì** per pubblicare la versione più recente.  

    > [!NOTE]  
    >  Se il software client non è stato pubblicato in precedenza nel punto di aggiornamento software, questa casella è vuota.  

L'aggiornamento software per il client di Configuration Manager non viene automaticamente aggiornato quando esiste una nuova versione. Se si esegue l'aggiornamento del sito, che include una nuova versione client, ripetere questa procedura e fare clic su **Sì** per il passaggio 6.  



##  <a name="BKMK_ClientGP"></a> Come installare i client con i criteri di gruppo  
 È possibile usare Criteri di gruppo in Active Directory Domain Services per pubblicare o assegnare il client di Configuration Manager da installare nei computer aziendali. Il client viene installato all'avvio del computer. Quando si usa Criteri di gruppo, il client viene visualizzato in **Installazione applicazioni** nel Pannello di controllo a disposizione dell'utente per eseguire l'installazione.  

 Usare il pacchetto di Windows Installer (CCMSetup.msi) per le installazioni basate su Criteri di gruppo. Il file si trova nella cartella **&lt;directory di installazione di ConfigMgr\>\bin\i386** nel server del sito di Configuration Manager. Non è possibile aggiungere proprietà a questo file per modificare il comportamento di installazione.  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client, è necessario disporre delle autorizzazioni di amministratore.  

-   Se lo schema di Active Directory viene esteso per Configuration Manager ed è selezionata l'opzione **Publish this site in Active Directory Domain Services** (Pubblica questo sito in Active Directory Domain Services) nella scheda **Avanzate** della finestra di dialogo **Proprietà sito**, i computer client eseguono automaticamente una ricerca in Active Directory Domain Services per individuare le proprietà di installazione. Per altre informazioni sulle proprietà di installazione pubblicate, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Se lo schema di Active Directory non è stato esteso, è possibile usare la procedura descritta in questo argomento per archiviare le proprietà di installazione nel Registro di sistema dei computer: [Come effettuare il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software)](#BKMK_Provision). Queste proprietà di installazione vengono usate quando il client è installato.  

Per informazioni sull'uso di Criteri di gruppo in Active Directory Domain Services per l'installazione del software, fare riferimento alla documentazione di Windows Server.  



##  <a name="BKMK_Manual"></a> Come installare manualmente i client  
 È possibile installare manualmente il software client nei computer aziendali usando il programma CCMSetup.exe. Questo programma e i relativi file di supporto si trovano nella cartella **Client** all'interno della cartella di installazione di Configuration Manager sul server del sito e sui punti di gestione nel sito. La cartella è condivisa in rete come  

 \\\\*&lt;<Nome server del sito\>* \SMS_*&lt;Codice del sito\>* \Client\  

 dove *&lt;Nome server del sito\>* è il nome di uno dei server che ospitano un punto di gestione e *&lt;Codice del sito\>* è il codice del sito primario al quale il client è assegnato. Per eseguire CCMSetup.exe dalla riga di comando nel client, è necessario eseguire il mapping di un'unità di rete in questo percorso e quindi eseguire il comando.  

> [!IMPORTANT]  
>  Per accedere ai file di installazione client, è necessario disporre delle autorizzazioni di amministratore.  

 CCMSetup.exe copia tutti i prerequisiti necessari nel computer client e chiama il pacchetto di Windows Installer (Client.msi) per installare il client. Non è possibile eseguire Client.msi direttamente.  

 È possibile specificare le proprietà di riga di comando per CCMSetup.exe e Client.msi per modificare il comportamento dell'installazione client. Verificare di aver specificato le proprietà CCMSetup (le proprietà che iniziano con **/**) prima di specificare le proprietà Client.msi. Ad esempio:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

e il client viene installato con le proprietà seguenti:  

|Proprietà|Descrizione|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Questa proprietà CCMSetup specifica al punto di gestione SMSMP01 di scaricare i file di installazione client richiesti.|  
|**/logon**|Questa proprietà CCMSetup specifica che l'installazione deve essere interrotta se viene rilevato un client di Configuration Manager sul computer.|  
|**SMSSITECODE=AUTO**|Questa proprietà Client.msi specifica che il client cerca di individuare il codice sito di Configuration Manager da usare, ad esempio usando Active Directory Domain Services.|  
|**FSP=SMSFP01**|La proprietà Client.msi specifica che il punto di stato di fallback denominato SMSFP01 viene usato per ricevere i messaggi di stato inviati dal computer client.|  

 Per i dettagli su tutte le proprietà CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione](../../../core/clients/deploy/about-client-installation-properties.md)  

> [!Tip]  
> Per conoscere la procedura di installazione del client di Configuration Manager in un dispositivo Windows 10 moderno usando un'identità di Azure AD, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Tale procedura è riservata ai client sulla Intranet o su Internet.  


### <a name="examples"></a>Esempi
 Questi esempi sono specifici per client di Active Directory sulla Intranet. Per rappresentare i diversi aspetti del sito, vengono usati i valori seguenti:  

 **MPSERVER** = server che ospita il punto di gestione   
**FSPSERVER** = server che ospita il punto di stato di fallback  
**ABC** = codice del sito  
**contoso.com** = nome di dominio  

 Tutti i server del sistema del sito sono configurati con un FQDN Intranet. Il sito è pubblicato nella foresta Active Directory del client.  

 Nel computer client accedere come amministratore locale, eseguire il mapping dell'unità (z:) a \\\MPSERVER\SMS_ABC\Client, passare all'unità z nel prompt dei comandi ed eseguire uno di questi comandi:  

 **Esempio 1:**  

`CCMSetup.exe`  

In questo esempio il client viene installato senza proprietà aggiuntive. Il client viene configurato automaticamente con le proprietà di installazione client pubblicate in Active Directory Domain Services. È configurato automaticamente per le impostazioni seguenti: 
- Codice sito. Per questa impostazione è necessario includere il percorso di rete del client in un gruppo di limiti configurato per l'assegnazione del client. 
- Punto di gestione
- Punto di stato di fallback
- Comunicare solo tramite HTTPS  
  
Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Esempio 2:**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
In questo esempio viene eseguito l'overrride della configurazione automatica disponibile in Active Directory Domain Services. In questo caso non è necessario includere il percorso di rete del client in un gruppo di limiti configurato per l'assegnazione del client. Al contrario, è l'installazione a specificare le impostazioni seguenti:
- Codice sito
- Punto di gestione Intranet 
- Punto di gestione basato su Internet
- Punto di stato di fallback che accetta connessioni Internet
- Usare un certificato client PKI con il periodo di validità più lungo  



##  <a name="BKMK_ClientLogonScript"></a> Come installare i client con gli script di accesso  
 Configuration Manager supporta gli script di accesso per installare il software client di Configuration Manager. È possibile usare il file di programma **CCMSetup.exe** in uno script di accesso per avviare l'installazione client.  

 L'installazione con script di accesso usa gli stessi metodi dell'installazione client manuale. È possibile specificare la proprietà di installazione **/Logon** per CCMSsetup.exe. Se nel computer esiste già una versione del client, questa proprietà impedisce l'installazione del client. In questo modo è possibile evitare la reinstallazione del client ogni volta che viene eseguito lo script di accesso.  

 Se non viene specificata un'origine dell'installazione con la proprietà **/Source** né viene specificato un punto di gestione da cui ottenere l'installazione usando la proprietà **/MP**, CCMSetup.exe individua il punto di gestione eseguendo una ricerca in Active Directory Domain Services. Questo comportamento si verifica solo se lo schema è stato esteso a Configuration Manager e il sito è pubblicato in Active Directory Domain Services. In alternativa, il client può usare DNS o WINS per individuare un punto di gestione.  



##  <a name="BKMK_ClientApp"></a> Come installare i client con un pacchetto e un programma  
 È possibile usare Configuration Manager per creare e distribuire un pacchetto e un programma di aggiornamento per il software client di computer selezionati nella gerarchia. Con Configuration Manager viene fornito un file di definizione pacchetto che popola le proprietà del pacchetto con i valori tipici. È possibile personalizzare il comportamento dell'installazione del client specificando proprietà della riga di comando aggiuntive.  

> [!NOTE]  
>  Non è possibile aggiornare i client di Configuration Manager 2007 con questo metodo. Usare invece l'aggiornamento automatico del client, che crea e distribuisce automaticamente un pacchetto contenente la versione più recente del client. Per altre informazioni, vedere [Aggiornare i client](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Per altre informazioni sulla migrazione da versioni precedenti del client di Configuration Manager, vedere [Pianificare una strategia di migrazione client](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Creare un pacchetto e un programma per il software client  

Usare la procedura seguente per creare un pacchetto e un programma di Configuration Manager che possa essere distribuito nei computer client di Configuration Manager per aggiornare il software client.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Pacchetti**.  

3.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea pacchetto da definizione**.  

4.  Nella pagina **Definizione pacchetto** della creazione guidata selezionare **Microsoft** nell'elenco a discesa **Autore** e selezionare **Aggiornamento client di Configuration Manager** nell'elenco **Definizione pacchetto**.  

5.  Nella pagina **File di origine** selezionare **Reperisci sempre i file di origine da una cartella di origine**.  

6.  Nella pagina **Cartella di origine** selezionare **Percorso di rete (nome UNC)**. A questo punto immettere il percorso di rete per il computer e la cartella che contiene i file di installazione del client.  

    > [!NOTE]  
    >  Il computer in cui è in esecuzione la distribuzione di Configuration Manager deve avere accesso alla cartella di rete specificata. In caso contrario, l'installazione avrà esito negativo.  

    Per cambiare una proprietà di installazione client, è possibile modificare i parametri della riga di comando CCMSetup.exe nella scheda **Generale** della finestra di dialogo del programma **Aggiornamento automatico dell'agente di Configuration Manager - Proprietà**. Le proprietà di installazione predefinite sono **/noservice SMSSITECODE=AUTO**.  

9. Distribuire il pacchetto a tutti i punti di distribuzione in cui si desidera venga ospitato il pacchetto di aggiornamento client. È quindi possibile distribuire il pacchetto alle raccolte di computer contenenti i client da aggiornare.  



## <a name="bkmk_mdm"></a>Come installare i client nei dispositivi Windows gestiti da MDM di Intune

È possibile distribuire i file di installazione del client nei computer registrati in Microsoft Intune. 

Questa procedura è valida per un client tradizionale connesso alla Intranet. Usa i metodi di autenticazione client tradizionali. Per garantire che il dispositivo rimanga in uno stato gestito dopo l'installazione del software client, il dispositivo deve essere sulla Intranet e all'interno di un limite del sito di Configuration Manager.  

Per conoscere la procedura di installazione del client di Configuration Manager in un dispositivo Windows 10 moderno usando un'identità di Azure AD, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Dopo l'installazione del software client, la registrazione del dispositivo con Intune viene annullata.
> 
> A partire dalla versione 1710, la registrazione con Intune non viene annullata dai client. È possibile avere sia il client di Configuration Manager sia la registrazione MDM nello stesso momento. Per altre informazioni, vedere [Co-gestione](/sccm/core/clients/manage/co-management-overview).

###  <a name="install-clients-with-intune"></a>Installare i client con Intune:

1. In Intune [creare un'app](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) contenente il file di installazione client di Configuration Manager **ccmsetup.msi**. Il file si trova nella cartella **&lt;directory di installazione di ConfigMgr\>\bin\i386** nel server del sito di Configuration Manager.

2. In Autore del software Microsoft Intune immettere i parametri della riga di comando. Ad esempio, usare la riga di comando seguente con un client tradizionale sulla Intranet:

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Per una riga di comando di esempio da usare con un client Windows 10 moderno che usa l'autenticazione di Azure AD, vedere [Preparare i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Distribuire l'app](/intune/deploy-use/deploy-apps-in-microsoft-intune) ai computer Windows registrati.



##  <a name="BKMK_ClientImage"></a> Come installare i client con un'immagine di computer  
È possibile preinstallare il software client di Configuration Manager in un computer di riferimento usato per creare un'immagine del sistema operativo.   

> [!Important]
> Quando si usa la sequenza di attività di Configuration Manager per distribuire l'immagine del sistema operativo, il passaggio [Prepara Client ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) rimuove completamente il client di Configuration Manager. 

### <a name="prepare-the-client-computer-for-imaging"></a>Preparare il computer client per la creazione dell'immagine  

1.  Installare manualmente il software client di Configuration Manager nel computer di riferimento. Per ulteriori informazioni, vedere [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Non specificare un codice sito di Configuration Manager per il client nelle proprietà della riga di comando CCMSetup.exe.  

2.  In un prompt dei comandi digitare `net stop ccmexec` per accertarsi che il servizio **Host agenti di SMS** (Ccmexec.exe) non sia in esecuzione nel computer di riferimento.
3.  Eliminare il file **SMSCFG.INI** dalla cartella **Windows** nel computer di riferimento.  
3.  Rimuovere i certificati memorizzati nell'archivio del computer locale nel computer di riferimento. Ad esempio, se si usano certificati di infrastruttura a chiave pubblica (PKI), è necessario rimuovere i certificati nell'archivio **Personale** per **Computer** e **Utente** prima di creare l'immagine del computer.

4.  Se i client sono installati in una gerarchia di Configuration Manager diversa rispetto al computer di riferimento, rimuovere la chiave radice attendibile dal computer di riferimento.  
    > [!NOTE]  
    >  Se i client non possono eseguire query in Servizi di dominio Active Directory per individuare un punto di gestione, usano la chiave radice attendibile per determinare i punti di gestione attendibili. Se tutti i client creati da un'immagine vengono distribuiti nella stessa gerarchia del computer master, non rimuovere la chiave radice attendibile. Se i client vengono distribuiti in gerarchie diverse, rimuovere la chiave radice attendibile. Effettuare anche il provisionig di questi client con la nuova chiave radice attendibile. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Usare il software di creazione dell'immagine per acquisire l'immagine del computer master.  

6.  Distribuire l'immagine ai computer di destinazione.  



##  <a name="BKMK_ClientWorkgroup"></a> Come installare i client sui computer dei gruppi di lavoro  
 Configuration Manager supporta l'installazione di client per i computer nei gruppi di lavoro. Installare il client nei computer nei gruppi di lavoro usando il metodo specificato in [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

 Prerequisiti:  

-   Il client deve essere installato manualmente su ciascun computer del gruppo di lavoro. Durante l'installazione, l'utente connesso deve disporre dei diritti di amministratore locale.  

-   Per accedere alle risorse nel dominio del server del sito di Configuration Manager, è necessario configurare l'account di accesso di rete per il sito. Specificare questo account come una proprietà del componente di distribuzione software. Per altre informazioni, vedere [Componenti del sito per System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitazioni:  

-   I client del gruppo di lavoro non possono individuare i punti di gestione dai Servizi di dominio Active Directory e devono quindi usare DNS, WINS o un altro punto di gestione.  

-   Il roaming globale non è supportato perché i client non possono eseguire query in Servizi di dominio Active Directory per ottenere le informazioni sul sito.  

-   I metodi di individuazione di Active Directory non sono in grado di individuare i computer nei gruppi di lavoro.  

-   Non è possibile distribuire software agli utenti dei computer del gruppo di lavoro.  

-   Non è possibile usare il metodo di installazione push client per installare il client sui computer del gruppo di lavoro.  

-   I client del gruppo di lavoro non possono usare l'autenticazione Kerberos e potrebbero richiedere l'approvazione manuale.  

-   Non è possibile configurare un client di un gruppo di lavoro come un punto di distribuzione. Configuration Manager richiede che i computer del punto di distribuzione siano membri di un dominio.  

### <a name="install-the-client-on-workgroup-computers"></a>Installare il client nei computer del gruppo di lavoro  

Controllare i prerequisiti e seguire le istruzioni della sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual).  

   In questo esempio viene installato il client per la gestione client sulla intranet e vengono specificati codice sito e suffisso DNS per individuare un punto di gestione. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   In questo esempio è necessario che il client si trovi in un percorso di rete configurato in un gruppo di limiti affinché l'assegnazione automatica del sito sia completata correttamente. Il comando include un punto di stato di fallback nel server FSPSERVER. Questa proprietà consente di tenere traccia della distribuzione client e di identificare eventuali problemi di comunicazione con il client. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Come installare i client per la gestione client basata su Internet  
 
> [!Note]
> Questa sezione non si applica ai client che usano un [gateway di gestione cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Per installare i client basati su Internet che usano un gateway di gestione cloud, vedere [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

Quando il sito di Configuration Manager supporta la [gestione client basata su Internet](/sccm/core/clients/manage/plan-internet-based-client-management) per client che si trovano a volte sulla Intranet e a volte su Internet, sono disponibili due opzioni per l'installazione dei client sulla Intranet:  

-   È possibile includere la proprietà Client.msi di CCMHOSTNAME=*&lt;FQDN Internet del punto di gestione basato su Internet\>* quando si installa il client, ad esempio usando l'installazione manuale o push client. Quando si usa questo metodo, è necessario anche assegnare direttamente il client al sito e non è possibile usare l'assegnazione automatica del sito. La sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual) in questo argomento contiene un esempio di questo metodo di configurazione.  

-   È possibile installare il client per la gestione client sulla Intranet, quindi assegnare un punto di gestione client basato su Internet al client. Modificare il punto di gestione usando le proprietà di client di Configuration Manager nel Pannello di controllo oppure usando uno script. Questo metodo consente di usare l'assegnazione client automatica. Per altre informazioni, vedere la sezione [ Configurare i client per la gestione client basata su Internet dopo l'installazione](#BKMK_ConfigureIBCM_MP) in questo argomento.  

 Se è necessario installare i client sulla Internet, scegliere uno dei metodi supportati descritti di seguito:  

-   Predisporre un meccanismo per questi client affinché possano temporaneamente connettersi alla Intranet tramite VPN. Installare quindi il client usando un metodo di installazione client appropriato.  

-   Usare un metodo di installazione indipendente da Configuration Manager. Ad esempio, creare un pacchetto dei file di origine dell'installazione client su un supporto rimovibile che può essere inviato agli utenti insieme alla istruzioni per l'installazione. I file di origine dell'installazione client si trovano nella cartella *&lt;PercorsoInstallazione\>* \Client nel server del sito e nei punti di gestione di Configuration Manager. Includere nel supporto uno script per la copia manuale sulla cartella client e da questa cartella, installare il client usando CCMSetup.exe e tutte le proprietà della riga di comando CCMSetup appropriate.  

> [!NOTE]  
>  Configuration Manager non supporta l'installazione di un client direttamente dal punto di gestione basato su Internet o dal punto di aggiornamento software basato su Internet.  

 I client gestiti su Internet devono comunicare con sistemi del sito basati su Internet. Assicurarsi che questi client abbiano anche i certificati per un'infrastruttura a chiave pubblica (PKI) prima di installare il client. Installare tali certificati in modo indipendente da Configuration Manager. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Istallare i client su Internet specificando le proprietà della riga di comando CCMSetup  

1.  Seguire le istruzioni nella sezione [Come installare manualmente i client di Configuration Manager](#BKMK_Manual) e includere sempre quanto segue:  

    -   Proprietà della riga di comando CCMSetup **/source:***&lt;percorso locale alla cartella client copiata\>*  

    -   Proprietà della riga di comando CCMSetup **/UsePKICert**  

    -   Proprietà Client.msi **CCMHOSTNAME=***&lt;FQDN del punto di gestione basato su Internet\>*  

    -   Proprietà Client.msi **SMSSIGNCERT=***&lt;percorso locale al certificato di firma del server del sito esportato\>*  

    -   Proprietà Client.msi **SMSSITECODE=***&lt;codice sito del punto di gestione basato su Internet\>*  

    > [!NOTE]  
    >  Se il sito ha più di un punto di gestione basato su Internet, non ha importanza quale punto di gestione basato su Internet viene specificato per la proprietà CCMHOSTNAME. Quando un client di Configuration Manager si connette al punto di gestione basato su Internet specificato, questo invia al client un elenco di punti di gestione basati su Internet disponibili nel sito e il client ne seleziona uno in modo casuale.  

2.  Se non si desidera che il client controlli l'elenco di revoche di certificati (CRL), specificare la proprietà della riga di comando CCMSetup **/NoCRLCheck**.  

3.  Se si sta usando un punto di stato di fallback basato su Internet, specificare la proprietà Client.msi **FSP=***&lt;FQDN Internet del punto di stato di fallback basato su Internet\>*.  

4.  Se si sta installando il client per la gestione client Internet esclusiva, specificare la proprietà Client.msi **CCMALWAYSINF=1**.  

5.  Verificare se è necessario specificare proprietà della riga di comando CCMSetup aggiuntive. Ad esempio, potrebbe essere necessario specificare un criterio di selezione del certificato qualora il client disponesse di più di un certificato PKI valido. Per un elenco delle proprietà disponibili, vedere [Informazioni sulle proprietà di installazione client](../../../core/clients/deploy/about-client-installation-properties.md).  

   Esempio:  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   In questo esempio il client viene installato con i comportamenti seguenti:
   - Usare i file di origine da una cartella sull'unità D
   - Usare un certificato PKI del client 
   - Selezionare il certificato con il periodo di validità più esteso 
   - Gestione client Internet esclusiva
   - Assegnare il client per usare il punto di gestione basato su Internet denominato SERVER1
   - Assegnare il punto di stato di fallback basato su Internet nel dominio contoso.com
   - Assegnare il client al sito ABC  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Configurare i client per la gestione client basata su Internet dopo l'installazione  
 Per assegnare il punto di gestione basato su Internet dopo l'installazione del client, usare una delle procedure seguenti. La prima richiede la configurazione manuale ed è appropriata per alcuni client. La seconda è più appropriata per la configurazione di molti client.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Configurare i client per la gestione client basata su Internet dopo l'installazione tramite l'assegnazione del punto di gestione basato su Internet nelle proprietà di Configuration Manager  

1.  Passare a **Configuration Manager** nel Pannello di controllo del computer client, quindi fare doppio clic per aprirne le relative proprietà.  

2.  Nella scheda **Internet** immettere il nome di dominio completo del punto di gestione basato su Internet nella casella di testo dell'FQDN Internet.  

    > [!NOTE]  
    >  La scheda **Internet** è disponibile solo per i client che dispongono di un certificato PKI.  

3.  Se il client accede a Internet tramite un server proxy, immettere le impostazioni di tale server.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurare i client per la gestione client basata su Internet dopo l'installazione usando uno script  

1.  Aprire un editor di testo, come Blocco note.  

2.  Copiare e inserire l'esempio di VBScript seguente nel file. Sostituire *mp.contoso.com* con l'FQDN Internet del punto di gestione basato su Internet.  

    ```  
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
    >  Se è necessario eliminare un punto di gestione basato su Internet specificato affinché il client non sia configurato per l'uso di un punto di gestione basato su Internet, rimuovere il valore all'interno delle virgolette in modo che questa riga diventi: `newInternetBasedManagementPointFQDN = ""`  

4.  Salvare il file con un'estensione .vbs.  

5.  Usare cscript.exe per eseguire lo script nei computer client, ricorrendo a uno dei metodi seguenti:  

    -   Distribuire il file ai client di Configuration Manager esistenti usando un pacchetto e un programma.  

    -   Eseguire il file localmente sui client di Configuration Manager esistenti facendo doppio clic sul file di script in Esplora risorse.  

 Potrebbe essere necessario riavviare il client per rendere effettive le modifiche.  



##  <a name="BKMK_Provision"></a> Come eseguire il provisioning delle proprietà di installazione client (Criteri di gruppo e installazione client basata su aggiornamento software)  
 È possibile usare Criteri di gruppo di Windows per effettuare il provisioning dei computer con le proprietà di installazione client di Configuration Manager. Queste proprietà vengono archiviate nel Registro di sistema del computer e lette al momento dell'installazione del software client. Questa procedura normalmente non è richiesta, ma potrebbe essere necessaria in alcuni scenari di installazione client, come i seguenti:  

-   Si usano le impostazioni di Criteri di gruppo o i metodi di installazione client basata sull'aggiornamento software. Lo schema di Active Directory non è stato esteso a Configuration Manager.  

-   Si desidera sostituire le proprietà di installazione client su computer specifici.  

> [!NOTE]  
>  Se nella riga di comando CCMSetup.exe vengono specificate le proprietà di installazione, le proprietà di cui viene effettuato il provisioning nei computer non vengono usate.  

 Il supporto di installazione di Configuration Manager offre un modello amministrativo di Criteri di gruppo denominato ConfigMgrInstallation.adm che può essere usato per effettuare il provisioning dei computer client con le proprietà di installazione.   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurare e assegnare le proprietà di installazione client tramite un oggetto Criteri di gruppo  

1.  Importare il modello amministrativo ConfigMgrInstallation.adm in un oggetto Criteri di gruppo nuovo o esistente usando un editor, ad esempio l'Editor oggetti Criteri di gruppo di Windows. Il file è disponibile nella cartella **TOOLS\ConfigMgrADMTemplates** nel supporto di installazione di Configuration Manager.  

2.  Aprire le proprietà dell'impostazione importata **Configurare le impostazioni di distribuzione client**.  

3.  Scegliere **Abilitato**.  

4.  Nella casella **CCMSetup** immettere le proprietà necessarie della riga di comando di CCMSetup. Per un elenco di tutte le proprietà della riga di comando di CCMSetup con i relativi esempi di uso, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Assegnare l'oggetto Criteri di gruppo ai computer per i quali si vuole effettuare il provisioning delle proprietà di installazione client di Configuration Manager.  

Per informazioni su Criteri di gruppo di Windows, fare riferimento alla documentazione di Windows Server.  



## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'installazione del client di Configuration Manager, vedere [Metodi di installazione client](../../../core/clients/deploy/plan/client-installation-methods.md).