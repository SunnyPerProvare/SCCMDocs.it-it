---
title: Configurare la pre-cache del contenuto
titleSuffix: Configuration Manager
description: Informazioni su come i client possono scaricare il contenuto della distribuzione del sistema operativo prima di installare la sequenza di attività.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ba7380d35742f01c620d95bfb9351180d56f7df
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537719"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Configurare il contenuto pre-cache per le sequenze di attività

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1021244-->
La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente prima che un utente installi la sequenza di attività. Il client può eseguire il pre-cache del contenuto per le sequenze di attività che [aggiornano un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) o [installano un'immagine del sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

Si supponga, ad esempio, di volere una sola sequenza di attività di aggiornamento sul posto per tutti gli utenti, pur avendo molte architetture e lingue diverse. Nelle versioni precedenti il download del contenuto inizia quando l'utente installa una distribuzione di sequenze di attività disponibile da Software Center. Questo ritardo aggiunge ulteriore tempo prima che l'installazione sia pronta per essere avviata. Tutto il contenuto a cui viene fatto riferimento nella sequenza di attività viene scaricato. Questo contenuto include il pacchetto di aggiornamento del sistema operativo per tutte le lingue e tutte le architetture. Se ogni pacchetto di aggiornamento è circa 3 GB, il contenuto totale è molto elevato.

Con la funzionalità pre-cache del contenuto è possibile consentire al client di scaricare solo il contenuto applicabile e tutto il contenuto a cui si fa riferimento non appena riceve la distribuzione. Quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto. L'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

In Configuration Manager versione 1902 e versioni precedenti questo comportamento si applica solo al *pacchetto di aggiornamento del sistema operativo*. Tale pacchetto è il solo il contenuto per il quale si specifica la lingua o l'architettura corrispondente. Ad esempio, se la sequenza di attività fa riferimento anche a più pacchetti driver, il client li scarica tutti. Il motore della sequenza di attività valuta le condizioni per i passaggi quando la sequenza di attività viene eseguita, non prima. Il client usa i tag nelle proprietà del pacchetto per determinare per quale contenuto eseguire la funzione pre-cache.

A partire dalla versione 1906,<!--4224642--> è possibile usare la pre-caching per ridurre l'utilizzo della larghezza di banda dei tipi di contenuto seguenti:

- Pacchetti di aggiornamento del sistema operativo
- Immagini dei sistemi operativi
- Pacchetti driver
- Pacchetti


## <a name="configure-pre-caching"></a>Configurare la pre-memorizzazione nella cache

Per configurare la funzionalità pre-cache sono necessari tre passaggi:

1. [Creare e configurare i pacchetti](#bkmk_createpkg)
2. [Creare una sequenza di attività con i passaggi condizionali](#bkmk_createts)
3. [Distribuire la sequenza di attività e abilitare la pre-memorizzazione nella cache](#bkmk_deploy)


### <a name="bkmk_createpkg"></a>-1 Creare e configurare i pacchetti

Il client valuta gli attributi dei pacchetti per determinare il contenuto scaricato durante la pre-memorizzazione nella cache.  

#### <a name="os-upgrade-package"></a>Pacchetto di aggiornamento del sistema operativo

Creare [pacchetti di aggiornamento del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages) per lingue e architetture specifiche. Specificare i valori per **Architettura** e **Lingua** nella scheda **Origine dati** delle proprietà.

#### <a name="os-image"></a>Immagine del sistema operativo

Creare [immagini del sistema operativo](/sccm/osd/get-started/manage-operating-system-images) per lingue e architetture specifiche. Specificare i valori per **Architettura** e **Lingua** nella scheda **Origine dati** delle proprietà.

#### <a name="driver-package"></a>Pacchetto driver

Creare [pacchetti driver](/sccm/osd/get-started/manage-drivers#BKMK_ManagingDriverPackages) per modelli di hardware specifici. Specificare il **modello** nella scheda **generale** delle relative proprietà.

Per determinare quale pacchetto di driver scaricare durante la memorizzazione anticipata nella cache, il client valuta il modello rispetto alla proprietà WMI **Win32_ComputerSystemProduct**.  

#### <a name="package"></a>Pacchetto

Creare [pacchetti](/sccm/apps/deploy-use/packages-and-programs) per lingue e architetture specifiche. Specificare l' **architettura** e la **lingua** nella scheda **generale** delle relative proprietà.


### <a name="bkmk_createts"></a> 2. Creare una sequenza di attività

Creare una sequenza di attività con i passaggi condizionali per le diverse lingue e architetture oppure modelli hardware diversi per i pacchetti driver.

|Content|Passaggio|
|---------|---------|
|Pacchetto di aggiornamento del sistema operativo|[Aggiorna sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)|
|Immagine del sistema operativo|[Applica immagine del sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage)|
|Pacchetto driver|[Applica pacchetto di driver](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage)|
|Pacchetto|[Installa pacchetto](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)|

Ad esempio, il passaggio di **aggiornamento del sistema operativo** seguente usa la versione in lingua inglese:  

![Editor delle sequenze di attività in cui sono visualizzati più passaggi di aggiornamento del sistema operativo per ENU, DEU e JPN](../media/precacheproperties2.png)

![Editor delle sequenze di attività, scheda Opzioni, in cui è visualizzata la query WQL WMI per Locale e OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> La query WMI seguente è consigliata per il sistema operativo in lingua inglese (Stati Uniti) e l'architettura a 64 bit:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage=1033`
> ```
>
> Per prima cosa, aggiungere la lingua selezionando la condizione della **lingua del sistema operativo** . Modificare quindi la query WMI per includere la clausola Architecture.


### <a name="bkmk_deploy"></a> 3. Distribuire la sequenza di attività

[Distribuire la sequenza di attività](/sccm/osd/deploy-use/deploy-a-task-sequence). Per la funzionalità di pre-cache configurare le impostazioni seguenti:  

- Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.  

- Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile**.  

- Nella scheda **Pianificazione** scegliere l'ora attualmente selezionata per l'impostazione **Pianifica quando questa distribuzione diventerà disponibile**. Il client avvia la funzionalità di pre-cache del contenuto nell'orario disponibile della distribuzione. Quando un client di destinazione riceve questo criterio, l'orario disponibile cade nel passato, quindi il download di pre-cache inizia immediatamente. Se il client riceve questo criterio ma l'orario disponibile è nel futuro, il client non avvia la funzionalità di pre-cache del contenuto fino all'orario disponibile.  

- Nella scheda **Punti di distribuzione** configurare le impostazioni **Opzioni di distribuzione**. Se non viene eseguita la funzione pre-cache prima che l'utente avvii l'installazione, il client usa queste impostazioni.  

    > [!Important]  
    > Per una sequenza di attività che installa un'immagine del sistema operativo, non usare l'opzione di distribuzione per **scaricare il contenuto localmente quando necessario per la sequenza di attività in esecuzione**. Quando la sequenza di attività cancella il disco prima di applicare l'immagine del sistema operativo, viene rimossa la cache del client. Poiché il contenuto è andato perso, la sequenza di attività ha esito negativo.<!-- SCCMDocs-PR #1338 -->


## <a name="user-experience"></a>Esperienza utente

- Quando il client riceve i criteri di distribuzione, avvia la funzionalità pre-cache del contenuto dopo l'orario disponibile della distribuzione. Questo contenuto include tutti i pacchetti a cui si fa riferimento, ma solo il pacchetto di aggiornamento del sistema operativo che corrisponde agli attributi di architettura e lingua del pacchetto.  

- Quando il cliente rende disponibile la distribuzione agli utenti, una notifica informa gli utenti della nuova distribuzione e la sequenza di attività diventa visibile in Software Center. Per avviare l'installazione l'utente può passare a Software Center e fare clic su **Installa**.  

- Se la funzionalità di pre-cache del contenuto non è stata completamente eseguita quando l'utente installa la sequenza di attività, il client usa le impostazioni specificate nella scheda **Opzione di distribuzione** della distribuzione.  


## <a name="see-also"></a>Vedere anche

- [Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)
- [Scenario di aggiornamento di Windows alla versione più recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)
