---
title: Certificati per il gateway di gestione cloud
description: Informazioni sui diversi certificati digitali da usare con il gateway di gestione cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: fbae44d1344dd36d3c0a6faf2e50727dfa830ba0
ms.sourcegitcommit: 8060ea520fb08629e1d5f249daffe825536673a5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2018
ms.locfileid: "35232371"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificati per il gateway di gestione cloud

*Si applica a: System Center Configuration Manager (Current Branch)*

In base allo scenario in cui si gestiscono i client su Internet con il gateway di gestione cloud, è necessario usare uno o più certificati digitali. Per altre informazioni sui diversi scenari, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="cmg-server-authentication-certificate"></a>Certificato di autenticazione server del gateway di gestione cloud

*Questo certificato è necessario in tutti gli scenari.*

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione cloud crea un servizio HTTPS a cui si connettono i client basati su Internet. Il server richiede un certificato di autenticazione server per compilare il canale sicuro. Acquistare un certificato per questo scopo da un provider pubblico o inviarlo dall'infrastruttura a chiave pubblica. Per altre informazioni, vedere [Certificato radice trusted del gateway di gestione cloud per i client](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Questo certificato richiede un nome univoco globale per identificare il servizio in Azure. Prima di richiedere un certificato, verificare che il nome di dominio di Azure sia univoco. Ad esempio, *GraniteFalls.CloudApp.Net*. Accedere al [portale di Microsoft Azure](https://portal.azure.com). Fare clic su **Crea una risorsa**, selezionare la categoria **Calcolo**, quindi fare clic su **Servizio cloud**. Digitare un prefisso nel campo **Nome DNS**, ad esempio *GraniteFalls*. L'interfaccia indica se il nome di dominio è disponibile o se è già in uso in un altro servizio. Non creare il servizio nel portale, usare questo processo per verificare la disponibilità del nome. 
  
 > [!NOTE]
 > A partire dalla versione 1802, il certificato di autenticazione server del gateway di gestione cloud supporta i caratteri jolly. Alcune autorità di certificazione rilasciano certificati in cui viene usato un carattere jolly per il nome host. Ad esempio, **\*.contoso.com**. Alcune organizzazioni usano certificati con caratteri jolly per semplificare l'infrastruttura a chiave pubblica e ridurre i costi di manutenzione.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificato radice trusted del gateway di gestione cloud per i client

I client devono considerare attendibile il certificato di autenticazione server del gateway di gestione cloud. Esistono due metodi per confermare l'attendibilità:
- Usare un certificato di un provider pubblico considerato attendibile a livello globale. Ad esempio, tra gli altri, DigiCert, Thawte, o VeriSign. I client Windows includono le autorità di certificazione (CA) che rilasciano i certificati radice trusted da questi provider. Usando un certificato di autenticazione server rilasciato da uno di questi provider, i client confermano automaticamente l'attendibilità. 
- Usare un certificato rilasciato da un'autorità di certificazione globale (enterprise) dall'infrastruttura a chiave pubblica. Nella maggior parte delle implementazioni di infrastruttura a chiave pubblica di tipo Enterprise le autorità di certificazione radice attendibili vengono aggiunte ai client di Windows. Ad esempio, usando i servizi certificati Active Directory con criteri di gruppo. Se si rilascia il certificato di autenticazione server per il gateway di gestione cloud da un'autorità di certificazione che i client non considerano automaticamente attendibile, è necessario aggiungere il certificato radice trusted di tale autorità ai client basati su Internet.
    - È inoltre possibile usare i profili dei certificati di Configuration Manager per eseguire il provisioning dei certificati nei client. Per altre informazioni, vedere l'[introduzione alle raccolte](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificato di autenticazione server rilasciato da un provider pubblico

Quando si usa questo metodo, i client considereranno automaticamente attendibile il certificato e non è necessario creare un certificato personalizzato. Configuration Manager crea il servizio in Azure con il dominio cloudapp.net. Un provider di certificati pubblico non può emettere un certificato con lo stesso nome per l'utente. Usare la seguente procedura per creare un alias DNS:

1. Creare un record di nome canonico (CNAME) nel DNS pubblico dell'organizzazione. Questo record crea un alias per il gateway di gestione cloud con un nome descrittivo usato dall'utente nel certificato pubblico.
Ad esempio, Contoso assegna al gateway di gestione cloud il nome **GraniteFalls**, che diventa **GraniteFalls.CloudApp.Net** in Azure. Nello spazio dei nomi contoso.com del DNS pubblico di Contoso l'amministratore DNS crea un nuovo record CNAME **GraniteFalls.Contoso.com** per il nome host effettivo, **GraniteFalls.CloudApp.net**.
2. Richiedere un certificato di autenticazione server da un provider pubblico usando il nome comune dell'alias CNAME.
Ad esempio, Contoso usa **GraniteFalls.Contoso.com** per il nome comune del certificato.
3. Creare il gateway di gestione cloud nella console di Configuration Manager usando questo certificato. Nella pagina **Impostazioni** della Creazione guidata del gateway di gestione cloud: 
    - Quando si aggiunge il certificato del server per questo servizio cloud (da **File di certificato**), la procedura guidata estrae il nome host dal nome comune del certificato come nome del servizio. 
    - Aggiunge quindi tale nome host a **cloudapp.net** o **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti come FQDN del servizio per creare il servizio in Azure.
    - Ad esempio, quando Contoso crea il gateway di gestione cloud, Configuration Manager estrae il nome host **GraniteFalls** dal nome comune del certificato. Azure crea il servizio effettivo come **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise

