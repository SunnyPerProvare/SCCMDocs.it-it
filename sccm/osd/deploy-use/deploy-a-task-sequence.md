---
title: Distribuire una sequenza di attività
titleSuffix: Configuration Manager
description: Usare le informazioni seguenti per distribuire una sequenza di attività ai computer in una raccolta.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3ff204e1908446cde9b0a4906c33b02ebb5a3bf
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75827003"
---
# <a name="deploy-a-task-sequence"></a>Distribuire una sequenza di attività

*Si applica a: Configuration Manager (Current Branch)*

Dopo aver creato una sequenza di attività e aver distribuito il contenuto di riferimento, distribuirla a una raccolta di dispositivi. Questa azione consente alla sequenza di attività di essere eseguita in un dispositivo. Una sequenza di attività distribuita può essere eseguita automaticamente o quando viene installata da un utente del dispositivo.

> [!WARNING]  
> È possibile gestire il comportamento relativo alle distribuzioni di sequenze di attività ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente e può causare risultati imprevisti. Ad esempio, una sequenza di attività con scopo impostato su **Richiesto** che distribuisce un sistema operativo viene considerata una distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](/configmgr/core/servers/manage/settings-to-manage-high-risk-deployments).  

## <a name="process"></a>Processo

Usare la seguente procedura per distribuire una sequenza di attività ai computer in una raccolta.  

> [!NOTE]  
> I messaggi di stato per la distribuzione della sequenza di attività vengono visualizzati nella finestra di messaggio in un sito primario, ma non vengono visualizzati in un sito di amministrazione centrale.  

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

2. Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da distribuire.  

3. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci** nel gruppo **Distribuzione**.  

    > [!NOTE]  
    > Se l'opzione **Distribuisci** non è disponibile, la sequenza di attività presenta un riferimento non valido. Correggere il riferimento e quindi tentare nuovamente la distribuzione della sequenza di attività.  

