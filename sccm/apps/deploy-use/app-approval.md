---
title: Approvare le applicazioni
titleSuffix: Configuration Manager
description: Informazioni sulle impostazioni e i comportamenti per l'approvazione delle applicazioni in Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f78ec291701d15c0907aa780b4bed23b712995c7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135222"
---
# <a name="approve-applications-in-configuration-manager"></a>Approvare le applicazioni in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si [distribuiscono applicazioni](/sccm/apps/deploy-use/deploy-applications) in Configuration Manager, è possibile richiedere l'approvazione prima dell'installazione. Gli utenti richiedono l'applicazione in Software Center e quindi la richiesta viene esaminata nella console di Configuration Manager. La richiesta può essere approvata o rifiutata. 



## <a name="bkmk_approval"></a> Impostazioni di approvazione

Il comportamento di approvazione delle applicazioni varia a seconda della versione di Configuration Manager. Nella pagina **Impostazioni di distribuzione** dell'applicazione di distribuzione viene visualizzata una delle seguenti impostazioni di approvazione:  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione
*Si applica alla versione 1710 e alle versioni precedenti*

L'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi.  

Le richieste di approvazione dell'applicazione vengono visualizzate nel nodo **Richieste di approvazione** , in **Gestione applicazioni** , nell'area di lavoro **Raccolta software** . Se una richiesta non viene approvata entro 30 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  

Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Questa azione non provoca la disinstallazione dell'applicazione dai dispositivi da parte del client. Impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.  


#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo
*Si applica alla versione 1802 e alle versioni successive <sup>[Nota 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **Nota 1**: Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti). 
> 
> Se non si abilita questa funzionalità, viene visualizzata l'esperienza precedente.  

L'amministratore deve approvare qualsiasi richiesta utente per l'applicazione prima che l'utente possa installarla nel dispositivo desiderato. Se l'amministratore approva la richiesta, l'utente può installare l'applicazione solo su quel dispositivo. Per installare l'applicazione in un altro dispositivo dovrà inviare un'altra richiesta. Questa opzione è disattivata quando lo scopo della distribuzione è **Richiesto** o quando si distribuisce l'applicazione un una raccolta di dispositivi. <!--1357015-->  

> [!Note]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.<!--SCCMDocs issue 646-->  

Nell'area di lavoro **Raccolta software** della console di Configuration Manager visualizzare **Richieste di approvazione** in **Gestione applicazioni**. Nell'elenco è ora presente una colonna **Dispositivo** per ogni richiesta. Quando si intraprende un'azione sulla richiesta, la finestra di dialogo Richiesta di applicazioni include anche il nome del dispositivo da cui l'utente ha inviato la richiesta.  

Se una richiesta non viene approvata entro 30 giorni, viene rimossa. La reinstallazione del client potrebbe annullare eventuali richieste di approvazione in sospeso.  

Dopo avere approvato un'applicazione per l'installazione, è possibile scegliere di negare la richiesta facendo clic su **Nega** nella console di Configuration Manager. Questa azione non provoca la disinstallazione dell'applicazione dai dispositivi da parte del client. Impedisce agli utenti di installare nuove copie dell'applicazione da Software Center.  

> [!Important]  
> A partire dalla versione 1806, *il comportamento è cambiato* quando si revoca l'approvazione per un'applicazione approvata e installata in precedenza. Ora, quando si **Nega** la richiesta per l'applicazione, il client disinstalla l'applicazione dal dispositivo dell'utente.<!--1357891-->  



## <a name="bkmk_email-approve"></a> Notifiche tramite posta elettronica
<!--1321550-->

A partire dalla versione 1810 è possibile configurare le notifiche tramite posta elettronica per le richieste di approvazione dell'applicazione. Quando un utente richiede un'applicazione, si riceve un messaggio di posta elettronica. Fare clic sui collegamenti nel messaggio di posta elettronica per approvare o rifiutare la richiesta, senza che sia necessario usare la console di Configuration Manager.

È possibile definire gli indirizzi di posta elettronica degli utenti che possono approvare o rifiutare la richiesta durante la creazione di una nuova distribuzione per l'applicazione. Se è necessario modificare l'elenco degli indirizzi di posta elettronica in un secondo momento, passare all'area di lavoro **Monitoraggio**, espandere **Avvisi** e selezionare il nodo **Sottoscrizioni**. Selezionare **Proprietà** da una delle sottoscrizioni **Approva l'applicazione tramite posta elettronica** correlate alla distribuzione dell'applicazione. 

Se sono presenti più avvisi, è possibile determinare a quale distribuzione si riferisce ognuno di questi. Aprire le proprietà dell'avviso e visualizzare l'elenco di **Avvisi selezionati** nella scheda Generale. La distribuzione viene abilitata come avviso per questa sottoscrizione. 


### <a name="prerequisites"></a>Prerequisiti

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Per inviare notifiche tramite posta elettronica e intraprendere un'azione nella rete interna
Con questi prerequisiti, i destinatari ricevono una notifica della richiesta tramite posta elettronica. Se sono collegati alla rete interna, possono anche approvare o negare la richiesta direttamente dal messaggio di posta elettronica.

