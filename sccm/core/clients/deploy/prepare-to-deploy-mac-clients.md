---
title: Preparare la distribuzione del software client in computer Mac
titleSuffix: Configuration Manager
description: Attività di configurazione che precedono la distribuzione del client di Configuration Manager in computer Mac.
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 748a56155ca7dbbcf6764c72cf5fdf37d24a277b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparare la distribuzione del software client in computer Mac

*Si applica a: System Center Configuration Manager (Current Branch)*

Seguire questa procedura per assicurarsi di essere pronti a [distribuire il client di Configuration Manager in computer Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).

## <a name="mac-prerequisites"></a>Prerequisiti Mac

Il pacchetto di installazione del client per Mac non viene fornito con i supporti di Configuration Manager. Scaricare i **client per altri sistemi operativi** dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Versioni supportate:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

-   **Mac OS X 10.13** (macOS High Sierra )  

## <a name="certificate-requirements"></a>Requisiti del certificato
Per installare e gestire i client per computer Mac sono necessari i certificati di infrastruttura a chiave pubblica (PKI). I certificati PKI proteggono la comunicazione tra i computer Mac e il sito di Configuration Manager usando l'autenticazione manuale e i trasferimenti di dati crittografati. Configuration Manager può chiedere e installare un certificato client utente usando i Servizi certificati Microsoft con un'autorità di certificazione dell'organizzazione (CA) e il punto di registrazione di Configuration Manager e i ruoli del sistema del sito del punto proxy di registrazione. In alternativa, è possibile richiedere e installare un certificato del computer indipendentemente da Configuration Manager se il certificato soddisfa i requisiti per Configuration Manager.   

I client Mac di Configuration Manager eseguono sempre il controllo della revoca del certificato. Questa funzione non può essere disabilitata.  

Se i client Mac non riescono a confermare lo stato di revoca del certificato per un certificato del server poiché non riescono a individuare il CRL, non potranno connettersi ai sistemi del sito di Configuration Manager. Per i client Mac che si trovano in una foresta diversa rispetto a quella dell'autorità di certificazione emittente, controllare la struttura del CRL per verificare che i client Mac siano in grado di individuare e connettersi a un punto di distribuzione dell'elenco di revoche di certificati (CDP) per la connessione dei server del sistema del sito.  

Prima di installare il client di Configuration Manager in un computer Mac, stabilire come installare il certificato client:  

