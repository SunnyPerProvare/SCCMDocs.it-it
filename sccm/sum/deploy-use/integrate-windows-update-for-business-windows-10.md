---
title: Integrare Windows Update per le aziende
titleSuffix: Configuration Manager
description: Usare Windows Update for business (WUfB) per lasciare Windows 10 aggiornato per i dispositivi connessi al servizio Windows Update.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/04/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.collection: M365-identity-device-management
ms.openlocfilehash: 504ace282988ef8b52863184f0685ea5a6958a27
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892284"
---
# <a name="integrate-with-windows-update-for-business"></a>Integrazione con Windows Update for business

*Si applica a: System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) consente di mantenere i dispositivi basati su Windows 10 nell'organizzazione sempre aggiornati con le difese per la sicurezza e le funzionalità di Windows più recenti, quando questi dispositivi si connettono direttamente al servizio Windows Update (WU). Configuration Manager è in grado di distinguere tra i computer Windows 10 che ricevono gli aggiornamenti software da Windows Update for Business e i computer che li ricevono da WSUS.  

>[!WARNING]
> Se si usa la co-gestione per i dispositivi e si sono spostati i [criteri di Windows Update](/sccm/comanage/workloads#windows-update-policies) in Intune, i dispositivi otterranno i [criteri di Windows Update for Business da Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Se il client di Configuration Manager è ancora installato nel dispositivo co-gestito, le impostazioni per gli aggiornamenti cumulativi e gli aggiornamenti delle funzionalità sono gestiti da Intune. Tuttavia, l'applicazione di patch di terze parti, se abilitata nelle [ **Impostazioni client**](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates), è ancora gestita da Configuration Manager.  

 Alcune funzionalità di Configuration Manager non sono disponibili per i client di Configuration Manager configurati per ricevere gli aggiornamenti da Windows Update. Tra queste, Windows Update for Business e Windows Insider:  

-   Report della conformità di Windows Update:  

    -   Configuration Manager non è a conoscenza degli aggiornamenti pubblicati in Windows Update. Questi aggiornamenti saranno visualizzati come **sconosciuti** nella console di Configuration Manager per i client di Configuration Manager configurati per ricevere gli aggiornamenti da Windows Update.  

    -   La risoluzione dei problemi relativi allo stato di conformità generale risulta difficile, perché lo stato **sconosciuto** era riservato solo ai client per cui non veniva segnalato lo stato di analisi da WSUS. Questo stato include ora anche i client di Configuration Manager che ricevono gli aggiornamenti da Windows Update.  

    -   L'accesso condizionale (per le risorse aziendali) basato sullo stato di conformità di aggiornamento non funzionerà come previsto per i client che ricevono gli aggiornamenti da Windows Update, perché non risulterebbero mai conformi per Configuration Manager.  

    -   La conformità degli aggiornamenti delle definizioni fa parte dei report di verifica aggiornamenti generale e anche questo aspetto non funzionerà come previsto.  La conformità degli aggiornamenti delle definizioni fa anche parte della valutazione di accesso condizionale.  

-   Nel complesso, i report di Endpoint Protection per Defender basati sullo stato di conformità degli aggiornamenti non restituiscono risultati precisi a causa della mancanza dei dati di analisi.  

-   Configuration Manager non sarà in grado di distribuire gli aggiornamenti Microsoft, ad esempio Office, Internet Explorer e Visual Studio, ai client connessi a Windows Update for Business per la ricezione degli aggiornamenti.  

-   Configuration Manager non è in grado di distribuire gli aggiornamenti di terze parti pubblicati in WSUS e gestiti tramite Configuration Manager ai client connessi a Windows Update for Business per la ricezione degli aggiornamenti. Se non si desidera che eventuali aggiornamenti di terze parti siano installati nei client connessi a WUfB, disabilitare l'impostazione client denominata [Abilitare aggiornamento software nei client](/sccm/core/clients/deploy/about-client-settings#software-updates).

-   La distribuzione di client completi di Configuration Manager che usa l'infrastruttura di aggiornamenti software non funzionerà per i client connessi a Windows Update for Business per la ricezione degli aggiornamenti.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificare i client che usano WUfB per gli aggiornamenti di Windows 10  
 Usare la procedura seguente per identificare i client che usano WUfB per ottenere gli aggiornamenti di Windows 10, quindi configurarli in modo da interrompere l'uso di WSUS per ottenere gli aggiornamenti e distribuire l'impostazione di un agente client per disabilitare il flusso di lavoro di aggiornamenti software per questi client.  

 **Prerequisiti**  

-   Client che eseguono Windows 10 Desktop Pro o Windows 10 Enterprise Edition versione 1511 o successive  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) è distribuito e i client usano WUfB per ottenere gli aggiornamenti di Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Per identificare i client che usano WUfB  

