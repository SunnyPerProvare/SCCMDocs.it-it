---
title: "Supporto per le funzionalità di Windows | Microsoft Docs"
description: "Informazioni su quali funzionalità di Windows e di rete sono supportate in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 29e4f8a70b56b772a54ee858a392533780ccbaf9


---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Supporto per le funzionalità e le reti Windows in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento viene illustrato il supporto di System Center Configuration Manager per le funzionalità comuni di Windows e di rete.  


##  <a name="a-namebkmkbranchcachea-branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  
Windows BranchCache è stato integrato in Configuration Manager. È possibile configurare le impostazioni di BranchCache su un tipo di distribuzione per le applicazioni, sulla distribuzione per un pacchetto e per le sequenze attività.  

Quando vengono soddisfatti tutti i requisiti per BranchCache, questa funzionalità abilita i client in remoto per ottenere contenuto da client locali che hanno una cache corrente del contenuto.  

Ad esempio, quando il primo computer client abilitato per BranchCache richiede contenuto da un punto di distribuzione configurato come server BranchCache, il computer client scarica il contenuto e lo memorizza nella cache. Tale contenuto è quindi reso disponibile ai client presenti sulla stessa subnet che richiedono questo stesso contenuto e tali client memorizzano anche il contenuto nella cache. In tal modo, client successivi sulla stessa subnet non devono scaricare contenuto dal punto di distribuzione e il contenuto viene distribuito tra più client per trasferimenti futuri.  

**Per supportare BranchCache con Configuration Manager:**  

-   Aggiungere la funzionalità **Windows BranchCache** al server di sistema del sito configurato come un punto di distribuzione.  

    -   I punti di distribuzione nei server configurati per supportare BranchCache non richiedono alcuna configurazione aggiuntiva.  

    -   Non è possibile aggiungere Windows BranchCache a un punto di distribuzione basato su cloud, ma i punti di distribuzione basati su cloud supportano il download del contenuto da parte dei client configurati per Windows BranchCache.  

**Per consentire ai client di usare BranchCache:**  

-   I client che possono supportare BranchCache devono essere configurati per la modalità distribuita di BranchCache  

-   L'impostazione del sistema operativo per le impostazioni client BITS deve essere abilitata per supportare BranchCache  

**Con Windows BranchCache sono supportati i seguenti sistemi operativi client:**  

