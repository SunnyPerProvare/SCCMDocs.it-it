---
title: "Introduzione alle impostazioni di conformità | Microsoft Docs"
description: "Informazioni sul funzionamento delle impostazioni di conformità in System Center Configuration Manager. Informazioni anche sui concetti principali che è necessario conoscere."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: "11"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b9f997caf5ca4753f95ab2e2cf680bdac40d29b7
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introduzione alle impostazioni di conformità in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di iniziare a creare elementi di configurazione di System Center Configuration Manager, è consigliabile leggere questo argomento per capire il funzionamento delle impostazioni di conformità e apprendere i concetti principali necessari.  

## <a name="how-compliance-settings-works"></a>Funzionamento delle impostazioni di conformità  
 Con le impostazioni di conformità è possibile gestire la configurazione e la conformità di server, portatili, PC e dispositivi mobili nell'organizzazione.  

 Gli elementi di configurazione rientrano in due categorie principali:  

-   **Impostazioni per dispositivi gestiti con il client di Configuration Manager**: in genere i dispositivi in cui è stato installato il software client di Configuration Manager con il quale è possibile gestire il dispositivo.  

-   **Impostazioni per dispositivi gestiti senza il client di Configuration Manager**: in genere i dispositivi gestiti con Microsoft Intune o con la gestione dei dispositivi locale di Configuration Manager.  

## <a name="what-devices-are-supported"></a>Quali dispositivi sono supportati?  


|Tipo di dispositivo|Altre informazioni|  
|------------|----------------------|  
|PC Windows con il client di Configuration Manager|Consente di creare elementi di configurazione personalizzati con cui valutare elementi come chiavi del Registro di sistema, file e attributi di Active Directory.<br /><br /> Quando si usa il tipo di elemento di configurazione Windows 10, è possibile selezionare le impostazioni desiderate da un elenco predefinito.|  
|PC Windows registrati con Microsoft Intune|Selezionare le impostazioni desiderate da un elenco predefinito.|  
|Dispositivi iOS registrati con Microsoft Intune|Selezionare le impostazioni desiderate da un elenco predefinito.|  
|Dispositivi Android registrati con Microsoft Intune|Selezionare le impostazioni desiderate da un elenco predefinito.|  
|Dispositivi Windows Phone registrati con Microsoft Intune|Selezionare le impostazioni desiderate da un elenco predefinito.|  
|Computer Mac con il client di Configuration Manager|Consente di creare elementi di configurazione personalizzati con cui valutare elementi come valori delle preferenze (elenco delle proprietà) di Mac OS X e risultati restituiti da uno script.|  
|Computer Mac registrati con Microsoft Intune|Selezionare le impostazioni desiderate da un elenco predefinito.|  

## <a name="what-is-a-configuration-item"></a>Cos'è un elemento di configurazione?  
 Si può considerare un elemento di configurazione come un contenitore che archivia le informazioni seguenti (le informazioni configurazione dipenderanno dal tipo di elemento di configurazione):  

