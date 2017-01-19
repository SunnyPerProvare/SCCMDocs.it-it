---
title: Controlli dei prerequisiti | Microsoft Docs
description: Esaminare i controlli dei prerequisiti disponibili per System Center Configuration Manager. Include i controlli per i privilegi di protezione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9ace6e8fa05122924daaeceddf097ce1db12cf39


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>Elenco dei controlli dei prerequisiti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sezioni seguenti illustrano in dettaglio i controlli dei prerequisiti disponibili.  


 Per informazioni sul controllo dei prerequisiti, vedere [Prerequisite Checker](prerequisite-checker.md) (Controllo dei prerequisiti).  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> Controlli dei prerequisiti per i privilegi di protezione  
 Di seguito sono indicati i controlli dei prerequisiti eseguiti da Controllo prerequisiti per i diritti di sicurezza.  

 **Diritti amministrativi per il sito di amministrazione centrale**: verifica che l'account utente che esegue l'installazione di Configuration Manager abbia i diritti di **Amministratore** locale nel computer del sito di amministrazione centrale.  

-   **Gravità:** Errore  

-   **Applicabilità:**  
      -   Sito primario  

**Diritti amministrativi nel sito primario di espansione**: verifica che l'utente che esegue l'installazione abbia i diritti di **Amministratore** locale nel sito primario autonomo che verrà espanso.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Diritti amministrativi nel sistema del sito**: verifica che l'account utente che esegue l'installazione di Configuration Manager abbia i diritti di **Amministratore** locale nel computer del server del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  
    -   Sito primario  
    -   Sito secondario  

**Diritti amministrativi per il computer CAS nel sito primario di espansione**: verifica che l'account computer del sito di amministrazione centrale abbia i diritti di **Amministratore** locale nel sito primario autonomo che verrà espanso.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Connessione a SQL Server nel sito di amministrazione centrale**: verifica che l'account utente che esegue l'installazione di Configuration Manager nel sito primario per l'aggiunta a una gerarchia esistente abbia il ruolo **sysadmin** nell'istanza di SQL Server per il sito di amministrazione centrale.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario  

**Diritti amministrativi dell'account computer del server del sito**: verifica che l'account computer del server del sito abbia i diritti amministrativi in SQL Server e nei computer del punto di gestione.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario  
    -   SQL Server  

**Sistema del sito nella comunicazione con SQL Server**: verifica che un nome dell'entità servizio (SPN) valido venga registrato in Active Directory Domain Services per l'account configurato per eseguire il servizio SQL Server per l'istanza di SQL Server usata per ospitare il database del sito di Configuration Manager. È necessario registrare un SPN valido in Servizi di dominio Active Directory per supportare l'autenticazione Kerberos.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito secondario  
    -   Punto di gestione  

**Modalità di sicurezza di SQL Server**: verifica che SQL Server sia configurato per la sicurezza di autenticazione di Windows.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   SQL Server  

**Diritti di amministratore di sistema di SQL Server**: verifica che l'account utente che esegue l'installazione di Configuration Manager abbia il ruolo **sysadmin** nell'istanza di SQL Server selezionata per l'installazione del database del sito. Questo controllo ha esito negativo anche quando l'installazione non riesce ad accedere all'istanza di SQL Server per verificare le autorizzazioni.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**Diritti di amministratore di sistema di SQL Server per il sito di riferimento** : verifica che l'account utente che esegue l'installazione di Configuration Manager abbia il ruolo **sysadmin** nell'istanza del ruolo di SQL Server selezionata come database del sito di riferimento.  Le autorizzazioni del ruolo **sysadmin** di SQL Server sono necessarie per modificare il database del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Controlli dei prerequisiti per le dipendenze di Configuration Manager  
 Di seguito sono indicati i controlli dei prerequisiti eseguiti da Controllo prerequisiti per la dipendenze di Configuration Manager.  

**Mapping di migrazione attivi nel sito primario di destinazione**  

 Verifica che non siano presenti mapping di migrazione attivi nei siti primari.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Replica di MP attiva**: cerca una replica del punto di gestione attiva.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario  

**Diritti amministrativi per il punto di distribuzione**: verifica che l'utente che esegue il programma di installazione abbia i diritti di **Amministratore** locale nel computer del punto di distribuzione.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di distribuzione  

**Diritti amministrativi nel punto di gestione**: verifica che l'account computer del server del sito abbia i diritti di **Amministratore** nel computer del punto di gestione e del punto di distribuzione.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione  

