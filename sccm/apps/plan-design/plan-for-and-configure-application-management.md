---
title: Pianificare e configurare la gestione delle applicazioni
titleSuffix: Configuration Manager
description: Implementare e configurare le dipendenze necessarie per la distribuzione di applicazioni in System Center Configuration Manager.
ms.date: 11/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18d9fe80a1c5525457579dadbfeaeafa3425202d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni incluse in questo articolo per implementare le dipendenze necessarie per la distribuzione di applicazioni in System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dipendenze esterne a Configuration Manager  

|Dipendenza|Altre informazioni|  
|------------------|----------------------|  
|Internet Information Services (IIS) è richiesto nei server del sistema del sito che eseguono il punto per siti Web del Catalogo applicazioni, il punto per servizi Web del Catalogo applicazioni, il punto di gestione e il punto di distribuzione.|Per altre informazioni su questo requisito, vedere [Configurazioni supportate](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivi mobili registrati da Configuration Manager|Per firmare un'applicazione con codice per distribuirla nei dispositivi mobili, non usare un certificato generato tramite un modello della versione 3 (**Windows Server 2008, Enterprise Edition**). Questo modello di certificato crea un certificato non compatibile con le applicazioni di Configuration Manager per dispositivi mobili.<br /><br /> Se si usano i Servizi certificati Active Directory per firmare con codice applicazioni per dispositivi mobili, non usare un modello di certificato della versione 3.|  
|Se si vuole creare automaticamente le affinità utente dispositivo, i client devono essere configurati per il controllo degli eventi di accesso.|Il client di Configuration Manager legge gli eventi di accesso di tipo **Riuscito** dal registro eventi di sicurezza del PC per determinare le affinità utente-dispositivo automatiche.  Questi eventi vengono abilitati dai due criteri di controllo seguenti:<br>**Controlla eventi di accesso account**<br>**Controlla eventi di accesso**<br>Per creare automaticamente relazioni tra utenti e dispositivi, verificare che queste due impostazioni siano attivate nei computer client. Per configurare queste impostazioni, è possibile usare i criteri di gruppo di Windows.|  

## <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager   

|Dipendenza|Altre informazioni|  
|------------------|----------------------|  
|Punto di gestione|I client contattano un punto di gestione per scaricare i criteri client, individuare il contenuto e connettersi al Catalogo applicazioni.<br /><br /> Se i client non possono accedere a un punto di gestione, non potranno usare il Catalogo applicazioni.|  
|Punto di distribuzione|Prima di poter distribuire le applicazioni ai client, è necessario disporre di almeno un punto di distribuzione nella gerarchia. Per impostazione predefinita, durante un'installazione standard nel server del sito è attivato un ruolo del sito del punto di distribuzione. Il numero e la posizione dei punti di distribuzione varia in base ai requisiti specifici dell'azienda.<br /><br /> Per altre informazioni su come installare i punti di distribuzione e gestire il contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Impostazioni client|Esistono numerose impostazioni client che controllano la modalità di installazione delle applicazioni nel client e l'esperienza dell'utente nel client. Queste impostazioni client includono:<br /><br /><ul><li>Agente computer</li><li>Riavvio del computer</li><li>Distribuzione software</li><li>Affinità utente-dispositivo</li></ul> Per altre informazioni sulle impostazioni client, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Per altre informazioni su come configurare le impostazioni client, vedere [Come configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).|  
|Account utente individuati per il Catalogo applicazioni |Prima che gli utenti possano visualizzare e richiedere applicazioni dal Catalogo applicazioni, Configuration Manager deve individuare gli account utente. Per altre informazioni, vedere [Eseguire l'individuazione](/sccm/core/servers/deploy/configure/run-discovery).|  
|App-V 4.6 SP1 o client successivo per l'esecuzione di applicazioni virtuali|Per creare applicazioni virtuali in Configuration Manager, è necessario che nei computer sia installato un client App-V 4.6 SP1 o versione successiva.<br /><br /> Per poter distribuire applicazioni virtuali è necessario anche aggiornare il client App-V con l'aggiornamento rapido descritto nell'[articolo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) della Knowledge Base.|  
|Punto per servizi Web del Catalogo applicazioni|Il punto per servizi Web del Catalogo applicazioni è un ruolo del sistema del sito che fornisce informazioni sul software disponibile nella Raccolta software del sito Web del Catalogo applicazioni.<br /><br /> Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center e il Catalogo applicazioni (solo PC Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in questo articolo.|  
|Punto per siti Web del Catalogo applicazioni|Il punto del sito Web del Catalogo applicazioni è un ruolo del sistema del sito che offre agli utenti un elenco del software disponibile.<br /><br /> Per altre informazioni su come configurare il ruolo del sistema del sito, vedere [Configurare Software Center e il Catalogo applicazioni (solo PC Windows)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) in questo articolo.|  
|Punto di Reporting Services|Per usare i report in Configuration Manager per la gestione delle applicazioni, è prima necessario installare e configurare un punto di Reporting Services.<br /><br /> Per altre informazioni, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Autorizzazioni di sicurezza per la gestione delle applicazioni|Per gestire le applicazioni, sono necessarie le autorizzazioni di sicurezza seguenti:<br /><br /> Il ruolo sicurezza **Autore applicazioni** include le autorizzazioni elencate in precedenza, necessarie per creare, modificare e disattivare le applicazioni in Configuration Manager.<br /><br /> **Per distribuire le applicazioni:**<br /><br /> Il ruolo sicurezza **Gestione distribuzione applicazioni** include le autorizzazioni elencate precedentemente, necessarie per distribuire le applicazioni in Configuration Manager.<br /><br /> Il ruolo sicurezza **Amministratore applicazione** dispone di tutte le autorizzazioni da entrambi i ruoli sicurezza: **Autore applicazioni** e **Gestione distribuzione applicazioni**.<br /><br /> Per altre informazioni, vedere [Configurare un'amministrazione basata su ruoli](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurare Software Center e il Catalogo applicazioni (solo PC Windows)  

 In System Center Configuration Manager sono ora disponibili due opzioni per la modifica delle impostazioni: la ricerca e l'installazione di applicazioni.  

-   **Nuovo Software Center**: il nuovo Software Center ha un aspetto rinnovato e moderno e le app che venivano visualizzate solo nel Catalogo applicazioni dipendente da Silverlight (app disponibili per gli utenti) vengono visualizzate ora in Software Center nella scheda **Applicazioni**. È ancora possibile accedere al Catalogo applicazioni con il collegamento disponibile nella scheda **Stato dell'installazione** di Software Center.  

     È possibile configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** > **Usa il nuovo Software Center**.  

    > [!IMPORTANT]  
    >  Anche se non è più necessario connettersi al Catalogo applicazioni, occorre comunque configurare il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni, come indicato nella sezione successiva.  

-   **Software Center precedente e Catalogo applicazioni**: per impostazione predefinita, gli utenti continuano a connettersi alla versione precedente di Software Center e al Catalogo applicazioni (è necessario un Web browser abilitato per Silverlight) per cercare le applicazioni disponibili.  

 Indipendentemente dalla versione che si sceglie di usare, Software Center viene installato automaticamente quando si installa il client di Configuration Manager nei PC Windows.  

    > [!TIP]  
    >  La versione di Software Center visualizzata dagli utenti si basa sulle impostazioni client di Configuration Manager. Questo offre la flessibilità necessaria per controllare la versione usata in base alle impostazioni client personalizzate che vengono distribuite in una raccolta. 

    > [!IMPORTANT]
    > Nei prossimi mesi verrà pertanto rimossa la versione precedente di Software Center, che non sarà più disponibile.
    > È possibile configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** > **Usa il nuovo Software Center**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Passaggi per installare e configurare il Catalogo applicazioni e Software Center  

> [!IMPORTANT]  
>  Prima di eseguire questa procedura, assicurarsi di aver soddisfatto tutti i prerequisiti elencati in precedenza.  

|Passaggi|Dettagli|Altre informazioni|  
|-----------|-------------|----------------------|  
|**Passaggio 1:** se si usano connessioni HTTPS, assicurarsi di aver distribuito un certificato del server Web ai server del sistema del sito.|Distribuire un certificato server Web ai server del sistema del sito che eseguiranno il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni.<br /><br /> Se si vuole che i client usino il Catalogo applicazioni da Internet, distribuire anche un certificato server Web ad almeno un server del sistema del sito del punto di gestione e configurarlo per le connessioni client da Internet.|Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passaggio 2:** se si usa un certificato PKI client per le connessioni ai punti di gestione, distribuire un certificato di autenticazione client ai computer client.|Anche se i client non usano un certificato PKI del client per connettersi al Catalogo applicazioni, è necessario che si connettano a un punto di gestione prima di poter usare il Catalogo applicazioni. È necessario distribuire un certificato di autenticazione client ai computer client nei seguenti scenari:<br /><br /><ul><li>Tutti i punti di gestione in Intranet accettano solo connessioni client HTTPS.</li><li>I client eseguono la connessione al Catalogo applicazioni da Internet.</li></ul>|Per altre informazioni sui requisiti del certificato, vedere [Requisiti dei certificati PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Passaggio 3:** installare e configurare il punto per servizi Web del Catalogo applicazioni e il sito Web del Catalogo applicazioni.|È necessario installare entrambi i ruoli del sistema del sito nello stesso sito. Non è necessario installarli nello stesso server del sistema del sito o nella stessa foresta Active Directory. Il punto per servizi Web del Catalogo applicazioni deve trovarsi tuttavia nella stessa foresta del database del sito.|Per altre informazioni sul posizionamento dei ruoli di sistema del sito, vedere [Pianificare i server e i ruoli di sistema del sito](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Per configurare il punto di servizi Web del Catalogo applicazioni e il punto di siti Web del Catalogo applicazioni, vedere **Passaggio 3: Installare e configurare i ruoli del sistema del sito del Catalogo applicazioni**.|  
|**Passaggio 4** : Configurare le impostazioni client per il Catalogo applicazioni e Software Center.|Configurare le impostazioni client predefinite se si desidera che tutti gli utenti abbiano la stessa impostazione. In caso contrario, configurare le impostazioni client personalizzate per raccolte specifiche.|Per altre informazioni sulle impostazioni client, vedere [Informazioni sulle impostazioni client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Per altre informazioni su come configurare queste impostazioni client, vedere: **Passaggio 4: Configurare le impostazioni client per il Catalogo applicazioni e Software Center**.|  
|**Passaggio 5** : Verificare che il Catalogo applicazioni sia operativo.|È possibile usare direttamente il Catalogo applicazioni da un browser o da Software Center.|Vedere **Passaggio 5: Verificare che il Catalogo applicazioni sia operativo**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedure aggiuntive per installare e configurare il Catalogo applicazioni e Software Center  
 Usare le seguenti informazioni quando i passaggi indicati nella tabella precedente richiedono procedure aggiuntive.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Passaggio 3: Installare e configurare i ruoli del sistema del sito del Catalogo applicazioni  
 Queste procedure consentono di configurare i ruoli del sistema del sito per il Catalogo applicazioni. Scegliere una delle due procedure seguenti a seconda che si installi un nuovo server di sistema del sito oppure si usi un server di sistema del sito esistente:  

> [!NOTE]  
>  È impossibile installare il Catalogo applicazioni in un sito secondario o in un sito di amministrazione centrale.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Per installare e configurare i sistemi del sito del Catalogo applicazioni: nuovo server del sistema del sito  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Configurazione del sito** > **Server e ruoli di sistema del sito**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi scegliere **Avanti**.  

    > [!TIP]  
    >  Se si vuole che i computer client usino il Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto per servizi Web del Catalogo applicazioni** e **Punto per siti Web del Catalogo applicazioni** dall'elenco dei ruoli disponibili e quindi scegliere **Avanti**.  

6.  Completare i passaggi rimanenti.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Per installare e configurare i sistemi del sito del Catalogo applicazioni: server del sistema del sito esistente  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e scegliere il server da usare per il Catalogo applicazioni.  

3.  Nella scheda **Home**, nel gruppo **Server**, scegliere **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi scegliere **Avanti**.  

    > [!TIP]  
    >  Se si vuole che i computer client usino il Catalogo applicazioni su Internet, specificare il nome di dominio completo (FQDN) per Internet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto per servizi Web del Catalogo applicazioni** e **Punto per siti Web del Catalogo applicazioni** dall'elenco dei ruoli disponibili e quindi scegliere **Avanti**.  

6.  Completare i passaggi rimanenti.  

7. Verificare l'installazione di questi ruoli del sistema del sito utilizzando i messaggi di stato e riesaminando i file di log:  

    Messaggi di stato: Utilizzare i componenti **SMS_PORTALWEB_CONTROL_MANAGER** e **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Ad esempio, l'ID stato **1015** per **SMS_PORTALWEB_CONTROL_MANAGER** conferma che Gestione componenti del sito ha completato l'installazione del punto per siti Web del Catalogo applicazioni.  

    File di log: cercare **SMSAWEBSVCSetup.log** e **SMSPORTALWEBSetup.log**.  

    Per altre informazioni, cercare i file di log **awebsvcMSI.log** e **portlwebMSI.log**.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Passaggio 4: Configurare le impostazioni client per il Catalogo applicazioni e Software Center  
 Questa procedura consente di configurare le impostazioni client predefinite per il Catalogo applicazioni e Software Center applicabili a tutti i dispositivi nella gerarchia. Se si vogliono applicare queste impostazioni solo ad alcuni dispositivi, è possibile creare un'impostazione client personalizzata e distribuirla a una raccolta che contenga i dispositivi con le impostazioni specifiche. Per altre informazioni su come creare un'impostazione personalizzata per dispositivi, vedere la sezione [Creare e distribuire impostazioni client personalizzate](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) in [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Impostazioni client** > **Impostazioni client predefinite**.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Riesaminare e configurare le impostazioni relative a notifiche utente, Catalogo applicazioni e Software Center. Ad esempio:  

    1.  Gruppo**Agente computer** :  

        -   **Punto per siti Web del Catalogo applicazioni predefinito**.  

        -   **Aggiungere il sito Web del Catalogo applicazioni predefinito all'area siti attendibili di Internet Explorer**.  

        -   **Nome organizzazione visualizzato in Software Center**.  

            > [!TIP]  
            >  Per specificare il nome dell'organizzazione visualizzato nel Catalogo applicazioni e configurare il tema del sito Web, usare la scheda **Personalizzazione** nelle proprietà del sito Web del Catalogo applicazioni.  

        -   **Usa il nuovo Software Center**. Impostare su **Sì** se si vuole usare il nuovo Software Center, che consente agli utenti di cercare e installare le app disponibili senza dover accedere al Catalogo applicazioni, che richiede un Web browser abilitato per Silverlight.  

        -   **Autorizzazioni di installazione**.  

        -   **Mostra notifiche per nuove distribuzioni**.  

    2.  Gruppo**Risparmio energia** :  

        -   **Consentire agli utenti di escludere il dispositivo usato dal risparmio energia**.  

    3.  Gruppo**Strumenti remoti** :  

        -   **Gli utenti possono modificare le impostazioni di criteri o notifiche in Software Center**.  

    4.  Gruppo**Affinità dispositivi e utenti** :  

        -   **Consentire all'utente di definire i dispositivi primari**.  

    > [!NOTE]  
    >  Per ulteriori informazioni sulle impostazioni client, vedere [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Scegliere **OK** per chiudere la finestra di dialogo **Impostazioni client predefinite**.  

I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per iniziare il recupero dei criteri per un singolo client, vedere [Come gestire i client](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Per personalizzare Software Center

In Software Center la personalizzazione viene applicata secondo le regole seguenti:

1. Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni non è installato, Software Center visualizzerà il nome dell'organizzazione specificato nell'impostazione **Nome organizzazione visualizzato in Software Center** del client **Agente computer**. Per istruzioni, vedere [Come configurare le impostazioni client](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni è installato, Software Center visualizzerà il nome dell'organizzazione e il colore specificati nelle proprietà del ruolo del server del sito punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Configuration options for Application Catalog website point](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website) (Opzioni di configurazione per il punto per siti Web del Catalogo applicazioni).
3. Se una sottoscrizione di Microsoft Intune è configurata e connessa a Configuration Manager, Software Center visualizzerà il nome dell'organizzazione, il colore e il logo aziendale specificati nelle proprietà della sottoscrizione di Intune. Per ulteriori informazioni, vedere [Configuring the Microsoft Intune subscription](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

#### <a name="to-manually-set-software-center-branding"></a>Per impostare manualmente la personalizzazione di Software Center
<!-- 1351224 -->
Con la versione 1710, è possibile aggiungere manualmente elementi di personalizzazione aziendale e specificare la visibilità delle schede in Software Center. È possibile aggiungere il nome specifico della società per Software Center, impostare un tema di colori per la configurazione di Software Center, impostare il logo della società e impostare le schede visibili per i dispositivi client.

1. Nella console di **Configuration Manager** scegliere **Amministrazione** > **Impostazioni client**. Fare clic sull'istanza di impostazione client desiderata.
2. Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.
3. Nella finestra di dialogo **Impostazioni predefinite** scegliere **Software Center**.
4. Selezionare **Sì** per **scegliere le nuove impostazioni per specificare informazioni sulla società**, in modo da abilitare le impostazioni di personalizzazione di Software Center.
5. Digitare il **nome della società**.
6. Selezionare la **combinazione colori per Software Center**.
7. Fare clic su **Sfoglia** per accedere al logo per Software Center. Il logo deve essere di 400 x 100 pixel, nel formato JPEG o PNG e con dimensioni massime di 750 KB.
8. Selezionare **SÌ** per rendere visibili le schede in Software Center per i dispositivi client. È necessario che sia visibile almeno una scheda:

    -  Scheda Enable Applications (Abilita applicazioni)
    -  Scheda Abilita aggiornamenti
    -  Scheda Enable Operating Systems (Abilita sistemi operativi)
    -  Scheda Enable Installation Status (Abilita stato installazione)
    -  Scheda Enable Device compliance (Abilita conformità dispositivo)
    -  Scheda Enable Options (Abilita opzioni)

> [!IMPORTANT]  
>  La personalizzazione di Software Center viene sincronizzata con il servizio Intune ogni 14 giorni. È possibile quindi che le modifiche apportate in Intune vengano visualizzate in Configuration Manager con un certo ritardo.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Passaggio 5: Verificare che il Catalogo applicazioni sia operativo  
 Utilizzare le seguenti procedure per verificare che il Catalogo applicazioni sia operativo. È possibile usare direttamente il Catalogo applicazioni da un browser o da Software Center.  

> [!NOTE]  
>  Il Catalogo applicazioni richiede Microsoft Silverlight, che viene installato automaticamente come prerequisito del client di Configuration Manager. Se si usa il Catalogo applicazioni direttamente da un browser usando un computer senza il client di Configuration Manager, verificare prima che Microsoft Silverlight sia installato nel computer.  

> [!TIP]  
>  La non aderenza ai prerequisiti è una delle più comuni cause di malfunzionamento del Catalogo applicazioni dopo l'installazione. Verificare i prerequisiti del ruolo del sistema del sito per i ruoli del sistema del sito del Catalogo applicazioni. A questo scopo, leggere l'articolo [Configurazioni supportate](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Se l'accesso è stato eseguito usando un account di amministratore di dominio, i messaggi di notifica dal client di Configuration Manager, ad esempio quelli che indicano che è disponibile nuovo software, non verranno visualizzati.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Per usare il Catalogo applicazioni direttamente da un browser  

-   In un browser specificare l'indirizzo del sito Web del Catalogo applicazioni e verificare che nella pagina Web siano presenti tre schede: **Catalogo applicazioni**, **Richieste di applicazioni** e **Dispositivi personali**.  

     Selezionare tra gli indirizzi seguenti quello appropriato per il Catalogo applicazioni, tenendo presente che &lt;server&gt; è il nome del computer, l'FQDN Intranet o l'FQDN Internet:  

    -   Connessioni client HTTPS e impostazioni predefinite del ruolo del sistema del sito: **https://&lt;server&gt;/CMApplicationCatalog**  

    -   Connessioni client HTTP e impostazioni predefinite del ruolo del sistema del sito: **http://&lt;server&gt;/CMApplicationCatalog**  

    -   Connessioni client HTTPS e impostazioni personalizzate del ruolo del sistema del sito: **https://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

    -   Connessioni client HTTP e impostazioni personalizzate del ruolo del sistema del sito: **http://&lt;server&gt;:&lt;port&gt;/&lt;web application name&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Per usare il Catalogo applicazioni da Software Center (non si applica alla nuova versione di Software Center)  

1.  In un computer selezionare **Start** > **Tutti i programmi** > **Microsoft System Center 2012** > **Configuration Manager** > **Software Center**.  

2.  Se in precedenza è stato configurato un nome organizzazione per Software Center come impostazione client, verificare che venga visualizzato come specificato.  

3.  Selezionare **Trova applicazioni aggiuntive dal catalogo delle applicazioni** e verificare che nella pagina siano presenti tre schede: **Catalogo applicazioni**, **Richieste di applicazioni** e **Dispositivi personali**.  

> [!WARNING]  
>  Dopo aver installato i ruoli del sistema del sito del Catalogo applicazioni, il Catalogo non verrà visualizzato immediatamente selezionando **Trova applicazioni aggiuntive dal catalogo delle applicazioni** da Software Center. Il Catalogo applicazioni diventa disponibile in Software Center al successivo download dei criteri client da parte del client oppure dopo un massimo di 25 ore dall'installazione dei ruoli del sistema del sito del Catalogo applicazioni.  