1.  Verificare che l'agente di Windows Update non stia eseguendo l'analisi rispetto a WSUS, se è stato precedentemente abilitato. Per indicare se il computer esegue l'analisi rispetto a Windows Update o a WSUS, è possibile impostare la chiave del Registro di sistema seguente. Se la chiave del registro di sistema non esiste, l'analisi non viene eseguita rispetto a WSUS.
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Esiste un nuovo attributo, **UseWUServer**, nel nodo **Windows Update** di Esplora inventario risorse di Configuration Manager.  

3.  Creare una raccolta sulla base dell'attributo **UseWUServer** per tutti i computer connessi tramite WUfB per gli aggiornamenti. È possibile creare una raccolta in base a una query simile a quella riportata di seguito:  

    ``` WQL
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

4.  Creare un'impostazione dell'agente client per disabilitare il flusso di lavoro di aggiornamento software. Distribuire l'impostazione nella raccolta di computer connessi direttamente a WUfB.  

5.  Lo stato di conformità dei computer gestiti tramite Windows Update for Business sarà **Sconosciuto** e quindi questi non verranno conteggiati come parte della percentuale di conformità complessiva.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configurare i criteri di rinvio di Windows Update for Business
<!-- 1290890 -->
A partire da Configuration Manager versione 1706, è possibile configurare i criteri di rinvio dei dispositivi per gli aggiornamenti delle funzionalità di Windows 10 o dei dispositivi con aggiornamenti di qualità di Windows 10 gestiti direttamente da Windows Update for Business. È possibile gestire i criteri di rinvio nel nuovo nodo **Criteri di Windows Update for Business** in **Libreria Software** > **Manutenzione pacchetti di Windows 10**.

>[!NOTE] 
>A partire da Configuration Manager versione 1802, è possibile impostare i criteri di differimento per Windows Insider. <!--507201-->Per altre informazioni sul programma Windows Insider, vedere [Introduzione al programma Windows Insider per le aziende](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Prerequisiti
-   Windows 10 versione 1703 o successiva
-   I dispositivi Windows 10 gestiti da Windows Update per le aziende devono disporre di connettività Internet

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Per creare i criteri di rinvio di Windows Update for Business
1. In **Libreria Software** > **Manutenzione pacchetti di Windows 10** > **Criteri di Windows Update for Business**
2. Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea un criterio di Windows Update for Business** per aprire la procedura guidata Creazione guidata di un criterio di Windows Update for Business.
3. Nella pagina **Generale** specificare un nome e una descrizione per il criterio.
4. Nella pagina **Criteri di differimento** configurare se si desidera differire o sospendere gli aggiornamenti delle funzionalità. Gli aggiornamenti delle funzionalità sono generalmente nuove funzionalità per Windows. Dopo aver configurato l'impostazione **Livello di conformità con Branch**, è possibile definire se e per quanto tempo si desidera rinviare la ricezione di aggiornamenti delle funzionalità in base alla disponibilità da Microsoft.
    - **Livello di conformità con Branch**: impostare il branch per il quale il dispositivo riceverà gli aggiornamenti di Windows (Current Branch o Current Branch for Business).
    - **Periodo di differimento (giorni):** specificare il numero di giorni per cui verranno posticipati gli aggiornamenti delle funzionalità. È possibile differire la ricezione di questi aggiornamenti delle funzionalità per massimo 365 giorni dopo il rilascio.
    - **Pause Features Updates starting** (Sospendi avvio degli aggiornamenti delle funzionalità): selezionare se sospendere la ricezione da parte dei dispositivi degli aggiornamenti delle funzionalità per massimo 60 giorni a partire dal momento in cui si sospendono gli aggiornamenti. Una volta trascorso il numero massimo di giorni, la sospensione della funzionalità scadrà automaticamente e il dispositivo analizzerà Windows Updates per gli aggiornamenti applicabili. Dopo questa analisi, è possibile sospendere nuovamente gli aggiornamenti. È possibile riprendere gli aggiornamenti delle funzionalità deselezionando la casella di controllo.   
5. Scegliere se rinviare o sospendere gli aggiornamenti di qualità. Gli aggiornamenti di qualità sono in genere correzioni e miglioramenti alle funzionalità esistenti di Windows e vengono generalmente pubblicati il primo martedì di ogni mese, sebbene possano essere rilasciati in qualsiasi momento da Microsoft. È possibile definire se e per quanto tempo si desidera rinviare la ricezione degli aggiornamenti di qualità dopo la loro disponibilità.
    - **Periodo di differimento (giorni):** specificare il numero di giorni per cui gli aggiornamenti qualitativi verranno differiti. È possibile differire la ricezione di questi aggiornamenti qualitativi per massimo 30 giorni dopo il rilascio.
    - **Pause Quality Updates starting** (Sospendi avvio degli aggiornamenti di qualità): selezionare se sospendere la ricezione da parte dei dispositivi degli aggiornamenti di qualità per massimo 35 giorni a partire dal momento in cui si sospendono gli aggiornamenti. Una volta trascorso il numero massimo di giorni, la sospensione della funzionalità scadrà automaticamente e il dispositivo analizzerà Windows Updates per gli aggiornamenti applicabili. Dopo questa analisi, è possibile sospendere nuovamente gli aggiornamenti. È possibile riprendere gli aggiornamenti di qualità deselezionando la casella di controllo.
6. Selezionare **Installa gli aggiornamenti per altri prodotti Microsoft** per abilitare l'impostazione dei criteri di gruppo che rendono le impostazioni di rinvio applicabili a Microsoft Update, oltre agli aggiornamenti di Windows.
7. Selezionare **Include drivers with Windows Update** (Includi i driver con Windows Update) per aggiornare automaticamente i driver da Windows Update. Se si deseleziona questa impostazione, gli aggiornamenti dei driver non vengono scaricati da Windows Update.
8. Completare la procedura guidata per creare i nuovi criteri di rinvio.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Per distribuire i criteri di rinvio di Windows Update for Business
1. In **Libreria Software** > **Manutenzione pacchetti di Windows 10** > **Criteri di Windows Update for Business**
2. Nella scheda **Home**, nel gruppo **Distribuzione** selezionare **Distribuisci il criterio di Windows Update for Business**.
3. Configurare le seguenti impostazioni:
    - **Criteri di configurazione da distribuire**: selezionare il criterio Windows Update for Business che si desidera distribuire.
    - **Raccolta**: fare clic su **Sfoglia** per selezionare la raccolta in cui si desidera distribuire i criteri.
    - **Monitora e aggiorna le regole non conformi, se supportato**: selezionare per correggere automaticamente tutte le regole non conformi per Strumentazione gestione Windows (WMI), il registro di sistema, gli script e tutte le impostazioni per i dispositivi mobili registrati da Configuration Manager.
    - **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**: se è stata configurata una finestra di manutenzione per la raccolta in cui si distribuiscono i criteri, abilitare questa opzione per consentire alle impostazioni di conformità di monitorare e aggiornare il valore fuori dalla finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Genera un avviso**: configura un avviso che viene generato se la conformità della linea di base di configurazione è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.
    - **Ritardo casuale (ore)** : specifica una finestra di ritardo per evitare un'elaborazione eccessiva nel servizio Registrazione dispositivi di rete. Il valore predefinito è 64 ore.
    - **Pianificazione**: specifica la pianificazione per la valutazione della conformità in base alla quale il profilo distribuito viene valutato nei computer client. Può trattarsi di una pianificazione semplice o personalizzata. Il profilo viene valutato dai computer client quando l'utente effettua l'accesso.
4.  Completare la procedura guidata per distribuire il profilo.
