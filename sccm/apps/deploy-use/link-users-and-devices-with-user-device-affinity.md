---
title: Collegare utenti e dispositivi mediante l'affinità utente dispositivo
titleSuffix: Configuration Manager
description: Collegare gli utenti e i dispositivi mediante l'affinità utente-dispositivo e distribuire automaticamente le app a tutti i dispositivi associati a un utente.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 40bab1725b074bc549eeb9e9764ab8a1dd8b83e7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337718"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Collegare utenti e dispositivi mediante l'affinità utente dispositivo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'affinità utente-dispositivo in System Center Configuration Manager (Configuration Manager) associa un utente a uno o più dispositivi. Ciò fa sì che non sia più necessario conoscere i nomi dei dispositivi di un utente per poter distribuire un'applicazione a tale utente. Anziché distribuire l'applicazione a tutti i dispositivi dell'utente, è possibile distribuire l'applicazione all'utente. L'affinità utente dispositivo garantisce quindi automaticamente l'installazione dell'applicazione in tutti i dispositivi associati a tale utente.  

 È possibile definire i dispositivi primari che gli utenti usano quotidianamente per eseguire le proprie attività. Quando si crea un'affinità tra un utente e un dispositivo, si ottengono più opzioni di distribuzione delle app. Se ad esempio un utente deve usare Microsoft Visio, è possibile installarlo nel dispositivo primario dell'utente usando una distribuzione di Windows Installer. Tuttavia, in un dispositivo non primario si potrebbe distribuire Visio come un'applicazione virtuale. È anche possibile usare l'affinità utente-dispositivo per pre-distribuire il software nel dispositivo di un utente quando l'utente non è connesso. In questo modo, quando l'utente esegue l'accesso, l'app è già installata e pronta per essere eseguita.  

 È necessario gestire le informazioni sull'affinità utente dispositivo per i computer. Configuration Manager gestisce automaticamente le affinità utente-dispositivo per i dispositivi mobili che registra.  

## <a name="manually-set-up-user-device-affinity"></a>Configurare manualmente l'affinità utente-dispositivo  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi**.  

3.  Selezionare un dispositivo dall'elenco. Nella scheda **Home** nel gruppo **Dispositivo** selezionare **Modifica utenti primari**.  

4.  Nella finestra di dialogo **Modifica utenti primari** individuare e selezionare gli utenti da aggiungere come utenti primari per il dispositivo selezionato. Scegliere **Aggiungi**.  

    > [!NOTE]  
    > Nell'elenco **Utenti primari** vengono visualizzati gli utenti già configurati come utenti primari del dispositivo e il metodo con cui è stata assegnata ogni relazione utente-dispositivo.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurare i dispositivi primari per un utente  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Utenti**.  

3.  Selezionare un utente dall'elenco. Nella scheda **Dispositivo** scegliere **Modifica dispositivi primari**.  

4.  Nella finestra di dialogo **Modifica dispositivi primari** individuare e selezionare i dispositivi da aggiungere come dispositivi primari per l'utente selezionato. Scegliere **Aggiungi**.  

    > [!NOTE]  
    > Nell'elenco **Dispositivi primari** vengono visualizzati i dispositivi già configurati come dispositivi primari per l'utente e il metodo con cui è stata assegnata ogni relazione utente-dispositivo.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Creare automaticamente le affinità utente dispositivo (solo PC Windows)  
 Configuration Manager legge i dati sugli accessi utente dal registro eventi di Windows. Per creare automaticamente le affinità utente-dispositivo, è necessario attivare le due opzioni seguenti dai criteri di sicurezza locali nei computer client per archiviare gli eventi di accesso nel registro eventi di Windows:  

-   **Controlla eventi di accesso account**  
-   **Controlla eventi di accesso**  

 Per configurare queste impostazioni, usare i criteri di gruppo di Windows.  

> [!IMPORTANT]  
> Se un errore causa la generazione di un numero elevato di voci da parte del registro eventi di Windows, è possibile che venga creato un nuovo registro eventi. In questo caso, gli eventi di accesso esistenti potrebbero non essere più disponibili per Configuration Manager.  
>   
> Prestare attenzione quando si abilitano le impostazioni **Controlla eventi accesso account** e **Controlla eventi di accesso** in Windows XP. Per impostazione predefinita i criteri di conservazione sono di 7 giorni ed è molto probabile che questi eventi vadano a riempire il registro eventi di protezione. Gli utenti standard non saranno in grado di connettersi se il registro eventi è pieno. Per evitare il problema, impostare il valore dei criteri **Retention Method** (Metodo di conservazione) per il registro di protezione su **Sovrascrivi eventi se necessario**. Per consentire dati sufficienti per l'affinità utente-dispositivo, è anche possibile impostare la massima dimensione del registro di protezione su un valore ragionevole, ad esempio da 5 a 20 MB.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurare il sito per creare automaticamente le affinità utente-dispositivo  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.  

