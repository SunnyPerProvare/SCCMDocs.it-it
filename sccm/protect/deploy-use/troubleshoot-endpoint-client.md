---
title: Risoluzione dei problemi di Windows Defender o del client Endpoint Protection
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi con Windows Defender ed Endpoint Protection.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f7528f15c67e8ce339013db583d545cb252712d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125664"
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Risoluzione dei problemi di Windows Defender o del client Endpoint Protection

*Si applica a: System Center Configuration Manager (Current Branch)*


Se si verificano problemi con Windows Defender o Endpoint Protection, chiedere assistenza all'amministratore della protezione. È anche possibile provare a risolvere i problemi seguenti:  

-   [Aggiornamento di Windows Defender o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Avvio del servizio di Windows Defender o Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
-   [Problemi di connessione a Internet](#internet-connection-issues)  
-   [Minaccia rilevata che non è possibile correggere](#detected-threat-cant-be-remediated)  
-   [Installazione del client Endpoint Protection](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Aggiornamento di Windows Defender o Endpoint Protection  
 Windows Defender o Endpoint Protection interagisce automaticamente con Microsoft Update garantendo in tal modo che le definizioni di virus e spyware siano sempre aggiornate.  

 **Sintomi**  

 Questo articolo illustra i problemi più comuni relativi agli aggiornamenti automatici, incluse le situazioni seguenti:  

- Vengono visualizzati messaggi di errore per indicare che gli aggiornamenti non sono riusciti.  

- Durante la verifica della disponibilità degli aggiornamenti viene visualizzato un messaggio di errore in cui si informa che non è possibile verificare, scaricare o installare gli aggiornamenti delle definizioni di virus e spyware.  

- Gli aggiornamenti non riescono anche se si è connessi a Internet.  

- Gli aggiornamenti non vengono installati automaticamente come pianificato.  

  **Causa**  

  Le cause più comuni dei problemi di aggiornamento sono correlate a problemi di connettività Internet. Se però si sa di essere connessi a Internet perché si riesce a esplorare altri siti Web, il problema potrebbe dipendere da conflitti nelle impostazioni di Windows Internet Explorer.  

> [!IMPORTANT]  
>  Per completare questa procedura, è necessario chiudere Internet Explorer. Di conseguenza, stampare o annotare queste istruzioni oppure copiarle in un altro file e quindi aggiungere un segnalibro a questo argomento per potervi accedere in seguito.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Passaggio 1: reimpostare le impostazioni di Internet Explorer  

1.  Chiudere tutti i programmi aperti, incluso Internet Explorer.  

    > [!NOTE]  
    >  La reimpostazione di Internet Explorer implica l'eliminazione dei file temporanei, dei cookie, della cronologia di esplorazione e delle password online, ma non dei Preferiti.  

2.  Fare clic su **Start** , cercare **inetcpl.cpl**e quindi premere **INVIO**.  

3.  Nella finestra di dialogo **Opzioni Internet** fare clic sulla scheda **Avanzate** .  

4.  In **Reimposta Internet Explorer**fare clic su **Reimposta**e quindi di nuovo su **Reimposta** .  

5.  Attendere che Internet Explorer completi la reimpostazione, quindi fare clic su **OK**.  

6.  Aprire Internet Explorer.  

7.  Aprire Microsoft Security Essentials, fare clic sulla scheda **Aggiornamento** e quindi su **Aggiorna**.  

8.  Se il problema persiste, procedere con il passaggio successivo.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Passaggio 2: impostare Internet Explorer come browser predefinito  

1.  Chiudere tutti i programmi aperti, incluso Internet Explorer.  

2.  Fare clic su **Start** , cercare **inetcpl.cpl**e quindi premere **INVIO**.  

3.  Nella finestra di dialogo **Opzioni Internet** fare clic sulla scheda **Programmi** .  

4.  In **Browser predefinito**fare clic su **Predefinito**.  

5.  Fare clic su **OK**.  

6.  Aprire Windows Defender o Endpoint Protection. Fare clic sulla scheda **Aggiornamento** e quindi su **Aggiorna**.  

7.  Se il problema persiste, procedere con il passaggio successivo.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Passaggio 3: verificare che data e ora siano impostate correttamente nel computer  

1.  Aprire Windows Defender o Endpoint Protection.  

2.  Se il messaggio di errore visualizzato contiene il codice 0x80072f8f, è molto probabile che il problema dipenda dall'impostazione errata della data o dell'ora nel computer.  

3.  Per reimpostare data e ora del computer, eseguire la procedura in [Individuare e cancellare file e collegamenti inutilizzati ed eseguire attività di manutenzione](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Passaggio 4: rinominare la cartella SoftwareDistribution nel computer  

1. Arrestare il servizio Aggiornamenti automatici nel modo seguente:  

    1.  Fare clic su **Start** , cercare **services.msc**e quindi fare clic su **OK**.  

    2.  Fare clic con il pulsante destro del mouse sul servizio **Aggiornamenti automatici**, quindi scegliere **Arresta**.  

    3.  Ridurre a icona lo snap-in Servizi.  

2.  Rinominare la directory **SoftwareDistribution** nel modo seguente:  

    1.  Fare clic su **Start** , cercare  **cmd**e quindi fare clic su **OK**.  

    2.  Digitare **cd %windir%** e quindi premere **INVIO**.  

    3.  Digitare **ren SoftwareDistribution SDTemp**e quindi premere **INVIO**.  

    4.  Digitare **exit**e quindi premere **INVIO**.  

3.  Avviare il servizio Aggiornamenti automatici nel modo seguente:  

    1.  Ingrandire lo snap-in Servizi.  

    2.  Fare clic con il pulsante destro del mouse sul servizio **Aggiornamenti automatici**, quindi scegliere **Avvia**.  

    3.  Chiudere la finestra dello snap-in Servizi.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Passaggio 5: reimpostare il motore di aggiornamento dell'antivirus Microsoft nel computer  

1.  Fare clic su **Start** , cercare  **cmd**, fare clic su **OK**e quindi fare clic con il pulsante destro del mouse su **Prompt dei comandi**e scegliere **Esegui come amministratore**.  

2.  Nella finestra **Prompt dei comandi** digitare i comandi seguenti e premere **INVIO** dopo ogni comando:  

     **Cd\\**  

     **Cd programmi\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **File**  

3.  Riavviare il computer.  

4.  Aprire Windows Defender o  
          Endpoint Protection, fare clic sulla scheda **Aggiorna** e su **Aggiorna**.  

5.  Se il problema persiste, procedere con il passaggio successivo.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Passaggio 6: installare manualmente gli aggiornamenti delle definizioni di virus e spyware  

-   Se si esegue un sistema operativo Windows a 32 bit, scaricare gli aggiornamenti più recenti manualmente all'indirizzo [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342).  

-   Se si esegue un sistema operativo Windows a 64 bit, scaricare gli aggiornamenti più recenti manualmente all'indirizzo [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341).  

-   Fare clic su **Esegui**. Gli aggiornamenti più recenti vengono installati manualmente nel computer.  


### <a name="step-7-contact-support"></a>Passaggio 7: contattare il supporto  

-   Se la procedura non ha consentito di risolvere il problema, contattare il supporto tecnico. Per altre informazioni, vedere il [supporto tecnico](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Avvio del servizio di Windows Defender o Endpoint Protection  
 **Sintomo**  

 Viene visualizzato il messaggio seguente: **Il computer non è monitorato da Windows Defender or Endpoint Protection perché il servizio del programma è stato arrestato. È necessario riavviarlo.** 

 **Soluzione**  

### <a name="step-1-restart-your-computer"></a>Passaggio 1: riavviare il computer.  

-   Chiudere tutte le applicazioni e riavviare il computer.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Passaggio 2: verificare che il servizio "Windows Defender" o "Endpoint Protection" sia impostato su Automatico e che sia avviato.  

1.  Fare clic su **Start** , cercare **services.msc**e quindi premere **INVIO**.  

2.  Cercare **Microsoft Antimalware Service**. Farvi clic con il pulsante destro del mouse e scegliere **Proprietà** o farvi doppio clic per aprire il servizio.  

3.  Verificare che**Tipo di avvio**sia impostato su**Automatico**.  

4.  Fare clic sul pulsante **Avvia** per avviare il servizio. Se il pulsante **Avvia** non è disponibile, fare clic sul pulsante **Arresta** , quindi fare clic sul pulsante **Avvia** per riavviare il servizio.  

5.  Annotare gli eventuali errori che possono verificarsi durante questo processo e inviare una richiesta online includendo le informazioni sull'errore.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Passaggio 3: rimuovere eventuali programmi esistenti per la sicurezza in Internet  

1.  Fare clic su **Start** , cercare **appwiz.cpl**e quindi premere **INVIO**.  

2.  Nell'elenco dei programmi installati disinstallare tutti i programmi per la sicurezza in Internet di terze parti.*  

3.  Riavviare il computer e riprovare a installare Windows Defender o  
          Endpoint Protection.  

> [!NOTE]  
>  Alcune applicazioni per la sicurezza in Internet non vengono disinstallate completamente. È possibile che sia necessario scaricare ed eseguire un'utilità di pulitura per rimuovere completamente l'applicazione di sicurezza precedente.  

> [!CAUTION]  
>  Quando si rimuovono i programmi per la sicurezza in Internet, il computer non sarà protetto. Se si verificano problemi durante l'installazione di   
>       Endpoint Protection dopo aver rimosso i programmi di sicurezza Internet esistenti, contattare l'assistenza di Windows Defender o  
>       Endpoint Protection inviando un caso online. Per altre informazioni, vedere [How to Submit a Case Online](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx) (Come inviare un caso online).  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Passaggio 4: disinstallare/reinstallare Endpoint Protection  

1.  Fare clic su **Start** , cercare **appwiz.cpl**e quindi premere **INVIO**.  

2.  Nell'elenco dei programmi installati fare clic su **Endpoint Protection**e quindi disinstallarlo.  

3.  Se richiesto, riavviare il computer e quindi riprovare a installare Endpoint Protection.  

##  <a name="internet-connection-issues"></a>Problemi di connessione a Internet  
 Per essere certi che il computer riceva gli aggiornamenti più recenti da Windows Update, è necessario essere connessi a Internet.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Passaggio 1: verificare che il computer sia connesso a Internet  

1.  Fare clic su **Start**, cercare **ncpa.cpl**e quindi premere **INVIO**.  

2.  Fare clic con il pulsante destro del mouse sul nome della connessione, quindi scegliere **Stato**.  

3.  Se il computer è connesso, in Windows XP lo stato della connessione sarà indicato come **Connesso**, **Abilitato**o **Autenticazione riuscita** . In Windows Vista e Windows 7 lo stato di **IPv4** verrà visualizzato come **Internet**.  

4.  Se il computer non sembra connesso, fare clic con il pulsante destro del mouse sul nome della connessione, quindi fare clic su **Connetti**, **Abilita**, **Autentica**o **Ripristina**.  

### <a name="step-3-restart-your-computer"></a>Passaggio 3: riavviare il computer  

-   Chiudere eventuali programmi aperti e riavviare il computer.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Passaggio 4: se non è ancora possibile connettersi a Internet, controllare le connessioni  

1.  Se si usa una connessione remota, assicurarsi che il cavo telefonico sia ben collegato alla presa a muro e al modem.  

2.  Se si usa un modem via cavo, assicurarsi che la connessione via cavo al modem e quella tra il modem e il computer siano corrette.  

3.  Se si usa un modem via cavo o un router DSL, assicurarsi che le connessioni al router e al computer siano corrette. Provare a scollegare e spegnere il router e il modem. Attendere qualche minuto, quindi collegare prima il modem, attendere un minuto, collegare il router e infine riavviare il computer.  

##  <a name="detected-threat-cant-be-remediated"></a>Minaccia rilevata che non è possibile correggere  
 Non appena viene rilevata una minaccia potenziale all'interno di un file compresso con estensione zip o all'interno di una condivisione di rete, Windows Defender o Endpoint Protection tenta di metterla in quarantena o di rimuoverla.  

### <a name="remove-or-scan-the-file"></a>Rimuovere o analizzare il file  

-   Se la minaccia viene rilevata in un file zip, individuare il file quindi rimuoverlo o analizzarlo facendovi clic con il pulsante destro del mouse e selezionando **Analizza con Windows Defender** o **Analizza con Endpoint Protection**. Se Windows Defender o Endpoint Protection rileva altre minacce nel file, l'utente viene avvisato in modo da poter scegliere l'azione appropriata.  

-   Se la minaccia viene rilevata in una condivisione di rete, individuare la condivisione di rete e analizzarla facendovi clic con il pulsante destro del mouse e selezionando **Analizza con Windows Defender** o **Analizza con Endpoint Protection**. Se Windows Defender o Endpoint Protection rileva altre minacce nella condivisione di rete, l'utente viene avvisato in modo da poter scegliere l'azione appropriata.  

-   Se non si è certi dell'origine del file, una delle soluzioni migliori è eseguire una scansione completa del computer. L'analisi completa può richiedere un po' di tempo ma consente a Windows Defender o Endpoint Protection di cercare l'origine dell'infezione ed eliminarla.  

##  <a name="install-the-endpoint-protection-client"></a>Installazione del client Endpoint Protection  

> [!NOTE]  
>  Windows Defender viene installato con il sistema operativo nei PC Windows 10.  

 **Sintomi**  

 L'installazione non riesce per motivi sconosciuti oppure viene visualizzato un messaggio di errore con codice di errore, ad esempio 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41, 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E o 0x8007007E.  

 Se nel computer è in esecuzione Windows XP Service Pack 2 (SP2), verrà visualizzato uno o più messaggi di errore seguenti:  

- L'installazione guidata non dispone di un pacchetto di rollup di gestione filtri necessario per completare l'installazione.  

- KB914882 Errore di installazione: impossibile aggiornare i file di Windows XP poiché la lingua installata nel sistema è diversa dalla lingua dell'aggiornamento.  

  **Causa**  

  Non è possibile installare Endpoint Protection in un computer in cui sono in esecuzione altri programmi di sicurezza. Talvolta gli altri programmi di sicurezza non vengono disinstallati completamente, sebbene vengano rimossi. Per installare Endpoint Protection, è necessario usare una versione originale del sistema operativo Windows.  

  **Soluzione**  

> [!IMPORTANT]  
>  Poiché durante la risoluzione di questo problema sarà necessario riavviare il computer, creare un segnalibro per tale pagina aggiungendola ai Preferiti in modo da ritrovare l'argomento più facilmente oppure stamparla come riferimento.  

### <a name="step-1-remove-any-existing-security-programs"></a>Passaggio 1: rimuovere eventuali programmi di sicurezza esistenti  
**Solo Endpoint Protection**

1.  Disinstallare completamente eventuali programmi di sicurezza Internet esistenti.  

2.  Riavviare il computer.  

3.  Installare di nuovo Endpoint Protection. Se il problema non viene risolto, continuare con il passaggio successivo.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Passaggio 2: accertarsi che il servizio Windows Installer sia in esecuzione  

1.  Fare clic su **Start** , cercare **services.msc**e quindi premere **INVIO**.  

2.  Fare clic con il pulsante destro del mouse su **Windows Installer**, quindi scegliere **Avvia**. Se **Avvia** non è disponibile mentre sono disponibili le opzioni **Arresta** e **Riavvia** , significa che il servizio è già avviato.  

3.  Nella pagina **Servizi** scegliere **Esci** dal menu **File**.  

4.  Fare clic sul pulsante **Start** e cercare **Prompt dei comandi**. Fare clic con il pulsante destro del mouse su **Prompt dei comandi**, quindi scegliere **Esegui come amministratore**.  

5.  Digitare **MSIEXEC /REGSERVER**, quindi premere **INVIO**.  

    > [!NOTE]  
    >  Non verrà indicato se il comando è riuscito o meno.  

6.  Installare di nuovo Endpoint Protection. Se il problema non viene risolto, continuare con il passaggio successivo.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Passaggio 3: avviare Windows in modalità Avvio selettivo  

1.  Fare clic su **Start** , cercare **msconfig**e quindi premere **INVIO**.  

2.  Nella scheda **Generale** , fare clic su **Avvio selettivo**e deselezionare la casella di controllo **Carica elementi di avvio** .  

3.  Nella scheda **Servizi** , selezionare la casella di controllo **Nascondi tutti i servizi Microsoft** , quindi deselezionare tutte le caselle di controllo dei servizi rimaste nell'elenco.  

4.  Fare clic su **OK**, quindi su **Riavvia** per riavviare il computer.  

5.  Riprovare a installare Endpoint Protection.  



### <a name="see-also"></a>Vedere anche  
 [Endpoint Protection client frequently asked questions](../../protect/deploy-use/endpoint-protection-client-faq.md) (Domande frequenti relative al client Endpoint Protection)   

 [Endpoint Protection Client Help](../../protect/deploy-use/endpoint-protection-client-help.md) (Guida del client Endpoint Protection)
