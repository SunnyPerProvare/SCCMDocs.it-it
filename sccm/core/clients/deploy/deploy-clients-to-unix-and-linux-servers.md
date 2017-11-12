---
title: Distribuire client UNIX/Linux
titleSuffix: Configuration Manager
description: Informazioni su come distribuire i client nei server UNIX e Linux in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 808997a423dbac6785c9da82f7b6bc8663168486
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>Come distribuire i client nei server UNIX e Linux in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter gestire un server Linux o UNIX con System Center Configuration Manager, è necessario installare il client di Configuration Manager per Linux e UNIX in ogni server Linux o UNIX. L'installazione del client può essere eseguita manualmente in ogni computer o con uno script della shell che installa il client in modalità remota. Configuration Manager non supporta l'uso dell'installazione push client per i server Linux o UNIX. Facoltativamente è possibile configurare un Runbook per System Center Orchestrator per automatizzare l'installazione del client nel server Linux o UNIX.  

 Indipendentemente dal metodo di installazione usato, la gestione del processo di installazione richiede uno script denominato **install** . Questo script viene incluso quando si scarica il Client per Linux e UNIX.  

 Lo script di installazione per il client di Configuration Manager per Linux e UNIX supporta le proprietà della riga di comando. Alcune proprietà della riga di comando sono obbligatori, mentre altri sono facoltativi. Ad esempio, quando si installa il client, è necessario specificare un punto di gestione dal sito utilizzato dal server Linux o UNIX per il contatto iniziale con il sito. Per l'elenco completo delle proprietà della riga di comando, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient).  

 Dopo aver installato il client, specificare le impostazioni client nella console di Configuration Manager per configurare l'agente client in modo analogo ai client basati su Windows. Per altre informazioni, vedere  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> Sui pacchetti di installazione Client e Universal Agent  
 Per installare il client per Linux e UNIX in una piattaforma specifica, è necessario usare il pacchetto di installazione client applicabile al computer in cui si installa il client. I pacchetti di installazione client applicabili sono inclusi in ogni download del client eseguito dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Oltre ai pacchetti di installazione client, il download del client include lo script di **install** che gestisce l'installazione del client in ogni computer.  

 Quando si installa un client, è possibile utilizzare le stesse proprietà di processo e della riga di comando indipendentemente dal pacchetto di installazione client che è utilizzare.  

 Per informazioni su sistemi operativi, piattaforme e pacchetti di installazione client supportati per ogni versione del client di Configuration Manager per Linux e UNIX, vedere [Linux and UNIX servers](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers) (Server Linux e UNIX).  

##  <a name="BKMK_InstallLnUClient"></a> Installare il Client su server Linux e UNIX  
 Per installare il client per Linux e UNIX, si esegue uno script in ogni computer Linux o UNIX. Lo script è denominato **installare** e supporta le proprietà della riga di comando che modificano il comportamento di installazione e fare riferimento a pacchetto di installazione client. Il pacchetto di installazione client e script di installazione deve trovarsi sul client. Il pacchetto di installazione client contiene i file del client di Configuration Manager per una specifica piattaforma e sistema operativo Linux o UNIX.
Ogni pacchetto di installazione client contiene tutti i file necessari per completare l'installazione del client e a differenza dei computer basati su Windows, scaricare file aggiuntivi da un punto di gestione o un altro percorso di origine.  

 Dopo aver installato il client di Configuration Manager per Linux e UNIX, è necessario riavviare il computer. Non appena viene completata l'installazione del software, il client è operativo. Se si riavvia il computer, il client di Configuration Manager viene riavviato automaticamente.  

 Il client installato viene eseguito con le credenziali radice. Per raccogliere l'inventario hardware e per eseguire le distribuzioni software sono necessarie le credenziali radice.  

 Il formato del comando è il seguente:  

 **./install -mp &lt;computer\> -sitecode &lt;codicesito\> &lt;proprietà 1> &lt;proprietà 2> &lt;pacchetto installazione client\>**  

-   **installare** è il nome del file di script che installa il client per Linux e UNIX. Questo file viene fornito con il software client.  

-   **-mp &lt;computer** specifica il punto di gestione iniziale usato dal client.  

     Esempio: smsmp.contoso.com  