Creare un certificato SSL personalizzato per il gateway di gestione cloud identico a quello di un punto di distribuzione cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) procedendo in modo diverso per le operazioni seguenti:

- Quando si richiede il certificato del server Web personalizzato, specificare un FQDN per il nome comune del certificato. Per usare il gateway di gestione cloud nel cloud pubblico di Azure, usare un nome che termina con **cloudapp.net** o **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti.



## <a name="azure-management-certificate"></a>Certificato di gestione di Azure

*Questo certificato è obbligatorio per le distribuzioni di servizi classiche. Non è necessario per le distribuzioni di Azure Resource Manager.*

Specificare questo certificato nel portale di Azure quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Per creare il gateway di gestione cloud in Azure, il punto di connessione del servizio Configuration Manager deve prima eseguire l'autenticazione alla sottoscrizione di Azure. Quando si usa una distribuzione classica del servizio, per l'autenticazione viene usato il certificato di gestione di Azure. Un amministratore di Azure carica questo certificato nella sottoscrizione dell'utente. Quando si crea il gateway di gestione cloud nella console di Configuration Manager specificare questo certificato.

Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:

- [Servizi cloud e certificati di gestione](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Caricare un certificato di gestione dei servizi di Azure](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Usare questo certificato per creare il gateway di gestione cloud nella console di Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificato di autenticazione client

*Questo certificato è necessario per i client basati su Internet che eseguono Windows 7, Windows 8.1 e dispositivi Windows 10 che non fanno parte di Azure Active Directory (Azure AD). È necessario anche per il punto di connessione del gateway di gestione cloud. Non è richiesto per i client Windows 10 aggiunti ad Azure AD.*

I client usano questo certificato per l'autenticazione con il gateway di gestione cloud. I dispositivi Windows 10 ibridi o aggiunti a un dominio cloud non richiedono questo certificato perché usano Azure AD per l'autenticazione.

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare i certificati di autenticazione client. Per altre informazioni, vedere [Distribuzione del certificato client per computer Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificato radice trusted del client per il gateway di gestione cloud

*Questo certificato è necessario quando si usano i certificati di autenticazione client. Quando tutti i client usano Azure AD per l'autenticazione, questo certificato non è obbligatorio.* 

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione client deve considerare attendibile il certificato di autenticazione del client. Per confermare l'attendibilità, specificare la catena di certificati radice trusted. È possibile specificare due autorità di certificazione radice attendibili e quattro autorità intermedie (subordinate). 


#### <a name="export-the-client-certificates-trusted-root"></a>Esportare la radice attendibile del certificato client

Dopo aver emesso un certificato di autenticazione client per un computer, usare questo processo in tale computer per esportare la radice attendibile.

1.  Aprire il menu Start. Digitare "esegui" per aprire la finestra di esecuzione. Aprire **mmc**. 

2.  Dal menu file scegliere **Aggiungi/Rimuovi snap-in**.

3.  Nella finestra di dialogo Aggiungi o rimuovi snap-in selezionare **Certificati**, quindi fare clic su **Aggiungi**. 
    a. Nella finestra di dialogo Snap-in certificati selezionare **Account del computer** e fare clic su **Avanti**. 
    b. Nella finestra di dialogo Selezione computer selezionare **Computer locale** e quindi fare clic su **Fine**. 
    c. Nella finestra di dialogo Aggiungi o rimuovi snap-in fare clic su **OK**.

4.  Espandere **Certificati**, espandere **Personale** e selezionare **Certificati**.

5.  Selezionare un certificato il cui scopo designato è **Autenticazione client**. 
    a. Dal menu Azione selezionare **Apri**. 
    b. Passare alla scheda **Percorso certificazione**. c. Selezionare il certificato successivo procedendo verso l'alto nella catena, quindi gare clic su **Visualizza certificato**.

6.  Nella nuova finestra di dialogo Certificato passare alla scheda **Dettagli**. Fare clic su **Copia su file**.

7.  Completare l'Esportazione guidata certificati usando il formato di certificato predefinito, **DER encoded binary X.509 (.CER)**. Prendere nota del nome e del percorso del certificato esportato.

8. Esportare tutti i certificati presenti nel percorso di certificazione del certificato di autenticazione client originale. Prendere nota dei certificati esportati che rappresentano autorità di certificazione intermedie e di quelli che rappresentano autorità radice attendibili.



## <a name="enable-management-point-for-https"></a>Abilitare i punti di gestione per HTTPS

*Requisiti relativi ai certificati*
- Nelle versioni 1706 o 1710, quando si gestiscono client tradizionali con identità locale usando un certificato di autenticazione client, questo certificato è consigliato ma non obbligatorio.
- Nella versione 1710, quando si gestiscono i client Windows 10 aggiunti ad Azure AD, questo certificato è obbligatorio per i punti di gestione. 
- A partire dalla versione 1802 questo certificato è necessario in tutti gli scenari. Solo i punti di gestione abilitati per il gateway di gestione cloud devono essere HTTPS. Questa modifica del comportamento offre un supporto migliore per l'autenticazione basata su token di Azure AD. 

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare un certificato del server Web. Per altre informazioni, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Passaggi successivi

- [Configurare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Domande frequenti sul gateway di gestione cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Sicurezza e privacy per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
