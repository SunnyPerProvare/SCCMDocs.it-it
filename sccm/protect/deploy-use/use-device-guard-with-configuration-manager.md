---
title: Come gestire Windows Device Guard | Microsoft Docs
description: Informazioni su come usare System Center Configuration Manager per gestire Windows Device Guard.
ms.custom: na
ms.date: 04/14/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 49599f529bb409f40caf9057989762e759f1c0ac
ms.openlocfilehash: 113dddb2939fedf24e8d489ff4443bd5e3e72c65
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---


# <a name="device-guard-management-with-configuration-manager"></a>Gestione di Device Guard con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>Introduzione
Windows Device Guard è un gruppo di funzionalità di Windows 10 progettate per proteggere i PC dal malware e da altro software non attendibile. Impedisce l'esecuzione di codice dannoso, garantendo che solo il codice approvato e conosciuto possa essere eseguito.

Windows Device Guard comprende funzionalità basate sia su software che su hardware. L'integrità del codice configurabile è un livello di protezione basato su software che applica un elenco esplicito di software che può essere eseguito su un PC. Autonomamente, l'integrità del codice configurabile non ha alcun prerequisito hardware o firmware. I criteri di Windows Device Guard distribuiti con Configuration Manager abilitano un criterio di integrità del codice configurabile nei PC di raccolte mirate che soddisfa i requisiti minimi di SKU e versione Windows elencati di seguito. Facoltativamente, è possibile abilitare la protezione basata su hypervisor dei criteri di integrità del codice distribuiti con Configuration Manager usando Criteri di gruppo su hardware idoneo.

