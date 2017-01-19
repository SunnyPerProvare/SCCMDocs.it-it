---
title: Configurare Endpoint Protection | Microsoft Docs
description: Informazioni su come configurare Configuration Manager per aggiornare e distribuire le definizioni dei malware per Windows Defender.
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
ms.sourcegitcommit: 180d05d3493f8c4288ad4bf640da15bd599c2072
ms.openlocfilehash: 783d8352e3e1f06af3a5d8534b4fa811f36fdc17


---

# <a name="configure-endpoint-protection-in-system-center-configuration-manager"></a>Configurare Endpoint Protection in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter usare Endpoint Protection per gestire la sicurezza e i malware nei computer client di Configuration Manager, è necessario eseguire i passaggi di configurazione descritti in questo argomento.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Come configurare Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager ha relazioni esterne e relazioni all'interno del prodotto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Passaggi per la configurazione di Endpoint Protection in Configuration Manager  
 Usare la tabella seguente per passaggi, dettagli e altre informazioni su come configurare Endpoint Protection.  

> [!IMPORTANT]  
>  Se si gestisce Endpoint Protection per i computer Windows 10, è necessario configurare Configuration Manager per aggiornare e distribuire le definizioni dei malware per Windows Defender. Windows Defender è incluso in Windows 10 ma è necessario che sia installato SCEPInstall e le impostazioni client personalizzate per Endpoint Protection (**Passaggio 5** sotto) sono comunque necessarie.  

|Passaggi|Dettagli|  
|-----------|-------------|  
|**Passaggio 1:** Creare un ruolo del sistema del sito del punto di Endpoint Protection.|Prima di poter usare Endpoint Protection, è necessario installare il ruolo del sistema del sito Punto di Endpoint Protection. Il ruolo deve essere installato in un solo server di sistema del sito, al livello superiore della gerarchia in un sito di amministrazione centrale o un sito primario autonomo. Vedere [Passaggio 1: Creare un ruolo del sistema del sito del punto di Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Passaggio 2**: Configurare gli avvisi per Endpoint Protection.|Gli avvisi informano l'amministratore quando si verificano eventi specifici, ad esempio un'infezione causata da un malware. Gli avvisi vengono visualizzati nel nodo **Avvisi** dell'area di lavoro **Monitoraggio** oppure possono essere inviati via posta elettronica a utenti specifici. Vedere [Passaggio 2: Configurare gli avvisi per Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Passaggio 3:** Configurare le origini degli aggiornamenti delle definizioni per i client di Endpoint Protection.|È possibile configurare Endpoint Protection per usare più origini per il download degli aggiornamenti delle definizioni. Vedere [Passaggio 3: Configurare le origini degli aggiornamenti delle definizioni per i client di Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  
|**Passaggio 4:** Configurare il criterio antimalware predefinito e creare criteri antimalware personalizzati.|Il criterio antimalware predefinito viene applicato quando viene installato il client di Endpoint Protection. Eventuali criteri personalizzati distribuiti vengono applicati per impostazione predefinita, entro 60 minuti dalla distribuzione del client. Verificare di aver configurato i criteri antimalware prima di distribuire il client di Endpoint Protection. Vedere [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/endpoint-antimalware-policies.md) (Creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager).|  
|**Passaggio 5:** Configurare impostazioni client personalizzate per Endpoint Protection.|Usare impostazioni client personalizzate per configurare le impostazioni di Endpoint Protection per le raccolte di computer nella gerarchia.<br /><br /> Nota: configurare le impostazioni client predefinite per Endpoint Protection solo se si è certi di voler applicare tali impostazioni a tutti i computer nella gerarchia. Vedere [Passaggio 5: Configurare impostazioni client personalizzate per Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md).|  



<!--HONumber=Dec16_HO3-->


