---
title: Escludere gli aggiornamenti dei client | Windows | System Center Configuration Manager
description: Informazioni su come evitare l&quot;aggiornamento di client Windows in System Center Configuration Manager.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 6451ce59e01254d96ca4aa9bbe07cde829fae9ce
ms.lasthandoff: 12/16/2016


---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Come evitare l'aggiornamento dei client per i computer Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, è possibile impedire che una raccolta di client installi automaticamente le versioni aggiornate. Questa funzione si applica sia all'aggiornamento automatico sia ad altri metodi, ad esempio all'aggiornamento basato sull'aggiornamento software, agli script di accesso e ai criteri di gruppo. Questa opzione può essere usata per una raccolta di computer che richiede particolare attenzione durante l'aggiornamento del client. I client che appartengono a una raccolta esclusa ignorano le richieste di aggiornamento del software client.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurare l'esclusione per gli aggiornamenti automatici

1. Nella console di Configuration Manager accedere a **Amministrazione** > **Configurazione del sito** > **Siti** e fare clic su **Impostazioni gerarchia**.

2. Fare clic sulla scheda **Aggiornamento client**.

3. Selezionare la casella di controllo **Exclude specified clients from upgrade** (Escludi dall'aggiornamento i client specificati) e, in Exclusion collection (Raccolta di esclusione) selezionare la raccolta da escludere. È possibile selezionare per l'esclusione solo una singola raccolta.

4.  Fare clic su **OK** per chiudere e salvare la configurazione. Dopo che i client avranno aggiornato i criteri, i client appartenenti alla raccolta esclusa non installeranno più automaticamente gli aggiornamenti per il software client. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](upgrade-clients-for-windows-computers.md).

![Impostazioni per l'esclusione dall'aggiornamento automatico](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Anche se l'interfaccia utente indica che i client non verranno aggiornati, esistono due metodi che è possibile usare per sostituire queste impostazioni. L'installazione push del client e l'installazione manuale del client consentono di sostituire questa configurazione. Per altre informazioni, vedere la sezione seguente.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Come aggiornare un client in una raccolta esclusa

Se una raccolta è configurata per l'esclusione, i membri di tale raccolta possono aggiornare il software client solo tramite uno dei due metodi che sostituiscono l'esclusione:
 - **Installazione push client**: è possibile usare l'installazione push del client per eseguire l'aggiornamento di un client che appartiene a una raccolta esclusa. Questa operazione è consentita in quanto richiesta dall'amministratore e permette di aggiornare i client lasciando invariata l'esclusione dell'intera raccolta.       

 - **Installazione client manuale**: è possibile aggiornare manualmente i client che appartengono a una raccolta esclusa usando la seguente opzione della riga di comando con ccmsetup: ***/ignoreskipupgrade***.

  Se si tenta di aggiornare manualmente un client che fa parte della raccolta esclusa senza usare questa opzione, il client non installa il nuovo software client. Per altre informazioni, vedere [Come installare manualmente i client di Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Per altre informazioni su questi metodi di installazione del client, vedere [Come distribuire i client nei computer Windows in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

