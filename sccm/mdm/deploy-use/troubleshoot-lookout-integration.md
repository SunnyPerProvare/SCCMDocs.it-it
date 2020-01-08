---
title: Risoluzione dei problemi di integrazione di Lookout
titleSuffix: Configuration Manager
description: Questo argomento descrive la risoluzione di problemi che possono verificarsi con l'integrazione di Lookout.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 055b5b0499eddc04ceb73363b288a0096418aa35
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519624"
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Risolvere i problemi di integrazione di Lookout con Intune

*Si applica a: Configuration Manager (Current Branch)*

## <a name="troubleshoot-login-errors"></a>Risolvere i problemi relativi all'accesso
### <a name="403-errors"></a>Errori 403
Quando si accede alla [console di Lookout MTP](https://aad.lookout.com) può essere visualizzato un errore 403: **You are not authorized to access the service** (Non si dispone dell'autorizzazione per accedere al servizio). Questa situazione può verificarsi quando il nome utente specificato non è membro del gruppo Azure Active Directory (Azure AD) configurato per l'accesso a Lookout MTP.

Lookout MTP consente l'accesso solo agli utenti di un gruppo di Azure AD configurato. Se non si sa quale gruppo è configurato per l'accesso a Lookout MTP, contattare il supporto tecnico di Lookout.

È possibile contattare il supporto tecnico di Lookout con uno dei metodi seguenti:

* Posta elettronica: enterprisesupport@lookout.com
* Accedere alla [console di MTP](https://aad.lookout.com) e passare al modulo **Support** (Supporto).
* Passare a: https://enterprise.support.lookout.com/hc/requests e inoltrare una richiesta di supporto.

### <a name="unable-to-sign-in"></a>Impossibile accedere
Il seguente errore può apparire quando l'utente amministratore globale di Azure AD non ha accettato la configurazione iniziale di Lookup.

![Schermata della pagina di accesso a Lookout con l'errore di accesso](media/lookout-consent-not-accepted-error.png)

Per risolvere questo problema, l'utente amministratore globale deve accedere a https://aad.lookout.com/les?action=consent e accettare la richiesta di avviare il programma di installazione. Per altre informazioni, vedere [Set up your subscription with Lookout MTP](set-up-your-subscription-with-lookout.md) (Configurare l'abbonamento a Lookout MTP)

## <a name="troubleshoot-device-status-issues"></a>Risolvere i problemi di stato del dispositivo

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Il dispositivo non appare nell'elenco dei dispositivi della console di Lookout MTP

Questo problema può verificarsi in uno dei seguenti scenari:
* Se l'utente che possiede il dispositivo non appartiene al gruppo **Enrollment Group** (Gruppo di registrazione) specificato nella **console di Lookout MTP**.  Nel modulo **System** (Sistema), andare alla scheda **Intune Connector** ed esaminare le impostazioni **Enrollment Management** (Gestisci registrazione).  Saranno presenti uno o più gruppi di Azure AD configurati per la registrazione.  Verificare che l'utente proprietario del dispositivo mancante appartenga a uno dei gruppi Azure AD specificati.  Dopo che un nuovo utente viene aggiunto al gruppo di registrazione sarà necessario un tempo massimo pari all'intervallo di polling (5 minuti è il valore predefinito) perché il dispositivo appaia nel modulo **Devices** (Dispositivi) della console di Lookout MTP.

* Se il dispositivo non è supportato da Lookout MTP.  I dispositivi che sono non supportati appaiono nella sezione **Managed Devices** (Dispositivi gestiti) delle impostazioni connettore nella console di Lookout MTP.

### <a name="device-continues-to-be-reported-as-pending"></a>Il dispositivo continua a essere segnalato come **Pending** (In sospeso)

Se un dispositivo risulta **Pending**  (In sospeso), l'utente finale non ha aperto l'app Lookout for Work e non ha toccato il pulsante **Activate** (Attiva). Per altri dettagli sull'attivazione del dispositivo con l'app Lookout for Work, leggere l'argomento seguente:

[Richiesta di installare Lookout for Work](https://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Nella console di Lookout MTP un dispositivo appare come attivo, ma non ha un ID dispositivo.
Ciò significa che l'utente che possiede il dispositivo non appartiene al gruppo di registrazione specificato nella console di Lookout MTP.   Un dispositivo può assumere questo stato se l'utente che lo possiede è stato rimosso dal gruppo di registrazione o se il gruppo di registrazione a cui appartiene l'utente è stato rimosso.

Nel modulo **System** (Sistema) della console di Lookout MTP, andare alla scheda **Intune Connector** ed esaminare le impostazioni **Enrollment** (Registrazione).  Saranno presenti uno o più gruppi di Azure AD configurati per la registrazione.  Verificare che l'utente proprietario del dispositivo appartenga a uno dei gruppi Azure AD specificati.

Quando un dispositivo è in questo stato, Lookout continua a notificare all'utente le eventuali minacce rilevate, ma non invia informazioni relative alle minacce a Intune.

### <a name="device-shows-disconnected-state"></a>Lo stato del dispositivo è disconnesso

Se lo stato il dispositivo è disconnesso, Lookout MTP non ha ricevuto comunicazioni dal dispositivo per un periodo superiore all'intervallo preconfigurato (il valore predefinito è 30 giorni, con un minimo di 7 giorni). Ciò significa che l'app Portale aziendale o l'app Lookout for Work non è installata nel dispositivo o è stata disinstallata. La reinstallazione dell'app dovrebbe risolvere il problema. Quando l'utente apre Lookout for Work e attiva l'app, il dispositivo ripete la sincronizzazione con Lookout MTP e Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forzare la risincronizzazione del dispositivo
Dal modulo **Devices** (Dispositivi) della console di Lookout MTP, l'amministratore può selezionare il dispositivo e scegliere di eliminarlo.   Quando il proprietario del dispositivo apre di nuovo l'app Lookout for Work e tocca **Activate** (Attiva), verrà eseguita una risincronizzazione completa dello stato del dispositivo.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>Il proprietario del dispositivo non usa più il dispositivo
È necessario cancellare i dati del dispositivo e richiedere al nuovo utente di eseguire la registrazione come descritto in [questo argomento](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


È anche possibile passare al modulo **Devices** (Dispositivi) della console di Lookout MTP e scegliere **Elimina**.

Se il nuovo utente è incluso in uno dei gruppi di registrazione specificati nella console di Lookout MTP, il dispositivo viene visualizzato una volta che Azure AD lo associa al nuovo utente.

## <a name="compliance-remediation-workflows"></a>Flussi di lavoro per risolvere i problemi di conformità
[Richiesta di installare Lookout for Work]( https://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[È necessario risolvere una minaccia trovata da Lookout for Work](https://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
