---
title: Domande frequenti per Desktop Analytics
titleSuffix: Configuration Manager
description: Domande frequenti per Desktop Analytics.
ms.date: 11/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 279da97960866123e109fd8f51d9a6c81353c593
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75825626"
---
# <a name="desktop-analytics-faq"></a>Domande frequenti su Desktop Analytics

## <a name="prerequisites"></a>Prerequisiti

### <a name="bkmk_intune"></a> È possibile usare Desktop Analytics con i dispositivi gestiti da Intune? 

La maggior parte dei clienti che possono trarre vantaggio dal flusso di lavoro di Desktop Analytics usa Configuration Manager per distribuire Windows. I clienti di Intune apprezzano le informazioni aggiuntive offerte dai dati di Analytics e Microsoft sta lavorando per individuare il modo di condividere i dati analitici anche con questi clienti.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Il portale sta elaborando i dati da più di 72 ore. Cosa si può fare? 

Quando si configura Desktop Analytics per la prima volta, è possibile che i report in Configuration Manager e nel portale di Desktop Analytics non visualizzino immediatamente i dati completi. L'elaborazione dei dati da parte del servizio può richiedere 2-3 giorni di tempo. Se il portale sta elaborando i dati da più di 72 ore, seguire questa procedura:

- Per verificare che i dispositivi attivi siano configurati correttamente usare la [dashboard Integrità connessione](/sccm/desktop-analytics/monitor-connection-health). Questa dashboard non viene aggiornata in tempo reale.
- Verificare che i dispositivi inviino i dati di diagnostica al servizio Desktop Analytics. Per altre informazioni, vedere [Abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing).
- Effettuare il provisioning delle [applicazioni Azure AD](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps) in Azure AD.
- Controllare i dispositivi associati all'organizzazione negli ultimi sette giorni. Nel [portale di Desktop Analytics](https://aka.ms/desktopanalytics) passare al riquadro **Servizi connessi**. Selezionare **Registra dispositivi** e **Visualizza dati recenti**

Se i dispositivi sono configurati correttamente e i dati non vengono ancora visualizzati nell'area di lavoro, [contattare il supporto tecnico Microsoft](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>È possibile modificare le raccolte di destinazione o quelle aggiuntive?

Sì, usare il processo seguente:

- Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Aprire le proprietà per la voce associata al servizio Desktop Analytics.

- Nella scheda **Connessione di Desktop Analytics** modificare **Raccolta di destinazione** o gestire le raccolte aggiuntive.

