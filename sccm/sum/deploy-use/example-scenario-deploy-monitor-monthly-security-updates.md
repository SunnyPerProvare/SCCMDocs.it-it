---

title: Scenario di esempio per distribuire e monitorare gli aggiornamenti software di sicurezza | Microsoft Docs
description: Questo scenario di esempio descrive come usare gli aggiornamenti software in Configuration Manager per distribuire e monitorare gli aggiornamenti software di sicurezza rilasciati ogni mese da Microsoft.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-sum
ms.service: 
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 0e6e2b3a9455bb6eda437eb1325aaaadb3d83420



---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>Scenario di esempio per l'uso di System Center Configuration Manager per la distribuzione e il monitoraggio degli aggiornamenti software della sicurezza rilasciati ogni mese da Microsoft

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento illustra uno scenario di esempio sull'uso degli aggiornamenti software in System Center Configuration Manager per la distribuzione e il monitoraggio degli aggiornamenti software di sicurezza rilasciati ogni mese da Microsoft.  

 In questo scenario Giorgio è l'amministratore di Configuration Manager presso Woodgrove Bank. Giorgio deve creare una strategia di distribuzione degli aggiornamenti del software con i requisiti e le condizioni seguenti:  

-   La distribuzione degli aggiornamenti del software attivo avviene una settimana dopo il rilascio da parte di Microsoft degli aggiornamenti del software di protezione il secondo martedì di ogni mese. In genere, questo evento viene definito Patch martedì.  

-   Gli aggiornamenti software vengono scaricati e pre-installati nei punti di distribuzione. Una distribuzione viene quindi testata in un sottoinsieme di client prima che Giorgio distribuisca gli aggiornamenti software in un ambiente di produzione.  

-   Giorgio deve essere in grado di monitorare la conformità degli aggiornamenti del software in base al mese o all'anno.  

 Questo scenario si presuppone che l'infrastruttura del punto di aggiornamento software sia già stata implementata. Usare le informazioni seguenti per pianificare e configurare gli aggiornamenti software in Configuration Manager.  

|Processo|Riferimento|  
|-------------|---------------|  
|Esaminare i concetti chiave per gli aggiornamenti software.|[Introduction to software updates](../understand/software-updates-introduction.md) (Introduzione agli aggiornamenti software)|  
|Pianificare gli aggiornamenti del software. Queste informazioni consentono di pianificare considerazioni relative alla capacità e di determinare l'infrastruttura del punto di aggiornamento software e le impostazioni di sincronizzazione e del client per gli aggiornamenti software.|[Plan for software updates](../plan-design/plan-for-software-updates.md) (Pianificare gli aggiornamenti del software)|  
|Configurare gli aggiornamenti software. Queste informazioni consentono di installare e configurare punti di aggiornamento software nella gerarchia e di configurare e sincronizzare gli aggiornamenti software.<br /><br /> In questo scenario Giorgio configura la pianificazione di sincronizzazione degli aggiornamenti software in modo che venga eseguita il secondo mercoledì di ogni mese, così da assicurarsi di recuperare gli aggiornamenti software di sicurezza più recenti rilasciati da Microsoft.|[Synchronize software updates](../get-started/synchronize-software-updates.md) (Sincronizzare gli aggiornamenti software)|  

 Le sezioni seguenti di questo argomento includono procedure di esempio che consentono di distribuire e monitorare gli aggiornamenti software di sicurezza di Configuration Manager all'interno dell'organizzazione.

##  <a name="a-namebkmkstep1a-step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a> Passaggio 1: Creare un gruppo di aggiornamento software per la conformità annuale  
 Giorgio crea un gruppo di aggiornamento software che può usare per monitorare la conformità di tutti gli aggiornamenti software di sicurezza rilasciati nel 2016. Esegue quindi i passaggi indicati nella seguente tabella.  

|Processo|Riferimento|  
|-------------|---------------|  
|Dal nodo **Tutti gli aggiornamenti software** nella console di Configuration Manager Giorgio aggiunge i criteri per visualizzare solo gli aggiornamenti software di sicurezza rilasciati o rivisiti nel corso del 2015 che soddisfano i requisiti seguenti:<br /><br /><ul><li>**Criteri**: Data rilascio o revisione</li><li>**Condizione**: è maggiore o uguale a una data specifica<br />**Valore**: 1/1/2015</li><li>**Criteri**: Classificazione aggiornamento<br />**Valore**: Aggiornamenti della sicurezza</li><li>**Criteri**: Scaduto <br />**Valore**: No</li></ul>|Nessuna informazione aggiuntiva|
|Giorgio aggiunge tutti gli aggiornamenti software filtrati in un nuovo gruppo di aggiornamento software con i seguenti requisiti:<br /><br /><ul><li>**Nome**: Gruppo di conformità - Aggiornamenti della sicurezza Microsoft 2015</li><li>**Descrizione**: Aggiornamenti software|[Aggiungere aggiornamenti software a un gruppo di aggiornamento](add-software-updates-to-an-update-group.md)|  

