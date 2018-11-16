---
title: Co-gestione per dispositivi Windows 10
titleSuffix: Configuration Manager
description: Informazioni su come gestire dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 1791217e22e2bcc6d5fd2603abee3aaced816afe
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223739"
---
# <a name="co-management-for-windows-10-devices"></a>Co-gestione per dispositivi Windows 10    

Con gli aggiornamenti precedenti di Windows 10 è già possibile aggiungere un dispositivo Windows 10 ad Active Directory (AD) locale e ad Azure AD basato sul cloud allo stesso tempo (Azure AD ibrida). A partire da Configuration Manager versione 1710, la co-gestione sfrutta questo miglioramento. Consente di gestire più dispositivi Windows 10 versione 1709 contemporaneamente usando Configuration Manager e Intune. <!-- 1350871 -->


## <a name="why-co-management"></a>Perché scegliere la co-gestione

Molti clienti vogliono gestire i dispositivi Windows 10 nello stesso modo in cui gestiscono i dispositivi mobili usando una soluzione semplice, a costi contenuti e basata su cloud. Tuttavia, la transizione dalla gestione tradizionale a una gestione moderna può essere complessa.  


## <a name="what-is-co-management"></a>Informazioni sulla co-gestione

La co-gestione consente di gestire più dispositivi Windows 10 contemporaneamente usando Configuration Manager e Intune. È una soluzione che costituisce un ponte tra la gestione tradizionale e quella moderna e che consente di eseguire la transizione mediante un approccio per fasi.


## <a name="benefits"></a>Vantaggi 