-   **Informazioni sul metodo di rilevamento** (per gli elementi di configurazione di Windows che contengono solo impostazioni dell'applicazione): consentono di rilevare se un'applicazione è installata rilevando il file Windows Installer corrispondente o con uno script personalizzato.  

-   **Impostazioni** : le impostazioni rappresentano le condizioni aziendali o tecniche usate per valutare la conformità nei dispositivi client. È possibile configurare una nuova impostazione o selezionare un'impostazione esistente in un computer di riferimento.  

-   **Regole di conformità** : le regole di conformità consentono di specificare le condizioni che definiscono la conformità di un elemento di configurazione. Prima che sia possibile valutare la conformità di un'impostazione, è necessario che tale impostazione disponga almeno di una regola di conformità. Alcune impostazioni consentono di monitorare e aggiornare i valori che risultano non conformi. È possibile creare nuove regole o passare a un'impostazione esistente in qualsiasi elemento di configurazione per selezionare le regole in esso contenute.  

-   **Piattaforme supportate** : si tratta delle piattaforme di dispositivo definite dall'utente su cui verrà valutata la conformità dell'elemento di configurazione. Se si distribuisce un elemento di configurazione in un dispositivo non incluso nell'elenco delle piattaforme supportate, non verrà valutato per la conformità.  

## <a name="what-is-a-configuration-baseline"></a>Cos'è una linea di base di configurazione?  
 La conformità viene valutata definendo una linea di base di configurazione che contiene gli elementi di configurazione da valutare, più una serie di impostazioni e regole che descrivono il livello di conformità desiderato. È possibile importare questi dati di configurazione dal Web nei pacchetti di configurazione di Microsoft System Center Configuration Manager come procedure consigliate da Microsoft e altri fornitori e importarli poi in Configuration Manager. In alternativa, è possibile creare nuovi elementi e linee di base di configurazione.  

 Dopo aver definito una linea di base di configurazione, è possibile distribuirla a utenti e dispositivi attraverso le raccolte e valutare la conformità delle relative impostazioni in base a una pianificazione. È possibile distribuire nei dispositivi più linee di base di configurazione. Questo garantisce un livello di controllo elevato.  

 I dispositivi client valutano la conformità rispetto a ogni linea di base di configurazione distribuita e segnalano immediatamente i risultati al sito usando messaggi sullo stato attuale e messaggi di stato. Se un dispositivo client non è attualmente connesso alla rete, ma ha scaricato gli elementi di configurazione a cui viene fatto riferimento in una linea di base di configurazione distribuita, viene valutata la conformità della linea di base di configurazione. Le informazioni di conformità vengono inviate dopo la riconnessione.  

 È possibile monitorare i risultati della valutazione della conformità della linea di base di configurazione dal nodo **Distribuzioni** nell'area di lavoro **Monitoraggio** della console di Configuration Manager, per visualizzare le cause più comuni di mancata conformità, gli errori e il numero di utenti e dispositivi interessati. È anche possibile eseguire report delle impostazioni di conformità per ottenere maggiori dettagli, ad esempio quali sono i dispositivi conformi o non conformi e quale elemento della linea di base di configurazione sta causando la mancata conformità di un computer. È anche possibile visualizzare i risultati della valutazione della conformità da computer Windows che eseguono il software client di Configuration Manager usando la scheda **Configurazioni** in **Configuration Manager** nel Pannello di controllo.  

## <a name="user-data-and-profiles-configuration-items"></a>Elementi di configurazione di profili e dati utente  
 Gli elementi di configurazione di profili e dati utente contengono le impostazioni che controllano il modo in cui gli utenti nella gerarchia gestiscono il reindirizzamento cartelle, i file offline e i profili mobili nei computer che eseguono Windows 8 o versione successiva. È possibile distribuirli in raccolte di utenti e monitorarne la conformità dal nodo **Monitoraggio** della console di Configuration Manager. A differenza di altri elementi di configurazione, non vanno aggiunti alle linee di base di configurazione prima di distribuirli. È infatti possibile distribuirli direttamente con la finestra di dialogo **Distribuisci elemento di configurazione profili e dati utente** .  

 Per informazioni dettagliate, vedere [Create user data and profiles configuration items](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items) (Creare dati utente ed elementi di configurazione dei profili).  

## <a name="remote-connection-profiles"></a>Profili di connessione remota  
 I profili di connessione remota in forniscono un set di strumenti e risorse che consentono di creare, distribuire e monitorare le impostazioni di connessione remota nei dispositivi dell'organizzazione. Distribuendo queste impostazioni, viene ridotto al minimo lo sforzo necessario degli utenti finali per connettersi ai computer nella rete aziendale.  

Per informazioni dettagliate, vedere [Create remote connection profiles](/sccm/compliance/deploy-use/create-remote-connection-profiles) (Creare profili connessione remota).  

## <a name="windows-edition-upgrade"></a>Aggiornamento dell'edizione Windows
I criteri di aggiornamento edizione consentono di aggiornare automaticamente i dispositivi che eseguono alcune versioni di Windows 10 a un'edizione più recente, specificando un nuovo codice Product Key o un file di licenza.

Per informazioni dettagliate, vedere [Upgrade Windows devices with the edition upgrade policy](/sccm/compliance/deploy-use/upgrade-windows-version) (Aggiornare i dispositivi Windows con i criteri di aggiornamento edizione)
