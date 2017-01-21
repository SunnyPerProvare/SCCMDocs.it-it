---
title: Disinstallare siti | Microsoft Docs
description: Usare queste informazioni come guida per disinstallare un sito di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f41e70c98c4b2ede575debb868978afa3dad1abc


---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Disinstallare siti e gerarchie in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni dettagliate seguenti come guida per disinstallare un sito di System Center Configuration Manager.  

Per rimuovere una gerarchia con più siti, la sequenza di rimozione è un aspetto importante:  

-   Per iniziare, disinstallare i siti nella parte inferiore della gerarchia e quindi procedere verso l'alto.  

-   Rimuovere prima i siti secondari collegati a siti primari  

-   Rimuovere quindi i siti primari  

-   Una volta rimossi tutti i siti primari, è possibile disinstallare il sito di amministrazione centrale.  


##  <a name="a-namebkmkremovesecondarysitea-remove-a-secondary-site-from-a-hierarchy"></a><a name="BKMK_RemoveSecondarysite"></a> Rimuovere un sito secondario da una gerarchia  
Non è possibile spostare o riassegnare siti secondari a un nuovo sito primario padre. Per rimuovere un sito secondario da una gerarchia, è necessario eliminarlo dal sito padre diretto. Usare l'Eliminazione guidata sito secondario dalla console di Configuration Manager per rimuovere il sito secondario. Quando si rimuove un sito secondario, è necessario scegliere se eliminarlo o disinstallarlo:  

-   **Disinstalla sito secondario**: usare questa opzione per rimuovere un sito secondario funzionale accessibile dalla rete. Questa opzione consente di disinstallare Configuration Manager dal server del sito secondario, eliminando tutte le informazioni sul sito e sulle relative risorse dalla gerarchia di Configuration Manager. Se Configuration Manager ha installato SQL Server Express come parte dell'installazione del sito secondario, Configuration Manager disinstalla anche SQL Express durante la disinstallazione del sito secondario. Se SQL Server Express è stato installato prima dell'installazione del sito secondario, Configuration Manager non lo disinstalla.  

-   **Elimina sito secondario**: usare questa opzione nei casi seguenti:  

    -   Non è stato possibile installare un sito secondario.  

    -   Il sito secondario continua a essere visualizzato nella console di Configuration Manager anche dopo essere stato disinstallato.  

    Questa opzione consente di eliminare tutte le informazioni sul sito e sulle relative risorse dalla gerarchia di Configuration Manager, lasciando tuttavia installato Configuration Manager sul server del sito secondario.  

    > [!NOTE]  
    >  È anche possibile usare lo strumento di manutenzione gerarchia e l'opzione **/DELSITE** per eliminare un sito secondario. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Per disinstallare o eliminare un sito secondario  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti amministrativi sul computer del sito secondario.  

    -   Diritti di amministratore locale sul server di database del sito remoto per il sito primario, se è remoto.  

    -   Ruolo di sicurezza Amministratore infrastruttura o Amministratore completo sul sito primario padre.  

    -   Diritti di amministratore di sistema sul database del sito del sito secondario.  

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

3.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

4.  Selezionare il server del sito secondario da rimuovere.  

5.  Nella scheda **Home** , nel gruppo **Sito di origine** , fare clic su **Elimina**.  

6.  Nella pagina **Generale** selezionare se disinstallare o eliminare il sito secondario, quindi fare clic su **Avanti**.  

7.  Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  

8.  Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

##  <a name="a-namebkmkuninstallprimarya-uninstall-a-primary-site"></a><a name="BKMK_UninstallPrimary"></a> Disinstallare un sito primario  
È possibile eseguire il programma di installazione di Configuration Manager per disinstallare un sito primario che non ha un sito secondario associato. Prima di disinstallare un sito primario, tenere in considerazione quanto segue:  

-   Quando i client di Configuration Manager si trovano all'interno dei limiti configurati del sito e il sito primario fa parte di una gerarchia di Configuration Manager, aggiungere tali limiti a un sito primario diverso all'interno della gerarchia prima di disinstallare il sito primario.  

-   Quando il server del sito primario non è più disponibile, è necessario usare lo strumento di manutenzione gerarchia nel sito di amministrazione centrale per eliminare il sito primario dal database del sito. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Usare la procedura seguente per disinstallare un sito primario.  

#### <a name="to-uninstall-a-primary-site"></a>Per disinstallare un sito primario  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale nel server del sito di amministrazione centrale.  

    -   Diritti di amministratore locale sul server di database del sito remoto per il sito di amministrazione centrale, se è remoto.  

    -   Diritti di amministratore di sistema sul database del sito del sito di amministrazione centrale.  

    -   Diritti di amministratore locale sul computer del sito primario.  

    -   Diritti di amministratore locale sul server di database del sito remoto per il sito primario, se è remoto.  

    -   Nome utente associato al ruolo di sicurezza Amministratore infrastruttura o Amministratore completo sul sito di amministrazione centrale.  

