---
title: Configurare Asset Intelligence | System Center Configuration Manager
description: Configurare Asset Intelligence in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 43e04a447b03885286c6c7201afb4d1b7a10aa91


---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurare Asset Intelligence in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È necessario completare una serie di passaggi di configurazione prima di poter usare Asset Intelligence in System Center Configuration Manager per eseguire l'inventario e gestire l'uso delle licenze software a livello aziendale.  

## <a name="steps-to-configure-asset-intelligence"></a>Passaggi per la configurazione di Asset Intelligence  
 Per raccogliere i dati di inventario necessari per i report di Asset Intelligence, è necessario abilitare Hardware Inventory Client Agent. Per informazioni sull'abilitazione di Hardware Inventory Client Agent, vedere [Come estendere l'inventario hardware in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

|Passaggio|Dettagli|Altre informazioni|  
|----------|-------------|----------------------|  
|**Passaggio 1**: Abilitare le classi di report per l'inventario hardware di Asset Intelligence|La raccolta di informazioni per Asset Intelligence non è abilitata alla prima installazione di Configuration Manager. Per abilitare Asset Intelligence, è necessario abilitare almeno una delle classi di report per l'inventario hardware richieste su cui si basano i report di Asset Intelligence.|Per altre informazioni, vedere la procedura seguente in questo argomento: [Enable Asset Intelligence hardware inventory reporting classes](#BKMK_EnableAssetIntelligence).|  
|**Passaggio 2**: Installare un punto di sincronizzazione di Asset Intelligence|Il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence viene usato per connettere i siti di Configuration Manager a System Center Online per la sincronizzazione delle informazioni del catalogo di Asset Intelligence. Il punto di sincronizzazione di Asset Intelligence può essere installato solo in un sistema del sito nel sito principale della gerarchia di Configuration Manager e richiede l'accesso a Internet per la sincronizzazione con System Center Online tramite la porta TCP 443.<br /><br /> Oltre al download di nuove informazioni per il catalogo di Asset Intelligence, il punto di sincronizzazione di Asset Intelligence consente di caricare le informazioni sui titoli software personalizzati in System Center Online per la categorizzazione. Microsoft considera informazioni pubbliche tutti i titoli software caricati in System Center Online per la categorizzazione. È quindi necessario accertarsi che i titoli software personalizzati non contengano informazioni riservate o proprietarie. Per altre informazioni su come richiedere la categorizzazione dei titoli software, vedere [Richiedere un aggiornamento del catalogo per i titoli software senza categoria](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).|Per altre informazioni, vedere la procedura seguente in questo argomento: [Install an Asset Intelligence Synchronization Point](#BKMK_InstallAssetIntelligenceSynchronizationPoint).|  
|**Passaggio 3**: Abilitare il controllo degli eventi di accesso con esito positivo|Quattro report di Asset Intelligence visualizzano informazioni raccolte dai registri eventi di sicurezza di Windows nei computer client. Se le impostazioni del registro eventi di sicurezza non sono configurate in modo da registrare tutti gli eventi di accesso con esito positivo, questi report non contengono dati anche se è abilitata la classe di report appropriata per l'inventario hardware. Per abilitare Hardware Inventory Client Agent per l'esecuzione dell'inventario delle informazioni necessarie per supportare questi report, è prima necessario modificare le impostazioni del registro eventi di sicurezza di Windows nei client in modo da registrare tutti gli eventi di accesso con esito positivo e abilitare la classe di report per l'inventario hardware **SMS_SystemConsoleUser** .|Per altre informazioni, vedere le procedure seguenti in questo argomento: [Enable auditing of success logon events](#BKMK_EnableSuccessLogonEvents).|  
|**Passaggio 4**: Importare le informazioni sulle licenze software|L'Importazione guidata licenze software viene usata per importare informazioni Microsoft Volume Licensing (MVLS) e resoconti delle licenze generali nel catalogo di Asset Intelligence.<br /><br /> Il resoconto delle licenze MVLS contiene informazioni sui diritti di licenza o sul numero di licenze acquistate per i prodotti Microsoft.<br /><br /> Un resoconto delle licenze generale contiene informazioni sulle licenze acquistate per qualsiasi editore.|Per altre informazioni, vedere le procedure seguenti in questo argomento: [Import software license information](#BKMK_ImportSoftwareLicenseInformation).|  
|**Passaggio 5**: Configurare le attività di manutenzione di Asset Intelligence|Ad Asset Intelligence sono associate le attività di manutenzione seguenti. Per impostazione predefinita, entrambe le attività di manutenzione sono abilitate e configurate con una pianificazione predefinita.<br /><br /> **Verifica titolo applicazione con le informazioni di inventario**: questa attività di manutenzione controlla che il titolo software riportato nell'inventario software coincida con il titolo software nel catalogo di Asset Intelligence.<br /><br /> **Riepiloga dati software installato**: questa attività di manutenzione fornisce le informazioni visualizzate nell'area di lavoro **Asset e conformità** nel nodo **Asset Intelligence** all'interno del nodo **Software di inventario** . All'esecuzione dell'attività, Configuration Manager raccoglie un conteggio di tutti i titoli software di inventario nel sito primario.|Per altre informazioni, vedere le procedure seguenti in questo argomento: [Configure Asset Intelligence maintenance tasks](#BKMK_ConfigureMaintenanceTasks).|  

> [!NOTE]  
>  L'attività di manutenzione **Riepiloga dati software installato** è disponibile solo nei siti primari.  

## <a name="supplemental-procedures-for-configuring-asset-intelligence"></a>Procedure aggiuntive per la configurazione di Asset Intelligence  
 Usare le informazioni seguenti per i passaggi nella tabella precedente.  

###  <a name="a-namebkmkenableassetintelligencea-enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Abilitare le classi di report per l'inventario hardware di Asset Intelligence  
 Per abilitare Asset Intelligence nei siti di Configuration Manager, è necessario abilitare una o più classi di report per l'inventario hardware di Asset Intelligence. È possibile abilitare le classi nella home page di **Asset Intelligence** o nell'area di lavoro **Amministrazione** , nel nodo **Impostazioni client** , nelle proprietà delle impostazioni client. Usare una delle procedure seguenti per abilitare le classi di report per l'inventario hardware di Asset Intelligence.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Per abilitare le classi di report per l'inventario hardware di Asset Intelligence dalla home page di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**.  

3.  Nella scheda **Home** , nel gruppo **Asset Intelligence** , fare clic su **Modifica classi di inventario**. Verrà visualizzata la finestra di dialogo **Modifica classi di inventario** .  

4.  Per abilitare i report di Asset Intelligence, selezionare **Abilita tutte le classi di report di Asset Intelligence** oppure selezionare **Abilita solo le classi di report di Asset Intelligence selezionate**e selezionare almeno una classe di report tra quelle visualizzate.  

    > [!NOTE]  
    >  I report di Asset Intelligence che dipendono dalle classi di inventario hardware abilitate con questa procedura non visualizzano dati fino a quando i client non eseguono un'analisi dell'hardware e restituiscono l'inventario hardware.  

5.  Fare clic su **OK** per abilitare le classi di report selezionate per l'inventario hardware di Asset Intelligence.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Per abilitare le classi di report per l'inventario hardware di Asset Intelligence dalle proprietà delle impostazioni client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**e quindi selezionare **Impostazioni agente client predefinite**.  

    > [!NOTE]  
    >  Se sono state create impostazioni client personalizzate, è possibile selezionare le impostazioni client personalizzate invece di quelle predefinite.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**. Verrà visualizzata la finestra di dialogo **Impostazioni client Proprietà** .  

4.  Fare clic su **Inventario hardware**e quindi su **Imposta classi**. Verrà visualizzata la finestra di dialogo **Classi di inventario hardware** .  

5.  Fare clic su **Filtra per categoria**e quindi su **Classi di report di Asset Intelligence**. L'elenco delle classi viene aggiornato in modo da includere solo le classi di report per l'inventario hardware di Asset Intelligence.  

6.  Selezionare almeno una classe di report nell'elenco delle classi di report di Asset Intelligence.  

    > [!NOTE]  
    >  I report di Asset Intelligence che dipendono dalle classi di inventario hardware abilitate con questa procedura non visualizzano dati fino a quando i client non eseguono un'analisi dell'hardware e restituiscono l'inventario hardware.  

7.  Fare clic su **OK** per abilitare le classi di report selezionate per l'inventario hardware di Asset Intelligence.  

###  <a name="a-namebkmkinstallassetintelligencesynchronizationpointa-install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Installare un punto di sincronizzazione di Asset Intelligence  
 Usare la procedura seguente per installare un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence.  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Per installare un ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, quindi fare clic su **Server e ruoli del sistema del sito**.  

3.  Aggiungere il ruolo del sistema sito del punto di sincronizzazione di Asset Intelligence a un server del sistema del sito nuovo o esistente usando il passaggio associato:  

    -   **Nuovo server del sistema sito**: nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**. Viene visualizzata la Creazione guidata server del sistema sito.  

        > [!NOTE]  
        >  Per impostazione predefinita, quando Configuration Manager installa un ruolo del sistema del sito, i file di installazione vengono installati nella prima unità disco rigido NTFS con la maggiore quantità di spazio su disco disponibile. Per evitare l'installazione di Configuration Manager in unità specifiche, creare un file vuoto denominato No_sms_on_drive.sms e copiarlo nella cartella radice dell'unità prima dell'installazione del server del sistema del sito.  

    -   **Server del sistema del sito esistente**: selezionare il server in cui si vuole installare il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence. Quando si seleziona un server, nel riquadro dei dettagli viene visualizzato un elenco dei ruoli del sistema del sito già installati sul server.  

         Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**. Verrà visualizzata la finestra di Aggiunta guidata ruoli del sistema del sito.  

4.  Nella scheda **Generale** specificare le impostazioni generali per il server del sistema del sito. Quando si aggiunge il punto di sincronizzazione di Asset Intelligence a un server del sistema del sito esistente, verificare i valori configurati in precedenza.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di sincronizzazione di Asset Intelligence** nell'elenco dei ruoli disponibili e quindi fare clic su **Avanti**.  

6.  Nella pagina **Punto di sincronizzazione di Asset Intelligence Impostazioni di connessione** fare clic su **Avanti**.  

     Per impostazione predefinita, l'impostazione **Utilizza questo punto di sincronizzazione di Asset Intelligence** è selezionata e non può essere configurata in questa pagina. System Center Online accetta il traffico di rete solo sulla porta TCP 443, pertanto l'impostazione **Numero porta SSL** non può essere configurata in questa pagina della procedura guidata.  

7.  Facoltativamente, è possibile specificare un percorso per il file del certificato di autenticazione (con estensione pfx) di System Center Online e quindi fare clic su **Avanti**. In genere, non si specifica un percorso per il certificato perché il provisioning del certificato di connessione viene eseguito automaticamente durante l'installazione del ruolo del sito.  

8.  Nella pagina **Impostazioni server proxy** specificare se il punto di sincronizzazione di Asset Intelligence userà un server proxy per la connessione a System Center Online per sincronizzare il catalogo e se usare credenziali per connettersi al server proxy, quindi fare clic su **Avanti**.  

    > [!WARNING]  
    >  Se è necessario un server proxy per connettersi a System Center Online, il certificato di connessione potrebbe anche essere eliminato se scade la password dell'account utente configurato per l'autenticazione del server proxy.  

9. Nella pagina **Pianificazione della sincronizzazione** specificare se si vuole usare una pianificazione per sincronizzare il catalogo di Asset Intelligence. Quando si abilita la pianificazione della sincronizzazione, è necessario specificare una pianificazione della sincronizzazione semplice o personalizzata. Durante la sincronizzazione pianificata, il punto di sincronizzazione di Asset Intelligence si connette a System Center Online per recuperare il catalogo di Asset Intelligence più recente. È possibile sincronizzare manualmente il catalogo di Asset Intelligence dal nodo di Asset Intelligence nella console di Configuration Manager. Per i passaggi relativi alla sincronizzazione manuale del catalogo di Asset Intelligence, vedere la sezione [Per sincronizzare manualmente il catalogo di Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) in [Operazioni per Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Nella pagina **Riepilogo** della creazione guidata del ruolo del sito, verificare le impostazioni specificate per assicurarsi che siano corrette prima di continuare. Per apportare modifiche alle impostazioni, fare clic su **Indietro** fino a tornare alla pagina appropriata, apportare le modifiche e tornare alla pagina **Riepilogo** .  

###  <a name="a-namebkmkenablesuccesslogoneventsa-enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Abilitare il controllo degli eventi di accesso con esito positivo  
 Usare la procedura seguente per configurare le impostazioni di accesso dei criteri di sicurezza del computer per abilitare il controllo degli eventi di accesso con esito positivo.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Per abilitare la registrazione degli eventi di accesso con esito positivo tramite criteri di sicurezza locali  

1.  In un computer client di Configuration Manager fare clic su **Start**, scegliere **Strumenti di amministrazione** e quindi fare clic su **Criteri di sicurezza locali**.  

2.  Nella finestra di dialogo **Criteri di sicurezza locali** , in **Impostazioni sicurezza**, espandere **Criteri locali**e quindi fare clic su **Criteri controllo**.  

3.  Nel riquadro dei risultati fare doppio clic su **Controlla eventi di accesso**, verificare che la casella di controllo **Operazione riuscita** sia selezionata e quindi fare clic su **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Per abilitare la registrazione degli eventi di accesso con esito positivo tramite i criteri di sicurezza del dominio di Active Directory  

1.  In un computer controller di dominio fare clic su **Start**, scegliere **Strumenti di amministrazione**e quindi fare clic su **Criterio di protezione del dominio**.  

2.  Nella finestra di dialogo **Criteri di sicurezza locali** , in **Impostazioni sicurezza**, espandere **Criteri locali**e quindi fare clic su **Criteri controllo**.  

3.  Nel riquadro dei risultati fare doppio clic su **Controlla eventi di accesso**, verificare che la casella di controllo **Operazione riuscita** sia selezionata e quindi fare clic su **OK**.  

###  <a name="a-namebkmkimportsoftwarelicenseinformationa-import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Importare informazioni sulle licenze software  
 Le sezioni seguenti descrivono le procedure necessarie per importare le informazioni sulle licenze software in generale e quelle Microsoft nel database del sito di Configuration Manager usando Importazione guidata licenze software. Quando si importano informazioni sulle licenze software nel database del sito dai file di resoconto delle licenze, per l'account computer del server del sito sono necessarie le autorizzazioni **Controllo completo** per il file system NTFS per la condivisione file usata per importare le informazioni sulle licenze software.  

> [!IMPORTANT]  
>  Quando le informazioni sulle licenze software vengono importate nel database del sito, le informazioni esistenti vengono sovrascritte. Assicurarsi che il file di informazioni sulle licenze software usato con l'Importazione guidata licenze software contenga un elenco completo di tutte le informazioni sulle licenze software necessarie.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Per importare le informazioni sulle licenze software nel catalogo di Asset Intelligence  

1.  Nell'area di lavoro **Asset e conformità** fare clic su **Asset Intelligence**.  

2.  Nella scheda **Home** , nel gruppo **Asset Intelligence** , fare clic su **Importa licenze software**. Verrà visualizzata l'Importazione guidata licenze software.  

3.  Nella pagina **Benvenuti** fare clic su **Avanti**.  

4.  Nella pagina **Importa** specificare se si intende importare un file di Microsoft Volume Licensing (MVLS) (con estensione xml o csv) o un file di resoconto delle licenze generale (con estensione csv). Per altre informazioni sulla creazione di un file di resoconto delle licenze generale, vedere [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) più avanti in questo argomento.  

    > [!WARNING]  
    >  Per scaricare un file MVLS in formato CSV che è possibile importare nel catalogo di Asset Intelligence, vedere [Microsoft Volume Licensing Service Center](http://go.microsoft.com/fwlink/p/?LinkId=226547). Per accedere a queste informazioni, è necessario disporre di un account registrato nel sito Web. È necessario contattare il rappresentante Microsoft per informazioni su come ottenere il file MVLS in formato XML.  

5.  Immettere il percorso UNC del file di resoconto delle licenze oppure fare clic su **Sfoglia** per selezionare una cartella di rete condivisa e un file.  

    > [!NOTE]  
    >  La cartella condivisa deve essere protetta adeguatamente per evitare accessi non autorizzati al file di informazioni sulle licenze e l'account computer del computer in cui è in esecuzione la procedura guidata deve disporre delle autorizzazioni di controllo completo per la condivisione contenente il file di importazione delle licenze.  

6.  Nella pagina **Riepilogo** esaminare le informazioni specificate per verificare che siano corrette prima di continuare. Per apportare modifiche, fare clic su **Indietro** per tornare alla pagina **Importa** .  

###  <a name="a-namebkmkcreategenerallicensestatementa-create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Creare un file di resoconto delle licenze generale per l'importazione  
 È anche possibile importare un resoconto delle licenze generale nel catalogo di Asset Intelligence tramite un file di importazione delle licenze creato manualmente in formato delimitato da virgole (con estensione csv).  

> [!NOTE]  
>  Anche se solo i campi **Name**, **Publisher**, **Version**ed **EffectiveQuantity** devono contenere dati, nella prima riga del file di importazione delle licenze è necessario immettere tutti i campi. Tutti i campi di dati devono essere visualizzati nel formato seguente: mese/giorno/anno, ad esempio, 08/04/2008.  

 Asset Intelligence abbina i prodotti specificati nel resoconto delle licenze generale in base al nome e alla versione del prodotto, ma non in base al nome dell'editore. Nel resoconto delle licenze generale è necessario usare un nome di prodotto esattamente uguale al nome del prodotto archiviato nel database del sito. Asset Intelligence usa il numero **EffectiveQuantity** specificato nel resoconto delle licenze generale e confronta questo valore con il numero di prodotti installati nell'inventario di Configuration Manager.  

> [!TIP]  
>  Per ottenere un elenco completo dei nomi di prodotto archiviati nel database del sito di Configuration Manager, è possibile eseguire la query seguente nel database del sito: SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 È possibile specificare le versioni esatte per un prodotto o una parte della versione, ad esempio solo la versione principale. Gli esempi seguenti indicano le corrispondenze di versione risultanti per una voce di versione nel resoconto delle licenze generale per un prodotto specifico.  

|Voce resoconto licenze generale|Voci corrispondenti database del sito|  
|-------------------------------------|------------------------------------|  
|Name: "Software", ProductVersion0: "2"|ProductName0: "Software", ProductVersion0: "2.01.1234"<br /><br /> ProductName0: "Software", ProductVersion0: "2.02.5678"<br /><br /> ProductName0: "Software", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "Software", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "Software", ProductVersion0: "2.05.3579.000"<br /><br /> ProductName0: "Software", ProductVersion0: "2.10.1234"|  
|Name: "Software", Version "2.05"|ProductName0: "Software", ProductVersion0: "2.05.1234"<br /><br /> ProductName0: "Software", ProductVersion0: "2.05.5678"<br /><br /> ProductName0: "Software", ProductVersion0: "2.05.3579.000"|  
|Name: "Software", Version "2"<br /><br /> Name: "Software", Version "2.05"|Errore durante l'importazione. L'importazione non riesce quando più voci corrispondono alla stessa versione del prodotto.|  

 La procedura seguente descrive il processo che può essere usato per creare un file di importazione del resoconto delle licenze generale tramite Microsoft Excel.  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Per creare un file di importazione del resoconto delle licenze generale tramite Microsoft Excel  

1.  Aprire Microsoft Excel e creare un nuovo foglio di calcolo.  

2.  Nella prima riga del nuovo foglio di calcolo immettere tutti nomi dei campi di dati delle licenze software.  

3.  Nella seconda riga e in quelle successive del nuovo foglio di calcolo immettere le informazioni sulle licenze software richieste. Assicurarsi di immettere almeno tutti i campi dei dati delle licenze software obbligatori nelle righe successive per ogni licenza software da importare. Il nome del titolo software immesso nel foglio di calcolo deve essere uguale a quello visualizzato in Esplora inventario risorse per un computer client dopo l'esecuzione dell'inventario hardware.  

4.  Scegliere **Salva con nome** dal menu **File**e quindi salvare il file in formato CSV.  

5.  Copiare il file con estensione csv nella condivisione file usata per importare le informazioni sulle licenze software nel catalogo di Asset Intelligence.  

6.  Nella console di Configuration Manager usare l'Importazione guidata licenze software per importare il file di informazioni sulle licenze in formato CSV appena creato.  

7.  Eseguire il report **Licenza 15A - Report di riconciliazione licenza generale** per verificare che le informazioni sulle licenze siano state importate correttamente nel catalogo di Asset Intelligence.  

> [!NOTE]  
>  Per un esempio di un file di licenza software generale che è possibile usare a scopo di test, vedere [File generale di importazione delle licenze di Asset Intelligence di esempio in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Tabella di esempio per descrivere le licenze software  
 Quando si crea un file di importazione del resoconto delle licenze generale, è possibile usare le informazioni nella tabella seguente per descrivere le licenze software da importare nel catalogo di Asset Intelligence.  

|Nome della colonna|Tipo di dati|Richiesto|Esempio|  
|-----------------|---------------|--------------|-------------|  
|Name|Fino a 255 caratteri|Sì|Titolo software|  
|Publisher|Fino a 255 caratteri|Sì|Autore del software|  
|Version|Fino a 255 caratteri|Sì|Versione del titolo software|  
|Language|Fino a 255 caratteri|Sì|Lingua del titolo software|  
|EffectiveQuantity|Valore intero|Sì|Numero di licenze acquistate|  
|PONumber|Fino a 255 caratteri|No|Informazioni sull'ordine di acquisto|  
|ResellerName|Fino a 255 caratteri|No|Informazioni sul rivenditore|  
|DateOfPurchase|Valore di data nel formato seguente: MM/GG/AAAA|No|Data di acquisto della licenza|  
|SupportPurchased|Valore bit|No|0 o 1: immettere 0 per sì o 1 per no|  
|SupportExpirationDate|Valore di data nel formato seguente: MM/GG/AAAA|No|Data di fine del supporto acquistato|  
|Commenti|Fino a 255 caratteri|No|Commenti facoltativi|  

###  <a name="a-namebkmkconfiguremaintenancetasksa-configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configurare le attività di manutenzione di Asset Intelligence  
 Per Asset Intelligence sono disponibili le attività di manutenzione seguenti:  

-   **Verifica titolo applicazione con le informazioni di inventario**: questa attività di manutenzione controlla che il titolo software riportato nell'inventario software coincida con il titolo software nel catalogo di Asset Intelligence. Per impostazione predefinita, questa attività è abilitata e pianificata per l'esecuzione sabato tra le 00.00 e le 5.00. Questa attività di manutenzione è disponibile solo nel sito principale nella gerarchia di Configuration Manager.  

-   **Riepiloga dati software installato**: questa attività di manutenzione fornisce le informazioni visualizzate nell'area di lavoro **Asset e conformità** nel nodo **Asset Intelligence** all'interno del nodo **Software di inventario** . All'esecuzione dell'attività, Configuration Manager raccoglie un conteggio di tutti i titoli software di inventario nel sito primario. Per impostazione predefinita, questa attività è abilitata e pianificata per l'esecuzione giornaliera tra le 00.00 e le 5.00. Questa attività di manutenzione è disponibile solo nei siti primari.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Per configurare le attività di manutenzione di Asset Intelligence  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Selezionare il sito in cui si vuole configurare l'attività di manutenzione di Asset Intelligence.  

    > [!NOTE]  
    >  L'attività di manutenzione **Riepiloga dati software installato** è disponibile solo nei siti primari.  

4.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Manutenzione sito**. Verrà visualizzato un elenco di tutte le attività di manutenzione del sito disponibili.  

5.  Selezionare l'attività di manutenzione desiderata e quindi fare clic su **Modifica** per modificare le impostazioni.  

6.  Abilitare e configurare l'attività di manutenzione. Per evitare al massimo interferenze con le attività del sito, è consigliabile impostare il periodo di tempo su orari non di punta per il sito. Il periodo di tempo è l'intervallo di tempo in cui è possibile eseguire l'attività. È definito dagli orari specificati in **Avvia dopo** e **Ultima ora di avvio** nella finestra di dialogo **Attività Proprietà** .  

    > [!WARNING]  
    >  È possibile avviare immediatamente l'attività selezionando il giorno corrente e impostando **Avvia dopo** su un orario di un paio di minuti successivo all'ora corrente.  

7.  Fare clic su **OK** per salvare le impostazioni. L'attività viene ora eseguita in base alla pianificazione.  

    > [!NOTE]  
    >  Se l'esecuzione dell'attività non riesce al primo tentativo, Configuration Manager esegue altri tentativi fino a quando l'attività non viene eseguita correttamente o fino alla scadenza del periodo di tempo impostato per l'esecuzione dell'attività.  



<!--HONumber=Nov16_HO1-->


