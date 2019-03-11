---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Knowledge Base del supporto tecnico Microsoft.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7e4307d61cccf968729f013ebaa4bfab4b0027e
ms.sourcegitcommit: 56ec6933cf7bfc93842f55835ad336ee3a1c6ab5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57211534"
---
# <a name="release-notes-for-configuration-manager"></a>Note sulla versione per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora stati risolti nel prodotto né trattati in dettaglio in un articolo della Knowledge Base del supporto tecnico Microsoft.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

Questo argomento contiene le note sulla versione di Configuration Manager (Current Branch). Per informazioni sul Technical Preview Branch, vedere [Technical Preview](/sccm/core/get-started/technical-preview)  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:
- [Novità della versione 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novità della versione 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novità della versione 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`



## <a name="set-up-and-upgrade"></a>Configurazione e aggiornamento  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Quando si usano file ridistribuibili dalla cartella CD.Latest, l'installazione non riesce con un errore di verifica del manifesto
<!-- 510080, 490569  -->

Quando si esegue il programma di installazione dalla cartella CD.Latest creata per la versione 1606 e si usano i file ridistribuibili inclusi in tale cartella, l'esecuzione del programma di installazione non riesce e restituisce gli errori seguenti nel registro di installazione di Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Soluzione alternativa
Usare una delle opzioni seguenti:
 - Durante l'installazione, scegliere di scaricare i file ridistribuibili più aggiornati da Microsoft. Usare i file ridistribuibili più recenti invece di quelli inclusi nella cartella CD.Latest.
 - Eliminare manualmente la cartella *cd.latest\redist\languagepack\zhh* ed eseguire di nuovo l'installazione.


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
*Si applica a: Configuration Manager versione 1810*

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


### <a name="changing-office-365-client-setting-doesnt-apply"></a>La modifica dell'impostazione client di Office 365 non è applicabile 
<!--511551-->
*Si applica a: Configuration Manager versione 1802*  

Distribuire un'[impostazione client](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) con **Abilitare la gestione dell'agente del client Office 365** impostato su `Yes`. Modificare quindi tale impostazione in `No` o `Not Configured`. Dopo l'aggiornamento dei criteri nei client di destinazione, gli aggiornamenti di Office 365 vengono ancora gestiti da Configuration Manager. 

#### <a name="workaround"></a>Soluzione alternativa
Impostare il valore del Registro di sistema seguente su `0` e riavviare il **Servizio A portata di clic di Microsoft Office** (ClickToRunSvc):

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Gestione di dispositivi mobili  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Non è più possibile distribuire profili VPN di Windows Phone 8.1 in Windows 10
<!-- 503274  -->
*Si applica a: Configuration Manager versione 1710*

Non è più possibile creare un profilo VPN tramite il flusso di lavoro di Windows Phone 8.1 che sia applicabile anche a dispositivi Windows 10. Per questi profili, la procedura guidata di creazione non visualizza più la pagina Piattaforme supportate. Windows Phone 8.1 è selezionato automaticamente nel back-end. La pagina Piattaforme supportate è disponibile nelle proprietà del profilo ma non visualizza le opzioni di Windows 10.

#### <a name="workaround"></a>Soluzione alternativa
 Per i dispositivi Windows 10 usare il flusso di lavoro del profilo VPN di Windows 10. Se questa opzione non è praticabile nell'ambiente in uso, contattare il supporto tecnico, che indicherà come aggiungere la destinazione Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
