---
title: Come gestire Windows Device Guard
titleSuffix: Configuration Manager
description: Informazioni su come usare System Center Configuration Manager per gestire Windows Device Guard.
ms.custom: na
ms.date: 10/20/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 8d84d0d65db7668baa7be9bbf0ad1df869b37919
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Gestione di Device Guard con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduzione
Device Guard è un gruppo di funzionalità di Windows 10 progettate per proteggere i PC dal malware e da altro software non attendibile. Impedisce l'esecuzione di codice dannoso, garantendo che solo il codice approvato e conosciuto possa essere eseguito.

Device Guard comprende funzionalità basate sia su software che su hardware. L'integrità del codice configurabile è un livello di protezione basato su software che applica un elenco esplicito di programmi software che possono essere eseguiti in un PC. Autonomamente, l'integrità del codice configurabile non ha alcun prerequisito hardware o firmware. I criteri di controllo delle applicazioni di Windows Defender distribuiti con Configuration Manager abilitano un criterio di integrità del codice configurabile nei PC inclusi in raccolte di destinazione che soddisfano i requisiti minimi relativi a SKU e versione di Windows descritti in questo articolo. Facoltativamente, è possibile abilitare la protezione basata su hypervisor dei criteri di integrità del codice distribuiti con Configuration Manager usando Criteri di gruppo su hardware idoneo.

