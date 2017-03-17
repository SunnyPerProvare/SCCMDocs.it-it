---
title: Configurare i certificati | Microsoft Docs
description: Configurare i certificati per le comunicazioni attendibili per la gestione dei dispositivi mobili locale in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
caps.latest.revision: 27
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ef35e98ccae0c708cd12767eef9f923f211849fb
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione dei dispositivi mobili locale di System Center Configuration Manager richiede che i ruoli del sistema del sito punto di registrazione, punto proxy di registrazione, punto di distribuzione e punto di gestione dispositivi siano configurati per le comunicazioni attendibili con i dispositivi gestiti. Qualsiasi server del sistema del sito che ospita uno o più di tali ruoli deve avere un certificato PKI univoco associato al server Web in tale sistema. Per stabilire una connessione attendibile con i dispositivi gestiti, inoltre, è necessario archiviarvi un certificato con la stessa radice del certificato sui server.  

 Per i dispositivi aggiunti a un dominio, Servizi certificati Active Directory installa automaticamente il certificato necessario con la radice attendibile su tutti i dispositivi. Per i dispositivi non aggiunti a un dominio, è necessario ottenere un certificato valido con una radice attendibile in altro modo. Se si usa l'autorità di certificazione del sito come radice attendibile (la stessa usata da Active Directory per i dispositivi aggiunti a un dominio), ai server del sistema del sito per il punto di registrazione e per il punto proxy di registrazione deve essere associato un certificato rilasciato dalla stessa autorità di certificazione.  

 Anche in ogni dispositivo da gestire dovrà essere installato un certificato con la stessa radice per supportare le comunicazioni attendibili con i ruoli del sistema del sito. Per i dispositivi registrati in blocco, è possibile includere il certificato nel pacchetto di registrazione che viene aggiunto al dispositivo per la registrazione quando il dispositivo viene avviato per la prima volta da un utente. Per i dispositivi registrati dagli utenti, è necessario aggiungere il certificato tramite posta elettronica, download Web o altro metodo.  

 Come alternativa per i dispositivi non aggiunti al dominio, è possibile usare la radice di una CA pubblica nota, come Verisign o GoDaddy, per rilasciare il certificato server, evitando così di dover installare manualmente un certificato sul dispositivo, in quanto la maggior parte dei dispositivi considera attendibili in modo nativo le connessioni al server che usano la stessa radice dell'autorità di certificazione pubblica. Si tratta di un'alternativa utile per i dispositivi registrati dagli utenti in cui non è possibile installare i certificati attendibili attraverso l'autorità di certificazione del sito.  

> [!IMPORTANT]  
>  Esistono diversi modi per configurare i certificati per le comunicazioni attendibili tra i dispositivi e i server del sistema del sito per la gestione dei dispositivi mobili locale. Le informazioni in questo articolo sono un esempio di uno dei modi possibili. Per questo metodo è necessario che nel sito sia in esecuzione un server con il ruolo Servizi certificati Active Directory e con i servizi ruolo Autorità di certificazione e Registrazione Web Autorità di certificazione installati. Per altre informazioni e linee guida su questo ruolo di Windows server, vedere [Servizi certificati Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=115018).  

 Per configurare il sito di Configuration Manager per le comunicazioni SSL richieste dalla gestione dei dispositivi mobili locale, attenersi alla procedura seguente:  

