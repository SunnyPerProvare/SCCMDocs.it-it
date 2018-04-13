---
titleSuffix: Configuration Manager
description: Informazioni sulla funzionalità di Informazioni dettagliate sulla gestione disponibile nella console di Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2d6a58bd5aba873ea35c5bcf511a3cc22514b51
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Informazioni dettagliate sulla gestione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Informazioni dettagliate sulla gestione in System Center Configuration Manager offre informazioni sullo stato attuale dell'ambiente. Le informazioni si basano sull'analisi dei dati presenti nel database del sito. Le informazioni dettagliate aiutano a capire meglio l'ambiente e a intervenire di conseguenza. Questa funzionalità è stata rilasciata in Configuration Manager versione 1802. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Rivedere le Informazioni dettagliate sulla gestione nella console di Configuration Manager 
L'autorizzazione di **lettura del sito** è necessaria per visualizzare le regole.

1. Aprire la console di Configuration Manager. 
2. Passare al nodo **Amministrazione** e fare clic su **Informazioni dettagliate sulla gestione**.
3. Selezionare **All Insights** (Tutte le informazioni dettagliate)
4. Fare doppio clic sul **Nome del gruppo di informazioni dettagliate sulla gestione** che si desidera esaminare. In alternativa, evidenziarlo e fare clic su **Mostra i dettagli** nella barra multifunzione. 
5. Sono disponibili quattro schede per la revisione insieme ai prerequisiti necessari per eseguire la regola. 
    - **Tutte le regole**: offre l'elenco completo delle regole per il gruppo di informazioni dettagliate di gestione scelto.
    - **Completa**: elenca le regole in cui non è necessaria alcuna azione. 
    - **In corso**: mostra le regole in cui alcuni, ma non tutti i prerequisiti sono soddisfatti.
    - **Azione richiesta**: sono elencate le regole che richiedono le azioni adottate. Fare clic con il pulsante destro del mouse e scegliere **Altri dettagli** per recuperare elementi specifici in cui è necessaria un'azione. 
    - **Prerequisiti**: se una regola richiede il completamento di elementi prima che possano eseguiti, gli elementi richiesti saranno elencati qui.   
    
    **Tutte le regole e i prerequisiti per il gruppo di servizi cloud** ![Informazioni dettagliate sulla gestione- Tutte le regole e i prerequisiti per il gruppo di servizi cloud](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Nuova valutazione e registro delle informazioni dettagliate sulla gestione
Le regole delle informazioni dettagliate sulla gestione rivalutano la loro applicabilità a una pianificazione settimanale. È possibile valutare nuovamente una regola su richiesta facendo clic con il pulsante destro del mouse sulla regola e selezionando **Valuta di nuovo**.

**File di registro per le regole di informazioni dettagliate sulla gestione**: SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Gruppi e regole di informazioni dettagliate sulla gestione
Le regole sono organizzate in diversi gruppi di informazioni dettagliate sulla gestione. Quando vengono aggiunti gruppi e regole, vengono inclusi nell'elenco seguente:

**Applicazioni**: informazioni dettagliate per la gestione dell'applicazione.

- **Applicazioni senza distribuzioni**: elenca le applicazioni dell'ambiente senza distribuzioni attive. Questa regola aiuta a individuare ed eliminare le applicazioni non usate per semplificare l'elenco di applicazioni visualizzato nella console. 

**Servizi cloud**: consente l'integrazione con molti servizi cloud; abilitazione moderna della gestione dei dispositivi. 
 - **Valutare la preparazione alla co-gestione** - Consente di comprendere quali passaggi sono necessari per abilitare la gestione di condivisione. Questa regola ha dei prerequisiti. 
 - **Abilitare i dispositivi per l'aggiunta ad Azure Active Directory ibrido** -I dispositivi aggiunti a un Active Directory di Azure consentono agli utenti di accedere con le credenziali del dominio garantendo al contempo che i dispositivi soddisfino gli standard di sicurezza e conformità dell'organizzazione. 
 - **Modernizzare l'infrastruttura di identità e accesso** -Il servizio cloud di Azure AD con l'autenticazione a più fattori integrata protegge i dati sensibili e le applicazioni sia in locale che nel cloud. 
 - **Aggiornare i client a Windows 10, versione 1709 o successiva** -Windows 10, versione 1709 o versioni successive, migliora e modernizza l'esperienza di elaborazione degli utenti. 


**Raccolte**: informazioni dettagliate che consentono di semplificare la gestione tramite la pulizia e la riconfigurazione delle raccolte.
   - **Raccolte vuote**: elenco delle raccolte dell'ambiente che non hanno membri. 

**Gestione semplificata**: informazioni dettagliate che consentono di semplificare la gestione quotidiana del proprio ambiente. 
   - **Versioni client obsolete**: vengono elencati tutti i client le cui versioni hanno più di due anni. 

**Software Center**: informazioni dettagliate per la gestione di Software Center. 
   - **Indirizzare gli utenti a Software Center anziché al Catalogo applicazioni** -controlla se gli utenti hanno installato o richiesto applicazioni dal Catalogo applicazioni negli ultimi 14 giorni. La funzionalità principale del Catalogo applicazioni è ora inclusa in Software Center. Il supporto per il sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1 giugno 2018
   - **Usare la nuova versione di Software Center** - La versione precedente di Software Center non è più supportata. Configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** >**Usa il nuovo Software Center**.

**Windows 10**: informazioni dettagliate relative alla distribuzione e manutenzione di Windows 10. Il gruppo di informazioni dettagliate sulla gestione di Windows 10 è disponibile quando in più della metà dei client è in esecuzione Windows 7, Windows 8 o Windows 8.1.
   - **Configurare la telemetria di Windows e la chiave ID commerciale** -Per usare i dati da Preparazione aggiornamenti, i dispositivi devono essere configurati con una chiave ID esterna e avere la telemetria abilitata. I dispositivi Windows 10 devono essere impostati sul livello di telemetria Avanzata (con limitazioni) o superiore.
   - **Connettere Configuration Manager a Preparazione aggiornamenti** -Sfruttare Preparazione aggiornamenti per velocizzare le distribuzioni di Windows 10 prima che venga abbandonato il supporto di Windows 7. **Configurare la telemetria di Windows e la chiave ID commerciale** costituisce un prerequisito.

     **Regole delle informazioni dettagliate sulla gestione di Windows 10**
    ![Informazioni dettagliate sulla gestione - Regole per Windows 10](./media/Windows-10-insights-group.png)
    