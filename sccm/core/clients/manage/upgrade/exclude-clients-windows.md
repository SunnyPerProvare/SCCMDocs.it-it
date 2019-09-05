---
title: Evitare l'aggiornamento di client per Windows
titleSuffix: Configuration Manager
description: Informazioni su come evitare l'aggiornamento di client Windows in Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a16bc859006b0253459259d354a68e2ff1dec83
ms.sourcegitcommit: 2d38de4846ea47a03cc884cbd3df27db48f64a6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/28/2019
ms.locfileid: "70110146"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Come evitare l'aggiornamento di client in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile impedire che una raccolta di client installi automaticamente le versioni di client aggiornate. Questa opzione può essere usata per una raccolta di computer che richiede particolare attenzione durante l'aggiornamento del client. I client che appartengono a una raccolta esclusa ignorano le richieste di aggiornamento del software client.

Questa esclusione si applica ai metodi seguenti:

- Aggiornamento automatico
- Aggiornamento basato sull'aggiornamento software
- Script di accesso
- Criteri di gruppo

> [!NOTE]
> Anche se l'interfaccia utente indica che i client non verranno aggiornati, esistono due metodi che è possibile usare per sostituire queste impostazioni. Usare l'installazione push del client o l'installazione manuale del client per sostituire questa configurazione. Per altre informazioni, vedere [Come aggiornare un client escluso](#bkmk_override).

## <a name="bkmk_exclude"></a> Configurare l'esclusione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Configurazione del sito**, selezionare il nodo **Siti** e quindi selezionare **Impostazioni gerarchia** nella barra multifunzione.

2. Passare alla scheda **Aggiornamento client**.

3. Selezionare l'opzione **Escludi i client specificati dall'aggiornamento**. Selezionare quindi la **Raccolta di esclusioni** da escludere. È possibile selezionare per l'esclusione solo una singola raccolta.

4. Selezionare **OK** per chiudere e salvare la configurazione.

![Impostazioni per l'esclusione dall'aggiornamento automatico](media/automatic_upgrade_exclusion.png)

Dopo l'aggiornamento dei criteri dei client nella raccolta esclusa, gli aggiornamenti client non vengono più installati automaticamente. Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).

> [!NOTE]
> I client esclusi scaricano ed eseguono comunque Ccmsetup, ma non saranno aggiornati.

Quando si rimuove un client dalla raccolta di esclusione, questo non viene aggiornato automaticamente fino al successivo ciclo di aggiornamento automatico.

## <a name="bkmk_override"></a> Come aggiornare un client escluso

Se un dispositivo è membro di una raccolta esclusa dall'aggiornamento, è comunque possibile aggiornare il client usando uno dei metodi seguenti:

- **Installazione push client**: Ccmsetup consente l'installazione push client perché è la finalità diretta. Questo metodo consente di aggiornare un client senza rimuoverlo dalla raccolta o rimuovendo l'intera raccolta dall'esclusione.

- **Installazione client manuale**: Aggiornare manualmente un client escluso usando il seguente parametro della riga di comando Ccmsetup: **/IgnoreSkipUpgrade**

    Se si tenta di aggiornare manualmente un client che fa parte della raccolta esclusa senza usare questo parametro, il client non viene aggiornato. Per altre informazioni, vedere [Come installare manualmente i client di Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

## <a name="see-also"></a>Vedere anche

- [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients)

- [Come distribuire i client nei computer Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)

- [Client di interoperabilità estesa](/sccm/core/understand/interoperability-client)
