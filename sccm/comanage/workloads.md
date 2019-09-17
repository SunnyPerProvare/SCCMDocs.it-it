---
title: Carichi di lavoro con co-gestione
titleSuffix: Configuration Manager
description: Informazioni sui carichi di lavoro che è possibile trasferire da Configuration Manager a Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/06/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: 766d1f0c258dd25fc4aa51ef20b2d3921ac8cc74
ms.sourcegitcommit: ba68f10d2ca7997057a01af911a2e7cf7e010cf0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70863132"
---
# <a name="co-management-workloads"></a>Carichi di lavoro con co-gestione

Non è obbligatorio trasferire i carichi di lavoro oppure è possibile procedere singolarmente al momento opportuno. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro che non vengono trasferiti a Intune, e tutte le altre funzionalità di Configuration Manager non supportate dalla co-gestione.

Se si trasferisce un carico di lavoro a Intune, ma in seguito si cambia idea, è possibile tornare a Configuration Manager.

La co-gestione supporta i carichi di lavoro seguenti:

- [Criteri di conformità](#compliance-policies)  

- [Criteri di Windows Update](#windows-update-policies)  

- [Criteri di accesso alle risorse](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configurazione del dispositivo](#device-configuration)  

- [App A portata di clic di Office](#office-click-to-run-apps)  

- [App client](#client-apps)  


## <a name="compliance-policies"></a>Criteri di conformità

I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. Usare tali criteri anche per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale.

Per altre informazioni sulla funzionalità Intune, vedere [Criteri di conformità dei dispositivi](https://docs.microsoft.com/intune/device-compliance-get-started).  


## <a name="windows-update-policies"></a>Criteri di Windows Update

I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende.

Per altre informazioni sulla funzionalità Intune, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure).  


## <a name="resource-access-policies"></a>Criteri di accesso alle risorse

I criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi.

Per altre informazioni sulla funzionalità Intune, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).

> [!Note]  
> Il carico di lavoro di accesso alle risorse fa parte anche della configurazione del dispositivo. Questi criteri vengono gestiti da Intune quando si passa al carico di lavoro [Configurazione del dispositivo](#device-configuration).


## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

A partire da Configuration Manager 1802, il carico di lavoro di Endpoint Protection include la suite di funzionalità di protezione antimalware di Windows Defender:

- Windows Defender Antimalware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Crittografia di Windows  
- Windows Defender Exploit Guard  
- Controllo delle applicazioni di Windows Defender  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection (ora denominato Microsoft Defender Threat Protection)
- Windows Information Protection  

Per altre informazioni sulla funzionalità Intune, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

> [!Note]  
> Quando si passa a questo carico di lavoro, i criteri di Configuration Manager vengono mantenuti nel dispositivo fino a quando non vengono sovrascritti dai criteri di Intune. Questo comportamento garantisce che il dispositivo abbia i criteri di protezione anche durante la transizione.
>
> Il carico di lavoro Endpoint Protection fa parte anche della configurazione del dispositivo. Lo stesso comportamento si applica quando si passa al carico di lavoro [Configurazione del dispositivo](#device-configuration).<!-- SCCMDocs.nl-nl issue #4 -->


## <a name="device-configuration"></a>Configurazione del dispositivo

<!--1357903-->

A partire da Configuration Manager 1806, il carico di lavoro di configurazione dei dispositivi include le impostazioni gestite per i dispositivi dell'organizzazione. Trasferendo questo carico di lavoro vengono spostati anche i carichi di lavoro **Accesso alla risorsa** ed **Endpoint Protection**.

È comunque possibile continuare a distribuire le impostazioni da Configuration Manager ai dispositivi con co-gestione, anche se Intune è l'autorità di configurazione del dispositivo. Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune. Specificare questa eccezione in una [linea di base di configurazione di Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Abilitare l'opzione **Applica sempre questa baseline anche per client con co-gestione** quando si crea la baseline. È possibile modificarla in un secondo momento nella scheda **Generale** delle proprietà di una baseline esistente.  

Per altre informazioni sulla funzionalità Intune, vedere [Creare un profilo di dispositivo in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  


## <a name="office-click-to-run-apps"></a>App A portata di clic di Office

<!--1357841-->

A partire da Configuration Manager 1806, questo carico di lavoro consente di gestire le app di Office 365 nei dispositivi con co-gestione.

- Dopo lo spostamento del carico di lavoro, l'app viene visualizzata nel **portale aziendale** sul dispositivo  

- Gli aggiornamenti di Office possono richiedere circa 24 ore prima di essere visualizzati nei client, a meno che i dispositivi non vengano riavviati  

- È disponibile una nuova condizione globale che determina se **le applicazioni di Office 365 sono gestite da Intune nel dispositivo**. Questa condizione viene aggiunta per impostazione predefinita come requisito alle nuove applicazioni di Office 365. Durante la transizione di questo carico di lavoro, i client in co-gestione non soddisfano il requisito relativo all'applicazione. Non installano quindi Office 365 distribuito da Configuration Manager.  

Per altre informazioni sulla funzionalità Intune, vedere [Assegnare le app di Office 365 ai dispositivi Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365).


## <a name="client-apps"></a>App client

<!--1357892-->

A partire da Configuration Manager versione 1806, usare Intune per gestire le app client e gli script di PowerShell in dispositivi Windows 10 con co-gestione. Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center.

Per altre informazioni sulla funzionalità Intune, vedere [Informazioni sulla gestione delle app in Microsoft Intune](https://docs.microsoft.com/intune/app-management).

> [!Note]  
> Il carico di lavoro delle app client è una funzionalità non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).  


## <a name="diagram-for-app-workloads"></a>Diagramma per i carichi di lavoro delle app

![Diagramma dei carichi di lavoro delle app di co-gestione](media/co-management-apps.svg)

[Visualizzare il diagramma per intero](media/co-management-apps.svg)


## <a name="next-steps"></a>Passaggi successivi

[Come trasferire i carichi di lavoro](/sccm/comanage/how-to-switch-workloads)  
