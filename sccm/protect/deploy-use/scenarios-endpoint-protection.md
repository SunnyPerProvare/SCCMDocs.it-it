---
title: Scenario Endpoint Protection protegge i computer da malware | Documentazione Microsoft
description: Informazioni su come implementare Endpoint Protection in Configuration Manager per proteggere i computer da attacchi malware.
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: 8
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9fcbc0bb9c8ccd4265381ca4db7a363c8ae3b54a
ms.openlocfilehash: 2cdc57b766b18a6fdf21ec8748172c12b11b08db


---

# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>Scenario di esempio: uso di System Center Endpoint Protection per proteggere i computer dal malware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento illustra uno scenario d'esempio di implementazione di Endpoint Protection in Configuration Manager per proteggere i computer di un'organizzazione da attacchi malware.  

 In questo scenario Giorgio è l'amministratore di Configuration Manager presso Woodgrove Bank. La banca attualmente usa Microsoft Forefront Endpoint Protection 2010 per proteggere i computer dagli attacchi malware. Inoltre, la banca usa Criteri di gruppo di Windows per garantire che Windows Firewall sia abilitato in tutti i computer dell'azienda e che venga visualizzata una notifica agli utenti quando Windows Firewall blocca un nuovo programma.  

 A Giorgio è stato chiesto di aggiornare il software antimalware di Woodgrove Bank con System Center Endpoint Protection, in modo che la banca possa trarre vantaggio dalle funzionalità antimalware più recenti e sia in grado di gestire in modo centralizzato la soluzione antimalware dalla console di Configuration Manager. Questa implementazione presenta i requisiti seguenti:  

-   Usare Configuration Manager per gestire le impostazioni di Windows Firewall che sono attualmente gestite tramite i criteri di gruppo.  

-   Usare gli aggiornamenti software di Configuration Manager per scaricare le definizioni malware nei computer. Se gli aggiornamenti software non sono disponibili, ad esempio se il computer non è connesso alla rete aziendale, i computer devono scaricare gli aggiornamenti delle definizioni da Microsoft Update.  

-   I computer degli utenti devono eseguire un'analisi rapida del malware ogni giorno. I server devono invece eseguire un'analisi completa ogni sabato, fuori dall'orario lavorativo, alle ore 1:00.  

-   Inviare un messaggio di avviso ogni volta che si verifica uno dei seguenti eventi:  

    -   Viene rilevato malware su qualsiasi computer  

    -   Viene rilevata la stessa minaccia di tipo malware in più del 5% dei computer  

    -   Viene rilevata la stessa minaccia di tipo malware più di 5 volte nell'arco di 24 ore  

    -   Vengono rilevati più di 3 tipi diversi di malware nell'arco di 24 ore  

-   Disinstallare la soluzione antimalware esistente.  

 Giorgio esegue quindi la procedura seguente per implementare Endpoint Protection:  

