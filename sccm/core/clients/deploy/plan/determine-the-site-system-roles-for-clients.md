---
title: Ruoli del sistema del sito per i client | System Center Configuration Manager
description: Determinare i ruoli del sistema del sito per i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 17f28ff5addfbfbab251bdb72be9b405487d1403


---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Determinare i ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le informazioni contenute in questo articolo consentono di determinare i sistemi del sito necessari per la distribuzione dei client di Configuration Manager:  

 Per altre informazioni sul percorso di installazione dei ruoli di sistema del sito necessari nella gerarchia, vedere [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Progettare una gerarchia di siti per System Center Configuration Manager).  

 Per altre informazioni sulla modalità di installazione e configurazione dei ruoli del sistema del sito necessari, vedere [Install site system roles](../../../../core/servers/deploy/configure/install-site-system-roles.md) (Installare i ruoli del sistema del sito).  

##  <a name="a-namebkmkdeterminempa-determine-whether-you-require-a-management-point"></a><a name="BKMK_Determine_MP"></a> Determinare se è necessario un punto di gestione  
 Per impostazione predefinita, tutti i computer client Windows usano un punto di distribuzione per installare il client di Configuration Manager e possono ricorrere a un punto di gestione quando non è disponibile un punto di distribuzione. È tuttavia possibile installare i client Windows su computer da un'origine alternativa quando si usa la proprietà della riga di comando CCMSetup **/source:<Percorso\>**. Ad esempio, questa opzione potrebbe essere appropriata se si installano i client su Internet. Un altro possibile scenario è quando si desidera evitare l'invio di pacchetti di rete tra il computer e il punto di gestione durante l'installazione dei client a causa, ad esempio, di un firewall che blocca le porte richieste per il metodo di installazione adottato o di una connessione con larghezza di banda ridotta. Tutti i client devono tuttavia comunicare con un punto di gestione per essere assegnati a un sito e gestiti da Configuration Manager.  

 Per altre informazioni sulla proprietà della riga di comando CCMSetup **/source:<Percorso\>**, vedere [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md) (Informazioni sulle proprietà di installazione del client in System Center Configuration Manager).  

 Quando si installa più di un punto di gestione nella gerarchia, i client si collegano automaticamente a quello più appropriato sulla base della loro appartenenza alla foresta e del percorso di rete. Non è possibile installare più di un punto di gestione in un sito secondario.  

 I client di computer Mac e i client di dispositivi mobili registrati con Configuration Manager richiedono sempre un punto di gestione per l'installazione client. Questo punto di gestione deve trovarsi in un sito primario, essere configurato per il supporto di dispositivi mobili e accettare le connessioni client da Internet. Questi client non possono utilizzare i punti di gestione in siti secondari o connettersi a punti di gestione in altri siti primari.  

##  <a name="a-namebkmkdeterminefspa-determine-whether-you-require-a-fallback-status-point"></a><a name="BKMK_Determine_FSP"></a> Determinare se è necessario un punto di stato di fallback  
 È possibile utilizzare un punto di stato di fallback per controllare la distribuzione dei client per i computer Windows e individuare i client su quei computer non gestiti a causa della mancata comunicazione con un punto di gestione. I computer Mac, i dispositivi mobili registrati da Configuration Manager e i dispositivi mobili gestiti con il connettore Exchange Server non usano un punto di stato di fallback.  

> [!NOTE]  
>  Non è richiesto un punto di stato di fallback per monitorare l'attività e lo stato dei client.  

 Il punto di stato di fallback comunica sempre con i client tramite HTTP, che utilizza connessioni non autenticate e invia dati sotto forma di testo non crittografato. In questo modo il punto di stato di fallback diventa vulnerabile ad attacchi, in particolare quando viene utilizzato con la gestione client basata su Internet. Per ridurre la superficie d'attacco, destinare sempre un server all'esecuzione del punto di stato di fallback e non installare altri ruoli del sistema del sito sullo stesso server in un ambiente di produzione.  

 Installare un punto di stato di fallback in presenza di tutte le condizioni seguenti:  

-   Si desidera che gli errori di comunicazione client dai computer Windows siano inviati al sito, anche se questi computer client non possono comunicare con un punto di gestione.  

