---
title: "Attività di manutenzione | System Center Configuration Manager"
description: "Individuare le attività di manutenzione da eseguire per i siti e le gerarchie di Configuration Manager e il momento adatto in cui eseguirle."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ac47f1b88a89a42bb51b87b36147b731e37a5824


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Attività di manutenzione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I siti e le gerarchie di System Center Configuration Manager richiedono manutenzione e monitoraggio regolari per offrire servizi in modo efficace e continuativo. Una regolare manutenzione garantisce che l'hardware, il software e il database di Configuration Manager continuino a funzionare in modo corretto ed efficace. Delle prestazioni ottimali riducono notevolmente il rischio di errore.  

 Per configurare gli avvisi e usare il sistema di stato per monitorare l'integrità di Configuration Manager, vedere [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md) (Usare gli avvisi e il sistema di stato per System Center Configuration Manager).  

-   [Attività di manutenzione](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> Attività di manutenzione  
 Eseguire una regolare manutenzione è importante per garantire corrette operazioni del sito. Mantenere un registro di manutenzione per documentare le date in cui è stata effettuata la manutenzione, da chi è stata effettuata ed eventuali commenti a essa relativi sull'attività eseguita.  

### <a name="when-to-perform-common-maintenance-tasks"></a>Quando eseguire attività comuni di manutenzione  
 Per eseguire la manutenzione del sito, prendere in considerazione di eseguire una manutenzione regolare con una pianificazione quotidiana, settimanale e, per alcune attività, più periodica. Una manutenzione comune può includere sia attività di manutenzione incorporate che altre attività, come la manutenzione dell'account per mantenere la conformità con le politiche aziendali.  

 Usare le seguenti informazioni come guida per pianificare quando eseguire le diverse attività di manutenzione. Usare questi elenchi come punto di partenza e aggiungere eventuali attività aggiuntive che potrebbe essere necessarie.  

**Attività quotidiane**   
Quelle che seguono sono le attività di manutenzione che si consiglia di eseguire su base giornaliera:  

-   Verificare che le attività di manutenzione predefinite che sono pianificate per l'esecuzione giornaliera vengano eseguite correttamente  

-   Controllare lo stato del database di Configuration Manager  

-   Controllare lo stato del server del sito  

-   Cercare i backlog di file nelle cartelle di posta in arrivo di sistema del sito di Configuration Manager  

-   Controllare lo stato del sistema del sito  

-   Controllare i registri eventi del sistema operativo nei sistemi del sito  

-   Controllare il registro degli errori di SQL Server sul computer del database del sito  

-   Controllare le prestazioni del sistema  

-   Controllare gli avvisi di Configuration Manager  

**Attività settimanali**   
Quelle che seguono sono le attività di manutenzione che si consiglia di eseguire su base settimanale:  

-   verificare che le attività di manutenzione predefinite pianificate per l'esecuzione settimanale vengano eseguite correttamente.  

-   Eliminare i file non necessari dai sistemi del sito  

-   Produrre e distribuire i report per l'utente finale, se necessario  

-   Eseguire il backup dei registri eventi di sistema, sicurezza e applicazione e cancellarli  

-   Controllare le dimensioni del database del sito e verificare che sul server di database del sito sia disponibile spazio su disco sufficiente, in modo che il database del sito possa aumentare  

-   Eseguire la manutenzione del database di SQL Server nel database del sito in base al piano di manutenzione di SQL Server  

-   Controllare lo spazio disponibile su disco in tutti i sistemi del sito  

-   Eseguire l'utilità di deframmentazione disco in tutti i sistemi del sito  

**Attività periodiche**   
Alcune attività non devono essere eseguite durante la manutenzione giornaliera o settimanale, ma sono comunque importanti per garantire un'integrità del sistema nel suo complesso e che i piani di sicurezza e di ripristino di emergenza siano aggiornati. Quelle che seguono sono le attività di manutenzione che si consiglia di eseguire su una base più periodica rispetto alle attività giornaliere o settimanali:  

-   Cambiare gli account e le password, se necessario, in base al piano di sicurezza  

-   Rivedere il piano di manutenzione per verificare che le attività di manutenzione pianificate vengono programmate in modo corretto ed efficiente in base alle impostazioni del sito configurate  

-   Rivedere la struttura della gerarchia di Configuration Manager per eventuali modifiche necessarie  

-   Controllare le prestazioni della rete per garantire che non siano state apportate modifiche che influenzino le operazioni del sito  

-   Verificare che le impostazioni di Active Directory che interessano le operazioni del sito non siano state modificate. Ad esempio, verificare che le subnet assegnate ai siti di Active Directory che sono usati come limiti per il sito di Configuration Manager non siano state modificate  

-   Rivedere il piano di ripristino di emergenza per eventuali modifiche necessarie  

-   Eseguire un ripristino del sito in base al piano di ripristino di emergenza in un lab di test usando una copia di backup del backup più recente creato dall'attività di manutenzione Backup server sito  

-   Controllare l'hardware per eventuali errori o per aggiornamenti hardware disponibili  

-   Controllare l'integrità generale del sito  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Mantenere l'integrità operativa del database del sito  
 Mentre il sito e la gerarchia di Configuration Manager eseguono le attività pianificate e configurate, i componenti del sito aggiungono continuamente dati al database di Configuration Manager. Man mano che la quantità di dati aumenta, le prestazioni del database e lo spazio libero di archiviazione nel database diminuiscono. È possibile configurare le attività di manutenzione del sito per rimuovere dati obsoleti che non sono più necessari.  

 Configuration Manager include attività di manutenzione predefinite che è possibile usare per mantenere l'integrità del database di Configuration Manager. Non tutte le attività di manutenzione sono disponibili in ogni sito per impostazione predefinita, alcune sono abilitate altre no, mentre tutte supportano una pianificazione da configurare per l'esecuzione.  

 La maggior parte delle attività di manutenzione rimuovono i dati non aggiornati dal database di Configuration Manager. La riduzione delle dimensioni del database attraverso la rimozione di dati non necessari migliora le prestazioni e l'integrità del database stesso, aumentando al contempo l'efficienza del sito e della gerarchia. Altre attività, come **Ricompila indici**, consentono di mantenere l'efficienza del database, mentre altre, come l'attività **Backup server sito** , di preparare il ripristino di emergenza.  

> [!IMPORTANT]  
>  Quando si pianifica la pianificazione di qualsiasi attività che elimina dati, tenere in considerazione l'utilizzo di quei dati nella gerarchia. Quando un'attività che elimina dati viene eseguita su un sito, le informazioni vengono rimosse dal database di Configuration Manager e questa modifica viene replicata su tutti i siti nella gerarchia. Questo può influire sulle altre attività che si basano su quei dati. Ad esempio, nel sito di amministrazione centrale è possibile configurare l'esecuzione dell'individuazione una volta al mese per identificare i computer non client e pianificare l'installazione del client di Configuration Manager su questi computer entro due settimane dalla loro individuazione. Tuttavia, in un sito della gerarchia, un amministratore configura l'esecuzione dell'attività Elimina dati di individuazione obsoleti ogni sette giorni con il risultato che sette giorni dopo vengono individuati i computer non client e questi vengono eliminati dal database di Configuration Manager. Tornare al sito di amministrazione centrale, preparare l'installazione push del client di Configuration Manager in questi nuovi computer il giorno 10. Tuttavia, poiché l'attività Elimina dati di individuazione obsoleti è stata eseguita di recente e ha eliminato i dati vecchi di sette giorni o più, i computer individuati di recente non sono più disponibili nel database.  

Dopo l'installazione di un sito di Configuration Manager, rivedere le attività di manutenzione disponibili e abilitare quelle richieste dalle operazioni. Rivedere la pianificazione predefinita di ogni attività e, quando necessario, modificare la pianificazione per definire l'attività di manutenzione in base alla gerarchia e all'ambiente. Nonostante la pianificazione predefinita di ogni attività dovrebbe adattarsi alla maggior parte degli ambienti, monitorare le prestazioni dei siti e del database e prevedere la definizione delle attività per aumentare l'efficienza della distribuzione. Pianificare di rivedere periodicamente le prestazioni del sito e del database e di riconfigurare le attività di manutenzione e le relative pianificazioni per mantenere tale efficienza.  

#### <a name="configure-maintenance-tasks"></a>Configurare le finestre di manutenzione  
 Ogni sito di Configuration Manager supporta attività di manutenzione che consentono di gestire l'efficienza operativa del database del sito. Per impostazione predefinita, alcune attività di manutenzione sono abilitate in ogni sito e tutte le attività supportano pianificazioni indipendenti. Attività di manutenzione vengono configurate singolarmente per ogni sito e applicare al database in tale sito. Tuttavia, alcune attività, ad esempio **Elimina dati di individuazione obsoleti**, influiscono sulle informazioni disponibili in tutti i siti in una gerarchia.  

 Vengono visualizzate solo le attività di manutenzione che è possibile configurare in un sito della console di Configuration Manager. Per un elenco completo delle attività di manutenzione di ogni tipo di sito, vedere [Reference for maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md) (Riferimento per le attività di manutenzione per System Center Configuration Manager)  

 Utilizzare la procedura seguente per configurare le impostazioni comuni delle attività di manutenzione.  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>Per configurare le attività di manutenzione per Configuration Manager  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** >**Siti**.  

2.  Selezionare il sito che contiene l'attività di manutenzione che si desidera configurare.  

3.  Nel **Home** nella scheda il **impostazioni** di gruppo, fare clic su **manutenzione del sito**, e quindi selezionare l'attività di manutenzione che si desidera configurare.  

    > [!TIP]  
    >  Vengono visualizzate solo le attività disponibili nel sito selezionato.  

4.  Per configurare l'attività, fare clic su **Modifica**, assicurarsi di **Abilita questa attività** casella di controllo è selezionata e configurare una pianificazione per quando viene eseguita l'attività. Se l'attività Elimina anche i dati obsoleti, configurare la validità dei dati che verranno eliminati dal database quando viene eseguita l'attività. Fare clic su **OK** per chiudere l'attività **proprietà**.  

    > [!NOTE]  
    >  Per **eliminare i messaggi di stato obsoleti**, si configura la validità dei dati da eliminare quando si configurano le regole di filtro dello stato.  

5.  Per abilitare o disabilitare l'attività senza modificare le proprietà dell'attività, fare clic su di **abilitare** o **disattivare** pulsante. Il pulsante etichetta cambia a seconda della configurazione corrente dell'attività.  

6.  Dopo aver configurato le attività di manutenzione, fare clic su **OK** per completare la procedura.



<!--HONumber=Nov16_HO1-->


