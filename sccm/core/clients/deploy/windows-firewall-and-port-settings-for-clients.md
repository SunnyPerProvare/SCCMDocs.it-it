---
title: Impostazioni della porta e del firewall per i client Windows | System Center Configuration Manager
description: Selezionare le impostazioni della porta e di Windows Firewall per i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d74f882e99383ed1f159bcdb24b2c5fe6052c349


---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>Impostazioni di Windows Firewall e delle porte per i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I computer client in System Center Configuration Manager che eseguono Windows Firewall richiedono spesso la configurazione delle eccezioni per consentire la comunicazione con il sito. Le eccezioni da configurare dipendono dalle funzionalità di gestione usate con il client di Configuration Manager.  

 Utilizzare le seguenti sezioni per identificare queste funzionalità di gestione e per ulteriori informazioni su come configurare Windows Firewall per le eccezioni.  

##  <a name="a-namebkmkmodifyingwindowsfirewalla-modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Modifica delle porte e dei programmi consentiti da Windows Firewall  
 Usare la seguente procedura per modificare le porte e i programmi in Windows Firewall per il client di Configuration Manager.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Per modificare le porte e i programmi consentiti da Windows Firewall  

1.  Nel computer che esegue Windows Firewall, aprire il Pannello di controllo.  

2.  Fare clic con il pulsante destro del mouse su **Windows Firewall**, quindi scegliere **Apri**.  

3.  Configurare le eccezioni necessarie, nonché le porte e i programmi personalizzati richiesti.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Porte e programmi richiesti da Configuration Manager  
 Le seguenti funzionalità di Configuration Manager richiedono eccezioni in Windows Firewall:  

### <a name="queries"></a>Query  
 Se la console di Configuration Manager viene eseguita in un computer che esegue Windows Firewall, durante la prima esecuzione delle query si verifica un errore e il sistema operativo visualizza una finestra di dialogo in cui all'utente viene richiesto se desidera sbloccare statview.exe. Se si sblocca statview.exe, le query successive verranno eseguite senza errori. Prima di eseguire una query è inoltre possibile aggiungere manualmente Statview.exe all'elenco di programmi e servizi nella scheda **Eccezioni** di Windows Firewall.  

### <a name="client-push-installation"></a>Installazione push client  
 Per installare il client di Configuration Manager mediante push client, aggiungere le seguenti eccezioni a Windows Firewall:  

-   In uscita e in ingresso: **Condivisione file e stampanti**  

