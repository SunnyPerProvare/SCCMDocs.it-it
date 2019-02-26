---
title: Accesso condizionale con CO-gestione
titleSuffix: Configuration Manager
description: Controllare l'accesso utente alle risorse aziendali in base alle regole di conformità da Intune
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e5c7d6075697431f8c537366dc16164fedd1f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755202"
---
# <a name="conditional-access-with-co-management"></a>Accesso condizionale con CO-gestione

Accesso condizionale assicura che solo gli utenti attendibili possono accedere alle risorse aziendali nei dispositivi attendibili usando le applicazioni attendibili. Viene compilata da zero nel cloud. Se si gestiscono i dispositivi con Intune o estende la distribuzione di Configuration Manager con CO-gestione, funziona allo stesso modo.

Nel video seguente, senior program manager Joey Glocke e product marketing manager Locky Ainley discutere e demo di accesso condizionale con CO-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Con CO-gestione, Intune valuta tutti i dispositivi nella rete per determinare il grado di affidabilità è. Esegue questa versione di valutazione in un due modi seguenti:

1. Intune garantisce che un dispositivo o app è gestita e configurata in modo sicuro. Questa verifica dipende dalla modalità di impostazione dei criteri di conformità dell'organizzazione. Ad esempio, assicurarsi che tutti i dispositivi è possibile abilitare la crittografia e non sono jailbroken.  

    - Questa valutazione è violazione della pre- sicurezza e basata sulla configurazione  

    - Per i dispositivi con CO-gestione, Configuration Manager esegue inoltre una valutazione basata sulla configurazione. Obbligatorio, ad esempio, la conformità degli aggiornamenti o le app. Intune combina questa versione di valutazione e la propria valutazione.  

