---
title: Ruoli del sistema del sito per i client
titleSuffix: Configuration Manager
description: Determinare i ruoli del sistema del sito per i client in System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a7df7b8c1ff14e8783b6f988f315a477cc7065c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122118"
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Determinare i ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento può essere utile per determinare i ruoli del sistema del sito necessari per la distribuzione dei client di Configuration Manager:  

 Per altre informazioni sul percorso di installazione dei ruoli di sistema del sito necessari nella gerarchia, vedere [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Progettare una gerarchia di siti per System Center Configuration Manager).  

 Per altre informazioni sulla modalità di installazione e configurazione dei ruoli del sistema del sito necessari, vedere [Install site system roles](../../../../core/servers/deploy/configure/install-site-system-roles.md) (Installare i ruoli del sistema del sito).  

##  <a name="determine-if-you-need-a-management-point"></a>Stabilire se è necessario un punto di gestione  
 Per impostazione predefinita, tutti i computer client Windows usano un punto di distribuzione per installare il client di Configuration Manager e possono eseguire il fallback su un punto di gestione quando non è disponibile un punto di distribuzione. È tuttavia possibile installare i client Windows su computer da un'origine alternativa quando si usa la proprietà della riga di comando CCMSetup **/source:<Percorso\>**. Ad esempio, questa opzione potrebbe essere appropriata se si installano i client su Internet. Un altro possibile scenario è quando si vuole evitare l'invio di pacchetti di rete tra il computer e il punto di gestione durante l'installazione dei client, ad esempio a causa della presenza di un firewall che blocca le porte richieste o di una connessione con larghezza di banda ridotta. Tutti i client devono tuttavia comunicare con un punto di gestione per essere assegnati a un sito e gestiti da Configuration Manager.  

 Per altre informazioni sulla proprietà della riga di comando CCMSetup **/source:<Percorso\>**, vedere [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md) (Informazioni sulle proprietà di installazione del client in System Center Configuration Manager).  

 Quando si installa più di un punto di gestione nella gerarchia, i client si connettono automaticamente a un punto sulla base della loro appartenenza alla foresta e del percorso di rete. Non è possibile installare più di un punto di gestione in un sito secondario.  

 I client di computer Mac e i client di dispositivi mobili registrati con Configuration Manager richiedono sempre un punto di gestione per l'installazione client. Questo punto di gestione deve trovarsi in un sito primario, essere configurato per il supporto di dispositivi mobili e accettare le connessioni client da Internet. Questi client non possono utilizzare i punti di gestione in siti secondari o connettersi a punti di gestione in altri siti primari.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Stabilire se è necessario un punto di stato di fallback  
 È possibile usare un punto di stato di fallback per monitorare la distribuzione del client per i computer Windows. È anche possibile identificare i client Windows non gestiti perché non possono comunicare con un punto di gestione. I computer Mac, i dispositivi mobili registrati da Configuration Manager e i dispositivi mobili gestiti con il connettore Exchange Server non usano un punto di stato di fallback.  

 Non è richiesto un punto di stato di fallback per monitorare l'attività e lo stato dei client.  

 Il punto di stato di fallback comunica sempre con i client tramite HTTP, che usa connessioni non autenticate e invia i dati come testo non crittografato. In questo modo il punto di stato di fallback diventa vulnerabile ad attacchi, in particolare quando viene utilizzato con la gestione client basata su Internet. Per ridurre la superficie d'attacco, destinare sempre un server all'esecuzione del punto di stato di fallback e non installare altri ruoli del sistema del sito sullo stesso server in un ambiente di produzione.  

 Installare un punto di stato di fallback in presenza di tutte le condizioni seguenti:  

- Si desidera che gli errori di comunicazione client dai computer Windows siano inviati al sito, anche se questi computer client non possono comunicare con un punto di gestione.  

- Si vogliono usare i report di distribuzione client di Configuration Manager che visualizzano i dati inviati dal punto di stato di fallback.  

- Si dispone di un server dedicato per questo ruolo del sistema del sito e di ulteriori misure di sicurezza per proteggere il server da attacchi esterni.  

- I vantaggi dell'utilizzo di un punto di stato di fallback superano i rischi di protezione associati a connessioni non autenticate e trasferimenti di testo non crittografato nel traffico su HTTP.  

  Non installare un punto di stato di fallback se i rischi a livello di sicurezza dell'esecuzione di un sito Web con connessioni non autenticate e trasferimenti di testo non crittografato superano i vantaggi dell'identificazione dei problemi di comunicazione client.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Stabilire se è necessario un punto di Reporting Services  
 Configuration Manager offre molti report che consentono di monitorare l'installazione, l'assegnazione e la gestione dei client nella console di Configuration Manager. Alcuni dei report di distribuzione richiedono che i client siano assegnati a un punto di stato di fallback.  

 Sebbene i report non siano necessari per la distribuzione dei client e sia possibile visualizzare alcune informazioni sulla distribuzione nella console di Configuration Manager o vedere informazioni dettagliate tramite i file di log dei client, i report dei client offrono dettagli preziosi per il monitoraggio e la risoluzione dei problemi di distribuzione dei client.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Stabilire se è necessario un punto di registrazione e un punto proxy di registrazione  
 Configuration Manager richiede un punto di registrazione e un punto proxy di registrazione per registrare i dispositivi mobili e i certificati per computer Mac. Questi ruoli del sistema del sito non sono necessari se i dispositivi mobili saranno gestiti tramite il connettore Exchange Server, se si installa il client legacy del dispositivo mobile (ad esempio per Windows CE) oppure se si richiede e installa il certificato client in computer Mac indipendentemente da Configuration Manager.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Stabilire se è necessario un punto di distribuzione  
 Non è necessario un punto di distribuzione per installare i client di Configuration Manager in computer Windows. Per impostazione predefinita, tuttavia, Configuration Manager usa un punto di distribuzione per installare i file di origine client nei computer Windows, ma potrebbe ricorrere al download di questi file da un punto di gestione come soluzione di fallback. I punti di distribuzione non vengono usati per installare i client di dispositivi mobili registrati da Configuration Manager ma sono usati in caso di installazione del client legacy del dispositivo mobile. Se si installa il client di Configuration Manager nell'ambito della distribuzione di un sistema operativo, l'immagine del sistema operativo viene archiviata e recuperata da un punto di distribuzione.  

 Sebbene per l'installazione della maggior parte dei client di Configuration Manager non siano necessari punti di distribuzione, questi sono richiesti per l'installazione di software nei client, ad esempio applicazioni e aggiornamenti software.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Stabilire se è necessario un punto per siti Web del Catalogo applicazioni e un punto per servizi Web del Catalogo applicazioni  
 Il punto per siti Web del Catalogo applicazioni e il punto per servizi Web del Catalogo applicazioni non sono necessari per la distribuzione di client. Si potrebbe tuttavia volerli installare nell'ambito del processo di distribuzione client in modo da consentire agli utenti di eseguire le azioni seguenti al momento dell'installazione del client di Configuration Manager sui computer Windows:  

-   Cancellare i dati sui dispositivi mobili.  

-   Cercare e installare le applicazioni dal Catalogo applicazioni.  

-   Distribuire le applicazioni a utenti e dispositivi con scopo della distribuzione **Disponibile**.  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Stabilire se è necessario un punto di connessione del gateway di gestione cloud 

È necessario un punto di connessione del gateway di gestione cloud se si configura un [gateway di gestione cloud](/sccm/core/clients/manage/setup-cloud-management-gateway) per [gestire i client su Internet](/sccm/core/clients/manage/manage-clients-internet).


 
