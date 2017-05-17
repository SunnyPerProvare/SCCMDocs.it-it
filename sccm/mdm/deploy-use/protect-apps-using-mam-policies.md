---
title: Proteggere le app usando i criteri di gestione delle applicazioni mobili | Microsoft Docs
description: "Modificare la funzionalità delle app distribuite in modo che soddisfino i criteri aziendali di conformità e di sicurezza."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 74f4dd44089d4a13526c981589e1f497f0e10290
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteggere le app usando i criteri di gestione delle applicazioni mobili in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I criteri di gestione delle applicazioni di System Center Configuration Manager consentono di modificare le funzionalità delle app distribuite per adeguarle ai criteri aziendali di conformità e sicurezza. Ad esempio, è possibile limitare le operazioni taglia, copia e incolla in un'app con restrizioni oppure configurare un'app per aprire tutti i collegamenti Web in Managed Browser. I criteri di gestione delle app supportano:  

-   Dispositivi che eseguono Android 4 e versioni successive  

-   Dispositivi che eseguono iOS 7 e versioni successive  

È anche possibile usare i criteri di gestione delle app mobili per proteggere le app su dispositivi non gestiti da Intune. Con questa nuova funzionalità è possibile applicare i criteri di gestione delle app mobili ad app che si connettono ai servizi di Office 365. Questa funzionalità non è supportata per le app che si connettono a Exchange o SharePoint locale.  

Per usare questa nuova funzionalità, è necessario usare il portale di anteprima di Azure. Per acquisire familiarità con tale funzionalità, usare gli argomenti seguenti:  
-   [Introduzione ai criteri di gestione delle app mobili nel portale di Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Creare e distribuire i criteri di gestione delle app mobili con Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

 Un criterio di gestione delle applicazioni non viene distribuito direttamente come invece avviene per le linee base e gli elementi di configurazione in Configuration Manager. Al contrario, è possibile associare i criteri al tipo di distribuzione delle applicazioni che si vuole limitare. Le impostazioni specificate diventeranno effettive quando il tipo di distribuzione delle app verrà distribuito e installato nei dispositivi.  

Per applicare le restrizioni a un'app, è necessario che nell'app sia incorporato il Software Development Kit (SDK) dell'app di Microsoft Intune. Esistono due metodi per ottenere questo tipo di app:  

-   **Usare un'app gestita da criteri** (Android e iOS): queste app includono App SDK incorporato. Per aggiungere questo tipo di applicazione, è possibile specificare un collegamento all'app da un archivio di app, ad esempio l'iTunes store o Google Play. Non sono richieste ulteriori elaborazioni per questo tipo di app. Per un elenco delle app gestite da criteri disponibili per dispositivi iOS e Android, vedere [App gestite per criteri di gestione delle applicazioni per dispositivi mobili di Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Usare un'app con wrapper** (Android e iOS): app che sono state riassemblate per includere App SDK usando lo ** strumento per la disposizione testo per app di Microsoft Intune**. Questo strumento viene in genere usato per elaborare le app aziendali create internamente. Non può essere usato per elaborare le app state scaricate dall'App Store. Per altre informazioni, vedere i seguenti articoli:
    - [Preparare le app per iOS per la gestione di applicazioni per dispositivi mobili con lo strumento per la disposizione testo per app di Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx)

    - [Preparare le app per Android per la gestione di applicazioni per dispositivi mobili con lo strumento per la disposizione testo per app di Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Creare e distribuire un'app con criterio di gestione delle applicazioni mobili  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Passaggio 1: Ottenere il collegamento a un'app gestita da criteri o creare un'app con wrapper  

-   **Per ottenere un collegamento a un'app gestita da criteri**: nell'App Store trovare e prendere nota dell'URL dell'app gestita da criteri che si vuole distribuire.  

     Ad esempio, l'URL dell'app Microsoft Word per iPad è **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Per creare un'app con wrapper**: usare le informazioni negli argomenti [Preparare le app per iOS per la gestione di applicazioni per dispositivi mobili con lo strumento per la disposizione testo per app di Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) e [Preparare le app per Android per la gestione di applicazioni per dispositivi mobili con lo strumento per la disposizione testo per app di Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx) per creare un'app con wrapper.  

     Lo strumento crea un'app elaborata e un file manifesto associato. Questi file vengono usati quando si crea un'applicazione di Configuration Manager che contiene l'app.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Passaggio 2: Creare un'applicazione di Configuration Manager che contenga un'app  
 La procedura per creare l'applicazione di Configuration Manager è diversa quando si usa un'app gestita da criteri (collegamento esterno) o un'app creata tramite Microsoft Intune App Wrapping Tool di Microsoft Intune per iOS (pacchetto dell'app per iOS). Per creare l'applicazione di Configuration Manager, usare una delle procedure seguenti.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione** per aprire la **Creazione guidata applicazione**.  

4.  Nella pagina **Generale** selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

5.  Nell'elenco a discesa **Tipo** selezionare **Pacchetto app iOS (file \*.ipa)**.  

6.  Fare clic su **Sfoglia** per selezionare il pacchetto dell'app che si vuole importare e quindi fare clic su **Avanti**.  

7.  Nella pagina **Informazioni generali** immettere il testo descrittivo e le informazioni di categoria che si desidera visualizzare agli utenti nel portale della società.  

8.  Completare la procedura guidata.  

 La nuova applicazione viene visualizzata nel nodo **Applicazioni** dell'area di lavoro **Raccolta software** .  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Creare un'applicazione contenente un collegamento a un'app gestita da criteri  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea applicazione** per aprire la **Creazione guidata applicazione**.  

4.  Nella pagina **Generale** selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

5.  Nell'elenco a discesa **Tipo** selezionare una delle opzioni seguenti:  

    -   Per iOS: **Pacchetto app per iOS nell'App Store**  

    -   Per Android: **Pacchetto app per Android in Google Play**  

6.  Immettere l' URL per l'app (dal passaggio 1) e quindi fare clic su **Avanti**.  

7.  Nella pagina **Informazioni generali** immettere il testo descrittivo e le informazioni di categoria che si desidera visualizzare agli utenti nel portale della società.  

8.  Completare la procedura guidata.  

 La nuova applicazione viene visualizzata nel nodo **Applicazioni** dell'area di lavoro **Raccolta software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Passaggio 3: Creare criteri di gestione delle applicazioni  
 Creare quindi un criterio di gestione delle applicazioni che verrà associato all'applicazione. È possibile creare criteri di Managed Browser o generali.  

1)  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Criteri di gestione delle applicazioni**.  

