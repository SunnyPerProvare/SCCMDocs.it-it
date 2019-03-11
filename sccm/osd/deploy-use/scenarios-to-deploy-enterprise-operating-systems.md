---
title: Scenari di distribuzione di sistemi operativi aziendali
titleSuffix: Configuration Manager
description: Informazioni su vari scenari per distribuire i sistemi operativi aziendali con Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d34c3d8dfa753934f03337d68e989a8bf8fcd7
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838702"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Scenari per distribuire sistemi operativi aziendali con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli scenari di distribuzione del sistema operativo seguenti sono disponibili in Configuration Manager:  

#### <a name="upgrade-windows-to-the-latest-version"></a>Aggiornare Windows alla versione più recente
Questo scenario aggiorna il sistema operativo nei computer che attualmente eseguono Windows 7, Windows 8.1 o Windows 10. Il processo di aggiornamento mantiene applicazioni, impostazioni e dati dell'utente nel computer. Non esistono dipendenze esterne, ad esempio Windows ADK. Il processo può essere più veloce e più flessibile rispetto alle distribuzioni tradizionali del sistema operativo.  

Per altre informazioni, vedere [Aggiornare Windows alla versione più recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot per dispositivi esistenti
<!--3607717, fka 1358333--> A partire dalla versione 1810, Windows Autopilot per i dispositivi esistenti è disponibile con Windows 10 versione 1809 o successiva. Questa funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la modalità definita dall'utente di Windows Autopilot usando una singola sequenza di attività di Configuration Manager.

Per altre informazioni, vedere [Windows Autopilot per dispositivi esistenti](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aggiornare un computer esistente con una nuova versione di Windows
Questo scenario esegue il partizionamento e la formattazione (cancellazione) di un computer esistente e installa un nuovo sistema operativo nel computer. Dopo aver installato il sistema operativo, è possibile eseguire la migrazione delle impostazioni e dei dati dell'utente.  

Per altre informazioni, vedere [Aggiornare un computer esistente con una nuova versione di Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Installare una nuova versione di Windows in un nuovo computer (bare metal)
Questo scenario installa un sistema operativo in un nuovo computer. Si tratta di una nuova installazione del sistema operativo e non include la migrazione dei dati dell'utente o delle impostazioni.  

Per altre informazioni, vedere [Installare una nuova versione di Windows in un nuovo computer (bare metal)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Sostituire un computer esistente e trasferire le impostazioni
Questo scenario installa un sistema operativo in un nuovo computer. Facoltativamente, è possibile eseguire la migrazione delle impostazioni e dei dati dell'utente dal vecchio al nuovo computer.  

Per altre informazioni, vedere [Sostituire un computer esistente e trasferire le impostazioni](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings)


