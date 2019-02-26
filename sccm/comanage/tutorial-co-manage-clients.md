---
title: Esercitazione&#58; percorso di CO-gestione 1
titleSuffix: Configuration Manager
description: Configurare la co-gestione con Microsoft Intune quando già si gestiscono i dispositivi Windows 10 con Configuration Manager.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aecb2c33c874717f1da979f1316d1b46b785071
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755262"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Esercitazione: Abilitare la co-gestione per i client di Configuration Manager esistente
Con CO-gestione, è possibile mantenere i processi consolidati per l'uso di Configuration Manager per gestire i PC dell'organizzazione. Allo stesso tempo, sta impegnati a investire nel cloud tramite l'uso di Intune per la sicurezza e provisioning moderne.  

In questa esercitazione, è impostata la co-gestione dei dispositivi Windows 10 che sono già registrati in Configuration Manager. Questa esercitazione inizia con il presupposto che usi già Configuration Manager per gestire i dispositivi Windows 10.

Usare questa esercitazione quando:  

- Si dispone di un Active Directory in locale che sia possibile connettersi ad Azure Active Directory (Azure AD) in una configurazione ibrida di Azure AD
- Si dispone di client Configuration Manager esistente che si desidera collegare al cloud


**In questa esercitazione si apprenderà come:**  
> [!div class="checklist"]  
> * Esaminare i prerequisiti per Azure e l'ambiente locale  
> * Configurare Azure AD ibrido  
> * Configurare gli agenti client di Configuration Manager da registrare con Azure AD  
> * Configurare Intune per registrare automaticamente i dispositivi  
> * Assegnare le licenze Intune agli utenti  
> * Abilitare la co-gestione in Configuration Manager  


## <a name="prerequisites"></a>Prerequisiti  

