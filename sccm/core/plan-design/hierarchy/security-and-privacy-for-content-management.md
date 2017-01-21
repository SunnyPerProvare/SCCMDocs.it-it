---
title: Sicurezza e privacy per la gestione dei contenuti | Microsoft Docs
description: "È possibile ottimizzare la protezione e la privacy per la gestione dei contenuti in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 44c45bf87d27da23da5e1dc7b047cbacc6d9903e


---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Sicurezza e privacy per la gestione dei contenuti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento contiene informazioni sulla sicurezza e la privacy per la gestione dei contenuti in System Center Configuration Manager. È possibile leggerlo insieme ai seguenti argomenti:  

-   [Sicurezza e privacy per la gestione delle applicazioni in System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Sicurezza e privacy per gli aggiornamenti software in System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Sicurezza e privacy per la distribuzione del sistema operativo in System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="a-namebkmksecuritycontentmanagementa-security-best-practices-for-content-management"></a><a name="BKMK_Security_ContentManagement"></a> Procedure di sicurezza consigliate per la gestione del contenuto  
 Utilizzare le seguenti procedure ottimali di protezione per la gestione dei contenuti:  

 **Per i punti di distribuzione in Intranet, considerare i vantaggi e gli svantaggi dell'utilizzo di HTTP e HTTPS** : nella maggior parte degli scenari, l'utilizzo di HTTP e degli account di accesso al pacchetto per l'autorizzazione offre una maggiore protezione rispetto all'utilizzo di HTTPS con la crittografia senza autorizzazione. Se tuttavia sono presenti dati sensibili nel contenuto da crittografare durante il trasferimento, utilizzare HTTPS.  

-   **Quando si usa HTTPS per un punto di distribuzione**, Configuration Manager non usa gli account di accesso al pacchetto per autorizzare l'accesso al contenuto, ma il contenuto viene crittografato durante il trasferimento in rete.  

-   **Quando si usa HTTP per un punto di distribuzione**, è possibile usare gli account di accesso al pacchetto per l'autorizzazione, ma il contenuto non viene crittografato durante il trasferimento in rete.  


**Se si usa un certificato di autenticazione client PKI al posto di un certificato autofirmato per il punto di distribuzione, proteggere il file del certificato (con estensione PFX) con una password complessa. Se si archivia il file in rete, proteggere il canale di rete quando si importa il file in Configuration Manager**: impostando la richiesta di una password per importare il certificato di autenticazione client usato per la comunicazione tra il punto di distribuzione e i punti di gestione, il certificato viene protetto da potenziali attacchi. Utilizzare la firma SMB o IPsec tra il percorso di rete e il server del sito per impedire all'autore di un attacco di manomettere il file di certificato.  

**Rimuovere il ruolo di punto di distribuzione dal server del sito** : per impostazione predefinita, un punto di distribuzione è installato nello stesso server come server del sito. I client non devono comunicare direttamente con il server del sito, perciò, per ridurre la superficie di attacco. assegnare il ruolo del punto di distribuzione ad altri sistemi del sito e rimuoverlo dal server del sito.  

**Proteggere il contenuto a livello di accesso al pacchetto** : la condivisione del punto di distribuzione consente l'accesso in lettura a tutti gli utenti. Per limitare gli utenti che possono accedere al contenuto, utilizzare gli account di accesso al pacchetto durante la configurazione del punto di distribuzione per HTTP. Questa opzione non viene applicata ai punti di distribuzione basati sul cloud, che non supportano gli account di accesso ai pacchetti. Per altre informazioni sugli account di accesso al pacchetto, vedere [Gestire gli account per accedere al contenuto](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Se Configuration Manager installa IIS durante l'aggiunta di un ruolo del sistema del sito del punto di distribuzione, rimuovere Reindirizzamento HTTP e Strumenti e script di gestione IIS quando l'installazione del punto di distribuzione è completata**: il punto di distribuzione non richiede il reindirizzamento HTTP né gli strumenti e gli script di gestione IIS. Per ridurre la superficie di attacco, rimuovere questi servizi ruolo per il ruolo server Web (IIS).  Per altre informazioni sui servizi ruolo per il ruolo server Web (IIS) per i punti di distribuzione, vedere l'argomento relativo ai [prerequisiti dei siti e dei sistemi del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

**Impostare le autorizzazioni di accesso al pacchetto durante la creazione del pacchetto** : poiché le modifiche apportate agli account di accesso nei file del pacchetto diventano effettive solo quando il pacchetto viene ridistribuito, impostare con attenzione le autorizzazioni di accesso al pacchetto quando si crea il pacchetto per la prima volta. Ciò è particolarmente importante quando il pacchetto è grande o viene distribuito a molti punti di distribuzione e quando la capacità di larghezza di banda di rete per la distribuzione del contenuto è limitata.  

**Implementare i controlli di accesso per proteggere i supporti che contengono il contenuto pre-installato** : il contenuto pre-installato viene compresso ma non crittografato. L'autore di un attacco potrebbe leggere e modificare i file che vengono scaricati dai dispositivi. I client di Configuration Manager rifiuteranno il contenuto manomesso, ma lo scaricano comunque.  

**Importare il contenuto pre-installato usando solo lo strumento della riga di comando ExtractContent (ExtractContent.exe) accluso a Configuration Manager e verificare che sia firmato da Microsoft**: per evitare la manomissione e l'elevazione dei privilegi, usare solo lo strumento della riga di comando accluso a Configuration Manager.  

**Proteggere il canale di comunicazione tra il server del sito e il percorso di origine del pacchetto** : usare la firma SMB o IPsec tra il server del sito e il percorso di origine del pacchetto quando si creano applicazioni e pacchetti. In questo modo è possibile impedire all'autore di un attacco di manomettere i file di origine.  

**Se si modifica l'opzione di configurazione del sito per usare un sito Web personalizzato al posto del sito Web predefinito dopo l'installazione di punti di distribuzione, rimuovere le directory virtuali predefinite**: quando si passa dall'uso del sito Web predefinito all'uso di un sito Web personalizzato, Configuration Manager non rimuove le directory virtuali usate in precedenza. Rimuovere le directory virtuali create in origine da Configuration Manager nel sito Web predefinito:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Per i punti di distribuzione basati sul cloud, proteggere i dettagli della sottoscrizione e i certiificati** : quando si usano punti di distribuzione basati sul cloud, proteggere gli elementi importanti, inclusi il nome utente e la password per la sottoscrizione di Azure, il certificato di gestione di Azure e il certificato di servizio del punto di distribuzione basato sul cloud. Archiviare i certificati in modo protetto e se vengono selezionati dalla rete durante la configurazione del punto di distribuzione basato sul cloud, utilizzare la firma SMB o IPsec tra il server del sistema del sito e il percorso di origine.  

**Per i punti di distribuzione basati sul cloud: per la continuità del servizio, monitorare la data di scadenza dei certificati**: Configuration Manager non avvisa l'utente quando i certificati importati per la gestione del servizio punto di distribuzione basato sul cloud sta per scadere. È necessario monitorare le date di scadenza indipendentemente da Configuration Manager e assicurarsi di effettuare il rinnovo, quindi importare il nuovo certificato prima della data di scadenza. Questa operazione è importante specialmente se si acquista un certificato di servizio del punto di distribuzione basato sul cloud di Configuration Manager da un'autorità di certificazione (CA) esterna, perché potrebbe richiedere altro tempo per ottenere un certificato rinnovato.  

 Se un certificato scade, **Gestione servizi cloud** genera l'ID messaggio di stato **9425** e il file **CloudMgr.log** contiene una voce per indicare che il certificato **is in expired state**, con la data di scadenza registrata in base all'ora UTC.  

## <a name="security-considerations-for-content-management"></a>Considerazioni sulla sicurezza per la gestione del contenuto  
Considerare quanto segue durante la pianificazione della gestione del contenuto:  

-   I client convalidano il contenuto solo dopo che è stato scaricato  

     I client di Configuration Manager convalidano l'hash nel contenuto solo dopo che è stato scaricato nella cache del client. Se l'autore di un attacco manomette l'elenco dei file da scaricare o il contenuto stesso, il processo di download può richiedere una larghezza di banda di rete considerevole affinché il client scarti il contenuto quando incontra l'hash non valido.  

-   Quando si usano i punti di distribuzione basati sul cloud, l'accesso al contenuto viene automaticamente limitato all'azienda e non è possibile limitarlo ulteriormente per gruppi o utenti selezionati.  

-   Quando si usano i punti di distribuzione basati sul cloud, i client vengono autenticati dal punto di gestione e quindi usano un token di Configuration Manager per accedere ai punti di distribuzione basati sul cloud. Il token è valido per 8 ore, perciò anche se si blocca un client perché non è più attendibile, può continuare a scaricare il contenuto da un punto di distribuzione basato sul cloud finché il periodo di validità del token non scade. Al termine di questo periodo, il punto di gestione non creerà un altro token per il client perché il client è bloccato.  

     Per evitare che un client bloccato scarichi il contenuto in questo periodo di 8 ore, è possibile arrestare il servizio cloud dal nodo **Cloud**, **Configurazione della gerarchia**, nell'area di lavoro **Amministrazione** della console di Configuration Manager.  

##  <a name="a-namebkmkprivacycontentmanagementa-privacy-information-for-content-management"></a><a name="BKMK_Privacy_ContentManagement"></a> Informazioni sulla privacy per la gestione dei contenuti  
 Configuration Manager non include dati utente nei file di contenuto, tuttavia un utente amministratore può scegliere di inserirli.  

 Prima di configurare la gestione dei contenuti, considerare i requisiti sulla privacy.  



<!--HONumber=Dec16_HO3-->


