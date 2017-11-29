---
title: "Azioni per la mancata conformità"
titleSuffix: Configuration Manager
description: "Informazioni su come configurare azioni per la mancata conformità con Configuration Manager"
ms.custom: na
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 1dd10d9452fae85f2ecc3d3077fba420454ef337
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="set-up-actions-for-non-compliance"></a>Configurare azioni per la mancata conformità

La funzionalità **Azioni per la non conformità** consente di configurare una sequenza in ordine temporale delle azioni applicate ai dispositivi che non soddisfano la conformità. Ad esempio, è possibile inviare messaggi di posta elettronica all'utente finale dei dispositivi non conformi e/o contrassegnare i dispositivi come non conformi.

## <a name="before-you-begin"></a>Prima di iniziare

> [!IMPORTANT]
> Per poter configurare azioni per la mancata conformità, è necessario aver creato almeno un criterio di conformità del dispositivo.

Ecco le azioni supportate per la mancata conformità:

- Invia un messaggio di posta elettronica all'utente finale
- Contrassegna il dispositivo come non conforme

### <a name="send-e-mail-to-end-user"></a>Invia un messaggio di posta elettronica all'utente finale

È possibile scegliere tra modelli di messaggio di posta elettronica predefiniti oppure creare una notifica tramite posta elettronica completamente personalizzata. Configuration Manager consente la personalizzazione di oggetto, corpo del messaggio, incluso il logo aziendale, informazioni di contatto e destinatari aggiuntivi.

### <a name="mark-devices-non-compliant"></a>Contrassegna il dispositivo come non conforme

È possibile definire una pianificazione per il numero di giorni per cui impedire al dispositivo l'accesso a risorse aziendali. Questo può avvenire immediatamente, ma è anche possibile concedere all'utente un periodo di tolleranza entro cui soddisfare la conformità tramite criteri di conformità del dispositivo.

### <a name="supported-platforms"></a>Piattaforme supportate

Supporto per [tutte le piattaforme gestite tramite Intune](https://docs.microsoft.com/intune/supported-devices-browsers).

## <a name="to-add-an-email-template"></a>Per aggiungere un modello di messaggio di posta elettronica

Configuration Manager offre alcuni modelli di messaggio di posta elettronica, ma è possibile crearne di personalizzati. Il modello viene usato successivamente nel processo di creazione delle azioni per la mancata conformità per comunicare con gli utenti.

1. Nella console di Configuration Manager scegliere **Asset e conformità**.

2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e quindi scegliere **Modelli di notifica sulla conformità**.

3. Nella scheda **Home** in **Crea il modello di notifica sulla conformità**:

4. È necessario immettere le informazioni seguenti: a. Nome: nome del modello di messaggio di posta elettronica.
    b. Da: indirizzo di posta elettronica da cui viene inviata la notifica.
    c. Oggetto: oggetto che descrive la notifica inviata.
    d. Corpo del messaggio: altri dettagli sulla notifica tramite posta elettronica.

    > [!TIP] 
    > È anche possibile includere un'**intestazione del messaggio di posta elettronica** con il logo dell'azienda e un piè di pagina contenente il nome dell'azienda e le informazioni di contatto. Questi elementi possono essere modificati anche nelle proprietà della sottoscrizione di Intune.

5. Fare clic su **OK** per salvare il nuovo modello di messaggio di posta elettronica.

6. Nella pagina **Aggiungi azione** è possibile selezionare il nuovo modello di messaggio di posta elettronica nell'elenco.

7. Dopo aver selezionato il modello, fare clic su **OK**.

## <a name="to-create-actions-for-non-compliance"></a>Per creare azioni per la mancata conformità

1. Nella console di Configuration Manager scegliere **Asset e conformità**.

2. Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità** e scegliere**Criteri di conformità**.

3. Nel gruppo **Crea** della scheda **Home** scegliere **Crea criteri di conformità**.

4. Selezionare gli elementi desiderati in **Piattaforme supportate** e quindi fare clic su **Avanti** due volte. È possibile ignorare la pagina **Regole**.

5. Nella pagina **Azioni di non conformità** è necessario definire il comportamento desiderato quando un dispositivo diventa non conforme facendo clic su **Nuovo**.
6. È possibile scegliere tra due opzioni: **Invia un messaggio di posta elettronica all'utente finale** e **Contrassegna il dispositivo come non conforme**.

7. Se si seleziona **Invia un messaggio di posta elettronica all'utente finale**, è necessario immettere le informazioni seguenti: a. **Periodo di tolleranza (in giorni)**: è possibile immettere da 0 a 365 giorni.
    b. **Altri destinatari (tramite posta elettronica)** c. **Selezionare un modello di messaggio**: è possibile scegliere i modelli di messaggio di posta elettronica predefiniti oppure quelli personalizzati aggiunti.
    
    > [!TIP] 
    > È anche possibile aggiungere un nuovo modello di messaggio di posta elettronica durante l'aggiunta dell'azione **Invia un messaggio di posta elettronica all'utente finale** facendo clic su **Nuovo** nella pagina **Aggiungi azione**.

8. Se si seleziona **Contrassegna il dispositivo come non conforme**, è necessario immettere le informazioni seguenti: a. **Periodo di tolleranza (in giorni)**: è possibile immettere da 0 a 365 giorni.

9. Dopo aver scelto l'azione e aver immesso le impostazioni correlate, fare clic su **Avanti** due volte e quindi su **Chiudi**.


