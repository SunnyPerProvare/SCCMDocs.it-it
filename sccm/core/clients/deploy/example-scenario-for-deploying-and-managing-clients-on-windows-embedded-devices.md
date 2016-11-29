---
title: 'Scenario di esempio: distribuire i client con Windows Embedded | System Center Configuration Manager'
description: Scenario di esempio per la distribuzione e la gestione dei client di System Center Configuration Manager in dispositivi con Windows Embedded.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dd97ae9afb2d0ecfc33266267a65f3c3f6d1dd29


---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Scenario di esempio per la distribuzione e la gestione dei client di System Center Configuration Manager in dispositivi con Windows Embedded

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo scenario illustra come è possibile gestire i dispositivi con Windows Embedded che hanno i filtri di scrittura abilitati usando System Center Configuration Manager. Se i dispositivi integrati non supportano i filtri di scrittura, funzionano come client standard di Configuration Manager e non è necessario eseguire i passaggi descritti in questo scenario necessari invece per gestire i filtri di scrittura.  

 Coho Vineyard & Winery sta per aprire un centro visite e vorrebbe installare dei chioschi con Windows Embedded per trasmettere delle presentazioni interattive. L'edificio per il nuovo centro visite non si trova vicino al dipartimento IT, per cui è importante che i chioschi possano essere gestiti in remoto. Oltre a installare il software che trasmetterà le presentazioni interattive, questi dispositivi dovranno eseguire un software di protezione antimalware aggiornato per adempiere alle politica di sicurezza dell'azienda. Per avere la certezza che le presentazioni interattive siano sempre disponibili ai visitatori, i chioschi devono trasmettere 7 giorni a settimana e non si devono verificare tempi di inattività durante gli orari di apertura.  

 Coho Vineyard & Winery esegue già Configuration Manager per gestire i dispositivi di rete. Configuration Manager è configurato per eseguire Endpoint Protection e per installare gli aggiornamenti di software e applicazioni. Tuttavia, poiché il team IT non ha mai gestito dispositivi con Windows Embedded, Jane, amministratore di Configuration Manager, esegue un progetto pilota per gestire due chioschi multimediali che si trovano nella sala d'attesa della reception aziendale. Se il progetto pilota esegue con successo la gestione di questi dispositivi, l'ordine di acquisto per i chioschi del centro visite potrà essere approvato.  

 Per gestire questi dispositivi con Windows Embedded che hanno i filtri di scrittura abilitati, Jane esegue i passaggi seguenti per installare il client di Configuration Manager, proteggere il client usando Endpoint Protection e installare il software per la presentazione interattiva.  

1.  Jane legge in che modo i dispositivi con Windows Embedded usano i filtri di scrittura e come Configuration Manager può semplificare questa operazione disabilitando e riabilitando automaticamente i filtri di scrittura per salvare in modo permanente un'installazione software.  

     Per altre informazioni, vedere [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md) (Pianificazione della distribuzione client a dispositivi con Windows Embedded in System Center Configuration Manager).  

2.  Prima di installare il client di Configuration Manager, Jane crea una nuova raccolta dispositivi basata su query per i dispositivi con Windows Embedded. Poiché l'azienda usa formati di denominazione standard per identificare i computer, Jane può identificare i dispositivi con Windows Embedded con le prime sei lettere del nome del computer: **WEMDVC**. Usa la seguente query WQL per creare questa raccolta: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     Questa raccolta consente di gestire i dispositivi con Windows Embedded con diverse opzioni di configurazione da altri dispositivi. Utilizzerà questa raccolta per controllare i riavvii, per distribuire Endpoint Protection con le impostazioni client e per distribuire l'applicazione per le presentazioni interattive.  

     Vedere [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md) (Come creare raccolte in System Center Configuration Manager).  

3.  Jane configura la raccolta per una finestra di manutenzione per assicurarsi che i riavvii richiesti per l'installazione dell'applicazione per le presentazioni ed eventuali aggiornamenti non si verifichino durante gli orari di apertura del centro visite. Gli orari di apertura saranno dalle 9:00 alle 18:00, da lunedì a domenica. Configura la finestra di manutenzione per ogni giorno, dalle 18:30 alle 06:00.  

4.  Per altre informazioni, vedere [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md) (Come usare le finestre di manutenzione in Configuration Manager).  