Per altre informazioni su Windows Device Guard, vedere [Guida alla distribuzione di Controllo dispositivo](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

È possibile usare Configuration Manager per distribuire un criterio che consenta di configurare la modalità in cui Device Guard verrà eseguito nei PC in una raccolta. 

È possibile configurare una delle modalità seguenti:

1.    **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
2.    **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.

>[!TIP]
>In questa versione di Configuration Manager, Device Guard è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

### <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>Cosa è possibile eseguire quando si distribuisce un criterio di Device Guard?

Windows Device Guard consente di controllare rigorosamente cosa può essere eseguito sui PC gestiti dall'utente. Ciò può risultare particolarmente utile per i PC nei reparti con sicurezza elevata, in cui è fondamentale che il software indesiderato non possa essere eseguito.

Quando si distribuisce un criterio, in genere, sarà possibile eseguire i seguenti file eseguibili:

- Componenti del sistema operativo Windows
- Driver di Hardware Dev Center (con firme Windows Hardware Quality Labs)
- App di Windows Store
- Client di Configuration Manager 
- Tutto il software distribuito attraverso Configuration Manager installato nei PC dopo l'elaborazione del criterio di Device Guard. 
- Aggiornamenti ai componenti di Windows da:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Non è incluso software **non** incorporato in Windows, che viene aggiornato automaticamente da Internet o da aggiornamenti software di terze parti, che sia stato installato usando uno qualsiasi dei meccanismi di aggiornamento indicati in precedenza o da Internet. Solo le modifiche software che vengono distribuite usando il client di Configuration Manager potranno essere eseguite.

## <a name="before-you-start"></a>Prima di iniziare

Prima di configurare o distribuire i criteri di Device Guard, leggere le informazioni seguenti:

- La gestione di Device Guard è una funzionalità di versione non definitiva per Configuration Manager ed è soggetta a modifiche.
- Per usare Device Guard, i PC gestiti devono eseguire Windows 10 Enterprise con Creators Update o versione successiva.
- Una volta che un criterio viene elaborato correttamente su un PC client, Configuration Manager viene configurato come programma di installazione gestito su quel client e il software distribuito con SCCM dopo l'elaborazione del criterio viene considerato automaticamente attendibile. Il software installato da Configuration Manager prima che venga elaborato il criterio di Device Guard non è considerato automaticamente attendibile.
- In questa versione non definitiva, quando un PC client avrà ricevuto una distribuzione di un criterio di Device Guard, il tempo di elaborazione di questo criterio sarà scelto in modo casuale in un periodo di due ore. 
- I PC client devono essere connessi al rispettivo Controller di dominio per poter elaborare correttamente il criterio di Device Guard.
- Secondo la pianificazione, la valutazione di conformità predefinita per i criteri di Device Guard, configurabile durante la distribuzione, avviene ogni giorno. Se si osservano problemi nell'elaborazione dei criteri, può essere utile configurare una pianificazione di valutazione di conformità più breve, ad esempio ogni ora. Questa pianificazione determina la frequenza con cui i client proveranno nuovamente a elaborare un criterio di Device Guard in caso di errore.
- Indipendentemente dalla modalità di imposizione selezionata, quando si distribuisce un criterio di Device Guard, i PC client non riusciranno a eseguire le applicazioni HTML con l'estensione HTA.

## <a name="how-to-create-a-device-guard-policy"></a>Procedura: Creare un criterio di Device Guard
1.    Nella console di Configuration Manager fare clic su **Asset e conformità**.
2.    Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection**e quindi fare clic su **Criteri di Device Guard**.
3.    Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea criterio di Device Guard**.
4.    Nella pagina **Generale** della **Creazione guidata criterio di conformità**, specificare le seguenti informazioni:
    - **Nome**: immettere un nome univoco per questo criterio di Device Guard. 
    - **Descrizione**: facoltativamente, immettere una descrizione per il criterio che consenta di identificarlo nella console di Configuration Manager.
    - **Modalità di imposizione**: scegliere uno dei seguenti metodi di imposizione di Device Guard sul PC client.
        - **Imposizione abilitata**: è possibile eseguire solo file eseguibili attendibili.
        - **Solo controllo**: è possibile eseguire tutti i file eseguibili, ma quelli non attendibili vengono registrati nel Registro eventi del client locale.
5.    Fare clic su **Avanti** e completare la procedura guidata.

## <a name="how-to-deploy-a-device-guard-policy"></a>Procedura: Distribuire un criterio di Device Guard
1.    Nella console di Configuration Manager fare clic su **Asset e conformità**.
2.    Nell'area di lavoro **Asset e conformità** espandere **Endpoint Protection**e quindi fare clic su **Criteri di Device Guard**.
3.    Nell'elenco dei profili selezionare il profilo da distribuire e fare clic su **Distribuisci** nel gruppo **Distribuzione** della scheda **Home**.
4.    Nella finestra di dialogo di **distribuzione del criterio di Device Guard**, selezionare la raccolta a cui si vuole distribuire il criterio, configurare una pianificazione in base alla quale i client valuteranno i criteri e infine selezionare se il client può valutare il criterio di fuori delle finestre di manutenzione configurate.
5.    Al termine, fare clic su **OK** per distribuire il criterio. 

Dopo che il criterio è stato elaborato su un PC client, verrà pianificato un riavvio di tale client secondo le **Impostazioni client** per **Riavvio del computer**.
**Fino a quando non si riavvia il PC client, il criterio non sarà effettivo.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Procedura: Monitorare un criterio di Device Guard

Usare le informazioni contenute nell'argomento [Monitorare le impostazioni di conformità](/sccm/compliance/deploy-use/monitor-compliance-settings) per monitorare il criterio distribuito e accertarsi che sia stato applicato a tutti i PC in modo corretto.

Usare il seguente file di registro nei PC client per monitorare l'elaborazione di un criterio di protezione dispositivo:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Per verificare che il software specifico venga bloccato o controllato, vedere i seguenti registri eventi del client locale. Nel Visualizzatore eventi, i registri pertinenti sono i seguenti:

1.    Per il blocco e controllo di file eseguibili, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **Integrità del codice** > **Operativo**.
2.    Per il blocco e il controllo di Windows Installer e dei file di script, usare **Registri applicazioni e servizi** > **Microsoft** > **Windows** > **AppLocker** > **MSI e Script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Informazioni sulla sicurezza e sulla privacy di Device Guard

- In questa versione non definitiva, non distribuire i criteri di Device Guard con la modalità di imposizione **Solo controllo** in un ambiente di produzione. Questa modalità consente di testare la funzionalità solo in un ambiente di prova.
- I dispositivi in cui è stato distribuito un criterio in modalità **Solo controllo** o i dispositivi in cui è stato distribuito un criterio in modalità **Imposizione abilitata** e che non sono ancora stati riavviati per applicare i criteri, sono vulnerabili al software non attendibile installato.
In questo caso, l'esecuzione del software potrebbe ancora essere consentita anche se il dispositivo si riavvia o riceve un criterio in modalità **Imposizione abilitata**.
- Per garantire l'efficacia del criterio di Device Guard, preparare il dispositivo in un ambiente di laboratorio, distribuire il criterio **Imposizione abilitata**, quindi riavviare il dispositivo prima di assegnare il dispositivo a un utente finale.
- Non distribuire un criterio in modalità **Imposizione abilitata** per poi distribuire in un secondo momento un criterio in modalità **Solo controllo** nello stesso dispositivo. Questa operazione potrebbe consentire l'esecuzione di software non attendibile.
- Quando si usa Configuration Manager per abilitare l'integrità del codice configurabile nei PC client con i criteri di Device Guard, il criterio **non** impedisce agli utenti con diritti di amministratore locale di eludere il criterio di Device Guard o di eseguire altrimenti software non attendibile. 
- L'unico modo per impedire agli utenti con diritti di amministratore locale di disabilitare l'integrità del codice consiste nel distribuire un criterio di binario firmato, operazione possibile con Criteri di gruppo, ma non attualmente supportata in Configuration Manager.
- La configurazione di Configuration Manager come programma di installazione gestito nei PC client usa criteri di AppLocker. AppLocker è usato solo per identificare i programmi di installazione gestiti e qualsiasi imposizione avviene con l'integrità del codice configurabile. 