##  <a name="steps-to-implement-endpoint-protection"></a>Passaggi per l'implementazione di Endpoint Protection  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio rivede le informazioni disponibili sui concetti di base per Endpoint Protection in Configuration Manager.|Per informazioni generali su Endpoint Protection, vedere [Endpoint Protection in System Center Configuration Manager](endpoint-protection.md).|  
|Giorgio esamina e implementa i prerequisiti necessari per l'uso di Endpoint Protection.|Per informazioni sui prerequisiti per Endpoint Protection, vedere [Pianificazione di Endpoint Protection](../plan-design/planning-for-endpoint-protection.md).|  
|Giorgio installa il ruolo di sistema del sito di Endpoint Protection in un solo server di sistema del sito, nella parte superiore della gerarchia di Woodgrove Bank.|Per altre informazioni su come installare il ruolo di sistema del sito di Endpoint Protection, vedere "Prerequisiti" in [Configurare Endpoint Protection](configure-endpoint-protection.md).|  
|Giorgio configura Configuration Manager per l'uso di un server SMTP per l'invio degli avvisi di posta elettronica.<br /><br /> **Nota:** è necessario configurare un server SMTP solo se si vuole ricevere una notifica tramite posta elettronica quando viene generato un avviso di Endpoint Protection.|Per altre informazioni, vedere [Configurare gli avvisi in Endpoint Protection](endpoint-configure-alerts.md).|  
|Giorgio crea una raccolta di dispositivi che contiene tutti i computer e i server in cui installare il client di Endpoint Protection. Assegna a questa raccolta il nome **Tutti i computer protetti da Endpoint Protection**.<br /><br /> **Suggerimento:** non è possibile configurare avvisi per raccolte di utenti.|Per informazioni su come creare raccolte, vedere [Come creare raccolte in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Configura gli avvisi seguenti per la raccolta: <br /><br />1) **Rilevato Malware**: Giorgio configura una gravità di avviso **critico**. <br /><br />2) **Lo stesso tipo di malware viene rilevato in un numero di computer**: Giorgio configura una gravità di avviso **critico** e specifica che l'avviso viene generato quando più del 5% dei computer esegue software dannoso rilevato. <br /><br />3) **Lo stesso tipo di software dannoso è stato rilevato più volte entro l'intervallo specificato in un computer**: Giorgio configura una gravità di avviso **critico** e specifica che l'avviso viene generato quando viene rilevato malware più di 5 volte in un periodo di 24 ore. <br /><br />4) **Più tipi di malware vengono rilevati nello stesso computer nell'intervallo specificato**: Giorgio configura una gravità di avviso **critico** e specifica che l'avviso viene generato quando vengono riscontrati più di 3 tipi di malware in un periodo di 24 ore.<br /><br /> Il valore di **gravità di avviso** indica il livello di avviso che verrà visualizzato nella console di Configuration Manager e negli avvisi ricevuti in un messaggio di posta elettronica.<br /><br /> Giorgio seleziona anche l'opzione **Visualizza questa raccolta nel dashboard di Endpoint Protection** in modo da poter monitorare gli avvisi nella console di Configuration Manager.|Vedere "Configurare gli avvisi per Endpoint Protection" in [Configurazione di Endpoint Protection in Configuration Manager](endpoint-configure-alerts.md).|  
|Giorgio configura gli aggiornamenti software di Configuration Manager per scaricare e distribuire gli aggiornamenti delle definizioni tre volte al giorno tramite una regola di distribuzione automatica.|Per altre informazioni, vedere la sezione "Uso degli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni" in [Usare gli aggiornamenti software di Configuration Manager per recapitare gli aggiornamenti delle definizioni](endpoint-definitions-configmgr.md).|  
|Giorgio verifica le impostazioni nel criterio antimalware predefinito, che contiene le impostazioni di sicurezza consigliate da Microsoft. Per consentire ai computer di eseguire un'analisi rapida ogni giorno, modifica le impostazioni seguenti:<br /><br /> 1) **Eseguire un'analisi veloce giornaliera nei computer client**: **Sì**.<br /><br /> 2) **Ora pianificazione analisi rapida giornaliera**:  **9.00**.<br /><br /> Giorgio nota che **Aggiornamenti distribuiti da Microsoft Update** è selezionata per impostazione predefinita come origine di aggiornamento delle definizioni. Ciò soddisfa il requisito aziendale per cui i computer devono scaricare le definizioni da Microsoft Update quando non possono ricevere gli aggiornamenti software di Configuration Manager.|Vedere [Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Giorgio crea una raccolta che contiene solo i server di Woodgrove Bank, denominata **Server di Woodgrove Bank**.|Vedere [Come creare le raccolte in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md)|  
|Giorgio crea un criterio antimalware personalizzato, denominato **Criterio server di Woodgrove Bank**. Aggiunge solo le impostazioni per **Analisi pianificate** e apporta le modifiche seguenti:<br /><br /> **Tipo di analisi**:  **Completa**<br /><br /> **Giorno analisi**:  **Sabato**<br /><br /> **Ora analisi**: **1:00**<br /><br /> **Eseguire un'analisi rapida giornaliera dei computer client**:  **No**.|Vedere [Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Giorgio distribuisce il criterio antimalware personalizzato **Criterio server di Woodgrove Bank** nella raccolta **Server di Woodgrove Bank** .|Vedere "Per distribuire criteri antimalware nei computer client" nell'argomento [Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Giorgio crea un nuovo set di impostazioni dei dispositivi client personalizzate per Endpoint Protection e assegna loro il nome **Impostazioni di Endpoint Protection per Woodgrove Bank**.<br /><br /> **Nota:** se non si vuole installare e abilitare Endpoint Protection in tutti i client nella gerarchia, assicurarsi che le opzioni **Gestire il client Endpoint Protection nei computer client** e **Installare il client Endpoint Protection nei computer client** siano entrambe impostate a **No** nelle impostazioni client predefinite.|Per altre informazioni, vedere [Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md).|  
|Configura le impostazioni seguenti per Endpoint Protection:<br /><br /> **Gestire il client Endpoint Protection nei computer client**:  **Sì**<br /><br /> Questa impostazione e il relativo valore assicurano che tutti i client di Endpoint Protection esistenti installati vengano gestiti da Configuration Manager.<br /><br /> **Installare il client Endpoint Protection nei computer client**:  **Sì**.<br /><br /> **Rimuovere automaticamente il software antimalware installato in precedenza prima di installare Endpoint Protection**:  **Sì**.<br /><br /> Questa impostazione e il relativo valore soddisfano il requisito aziendale per cui il software antimalware esistente deve essere rimosso prima che Endpoint Protection venga installato e abilitato.|Per altre informazioni, vedere [Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md).|  
|Giorgio distribuisce le impostazioni client **Impostazioni di Endpoint Protection di Woodgrove Bank** alla raccolta **Tutti i computer protetti da Endpoint Protection**.|Vedere "Configurare le impostazioni client personalizzate per Endpoint Protection" in [Configurazione di Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md).|  
|Giorgio usa la Creazione guidata criteri di Windows Firewall per creare un criterio configurando le impostazioni seguenti per il profilo di dominio:<br /><br /> 1) **Abilitare Windows Firewall**: **Sì**<br /><br /> 2)<br />                    **Notifica all'utente quando Windows Firewall blocca un nuovo programma**: **Sì**|Vedere [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md)|  
|Giorgio distribuisce i nuovi criteri firewall alla raccolta **Tutti i computer protetti da Endpoint Protection** che ha creato in precedenza.|Vedere "Per distribuire criteri di Windows Firewall" in [Come creare e distribuire criteri di Windows Firewall per Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md)|  
|Giorgio usa le attività di gestione disponibili per Endpoint Protection per gestire i criteri antimalware e di Windows Firewall, per eseguire analisi su richiesta dei computer quando necessario, per imporre ai computer di scaricare le definizioni più recenti e per specificare altre azioni da eseguire quando viene rilevato malware.|Vedere [Come gestire i criteri antimalware e le impostazioni del firewall per Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md)|  
|Giorgio usa i metodi seguenti per monitorare lo stato di Endpoint Protection e le azioni eseguite da Endpoint Protection:<br /><br /> 1) Tramite il nodo **Stato Endpoint Protection** di **Sicurezza** nell'area di lavoro **Monitoraggio**.<br /><br /> 2) Tramite il nodo **Endpoint Protection** nell'area di lavoro **Asset e conformità**.<br /><br /> 3) Tramite i report predefiniti di Configuration Manager.|Vedere [Come monitorare Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md)|  

 Giorgio comunica la corretta implementazione di Endpoint Protection al suo manager e conferma che i computer di Woodgrove Bank sono ora protetti dalla funzionalità antimalware, in base ai requisiti aziendali che gli sono stati specificati.



<!--HONumber=Dec16_HO3-->


