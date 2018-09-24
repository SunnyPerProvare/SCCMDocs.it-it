---
title: Soluzione MDM ibrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Informazioni sulla gestione di dispositivi mobili (MDM) ibrida con Configuration Manager e Microsoft Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f65c7665d5c055fc2a1636a1c9556b4ff75a4f7
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584612"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Soluzione MDM ibrida con Configuration Manager e Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
> <!--Intune feature 2683117--> Dopo il lancio in Azure oltre un anno fa, sono state aggiunte a Intune centinaia di nuove funzionalità del servizio leader di settore e richieste dai clienti. Il servizio offre ora molte più funzionalità di quelle offerte nella gestione di dispositivi mobili (MDM) ibrida. Intune in Azure offre un'esperienza amministrativa più integrata e semplificata per le esigenze di mobilità aziendale.
> 
> La maggior parte dei clienti sceglie di conseguenza Intune in Azure piuttosto che la soluzione MDM ibrida. Sempre meno clienti usano la soluzione MDM ibrida, mentre il numero di quelli che passano al cloud è in continuo aumento. L'1 settembre 2019, Microsoft ritirerà quindi l'offerta di servizio MDM ibrido. Pianificare la [migrazione a Intune in Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) per la gestione dei dispositivi mobili. 
> 
> Questa modifica non incide su Configuration Manager locale o sulla [co-gestione per i dispositivi Windows 10](/sccm/core/clients/manage/co-management-overview). Se non si è certi di usare la soluzione MDM ibrida, passare all'area di lavoro **Amministrazione** della console di Configuration Manager, espandere **Servizi Cloud** e fare clic su **Sottoscrizioni a Microsoft Intune**. Se è configurata una sottoscrizione di Microsoft Intune, il tenant è configurato per la soluzione MDM ibrida.
> 
> **Quali sono le conseguenze di questa modifica?**
> 
> - Microsoft supporterà l'utilizzo di MDM ibrido per il prossimo anno. La funzionalità continuerà a ricevere le principali correzioni di bug. Microsoft supporterà le funzionalità esistenti nelle nuove versioni del sistema operativo, ad esempio la registrazione in iOS 12. Non saranno disponibili nuove funzionalità per la soluzione MDM ibrida.  
> 
> - Se si esegue la migrazione a Intune in Azure prima della fine dell'offerta MDM ibrida, non ci sarà alcun impatto sugli utenti finali.  
> 
> - Le licenze rimangono invariate. Le licenze di Intune in Azure sono incluse con la soluzione MDM ibrida.  
> 
> - Microsoft inizierà a bloccare l'onboarding dei nuovi clienti della soluzione MDM ibrida a partire da novembre 2018.  
> 
> - L'1 settembre 2019, i dispositivi MDM ibridi rimanenti non riceveranno più criteri, app o aggiornamenti della sicurezza.  
> 
> **Operazioni di preparazione alla modifica**
> 
> - Iniziare a pianificare la migrazione della soluzione MDM dalla console di ConfigMgr ad Azure. Molti clienti, incluso Microsoft IT, hanno completato questo processo. Per altre informazioni, vedere questo [case study di Microsoft](https://aka.ms/Intune_MSFT).  
> 
> - Esaminare gli strumenti e la documentazione seguenti per semplificare il processo di transizione dalla soluzione MDM ibrida a Intune in Azure:  
>     - [Importare i dati di Configuration Manager in Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Contattare il Partner of Record o il partner di FastTrack per assistenza. [FastTrack per Microsoft 365](https://aka.ms/hybrid_fasttrack) può agevolare la migrazione dalla soluzione MDM ibrida a Intune in Azure. 
> 
> Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://aka.ms/hybrid_notification).



Con la funzionalità di gestione di dispositivi mobili (MDM) ibrida di Configuration Manager, gestire i dispositivi iOS, Windows e Android. Tutte le attività di gestione vengono gestite dalla console di Configuration Manager in cui si esegue il resto delle attività di gestione, integrate perfettamente con il servizio online di Microsoft Intune via Internet. Usare Configuration Manager per consentire agli utenti di accedere alle risorse aziendali dai propri dispositivi in modo protetto e gestito. Usando la gestione di dispositivi si proteggono i dati aziendali e si dà la possibilità agli utenti di registrare i propri dispositivi mobili personali o di proprietà dell'azienda per l'accesso ai dati aziendali. 

Questo articolo presuppone che si usi Configuration Manager per gestire i computer. Presuppone anche che si sia interessati a estendere la console di Configuration Manager con Intune per gestire i dispositivi mobili. 



## <a name="capabilities"></a>Funzionalità

La soluzione MDM ibrida supporta le funzionalità di gestione seguenti nei dispositivi:

-   Ritirare e cancellare dispositivi  

-   Configurare le impostazioni di conformità come le password, la protezione, il roaming, la crittografia e le comunicazioni wireless  

-   Distribuire app line-of-business (LOB) ai dispositivi  

-   Distribuire le app ai dispositivi che si connettono a Windows Store, Windows Phone Store, App Store o Google Play  

-   Raccogliere l'inventario hardware  

-   Raccogliere l'inventario software usando i report incorporati  

Per informazioni sulle nuove funzionalità disponibili per il software MDM ibrido, vedere [What's new in hybrid mobile device management](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management) (Novità della gestione di dispositivi mobili ibrida).



## <a name="hybrid-mdm-enrollment"></a>Registrazione della soluzione MDM ibrida

Per introdurre i dispositivi nella gestione ibrida, i dispositivi devono essere registrati nel servizio. La modalità di registrazione dei dispositivi varia a seconda del tipo di dispositivo in uso, della proprietà e del livello di gestione necessario.

- **BYOD (Bring Your Own Device)**: gli utenti registrano i telefoni, i tablet o i PC personali  

- **Dispositivo di proprietà dell'azienda**: rende possibili scenari di gestione come la cancellazione remota, i dispositivi condivisi o l'affinità utente per un dispositivo  

- Se si usa [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), sia in locale che ospitato nel cloud, è possibile abilitare la gestione semplice con Intune, senza registrazione. I PC Windows possono essere anche gestiti tramite il [software client di Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