### <a name="azure-services-and-environment"></a>Ambiente e servizi di azure
- Sottoscrizione di Azure ([versione di valutazione gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Sottoscrizione di Microsoft Intune
  > [!TIP]  
  > Un Enterprise Mobility + Security (EMS) sottoscrizione include Azure Active Directory Premium e Microsoft Intune. Sottoscrizione di EMS ([versione di valutazione gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Se non è già presente nel proprio ambiente, durante questa esercitazione sarà:
- Assegnare una licenza per gli utenti *Intune* e per *Azure Active Directory Premium*
- Configurare [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) tra Active Directory in locale e di Azure Active Directory (AD) del tenant


### <a name="on-premises-infrastructure"></a>Infrastruttura locale
- Oggetto [versione supportata](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) di System Center Configuration Manager current branch
- Il [autorità MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) deve essere impostata su Intune  


### <a name="permissions"></a>Autorizzazioni
In questa esercitazione, usare le autorizzazioni seguenti per completare le attività:  
- Un account che sia un *amministratore globale* in Azure  
- Un account che sia un *amministratore di dominio* sulla tua infrastruttura locale  
- Un account che sia un *amministratore completo* per *tutte* ambiti in Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configurare Azure AD ibrido
Quando si configura un'identità ibrida di Azure AD, si sta effettivamente configurando l'integrazione di un'infrastruttura Active Directory con Azure AD usando Azure AD Connect e Active Directory Federated Services (ADFS). Con la configurazione, i ruoli di lavoro possono facilmente accedere a sistemi esterni usando locale le credenziali di Active Directory.

> [!IMPORTANT]  
> Questa esercitazione illustra in dettaglio un processo pressoché essenziale per impostare le identità ibrida di Azure AD per un dominio gestito. È consigliabile avere dimestichezza con il processo e non fare affidamento su questa esercitazione come guida alla comprensione e la distribuzione ibrida di Azure AD.
>
> Per altre informazioni sull'identità ibrida di Azure AD, iniziare con gli articoli seguenti nella documentazione di Azure Active Directory:
> - [Pianificare l'implementazione di join Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Pianificare l'implementazione di join Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Controllare il join Azure AD ibrida dei dispositivi](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurare aggiunta ad Azure AD ibrido per i domini federati](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurare Azure AD Connect  
Identità ibrida di Azure AD richiede la configurazione di Azure AD Connect per sincronizzare gli account computer in locale Active Directory (AD) e l'oggetto dispositivo in Azure AD.

A partire dalla versione 1.1.819.0, Azure AD Connect offre una procedura guidata per configurare l'aggiunta ad Azure AD ibrido. Uso della procedura guidata semplifica il processo di configurazione.  

Per configurare Azure AD Connect, sono necessarie le credenziali di amministratore globale per il tenant di Azure AD.  

> [!TIP]  
> La procedura seguente non deve essere considerata attendibile per set di backup di Azure AD Connect, ma è disponibile qui per semplificare la configurazione della co-gestione tra Intune e Configuration Manager. Per il contenuto autorevole su questo e sulle procedure correlate per set di backup di Azure AD, vedere [configura l'aggiunta ad Azure AD ibrido per i domini gestiti](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) nella documentazione di Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurare un'aggiunta ad Azure AD ibrido con Azure AD Connect

1. Ottenere e installare il [versione più recente di Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o versione successiva).  
2. Avviare Azure AD Connect e quindi selezionare **configura**.
3. Nel **attività aggiuntive** pagina, selezionare **configurare le opzioni di dispositivo**e quindi selezionare **Next**.
4. Nel **Overview** pagina, selezionare **successivo**.
5. Nel **ad Azure AD Connect** pagina, immettere le credenziali di amministratore globale per il tenant di Azure AD.
6. Nel **opzioni di dispositivi** pagina, selezionare **aggiunta all'identità ibrida Configura Azure AD**e quindi selezionare **Avanti**.
7. Nel **SCP** pagina, per ogni foresta locale si vuole che Azure AD Connect per configurare il punto di connessione del servizio (SCP), seguire questa procedura e quindi selezionare **successivo**:  
   1. Selezionare la foresta.  
   2. Selezionare il servizio di autenticazione.  Se si dispone di un dominio federato, selezionare i server AD FS, a meno che l'organizzazione dispone esclusivamente i client Windows 10 e aver configurato sincronizzazione computer/dispositivo o l'organizzazione Usa [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Fare clic su **Add** immettere le credenziali di amministratore dell'organizzazione.  
8. Nel **sistemi operativi dei dispositivi** pagina, selezionare i sistemi operativi usati dai dispositivi nell'ambiente Active Directory e quindi selezionare **successivo**.  

   È possibile selezionare l'opzione per supportare i dispositivi Windows di livello inferiore aggiunti a un dominio, ma tenere presente che la co-gestione dei dispositivi è supportata solo per Windows 10.

9. Se si dispone di un dominio gestito, ignorare questo passaggio.  

   Nel **configurazione della federazione** pagina, immettere le credenziali dell'amministratore di AD FS e quindi selezionare **successivo**.
10. Nel **pronti per configurare** pagina, selezionare **configura**.
11. Nel **configurazione completata** pagina, selezionare **uscita**.

Se si verificano problemi con il completamento di identità ibrida di Azure AD join per dominio dispositivi aggiunti all'identità Windows, vedere [risoluzione dei problemi l'aggiunta ad Azure AD ibrido per i dispositivi correnti di Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configurare le impostazioni Client per indirizzare i client registrano in Azure AD  
Usare le impostazioni Client per configurare i client di Configuration Manager per la registrazione automatica con Azure AD.  

1. Aprire il **console di Configuration Manager** > **amministrazione** > **Panoramica** > **impostazioni Client** , quindi modificare il **impostazioni Client predefinite**.  

2. Selezionare **servizi Cloud**.  

3. Nel **impostazioni predefinite** pagina, impostare **automaticamente registrare nuovi dispositivi aggiunti a un dominio di Windows 10 con Azure Active Directory** a = **Sì**.  

4. Selezionare **OK** per salvare la configurazione.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurare la registrazione automatica dei dispositivi in Intune   
Successivamente, verrà configurato la registrazione automatica dei dispositivi con Intune. Con la registrazione automatica, i dispositivi gestiti con Configuration Manager automaticamente registrati con Intune.

La registrazione automatica consente inoltre agli utenti di registrare i propri dispositivi Windows 10 in Intune. I dispositivi registrati quando un utente aggiunge l'account aziendale nel dispositivo di proprietà personale o quando un dispositivo aziendali è stato aggiunto ad Azure Active Directory.  

1. Accedi per il [portale di Azure](https://portal.azure.com/) e selezionare **Azure Active Directory** > **servizi Mobility (MDM e MAM)** > **Microsoft Intune** .  

2. Configurare **ambito utente MDM**. Specificare uno dei modi seguenti per configurare i dispositivi degli utenti che sono gestiti da Microsoft Intune e accettare le impostazioni predefinite per i valori di URL.  

   - **Alcuni** : selezionare il **gruppi** che possono registrare automaticamente i dispositivi Windows 10  

   - **Tutti i** -tutti gli utenti possono registrare automaticamente i dispositivi Windows 10 quando impostati su **None**, la registrazione automatica di gestione dei dispositivi mobili (MDM) è disabilitata

   > [!IMPORTANT]  
   > Se entrambe **ambito utente MAM** e la registrazione MDM automatica (**ambito utente MDM**) sono abilitate per un gruppo, è attivato solo MAM. Viene aggiunto solo Mobile Application Management (MAM) per gli utenti in tale gruppo quando essi dispositivo personale all'area di lavoro. I dispositivi non sono automaticamente registrati MDM.  

3. Selezionare **salvare** per completare la configurazione della registrazione automatica.  

4. Tornare alla **servizi Mobility (MDM e MAM)** e quindi selezionare **registrazione di Microsoft Intune**.  

5. Per ambito utente MDM, selezionare **tutte**e quindi **salvare**.  


## <a name="assign-intune-licenses-to-users"></a>Assegnare le licenze Intune agli utenti   
Un'azione in genere trascurata ma critica consiste nell'assegnare una licenza di Intune a ogni utente che userà un dispositivo è CO-gestito.  

Per assegnare licenze a gruppi di utenti, usare Azure Active Directory.  

1. Accedi per il [portale di Azure](https://portal.azure.com/) con un account amministratore. Per gestire le licenze, l'account deve essere un amministratore dell'account utente o ruolo amministratore globale.  

2. Selezionare **tutti i servizi** nel riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**.  

3. Nel **Azure Active Directory** riquadro, selezionare **licenze** per aprire un riquadro in cui è possibile visualizzare e gestire tutti i prodotti con contratto multilicenza del tenant.  

4. Sotto **All products**, selezionare l'opzione di prodotto che include la licenza di Intune e quindi selezionare **assegnare** nella parte superiore del riquadro.  

   Ad esempio, è possibile selezionare **Enterprise Mobility + Security E5** se questo è il modo in cui ottenere Intune.  

5. Nel **assegna licenza** riquadro, fare clic su **utenti e gruppi** per aprire il **utenti e gruppi** riquadro. Selezionare i gruppi e singoli utenti a cui si vuole assegnare una licenza.  Fare quindi clic **seleziona** nella parte inferiore del riquadro per confermare che la selezione.  

6. Nel **assegna licenza** riquadro, fare clic su **opzioni di assegnazione** per visualizzare tutti i piani di servizio inclusi nel prodotto selezionato in precedenza. Se è stato selezionato un unico prodotto, ad esempio Intune, viene visualizzato solo quel prodotto.  
   - Impostare **Microsoft Intune** al **su**.  
   - Assegnare una licenza per ogni utente **Azure Active Directory Premium**.  

   Quando vengono assegnate le licenze applicabile, selezionare **OK**.  

7. Completamento dell'assegnazione, il **assegna licenza** riquadro, fare clic su **assegnare** nella parte inferiore del riquadro.

8. Viene visualizzata una notifica nell'angolo superiore destro che mostra lo stato e il risultato del processo. Se non è stato possibile completare l'assegnazione al gruppo (ad esempio, a causa di licenze già esistenti nel gruppo), fare clic sulla notifica per visualizzare i dettagli dell'errore.

Per altre informazioni sull'assegnazione delle licenze di Intune agli utenti, vedere [assegnare le licenze](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Abilitare la co-gestione in Configuration Manager
Con hybrid Azure AD di configurazione, le configurazioni client di Configuration Manager, e le licenze di prodotto assegnate agli utenti, si è pronti per disattivare l'opzione e abilitare la co-gestione dei dispositivi Windows 10.  

> [!TIP]  
>  Nel passaggio 6 della procedura seguente, è possibile assegnare una raccolta come un *gruppo pilota* per la co-gestione. Si tratta di un gruppo che contiene un numero limitato di client per testare le configurazioni di CO-gestione. Si consiglia di che creare una raccolta appropriata prima di avviare la procedura. È possibile selezionare tale raccolta senza chiudere la procedura per eseguire questa operazione.  

1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).

2. Nella scheda Home, nel gruppo di gestione, selezionare **configurare la co-gestione** per aprire la procedura guidata configurazione CO-gestione.

3. Nella pagina di sottoscrizione, selezionare **Sign In** e accedere al tenant di Intune e quindi selezionare **successivo**.

4. Nella pagina di attivazione dal *registrazione automatica in Intune* dall'elenco a discesa selezionare una delle opzioni seguenti:  

   - **Progetto pilota**  - *(scelta consigliata)* membri della raccolta è specificare automaticamente registrati in Intune e possono quindi essere co-gestiti. Specificare la raccolta pilota nel *Staging* pagina della procedura guidata. Questa opzione consente di testare CO-gestione su un subset di client. È quindi possibile eseguire il roll la co-gestione ai client aggiuntivi usando un approccio per fasi.  

   - **Tutti i** -CO-gestione è abilitato per tutti i client.  

5. Nella pagina carichi di lavoro è possibile passare i carichi di lavoro dalla **Configuration Manager** a uno dei seguenti, quindi quando si è pronti per continuare, selezionare **successivo**.  

   - **Avviare un programma pilota di Intune** -trasferisce un carico di lavoro solo per i dispositivi nel gruppo pilota. È possibile assegnare una raccolta come il gruppo pilota nella pagina successiva della procedura guidata.  

   - **Intune** -trasferisce il carico di lavoro associato per tutti i dispositivi Windows 10 CO-gestiti.  

   Non è necessario passare i carichi di lavoro in fase di che aver abilitato la co-gestione. È possibile modificare questa configurazione dalla console di Configuration Manager in un secondo momento, dopo aver configurato CO-gestione.  

   Prima di passare un carico di lavoro, assicurarsi che il carico di lavoro corrispondente in Intune viene configurato e distribuito. In questo modo, viene mantenuto in tal caso i carichi di lavoro gestiti.  

6. Nella pagina della gestione temporanea, specificare una raccolta da usare per la **raccolta pilota**, quindi fare clic su **successivo**. La raccolta specificata è parte integrante dell'implementazione a fasi della co-gestione. È possibile modificare le raccolte del gruppo pilota in qualsiasi momento dalle proprietà della co-gestione.  

7. Nella pagina di riepilogo, selezionare **successivo**e quindi **Chiudi** per completare la procedura guidata.  


## <a name="next-steps"></a>Passaggi successivi
- Esaminare lo stato di dispositivi CO-gestiti con il [dashboard di CO-gestione](/sccm/comanage/how-to-monitor)
- Iniziare a ottenere [valore immediato](quickstarts.md#immediate-value) dalla co-gestione
- Uso [accesso condizionale](quickstart-conditional-access.md) e regole di conformità di Intune per gestire l'accesso utente alle risorse aziendali
