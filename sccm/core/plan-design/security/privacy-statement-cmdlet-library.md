---
title: Informativa sulla privacy per la libreria di cmdlet di Configuration Manager
description: Informazioni su come Microsoft raccoglie e usa i dati relativi alla libreria di cmdlet di System Center Configuration Manager.
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: c00bbd176dfef83a3e32d8e6747fd902bebb104b
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Informativa sulla privacy di System Center Configuration Manager - Libreria di cmdlet di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa informativa sulla privacy riguarda le funzionalità di System Center Configuration Manager Cmdlet Library.  

## <a name="usage-data"></a>Dati di utilizzo  
 **Scopo della funzionalità**   
La libreria di cmdlet di System Center Configuration Manager consente di usare i cmdlet e gli script di Windows PowerShell per gestire una gerarchia di Configuration Manager. Oltre a raccogliere informazioni sul modo in cui vengono usati i cmdlet della libreria per individuare le tendenze e i modelli di utilizzo, la libreria di cmdlet raccoglie anche i tipi e i numeri di errori riscontrati durante l'uso dei cmdlet.  

 **Informazioni raccolte, elaborate o trasmesse**   
I dati di utilizzo raccolti includono quelli sull'avvio, l'arresto e l'interruzione di cmdlet e sull'esecuzione di metriche di attività e di cmdlet deprecati per le operazioni dei provider di Systems Management Server (SMS) correlate ai cmdlet. Si tratta di informazioni che non consentono di identificare l'utente.  Le informazioni sugli errori raccolte includono gli errori restituiti dai cmdlet e i dettagli relativi agli errori delle eccezioni. Alcune segnalazioni con i dettagli sugli errori potrebbero inavvertitamente contenere identificatori individuali, come il numero di serie di un dispositivo connesso al computer. La libreria dei cmdlet filtra e rende anonime le informazioni nelle segnalazioni errori, al fine di rimuovere gli identificatori individuali prima della trasmissione a Microsoft.  

 **Uso delle informazioni**   
Microsoft usa queste informazioni per migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi offerti.  

 **Scelta/controllo**   
La funzionalità Dati di Utilizzo è abilitata per impostazione predefinita. La libreria di cmdlet di System Center Configuration Manager ha due chiavi del Registro di sistema che controllano questa funzionalità.  

 Per esprimere un rifiuto esplicito, l'utente deve configurare questi due valori delle chiavi del Registro di sistema, uno per ognuno dei provider di Event Tracing for Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (consente di rifiutare in modo esplicito la funzionalità Dati di utilizzo per il provider dell'unità)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (consente di rifiutare in modo esplicito la funzionalità Dati di utilizzo per i cmdlet)  

 Le modifiche alle impostazioni relative ai dati di utilizzo sono specifiche per il computer in cui vengono apportate.  

 Per dettagli su come configurare i dati di utilizzo (raccolta), vedere la [documentazione della libreria di cmdlet di System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).   
