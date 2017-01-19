---
title: "Funzionalità della versione Technical Preview 1602 per System Center Configuration Manager | Microsoft Docs"
description: "Informazioni sulle funzionalità disponibili nella versione Technical Preview 1602 per System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3bf44f850722afdb8dfe5922c8ceff11c9b56d08
ms.openlocfilehash: da69e2363114faa4f2e701f2784c90ec23537e42

---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>Funzionalità della versione Technical Preview 1602 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo presenta le funzionalità disponibili nella versione Technical Preview 1602 per System Center Configuration Manager. È possibile installare questa versione per aggiornare e aggiungere nuove funzionalità al sito di Technical Preview di Configuration Manager. Prima di installare questa versione Technical Preview, consultare l'argomento introduttivo [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager) per acquisire familiarità con i requisiti generali e con le limitazioni per l'uso di una versione Technical Preview, con le modalità di aggiornamento tra le versioni e con le modalità per offrire feedback e suggerimenti sulle funzionalità di una versione Technical Preview.  

 Di seguito sono riportate le nuove funzionalità disponibili con questa versione.  

##  <a name="a-namebkmkmdma-improvements-to-mobile-device-management"></a><a name="BKMK_MDM"></a> Miglioramenti nella gestione dei dispositivi mobili  

### <a name="ios-activation-lock"></a>Blocco attivazione di iOS  
 System Center Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone in un dispositivo. Una volta abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima di poter:  

-   Disattivare Trova il mio iPhone  

-   Cancellare il dispositivo  

-   Riattivare il dispositivo  

 Configuration Manager può richiedere lo stato del blocco attivazione per i dispositivi con e senza supervisione che eseguono iOS 7.1 e versioni successive. Per i dispositivi con supervisione, Intune può recuperare il codice del bypass del blocco attivazione e inviarlo direttamente al dispositivo.  

 Per altre informazioni, vedere [Proteggere i dispositivi iOS con il bypass del blocco attivazione per Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock)  

##  <a name="a-namebkmksc1601a-improvements-to-software-center-in-version-1602"></a><a name="BKMK_SC1601"></a> Miglioramenti di Software Center nella versione 1602  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aggiornare i criteri di computer e utenti da Software Center  
 È stata aggiunta una nuova opzione, **Criteri sincronizzazione**, alla pagina **Opzioni** > **Manutenzione computer** di Software Center che consente al computer di aggiornare i criteri di computer e utenti di Configuration Manager.  

##  <a name="a-namebkmkwin10servicinga-improvements-to-windows-10-servicing"></a><a name="BKMK_Win10Servicing"></a> Miglioramenti della manutenzione di Windows 10  
 Nella Technical Preview 1602 sono stati aggiunti i miglioramenti seguenti per la manutenzione di Windows 10:  

-   Nuove opzioni di filtro per i piani di manutenzione.  È ora possibile filtrare per **Lingua**, **Richiesto** e **Titolo**. Verranno aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati.  

-   Quando si seleziona la classificazione **Aggiornamenti** per la sincronizzazione degli aggiornamenti software, viene visualizzata una finestra di dialogo di avviso per informare gli utenti che è necessario l'[hotfix 3095113](https://support.microsoft.com/kb/3095113) di WSUS per la corretta sincronizzazione degli aggiornamenti software e per il corretto funzionamento della manutenzione di Windows 10.  Nella finestra di dialogo è possibile passare all'articolo della Knowledge Base per l'hotfix.  

-   Gli aggiornamenti disponibili di Windows 10 vengono visualizzati ora solo nel nodo **Manutenzione di Windows 10** \ **Tutti gli aggiornamenti di Windows 10** della console di Configuration Manager. Questi aggiornamenti non vengono più visualizzati nel nodo **Aggiornamenti software ** \ **Tutti gli aggiornamenti software**.  

-   Quando gli utenti finali avviano un pacchetto di aggiornamento di Windows 10, verrà visualizzata una finestra di dialogo che li informa che stanno per aggiornare il proprio sistema operativo.  



<!--HONumber=Dec16_HO3-->


