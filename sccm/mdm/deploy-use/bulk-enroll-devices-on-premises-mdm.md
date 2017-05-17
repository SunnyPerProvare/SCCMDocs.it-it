---

title: Registrare in blocco i dispositivi | Microsoft Docs | Gestione dei dispositivi mobili locale
description: Registrare dispositivi in blocco automaticamente con Gestione dispositivi mobili locali in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
caps.latest.revision: 13
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: be9596537e9c80a6d78aa0685d33382bfd242afe
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Come registrare in blocco i dispositivi con la gestione di dispositivi mobili locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


La registrazione in blocco in Gestione dispositivi mobili locali in System Center Configuration Manager è una modalità di registrazione dei dispositivi più automatizzata rispetto alle registrazione utente, che richiede agli utenti di immettere le credenziali per registrare il dispositivo.  La registrazione in blocco usa un pacchetto di registrazione per autenticare il dispositivo durante la registrazione. Il pacchetto, ovvero un file con estensione ppkg, contiene un profilo del certificato e, facoltativamente, un profilo Wi-Fi se il dispositivo richiede la connettività intranet per supportare la registrazione.  

> [!NOTE]  
>  Il ramo corrente di Configuration Manager supporta la registrazione in Gestione dispositivi mobili locali per i dispositivi che eseguono i sistemi operativi seguenti:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

Le attività seguenti illustrano come registrare in blocco computer e dispositivi per Gestione dispositivi mobili locali:  