2.  Per modificare le impostazioni client predefinite, selezionare **Impostazioni client predefinite** e quindi nella scheda **Home** nel gruppo **Proprietà** fare clic su **Proprietà**. Per creare impostazioni agente client personalizzate, selezionare il nodo **Impostazioni client** e quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea impostazioni dispositivo client personalizzate**.  

    > [!NOTE]  
    > Se si modificano le impostazioni client predefinite, verranno distribuite a tutti i computer nella gerarchia. Per altre informazioni sulla configurazione delle impostazioni client, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Per **Affinità dispositivi e utenti**, impostare quanto segue:  

    -   **Soglia di utilizzo di affinità utente dispositivo (minuti)**. Impostare il numero di minuti di utilizzo del dispositivo prima che venga creata un'affinità utente-dispositivo.  

    -   **Soglia di utilizzo di affinità utente dispositivo (giorni)**. Impostare il numero di giorni in cui viene misurata la soglia di affinità in base all'utilizzo.  

    -   **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo**. Per consentire al sito di creare automaticamente affinità utente-dispositivo, nell'elenco a discesa selezionare **True**. Se si seleziona **False**, sarà necessario approvare tutte le assegnazioni affinità utente-dispositivo.  

    > [!TIP]  
    > **Esempio:** se l'opzione **Soglia di utilizzo di affinità utente dispositivo (minuti)** viene impostata su **60** minuti e **Soglia di utilizzo di affinità utente dispositivo (giorni)** viene impostata su **5** giorni, l'utente dovrà usare il dispositivo per almeno 60 minuti in un periodo di 5 giorni per creare automaticamente un'affinità utente-dispositivo.  

Dopo aver creato automaticamente un'affinità utente-dispositivo, Configuration Manager continua a monitorare le soglie di affinità utente-dispositivo. Se l'attività dell'utente per il dispositivo è inferiore alle soglie configurate, l'affinità utente-dispositivo verrà rimossa. Impostare **Soglia di utilizzo di affinità utente dispositivo (giorni)** su un valore di almeno **7** giorni per evitare che un'affinità utente-dispositivo configurata automaticamente possa andare perduta mentre l'utente non è connesso, ad esempio durante il weekend.  

## <a name="import-user-device-affinities-from-a-file"></a>Importare le affinità utente dispositivo da un file  
 Per creare più relazioni in una volta è possibile importare un file contenente dettagli per più affinità utente-dispositivo. Per questa procedura, i dispositivi devono essere stati individuati e devono esistere come risorse nel database di Configuration Manager, in caso contrario la procedura non verrà completata.  

1.  Nella console di Configuration Manager selezionare **Asset e conformità** > **Utenti** o **Dispositivi**.  

2.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Importa affinità utente dispositivo**.  

3.  Nell'Importazione guidata affinità utente dispositivo nella pagina **Scegliere il mapping** specificare le informazioni seguenti:  

    -   **Nome file**. Specificare un file con valori delimitati da virgole, con estensione CSV, che contenga un elenco di utenti e dispositivi tra cui si vuole creare un'affinità. In questo file ogni coppia utente-dispositivo deve trovarsi su una riga separata, con valori delimitati da una virgola. Usare il formato <*Dominio*>&#92;<*nome utente*>,<*nome NetBIOS dispositivo*>.  

    -   **Questo file contiene intestazioni di colonna a scopo di riferimento**. Se il file CSV include un'intestazione di riga superiore, selezionare questa opzione per far sì che la riga di intestazione venga ignorata durante l'importazione.  

4.  Se il file che si sta importando contiene più di due elementi per riga, è possibile usare **Colonna** e **Assegna** per specificare quali colonne rappresentano gli utenti e i dispositivi e quali vanno ignorate durante l'importazione.  

5.  Scegliere **Avanti** e completare l'Importazione guidata affinità utente dispositivo.  

## <a name="let-users-create-their-own-device-affinities"></a>Consentire agli utenti di creare le proprie affinità dispositivo  
 Con la procedura successiva, è possibile configurare un utente perché possa creare un'affinità dispositivo-utente nell'app Software Center.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurare il sito per consentire le richieste di affinità utente-dispositivo create dagli utenti  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.  

2.  Per modificare le impostazioni client predefinite, selezionare **Impostazioni client predefinite** e quindi nella scheda **Home** nel gruppo **Proprietà** fare clic su **Proprietà**. Per creare impostazioni agente client personalizzate, selezionare il nodo **Impostazioni client** e quindi nella scheda **Home** nel gruppo **Crea** fare clic su **Crea impostazioni utente client personalizzate**.  

    > [!NOTE]  
    > Se si modificano le impostazioni client predefinite, verranno distribuite a tutti i computer nella gerarchia. Per altre informazioni sulla configurazione delle impostazioni client, vedere [Configurare le impostazioni client](../../core/clients/deploy/configure-client-settings.md).  

3.  Selezionare l'impostazione client **Affinità dispositivi e utenti** e quindi nell'elenco a discesa **Consentire all'utente di definire i dispositivi primari** selezionare **True**.  

### <a name="set-up-a-user-device-affinity"></a>Configurare un'affinità utente-dispositivo  

1.  Nel Catalogo applicazioni fare clic su **My Systems** (Sistemi personali).  

2.  Attivare l'opzione **Uso regolarmente il computer per lavorare**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gestire le richieste di affinità utente dispositivo dagli utenti  
 Quando l'impostazione client **Configurare automaticamente l'affinità utente dispositivo dai dati di utilizzo** è impostata su **False**, è necessario approvare tutte le assegnazioni affinità utente dispositivo.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Approvare o rifiutare una richiesta di affinità utente-dispositivo  

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** selezionare la raccolta utenti o dispositivi per cui si desidera gestire le richieste di affinità.  

3.  Nella scheda **Home** nel gruppo **Raccolta** selezionare **Gestisci richieste affinità**.  

4.  Nella finestra di dialogo **Gestire le richieste di affinità utente dispositivo** selezionare una richiesta di affinità e quindi fare clic su **Approva** o **Rifiuta**.  
