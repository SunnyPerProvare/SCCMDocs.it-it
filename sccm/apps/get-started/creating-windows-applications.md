---
title: Creare applicazioni Windows| System Center Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Windows.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f776e624c7fff5f52b573e5066a6e7d20396ce91

---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Creare applicazioni Windows con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di System Center Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni per i dispositivi Windows è necessario tenere presente quanto segue.  

## <a name="general-considerations"></a>Considerazioni generali  
 Configuration Manager supporta la distribuzione dei tipi di app seguenti:  

|Tipo di dispositivo|File supportati|  
|-----------------|---------------------|  
|Windows RT e Windows RT 8.1|*.appx, \*.appxbundle|  
|Windows 8.1 e versioni successive registrato come dispositivo mobile|*.appx, \*.appxbundle|  

 Sono supportate le azioni di distribuzione seguenti:  

|Tipo di dispositivo|Azioni supportate|  
|-----------------|-----------------------|  
|Windows 8.1 e versioni successive|Disponibile, Richiesto Disinstalla|  
|Windows RT|Disponibile, Richiesto, Disinstalla|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Supporto per app della piattaforma UWP (Universal Windows Platform)  
 Nei dispositivi Windows 10 non è necessario disporre di una chiave di trasferimento locale per installare le app line-of-business. Tuttavia, la chiave del Registro di sistema **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** deve avere un valore pari a 1 per abilitare il trasferimento locale.  

 Se la chiave del Registro di sistema non è configurata, Configuration Manager imposterà automaticamente questo valore su **1** la prima volta che si distribuisce un'app al dispositivo. Se questo valore è stato impostato su **0**, Configuration Manager può modificare automaticamente il valore e la distribuzione delle app line-of-business avrà esito negativo.  

 Le app line-of-business della piattaforma UWP devono essere firmate con un certificato di firma codice attendibile su ogni dispositivo in cui l'applicazione viene distribuita. È possibile usare i certificati da un'infrastruttura a chiave pubblica (PKI) interna o un certificato da una radice pubblica di terze parti installato nel dispositivo.  

 Nei dispositivi Windows 10 Mobile, è possibile usare un certificato di firma codice non Symantec per firmare le app universali **.appx** . Per le app **.xap** e per i pacchetti **.appx** compilati per Windows Phone 8.1 che si vuole installare nei dispositivi Windows 10 Mobile, è necessario usare un certificato di firma codice Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Distribuire app Windows Installer nei PC Windows 10 registrati  
 Il tipo di programma di installazione **Windows Installer tramite MDM (\*.msi)** consente di creare e distribuire app basate su Windows Installer nei PC registrati che eseguono Windows 10.  

 Quando si usa questo tipo di programma di installazione, considerare gli aspetti seguenti:  

-   È possibile caricare solo un singolo file con estensione msi.  

-   Per il rilevamento delle app vengono usati il codice e la versione prodotto del file.  

-   Verrà usato il comportamento di riavvio predefinito dell'app. Configuration Manager non controlla questo comportamento.  

-   I pacchetti MSI per utente vengono installati per un singolo utente.  

-   I pacchetti MSI per computer vengono installati per tutti gli utenti del dispositivo.  

-   Gli aggiornamenti delle app sono supportati quando il codice prodotto MSI di ogni versione è lo stesso.  



<!--HONumber=Nov16_HO1-->

