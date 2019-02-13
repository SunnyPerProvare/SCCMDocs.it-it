---
title: Affinità utente per i dispositivi gestiti ibridi
titleSuffix: Configuration Manager
description: Configurare l'affinità utente per i dispositivi gestiti in Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54ca57956db37a26e2edad27c6cf6b92aecd1645
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138909"
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Affinità utente per i dispositivi gestiti ibridi in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si configurano profili per i dispositivi di proprietà dell'azienda, l'amministratore può specificare se i dispositivi gestiti possono avere un'*affinità utente* che identifica un utente specifico con il dispositivo.  

##  <a name="BKMK_iOSCP"></a> Dispositivi gestiti con affinità utente  
 I dispositivi configurati con **user affinity** possono installare ed eseguire l'app Portale aziendale per scaricare le app e gestire i dispositivi. Quando gli utenti ricevono i dispositivi, devono eseguire alcuni passaggi supplementari per completare l'Assistente configurazione e installare l'app Portale aziendale.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Come registrare i dispositivi iOS con l'affinità utente  

1.  Quando gli utenti accendono per la prima volta i dispositivi nuovi, viene chiesto di completare l'Assistente configurazione. Nel profilo di registrazione può essere specificata la richiesta di credenziali durante l'installazione. Gli utenti devono usare le credenziali, ossia nome personale univoco o UPN, associate alla propria sottoscrizione in Intune.  

2.  Durante la configurazione, può anche essere richiesta l'immissione di un ID Apple. L'ID Apple è necessario per consentire al dispositivo di installare il Portale aziendale. Gli utenti possono specificare un ID Apple dopo la configurazione dal menu **Impostazioni** di iOS.  

3.  Al termine della configurazione, il dispositivo iOS deve installare l'app Portale aziendale dall'App Store, ad esempio [App Portale aziendale](https://itunes.apple.com/us/app/id719171358).  

4.  A questo punto l'utente può accedere al Portale aziendale con l'UPN usato durante la configurazione del dispositivo.  

5.  Dopo l'accesso, viene chiesto di registrare il dispositivo. Il primo passaggio consiste nell' **identificare il dispositivo**. L'applicazione visualizza un elenco di dispositivi iOS registrati dall'azienda e assegnati all'account di Intune dell'utente finale. Scegliere il dispositivo corrispondente.  

     Se il dispositivo non è registrato dall'azienda, selezionare "nuovo dispositivo" per continuare con il flusso di registrazione standard.  

6.  Nella schermata successiva l'utente deve confermare il numero di serie del nuovo dispositivo. L'utente può toccare il collegamento "confermare il numero di serie" per avviare l'app Impostazioni e verificare il numero di serie. Deve quindi immettere gli ultimi 4 caratteri del numero di serie nell'app Portale aziendale.  

     Questo passaggio verifica che il dispositivo sia il dispositivo aziendale registrato in Intune. Se il numero di serie sul dispositivo non corrisponde, è stato selezionato il dispositivo errato. Tornare alla schermata precedente e selezionare un dispositivo diverso.  

7.  Dopo aver verificato il numero di serie, l'app Portale aziendale reindirizza al sito Web del Portale aziendale per completare la registrazione e quindi chiede all'utente di tornare all'app.  

8.  La registrazione è stata completata. Ora si può usare il dispositivo con il set completo di funzionalità.  

##  <a name="BKMK_noUA"></a> Dispositivi gestiti senza affinità utente  
 I dispositivi configurati con **no user affinity** non è supportato il Portale aziendale e non si dovrebbe installare l'app. Il Portale aziendale è progettato per gli utenti che hanno credenziali aziendali e richiedono l'accesso a risorse aziendali personalizzate, ad esempio la posta elettronica. I dispositivi registrati **senza affinità utente** non sono pensati per l'accesso utente dedicato. Chioschi multimediali, POS o dispositivi di utilità condivisi sono casi d'uso tipici per i dispositivi registrati senza affinità utente. Se è necessaria l'affinità utente, verificare che nel profilo di registrazione del dispositivo sia selezionata l'opzione **Affinità utente** prima di registrare il dispositivo. Per modificare lo stato di affinità in un dispositivo è necessario ritirare il dispositivo e quindi registrarlo nuovamente.
