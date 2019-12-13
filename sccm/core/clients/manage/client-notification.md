---
title: Notifica client
titleSuffix: Configuration Manager
description: Gestire i client intraprendendo azioni immediate dalla console centrale di Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 770b25908512c8a9be475c4276cde8bbddbb85d2
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74658473"
---
# <a name="client-notification-in-configuration-manager"></a>Notifica del client in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Agire immediatamente sui client remoti, inviare un'azione di notifica client dalla console di Configuration Manager. Avviare queste azioni su un singolo dispositivo o su una raccolta di dispositivi.

## <a name="actions"></a>Azioni

Le azioni seguenti sono disponibili nella barra multifunzione del gruppo Dispositivi o Raccolta della scheda Home.

### <a name="install-client"></a>Installa client

Apre la **procedura guidata Installa client**. Questa procedura guidata usa l'installazione push client per installare un client di Configuration Manager. Per altre informazioni, vedere [Installazione push client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>Autorizzazioni - Installa client

Questa azione richiede le autorizzazioni **Modifica risorsa** e **Lettura** per l'oggetto **Raccolta**.

I ruoli predefiniti seguenti hanno queste autorizzazioni per impostazione predefinita:

- Amministratore applicazione  
- Amministratore completo  
- Amministratore infrastruttura  
- Amministratore operazioni  
- Gestione distribuzione del sistema operativo  

Aggiungere queste autorizzazioni a tutti i ruoli personalizzati che devono eseguire l'installazione push client.

### <a name="run-script"></a>Esegui script

