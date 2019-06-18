---
title: Asset nel Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sui dispositivi, driver e le app Desktop Analitica.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0e47541d7acf5e1f5a74a58f6d39603bfcb9269
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159236"
---
# <a name="assets-in-desktop-analytics"></a>Asset nel Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Dopo che i dispositivi segnalano i dati per Desktop Analitica, esso fornisce un inventario degli asset seguenti:

- Dispositivi  
- Driver dell'hardware  
- App installate  

Nel portale dei servizi, selezionare **asset** nel menu Desktop Analitica.


## <a name="devices"></a>Dispositivi

Il **dispositivi** scheda vengono visualizzate informazioni sulla chiave su tutti i dispositivi nell'organizzazione che si registra per Desktop Analitica. È possibile ordinare qualsiasi colonna o un filtro per determinati valori.

> [!NOTE]  
> Se il dashboard non segnala il numero di dispositivi previsto per l'ambiente, vedere [risoluzione dei problemi relativi a Desktop Analitica](/sccm/desktop-analytics/troubleshooting).  

In un piano di distribuzione, è più in dettaglio i dispositivi. Per altre informazioni, vedere [pianificare gli asset](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>App

Il **app** scheda installato Mostra tutte le app che il servizio rileva nei dispositivi Windows.

**Degno di nota** le app vengono installate in più di 2% dei dispositivi registrati.

Configurare il **importanza** delle App quando si imposta una delle categorie seguenti:

- Critico
- Importante
- Ignora
- Verifica non effettuata

Selezionare l'app dall'elenco e selezionare **modifica**. Questa azione consente di visualizzare i dettagli per l'app. Selezionare il **importanza** dal menu a discesa e impostare un valore. È anche possibile assegnare un **proprietario**. Se si apportano modifiche, selezionare **salvare**.

In un piano di distribuzione, è anche possibile impostare il **decisione di aggiornamento**. Per altre informazioni, vedere [pianificare gli asset](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione Desktop Analitica](/sccm/desktop-analytics/about-deployment-plans)  

- [Informazioni sugli aggiornamenti di sicurezza e funzionalità](/sccm/desktop-analytics/about-updates)  

- [Valutazione della compatibilità nel Desktop Analitica](/sccm/desktop-analytics/compat-assessment)  