-   [Creare un profilo del certificato](#bkmk_createCert)  

-   [Creare un profilo Wi-Fi](#CreateWifi)  

-   [Creare un profilo di registrazione](#bkmk_createEnroll)  

-   [Creare un file del pacchetto di registrazione (ppkg)](#bkmk_createPpkg)  

-   [Usare il pacchetto per registrare in blocco un dispositivo](#bkmk_getPpkg)  

-   [Verificare la registrazione del dispositivo](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Creare un profilo del certificato  
 Il componente principale del pacchetto di registrazione è un profilo del certificato, che viene usato per effettuare automaticamente il provisioning di un certificato radice trusted nel dispositivo da registrare.  Questo certificato radice è necessario per la comunicazione attendibile tra i dispositivi e i ruoli del sistema del sito necessari per Gestione dispositivi mobili locali. Senza il certificato radice, il dispositivo non verrà considerato attendibile nelle connessioni HTTPS tra il dispositivo stesso e i server che ospitano i ruoli del sistema del sito del punto di registrazione, del punto proxy di registrazione, del punto di distribuzione e del punto di gestione dei dispositivi.  

 Come parte della preparazione del sistema per Gestione dispositivi mobili locali, esportare un certificato radice che è possibile usare nel profilo del certificato del pacchetto di registrazione. Per istruzioni su come ottenere il certificato radice attendibile, vedere [Export the certificate with the same root as the web server certificate](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert) (Esportare il certificato con la stessa radice del certificato del server Web).  

 Usare il certificato radice esportato per creare un profilo del certificato. Per altre informazioni, vedere [How to create certificate profiles in System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md) (Come creare profili di certificato in System Center Configuration Manager).  

##  <a name="CreateWifi"></a> Creare un profilo Wi-Fi  
 L'altro componente del pacchetto usato per la registrazione in blocco è il profilo Wi-Fi. Alcuni dispositivi potrebbero non avere la connettività di rete necessaria per supportare la registrazione fino a quando non viene effettuato il provisioning delle impostazioni di rete. Includere un profilo Wi-Fi nel pacchetto di registrazione consente di stabilire la connettività di rete per il dispositivo.  

 Per creare un profilo Wi-Fi in Configuration Manager, seguire le istruzioni in [How to create Wi-Fi profiles in System Center Configuration Manager](../../protect/deploy-use/create-wifi-profiles.md) (Come creare profili Wi-Fi in System Center Configuration Manager).  

> [!IMPORTANT]  
>Quando si crea un profilo Wi-Fi per la registrazione in blocco, tenere presente i seguenti problemi:
>
> - Il ramo corrente di Configuration Manager supporta solo le configurazioni di sicurezza Wi-Fi seguenti per Gestione dispositivi mobili locali:  
>   
>   - Tipi di sicurezza: **WPA2 Enterprise** o **WPA2 Personal**  
>   - Tipi di crittografia: **AES** o **TKIP**  
>   - Tipi EAP: **Smart Card o altro certificato** o **PEAP**  
>
>
> - Anche se Configuration Manager ha un'impostazione per le informazioni del server proxy nel profilo Wi-Fi, non configura il proxy quando il dispositivo viene registrato. Se è necessario configurare un server proxy con i dispositivi registrati, è possibile distribuire le impostazioni usando gli elementi di configurazione dopo che i dispositivi sono stati registrati o creare il secondo pacchetto mediante Progettazione immagine e configurazione di Windows da distribuire insieme al pacchetto per la registrazione in blocco.

##  <a name="bkmk_createEnroll"></a> Creare un profilo di registrazione  
 Il profilo di registrazione consente di specificare le impostazioni necessarie per la registrazione dei dispositivi, tra cui un profilo del certificato che effettuerà il provisioning dinamico di un certificato radice trusted nel dispositivo e un profilo Wi-Fi che eseguirà il provisioning delle impostazioni di rete, se necessario.  

 Prima di creare un profilo di registrazione, assicurarsi di aver creato un profilo del certificato e un profilo Wi-Fi (se necessario). Per altre informazioni, vedere [Creare un profilo del certificato](#bkmk_createCert) e [Creare un profilo Wi-Fi](#CreateWifi).  

#### <a name="to-create-an-enrollment-profile"></a>Per creare un profilo di registrazione:  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** >**Panoramica** >**Tutti i dispositivi di proprietà dell'azienda** >**Windows** >**Profili di registrazione**.  

2.  Fare clic con il pulsante destro del mouse su **Profilo di registrazione** e quindi scegliere **Crea profilo**.  

3.  Nella Creazione guidata profilo di registrazione immettere un nome per il profilo, assicurarsi che sia selezionato **Locale** per **Autorità di gestione**e quindi fare clic su **Avanti**.  

4.  Selezionare il codice del sito e fare clic su **Avanti**.  

5.  Selezionare **Solo intranet**, selezionare i punti proxy di registrazione che il dispositivo userà per avviare il processo di registrazione e quindi fare clic su **Avanti**.  

6.  Selezionare il profilo del certificato contenente il certificato radice trusted (si tratta del profilo creato in [Create a certificate profile](#bkmk_createCert)) e fare clic su **Avanti**.  

7.  Selezionare il profilo W-Fi contenente le impostazioni di rete necessarie per la connessione dei dispositivi alla rete intranet (si tratta del profilo creato in [Create a Wi-Fi profile](#CreateWifi)) e fare clic su **Avanti**.  

    > [!NOTE]  
    >  Se non si usa un profilo Wi-Fi per il pacchetto di registrazione, ignorare questo passaggio.  

8.  Confermare le impostazioni per il profilo di registrazione e fare clic su **Avanti**. Fare clic su **Chiudi** per uscire dalla procedura guidata.  

##  <a name="bkmk_createPpkg"></a> Creare un file del pacchetto di registrazione (ppkg)  
 Il pacchetto di registrazione è il file utilizzato per registrare in blocco i dispositivi per Gestione dispositivi mobili locali.  Questo file deve essere creato con Configuration Manager. È possibile creare tipi simili di pacchetti con Progettazione immagine e configurazione di Windows, ma solo i pacchetti creati in Configuration Manager possono essere utilizzati per registrare i dispositivi per Gestione dispositivi mobili locali dall'inizio alla fine. I pacchetti creati con Progettazione immagine e configurazione di Windows possono fornire solo il nome dell'entità utente (UPN) necessario per la registrazione, ma non eseguire il processo di registrazione effettivo.  

 Il processo per creare il pacchetto di registrazione richiede Windows Assessment and Deployment Kit (ADK) per Windows 10.  Nel server in cui è in esecuzione la console di Configuration Manager assicurarsi che sia installata la versione 1511 di Windows ADK. Per altre informazioni, vedere la sezione ADK dell'articolo relativo al [download di kit e strumenti per Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx).  

> [!TIP]  
>  Se un pacchetto di registrazione viene rimosso dalla console di Configuration Manager, non potrà più essere usato per registrare i dispositivi. La rimozione dei pacchetti può essere usata per gestire i pacchetti che non si vogliono più usare per la registrazione in blocco dei dispositivi.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>Per creare un file del pacchetto di registrazione (ppkg):  

1.  Fare clic con il pulsante destro del mouse sul profilo appena creato (in [Creare un profilo di registrazione](#bkmk_createEnroll)) e fare clic su **Esporta**.  

2.  Fare clic su **Sfoglia**, selezionare il percorso in cui si vuole salvare il file ppkg, immettere un nome per il pacchetto e quindi fare clic su **Salva**.  

3.  Se si vuole proteggere il pacchetto con una password, fare clic sulla casella di controllo accanto a **Crittografa pacchetto**, quindi fare clic su **Esporta** e attendere il completamento dell'esportazione che dura circa 10 secondi.  

    > [!NOTE]  
    >  Se si è crittografato il pacchetto, Configuration Manager fornisce un messaggio contenente la password decrittografata. Assicurarsi di salvare le informazioni sulla password perché saranno necessarie per effettuare il provisioning del pacchetto nei dispositivi.  

4.  Fare clic su **OK**.  

##  <a name="bkmk_getPpkg"></a> Usare il pacchetto per registrare in blocco un dispositivo  
 È possibile usare il pacchetto per registrare i dispositivi prima o dopo il provisioning del dispositivo tramite la configurazione guidata.   Il pacchetto di registrazione può anche essere incluso come parte di un pacchetto di provisioning dell'OEM (Original Equipment Manufacturer).  

 Il pacchetto deve essere distribuito fisicamente al dispositivo per usarlo per la registrazione in blocco. È possibile distribuire il pacchetto di registrazione al dispositivo in vari modi a seconda delle esigenze, tra cui:  

-   Copia dal file system  

-   Allegato al messaggio di posta elettronica  

-   Copia tramite la connessione NFC (Near Field Communication)  

-   Copia dalla scheda di memoria  

-   Acquisizione del codice a barre  

-   Copia da un dispositivo con tethering  

-   Inserito nel pacchetto di provisioning dell'OEM  

#### <a name="to-bulk-enroll-a-device"></a>Per registrare in blocco i dispositivi:  

1.  Nel dispositivo da registrare trovare il pacchetto di registrazione (con Esplora file) e fare doppio clic sul file ppkg.  

2.  Fare clic su **Sì** nel messaggio Controllo dell'account utente.  

3.  Nella finestra di dialogo in cui viene richiesto se il pacchetto proviene da una fonte attendibile fare clic su **Sì, aggiungi**.  

     Viene avviato il processo di registrazione che impiega circa 5 minuti.  

4.  Aprire **Impostazioni**.  

5.  Fare clic su  **Account** > **Accesso società**. Al termine della registrazione viene visualizzato un account in **CompanyApps**.  

6.  Fare clic sull'account e quindi fare clic su **Sincronizza** per avviare la gestione con Configuration Manager.  

##  <a name="bkmk_verifyEnroll"></a> Verificare la registrazione del dispositivo  
 È possibile verificare se i dispositivi sono stati registrati correttamente nella console di Configuration Manager.  

-   Avviare la console di Configuration Manager.  

-   Fare clic su **Asset e conformità** > **Panoramica** > **Dispositivi**. Il dispositivo registrato viene visualizzato nell'elenco.  

