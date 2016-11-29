---

title: Integrazione con Windows Update for Business in Windows 10 | Configuration Manager
description: Usare Windows Update for Business per mantenere aggiornati i dispositivi dell'organizzazione basati su Windows 10 connessi al servizio Windows Update.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c4c6e50d0e1a34653226369cffdc0bde905398fc


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integrazione con Windows Update for Business in Windows 10

*Si applica a: System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) consente di mantenere i dispositivi basati su Windows 10 nell'organizzazione sempre aggiornati con le difese per la sicurezza e le funzionalità di Windows più recenti, quando questi dispositivi si connettono direttamente al servizio Windows Update (WU). Configuration Manager è in grado di distinguere tra i computer Windows 10 che ricevono gli aggiornamenti software da Windows Update for Business e i computer che li ricevono da WSUS.  

 Alcune funzionalità di Configuration Manager non sono disponibili per i client di Configuration Manager configurati per ricevere gli aggiornamenti da Windows Update. Tra queste, Windows Update for Business e Windows Insider:  

-   Report della conformità di Windows Update:  

    -   Configuration Manager non è a conoscenza degli aggiornamenti pubblicati in Windows Update. Questi aggiornamenti saranno visualizzati come **sconosciuti** nella console di Configuration Manager per i client di Configuration Manager configurati per ricevere gli aggiornamenti da Windows Update.  

    -   La risoluzione dei problemi relativi allo stato di conformità generale risulta difficile, perché lo stato **sconosciuto** veniva usato tipicamente solo per i client per cui non veniva segnalato lo stato di analisi da WSUS.  Questo stato include ora anche i client di Configuration Manager che ricevono gli aggiornamenti da Windows Update.  

    -   L'accesso condizionale (per le risorse aziendali) basato sullo stato di conformità di aggiornamento non funzionerà come previsto per i client che ricevono gli aggiornamenti da Windows Update, perché non risulterebbero mai conformi per Configuration Manager.  

    -   La conformità degli aggiornamenti delle definizioni fa parte dei report di verifica aggiornamenti generale e anche questo aspetto non funzionerà come previsto.  La conformità degli aggiornamenti delle definizioni fa anche parte della valutazione di accesso condizionale.  

-   Il report di stato generale di Endpoint Protection per Defender basato sullo stato di verifica aggiornamenti non restituirà risultati accurati a causa dei dati di analisi mancanti.  

-   Configuration Manager non è in grado di distribuire gli aggiornamenti Microsoft, ad esempio Office, Internet Explorer e Visual Studio, ai client connessi a Windows Update for Business per la ricezione degli aggiornamenti.  

-   Configuration Manager non è in grado di distribuire gli aggiornamenti di terze parti pubblicati in WSUS e gestiti tramite Configuration Manager ai client connessi a Windows Update for Business per la ricezione degli aggiornamenti.  

-   La distribuzione di client completi di Configuration Manager che usa l'infrastruttura di aggiornamenti software non funzionerà per i client connessi a Windows Update for Business per la ricezione degli aggiornamenti.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificare i client che usano WUfB per gli aggiornamenti di Windows 10  
 Usare la procedura seguente per identificare i client che usano WUfB per ottenere gli aggiornamenti di Windows 10, configurare tali client per interrompere l'uso di WSUS per ottenere gli aggiornamenti e distribuire l'impostazione di un agente client per disabilitare il flusso di lavoro di aggiornamenti software per questi client.  

 **Prerequisiti**  

-   Client che eseguono Windows 10 Desktop Pro o Windows 10 Enterprise Edition versione 1511 o successive  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) è distribuito e i client usano WUfB per ottenere gli aggiornamenti di Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Per identificare i client che usano WUfB  

1.  Disabilitare l'agente di Windows Update in modo che non esegua l'analisi rispetto a WSUS, se è stata precedentemente abilitata.   
    La chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** può essere impostata in modo da indicare se il computer sta eseguendo l'analisi rispetto a Windows Update o a WSUS.  Se il valore è 2, l'analisi non viene eseguita rispetto a WSUS.  

2.  Esiste un nuovo attributo, **UseWUServer**, nel nodo **Windows Update** di Configuration Manager - Esplora inventario risorse.  

3.  Creare una raccolta sulla base dell'attributo **UseWUServer** per tutti i computer connessi tramite WUfB per gli aggiornamenti.  

4.  Creare un'impostazione dell'agente client per disabilitare il flusso di lavoro di aggiornamento software e distribuire l'impostazione nella raccolta di computer connessi direttamente a WUfB.  

5.  Lo stato di conformità dei computer gestiti tramite Windows Update for Business sarà **Sconosciuto** e quindi questi non verranno conteggiati come parte della percentuale di conformità complessiva.  



<!--HONumber=Nov16_HO1-->