|Sistema operativo|Dettagli sul supporto|  
|----------------------|---------------------|  
|Windows 7 con SP1|Supportato per impostazione predefinita|  
|Windows 8|Supportato per impostazione predefinita|  
|Windows 8.1|Supportato per impostazione predefinita|  
|Windows 10|Supportato per impostazione predefinita|  
|Windows Server 2008 con SP2|**Richiede BITS 4.0**: è possibile installare BITS 4.0 nei client di Configuration Manager usando gli aggiornamenti software o la distribuzione del software. Per altre informazioni su BITS 4.0, vedere [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> Su questo sistema operativo, la funzionalità client BranchCache non è supportata per la distribuzione di software eseguita dalla rete o per i trasferimenti di file SMB. Inoltre, questo sistema operativo non può usare la funzionalità BranchCache con punti di distribuzione basati su cloud.|  
|Windows Server 2008 R2|Supportato per impostazione predefinita|  
|Windows Server 2012|Supportato per impostazione predefinita|  
|Windows Server 2012 R2|Supportato per impostazione predefinita|  

 Per altre informazioni su BranchCache, vedere [BranchCache per Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) nella documentazione di Windows Server.  

##  <a name="a-namebkmkworkgroupsa-computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Computer in gruppi di lavoro  
Configuration Manager offre il supporto per i client in gruppi di lavoro.  

-   Configuration Manager supporta lo spostamento di un client da un gruppo di lavoro a un dominio o da un dominio a un gruppo di lavoro. Per altre informazioni, vedere la sezione [How to Install Configuration Manager Clients on Workgroup Computers](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) (Come installare i client di Configuration Manager in computer di gruppi di lavoro) nell'argomento [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md) (Come distribuire client a computer Windows in System Center Configuration Manager).  

> [!NOTE]  
>  Nonostante i clienti nei gruppi di lavoro siano supportati, tutti i sistemi del sito devono essere membri di un dominio Active Directory supportato.  


##  <a name="a-namebkmmkdatadedupa-data-deduplication"></a><a name="bkmmk_datadedup"></a> Deduplicazione dati  
Configuration Manager supporta l'uso della deduplicazione dati con punti di distribuzione nei sistemi operativi seguenti:  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  Non è possibile contrassegnare i file di origine del pacchetto host per la deduplicazione dei dati perché la deduplicazione dati usa reparse point e Configuration Manager non supporta l'uso di un percorso di origine del contenuto con file archiviati nei reparse point.  

Per altre informazioni, vedere [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) (Deduplicazione dati dei punti di distribuzione di Configuration Manager e di Windows Server 2012) nel blog del team di Configuration Manager e [Panoramica di Deduplicazione dati](http://technet.microsoft.com/library/hh831602.aspx) nella libreria TechNet di Windows Server.  

##  <a name="a-namebkmkdaa-directaccess"></a><a name="bkmk_DA"></a> DirectAccess  
Configuration Manager supporta la funzionalità DirectAccess in Windows Server 2008 R2 per la comunicazione tra client e server del sistema del sito.  

-   Quando vengono soddisfatti tutti i requisiti per DirectAccess tramite questa funzionalità, i client di Configuration Manager su Internet possono comunicare con il relativo sito assegnato come se fossero nella Intranet.  

-   Per le azioni avviate dal server, ad esempio il controllo remoto e l’installazione push client, il computer di origine (ad esempio il server del sito) deve eseguire IPv6 e questo protocollo deve essere supportato in tutti i dispositivi di rete.  

Configuration Manager non supporta le operazioni seguenti su DirectAccess:  

-   Distribuzione dei sistemi operativi  

-   Comunicazione tra siti di Configuration Manager  

-   Comunicazione tra server del sistema del sito di Configuration Manager all'interno di un sito  

##  <a name="a-namebkmkdualboota-dual-boot-computers"></a><a name="bkmk_dualboot"></a> Computer ad avvio doppio  
 Configuration Manager non può gestire più di un sistema operativo in un singolo computer. Se in un computer è presente più di un sistema operativo da gestire, regolare i metodi di individuazione e installazione usati per accertarsi che il client di Configuration Manager sia installato solo sul sistema operativo che deve essere gestito.  

##  <a name="a-namebkmkipv6a-internet-protocol-version-6"></a><a name="bkmk_IPv6"></a> Internet Protocol versione 6  
 Oltre a al protocollo IP versione 4 (IPv4), Configuration Manager supporta il protocollo IPv6 con le eccezioni seguenti:  

|Funzione|Eccezione per il supporto di IPv6|  
|--------------|-------------------------------|  
|Punti di distribuzione basati su cloud|IPv4 è necessario per supportare Microsoft Azure e i punti di distribuzione basati su cloud.|  
|Dispositivi mobili registrati da Microsoft Intune e Microsoft Service Connector|IPv4 è necessario per supportare i dispositivi mobili registrati da Microsoft Intune e da Microsoft Service Connector.|  
|Individuazione rete|IPv4 è obbligatorio quando si configura un server DHCP per la ricerca nell'individuazione di rete.|  
|Distribuzione del sistema operativo|IPv4 è necessario per supportare la distribuzione del sistema operativo.|  
|Comunicazione del proxy di riattivazione|IPv4 è necessario per supportare i pacchetti proxy di riattivazione del client.|  
|Windows CE|IPv4 è necessario per supportare il client di Configuration Manager nei dispositivi Windows CE.|  

##  <a name="a-namebkmknata-network-address-translation"></a><a name="bkmk_NAT"></a> Network Address Translation  
 Network Address Translation (NAT) non è supportato in Configuration Manager, a meno che il sito supporti i client presenti in Internet e il client rilevi che è connesso a Internet. Per altre informazioni sulla gestione client basata su Internet, vedere [Plan for managing Internet-based clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md) (Pianificare la gestione di client basata su Internet in System Center Configuration Manager).  

##  <a name="a-namebkmkstoragea-specialized-storage-technology"></a><a name="bkmk_storage"></a> Tecnologia di archiviazione specializzata  
 Configuration Manager funziona con qualsiasi hardware certificato nell'Hardware Compatibility List di Windows per la versione del sistema operativo su cui è installato il componente di Configuration Manager. I ruoli server del sito richiedono file system NTFS in modo che sia possibile impostare le autorizzazioni directory e file. Poiché Configuration Manager presuppone di avere la proprietà completa di un'unità logica, i sistemi del sito eseguiti in computer separati non possono condividere una partizione logica in una tecnologia di archiviazione. Tuttavia, ogni computer può usare una partizione logica separata nella stessa partizione fisica di un dispositivo di archiviazione condivisa.  

 **Considerazioni sul supporto:**  

-   **Storage Area Network**: una rete SAN (Storage Area Network) è supportata quando un server basato su Windows supportato è collegato direttamente al volume ospitato dalla SAN.  

-   **Single Instance Storage**: Configuration Manager non supporta la configurazione di cartelle di pacchetto punto di distribuzione e firma in un volume compatibile con Single Instance Storage (SIS).  

     La cache di un client di Configuration Manager non è supportata in un volume compatibile con SIS.  

-   **Unità disco rimovibile**: Configuration Manager non supporta l'installazione del sistema del sito o dei client di Configuration Manager in un'unità disco rimovibile.  



<!--HONumber=Dec16_HO3-->


