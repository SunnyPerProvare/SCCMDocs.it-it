---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Knowledge Base del supporto tecnico Microsoft.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a21fcce7d5e8db66a7e85c14c0ef4ad1050b342c
ms.sourcegitcommit: 4316bff400ffbde8404f8a2092ec17e3601b8d29
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70738426"
---
# <a name="release-notes-for-configuration-manager"></a>Note sulla versione per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora stati risolti nel prodotto né trattati in dettaglio in un articolo della Knowledge Base del supporto tecnico Microsoft.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

Questo articolo include note sulla versione per l'edizione Current Branch di Configuration Manager. Per informazioni sul Technical Preview Branch, vedere [Technical Preview](/sccm/core/get-started/technical-preview)  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:

- [Novità della versione 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906)  
- [Novità della versione 1902](/sccm/core/plan-design/changes/whats-new-in-version-1902)
- [Novità della versione 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novità della versione 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`


## <a name="set-up-and-upgrade"></a>Configurazione e aggiornamento  

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


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>È necessario specificare l'opzione della riga di comando del programma di installazione JoinCEIP

<!--510806-->
*Si applica a: Configuration Manager versione 1802*

A partire da Configuration Manager versione 1802, la funzionalità Analisi utilizzo software è stata rimossa dal prodotto. Quando si esegue l'[automazione dell'installazione](/sccm/core/servers/deploy/install/command-line-options-for-setup) di un nuovo sito dalla riga di comando o da uno script automatico, il programma di installazione restituisce un errore relativo alla mancanza di un parametro obbligatorio.

#### <a name="workaround"></a>Soluzione alternativa

Anche se non produce alcun effetto sul risultato del processo di installazione, includere il parametro **JoinCEIP** nella riga di comando del programma di installazione.

> [!Note]  
> Il parametro EnableSQM per il [programma di installazione della console](/sccm/core/servers/deploy/install/install-consoles) non è necessario.

### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente di gestione del servizio cloud arrestato nel server del sito in modalità passiva

<!--VSO 2858826, SCCMDocs issue 772-->
*Si applica a: Configuration Manager versione 1806*

Se il [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) si trova nella stessa posizione di un [server del sito in modalità passiva](/sccm/core/servers/deploy/configure/site-server-high-availability), la distribuzione e il monitoraggio di un [gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) non vengono avviati. Il componente di gestione del servizio cloud (SMS_CLOUD_SERVICES_MANAGER) è nello stato arrestato.

#### <a name="workaround"></a>Soluzione alternativa

Spostare il ruolo del punto di connessione del servizio in un altro server.


<!-- ## Backup and recovery  -->

<!--## Client deployment and upgrade-->


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

### <a name="changing-office-365-client-setting-doesnt-apply"></a>La modifica dell'impostazione client di Office 365 non si applica

<!--511551-->
*Si applica a: Configuration Manager versione 1802*  

Distribuire un'[impostazione client](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) con **Abilitare la gestione dell'agente del client Office 365** impostato su `Yes`. Modificare quindi tale impostazione in `No` o `Not Configured`. Dopo l'aggiornamento dei criteri nei client di destinazione, gli aggiornamenti di Office 365 vengono ancora gestiti da Configuration Manager.

#### <a name="workaround"></a>Soluzione alternativa

Impostare il valore del Registro di sistema seguente su `0` e riavviare il **Servizio A portata di clic di Microsoft Office** (ClickToRunSvc):

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```

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


## <a name="mobile-device-management"></a>Gestione di dispositivi mobili  

### <a name="validation-for-ios-app-link-sometimes-fails-on-valid-link"></a>Talvolta si verifica un errore di convalida per il collegamento dell'app iOS anche se il collegamento è valido

*Si applica a: Configuration Manager versione 1810 e precedenti*

<!-- LSI 106004348 -->
Quando si crea una nuova applicazione di tipo **Pacchetto app per iOS nell'App Store**, il validator non accetta alcuni URL validi come **Percorso**. In particolare, l'App Store iOS non richiede un valore per la sezione dell'URL relativa al nome dell'app. Ad esempio, entrambi i collegamenti seguenti sono validi e puntano alla stessa app, ma la **Creazione guidata applicazione** accetta solo il primo:

- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### <a name="workaround"></a>Soluzione alternativa

Quando si crea un'app iOS e il nome dell'app non è presente nell'URL, aggiungere qualsiasi valore nell'URL come se fosse il nome dell'app. Ad esempio:

- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

Questa azione consente di completare la procedura guidata. L'app viene comunque distribuita correttamente nei dispositivi iOS. La stringa aggiunta all'URL viene visualizzata come **Nome** nella scheda **Informazioni generali** della procedura guidata. Corrisponde anche all'etichetta dell'app nel Portale aziendale.




<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->

<!-- ## Endpoint Protection -->