Apre la procedura guidata **Esegui script** per eseguire uno script di PowerShell in tutti i client della raccolta. Per altre informazioni, vedere [Creare ed eseguire script di PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

#### <a name="permissions---run-script"></a>Autorizzazioni - Esegui script

Questa azione richiede l'autorizzazione **Esegui script** per l'oggetto **Raccolta**.

I ruoli predefiniti seguenti hanno questa autorizzazione per impostazione predefinita:

- Amministratore completo  
- Amministratore infrastruttura  
- Amministratore operazioni  

Aggiungere questa autorizzazione ai ruoli personalizzati che devono eseguire degli script.

### <a name="start-cmpivot"></a>Avviare CMPivot

Avvia **CMPivot**, che esegue query in tempo reale sui dispositivi di destinazione. Per altre informazioni, vedere [CMPivot](/sccm/core/servers/manage/cmpivot).

#### <a name="permissions---start-cmpivot"></a>Autorizzazioni - Avvia CMPivot

Questa azione richiede le stesse autorizzazioni dell'azione [Esegui script](#run-script).

A partire dalla versione 1906, è possibile usare l'autorizzazione **Esegui CMPivot** nell'oggetto **Raccolta**.

## <a name="client-notification"></a>Notifica client

Le azioni seguenti sono disponibili nel menu **Notifica client**, nella barra multifunzione del gruppo Dispositivi o Raccolta della scheda Home.

Nella versione 1806 o nelle versioni precedenti, l'opzione **Notifica client** è disponibile solo dal nodo Raccolta di dispositivi oppure quando si visualizza l'appartenenza di una raccolta di dispositivi. A partire dalla versione 1810, l'opzione **Notifica client** è disponibile direttamente nel nodo **Dispositivi**. Non è più un requisito essere all'interno di una visualizzazione di appartenenza della raccolta. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Autorizzazioni - Notifica client

<!--SCCMDocs-pr issue #2972-->
A partire dalla versione 1810, per le azioni di notifica client ora è necessaria l'autorizzazione **Invia una notifica alla risorsa** per l'oggetto Raccolta. Questa autorizzazione è applicabile a tutte le azioni del menu **Notifica client**.

I ruoli predefiniti seguenti hanno questa autorizzazione per impostazione predefinita:

- Amministratore completo  
- Amministratore operazioni  

Aggiungere questa autorizzazione ai ruoli personalizzati che devono usare le azioni di notifica client.

### <a name="download-computer-policy"></a>Scarica criteri computer

Aggiornare i criteri del dispositivo. Per altre informazioni, vedere [Avviare il recupero criteri per un client di Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Scarica criteri utente

Aggiornare i criteri dell'utente.  

### <a name="collect-discovery-data"></a>Raccogli dati di individuazione

Attivare i client per l'invio di un record dei dati di individuazione. Per altre informazioni, vedere [Individuazione heartbeat](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

### <a name="collect-software-inventory"></a>Raccogli l'inventario software

Attivare i client per l'esecuzione di un ciclo di inventario software. Per altre informazioni, vedere [Introduzione all'inventario software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

### <a name="collect-hardware-inventory"></a>Raccogliere l'inventario hardware

Attivare i client per l'esecuzione di un ciclo di inventario hardware. Per altre informazioni, vedere [Introduzione all'inventario hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

### <a name="evaluate-application-deployments"></a>Valuta le distribuzioni dell'applicazione

Attivare i client per l'esecuzione di un ciclo di valutazione delle distribuzioni dell'applicazione. Per altre informazioni, vedere [Pianificare nuova valutazione per le distribuzioni](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Valuta le distribuzioni di aggiornamento software

Attivare i client per l'esecuzione di un ciclo di valutazione delle distribuzioni degli aggiornamenti software. Per altre informazioni, vedere [Introduzione agli aggiornamenti software](/sccm/sum/understand/software-updates-introduction).  

### <a name="switch-to-the-next-software-update-point"></a>Passare al punto di aggiornamento software successivo

Attivare i client per il passaggio al successivo punto di aggiornamento software disponibile. Per altre informazioni, vedere [Passaggio a un nuovo punto di aggiornamento software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Valuta l'attestazione dell'integrità del dispositivo

Attivare i client di Windows 10 per il controllo e l'invio dello stato dell'integrità del dispositivo più recente. Per altre informazioni, vedere [Attestazione dell'integrità](/sccm/core/servers/manage/health-attestation).  

### <a name="check-conditional-access-compliance"></a>Controlla la conformità dell'accesso condizionale

Attivare i client per il controllo della conformità dell'accesso condizionale. Per altre informazioni, vedere [Gestire l'accesso ai servizi di Office 365 per i PC](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

### <a name="wake-up"></a>Riattiva

A partire dalla versione 1810, è possibile attivare i dispositivi configurati per supportare la riattivazione LAN usando altri dispositivi nella stessa subnet per inviare il pacchetto di riattivazione LAN. Per altre informazioni, vedere [Come configurare la riattivazione LAN](/sccm/core/clients/deploy/configure-wake-on-lan).

### <a name="restart"></a>Riavvia

Attivare i dispositivi selezionati per riavviarli. Per altre informazioni, vedere [Riavviare i client](/sccm/core/clients/manage/manage-clients#restart-clients).

## <a name="client-diagnostics"></a>Diagnostica client

<!--4433455-->

A partire dalla versione 1910, sono disponibili nuove azioni del dispositivo per **Diagnostica client** nella console di Configuration Manager. Questa versione include le azioni seguenti:

- **Abilita la registrazione dettagliata**: modificare il livello di registrazione per il componente CCM da globale a dettagliata e abilitare la registrazione debug.
- **Disabilita la registrazione dettagliata**: modificare il livello di registrazione da globale a predefinita e disabilitare la registrazione debug.

> [!IMPORTANT]
> Queste azioni modificano solo il livello di dettaglio dei log, non le dimensioni o la cronologia. Una registrazione più dettagliata può generare un maggior contenuto dei log.

Per altre informazioni su queste impostazioni, vedere [Informazioni sui file di log](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-client).

> [!NOTE]
> Anche il ruolo del punto di gestione usa il componente CCM. Se il dispositivo di destinazione è anche un punto di gestione, questa azione si applica anche a tale ruolo.

Tenere traccia dello stato dell'attività in **diagnostics.log** nel client.

### <a name="prerequisites---client-diagnostics"></a>Prerequisiti - Diagnostica client

- Aggiornare il client di destinazione alla versione più recente.

- L'utente amministratore di Configuration Manager necessita dell'autorizzazione **Invia una notifica alla risorsa**.

  I ruoli predefiniti seguenti hanno questa autorizzazione per impostazione predefinita:

  - Amministratore completo  
  - Amministratore infrastruttura  

  Aggiungere questa autorizzazione ai ruoli personalizzati che devono usare le azioni di notifica client.

## <a name="endpoint-protection"></a>Endpoint Protection

Le azioni seguenti sono disponibili nel menu **Endpoint Protection**. Il menu si trova nella barra multifunzione del gruppo Raccolta della scheda Home. Quando si selezionano uno o più dispositivi, queste azioni si trovano nella scheda **Oggetto selezionato** della barra multifunzione.

Per altre informazioni, vedere [Endpoint Protection in Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

### <a name="permissions---endpoint-protection"></a>Autorizzazioni - Endpoint Protection

Questa azione richiede l'autorizzazione **Applica protezione** per l'oggetto **Raccolta**.

I ruoli predefiniti seguenti hanno questa autorizzazione per impostazione predefinita:

- Amministratore completo  
- Endpoint Protection Manager  
- Amministratore operazioni  

Aggiungere questa autorizzazione ai ruoli personalizzati che devono attivare azioni di Endpoint Protection.

### <a name="full-scan"></a>Analisi completa

Attivare Endpoint Protection o Windows Defender per l'esecuzione di un'analisi antimalware *completa*.  

### <a name="quick-scan"></a>Analisi veloce

Attivare Endpoint Protection o Windows Defender per l'esecuzione di un'analisi antimalware *veloce*.  

### <a name="download-definition"></a>Scarica definizione

Attivare Endpoint Protection o Windows Defender per il download delle definizioni antimalware più recenti.  

## <a name="see-also"></a>Vedere anche

- [Come gestire i client](/sccm/core/clients/manage/manage-clients)
- [Come gestire le raccolte](/sccm/core/clients/manage/collections/manage-collections)
