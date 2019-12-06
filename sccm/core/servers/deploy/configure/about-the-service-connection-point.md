---
title: punto di connessione del servizio
titleSuffix: Configuration Manager
description: Informazioni sul ruolo di sistema del sito di Configuration Manager e pianificazione della gamma di usi.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: af65085590d8b02d6b3a020668566a334de42f13
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "67285562"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Informazioni sul punto di connessione del servizio in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il punto di connessione del servizio è un ruolo del sistema del sito che svolge diverse funzioni importanti per la gerarchia. Prima di configurare il punto di connessione del servizio, esaminare e pianificare i diversi usi. La pianificazione dell'utilizzo potrebbe influire sulla modalità di configurazione di questo ruolo del sistema del sito:  

- **Gestire i dispositivi mobili con Microsoft Intune**: questo ruolo sostituisce il connettore Microsoft Intune usato dalle versioni precedenti di Configuration Manager e può essere configurato con i dettagli della sottoscrizione di Intune. Per altre informazioni, vedere l'articolo relativo alla [gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Gestire i dispositivi mobili con MDM locale**: questo ruolo offre il supporto per i dispositivi locali gestiti che non si connettono a Internet. Per altre informazioni, vedere [Gestire i dispositivi mobili con l'infrastruttura locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Caricare i dati di utilizzo dall'infrastruttura di Configuration Manager**: è possibile controllare il livello di dettaglio dei dati caricati. I dati caricati consentono di:  

    - Identificare e risolvere i problemi in modo proattivo  

    - Migliorare i prodotti e il servizio  

    - Identificare gli aggiornamenti per Configuration Manager applicabili alla versione in uso  

    Per altre informazioni sui dati raccolti da ogni livello e su come modificare il livello di raccolta dopo l'installazione del ruolo, vedere [Dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Selezionare quindi il collegamento corrispondente alla versione di Configuration Manager in uso.  

    Per altre informazioni, vedere [Impostazioni e livelli per i dati di utilizzo](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Scaricare gli aggiornamenti applicabili all'infrastruttura di Configuration Manager**: vengono resi disponibili solo gli aggiornamenti rilevanti per l'infrastruttura, in base ai dati di utilizzo caricati.  

- **Ogni gerarchia supporta una sola istanza di questo ruolo:**  

    - Il ruolo del sistema del sito può essere installato solo nel sito di livello più alto della gerarchia, ovvero in un sito di amministrazione centrale o in un sito primario autonomo.  

    - Se si espande un sito primario autonomo in una gerarchia più ampia, è necessario disinstallare questo ruolo dal sito primario per poterlo quindi installare nel sito di amministrazione centrale.  


##  <a name="bkmk_modes"></a> Modalità di funzionamento  
Il punto di connessione del servizio supporta due modalità di funzionamento:  

- In **modalità online** il punto di connessione del servizio controlla automaticamente ogni 24 ore se sono presenti aggiornamenti. Scarica quindi i nuovi aggiornamenti disponibili per la versione corrente del prodotto e dell'infrastruttura, rendendoli disponibili nella console di Configuration Manager.  

- In **modalità offline**, il punto di connessione del servizio non si connette al servizio cloud Microsoft. Per importare manualmente gli aggiornamenti disponibili, usare lo [strumento di connessione del servizio](/sccm/core/servers/manage/use-the-service-connection-tool).  

Se si passa dalla modalità online a quella offline o viceversa dopo aver installato il punto di connessione del servizio, è necessario riavviare il thread SMS_DMP_DOWNLOADER del servizio SMS_Executive di Configuration Manager per rendere effettiva la modifica. È possibile usare Configuration Manager Service Manager per riavviare solo il thread SMS_DMP_DOWNLOADER del servizio SMS_Executive. È anche possibile riavviare il servizio SMS_Executive per Configuration Manager che riavvia la maggior parte dei componenti del sito. In alternativa, è possibile attendere l'esecuzione di un'attività pianificata, ad esempio un backup del sito che arresta e riavvia il servizio SMS_Executive.  

Per usare Configuration Manager Service Manager, nella console passare a **Monitoraggio** > **Stato sistema** > **Stato componente**, scegliere **Avvia** e quindi **Configuration Manager Service Manager**. In Service Manager:  

- Nel riquadro di spostamento espandere il sito, quindi espandere **Componenti** e infine scegliere il componente da riavviare.  

- Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sul componente e scegliere **Query**.  

- Dopo aver verificato lo stato del componente, fare di nuovo clic con il pulsante destro del mouse sul componente e quindi scegliere **Arresta**.  

- Ripetere la **query** sul componente per verificare che sia stato arrestato. Fare quindi di nuovo clic con il pulsante destro del mouse sul componente e scegliere **Avvia**.  

> [!IMPORTANT]  
> Il processo che aggiunge una sottoscrizione di Microsoft Intune al punto di connessione del servizio imposta automaticamente il ruolo del sistema del sito sulla modalità online. Il punto di connessione del servizio non supporta la modalità offline se è configurato con una sottoscrizione di Intune.  

**Quando il ruolo viene installato in un computer remoto rispetto al server del sito:**  

- L'account computer del server del sito deve essere un amministratore locale sul computer che ospita una connessione al servizio remoto.

- È necessario configurare il server del sistema del sito che ospita il ruolo con un account di installazione del sistema del sito.  

- Il responsabile della distribuzione nel server del sito usa l'account di installazione del sistema del sito per trasferire gli aggiornamenti dal punto di connessione del servizio.


## <a name="bkmk_urls"></a> Requisiti per l'accesso a Internet  

Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, è necessario consentire al punto di connessione del servizio di accedere agli endpoint Internet.

Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints#bkmk_scp).


## <a name="install-the-service-connection-point"></a>Installare il punto di connessione del servizio
Quando si esegue il **programma di installazione** per installare il sito di livello superiore di una gerarchia, viene offerta la possibilità di installare il punto di connessione del servizio.

Dopo l'esecuzione del programma di installazione, o se si reinstalla il ruolo del sistema del sito, usare l'**Aggiunta guidata ruoli del sistema del sito** o la **Creazione guidata server del sistema sito** per installare il sistema del sito in un server nel sito di livello più alto della gerarchia, ovvero il sito di amministrazione centrale o un sito primario autonomo. Entrambe le procedure guidate sono disponibili nella scheda **Home** della console, in **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito**.



## <a name="log-files-used-by-the-service-connection-point"></a>File di log usati dal punto di connessione del servizio
Per visualizzare informazioni sui caricamenti in Microsoft, visualizzare **Dmpuploader.log** nel computer che esegue il punto di connessione del servizio.  Per i download, incluso lo stato di avanzamento dei download degli aggiornamenti, visualizzare **Dmpdownloader.log**. Per l'elenco completo dei log correlati al punto di connessione del servizio, vedere [Punto di connessione del servizio](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) nell'articolo relativo ai file di log di Configuration Manager.

È inoltre possibile usare i diagrammi di flusso seguenti per comprendere il flusso del processo e le voci di log chiave per i download degli aggiornamenti e la replica degli aggiornamenti in altri siti:
- [Diagramma di flusso - scaricare gli aggiornamenti](/sccm/core/servers/manage/download-updates-flowchart)
- [Diagramma di flusso - replica di aggiornamento](/sccm/core/servers/manage/update-replication-flowchart)
