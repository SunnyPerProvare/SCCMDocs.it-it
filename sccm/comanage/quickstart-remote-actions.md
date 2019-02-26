---
title: Azioni remote con CO-gestione
titleSuffix: Configuration Manager
description: Eseguire azioni remote da Intune per dispositivi CO-gestiti
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4439aa280edaffbb59f8d49ece58e067a729ec91
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755426"
---
# <a name="remote-actions-with-co-management"></a>Azioni remote con CO-gestione

È necessario assicurarsi che tutti i dispositivi gestiti sono raggiungibili, indipendentemente da dove, ogni volta che si connette. È inoltre necessario fornire a ogni utente le informazioni che necessarie per rimanere produttivi, continuando a proteggere le App e dati. Con le azioni di dispositivi supportate da Intune, è possibile risolvere in modo remoto queste funzioni critiche.

Nel video seguente, principal program manager per Heidi Cheng e senior program manager Danny Guillory discutere e demo di azioni remote con CO-gestione:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Vantaggi

Azioni remote dispositivo offrono controlli di gestione del dispositivo senza interferire con i dati personali. Queste azioni dispositivo remoto consentono di: 
- Eliminare i dati aziendali nei dispositivi smarriti o rubati  
- Rinomina un dispositivo  
- Riavviare un dispositivo  
- Inventario dei dispositivi di revisione  
- Controllare in remoto un dispositivo  
- Cancellano le app OEM preinstallate con un riavvio Fresh Start  
- Eseguire un ripristino in qualsiasi dispositivo Windows 10 delle impostazioni  

Queste funzioni sono un modo semplice e importante proteggere i dati aziendali memorizzati su tali dispositivi, nel messaggio di posta elettronica o OneDrive.

Per altre informazioni su queste azioni, vedere [azioni remote disponibili](#available-remote-actions). 



## <a name="case-studies"></a>Case study

La società di consulenza globale Avanade Usa regolarmente azioni remote per gestire i dispositivi usati ai dipendenti di 30.000. In un [post di blog recenti](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), CIO di Avanade indicato:

> *Nostro win immediato evitando la funzionalità di Intune è la possibilità di reimpostare in modalità remota Windows su un computer. Questo è importante per noi per i computer persi o rubati, che è più comune nei nostri ad alta mobilità della forza lavoro. * 
>  *Questa è una funzionalità che è in caso contrario, sarebbe stato necessario compilare e gestire in un pacchetto di Configuration Manager personalizzato.*

Per altre informazioni su come usare queste azioni remote, vedere [azioni del dispositivo disponibili](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposta di valore

Quando un dispositivo di Configuration Manager è CO-gestito, queste funzioni in modo nativo privo di Configuration Manager aggiunge immediatamente. A questo punto è ora possibile eseguire qualsiasi azione remota che è supportata da Intune. 

Con CO-gestione, i dispositivi di Configuration Manager sono ora esattamente come qualsiasi altro dispositivo gestito da Intune. Ad esempio, hanno una presenza completa nel cloud e si può raggiungere fino a quando hanno accesso a internet. È possibile eseguire tutte queste azioni senza eseguire passaggi aggiuntivi oltre il CO-gestione.

Poiché il processo di autoregistrazione è trasparente all'utente, non vi è alcun impatto sulla loro produttività. L'utente non è necessario eseguire alcuna operazione.


### <a name="available-remote-actions"></a>Azioni remote disponibili

Usare queste azioni remote da Intune dopo aver [abilitare la co-gestione](/sccm/comanage/how-to-enable) in Configuration Manager.

#### <a name="remove-devices"></a>Rimuovere i dispositivi
- **Ritirare**: Questa azione rimuove le app gestite e dei dati (dove applicabile), le impostazioni e messaggio di posta elettronica i profili che sono stati assegnati al dispositivo. Il dispositivo viene quindi rimosso dalla gestione di Intune. Questo processo avviene alla successiva ora il dispositivo consente di archiviare e riceve remoto ritirare l'azione. La funzione Retire lascia i dati personali dell'utente nel dispositivo.  

- **Cancellazione**: Questa azione consente di ripristinare un dispositivo per le impostazioni predefinite. Se si sceglie l'opzione **mantenere l'account utente e lo stato di registrazione**, quindi i dati dell'utente vengano mantenuti. In caso contrario, l'unità in modo sicuro viene cancellato.  

- **Elimina**: Se si desidera rimuovere i dispositivi da Intune nel portale di Azure, eliminarli dal riquadro del dispositivo specifico. Alla successiva che verifica il dispositivo, rimuove tutti i dati aziendali memorizzati su di esso.  

Per altre informazioni, vedere [rimuovere i dispositivi con la cancellazione, ritiro o annullare manualmente la registrazione del dispositivo](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Cancellazione selettiva
<!--SCCMDocs issue 973--> Quando si sceglie un' **cancellazione selettiva di App**, rimuove i dati aziendali senza rimuovere i dati personali. Usare questa azione quando un dispositivo viene segnalato come smarrito o rubato. 

Per altre informazioni, vedere [come cancellare solo i dati aziendali dalle App gestite da Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>Sincronizzazione
Il **sincronizzazione** azione del dispositivo forza il dispositivo selezionato a registrarsi immediatamente in Intune. Quando un dispositivo esegue l'archiviazione, riceve immediatamente le azioni in sospeso o i criteri che è stato assegnato a esso.

Questa funzionalità consente di convalidare e risolvere i problemi di criteri assegnati, senza tempi di attesa per il successivo pianificato controllo immediatamente.

Per altre informazioni, vedere [sincronizzare i dispositivi per ottenere i criteri e le azioni con Intune più recente](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Riavvia
Il **riavviare** azione del dispositivo consente al dispositivo si sceglie di riavviare. Questa azione è utile quando è presente un riavvio in sospeso, ma l'utente non è disponibile per eseguire questa operazione.

Per altre informazioni, vedere [riavviare in remoto i dispositivi con Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Fresh Start
Il **Fresh Start** azione del dispositivo rimuove tutte le app installate in un dispositivo che esegue Windows 10, versione 1703 o successiva. Fresh Start consente di rimuovere le App (OEM) preinstallate in genere installati con un nuovo dispositivo.

Se si sceglie di non conservare i dati utente, il dispositivo ripristinato lo stato di out-of-box. Annulla la registrazione da Azure AD e MDM.

Se si dispongono di predeterminati requisiti in materia di quali App devono essere sul dispositivo, questa azione Elimina quelli che non soddisfano i criteri specificati.

Per altre informazioni, vedere [usare Fresh Start per ripristinare i dispositivi Windows 10 con Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Controllo remoto
Dispositivi gestiti da Intune possono essere amministrati in remoto mediante [TeamViewer](https://www.teamviewer.com/). TeamViewer è un programma di terze parti acquistati separatamente.

Per altre informazioni, vedere [usare TeamViewer per amministrare in remoto i dispositivi di Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurare

Diverso da controllo remoto con TeamViewer, per iniziare a usare queste azioni remote dispositivo in Intune, non sono necessarie ulteriori impostazioni dopo aver [abilitare la co-gestione](/sccm/comanage/how-to-enable).

Per altre informazioni sull'uso di TeamViewer per il controllo remoto, vedere [usare TeamViewer per amministrare in remoto i dispositivi di Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

