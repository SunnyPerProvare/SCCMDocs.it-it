---
title: Creare profili di connessione remota
titleSuffix: Configuration Manager
description: Usare i profili di connessione remota di System Center Configuration Manager per consentire agli utenti di connettersi in modalità remota ai computer aziendali.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5cdb08070c13feed573a947ba1f5ccf6a47b3e1
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62214550"
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Profili di connessione remota in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare i profili di connessione remota in System Center Configuration Manager per consentire agli utenti di connettersi in modalità remota ai computer aziendali quando non sono connessi al dominio o se i loro PC sono connessi tramite Internet.  

 Gli utenti possono connettersi al PC di lavoro dai seguenti tipi di dispositivo:  

-   Computer che eseguono Microsoft Windows  

-   Dispositivi che eseguono iOS  

-   Dispositivi che eseguono Android  

I profili di connessione remota consentono di distribuire le impostazioni di connessione Desktop remoto agli utenti nella gerarchia di Configuration Manager. In questo modo gli utenti possono usare il portale aziendale per accedere ai computer aziendali primari tramite Desktop remoto usando le impostazioni di connessione Desktop remoto fornite dal portale aziendale.  

Windows Intune è necessario se si vuole che gli utenti si connettano ai propri PC aziendali con il portale aziendale. Se non si usa Intune, gli utenti possono comunque usare le informazioni del profilo di connessione remota per connettersi ai propri PC aziendali usando Desktop remoto su una connessione VPN.  

> [!IMPORTANT]  
>  Quando vengono specificate le impostazioni del profilo di connessione remota usando la console di Configuration Manager, le impostazioni vengono archiviate nei criteri locali del computer client. Queste impostazioni potrebbero sostituire le impostazioni di Desktop remoto configurate da un'altra applicazione. Inoltre, se si usano i Criteri di gruppo di Windows per configurare le impostazioni di Desktop remoto, le impostazioni specificate nei Criteri di gruppo sostituiranno quelle configurate usando Configuration Manager.  

 Quando si installa Configuration Manager, viene creato un nuovo gruppo di protezione denominato **Connessione desktop remoto**. Questo gruppo viene popolato quando si distribuisce un profilo di connessione remota che include gli utenti primari del computer a cui si distribuisce il profilo. Benché un amministratore locale possa aggiungere i nomi utente al gruppo, gli utenti verranno rimossi dal gruppo alla successiva valutazione della conformità dei profili di connessione remota distribuiti.  

 Se si aggiunge manualmente un utente al gruppo, l'utente può avviare le connessioni remote, ma le informazioni di connessione non verranno pubblicate nel portale aziendale.  

 Se si rimuove manualmente dal gruppo un utente che è stato aggiunto da Configuration Manager, questa modifica verrà automaticamente corretta in Configuration Manager aggiungendo di nuovo l'utente alla successiva valutazione della conformità del profilo di connessione remota.  