**Condivisione amministrativa (sistema del sito)**: verifica che le condivisioni amministrative necessarie siano presenti nel computer del sistema del sito.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione  

**Compatibilità applicazione**: verifica che le applicazioni correnti siano compatibili con lo schema dell'applicazione.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  

**BITS abilitato**: verifica che il Servizio trasferimento intelligente in background (BITS) sia installato nel computer del sistema del sito del punto di gestione. Se questo controllo ha esito negativo BITS non è installato, il componente di compatibilità WMI IIS 6 per IIS7 non è installato nel computer oppure nell'host IIS remoto oppure non è stato possibile verificare le impostazioni IIS remote poiché i componenti comuni IIS non sono stati installati nel computer del server del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Punto di gestione  

**BITS installato**: verifica che il Servizio trasferimento intelligente in background (BITS) sia installato in Internet Information Services (IIS).  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione  

**Regole di confronto senza distinzione tra maiuscole e minuscole in SQL Server**: verifica che l'installazione di SQL Server usi regole di confronto senza distinzione tra maiuscole e minuscole, ad esempio SQL_Latin1_General_CP1_CI_AS.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**Verifica della versione e del codice sito di un sito primario autonomo esistente**: verifica che il sito primario che si intende espandere sia un sito primario autonomo e abbia la stessa versione di Configuration Manager, ma con un codice del sito diverso rispetto al sito di amministrazione centrale da installare.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  

**Verifica la presenza di riferimenti a raccolte incompatibili**: durante un aggiornamento, questo controllo verifica che le raccolte facciano riferimento solo ad altre raccolte dello stesso tipo.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Versione client nel computer del punto di gestione**: verifica che nel computer in cui si sta installando il punto di gestione non sia installata una versione diversa del client di Configuration Manager.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Punto di gestione  

**Configurazione per l'utilizzo della memoria di SQL Server**: controlla se SQL Server è configurato per un utilizzo della memoria illimitato. È necessario configurare la memoria di SQL Server per un limite massimo.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   SQL Server  

**Istanza di SQL Server dedicata**: controlla se un'istanza dedicata di SQL Server è configurata per ospitare il database del sito di Configuration Manager. Se un altro sito usa l'istanza, è necessario selezionare un'istanza diversa per il nuovo sito. In alternativa, è possibile disinstallare l'altro sito o spostare il relativo database in un'istanza diversa di SQL Server.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Componenti del server di Configuration Manager esistenti nel server del sito**: verifica che un server del sito o un ruolo del sistema del sito non sia già installato nel computer selezionato per l'installazione del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Eccezione del firewall per SQL Server**: controlla se Windows Firewall è disattivato o se è presente un'eccezione relativa a Windows Firewall per SQL Server. È necessario consentire l'accesso remoto a sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Broker Service usa la porta TCP 4022.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario    
    -   Punto di gestione  

**Eccezione firewall per SQL Server (sito primario autonomo)**: controlla se Windows Firewall è disattivato o se è presente un'eccezione relativa a Windows Firewall per SQL Server. È necessario consentire l'accesso remoto a sqlservr.exe o alle porte TCP richieste. Per impostazione predefinita, SQL Server è in ascolto sulla porta TCP 1433 e SQL Broker Service usa la porta TCP 4022.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito primario (solo autonomo)  

**Eccezione del firewall di SQL Server per il punto di gestione**: controlla se Windows Firewall è disattivato o se è presente un'eccezione relativa a Windows Firewall per SQL Server.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione  

**Configurazione HTTPS di IIS**: verifica i binding del sito Web Internet Information Services (IIS) per il protocollo di comunicazione HTTPS. Quando si desidera installare ruoli del sito che richiedono HTTPS, è necessario configurare i binding del sito IIS nel server specificato con un certificato PKI valido.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione    
    -   Punto di distribuzione  

**Servizio IIS in esecuzione**: verifica che Internet Information Services (IIS) sia installato e in esecuzione nel computer per installare il punto di gestione o il punto di distribuzione.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Punto di gestione    
    -   Punto di distribuzione  

