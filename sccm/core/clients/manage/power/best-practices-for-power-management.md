---
title: Procedure consigliate per il risparmio energia | Microsoft Docs
description: Apprendere le procedure consigliate per il risparmio energia in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89


---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Procedure consigliate per il risparmio energia in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager usare le seguenti procedure consigliate per il risparmio energia.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Eseguire la fase di monitoraggio in un momento rappresentativo  
 La fase di monitoraggio del risparmio energia fornisce informazioni su consumo di energia elettrica, attività, funzionalità di risparmio energia e impatto sull'ambiente dei computer nell'organizzazione. Assicurarsi di aver scelto un momento rappresentativo per eseguire la fase di monitoraggio. Ad esempio, eseguire la fase di monitoraggio durante un giorno festivo non genera un report realistico relativo all'uso di energia elettrica da parte dei computer.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Creare una raccolta di controllo dei computer senza alcuna combinazione per il risparmio di energia applicata  
 Creare due raccolte di computer per semplificare il monitoraggio degli effetti dell'applicazione delle combinazioni per il risparmio di energia ai computer. La prima raccolta deve contenere la maggior parte dei computer a cui si vuole applicare le impostazioni di risparmio energia e l'altra raccolta (raccolta di controllo) deve contenere gli altri computer. Applicare la combinazione per il risparmio energia necessaria alla raccolta contenente la maggior parte dei computer. È quindi possibile eseguire report per confrontare i costi energetici, il consumo energetico e l'impatto ambientale dei computer a cui sono state applicate le impostazioni di risparmio energia con la raccolta di controllo a cui invece tali impostazioni non sono state applicate.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Eseguire il report Impostazioni risparmio energia prima di applicare una combinazione per il risparmio energia  
 Prima di applicare una combinazione per il risparmio energia a una raccolta di computer, eseguire il report **Impostazioni risparmio energia** per analizzare le impostazioni di risparmio energia già configurate nei computer della raccolta. Se si applicano nuove impostazioni di risparmio energia ai computer senza prima esaminare le impostazioni esistenti, ciò potrebbe causare un aumento del consumo di energia.  

## <a name="exclude-servers-from-power-management"></a>Escludere server dal risparmio energia  
 La funzionalità di risparmio energia per i computer che eseguono Windows Server non è supportata, anche se vengono raccolti i dati relativi al consumo di energia. Assicurarsi di aggiungere i server a una raccolta ed escludere tale raccolta dal risparmio energia.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Escludere i computer che non si vuole gestire  
 Se sono presenti computer a cui non si vuole applicare il risparmio energia, aggiungerli a una raccolta e assicurarsi che tale raccolta venga esclusa dal risparmio energia.  

 Esempi di computer che possono essere esclusi dal risparmio energia:  

-   Computer che devono rimanere accesi.  

-   Computer a cui gli utenti devono collegarsi mediante Connessione desktop remoto.  

-   Computer che non possono usare il risparmio energia.  

-   Computer con il ruolo del sistema del sito del punto di distribuzione.  

-   Computer pubblici, ad esempio chioschi multimediali, display informativi o console di monitoraggio, in cui il computer e il monitor devono essere sempre accesi.  

 Per altre informazioni, vedere [Configuring Power Management in System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md) (Configurazione del risparmio energia in System Center Configuration Manager).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>Applicare la combinazione per il risparmio di energia a una raccolta di test di computer  
 Analizzare sempre l'effetto dell'applicazione della combinazione per il risparmio di energia a una raccolta di test di computer prima di applicare tale combinazione a una raccolta più grande di computer.  

 Le impostazioni di risparmio energia applicate a computer che eseguono Windows XP o Windows Server 2003 non vengono ripristinate sui valori originali anche se i computer vengono esclusi dalla funzionalità di risparmio energia. Nelle versioni successive di Windows, l'esclusione di un computer dal risparmio energia causa il ripristino sui valori originali di tutte le impostazioni di risparmio energia. Non è possibile ripristinare i valori originali per singole impostazioni di risparmio energia.  

## <a name="apply-power-plan-settings-individually"></a>Applicare le impostazioni della combinazione per il risparmio di energia singolarmente  
 Monitorare l'effetto dell'applicazione di ogni impostazione di risparmio energia prima di applicare quello successivo per verificare che ogni impostazione abbia l'effetto richiesto. Per altre informazioni sulle impostazioni della combinazione per il risparmio di energia, vedere la sezione [Impostazioni disponibili per le combinazioni per il risparmio di energia](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) (Available power management plan settings) nell'argomento [How to create and apply power plans in System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md) (Come creare e applicare combinazioni per il risparmio di energia in System Center Configuration Manager).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Monitorare regolarmente i computer per verificare se sono applicate più combinazioni per il risparmio di energia  
 La funzionalità Risparmio energia include un report che visualizza i computer a cui sono applicate più combinazioni per il risparmio di energia.  

 Se un computer è un membro di più raccolte, ognuna con combinazioni per il risparmio di energia diverse, verranno eseguite le azioni seguenti:  

-   Combinazione per il risparmio di energia: se a un computer sono applicati più valori per le impostazioni di risparmio energia, viene usato il valore meno restrittivo.  

-   Ora riattivazione: se a un computer desktop vengono applicate più ore di riattivazione, verrà usata l'ora più vicina alla mezzanotte.  

     Per altre informazioni, vedere la sezione [Computer con più combinazioni per il risparmio di energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) (Computer con più combinazioni per il risparmio di energia) nell'argomento [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md) (Come monitorare e pianificare il risparmio di energia in System Center Configuration Manager). Per altre informazioni su come il risparmio di energia risolve i conflitti, vedere [How to create and apply power plans in System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md) (Come creare a applicare combinazioni per il risparmio di energia in System Center Configuration Manager).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Salvare o esportare le informazioni sul risparmio di energia durante la fase di pianificazione e monitoraggio del risparmio energia  
 Le informazioni relative al risparmio energia utilizzate per i report giornalieri vengono conservate nel database del sito di Configuration Manager per 31 giorni.  

 Le informazioni relative al risparmio energia usate per i report mensili vengono conservate nel database del sito di Configuration Manager per 13 mesi.  

 Quando si creano report durante le fasi di monitoraggio e pianificazione e di verifica della conformità per il risparmio energia, è necessario salvare o esportare i risultati dei report di cui si vuole conservare i dati per confronti successivi, nel caso vengano in seguito rimossi da Configuration Manager.  



<!--HONumber=Dec16_HO3-->


