---
title: Domande frequenti su desktop Analytics
titleSuffix: Configuration Manager
description: Domande frequenti su desktop Analytics.
ms.date: 10/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96f84adcacdf298840a981360478bf828a22716a
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72385476"
---
# <a name="desktop-analytics-faq"></a>Domande frequenti su desktop Analytics

## <a name="prerequisites"></a>Prerequisites

### <a name="bkmk_intune"></a>È possibile usare analisi desktop con i dispositivi gestiti da Intune? 

La maggior parte dei clienti che possono trarre vantaggio dal flusso di lavoro di analisi desktop USA Configuration Manager per la distribuzione di Windows. I clienti di Intune apprezzano le informazioni aggiuntive dai dati di analisi e sono in grado di condividere informazioni approfondite anche con loro.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Sono passate oltre 72 ore e il portale sta ancora elaborando i dati? 

Quando si configura per la prima volta analisi desktop, è possibile che i report Configuration Manager e il portale di analisi desktop non visualizzino immediatamente i dati completi. Per elaborare i dati, il servizio può richiedere 2-3 giorni. Se è passato più di 72 ore e il portale sta ancora elaborando i dati, attenersi alla procedura seguente:

- Per verificare che i dispositivi attivi siano configurati correttamente, usare il [dashboard di integrità della connessione](/sccm/desktop-analytics/monitor-connection-health). Questo dashboard non viene aggiornato in tempo reale.
- Assicurarsi che i dispositivi inviino i dati di diagnostica al servizio desktop Analytics. Per altre informazioni, vedere [abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing).
- Effettuare il provisioning di [Azure ad applicazioni](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps) nel Azure ad.
- Controllare i dispositivi associati all'organizzazione negli ultimi sette giorni. Nel [portale di analisi dei desktop](https://aka.ms/desktopanalytics)passare al riquadro **servizi connessi** . Selezionare **registra i dispositivi**e **visualizzare i dati recenti**

Se i dispositivi sono configurati correttamente e non vengono ancora visualizzati i dati nell'area di lavoro, [contattare il supporto tecnico Microsoft](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>È possibile modificare la destinazione o le raccolte aggiuntive?

Sì, usare il processo seguente:

- Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Aprire le proprietà per la voce associata al servizio desktop Analytics.

- Nella scheda **Connessione desktop analisi** modificare la raccolta di **destinazione** o gestire le raccolte aggiuntive.

> [!IMPORTANT]  
> Configuration Manager usa un criterio impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni dei dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. La modifica della raccolta di destinazione non comporta l'annullamento del criterio impostazioni nei dispositivi non più nella raccolta di destinazione. Se non si vuole che i dispositivi continuino a inviare i dati di diagnostica, [riconfigurare i dispositivi](/sccm/desktop-analytics/account-close#reconfigure-clients).

## <a name="windows-upgrade"></a>Aggiornamento di Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>È possibile aggiornare Windows e modificare l'architettura?

Desktop Analytics è progettato per supportare al meglio gli aggiornamenti sul posto. Gli aggiornamenti sul posto non supportano le migrazioni dall'architettura a 32 bit a quella a 64 bit. Se è necessario eseguire la migrazione dei computer in questo scenario, usare lo scenario di aggiornamento. Le informazioni dettagliate su desktop Analytics sono ancora utili in questo scenario, ma è possibile ignorare le indicazioni specifiche per l'aggiornamento.

