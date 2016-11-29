---
title: Informativa sulla privacy di System Center Configuration Manager - Libreria di cmdlet di Configuration Manager
description: Informazioni su come Microsoft raccoglie e usa i dati relativi alla libreria di cmdlet di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Informativa sulla privacy di System Center Configuration Manager - Libreria di cmdlet di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa informativa sulla privacy riguarda le funzionalità di System Center Configuration Manager Cmdlet Library.  

## <a name="usage-data"></a>Dati di utilizzo  
 **Scopo della funzionalità**   
System Center Configuration Manager Cmdlet Library consente di usare i cmdlet e gli script di Windows PowerShell per gestire una gerarchia di Configuration Manager. Oltre a raccogliere informazioni sul modo in cui vengono usati i cmdlet inclusi nella libreria allo scopo di individuare le tendenze e i modelli di utilizzo,  Cmdlet Library raccoglie anche i tipi e i numeri di errori riscontrati durante l'utilizzo dei cmdlet.  

 **Informazioni raccolte, elaborate o trasmesse**   
i dati di utilizzo raccolti includono quelli sull'avvio, l'arresto e l'interruzione di cmdlet e sull'esecuzione di metriche di attività e di cmdlet deprecati per le operazioni dei provider di SMS correlate ai cmdlet. Si tratta di informazioni che non consentono di identificare l'utente.  Le informazioni sugli errori raccolte includono gli errori restituiti dai cmdlet e i dettagli relativi agli errori delle eccezioni. Alcune segnalazioni con i dettagli sugli errori potrebbero inavvertitamente contenere identificatori individuali, ad esempio il numero di serie di un dispositivo connesso al computer. Cmdlet Library filtra e rende anonime le informazioni contenute nelle segnalazioni errori, al fine di rimuovere eventuali identificatori individuali prima della trasmissione a Microsoft.  

 **Uso delle informazioni**   
Microsoft usa queste informazioni per migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi offerti.  

 **Scelta/controllo**   
La funzionalità Dati di Utilizzo è abilitata per impostazione predefinita. System Center Configuration Manager Cmdlet Library include due chiavi del Registro di sistema per controllare questa funzionalità.  

 Per esprimere un rifiuto esplicito, l'utente deve configurare questi due valori delle chiavi del Registro di sistema, uno per ognuno dei provider di Event Tracing for Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (consente di rifiutare in modo esplicito la funzionalità Dati di utilizzo per il provider dell'unità)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (consente di rifiutare in modo esplicito la funzionalità Dati di utilizzo per i cmdlet)  

 Le modifiche alle impostazioni relative ai dati di utilizzo sono specifiche per il computer in cui vengono apportate.  

 Per altre informazioni su come configurare i dati di utilizzo (raccolta), vedere la [documentazione della libreria di cmdlet di System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  

## <a name="update-check"></a>Verifica degli aggiornamenti  
 **Scopo della funzionalità**   
System Center Configuration Manager Cmdlet Library verifica automaticamente ogni giorno se sono disponibili aggiornamenti per la libreria e invita l'utente a scaricare la libreria aggiornata.  

 **Informazioni raccolte, elaborate o trasmesse**   
Durante la verifica degli aggiornamenti di Cmdlet Library verrà eseguito il download di un file di testo di piccole dimensioni dall'Area download Microsoft per eseguire un controllo della versione.   Questo file non viene archiviato a livello locale.  Cmdlet Library non eseguirà l'aggiornamento automatico del software.  

 **Uso delle informazioni**   
Microsoft usa queste informazioni per migliorare la qualità, la sicurezza e l'integrità dei prodotti e dei servizi offerti.  

 **Scelta/controllo**   
il controllo degli aggiornamenti è abilitato per impostazione predefinita.  La libreria di cmdlet di System Center Configuration Manager include questi cmdlet per il controllo della funzionalità di notifica degli aggiornamenti:  

-   `Get-CMCmdletUpdateCheck` scarica la configurazione della funzionalità di aggiornamento e indicherà se i criteri utente verranno sostituiti da criteri di sistema.  

-   `Send-CMCmdletUpdateCheck` consente di eseguire una verifica non pianificata degli aggiornamenti. Durante una verifica non pianificata le impostazioni dei criteri non vengono prese in considerazione.  

-   `Set-CMCmdletUpdateCheck` consente di configurare le impostazioni per la verifica degli aggiornamenti per singolo utente o per singolo sistema. Per configurare le impostazioni di sistema, è necessario essere un amministratore.  

 Per altre informazioni su come configurare il controllo degli aggiornamenti, vedere la [documentazione della libreria di cmdlet di System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  



<!--HONumber=Nov16_HO1-->


