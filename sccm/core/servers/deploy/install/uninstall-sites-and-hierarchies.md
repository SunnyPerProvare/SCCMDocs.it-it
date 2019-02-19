---
title: Siti di disinstallazione
titleSuffix: Configuration Manager
description: Leggere queste informazioni per disinstallare un sito di System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50543fdd042eb0285c070d8714cb98eec9a7629f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129069"
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Disinstallare siti e gerarchie in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Leggere le informazioni dettagliate seguenti per disinstallare un sito di System Center Configuration Manager.  

Per rimuovere le autorizzazioni da una gerarchia con più siti, la sequenza di rimozione è importante. Iniziare dalla disinstallazione dei siti dai livelli bassi della gerarchia e procedere verso i livelli alti:  

1.  Rimuovere i siti secondari collegati a siti primari.  
2.  Rimuovere i siti primari.
3.  Una volta rimossi tutti i siti primari, è possibile disinstallare il sito di amministrazione centrale.  


##  <a name="BKMK_RemoveSecondarysite"></a> Rimuovere un sito secondario da una gerarchia  
Non è possibile spostare o riassegnare un sito secondario a un nuovo sito primario padre. Per rimuovere un sito secondario da una gerarchia, è necessario eliminarlo dal sito padre diretto. Usare l'Eliminazione guidata sito secondario dalla console di Configuration Manager per rimuovere un sito secondario. Quando si rimuove un sito secondario, è necessario scegliere se eliminarlo o disinstallarlo:  

-   **Disinstallare il sito secondario**. Usare questa opzione per rimuovere un sito secondario funzionante accessibile dalla rete. Questa opzione disinstalla Configuration Manager dal server del sito secondario, elimina tutte le informazioni relative al sito e alle risorse dalla gerarchia del sito di Configuration Manager. Se Configuration Manager ha installato SQL Server Express come parte dell'installazione del sito secondario, Configuration Manager disinstalla anche SQL Express durante la disinstallazione del sito secondario. Se SQL Server Express è stato installato prima dell'installazione del sito secondario, Configuration Manager non lo disinstalla.  

-   **Eliminare il sito secondario**. Usare questa opzione in presenza di una delle seguenti condizioni:  

    -   Non è stato possibile installare un sito secondario  
    -   Il sito secondario continua a essere visualizzato nella console di Configuration Manager anche dopo essere stato disinstallato

    Questa opzione consente di eliminare tutte le informazioni sul sito e sulle relative risorse dalla gerarchia di Configuration Manager, lasciando tuttavia installato Configuration Manager sul server del sito secondario.  

    > [!NOTE]  
    >  È anche possibile usare lo strumento di manutenzione gerarchia e l'opzione **/DELSITE** per eliminare un sito secondario. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Per disinstallare o eliminare un sito secondario  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti amministrativi sul computer del sito secondario  
    -   Diritti di amministratore locale sul server di database del sito remoto per il sito primario, se è remoto  
    -   Ruolo di sicurezza Amministratore infrastruttura o Amministratore completo sul sito primario padre  
    -   Diritti di amministratore di sistema sul database del sito del sito secondario  

2.  Nella console di Configuration Manager selezionare **Amministrazione**.  
3.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito** e quindi selezionare **Siti**.  
4.  Selezionare il server del sito secondario che si vuole rimuovere.  
5.  Nel gruppo **Sito** della scheda **Home** fare clic su **Elimina**.  
6.  Nella pagina **Generale** selezionare se disinstallare o eliminare il sito secondario, quindi fare clic su **Avanti**.  
7.  Nella pagina **Riepilogo** verificare le impostazioni e quindi fare clic su **Avanti**.  
8.  Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata.  

##  <a name="BKMK_UninstallPrimary"></a> Disinstallare un sito primario  
È possibile eseguire il programma di installazione di Configuration Manager per disinstallare un sito primario che non ha un sito secondario associato. Prima di disinstallare un sito primario, tenere in considerazione quanto segue:  

-   Quando i client di Configuration Manager si trovano all'interno dei limiti configurati del sito e il sito primario fa parte di una gerarchia di Configuration Manager, aggiungere tali limiti a un sito primario diverso all'interno della gerarchia prima di disinstallare il sito primario.  
-   Quando il server del sito primario non è più disponibile, è necessario usare lo strumento di manutenzione gerarchia nel sito di amministrazione centrale per eliminare il sito primario dal database del sito. Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Usare la procedura seguente per disinstallare un sito primario.  

#### <a name="to-uninstall-a-primary-site"></a>Per disinstallare un sito primario  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale sul server del sito di amministrazione centrale  
    -   Diritti di amministratore locale sul server di database del sito remoto per il sito di amministrazione centrale, se è remoto
    -   Diritti di amministratore di sistema sul database del sito del sito di amministrazione centrale  
    -   Diritti di amministratore locale sul computer del sito primario  
    -   Diritti di amministratore locale sul server di database del sito remoto per il sito primario, se è remoto  
    -   Nome utente associato al ruolo di sicurezza Amministratore infrastruttura o Amministratore completo sul sito di amministrazione centrale  

