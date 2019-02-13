---
title: Creare un lab in Azure
titleSuffix: Configuration Manager
description: Automatizzare la creazione di un lab di Configuration Manager Technical Preview usando i modelli di Azure
ms.date: 01/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6f087b6905d307c707b95e3926a01b0c482f857
ms.sourcegitcommit: b8167a60fd6f2d8387b2db723976c0e2c4198d33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54833027"
---
# <a name="create-a-configuration-manager-technical-preview-lab-in-azure"></a>Creare un lab di Configuration Manager Technical Preview in Azure

*Si applica a: System Center Configuration Manager (Technical Preview)*

<!--3556017-->

Questa guida descrive come compilare un ambiente lab per Configuration Manager in Microsoft Azure. Vengono usati modelli di Azure per semplificare e automatizzare la creazione di un lab con le risorse di Azure. Il processo installa l'ultima versione del ramo di Configuration Manager Technical Preview. 

Per altre informazioni sul ramo corrente di Configuration Manager, vedere [Configuration Manager in Azure](/sccm/core/understand/configuration-manager-on-azure).



## <a name="prerequisites"></a>Prerequisiti

Questo processo richiede una sottoscrizione di Azure in cui è possibile creare gli oggetti seguenti: 
- Quattro macchine virtuali Standard_D2s_v3
- Account di archiviazione Standard_LRS

> [!Tip]  
> Vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/) per determinare i costi potenziali.  



## <a name="process"></a>Processo

1. Passare al [modello di Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/).  

2. Selezionare **Distribuisci in Azure**. Si aprirà il portale di Azure.  

3. Completare il modello di avvio rapido di Azure con le informazioni seguenti:

    - Informazioni di base  

        - **Sottoscrizione**: Nome della sottoscrizione in cui creare le macchine virtuali  

        - **Gruppo di risorse**: Selezionare un gruppo di risorse da usare con le macchine virtuali  

        - **Location** (Percorso): Selezionare un data center di Azure per ospitare questo ambiente lab  

    - Impostazioni  

        - **Prefisso:**: Nome del prefisso delle macchine. Per altre informazioni, vedere [Informazioni sulle macchine virtuali di Azure](#azure-vm-info).  

        - **Nome utente amministratore**: Nome di un utente nelle macchine virtuali con diritti amministrativi. Questo utente viene usato per accedere alle macchine virtuali.  

        - **Password amministratore**: La password deve soddisfare i requisiti di complessità di Azure. Per altre informazioni, vedere [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Azure richiede le impostazioni seguenti. Usare i valori predefiniti. Non modificarli.  
    > 
    > - **\_artifacts Location** (Percorso Artifacts): Percorso degli script per questo modello <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_artifacts Location Sas Token** (token SAS percorso Artifacts): Il token SAS è necessario per accedere al percorso Artifacts  
    > 
    > - **Location** (Percorso): Percorso di tutte le risorse

4. Leggere i termini e le condizioni. Se si accettano, selezionare **Accetto le condizioni riportate sopra**, quindi selezionare **Acquista** per continuare. 

Azure convalida le impostazioni e inizia la distribuzione. Controllare lo stato della distribuzione nel portale di Azure. Il processo può durare 2/4 ore. L'esecuzione degli script di configurazione continua anche quando nel portale di Azure viene specificato che la distribuzione è stata completata. Non riavviare le macchine virtuali durante il processo.

Per visualizzare lo stato degli script di configurazione, collegarsi al server `<prefix>PS1` e visualizzare il file`%windir%\TEMP\ProvisionScript\PS1.json` seguente. Se tutti i passaggi sono stati completati, il processo è terminato.

Per connettersi alle macchine virtuali, ottenere prima gli indirizzi IP pubblici per ogni macchina virtuale dal portale di Azure. Quando ci si connette alla macchina virtuale, il nome di dominio è `contoso.com`. Usare le credenziali specificate nel modello di distribuzione. Per altre informazioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informazioni sulle macchine virtuali di Azure

Le specifiche di tutte le quattro macchine virtuali sono le seguenti:
- Standard_D2s_v3, con due core CPU e 8 GB di memoria  
- Windows Server 2016 Datacenter Edition
- 150 GB di spazio su disco
- Sia un indirizzo IP pubblico che uno privato. Gli indirizzi IP pubblici si trovano in un gruppo di sicurezza di rete che consente solo connessioni desktop remote alla porta TCP 3389. 

Il prefisso specificato nel modello di distribuzione è il prefisso del nome della macchina virtuale. Ad esempio se si imposta il prefisso "contoso", il nome del computer del controller di dominio sarà `contosoDC`.


### `<prefix>DC`

Controller di dominio Active Directory

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- Active Directory Domain Services (ADDS)
- .NET
- Compressione differenziale remota (RDC)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK con Windows PE 
- Sito primario di Configuration Manager

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- .NET
- Compressione differenziale remota (RDC) 
- Internet Information Service (IIS)


### `<prefix>MPDP`

- Punto di gestione
- Punto di distribuzione

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- .NET
- Compressione differenziale remota (RDC) 
- Internet Information Service (IIS)
- Servizio trasferimento intelligente in background (BITS)


### `<prefix>Other`

Questa macchina virtuale può essere usata come client o per ospitare altri ruoli del sito.

#### <a name="windows-features-and-roles"></a>Ruoli e funzionalità di Windows
- .NET
- Compressione differenziale remota (RDC) 