2.  Avviare il programma di installazione di Configuration Manager sul server del sito primario usando uno dei metodi seguenti:  

    -   In **Avvia**fare clic su **Installazione di Configuration Manager**.  

    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  

    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

4.  Nella pagina **Riquadro attività iniziale** selezionare **Disinstalla un server di sito di Configuration Manager**, quindi fare clic su **Avanti**.  

5.  In **Disinstalla il sito di Configuration Manager**specificare se rimuovere il database del sito dal server del sito primario e se rimuovere la console di Configuration Manager. Per impostazione predefinita, il programma di installazione li rimuoverà entrambi.  

    > [!IMPORTANT]  
    >  Quando un sito secondario è collegato al sito principale, è necessario rimuovere il sito secondario prima di disinstallare il sito principale.  

6.  Fare clic su **Sì** per confermare la disinstallazione del sito primario di Configuration Manager.  

##  <a name="a-namebkmkuninstallprimarydistviewsa-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a><a name="BKMK_UninstallPrimaryDistViews"></a> Disinstallare un sito primario configurato con viste distribuite  
 Prima di disinstallare un sito primario figlio che include viste distribuite configurate nel collegamento di replica al sito di amministrazione centrale, sarà necessario disabilitare le viste distribuite nella gerarchia. Usare le seguenti informazioni per disattivare le viste distribuite prima di disinstallare un sito primario.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Per disinstallare un sito primario configurato con viste distribuite  

1.  Prima di disinstallare un sito primario, è necessario disabilitare le viste distribuite in ogni collegamento della gerarchia tra il sito di amministrazione centrale e un sito primario.  

2.  Dopo avere disattivato le viste distribuite su ogni collegamento, confermare che i dati del sito primario completino la reinizializzazione nel sito di amministrazione centrale. È possibile monitorare l'inizializzazione dei dati quando si visualizza il collegamento nel nodo **Replica di database** dell'area di lavoro **Monitoraggio** della console di Configuration Manager.  

3.  Dopo la reinizializzazione corretta dei dati con il sito di amministrazione centrale, sarà possibile disinstallare il sito primario. Per disinstallare un sito primario, vedere la sezione [Disinstallare un sito primario](#BKMK_UninstallPrimary) in questo argomento.  

4.  Dopo la disinstallazione completa del sito primario, sarà possibile riconfigurare le viste distribuite nei collegamenti ai siti primari.  

    > [!IMPORTANT]  
    >  Se si disinstalla il sito primario prima di disabilitare le viste distribuite in ogni sito oppure prima della reinizializzazione corretta dei dati dal sito primario nel sito di amministrazione centrale, è possibile che si verifichino errori di replica dei dati tra i siti primari e il sito di amministrazione centrale. In questo scenario è necessario disabilitare le viste distribuite per ogni collegamento nella gerarchia, quindi, dopo la reinizializzazione corretta dei dati nel sito di amministrazione centrale, sarà possibile riconfigurare le viste distribuite.  

##  <a name="a-namebkmkuninstallcasa-uninstall-the-central-administration-site"></a><a name="BKMK_UninstallCAS"></a> Disinstallare il sito di amministrazione centrale  
 È possibile eseguire il programma di installazione di Configuration Manager per disinstallare un sito di amministrazione centrale senza siti primari figlio. Usare la procedura seguente per disinstallare il sito di amministrazione centrale.  

#### <a name="to-uninstall-a-central-administration-site"></a>Per disinstallare un sito di amministrazione centrale  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale nel server del sito di amministrazione centrale.  

    -   Diritti di amministratore locale nel server di database del sito per il sito di amministrazione centrale, se il server di database del sito non è installato nel server del sito.  

2.  Avviare il programma di installazione di Configuration Manager sul server del sito di amministrazione centrale usando uno dei metodi seguenti:  

    -   In **Avvia**fare clic su **Installazione di Configuration Manager**.  

    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  

    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

4.  Nella pagina **Riquadro attività iniziale** selezionare **Disinstalla un server di sito di Configuration Manager**, quindi fare clic su **Avanti**.  

5.  In **Disinstalla il sito di Configuration Manager**specificare se rimuovere il database del sito dal server del sito di amministrazione centrale e se rimuovere la console di Configuration Manager. Per impostazione predefinita, il programma di installazione li rimuoverà entrambi.  

    > [!IMPORTANT]  
    >  Se al sito di amministrazione centrale è collegato un sito primario, sarà necessario disinstallare il sito primario prima di disinstallare il sito di amministrazione centrale.  

6.  Fare clic su **Sì** per confermare la disinstallazione del sito di amministrazione centrale di Configuration Manager.  



<!--HONumber=Dec16_HO3-->


