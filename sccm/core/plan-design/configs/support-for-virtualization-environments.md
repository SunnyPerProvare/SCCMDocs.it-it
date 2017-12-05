---
title: Supporto della virtualizzazione
titleSuffix: Configuration Manager
description: Requisiti per l'installazione di ruoli del sistema del sito e dei client di System Center Configuration Manager in un ambiente di virtualizzazione.
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: "6"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 941c0fffd351a7cc345c5bcc0529633c22c27ed5
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Supporto per gli ambienti di virtualizzazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione di ruoli del sistema del sito e client in sistemi operativi supportati eseguiti come macchina virtuale negli ambienti di virtualizzazione elencati in questo articolo. Questo supporto è presente anche quando l'host macchina virtuale (ambiente di virtualizzazione) non è supportato come server del sito o del client.  

 Ad esempio, se si usa Microsoft Hyper-V Server 2012 per ospitare una macchina virtuale che esegue Windows Server 2012, è possibile installare i ruoli del sistema del sito o client nella macchina virtuale (Windows Server 2012), ma non nell'host (Microsoft Hyper-V Server 2012).  

|Ambiente di virtualizzazione|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(vedere *nota 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(vedere *nota 1*)|
-  *Nota 1*: Configuration Manager non supporta la [virtualizzazione nidificata ](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), introdotta con Windows Server 2016.


 Ogni computer virtuale in uso deve soddisfare gli stessi requisiti hardware e software che sarebbero previsti per un computer Configuration Manager fisico.  

 È possibile confermare che l'ambiente di virtualizzazione è supportato per Configuration Manager usando il programma SVVP (Server Virtualization Validation Program) e la relativa procedura guidata online per criteri di supporto del programma di virtualizzazione. Per altre informazioni sul programma SVVP (Server Virtualization Validation Program), vedere [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager non supporta i sistemi operativi guest Virtual PC o Virtual Server eseguiti su computer Mac.  

Configuration Manager non può gestire macchine virtuali, a meno che non siano online. Non è possibile aggiornare un'immagine di macchina virtuale offline né raccogliere un inventario tramite il client di Configuration Manager nel computer host.  

Nessuna considerazione speciale è attribuita alle macchine virtuali. Ad esempio, Configuration Manager potrebbe non riuscire a determinare se un aggiornamento deve essere nuovamente applicato a un'immagine di macchina virtuale se la macchina virtuale è stata arrestata e riavviata senza salvare lo stato della macchina virtuale a cui è stato applicato l'aggiornamento.  

##  <a name="bkmk_Azure"></a> Macchine virtuali di Microsoft Azure  
 Configuration Manager può essere eseguito in macchine virtuali di Azure così come viene eseguito in locale all'interno della rete fisica aziendale. È possibile usare Configuration Manager con macchine virtuali di Azure negli scenari seguenti:  

-   **Scenario 1:** è possibile eseguire Configuration Manager in una macchina virtuale di Azure e usarlo per gestire client installati in altre macchine virtuali di Azure.  

-   **Scenario 2:** è possibile eseguire Configuration Manager in una macchina virtuale di Azure e usarlo per gestire i client che non vengono eseguiti in Azure.  

-   **Scenario 3:** è possibile eseguire diversi ruoli del sistema del sito di Configuration Manager in macchine virtuali di Azure e al tempo stesso eseguire altri ruoli nella rete aziendale fisica (con connettività di rete appropriata per le comunicazioni).  

Gli stessi requisiti di System Center Configuration Manager per reti, configurazioni supportate e requisiti hardware che si applicano all'installazione locale di Configuration Manager nella rete aziendale fisica si applicano anche all'installazione in macchine virtuali di Azure.  

Per altre informazioni, vedere [Configuration Manager in Azure: domande frequenti](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  I siti e i client di Configuration Manager in esecuzione in macchine virtuali di Azure sono soggetti anche agli stessi requisiti di licenza delle installazioni locali.  
