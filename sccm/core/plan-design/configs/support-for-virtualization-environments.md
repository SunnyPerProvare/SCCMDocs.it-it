---
title: Supporto della virtualizzazione
titleSuffix: Configuration Manager
description: Requisiti per l'installazione di ruoli del sistema del sito e dei client di Configuration Manager in un ambiente di virtualizzazione.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a49b5f73b235f5c90279a871e0a80b4d414eec69
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80601222"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Supporto per gli ambienti di virtualizzazione per Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager supporta l'installazione di ruoli del sistema del sito e di client in sistemi operativi supportati eseguiti come macchina virtuale negli ambienti di virtualizzazione in questo articolo. Questo supporto è presente anche quando l'host macchina virtuale (ambiente di virtualizzazione) non è supportato come server del sito o del client.  

Ad esempio, si usa Microsoft Hyper-V Server 2012 per ospitare una macchina virtuale che esegue Windows Server 2012. È possibile installare i ruoli del sistema del sito o client nella macchina virtuale che esegue Windows Server 2012. È possibile installare il client nell'host che esegue Microsoft Hyper-V Server 2012.  

## <a name="virtualization-environments"></a>Ambienti di virtualizzazione

- Windows Server 2019  
- Windows Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Nota 1](#bkmk_note1)</sup>  
- R2 per Windows Server 2012  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a> Nota 1: Virtualizzazione annidata

Configuration Manager non supporta la [virtualizzazione annidata](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), introdotta con Windows Server 2016.

### <a name="virtualization-environment-support"></a>Supporto dell'ambiente di virtualizzazione

Per ogni computer virtuale è richiesta la stessa dotazione hardware e software (o superiore) che verrebbe usata per un computer Configuration Manager fisico.  

Per verificare che l'ambiente di virtualizzazione sia supportato per Configuration Manager, usare il programma SVVP (Server Virtualization Validation Program), che include una procedura guidata online per criteri di supporto del programma di virtualizzazione. Per altre informazioni, vedere [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programma SVVP - Server Virtualization Validation Program).  

> [!NOTE]  
> Configuration Manager non supporta i sistemi operativi guest Virtual PC o Virtual Server eseguiti su computer Mac.  

Configuration Manager non può gestire macchine virtuali se sono offline. Non è possibile aggiornare un'immagine di macchina virtuale offline né raccogliere un inventario tramite il client di Configuration Manager nel computer host.  

Nessuna considerazione speciale è attribuita alle macchine virtuali. Ad esempio, Configuration Manager potrebbe non riuscire a determinare se un aggiornamento deve essere nuovamente applicato a un'immagine di macchina virtuale se la macchina virtuale è stata arrestata e riavviata senza salvare lo stato della macchina virtuale a cui è stato applicato l'aggiornamento.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Macchine virtuali di Microsoft Azure  

Configuration Manager può essere eseguito in macchine virtuali di Azure così come viene eseguito in locale all'interno del data center. Usare Configuration Manager con macchine virtuali di Azure negli scenari seguenti:  

- **Scenario 1**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client in altre macchine virtuali di Azure.  

- **Scenario 2**: eseguire Configuration Manager in una macchina virtuale di Azure. Usarlo per gestire i client che non sono in esecuzione in Azure.  

- **Scenario 3:** eseguire ruoli del sistema del sito di Configuration Manager diversi in macchine virtuali di Azure. Eseguire altri ruoli nel data center locale, con la connessione appropriata ad Azure.  

Gli stessi requisiti di Configuration Manager per reti, configurazioni supportate e requisiti hardware che si applicano all'installazione locale di Configuration Manager in locale, si applicano anche all'installazione in macchine virtuali di Azure.  

Per altre informazioni, vedere [Configuration Manager in Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> I siti e i client di Configuration Manager in esecuzione in macchine virtuali di Azure sono soggetti anche agli stessi requisiti di licenza delle installazioni locali.  

## <a name="windows-virtual-desktop"></a>Desktop virtuale Windows

[Desktop virtuale Windows](https://docs.microsoft.com/azure/virtual-desktop/) è una funzionalità di anteprima di Microsoft Azure e Microsoft 365. A partire dalla versione 1906, usare Configuration Manager per gestire questi dispositivi virtuali che eseguono Windows in Azure. Per altre informazioni, vedere [Sistemi operativi supportati per client e dispositivi](/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