2)  Nella scheda **Home** nel gruppo **Crea** scegliere **Crea criteri di gestione delle applicazioni**.  

3)  Nella pagina **Generale** immettere il nome e la descrizione per il criterio e quindi fare clic su **Avanti**.  

4)  Nella pagina **Tipo di criterio** selezionare la piattaforma e il tipo di criterio e quindi fare clic su **Avanti**. Sono disponibili i tipi di criterio seguenti:  

-   **Generale**: il tipo di criterio Generale consente di modificare la funzionalità delle app distribuite per adeguarle ai criteri aziendali di conformità e sicurezza. Ad esempio, è possibile limitare le operazioni taglia, copia e incolla in un'app con restrizioni.  

-   **Managed Browser**: consente di scegliere se consentire o meno a Managed Browser di aprire un elenco di URL. Il tipo di criteri Managed Browser consente di modificare la funzionalità dell'app Intune Managed Browser. Si tratta di un Web browser che consente di gestire le azioni eseguibili dagli utenti, inclusi i siti che possono visitare, e come aprire i collegamenti al contenuto all'interno del browser. Altre informazioni sull'  [app Intune Managed Browser per iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e l' [app Intune Managed Browser per Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  Nella pagina **Criteri iOS** o **Criteri Android** configurare i valori seguenti come richiesto e quindi fare clic su **Avanti**. Le opzioni possono variare a seconda del tipo di dispositivo per il quale si sta configurando il criterio.  

|Valore|Altre informazioni|  
|-----------|----------------------|  
|**Limitare il contenuto Web per la visualizzazione in Managed Browser dell'azienda**|Abilita tutti i collegamenti nell'app da aprire in Managed Browser. Per usare questa opzione, è necessario avere distribuito l'app nei dispositivi.|  
|**Impedisci backup in Android** o **Impedisci backup in iTunes e iCloud**|Disabilita il backup delle informazioni presenti nell'app.|  
|**Consenti all'app di trasferire i dati ad altre app**|Specifica le app a cui questa app può inviare dati. È possibile scegliere di non consentire il trasferimento dei dati a qualsiasi app, consentire il trasferimento solo ad altre app con restrizioni o consentire il trasferimento a qualsiasi app.<br /><br /> Nei dispositivi iOS, per impedire il trasferimento di documenti tra app gestite e non gestite, è necessario anche configurare e distribuire un criterio di sicurezza dei dispositivi mobili che disabilita l'impostazione **Consenti documenti gestiti in altre app non gestite**.<br /><br /> Se si sceglie di consentire il trasferimento solo ad altre app con restrizioni, vengono usati i visualizzatori Intune di immagini e PDF (se distribuiti) per aprire il contenuto dei rispettivi tipi.|  
|**Consenti all'app di ricevere i dati da altre app**|Specifica le app da cui questa app può ricevere dati. È possibile scegliere di non consentire il trasferimento dei dati da qualsiasi app, consentire il trasferimento solo da altre app con restrizioni o consentire il trasferimento da qualsiasi app.|  
|**Impedisci "Salva con nome"**|Disabilita l'uso dell'opzione **Salva con nome** in qualsiasi app che usa questo criterio.|  
|**Limita le operazioni taglia, copia e incolla con le altre app**|Specifica come è possibile usare le operazioni taglia, copia e incolla con l'app. È possibile scegliere tra:<br /><br /> **Bloccato**: non consente le operazioni taglia, copia e incolla tra questa app e altre app.<br /><br /> **App gestite da criteri**: consente le operazioni taglia, copia e incolla solo tra questa app e altre app con restrizioni.<br /><br /> **App gestite da criteri con Incolla in**: consente di incollare i dati tagliati o copiati da questa app solo in altre app con restrizioni. I dati tagliati o copiati da qualsiasi app possono essere incollati in questa app.<br /><br /> **Qualsiasi app**: nessuna restrizione per le operazioni taglia, copia e incolla in o da questa app.|  
|**Richiedi PIN semplice per l'accesso**|Richiede all'utente di immettere un PIN specificato per l'uso dell'app. All'utente viene richiesto di impostare questo numero alla prima esecuzione dell'app.|  
|**Numero di tentativi prima della reimpostazione del PIN**|Specifica il numero di tentativi di immissione del PIN che è possibile effettuare prima che all'utente venga richiesto di reimpostare il PIN.|  
|**Richiedi credenziali aziendali per l'accesso**|Richiede all'utente di immettere le informazioni di accesso aziendali per poter accedere all'app.|  
|**Richiedi la conformità del dispositivo ai criteri aziendali per l'accesso**|Consente l'uso dell'app solo se il dispositivo non è jailbroken o rooted.|  
|**Controlla di nuovo i requisiti di accesso dopo (minuti)**|Specifica il periodo di tempo che deve trascorrere prima che vengano controllati di nuovo i requisiti di accesso per l'app dopo l'avvio (nel campo **Timeout**).<br /><br /> Nel campo **Periodo di prova offline**, se il dispositivo è offline, specifica il periodo di tempo che deve trascorrere prima che vengano controllati di nuovo i requisiti di accesso per l'app.|  
|**Crittografa dati app**|Specifica che tutti i dati associati a questa app siano crittografati, compresi i dati archiviati esternamente come, ad esempio, i dati archiviati sulle schede SD.<br /><br /> **Crittografia per iOS**<br /><br /> Per le app associate ai criteri di gestione delle applicazioni mobili di Configuration Manager, i dati vengono crittografati a riposo usando la crittografia a livello di dispositivo implementata dal sistema operativo. Ciò viene abilitato tramite i criteri PIN del dispositivo che devono essere impostati dall'amministratore IT. Quando viene richiesto un PIN, i dati vengono crittografati in base alle impostazioni nei criteri di gestione delle applicazioni mobili. Come indicato nella documentazione di Apple, [i moduli usati da iOS 7 sono FIPS 140-2 certified](http://support.apple.com/en-us/HT202739).<br /><br /> **Crittografia per Android**<br /><br /> Per le app associate ai criteri di gestione delle applicazioni mobili di Configuration Manager, la crittografia viene implementata da Microsoft. I dati vengono crittografati in modo sincrono durante le operazioni di I/O dei file in base all'impostazione nei criteri di gestione delle applicazioni mobili. Le app gestite su Android usano la crittografia AES-128 in modalità CBC con le librerie di crittografia della piattaforma. Il metodo di crittografia non è conforme agli standard FIPS 140-2. Il contenuto nell'archivio del dispositivo è sempre crittografato.|  
    |**Blocca acquisizione schermo** (solo per dispositivi Android)|Specifica che le funzionalità di acquisizione schermo del dispositivo vengono bloccate quando si usa questa app.|  

6)  Nella pagina **Managed Browser** selezionare se Managed Browser è autorizzato ad aprire solo gli URL nell'elenco o meno e quindi fare clic su **Avanti**.  
Per altre informazioni, vedere [Gestire un accesso Internet tramite i criteri di Managed Browser](manage-internet-access-using-managed-browser-policies.md).  

