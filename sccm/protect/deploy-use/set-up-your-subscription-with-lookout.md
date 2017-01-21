---
title: Configurare la sottoscrizione con Lookout| System Center Configuration Manager
description: Questo argomento offre informazioni dettagliate su come configurare la protezione dalle minacce per il dispositivo di Lookout.
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f125a9e-567a-4d10-a858-112b6159d0e9
caps.latest.revision: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c13c6268fa76ade7feb0981f9c4a6e325e393aca
ms.openlocfilehash: f29d5834b82dd8888cff56fb0ad8024629f829ab


---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configurare la sottoscrizione con la protezione dalle minacce per il dispositivo di Lookout

*Si applica a: System Center Configuration Manager (Current Branch)*

Per preparare la sottoscrizione per il servizio di protezione dalle minacce per il dispositivo di Lookout, il supporto tecnico di Lookout (enterprisesupport@lookout.com) ha bisogno delle informazioni seguenti sulla sottoscrizione di Azure Active Directory (Azure AD). Il tenant di Lookout Mobility Endpoint Security verrà associato alla sottoscrizione di Azure AD per l'integrazione di Lookout con Intune. 

* **ID tenant di Azure AD**
* **ID oggetto gruppo di Azure AD** per accesso **completo** alla console di Lookout
* **ID oggetto gruppo di Azure AD** per accesso **limitato** alla console di Lookout (facoltativo)

> [!IMPORTANT]
> Un tenant esistente di Lookout Mobile Endpoint Security non ancora associato al tenant di Azure AD non può essere usato per l'integrazione con Azure AD e Intune. Contattare il supporto di Lookout per creare un nuovo tenant di Lookout Mobile Endpoint Security. Usare il nuovo tenant per caricare gli utenti di AD Azure.

Leggere la sezione seguente per raccogliere le informazioni necessarie al team di supporto di Lookout.  