> [!IMPORTANT]  
>  Se la relazione di affinità utente dispositivo tra un utente e un dispositivo viene modificata (ad esempio, il computer a cui si connette un utente non è più il dispositivo primario dell'utente), Configuration Manager disabilita il profilo di connessione remota e le impostazioni di Windows Firewall per impedire le connessioni al computer.  

## <a name="prerequisites"></a>Prerequisiti  

### <a name="external-dependencies"></a>Dipendenze esterne  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Server Gateway Desktop remoto.|Se si desidera consentire agli utenti di connettersi a Internet al di fuori del dominio aziendale, è necessario installare e configurare un server Gateway Desktop remoto.<br /><br /> I profili di connessione remota potrebbero non funzionare correttamente se le impostazioni Desktop remoto o le impostazioni Servizi terminal sono gestite da un'altra applicazione o dalle impostazioni dei Criteri di gruppo. Quando vengono distribuiti i profili di connessione remota dalla console di Configuration Manager, le impostazioni vengono archiviate nei criteri locali del computer client. Tali impostazioni potrebbero sostituire le impostazioni Desktop remoto configurate da un'altra applicazione. Se inoltre si usano le impostazioni Criteri di gruppo per configurare le impostazioni Desktop remoto, le impostazioni specificate nelle impostazioni Criteri di gruppo sostituiranno quelle configurate da Configuration Manager.<br /><br /> Per altre informazioni su come installare e configurare un server gateway desktop remoto, vedere la documentazione di Windows Server.|  
|Se i computer client eseguono un firewall basato su host, è necessario attivare il programma Mstsc.exe.|Quando si configura un profilo di connessione remota, è necessario abilitare l'impostazione **Consenti eccezione Windows Firewall per connessioni in domini Windows e in reti private** . Una volta abilitata tale impostazione, Configuration Manager configura automaticamente Windows Firewall per attivare il programma Mstsc.exe. Tuttavia, se i computer client eseguono un firewall basato su host diverso, è necessario configurare manualmente questa dipendenza del firewall.<br /><br /> Le impostazioni di Criteri di gruppo per configurare Windows Firewall possono sostituire la configurazione impostata in Configuration Manager. Se si usano i Criteri di gruppo per configurare Windows Firewall, assicurarsi che le impostazioni dei Criteri di gruppo non blocchino il programma Mstsc.exe.|  

### <a name="configuration-manager-dependencies"></a>Dipendenze di Configuration Manager  

|Dipendenza|Altre informazioni|  
|----------------|----------------------|  
|Configuration Manager deve essere connesso a Microsoft Intune (situazione nota come configurazione ibrida).|Per altre informazioni sulla connessione di Configuration Manager a Microsoft Intune, vedere Gestire i dispositivi mobili con Configuration Manager e Microsoft Intune.|  
|Per far sì che l'utente possa connettersi a un computer della rete aziendale, tale computer deve essere un dispositivo principale dell'utente.|Per altre informazioni sull'affinità utente dispositivo, vedere l'argomento sul [collegamento di utenti e dispositivi con l'affinità utente dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|È necessario aver ottenuto specifiche autorizzazioni di sicurezza per gestire i profili di connessione remota.|Il ruolo di sicurezza **Gestione impostazioni di conformità** include le autorizzazioni necessarie per gestire i profili di connessione remota. Per ulteriori informazioni, vedere <br />[Configurare l'amministrazione basata su ruoli](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Considerazione su sicurezza e privacy per i profili di connessione remota  

### <a name="security-considerations"></a>Considerazioni sulla sicurezza  

|Procedura di sicurezza consigliata|Altre informazioni|  
|----------------------------|----------------------|  
|Specificare manualmente l'affinità utente dispositivo invece di consentire agli utenti di identificare il dispositivo principale. Inoltre, non abilitare la configurazione basata sulle statistiche di utilizzo.|Dal momento che è necessario abilitare **Consenti a tutti gli utenti primari del computer aziendale di connettersi in remoto** prima di poter distribuire un profilo di connessione remota, occorre sempre specificare manualmente l'affinità utente dispositivo. Non considerare autorevoli le informazioni raccolte dagli utenti o dal dispositivo. Se si distribuiscono profili di connessione remota e l'affinità utente dispositivo non è specificata da un utente amministratore attendibile, utenti non autorizzati potrebbero ricevere privilegi elevati ed essere in grado di connettersi in remoto ai computer.<br /><br /> Se si abilita la configurazione basata sulle statistiche di utilizzo, queste informazioni vengono raccolte usando messaggi di stato per cui Configuration Manager non fornisce protezione. Per attenuare questa minaccia, usare la firma Server Message Block (SMB) o Internet Protocol security (IPsec) tra computer client e punto di gestione.|  
|Limitare i diritti amministrativi locali sul computer del server del sito.|Un utente con diritti amministrativi locali sul server del sito può aggiungere manualmente membri al gruppo di protezione relativo alla connessione del PC remoto che Configuration Manager crea e mantiene automaticamente. Ciò potrebbe causare un'elevazione di privilegi perché i membri che vengono aggiunti a questo gruppo ricevono le autorizzazioni di Desktop remoto.|  

### <a name="privacy-considerations"></a>Considerazioni sulla privacy  

-   Se un utente avvia una connessione a un computer aziendale dal portale dell'azienda, viene scaricato un file con estensione .rdp o .wsrdp contenente il nome del dispositivo e il nome del server Gateway Desktop remoto richiesto per avviare la sessione Desktop remoto. L'estensione del file dipende dal sistema operativo del dispositivo. Ad esempio, i sistemi operativi Windows 7 e Windows 8 usano un file RDP, mentre Windows 8.1 usa un file WSRDP.  

-   L'utente può scegliere di aprire o salvare il file .rdp. Se l'utente sceglie di aprire il file .rdp, tale file potrebbe essere archiviato nella cache del browser Web in base alle impostazioni di conservazione configurate per il browser. Se l'utente sceglie di salvare il file, il file non viene archiviato nella cache del browser. Il file viene salvato fino a quando l'utente non lo elimina manualmente.  

-   Il file .wsrdp viene scaricato e salvato automaticamente in locale. Tale file viene sovrascritto alla successiva esecuzione di una sessione di Desktop remoto.  

-   Prima di configurare i profili di connessione remota, considerare i requisiti sulla privacy.  


## <a name="create-a-remote-connection-profile"></a>Creare un profilo di connessione remota

1. Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Profili connessione remota**.  

2. Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo di connessione remota**.  

3. Nella pagina **Generale** della **Creazione guidata profilo connessione remota**specificare un massimo di 256 caratteri per il nome e la descrizione facoltativa del profilo.  

4. Nella pagina delle impostazioni **Profilo** specificare le impostazioni seguenti per il profilo di connessione remota:  

   -   **Nome completo e porta del server Gateway Desktop remoto (facoltativo)** : specificare il nome del server Gateway Desktop remoto da usare per le connessioni.  

       > [!NOTE]  
       >  Configuration Manager non supporta l'uso di un nome IDN (Internationalized Domain Name) per specificare un server in questa casella.  
       >   
       >  Il nome del server non deve essere superiore a 256 caratteri e può contenere caratteri maiuscoli, minuscoli, numerici e i caratteri **–** e **_** separati da punti.  

   -   **Consenti connessioni solo da computer che eseguono Desktop remoto con Autenticazione a livello di rete**  

5. Selezionare **Abilitato** o **Non abilitato** per ciascuna delle seguenti impostazioni di connessione:  

   -   **Consenti connessioni remote a computer aziendali**  

   -   **Consenti a tutti gli utenti primari del computer aziendale di connettersi in remoto**  

   -   **Consenti eccezione di Windows Firewall per le connessioni nei domini Windows e nelle reti private**  

   > [!IMPORTANT]  
   >  Tutte e tre le impostazioni devono essere identiche prima di procedere al passaggio successivo della procedura guidata.  

6. Nella pagina **Riepilogo** esaminare le azioni da eseguire e completare la procedura guidata.  

   Il nuovo profilo di connessione remota viene visualizzato nel nodo **Profili connessione remota** dell'area di lavoro **Asset e conformità** .  

Distribuire un profilo di connessione remota  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Profili connessione remota**.  

3.  Nell'elenco **Profili connessione remota** selezionare il profilo di connessione remota che si desidera distribuire e quindi nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

4.  Nella finestra di dialogo **Distribuisci profilo connessione remota** specificare le seguenti informazioni:  

    -   **Raccolta** : fare clic su **Sfoglia** per selezionare la raccolta di dispositivi in cui si desidera distribuire il profilo di connessione remota.  

    -   **Monitora e aggiorna le regole non conformi, se supportato**: abilitare questa opzione per monitorare e aggiornare automaticamente il profilo di connessione remota quando risulta non conforme su un dispositivo, ad esempio, se non è presente.  

    -   **Consenti monitoraggio e aggiornamento fuori dalla finestra di manutenzione**: se è stata configurata una finestra di manutenzione per la raccolta in cui si distribuisce il profilo di connessione remota, abilitare questa opzione per consentire a Configuration Manager di monitorare e aggiornare il profilo di connessione remota fuori dalla finestra di manutenzione. Per altre informazioni sulle finestre di manutenzione, vedere l'argomento relativo all'[uso delle finestre di manutenzione](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Genera un avviso** : abilitare questa opzione per configurare un avviso che viene generato se la conformità del profilo di connessione remota è inferiore a una percentuale specificata in base a una data e un orario specifici. È inoltre possibile specificare se si desidera che un avviso venga inviato a System Center Operations Manager.  

    -   **Specifica la pianificazione per la valutazione della conformità per questa linea di base di configurazione** : specificare la pianificazione in base alla quale il profilo di connessione remota distribuito viene valutato nei dispositivi. È possibile specificare una pianificazione semplice o personalizzata.  

    > [!TIP]  
    >  Se un dispositivo lascia la raccolta a cui è stato distribuito un profilo di connessione remota, le impostazioni di tale profilo vengono disattivate sul dispositivo. Tuttavia, affinché questo processo venga eseguito correttamente, è necessario aver già distribuito almeno un elemento di configurazione o una linea di base della configurazione contenente un elemento di configurazione dal sito.  
    >   
    >  Il profilo viene valutato dai dispositivi quando l'utente esegue l'accesso.  
    >   
    >  Se due profili di connessione remota vengono distribuiti nella stessa raccolta di dispositivi, dove in un profilo è selezionato **Monitora e aggiorna le regole non conformi, se supportato** e nell'altro profilo la stessa opzione non è selezionata e i due profili di connessione remota hanno diverse impostazioni di connessione, il profilo in cui l'opzione non è selezionata potrebbe quindi sostituire le impostazioni nell'altro profilo. Questo tipo di distribuzione del profilo di connessione remota non è supportato da Configuration Manager.  

5.  Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci profilo connessione remota** e creare la distribuzione.  

## <a name="monitor-a-remote-connection-profile"></a>Monitorare un profilo di connessione remota  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Visualizzare i risultati di conformità nella console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio** > **Distribuzioni**.  

3.  Nell'elenco **Distribuzioni** selezionare la distribuzione del profilo di connessione remota per cui si desidera esaminare le informazioni sulla conformità.  

4.  È possibile esaminare le informazioni di riepilogo sulla conformità della distribuzione del profilo di connessione remota nella pagina principale. Per visualizzare informazioni più dettagliate, selezionare la distribuzione del profilo di connessione remota, quindi nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Visualizza stato** per aprire il riquadro **Stato distribuzione** .  

     La pagina **Stato distribuzione** contiene le seguenti schede:  

    -   **Conforme** : visualizza la conformità del profilo di connessione remota in base al numero degli asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti i dispositivi che sono conformi al profilo di connessione remota. Il riquadro **Dettagli asset** visualizza anche i dispositivi che sono conformi a questo profilo. Fare doppio clic su un dispositivo nell'elenco per visualizzare informazioni aggiuntive.  

        > [!IMPORTANT]  
        >  Un profilo di connessione remota non viene valutato se non è applicabile a un dispositivo client. Tuttavia, viene restituito come conforme.  

    -   **Errore** : visualizza un elenco di tutti gli errori per la distribuzione del profilo di connessione remota selezionata in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti i dispositivi che hanno generato errori con questo profilo. Quando si seleziona un dispositivo, il riquadro **Dettagli asset** visualizza i dispositivi interessati dal problema selezionato. Fare doppio clic su un dispositivo nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Non conforme** : visualizza un elenco di tutte le regole non conformi nel profilo di connessione remota in base al numero di asset interessati. È possibile fare doppio clic su una regola per creare un nodo temporaneo nel nodo **Utenti** nell'area di lavoro **Asset e conformità** . Questo nodo contiene tutti i dispositivi che non sono conformi a questo profilo. Quando si seleziona un dispositivo, il riquadro **Dettagli asset** visualizza i dispositivi interessati dal problema selezionato. Fare doppio clic su un dispositivo nell'elenco per visualizzare informazioni aggiuntive sul problema.  

    -   **Sconosciuto** : visualizza un elenco di tutti i dispositivi che non sono conformi alla distribuzione del profilo di connessione remota selezionata insieme allo stato client corrente dei dispositivi.  

5.  Nella pagina **Stato distribuzione** è possibile esaminare le informazioni dettagliate sulla conformità del profilo di connessione remota distribuito. Viene creato un nodo temporaneo nel nodo **Distribuzioni** che consente di ritrovare rapidamente queste informazioni.  

### <a name="view-compliance-results-with-reports"></a>Visualizzare i risultati di conformità con i report  
 Configuration Manager include report predefiniti che è possibile usare per monitorare le informazioni sui profili di connessione remota. Tali report dispongono della categoria report di **Gestione conformità e impostazioni**.  

> [!IMPORTANT]  
>  È necessario utilizzare un carattere jolly (%) quando si utilizzano i parametri **Filtro dispositivo** e **Filtro utente** nei report per le impostazioni di conformità.  

 Per altre informazioni sulle modalità di configurazione dei report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](/sccm/core/servers/manage/reporting).  