2. Intune rileva gli incidenti di sicurezza attive in un dispositivo. Usa la sicurezza intelligente dei [Windows Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) e altre [provider di mobile threat defense](https://www.lookout.com/about/partners/microsoft). Questi partner eseguire analisi del comportamento in corso nei dispositivi. Questa analisi rileva eventi imprevisti attivi e quindi passa tali informazioni a Intune per la valutazione della conformità in tempo reale.  

    - Questa valutazione è post-sicurezza violazione e basata su evento imprevisto  

Microsoft corporate vice president Brad Anderson descrive l'accesso condizionale in modo approfondito con le demo live durante la presentazione di Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Accesso condizionale offre anche una posizione centralizzata per visualizzare l'integrità di tutti i dispositivi connessi alla rete. Si ottengono i vantaggi della scalabilità cloud, che è particolarmente utile per test le istanze di produzione di Configuration Manager.


## <a name="benefits"></a>Vantaggi

Ogni team IT è ossessionata con sicurezza di rete. È obbligatorio per assicurarsi che ogni dispositivo soddisfi i requisiti aziendali e di sicurezza prima dell'accesso alla rete. Grazie all'accesso condizionale, è possibile determinare i fattori seguenti: 
- Se tutti i dispositivi vengono crittografati  
- Se viene installato malware  
- Se le relative impostazioni sono state aggiornate  
- Se è jailbroken o rooted  

Accesso condizionale combina un controllo granulare ai dati aziendali con un'esperienza utente in grado di ottimizzare la produttività su qualsiasi dispositivo da qualsiasi posizione.

Il video seguente viene illustrato come [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) è integrato in scenari comuni che si verificano regolarmente:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Con CO-gestione, Intune può incorporare le responsabilità di Configuration Manager per valutare la conformità agli standard di protezione delle App o gli aggiornamenti necessari. Questo comportamento è importante per qualsiasi organizzazione IT che vuole continuare a usare Configuration Manager per app complesse e la gestione delle patch.

Accesso condizionale è anche un aspetto essenziale dello sviluppo di [Zero Trust rete](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) architettura. Con l'accesso condizionale i controlli di accesso dispositivo conforme coprono i livelli base della rete attendibile di Zero. Questa funzionalità è una parte rilevante della modalità di protezione dell'organizzazione in futuro.

Per altre informazioni, vedere il post di blog sul [miglioramento dell'accesso condizionale con i dati sul rischio di computer da Windows Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Case study

L'IT Wipro società di consulenza utilizza l'accesso condizionale per proteggere e gestire i dispositivi usati da tutti i 91,000 dipendenti. In un recente case study, vice presidente del personale IT Wipro indicato:

> *Ottenere l'accesso condizionale è una vera conquista per Wipro. A questo punto, tutti i dipendenti hanno accesso mobile alle informazioni su richiesta. * 
>  *è migliorato la produttività di dipendente e comportamento di sicurezza. A questo punto i 91,000 dipendenti trarre profitto dall'accesso a sicurezza elevata per più di 100 applicazioni da qualsiasi dispositivo, ovunque.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Altri esempi includono: 

- Nestle, chi usa l'accesso condizionale basato su app per dipendenti oltre 150.000  

- La società di software di automazione, cadenza, chi può ora assicurarsi che "solo i dispositivi gestiti hanno accesso alle app di Office 365, ad esempio i team e la rete intranet aziendale." Possano offrire anch ' personale di "accesso sicuro ad altre App basate su cloud, ad esempio Workday e Salesforce". Per altre informazioni sull'esperienza del cadenza con Intune, vedere [cadenza aumenta la velocità del business con gli strumenti di collaborazione per dispositivi mobili in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune è anche completamente integrato con partner come Cisco ISE, Aruba Clear Pass e Citrix NetScaler. Questi partner, è possibile mantenere i controlli di accesso in base allo stato di conformità del dispositivo e la registrazione in Intune in queste altre piattaforme.

Per altre informazioni, vedere i video seguenti:
- [Accesso condizionale di Brad Anderson demo in dettaglio](https://youtu.be/8321obNofgM?t=547)  
- [Dettagli aggiuntivi da Endpoint zona 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposta di valore

Con accesso condizionale e l'integrazione di ATP, si sta, l'ottimizzazione di un componente fondamentale di tutte le organizzazioni IT: proteggere l'accesso cloud.

In più di 63% di tutte le violazioni della sicurezza dei dati, gli utenti malintenzionati accedere alla rete dell'organizzazione tramite le credenziali utente deboli, impostate come predefinite o rubate. Poiché l'accesso condizionale è incentrato sulla protezione l'identità dell'utente, limita il furto di credenziali. Accesso condizionale, gestisce e protegge le identità con privilegi o senza privilegi. Non vi è alcun modo migliore per proteggere i dispositivi e dati al loro interno.

Poiché l'accesso condizionale è un componente essenziale di Enterprise Mobility + Security (EMS), non il programma di installazione in locale o architettura necessarie. Con Intune e Azure Active Directory (Azure AD), è possibile configurare rapidamente l'accesso condizionale nel cloud. Se attualmente si usa Configuration Manager, è facilmente possibile estendere l'ambiente nel cloud con CO-gestione e iniziare a usarlo subito.

Per altre informazioni sull'integrazione ATP, vedere questo post di blog [punteggio di rischio di dispositivo Windows Defender ATP espone nuove ad attacco informatico, le unità di accesso condizionale per proteggere le reti](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Illustra in dettaglio come un gruppo di hacker avanzate utilizzato mai prima d'ora gli strumenti di visualizzazione. Microsoft cloud rilevato e li arrestato utenti designati risultavano l'accesso condizionale. L'intrusione attivato i criteri di accesso condizionale basati sul rischio del dispositivo. Anche se l'autore dell'attacco già presente un punto di appoggio in rete, le macchine sfruttate. sono state automaticamente limitare l'accesso ai servizi dell'organizzazione e i dati gestiti da Azure AD.



## <a name="configure"></a>Configurare

Accesso condizionale è facile da usare quando si [abilitare la co-gestione](/sccm/comanage/how-to-enable). Richiede lo spostamento di **i criteri di conformità** carico di lavoro di Intune. Per altre informazioni, vedere [Come passare i carichi di lavoro di Configuration Manager a Intune](/sccm/comanage/how-to-switch-workloads). 

Per altre informazioni sull'uso dell'accesso condizionale, vedere gli articoli seguenti: 

- [Accesso condizionale in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Criteri di conformità del dispositivo Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Accesso condizionale basato su App con Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Funzionalità di accesso condizionale diventano disponibili immediatamente per la gestione ibrida Azure dispositivi aggiunti ad AD. Queste funzionalità includono l'autenticazione a più fattori e controllo di accesso di Azure AD join ibrido. Questo comportamento è perché questi elementi sono basati sulle proprietà di Azure AD. Per sfruttare basata sulla configurazione della valutazione di Intune e Configuration Manager, abilitare la co-gestione. Questa configurazione consente controllo di accesso direttamente da Intune per i dispositivi conformi. Offre inoltre funzionalità valutazione dei criteri di conformità di Intune.  

