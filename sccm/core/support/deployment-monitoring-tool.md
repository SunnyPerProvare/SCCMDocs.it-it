---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Usare Deployment Monitoring Tool per risolvere i problemi di distribuzione del software in un client di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 67a052fffcaf6ad105f417649aa9f3826922ce80
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385892"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*Si applica a: System Center Configuration Manager (Current Branch)*

Deployment Monitoring Tool è uno [strumento di Configuration Manager](/sccm/core/support/tools). È un'interfaccia utente grafica progettata per assistere nella risoluzione dei problemi dell'applicazione, negli aggiornamenti software e nelle distribuzioni della linea di base di configurazione in un client di Configuration Manager. Lo strumento è di sola lettura perché non modifica alcuno stato nel client. È possibile usarlo in modo sicuro per diagnosticare gli scenari di distribuzione comuni.


## <a name="features"></a>Caratteristiche

- Eseguirlo come amministratore per risolvere i problemi di distribuzione in un client locale.  

- Risolvere i problemi di distribuzione in un client remoto. Avviare lo strumento e connettersi a un computer remoto come amministratore.  

- Esportare in formato XML tutti i dati raccolti nello strumento. Condividere il file XML con altri utenti e usarlo come piattaforma comune per discutere della risoluzione dei problemi di distribuzione.  

- Importare i dati esportati precedentemente in un computer diverso e usarlo per eseguire lo strumento in modalità offline.   


## <a name="usage"></a>Utilizzo

Deployment Monitoring Tool supporta solo l'interfaccia utente grafica. Per avviare lo strumento, eseguire **DeploymentMonitoringTool.exe** come amministratore. Sono disponibili tre viste:  

- **Proprietà client**: un elenco di attributi utili relativi al dispositivo e al client di Configuration Manager. Questa vista è quella predefinita.   

- **Distribuzioni**: consente di visualizzare tutte le distribuzioni di destinazione correnti. Selezionare una distribuzione nel riquadro dei risultati per visualizzare altre informazioni nel riquadro dei dettagli.  

- **Tutti gli aggiornamenti**: visualizza tutti gli aggiornamenti software e il relativo stato.  

Per copiare i dati in qualsiasi visualizzazione, selezionare una cella e premere **CTRL** + **C**.


### <a name="actions-menu"></a>Menu Azioni

Nel menu **Azioni** sono disponibili le seguenti azioni:  

- **Connect to remote machine** (Connettersi al computer remoto): selezionare un computer a cui connettersi. Se non si specifica un nome utente e password, usa le credenziali correnti. Fare clic su **Salva** per connettersi a un computer remoto.  

- **Esporta dati**: selezionare il file su cui scrivere i dati e fare clic su **Salva**. Usare il file XML esportato per la risoluzione remota dei problemi in un computer diverso.  

- **Importa dati**: selezionare un file da importare nello strumento.  

- **Visualizza registro**: consente di aprire un file di log associato, a seconda della visualizzazione:  
    - Proprietà client: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Distribuzioni: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Tutti gli aggiornamenti: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Vedere anche

- [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications)
- [Distribuire gli aggiornamenti software](/sccm/sum/deploy-use/deploy-software-updates)
- [Distribuire linee di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines)
