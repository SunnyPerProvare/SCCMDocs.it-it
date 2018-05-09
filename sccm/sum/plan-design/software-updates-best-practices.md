---
title: Procedure consigliate per gli aggiornamenti software
titleSuffix: Configuration Manager
description: Usare queste procedure consigliate per gli aggiornamenti software in System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/06/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 0604c75aedfea5d82bd7d274c4a43edccb497f1e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Procedure consigliate per gli aggiornamenti software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento illustra le procedure consigliate per gli aggiornamenti software in System Center Configuration Manager. Le informazioni sono suddivise in procedure ottimali per l'installazione iniziale e procedure ottimali per le operazioni in corso.  

## <a name="installation-best-practices"></a>Procedure ottimali per l'installazione  
 Usare le procedure consigliate seguenti durante l'installazione degli aggiornamenti software in Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Utilizzare un database WSUS condiviso per punti di aggiornamento software  
 In caso di installazione di più di un punto di aggiornamento software in un sito primario, utilizzare lo stesso database WSUS per ciascun punto di aggiornamento software nella stessa foresta Active Directory. La condivisione dello stesso database consente di ridurre notevolmente l'impatto sulle prestazioni di rete e del client provocato dal passaggio dei client a un nuovo punto di aggiornamento software. Quando un client esegue il passaggio a un nuovo punto di aggiornamento software che condivide un database con il punto di aggiornamento software precedente, viene comunque eseguita una scansione differenziale. Se il server WSUS disponesse di un proprio database, tuttavia, le dimensioni di tale scansione sarebbero ampiamente superiori.  

> [!IMPORTANT]  
>  È necessario anche condividere le cartelle di contenuti WSUS locali quando si usa un database WSUS condiviso per i punti di aggiornamento software.  

 Per altre informazioni sul passaggio tra punti di aggiornamento software, vedere la sezione [Software Update Point Switching](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) (Passaggio tra punti di aggiornamento software) nell'argomento [Plan for software updates in Configuration Manager](../../sum/plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti software in Configuration Manager).  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Se Configuration Manager e WSUS utilizzano lo stesso SQL Server, configurare uno dei due per l'utilizzo di un'istanza denominata e l'altro per l'utilizzo dell'istanza predefinita di SQL Server  
 Se i database WSUS e Configuration Manager usano lo stesso SQL Server e condividono la stessa istanza di SQL Server, non è facile determinare l'uso delle risorse tra le due applicazioni. Se per Configuration Manager e WSUS si usano due istanze di SQL Server diverse, è più semplice risolvere e diagnosticare eventuali problemi relativi all'uso delle risorse che possono verificarsi in ogni applicazione.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Per l'installazione di WSUS specificare l'impostazione "Archivia aggiornamenti in locale"  
 Quando si installa WSUS, selezionare l'impostazione **Archivia aggiornamenti in locale**. Se questa impostazione è selezionata, le condizioni di licenza associate agli aggiornamenti software vengono scaricate durante il processo di sincronizzazione e archiviate nell'unità disco rigido locale per il server WSUS. Se questa impostazione non è selezionata, i computer client potrebbero non essere in grado di esaminare la conformità degli aggiornamenti software per gli aggiornamenti software che dispongono delle condizioni di licenza. Quando viene installato il punto di aggiornamento software, Gestione sincronizzazione WSUS verifica che l'impostazione sia attivata ogni 60 minuti, per impostazione predefinita.  

## <a name="operational-best-practices"></a>Procedure operative ottimali  
 Utilizzare le seguenti procedure ottimali durante l'utilizzo degli aggiornamenti software:  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Limitare gli aggiornamenti software a 1000 in un'unica distribuzione degli aggiornamenti software  
 È necessario limitare il numero di aggiornamenti software a 1000 per ogni distribuzione degli aggiornamenti software. Quando viene creata una regola di distribuzione automatica, verificare che i criteri specificati non prevedano più di 1000 aggiornamenti software. Durante la distribuzione manuale degli aggiornamenti software, non selezionare più di 1000 aggiornamenti per la distribuzione.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Creare un nuovo gruppo di aggiornamento software ogni volta che viene eseguita una regola di distribuzione automatica per il "Patch Tuesday" e per la distribuzione generale  
 Per una distribuzione degli aggiornamenti software è previsto un limite di 1000 aggiornamenti software. Durante la creazione di una regola di distribuzione automatica è necessario specificare se utilizzare un gruppo di aggiornamento esistente o se crearne uno nuovo ogni volta che viene eseguita la regola. Quando vengono specificati i criteri in una regola di distribuzione automatica che comporta più aggiornamenti software e tale regola viene eseguita in base a una pianificazione ricorrente, è necessario specificare la creazione di un nuovo gruppo di aggiornamento software ogni volta che viene eseguita la regola. In questo modo la distribuzione non oltrepasserà il limite di 1000 aggiornamenti software per ogni distribuzione.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Utilizzare un gruppo di aggiornamento software esistente per le regole di distribuzione automatica relative agli aggiornamenti delle definizioni di Endpoint Protection  
 Se si utilizza regolarmente una regola di distribuzione automatica per la distribuzione degli aggiornamenti delle definizioni di Endpoint Protection è consigliabile utilizzare sempre un gruppo di aggiornamento software esistente. In caso contrario, nel tempo potrebbero essere potenzialmente creati centinaia di gruppi di aggiornamento software. In genere, gli autori degli aggiornamenti delle definizioni fanno in modo che tali aggiornamenti scadano nel momento in cui vengono sostituiti da quattro aggiornamenti più recenti. Il gruppo di aggiornamento software creato dalla regola di distribuzione automatica, pertanto, non conterrà mai più di quattro aggiornamenti delle definizioni per l'autore: uno attivo e tre sostituiti.  

## <a name="see-also"></a>Vedere anche  
 [Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti software in System Center Configuration Manager)
