---
title: Attività di manutenzione
titleSuffix: Configuration Manager
description: Individuare le attività di manutenzione da eseguire per i siti e le gerarchie di Configuration Manager e il momento adatto in cui eseguirle.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26e17b190312dd1d3b1b73f5b1d6b91912938255
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501078"
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Attività di manutenzione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I siti e le gerarchie di System Center Configuration Manager richiedono manutenzione e monitoraggio regolari per offrire servizi in modo efficace e continuativo. Una regolare manutenzione garantisce che l'hardware, il software e il database di Configuration Manager continuino a funzionare in modo corretto ed efficace. Delle prestazioni ottimali riducono notevolmente il rischio di errore.  

 Per impostare gli avvisi e usare il sistema di stato per monitorare l'integrità di Configuration Manager, vedere [Usare gli avvisi e il sistema di stato per System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Attività di manutenzione](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> Attività di manutenzione  
 Una regolare manutenzione è importante per garantire il corretto funzionamento del sito. Conservare un registro di manutenzione per documentare le date della manutenzione, le persone che l'hanno effettuata ed eventuali commenti relativi alle attività svolte.  

### <a name="when-to-do-common-maintenance-tasks"></a>Quando svolgere attività comuni di manutenzione  
 È consigliabile effettuare la manutenzione del sito ogni giorno o una volta alla settimana. Alcune attività possono richiedere una pianificazione diversa. La manutenzione normale può includere sia attività di manutenzione incorporate che altre attività, ad esempio la manutenzione dell'account per mantenere la conformità con i criteri aziendali.  

 Usare le seguenti informazioni come guida per pianificare l'esecuzione di diverse attività di manutenzione. Usare questi elenchi come punto di partenza e aggiungere eventuali attività necessarie.  

**Attività quotidiane**   
Di seguito sono riportate le attività di manutenzione che si consiglia di svolgere ogni giorno:  

-   Verificare se le attività di manutenzione predefinite pianificate per l'esecuzione giornaliera vengono eseguite correttamente.  

-   Controllare lo stato del database di Configuration Manager.  

-   Controllare lo stato del server del sito.  

-   Verificare la presenza di backlog di file nelle cartelle della posta in arrivo del sistema del sito di Configuration Manager.  

-   Controllare lo stato del sistema del sito.  

-   Controllare i registri eventi del sistema operativo nei sistemi del sito.  

-   Controllare il registro degli errori di SQL Server sul computer del database del sito.  

-   Controllare le prestazioni del sistema.  

-   Controllare gli avvisi di Configuration Manager.  

**Attività settimanali**   
Di seguito sono riportate le attività di manutenzione che si consiglia di svolgere ogni settimana:  

-   Verificare se le attività di manutenzione predefinite pianificate per l'esecuzione settimanale vengono eseguite correttamente.  

-   Eliminare i file non necessari dai sistemi del sito.  

-   Produrre e distribuire i report per l'utente finale se necessario.  

-   Eseguire il backup dei registri eventi di sistema, sicurezza e applicazione e cancellarli.  

-   Controllare le dimensioni del database del sito e verificare che sul server di database del sito sia disponibile spazio su disco sufficiente, in modo che il database del sito possa aumentare.  

-   Eseguire la manutenzione del database di SQL Server nel database del sito in base al piano di manutenzione di SQL Server.  

-   Controllare lo spazio disponibile su disco in tutti i sistemi del sito.  

-   Eseguire l'utilità di deframmentazione disco in tutti i sistemi del sito.  

**Attività periodiche**   
Alcune attività che non richiedono la manutenzione giornaliera o settimanale sono importanti per garantire l'integrità del sito. Queste attività verificano inoltre che i piani di ripristino di emergenza e sicurezza siano aggiornati. Di seguito sono riportate le attività di manutenzione per cui si consiglia una pianificazione più periodica rispetto alle attività giornaliere o settimanali:  

-   cambiare gli account e le password, se necessario, secondo il piano di sicurezza.  

-   Rivedere il piano di manutenzione per verificare che le attività di manutenzione pianificate siano programmate in modo corretto ed efficiente in base alle impostazioni del sito configurate.  

-   Esaminare la struttura della gerarchia di Configuration Manager per verificare se sono necessarie modifiche.  

-   Controllare le prestazioni della rete per verificare che non siano state apportate modifiche che influiscono sulle operazioni del sito.  

-   Verificare che le impostazioni di Active Directory che interessano le operazioni del sito non siano state modificate. Verificare ad esempio che le subnet assegnate ai siti di Active Directory e usate come limiti per il sito di Configuration Manager non siano state modificate.  

-   Rivedere il piano di ripristino di emergenza per eventuali modifiche necessarie.  

-   Eseguire un ripristino del sito in base al piano di ripristino di emergenza in un lab di test usando una copia di backup del backup più recente creato dall'attività di manutenzione Backup server sito.

-   Controllare l'hardware per eventuali errori o per aggiornamenti hardware disponibili.  

-   Controllare l'integrità generale del sito.  