4. Nella pagina **Generale** specificare le informazioni seguenti.  

    - **Sequenza di attività**: specificare la sequenza di attività da distribuire. Per impostazione predefinita, in questa casella viene visualizzata la sequenza di attività selezionata.  

    - **Raccolta**: selezionare la raccolta contenente i computer che eseguono la sequenza di attività.  

        Non distribuire sequenze di attività che installano sistemi operativi in raccolte inappropriate, come ad esempio una raccolta di tutti i server di data center. Assicurarsi che la raccolta selezionata contenga solo i computer che devono eseguire la sequenza di attività.  

        Per altre informazioni sulle distribuzioni ad alto rischio, vedere [Distribuzioni ad alto rischio](#bkmk_high-risk).

    - **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**: archivia il contenuto della sequenza di attività nel gruppo di punti di distribuzione predefinito della raccolta. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, l'opzione è disattivata.  

    - **Distribuisci automaticamente contenuto per dipendenze**: se uno dei contenuti di riferimento ha dipendenze, il sito invia anche il contenuto dipendente ai punti di distribuzione.  

    - **Pre-download del contenuto per questa sequenza di attività**: Per altre informazioni, vedere [Configurare la pre-cache del contenuto](/configmgr/osd/deploy-use/configure-precache-content).  

    - **Selezionare il modello di distribuzione**: salvare e specificare un modello di distribuzione per una sequenza di attività.<!--1357391-->  

        > [!IMPORTANT]  
        > Alcuni elementi non vengono salvati nel modello.<!--510610--> Quando si esegue la distribuzione guidata, verificare di applicare gli elementi seguenti:  
        >
        > - Installazione software
        > - Pianificazione
        > - Download anticipato del contenuto

    - **Commenti (facoltativo)**: Specificare informazioni aggiuntive che descrivono la distribuzione della sequenza di attività.  

5. Nella pagina **Impostazioni distribuzione** specificare le informazioni seguenti:  

    - **Scopo**: dall'elenco a discesa scegliere una delle seguenti opzioni:  

        - **Disponibile**: l'utente visualizza la sequenza di attività in Software Center e può installarla su richiesta.  

        - **Richiesto**: Configuration Manager esegue automaticamente la sequenza di attività in base alla pianificazione configurata. Se la sequenza di attività non è nascosta, l'utente può comunque tenere traccia dello stato di distribuzione. Gli utenti possono anche usare Software Center per installare la sequenza di attività prima della scadenza.  

        > [!NOTE]
        > Se più utenti hanno eseguito l'accesso al dispositivo, le distribuzioni di sequenze di attività e di pacchetti potrebbero non comparire in Software Center.  

    - **Rendi disponibile per**: specificare se la sequenza di attività è disponibile per uno dei tipi seguenti:  

        - Solo client di Configuration Manager  
        - Client di Configuration Manager, supporti e PXE  
        - Solo supporti e PXE  
        - Solo supporti e PXE (nascosto)  

        > [!IMPORTANT]  
        > Usare l'impostazione **Solo supporti e PXE (nascosto)** per le distribuzioni sequenza di attività automatiche. Per fare in modo che il computer si avvii automaticamente al momento della distribuzione senza intervento dell'utente, selezionare **Consenti distribuzione automatica del sistema operativo** e impostare la variabile **SMSTSPreferredAdvertID** come parte del supporto. Per altre informazioni sulle variabili della sequenza di attività, vedere [Variabili della sequenza di attività](/configmgr/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID).  

    - **Invia pacchetti di riattivazione**: se la distribuzione è impostata su **Richiesto** e si seleziona questa opzione, il sito invia un pacchetto di riattivazione ai computer prima che il client esegua la distribuzione. Il pacchetto riattiva il computer dalla sospensione nel momento in cui scade l'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per la riattivazione LAN. Per altre informazioni, vedere [Pianificare la riattivazione dei client](/configmgr/core/clients/deploy/plan/plan-wake-up-clients).  

    - **Consente a tutti i client che utilizzano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**: questa opzione è disponibile solo quando la distribuzione è impostata su **Richiesto**. Quando una sequenza di attività personalizzata installa un'applicazione ma non distribuisce un sistema operativo, è possibile specificare se consentire ai client di scaricare il contenuto dopo la scadenza dell'installazione se usano una connessione Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati usati quando si usa una connessione Internet a consumo.  

        > [!NOTE]  
        > Anche se potrebbe funzionare per le sequenze di attività che non distribuiscono un sistema operativo, l'uso di una connessione Internet a consumo non è supportato.  

6. Nella pagina **Pianificazione** specificare le informazioni seguenti:  

    > [!IMPORTANT]  
    > Quando un client di Windows PE viene avviato da PXE o da supporti di avvio, il client non valuta le pianificazioni della distribuzione. Queste pianificazioni includono avvio, scadenza e date di scadenza. Configurare le pianificazioni solo nelle distribuzioni ai client che vengono avviati dal sistema operativo Windows completo. Considerare la possibilità di usare altri metodi, ad esempio le finestre di manutenzione, per controllare le sequenze di attività attive distribuite ai client che vengono avviati da Windows PE.  

    - **Pianifica quando questa distribuzione diventerà disponibile**: Specificare la data e l'ora in cui la sequenza di attività è disponibile per l'esecuzione nel computer di destinazione. Quando si seleziona l'opzione **UTC**, la sequenza di attività è disponibile per più computer contemporaneamente. In caso contrario, la distribuzione è disponibile a orari diversi, in base all'ora locale di ogni computer.  

        Se l'ora di avvio è precedente rispetto al tempo necessario, il client scarica il contenuto della sequenza di attività all'ora di avvio.  

    - **Pianifica alla scadenza di questa assegnazione**: Specificare la data e l'ora di scadenza della sequenza di attività nel computer di destinazione. Quando si seleziona l'opzione **UTC**, la sequenza di attività scade in più computer contemporaneamente. In caso contrario, la distribuzione scade a orari diversi, in base all'ora locale di ogni computer.  

    - **Pianificazione assegnazione**: per una distribuzione di tipo **Richiesto**, specificare quando il client esegue la sequenza di attività. È possibile aggiungere più pianificazioni. La pianificazione dell'assegnazione può avere una delle configurazioni seguenti:  

        - Data e ora specifiche  
        - Criterio di ricorrenza mensile, settimanale o personalizzato  
        - Non appena possibile  
        - Eventi di accesso o disconnessione  

        > [!NOTE]  
        > Se si pianifica un'ora di avvio per una distribuzione richiesta precedente alla data e ora in cui la sequenza di attività è disponibile, il client di Configuration Manager scarica il contenuto all'ora di avvio assegnata. Questo comportamento si verifica anche se si è pianificato che la sequenza di attività sia disponibile in un secondo momento.<!--SCCMDocs issue 777-->  

    - **Riesegui comportamento**: specificare quando viene eseguita nuovamente la sequenza di attività. Selezionare una delle opzioni seguenti:  

        - **Non rieseguire mai un programma distribuito**: se la sequenza di attività è già stata eseguita nel client, non viene eseguita nuovamente. Anche se originariamente si sono verificati errori o se sono stati modificati i file della sequenza di attività, la sequenza di attività non viene rieseguita.  

        - **Riesegui sempre un programma**: la sequenza di attività viene sempre rieseguita nel client quando la distribuzione è pianificata. Viene rieseguita anche se la sequenza di attività è già stata eseguita correttamente. Questa impostazione è utile quando si usano distribuzioni ricorrenti in cui la sequenza di attività viene regolarmente aggiornata.  

            > [!IMPORTANT]  
            > Questa opzione è selezionata per impostazione predefinita. Non ha tuttavia effetto fino a quando non si assegna una distribuzione richiesta. Un utente può sempre rieseguire le distribuzioni disponibili.  

        - **Riesegui se il tentativo precedente non è riuscito**: la sequenza di attività viene rieseguita quando la distribuzione è pianificata solo se non è stata eseguita correttamente in precedenza. Questa impostazione è utile per una distribuzione obbligatoria. Se l'ultimo tentativo di esecuzione non è riuscito, la sequenza di attività verrà nuovamente eseguita in base alla pianificazione di assegnazione.  

        - **Riesegui se il tentativo precedente è riuscito**: la sequenza di attività viene rieseguita solo se è stata eseguita correttamente in precedenza nel client. Questa impostazione è utile quando di usano distribuzioni ricorrenti in cui la sequenza di attività viene regolarmente aggiornata e ogni aggiornamento richiede che quello precedente sia installato correttamente.  

        > [!NOTE]  
        > Un utente può rieseguire la distribuzione di una sequenza di attività disponibile. Prima di distribuire una sequenza di attività disponibile in un ambiente di produzione, testare che cosa accade se un utente riesegue la sequenza di attività più volte.  

7. Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

    - **Consenti agli utenti di eseguire il programma indipendentemente dalle assegnazioni**: specificare se un utente può eseguire una distribuzione richiesta al di fuori della pianificazione di assegnazione. Questa opzione è sempre abilitata per le distribuzioni disponibili.  

    - **Mostra stato sequenza di attività**: specificare se il client di Configuration Manager visualizza lo stato di avanzamento della sequenza di attività.  

    - **Installazione software**: specificare se l'utente è autorizzato a installare il software al di fuori di una finestra di manutenzione configurata dopo l'orario pianificato.  

    - **Riavvio del sistema (se necessario per completare l'installazione)**: Specificare se l'utente è autorizzato a riavviare il computer dopo l'installazione software all'esterno di una finestra di manutenzione configurata dopo il periodo di assegnazione.  

    - **Gestione filtri di scrittura per dispositivi con Windows Embedded**: questa impostazione controlla il comportamento di installazione nei dispositivi con Windows Embedded in cui è abilitato un filtro di scrittura. Scegliere l'opzione per eseguire il commit delle modifiche alla scadenza dell'installazione o durante una finestra di manutenzione. Quando si seleziona questa opzione, è necessario un riavvio e la modifica viene salvata in modo permanente nel dispositivo. In caso contrario, l'applicazione viene installata nell'overlay temporaneo e il commit viene eseguito successivamente. Quando si distribuisce una sequenza di attività in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata.  

    - **Consenti l'esecuzione della sequenza di attività per il client in Internet**: specificare se la sequenza attività può essere eseguita in un client basato su Internet. Le operazioni che richiedono un supporto di avvio, ad esempio l'installazione di un sistema operativo, non sono supportate con questa impostazione. Usare questa opzione solo per installazioni software o sequenze di attività generiche basate su script che eseguono operazioni nel sistema operativo standard.  

        - Questa impostazione è supportata per le distribuzioni di una sequenza di attività di aggiornamento sul posto di Windows 10 in client basati su Internet mediante Cloud Management Gateway. Per altre informazioni, vedere [Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. Nella pagina **Avvisi** specificare le impostazioni di avviso desiderate per la distribuzione di questa sequenza di attività.  

9. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti:  

    - **Opzioni di distribuzione**: Specificare una delle opzioni seguenti:  

        > [!NOTE]  
        > Quando si usa il multicast per distribuire un sistema operativo, scaricare il contenuto nei computer quando necessario oppure prima dell'esecuzione della sequenza di attività.  

        - **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**: specificare che i client scaricano contenuto dal punto di distribuzione nel computer di destinazione come richiesto dalla sequenza di attività. Il client avvia la sequenza di attività. Quando un passaggio della sequenza di attività richiede il contenuto, il download viene eseguito prima dell'esecuzione del passaggio.  

        - **Scaricare tutto il contenuto localmente prima di avviare la sequenza di attività**: specificare che i client scaricano tutto il contenuto dal punto di distribuzione prima dell'esecuzione della sequenza di attività. Se si è resa la sequenza di attività disponibile nelle distribuzioni PXE e dei supporti di avvio nella pagina **Impostazioni distribuzione**, questa opzione non viene visualizzata.  

        - **Accedere al contenuto direttamente da un punto di distribuzione quando necessario eseguendo la sequenza di attività**: Specificare che i client eseguono il contenuto dal punto di distribuzione. Questa opzione è disponibile solo quando si abilitano tutti i pacchetti associati con la sequenza di attività all'uso di una condivisione pacchetto nel punto di distribuzione. Per abilitare il contenuto all'utilizzo di una condivisione pacchetto, vedere la scheda **Accesso dati** nelle **Proprietà** di ciascun pacchetto.  

            > [!IMPORTANT]  
            > Per maggior sicurezza, selezionare le opzioni che consentono di **scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività** o di **scaricare tutto il contenuto localmente prima di avviare la sequenza di attività**. Quando si seleziona una di queste opzioni, Configuration Manager genera un hash del pacchetto in modo da garantire l'integrità del pacchetto. Quando si seleziona l'opzione che consente di **accedere al contenuto direttamente da un punto di distribuzione quando necessario eseguendo la sequenza di attività**, Configuration Manager non verifica l'hash del pacchetto prima di eseguire il programma specificato. Poiché il sito non può garantire l'integrità del pacchetto, gli utenti con diritti amministrativi possono modificare o alterare i contenuti del pacchetto.  

    - **Usare un punto di distribuzione remoto quando non sono disponibili punti di distribuzione locali**: specificare se i client possono usare punti di distribuzione remoti da un gruppo di limiti vicino per scaricare il contenuto necessario per la sequenza di attività.  

    - **Consenti ai client di usare punti di distribuzione dal gruppo di limiti del sito predefinito**: specificare se i clienti devono scaricare il contenuto da un punto di distribuzione nel gruppo di limiti del sito predefinito quando il contenuto non è disponibile in un punto di distribuzione nel gruppo di limiti corrente o nei gruppi di limiti vicini.  

        > [!Note]  
        > A partire dalla versione 1810, quando un dispositivo esegue una sequenza di attività e deve acquisire il contenuto, il dispositivo usa comportamenti dei gruppi di limiti simili al client Configuration Manager. Per altre informazioni, vedere [Supporto della sequenza di attività per i gruppi di limiti](/configmgr/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).<!--1359025-->  

10. Per salvare queste impostazioni per riutilizzarle, nella scheda **Riepilogo** selezionare **Salva come modello**. Assegnare un nome al modello e selezionare le impostazioni da salvare.  

11. Completare la procedura guidata.  

## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway

<!-- 1357149 -->
La sequenza di attività di aggiornamento sul posto di Windows 10 supporta la distribuzione nei client basati su Internet gestiti tramite [Cloud Management Gateway](/configmgr/core/clients/manage/plan-cloud-management-gateway) (CMG). Ciò consente agli utenti remoti di eseguire più facilmente l'aggiornamento a Windows 10 senza doversi connettere a Internet.

Verificare che tutto il contenuto a cui fa riferimento la sequenza di attività di aggiornamento sul posto sia distribuito a un CMG abilitato per il contenuto. [Consenti il funzionamento di CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#settings) **come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**: È anche possibile usare un [punto di distribuzione cloud](/configmgr/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). In caso contrario i dispositivi non potranno eseguire la sequenza di attività.

Per distribuire una sequenza di attività di aggiornamento sul posto usare le impostazioni seguenti:

- **Consenti l'esecuzione della sequenza di attività per il client in Internet** nella scheda Esperienza utente della distribuzione.  

- Scegliere una delle opzioni seguenti nella scheda punti di distribuzione della distribuzione:

  - **Scaricare il contenuto localmente quando necessario eseguendo la sequenza di attività**. A partire dalla versione 1910, il motore della sequenza di attività può scaricare pacchetti su richiesta da un servizio CMG abilitato per il contenuto o da un punto di distribuzione cloud. Questa modifica offre ulteriore flessibilità con le distribuzioni di aggiornamento sul posto di Windows 10 ai dispositivi basati su Internet.<!--3601238-->

  - **Scaricare tutto il contenuto in locale prima di avviare la sequenza di attività**. In Configuration Manager versione 1906 e versioni precedenti, altre opzioni come **scaricare il contenuto localmente quando necessario per la sequenza di attività in esecuzione** non funzionano in questo scenario. Il motore della sequenza di attività non è in grado di scaricare il contenuto da un'origine cloud. Il client Gestione configurazione deve scaricare il contenuto dall'origine cloud prima di avviare la sequenza di attività. È comunque possibile usare questa opzione nella versione 1910, se necessario, per soddisfare i requisiti.

- (*Facoltativo*) **Pre-download del contenuto per questa sequenza di attività** nella scheda Generale della distribuzione. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](/configmgr/osd/deploy-use/configure-precache-content).  

> [!NOTE]
> Avviare la sequenza di attività da Software Center. Questo scenario non supporta Windows PE, PXE e i supporti per sequenza di attività.

## <a name="bkmk_high-risk"></a> Distribuzioni ad alto rischio

Quando si esegue una distribuzione ad alto rischio, ad esempio quella di un sistema operativo, nella finestra **Seleziona raccolta** vengono visualizzate soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito. Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**. Per visualizzare tutte le raccolte personalizzate che contengono un numero di client inferiore rispetto alla dimensione massima configurata, disabilitare **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](/configmgr/core/servers/manage/settings-to-manage-high-risk-deployments).  

Le impostazioni di verifica della distribuzione sono basate sull'appartenenza attuale della raccolta. Dopo aver distribuito la sequenza di attività, Configuration Manager non rivaluta l'appartenenza alla raccolta per le impostazioni di distribuzione ad alto rischio.  

Ad esempio, si supponga di impostare **Dimensione predefinita** su 100 e **Dimensione massima** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** vengono visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  

Quando si seleziona una raccolta che include un ruolo del sito, si applicano i comportamenti seguenti:  

- Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da bloccare le raccolte con server di sistema del sito, si verifica un errore. A questo punto la creazione della distribuzione non continua.  

- Se si applica uno dei criteri seguenti, nella Distribuzione guidata del software viene visualizzato un messaggio sul rischio elevato. Per continuare, è necessario accettare di creare una distribuzione ad alto rischio. Il sito genera un messaggio di stato di controllo.  

  - Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da generare un avviso per le raccolte con server di sistema del sito  

  - Se la raccolta supera il valore predefinito delle dimensioni

  - Se la raccolta contiene un server  

## <a name="see-also"></a>Vedere anche

[Gestire le sequenze di attività per automatizzare le attività](/configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks)