##  <a name="a-namebkmkstep2a-step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a> Passaggio 2: Creare una regola di distribuzione automatica per il mese corrente  
 Giorgio rea una regola di distribuzione automatica per gli aggiornamenti software di protezione rilasciati da Microsoft per il mese corrente. Esegue quindi i passaggi indicati nella seguente tabella.  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio crea una regola di distribuzione automatica con i seguenti requisiti:<br /><br /><ol><li>Nella scheda **Generale** Giorgio configura quanto segue:<br /> <ul><li>Specifica **Aggiornamenti mensili della sicurezza** come nome.</li><li>Seleziona una raccolta di test con client limitati.</li><li>Seleziona **Crea un nuovo gruppo di aggiornamento software**.</li><li>Verifica che l'opzione **Abilita la distribuzione dopo l'esecuzione della regola** non sia selezionata.</li></ul></li><li>Nella scheda **Impostazioni di distribuzione** Giorgio seleziona le impostazioni predefinite.</li><li>Nella pagina **Aggiornamenti software** Giorgio configura i filtri proprietà e i criteri di ricerca seguenti:<br /><ul><li>Data rilascio o revisione: **Ultimo mese**.</li><li>Classificazione aggiornamento: **Aggiornamenti della sicurezza**.</li></ul></li><li>Nella pagina **Valutazione** Giorgio abilita la regola in modo che venga eseguita secondo pianificazione il **secondo giovedì** di ogni **mese**. Giorgio verifica anche che la pianificazione della sincronizzazione sia impostata per essere eseguita il **secondo mercoledì** di ogni **mese**.</li><li>Giorgio utilizza le impostazioni predefinite nelle pagine Pianificazione della distribuzione, Esperienza utente, Avvisi e Impostazioni download.</li><li>Nella pagina **Pacchetto di distribuzione** Giorgio specifica un nuovo pacchetto di distribuzione.</li><li>Giorgio utilizza le impostazioni predefinite nelle pagine Percorso download e Selezione lingua.</li></ol>|[Distribuire automaticamente gli aggiornamenti software](automatically-deploy-software-updates.md)|  

##  <a name="a-namebkmkstep3a-step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a> Passaggio 3: Verificare che gli aggiornamenti software siano pronti per la distribuzione  
 Il secondo giovedì di ogni mese Giorgio verifica che gli aggiornamenti software siano pronti per la distribuzione. Esegue il passo seguente.  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio verifica che la sincronizzazione degli aggiornamenti del software sia stata completata correttamente.|[Software updates synchronization status](monitor-software-updates.md#BKMK_SUSyncStatus) (Stato di sincronizzazione degli aggiornamenti software)|  

##  <a name="a-namebkmkstep4a-step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a> Passaggio 4: Distribuire il gruppo di aggiornamenti software  
 Dopo aver verificato che gli aggiornamenti software sono pronti per la distribuzione, Giorgio esegue la distribuzione. Esegue quindi i passaggi indicati nella seguente tabella.  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio crea due distribuzioni di prova per il nuovo gruppo di aggiornamento software. Per ogni distribuzione, considera i seguenti ambienti:<br /><br /> **Distribuzione di test delle workstation**: per la distribuzione di test delle workstation, Giorgio considera quanto segue:<br /><br /><ul><li>Specifica una raccolta di distribuzioni che contiene un subset di client per workstation per la verifica della distribuzione.</li><li>Configura le impostazioni di distribuzione appropriate per i client per workstation presenti nell'ambiente.</li></ul><br />**Distribuzione di test dei server**: per la distribuzione di test dei server, Giorgio considera quanto segue:<br /><br /><ul><li>Specifica una raccolta di distribuzioni che contiene un subset di client di server per la verifica della distribuzione.</li><li>Configura le impostazioni di distribuzione appropriate per i client di server presenti nell'ambiente.</li></ul>|[Deploy software updates](deploy-software-updates.md) (Distribuire gli aggiornamenti software)|  
|Giorgio verifica che le distribuzioni di prova siano state distribuite correttamente.|[Software updates deployment status](monitor-software-updates.md#BKMK_SUDeployStatus) (Stato di distribuzione degli aggiornamenti software)|  
|Giorgio aggiorna le due distribuzioni con nuove raccolte che includono i server e le workstation di produzione relativi.|Nessuna informazione aggiuntiva|  

##  <a name="a-namebkmkstep5a-step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a> Passaggio 5: Monitorare la conformità per gli aggiornamenti software distribuiti  
 Giorgio monitora la conformità delle distribuzioni degli aggiornamenti software. Esegue quindi la procedura indicata nella seguente tabella.  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio monitora lo stato della distribuzione degli aggiornamenti software nella console di Configuration Manager e controlla i relativi report disponibili nella console.|[Monitor software updates in System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md) (Monitorare gli aggiornamenti software in System Center Configuration Manager)|  

##  <a name="a-namebkmkstep6a-step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a> Passaggio 6: Aggiungere aggiornamenti software mensili al gruppo di aggiornamento annuale  
 Giorgio aggiunge gli aggiornamenti software dal gruppo di aggiornamento software mensile al gruppo di aggiornamento software annuale. Esegue quindi la procedura indicata nella seguente tabella.  

|Processo|Riferimento|  
|-------------|---------------|  
|Giorgio seleziona gli aggiornamenti software dal gruppo di aggiornamento mensile e li aggiunge al gruppo di aggiornamento creato per la conformità annuale. Tiene traccia della conformità degli aggiornamenti software e crea diversi report per la gestione.|[Add software updates to a deployed update group](add-software-updates-to-an-update-group.md) (Aggiungere gli aggiornamenti software a un gruppo di aggiornamento distribuito)|  

Giorgio ha completato la distribuzione mensile per gli aggiornamenti del software di protezione. Continua a monitorare e creare report relativi alla compatibilità degli aggiornamenti software per assicurarsi che i client presenti nell'ambiente rientrino nei livelli di conformità accettabili.  

##  <a name="a-namebkmkmonthlyprocessa-recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a> Processo mensile ricorrente per la distribuzione degli aggiornamenti software  
 Dopo il primo mese di distribuzione degli aggiornamenti software, Giorgio esegue la procedura (dal passaggio 3 al passaggio 6) per distribuire gli aggiornamenti mensili del software di protezione rilasciati da Microsoft.  



<!--HONumber=Dec16_HO3-->


