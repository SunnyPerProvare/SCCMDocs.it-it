---
title: Informativa sulla privacy per i cmdlet
titleSuffix: Configuration Manager
description: Informazioni su come Microsoft raccoglie e usa i dati correlati ai cmdlet di Configuration Manager
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e777c509ae0461120ae195712aaecf7f44813261
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70889233"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Informativa sulla privacy per la libreria di cmdlet di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa informativa sulla privacy riguarda le funzionalità di System Center Configuration Manager Cmdlet Library.  

## <a name="usage-data"></a>Dati di utilizzo  

#### <a name="what-this-feature-does"></a>Descrizione della funzionalità

La libreria di cmdlet di System Center Configuration Manager consente di usare i cmdlet e gli script di Windows PowerShell per gestire una gerarchia di Configuration Manager. Oltre a raccogliere informazioni sul modo in cui vengono usati i cmdlet della libreria per individuare le tendenze e i modelli di utilizzo, la libreria di cmdlet raccoglie anche i tipi e i numeri degli errori ricevuti durante l'uso dei cmdlet.  

#### <a name="information-collected-processed-or-transmitted"></a>Informazioni raccolte, elaborate o trasmesse
   
I dati di utilizzo raccolti includono quelli sull'avvio, sull'arresto e sull'interruzione di cmdlet e sull'esecuzione di metriche di attività e di cmdlet deprecati per le operazioni dei provider SMS correlate ai cmdlet. Si tratta di informazioni che non consentono di identificare l'utente. Le informazioni sugli errori raccolte includono gli errori restituiti dai cmdlet e i dettagli relativi agli errori delle eccezioni. Alcune segnalazioni con i dettagli sugli errori possono inavvertitamente includere identificatori individuali, come il numero di serie di un dispositivo connesso al computer. La libreria dei cmdlet filtra e rende anonime le informazioni nelle segnalazioni errori, al fine di rimuovere gli identificatori individuali prima della trasmissione a Microsoft.  

#### <a name="use-of-information"></a>Uso delle informazioni
   
Microsoft usa queste informazioni per migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi offerti.  

#### <a name="choicecontrol"></a>Scelta/controllo   

La funzionalità Dati di Utilizzo è abilitata per impostazione predefinita. La libreria di cmdlet di System Center Configuration Manager ha due chiavi del Registro di sistema che controllano questa funzionalità.  

 Per rifiutare esplicitamente e completamente, impostare questi due valori di chiave del Registro di sistema, relativi a ognuno dei provider Event Tracing for Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (consente di rifiutare esplicitamente la funzionalità Dati di utilizzo per il provider dell'unità)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (consente di rifiutare esplicitamente la funzionalità Dati di utilizzo per i cmdlet)  

  Le modifiche alle impostazioni relative ai dati di utilizzo sono specifiche per il computer in cui vengono apportate.  


## <a name="next-steps"></a>Passaggi successivi

[Documentazione della libreria di cmdlet di System Center Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
