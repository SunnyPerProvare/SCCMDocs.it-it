---
title: Gestire il blocco attivazione iOS | Microsoft Docs
description: Gestire il blocco attivazione iOS con System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 88bef04a52f716ae13afc21c25d33dea06a3fc9c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Gestire il blocco attivazione iOS con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Quando il blocco attivazione iOS è abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima che sia possibile:

- Disattivare Trova il mio iPhone
- Cancellare il dispositivo
- Riattivare il dispositivo

Nei dispositivi **senza supervisione** il blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone.

Nei dispositivi **son supervisione** è necessario attivare il blocco attivazione tramite le impostazioni di conformità di Configuration Manager.

> [!TIP]
> Nella modalità supervisionata per i dispositivi iOS è possibile usare lo strumento Apple Configurator per bloccare un dispositivo e limitarne la funzionalità per specifici scopi aziendali. Questa modalità è in genere usata solo per dispositivi di proprietà dell'azienda.

Anche se il blocco attivazione consente di proteggere i dispositivi iOS e di aumentare le possibilità di ripristino in caso di smarrimento o furto del dispositivo, questa funzionalità può presentare una serie di difficoltà per gli amministratori IT. Ad esempio:

- Uno degli utenti configura Blocco attivazione in un dispositivo. L'utente lascia la società e restituisce il dispositivo. Senza l'ID Apple e la password dell'utente il dispositivo non può essere riattivato in alcun modo, neanche cancellandolo.
- È necessario creare un report di tutti i dispositivi in cui è abilitato il blocco attivazione.
- Durante un aggiornamento dei dispositivi nell'organizzazione si vuole riassegnare alcuni dispositivi a un reparto diverso. È possibile riassegnare solo i dispositivi per cui non è abilitato il blocco attivazione.


Per facilitare la soluzione di questi problemi, Apple ha introdotto il bypass di Blocco attivazione in iOS 7.1 che consente di rimuovere Blocco attivazione dai dispositivi supervisionati senza richiedere Apple ID e password dell'utente. I dispositivi supervisionati possono generare un codice bypass di Blocco attivazione specifico, che viene archiviato nel server di attivazione di Apple.

Altre informazioni sul blocco attivazione sono disponibili [qui](https://support.apple.com/HT201365).

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Come gestire il blocco di attivazione con Configuration Manager

Configuration Manager consente di gestire il blocco attivazione in due modi:

1. Abilitando il blocco attivazione nei dispositivi con supervisione.
2. Effettuando il bypass del blocco attivazione nei dispositivi con supervisione.

> [!IMPORTANT]
> Non è possibile eseguire il bypass del blocco attivazione nei dispositivi con supervisione.

I vantaggi garantiti alle aziende da questa funzionalità sui dispositivi di proprietà dell'azienda sono:



- L'utente può usufruire dei vantaggi dell'app Trova il mio iPhone in termini di sicurezza.
- L'amministratore può consentire all'utente di continuare a lavorare sapendo che, in caso di ridestinazione del dispositivo, potrà ritirarlo o sbloccarlo.


## <a name="enable-activation-lock-on-supervised-devices"></a>Abilitare il blocco attivazione nei dispositivi con supervisione

Per abilitare il blocco attivazione nei dispositivi con supervisione, si usano le impostazioni di conformità di Configuration Manager per creare e distribuire un elemento di configurazione di tipo **iOS e Mac OS X** :

1. Usare le informazioni nell'argomento [Come creare elementi di configurazione per dispositivi iOS e Mac OS X gestiti senza il client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) per creare un elemento di configurazione di tipo **iOS e Mac OS X**.
2. Nella pagina **Protezione del sistema** della Creazione guidata dell'elemento di configurazione configurare l'impostazione **Consenti blocco attivazione (solo modalità di supervisione)** su **Consentito**.
3. [Aggiungere l'elemento di configurazione a una linea di base di configurazione](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Distribuire questa linea di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines) a una raccolta contenente i dispositivi iOS per i quali si vuole abilitare il blocco di attivazione.

> [!IMPORTANT]
> Assicurarsi di essere fisicamente in possesso del dispositivo prima di eseguire questa procedura. In caso contrario, il bypass del blocco attivazione verrà eseguito e chiunque sia in possesso del dispositivo avrà accesso completo ad esso e potrà disattivare Trova il mio iPhone, cancellare il dispositivo o riattivarlo.

È possibile eseguire il bypass del blocco attivazione o recuperare il codice di bypass del blocco solo per i dispositivi con supervisione. Se si tenta di eseguire il bypass del blocco attivazione per i dispositivi senza supervisione o di visualizzare i risultati del codice di bypass, si ottiene un errore.



## <a name="view-the-activation-lock-bypass-code"></a>Visualizzare il codice di bypass del blocco attivazione

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi**.
3. Selezionare un dispositivo registrato in modalità di supervisione e con blocco attivazione abilitato.
4. Nella scheda **Home** , nel gruppo **Dispositivo** , fare clic su **Azioni remote dispositivo** > **Visualizza il codice di bypass del blocco attivazione**.
5. Nella finestra di dialogo **Visualizza il codice di bypass del blocco attivazione** è visualizzato il codice di bypass per il dispositivo selezionato.

## <a name="bypass-activation-lock"></a>Eseguire il bypass del blocco attivazione

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi**.
3. Selezionare un dispositivo registrato in modalità di supervisione e con blocco attivazione abilitato.
3. Nella scheda **Home** , nel gruppo **Dispositivo** , fare clic su **Azioni remote dispositivo** > **Bypass del blocco attivazione**.
5. Leggere i messaggi nella finestra di dialogo di avviso e fare clic su **Sì** quando si è pronti a proseguire.
6. È possibile esaminare lo stato della richiesta di sblocco tramite:

    - I dati di individuazione per il dispositivo nella finestra di dialogo delle proprietà del dispositivo.
    - La colonna **Stato di bypass del blocco attivazione** nella vista **Dispositivi** questa colonna è nascosta.
    - La sezione **Informazioni sulle azioni remote dei dispositivi** nella scheda **Riepilogo** del riquadro dei dettagli, quando è selezionato un dispositivo.