**Corrispondenza delle regole di confronto del sito primario di espansione**: verifica che il database del sito per il sito primario autonomo da espandere usi le stesse regole di confronto del database del sito nel sito di amministrazione centrale.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Libreria di Compressione differenziale remota Microsoft (RDC) registrata**: verifica che la libreria di Compressione differenziale remota Microsoft (RDC) sia registrata nel server del sito di Configuration Manager.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Microsoft Windows Installer**: verifica la versione di Windows Installer. Se questo controllo ha esito negativo, l'installazione non riesce a verificare la versione oppure la versione installata non soddisfa il requisito minimo di Windows Installer versione 4.5.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Microsoft XML Core Services 6.0 (MSXML60)**: verifica che nel computer sia installato Microsoft Core XML Services (MSXML) 6.0 o versioni successive.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario    
    -   Console di Configuration Manager    
    -   Punto di gestione    
    -   Punto di distribuzione  

**Versione minima di .NET Framework per la console di Configuration Manager**: controlla se nel computer della console di Configuration Manager è installato Microsoft .NET Framework versione 4.0. È possibile scaricare Microsoft .NET Framework versione 4.0 dall' [Area download Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=189149).  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Console di Configuration Manager  

**Versione minima di .NET Framework per il server del sito di Configuration Manager**: controlla se nel server del sito di Configuration Manager è installato Microsoft .NET Framework versione 3.5. Per Windows Server 2008, è possibile scaricare Microsoft .NET Framework versione 3.5 dall' [Area download Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=185604). Per Windows Server 2008 R2, è possibile attivare Microsoft .NET Framework versione 3.5 come funzionalità di Server Manager.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Versione minima di .NET Framework per l'installazione di SQL Server Express Edition per il sito secondario di Configuration Manager**: verifica che Microsoft .NET Framework versione 4.0 sia installato nei computer del sito secondario di Configuration Manager per l'installazione di SQL Server Express Edition.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito secondario  

**Regole di confronto del database padre/figlio**: verifica che le regole di confronto del database del sito corrispondano a quelle del database del sito padre. Tutti i siti in una gerarchia devono usare le stesse regole di confronto del database.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario    
    -   Sito secondario  

**PowerShell 2.0 nel server del sito**: verifica che Windows PowerShell versione 2.0 o successiva sia installato nel server del sito per Configuration Manager Exchange Connector. Per altre informazioni su PowerShell 2.0, vedere l' [articolo 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) nella Microsoft Knowledge Base.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito primario  

