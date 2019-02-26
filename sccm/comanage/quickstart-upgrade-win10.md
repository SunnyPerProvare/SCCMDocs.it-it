---
title: Aggiornare Windows 10
titleSuffix: Configuration Manager
description: Aggiornare i dispositivi a Windows 10 versione 1709 o versioni successive, che è necessario per la co-gestione
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0815a974f3b1f29f664a2948eed33de24c6ecff3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755301"
---
# <a name="upgrade-windows-10-for-co-management"></a>Aggiornare Windows 10 per la co-gestione

Quando si lavora verso onboarding all'organizzazione di CO-gestione, recupero ora corrente è un ostacolo significativo per alcuni clienti. Richiede la co-gestione [Windows 10 versione 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) o versione successiva. Dopo l'aggiornamento di Windows e configurare la registrazione automatica, i client vengono registrati automaticamente per CO-gestione.

Nel video seguente, senior program manager Rob York e product marketing manager Locky Ainley discutere e demo per l'aggiornamento a Windows 10 per la co-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Il motivo per cui eseguire l'aggiornamento?

Tra gli altri miglioramenti della piattaforma, Windows 10 versione 1709 e successive supporta la registrazione automatica. Questo comportamento rende un dispositivo registrati in Intune automaticamente quando è stato aggiunto l'Azure Active Directory (Azure AD). 

Per altre informazioni, vedere [la registrazione automatica di attivare Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Come eseguire questa operazione

Di seguito sono riportati alcuni suggerimenti che appresi di aiutare migliaia di clienti di ottenere rapidamente corrente:

- Usare le distribuzioni in più fasi per implementare questo aggiornamento per le persone giuste a destra volte. Per altre informazioni, vedere [Creare distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Utilizzare memorizzazione anticipata nella cache per ridurre i tempi di attesa degli utenti. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Usare il modello di sequenza di attività di aggiornamento sul posto predefinito. Configurare quindi i passaggi per la pre e post-aggiornamento e le azioni di errore. Per altre informazioni, vedere [consigliati i passaggi della sequenza di attività post-elaborazione](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Se l'ambiente dispone di una forza lavoro mobile elevata, Configuration Manager supporta l'aggiornamento sul posto tramite cloud management gateway (CMG). Questa funzionalità consente di aggiornare i client Windows 10 quando si trovano su internet. Per altre informazioni sul gateway di gestione cloud, vedere [ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Offrire un acconsenti esplicitamente al CO-gestione per gli utenti che desiderano essere adottato. Questo approccio accelera l'adozione iniziale. Identificando queste persone in anticipo, è possibile rendere certi un'adeguata copertura le radici di un'implementazione. Riceverai inoltre la convalida e commenti e suggerimenti da utenti che sono interessati a versioni più frequenti e di modifica. Primi programmi adopter generano interesse per le nuove tecnologie e aumento delle dimensioni nel corso del tempo.  


## <a name="case-studies"></a>Case study

Microsoft IT distribuito Windows 10 utenti distribuiti 96,000 presso Microsoft. La distribuzione inclusi sia gli utenti remoti e gli utenti nella rete aziendale. La distribuzione completata nelle nove settimane. Per altre informazioni sull'esperienza relativa, vedere [distribuzione di Windows 10 in Microsoft come un aggiornamento sul posto](https://www.microsoft.com/download/details.aspx?id=50377).  

Un produttore di grandi dimensioni European software Usa correttamente un gruppo di utilizzatori iniziali. Dopo il test iniziale e la distribuzione pilota di gruppi, circa 2.000 dipendenti riceveranno il primo aggiornamento, gli aggiornamenti e software. Questo gruppo include il personale IT e fornire il consenso esplicito volontari. Questo livello di coinvolgimento con i propri utenti offre un maggiore livello di confidenza durante il test e più credibilità quando iniziano a implementazioni di massa.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se è necessaria assistenza con l'aggiornamento a Windows 10 in qualsiasi punto del processo, andare al [Microsoft FastTrack](https://Microsoft.com/FastTrack/), accedi e richiedere assistenza. 

Per altre informazioni, vedere [assistenza dal FastTrack](/sccm/comanage/quickstart-fasttrack). 