Uso immediato delle funzionalità di Intune seguenti:  
 
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
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10), a partire da Configuration Manager 1802 <!-- 1357365 -->
    - [Configurazione del dispositivo](https://docs.microsoft.com/intune/device-profile-create), a partire da Configuration Manager 1806. <!-- 1357903 -->
    - [App A portata di clic di Office](https://docs.microsoft.com/intune/apps-add-office365), a partire da Configuration Manager 1806 <!--1357841-->
    - [App per dispositivi mobili](https://docs.microsoft.com/intune/app-management), a partire da Configuration Manager 1806 come funzionalità di versione non definitiva. <!--1357892-->



## <a name="how-to-configure-co-management"></a>Come configurare la co-gestione

 I percorsi principali per realizzare la co-gestione sono due:  

   - Configuration Manager effettua il provisioning della co-gestione: si registrano in Intune i dispositivi Windows 10 aggiunti ad Azure AD che sono già client Configuration Manager.  

   - Provisioning effettuato da Intune: per i dispositivi già registrati in Intune, si installa il client Configuration Manager per raggiungere uno stato di co-gestione. 


### <a name="configuration-manager"></a>Configuration Manager

 -  Eseguire l'aggiornamento a Configuration Manager 1710 o versione successiva.


### <a name="azure-active-directory"></a>Azure Active Directory

 - I dispositivi Windows 10 devono essere aggiunti ad Azure AD. Possono essere di uno dei due tipi seguenti:  

     - [Aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup), il dispositivo è aggiunto ad Active Directory locale e registrato in Azure Active Directory.

     - Aggiunto solo ad Azure AD. Questo tipo è anche noto come "aggiunto a un dominio cloud".<!--SCCMDocs issue 605-->

 - [Abilitare la registrazione automatica di Windows 10](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="intune"></a>Intune

 - [Come configurare la sottoscrizione di Intune](/sccm/mdm/deploy-use/configure-intune-subscription) o [Configurare Intune](/intune/setup-steps)  

 - [Avviare la migrazione da MDM ibrido a Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione. È tuttavia possibile avviare la migrazione degli utenti a Intune autonomo e quindi abilitare i dispositivi Windows 10 ad essi associati per la co-gestione. Per altre informazioni sulla migrazione a Intune autonomo, vedere [Avviare la migrazione da MDM ibrido a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Abilitare la co-gestione 

 > [!Important]  
 > A partire dalla versione 1802, per abilitare la co-gestione, l'account utente amministratore in Configuration Manager deve essere un **amministratore completo** con **tutti** gli ambiti di protezione. Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Fare clic su **Configura la co-gestione** nella barra multifunzione per aprire **Co-management Onboarding Wizard** (Caricamento guidato della co-gestione). 
   
1. Nella pagina **Sottoscrizione** fare clic su **Accedi**. Accedere al tenant di Intune e quindi fare clic su **Avanti**.  

    > [!Tip]   
    > Assicurarsi che all'account usato per accedere al tenant sia assegnata una licenza di Intune. In caso contrario, sarà visualizzato il messaggio di errore "Utente non riconosciuto".  

2. Nella pagina **Abilitazione** scegliere l'impostazione **Automatic enrollment into Intune** (Registrazione automatica a Intune). Copiare la riga di comando per i dispositivi già registrati in Intune, se necessario.  

    > [!Note]  
    > A partire dalla versione 1806, la registrazione automatica non è immediata per tutti i client. Questo comportamento consente una migliore scalabilità della registrazione per gli ambienti di grandi dimensioni. Configuration Manager sceglie in modo casuale la registrazione in base al numero di client. Se ad esempio la registrazione ha 100.000 client, quando si abilita questa impostazione, la registrazione viene eseguita in più giorni.<!--1358003-->  

3. Nella pagina **Carichi di lavoro** per ogni carico di lavoro scegliere il gruppo di dispositivi da spostare per la gestione con Intune.  

4. Nella pagina **Staging** selezionare una raccolta di dispositivi come **raccolta pilota**. Verificare le informazioni di **riepilogo** e completare la procedura guidata.  


### <a name="upgrade-windows-10-client"></a>Aggiornare il client Windows 10

- Eseguire l'aggiornamento a [Windows 10, versione 1709 (denominata anche Fall Creators Update) e successive](/sccm/osd/deploy-use/manage-windows-as-a-service)


### <a name="configure-workloads-to-switch-to-intune"></a>Configurare i carichi di lavoro per passare a Intune 

L'articolo [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) illustra come passare specifici carichi di lavoro di Configuration Manager a Intune. L'articolo contiene anche le istruzioni su come modificare i gruppi di dispositivi per i carichi di lavoro che vengono passati.

#### <a name="compliance-policies"></a>Criteri di conformità 
I criteri di conformità definiscono le regole e le impostazioni che un dispositivo deve avere per essere considerato conforme ai criteri di accesso condizionale. Usare tali criteri anche per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale. Per altre informazioni, vedere [Criteri di conformità del dispositivo in System Center Configuration Manager](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### <a name="windows-update-policies"></a>Criteri di Windows Update
I criteri di Windows Update per le aziende consentono di configurare i criteri di rinvio per gli aggiornamenti delle funzionalità di Windows 10 o gli aggiornamenti di qualità dei dispositivi Windows 10 gestiti direttamente da Windows Update per le aziende. Per altre informazioni, vedere [Configurare i criteri di rinvio di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### <a name="resource-access-policies"></a>Criteri di accesso alle risorse
I criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi. Per informazioni dettagliate, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).

#### <a name="endpoint-protection"></a>Endpoint Protection
A partire da Configuration Manager 1802, è possibile eseguire la transizione del carico di lavoro di Endpoint Protection a Intune. Per altre informazioni, vedere [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> e [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### <a name="device-configuration"></a>Configurazione del dispositivo
A partire da Configuration Manager 1806, è possibile eseguire la transizione del carico di lavoro di configurazione del dispositivo a Intune. Per altre informazioni, vedere [Creare un profilo di dispositivo in Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) e [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>App A portata di clic di Office
A partire da Configuration Manager 1806, è possibile eseguire la transizione del carico di lavoro di Office 365 a Intune. Per altre informazioni, vedere [Carichi di lavoro che è possibile passare a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### <a name="mobile-apps"></a>App per dispositivi mobili
A partire da Configuration Manager versione 1806, è possibile eseguire la transizione del carico di lavoro delle app per dispositivi mobili a Intune. Si tratta di una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features). Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale. Le app distribuite da Configuration Manager sono disponibili in Software Center.<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Installare il client di Configuration Manager nei dispositivi registrati in Intune

Quando i dispositivi Windows 10 sono registrati in Intune, installare il client Configuration Manager nei dispositivi, [usando una riga di comando specifica](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client), per preparare i client alla co-gestione. In seguito è possibile abilitare la co-gestione dalla console di Configuration Manager per avviare lo spostamento di carichi di lavoro specifici in Intune per alcuni dispositivi Windows 10.
Per i dispositivi Windows 10 non ancora registrati in Intune, usare la registrazione automatica in Azure per registrare i dispositivi. Per i nuovi dispositivi Windows 10, usare [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) per avviare la configurazione guidata che include la registrazione automatica dei dispositivi in Intune.

Quando si usa Intune per installare il client Configuration Manager, abilitare un [gateway di gestione cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager.



## <a name="monitor-co-management"></a>Monitorare la co-gestione

[Il dashboard di co-gestione](/sccm/core/clients/manage/co-management-dashboard) consente di esaminare i computer co-gestiti presenti nell'ambiente. I grafici consentono di identificare i dispositivi che potrebbero richiedere attenzione.



## <a name="next-steps"></a>Passaggi successivi

[Preparare i dispositivi Windows 10 per la co-gestione](co-management-prepare.md)
