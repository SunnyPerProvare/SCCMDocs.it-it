---
title: Monitorare il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Monitorare i client e il traffico di rete attraverso il gateway di gestione di cloud.
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6b52a97432dd85987dd98f11b0a048b1f730db84
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140678"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorare il gateway di gestione cloud in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Se il gateway di gestione cloud (CMG) è in esecuzione e i client si connettono attraverso di esso, è possibile monitorare i client e il traffico di rete per controllare le prestazioni del servizio.



## <a name="monitor-clients"></a>Monitorare i client

I client connessi attraverso il CMG vengono visualizzati nella console di Configuration Manager allo stesso modo dei client locali. Per altre informazioni, vedere [Come monitorare i client in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Monitorare il traffico nella console

Monitorare il traffico attraverso il CMG usando la console di Configuration Manager:

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Cloud Management Gateway**.  

2. Selezionare il CMG nel riquadro dell'elenco.  

3. Visualizzare le informazioni sul traffico nel riquadro dei dettagli per il punto di connessione del CMG e per i ruoli del sistema del sito ai quali è connesso.  



## <a name="set-up-outbound-traffic-alerts"></a>Configurare gli avvisi del traffico in uscita

Gli avvisi del traffico in uscita consentono di sapere quando il traffico di rete sta per raggiungere un livello di soglia di 14 giorni. Quando si crea il CMG, è possibile impostare avvisi relativi al traffico. Se questa operazione non è stata eseguita, è possibile configurare gli avvisi anche dopo che il servizio è in esecuzione. È possibile regolare le impostazioni degli avvisi in qualsiasi momento.

1. Accedere all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Cloud Management Gateway**.  

2. Selezionare il CMG nel riquadro elenco e quindi selezionare **Proprietà** nella barra multifunzione.  

3. Passare alla scheda **Avvisi** per abilitare la soglia e gli avvisi. Specificare la soglia di 14 giorni per i dati in gigabyte (GB). Specificare anche le percentuali della soglia in corrispondenza delle quali devono essere generati i diversi livelli di avviso.  

4. Al termine selezionare **OK**.  



## <a name="monitor-logs"></a>Monitorare i log

Il CMG genera voci in diversi file di log. Per altre informazioni, vedere [Log in Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="cloud-management-dashboard"></a>Dashboard di gestione del cloud
<!--1358461--> A partire dalla versione 1806, il dashboard di gestione del cloud offre una visualizzazione centralizzata per l'uso del CMG. Dopo l'onboarding del sito nei [servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la gestione del cloud, il dashboard visualizza anche dati sugli utenti e i dispositivi del cloud.  

Lo screenshot seguente illustra una parte del dashboard di gestione del cloud che mostra due dei riquadri disponibili:  
![Riquadri del dashboard di gestione del cloud: traffico CMG e Client online correnti](media/1358461-cmg-dashboard.png)

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Selezionare il nodo **Gestione cloud** e visualizzare i riquadri del dashboard.  



## <a name="connection-analyzer"></a>Analizzatore della connessione

A partire dalla versione 1806, usare l'analizzatore della connessione CMG per verifiche in tempo reale a supporto della risoluzione dei problemi. L'utilità inclusa nella console controlla lo stato corrente del servizio e il canale di comunicazione dal punto di connessione CMG a tutti i punti di gestione che consentono il traffico CMG.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Gateway di gestione cloud**.  

2. Selezionare l'istanza di CMG di destinazione e quindi selezionare **Analizzatore della connessione** sulla barra multifunzione.  

3. Nella finestra dell'analizzatore della connessione CMG selezionare una delle opzioni seguenti per l'autenticazione nel servizio:  

     1. **Utente di Azure AD**: usare questa opzione per simulare la comunicazione di un'identità utente basata sul cloud che ha eseguito l'accesso a un dispositivo Windows 10 aggiunto ad Azure AD. Fare clic su **Accedi** per immettere le credenziali per questo account utente di Azure AD in modo sicuro.  

     2. **Certificato client**: usare questa opzione per simulare la comunicazione di un client di Configuration Manager con un [certificato di autenticazione client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate).  

4. Selezionare **Avvia** per avviare l'analisi. La finestra dell'analizzatore visualizza i risultati. Selezionare una voce per visualizzare ulteriori dettagli nel campo Descrizione.  