## <a name="get-your-azure-ad-information"></a>Ottenere le informazioni su Azure AD
### <a name="azure-ad-tenant-id"></a>ID tenant di Azure AD
Accedere al [portale di gestione di Azure AD](https://manage.windowsazure.com) e selezionare la sottoscrizione. 

![schermata della pagina di Azure AD con il nome del tenant visualizzato](../media/aad_tenant_name.png). Dopo aver selezionato il nome della sottoscrizione, l'URL risultante include l'ID sottoscrizione.  In caso di problemi a trovare l'ID sottoscrizione, vedere l'[articolo del supporto tecnico Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) per suggerimenti su come recuperare l'ID sottoscrizione.   
### <a name="azure-ad-group-id"></a>ID gruppo di Azure AD
La console di Lookout supporta 2 livelli di accesso:  
* **Accesso completo:** l'amministratore di Azure AD può creare un gruppo di utenti che avrà accesso completo. Può facoltativamente creare un gruppo di utenti che avrà invece accesso limitato.  Solo gli utenti di questi gruppi potranno accedere alla **console di Lookout**.
* **Accesso limitato:** gli utenti di questo gruppo non avranno accesso a diversi moduli correlati alla configurazione e alla registrazione della console di Lookout e avranno accesso in sola lettura al modulo **Security Policy** (Criteri di sicurezza) della console di Lookout.  

Per altri dettagli sulle autorizzazioni, leggere [questo articolo](https://personal.support.lookout.com/hc/en-us/articles/114094105653) nel sito Web di Lookout.

L'**ID oggetto gruppo** è disponibile nella pagina **Proprietà** del gruppo nella **console di gestione di Azure AD**.

![screenshot della pagina delle proprietà con il campo ID evidenziato](../media/aad_group_object_id.png)

Dopo aver raccolto le informazioni, contattare il supporto di Lookout all'indirizzo di posta elettronica enterprisesupport@lookout.com.

Il supporto di Lookout collaborerà con il contatto principale dell'utente per caricare la sottoscrizione e creare l'account aziendale per Lookout, usando le informazioni raccolte.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configurare la sottoscrizione con la protezione dalle minacce per il dispositivi di Lookout
### <a name="step-1-set-up-your-device-threat-protection"></a>Passaggio 1: Configurare la protezione dalle minacce per il dispositivo
Dopo che il supporto di Lookout ha creato l'account aziendale di Lookout, è possibile accedere alla console di Lookout.   Lookout invierà al contatto principale dell'azienda un messaggio di posta elettronica contenente un collegamento all'URL di accesso:https://aad.lookout.com/les?action=consent

Quando si accede per la prima volta alla console di Lookout, è necessario usare un account utente con il ruolo di Amministratore globale di Azure AD, poiché Lookout possa usare queste informazioni per registrare il tenant di Azure AD.   Per gli accessi successivi non è necessario che l'utente abbia questo livello di privilegi per Azure AD.  Al primo accesso viene visualizzata una pagina di consenso. Scegliere **Accetta** per completare la registrazione.

![screenshot della pagina di primo accesso della console di Lookout](../media/lookout-initial-login.png)

Dopo aver accettato e fornito il consenso , si verrà reindirizzati alla console di Lookout. Dopo aver eseguito la registrazione iniziale, è possibile accedere usando l'URL https://aad.lookout.com

Se si verificano problemi durante l'accesso, vedere l'[articolo dedicato alla risoluzione dei problemi]().

I passaggi successivi descrivono le attività da eseguire per completare la configurazione di Lookout nella [console di Lookout](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Passaggio 2: Configurare Intune Connector

1.  Nel modulo **System** (Sistema) della console di Lookout scegliere la scheda **Connectors** (Connettori) e selezionare **Intune**.

  ![screenshot della console di Lookout con la scheda Connectors (Connettori) aperta e l'opzione Intune evidenziata](../media/lookout-setup-intune-connector.png)

2.  Nella sezione delle impostazioni di connessione configurare la frequenza di heartbeat in minuti.  Il connettore Intune è pronto.  

  ![screenshot della scheda delle impostazioni di connessione che visualizza la frequenza di heartbeat configurata](../media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Passaggio 3: Configurare i gruppi di registrazione
Nella sezione **Enrollment Management** (Gestione registrazione) definire un set di utenti i cui dispositivi devono essere registrati in Lookout. Si consiglia di procedere iniziando con un piccolo gruppo di utenti di test e acquisire familiarità con il funzionamento dell'integrazione.  Se i risultati dei test sono soddisfacenti, è possibile estendere la registrazione a gruppi di utenti aggiuntivi.

Per iniziare con i gruppi di registrazione, definire prima un gruppo di sicurezza di Azure AD che rappresenta un primo set di utenti valido da registrare nella protezione dalle minacce per il dispositivo di Lookout. Dopo aver creato il gruppo in Azure AD, nella console di Lookout passare all'opzione **Enrollement Management** (Gestione registrazione) e aggiungere il valore per **Display Name** (Nome visualizzato) relativo al gruppo di sicurezza di Azure AD per la registrazione.

Quando un utente è in un gruppo di registrazione, tutti i dispositivi di tale utente identificati e supportati in Azure AD vengono registrati e sono idonei per l'attivazione nella protezione dalle minacce per il dispositivo di Lookout.  Alla prima apertura dell'app Lookout for Work nel dispositivo supportato, il dispositivo viene attivato in Lookout.

![screenshot della pagina registrazione di Intune Connector](../media/lookout-enrollment.png)

La procedura consigliata prevede l'uso dell'incremento predefinito di 5 minuti per verificare la presenza di nuovi dispositivi.

>[!IMPORTANT]
> Per il nome visualizzato viene fatta distinzione tra maiuscole e minuscole.  Usare il **Nome visualizzato** come illustrato nella pagina **Proprietà** del gruppo di sicurezza nel portale di Azure. Nell'immagine seguente notare le iniziali maiuscole del nome visualizzato nella pagina **Proprietà** del gruppo di sicurezza.  Nel titolo il nome è invece visualizzato tutto in minuscolo e questa forma non deve essere usata per l'immissione nella console di Lookout.
>![screenshot del portale di Azure, servizio Microsoft Azure Active Directory, pagina Proprietà](../media/aad-group-display-name.png)

La versione corrente presenta le limitazioni seguenti:  
* Non è prevista la convalida dei nomi visualizzati dei gruppi.  Assicurarsi di usare il valore indicato nel campo **NOME VISUALIZZATO** nel portale di Azure per il gruppo di sicurezza di Azure AD.
* La creazione di gruppi all'interno di altri gruppi non è attualmente supportata.  I gruppi di sicurezza di Azure AD specificati devono contenere solo utenti e non gruppi annidati.


### <a name="step-4-configure-state-sync"></a>Passaggio 4: Configurare la sincronizzazione dello stato
Nell'opzione **State Sync** (Sincronizzazione stato) specificare il tipo di dati che deve essere inviato a Intune.  È attualmente necessario abilitare sia lo stato del dispositivo che lo stato delle minacce per il corretto funzionamento dell'integrazione di Lookout e Intune.  Queste opzioni sono abilitate per impostazione predefinita.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Passaggio 5: Configurare le informazioni sul destinatario dei report sugli errori inviate tramite posta elettronica
In **Error Management** (Gestione errori) immettere l'indirizzo di posta elettronica del destinatario dei report sugli errori.

![screenshot della pagina di gestione degli errori di Intune Connector](../media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Passaggio 6: Configurare le impostazioni di registrazione
Nel modulo **System** (Sistema), nella pagina **Connectors** (Connettori), specificare il numero di giorni prima dei quali un dispositivo deve essere considerato disconnesso.  I dispositivi disconnessi sono considerati non conformi. L'accesso alle applicazioni aziendali tramite questi dispositivi in base ai criteri di accesso condizionale SCCM è bloccato. È possibile specificare un valore compreso tra 1 e 90 giorni.

![](../media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Passaggio 7: Configurare le notifiche tramite posta elettronica
Per ricevere avvisi relativi alle minacce tramite posta elettronica, accedere alla [console di Lookout](https://aad.lookout.com) con l'account utente che deve ricevere le notifiche. Nella scheda **Preferences** (Preferenze) del modulo **System** (Sistema) scegliere le notifiche desiderate e impostarle su **ON** (Attivato). Salvare le modifiche.

![screenshot della pagina delle preferenze con l'account utente visualizzato](../media/lookout-email-notifications.png) Se non si vogliono più ricevere notifiche tramite posta elettronica, impostare le notifiche su **OFF** (Disattivato) e salvare le modifiche.
### <a name="step-8-configure-threat-classification"></a>Passaggio 8: Configurare la classificazione delle minacce
La protezione dalle minacce per il dispositivo di Lookout usa vari tipi di classificazione per le minacce per i dispositivi mobili. Alle [classificazioni delle minacce di Lookout](http://personal.support.lookout.com/hc/en-us/articles/114094130693) sono associati livelli di rischio predefiniti, che possono essere modificati in qualsiasi momento per adattarli ai requisiti aziendali.

![screenshot della pagina dei criteri con le minacce e le classificazioni visualizzate](../media/lookout-threat-classification.png)

>[!IMPORTANT]
> I livelli di rischio qui specificati rappresentano un aspetto importante della protezione dalle minacce per il dispositivo perché l'integrazione con Intune calcola la conformità dei dispositivi in base a questi livelli di rischio in fase di esecuzione. In altre parole, l'amministratore di Intune imposta una regola nei criteri per identificare un dispositivo come non conforme se presenta una minaccia attiva con un livello minimo di rischio alto, medio o basso. Il calcolo di conformità dei dispositivi in Intune dipende direttamente dai criteri di classificazione delle minacce nella protezione dalle minacce per il dispositivo di Lookout.

## <a name="watching-enrollment"></a>Controllo della registrazione
Dopo aver completato la configurazione, la protezione dalle minacce per il dispositivo di Lookout inizia a eseguire il polling di Azure AD per i dispositivi corrispondenti ai gruppi di registrazione specificati.  Le informazioni sui dispositivi registrati sono disponibili nel modulo Devices (Dispositivi).  Per i dispositivi viene visualizzato lo stato iniziale in sospeso.  Lo stato del dispositivo cambia dopo l'installazione, l'apertura e l'attivazione nel dispositivo dell'app Lookout for Work.  Per informazioni dettagliate su come ottenere l'app Lookout for Work nel dispositivo, vedere l'argomento [Configurare e distribuire l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).
## <a name="next-steps"></a>Passaggi successivi
[Abilitare la connessione a Lookout MTP in Intune](enable-lookout-connection-in-intune.md)



<!--HONumber=Dec16_HO3-->


