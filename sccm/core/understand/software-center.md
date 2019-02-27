---
title: Manuale dell'utente di Software Center
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità di Software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.collection: M365-identity-device-management
ms.openlocfilehash: da01c741107d4eb4a707f7f0d8ada5d82706f292
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119892"
---
# <a name="software-center-user-guide"></a>Manuale dell'utente di Software Center

*Si applica a: System Center Configuration Manager (Current Branch)*

L'amministratore IT dell'organizzazione usa Software Center per installare le applicazioni e gli aggiornamenti dei prodotti software e di Windows. Questo manuale dell'utente illustra le funzionalità di Software Center per gli utenti del computer.

### <a name="general-notes-about-software-center-functionality"></a>Note generali sulle funzionalità di Software Center
- Questo articolo descrive le funzionalità più recenti di Software Center. Se l'organizzazione usa una versione precedente ma ancora supportata di Software Center, non sono disponibili tutte le funzionalità. Per altre informazioni, contattare l'amministratore IT.
- L'amministratore IT può disabilitare alcune funzionalità di Software Center. L'esperienza specifica può variare.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Come aprire Software Center

Il metodo più semplice per avviare Software Center in un computer Windows 10 consiste nel premere **Start** e digitare `Software Center`. 

Se si scorre il menu Start, trovare nel gruppo **Microsoft System Center** l'icona **Software Center**.



## <a name="applications"></a>Applicazioni

Fare clic sulla scheda **Applicazioni** per trovare e installare le applicazioni che l'amministratore IT distribuisce all'utente o al computer.
- **Tutte**: visualizza tutte le applicazioni che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di queste applicazioni. Se si disinstalla una di queste applicazioni, Software Center la reinstalla.
- **Filtri**: l'amministratore IT può creare categorie di applicazioni. Se disponibile, fare clic sull'elenco a discesa per filtrare la visualizzazione e visualizzare solo le applicazioni di una categoria specifica. Selezionare **Tutte** per visualizzare tutte le applicazioni.
- **Ordina per**: consente di riordinare l'elenco delle applicazioni. Per impostazione predefinita questo elenco è ordinato per **Più recente**.
- **Cerca**: l'elemento cercato non è stato trovato? Immettere parole chiave nella casella di ricerca per trovarlo.
-  **Alternare la visualizzazione**: fare clic sulle icone per alternare tra la visualizzazione elenco e la visualizzazione affiancata. Per impostazione predefinita l'elenco delle applicazioni viene visualizzato sotto forma di elementi grafici affiancati. 
    - Visualizzazione affiancata: l'amministratore IT può personalizzare le icone. Sotto ogni riquadro vengono visualizzati il nome dell'applicazione, l'editore e la versione. 
    - Visualizzazione elenco: contiene l'icona dell'applicazione, il nome, l'editore, la versione e lo stato. 


### <a name="install-multiple-applications"></a>Installare più applicazioni 
<!-- 1357126 --> È possibile installare più applicazioni contemporaneamente anziché attendere il completamento di un'installazione prima di iniziare quella successiva. Non tutte le applicazioni sono idonee:
- L'app deve essere visibile all'utente
- L'app non deve essere già installata o in fase di download
- Per installare l'app non è necessaria l'approvazione dell'admin IT

Per installare più applicazioni contemporaneamente:
 1. Per accedere alla modalità di selezione multipla nella visualizzazione elenco, fare clic sull'icona di selezione multipla ![Icona di selezione multipla del Software Center](media/software-center-multi-select-apps.png) nell'angolo superiore destro.
 2. Selezionare due o più app da installare facendo clic sulla casella di controllo a sinistra delle app nell'elenco.
 3. Fare clic sul pulsante di **installazione degli elementi selezionati**.

Le app vengono installate come di consueto, ma in successione.




## <a name="updates"></a>Aggiornamenti

Fare clic sulla scheda **Aggiornamenti** per visualizzare e installare gli aggiornamenti software che l'amministratore IT distribuisce a questo computer.  
- **Tutti**: visualizza tutti gli aggiornamenti che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di questi aggiornamenti.
- **Ordina per**: consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.

Per installare gli aggiornamenti, fare clic su **Installa tutto**.

Per installare solo aggiornamenti specifici, fare clic sull'icona che consente di passare alla modalità di selezione multipla. Selezionare gli aggiornamenti da installare, quindi fare clic su **Installa selezionati**.



## <a name="operating-systems"></a>Sistemi operativi

