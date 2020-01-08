---
title: Configurare un punto di connessione del servizio
titleSuffix: Configuration Manager
description: Creare un punto di connessione del servizio usando Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e620ce639d20b52e106026a88162e6b1ada6a5fb
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75521001"
---
# <a name="create-a-service-connection-point-with-configuration-manager-and-microsoft-intune"></a>Creare un punto di connessione del servizio con Configuration Manager e Microsoft Intune

*Si applica a: Configuration Manager (Current Branch)*

Dopo avere creato la sottoscrizione, sarà quindi possibile installare il ruolo del sistema del sito del punto di connessione del servizio che consente di connettersi al servizio Intune. Questo ruolo del sistema del sito effettuerà il push delle impostazioni e delle applicazioni al servizio Intune.

 Il punto di connessione del servizio invia le impostazioni e le informazioni di distribuzione del software a Configuration Manager e recupera i messaggi di stato e di inventario dai dispositivi mobili. Il servizio Configuration Manager funge da gateway che comunica con i dispositivi mobili e archivia le impostazioni.

> [!NOTE]
>  Il ruolo del sistema del sito del punto di connessione del servizio può essere installato solo in un sito di amministrazione centrale o in un sito primario autonomo. Il punto di connessione del servizio deve avere accesso a Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurare il ruolo del punto di connessione del servizio

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, quindi fare clic su **Server e ruoli del sistema del sito**.

3.  Aggiungere il ruolo del **punto di connessione del servizio** a un server del sistema del sito nuovo o esistente usando il passaggio associato:

    -   nuovo server del sistema del sito: Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito** per avviare la Creazione guidata server del sistema sito.

    -   Server del sistema del sito esistente: fare clic sul server in cui si vuole installare il ruolo del punto di connessione del servizio. Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito** per avviare l'Aggiunta guidata ruoli del sistema del sito.

4.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di connessione del servizio**, quindi fare clic su **Avanti**.
![Creare un punto di connessione del servizio](../media/mdm-service-connection-point.png)

* completare la procedura guidata.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Autenticazione del punto di connessione del servizio con il servizio Microsoft Intune
 Il punto di connessione del servizio estende Configuration Manager mediante una connessione al servizio basato su cloud Intune che gestisce i dispositivi mobili su Internet. Il punto di connessione del servizio esegue l'autenticazione con il servizio Intune come di seguito:

1.  Quando si crea una sottoscrizione di Intune nella console di Configuration Manager, l'amministratore di Configuration Manager viene autenticato mediante la connessione ad Azure Active Directory, che reindirizza al rispettivo server AD FS per la richiesta di nome utente e password. Intune rilascia quindi un certificato al tenant.

2.  Il certificato del passaggio 1 viene installato nel ruolo del sito del punto di connessione del servizio e viene usato per autenticare e autorizzare tutte le ulteriori comunicazioni con il servizio Microsoft Intune.

> [!div class="button"]
> [Passaggio successivo](enable-platform-enrollment.md) [< passaggio precedente](terms-and-conditions.md)>
