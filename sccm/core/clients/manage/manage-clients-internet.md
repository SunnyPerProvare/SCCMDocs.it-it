---
title: Gestire i client su Internet - Configuration Manager | Microsoft Docs
description: Informazioni sulla gestione dei client con gateway di gestione cloud e sulla gestione basata su Internet in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gestire i client in Internet con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In Configuration Manager, la maggior parte dei computer e dei server gestiti si trovano in genere fisicamente nella stessa rete interna privata o aziendale dei server del sistema del sito che eseguono le funzioni di gestione. È tuttavia possibile gestire i computer client all'esterno della rete aziendale se sono connessi a Internet senza che sia necessaria la connessione tramite reti private virtuali per raggiungere i server del sistema del sito.

Configuration Manager offre due modi per gestire i client connessi a Internet:

-   Gateway di gestione cloud

-   Gestione client basata su Internet

## <a name="cloud-management-gateway"></a>Gateway di gestione cloud

A partire dalla versione 1610, Configuration Manager introduce il gateway di gestione cloud. Questo nuovo metodo offre un modo per gestire i client basati su Internet usando una combinazione di un servizio cloud distribuito a Microsoft Azure e un nuovo ruolo del sistema del sito che comunica con il servizio. I client usano quindi il servizio per comunicare con Configuration Manager.

Vantaggi:

-   Nessun investimento aggiuntivo in infrastrutture.

-   Infrastruttura locale non esposta a Internet.

-   Macchine virtuali cloud che eseguono il servizio completamente gestite da Azure e senza necessità di manutenzione.

-   Facilità di impostazione e configurazione nella console di Configuration Manager.

Svantaggi:

-   Costo di sottoscrizione al servizio cloud.

-   Invio dei dati di gestione tramite il servizio cloud.

Per altre informazioni, vedere [Plan for cloud management gateway](plan-cloud-management-gateway.md) (Pianificare il gateway di gestione cloud).

## <a name="internet-based-client-management"></a>Gestione client basata su Internet

Questo metodo si basa sui server del sistema del sito con connessione a Internet con cui i client comunicano ai fini della gestione. Questo metodo richiede che client e server del sistema del sito siano configurati per la gestione basata su Internet.

Vantaggi:

-   Nessuna dipendenza del servizio cloud.

-   Nessun costo aggiuntivo associato alla sottoscrizione a un servizio cloud.

-   Controllo completo di server e ruoli che offrono il servizio.

Svantaggi:

-   Necessità di un investimento aggiuntivo in infrastrutture.

-   Carico e costo operativo di un'infrastruttura aggiuntiva.

-   Necessità di esporre l'infrastruttura a Internet.

Per altre informazioni, vedere [Plan for Internet-based client management](plan-internet-based-client-management.md) (Pianificare la gestione client basata su Internet).
