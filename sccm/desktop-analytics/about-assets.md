---
title: Asset in desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su dispositivi, driver e app in desktop Analytics.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63800bf6c8fa1d35eac44f64f2f03bde4f1d5022
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535945"
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

Selezionare l'app dall'elenco e quindi fare clic su **modifica**. Questa azione Visualizza i dettagli per l'app. Selezionare il menu a discesa **importanza** e impostare un valore. È anche possibile assegnare un **proprietario**. Se si apportano modifiche, fare clic su **Salva**.

In un piano di distribuzione è inoltre possibile impostare la **decisione di aggiornamento**. Per altre informazioni, vedere [pianificare asset](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione di analisi desktop](/sccm/desktop-analytics/about-deployment-plans)  

- [Informazioni sugli aggiornamenti della sicurezza e delle funzionalità](/sccm/desktop-analytics/about-updates)  

- [Valutazione della compatibilità in desktop Analytics](/sccm/desktop-analytics/compat-assessment)  
