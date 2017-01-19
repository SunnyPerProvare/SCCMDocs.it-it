---

title: Preparare la gestione degli aggiornamenti software | Microsoft Docs
description: "Per preparare la gestione degli aggiornamenti, completare queste attività per visualizzare i dati di valutazione di conformità nella console di System Center Configuration Manager."
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
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 5c34bd1ea108dffda10c30281fb9c97ba38ae1ae


---

# <a name="prepare-for-software-updates-management"></a>Preparare la gestione degli aggiornamenti software

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima che i dati di valutazione della conformità dell'aggiornamento software siano visualizzati nella console di System Center Configuration Manager e prima di poter distribuire gli aggiornamenti software nei computer client, è necessario completare i passaggi seguenti.

## <a name="step-1-install-a-software-update-point"></a>Passaggio 1: Installare un punto di aggiornamento software  
Il punto di aggiornamento software è necessario nel sito di amministrazione centrale e nei siti primari autonomi per abilitare la valutazione della conformità degli aggiornamenti software e per distribuire gli aggiornamenti software ai client. Il punto di aggiornamento software è facoltativo nei siti secondari. Per informazioni dettagliate, vedere[Installare un punto di aggiornamento software](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Passaggio 2: Sincronizzare gli aggiornamenti software
La sincronizzazione degli aggiornamenti software è il processo di recupero dei metadati degli aggiornamenti software che soddisfano i criteri configurati. Gli aggiornamenti software non vengono visualizzati nella console di Configuration Manager finché non verranno sincronizzati. Per informazioni dettagliate, vedere [Sincronizzare gli aggiornamenti software](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Passaggio 3: Configurare le classificazioni e i prodotti da sincronizzare
Eseguire questa configurazione nel sito di amministrazione centrale o nel sito primario autonomo. Dopo aver sincronizzato gli aggiornamenti software per la prima volta, Configuration Manager recupera un elenco aggiornato di classificazioni e prodotti. A questo punto, è possibile eseguire selezioni dalle nuove opzioni delle proprietà del componente punto di aggiornamento software. Dopo aver configurato le nuove classificazioni e i prodotti, ripetere il passaggio 2 per avviare la sincronizzazione degli aggiornamenti software per recuperare i metadati degli aggiornamenti software per i nuovi criteri. Per informazioni dettagliate, vedere [Configurare le classificazioni e i prodotti per la sincronizzazione](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Passaggio 4: Gestire le impostazioni per gli aggiornamenti software
Dopo aver sincronizzato gli aggiornamenti software, verificare le impostazioni client di Configuration Manager, le configurazioni dei criteri di gruppo e le impostazioni degli aggiornamenti software prima di distribuirle. Per informazioni dettagliate, vedere [Gestire le impostazioni per gli aggiornamenti software](manage-settings-for-software-updates.md).



<!--HONumber=Dec16_HO3-->


