---
title: Asset nel Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sui dispositivi, App, le app di Office, componenti aggiuntivi di Office e macro di Office nel Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149c5f2a4469a353c6dce6fde86527ca95518484
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755291"
---
# <a name="assets-in-desktop-analytics"></a>Asset nel Desktop Analitica 

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Dopo che i dispositivi segnalano i dati per Desktop Analitica, esso fornisce un inventario degli asset seguenti:
- Dispositivi  
- Driver dell'hardware  
- App installate  
- App di Office  
- Componenti aggiuntivi di Office  
- Macro di Office  

Nel portale dei servizi, selezionare **asset** nel menu Desktop Analitica.


## <a name="devices"></a>Dispositivi

Il **dispositivi** scheda vengono visualizzate informazioni sulla chiave su tutti i dispositivi nell'organizzazione che si registra per Desktop Analitica. È possibile ordinare qualsiasi colonna o un filtro per determinati valori.

> [!NOTE]  
> Se il dashboard non segnala il numero di dispositivi previsto per l'ambiente, vedere [risoluzione dei problemi relativi a Desktop Analitica](/sccm/desktop-analytics/troubleshooting).  



## <a name="apps"></a>App

Il **app** scheda installato Mostra tutte le app che il servizio rileva nei dispositivi Windows.

**Degno di nota** le app vengono installate in più di 2% dei dispositivi registrati. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configurare il **importanza** delle App quando si imposta una delle categorie seguenti:

- Critico
- Importante
- Ignora
- Verifica non effettuata

Selezionare l'app dall'elenco e selezionare **modifica**. Questa azione consente di visualizzare i dettagli per l'app. Selezionare il **importanza** dal menu a discesa e impostare un valore. È anche possibile assegnare un **proprietario**. Se si apportano modifiche, selezionare **salvare**. 


## <a name="office-apps"></a>App di Office

Il **le app di Office** scheda è simile alla scheda app. Visualizza solo le app, ad esempio Microsoft Word o Excel e non categorizzazione o conteggio degno di nota. Impostare l'importanza e il proprietario per le app di Office esattamente come con altre app.


## <a name="office-add-ins"></a>Componenti aggiuntivi di Office

Il **componenti aggiuntivi di Office** scheda Mostra strumenti, ad esempio, Microsoft Azure Information Protection o analisi di supporto. Questa scheda è simile alla scheda App, e include il conteggio degno di nota. Come con le app, impostare l'importanza e il proprietario. 


## <a name="office-macros"></a>Macro di Office

Il **macro di Office** scheda Mostra se tutti i dispositivi sono aperti di recente tutti i file che è possono includere macro. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> Se si usa anche il [Readiness Toolkit](https://aka.ms/readinesstoolkit) per componenti aggiuntivi di Office e Visual Basic, Applications Edition (VBA), questa scheda vengono visualizzate anche dati aggiuntivi da tali dispositivi. 
> 
> Non è necessario usare il Toolkit di conformità per usare Desktop Analitica.  



## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui piani di distribuzione Desktop Analitica](/sccm/desktop-analytics/about-deployment-plans)  

- [Informazioni sugli aggiornamenti di sicurezza e funzionalità](/sccm/desktop-analytics/about-updates)  

