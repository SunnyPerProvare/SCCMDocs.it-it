---
title: Portale self-service BitLocker
titleSuffix: Configuration Manager
description: Come utilizzare il portale self-service dell'utente in Configuration Manager per il ripristino di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3cbf700a25f34da5dc31fa5ac268126b1f69703a
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75820747"
---
# <a name="bitlocker-self-service-portal"></a>Portale self-service BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Dopo aver [installato il portale self-service di BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites), se BitLocker blocca il dispositivo di un utente, può ottenere l'accesso ai computer in modo indipendente. Per il portale self-service non è richiesta l'assistenza del personale dell'help desk.

[![screenshot del portale self-service BitLocker predefinito](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Per ottenere una chiave di ripristino dal portale self-service, è necessario che un utente abbia eseguito correttamente l'accesso al computer almeno una volta. Questo accesso deve essere locale nel dispositivo, non in una sessione remota. In caso contrario, è necessario contattare la help desk per il recupero della chiave. Un amministratore help desk può utilizzare il [sito Web di Administration and Monitoring](/configmgr/protect/deploy-use/bitlocker/helpdesk-portal) per richiedere la chiave di ripristino.

BitLocker è in grado di bloccare il dispositivo nelle situazioni seguenti:

- L'utente dimentica la password o il PIN di BitLocker

- È stata apportata una modifica ai file del sistema operativo del dispositivo, al BIOS o al Trusted Platform Module (TPM)

Per richiedere la chiave di ripristino di BitLocker dal portale self-service:

1. Quando BitLocker blocca un dispositivo, viene visualizzata la schermata di ripristino di BitLocker durante l'avvio. Annotare l'ID della chiave di ripristino di BitLocker a 32 cifre.

1. In un altro computer, accedere al portale self-service nel Web browser, ad esempio `https://webserver.contoso.com/SelfService`.

1. Leggere e accettare l'avviso.

1. Nel campo **ID chiave di ripristino** immettere le prime otto cifre dell'ID chiave di ripristino di BitLocker. Se corrisponde a più chiavi, immettere tutte 32 cifre.

1. Scegliere una delle opzioni seguenti per il **motivo** della richiesta:

    - BIOS/TPM modificato
    - Sistema operativo archiviato modificato
    - PIN/passphrase perso

1. Selezionare **Ottieni chiave**. Il portale self-service Visualizza la **chiave di ripristino di BitLocker**a 48 cifre.

1. Immettere questo codice di 48 cifre nella schermata di ripristino di BitLocker nel computer.

> [!NOTE]
> Il portale self-service di BitLocker può scadere dopo un periodo di inattività. Ad esempio, dopo cinque minuti è possibile che venga visualizzato un avviso di timeout con un contatore di 60 secondi.
>
> ![Avviso di timeout del portale self-service BitLocker](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Se non si risponde al conto alla rovescia, la sessione scadrà.
>
> ![Pagina scadenza della sessione del portale self-service BitLocker](media/bitlocker-self-service-portal-session-expired.png)
