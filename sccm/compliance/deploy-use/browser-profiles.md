---
title: Configurare le impostazioni di Microsoft Edge
titleSuffix: Configuration Manager
description: Configurare le impostazioni per il Web browser Microsoft Edge nei client Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: cb162e030249b02018af52ad3266b6b8df5ce355
ms.sourcegitcommit: aed99ba3c5e9482199cb3fc5c92f6f3a160cb181
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Configurare le impostazioni per Microsoft Edge in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!-- 1357310 -->
A partire dalla versione 1802 i clienti che usano il Web browser [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) nei client Windows 10 possono creare un criterio delle impostazioni di conformità di Configuration Manager per definire diverse impostazioni di Microsoft Edge. 

Questi criteri si applicano solo ai client con Windows 10 versione 1703 o successiva. <!--511552-->


## <a name="policy-settings"></a>Impostazioni criteri
Questo criterio include attualmente le impostazioni seguenti:
- **Imposta il browser Microsoft Edge come predefinito**: configura l'impostazione dell'app predefinita di Windows 10 per il Web browser su Microsoft Edge.
- **Consenti l'elenco a discesa della barra degli indirizzi**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Consenti la sincronizzazione dei Preferiti tra browser Microsoft**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Consenti la cancellazione dei dati di esplorazione all'uscita**: richiede Windows 10 versione 1703 o successiva. Per altre informazioni, vedere [Criterio del browser ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Consenti le intestazioni Do Not Track**: per altre informazioni, vedere [Criterio del browser AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Consenti riempimento automatico**: per altre informazioni, vedere [Criterio del browser AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Consenti i cookie**: per altre informazioni, vedere [Criterio del browser AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Consenti il blocco popup**: per altre informazioni, vedere [Criterio del browser AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Consenti suggerimenti di ricerca nella barra degli indirizzi**: per altre informazioni, vedere [Criterio del browser AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Consenti l'invio di traffico Intranet a Internet Explorer**: per altre informazioni, vedere [Criterio del browser SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Consenti lo strumento per la gestione delle password**: per altre informazioni, vedere [Criterio del browser AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Consenti gli Strumenti di sviluppo**: per altre informazioni, vedere [Criterio del browser AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Consenti le estensioni**: per altre informazioni, vedere [Criterio del browser AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Creare il profilo del browser Microsoft Edge

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità** e selezionare il nuovo nodo **Profili del browser Microsoft Edge**. Fare clic sull'opzione **Crea un criterio del browser Microsoft Edge** sulla barra multifunzione.
2. Specificare un nome per il criterio nel campo **Nome** e una descrizione facoltativa nel campo **Descrizione**, quindi fare clic su **Avanti**.
3. Nella pagina **Impostazioni** cambiare il valore delle impostazioni da includere nel criterio su **Configurato**, quindi fare clic su **Avanti**.
4. Nella pagina **Piattaforme supportate** selezionare le architetture e le versioni del sistema operativo a cui si applica il criterio, quindi fare clic su **Avanti**. 
5. Completare la procedura guidata.



## <a name="deploy-the-policy"></a>Distribuire il criterio

1. Selezionare il criterio e fare clic sull'opzione **Distribuisci** sulla barra multifunzione.
2. Fare clic su **Sfoglia** per selezionare la raccolta utenti o dispositivi nella quale si vuole distribuire il criterio. 
3. Selezionare le opzioni aggiuntive eventualmente necessarie. 
    a. Impostare la generazione di avvisi quando il criterio non è conforme. 
    b. Impostare la pianificazione in base alla quale il client valuta la conformità del dispositivo al criterio.
4. Fare clic su **OK** per creare la distribuzione.



## <a name="next-steps"></a>Passaggi successivi

Come avviene con qualsiasi criterio delle impostazioni di conformità, il client monitora e aggiorna le impostazioni sulla pianificazione specificata. [Monitorare e creare report sulla conformità dei dispositivi](/sccm/compliance/deploy-use/monitor-compliance-settings) nella console di Configuration Manager.