- Abilitare la [funzionalità facoltativa](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**.  

- Configurare la [notifica tramite posta elettronica per gli avvisi](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

- Consentire al provider SMS di usare un certificato.<!--SCCMDocs-pr issue 3135--> Usare una delle opzioni seguenti:  

    - Abilitare [HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http) (scelta consigliata)  

        > [!Note]  
        > Quando il sito crea un certificato per il provider SMS, non verrà considerato attendibile dal Web browser nel client. In base alle impostazioni di sicurezza, quando si risponde a una richiesta dell'applicazione, potrebbe essere visualizzato un avviso di sicurezza.  

    - Associare manualmente un certificato basato su PKI alla porta 443 in IIS sul server che ospita il ruolo Provider SMS  


#### <a name="to-take-action-from-internet"></a>Intraprendere un'azione da Internet
Con questi prerequisiti aggiuntivi facoltativi, i destinatari possono approvare o rifiutare la richiesta ovunque sia disponibile l'accesso a Internet.

- Abilitare il servizio di amministrazione del Provider SMS tramite Cloud Management Gateway. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**. Selezionare il server con il ruolo Provider SMS. Nel riquadro dei dettagli selezionare il ruolo **Provider SMS** e scegliere **Proprietà** nella barra multifunzione della scheda Ruolo del sito. Selezionare l'opzione **Consenti il traffico di Configuration Manager Cloud Management Gateway per il servizio di amministrazione**.  

    - Provider SMS richiede **.NET 4.5.2** o versioni successive.  

- [Gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Eseguire l'onboarding del sito in [servizi di Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la **gestione del cloud**  

    - Abilitare [Individuazione utente Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Configurare manualmente le impostazioni di Azure AD:  

        1. Andare al [portale di Azure](https://portal.azure.com), selezionare **Azure Active Directory**, quindi selezionare **Registrazioni app**.  

        2. Selezionare l'applicazione di tipo **Nativo** creata per l'integrazione **Cloud Management** di Configuration Manager.  

        3. Nelle proprietà dell'app selezionare **Impostazioni**, quindi selezionare **URI di reindirizzamento**.  

            1. Incollare il percorso seguente nel riquadro URI di reindirizzamento: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Sostituire `<CMG FQDN>` con il nome di dominio completo (FQDN) del servizio Cloud Management Gateway (CMG). Ad esempio, GraniteFalls.Contoso.com.  

            3. Selezionare **Salva**. Chiudere il riquadro **Impostazioni**.  

        4. Nella finestra proprietà dell'app, selezionare **Manifesto**.  

            1. Nel riquadro Modifica manifesto individuare la proprietà **oauth2AllowImplicitFlow**.  

            2. Impostarne il valore su **true**. L'intera riga dovrebbe assomigliare, ad esempio, alla riga seguente: `"oauth2AllowImplicitFlow": true,`   

            3. Selezionare **Salva**.  


### <a name="configure-email-approval"></a>Configurare l'approvazione tramite posta elettronica

1. Nella console di Configuration Manager [distribuire un'applicazione](/sccm/apps/deploy-use/deploy-applications) come disponibile a una raccolta di utenti. Nella pagina **Impostazioni di distribuzione** abilitarla per l'approvazione. Immettere quindi uno o più indirizzi di posta elettronica per ricevere le notifiche. Se vi sono più indirizzi di posta elettronica, separarli con un punto e virgola (`;`).  

     > [!Note]  
     > Chiunque riceva il messaggio di posta elettronica nell'organizzazione di Azure AD può approvare la richiesta. Non inoltrare il messaggio di posta elettronica ad altri utenti a meno che non si voglia che intervengano.  

2. Come utente, richiedere l'applicazione in Software Center.  

3. Si riceve una notifica tramite posta elettronica entro cinque minuti. Il contenuto del messaggio di posta elettronica è simile al seguente:  

![Notifica tramite posta elettronica di esempio per l'approvazione dell'applicazione](media/1321550-email.png)

> [!Note]  
> Il collegamento per approvare o rifiutare è monouso. Ad esempio, se si configura un alias di gruppo per ricevere le notifiche e un utente approva la richiesta, un altro utente del gruppo non potrà rifiutarla.  

Rivedere il file **NotiCtrl.log** nel server del sito per la risoluzione dei problemi.


## <a name="maintenance"></a>Manutenzione 

Configuration Manager memorizza le informazioni relative alla richiesta di approvazione per l'applicazione nel database del sito. La cronologia delle richieste annullate o rifiutate viene eliminata dal sito dopo 30 giorni. È possibile configurare il comportamento di eliminazione con l'[attività di manutenzione del sito](/sccm/core/servers/manage/maintenance-tasks) **Elimina dati richiesta applicazione obsoleti**. Il sito non elimina mai le richieste applicazione approvate o in attesa.

