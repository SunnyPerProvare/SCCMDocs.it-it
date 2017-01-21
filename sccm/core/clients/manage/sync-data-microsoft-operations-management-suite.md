---
title: 'Sincronizzare i dati | Microsoft Docs | Microsoft Operations Management Suite '
description: Sincronizzazione dei dati da System Center Configuration Manager a Microsoft Operations Management Suite.
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 0d8944bef9578a41b529a2d53b5a4d0094eaa21c

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizzazione dei dati da Configuration Manager a Microsoft Operations Management Suite

*Si applica a: System Center Configuration Manager (Current Branch)*

È ora possibile usare il connettore Microsoft Operations Management Suite (OMS) per sincronizzare i dati, ad esempio le raccolte, da System Center Configuration Manager a OMS. In questo modo i dati della distribuzione di Configuration Manager sono visibili in OMS.

## <a name="add-an-oms-connection-to-configuration-manager"></a>Aggiungere una connessione di OMS a Configuration Manager

Per aggiungere una connessione di OMS, è necessario che nell'ambiente di Configuration Manager sia stato configurato un [punto di connessione del servizio](../../../core/servers/deploy/configure/about-the-service-connection-point.md) in [modalità online](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Quando si aggiunge una connessione di OMS all'ambiente, viene installato anche Microsoft Monitoring Agent nel computer che esegue questo ruolo del sistema del sito.
1.  Nell'area di lavoro **Amministrazione** selezionare **OMS Connector**. Nella barra multifunzione fare clic su "Creare una connessione a Operations Management Suite". Verrà visualizzata la **Connessione guidata a Operations Management Suite**. Selezionare **Avanti**.
2.  Nella schermata **Generale** verificare di avere le informazioni seguenti, quindi selezionare **Avanti**.

    * Configuration Manager registrato come uno strumento di gestione "Applicazione Web e/o API Web" e di avere [l'ID client della registrazione](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Una chiave client creata per lo strumento di gestione registrato in Azure Active Directory.
    * Nel portale di gestione di Azure aver specificato l'autorizzazione di accesso OMS per l'app Web registrata, come descritto in [Fornire a Configuration Manager le autorizzazioni per accedere a OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

3.  Nella schermata di **Azure Active Directory** configurare le impostazioni di connessione a OMS, specificando **Tenant**, **ID client** e **Chiave privata del client**, poi selezionare **Avanti**.
4.  Nella schermata **OMS Connection Configuration** (Configurazione connessione OMS) specificare le impostazioni di connessione in **Sottoscrizione di Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite**.
5.  Verificare le impostazioni di connessione nella schermata **Riepilogo** e selezionare **Avanti**. Nella schermata **Avanzamento** verrà visualizzato lo stato della connessione e quindi **Completata**.

> [!NOTE]
> È necessario che OMS sia connesso al sito di livello superiore nella gerarchia. Se si connette OMS a un sito primario autonomo e poi si aggiunge un sito di amministrazione centrale all'ambiente, è necessario eliminare e ricreare la connessione di OMS all'interno della nuova gerarchia.

Dopo aver collegato Configuration Manager a OMS, è possibile aggiungere o rimuovere raccolte e visualizzare le proprietà della connessione OMS.

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Visualizzazione delle proprietà di connessione di Microsoft Operations Management Suite in Configuration Manager

1.  Passare a **Servizi cloud** e selezionare **OMS Connector** per aprire la pagina **OMS Connection Properties** (Proprietà connessione OMS).
2.  In questa pagina sono disponibili due schede:
  * La scheda **Azure Active Directory** visualizza **Tenant**, **ID client** e **Client secret key expiration** (Scadenza chiave privata del client) e consente la **Verifica** della **Chiave privata del client** se è scaduta.
  * La scheda **OMS Connection Properties** (Proprietà connessione OMS) visualizza **Sottoscrizione di Azure**, **Gruppo di risorse di Azure** e **Area di lavoro di Operations Management Suite** nonché un elenco di **raccolte di dispositivi per cui OMS può recuperare i dati**. Usare i pulsanti **Aggiungi** e **Rimuovi** per modificare le raccolte consentite.



<!--HONumber=Dec16_HO3-->


