---
title: Passare i carichi di lavoro di Configuration Manager a Intune
titleSuffix: Configuration Manager
description: Informazioni su come passare i carichi di lavoro attualmente gestiti da Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: e3bd3bfda92fb877bac3ca68dbecf8b4a4078d4d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416946"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Passare i carichi di lavoro di Configuration Manager a Intune

Dopo aver [preparato i dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare), il passaggio successivo prevede l'abilitazione della registrazione automatica del client in Intune. Quando si è pronti, avviare quindi il passaggio di specifici carichi di lavoro di Configuration Manager a Intune. 


## <a name="setup-co-management"></a>Configurare la co-gestione

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Gestisci** scegliere  **Configura la co-gestione**. Questa azione apre la Configurazione guidata della co-gestione.  

3. Nella pagina Sottoscrizione fare clic su **Accedi**. Accedere al tenant di Intune e quindi selezionare **Avanti**.  

4. Nella pagina Abilitazione scegliere **Pilota** o **Tutti**.  

    Questa azione abilita la registrazione automatica del client in Intune. Quando si sceglie **Pilota**, vengono registrati automaticamente in Intune solo i client di Configuration Manager che sono membri della raccolta pilota. Questa opzione consente di abilitare la co-gestione su un subset di client per iniziare a testarla e implementarla mediante un approccio per fasi.  

    Usare la riga di comando visualizzata per distribuire il client di Configuration Manager come app in Intune per i dispositivi già registrati in Intune. Per altre informazioni, vedere [Dispositivi Windows 10 registrati in Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. Nella pagina dei carichi di lavoro scegliere se passare i carichi di lavoro di Configuration Manager a Intune. È possibile abilitare la registrazione nella pagina precedente senza trasferire i carichi di lavoro in questa fase. 

    L'impostazione **Intune pilota** trasferisce il carico di lavoro associato solo per i dispositivi nella raccolta pilota. L'impostazione **Intune** trasferisce il carico di lavoro associato per tutti i dispositivi Windows 10 co-gestiti.  

    > [!Important] 
    > Prima di trasferire qualsiasi carico di lavoro, assicurarsi di configurare e distribuire correttamente il carico di lavoro corrispondente in Intune. Verificare che i carichi di lavoro siano sempre gestiti da uno degli strumenti di gestione per i dispositivi.  

6. Nella pagina Gestione temporanea è possibile configurare le impostazioni seguenti:  

    - **Pilota**: il gruppo pilota contiene una o più raccolte selezionate. Usare il gruppo come parte dell'implementazione a fasi della co-gestione. Iniziare con una raccolta di test di piccole dimensioni e quindi aggiungere più raccolte al gruppo pilota durante l'implementazione della co-gestione per più utenti e dispositivi. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento.  

    - **Production**: Configurare **Exclusion group** (Gruppo di esclusione) con una o più raccolte. I dispositivi che sono membri di una raccolta nel gruppo vengono esclusi dalla co-gestione.  

7. Per abilitare la co-gestione, completare la procedura guidata.  

<!--1357377--> A partire da Configuration Manager versione 1806, quando si passa a un altro carico di lavoro con co-gestione, i dispositivi in co-gestione sincronizzano automaticamente i criteri MDM da Microsoft Intune. La sincronizzazione si verifica anche quando si avvia l'azione **Scarica criteri computer** dalle notifiche client nella console di Configuration Manager. Per altre informazioni, vedere [Avviare il recupero dei criteri client usando la notifica client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="modify-your-co-management-settings"></a>Modificare le impostazioni di co-gestione

Dopo aver abilitato la co-gestione tramite la procedura guidata, modificare le impostazioni nelle proprietà di co-gestione. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**. Selezionare l'oggetto co-gestione e quindi selezionare **Proprietà** nella barra multifunzione. 



## <a name="supported-workloads"></a>Carichi di lavoro supportati

I carichi di lavoro seguenti sono attualmente disponibili per il passaggio da Configuration Manager a Intune:

- **Criteri di conformità dei dispositivi**  

- **Criteri di accesso alle risorse**: per altre informazioni su questi criteri di Intune, vedere [Distribuire profili di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles).
    - Profilo di posta elettronica  
    - Profilo Wi-Fi  
    - Profilo VPN  
    - Profilo certificato  

- **Criteri di Windows Update**  

- **Endpoint Protection**: a partire da Configuration Manager versione 1802, questo carico di lavoro include le funzionalità seguenti:  
    - Windows Defender Application Guard  
    - Windows Defender Firewall  
    - Windows Defender SmartScreen  
    - Crittografia di Windows  
    - Windows Defender Exploit Guard  
    - Controllo delle applicazioni di Windows Defender  
    - Windows Defender Security Center  
    - Windows Defender Advanced Threat Protection  
    - Windows Information Protection  

- **Configurazione del dispositivo**: a partire da Configuration Manager versione 1806<!--1357903-->:  

    - Lo spostamento del carico di lavoro di configurazione del dispositivo comporta anche lo spostamento dei carichi di lavoro **Accesso alla risorsa** ed **Endpoint Protection**  

    - È comunque possibile continuare a distribuire le impostazioni da Configuration Manager ai dispositivi con co-gestione, anche se Intune è l'autorità di configurazione del dispositivo. Questa eccezione può essere usata per configurare le impostazioni richieste dall'organizzazione, ma non ancora disponibili in Intune. Specificare questa eccezione in una [linea di base di configurazione di Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Abilitare l'opzione per **applicare sempre la linea di base anche per i client con co-gestione** quando si crea la linea di base o nella scheda **Generale** delle proprietà di una linea di base esistente.  

- **App A portata di clic di Office 365**: a partire da Configuration Manager versione 1806<!--1357841-->:  

    - Dopo lo spostamento del carico di lavoro, l'app viene visualizzata nel **portale aziendale** sul dispositivo  

    - Gli aggiornamenti di Office possono richiedere circa 24 ore prima di essere visualizzati nei client, a meno che i dispositivi non vengano riavviati  

    - È disponibile una nuova condizione globale che determina se **le applicazioni di Office 365 sono gestite da Intune nel dispositivo**. Questa condizione viene aggiunta per impostazione predefinita come requisito alle nuove applicazioni di Office 365. Durante la transizione di questo carico di lavoro, i client in co-gestione non soddisfano il requisito relativo all'applicazione. Non installano quindi Office 365 distribuito da Configuration Manager.  

- **App client**: a partire da Configuration Manager versione 1806 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features)<!--1357892-->:  

    - Dopo la transizione di questo carico di lavoro, qualsiasi app disponibile distribuita da Intune sarà disponibile nel portale aziendale  

    - Le app distribuite da Configuration Manager sono disponibili in Software Center  



## <a name="monitor-co-management"></a>Monitorare la co-gestione

Dopo aver abilitato la co-gestione, monitorare i dispositivi di co-gestione usando i metodi seguenti:

- [Dashboard di co-gestione](/sccm/core/clients/manage/co-management-dashboard)  

- **Visualizzazione SQL e classe WMI**: eseguire query sulla visualizzazione SQL **v_ClientCoManagementState** nel database del sito di Configuration Manager o sulla classe WMI **SMS_Client_ComanagementState**. Con le informazioni nella classe WMI è possibile creare raccolte personalizzate in Configuration Manager per determinare lo stato della distribuzione della co-gestione. Per informazioni dettagliate, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections). Nella visualizzazione SQL e nella classe WMI sono disponibili i campi seguenti:  
  - **MachineId**: specifica un ID dispositivo univoco per il client di Configuration Manager  
  - **MDMEnrolled**: specifica se il dispositivo è registrato nella soluzione MDM  
  - **Authority**: specifica l'autorità per cui è registrato il dispositivo  
  - **ComgmtPolicyPresent**: specifica se nel client sono presenti criteri di co-gestione di Configuration Manager. Se il valore di **MDMEnrolled** è **0**, il dispositivo non è co-gestito, indipendentemente dalla presenza o meno di criteri di co-gestione nel client.  

    > [!Note]  
    > Un dispositivo è co-gestito quando i campi **MDMEnrolled** e **ComgmtPolicyPresent** sono entrambi impostati su **1**.  

- **Criteri di distribuzione**: vengono creati due criteri nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Un criterio è per il gruppo pilota e uno per la produzione. Questi criteri segnalano solo il numero di dispositivi in cui Configuration Manager ha applicato il criterio. Non tengono conto del numero di dispositivi registrati in Intune, che è un requisito necessario prima che i dispositivi possano essere co-gestiti.  



## <a name="check-compliance-for-co-managed-devices"></a>Verificare la conformità per i dispositivi co-gestiti

Gli utenti possono usare Software Center per verificare la conformità dei dispositivi Windows 10 co-gestiti, indipendentemente dal fatto che l'accesso condizionale venga gestito da Configuration Manager o da Intune. Gli utenti possono anche verificare la conformità utilizzando l'app Portale aziendale quando l'accesso condizionale è gestito da Intune.



## <a name="next-steps"></a>Passaggi successivi

Usare le risorse seguenti per informazioni sulla gestione dei carichi di lavoro passati a Intune:
- [Criteri di conformità dei dispositivi](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Criteri di accesso alle risorse](https://docs.microsoft.com/intune/device-profiles)
- [Criteri di Windows Update per le aziende](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection per Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
