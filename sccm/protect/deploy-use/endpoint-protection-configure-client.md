---
title: Configurare il client di Endpoint Protection | Microsoft Docs
description: Informazioni su come configurare le impostazioni client personalizzate per Endpoint Protection che possono essere distribuite alle raccolte di computer nella gerarchia.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 2d7ec9cc626f3ccfded990cf8ba392c4979adfee


---

# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurare le impostazioni client personalizzate per Endpoint Protection

*Si applica a: System Center Configuration Manager (Current Branch)*

Questa procedura consente di configurare impostazioni client personalizzate per Endpoint Protection, distribuibili nelle raccolte di computer nella gerarchia.

> [!IMPORTANT]
>  Configurare le impostazioni client predefinite per Endpoint Protection solo se si è certi di volerle applicare a tutti i computer nella gerarchia.

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Per abilitare Endpoint Protection e configurare impostazioni client personalizzate

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea impostazioni dispositivo client personalizzate**.

4.  Nella finestra di dialogo **Crea impostazioni dispositivo client personalizzate** specificare un nome e una descrizione per il gruppo di impostazioni e quindi selezionare **Endpoint Protection**.

5.  Configurare le impostazioni client per Endpoint Protection che si ritengono necessarie. Per un elenco completo delle impostazioni client di Endpoint Protection che è possibile configurare, vedere la sezione Endpoint Protection nell'argomento [About Client Settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client in System Center Configuration Manager).

   > [!IMPORTANT]
   >  È necessario installare il ruolo del sistema del sito di Endpoint Protection prima di configurare le impostazioni client per Endpoint Protection.

6.  Fare clic su **OK** per chiudere la finestra di dialogo **Crea impostazioni dispositivo client personalizzate** . Le nuove impostazioni client vengono visualizzate nel nodo **Impostazioni client** dell'area di lavoro **Amministrazione** .

7.  Per poter usare le impostazioni client personalizzate, è necessario distribuirle in una raccolta. Selezionare le impostazioni client personalizzate da distribuire e quindi nel gruppo **Impostazioni client** della scheda **Home** fare clic su **Distribuisci**.

8.  Nella finestra di dialogo **Seleziona raccolta** scegliere la raccolta in cui distribuire le impostazioni client e quindi fare clic su **OK**. La nuova distribuzione viene visualizzata nella scheda **Distribuzioni** del riquadro dei dettagli.

I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere la sezione Initiate Policy Retrieval for a Configuration Manager Client (Avviare il recupero criteri per un client di Configuration Manager) in [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) (Come gestire client in System Center Configuration Manager).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Come eseguire il provisioning del client Endpoint Protection in un'immagine disco in Configuration Manager
È possibile installare il client di Endpoint Protection in un computer che si prevede di usare come origine immagine disco per la distribuzione del sistema operativo di Configuration Manager. In genere questo computer è denominato computer di riferimento. Dopo aver creato l'immagine del sistema operativo, è possibile usare la distribuzione del sistema operativo di Configuration Manager per distribuire nei computer client l'immagine che può contenere pacchetti software, incluso Endpoint Protection.

Usare le procedure descritte in questo argomento per installare e configurare il client in Endpoint Protection in un computer di riferimento

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Prerequisiti per l'installazione del client Endpoint Protection nel computer di riferimento
Nell'elenco seguente sono inclusi i prerequisiti necessari per installare il software client di Endpoint Protection in un computer di riferimento.

-   È necessario accedere al pacchetto di installazione del client di Endpoint Protection, **scepinstall.exe**. Tale pacchetto è disponibile nella cartella **Client** della cartella di installazione di Microsoft System Center Configuration Manager nel server del sito.

-   Per verificare che il client di Endpoint Protection venga distribuito con la configurazione necessaria all'organizzazione, creare e quindi esportare i criteri antimalware. È quindi possibile specificare i criteri antimalware da usare quando si installa manualmente il client di Endpoint Protection. Per altre informazioni, vedere [How to Create and Deploy Antimalware Policies for Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md) (Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager).

   > [!NOTE]
   >  I **Criteri antimalware predefiniti del client** non possono essere esportati.

