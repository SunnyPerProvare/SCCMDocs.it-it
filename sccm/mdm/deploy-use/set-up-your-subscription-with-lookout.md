---
title: Configurare la sottoscrizione Lookout
titleSuffix: Configuration Manager
description: Informazioni su come configurare Lookout Mobile Threat Defense.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 85c2ae1039058f39bd96c7d0752f798504b0dd4d
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2018
ms.locfileid: "34746111"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurare la sottoscrizione per Lookout Mobile Threat Defense

*Si applica a: System Center Configuration Manager (Current Branch)*

Per configurare la sottoscrizione per Lookout Mobile Threat Defense, seguire questa procedura:

| #        |Passaggio  |
| ------------- |-------------|
| 1 | [Ottenere le informazioni su Azure AD](#collect-azure-ad-information) |
| 2 | [Configurare la sottoscrizione](#configure-your-subscription) |
| 3 | [Configurare i gruppi di registrazione](#configure-enrollment-groups) |
| 4 | [Configurare la sincronizzazione dello stato](#configure-state-sync) |
| 5 | [Configurare le informazioni sul destinatario dei report sugli errori inviate tramite posta elettronica](#configure-error-report-email-recipient-information) |
| 6 | [Configurare le impostazioni di registrazione](#configure-enrollment-settings) |
| 7 | [Configurare le notifiche tramite posta elettronica](#configure-email-notifications) |
| 8 | [Configurare la classificazione delle minacce](#configure-threat-classification) |
| 9 | [Controllo della registrazione](#watching-enrollment) |


> [!IMPORTANT]  
> Un tenant esistente di Lookout Mobile Endpoint Security non ancora associato al tenant di Azure AD non può essere usato per l'integrazione con Azure AD e Intune. Contattare il supporto di Lookout per creare un nuovo tenant di Lookout Mobile Endpoint Security. Usare il nuovo tenant per caricare gli utenti di AD Azure.




## <a name="collect-azure-ad-information"></a>Ottenere le informazioni su Azure AD
Il tenant di Lookout Mobility Endpoint Security verrà associato alla sottoscrizione di Azure AD per l'integrazione di Lookout con Intune. Per abilitare la sottoscrizione al servizio Lookout Mobile Threat Defense, il supporto di Lookout (enterprisesupport@lookout.com) richiede le informazioni seguenti:

- **ID tenant di Azure AD**
- **ID oggetto gruppo di Azure AD** per accesso *completo* alla console di Lookout
- **ID oggetto gruppo di Azure AD** per accesso *limitato* alla console di Lookout (facoltativo)

Eseguire i passaggi seguenti per raccogliere le informazioni richieste dal team di supporto di Lookout.

1. Accedere al [portale di Azure](https://portal.azure.com) e selezionare la sottoscrizione. 

2. Quando si sceglie il nome della sottoscrizione, l'URL risultante include l'ID sottoscrizione. In caso di problemi a trovare l'ID sottoscrizione, vedere l'[articolo del supporto tecnico Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) per suggerimenti su come recuperare l'ID sottoscrizione.

3. Individuare l'ID gruppo di Azure AD.  
     > [!NOTE]   
     > L'**ID oggetto del gruppo** è indicato nella pagina **Proprietà** del gruppo nel pannello di Azure AD del portale di Azure.  

   La console di Lookout supporta due livelli di accesso:  

   - **Accesso completo:** l'amministratore di Azure AD può creare un gruppo per gli utenti che hanno completo e facoltativamente creare un gruppo per gli utenti che hanno accesso limitato. Solo gli utenti di questi gruppi possono accedere alla **console di Lookout**.
   - **Accesso limitato:** gli utenti di questo gruppo non avranno accesso a diversi moduli correlati alla configurazione e alla registrazione della console di Lookout e avranno accesso in sola lettura al modulo **Security Policy** (Criteri di sicurezza) della console di Lookout.  

     > [!TIP]  
     > Per altre informazioni sulle autorizzazioni, vedere [questo articolo del supporto tecnico di Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Dopo aver raccolto le informazioni, contattare il supporto di Lookout all'indirizzo di posta elettronica enterprisesupport@lookout.com. Il supporto di Lookout collaborerà con il contatto principale dell'utente per caricare la sottoscrizione e creare l'account aziendale per Lookout, usando le informazioni raccolte.



## <a name="configure-your-subscription"></a>Configurare la sottoscrizione

1. Dopo che il supporto tecnico di Lookout ha creato l'account Lookout Enterprise, Lookout invierà al contatto principale dell'azienda un messaggio di posta elettronica contenente un [URL di accesso](https://aad.lookout.com/les?action=consent).

2. Quando si accede per la prima volta alla console di Lookout, è necessario usare un account utente con il ruolo di Amministratore globale di Azure AD per registrare il tenant di Azure AD. Gli accessi successivi non richiedono questo livello di privilegi di Azure AD. Viene visualizzata una pagina di consenso. Scegliere **Accetta** per completare la registrazione. Dopo aver accettato e fornito il consenso, si viene reindirizzati alla console di Lookout.

   ![screenshot della pagina di primo accesso della console di Lookout](media/lookout-initial-login.png)

3. Nella [console di Lookout](https://aad.lookout.com) nel modulo **System** (Sistema) scegliere la scheda **Connectors** (Connettori) e selezionare **Intune**.

   ![screenshot della console di Lookout con la scheda Connectors (Connettori) aperta e l'opzione Intune evidenziata](media/lookout-setup-intune-connector.png)

4. Passare a **Connectors** (Connettori)  > **Connection Settings** (Impostazioni connessione) e specificare **Heartbeat Frequency** (Frequenza di heartbeat) in minuti.

   ![screenshot della scheda delle impostazioni di connessione che visualizza la frequenza di heartbeat configurata](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurare i gruppi di registrazione
1. È consigliabile creare un gruppo di sicurezza Azure AD nel [portale di Azure](https://portal.azure.com) contenente un numero limitato di utenti per testare l'integrazione di Lookout.

    > [!NOTE]  
    > Tutti i dispositivi supportati da Lookout e registrati in Intune degli utenti di un gruppo di registrazione in Azure AD identificati e supportati vengono registrati e sono idonei all'attivazione nella console di Lookout MTD.

2. Nella [console di Lookout](https://aad.lookout.com) nel modulo **System** (Sistema) scegliere la scheda **Connectors** (Connettori) e selezionare **Enrollment Management** (Gestione registrazioni) per definire un gruppo di utenti i cui dispositivi devono essere registrati in Lookout. Aggiungere il **Nome visualizzato** del gruppo di sicurezza di Azure AD per la registrazione.

    ![screenshot della pagina registrazione di Intune Connector](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > Nel **Nome visualizzato** viene fatta distinzione tra maiuscole e minuscole come illustrato nella pagina **Proprietà** del gruppo di sicurezza nel portale di Azure. Come illustrato nell'immagine seguente, per il **Nome visualizzato** del gruppo di sicurezza è usata la notazione Camel, mentre il titolo è in lettere minuscole. Nella console di Lookout specificare il **Nome visualizzato** del gruppo di sicurezza con la stessa notazione.
    >![screenshot del portale di Azure, servizio Microsoft Azure Active Directory, pagina Proprietà](media/aad-group-display-name.png)

    >[!NOTE]  
    >La procedura consigliata prevede l'uso dell'incremento predefinito di cinque minuti per verificare la presenza di nuovi dispositivi. Limitazioni attuali, **Lookout non convalida i nomi visualizzati dei gruppi:** assicurarsi che il campo **NOME VISUALIZZATO** del portale di Azure corrisponda esattamente al gruppo di sicurezza di Azure AD. **Non è supportata la creazione di gruppi nidificati:** i gruppi di sicurezza di Azure AD usati in Lookout devono contenere solo utenti. Non possono contenere altri gruppi.

3.  Dopo aver aggiunto un gruppo, alla successiva apertura dell'app Lookout for Work nel dispositivo supportato, il dispositivo viene attivato in Lookout.

4.  Se si è soddisfatti dei risultati, estendere la registrazione a ulteriori gruppi di utenti.



## <a name="configure-state-sync"></a>Configurare la sincronizzazione dello stato
Nell'opzione **State Sync** (Sincronizzazione stato) specificare il tipo di dati che deve essere inviato a Intune. Per un corretto funzionamento dell'integrazione di Lookout e Intune sono necessari lo stato del dispositivo e lo stato delle minacce. Queste impostazioni sono abilitate per impostazione predefinita.



## <a name="configure-error-report-email-recipient-information"></a>Configurare le informazioni sul destinatario dei report sugli errori inviate tramite posta elettronica
In **Error Management** (Gestione errori) immettere l'indirizzo di posta elettronica del destinatario dei report sugli errori.

![screenshot della pagina di gestione degli errori di Intune Connector](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Configurare le impostazioni di registrazione
Nel modulo **System** (Sistema), nella pagina **Connectors** (Connettori), specificare il numero di giorni prima dei quali un dispositivo deve essere considerato disconnesso. I dispositivi disconnessi sono considerati non conformi. L'accesso alle applicazioni aziendali tramite questi dispositivi in base ai criteri di accesso condizionale SCCM è bloccato. È possibile specificare un valore compreso tra 1 e 90 giorni.

![Impostazioni di registrazione di Lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurare le notifiche tramite posta elettronica
Per ricevere avvisi relativi alle minacce tramite posta elettronica, accedere alla [console di Lookout](https://aad.lookout.com) con l'account utente che deve ricevere le notifiche. Nella scheda **Preferences** (Preferenze) del modulo **System** (Sistema) scegliere i livelli delle minacce per cui ricevere una notifica e impostarle su **ON** (Attivato). Salvare le modifiche.

![screenshot della pagina delle preferenze con l'account utente visualizzato](media/lookout-email-notifications.png) Se non si vogliono più ricevere notifiche tramite posta elettronica, impostare le notifiche su OFF (Disattivato) e salvare le modifiche.



## <a name="configure-threat-classification"></a>Configurare la classificazione delle minacce
Lookout Mobile Threat Defense classifica diversi tipi di minacce per i dispositivi mobili. Alle [classificazioni delle minacce di Lookout](http://personal.support.lookout.com/hc/articles/114094130693) sono associati livelli di rischio predefiniti, Queste impostazioni possono essere modificate in qualsiasi momento per adattarle ai requisiti aziendali.

![screenshot della pagina dei criteri con le minacce e le classificazioni visualizzate](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> I livelli di rischio sono un aspetto importante della difesa dalle minacce per dispositivi mobili. L'integrazione di Intune calcola la conformità del dispositivo in base a questi livelli di rischio in fase di esecuzione. L'amministratore di Intune imposta una regola nei criteri per identificare un dispositivo come non conforme se presenta una minaccia attiva con un livello minimo **alto**, **medio** o **basso**. Il calcolo di conformità dei dispositivi in Intune dipende direttamente dai criteri di classificazione delle minacce in Lookout Mobile Threat Defense.



## <a name="watching-enrollment"></a>Controllo della registrazione
Dopo aver completato la configurazione, Lookout Mobile Threat Defense avvia il polling di Azure AD per i dispositivi corrispondenti ai gruppi di registrazione specificati. Le informazioni sui dispositivi registrati sono disponibili nel modulo Devices (Dispositivi). Per i dispositivi viene visualizzato lo stato iniziale in sospeso. Lo stato del dispositivo cambia dopo l'installazione, l'apertura e l'attivazione nel dispositivo dell'app Lookout for Work. Per altre informazioni su come ottenere l'app Lookout for Work nel dispositivo, vedere [Configurare e distribuire l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Passaggi successivi
[Abilitare la connessione a Lookout MTP in Intune](enable-lookout-connection-in-intune.md)