-   **-sitecode &lt;codice sito\>** specifica il codice del sito a cui è assegnato il client.  

     Esempio: S01  

-   &lt;proprietà 1> &lt;proprietà 2> specifica le proprietà della riga di comando da usare con lo script di installazione.  

    > [!NOTE]  
    >  Per altre informazioni, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

-   **Pacchetto installazione client** è il nome del pacchetto TAR di installazione client per il sistema operativo del computer, la versione e l'architettura della CPU. Il file. tar installazione del client deve essere specificato per ultimo.  

     Esempio: ccm-Universal-x64.&lt;build\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> Per installare il Client di Configuration Manager su server Linux e UNIX  

1.  In un computer Windows [scaricare il file client appropriato per il server Linux o UNIX](http://go.microsoft.com/fwlink/?LinkID=525184) che si vuole gestire.  

2.  Eseguire il file autoestraente EXE nel computer Windows per estrarre lo script di installazione e il file TAR di installazione del client.  

3.  Copiare lo script di **installazione** e il file TAR in una cartella sul server che si vuole gestire.  

4.  Nel server UNIX o Linux eseguire il comando seguente per abilitare l'esecuzione dello script come programma: **chmod +x install**  

    > [!IMPORTANT]  
    >  Per installare il client, è necessario utilizzare le credenziali radice.  

5.  Usare quindi il comando seguente per installare il client di Configuration Manager: **./install -mp &lt;nome host\> -sitecode &lt;codice\> ccm-Universal-x64.&lt;build\>.tar**  

     Quando si immette questo comando, utilizzare le proprietà della riga di comando aggiuntive che necessarie.  Per l'elenco completo delle proprietà della riga di comando, vedere [Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Dopo l'esecuzione dello script, convalidare l'installazione esaminando il file **/var/opt/microsoft/scxcm.log** . È anche possibile verificare che il client sia installato e in comunicazione con il sito visualizzando i dettagli per il client nel nodo **Dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Proprietà della riga di comando per l'installazione del client nei server Linux e UNIX  
 Per modificare il comportamento dello script di installazione sono disponibili le proprietà seguenti:  

> [!NOTE]  
>  Utilizzare la proprietà **-h** per visualizzare l'elenco delle proprietà supportate.  

-   **-mp &lt;FQDN server\>**  

     Obbligatorio. Specifica nome di dominio completo, i server del punto di gestione che il client utilizzerà come punto iniziale del contatto.  

    > [!IMPORTANT]  
    >  Questa proprietà non specifica il punto di gestione a cui verrà assegnato il client dopo l'installazione.  

    > [!NOTE]  
    >  Quando si usa la proprietà **-mp** per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS, è necessario usare anche la proprietà **-UsePKICert** .  

-   **-sitecode &lt;codice sito\>**  

     Obbligatorio. Specifica il sito primario di Configuration Manager al quale assegnare il client di Configuration Manager.  

     Esempio: -sitecode S01  

-   **-fsp &lt;server_FQDN>**  

     Facoltativo. Specifica nome di dominio completo, i server del punto di stato di fallback che il client utilizza per inviare messaggi di stato.  

     Per altre informazioni sul punto di stato di fallback, vedere [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) .  


-   **-dir &lt;directory\>**  

     Facoltativo. Specifica un percorso alternativo per installare i file del client di Configuration Manager.  

     Per impostazione predefinita, il client viene installato nel percorso seguente: **/opt/microsoft**.  

-   **-nostart**  

     Facoltativo. Impedisce l'avvio automatico del servizio client di Configuration Manager, **ccmexec.bin**, al termine dell'installazione del client.  

     Dopo aver installato il client, è necessario avviare manualmente il servizio client.  

     Per impostazione predefinita, il servizio client viene avviata dopo il completamento dell'installazione del client e ogni volta che il computer viene riavviato.  

-   **-normale**  

     Facoltativo. Specifica la rimozione di tutti i file del client e i dati da un client installato in precedenza per Linux e UNIX, prima che inizi la nuova installazione. Consente di rimuovere il database del client e l'archivio certificati.  

-   **-keepdb**  

     Facoltativo. Specifica che il database client locale viene mantenuto e riutilizzato quando si reinstalla un client. Per impostazione predefinita, quando si reinstalla un client viene eliminato il database.  

-   **-UsePKICert &lt;parametro\>**  

     Facoltativo. Specifica il percorso e il nome completo per un certificato x. 509 PKI nel formato Public Key Certificate Standard (PKCS #12). Questo certificato viene utilizzato per l'autenticazione client. Se non è stato specificato un certificato durante l'installazione e si vuole aggiungere o modificare un certificato, usare l'utilità **certutil** . Per informazioni su certutil, consultare [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Quando si usa **-UsePKICert**, è necessario specificare anche la password associata al file PKCS#12 usando il parametro della riga di comando **-certpw** .  

     Se non si utilizza questa proprietà per specificare un certificato PKI, il client utilizza un certificato autofirmato e tutte le comunicazioni ai sistemi del sito avvengono tramite HTTP.  

     Se si specifica un certificato non valido nella riga di comando di installazione del client, non vengono restituiti errori Questo accade perché la convalida dei certificati si verifica dopo l'installazione di client. Quando viene avviato il client, vengono convalidati i certificati con il punto di gestione e se un certificato non viene visualizzato il seguente messaggio di **scxcm.log**, il file di log client Unix e Linux Configuration Manager: **Non riuscito di convalidare il certificato per punto di gestione**. Il percorso predefinito del file di log è:  **/var/opt/microsoft/scxcm.log**.  

    > [!NOTE]  
    >  È necessario specificare questa proprietà quando si installa un client e usare la proprietà **-mp** per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS.  

     Esempio: -UsePKICert &lt;Percorso completo e nome file\> -certpw &lt;password\>  

-   **-certpw &lt;parametro\>**  

     Facoltativo. Specifica la password associata al file PKCS #12 specificato utilizzando il **- /usepkicert** proprietà.  

     Esempio: -UsePKICert &lt;Percorso completo e nome file\> -certpw &lt;password\>  

-   **-/Nocrlcheck**  

     Facoltativo. Specifica che un client non deve verificare l'elenco di revoche di certificati (CRL) per comunicare tramite HTTPS mediante l'utilizzo di un certificato PKI. Quando questa opzione non è specificata, il client controlla l'elenco di revoche di certificati prima di stabilire una connessione HTTPS usando i certificati PKI. Per ulteriori informazioni sul controllo CRL client, vedere pianificazione di revoche di certificati PKI.  

     Esempio: -UsePKICert &lt;Percorso completo e nome file\> -certpw &lt;password\> -NoCRLCheck  

-   **-rootkeypath &lt;percorso file\>**  

     Facoltativo. Specifica il percorso e il nome completo per la chiave radice attendibile di Configuration Manager. La chiave radice attendibile di Configuration Manager offre un meccanismo usato dai client Linux e UNIX per verificare che siano connessi a un sistema del sito che appartiene alla gerarchia corretta.  

     Se non si specifica la chiave radice attendibile nella riga di comando, il client considererà attendibile il primo punto di gestione con cui comunica e recupererà automaticamente la chiave radice attendibile dal punto di gestione.  

     Per altre informazioni, vedere  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Esempio: -rootkeypath &lt;Percorso completo e nome file\>  

-   **-httpport &lt;porta\>**  

     Facoltativo. Specifica la porta configurato nei punti di gestione utilizzato dal client durante la comunicazione ai punti di gestione su HTTP. Se la porta non è specificata, viene utilizzato il valore predefinito pari a 80.  

     Esempio: -httpport 80  

-   **-httpsport &lt;porta\>**  

     Facoltativo. Specifica la porta configurato nei punti di gestione utilizzato dal client durante la comunicazione ai punti di gestione tramite HTTPS. Se la porta non è specificata, viene utilizzato il valore predefinito 443.  

     Esempio: -UsePKICert &lt;Percorso completo e nome certificato\> -httpsport 443  

-   **-ignoreSHA256validation**  

     Facoltativo. Specifica che l'installazione del client ignora la convalida di SHA-256. Usare questa opzione quando si installa il client in sistemi operativi non rilasciati con una versione di OpenSSL che supporta SHA-256. Per altre informazioni, vedere [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   **-signcertpath &lt;percorso file\>**  

     Facoltativo. Specifica il percorso completo e **. cer** nome file del certificato autofirmato esportato nel server del sito. Se non sono disponibili i certificati PKI, il server del sito di Configuration Manager genera automaticamente i certificati autofirmati.  

     Questi certificati vengono utilizzati per convalidare che i criteri client scaricati dal punto di gestione sono stati inviati dal sito di destinazione. Se non è stato specificato un certificato autofirmato durante l'installazione o si vuole modificare il certificato, usare l'utilità **certutil** . Per informazioni su certutil, consultare [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Il certificato può essere recuperato dall'archivio certificati **SMS** e ha il nome oggetto **Server del sito** e il nome descrittivo **Certificato di firma del server del sito**.  

     Se questa opzione non è specificata durante l'installazione, i client Linux e UNIX considereranno attendibile il primo punto di gestione che comunicano con e recupererà automaticamente il certificato di firma da tale punto di gestione.  

     Esempio: - signcertpath &lt;Percorso completo e nome file\>  

-   **-rootcerts**  

     Facoltativo. Specifica ulteriori certificati PKI per l'importazione che non fanno parte di una gerarchia di autorità di (certificazione CA) certificazione punti gestione. Se si specificano più certificati nella riga di comando, dovranno essere delimitati da virgole.  

     Utilizzare questa opzione se si utilizzano certificati client PKI concatenati a un certificato CA radice attendibile per i punti di gestione di siti. I punti di gestione rifiuteranno il client se il certificato client non è concatenato a un certificato radice trusted nell'elenco di autorità di certificazione del sito.  

     Se non si utilizza questa opzione, il client Linux e UNIX verificherà la gerarchia di trust utilizzando solo il certificato nel **- /usepkicert** opzione.  

     Esempio: - rootcerts &lt;Percorso completo e nome file\>,&lt;Percorso completo e nome file\>  

###  <a name="BKMK_UninstallLnUClient"></a> Disinstallazione del client da server Linux e UNIX  
 Per disinstallare il client di Configuration Manager per Linux e UNIX, usare l'utilità di disinstallazione, **uninstall**. Per impostazione predefinita, questo file si trova nel **/rifiutare/microsoft/configmgr/bin/** cartella nel computer client. Questo comando di disinstallazione non supporta i parametri della riga di comando e rimuoverà tutti i file relativi al software client dal server.  

 Per disinstallare il client, utilizzare la seguente riga di comando: **/opt/microsoft/configmgr/bin/uninstall**  

 Dopo aver disinstallato il client di Configuration Manager per Linux e UNIX, non è necessario riavviare il computer.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Configurare le porte richieste per il Client per Linux e UNIX  
 Come per i client basati su Windows, anche il client di Configuration Manager per Linux e UNIX usa HTTP e HTTPS per comunicare con i sistemi del sito di Configuration Manager. Le porte che il client di Configuration Manager usa per comunicare vengono definite porte di richiesta.  

 Quando si installa il client di Configuration Manager per Linux e UNIX, è possibile modificare le porte di richiesta predefinite del client specificando le proprietà di installazione **-httpport** e **-httpsport**. Quando non si specifica la proprietà di installazione e un valore personalizzato, il client utilizza i valori predefiniti. I valori predefiniti sono **80** per il traffico HTTP e **443** per il traffico HTTPS.  

 Dopo aver installato il client, è possibile modificare la configurazione della porta di richiesta. Per modificare la configurazione della porta è invece necessario reinstallare il client e specificare la nuova configurazione della porta. Quando si reinstalla il client per modificare i numeri di porta richiesta, eseguire il **installare** comando simile alla nuova installazione di client, ma utilizzare la proprietà della riga di comando aggiuntivi di **- keepdb**. Questa opzione indica l'installazione di mantenere i file inclusi nell'archivio GUID e il certificato client e un database client.  

 Per altre informazioni sui numeri di porta di comunicazione client, vedere [Come configurare porte di comunicazione client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Configurare il Client per Linux e UNIX individuare i punti di gestione  
 Quando si installa il client di Configuration Manager per Linux e UNIX, è necessario specificare un punto di gestione da usare come punto iniziale del contatto.  

 Il client di Configuration Manager per Linux e UNIX contatta il punto di gestione nel momento in cui viene installato il client. Se il client non riesce a contattare il punto di gestione, il software client continuerà a provare fino a quando non riesce.  

 Per altre informazioni sulle modalità con cui i client individuano i punti di gestione, vedere [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).
