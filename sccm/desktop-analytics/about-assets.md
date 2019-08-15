---
title: Asset in desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su dispositivi, driver e app in desktop Analytics.
ms.date: 08/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 225cc93d38607c90332c1bc56ea12b2c344ab4ea
ms.sourcegitcommit: fe8934487158ed3bd15c7a6a456c3cafe58aed64
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "68995383"
---
# <a name="assets-in-desktop-analytics"></a>Asset in desktop Analytics

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Dopo che i dispositivi hanno segnalato i dati a analisi desktop, fornisce un inventario delle risorse seguenti:

- Dispositivi
- App installate  

Nel portale dei servizi selezionare **Asset** nel menu desktop Analytics.


## <a name="devices"></a>Dispositivi

La scheda **dispositivi** Visualizza le informazioni chiave su tutti i dispositivi dell'organizzazione che si registrano a desktop Analytics. È possibile ordinare qualsiasi colonna o filtro per determinati valori.

> [!NOTE]  
> Se il dashboard non segnala il numero di dispositivi che si prevede di visualizzare per l'ambiente, vedere [risoluzione dei problemi di analisi del desktop](/sccm/desktop-analytics/troubleshooting).  

In un piano di distribuzione sono disponibili maggiori dettagli sui dispositivi. Per altre informazioni, vedere [pianificare asset](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>App

La scheda **app** Mostra tutte le app installate che il servizio rileva nei dispositivi Windows.

Le app **degne** di nota sono installate in più del 2% dei dispositivi registrati.

Configurare l' **importanza** delle app impostando una delle categorie seguenti:

- Critico
- Importante
- Ignora 
- Non verificato
- Non importante<!-- 3587232 -->


Selezionare l'app dall'elenco e quindi fare clic su **modifica**. Questa azione Visualizza i dettagli per l'app. Selezionare il menu a discesa **importanza** e impostare un valore. È anche possibile assegnare un **proprietario**. Se si apportano modifiche, fare clic su **Salva**.

### <a name="a-namebkmk_plan-autoapp--automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Decisione di aggiornamento automatico delle app di sistema e dello Store

<!-- 3587232 -->
L'identificazione dell' **importanza** e della **decisione di aggiornamento** è fondamentale per tutte le app degne di nota nel flusso di lavoro di analisi desktop. Per ridurre il lavoro richiesto per l'annotazione di queste app, determinati tipi di app vengono automaticamente contrassegnati come *non importanti*. La decisione di aggiornamento del piano di distribuzione per queste app è inoltre contrassegnata come *pronta*. Le app seguenti sono compatibili e continueranno a funzionare dopo l'aggiornamento di Windows:

- App di sistema e componenti pubblicati da Microsoft

- App gestite e aggiornate dalla Microsoft Store

> [!Tip]
> Gestisci gli input per qualsiasi app a livello globale o per piano di distribuzione. 
>
> 1. Nel menu Gestisci del portale di analisi del desktop selezionare **Asset**. Quindi selezionare **app**.
>
> 2. Usare le colonne **tipo** e **categoria** per gestire le categorie di app:
>
>    - Per le app dello Store, filtrare il **tipo** come **moderno**
>    - Per le app di sistema, filtrare la **categoria** come **processo in background** o **componente di Windows**



In un piano di distribuzione è inoltre possibile impostare la **decisione di aggiornamento**. Per altre informazioni, vedere [pianificare asset](/sccm/desktop-analytics/about-deployment-plans#plan-assets)




## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione di analisi desktop](/sccm/desktop-analytics/about-deployment-plans)  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](/sccm/desktop-analytics/about-updates)  

- [Valutazione della compatibilità in desktop Analytics](/sccm/desktop-analytics/compat-assessment)  