5.  Jane configura quindi un'impostazione client di dispositivi personalizzata per installare il client di Endpoint Protection selezionando **Sì** per le seguenti impostazioni, quindi distribuisce questa impostazione client personalizzata nella raccolta dispositivi con Windows Embedded:  

    -   **Installare il client Endpoint Protection nei computer client**  

    -   **Per i dispositivi con Windows Embedded con filtri di scrittura, confermare l'installazione del client di Endpoint Protection (richiesto riavvio)**  

    -   **Consentire l'installazione del client di Endpoint Protection e i riavvii al di fuori delle finestre di manutenzione**  

     Quando viene installato il client di Configuration Manager, queste impostazioni installano il client di Endpoint Protection, garantendo cosi che sarà salvato in modo permanente nel sistema operativo come parte dell'installazione e non solo scritto sull'overlay. Le politiche di sicurezza dell'azienda richiedono che il software antimalware sia sempre installato e Jane non vuole correre il rischio che i chioschi non siano protetti nel breve periodo di tempo del riavvio.  

    > [!NOTE]  
    >  I riavvii richiesti per installare il client di Endpoint Protection avvengono solo una volta, che avviene durante l'installazione dei dispositivi e prima che il centro visite sia operativo. Diversamente dalla distribuzione periodica degli aggiornamenti di definizioni per applicazioni o software, il client di Endpoint Protection sarà installato nuovamente nello stesso dispositivo quando l'azienda eseguirà l'aggiornamento alla nuova versione di Configuration Manager.  

     Per altre informazioni, vedere [Configuring Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md) (Configurazione di Endpoint Protection in System Center Configuration Manager).  

6.  Dopo aver definito le impostazioni di configurazione per il client, Jane prepara l'installazione dei client di Configuration Manager. Prima di installare i client, deve disabilitare manualmente il filtro di scrittura sui dispositivi con Windows Embedded. Legge la documentazione OEM che accompagna i chioschi e segue le istruzioni per disabilitare i filtri di scrittura.  

     Jane rinomina il dispositivo per usare il formato di denominazione standard dell'azienda, quindi installa il client manualmente eseguendo CCMSetup con il comando seguente da un'unità mappata che contiene i file di origine client: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     Questo comando installa il client, assegna il client al punto di gestione che ha l'intranet FQDN di **mpserver.cohovineyardandwinery.com**e assegna il client al sito primario denominato **CO1**.  

     Jane sa che occorre sempre un po' di tempo per l'installazione dei client e per reinviare il loro stato al sito. Quindi aspetta un po' prima di confermare l'installazione corretta dei client, la loro assegnazione al sito e la loro visualizzazione come client nella raccolta da lei creata per i dispositivi con Windows Embedded.  

     Per essere più sicura, nei dispositivi con Windows Embedded controlla le proprietà di Configuration Manager nel Pannello di controllo e le confronta con i computer Windows standard che sono gestiti dal sito. Ad esempio, nella scheda **Componenti** , l' **Agente di inventario hardware** visualizza **Abilitato**e nella scheda **Azioni** , sono disponibili 11 azioni che includono **Ciclo di valutazione distribuzione applicazione** e **Ciclo di recupero dati di rilevamento**.  

     Sicura che i client sono stati correttamente installati, assegnati e avendo ricevuto i criteri client dal punto di gestione, Jane abilita manualmente i filtri di scrittura seguendo le istruzioni OEM.  

     Per altre informazioni, vedere:  

    -   [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) (Come distribuire i client nei computer Windows in System Center Configuration Manager)  

    -   [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md) (Come assegnare i client a un sito in System Center Configuration Manager)  

7.  Dopo aver installato il client di Configuration Manager nei dispositivi con Windows Embedded, Jane conferma di poterli gestire nello stesso modo in cui gestisce i client Windows standard. Dalla console di Configuration Manager può ad esempio gestire i client in remoto usando il controllo remoto, avviare criteri client e visualizzare le proprietà client e l'inventario hardware.  

     Questi dispositivi sono associati a un dominio di Active Directory. Jane non deve pertanto approvarli manualmente come client attendibili, ma ne conferma l'approvazione dalla console di Configuration Manager.  

     Per altre informazioni, vedere [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  Per installare il software per le presentazioni interattive, Jane esegue la **Distribuzione guidata del software** e configura un'applicazione richiesta. Nella pagina **Esperienza utente** della procedura guidata, nella sezione **Gestione filtri di scrittura per dispositivi con Windows Embedded** , accetta l'opzione predefinita che seleziona **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)**.  

     Jane mantiene questa opzione predefinita per i filtri di scrittura per assicurarsi che l'applicazione rimanga permanente dopo un riavvio e sia quindi sempre disponibile per i visitatori che utilizzano i chioschi. La finestra di manutenzione quotidiana fornisce un periodo di tempo sicuro durante si possono effettuare i riavvii per l'installazione ed eventuali aggiornamenti.  

     Jane distribuisce l'applicazione nella raccolta dispositivi con Windows Embedded.  

     Per altre informazioni, vedere [How to deploy applications with System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md) (Come distribuire le applicazioni con System Center Configuration Manager).  

