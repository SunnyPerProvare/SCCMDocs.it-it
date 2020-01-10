---
title: Gestire l'accesso alla posta elettronica
titleSuffix: Configuration Manager
description: Informazioni su come usare Configuration Manager l'accesso condizionale per gestire l'accesso alla posta elettronica di Exchange.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cae842c5da715d513630b24be98a00138ce9efad
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75821784"
---
# <a name="manage-email-access-in-configuration-manager"></a>Gestire l'accesso alla posta elettronica in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare Configuration Manager accesso condizionale per gestire l'accesso alla posta elettronica di Exchange in base alle condizioni specificate.  

È possibile gestire l'accesso a:  

- Microsoft Exchange locale  

- Microsoft Exchange Online  

- Exchange Online dedicato  

È possibile controllare l'accesso a Exchange Online ed Exchange locale dal client di posta elettronica predefinito nelle seguenti piattaforme:  

- Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive  

- iOS 9.0 e versioni successive  

- Windows Phone 8.1 e versioni successive  

- Applicazione di posta elettronica in Windows 8.1 e versioni successive  

Le applicazione desktop di Office possono accedere a Exchange Online nei PC che eseguono:  

- La versione desktop di Office 2013 e versioni successive con [autenticazione moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) attiva.  

- Windows 7.0 o Windows 8.1  

> [!NOTE]  
> I PC devono essere aggiunti a un dominio o essere conformi ai criteri impostati in Intune.  


## <a name="device-requirements"></a>Requisiti dei dispositivi
Se si configura l'accesso condizionale, prima che un utente possa connettersi alla posta elettronica, il dispositivo in uso:  

- Deve essere registrato in Intune o essere un PC aggiunto a un dominio.  

- Deve essere registrato in Azure Active Directory. La registrazione viene eseguita automaticamente quando il dispositivo è registrato in Intune (solo per Exchange Online). Inoltre, l'ID di Exchange ActiveSync del client deve essere registrato con Azure Active Directory (non applicabile a dispositivi Windows e Windows Phone collegati a Exchange in locale).  

    Per un PC aggiunto a un dominio, è necessario impostarlo in modo che venga registrato automaticamente con Azure Active Directory. La sezione **accesso condizionale per i PC** nell'articolo [gestire l'accesso ai servizi](../../protect/deploy-use/manage-access-to-services.md) elenca il set completo di requisiti per abilitare l'accesso condizionale per i PC.  

- Deve essere compatibile con i criteri di compatibilità di Configuration Manager distribuiti nel dispositivo  

    Se non viene soddisfatta una condizione di accesso condizionale, viene visualizzato uno dei messaggi seguenti quando l'utente esegue l'accesso:  

- Se il dispositivo non è registrato con Intune oppure non è registrato in Azure Active Directory, viene visualizzato un messaggio con le istruzioni su come installare l'app portale aziendale, registrare il dispositivo e, per i dispositivi Android e iOS, attivare la posta elettronica, che associa il ID Exchange ActiveSync del dispositivo con il record del dispositivo in Azure Active Directory.  

- Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al portale Web di Intune dove sono reperibili informazioni sul problema e su come risolverlo.  

#### <a name="for-mobile-devices"></a>Per i dispositivi mobili

È possibile limitare l'accesso a **Outlook Web Access (OWA)** in Exchange Online quando si accede da un browser in dispositivi **iOS** e **Android**. L'accesso verrà consentito solo dai browser supportati su dispositivi conformi:  

- Safari (iOS)  
- Chrome (Android)  
- Managed Browser (iOS e Android)  

I browser non supportati verranno bloccati. Le app OWA per iOS e Android non sono supportate. Devono essere bloccate usando le regole delle attestazioni ADFS:  