-   In ingresso: **Strumentazione gestione Windows (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Installazione client mediante i criteri di gruppo  
 Per installare il client di Configuration Manager mediante i criteri di gruppo, aggiungere **Condivisione file e stampanti** come eccezione in Windows Firewall.  

### <a name="client-requests"></a>Richieste client  
 Per stabilire la comunicazione tra i computer client e i sistemi del sito di Configuration Manager, aggiungere le seguenti eccezioni a Windows Firewall:  

 In uscita: porta TCP **80** (per la comunicazione HTTP)  

 In uscita: porta TCP **443** (per la comunicazione HTTPS)  

> [!IMPORTANT]  
>  Questi numeri di porta predefiniti possono essere modificati in Configuration Manager. Per altre informazioni, vedere [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md) (Come configurare i numeri di porta di comunicazione client in System Center Configuration Manager). Se queste porte sono state modificate rispetto ai valori predefiniti, è necessario configurare anche le eccezioni corrispondenti in Windows Firewall.  

### <a name="client-notification"></a>Notifica client  
 Per fare in modo che il punto di gestione invii una notifica ai computer client sull'azione da eseguire quando un utente amministratore seleziona un'azione client nella console di Configuration Manager, ad esempio scaricare criteri computer o avviare una scansione malware, aggiungere la seguente eccezione a Windows Firewall:  

 In uscita: porta TCP **10123**  

 Se la comunicazione non riesce, Configuration Manager esegue automaticamente il fallback alla porta HTTP o HTTPS esistente per la comunicazione tra client e punto di gestione:  

 In uscita: porta TCP **80** (per la comunicazione HTTP)  

 In uscita: porta TCP **443** (per la comunicazione HTTPS)  

> [!IMPORTANT]  
>  Questi numeri di porta predefiniti possono essere modificati in Configuration Manager. Per altre informazioni, vedere [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md) (Come configurare i numeri di porta di comunicazione client in System Center Configuration Manager). Se queste porte sono state modificate rispetto ai valori predefiniti, è necessario configurare anche le eccezioni corrispondenti in Windows Firewall.  

### <a name="remote-control"></a>Controllo remoto  
 Per usare il controllo remoto di Configuration Manager, consentire la seguente porta:  

-   In ingresso: porta TCP**2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Assistenza remota e Desktop remoto  
 Per avviare Assistenza remota dalla console di Configuration Manager, aggiungere il programma personalizzato **Helpsvc.exe** e la porta in entrata TCP personalizzata **135** all'elenco di programmi e servizi consentiti in Windows Firewall nel computer client. È inoltre necessario consentire **Assistenza remota** e **Desktop remoto**. Se Assistenza remota viene avviata dal computer client, Windows Firewall consente e configura automaticamente **Assistenza remota** e **Desktop remoto**.  

### <a name="wake-up-proxy"></a>Proxy di riattivazione  
 Se si attiva l'impostazione client Proxy di riattivazione, il nuovo servizio Proxy di riattivazione di Configuration Manager utilizza un protocollo peer-to-peer per verificare che gli altri computer della subnet siano attivi e riattivarli se necessario. Questa comunicazione utilizza le seguenti porte:  

 In uscita: porta UDP **25536**  

 In uscita: porta UDP **9**  

 Questi numeri di porta predefiniti possono essere modificati in Configuration Manager usando le impostazioni client **Risparmio energia**: **Numero di porta del proxy di riattivazione (UDP)** e **Numero di porta di riattivazione LAN (UDP)**. Se si specifica l'impostazione client **Risparmio energia**: **Eccezione di Windows Firewall per il proxy di riattivazione** , queste porte vengono configurate automaticamente in Windows Firewall per i client. Tuttavia, se i client eseguono un firewall diverso, è necessario configurare manualmente le eccezioni per i numeri di porta.  

 Oltre a queste porte, il proxy di riattivazione utilizza i messaggi di richiesta echo di Internet Control Message Protocol (ICMP) da un computer client all'altro. Questo tipo di comunicazione viene usata per verificare se l'altro computer è attivo nella rete. ICMP viene talvolta indicato come comandi ping TCP/IP.  

 Per altre informazioni sul proxy di riattivazione, vedere [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md) (Pianificare la riattivazione dei client in System Center Configuration Manager).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Visualizzatore eventi di Windows, Monitoraggio prestazioni di Windows e Diagnostica Windows  
 Per accedere a Visualizzatore eventi di Windows, Monitoraggio prestazioni di Windows e Diagnostica Windows dalla console di Configuration Manager, attivare **Condivisione file e stampanti** come eccezione in Windows Firewall.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Porte utilizzate durante la distribuzione client di Configuration Manager  
 Nelle seguenti tabelle sono elencate le porte utilizzate durante il processo di installazione client.  

> [!IMPORTANT]  
>  Se tra i server di sistema del sito e il computer client è presente un firewall, verificare che il firewall consenta il traffico per le porte richieste per il metodo di installazione client selezionato. I firewall, ad esempio, spesso impediscono l'installazione push client poiché bloccano SMB (Server Message Block) e RPC (Remote Procedure Call). In questo scenario, utilizzare un metodo di installazione client diverso, come l'installazione manuale (eseguendo CCMSetup.exe) o l'installazione client basata sui criteri di gruppo. Questi metodi di installazione client alternativi non richiedono SMB o RPC.  

 Per informazioni sulla configurazione di Windows Firewall nel computer client, vedere [Modifica delle porte e dei programmi consentiti da Windows Firewall](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Porte utilizzate per tutti i metodi di installazione  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal computer client a un punto di stato di fallback, in caso di assegnazione di un punto di stato di fallback al client.|--|80 (vedere la nota 1, **Porta alternativa disponibile**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Porte utilizzate con l'installazione push client  
 Oltre alle porte elencate nella tabella seguente, l'installazione push client utilizza i messaggi di richiesta echo di Internet Control Message Protocol (ICMP) dal server del sito al computer client per verificare che il computer client sia disponibile nella rete. ICMP viene talvolta indicato come comandi ping TCP/IP. ICMP non dispone di un numero di protocollo UDP o TCP e pertanto non è elencato nella seguente tabella. Eventuali altri dispositivi di rete, ad esempio i firewall, devono tuttavia consentire il traffico ICMP per una corretta installazione push client.  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) tra il server del sito e il computer client.|--|445|  
|Agente mapping endpoint RPC tra il server del sito e il computer client.|135|135|  
|Porte dinamiche RPC tra il server del sito e il computer client.|--|DINAMICHE|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTP.|--|80 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Protocollo HTTPS (Secure Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTPS.|--|443 (vedere la nota 1, **Porta alternativa disponibile**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Porte utilizzate con l'installazione basata sul punto di aggiornamento software  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal computer client al punto di aggiornamento software.|--|80 o 8530 (vedere la nota 2, **Windows Server Update Services**)|  
|Protocollo HTTPS (Secure Hypertext Transfer Protocol) dal computer client al punto di aggiornamento software.|--|443 o 8531 (vedere la nota 2, **Windows Server Update Services**)|  
|Server Message Block (SMB) tra il server di origine e il computer client quando si specifica la proprietà della riga di comando CCMSetup **/source:&lt;percorso\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Porte utilizzate con l'installazione basata sui criteri di gruppo  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTP.|--|80 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Protocollo HTTPS (Secure Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTPS.|--|443 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Server Message Block (SMB) tra il server di origine e il computer client quando si specifica la proprietà della riga di comando CCMSetup **/source:&lt;percorso\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Porte utilizzate con l'installazione manuale e l'installazione basata sugli script di accesso  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) tra il computer client e una condivisione di rete da cui si esegue CCMSetup.exe.<br /><br /> Quando si installa Configuration Manager, i file di origine dell'installazione client vengono copiati e automaticamente condivisi dalla cartella *&lt;PercorsoInstallazione\>*\Client nei punti di gestione. È tuttavia possibile copiare i file e creare una nuova condivisione in qualsiasi computer della rete. In alternativa, è possibile eliminare il traffico di rete eseguendo CCMSetup.exe in locale, utilizzando ad esempio supporti rimovibili.|--|445|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTP e quando non viene specificata la proprietà della riga di comando CCMSetup **/source:&lt;percorso\>**.|--|80 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Protocollo HTTPS (Secure Hypertext Transfer Protocol) dal computer client a un punto di gestione in caso di connessione tramite HTTPS e quando non viene specificata la proprietà della riga di comando CCMSetup **/source:&lt;percorso\>**.|--|443 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Server Message Block (SMB) tra il server di origine e il computer client quando si specifica la proprietà della riga di comando CCMSetup **/source:&lt;percorso\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Porte utilizzate con l'installazione basata sul punto di distribuzione software  

|Descrizione|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) tra il punto di distribuzione e il computer client.|--|445|  
|Protocollo HTTP (Hypertext Transfer Protocol) dal client a un punto di distribuzione in caso di connessione tramite HTTP.|--|80 (vedere la nota 1, **Porta alternativa disponibile**)|  
|Protocollo HTTPS (Secure Hypertext Transfer Protocol) dal client a un punto di distribuzione in caso di connessione tramite HTTPS.|--|443 (vedere la nota 1, **Porta alternativa disponibile**)|  

## <a name="notes"></a>Note  
 **1 Porta alternativa disponibile** In Configuration Manager è possibile definire una porta alternativa per questo valore. Se è stata definita una porta personalizzata, sostituirla durante la definizione delle informazioni sul filtro IP per i criteri IPsec o per la configurazione dei firewall.  

 **2 Windows Server Update Services** È possibile installare Windows Server Update Services (WSUS) sia nel sito Web predefinito (porta 80) che in un sito Web personalizzato (porta 8530).  

 Al termine dell'installazione, è possibile modificare la porta. Non è necessario usare lo stesso numero di porta per tutta la gerarchia del sito.  

 Se la porta HTTP è la porta 80, la porta HTTPS deve essere la porta 443.  

 Se la porta HTTP è diversa, la porta HTTPS deve essere maggiore di 1. Ad esempio, 8530 e 8531.



<!--HONumber=Nov16_HO1-->