> [!IMPORTANT]  
> Configuration Manager usa un criterio delle impostazioni per configurare i dispositivi presenti nella raccolta di destinazione. Questo criterio include le impostazioni relative ai dati di diagnostica per abilitare i dispositivi a inviare dati a Microsoft. La modifica della raccolta di destinazione non annulla il criterio delle impostazioni nei dispositivi che non fanno più parte della raccolta di destinazione. Se non si vuole che i dispositivi continuino a inviare dati di diagnostica, [riconfigurare i dispositivi](/sccm/desktop-analytics/account-close#reconfigure-clients).

## <a name="windows-upgrade"></a>Aggiornamento di Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>È possibile aggiornare Windows e modificare l'architettura?

Desktop Analytics è progettato per supportare al meglio gli aggiornamenti sul posto. Gli aggiornamenti sul posto non supportano le migrazioni dall'architettura a 32 bit a quella a 64 bit. Se è necessario eseguire la migrazione dei computer in questo scenario, usare lo scenario di aggiornamento. I dati analitici di Desktop Analytics risultano comunque utili in questo scenario, ma è possibile ignorare le indicazioni specifiche dell'aggiornamento.

Per altre informazioni, vedere [Aggiornare un computer esistente con una nuova versione di Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>È possibile passare da BIOS a UEFI durante l'aggiornamento di Windows?

Sì. Per altre informazioni, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>È possibile usare Desktop Analytics con Windows 10 LTSC?

Anche se è possibile usare Desktop Analytics per agevolare l'aggiornamento dei dispositivi da Windows 10 Long-Term Servicing Channel (LTSC) al canale semestrale di Windows 10, Desktop Analytics non supporta gli aggiornamenti a Windows 10 LTSC. Questo canale di Windows 10 non è destinato a un ampio uso e non riceve gli aggiornamenti delle funzionalità, quindi non è una destinazione supportata in Desktop Analytics. Per altre informazioni, vedere [Panoramica di Windows as a Service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>È possibile ridurre la quantità di tempo necessaria per l'aggiornamento dei dati nel portale di Desktop Analytics?

Nel portale di Desktop Analytics sono disponibili due tipi di dati: dati dell'amministratore e dati di diagnostica. Per aggiornare i dati dell'amministratore su richiesta, aprire il riquadro a comparsa sull'attualità dei dati e selezionare **Applica modifiche**. Questa azione attiva immediatamente un aggiornamento su richiesta delle modifiche in sospeso dell'amministratore nelle aree di lavoro. Le modifiche vengono propagate e sono in genere disponibili entro 15-60 minuti. I tempi dipendono dalle dimensioni dell'area di lavoro e dall'ambito delle modifiche in sospeso. È possibile richiedere un aggiornamento dei dati su richiesta fino a sei volte nell'arco di 24 ore.

Tutti i dati vengono aggiornati automaticamente una volta al giorno, anche se non si richiede un aggiornamento dei dati su richiesta. Non è possibile attivare un aggiornamento su richiesta dei dati di diagnostica. Per altre informazioni sui diversi tipi di dati in Desktop Analytics, vedere [Latenza dei dati](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacy

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Desktop Analytics può essere usato senza una connessione client diretta al servizio Gestione dati Microsoft?

No, l'intero servizio è supportato dai dati di diagnostica di Windows ed è pertanto necessario che i dispositivi abbiano la connettività diretta.

### <a name="can-i-choose-the-data-center-location"></a>È possibile scegliere la località del data center?

Per Azure Log Analytics: sì, durante la configurazione di Desktop Analytics e la creazione dell'area di lavoro Log Analytics.

Per il servizio Gestione dati Microsoft e Analisi archiviazione di Azure: no, questi due servizi sono ospitati negli Stati Uniti.

### <a name="where-is-my-organizations-data-stored"></a>Dove vengono archiviati i dati dell'organizzazione?

I dati di diagnostica di Windows provenienti dai computer del cliente vengono crittografati, inviati ed elaborati in data center protetti gestiti da Microsoft dislocati negli Stati Uniti. Microsoft offre all'utente l'analisi dei dati correlati a Desktop Analytics tramite la soluzione Desktop Analytics nel portale di Azure. Desktop Analytics è supportato nella maggior parte delle aree in cui [è disponibile Log Analytics](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Se si seleziona un'area di Azure internazionale, i dati di diagnostica vengono comunque inviati ed elaborati nei data center protetti Microsoft negli Stati Uniti.

## <a name="existing-windows-analytics-customers"></a>Clienti esistenti di Windows Analytics

### <a name="can-i-migrate-inputs-from-windows-analytics"></a>È possibile eseguire la migrazione degli input da Windows Analytics?

Sì, se si imposta un'area di lavoro Windows Analytics esistente come area di lavoro Desktop Analytics durante l'[onboarding iniziale](/sccm/desktop-analytics/set-up#initial-onboarding). Se si crea una nuova area di lavoro o se ne seleziona una che non è un'area di lavoro Windows Analytics, Desktop Analytics non eseguirà la migrazione degli input.

#### <a name="migration-scope"></a>Ambito di migrazione

| Tipo di input | Migrazione |
|------------|---------------|
| Importanza | Sì |
| Proprietario dell'app | Sì |
| Decisione di aggiornamento | No |
| Piano di test | No |
| Risultato del test | No |

#### <a name="importance-mapping"></a>Mapping importanza

| Windows Analytics | Desktop Analytics |
|-------------------| ------------------|
| Numero di installazioni basso | (Non applicabile) <br> Nota: Desktop Analytics esegue la propria euristica per determinare il basso numero di installazioni |
| Non riviste | Non revisionato |
| Revisione in corso | Non revisionato |
| Cruciale | Critico |
| Business Critical | Critico |
| Importante | Importante |
| Massimo sforzo | Importante |
| Ignora | Non importante |

### <a name="can-i-migrate-from-multiple-windows-analytics-workspaces"></a>È possibile eseguire la migrazione da più aree di lavoro Windows Analytics?

No, è possibile selezionare una sola area di lavoro Windows Analytics da cui eseguire la migrazione degli input. Se si è proprietari di più aree di lavoro Windows Analytics, selezionare quella più vantaggiosa per l'organizzazione.

### <a name="ive-chosen-to-migrate-where-can-i-find-the-inputs-on-desktop-analytics"></a>Si è scelto di eseguire la migrazione. Dove sono gli input in Desktop Analytics?

Dopo la registrazione dei dispositivi, per vedere gli input di cui è stata eseguita la migrazione nel portale di Desktop Analytics selezionare **Gestisci > Risorse > App**.

### <a name="when-can-i-see-my-migrated-inputs"></a>Quando saranno visibili gli input di cui è stata eseguita la migrazione?

Il processo di migrazione è transazionale. Saranno visibili tutti gli input di cui è stata eseguita la migrazione senza danneggiamento oppure nessun input. Se gli input non risultano visibili entro 24 ore, contattare il supporto tecnico Microsoft. Iniziare a contrassegnare le app non appena gli input di cui è stata eseguita la migrazione risultano visibili. Se alcune app sono già state contrassegnate, Desktop Analytics conserva questi input in caso risultino in conflitto con gli input di Windows Analytics.

### <a name="how-long-do-i-have-to-migrate-my-data"></a>Per quanto tempo è necessario eseguire la migrazione dei dati?

La soluzione Preparazione aggiornamenti di Windows Analytics verrà [ritirata il 31 gennaio 2020](https://aka.ms/waretirement). Dopo il ritiro, in base ai criteri di conservazione dell'area di lavoro Log Analytics, i dati verranno con il tempo eliminati. I clienti che vogliono mantenere i dati devono eseguirne la migrazione o esportarli prima dell'eliminazione.

### <a name="can-i-migrate-after-the-initial-onboarding"></a>È possibile eseguire la migrazione dopo l'onboarding iniziale?

Sì.<!-- 5202803 --> I clienti esistenti di Windows Analytics possono ora eseguire la migrazione dei dati dopo l'onboarding iniziale a condizione che un'area di lavoro Windows Analytics esistente sia stata impostata come area di lavoro Desktop Analytics durante l'[onboarding iniziale](/sccm/desktop-analytics/set-up#initial-onboarding). Nel portale di Desktop Analytics passare a **Servizi connessi** e selezionare l'opzione per eseguire la migrazione dei dati da Windows Analytics.

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>È possibile usare Conformità aggiornamenti insieme a Desktop Analytics?

Sì. Se attualmente si usa [Conformità aggiornamenti](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) nel portale di Azure, è possibile continuare a farlo ora e dopo gennaio 2020.

Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Ci sono funzionalità di Windows Analytics che non sono disponibili in Desktop Analytics?

<!-- 3616924 -->
Sì, le funzionalità di Windows Analytics seguenti verranno ritirate o non sono ancora disponibili in Desktop Analytics:

#### <a name="general"></a>Generale

- Supporto per scenari che non richiedono Configuration Manager. Ad esempio, il [supporto di Intune](#bkmk_intune).
- Prerequisito di licenza di qualsiasi licenza valida di Windows rispetto a E3, E5
- Supporto di più aree di lavoro per tenant di Azure AD
- Possibilità di eseguire query personalizzate ed esportare dati della soluzione non elaborati
- Documentazione del modello di dati per i report personalizzati

#### <a name="upgrade-readiness"></a>Preparazione aggiornamenti

- Dati di individuazione siti di Internet Explorer
- Dati analitici del componente aggiuntivo per Office (ora [disponibile in Configuration Manager](#bkmk_office))
- Dati analitici di Hub di Feedback

#### <a name="update-compliance"></a>Conformità aggiornamenti

- Supporto per Windows Update per le aziende
- Dati analitici di Ottimizzazione recapito
- Supporto per Windows 10 Long-Term Servicing Channel (LTSC)
- Report di Windows Insider
- Stato di Windows Defender

> [!Note]
> Tutte le funzionalità esistenti di Conformità aggiornamenti, incluse quelle non disponibili in Desktop Analytics, rimangono disponibili nella soluzione [Conformità aggiornamenti](/windows/deployment/update/update-compliance-get-started) nel portale di Azure.

#### <a name="device-health"></a>Integrità dispositivi

- Integrità dei driver
- Integrità delle app (al di fuori di un piano di distribuzione)
- Dispositivi con arresti anomali frequenti o arresti anomali generati dai driver
- Integrità dell'accesso a Windows
- Windows Information Protection
- Supporto per Windows Server

## <a name="other"></a>Altro

### <a name="bkmk_office"></a> È possibile usare Desktop Analytics per gli aggiornamenti di Office 365 ProPlus?

No, Desktop Analytics si concentra su Windows. Microsoft ha sviluppato Desktop Analytics in stretta collaborazione con molti clienti. Il feedback dei clienti riguarda il modo in cui Desktop Analytics migliora la capacità di gestire le distribuzioni di Windows in tutta sicurezza. I clienti esprimono anche interesse per una maggiore integrazione della [preparazione per Office 365 ProPlus](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) con gli strumenti di gestione di Office in Configuration Manager e Intune. Microsoft continua a investire in queste aree concentrandosi al contempo su scenari Windows in Desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Come si invia il feedback relativo a Desktop Analytics?

Per condividere il proprio feedback su Desktop Analytics, selezionare l'icona **Invia smile** nella parte superiore del portale. Per aiutare Microsoft a comprendere meglio il feedback, includere uno screenshot insieme al proprio contributo. È anche possibile inviare suggerimenti per il prodotto e votare altre idee in [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Non condividere mai informazioni private tramite Invia smile o UserVoice. Le informazioni private includono l'ID tenant o l'ID commerciale. Microsoft non offre supporto tramite i canali Invia smile o UserVoice. Per ottenere assistenza relativa all'area di lavoro Desktop Analytics, selezionare il collegamento **Guida e supporto** nel menu di spostamento per aprire un ticket di supporto.