###  <a name="BKMK_UseMTs"></a> Mantenere l'integrità operativa del database del sito  
 Mentre il sito e la gerarchia di Configuration Manager eseguono le attività pianificate e configurate, i componenti del sito aggiungono continuamente dati al database di Configuration Manager. Man mano che la quantità di dati aumenta, le prestazioni del database e lo spazio libero di archiviazione nel database diminuiscono. È possibile impostare le attività di manutenzione del sito in modo da rimuovere dati obsoleti che non sono più necessari.  

 Configuration Manager include attività di manutenzione predefinite che è possibile usare per mantenere l'integrità del database di Configuration Manager. Per impostazione predefinita, non tutte le attività di manutenzione sono disponibili in ogni sito. Diverse attività sono abilitate e altre non lo sono e tutte supportano una pianificazione che può essere impostata dall'utente.  

 La maggior parte delle attività di manutenzione rimuovono i dati non aggiornati dal database di Configuration Manager. La riduzione delle dimensioni del database attraverso la rimozione di dati non necessari migliora le prestazioni e l'integrità del database stesso, aumentando al contempo l'efficienza del sito e della gerarchia. Altre attività, ad esempio **Ricompila indici**, consentono di mantenere l'efficienza del database. Altre attività, ad esempio **Backup server sito**, consentono di preparare il ripristino di emergenza.  

> [!IMPORTANT]  
>  Quando si pianifica la pianificazione di qualsiasi attività che elimina dati, tenere in considerazione l'utilizzo di quei dati nella gerarchia. Quando un'attività che elimina dati viene eseguita su un sito, le informazioni vengono rimosse dal database di Configuration Manager e questa modifica viene replicata su tutti i siti nella gerarchia. Questo ritardo può influire sulle altre attività che si basano su quei dati. Ad esempio, nel sito di amministrazione centrale è possibile impostare l'attività di individuazione in modo che venga eseguita una volta al mese per identificare i computer non client. Si prevede di installare il client di Configuration Manager in questi computer entro due settimane dall'individuazione degli stessi. Tuttavia, in un sito della gerarchia un amministratore imposta l'attività Elimina dati di individuazione obsoleti in modo che sia eseguita ogni sette giorni. Il risultato è che sette giorni dopo l'individuazione dei computer non client, questi vengono eliminati dal database di Configuration Manager. Tornare al sito di amministrazione centrale, preparare l'installazione push del client di Configuration Manager in questi nuovi computer il giorno 10. Tuttavia, poiché l'attività Elimina dati di individuazione obsoleti è stata eseguita di recente e ha eliminato i dati vecchi di sette giorni o più, i computer individuati di recente non sono più disponibili nel database.  

Dopo l'installazione di un sito di Configuration Manager, rivedere le attività di manutenzione disponibili e abilitare quelle richieste dalle operazioni. Rivedere la pianificazione predefinita di ogni attività e, quando necessario, impostare la pianificazione per definire l'attività di manutenzione in base alla gerarchia e all'ambiente. Anche se la pianificazione predefinita di ogni attività deve adattarsi alla maggior parte degli ambienti, monitorare le prestazioni dei siti e del database e prevedere l'ottimizzazione delle attività per aumentare l'efficienza della distribuzione. Pianificare la revisione periodica delle prestazioni del sito e del database e riconfigurare le attività di manutenzione e le relative pianificazioni per mantenere tale efficienza.  

#### <a name="set-up-maintenance-tasks"></a>Impostare le attività di manutenzione  
 Ogni sito di Configuration Manager supporta attività di manutenzione che consentono di gestire l'efficienza operativa del database del sito. Per impostazione predefinita, alcune attività di manutenzione sono abilitate in ogni sito e tutte le attività supportano pianificazioni indipendenti. Le attività di manutenzione vengono impostate singolarmente per ogni sito e sono valide per il database in tale sito. Tuttavia, alcune attività, ad esempio **Elimina dati di individuazione obsoleti**, influiscono sulle informazioni disponibili in tutti i siti di una gerarchia.  

 Solo le attività di manutenzione che è possibile impostare in un sito vengono visualizzate nella console di Configuration Manager. Per un elenco completo delle attività di manutenzione di ogni tipo di sito, vedere [Informazioni di riferimento per le attività di manutenzione per System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Usare la procedura seguente per specificare le impostazioni comuni delle attività di manutenzione.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Per impostare le attività di manutenzione per Configuration Manager  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** >**Siti**.  

2.  Scegliere il sito che contiene l'attività di manutenzione da impostare.  

3.  Nel gruppo **Impostazioni** della scheda **Home** scegliere **Manutenzione del sito** e quindi selezionare l'attività di manutenzione da impostare.  

    > [!TIP]  
    >  Vengono visualizzate solo le attività disponibili nel sito selezionato.  

4.  Per impostare l'attività, scegliere **Modifica**, verificare che la casella di controllo **Abilita questa attività** sia selezionata e impostare una pianificazione per l'esecuzione dell'attività. Se l'attività elimina anche i dati obsoleti, impostare il periodo di validità dei dati che verranno eliminati dal database quando viene eseguita l'attività. Scegliere **OK** per chiudere le **Proprietà** dell'attività.  

    > [!NOTE]  
    >  Per **Elimina messaggi di stato obsoleti**, impostare il periodo di validità dei dati da eliminare quando si configurano le regole di filtro dello stato.  

5.  Per abilitare o disabilitare l'attività senza modificarne le proprietà, scegliere il pulsante **Abilita** o **Disabilita**. Il pulsante etichetta cambia a seconda della configurazione corrente dell'attività.  

6.  Dopo aver configurato le attività di manutenzione, scegliere **OK** per terminare la procedura.