-   [Configurare l'autorità di certificazione (CA) per la pubblicazione CRL](#bkmk_configCa)  

-   [Creare il modello di certificato del server Web nella CA](#bkmk_certTempl)  

-   [Richiedere il certificato del server Web per ogni ruolo del sistema del sito](#bkmk_requestCert)  

-   [Associare il certificato al server Web](#bkmk_bindCert)  

-   [Esportare il certificato con la stessa radice del certificato del server Web](#bkmk_exportCert)  

##  <a name="bkmk_configCa"></a> Configurare l'autorità di certificazione (CA) per la pubblicazione CRL  
 Per impostazione predefinita, l'autorità di certificazione (CA) usa gli elenchi di revoche di certificati (CRL) basati su LDAP che consentono le connessioni per i dispositivi aggiunti a un dominio. Per fare in modo che i dispositivi non aggiunti a un dominio siano considerati attendibili con certificati rilasciati dalla CA, è necessario aggiungere elenchi CRL basati su HTTP alla CA. Questi certificati sono necessari per le comunicazioni SSL tra i server che ospitano i ruoli del sistema del sito di Configuration Manager e i dispositivi registrati per la gestione dei dispositivi mobili locale.  

 Per configurare la CA per la pubblicazione automatica delle informazioni CRL per il rilascio di certificati che consentono connessioni attendibili per i dispositivi aggiunti e non aggiunti a un dominio, seguire questa procedura:  

1.  Nel server che esegue l'autorità di certificazione per il sito fare clic su **Start** > **Strumenti di amministrazione** > **Autorità di certificazione**.  

2.  Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **CertificateAuthority** e scegliere **Proprietà**.  

3.  Nelle proprietà di CertificateAuthority fare clic sulla scheda **Estensioni** e verificare che in **Selezionare l'estensione** sia impostato **Punto di distribuzione CRL**  

4.  Selezionare **http://<NomeDNSServer\>/CertEnroll/<NomeCA\><SuffissoNomeCRL\><DeltaCRLAllowed\>.crl**. Selezionare anche le tre opzioni seguenti:  

    -   **Includi nei CRL. I client la utilizzeranno per trovare i percorsi Delta CRL.**  

    -   **Includi nell'estensione dei punti di distribuzione dei certificati emessi.**  

    -   **Includi nell'estensione IDP dei CRL rilasciati**  

5.  Fare clic sulla scheda **Modulo uscita**, fare clic su **Proprietà**, selezionare **Consenti la pubblicazione di certificati nel file system**.  

6.  Fare clic su **OK** quando viene indicato che è necessario riavviare Servizi certificati Active Directory.  

7.  Fare clic con il pulsante destro del mouse su **Certificati revocati**, scegliere **Tutte le attività** e quindi **Pubblica**.  

8.  Nella finestra di dialogo Pubblicazione CRL selezionare solo **Delta CRL** e fare clic su **OK**.  

##  <a name="bkmk_certTempl"></a> Creare il modello di certificato del server Web nella CA  
 Dopo la pubblicazione del nuovo CRL nella CA, il passaggio successivo consiste nel creare un modello di certificato del server Web. Questo modello è necessario per il rilascio di certificati per i server che ospitano i ruoli del sistema del sito punto di registrazione, punto proxy di registrazione, punto di distribuzione e punto di gestione dispositivi. Questi server saranno gli endpoint SSL per le comunicazioni attendibili tra i ruoli del sistema del sito e i dispositivi registrati.    Per creare il modello di certificato, seguire questa procedura:  

1.  Creare un gruppo di sicurezza denominato **Server MDM ConfigMgr** che contiene i server che eseguono i sistemi del sito che richiedono comunicazioni attendibili con i dispositivi registrati.  

2.  Nella console Autorità di certificazione fare clic con il pulsante destro del mouse su **Modelli di certificato** e scegliere **Gestisci** per caricare la console Modelli di certificato.  

3.  All'interno del riquadro dei risultati fare clic con il pulsante destro del mouse sulla voce che visualizza **Server Web** nella colonna **Nome visualizzato modello**, quindi fare clic su **Duplica modello**.  

4.  Nella finestra di dialogo **Duplica modello** , verificare che sia selezionato **Windows 2003 Server, Enterprise Edition** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Non selezionare **Windows 2008 Server, Enterprise Edition**. Configuration Manager non supporta i modelli di certificato di Windows Server 2008 per le comunicazioni attendibili tramite HTTPS.  

    > [!NOTE]  
    >  Se l'autorità di certificazione in uso si trova in Windows Server 2012, non viene richiesta la versione del modello di certificato quando si fa clic su **Duplica modello**. Al contrario, specificarla nella scheda **Compatibilità** delle proprietà del modello, come indicato di seguito:  
    >   
    >  **Autorità di certificazione**: **Windows Server 2003**  
    >   
    >  **Destinatario certificato**: **Windows XP / Server 2003**  

5.  Nella finestra di dialogo **Proprietà nuovo modello** della scheda **Generale** immettere un nome di modello per generare i certificati Web che verranno usati nei sistemi del sito di Configuration Manager, ad esempio **Server Web MDM ConfigMgr**.  

6.  Fare clic sulla scheda **Nome oggetto**, selezionare **Crea in base alle informazioni di Active Directory** e per il formato del nome dell'oggetto specificare **Nome DNS**. Deselezionare la casella di controllo relativa al nome dell'oggetto alternativo se è selezionata l'opzione **Nome entità utente (UPN)**.  

7.  Fare clic sulla scheda **Protezione** e rimuovere l'autorizzazione **Registrazione** dai gruppi di protezione **Domain Admins** ed **Enterprise Admins**.  

8.  Fare clic su **Aggiungi**, immettere **Server MDM ConfigMgr** nella casella di testo, quindi fare clic su **OK**.  

9. Selezionare l'autorizzazione **Registrazione** per questo gruppo e non cancellare l'autorizzazione **Lettura** .  

10. Fare clic su **OK**e chiudere la console Modelli di certificato.  

11. Nella console Autorità di certificazione, fare clic con il pulsante destro del mouse su **Modelli di certificato**, quindi fare clic su **Nuovo**e successivamente su **Modello di certificato da emettere**.  

12. Nella finestra di dialogo **Attivazione modelli di certificato** selezionare il nuovo modello appena creato, **Server Web MDM ConfigMgr**, quindi fare clic su **OK**.  

##  <a name="bkmk_requestCert"></a> Richiedere il certificato del server Web per ogni ruolo del sistema del sito  
 I dispositivi registrati per la gestione dei dispositivi mobili locale devono considerare attendibili gli endpoint SSL che ospitano il punto di registrazione, il punto proxy di registrazione, il punto di distribuzione e il punto di gestione dispositivi.  La procedura seguente mostra come richiedere il certificato del server Web per IIS. È necessario eseguire questa operazione per ogni server (endpoint SSL) che ospita uno dei ruoli del sistema del sito necessari per la gestione dei dispositivi mobili locale.  

1.  Nel server del sito primario aprire il prompt dei comandi con le autorizzazioni di amministratore, digitare **MMC** e premere **INVIO**.  

2.  In MMC fare clic su **File** > **Aggiungi/Rimuovi snap-in**.  

3.  Nello snap-in Certificati selezionare **Certificati**, fare clic su **Aggiungi**, selezionare **Account del computer**, fare clic su **Avanti**, fare clic su **Fine** e quindi fare clic su **OK** per uscire dalla finestra Aggiungi o rimuovi snap-in.  

4.  Fare clic con il pulsante destro del mouse su **Personale** e scegliere **Tutte le attività** > **Richiedi nuovo certificato**.  

5.  Nella procedura guidata Registrazione certificato fare clic su **Avanti**, selezionare **Criteri di registrazione Active Directory** e fare clic su **Avanti**.  

6.  Selezionare la casella di controllo accanto al certificato del server Web (**Server Web MDM ConfigMgr**), quindi fare clic su **Registrazione**.  

7.  Al termine della registrazione del certificato, fare clic su **Fine**.  

 Dato che per ogni server sarà necessario un certificato server Web univoco, occorre ripetere questa procedura per ogni server che ospita uno dei ruoli del sistema del sito necessari per la gestione dei dispositivi mobili locale.  Se un server ospita tutti i ruoli del sistema del sito, è sufficiente richiedere un certificato del server Web.  

##  <a name="bkmk_bindCert"></a> Associare il certificato al server Web  
 A questo punto è necessario che il nuovo certificato venga associato al server Web per ogni server del sistema del sito che ospita i ruoli del sistema del sito necessari per la gestione dei dispositivi mobili locale. Seguire questa procedura per ogni server che ospita i ruoli del sistema del sito di punto di registrazione e punto proxy di registrazione. Se un server ospita tutti i ruoli del sistema del sito, è sufficiente eseguire la procedura una sola volta. Questa operazione non è necessaria per i ruoli del sistema del sito punto di distribuzione e punto di gestione dispositivi perché questi ricevono automaticamente il certificato richiesto durante la registrazione.  

1.  Nel server che ospita il punto di registrazione, il punto proxy di registrazione, il punto di distribuzione o il punto di gestione dispositivi fare clic su **Start** > **Strumenti di amministrazione** > **Gestione IIS**.  

2.  In Connessioni individuare e fare clic con il tasto destro del mouse su **Sito Web predefinito** e scegliere **Modifica binding**.  

3.  Nella finestra di dialogo Binding sito fare clic su **https** e quindi su **Modifica**.  

4.  Nella finestra di dialogo Modifica binding sito selezionare il certificato appena registrato per il **Certificato SSL**, fare clic su **OK**, quindi su **Chiudi**.  

5.  Nella console di Gestione IIS, in Connessioni, selezionare il server Web e quindi nel riquadro Azioni a destra fare clic su **Riavvia**.  

##  <a name="bkmk_exportCert"></a> Esportare il certificato con la stessa radice del certificato del server Web  
 Servizi certificati Active Directory in genere installa il certificato richiesto dalla CA in tutti i dispositivi aggiunti a un dominio. I dispositivi non aggiunti a un dominio, però, non potranno comunicare con i ruoli del sistema del sito senza il certificato della CA radice. Per ottenere il certificato richiesto per la comunicazione dei dispositivi con i ruoli del sistema del sito, è possibile esportarlo dal certificato associato al server Web.  

 Seguire questa procedura per esportare il certificato radice del certificato del server Web.  

1.  In Gestione IIS fare clic su **Sito Web predefinito** e quindi nel riquadro Azioni a destra fare clic su **Binding**.  

2.  Nella finestra di dialogo Binding sito fare clic su **https** e quindi fare clic su **Modifica**.  

3.  Assicurarsi che sia selezionato il certificato del server Web e fare clic su **Visualizza**.  

4.  Nelle proprietà del certificato del server Web fare clic su **Percorso certificazione**, fare clic sulla radice all'inizio del percorso di certificazione e fare clic su **Visualizza certificato**.  

5.  Nelle proprietà del certificato radice fare clic su **Dettagli** e quindi fare clic su **Copia su file**.  

6.  Nell'Esportazione guidata certificati fare clic su **Avanti**.  

7.  Assicurarsi che sia selezionata l'opzione **Binario codificato DER X.509 (.CER)** per il formato, quindi fare clic su **Avanti**.  

8.  Per il nome del file fare clic su **Sfoglia**, scegliere un percorso in cui salvare il file del certificato, assegnare un nome al file e fare clic su **Salva**.  

     I dispositivi da registrare dovranno avere accesso a questo file per importare il certificato radice, quindi scegliere un percorso comune a cui può accedere la maggior parte dei computer e dispositivi oppure salvarlo in una posizione facilmente raggiungibile, ad esempio l'unità C, e spostarlo successivamente nel percorso comune.  

     Fare clic su **Avanti**.  

9. Verificare le impostazioni e fare clic su **Fine**.  

