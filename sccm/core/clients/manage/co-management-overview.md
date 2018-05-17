---
title: Co-gestione per dispositivi Windows 10
titleSuffix: Configuration Manager
description: Informazioni su come gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 3a667ae075ac688d4b49789ed88f858c2ff39397
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="co-management-for-windows-10-devices"></a>Co-gestione per dispositivi Windows 10    
 Con gli aggiornamenti precedenti di Windows 10 è già possibile aggiungere un dispositivo Windows 10 ad Active Directory (AD) locale e ad Azure AD basato sul cloud allo stesso tempo (Azure AD ibrida). A partire da Configuration Manager versione 1710, la co-gestione sfrutta questo miglioramento e consente di gestire contemporaneamente i dispositivi Windows 10 versione 1709 usando sia Configuration Manager che Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>Perché scegliere la co-gestione
Molti clienti vogliono gestire i dispositivi Windows 10 nello stesso modo in cui gestiscono i dispositivi mobili usando una soluzione semplice, a costi contenuti e basata su cloud. Tuttavia, la transizione dalla gestione tradizionale a una gestione moderna può essere complessa.  
## <a name="what-is-co-management"></a>Informazioni sulla co-gestione
La co-gestione consente di gestire più dispositivi Windows 10 contemporaneamente usando Configuration Manager e Intune. È una soluzione che costituisce un ponte tra la gestione tradizionale e quella moderna e che consente di eseguire la transizione mediante un approccio per fasi.

## <a name="benefits"></a>Vantaggi 
- Uso immediato delle funzionalità di Intune 
    - Azioni remote
        - [Ripristino impostazioni predefinite](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Cancellazione selettiva](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Eliminazione di dispositivi](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Riavvio di dispositivi](https://docs.microsoft.com/intune/device-restart)
        - [Installazione da zero](https://docs.microsoft.com/intune/device-fresh-start)
    - Orchestrazione con Intune per i carichi di lavoro seguenti:
        - [Criteri di conformità](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Criteri di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles)
        - [Criteri di Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10), a partire da Configuration Manager 1802 <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Come configurare la co-gestione
I percorsi principali per realizzare la co-gestione sono due. Uno consiste nella co-gestione fornita da Configuration Manager, in cui i dispositivi Windows 10 gestiti da Configuration Manager e aggiunti ad Azure AD ibrido vengono registrati in Intune. Il secondo avviene quando i dispositivi sottoposti a provisioning da Intune e registrati in Intune e quindi installati con il client di Configuration Manager raggiungono uno stato di co-gestione.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Eseguire l'aggiornamento a Configuration Manager 1710 o versione successiva.


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [Dispositivo aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (aggiunto ad Active Directory e ad Azure AD).
  - [Abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll).


### <a name="intune"></a>**Intune**
 - [Come configurare la sottoscrizione di Intune](/sccm/mdm/deploy-use/configure-intune-subscription) o [Configurare Intune](/intune/setup-steps)  
 - [Avviare la migrazione da MDM ibrido a Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

> [!Note]  
> Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione. È tuttavia possibile avviare la migrazione degli utenti a Intune autonomo e quindi abilitare i dispositivi Windows 10 ad essi associati per la co-gestione. Per altre informazioni sulla migrazione a Intune autonomo, vedere [Avviare la migrazione da MDM ibrido a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Abilitare la co-gestione 
 Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione). Scegliere  **Configura la co-gestione** dalla barra multifunzione per aprire **Co-management Onboarding Wizard** (Caricamento guidato della co-gestione). 
   
1. Nella pagina **Sottoscrizione** fare clic su **Accedi**, accedere al tenant di Intune e fare clic su **Avanti**.    
2. Nella pagina **Abilitazione** scegliere l'impostazione **Automatic enrollment into Intune** (Registrazione automatica a Intune). Copiare la riga di comando per i dispositivi già registrati in Intune, se necessario. 
3. Nella pagina **Carichi di lavoro** per ogni carico di lavoro scegliere il gruppo di dispositivi da spostare per la gestione con Intune.
4. Nella pagina **Staging** selezionare una raccolta di dispositivi come **raccolta pilota**. Verificare le informazioni di **riepilogo** e completare la procedura guidata. 

### <a name="upgrade-windows-10-client"></a>Aggiornare il client Windows 10
- Eseguire l'aggiornamento a [Windows 10, versione 1709 (denominata anche Fall Creators Update) e successive](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Configurare i carichi di lavoro per passare a Intune 
L'articolo [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) illustra come passare specifici carichi di lavoro di Configuration Manager a Intune. L'articolo contiene anche le istruzioni su come modificare i gruppi di dispositivi per i carichi di lavoro che vengono passati.

- **Criteri di conformità:** i criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. È anche possibile usare tali criteri per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale. Per altre informazioni, vedere [Criteri di conformità del dispositivo in System Center Configuration Manager](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Criteri di Windows Update:** i criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende. Per altre informazioni, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Criteri di accesso alle risorse:** i criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi. Per informazioni dettagliate, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** a partire da Configuration Manager 1802, è possibile eseguire la transizione del carico di lavoro di Endpoint Protection a Intune. Per altre informazioni, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10)<!-- 1357365 --> e [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Installare il client di Configuration Manager nei dispositivi registrati in Intune
Quando i dispositivi Windows 10 sono registrati in Intune, è possibile installare il client di Configuration Manager nei dispositivi, [usando un argomento della riga di comando specifico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client), per preparare i client alla co-gestione. In seguito è possibile abilitare la co-gestione dalla console di Configuration Manager per avviare lo spostamento di carichi di lavoro specifici in Intune per alcuni dispositivi Windows 10.
Per i dispositivi Windows 10 non ancora registrati in Intune, è possibile usare la registrazione automatica in Azure per registrare i dispositivi. Per i nuovi dispositivi Windows 10, è possibile usare [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) per avviare la configurazione guidata che include la registrazione automatica dei dispositivi in Intune.
 - Abilitare [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (solo quando si usa Intune per installare il client di Configuration Manager).

## <a name="monitor-co-management"></a>Monitorare la co-gestione
[Il dashboard di co-gestione](/sccm/core/clients/manage/co-management-dashboard) consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.


## <a name="next-steps"></a>Passaggi successivi
[Preparare i dispositivi Windows 10 per la co-gestione](co-management-prepare.md)
