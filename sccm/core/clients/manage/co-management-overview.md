---
title: Co-gestione per dispositivi Windows 10
description: Informazioni su come gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune.
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 4b582d5fbd9e2e916c439b149e117f1a65da98bf
ms.sourcegitcommit: 5f4a584d4a833b0cc22bd8c47da7dd55aced97fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2017
---
# <a name="co-management-for-windows-10-devices"></a>Co-gestione per dispositivi Windows 10    
<!-- 1350871 -->
Molti clienti vogliono gestire i dispositivi Windows 10 nello stesso modo in cui gestiscono i dispositivi mobili usando una soluzione semplice, a costi contenuti e basata su cloud. Tuttavia, la transizione dalla gestione tradizionale a una gestione moderna può essere complessa. Negli aggiornamenti precedenti di Windows 10 è già possibile aggiungere un dispositivo Windows 10 ad Active Directory (AD) locale e ad Azure AD basata sul cloud allo stesso tempo (Azure AD ibrida). A partire da Configuration Manager versione 1710, la co-gestione sfrutta questo miglioramento e consente di gestire contemporaneamente i dispositivi Windows 10 versione 1709 (noto anche come Fall Creators Update) usando sia Configuration Manager sia Intune. È una soluzione che costituisce un ponte tra la gestione tradizionale e quella moderna e che consente di eseguire la transizione mediante un approccio per fasi. 

I percorsi principali per realizzare la co-gestione sono due.  Uno consiste nella co-gestione fornita da Configuration Manager, in cui i dispositivi Windows 10 gestiti da Configuration Manager e aggiunti ad Azure AD ibrido vengono registrati in Intune. Il secondo avviene quando i dispositivi sottoposti a provisioning da Intune e registrati in Intune e quindi installati con il client di Configuration Manager raggiungono uno stato di co-gestione.  

## <a name="prerequisites"></a>Prerequisiti
Prima di poter abilitare la co-gestione, è necessario soddisfare i prerequisiti seguenti. Esistono prerequisiti generali e prerequisiti diversi per i dispositivi con il client di Configuration Manager e i dispositivi in cui non è installato il client.

### <a name="general-prerequisites"></a>Prerequisiti generali
Di seguito sono elencati i prerequisiti generali per abilitare la co-gestione:  

- Configuration Manager 1710 o versioni successive
- Azure AD
- Licenza di EMS o Intune per tutti gli utenti
- [Registrazione automatica in Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) abilitata
- Sottoscrizione a Intune &#40; Autorità MDM impostata su **Intune**&#41;


   > [!Note]  
   > Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione. Se si vuole eseguire la migrazione a Intune autonomo, vedere [Avviare la migrazione da MDM ibrido a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Prerequisiti aggiuntivi per i dispositivi con il client di Configuration Manager
- Windows 10, versione 1709 (denominata anche Fall Creators Update) e successive
- [Dispositivo aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (aggiunto ad Active Directory e ad Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Prerequisiti aggiuntivi per i dispositivi senza il client di Configuration Manager
- Windows 10, versione 1709 (denominata anche Fall Creators Update) e successive
- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (quando si usa Intune per installare il client di Configuration Manager)

## <a name="workloads-you-can-switch-to-intune"></a>Carichi di lavoro che è possibile passare a Intune
Dopo aver abilitato la co-gestione, Configuration Manager continua a gestire tutti i carichi di lavoro. Quando si è pronti, impostare Intune perché inizi a gestire i carichi di lavoro disponibili. È possibile fare in modo che Intune gestisca i carichi di lavoro seguenti.   

### <a name="compliance-policies"></a>Criteri di conformità
I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. È anche possibile usare tali criteri per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale. Per altre informazioni, vedere [Criteri di conformità del dispositivo in System Center Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Criteri di Windows Update per le aziende
I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende. Per altre informazioni, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Criteri di accesso alle risorse
I criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi. Per informazioni dettagliate, vedere [Distribuire profili di accesso alle risorse](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

## <a name="architectural-overview-for-co-management"></a>Panoramica dell'architettura per la co-gestione
Il diagramma seguente offre una panoramica dell'architettura della co-gestione e illustra come questa si inserisce nelle infrastrutture di Configuration Manager e Intune esistenti.

![Diagramma architettura co-gestione](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Scenari per abilitare la co-gestione  
È possibile abilitare la co-gestione sia per i dispositivi Windows 10 registrati in Microsoft Intune sia per i client esistenti di Configuration Manager in Windows 10. In entrambi gli scenari i dispositivi Windows 10 vengono gestiti congiuntamente da Configuration Manager e da Intune, nonché aggiunti ad Active Directory e Azure AD.  

### <a name="devices-enrolled-in-intune"></a>Dispositivi registrati in Intune  
Quando i dispositivi Windows 10 sono registrati in Intune, è possibile installare il client di Configuration Manager nei dispositivi, mediante un argomento della riga di comando specifico, per preparare i client alla co-gestione. In seguito è possibile abilitare la co-gestione dalla console di Configuration Manager per avviare lo spostamento di carichi di lavoro specifici in Intune per alcuni dispositivi Windows 10.  

Per i dispositivi Windows 10 non ancora registrati in Intune, è possibile usare la registrazione automatica in Azure per registrare i dispositivi. Per i nuovi dispositivi Windows 10, è possibile usare [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) per avviare la configurazione guidata che include la registrazione automatica dei dispositivi in Intune.  

### <a name="configuration-manager-clients"></a>Client di Configuration Manager
Quando si hanno dispositivi Windows 10 che sono client di Configuration Manager, è possibile registrare tali dispositivi e abilitare la co-gestione dalla console di Configuration Manager. Configuration Manager attiva la registrazione automatica in Intune in base alle informazioni del tenant di Azure AD.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Azioni remote disponibili in Intune in Azure per dispositivi co-gestiti
Quando un dispositivo Windows 10 è abilitato per la co-gestione, sono disponibili le azioni remote seguenti da Intune in Azure:  
- [Ripristino impostazioni predefinite](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Cancellazione selettiva](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminazione di dispositivi](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Riavvio di dispositivi](https://docs.microsoft.com/intune/device-restart)
- [Installazione da zero](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Passaggi successivi
[Preparare i dispositivi Windows 10 per la co-gestione](co-management-prepare.md)