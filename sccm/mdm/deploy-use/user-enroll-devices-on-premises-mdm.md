---
title: Modalità di registrazione dei dispositivi da parte degli utenti
titleSuffix: Configuration Manager
description: Informazioni su come gli utenti registrano i dispositivi con la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e2d1eb0476eec975a458222134eb33ab8469cbb6
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76035218"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Come gli utenti registrano i dispositivi con MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager gestione di dispositivi mobili (MDM) locale, gli utenti possono registrare i propri dispositivi. È necessario disporre di due prerequisiti:

- Con le impostazioni client si concede all'utente l'autorizzazione per la registrazione.

- Installare il certificato radice trusted necessario nel dispositivo.

Per altre informazioni su come configurare la registrazione, vedere [configurare la registrazione dei dispositivi per MDM locale](/configmgr/mdm/get-started/set-up-device-enrollment-on-premises-mdm).

## <a name="bkmk_enrollDesk"></a>Registrare Windows 10

1. In un computer Windows 10, passare a **Impostazioni**.

1. Selezionare **account**, quindi **accedere all'ufficio o all'Istituto di istruzione**.

1. Selezionare **Connetti**, immettere il nome dell'entità utente (UPN) e selezionare **continua**. Il nome UPN può essere lo stesso dell'indirizzo di posta elettronica, ad esempio jdoe@contoso.com.

1. Immettere il nome di dominio completo (FQDN) del punto proxy di registrazione e selezionare **continua**.

1. Immettere la password e selezionare **Accedi**.

1. Non è necessario che Windows memorizzi le informazioni di accesso per questa azione, quindi selezionare **Ignora**.

Dopo un breve periodo di tempo, il dispositivo viene registrato con Configuration Manager.

## <a name="bkmk_enrollMob"></a>Registrazione di Windows 10 Mobile

1. In un dispositivo Windows 10 Mobile, passare a **Impostazioni**.

1. Selezionare **account**, quindi fare clic su **accesso**società.

1. Selezionare **Connetti**.

1. Immettere l'UPN e il nome di dominio completo del punto proxy di registrazione. Selezionare quindi **Connetti**.

1. Nella schermata successiva immettere l'UPN e la password e quindi selezionare **Accedi**.

Dopo un breve periodo di tempo, il dispositivo viene registrato con Configuration Manager. Seleziona **Chiudi**.

## <a name="bkmk_verify"></a>Verificare la registrazione

Usare la console di Configuration Manager per verificare che i dispositivi siano registrati correttamente. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare **Dispositivi**. Sfogliare o cercare il dispositivo registrato nell'elenco dei dispositivi.