- Configurare le regole delle attestazioni ADFS per bloccare i protocolli di autenticazione non moderni. Le istruzioni dettagliate sono disponibili nello scenario 3 per [bloccare l'accesso a Office 365 ad eccezione delle applicazioni basate su browser](https://technet.microsoft.com/library/dn592182.aspx).  

#### <a name="for-pcs"></a>Per i PC

- Se il requisito dei criteri di accesso condizionale prevede che siano consentiti dispositivi **aggiunti a un dominio** o **conformi**, viene visualizzato un messaggio con istruzioni su come registrare il dispositivo. Se il PC non soddisfa alcun requisito, all'utente verrà richiesto di registrare il dispositivo in Intune.  

- Se i requisiti del criterio di accesso condizionale è impostato in modo da consentire solo dispositivi Windows aggiunti a un dominio, il dispositivo viene bloccato e viene visualizzato un messaggio che indica all'utente di contattare l'amministratore IT.  

È possibile bloccare l'accesso alla posta elettronica di Exchange dal client di posta elettronica Exchange ActiveSync integrato dei dispositivi sulle piattaforme seguenti:  

- Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive  

- iOS 9.0 e versioni successive  

- Windows Phone 8.1 e versioni successive  

- L'applicazione **Posta elettronica** su Windows 8.1 e versioni successive  

L'app Outlook per iOS e Android e la versione desktop di Outlook 2013 e versioni successive sono supportate solo per Exchange Online.  

**Exchange Connector locale** tra Configuration Manager ed Exchange è necessario per il funzionamento dell'accesso condizionale.  

È possibile configurare un criterio di accesso condizionale per Exchange locale dalla console di Configuration Manager. Quando si configura un criterio di accesso condizionale per Exchange Online, è possibile iniziare il processo nella console di Configuration Manager che avvia la console di Intune dove è possibile completare il processo.  



## <a name="configure-conditional-access"></a>Configurare l'accesso condizionale

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Passaggio 1: Valutare l'effetto dei criteri di accesso condizionale  

Dopo la configurazione di **on-premises Exchange Connector**, è possibile usare il report Configuration Manager **elenco di dispositivi per stato di accesso condizionale** per identificare i dispositivi a cui verrà impedito l'accesso a Exchange dopo aver configurato i criteri di accesso condizionale. Questo report richiede inoltre:  

- Una sottoscrizione a Intune  

- Il punto di connessione del servizio deve essere configurato e distribuito  

Nei parametri del report selezionare il gruppo Intune da valutare e, se necessario, le piattaforme del dispositivo a cui si vuole applicare i criteri.  

Per altre su come eseguire i report, vedere [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).  

Dopo aver eseguito il report, esaminare le quattro colonne seguenti per determinare se un utente verrà bloccato:  

- **Canale di gestione**: il dispositivo è gestito da Intune, Exchange ActiveSync o entrambi.  

- **Registrato con AAD**: il dispositivo è registrato con Azure Active Directory, noto come aggiunta all'area di lavoro.  

- **Conforme**: il dispositivo è conforme ai criteri di conformità distribuiti.  

- **Attivato da EAS**: i dispositivi iOS e Android devono avere un ID Exchange ActiveSync associato al record di registrazione del dispositivo in Azure Active Directory. Ciò si verifica quando l'utente fa clic sul link **Attiva posta elettronica** nell'e-mail in quarantena.  

    > [!NOTE]  
    > Per i dispositivi Windows Phone un valore viene sempre visualizzato in questa colonna.  

L'accesso ad Exchange da parte dei dispositivi che appartengono a un gruppo di destinazione o a una raccolta verrà bloccato a meno che i valori delle colonne non corrispondano a quelli elencati nella tabella seguente:  

|Canale di gestione|AAD registrato|conformi|Attivato da EAS|Azione risultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Gestito da Microsoft Intune ed Exchange ActiveSync**|sì|sì|Viene visualizzato**Sì** o **No**|Accesso alla posta elettronica consentito|  
|Qualsiasi altro valore|No|No|Non viene visualizzato alcun valore|Accesso alla posta elettronica bloccato|  

È possibile esportare il contenuto del report e usare la colonna **Indirizzo di posta elettronica** per informare gli utenti che verranno bloccati.  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Passaggio 2: Configurare gruppi di utenti o raccolte per i criteri di accesso condizionale  

I criteri di accesso condizionale sono destinati a diversi gruppi o raccolte di utenti in base ai tipi di criteri. Questi gruppi contengono gli utenti a cui saranno destinati i criteri o che ne saranno esenti. Quando a un utente viene destinato un criterio, ogni dispositivo in uso deve essere conforme per accedere alla posta elettronica.  

- **Per i criteri di Exchange Online**: per Azure Active Directory gruppi di utenti di sicurezza. È possibile configurare questi gruppi nel **centro di amministrazione Microsoft 365**o nel portale per gli **account di Intune**.  

- **Per i criteri di Exchange locale**: per Configuration Manager le raccolte utenti. È possibile configurarli nell'area di lavoro **Asset e conformità** .  

È possibile specificare due tipi di gruppi in ogni criterio:  

- **Gruppi di destinazione**: gruppi o raccolte di utenti a cui sono applicati i criteri  

- **Gruppi esentati**: gruppi o raccolte di utenti che sono esentati dai criteri (facoltativo)  

Se un utente si trova in entrambi i gruppi, sarà esentato dai criteri.  

Solo i gruppi o le raccolte che sono considerati come destinazione dei criteri di accesso condizionale vengono valutati per l'accesso di Exchange.  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Passaggio 3: Configurare e distribuire i criteri di conformità  

Assicurarsi di aver creato e distribuito i criteri di conformità per tutti i dispositivi a cui saranno destinati i criteri di accesso condizionale di Exchange.  

Per informazioni dettagliate su come configurare i criteri di conformità, vedere [Gestire i criteri di conformità del dispositivo](device-compliance-policies.md).  

> [!IMPORTANT]  
> Se non sono stati distribuiti criteri di conformità e abilitati i criteri di accesso condizionale di Exchange, a tutti i dispositivi di destinazione verrà consentito l'accesso.  


### <a name="step-4-configure-the-conditional-access-policy"></a>Passaggio 4: Configurare i criteri di accesso condizionale  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Per Exchange Online (e i tenant nel nuovo ambiente Exchange Online dedicato)

> [!NOTE]  
> È possibile creare i criteri di accesso condizionale anche nella console di gestione di Azure AD. La console di gestione di Azure AD consente di creare i criteri di accesso condizionale dei dispositivi Intune (chiamati criteri di accesso condizionale basati su dispositivo in Azure AD) oltre ad altri criteri di accesso condizionale come Multi-Factor Authentication. È anche possibile impostare criteri di accesso condizionale per app aziendali di terze parti supportate da Azure AD, ad esempio Salesforce e Box. Per altre informazioni, vedere [procedura: richiedere i dispositivi gestiti per l'accesso alle app cloud con accesso condizionale](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

Il flusso seguente viene usato dai criteri di accesso condizionale per fare in modo che Exchange Online valuti se consentire o bloccare i dispositivi.  

![Flusso di accesso condizionale](media/ConditionalAccess8-1.png)  

Per accedere alla posta elettronica, il dispositivo:  

- Essere registrato con Intune  

- I PC devono essere aggiunti a un dominio o registrati e conformi ai criteri impostati in Intune  

- Registrare il dispositivo in Azure AD. Ciò avviene automaticamente quando il dispositivo è registrato in Intune. Per i PC aggiunti a un dominio, è necessario configurarlo in modo che [registri automaticamente il dispositivo](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps) con Azure ad.  

- Deve avere la posta elettronica attivata che associa l'ID Exchange ActiveSync del dispositivo al record del dispositivo in Azure Active Directory (si applica solo a dispositivi iOS e Android).  

- Deve essere compatibile con i criteri di compatibilità distribuiti  

Lo stato del dispositivo viene archiviato in Azure Active Directory che consente o blocca l'accesso alla posta elettronica, in base a condizioni valutate.  

Se non viene soddisfatta una condizione, viene visualizzato uno dei messaggi seguenti quando l'utente esegue l'accesso:  

- Se il dispositivo non è registrato o è registrato in Azure AD, viene visualizzato un messaggio con le istruzioni su come installare l'app portale aziendale ed eseguire la registrazione  

- Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al sito Web Portale aziendale Intune o all'app Portale aziendale dove possono trovare informazioni sul problema e su come risolverlo.  

- Per un PC:  

    - Se i criteri sono impostati in modo da richiedere l'aggiunta a un dominio e il PC non è aggiunto a un dominio, viene visualizzato un messaggio per contattare l'amministratore IT.  

    - Se i criteri sono impostati in modo da richiedere l'aggiunta a un dominio o la conformità e il PC non soddisfa questi requisiti, viene visualizzato un messaggio con le istruzioni su come installare l'app portale aziendale ed eseguire la registrazione.  

Il messaggio viene visualizzato sul dispositivo per gli utenti di Exchange Online e i tenant nel nuovo ambiente di Exchange Online dedicato e viene recapitato nella posta in arrivo degli utenti per dispositivi Exchange locale e Exchange Online legacy dedicato.  

> [!NOTE]  
> Le regole di accesso condizionale di Configuration Manager sovrascrivono, consentono, bloccano e mettono in quarantena le regole definite nella console di amministrazione di Exchange Online.  
> 
> I criteri di accesso condizionale devono essere configurati nella console di Intune. All'inizio della procedura seguente è necessario accedere alla console di Intune tramite Configuration Manager. Se richiesto, accedere con le stesse credenziali usate per configurare il punto di connessione del servizio tra Configuration Manager e Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Per abilitare i criteri di Exchange Online  

1. Nella console di Configuration Manager selezionare **Asset e conformità**.  

2. Espandere **impostazioni di conformità**, espandere **accesso condizionale**e quindi selezionare **Exchange Online**.  

3. Nella scheda **Home** , nel gruppo **collegamenti** , selezionare **Configura criteri di accesso condizionale nella console di Intune**. Potrebbe essere necessario specificare il nome utente e la password dell'account usato per connettere Configuration Manager a qualsiasi amministratore globale del servizio Intune. Viene visualizzata la console di amministrazione di Intune.  

4. Nel portale di Microsoft Intune selezionare **criteri** > **accesso condizionale** > **criteri di Exchange Online**.  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. Nella pagina **Criteri di Exchange Online** selezionare **Abilita criteri di accesso condizionale per Exchange Online**. Se si seleziona questa opzione, il dispositivo deve essere conforme. Se questa opzione non è selezionata, l'accesso condizionale non viene applicato.  

    > [!NOTE]  
    > Se non sono stati distribuiti criteri di conformità e abilitati i criteri di Exchange Online, tutti i dispositivi di destinazione vengono segnalati come conformi.  
   >   
   >  Indipendentemente dallo stato di conformità, tutti gli utenti interessati dai criteri dovranno registrare i propri dispositivi in Intune.  

6. In **accesso all'applicazione**, per Outlook e altre app che usano l'autenticazione moderna, è possibile scegliere di limitare l'accesso solo ai dispositivi conformi per ogni piattaforma. I dispositivi Windows devono essere aggiunti a un dominio oppure devono essere registrati in Intune e conformi.  

    > [!TIP]  
    > Con l'**autenticazione moderna** i client Office possono usare l'accesso basato su Active Directory Authentication Library (ADAL).  
    > 
    > - Questo tipo di autenticazione consente ai client Office di usare l'autenticazione basata su browser, nota anche come autenticazione passiva. Per eseguire l'autenticazione, l'utente viene indirizzato a una pagina Web di accesso.  
    > - Questo nuovo metodo di accesso offre nuovi scenari, tra cui l'accesso condizionale, basato sulla **conformità del dispositivo** e sull'uso dell' **autenticazione a più fattori** .  
    > 
    >  Per altre informazioni, vedere [Funzionamento dell'autenticazione moderna per le applicazioni client di Office 2013 e Office 2016](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016).  

    Se si usa Exchange Online con Configuration Manager e Intune, è possibile gestire non solo i dispositivi mobili con accesso condizionale, ma anche i computer desktop. I PC devono essere aggiunti a un dominio o essere registrati in Intune e conformi. È possibile impostare i requisiti seguenti:  

    - **I dispositivi devono essere aggiunti a un dominio o conformi.** I PC devono essere aggiunti a un dominio o conformi ai criteri. Se un PC non soddisfa uno di questi requisiti, all'utente verrà richiesto di registrare il dispositivo in Intune.  

    - **I dispositivi devono essere aggiunti a un dominio.** Per accedere a Exchange Online, i PC devono essere aggiunti a un dominio. Se un PC non è aggiunto a un dominio, l'accesso alla posta elettronica è bloccato e all'utente viene richiesto di contattare l'amministratore IT.  

    - **I dispositivi devono essere conformi.** I PC devono essere registrati in Intune e conformi. Se un PC non è registrato, viene visualizzato un messaggio contenente le istruzioni su come eseguire la registrazione.  

7. In **Outlook Web Access (OWA)** è possibile scegliere di consentire l'accesso a Exchange Online solo dai browser supportati: Safari (iOS) e Chrome (Android). Non sarà possibile accedere da altri browser. Vengono applicate anche le restrizioni di piattaforma selezionate per l'accesso all'applicazione per Outlook.  

    - Nei dispositivi **Android** gli utenti devono abilitare l'accesso al browser. Per eseguire questa azione, l'utente deve abilitare l'opzione "Abilita l'accesso al browser" nel dispositivo registrato come indicato di seguito:  

        1. Avviare **l'app Portale aziendale**.  

        2. Passare alla pagina **Impostazioni** facendo clic sui punti di sospensione (...) o sul tasto di menu.  

        3. Premere il pulsante **Abilita l'accesso al browser**.  

        4. Nel browser Chrome disconnettersi da Office 365 e riavviare Chrome.  

    - Nelle piattaforme **iOS e Android** , per identificare il dispositivo usato per accedere al servizio, Azure ad emetterà un certificato TLS sul dispositivo. Il dispositivo Visualizza il certificato con una richiesta all'utente di selezionare il certificato come illustrato nelle schermate seguenti. Per continuare a usare il browser, è necessario che l'utente selezioni il certificato.  

        - **iOS**  

        ![schermata del messaggio di richiesta del certificato in un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Android**  

        ![schermata del messaggio di richiesta del certificato in un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)  

8. Per le**App di posta elettronica di Exchange ActiveSync**è possibile impedire alla posta elettronica di accedere a Exchange Online se il dispositivo non è conforme e selezionare se consentire o bloccare l'accesso alla posta elettronica quando Intune non riesce a gestire il dispositivo.  

9. In **Gruppi di destinazione**selezionare i gruppi di sicurezza di Active Directory degli utenti ai quali applicare i criteri.  

    > [!NOTE]  
    > Per gli utenti inclusi nei gruppi di destinazione, i criteri di Intune sostituiranno le regole e i criteri di Exchange.  
    > 
    > Exchange applicherà le regole di autorizzazione, blocco e quarantena e i criteri di Exchange solo nei casi seguenti:  
    > 
    > - L'utente non dispone di una licenza per Intune.  
    > - L'utente ha una licenza per Intune, ma non appartiene ad alcun gruppo di sicurezza di destinazione nei criteri di accesso condizionale.  

10. In **Gruppi esentati**selezionare i gruppi di sicurezza di Active Directory degli utenti che verranno esentati da questi criteri. Se un utente è incluso sia nel gruppo di destinazione che in quello esentato, sarà esentato dai criteri e avrà accesso alla posta elettronica.  

11. Al termine, fare clic su **Salva**.  


Esaminare le note seguenti relative a questo criterio:  

- Non è necessario distribuire i criteri di accesso condizionale. viene applicato immediatamente.  

- Dopo la creazione di un account di posta elettronica da parte di un utente, il dispositivo viene bloccato immediatamente.  

- Se un utente bloccato registra il dispositivo in Intune o risolve il problema di conformità, l'accesso alla posta elettronica viene sbloccato entro 2 minuti.  

- Se l'utente annulla la registrazione del dispositivo, la posta elettronica viene bloccata dopo circa sei ore.  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Per Exchange locale (e i tenant nell’ambiente Exchange Online legacy dedicato)  
Il flusso seguente viene usato dai criteri di accesso condizionale per fare in modo che Exchange locale e i tenant nell’ambiente Exchange Online legacy dedicato valutino se consentire o bloccare i dispositivi.  

![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Per abilitare i criteri di Exchange locale  

1. Nella console di Configuration Manager selezionare **Asset e conformità**.  

2. Espandere **impostazioni di conformità**, espandere **accesso condizionale**e quindi selezionare **Exchange locale**.  

3. Nel gruppo **Exchange locale** della scheda **Home** selezionare **Configura criteri di accesso condizionale**.  

4. Nella pagina **generale** della **Configurazione guidata dei criteri di accesso condizionale**specificare se si vuole eseguire l'override della regola predefinita Exchange Active Sync. Selezionare questa opzione se si vuole che i dispositivi registrati e conformi abbiano sempre accesso alla posta elettronica, anche quando la regola predefinita è impostata su quarantena o blocca l'accesso.  

    > [!NOTE]  
    > Si è verificato un problema con la sostituzione predefinita per i dispositivi Android. Se la regola di accesso predefinita del server Exchange viene impostata su **Blocca** e il criterio di accesso condizionale di Exchange è attivato con l'opzione di sostituzione regola predefinita, i dispositivi Android degli utenti di destinazione potrebbero non essere sbloccati anche dopo che i dispositivi sono registrati e conformi con Intune. Per risolvere questo problema, impostare la regola di accesso predefinita di Exchange su **Quarantena**. Il dispositivo non ottiene l'accesso a Exchange per impostazione predefinita e l'amministratore può ottenere un report dal server Exchange nell'elenco dei dispositivi che vengono messi in quarantena.  

    Se non è stato configurato un account di posta elettronica di notifica quando si configura Exchange Connector, verrà visualizzato un avviso in questa pagina e il pulsante **Avanti** sarà disabilitato.  Prima di continuare, è necessario prima configurare le impostazioni di notifica di posta elettronica in Exchange Connector e quindi tornare alla **Configurazione guidata dei criteri di accesso condizionale** per completare il processo.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. Nella pagina **Raccolte di destinazione** aggiungere una o più raccolte utenti. Per accedere a Exchange, gli utenti nelle raccolte devono registrare i propri dispositivi in Intune e rispettare anche i criteri di conformità distribuiti.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. Nella pagina **Raccolte esentate** aggiungere tutte le raccolte di utenti che si desidera esentare dal criterio di accesso condizionale. Gli utenti di questi gruppi non devono registrare i propri dispositivi in Intune e non devono essere conformi ai criteri di conformità distribuiti per poter accedere a Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    Se un utente viene visualizzato in un elenco di destinazione ed esentato, sarà esentato dal criterio di accesso condizionale.  

7. Nella pagina **Modifica notifica utente** configurare il messaggio di posta elettronica inviato da Intune agli utenti e che contiene le istruzioni per sbloccare il dispositivo (in aggiunta al messaggio inviato da Exchange).  

    È possibile modificare il messaggio predefinito e usare i tag HTML per formattare l'aspetto del testo. È anche possibile inviare preventivamente un messaggio di posta elettronica ai dipendenti per informarli delle modifiche imminenti e fornire istruzioni sulla registrazione dei dispositivi.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > Perché il messaggio di posta elettronica di notifica di Intune contenente le istruzioni per la correzione viene recapitato alla cassetta postale di Exchange dell'utente, nel caso in cui il dispositivo dell'utente venga bloccato prima della ricezione del messaggio di posta elettronica, è possibile usare un dispositivo sbloccato o un altro metodo per accedere a Exchange e visualizzare il messaggio.  
    > 
    > Per consentire a Exchange di inviare il messaggio di posta elettronica di notifica, configurare l'account che verrà usato per inviare il messaggio di posta elettronica di notifica. Si esegue questa operazione quando si configurano le proprietà del connettore Exchange Server.  
    >   
    > Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

8. Nella pagina **Riepilogo** verificare le impostazioni e quindi completare la procedura guidata.  


Esaminare le note seguenti relative a questo criterio:  

- Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.  

- Dopo che un utente ha configurato un profilo di Exchange ActiveSync, il blocco del dispositivo potrebbe richiedere da 1 a tre ore (se non è gestito da Intune).  

- Se un utente bloccato registra il dispositivo in Intune (o corregge la mancata conformità), l'accesso alla posta elettronica verrà sbloccato entro due minuti.  

- Se l'utente annulla la registrazione da Intune, il blocco del dispositivo potrebbe richiedere da 1 a 3 ore.  


## <a name="see-also"></a>Vedere anche  

[Gestire l'accesso ai servizi](/sccm/protect/deploy-use/manage-access-to-services)