9. Per configurare gli aggiornamenti delle definizioni per Endpoint Protection, Jane utilizza gli aggiornamenti software ed esegue la Creazione guidata delle regole di distribuzione automatica. Seleziona il modello **Aggiornamenti delle definizioni** per il popolamento preliminare della procedura guidata con le impostazioni appropriate per Endpoint Protection.  

     Queste impostazioni includono i seguenti elementi nella pagina **Esperienza utente** della procedura guidata:  

    -   **Comportamento scadenza**: la casella di controllo **Installazione software** non è selezionata.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** non è selezionata.  

     Jane mantiene queste impostazioni predefinite. Insieme, queste due opzioni con questa configurazione consentono l'installazione di tutte le definizioni di aggiornamento software per Endpoint Protection nella sovrapposizione durante il giorno e nessuna attesa per l'installazione e l'invio durante la finestra di manutenzione. Questa configurazione soddisfa al meglio i criteri di sicurezza dell'azienda per i computer con protezione antimalware aggiornata.  

    > [!NOTE]  
    >  A differenza delle installazioni software per applicazioni, le definizioni di aggiornamento software per Endpoint Protection possono verificarsi molto spesso, anche più volte al giorno. Sono spesso file di piccole dimensioni. Per questi tipi di distribuzione relativi alla sicurezza, può essere spesso utile installare sempre nella sovrapposizione piuttosto che aspettare fino alla finestra di manutenzione. Il client di Configuration Manager reinstallerà rapidamente gli aggiornamenti delle definizioni software se il dispositivo si riavvia, perché questa azione avvia un controllo di valutazione e non aspetta fino alla valutazione pianificata successiva.  

     Jane seleziona la raccolta dispositivi con Windows Embedded per la regola di distribuzione automatica.  

     Per ulteriori informazioni, vedere  
                  Passaggio 3: Configure Configuration Manager Software Updates to Deliver Definition Updates to Client Computers (Configurare gli aggiornamenti software di Configuration Manager per inviare gli aggiornamenti delle definizioni ai computer client) in [Configuring Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md) (Configurazione di Endpoint Protection in System Center Configuration Manager)  

10. Jane decide di configurare un'attività di manutenzione che invia periodicamente tutte le modifiche nella sovrapposizione. Questa attività serve per supportare le definizioni di aggiornamento software e per ridurre il numero di aggiornamenti che si sono accumulati e che devono essere installati di nuovo ogni volta che il dispositivo si riavvia. Nella sua esperienza, in questo modo i programmi antimalware funzionano in modo più efficiente.  

    > [!NOTE]  
    >  Queste definizioni di aggiornamento software verrebbero automaticamente inviate al'immagine se i dispositivi con Windows Embedded eseguissero un'altra attività di gestione che supportasse l'invio delle modifiche. Ad esempio, anche l'installazione di una nuova versione del software per le presentazioni interattivi invierebbe le modifiche per le definizioni di aggiornamento software. In alternativa, anche l'installazione degli aggiornamenti software standard in ogni mese di installazione durante la finestra di manutenzione potrebbe inviare le modifiche per le definizioni di aggiornamento software. Tuttavia, in questo scenario in cui non vengono eseguiti gli aggiornamenti software standard e il software per le presentazioni interattive probabilmente non viene aggiornato molto spesso, potrebbe passare dei mesi prima che gli aggiornamenti delle definizioni software vengano inviati automaticamente all'immagine.  

     Jane crea prima una sequenza attività personalizzata che non presenta impostazioni diverse dal nome. Esegue la Creazione guidata della sequenza attività:  

    1.  Nella pagina **Crea una nuova sequenza attività** , seleziona **Crea una nuova sequenza attività personalizzata**, quindi fa clic su **Avanti**.  

    2.  Nella pagina **Informazioni sequenza di attività** immette **Maintenance task to commit changes on embedded devices** come nome della sequenza di attività e quindi fa clic su **Avanti**.  

    3.  Nella pagina **Riepilogo** , seleziona **Avanti**e completa la procedura guidata.  

     Jane quindi distribuisce questa sequenza attività personalizzata nella raccolta dispositivi con Windows Embedded e configura la pianificazione in modo che venga eseguita ogni mese. Come parte delle impostazioni di distribuzione, seleziona la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** per rendere permanenti le modifiche dopo un riavvio. Per configurare questa distribuzione, seleziona la sequenza attività personalizzata che ha appena creato, quindi nella scheda **Home** del gruppo **Distribuzione** , fa clic su **Distribuisci** per avviare la Distribuzione guidata del software:  

    1.  Nella pagina **Generale** , seleziona la raccolta dispositivi con Windows Embedded, quindi fa clic su **Avanti**.  

    2.  Nella pagina **Impostazioni distribuzione** , seleziona lo **Scopo** di **Richiesto**, quindi fa clic su **Avanti**.  

    3.  Nella pagina **Pianificazione** , fa clic su **Nuovo** per indicare una pianificazione settimanale durante la finestra di manutenzione, quindi fa clic su **Avanti**.  

    4.  Completa la procedura guidata senza ulteriori modifiche.  

     Per ulteriori informazioni, vedere  
                  [Manage task sequences to automate tasks in System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md) (Gestire le sequenze di attività per automatizzare le attività in System Center Configuration Manager).  

