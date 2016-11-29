---
title: Pianificare e configurare la gestione delle applicazioni | System Center Configuration Manager
description: Implementare e configurare le dipendenze necessarie per la distribuzione di applicazioni in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b1e21c2d6c90f02a1c616186b119b1a744d7f172


---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni incluse in questo argomento per implementare le dipendenze necessarie per la distribuzione di applicazioni in System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Dipendenza|Altre informazioni|  
|------------------|----------------------|  
|Internet Information Services (IIS) è richiesto nei server del sistema del sito che eseguono il punto per siti Web del Catalogo applicazioni, il punto per servizi Web del Catalogo applicazioni, il punto di gestione e il punto di distribuzione.|Per altre informazioni su questo requisito, vedere [Configurazioni supportate](../../core/plan-design/configs/supported-configurations.md).|  
|Per i dispositivi mobili registrati da Configuration Manager:|Quando si firmano con codice le applicazioni per distribuirle nei dispositivi mobili, non utilizzare un certificato generato tramite un modello della versione 3 (**Windows Server 2008, Enterprise Edition**). Questo modello di certificato crea un certificato non compatibile con le applicazioni di Configuration Manager per dispositivi mobili.<br /><br /> Se si utilizzano i Servizi certificati Active Directory per firmare con codice le applicazioni per dispositivi mobili, non utilizzare un modello di certificato della versione 3.|  
|Se si desidera creare automaticamente le affinità utente dispositivo, i client devono essere configurati per il controllo degli eventi di accesso.|Configuration Manager legge le due impostazioni seguenti dai criteri di sicurezza locali nei computer client per determinare le affinità utente dispositivo automatiche:<br /><br /> **Controlla eventi di accesso account**<br /><br /> **Controlla eventi di accesso**<br /><br /> Per creare automaticamente relazioni tra utenti e dispositivi, verificare che queste due impostazioni siano attivate nei computer client. Per configurare queste impostazioni, è possibile usare i criteri di gruppo di Windows.|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager   

