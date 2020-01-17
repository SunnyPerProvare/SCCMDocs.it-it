---
title: Aggiungere ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Informazioni sui ruoli del sistema del sito di Configuration Manager e su come aggiungerli per estendere la funzionalità e la capacità del sito.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 633b61e9a97cf61690168db920c271be11cb2198
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75799044"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>Aggiungere ruoli del sistema del sito per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Ogni sito di Configuration Manager supporta più ruoli del sistema del sito, ognuno dei quali estende la funzionalità e la capacità del sito per fornire servizi al sito e per gestire dispositivi e utenti. Ogni ruolo del sistema del sito in un server del sistema del sito deve provenire dallo stesso sito.   

Configuration Manager non supporta i ruoli del sistema del sito per più siti in un unico server di sistema del sito.  

> [!TIP]  
>  Se non si ha familiarità con i concetti di base relativi ai ruoli del sistema del sito o non si conosce la differenza tra server del sito, server del sistema del sito e ruoli del sistema del sito, vedere [Nozioni fondamentali di Configuration Manager](../../../../core/understand/fundamentals.md).  

 Gli argomenti seguenti descrivono le procedure e i relativi dettagli per l'installazione dei ruoli del sistema del sito:  

-   [Installare ruoli del sistema del sito per Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Questo argomento fornisce indicazioni di base su come usare le due procedure guidate nella console che permettono di installare nuovi ruoli del sistema del sito.  

-   [Installare punti di distribuzione basati sul cloud in Microsoft Azure per Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Quando si vuole usare Microsoft Azure per ospitare il contenuto da distribuire ai client, è possibile fare riferimento alle informazioni incluse in questo argomento per configurare i file di certificato necessari per permettere a Configuration Manager di comunicare con la sottoscrizione di Microsoft Azure e usarla. È anche necessario configurare la risoluzione dei nomi per permettere ai client di trovare i punti di distribuzione basati su cloud.  

-   [Installare ruoli del sistema del sito per Gestione dispositivi mobili locali](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Questo argomento consente di configurare correttamente i ruoli del sistema del sito in modo da supportare la gestione dei dispositivi moderni con MDM locale di Configuration Manager.  

-   [Opzioni di configurazione per i ruoli del sistema del sito per Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Alcuni ruoli del sistema del sito supportano configurazioni che richiedono un numero di dettagli superiore a quello che può illustrare l'interfaccia utente. In questo argomento sono riportati tali dettagli.  