-   Si vogliono usare i report di distribuzione client di Configuration Manager che visualizzano i dati inviati dal punto di stato di fallback.  

-   Si dispone di un server dedicato per questo ruolo del sistema del sito e di ulteriori misure di sicurezza per proteggere il server da attacchi esterni.  

-   I vantaggi dell'utilizzo di un punto di stato di fallback superano i rischi di protezione associati a connessioni non autenticate e trasferimenti di testo non crittografato nel traffico su HTTP.  

 Non installare un punto di stato di fallback in presenza delle seguenti condizioni:  

-   I rischi di protezione dell'esecuzione di un sito Web con connessioni non autenticate e trasferimenti di testo non crittografato superano i vantaggi dell'identificazione dei problemi di comunicazione client.  

##  <a name="a-namebkmkdeterminerspa-determine-whether-you-require-a-reporting-services-point"></a><a name="BKMK_Determine_RSP"></a> Determinare se è necessario un punto di Reporting Services  
 Configuration Manager offre molti report che consentono di monitorare l'installazione, l'assegnazione e la gestione dei client nella console di Configuration Manager. Alcuni dei report di distribuzione richiedono che i client siano assegnati a un punto di stato di fallback.  

 Sebbene i report non siano necessari per la distribuzione dei client e sia possibile visualizzare alcune informazioni sulla distribuzione nella console di Configuration Manager o vedere le informazioni dettagliate tramite i file di log dei client, i report dei client specificano dettagli preziosi per il monitoraggio e la risoluzione dei problemi di distribuzione dei client.  

##  <a name="a-namebkmkdetermineenrollmentpointsa-determine-whether-you-require-an-enrollment-point-and-an-enrollment-proxy-point"></a><a name="BKMK_Determine_EnrollmentPoints"></a> Determinare se è necessario un punto di registrazione e un punto proxy di registrazione  
 Configuration Manager richiede un punto di registrazione e un punto proxy di registrazione per registrare i dispositivi mobili e i certificati per computer Mac. Questi ruoli del sistema del sito non sono necessari se i dispositivi mobili saranno gestiti tramite il connettore Exchange Server, se si installa il client legacy del dispositivo mobile (ad esempio per Windows CE) oppure se si richiede e si installa il certificato client su computer Mac indipendentemente da Configuration Manager.  

##  <a name="a-namebkmkdeterminedpa-determine-whether-you-require-a-distribution-point"></a><a name="BKMK_Determine_DP"></a> Determinare se è necessario un punto di distribuzione  
 Sebbene non sia obbligatorio un punto di distribuzione per installare i client di Configuration Manager su computer Windows, per impostazione predefinita Configuration Manager usa un punto di distribuzione per installare i file di origine client sui computer Windows ma può tentare di scaricare questi file da un punto di gestione. I punti di distribuzione non vengono usati per installare i client di dispositivi mobili registrati da Configuration Manager ma sono usati in caso di installazione del client legacy del dispositivo mobile. Se si installa il client di Configuration Manager nell'ambito della distribuzione di un sistema operativo, l'immagine del sistema operativo viene archiviata e recuperata da un punto di distribuzione.  

 Sebbene per l'installazione della maggior parte dei client di Configuration Manager non siano obbligatori punti di distribuzione, questi sono necessari per installare il software, ad esempio applicazioni e aggiornamenti software, nei client.  

##  <a name="a-namebkmkdetermineapplicationcatalogpointsa-determine-whether-you-require-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a><a name="BKMK_Determine_ApplicationCatalogPoints"></a> Determinare se è necessario un punto per siti Web del Catalogo applicazioni e un punto per servizi Web del Catalogo applicazioni  
 Il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni non sono richiesti per la distribuzione di client. Si potrebbe tuttavia volerli installare nell'ambito del processo di distribuzione client in modo da consentire agli utenti di eseguire le azioni seguenti al momento dell'installazione del client di Configuration Manager sui computer Windows:  

-   Cancellare i dati sui dispositivi mobili.  

-   Cercare e installare le applicazioni dal Catalogo applicazioni.  

-   Distribuire le applicazioni a utenti e dispositivi con scopo della distribuzione **Disponibile**.  



<!--HONumber=Nov16_HO1-->