**FQDN primario**: verifica che il nome NetBIOS del computer corrisponda al nome host locale (prima etichetta dell'FQDN) del computer.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario    
    -   SQL Server  

**Connessione remota a WMI nel sito secondario**: controlla se il programma di installazione riesce a stabilire una connessione remota a WMI nel server del sito secondario.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito secondario  

**Regole di confronto di SQL Server richieste**: verifica che l'istanza per SQL Server e il database del sito di Configuration Manager, se installato, siano configurati per l'uso della regola di confronto SQL_Latin1_General_CP1_CI_AS, a meno che non si usi un sistema operativo cinese che richiede un supporto GB18030.  

 Per informazioni su come modificare le regole di confronto del database e dell'istanza di SQL Server, vedere [Impostazione e modifica di regole di confronto](http://go.microsoft.com/fwlink/p/?LinkID=234541) nella documentazione online di SQL Server 2008 R2.  Per informazioni sull'attivazione del supporto GB18030, vedere [Supporto internazionale in System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Cartella di origine di installazione**: verifica che l'account computer per il sito secondario abbia le autorizzazioni del file system NTFS **Lettura** e le autorizzazioni di condivisione **Lettura** per la cartella di origine di installazione e la condivisione.  

> [!NOTE]  
>  Se si usano condivisioni amministrative, ad esempio C$ e D$, l'account computer del sito secondario deve essere un amministratore nel computer.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito secondario  

**Versione dell'origine installazione**: verifica che la versione di Configuration Manager nella cartella di origine specificata per l'installazione del sito secondario corrisponda alla versione di Configuration Manager del sito primario.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito secondario  

**Codice del sito in uso**: verifica che il codice del sito specificato non sia già in uso nella gerarchia di Configuration Manager. È necessario specificare un codice univoco per questo sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario  

**Il computer del provider SMS ha lo stesso dominio del server del sito**: controlla se un computer che esegue un'istanza del Provider SMS ha lo stesso dominio del server del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   provider SMS  

**Edizione di SQL Server**: verifica che l'edizione di SQL Server nel sito non sia SQL Server Express.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**SQL Server Express nel sito secondario**: verifica che SQL Server Express possa essere installato correttamente nel computer del server del sito per un sito secondario.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito secondario  

**SQL Server nel computer del sito secondario**: verifica che SQL Server sia installato nel computer del sito secondario. Non è supportato per installare SQL Server nel sistema del sito remoto.  

> [!WARNING]  
>  La verifica viene eseguita solo quando si configura il programma di installazione in modo che usi un'istanza esistente di SQL Server.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito secondario  

**Allocazione di memoria per il processo di SQL Server**: verifica che SQL Server riservi almeno 8 GB di memoria per il sito di amministrazione centrale e per il sito primario e almeno 4 GB di memoria per il sito secondario. Per altre informazioni su come impostare una quantità fissa di memoria tramite SQL Server Management Studio, vedere [Procedura: Impostazione di una quantità di memoria fissa (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  Questo controllo non è applicabile a SQL Server Express in un sito secondario, limitato a 1 GB di memoria riservata  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   SQL Server  

**Account di esecuzione del servizio SQL Server**: verifica che l'account di accesso per il servizio SQL Server non sia un account utente locale o di tipo LOCAL SERVICE. È necessario configurare il servizio SQL Server per l'utilizzo di un account di dominio valido, di tipo NETWORK SERVICE o LOCAL SYSTEM.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Porta TCP di SQL Server**: verifica che TCP sia abilitato per SQL Server e che sia impostato per usare una porta statica.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**Versione di SQL Server**: verifica che una versione supportata di SQL Server sia installata nel server di database del sito specificato. Per altre informazioni, vedere [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) (Supporto per le versioni di SQL Server per System Center Configuration Manager).  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**Versione del sistema operativo del sistema del sito per l'aggiornamento non supportata**: durante un aggiornamento, questa regola verifica se i ruoli del sistema del sito, oltre ai punti di distribuzione, sono installati in computer che eseguono Windows Server 2008 o versioni precedenti.  

> [!NOTE]  
>  Poiché questo controllo non può risolvere lo stato dei ruoli del sistema del sito installati in Azure o per l'archiviazione cloud usata da Microsoft Intune quando si integra Intune con Configuration Manager, gli avvisi relativi a quei ruoli possono essere considerati falsi positivi e ignorati.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito primario    
    -   Sito secondario  

**Ruolo del sistema del sito 'punto di sincronizzazione di Asset Intelligence' non supportato nel sito primario esteso**: verifica che il ruolo del sistema del sito Punto di sincronizzazione di Asset Intelligence non sia installato nel sito primario autonomo da espandere.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Ruolo del sistema del sito 'Punto di Endpoint Protection' non supportato nel sito primario esteso**: verifica che il ruolo del sistema del sito Punto di Endpoint Protection non sia installato nel sito primario autonomo da espandere.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

<a name="-head"></a><<<<<<< HEAD
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **Ruolo del sistema del sito 'Connettore Microsoft Intune' non supportato nel sito primario esteso**: verifica che il ruolo del sistema del sito Connettore Microsoft Intune non sia installato nel sito primario autonomo da espandere.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale  

**Utilità di migrazione stato utente (USMT) installata**: verifica se è installato il componente Utilità di migrazione stato utente (USMT) di Windows Assessment and Deployment Kit (ADK) per Windows 8.1.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario (solo autonomo)  

**Convalida del nome FQDN del computer SQL Server**: verifica che il nome FQDN specificato per il computer SQL Server sia valido.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   SQL Server  

**Verifica della versione del sito di amministrazione centrale**: verifica che la versione del sito di amministrazione centrale sia uguale a quella di Configuration Manager.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito primario  

**Verifica delle autorizzazioni del server del sito da pubblicare in Active Directory**: verifica che l'account computer per il server del sito abbia autorizzazioni di tipo **Controllo completo** per il contenitore **System Management** nel dominio di Active Directory. Per altre informazioni sulle opzioni di configurazione delle autorizzazioni richieste, vedere [Estendere lo schema di Active Directory per System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

> [!NOTE]  
>  È possibile ignorare questo avviso se le autorizzazioni sono state verificate manualmente.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Strumenti di distribuzione Windows installati**: verifica se è installato il componente Strumenti di distribuzione Windows di Assessment and Deployment Kit (ADK) per Windows 10.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   provider SMS  

**Cluster di failover Windows**: verifica che i computer che hanno un punto di gestione o un punto di distribuzione non facciano parte di un cluster di Windows.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Punto di gestione    
    -   Punto di distribuzione  

**Ambiente preinstallazione di Windows installato**: verifica se è installato il componente Ambiente preinstallazione di Windows di Assessment and Deployment Kit (ADK) per Windows 10.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   provider SMS  

**Gestione remota Windows (WinRM) v1.1**: verifica che WinRM v1.1 sia installato nel server del sito primario o nel computer della console di Configuration Manager per l'esecuzione della console di gestione fuori banda. Per altre informazioni su come scaricare WinRM 1.1, vedere l' [articolo 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) nella Microsoft Knowledge Base.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito primario    
    -   Console di Configuration Manager  

**WSUS nel server del sito**: verifica che Windows Server Update Services (WSUS) versione 3.0 Service Pack 2 sia installato nel server del sito. Quando si usa un punto di aggiornamento software in un computer diverso rispetto al server del sito, è necessario installare la console di amministrazione WSUS nel server del sito. Per altre informazioni su WSUS, vedere la pagina Web [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) .  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> Controlli dei prerequisiti per i requisiti di sistema  
 Di seguito sono indicati i controlli dei prerequisiti eseguiti da Controllo prerequisiti per i requisiti di sistema.  

**Controllo del livello di funzionalità del dominio di Active Directory**: verifica che il livello funzionale del dominio di Active Directory sia almeno Windows Server 2008 R2.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  

**Verifica esecuzione del servizio Server**: verifica che il servizio Server sia avviato.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Appartenenza al dominio**: verifica che il computer di Configuration Manager sia membro di un dominio di Windows.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario    
    -   Provider SMS    
    -   SQL Server  

**Appartenenza al dominio**: verifica che il computer di Configuration Manager sia membro di un dominio di Windows.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Punto di gestione    
    -   Punto di distribuzione  

**Unità FAT nel server del sito**: verifica se l'unità disco è formattata con il file system FAT. Per una protezione migliore, installare i componenti del server del sito in unità disco formattate con il file system NTFS.  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito primario  

**Spazio su disco disponibile nel server del sito**: il computer del server del sito deve avere almeno 5 GB di spazio libero su disco per l'installazione del server del sito. Se si installa il ruolo del sistema del sito Provider SMS nello stesso computer, sarà necessario disporre di 1 GB aggiuntivo di spazio libero.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Riavvio del sistema in sospeso**: verifica se un altro programma necessita del riavvio del server prima dell'esecuzione del programma di installazione.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  
    -   Console di Configuration Manager    
    -   provider SMS    
    -   SQL Server    
    -   Punto di gestione    
    -   Punto di distribuzione  

**Controller di dominio di sola lettura**: i server di database del sito e i server dei siti secondari non sono supportati in un controller di dominio di sola lettura. Per altre informazioni, vedere [Si possono verificare problemi durante l'installazione di SQL Server in un controller di dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) nella Microsoft Knowledge Base.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Estensioni dello schema**: determina se lo schema di Active Directory Domain Services è stato esteso e, in tal caso, determina la versione delle estensioni dello schema usate. Le estensioni dello schema di Active Directory di Configuration Manager non sono necessarie per l'installazione del server del sito, ma sono consigliate per un supporto completo dell'utilizzo di tutte le caratteristiche di Configuration Manager. Per altre informazioni sui vantaggi offerti dall'estensione dello schema, vedere [Estendere lo schema di Active Directory per System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

-   **Gravità:** Avviso  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  

**Lunghezza FQDN del server del sito**: verifica la lunghezza del nome FQDN del computer del server del sito.  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario  

**Sistema operativo della console di Configuration Manager non supportato**: verifica che le console di Configuration Manager possano essere installate nei computer che eseguono una versione supportata del sistema operativo. Per altre informazioni, vedere [Supported operating systems for System Center Configuration Manager consoles](/sccm/core/plan-design/configs/supported-operating-systems-consoles) (Sistemi operativi supportati per le console di System Center Configuration Manager).  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Console di Configuration Manager  

**Versione del sistema operativo del server di sito non supportata per l'installazione**: verifica che nel server sia in esecuzione un sistema operativo supportato. Per altre informazioni, vedere [Supported operating systems for sites and clients for System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers) (Sistemi operativi supportati per siti e client per System Center Configuration Manager).  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario    
    -   Sito secondario    
    -   Console di Configuration Manager    
    -   Punto di gestione    
    -   Punto di distribuzione  

**Verifica coerenza database**: a partire dalla versione 1602, questo controllo verifica la coerenza del database  

-   **Gravità:** Errore  

-   **Applicabilità:**  

    -   Sito di amministrazione centrale    
    -   Sito primario  



<!--HONumber=Dec16_HO3-->


