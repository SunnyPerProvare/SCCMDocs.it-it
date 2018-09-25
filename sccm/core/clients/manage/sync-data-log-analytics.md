---
title: Sincronizzare i dati con Log Analytics
titleSuffix: Configuration Manager
description: Sincronizzare i dati da Configuration Manager ad Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0fd4c36ed03f0e0b158fe637a045553dab31ade
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995358"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Sincronizzare i dati da Configuration Manager ad Azure Log Analytics

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1258052--> Usare la **Procedura guidata per i servizi di Azure** per configurare una connessione da Configuration Manager al servizio cloud Azure Log Analytics. Questa connessione sincronizza i dati della raccolta dei dispositivi con Log Analytics. 

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> A partire da Configuration Manager 1802, il connettore Log Analytics non è più una funzionalità di versione non definitiva. Per altre informazioni, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/pre-release-features).



## <a name="prerequisites-for-the-log-analytics-connector"></a>Prerequisiti per il connettore Log Analytics

> [!Note]  
> Questo articolo si riferisce al *connettore Log Analytics*, che era in precedenza denominato *OMS Connector*. Non esistono differenze funzionali. Per altre informazioni, vedere [Gestione di Azure - Monitoraggio](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Prima di installare il connettore Log Analytics in Configuration Manager, fornire a Configuration Manager le autorizzazioni. Concedere l'*accesso di tipo Collaboratore* al *gruppo di risorse* di Azure che contiene l'area di lavoro di Log Analytics. Per altre informazioni, vedere [Fornire a Configuration Manager le autorizzazioni per Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Installare il connettore Log Analytics nel computer che ospita il [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) in modalità online.  

- Installare Microsoft Monitoring Agent per Log Analytics nel punto di connessione del servizio con il connettore. Configurare questo agente e il connettore per usare la stessa area di lavoro di Log Analytics. Per altre informazioni sull'installazione di questo agente, vedere [Scaricare e installare l'agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- Dopo aver installato il connettore e l'agente, configurare Log Analytics per l'uso dei dati di Configuration Manager. Per altre informazioni, vedere [Importare le raccolte di Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## <a name="configure-the-connection-to-log-analytics"></a>Configurare la connessione a Log Analytics

Usare la **Procedura guidata per i servizi di Azure** per configurare una connessione da Configuration Manager al servizio cloud Azure Log Analytics. Per altre informazioni e dettagli relativi a questo processo, vedere [Configurare i servizi di Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Nella procedura guidata selezionare l'opzione **OMS Connector**. 

> [!Note]  
> Questo articolo si riferisce al *connettore Log Analytics*, che era in precedenza denominato *OMS Connector*. Non esistono differenze funzionali. Per altre informazioni, vedere [Gestione di Azure - Monitoraggio](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

Se tutte le altre procedure sono state eseguite correttamente, le informazioni della schermata **Configurazione connessione** vengono automaticamente visualizzate dopo aver importato l'app Web. Le informazioni relative alle impostazioni di connessione vengono visualizzate in **Sottoscrizione Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.

La procedura guidata esegue la connessione al servizio Log Analytics usando le informazioni immesse dall'utente. Selezionare le raccolte di dispositivi da sincronizzare con il servizio cloud e quindi fare clic su **Aggiungi**.


## <a name="verify-the-connector-properties"></a>Verificare le proprietà del connettore

Dopo aver collegato Configuration Manager a Log Analytics, visualizzare le proprietà della connessione per aggiungere o rimuovere raccolte. 

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**.  

2. Selezionare la connessione a Log Analytics. Nella barra multifunzione selezionare **Proprietà**.  

La pagina delle proprietà ha le due schede seguenti:  

#### <a name="azure-active-directory"></a>Azure Active Directory
Questa scheda mostra gli attributi seguenti: 
- **Tenant**  
- **ID client**  
- **Scadenza della chiave privata del client**  

Verificare anche quando scadrà la chiave privata del client.

#### <a name="connection-properties"></a>Proprietà connessione
Questa scheda mostra gli attributi seguenti: 
- **Sottoscrizione di Azure**  
- **Gruppo di risorse di Azure**  
- **Area di lavoro di Log Analytics**  

Mostra anche l'elenco **Raccolte di dispositivi**. Usare i pulsanti **Aggiungi** e **Rimuovi** per modificare le raccolte da sincronizzare.
