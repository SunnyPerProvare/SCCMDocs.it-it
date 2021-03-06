---
title: Distribuire i profili di accesso alle risorse
titleSuffix: Configuration Manager
description: Informazioni su come distribuire profili certificato, Wi-Fi e VPN in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39ee7e69c2a24c3b5f169bd42f5e3d7acdc06de9
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76032677"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Distribuire i profili di accesso alle risorse in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver creato uno dei profili di accesso alle risorse seguenti, distribuirlo in una o più raccolte:

- [Wi-Fi](/configmgr/protect/deploy-use/create-wifi-profiles)
- [VPN](/configmgr/protect/deploy-use/create-vpn-profiles)
- [Certificato](/configmgr/protect/deploy-use/create-certificate-profiles)

Quando si distribuiscono questi profili, è necessario specificare la raccolta di destinazione e la frequenza con cui il client valuta la conformità del profilo.  

## <a name="deploy-a-profile"></a>Distribuire un profilo

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità** e quindi **Accesso risorse aziendali** e scegliere il nodo del profilo appropriato. Ad esempio, **Profili Wi-Fi**.

1. Nell'elenco dei profili selezionare il profilo da distribuire. Nella scheda **Home** della barra multifunzione selezionare quindi **Distribuisci** nel gruppo **Distribuzione**.  

1. Nella finestra di distribuzione del profilo specificare le informazioni seguenti:  

    - **Raccolta**: Selezionare la raccolta in cui si vuole distribuire il profilo.

    - **Genera un avviso**: abilitare questa opzione per configurare un avviso. Il sito genera questo avviso se la conformità del profilo è inferiore alla percentuale specificata in base alla data e all'ora specificate. È anche possibile specificare se si vuole che un avviso venga inviato a System Center Operations Manager.

    - **Ritardo casuale (ore)** : Per i profili certificato che contengono le impostazioni Simple Certificate Enrollment Protocol (SCEP) specificare una finestra di ritardo in modo da evitare un'elaborazione eccessiva nel servizio Registrazione dispositivi di rete (NDES). Il valore predefinito è `64` ore.  

    - **Specificare la pianificazione per la valutazione della conformità per questo profilo**: specificare la frequenza con cui il client valuta la conformità per il profilo. Selezionare **Pianificazione semplice** oppure **Pianificazione personalizzata** ed eseguire la configurazione. Per impostazione predefinita, la pianificazione semplice è ogni `12` ore.

1. Selezionare **OK** per chiudere la finestra e creare la distribuzione.

## <a name="delete-a-deployment"></a>Eliminare una distribuzione

Se si vuole eliminare una distribuzione, selezionarla nell'elenco. Nel riquadro dei dettagli passare alla scheda **Distribuzioni**. Selezionare la distribuzione e quindi nella scheda **Distribuzione** della barra multifunzione selezionare **Elimina**.

> [!IMPORTANT]
> Quando si rimuove una distribuzione del profilo VPN, Configuration Manager non rimuove il profilo VPN da Windows. Se si vuole rimuovere il profilo dai dispositivi, procedere manualmente.

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i profili Wi-Fi e VPN](/configmgr/protect/deploy-use/monitor-wifi-email-vpn-profiles)

[Monitorare i profili dei certificati](/configmgr/protect/deploy-use/monitor-certificate-profiles)
