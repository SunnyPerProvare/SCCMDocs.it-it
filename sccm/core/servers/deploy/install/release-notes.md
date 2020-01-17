---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Knowledge Base del supporto tecnico Microsoft.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bc899b6732d3fca21e35f82906001f25a942a4d6
ms.sourcegitcommit: cf978bfea545ed9116dacadfac830cbb08aaa649
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2020
ms.locfileid: "75951612"
---
# <a name="release-notes-for-configuration-manager"></a>Note sulla versione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora stati risolti nel prodotto né trattati in dettaglio in un articolo della Knowledge Base del supporto tecnico Microsoft.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

Questo articolo include note sulla versione per l'edizione Current Branch di Configuration Manager. Per informazioni sul Technical Preview Branch, vedere [Technical Preview](/sccm/core/get-started/technical-preview)  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:

- [Novità della versione 1910](/sccm/core/plan-design/changes/whats-new-in-version-1910)
- [Novità della versione 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906)  
- [Novità della versione 1902](/sccm/core/plan-design/changes/whats-new-in-version-1902)
- [Novità della versione 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`


## <a name="set-up-and-upgrade"></a>Configurazione e aggiornamento  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>L'aggiornamento automatico del client avviene immediatamente per tutti i client

<!-- 6040412 -->

*Si applica alla versione 1910*

Se il sito usa l'[aggiornamento automatico del client](/configmgr/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade), quando si aggiorna il sito alla versione 1910, tutti i client vengono immediatamente aggiornati dopo che il sito è stato aggiornato correttamente. L'unica impostazione casuale è quando i client ricevono i criteri, cosa che per impostazione predefinita avviene ogni ora. Per un sito di grandi dimensioni con molti client, questo comportamento può comportare l'utilizzo di una quantità significativa di traffico di rete e un sovraccarico dei punti di distribuzione.

Per risolvere questo problema, disabilitare temporaneamente l'aggiornamento automatico del client. Usare altri [metodi di aggiornamento del client](/configmgr/core/clients/manage/upgrade/upgrade-clients). Microsoft rilascerà presto un hotfix per questo problema per consentire di continuare a usare l'aggiornamento automatico del client.

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Il server del sito in modalità passiva non aggiorna configuration.mof

<!-- 5787848 -->

*Si applica alla versione 1910*

Se il sito include un [server del sito in modalità passiva](/configmgr/core/servers/deploy/configure/site-server-high-availability), quando si aggiorna il sito è possibile che le personalizzazioni dell'inventario vadano perse. Quando si esegue il failover dei server del sito, il sito non sincronizza il file configuration.mof.

Per risolvere questo problema, eseguire manualmente il backup e il ripristino del file configuration.mof del sito.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Avviso di prerequisito di installazione relativo al livello di funzionalità del dominio nell'edizione Server 2019

<!-- 4904376 -->

*Si applica alla versione 1906*

Quando si installa l'aggiornamento per la versione 1906 in un ambiente con controller di dominio che eseguono Windows Server 2019, il controllo dei prerequisiti per il livello di funzionalità del dominio restituisce l'avviso seguente:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

#### <a name="workaround"></a>Soluzione alternativa

Ignorare l'avviso.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>L'individuazione utenti e la sincronizzazione delle raccolte con i gruppi di Azure AD non funzionano dopo l'espansione del sito

<!-- 4797313 -->
*Si applica alla versione 1906*

Dopo aver configurato una delle funzionalità seguenti:

- Individuazione dei gruppi utenti in Azure Active Directory
- Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory

se si espande un sito primario autonomo a una gerarchia con un sito di amministrazione centrale, verrà visualizzato l'errore seguente in SMS_AZUREAD_DISCOVERY_AGENT. log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

#### <a name="workaround"></a>Soluzione alternativa

Rinnovare la chiave associata alla registrazione dell'app in Azure AD. Per altre informazioni, vedere [Rinnovare la chiave privata](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente di gestione del servizio cloud arrestato nel server del sito in modalità passiva

<!--VSO 2858826, SCCMDocs issue 772-->
*Si applica a: Configuration Manager versione 1806*

Se il [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) si trova nella stessa posizione di un [server del sito in modalità passiva](/sccm/core/servers/deploy/configure/site-server-high-availability), la distribuzione e il monitoraggio di un [gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) non vengono avviati. Il componente di gestione del servizio cloud (SMS_CLOUD_SERVICES_MANAGER) è nello stato arrestato.

#### <a name="workaround"></a>Soluzione alternativa

Spostare il ruolo del punto di connessione del servizio in un altro server.


<!-- ## Backup and recovery  -->

<!--## Client deployment and upgrade-->
## <a name="application-management"></a>Gestione delle applicazioni

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Non è possibile ottenere il certificato per l'errore di PowerShell durante la distribuzione di Microsoft Edge, versione 77 e successive
<!--5769384-->
*Si applica a: Configuration Manager versione 1910*

Se si esegue la console di Configuration Manager in un sistema operativo in lingua svedese, ungherese o giapponese, durante la distribuzione di Microsoft Edge, versione 77 e successive, verrà restituito l'errore seguente:

- Non è possibile ottenere il certificato per PowerShell

Questo errore si verifica perché non esiste una cartella `scripts` nella directory `AdminConsole\bin` per la lingua svedese, ungherese o giapponese. In queste lingue del sistema operativo la cartella scripts è localizzata.

#### <a name="workaround"></a>Soluzione alternativa

Creare una cartella denominata `scripts` nella directory `AdminConsole\bin`. Copiare i file dalla cartella localizzata nella nuova cartella `scripts` creata. Distribuire Microsoft Edge, versione 77 e successive, dopo aver copiato i file.


## <a name="os-deployment"></a>Distribuzione del sistema operativo

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Dopo che il server del sito passivo viene alzato di livello, i pacchetti di immagini di avvio predefiniti hanno ancora come origini dei pacchetti il server attivo precedente

<!--3453224, SCCMDocs-pr issue 3097-->
*Si applica a: Configuration Manager versione 1810*

Se si ha un server del sito in modalità passiva (server B), quando lo si alza di livello alla modalità attiva il percorso del contenuto per le immagini d'avvio predefinite continua a fare riferimento al server attivo in precedenza (server A). Se il server A registra un errore hardware non è possibile aggiornare o modificare le immagini d'avvio predefinite.

#### <a name="workaround"></a>Soluzione alternativa

Nessuno


## <a name="software-updates"></a>Aggiornamenti software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Non sono presenti ruoli di sicurezza per le distribuzioni in più fasi

<!--3479337, SCCMDocs-pr issue 3095-->
*Si applica a: Configuration Manager versioni 1810, 1902*

Il ruolo di sicurezza predefinito **Gestione distribuzione del sistema operativo** dispone di autorizzazioni per le [distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). I ruoli seguenti non dispongono di queste autorizzazioni:  

- **Amministratore applicazione**  
- **Gestione distribuzione applicazioni**  
- **Amministratore aggiornamento software**  

Per il ruolo **Autore di app** potrebbero risultare alcune autorizzazioni per le distribuzioni in più fasi, ma questo ruolo non dovrebbe essere in grado di creare distribuzioni.

Un utente con uno di questi ruoli può avviare la procedura guidata Crea una distribuzione in più fasi e visualizzare distribuzioni in più fasi per un'applicazione o un aggiornamento software. Non sarà tuttavia in grado di completare la procedura guidata o apportare modifiche a una distribuzione esistente.

#### <a name="workaround"></a>Soluzione alternativa

Creare un ruolo di sicurezza personalizzato. Copiare un ruolo di sicurezza esistente e aggiungere le autorizzazioni seguenti nella classe oggetto **Distribuzione in più fasi**:

- Creazione  
- Elimina  
- Modifica  
- Lettura  

Per altre informazioni, vedere [Creare ruoli di sicurezza personalizzati](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Se si usa l'inventario hardware per le viste distribuite, non è possibile eseguire l'onboarding in Desktop Analytics

<!-- 4950335 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo e versione 1906*

Se si ha una gerarchia e si abilitano i dati del sito **Inventario hardware** per le [viste distribuite](/sccm/core/plan-design/hierarchy/database-replication#bkmk_distviews) sui collegamenti di replica siti, dopo aver configurato la connessione a Desktop Analytics in Configuration Manager verrà visualizzato l'errore seguente in M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

#### <a name="workaround"></a>Soluzione alternativa

Disabilitare i dati del sito **Inventario hardware** per le viste distribuite su tutti i collegamenti di replica siti.


### <a name="console-unexpectedly-closes-when-removing-collections"></a>La console si chiude in modo imprevisto durante la rimozione di raccolte

<!-- 4749443 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo*

Dopo aver connesso il sito a [Desktop Analytics](/sccm/desktop-analytics/connect-configmgr), è possibile abilitare l'opzione can **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**. Se si rimuove una raccolta e si applicano le modifiche, l'aggiunta immediata di una nuova raccolta causa un'eccezione non gestita. La console si chiude in modo imprevisto.

#### <a name="workaround"></a>Soluzione alternativa

Quando si rimuove una raccolta, scegliere **OK** per chiudere la finestra delle proprietà. Aprire quindi di nuovo la finestra delle proprietà per aggiungere una nuova raccolta nella scheda **Connessione di Desktop Analytics** .

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Il riquadro dello stato della distribuzione pilota visualizza alcuni dispositivi come 'non definiti'

<!-- 4547783 -->
*Si applica a: Configuration Manager versione 1902 con aggiornamento cumulativo*

Quando si usa la console di Configuration Manager per monitorare lo stato della distribuzione pilota, i dispositivi pilota aggiornati nella versione di destinazione di Windows per il piano di distribuzione vengono visualizzati come **non definiti** nel riquadro dello stato della distribuzione pilota.  

Questi dispositivi **non definiti** sono **aggiornati** con la versione di destinazione del sistema operativo per il piano di distribuzione. Non sono richieste ulteriori azioni.

## <a name="cloud-services"></a>Servizi cloud

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Non è possibile scaricare contenuti da un gateway di gestione cloud abilitato per TLS 1.2

<!-- 5771680 -->

*Si applica alle versioni 1906, 1910 anello di aggiornamento anticipato*

Se si abilita un gateway di gestione cloud in modo che **funzioni come punto di distribuzione cloud e gestisca i contenuti di Archiviazione di Azure** ed **Enforce TLS 1.2**, è possibile che il download dei contenuti non riesca.

Nel file DataTransferService.log del client verranno riportati gli errori seguenti:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

Nel file CMGContentService.log del server verranno riportati gli errori seguenti:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Come soluzione alternativa a questo problema:

- Aggiornare il sito alla versione disponibile a livello globale 1910, rilasciata il 20 dicembre 2019. Se in precedenza è stato eseguito l'aggiornamento all'anello di aggiornamento anticipato della versione 1910, è necessario eseguire l'aggiornamento a questa build quando è disponibile.

- In alternativa, usare un [punto di distribuzione cloud](/configmgr/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) tradizionale. Tale ruolo non impone l'uso di TLS 1.2, ma è compatibile con i client che richiedono TLS 1.2.
