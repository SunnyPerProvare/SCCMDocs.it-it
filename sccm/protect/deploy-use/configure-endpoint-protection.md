---
title: Configurare Endpoint Protection | Microsoft Docs
description: Informazioni su come gestire la sicurezza e i malware nei computer client di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 3678fd1e2ba70ad1cc03a3e0ca294901fae96255


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>Configurazione di Endpoint Protection in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter usare Endpoint Protection per gestire la sicurezza e i malware nei computer client di Configuration Manager, procedere alla relativa configurazione, come descritto in questo argomento.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Come configurare Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager ha dipendenze all'interno e all'esterno del prodotto.  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Configurare Endpoint Protection in Configuration Manager  
La configurazione di Endpoint Protection prevede cinque passaggi:

|Passaggio|Dettagli|
|---|----|
|Passaggio 1|[Creare un ruolo del sistema del sito Punto di Endpoint Protection](endpoint-protection-site-role.md): installare il ruolo del sistema del sito Punto di Endpoint Protection |
|Passaggio 2|[Configurare gli avvisi per Endpoint Protection](endpoint-configure-alerts.md): configurare gli avvisi per Endpoint Protection per notificare agli amministratori quando si verificano eventi di sicurezza specifici nella gerarchia|
|Passaggio 3 | [Configurare le origini degli aggiornamenti di definizioni per i client di Endpoint Protection](endpoint-definition-updates.md): scegliere uno dei metodi disponibili per mantenere aggiornate le definizioni antimalware nei computer client|
|Passaggio 4|[Configurare i criteri antimalware predefiniti e creare criteri antimalware personalizzati](endpoint-antimalware-policies.md): il criterio antimalware predefinito viene applicato all'installazione del client Endpoint Protection; i criteri personalizzati vengono applicati entro 60 minuti dalla distribuzione del client|
|Passaggio 5|[Configurare le impostazioni client personalizzate per Endpoint Protection](endpoint-protection-configure-client.md): configurare le impostazioni client personalizzate per Endpoint Protection da distribuire agli insiemi di computer|

> [!IMPORTANT]  
>  Se si gestisce Endpoint Protection per i computer Windows 10, è necessario configurare Configuration Manager per aggiornare e distribuire le definizioni dei malware per Windows Defender. Windows Defender è incluso in Windows 10 ma è necessario che sia installato SCEPInstall e sono necessarie le impostazioni client personalizzate per Endpoint Protection (passaggio 5).  



<!--HONumber=Dec16_HO3-->


