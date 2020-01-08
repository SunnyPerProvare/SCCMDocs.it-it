---
title: Configurare la sottoscrizione di Intune
titleSuffix: Configuration Manager
description: Configurare la sottoscrizione di Intune usando Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 151dbab44aaf02e3c299df02ae771677a90eca38
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75521188"
---
# <a name="configure-your-intune-subscription-with-configuration-manager-and-microsoft-intune"></a>Configurare la sottoscrizione di Intune con Configuration Manager e Microsoft Intune

*Si applica a: Configuration Manager (Current Branch)*

La sottoscrizione di Intune consente di gestire i dispositivi su Internet. Consente anche di specificare quale raccolta utenti può registrare i dispositivi e di definire le informazioni presentate agli utenti. Durante la creazione della sottoscrizione di Intune è anche possibile aggiungere il proprio marchio al portale aziendale Intune con il logo e gli schemi di colori personalizzati della società.

La sottoscrizione di Intune esegue le operazioni seguenti:

-   Recupera il certificato necessario al punto di connessione del servizio per connettersi al servizio Intune
-   Definisce la raccolta di utenti che consente agli utenti di registrare i dispositivi mobili
-   Definisce e configura le piattaforme mobili da supportare

> [!IMPORTANT]
>  Quando si crea una sottoscrizione per Microsoft Intune in Configuration Manager, il punto di connessione del servizio del sito passerà in "modalità online". Vedere [informazioni sul punto di connessione del servizio](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Per creare la sottoscrizione a Microsoft Intune

1.  Se non è già stato fatto, creare un account di Microsoft Intune nel sito [Microsoft Intune](https://go.microsoft.com/fwlink/?LinkID=258216).  Dopo aver creato l'account di Intune, non sarà necessario aggiungere utenti per l'account di Intune o eseguire altre configurazioni.

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.

3.  Nell'area di lavoro **Amministrazione** espandere **Servizi cloud**e fare clic su **Sottoscrizioni a Microsoft Intune**. Nella scheda **Home** fare clic su **Aggiungi sottoscrizione a Microsoft Intune**.

![Creare una sottoscrizione di Intune](../media/mdm-set-intune.png)

4. Nella pagina **Introduzione** della Creazione guidata di una sottoscrizione a Microsoft Intune verificare il testo e quindi fare clic su **Avanti**.

5. Nella pagina **Sottoscrizione** fare clic su **Accedi** e accedere usando l'account aziendale o dell'istituto di istruzione. Nella finestra di dialogo **Impostare l'autorità di gestione dei dispositivi mobili** selezionare la casella di controllo per gestire solo i dispositivi mobili usando Configuration Manager mediante la console di Configuration Manager. Per continuare con la sottoscrizione, è necessario selezionare questa opzione.

   > [!IMPORTANT]
   >  Dopo aver selezionato Configuration Manager come autorità di gestione, è possibile cambiare l'autorità di gestione di Microsoft Intune senza dover contattare il supporto Microsoft e senza dover annullare e ripetere la registrazione dei dispositivi gestiti esistenti solo in Configuration Manager versione 1610 o versione successiva e Microsoft Intune versione 1705. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority).

6. Fare clic sui collegamenti privacy per verificarli e quindi fare clic su **Avanti**.

7. Nella pagina **Generale** specificare le seguenti opzioni e quindi fare clic su **Avanti**.

   - **Raccolta**: Specificare una raccolta utenti che contenga gli utenti che registreranno i dispositivi mobili.

     > [!NOTE]
     >  Se un utente viene rimosso dalla raccolta, il dispositivo dell'utente continuerà a essere gestito per un massimo di 24 ore finché il record utente non verrà rimosso dal database utenti.

   - **Nome società**: Specificare il nome della società.

   - **URL della documentazione sulla privacy**: se si pubblicano le informazioni sulla privacy della società in un collegamento accessibile tramite Internet, specificare un collegamento a cui gli utenti possono accedere dal portale aziendale, come ad esempio http://www.contoso.com/CP_privacy.html. Le informazioni sulla privacy possono chiarire quali informazioni gli utenti condividono con la società.

   - **Combinazione colori per portale società**: Facoltativamente, modificare il colore predefinito blu per i portali società.

   - **Codice del sito Configuration Manager**: Specificare un codice del sito per un sito primario per gestire i dispositivi mobili.

   > [!NOTE]
   >  La modifica del codice del sito riguarda solo le nuove registrazioni e non i dispositivi registrati esistenti.

8. Nella pagina **Informazioni di contatto società** specificare le informazioni di contatto dell'azienda che vengono visualizzate nell'app Portale aziendale in **Contatta l'IT**. Specificare le informazioni di contatto dell'azienda e quindi fare clic su **Avanti**.

9. Nella pagina **Logo società** scegliere se visualizzare un logo nel portale aziendale e quindi fare clic su **Avanti**.

10. completare la procedura guidata.

> [!div class="button"]
> [Passaggio successivo](terms-and-conditions.md) [< passaggio precedente](confirm-dns.md)>