11. Per l'esecuzione automatica dei chioschi, Raffaella scrive uno script per configurare i dispositivi per le seguenti impostazioni:  

    -   Accedere automaticamente, utilizzando un account guest senza password.  

    -   Eseguire automaticamente il software per la presentazione interattiva all'avvio.  

     Raffaella utilizza pacchetti e programmi per distribuire questo script nella raccolta di dispositivi Windows Embedded. Quando esegue la Distribuzione guidata del software, Raffaella seleziona nuovamente la casella di controllo **Invia modifiche alla scadenza o in una finestra di manutenzione (riavvio necessario)** per rendere permanenti le modifiche dopo un riavvio.  

     Per altre informazioni, vedere [Pacchetti e programmi in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Il mattino seguente, Raffaella controlla i dispositivi Windows Embedded. Conferma quanto segue:  

    -   Il chiosco viene automaticamente connesso utilizzando l'account guest.  

    -   Il software di presentazione interattiva è in esecuzione.  

    -   Il client Endpoint Protection è installato e dispone delle definizioni di aggiornamento software più recenti.  

    -   Il dispositivo è stato riavviato durante la finestra di manutenzione.  

     Per altre informazioni, vedere:  

    -   [How to monitor Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md) (Come monitorare Endpoint Protection in System Center Configuration Manager).  

    -   [Monitor applications with System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console) (Monitorare le applicazioni con System Center Configuration Manager)  

13. Raffaella monitora i chioschi e ne segnala la corretta gestione al responsabile. Di conseguenza, vengono ordinati 20 chioschi per il centro visite.  

     Per evitare di dover installare manualmente il client di Configuration Manager, che necessita la disabilitazione manuale e quindi la riabilitazione dei filtri di scrittura, Jane verifica che l'ordine includa un'immagine personalizzata comprensiva già dell'installazione e dell'assegnazione del sito del client di Configuration Manager. Inoltre, i dispositivi vengono denominati in base al formato dei nomi aziendali.  

     I chioschi vengono consegnati al centro visitate una settimana prima dell'apertura. Durante questo periodo, i chioschi vengono connessi alla rete, tutta la relativa gestione dei dispositivi è automatica e non sono necessari amministratori locali. Raffaella conferma che i chioschi funzionano come richiesto:  

    -   I client nei chioschi completano l'assegnazione del sito e scaricano la chiave radice attendibile da Servizi di dominio Active Directory.  

    -   I client nei chioschi vengono automaticamente aggiunti alla raccolta di dispositivi Windows Embedded e vengono configurati con la finestra di manutenzione.  

    -   Il client Endpoint Protection è installato e dispone delle definizioni di aggiornamento software più recenti per la protezione antimalware.  

    -   Il software di presentazione interattiva è installato e viene eseguito automaticamente, pronto per i visitatori.  

14. Al termine dell'installazione iniziale eventuali riavvii che potrebbero essere necessari per gli aggiornamenti si verificano solo quando il centro visite è chiuso.  



<!--HONumber=Nov16_HO1-->


