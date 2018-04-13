---
title: Note sulla versione
titleSuffix: Configuration Manager
description: Informazioni su problemi urgenti non ancora risolti nel prodotto o trattati in un articolo della Microsoft Knowledge Base.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e22bc4818f10a1f60fdb2135eb705e46dbaa10a4
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Note sulla versione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con Configuration Manager le note sulla versione del prodotto sono limitate ai problemi urgenti. Questi problemi non sono ancora risolti nel prodotto né trattati in dettaglio in un articolo della Microsoft Knowledge Base.  

La documentazione specifica delle funzionalità include informazioni sui problemi noti che interessano gli scenari di base.  

> [!TIP]  
>  Questo argomento contiene le note sulla versione di Configuration Manager (Current Branch). Per informazioni sul Technical Preview Branch, vedere [Technical Preview per System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Per informazioni sulle nuove funzionalità introdotte con le diverse versioni, vedere gli articoli seguenti:
- [Novità della versione 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novità della versione 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novità della versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



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
<!--also fixed in 1710 HFRU-->
Nello scenario relativo all'[installazione e all'assegnazione di client Windows 10 di Configuration Manager usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure), la comunicazione client ha esito negativo se il punto di gestione abilitato per HTTPS usa credenziali alternative per il database. 

#### <a name="workaround"></a>Soluzione alternativa
Attenuare il problema con una delle azioni seguenti:
- Aggiornare il sito alla versione più recente e applicare l'hotfix più recente
- Modificare le credenziali usate dal punto di gestione.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Aggiornamenti software

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>I piani di manutenzione creano molte distribuzioni e molti gruppi di aggiornamento software duplicati per impostazione predefinita  
<!-- 474326 -->
Per impostazione predefinita, la procedura guidata Crea piano di manutenzione viene attualmente eseguita dopo ogni sincronizzazione degli aggiornamenti software. A ogni esecuzione, la procedura guidata crea un nuovo gruppo di aggiornamento software e una nuova distribuzione. Se la pianificazione della sincronizzazione degli aggiornamenti software viene eseguita diverse volte al giorno, la procedura guidata Crea piano di manutenzione crea più distribuzioni e gruppi di aggiornamento software ogni giorno.  

#### <a name="workaround"></a>Soluzione alternativa
 dopo aver creato un piano di manutenzione, aprire le proprietà del piano, passare alla scheda **Pianificazione valutazione**, selezionare **Esegui la regola in base a una pianificazione**, fare clic su **Personalizza** e quindi creare una pianificazione personalizzata. Ad esempio, è possibile impostare l'esecuzione del piano di manutenzione ogni 60 giorni.  



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