7)  Completare la procedura guidata.  

 Il nuovo criterio viene visualizzato nel nodo **Criteri di gestione delle applicazioni** dell'area di lavoro **Raccolta software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Passaggio 4: Associare i criteri di gestione delle applicazioni a un tipo di distribuzione  

 Quando viene creato un tipo di distribuzione per un'app che richiede un criterio di gestione dell'applicazione, Configuration Manager lo riconosce e chiede di associare un criterio di gestione dell'app. Per Managed Browser, è necessario associare i criteri Managed Browser e Generale. Per altre informazioni, vedere [Create applications](create-applications.md) (Creare le applicazioni).  

> [!IMPORTANT]  
>  Se l'applicazione è già stata distribuita, la distribuzione per il nuovo tipo di distribuzione ha esito negativo fino a quando non viene eseguita questa associazione. È possibile eseguire l'associazione in **Proprietà** per l'applicazione nella scheda **Gestione applicazioni** .  

> [!IMPORTANT]  
>  Per i dispositivi che eseguono sistemi operativi precedenti a iOS 7.1, i criteri associati non vengono rimossi quando si disinstalla l'app.  
>   
>  Se viene annullata la registrazione del dispositivo da Configuration Manager, i criteri non vengono rimossi dalle app. Nelle app con i criteri applicati vengono mantenute le impostazioni dei criteri anche dopo che l'applicazione viene disinstallata e reinstallata.  

