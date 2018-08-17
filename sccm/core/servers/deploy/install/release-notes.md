---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Microsoft Knowledge Base.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9daf0fb53face0cf7ed56f2a45ab044fbfac203c
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385508"
---
# <a name="release-notes-for-configuration-manager"></a>Note sulla versione per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora risolti nel prodotto né trattati in dettaglio in un articolo della Microsoft Knowledge Base.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

> [!TIP]  
>  Questo argomento contiene le note sulla versione di Configuration Manager (Current Branch). Per informazioni sul Technical Preview Branch, vedere [Technical Preview](../../../../core/get-started/technical-preview.md)  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:
- [Novità della versione 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novità della versione 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novità della versione 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)



## <a name="setup-and-upgrade"></a>Configurazione e aggiornamento  


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



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Distribuzione e aggiornamento del client

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>I client abilitati per Azure AD non riescono a comunicare con il punto di gestione
<!--501089-->
*Si applica a: Configuration Manager versione 1706*
<!--also fixed in 1710 HFRU--> Nello scenario relativo all'[installazione e all'assegnazione di client Windows 10 di Configuration Manager usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure), la comunicazione client ha esito negativo se il punto di gestione abilitato per HTTPS usa credenziali alternative per il database. 

#### <a name="workaround"></a>Soluzione alternativa
Attenuare il problema con una delle azioni seguenti:
- Aggiornare il sito alla versione più recente e applicare l'hotfix più recente
- Modificare le credenziali usate dal punto di gestione.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Aggiornamenti software

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