Per altre informazioni su Device Guard, vedere [Guida alla distribuzione di Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Uso di Device Guard con Configuration Manager

È possibile usare Configuration Manager per distribuire un criterio di controllo delle applicazioni di Windows Defender che consente di configurare la modalità di esecuzione di Device Guard nei PC di una raccolta. 

È possibile configurare una delle modalità seguenti:

1.  **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
2.  **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.

>[!TIP]
>In questa versione di Configuration Manager, Device Guard è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Che cosa viene eseguito quando si distribuisce un criterio di controllo delle applicazioni di Windows Defender?

Windows Device Guard consente di controllare rigorosamente cosa può essere eseguito sui PC gestiti dall'utente. Questa funzione può essere utile per i PC nei reparti ad alta sicurezza, in cui è fondamentale che impedire l'esecuzione di software indesiderato.

Quando si distribuisce un criterio, in genere, è possibile eseguire i file eseguibili seguenti:

- Componenti del sistema operativo Windows
- Driver di Hardware Dev Center (con firme Windows Hardware Quality Labs)
- App di Windows Store
- Client di Configuration Manager 
- Tutto il software distribuito tramite Configuration Manager e installato nei PC dopo l'elaborazione del criterio di controllo delle applicazioni di Windows Defender. 
- Aggiornamenti ai componenti di Windows da:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Questi elementi non includono software *non* incorporato in Windows che venga aggiornato automaticamente da Internet o da aggiornamenti software di terze parti e che sia stato installato usando uno qualsiasi dei meccanismi di aggiornamento indicati in precedenza o da Internet. Possono essere eseguite solo modifiche software distribuite tramite il client di Configuration Manager.

## <a name="before-you-start"></a>Prima di iniziare

Prima di configurare o distribuire criteri di controllo delle applicazioni di Windows Defender, leggere le informazioni seguenti:

- La gestione di Device Guard è una funzionalità di versione non definitiva per Configuration Manager ed è soggetta a modifiche.
- Per usare Device Guard con Configuration Manager, i PC gestiti devono eseguire Windows 10 Enterprise versione 1703 o successiva.
- Dopo la corretta elaborazione di un criterio in un PC client, Configuration Manager viene configurato come programma di installazione gestito in tale client e il software distribuito con SCCM dopo l'elaborazione del criterio viene considerato automaticamente attendibile. Il software installato da Configuration Manager prima dell'elaborazione del criterio di controllo delle applicazioni di Windows Defender non è considerato automaticamente attendibile.
- Perché sia possibile elaborare correttamente un criterio di controllo delle applicazioni di Windows Defender, i PC client devono essere connessi al rispettivo controller di dominio.
- In base alla pianificazione, configurabile durante la distribuzione, la valutazione della conformità predefinita per i criteri di controllo delle applicazioni di Windows Defender avviene ogni giorno. Se si rilevano problemi nell'elaborazione dei criteri, può essere utile configurare una pianificazione di valutazione di conformità più breve, ad esempio ogni ora. Questa pianificazione determina la frequenza con cui i client riprovano a elaborare un criterio di controllo delle applicazioni di Windows Defender in caso di errore.
- Indipendentemente dalla modalità di applicazione selezionata, quando si distribuisce un criterio di controllo delle applicazioni di Windows Defender, i PC client non possono eseguire applicazioni HTML con estensione hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Come creare criteri di controllo delle applicazioni di Windows Defender
1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.
2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Windows Defender Application Control policies** (Criteri di controllo delle applicazioni di Windows Defender).
3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Create Windows Defender Application Control policy** (Crea criteri di controllo delle applicazioni di Windows Defender).
4.  Nella pagina **Generale** della procedura guidata **Create Windows Defender Application Control policy** (Crea criteri di controllo delle applicazioni di Windows Defender) specificare le informazioni seguenti:
    - **Nome**: immettere un nome univoco per il criterio di controllo delle applicazioni di Windows Defender. 
    - **Descrizione**: facoltativamente, immettere una descrizione per il criterio che consenta di identificarlo nella console di Configuration Manager.
    - **Modalità di imposizione**: scegliere uno dei seguenti metodi di imposizione di Device Guard sul PC client.
        - **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
        - **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.
5.  Nella scheda **Inclusioni** della procedura guidata **Create Windows Defender Application Control policy** (Crea criteri di controllo delle applicazioni di Windows Defender) fare clic su **Aggiungi** se si vuole specificare come attendibili cartelle o file specifici nei PC. 
6.  Nella finestra di dialogo **Aggiungi file o cartella attendibile** specificare le informazioni sul file o sulla cartella che si desidera considerare attendibile. È possibile specificare un percorso di file o cartella locale oppure connettersi a un dispositivo remoto per cui si dispone dell'autorizzazione per connettersi e specificare un percorso di file o cartella nel dispositivo.
Se si configura l'attendibilità per cartelle e file specifici in un criterio di controllo delle applicazioni di Windows Defender, è possibile:
    - Risolvere i problemi relativi ai comportamenti del programma di installazione gestito
    - Rendere attendibili le app line-of-business che non possono essere distribuite con Configuration Manager
    - Rendere attendibili le app incluse in un'immagine di distribuzione del sistema operativo. 
7.  Fare clic su **Avanti** e completare la procedura guidata.

>[!IMPORTANT]
>L'inclusione di file o cartelle attendibili è supportata solo nei PC client che eseguono la versione 1706 o versioni successive del client di Configuration Manager. Se si aggiungono regole di inclusione in un criterio di controllo delle applicazioni di Windows Defender e il criterio viene quindi distribuito in un PC client che esegue una versione precedente del client di Configuration Manager, il criterio non verrà applicato. Per risolvere il problema, aggiornare questi client precedenti. I criteri che non comprendono regole di inclusione possono comunque essere applicati alle versioni precedenti del client di Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Come distribuire criteri di controllo delle applicazioni di Windows Defender
1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.
2.  Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection** e quindi fare clic su **Windows Defender Application Control policies** (Criteri di controllo delle applicazioni di Windows Defender).
3.  Nell'elenco dei profili selezionare il profilo da distribuire e fare clic su **Distribuisci** nel gruppo **Distribuzione** della scheda **Home**.
4.  Nella finestra di dialogo **Distribuisci il criterio di controllo delle applicazioni di Windows Defender** selezionare la raccolta in cui si vuole distribuire il criterio, quindi configurare una pianificazione per la valutazione del criterio da parte dei client. Selezionare infine se i client possono valutare i criteri al di fuori delle finestre di manutenzione configurate.
5.  Al termine, fare clic su **OK** per distribuire il criterio. 

### <a name="restarting-the-device-after-deploying-the-policy"></a>Riavvio del dispositivo dopo la distribuzione del criterio

Dopo l'elaborazione del criterio in un PC client, viene pianificato un riavvio nel client in base a quanto specificato in **Impostazioni client** per **Riavvio del computer**. Per applicare i criteri non è necessario riavviare il computer, ma questo è il comportamento predefinito. Se si vuole disattivare il riavvio, seguire questa procedura:

1. Aprire la procedura guidata **Create Windows Defender Application Control Policy** (Crea criteri di controllo delle applicazioni di Windows Defender).
2. Nella pagina **Generale** deselezionare la casella di controllo **Imponi un riavvio dei dispositivi in modo che questo criterio possa essere applicato per tutti i processi**.
3. Fare clic su **Avanti** fino al termine della procedura guidata.



## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Come monitorare i criteri di controllo delle applicazioni di Windows Defender

Usare le informazioni contenute nell'argomento [Monitorare le impostazioni di conformità](/sccm/compliance/deploy-use/monitor-compliance-settings) per controllare che il criterio distribuito sia stato applicato correttamente a tutti i PC.

Per monitorare l'elaborazione di un criterio di controllo delle applicazioni di Windows Defender, usare il file di log seguente nei PC client:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Per verificare che il software specifico sia bloccato o controllato, vedere i registri eventi seguenti del client locale:

1.  Per il blocco e controllo di file eseguibili, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **Integrità del codice** > **Operativo**.
2.  Per il blocco e il controllo di Windows Installer e dei file di script, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

## <a name="automatically-let-software-run-if-it-is-trusted-by-intelligent-security-graph"></a>Impostare l'esecuzione automatica del software se è considerato attendibile da Intelligent Security Graph

È quindi possibile consentire che i dispositivi bloccati eseguano il software considerato attendibile in base a quanto determinato da Microsoft Intelligent Security Graph. Intelligent Security Graph include [Windows Defender SmartScreen](https://docs.microsoft.com/windows/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) e altri servizi Microsoft. Perché il software possa essere considerato attendibile, i dispositivi devono eseguire Windows Defender SmartScreen.

1. Aprire la procedura guidata **Create Windows Defender Application Control Policy** (Crea criteri di controllo delle applicazioni di Windows Defender).
2. Nella pagina **Inclusioni** selezionare la casella **Autorizza il software ritenuto attendibile da Intelligent Security Graph**.
3. Nella casella File o cartelle attendibili aggiungere i file e le cartelle che devono essere considerati attendibili.
4. Fare clic su **Avanti** fino al termine della procedura guidata.



## <a name="security-and-privacy-information-for-device-guard"></a>Informazioni sulla sicurezza e sulla privacy di Device Guard

- In questa versione non definitiva non distribuire criteri di controllo delle applicazioni di Windows Defender con la modalità di applicazione **Solo controllo** in un ambiente di produzione. Questa modalità consente di testare la funzionalità solo in un ambiente di prova.
- I dispositivi in cui è stato distribuito un criterio in modalità **Solo controllo** o **Imposizione abilitata** ma che non sono ancora stati riavviati per rendere effettivo il criterio sono vulnerabili nei confronti di eventuale software non attendibile installato.
In questo caso, l'esecuzione del software potrebbe ancora essere consentita anche se il dispositivo si riavvia o riceve un criterio in modalità **Imposizione abilitata**.
- Per assicurarsi che il criterio di controllo delle applicazioni di Windows Defender sia valido, preparare il dispositivo in un ambiente lab. Distribuire quindi il criterio con **Imposizione abilitata** e infine riavviare il dispositivo prima di consegnarlo a un utente finale.
- Non distribuire un criterio in modalità **Imposizione abilitata** per poi distribuire in un secondo momento un criterio in modalità **Solo controllo** nello stesso dispositivo. Questa configurazione potrebbe consentire l'esecuzione di software non attendibile.
- Quando si usa Configuration Manager per abilitare l'integrità del codice configurabile nei PC client con criteri di controllo delle applicazioni di Windows Defender, il sistema non impedisce agli utenti con diritti di amministratore locale di eludere i criteri di controllo delle applicazioni di Windows Defender o di eseguire in altro modo software non attendibile. 
- L'unico modo per impedire agli utenti con diritti di amministratore locale di disabilitare l'integrità del codice configurabile consiste nel distribuire un criterio binario firmato, operazione possibile con Criteri di gruppo, ma non attualmente supportata in Configuration Manager.
- La configurazione di Configuration Manager come programma di installazione gestito nei PC client usa criteri di AppLocker. AppLocker è usato solo per identificare i programmi di installazione gestiti e qualsiasi imposizione avviene con l'integrità del codice configurabile. 