##  <a name="step-5-monitor-the-app-deployment"></a>Passaggio 5: Monitorare la distribuzione dell'app  
 Dopo aver creato e distribuito un'app associata al criterio di gestione delle applicazioni mobili, è possibile monitorare l'app e risolvere eventuali conflitti di criteri.  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Panoramica** > **Distribuzioni**.  

3.  Selezionare la distribuzione che è stata creata. Nella scheda **Home** scegliere **Proprietà**.  

4.  Nel riquadro dei dettagli per la distribuzione scegliere **Criteri di gestione delle applicazioni** in **Oggetti correlati**.  

 Per altre informazioni sul monitoraggio delle applicazioni, vedere [Monitorare le applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Informazioni su come vengono risolti i conflitti tra criteri  
 Quando si verifica un conflitto tra i criteri di gestione delle applicazioni mobili nella prima distribuzione all'utente o al dispositivo, il valore di impostazione specifico in conflitto viene rimosso dai criteri distribuiti all'app. L'app usa quindi un valore in conflitto incorporato.  

 Quando si verifica un conflitto tra i criteri di gestione delle applicazioni mobili nelle successive distribuzioni all'utente o all'app, il valore di impostazione specifico in conflitto non viene aggiornato nei criteri distribuiti all'app e l'app usa il valore esistente per tale impostazione.  

 Nei casi in cui il dispositivo o l'utente riceva due criteri in conflitto, si applica il comportamento seguente:  

-   Se un criterio è già stato distribuito al dispositivo, le impostazioni dei criteri esistenti non vengono sovrascritte.  

-   Se al dispositivo non è stato ancora distribuito alcun criterio e vengono distribuite due impostazioni in conflitto, viene usata l'impostazione predefinita del dispositivo.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Vedere un elenco delle app gestite da criteri disponibili  
 Per un elenco delle app gestite da criteri disponibili per dispositivi iOS e Android, vedere [Partner di applicazioni per Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  

