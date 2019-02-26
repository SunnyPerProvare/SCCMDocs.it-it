---
title: Carichi di lavoro di CO-gestione
titleSuffix: Configuration Manager
description: Informazioni sui carichi di lavoro che è possibile passare da Configuration Manager a Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3723595091e57a7ad2267a4da325e7c134c7bf1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755271"
---
# <a name="co-management-workloads"></a>Carichi di lavoro di CO-gestione

Non è necessario passare i carichi di lavoro oppure è possibile eseguirli singolarmente quando sei pronto. Configuration Manager continua a gestire tutti gli altri carichi di lavoro, inclusi i carichi di lavoro non passati a Intune e non supporta tutte le altre funzionalità di Configuration Manager che la co-gestione.

CO-gestione supporta carichi di lavoro seguenti:

- [Criteri di conformità](#compliance-policies)  

- [Criteri di Windows Update](#windows-update-policies)  

- [Criteri di accesso alle risorse](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configurazione del dispositivo](#device-configuration)  

- [App di Office a portata di clic](#office-click-to-run-apps)  

- [App client](#client-apps)  



## <a name="compliance-policies"></a>Criteri di conformità 

I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. Usare tali criteri anche per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale. 

Per altre informazioni sulla funzionalità di Intune, vedere [dei criteri di conformità](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Criteri di Windows Update

I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende. 

Per altre informazioni sulla funzionalità di Intune, vedere [configurare Windows Update per i criteri di rinvio di Business](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Criteri di accesso alle risorse

I criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi. 

Per altre informazioni sulla funzionalità di Intune, vedere [distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

A partire da Configuration Manager 1802, il carico di lavoro di Endpoint Protection include il gruppo di Windows Defender di funzionalità di protezione antimalware: 

- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender SmartScreen  
- Crittografia di Windows  
- Windows Defender Exploit Guard  
- Controllo delle applicazioni di Windows Defender  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection  
- Windows Information Protection  

Per altre informazioni sulla funzionalità di Intune, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configurazione del dispositivo
<!--1357903-->

A partire da Configuration Manager 1806, il carico di lavoro di configurazione dispositivo include le impostazioni per i dispositivi gestiti nell'organizzazione. Passaggio di questo carico di lavoro viene anche il **accesso alle risorse** e **Endpoint Protection** carichi di lavoro.

È comunque possibile continuare a distribuire le impostazioni da Configuration Manager ai dispositivi con co-gestione, anche se Intune è l'autorità di configurazione del dispositivo. Questa eccezione può essere utilizzata per configurare le impostazioni che l'organizzazione richiede una ma non sono ancora disponibile in Intune. Specificare questa eccezione in una [linea di base di configurazione di Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Abilitare l'opzione **sempre questa linea di base si applicano anche per i client di CO-gestiti** quando si crea la linea di base. È possibile modificarlo in un secondo momento le **generale** scheda delle proprietà di una baseline esistente.  

Per altre informazioni sulla funzionalità di Intune, vedere [creare un profilo di dispositivo in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>App A portata di clic di Office
<!--1357841-->

A partire da Configuration Manager 1806, questo carico di lavoro consente di gestire le app di Office 365 nei dispositivi con CO-gestione. 

- Dopo lo spostamento del carico di lavoro, l'app viene visualizzata nel **portale aziendale** sul dispositivo  

- Gli aggiornamenti di Office possono richiedere circa 24 ore prima di essere visualizzati nei client, a meno che i dispositivi non vengano riavviati  

- È disponibile una nuova condizione globale che determina se **le applicazioni di Office 365 sono gestite da Intune nel dispositivo**. Questa condizione viene aggiunta per impostazione predefinita come requisito alle nuove applicazioni di Office 365. Durante la transizione di questo carico di lavoro, i client in co-gestione non soddisfano il requisito relativo all'applicazione. Non installano quindi Office 365 distribuito da Configuration Manager.  

Per altre informazioni sulla funzionalità di Intune, vedere [apps assegnare Office 365 ai dispositivi Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>App client
<!--1357892-->

A partire da Configuration Manager versione 1806, usare Intune per gestire le app client in dispositivi Windows 10 CO-gestiti. Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center.

Per altre informazioni sulla funzionalità di Intune, vedere [che cos'è gestione delle app di Microsoft Intune?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> Carico di lavoro di App client è una funzionalità di versioni non definitive. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Passaggi successivi

[Viene illustrato come passare i carichi di lavoro](/sccm/comanage/how-to-switch-workloads)  


