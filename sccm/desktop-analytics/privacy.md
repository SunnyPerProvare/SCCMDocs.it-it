---
title: Privacy dei dati di Analitica desktop
titleSuffix: Configuration Manager
description: Analitica desktop viene eseguito il commit per la privacy dei dati dei clienti
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 370bfc26b8a7b6ca0223803a36e765528460d89f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62258184"
---
# <a name="desktop-analytics-data-privacy"></a>Privacy dei dati di Analitica desktop

Analitica desktop viene eseguito il commit completo per la privacy dei dati dei clienti, ricropre questi principi:

- **Trasparenza:** È stato descritto completamente gli eventi di diagnostica di Windows. Esaminarli con i team di sicurezza e conformità dell'azienda. Visualizzatore dati di diagnostica Windows consente di visualizzare i dati diagnostici inviati da un determinato dispositivo. Per altre informazioni, vedere [Cenni preliminari sul visualizzatore dati di diagnostica](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Controllo:** Controllare il livello di dati di diagnostica da condividere con Microsoft. Windows 10, versione 1709, aggiunge un nuovo criterio per limitare i dati di diagnostica avanzati al minimo richiesto da Desktop Analitica.  

- **Sicurezza:** Microsoft protegge i dati con protezione avanzata e crittografia.  

- **Relazione di trust:** Analitica desktop supporta Microsoft [informativa sulla Privacy](https://privacy.microsoft.com/privacystatement) e [condizioni dei servizi Online](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flusso di dati di diagnostica

La figura seguente mostra i dati di diagnostica come flussi dai singoli dispositivi tramite il servizio dati di diagnostica, archiviazione di Azure Log Analitica e nell'area di lavoro di Log Analitica:

![Diagramma che illustra il flusso di dati diagnostici dai dispositivi](media/da-data-flow-v1.png)

1. Accedi al portale di Azure e l'onboarding a Desktop Analitica. Si crea l'app di Azure AD per la connessione con Configuration Manager. Quando si configura Desktop Analitica, si crea un'area di lavoro di Analitica di Log di Azure nella posizione di propria scelta.  

2. Ci si connette Configuration Manager e registrare i dispositivi  

    1. Configurare il servizio di cloud Analitica Desktop in Configuration Manager con i dettagli dell'app Azure AD.  

    2. Entro 15 minuti, Configuration Manager si sincronizza raccolte di dispositivi e i piani di distribuzioni con Desktop Analitica. Questo processo viene ripetuto ogni ora.  

    3. Configuration Manager imposta l'ID commerciale, a livello di dati di diagnostica e altre impostazioni per i dispositivi nella raccolta di destinazione. Questa configurazione consente di specificare i dispositivi da visualizzare nell'area di lavoro di Analitica Desktop.  

    4. Compatibilità aggiornamenti vengono distribuiti a tutti i dispositivi di destinazione. Facoltativamente, l'analizzatore dell'integrità di App e Office Readiness Toolkit vengono distribuiti in un set rappresentativo dei dispositivi. Questi strumenti offrono altre informazioni dettagliate sulla riga personalizzato di applicazioni aziendali e le macro di Office.  

3. I dispositivi inviano dati di diagnostica per i servizi di gestione dei dati di diagnostica Microsoft per Windows e Office. Questo servizio è ospitato negli Stati Uniti.  

4. Ogni giorno, Microsoft fornisce uno snapshot di insights incentrato sull'IT. Questo snapshot combina i dati di diagnostica da Windows e Office con l'input dell'utente per i dispositivi registrati. Questo processo avviene in un archivio temporaneo, ma viene utilizzato solo dai Desktop Analitica. Lo spazio di archiviazione temporaneo è ospitato nei data center di Microsoft negli Stati Uniti. Gli snapshot sono separati da ID commerciale.  

5. Gli snapshot vengono quindi copiati nell'area di lavoro di Analitica di Log di Azure appropriato.  

6. Desktop Analitica archivia l'input dell'utente in archiviazione di Azure Log Analitica. Queste configurazioni includono piani di distribuzione e le decisioni di asset per l'aggiornamento e importanza.  


<!-- ![Diagram illustrating flow of diagnostic data from devices](media/wa-data-flow-v1.png)

1. Devices send diagnostic data to the Microsoft Diagnostic Data Management service. This service is hosted in the United States.  

2. Set up and enrollment  

    1. You create an Azure Log Analytics workspace when you set up Desktop Analytics. You choose the location and copy the commercial ID. This ID identifies your workspace.  
    
    2. When you connect Configuration Manager to Desktop Analytics, it sets the commercial ID on the devices in your target collection. This configuration specifies the devices to appear in your workspace.  

3. Each day Microsoft produces a "snapshot" of IT-focused insights for each workspace in the Diagnostic Data Management service.  

4. These snapshots are copied to transient storage, which is only used by Desktop Analytics. The transient storage is hosted in Microsoft data centers in the United States. The snapshots are segregated by commercial ID.  

5. The snapshots are then copied to the appropriate Azure Log Analytics workspace.  

6. Desktop Analytics stores your configurations in Analytics Azure storage. These configurations include deployment plans and asset upgrade decisions.  
-->


## <a name="other-resources"></a>Altre risorse

Per altre informazioni sugli aspetti correlati sulla privacy, vedere gli articoli seguenti:

- [Windows 10 e il GDPR per Decision Maker dell'IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Campi ed eventi di dati di diagnostica Windows 7, Windows 8 e Windows 8.1 appraiser](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versione 1809 base livello Windows gli eventi di diagnostica e i campi](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versione 1709 migliorato gli eventi di dati di diagnostica e i campi usati da Desktop Analitica](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Cenni preliminari sul Visualizzatore di dati di diagnostica](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Le condizioni di licenza e documentazione](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Sicurezza e privacy nei data center di Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Fiducia nel cloud attendibile](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro protezione](https://www.microsoft.com/trustcenter)  



## <a name="faq"></a>Domande frequenti

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Desktop Analitica può essere usata senza una connessione client diretto al servizio di gestione dati di Microsoft?
No, l'intero servizio si basa su Windows i dati di diagnostica, che richiede che i dispositivi hanno la connettività diretta.


### <a name="can-i-choose-the-data-center-location"></a>È possibile scegliere la posizione del data center?

Per Analitica di Log di Azure: Sì, quando si imposta Desktop Analitica e crea l'area di lavoro di Log Analitica.

Per il servizio di gestione dati Microsoft e Analitica archiviazione di Azure: No, questi due servizi sono ospitati negli Stati Uniti.

