---
title: Supporto per la virtualizzazione | Microsoft Docs
description: Requisiti per l&quot;installazione di ruoli del sistema del sito e dei client di System Center Configuration Manager in un ambiente di virtualizzazione.
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 13df135828e383e666bfc11051011207245a774c
ms.openlocfilehash: 1c00324d2e7cc9a082ba837b29879e3a778d0c54


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Supporto per gli ambienti di virtualizzazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione di ruoli del sistema del sito e di client in sistemi operativi supportati eseguiti come macchina virtuale negli ambienti di virtualizzazione seguenti. Questo supporto è presente anche quando l'host macchina virtuale (ambiente di virtualizzazione) non è supportato come server del sito o del client.  

 **Ad esempio**, se si usa Microsoft Hyper-V Server 2012 per ospitare una macchina virtuale che esegue Windows Server 2012, è possibile installare i ruoli del sistema del sito o client nella macchina virtuale (Windows Server 2012), ma non nell'host (Microsoft Hyper-V Server 2012).  

|Ambiente di virtualizzazione|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|  

 Ogni computer virtuale in uso deve avere almeno la stessa configurazione hardware e software che si userebbe per un computer Configuration Manager fisico.  

 È possibile confermare che l'ambiente di virtualizzazione è supportato per Configuration Manager usando il programma SVVP (Server Virtualization Validation Program) e la relativa procedura guidata online per criteri di supporto del programma di virtualizzazione. Per altre informazioni sul programma SVVP (Server Virtualization Validation Program), vedere [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager non supporta i sistemi operativi guest Virtual PC o Virtual Server eseguiti su un Mac.  

Configuration Manager non può gestire macchine virtuali, a meno che non siano online. Non è possibile aggiornare un'immagine di macchina virtuale offline né raccogliere un inventario tramite il client di Configuration Manager nel computer host.  

Nessuna considerazione speciale è attribuita alle macchine virtuali. Ad esempio, Configuration Manager potrebbe non riuscire a determinare se un aggiornamento deve essere nuovamente applicato a un'immagine di macchina virtuale se la macchina virtuale viene arrestata e riavviata senza salvare lo stato della macchina virtuale a cui è stato applicato l'aggiornamento.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Macchine virtuali di Microsoft Azure  
 L'esecuzione di Configuration Manager è supportata nelle macchine virtuali in Microsoft Azure allo stesso modo in cui è supportata localmente all’interno della rete fisica aziendale. È possibile usare Configuration Manager con le macchine virtuali di Microsoft Azure negli scenari seguenti:  

-   **Scenario 1:** è possibile eseguire Configuration Manager in una macchina virtuale di Microsoft Azure e usarlo per gestire client installati in altre macchine virtuali di Microsoft Azure.  

-   **Scenario 2:** è possibile eseguire Configuration Manager in una macchina virtuale di Microsoft Azure e usarlo per gestire client non in esecuzione in Microsoft Azure.  

-   **Scenario 3:** è possibile eseguire diversi ruoli del sistema del sito di Configuration Manager nelle macchine virtuali di Microsoft Azure e allo stesso tempo eseguire altri ruoli nella rete aziendale fisica (con connettività di rete appropriata per le comunicazioni).  

Gli stessi requisiti di System Center Configuration Manager per reti, configurazioni supportate e requisiti hardware che si applicano all’installazione locale di Configuration Manager nella rete aziendale fisica si applicano anche all’installazione in Microsoft Azure.  

Per altre informazioni, vedere [Configuration Manager in Azure: domande frequenti](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  I siti e i client di Configuration Manager in esecuzione nelle macchine virtuali Azure sono soggetti anche agli stessi requisiti di licenza delle installazioni locali.  



<!--HONumber=Dec16_HO3-->


