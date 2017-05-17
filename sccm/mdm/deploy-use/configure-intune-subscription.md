---
title: Configurare la sottoscrizione di Intune tramite System Center Configuration Manager | Microsoft Docs
description: Configurare la sottoscrizione di Intune tramite System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 10cc64ae7e4d91f53201c2896b359e77ef04d32d
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la sottoscrizione di Intune con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

La sottoscrizione di Intune consente di gestire i dispositivi su Internet. Consente anche di specificare quale raccolta utenti può registrare i dispositivi e di definire le informazioni presentate agli utenti. Durante la creazione della sottoscrizione di Intune è anche possibile aggiungere il proprio marchio al portale aziendale Intune con il logo e gli schemi di colori personalizzati della società.

La sottoscrizione di Intune esegue le operazioni seguenti:

-   Recupera il certificato necessario al punto di connessione del servizio per connettersi al servizio Intune
-   Definisce la raccolta di utenti che consente agli utenti di registrare i dispositivi mobili
-   Definisce e configura le piattaforme mobili da supportare

> [!IMPORTANT]
>  Quando si crea una sottoscrizione per Microsoft Intune in Configuration Manager, il punto di connessione del servizio del sito passerà in "modalità online". Vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Per creare la sottoscrizione a Microsoft Intune

1.  Se non è già stato fatto, creare un account di Microsoft Intune nel sito [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Dopo aver creato l'account di Intune, non sarà necessario aggiungere utenti per l'account di Intune o eseguire altre configurazioni.

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.

3.  Nell'area di lavoro **Amministrazione** espandere **Servizi cloud**e fare clic su **Sottoscrizioni a Microsoft Intune**. Nella scheda **Home** fare clic su **Aggiungi sottoscrizione a Microsoft Intune**.

![Creare una sottoscrizione di Intune](../media/mdm-set-intune.png)

4.  Nella pagina **Introduzione** della Creazione guidata di una sottoscrizione a Microsoft Intune verificare il testo e quindi fare clic su **Avanti**.

5.  Nella pagina **Sottoscrizione** fare clic su **Accedi** e accedere usando l'account aziendale o dell'istituto di istruzione. Nella finestra di dialogo **Impostare l'autorità di gestione dei dispositivi mobili** selezionare la casella di controllo per gestire solo i dispositivi mobili usando Configuration Manager mediante la console di Configuration Manager. Per continuare con la sottoscrizione, è necessario selezionare questa opzione.

    > [!IMPORTANT]
    >  Dopo aver selezionato Configuration Manager come autorità di gestione, non sarà possibile modificarla successivamente in Microsoft Intune.

6.  Fare clic sui collegamenti privacy per verificarli e quindi fare clic su **Avanti**.

7.  Nella pagina **Generale** specificare le seguenti opzioni e quindi fare clic su **Avanti**.

  -   **Raccolta**: Specificare una raccolta utenti che contenga gli utenti che registreranno i dispositivi mobili.

      > [!NOTE]
      >  Se un utente viene rimosso dalla raccolta, il dispositivo dell'utente continuerà a essere gestito per un massimo di 24 ore finché il record utente non verrà rimosso dal database utenti.

  -   **Nome società**: specificare il nome della società.

  -   **URL della documentazione sulla privacy**: se si pubblicano le informazioni sulla privacy della società in un collegamento accessibile da Internet, fornire un collegamento a cui gli utenti possano accedere dal portale aziendale, ad esempio http://www.contoso.com/CP_privacy.html. Le informazioni sulla privacy possono chiarire quali informazioni gli utenti condividono con la società.

  -   **Combinazione colori per portale società**: Facoltativamente, modificare il colore predefinito blu per i portali società.

  -   **Codice del sito Configuration Manager**: Specificare un codice del sito per un sito primario per gestire i dispositivi mobili.

    > [!NOTE]
    >  La modifica del codice del sito riguarda solo le nuove registrazioni e non i dispositivi registrati esistenti.

8.  Nella pagina **Informazioni di contatto società** specificare le informazioni di contatto dell'azienda che vengono visualizzate nell'app Portale aziendale in **Contatta l'IT**. Specificare le informazioni di contatto dell'azienda e quindi fare clic su **Avanti**.

9. Nella pagina **Logo società** scegliere se visualizzare un logo nel portale aziendale e quindi fare clic su **Avanti**.

10. Completare la procedura guidata.

> [!div class="button"]
[< Passaggio precedente](confirm-dns.md)  [Passaggio successivo >](terms-and-conditions.md)

