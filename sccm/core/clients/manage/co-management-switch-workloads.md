---
title: Passare i carichi di lavoro di Configuration Manager a Intune
titleSuffix: Configuraton Manager
description: Informazioni su come passare i carichi di lavoro attualmente gestiti da Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: ceb4004c7f4cc24ff17f0e9648cddb29cb26d898
ms.sourcegitcommit: 493cc42f05b9388ef872e466e5a75d569642b9fc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/01/2018
ms.locfileid: "34569647"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Passare i carichi di lavoro di Configuration Manager a Intune
In [Preparare i dispositivi Windows 10 per la co-gestione](co-management-prepare.md) sono stati preparati i dispositivi Windows 10 a questo scopo. Tali dispositivi sono stati aggiunti ad AD e ad Azure AD, sono stati registrati in Intune e hanno il client di Configuration Manager. È probabile che vi siano ancora dispositivi Windows 10 aggiunti ad AD e che hanno il client di Configuration Manager, ma che non sono stati aggiunti ad Azure AD o registrati in Intune. Di seguito sono riportati i passaggi per abilitare la co-gestione, preparare il resto dei dispositivi Windows 10, ovvero quelli che hanno il client di Configuration Manager ma che non sono registrati in Intune, e avviare il passaggio di specifici carichi di lavoro di Configuration Manager a Intune.

1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).    

2. Nel gruppo Gestisci della scheda Home scegliere  **Configure co-management** (Configurazione co-gestione) per aprire la procedura guidata di configurazione della co-gestione.    
3. Nella pagina della sottoscrizione fare clic su **Accedi**, accedere al tenant di Intune e fare clic su **Avanti**.   
4. Nella pagina di attivazione scegliere **Pilota** o **Tutti** per abilitare la registrazione automatica in Intune e quindi fare clic su **Avanti**. Quando si sceglie **Pilota**, vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri del gruppo pilota. Questa opzione consente di abilitare la co-gestione su un subset di client per iniziare a testarla e implementarla mediante un approccio per fasi. È possibile usare la riga di comando per distribuire il client di Configuration Manager come app in Intune per i dispositivi già registrati in Intune. Per informazioni, vedere [Dispositivi Windows 10 registrati in Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. Nella pagina Carichi di lavoro scegliere se passare i carichi di lavoro di Configuration Manager perché vengano gestiti da Intune per il gruppo pilota o da Intune e quindi fare clic su **Avanti**. L'impostazione **Pilot Intune** (Intune pilota) trasferisce il carico di lavoro associato solo per i dispositivi nel gruppo pilota. L'impostazione **Intune** trasferisce il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti. 
        
   > [!Important]    
   > Prima di trasferire qualsiasi carico di lavoro, assicurarsi che il carico di lavoro corrispondente in Intune sia stato configurato e distribuito correttamente. In questo modo, si avrà la certezza che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.   
1. Nella pagina della gestione temporanea configurare le impostazioni seguenti e fare clic su **Avanti**:
    - **Pilota**: il gruppo pilota contiene una o più raccolte selezionate. Usare il gruppo come parte dell'implementazione a fasi della co-gestione. È possibile iniziare con una raccolta di test di piccole dimensioni e quindi aggiungere più raccolte al gruppo pilota durante l'implementazione della co-gestione per più utenti e dispositivi. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento dalle proprietà della co-gestione.
    - **Produzione**: configurare il **gruppo di esclusione** con una o più raccolte. I dispositivi che sono membri di una raccolta nel gruppo vengono esclusi dalla co-gestione. 
2. Per abilitare la co-gestione, completare la procedura guidata.  

## <a name="modify-your-co-management-settings"></a>Modificare le impostazioni di co-gestione
Dopo aver abilitato la co-gestione tramite la procedura guidata, è possibile modificare le impostazioni nelle proprietà di co-gestione.  
- Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).  
Selezionare l'oggetto di co-gestione e quindi fare clic su **Proprietà** nella scheda Home. 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>Carichi di lavoro che è possibile passare a Intune
Alcuni carichi di lavoro possono essere passati a Intune. L'elenco seguente verrà aggiornato quando i carichi di lavoro diventeranno disponibili per la transizione:
1. Criteri di conformità dei dispositivi
2. Criteri di accesso alle risorse: i criteri di accesso alle risorse configurano le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati per i dispositivi. Per altre informazioni, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).
      - Profilo di posta elettronica
      - Profilo Wi-Fi
      - Profilo VPN
      - Profilo certificato
3. Criteri di Windows Update
4. Endpoint Protection (a partire da Configuration Manager versione 1802)
      - Windows Defender Application Guard
      - Windows Defender Firewall
      - Windows Defender SmartScreen
      - Crittografia di Windows
      - Windows Defender Exploit Guard
      - Controllo delle applicazioni di Windows Defender
      - Windows Defender Security Center
      - Windows Defender Advanced Threat Protection
      - Windows Information Protection
      

## <a name="monitor-co-management"></a>Monitorare la co-gestione
Dopo aver abilitato la co-gestione, è possibile monitorare i dispositivi di co-gestione usando i metodi seguenti:

- [Dashboard di co-gestione](/sccm/core/clients/manage/co-management-dashboard)
- **Visualizzazione SQL e classe WMI**: è possibile eseguire query sulla visualizzazione SQL **v&#95;ClientCoManagementState** nel database del sito di Configuration Manager o sulla classe WMI **SMS&#95;Client&#95;ComanagementState**. Con le informazioni nella classe WMI è possibile creare raccolte personalizzate in Configuration Manager per determinare lo stato della distribuzione della co-gestione. Per informazioni dettagliate, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections). Nella visualizzazione SQL e nella classe WMI sono disponibili i campi seguenti: 
    - **MachineId**: specifica un ID dispositivo univoco per il client di Configuration Manager.
    - **MDMEnrolled**: specifica se il dispositivo è registrato nella soluzione MDM. 
    - **Authority**: specifica l'autorità per cui è registrato il dispositivo.
    - **ComgmtPolicyPresent**: specifica se nel client sono presenti criteri di co-gestione di Configuration Manager. Se il valore di **MDMEnrolled** è **0**, il dispositivo non è co-gestito, indipendentemente dalla presenza o meno di criteri di co-gestione nel client.

   > [!Note]    
   > Un dispositivo è co-gestito quando i campi **MDMEnrolled** e **ComgmtPolicyPresent** sono entrambi impostati su **1**.

- **Criteri di distribuzione**: vengono creati due criteri in **Monitoraggio** > **Distribuzioni**, uno per il gruppo pilota e uno per la produzione. Questi criteri indicano solo il numero di dispositivi in cui Configuration Manager ha applicato il criterio. Non tengono conto del numero di dispositivi registrati in Intune, che è un requisito necessario prima che i dispositivi possano essere co-gestiti.  

## <a name="check-compliance-for-co-managed-devices"></a>Verificare la conformità per i dispositivi co-gestiti
Gli utenti possono usare Software Center per verificare la conformità dei dispositivi Windows 10 co-gestiti, indipendentemente dal fatto che l'accesso condizionale venga gestito da Configuration Manager o da Intune. Gli utenti possono anche verificare la conformità utilizzando l'app Portale aziendale quando l'accesso condizionale è gestito da Intune.

## <a name="next-steps"></a>Passaggi successivi
Usare le risorse seguenti per informazioni sulla gestione dei carichi di lavoro passati a Intune:
- [Criteri di conformità dei dispositivi](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Criteri di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles)
- [Criteri di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