-   Se si vuole installare il client di Endpoint Protection con le definizioni più aggiornate, è necessario scaricarle dal [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Come installare il software client Endpoint Protection nel computer di riferimento
È possibile installare il client di Endpoint Protection in locale nel computer di riferimento a un prompt dei comandi. A tale scopo, è innanzitutto necessario ottenere il file di installazione **scepinstall.exe**. È inoltre possibile installare il client con un criterio antimalware preconfigurato o con un criterio antimalware esportato in precedenza.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Per installare il client Endpoint Protection da un prompt dei comandi

1.  Copiare **scepinstall.exe** dalla cartella **Client** nel supporto di installazione di System Center Configuration Manager nel computer in cui si vuole installare il software client di Endpoint Protection.

2.  Aprire un prompt dei comandi con privilegi da amministratore, cercare la cartella in cui si trova **scepinstall.exe** e quindi eseguire il comando seguente aggiungendo eventuali proprietà aggiuntive della riga di comando:

   ```
   scepinstall.exe
   ```

    È possibile specificare una delle seguenti proprietà della riga di comando:

   |Proprietà|Descrizione|
   |--------------|-----------------|
   |/s|Specifica che verrà eseguita un'installazione invisibile all'utente.|
   |/q|Specifica che verrà eseguita un'estrazione dei file di installazione invisibile all'utente.|
   |/i|Specifica che deve essere eseguita un'installazione standard.|
   |/noreplace|Specifica che il software antimalware di terze parti non viene disinstallato durante l'installazione.|
   |/policy|Specifica un file di criteri antimalware da utilizzare per configurare il client durante l'installazione.|
   |/sqmoptin|Specifica che l'installazione del software client viene associata al programma Analisi utilizzo software Microsoft.|

3.  Seguire le istruzioni a schermo per completare l'installazione client.

4.  Se è stato scaricato il pacchetto con le definizioni più recenti, copiare il pacchetto nel computer client e quindi fare doppio clic sul pacchetto delle definizioni per installarlo.

   > [!NOTE]
   >  Al termine dell'installazione del client di Endpoint Protection, il client esegue automaticamente la ricerca degli aggiornamenti delle definizioni. Se la ricerca di aggiornamenti viene completata, non è necessario installare manualmente il pacchetto con le definizioni più recenti.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Per installare il software client con un criterio antimalware dal prompt dei comandi

1.  Copiare **scepinstall.exe** e il criterio antimalware esportato o preconfigurato nel computer in cui si vuole installare il software client di Endpoint Protection.

2.  Aprire un prompt dei comandi con privilegi da amministratore, cercare la cartella in cui si trovano **scepinstall.exe** e il criterio antimalware, quindi eseguire il comando seguente:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Seguire le istruzioni a schermo per completare l'installazione client.

4.  Se è stato scaricato il pacchetto con le definizioni più recenti, copiare il pacchetto nel computer client e quindi fare doppio clic sul pacchetto delle definizioni per installarlo.

   > [!NOTE]
   >  Al termine dell'installazione del client di Endpoint Protection, il client esegue automaticamente la ricerca degli aggiornamenti delle definizioni. Se la ricerca di aggiornamenti viene completata, non è necessario installare manualmente il pacchetto con le definizioni più recenti.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Verificare che il client Endpoint Protection sia installato correttamente
Dopo aver installato il client di Endpoint Protection nel computer di riferimento, verificare che il client funzioni correttamente.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Per verificare che il client Endpoint Protection sia installato correttamente

1.  Nel computer di riferimento aprire **System Center Endpoint Protection** nell'area di notifica di Windows.

2.  Nella scheda **Home** della finestra di dialogo **System Center Endpoint Protection** verificare che **Protezione in tempo reale** sia impostato su **Attivato**.

3.  Verificare che venga visualizzato **Aggiornato** per **Definizioni di virus e spyware**.

4.  Per verificare che il computer di riferimento sia pronto per la creazione dell'immagine, in **Opzioni analisi**selezionare **Completo**e quindi **Avvia analisi**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Come preparare il client Endpoint Protection per la creazione dell'immagine
Dopo aver verificato che il client di Endpoint Protection sia installato correttamente nel computer di riferimento, è possibile preparare il computer per la creazione dell'immagine. Eseguire la procedura seguente per preparare il client di Endpoint Protection per la creazione dell'immagine.


Per altre informazioni, vedere [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images) (Gestire le immagini del sistema operativo con System Center Configuration Manager).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Per preparare il client Endpoint Protection per la creazione dell'immagine

1.  Accedere al computer di riferimento come utente con privilegi amministrativi.

2.  Scaricare e installare **PsTools** dal [sito di Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) in TechNet.

3.  Aprire un prompt dei comandi con privilegi elevati, cercare la cartella in cui è stato installato PsTools e quindi digitare il comando seguente

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Fare attenzione quando si esegue l'editor del Registro di sistema in questo modo: l'opzione -s in PsExec.exe esegue l'editor del Registro di sistema con privilegi LocalSystem.

4.  Nell'editor del Registro di sistema cercare tutte le chiavi del Registro di sistema seguenti ed eliminarle.

   > [!IMPORTANT]
   >  È necessario eliminare le chiavi del Registro di sistema come ultimo passaggio prima della creazione dell'immagine del computer di riferimento. Le chiavi del Registro di sistema vengono ricreate all'avvio del client di Endpoint Protection. Se si riavvia il computer di riferimento, eliminare di nuovo le chiavi del Registro di sistema.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Dopo aver completato i passaggi precedenti, è possibile preparare il computer di riferimento per la creazione dell'immagine. Per altre informazioni, vedere [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images) (Gestire le immagini del sistema operativo con System Center Configuration Manager).

Quando viene distribuita un'immagine che contiene il software client di Endpoint Protection, il client segnalerà automaticamente le informazioni al sito di Configuration Manager a cui il computer è assegnato e verranno scaricati e applicati i criteri necessari nel computer client.



<!--HONumber=Dec16_HO3-->


