---
title: Supporto della virtualizzazione
titleSuffix: Configuration Manager
description: Requisiti per l'installazione di ruoli del sistema del sito e dei client di Configuration Manager in un ambiente di virtualizzazione.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebf07aa7fba1a017821eb63a57f8c721b4a9860b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499425"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Supporto per gli ambienti di virtualizzazione per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione di ruoli del sistema del sito e di client in sistemi operativi supportati eseguiti come macchina virtuale negli ambienti di virtualizzazione in questo articolo. Questo supporto è presente anche quando l'host macchina virtuale (ambiente di virtualizzazione) non è supportato come server del sito o del client.  

Ad esempio, si usa Microsoft Hyper-V Server 2012 per ospitare una macchina virtuale che esegue Windows Server 2012. È possibile installare i ruoli del sistema del sito o client nella macchina virtuale che esegue Windows Server 2012. È possibile installare il client nell'host che esegue Microsoft Hyper-V Server 2012.  


## <a name="virtualization-environments"></a>Ambienti di virtualizzazione

- Windows Server 2019  
- Windows Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> Nota 1: Virtualizzazione annidata
Configuration Manager non supporta la [virtualizzazione annidata](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), introdotta con Windows Server 2016.


### <a name="virtualization-environment-support"></a>Supporto dell'ambiente di virtualizzazione

Per ogni computer virtuale è richiesta la stessa dotazione hardware e software (o superiore) che verrebbe usata per un computer Configuration Manager fisico.  

Per verificare che l'ambiente di virtualizzazione sia supportato per Configuration Manager, usare il programma SVVP (Server Virtualization Validation Program), che include una procedura guidata online per criteri di supporto del programma di virtualizzazione. Per altre informazioni, vedere [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programma SVVP - Server Virtualization Validation Program).  

> [!NOTE]  
> Configuration Manager non supporta i sistemi operativi guest Virtual PC o Virtual Server eseguiti su computer Mac.  

Configuration Manager non può gestire macchine virtuali se sono offline. Non è possibile aggiornare un'immagine di macchina virtuale offline né raccogliere un inventario tramite il client di Configuration Manager nel computer host.  

Nessuna considerazione speciale è attribuita alle macchine virtuali. Ad esempio, Configuration Manager potrebbe non riuscire a determinare se un aggiornamento deve essere nuovamente applicato a un'immagine di macchina virtuale se la macchina virtuale è stata arrestata e riavviata senza salvare lo stato della macchina virtuale a cui è stato applicato l'aggiornamento.  



##  <a name="bkmk_Azure"></a> Macchine virtuali di Microsoft Azure  

Configuration Manager può essere eseguito in macchine virtuali di Azure così come viene eseguito in locale all'interno del data center. Usare Configuration Manager con macchine virtuali di Azure negli scenari seguenti:  

- **Scenario 1**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client in altre macchine virtuali di Azure.  

- **Scenario 2**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client che non sono in esecuzione in Azure.  

- **Scenario 3:** eseguire ruoli del sistema del sito di Configuration Manager diversi in macchine virtuali di Azure. Eseguire altri ruoli nel data center locale, con la connessione appropriata ad Azure.  

Gli stessi requisiti di Configuration Manager per reti, configurazioni supportate e requisiti hardware che si applicano all'installazione locale di Configuration Manager in locale, si applicano anche all'installazione in macchine virtuali di Azure.  

Per altre informazioni, vedere [Configuration Manager in Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> I siti e i client di Configuration Manager in esecuzione in macchine virtuali di Azure sono soggetti anche agli stessi requisiti di licenza delle installazioni locali.  