|Dipendenza|Altre informazioni|  
|------------------|----------------------|  
|Punto di gestione|I client contattano un punto di gestione per scaricare i criteri client, individuare il contenuto e connettersi al Catalogo applicazioni.<br /><br /> Se i client non possono accedere a un punto di gestione, non potranno utilizzare il Catalogo applicazioni.|  
|Punto di distribuzione|Prima di poter distribuire le applicazioni ai client, è necessario disporre di almeno un punto di distribuzione nella gerarchia. Per impostazione predefinita, durante un'installazione standard nel server del sito è attivato un ruolo del sito del punto di distribuzione. Il numero e la posizione dei punti di distribuzione varia in base ai requisiti specifici dell'azienda.<br /><br /> Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Impostazioni client|Esistono numerose impostazioni client che controllano la modalità di installazione delle applicazioni nel client e l'esperienza dell'utente finale nel client. Queste impostazioni client includono:<br /><br /> - Agente computer<br /><br /> - Riavvio del computer<br /><br /> - Distribuzione software<br /><br /> - Affinità dispositivi e utenti<br /><br /> Per altre informazioni sulle impostazioni client, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Per altre informazioni su come configurare le impostazioni client, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).|  
|Per il Catalogo applicazioni:<br /><br /> Account utente rilevati|Gli utenti devono essere rilevati da Configuration Manager prima di poter visualizzare e richiedere le applicazioni dal Catalogo applicazioni. Per altre informazioni, vedere [Eseguire l'individuazione](/sccm/core/servers/deploy/configure/run-discovery).|  
|App-V 4.6 SP1 o client successivo per l'esecuzione di applicazioni virtuali|Per poter creare applicazioni virtuali in Configuration Manager, è necessario che i computer client abbiano App-V 4.6 SP1 o un client successivo installato.<br /><br /> Inoltre, per poter distribuire applicazioni virtuali è necessario aggiornare il client App-V con l'aggiornamento rapido descritto nell' [articolo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) della Knowledge Base.|  
|Punto per servizi Web del Catalogo applicazioni|Il punto per servizi Web del Catalogo applicazioni è un ruolo del sistema del sito che fornisce informazioni sul software disponibile nella Raccolta software del sito Web del Catalogo applicazioni.<br /><br /> Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center e il Catalogo applicazioni (solo PC Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in questo argomento.|  
|Punto per siti Web del Catalogo applicazioni|Il punto del sito Web del Catalogo applicazioni è un ruolo del sistema del sito che offre agli utenti un elenco del software disponibile.<br /><br /> Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center e il Catalogo applicazioni (solo PC Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in questo argomento.|  
|Punto di Reporting Services|Per usare i report in Configuration Manager per la gestione delle applicazioni, è necessario installare e configurare prima un punto di Reporting Services.<br /><br /> Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Autorizzazioni di sicurezza per la gestione delle applicazioni|È necessario disporre delle seguenti autorizzazioni di sicurezza per gestire le applicazioni.<br /><br /> Il ruolo sicurezza **Autore applicazioni** include le autorizzazioni elencate precedentemente, necessarie per creare, modificare e disattivare le applicazioni in Configuration Manager.<br /><br /> **Per distribuire le applicazioni:**<br /><br /> Il ruolo sicurezza **Gestione distribuzione applicazioni** include le autorizzazioni elencate precedentemente, necessarie per distribuire le applicazioni in Configuration Manager.<br /><br /> Il ruolo di sicurezza **Amministratore applicazione** contiene tutte le autorizzazioni da entrambi i ruoli di sicurezza: **Autore applicazioni** e **Gestione distribuzione applicazioni** .<br /><br /> Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurare Software Center e il Catalogo applicazioni (solo PC Windows)  

 In System Center Configuration Manager sono ora disponibili due opzioni per la modifica delle impostazioni, la ricerca e l'installazione di applicazioni:  

-   **Nuovo Software Center** : il nuovo Software Center ha un aspetto nuovo e moderno, e le app che venivano visualizzate solo nel Catalogo applicazioni dipendente da Silverlight (app disponibili per gli utenti) ora vengono visualizzate in Software Center nella scheda **Applicazioni** . È ancora possibile accedere al Catalogo applicazioni con il collegamento disponibile nella scheda **Stato dell'installazione** di Software Center.  

     È possibile configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** > **Usa il nuovo Software Center**.  

    > [!IMPORTANT]  
    >  Anche se non è più necessario che gli utenti finali si connettano al Catalogo applicazioni, occorre comunque configurare il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni come indicato di seguito.  

-   **Precedente Software Center e il Catalogo applicazioni** : per impostazione predefinita, gli utenti continuano a connettersi alla versione precedente di Software Center e al Catalogo applicazioni (è necessario il Web browser abilitato per Silverlight) per cercare le applicazioni disponibili.  

 Indipendentemente dalla versione che si sceglie di usare, Software Center viene installato automaticamente quando si installa il client di Configuration Manager nei PC Windows.  

> [!TIP]  
>  La versione di Software Center visualizzata dagli utenti si basa sulle impostazioni client di Configuration Manager. Questo offre la flessibilità necessaria per controllare la versione usata in base alle impostazioni client personalizzate che vengono distribuite nella raccolta.  

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Passaggi per installare e configurare il Catalogo applicazioni e Software Center  

> [!IMPORTANT]  
>  Prima di eseguire questi passaggi, assicurarsi di aver soddisfatto tutti i prerequisiti elencati in precedenza.  

|Passaggi|Dettagli|Altre informazioni|  
|-----------|-------------|----------------------|  
|**Passaggio 1:** se si intende utilizzare le connessioni HTTPS, assicurarsi di aver distribuito un certificato server Web ai server del sistema del sito.|Distribuire un certificato server Web ai server del sistema del sito che eseguiranno il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni.<br /><br /> Inoltre, se si desidera che i client accedano al Catalogo applicazione da Internet, distribuire un certificato server Web ad almeno un server del sistema del sito del punto di gestione e configurarlo per le connessioni client da Internet.|Per altre informazioni sui requisiti del certificato PKI, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passaggio 2:** se si intende utilizzare un certificato PKI del client per le connessioni ai punti di gestione, distribuire un certificato di autenticazione client ai computer client.|Anche se i client non devono utilizzare un certificato PKI del client per connettersi al Catalogo applicazioni, è necessario che si connettano a un punto di gestione prima di poter utilizzare il Catalogo applicazioni. È necessario distribuire un certificato di autenticazione client ai computer client nei seguenti scenari:<br /><br /> - Tutti i punti di gestione in Intranet accettano solo connessioni client HTTPS.<br /><br /> - I client eseguiranno la connessione al Catalogo applicazioni da Internet.|Per altre informazioni sui requisiti del certificato PKI, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passaggio 3:** installare e configurare il punto per servizi Web del Catalogo applicazioni e il sito Web del Catalogo applicazioni.|È necessario installare entrambi i ruoli del sistema del sito nello stesso sito. Non è necessario installarli nello stesso server del sistema del sito o nella stessa foresta Active Directory. Il punto per servizi Web del Catalogo applicazioni deve tuttavia trovarsi nella stessa foresta del database del sito.|Per altre informazioni sul posizionamento dei ruoli di sistema del sito, vedere [Pianificare i server e i ruoli di sistema del sito](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Per configurare il punto di servizi Web del Catalogo applicazioni e il punto di siti Web del Catalogo applicazioni, vedere **Passaggio 3: Installazione e configurazione dei ruoli del sistema del sito del Catalogo applicazioni**.|  
|**Passaggio 4** : Configurare le impostazioni client per il Catalogo applicazioni e Software Center.|Configurare le impostazioni client predefinite se si desidera che tutti gli utenti abbiano la stessa impostazione. In caso contrario, configurare le impostazioni client personalizzate per raccolte specifiche.|Per altre informazioni sulle impostazioni client, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Per informazioni su come configurare queste impostazioni client, vedere: **Passaggio 4: Configurazione delle impostazioni client per il Catalogo applicazioni e Software Center**.|  
|**Passaggio 5** : Verificare che il Catalogo applicazioni sia operativo.|È possibile accedere direttamente al Catalogo applicazioni da un browser o da Software Center.|Vedere **Passaggio 5: Verificare che il Catalogo applicazioni sia operativo**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedure aggiuntive per installare e configurare il Catalogo applicazioni e Software Center  
 Usare le seguenti informazioni quando i passaggi indicati nella tabella precedente richiedono procedure aggiuntive.  

###  <a name="step-3-installing-and-configuring-the-application-catalog-site-system-roles"></a>Passaggio 3: installazione e configurazione dei ruoli del sistema del sito del Catalogo applicazioni  
 Queste procedure consentono di configurare i ruoli del sistema del sito per il Catalogo applicazioni. Scegliere una delle 2 procedure seguenti a seconda che si installi un nuovo server di sistema del sito oppure si usi un server di sistema del sito esistente:  

> [!NOTE]  
>  È impossibile installare il Catalogo applicazioni in un sito secondario o in un sito di amministrazione centrale.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Per installare e configurare i sistemi del sito del Catalogo applicazioni: nuovo server del sistema del sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Server e ruoli di sistema del sito**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Se si desidera che i computer client accedano al Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto per servizi Web del Catalogo applicazioni** e **Punto per siti Web del Catalogo applicazioni** dall'elenco dei ruoli disponibili e quindi fare clic su **Avanti**.  

6.  Completare la procedura guidata.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Per installare e configurare i sistemi del sito del Catalogo applicazioni: server del sistema del sito esistente  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e selezionare il server da usare per il Catalogo applicazioni.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**.  

    > [!TIP]  
    >  Se si desidera che i computer client accedano al Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto per servizi Web del Catalogo applicazioni** e **Punto per siti Web del Catalogo applicazioni** dall'elenco dei ruoli disponibili e quindi fare clic su **Avanti**.  

6.  Completare la procedura guidata.  

 Verificare l'installazione di questi ruoli del sistema del sito utilizzando i messaggi di stato e riesaminando i file di log:  

1.  Messaggi di stato: Utilizzare i componenti **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

     Ad esempio, l'ID stato **1015** per **SMS_PORTALWEB_CONTROL_MANAGER** conferma che Gestione componenti del sito ha completato l'installazione del punto per siti Web del Catalogo applicazioni.  

2.  File di log: cercare **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

     Per ulteriori informazioni, cercare i file di log **awebsvcMSI.log** e **portlwebMSI.log**.  

###  <a name="step-4-configuring-the-client-settings-for-the-application-catalog-and-software-center"></a>Passaggio 4: Configurazione delle impostazioni client per il Catalogo applicazioni e Software Center  
 Questa procedura consente di configurare le impostazioni client predefinite per il Catalogo applicazioni e Software Center che verranno applicate a tutti i dispositivi nella gerarchia. Se si desidera applicare queste impostazioni solo ad alcuni dispositivi, è possibile creare un'impostazione client personalizzata e distribuirla a una raccolta che contenga i dispositivi a cui sono destinate le impostazioni specifiche. Per ulteriori informazioni su come creare un'impostazione client personalizzata, vedere la sezione [How to Create and Deploy Custom Client Settings](../../core/clients/deploy/configure-client-settings.md#BKMK_CustomClientSettings) nell'argomento [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) .  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Riesaminare e configurare le impostazioni relative a notifiche utente, Catalogo applicazioni e Software Center. Ad esempio:  

    1.  Gruppo**Agente computer** :  

        -   **Punto per siti Web del Catalogo applicazioni predefinito**  

        -   **Aggiungere il sito Web del Catalogo applicazioni predefinito all'area siti attendibili di Internet Explorer**  

        -   **Nome organizzazione visualizzato in Software Center**  

            > [!TIP]  
            >  Per specificare il nome dell'organizzazione visualizzato nel Catalogo applicazioni e configurare il tema del sito Web, utilizzare la scheda **Personalizzazione** nelle proprietà del sito Web del Catalogo applicazioni.  

        -   **Usa il nuovo Software Center** : impostare su **Sì** se si vuole usare il nuovo Software Center che consente agli utenti finali di cercare e installare le app disponibili senza dover accedere al Catalogo applicazioni (che richiede un Web browser abilitato per Silverlight).  

        -   **Autorizzazioni di installazione**  

        -   **Mostra notifiche per nuove distribuzioni**  

    2.  Gruppo**Risparmio energia** :  

        -   **Consentire agli utenti di escludere il dispositivo usato dal risparmio energia**  

    3.  Gruppo**Strumenti remoti** :  

        -   **Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center**  

    4.  Gruppo**Affinità dispositivi e utenti** :  

        -   **Consentire all'utente di definire i dispositivi primari**  

    > [!NOTE]  
    >  Per ulteriori informazioni sulle impostazioni client, vedere [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni client predefinite** .  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Come gestire i client](../../core/clients/manage/manage-clients.md).  

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passaggio 5: Verificare che il Catalogo applicazioni sia operativo  
 Utilizzare le seguenti procedure per verificare che il Catalogo applicazioni sia operativo. È possibile accedere direttamente al Catalogo applicazioni da un browser o da Software Center.  

> [!NOTE]  
>  Il Catalogo applicazioni richiede Microsoft Silverlight, che viene installato automaticamente come prerequisito del client di Configuration Manager. Se si accede al Catalogo applicazioni direttamente da un browser usando un computer senza il client di Configuration Manager, verificare prima che Microsoft Silverlight sia installato nel computer.  

> [!TIP]  
>  I prerequisiti mancanti sono tra le cause più comuni di malfunzionamento del Catalogo applicazioni dopo l'installazione. Verificare i prerequisiti del ruolo del sistema del sito per i ruoli del sistema del sito del Catalogo applicazioni. A questo scopo leggere l'argomento [Configurazioni supportate](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Se l'accesso è stato eseguito usando un account di amministratore di dominio, i messaggi di notifica dal client di Configuration Manager, ad esempio quelli che indicano che è disponibile nuovo software, non verranno visualizzati.  

### <a name="to-access-the-application-catalog-directly-from-a-browser"></a>Per accedere al Catalogo applicazioni direttamente da un browser  

-   In un browser, digitare l'indirizzo del sito Web del Catalogo applicazioni e verificare che nella pagina Web siano presenti tre schede: **Catalogo applicazioni**, **Richieste di applicazioni**e **Dispositivi personali**.  

     Selezionare tra i seguenti indirizzi quello appropriato per il Catalogo applicazioni, tenendo presente che <server\> è il nome del computer, l'FQDN Intranet o l'FQDN Internet:  

    -   Connessioni client HTTPS e impostazioni predefinite del ruolo del sistema del sito: **https://<server\>/CMApplicationCatalog**  

    -   Connessioni client HTTP e impostazioni predefinite del ruolo del sistema del sito: **http://<server\>/CMApplicationCatalog**  

    -   Connessioni client HTTPS e impostazioni personalizzate del ruolo del sistema del sito: **https://<server\>:<porta\>/<nome applicazione Web\>**  

    -   Connessioni client HTTP e impostazioni personalizzate del ruolo del sistema del sito: **http://<server\>:<porta\>/<nome applicazione Web\>**  

### <a name="to-access-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Per accedere al Catalogo applicazioni da Software Center (non si applica alla nuova versione di Software Center)  

1.  In un computer client fare clic su **Start** > **Tutti i programmi** > **Microsoft System Center 2012** > **Configuration Manager** > **Software Center**.  

2.  Se in precedenza è stato configurato un nome organizzazione per Software Center come impostazione client, verificare che venga visualizzato come specificato.  

3.  Fare clic su **Trova applicazioni aggiuntive dal catalogo delle applicazioni** e verificare che nella pagina siano presenti tre schede: **Catalogo applicazioni**, **Richieste di applicazioni**e **Dispositivi personali**.  

> [!WARNING]  
>  Dopo aver installato i ruoli del sistema del sito del Catalogo applicazioni, il Catalogo non verrà visualizzato immediatamente facendo clic sul collegamento **Trova applicazioni aggiuntive dal catalogo delle applicazioni** da Software Center. Il Catalogo applicazioni diventa disponibile in Software Center al successivo download dei criteri client da parte del client oppure dopo un massimo di 25 ore dall'installazione dei ruoli del sistema del sito del Catalogo applicazioni.  



<!--HONumber=Nov16_HO1-->


