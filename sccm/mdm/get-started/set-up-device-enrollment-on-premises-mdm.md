---
title: 'Impostare la registrazione dei dispositivi '
titleSuffix: Configuration Manager
description: Concedere autorizzazioni agli utenti per registrare i dispositivi per la gestione dei dispositivi mobili locale in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d0424b662df4baba7374685dd7631347501352c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349083"
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Impostare la registrazione dei dispositivi per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per consentire agli utenti di registrare i propri dispositivi per la gestione dei dispositivi mobili locale di System Center Configuration Manager, è necessario concedere loro le autorizzazioni appropriate. Per concedere agli utenti le autorizzazioni per la registrazione dei dispositivi, eseguire le attività seguenti.

-   [Creare un profilo di registrazione che consenta agli utenti di registrare i dispositivi moderni](#bkmk_createProf)  

-   [Configurare altre impostazioni client per i dispositivi registrati](#bkmk_addClient)  

-   [Consentire agli utenti di ricevere il profilo di registrazione dei dispositivi moderni](#bkmk_enableUsers)  

-   [Archiviare il certificato radice nei dispositivi da registrare](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Creare un profilo di registrazione che consenta agli utenti di registrare i dispositivi moderni  
 Per eseguire il push delle impostazioni necessarie per consentire agli utenti di registrare i dispositivi moderni, è possibile aggiungere un nuovo profilo di registrazione alle impostazioni client predefinite, che viene applicato a tutti gli utenti individuati nel sito di Configuration Manager.  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Panoramica** > **Impostazioni client**, aprire **Impostazioni client predefinite** e selezionare **Registrazione**.  

2.  In Impostazioni dispositivo specificare l'intervallo di polling per i dispositivi moderni.  

3.  In Impostazioni utente selezionare **Sì** per **Consenti agli utenti di registrare i dispositivi moderni**.  

4.  Accanto a **Profilo di registrazione per dispositivi moderni**, fare clic su **Imposta profilo** e quindi su **Crea**.  

5.  In Crea profilo di registrazione digitare un nome per il profilo di registrazione e scegliere il codice del sito di gestione che gli utenti con il profilo di registrazione dovranno usare. Fare clic su **OK** più volte per uscire dalla pagina Impostazioni predefinite.  

> [!NOTE]  
>  Se si vuole distribuire il profilo di registrazione a un sottoinsieme degli utenti individuati, è possibile usare una raccolta di utenti e creare impostazioni client personalizzate per eseguire la distribuzione in tale raccolta. Per informazioni sulla creazione di impostazioni client personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> Configurare altre impostazioni client per i dispositivi registrati  
 Oltre a configurare il profilo di registrazione per dispositivi moderni, è possibile usare altre impostazioni client per configurare i dispositivi quando vengono registrati.  Per informazioni sulla configurazione delle impostazioni client, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Non tutte le impostazioni client sono disponibili per la gestione dei dispositivi mobili locale. Current Branch di Configuration Manager supporta solo le configurazioni seguenti per la gestione dei dispositivi mobili locale:  

-   Registrazione: queste impostazioni specificano il profilo di registrazione per i dispositivi gestiti. Per altre informazioni sull'impostazione di un profilo di registrazione, vedere [Creare un profilo di registrazione che consenta agli utenti di registrare i dispositivi moderni](#bkmk_createProf).  

-   Criteri client: queste impostazioni specificano la frequenza di download dei criteri client nel dispositivo. È anche possibile abilitare le impostazioni per l'assegnazione del polling dei criteri agli utenti. Per altre informazioni sulle impostazioni dei criteri client, vedere la sezione Criteri client in [Informazioni sulle impostazioni client in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Distribuzione software: questa impostazione definisce l'intervallo per la valutazione dei dispositivi client per le distribuzioni software. Per altre informazioni sulle impostazioni di distribuzione software, vedere la sezione Distribuzione software in [Informazioni sulle impostazioni client in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)  

    > [!NOTE]  
    >  Per la gestione dei dispositivi mobili locale, le impostazioni di distribuzione software possono essere usate solo come impostazioni client predefinite. Le impostazioni di distribuzione software non possono essere usate con le impostazioni client personalizzate in Current Branch di Configuration Manager.  

##  <a name="bkmk_enableUsers"></a> Consentire agli utenti di ricevere il profilo di registrazione dei dispositivi moderni  
 Per fare in modo che ricevano le impostazioni client modificate con il profilo di registrazione per la gestione dei dispositivi mobili locale, è necessario che gli utenti vengano individuati tramite il metodo di individuazione Active Directory. Per assicurarsi che il profilo di registrazione venga ottenuto da tutti gli utenti che ne hanno bisogno, eseguire l'individuazione degli utenti di Active Directory. Per informazioni sulla procedura di individuazione degli utenti, vedere [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="bkmk_storeCert"></a> Archiviare il certificato radice nei dispositivi da registrare  
 È probabile che gli utenti con dispositivi appartenenti a un dominio abbiano già il certificato radice richiesto per la comunicazione attendibile con i server che ospitano i ruoli del sistema del sito, perché la radice è stata rilasciata come parte del processo di aggiunta al dominio con Active Directory. Per i dispositivi mobili non appartenenti a un dominio sarà necessario installare manualmente il certificato radice nel dispositivo per consentire la registrazione. Questi dispositivi non avranno automaticamente il certificato radice richiesto.  

 È necessario fornire al dispositivo il file del certificato esportato per l'installazione manuale. Questa operazione può essere eseguita tramite posta elettronica, OneDrive, una scheda SD, un'unità USB o qualsiasi metodo adatto alle proprie esigenze.  

 Il certificato radice da usare nei dispositivi è quello esportato in [Esportare il certificato con la stessa radice del certificato del server Web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  Nel dispositivo da registrare individuare il file del certificato radice e fare doppio clic su di esso.  

2.  Nella finestra Certificato fare clic su **Installa certificato**.  

3.  Nell'Importazione guidata certificati selezionare **Computer locale**e fare clic su **Avanti**.  

4.  Nella finestra Controllo dell'account utente fare clic su **Sì**.  

5.  Selezionare **Colloca tutti i certificati nel seguente archivio**e quindi fare clic su **Sfoglia**.  

6.  Fare clic su **Autorità di certificazione radice attendibili**, fare clic su **OK**e quindi fare clic su **Avanti**.  

7.  Fare clic su **Fine**.  