Fare clic sulla scheda **Sistemi operativi** per visualizzare e installare le versioni di Windows che l'amministratore IT distribuisce al computer.  
- **Tutte**: visualizza tutte le versioni di Windows che è possibile installare
- **Richiesto**: l'amministratore IT richiede l'installazione di questi aggiornamenti.
- **Ordina per**: consente di riordinare l'elenco degli aggiornamenti. Per impostazione predefinita questo elenco è ordinato per **Nome applicazione: da A a Z**.



## <a name="installation-status"></a>Stato installazione

Fare clic sulla scheda **Stato installazione** per visualizzare lo stato delle applicazioni. Possono essere visualizzati gli stati seguenti:
- **Installata**: Software Center ha già installato questa applicazione nel computer.
- **Download in corso**: Software Center sta scaricando il software da installare nel computer.
- **Operazione non riuscita**: Software Center ha riscontrato un errore nel tentativo di installare il software.
- **Installazione pianificata dopo** : mostra la data e ora della successiva finestra di manutenzione del dispositivo per installare software futuri. Le finestre di manutenzione vengono definite dall'amministratore IT.<!--1358131-->
    - Lo stato può essere visualizzato nelle schede **Tutto** e **Imminente**. 
    - È possibile eseguire l'installazione prima della data e dell'ora della finestra di manutenzione facendo sul pulsante **Installa adesso**. 

L'amministratore IT può consentire di visualizzare le applicazioni dal sito Web del Catalogo applicazioni. Per visualizzare il sito Web, fare clic su **Aprire il sito Web del Catalogo applicazioni** nell'angolo in alto a destra. <!--1358214-->

## <a name="device-compliance"></a>Conformità del dispositivo

Fare clic sulla scheda **Conformità del dispositivo** per visualizzare lo stato di conformità del computer.

Fare clic su **Controlla conformità** per confrontare le impostazioni del dispositivo con i criteri di sicurezza definiti dall'amministratore IT.



## <a name="options"></a>Opzioni

Fare clic sulla scheda **Opzioni** per visualizzare le impostazioni aggiuntive per questo computer.

### <a name="work-information"></a>Informazioni di lavoro

Indicare l'orario di lavoro generico. L'amministratore IT può pianificare installazioni di software fuori dall'orario lavorativo. Prevedere almeno quattro ore al giorno per le attività di manutenzione del sistema. L'amministratore IT può installare comunque applicazioni e aggiornamenti critici durante l'orario di ufficio.

- Fare clic sugli elenchi a discesa per selezionare le ore in cui si inizia e si smette di usare il computer. Per impostazione predefinita questi valori sono compresi tra **5.00** e **22.00**.

- Selezionare la casella di controllo accanto ai giorni della settimana nei quali in genere viene usato il computer. Per impostazione predefinita Software Center seleziona solo i giorni lavorativi.  


### <a name="power-management"></a>Risparmio energia

L'amministratore IT può impostare criteri di risparmio energia. Questi criteri aiutano l'organizzazione a risparmiare energia elettrica quando il computer non è in uso. 

Per rendere il computer esente da questi criteri, selezionare la casella di controllo **Non applicare le impostazioni di risparmio energia del reparto IT al computer**. Questa impostazione è disabilitata per impostazione predefinita. Il computer applica le impostazioni di risparmio energia. 


### <a name="computer-maintenance"></a>Manutenzione computer

Specifica come Software Center applica le modifiche al software prima della scadenza.
- **Installare o disinstallare automaticamente il software richiesto e riavviare il computer solo fuori dall'orario di lavoro specificato**: Per impostazione predefinita, questa impostazione è disabilitata.
- **Sospendi le attività di Software Center quando il computer si trova in modalità presentazione**: Questa opzione è attivata per impostazione predefinita.
- **Sincronizza criteri**: fare clic su questo pulsante quando richiesto dall'amministratore IT. Il computer verifica sui server la presenza di nuovi elementi, quali applicazioni, aggiornamenti software o sistemi operativi.

## <a name="custom-tab-in-software-center"></a>Scheda personalizzata in Software Center
L'amministratore IT potrebbe avere aggiunto una scheda aggiuntiva in Software Center. Questa scheda viene denominata dall'amministratore e porta a un sito Web specificato. Ad esempio, si potrebbe avere una scheda denominata "Help desk" che conduce al sito Web dell'help desk dell'organizzazione. <!--1358132-->
