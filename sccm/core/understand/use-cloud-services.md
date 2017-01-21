---
title: Usare i servizi cloud | Microsoft Docs
description: Il provisioning delle risorse cloud per System Center Configuration Manager consente di integrare l&quot;infrastruttura locale.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 539ad555b85b7517507c21718dab0b79fdf4dfb8


---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Usare i servizi cloud con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supporta diverse opzioni basate su cloud che integrano l'infrastruttura locale e consentono di risolvere problemi aziendali quali:  

-   Gestire la strategia BYOD usando Intune per la gestione dei dispositivi mobili  

-   Fornire risorse di contenuto a client isolati o risorse della rete Intranet, all'esterno del firewall aziendale (usando i punti di distribuzione basati su cloud)  

-   Scalare in orizzontale l'infrastruttura quando l'hardware fisico non è disponibile o logicamente inserito per supportare le proprie esigenze (usando macchine virtuali di Microsoft Azure)  

Anche se non è necessario eseguire il provisioning delle risorse cloud prima di distribuire Configuration Manager, può essere utile comprendere queste opzioni prima di addentrarsi troppo nella pianificazione della struttura della gerarchia. L'uso delle risorse cloud potrebbe portare a un risparmio in termini di tempo e di costo risolvendo al contempo problemi aziendali non risolvibili con l'infrastruttura locale.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Risorse basate su cloud che è possibile usare con Configuration Manager  
 Dal momento che ogni opzione ha requisiti diversi, analizzare ciascuna in modo più approfondito per comprendere i prerequisiti univoci, le limitazioni e la possibilità di costi aggiuntivi in base all'uso.  

-   Per informazioni sui punti di distribuzione basati su cloud, vedere [Installare punti di distribuzione basati su cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Per ulteriori informazioni su Windows Azure, vedere [Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) in MSDN Library.  

### <a name="microsoft-azure-virtual-machines-for-cloud-based-infrastructure"></a>Macchine virtuali di Microsoft Azure (per l'infrastruttura basata su cloud)  
 Configuration Manager supporta l'uso di computer eseguiti nelle macchine virtuali di Azure analogamente a quando vengono eseguiti in locale all'interno della rete fisica aziendale. È possibile usare le macchine virtuali di Azure negli scenari seguenti:  

-   **Scenario 1:** è possibile eseguire Configuration Manager in una macchina virtuale e usarlo per gestire i client installati in altre macchine virtuali.  

-   **Scenario 2:** è possibile eseguire Configuration Manager in una macchina virtuale e usarlo per gestire i client che non vengono eseguiti in Azure.  

-   **Scenario 3:** è possibile eseguire diversi ruoli del sistema del sito di Configuration Manager nelle macchine virtuali e allo stesso tempo eseguire altri ruoli nella rete aziendale fisica (con connettività di rete appropriata per le comunicazioni).  

Gli stessi requisiti per reti, sistemi operativi e requisiti hardware che si applicano all'installazione di Configuration Manager nella rete aziendale fisica si applicano anche all'installazione di Configuration Manager in Microsoft Azure.  

Per usare le macchine virtuali di Azure è necessario avere una sottoscrizione ad Azure e il costo varia in base al numero di macchine virtuali usate, alla relativa configurazione e all'uso di risorse basate su cloud.  

I siti e i client di Configuration Manager in esecuzione nelle macchine virtuali Azure sono inoltre soggetti agli stessi requisiti di licenza delle installazioni locali  

### <a name="microsoft-azure-services-for-cloud-based-distribution-points"></a>Servizi di Microsoft Azure (per i punti di distribuzione basati su cloud)  
 È possibile usare un servizio di Azure per ospitare un punto di distribuzione di Configuration Manager, definito punto di distribuzione basato su cloud.  È possibile [usare i punti di distribuzione basati su cloud con System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) insieme ai punti di distribuzione locali e ai punti di distribuzione distribuiti nelle macchine virtuali di Azure.  

 Questa situazione è diversa rispetto all'uso di una macchina virtuale di Azure, in cui si distribuisce un ruolo del sistema del sito. Punti di distribuzione basati su cloud:  

-   Vengono eseguiti come servizio in Microsoft Azure, non in una macchina virtuale  

-   Vengono scalati automaticamente per soddisfare l'incremento delle richieste di contenuto dai client  

-   Supportano client su Internet e intranet  

Per usare Azure per ospitare i punti di distribuzione è necessario avere una sottoscrizione ad Azure e il costo varia in base alla quantità di dati trasferiti da e verso il servizio.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (per la gestione dei dispositivi mobili)  
 È possibile integrare la sottoscrizione a Microsoft Intune con Configuration Manager per consentire la gestione dei dispositivi con il servizio Intune. Questa integrazione:  

-   Viene definita una configurazione ibrida ed estende Configuration Manager (o Intune a seconda della prospettiva) per supportare un'ampia varietà di dispositivi.  

-   Richiede il ruolo del sistema del sito del connettore Microsoft Intune.  

-   Richiede una sottoscrizione separata a Intune con numero di licenze sufficiente per i dispositivi che verranno gestiti con Intune  

Anche se Intune usa Microsoft Azure, non richiede una configurazione indipendente di Azure né di sostenere altri costi oltre a quelli della sottoscrizione a Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Funzionalità aggiuntive di Configuration Manager  
 Alcune funzionalità di Configuration Manager possono connettersi ai servizi basati su cloud, ad esempio:  

-   Windows Server Update Services (WSUS)  

-   Il servizio cloud di Configuration Manager per scaricare gli aggiornamenti per Configuration Manager  

Per queste funzionalità aggiuntive non è necessario avere una sottoscrizione ad Azure né configurare connessioni, certificati o servizi specifici nel cloud, ma vengono gestite automaticamente da Configuration Manager.  È sufficiente verificare che i dispositivi e i sistemi del sito applicabili possano accedere agli URL basati su Internet.  

##  <a name="a-namebkmkcloudseca-security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Sicurezza dei servizi basati su cloud  
 Configuration Manager usa i certificati per il provisioning e l'accesso al contenuto di Microsoft Azure e per la gestione dei servizi usati. Configuration Manager crittografa i dati archiviati in Azure, ma non introduce ulteriori controlli su dati o sicurezza oltre a quelli forniti da Azure.  

 Per altre informazioni, vedere i dettagli relativi ai diversi scenari di risorse basate su cloud. È anche possibile visualizzare gli argomenti seguenti per la sicurezza di Microsoft Azure:  

-   [Microsoft Azure: Gestione degli account di protezione in Microsoft Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Panoramica sulla protezione di Microsoft Azure](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Superare gli incroci di protezione nella migrazione cloud](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [Protezione dei dati in Azure (parte 1 di 2)](http://go.microsoft.com/fwlink/p/?LinkId=262974)  



<!--HONumber=Dec16_HO3-->