-   Usare la registrazione di Configuration Manager tramite lo [strumento CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Il processo di registrazione non supporta il rinnovo automatico del certificato, di conseguenza è necessario registrare nuovamente i computer Mac prima della scadenza del certificato installato.  

-   [Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Per altre informazioni sui requisiti del certificato del client Mac e altri certificati PKI necessari per supportare i computer Mac, vedere [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager).  

I client Mac vengono assegnati automaticamente al sito di Configuration Manager che li gestisce. I client Mac vengono installati come client solo Internet, anche se la comunicazione è limitata alla rete Intranet. In base a questa configurazione client, le comunicazioni avverranno con i ruoli del sistema del sito (punti di gestione e punti di distribuzione) nel sito assegnato quando questi ruoli del sistema del sito vengono configurati per consentire le connessioni client dalla rete Internet. I computer Mac non comunicano con i ruoli del sistema del sito al di fuori del sito assegnato.  

> [!IMPORTANT]  
>  Il client Mac di Configuration Manager non può essere usato per connettersi a un punto di gestione configurato per usare una [replica di database](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Distribuire un certificato server Web nei server di sistema del sito  
Se i sistemi del sito non hanno un certificato server Web, distribuirlo nei computer con questi ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

-   Punto di registrazione  

-   Punto proxy di registrazione  

Il certificato del server Web deve contenere l'FQDN Internet specificato nelle proprietà del sistema del sito. Il server non deve essere accessibile da Internet per supportare i computer Mac. Se non è richiesta la gestione client basata su Internet, è possibile specificare il valore FQDN intranet per FQDN Internet.  

Specificare il valore FQDN Internet del sistema del sito nel certificato server Web per il punto di gestione, il punto di distribuzione e il punto proxy di registrazione.

Per una distribuzione di esempio che crea e installa questo certificato server Web, vedere [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012) (Distribuire il certificato del server Web per sistemi del sito che eseguono IIS).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Distribuire un certificato di autenticazione client nei server di sistema del sito  
 Se i sistemi del sito non hanno un certificato di autenticazione client, distribuirlo nei computer con questi ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

 Per una distribuzione di esempio che crea e installa il certificato client per i punti di gestione, vedere [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012) (Distribuzione del certificato client per computer Windows)  

 Per una distribuzione di esempio che crea e installa il certificato client per i punti di gestione, vedere [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012) (Distribuzione del certificato client per punti di distribuzione).  

>[!IMPORTANT]
>  Per distribuire il client in dispositivi che eseguono macOS Sierra, il nome soggetto del certificato del punto di gestione deve essere configurato correttamente, ad esempio usando il nome FQDN del server del punto di gestione.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparare il modello di certificato client per i computer Mac  

 Il modello di certificato deve disporre delle autorizzazioni di **lettura** e **registrazione** per l'account utente che registrerà il certificato nel computer Mac.  

 Vedere [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1) (Distribuzione del certificato client per computer Mac).  

## <a name="configure-the-management-point-and-distribution-point"></a>Configurare il punto di gestione e il punto di distribuzione  
 Configurare i punti di gestione per le seguenti opzioni:  

-   HTTPS  

-   Consentire le connessioni client da Internet. Questo valore di configurazione è necessario per gestire computer Mac. Tuttavia, non significa che i server del sistema del sito devono essere accessibile da Internet.  

-   Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione  

 Nonostante i punti di distribuzione non siano necessari per l'installazione del client, è necessario configurarli per consentire le connessioni client da Internet se si vuole distribuire il software in questi computer dopo aver installato il client.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Per configurare i punti di gestione e i punti di distribuzione per supportare i computer Mac  

Prima di iniziare questa procedura, assicurarsi che il server del sistema del sito su cui sono in esecuzione il punto di gestione e di distribuzione siano configurati con un FQDN Internet. Se questi server non supportano la gestione client basata su Internet, è possibile specificare il valore FQDN Intranet come valore FQDN Internet.

Questi ruoli del sistema del sito devono trovarsi in un sito primario.  


1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e scegliere il server con i ruoli del sistema del sito corretti.  

3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Punto di gestione**, scegliere **Proprietà ruolo** e configurare le opzioni seguenti nella finestra di dialogo **Proprietà punto di gestione**:  

    1.  Scegliere **HTTPS**.  

    2.  Selezionare **Consenti solo connessione client Internet** o **Consenti connessione client Internet e Intranet**. Per queste opzioni è necessario un valore FQDN Internet o Intranet.  

    3.  Selezionare **Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**.  

4.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Punto di distribuzione**, scegliere **Proprietà ruolo** e configurare le opzioni seguenti nella finestra di dialogo **Proprietà punto di distribuzione**:  

    -   Scegliere **HTTPS**.  

    -   Selezionare **Consenti solo connessione client Internet** o **Consenti connessione client Internet e Intranet**. Per queste opzioni è necessario un valore FQDN Internet o Intranet.  

    -   Fare clic su **Importa certificato**, selezionare il file del certificato del punto di distribuzione client esportato e specificare la password.  

5.  Ripetere i passaggi da 2 a 4 per tutti i punti di gestione e i punti di distribuzione dei siti primari che verranno usati con i computer Mac.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurare il punto proxy di registrazione e il punto di registrazione  
 È necessario installare entrambi questi ruoli del sistema del sito nello stesso sito, ma non occorre installarli nello stesso server del sistema del sito o nella stessa foresta Active Directory.  

 Per altre informazioni sul posizionamento del ruolo del sistema del sito e relative considerazioni, vedere [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Ruoli del sistema del sito) in [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Pianificare i server e i ruoli del sistema del sito per System Center Configuration Manager).  

 Queste procedure consentono di configurare i ruoli del sistema del sito per supportare i computer Mac.   

-   [Nuovo server di sistema del sito](#new-site-system-server)  

-   [Server di sistema del sito esistente](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>nuovo server del sistema del sito  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Configurazione del sito** > **Server e ruoli del sistema del sito**  

3.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito.  Assicurarsi di aver specificato un valore FQDN Internet. Se il server non è accessibile da Internet, usare il valore FQDN Intranet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto proxy di registrazione** e **Punto di registrazione** dall'elenco dei ruoli disponibili.  

6.  Nella pagina **Punto proxy di registrazione** rivedere le impostazioni e apportare eventuali modifiche necessarie.  

7.  Nella pagina **Enrollment Point Settings** (Impostazioni punto di registrazione) rivedere le impostazioni e apportare eventuali modifiche necessarie. Completare la procedura guidata.  

### <a name="existing-site-system-server"></a>server del sistema del sito esistente  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Configurazione del sito** > **Server e ruoli del sistema del sito** e scegliere il server che si vuole usare per supportare i computer Mac.  

3.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**. Assicurarsi di aver specificato un valore FQDN Internet. Se il server non è accessibile da Internet, usare il valore FQDN Intranet.   

5.  Nella pagina **Selezione ruolo del sistema** scegliere **Punto proxy di registrazione** e **Punto di registrazione** dall'elenco dei ruoli disponibili.  

6.  Nella pagina **Punto proxy di registrazione** rivedere le impostazioni e apportare eventuali modifiche necessarie.  

7.  Nella pagina **Enrollment Point Settings** (Impostazioni punto di registrazione) rivedere le impostazioni e apportare eventuali modifiche necessarie. Completare la procedura guidata.  

## <a name="install-the-reporting-services-point"></a>Installare il punto di Reporting Services  
 [Installare il punto di Reporting Services](../../../core/servers/manage/configuring-reporting.md) se si vuole eseguire report per i computer Mac.  

### <a name="next-steps"></a>Passaggi successivi

[Distribuire il client di Configuration Manager in computer Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).  
