---
title: Assistenza a un gruppo di server | Configuration Manager
description: "La console di System Center Configuration Manager invia avvisi e stati per monitorare gli aggiornamenti e la conformità."
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
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: da7a5f1d075eb1fcd7c56b713401bb0f985fa487


---
# <a name="service-a-server-group"></a>Assistenza a un gruppo di server

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire da System Center Configuration Manager versione 1606, è possibile configurare le impostazioni di un gruppo di server per una raccolta per definire il numero, la percentuale o l'ordine con cui i computer nella raccolta installeranno gli aggiornamenti software. È anche possibile configurare gli script pre e post distribuzione di PowerShell per eseguire azioni personalizzate.

Quando si distribuiscono gli aggiornamenti software in una raccolta in cui sono state configurate le impostazioni del gruppo di server, Configuration Manager determina il numero dei computer nella raccolta che possono installare gli aggiornamenti software in qualsiasi momento e rende disponibile lo stesso numero di blocchi di distribuzione. Solo i computer che ottengono un blocco di distribuzione potranno avviare l'installazione dell'aggiornamento software. Quando un blocco di distribuzione è disponibile, un computer ottiene il blocco di distribuzione, installa gli aggiornamenti software e quindi rilascia il blocco di distribuzione quando l'installazione degli aggiornamenti software viene completata correttamente. In seguito, il blocco di distribuzione diventa disponibile per altri computer. Se un computer non può rilasciare un blocco di distribuzione, è possibile rilasciare manualmente tutti i blocchi di distribuzione del gruppo server per la raccolta.

>[!IMPORTANT]
>Tutti i computer della raccolta devono essere assegnati allo stesso sito.

#### <a name="to-create-a-collection-for-a-server-group"></a>Per creare una raccolta per un gruppo di server  
Le impostazioni del gruppo di server vengono configurate nelle proprietà di una raccolta di dispositivi. Per la manutenzione di un gruppo di server, tutti i membri della raccolta devono essere assegnati allo stesso sito. Per creare una raccolta e configurare le impostazioni del gruppo di server, procedere come segue:
1.  [Creare una raccolta di dispositivi](../../core/clients/manage/collections/create-collections.md) che contenga i computer del gruppo di server.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte di dispositivi**, quindi fare clic con il pulsante destro del mouse sulla raccolta che contiene i computer del gruppo di server e scegliere **Proprietà**.  

3.  Nella scheda **Generale** selezionare **Tutti i dispositivi fanno parte dello stesso gruppo di server**, quindi fare clic su **Impostazioni**.  

4.  Nella pagina **Impostazioni gruppo di server** specificare una delle impostazioni seguenti:  

    -   **Consentire a una percentuale di computer di essere aggiornati contemporaneamente**: specifica che solo una determinata percentuale di client vengono aggiornati in qualsiasi momento. Se, ad esempio, l'insieme ha 10 client e la raccolta viene configurata per aggiornare il 30% dei client allo stesso tempo, solo 3 client installeranno gli aggiornamenti software in qualsiasi momento.  

    -   **Consentire a un numero di computer di essere aggiornati contemporaneamente**: specifica che solo un certo numero di client possono essere aggiornati in un determinato momento.  

    -   **Specifica la sequenza di manutenzione**: specifica che i client nella raccolta saranno aggiornati uno alla volta nella sequenza che viene configurata. Un client installerà gli aggiornamenti software solo dopo che il client che lo precede nell'elenco avrà completato l'installazione degli aggiornamenti.  

5.  Specificare se usare uno script di pre-distribuzione (svuotamento del nodo) o di post-distribuzione (ripresa del nodo).  

    > [!TIP]  
    >Di seguito sono riportati alcuni esempi che è possibile usare nei test degli script di pre-distribuzione e post-distribuzione, con cui viene scritta l'ora corrente in un file di testo:  
    >   
    >  **Pre-distribuzione**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-distribuzione**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Distribuire gli aggiornamenti software nel gruppo di server e monitorare lo stato  
Gli aggiornamenti software vengono distribuiti alla raccolta del gruppo di server tramite il consueto processo di distribuzione. Dopo aver distribuito gli aggiornamenti software, è possibile monitorarne la distribuzione nella console di Configuration Manager.
1.  [Distribuire gli aggiornamenti software](manually-deploy-software-updates.md) nella raccolta del gruppo di server.   

2.  [Monitorare la distribuzione degli aggiornamenti software](monitor-software-updates.md). Oltre alle viste di monitoraggio standard per la distribuzione degli aggiornamenti software, viene visualizzato lo stato **In attesa del blocco** quando un client è in attesa del proprio turno per installare gli aggiornamenti software. Per altre informazioni, esaminare il file UpdatesDeployment.log.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Cancellare i blocchi di distribuzione per i computer di un gruppo di server  
Se un computer non può rilasciare un blocco di distribuzione, è possibile rilasciare manualmente tutti i blocchi di distribuzione del gruppo di server per la raccolta. Cancellare i blocchi solo quando una distribuzione è bloccata in fase di aggiornamento dei computer nella raccolta e sono presenti computer che non sono ancora conformi.  
1.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte di dispositivi** e quindi fare clic sulla raccolta per cancellare i blocchi di distribuzione.  

2.  Sulla scheda **Home**, nel gruppo **Distribuzione**, fare clic su **Cancellare i blocchi di distribuzione del gruppo di server**. Quando i client non sono riusciti a installare gli aggiornamenti software e impediscono ad altri client di installare i loro, i blocchi di distribuzione possono essere cancellati manualmente.  



<!--HONumber=Nov16_HO1-->