2.  Avviare il programma di installazione di Configuration Manager sul server del sito primario usando uno dei metodi seguenti:  

    -   In **Avvia** fare clic su **Installazione di Configuration Manager**.  
    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Nella pagina **Prima di iniziare** scegliere **Avanti**.  
4.  Nella pagina **Attività iniziale** selezionare **Disinstalla un sito di Configuration Manager** e fare clic su **Avanti**.  
5.  In **Disinstalla il sito di Configuration Manager** specificare se rimuovere il database del sito dal server del sito primario e se rimuovere la console di Configuration Manager. Per impostazione predefinita, il programma di installazione li rimuoverà entrambi.  

    > [!IMPORTANT]  
    >  Quando un sito secondario è collegato al sito principale, è necessario rimuovere il sito secondario prima di disinstallare il sito principale.  

6.  Fare clic su **Sì** per confermare la disinstallazione del sito primario di Configuration Manager.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Disinstallare un sito primario configurato con viste distribuite  
 Prima di disinstallare un sito primario figlio che include viste distribuite attivate per il collegamento di replica al sito di amministrazione centrale, sarà necessario disabilitare le viste distribuite nella gerarchia. Leggere le seguenti informazioni per disattivare le viste distribuite prima di disinstallare un sito primario.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Per disinstallare un sito primario configurato con viste distribuite  

1.  Prima di disinstallare un sito primario, è necessario disattivare le viste distribuite in ogni collegamento della gerarchia tra il sito di amministrazione centrale e un sito primario.  
2.  Dopo avere disattivato le viste distribuite in ogni collegamento, assicurarsi che i dati del sito primario completino la reinizializzazione nel sito di amministrazione centrale. Per monitorare l'inizializzazione dei dati, nell'area di lavoro **Monitoraggio** della console di Configuration Manager, visualizzare il collegamento nel nodo **Replica di database**.  
3.  Dopo la reinizializzazione corretta dei dati con il sito di amministrazione centrale, sarà possibile disinstallare il sito primario. Per disinstallare un sito primario, vedere [Disinstallare un sito primario](#BKMK_UninstallPrimary).  
4.  Dopo la disinstallazione completa del sito primario, sarà possibile riconfigurare le viste distribuite nei collegamenti ai siti primari.  

    > [!IMPORTANT]  
    >  Se si disinstalla il sito primario prima di disattivare le viste distribuite in ogni sito oppure prima della reinizializzazione corretta dei dati dal sito primario nel sito di amministrazione centrale, è possibile che si verifichino errori di replica dei dati tra i siti primari e il sito di amministrazione centrale. In questo scenario è necessario disattivare le viste distribuite per ogni collegamento nella gerarchia del sito e, dopo la reinizializzazione corretta dei dati nel sito di amministrazione centrale, sarà possibile riconfigurare le viste distribuite.  

##  <a name="BKMK_UninstallCAS"></a> Disinstallare il sito di amministrazione centrale  
 È possibile eseguire il programma di installazione di Configuration Manager per disinstallare un sito di amministrazione centrale che non ha siti primari figlio. Usare la procedura seguente per disinstallare il sito di amministrazione centrale.  

#### <a name="to-uninstall-a-central-administration-site"></a>Per disinstallare un sito di amministrazione centrale  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale sul server del sito di amministrazione centrale  
    -   Diritti di amministratore locale sul server di database del sito per il sito di amministrazione centrale, se il server di database del sito non è installato nel server del sito 

2.  Avviare il programma di installazione di Configuration Manager sul server del sito di amministrazione centrale usando uno dei metodi seguenti:  

    -   In **Avvia**fare clic su **Installazione di Configuration Manager**.  
    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Aprire Setup.exe da &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  Nella pagina **Prima di iniziare** scegliere **Avanti**.  
4.  Nella pagina **Attività iniziale** selezionare **Disinstalla un sito di Configuration Manager** e fare clic su **Avanti**.  
5.  In **Disinstalla il sito di Configuration Manager** specificare se rimuovere il database del sito dal server del sito di amministrazione centrale e se rimuovere la console di Configuration Manager. Per impostazione predefinita, il programma di installazione li rimuoverà entrambi.  

    > [!IMPORTANT]  
    >  Se al sito di amministrazione centrale è collegato un sito primario, sarà necessario disinstallare il sito primario prima di disinstallare il sito di amministrazione centrale.  

6.  Fare clic su **Sì** per confermare la disinstallazione del sito di amministrazione centrale di Configuration Manager.  