Per altre informazioni, vedere [Aggiornare un computer esistente con una nuova versione di Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>È possibile passare da BIOS a UEFI durante l'aggiornamento di Windows?

Sì. Per ulteriori informazioni, vedere [conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>È possibile usare desktop Analytics con Windows 10 LTSC?

Sebbene sia possibile usare l'analisi del desktop per supportare l'aggiornamento dei dispositivi da Windows 10 Long-Term Servicing Channel (LTSC) a un canale semestrale di Windows 10, desktop Analytics non supporta gli aggiornamenti per Windows 10 LTSC. Questo canale di Windows 10 non è destinato a un uso ampio e non riceve gli aggiornamenti delle funzionalità, quindi non si tratta di una destinazione supportata con analisi desktop. Per altre informazioni, vedere [Panoramica di Windows come servizio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>È possibile ridurre la quantità di tempo necessaria per l'aggiornamento dei dati nel portale di analisi desktop?

Sono disponibili due tipi di dati nel portale di analisi del desktop: dati dell'amministratore e dati di diagnostica. Per aggiornare i dati dell'amministratore su richiesta, aprire il riquadro a comparsa valuta dati e selezionare **Applica modifiche**. Questa azione attiva immediatamente un aggiornamento unico di eventuali modifiche amministrative in sospeso nelle aree di lavoro. Le modifiche vengono propagate e sono disponibili a livello generale entro 15-60 minuti. La durata dipende dalle dimensioni dell'area di lavoro e dall'ambito delle modifiche in sospeso. È possibile richiedere un aggiornamento dati su richiesta fino a sei volte nell'arco di 24 ore.

Tutti i dati vengono aggiornati automaticamente una volta al giorno, anche se non si richiede un aggiornamento dati su richiesta. Non è possibile attivare un aggiornamento su richiesta dei dati di diagnostica. Per altre informazioni sui diversi tipi di dati in analisi desktop, vedere [latenza dei dati](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacy

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>È possibile usare l'analisi del desktop senza una connessione client diretta al servizio Microsoft Gestione dati?

No, l'intero servizio è basato sui dati di diagnostica di Windows, che richiedono che i dispositivi abbiano questa connettività diretta.

### <a name="can-i-choose-the-data-center-location"></a>È possibile scegliere il percorso data center?

Per Log Analytics di Azure: Sì, quando si configura analisi desktop e si crea l'area di lavoro Log Analytics.

Per il servizio Microsoft Gestione dati e la risorsa di archiviazione di Azure: No, questi due servizi sono ospitati nel Stati Uniti.

### <a name="where-is-my-organizations-data-stored"></a>Dove vengono archiviati i dati dell'organizzazione?

I dati di diagnostica di Windows dei computer vengono crittografati, inviati ed elaborati nei data center protetti gestiti da Microsoft presenti nel Stati Uniti. L'analisi dei dati correlati a analisi desktop viene quindi fornita tramite la soluzione desktop Analytics nella portale di Azure. Desktop Analytics è supportato in tutte le aree di Azure. La selezione di un'area di Azure internazionale non impedisce l'invio e l'elaborazione dei dati di diagnostica nei data center protetti di Microsoft negli Stati Uniti.

## <a name="existing-windows-analytics-customers"></a>Clienti esistenti di Windows Analytics

### <a name="can-i-migrate-inputs-from-windows-analytics"></a>È possibile migrare gli input da Windows Analytics?

Sì, quando si imposta un'area di lavoro di Windows Analytics esistente come area di lavoro di analisi desktop durante l' [onboarding iniziale](/sccm/desktop-analytics/set-up#initial-onboarding). Se si crea una nuova area di lavoro o se ne seleziona una non un'area di lavoro di Windows Analytics, desktop Analytics non esegue la migrazione degli input.

#### <a name="migration-scope"></a>Ambito della migrazione

| Tipo di input | Viene eseguita la migrazione? |
|------------|---------------|
| Importanza | Yes |
| Proprietario dell'app | Yes |
| Decisione di aggiornamento | No |
| Piano di test | No |
| Risultato del test | No |

#### <a name="importance-mapping"></a>Mapping importanza

| Windows Analytics | Desktop Analytics |
|-------------------| ------------------|
| Numero di installazioni insufficienti | (Non applicabile) <br> Nota: desktop Analytics esegue la propria euristica per determinare il numero di installazioni basso |
| Non verificato | Non verificato |
| Revisione in corso | Non verificato |
| Mission-critical | Critico |
| Business critical | Critico |
| Importante | Importante |
| Massimo sforzo | Importante |
| Ignora | Non importante |

### <a name="can-i-migrate-from-multiple-windows-analytics-workspaces"></a>È possibile eseguire la migrazione da più aree di lavoro di Windows Analytics?

No, è possibile selezionare solo un'area di lavoro di Windows Analytics dalla quale migrare gli input. Se si è proprietari di più aree di lavoro di Windows Analytics, selezionarne una che migliori vantaggi per l'organizzazione.

### <a name="ive-chosen-to-migrate-where-can-i-find-the-inputs-on-desktop-analytics"></a>Si è scelto di eseguire la migrazione, dove è possibile trovare gli input in analisi desktop?

Una volta registrati i dispositivi, per visualizzare gli input migrati nel portale di analisi dei desktop, passare a **gestisci > asset > app**.

### <a name="when-can-i-see-my-migrated-inputs"></a>Quando è possibile visualizzare gli input migrati?

Il processo di migrazione è transazionale. Verranno visualizzati tutti gli input migrati senza danneggiamento o nessun input migrato. Se gli input migrati non vengono visualizzati in 24 ore, contattare supporto tecnico Microsoft. Avviare l'assegnazione di tag alle app quando vengono visualizzati gli input migrati. Se sono già state contrassegnate alcune app, desktop Analytics mantiene gli input nel caso in cui si verifichino conflitti con gli input da Windows Analytics.

### <a name="im-not-ready-yet-can-i-migrate-after-the-initial-onboarding"></a>Se non si è ancora pronti, è possibile eseguire la migrazione dopo l'onboarding iniziale?

Sì.<!-- 5202803 --> I clienti esistenti di Windows Analytics possono ora migrare i dati dopo l'onboarding iniziale. Passare a **servizi connessi** nel portale di analisi del desktop e selezionare l'opzione per la migrazione dei dati da Windows Analytics.

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>È possibile usare Conformità aggiornamenti insieme a Analytics per desktop?

Sì. Se attualmente si usa [conformità aggiornamenti](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) nella portale di Azure, è possibile continuare a farlo ora e oltre il 2020 gennaio.

Per ulteriori informazioni, vedere [KB 4521815: ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Sono disponibili funzionalità di Windows Analytics che non sono disponibili in analisi desktop?

<!-- 3616924 -->
Sì, le funzionalità di Windows Analytics seguenti verranno ritirate o non sono ancora disponibili in analisi desktop:

#### <a name="general"></a>Generale

- Supporto per gli scenari che non richiedono Configuration Manager. Ad esempio, il [supporto di Intune](#bkmk_intune).
- Prerequisiti per le licenze di qualsiasi licenza di Windows valida rispetto a E3, E5
- Supporto per più aree di lavoro per ogni tenant di Azure AD
- Possibilità di eseguire query personalizzate ed esportare dati non elaborati della soluzione
- Documentazione del modello di dati per i report personalizzati

#### <a name="upgrade-readiness"></a>Preparazione aggiornamenti

- Dati di individuazione sito Internet Explorer
- Informazioni dettagliate sui componenti aggiuntivi di Office (ora [disponibili in Configuration Manager](#bkmk_office))
- Informazioni dettagliate sull'hub feedback

#### <a name="update-compliance"></a>Conformità aggiornamenti

- Supporto per Windows Update for business
- Informazioni dettagliate sull'ottimizzazione recapito
- Supporto per il canale di manutenzione a lungo termine di Windows 10 (LTSC)
- Report di Windows Insider
- Stato di Windows Defender

> [!Note]
> Tutte le funzionalità di Conformità aggiornamenti esistenti, incluse quelle non disponibili in desktop Analytics, restano disponibili nella portale di Azure della soluzione [conformità aggiornamenti](/windows/deployment/update/update-compliance-get-started) .

#### <a name="device-health"></a>Integrità dispositivi

- Stato driver
- Integrità app (all'esterno di un piano di distribuzione)
- Dispositivi che si arrestano in modo anomalo o arresti anomali del driver
- Stato di accesso a Windows
- Windows Information Protection
- Supporto per Windows Server

## <a name="other"></a>Altro

### <a name="bkmk_office"></a>È possibile usare l'analisi del desktop per gli aggiornamenti di Office 365 ProPlus?

No, desktop Analytics è incentrato su Windows. Microsoft ha sviluppato desktop Analytics in stretta collaborazione con molti clienti. Il feedback dei clienti riguarda il modo in cui desktop Analytics migliora la propria capacità di gestire le distribuzioni di Windows. Indicano anche che desiderano che l'idoneità di [office 365 ProPlus](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) sia più strettamente integrata con gli strumenti di gestione di office in Configuration Manager e Intune. Microsoft continua a investire in tali aree, concentrandosi sugli scenari di Windows in desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Come è possibile fornire commenti e suggerimenti su desktop Analytics?

Per condividere commenti e suggerimenti su desktop Analytics, selezionare l'icona **Invia smile** nella parte superiore del portale. Includi uno screenshot con la tua presentazione per aiutare Microsoft a comprendere meglio i tuoi commenti. È anche possibile inviare suggerimenti sul prodotto e votare altre idee in [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Non condividere mai le informazioni private tramite Invia smile o UserVoice. Tali informazioni private includono l'ID tenant o l'ID commerciale. Microsoft non fornisce supporto tramite i canali Invia smile o UserVoice. Per ottenere assistenza con l'area di lavoro di desktop Analytics, selezionare il collegamento **Guida e supporto** nel menu di navigazione per aprire un ticket di supporto.
