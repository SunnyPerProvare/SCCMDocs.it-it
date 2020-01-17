---
title: Impostazioni di Windows Hello for Business
titleSuffix: Configuration Manager
description: Informazioni su come integrare Windows Hello for Business con Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 134f5e718fc72eddc2264ef5864c93bd519378c0
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75819302"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Impostazioni di Windows Hello for Business in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--1245704-->
Configuration Manager si integra con Windows Hello for Business. Questa funzionalità era nota in precedenza come Microsoft Passport for Work. Windows Hello for business è un metodo di accesso alternativo per i dispositivi Windows 10. Usa Active Directory o un account di Azure Active Directory (Azure AD) per sostituire una password, una smart card o una smart card virtuale. Hello for Business consente di eseguire l'accesso usando un *movimento dell'utente* anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo come un lettore di impronte digitali.

> [!Important]  
> A partire dalla versione 1910, l'autenticazione basata su certificati con le impostazioni di Windows Hello for business in Configuration Manager non è supportata. Per altre informazioni, vedere [Funzionalità deprecate](/configmgr/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). L'autenticazione basata su chiavi è ancora valida.
>
> La distribuzione di Active Directory Federation Services Registration Authority (ADFS RA) è più semplice, offre un'esperienza utente migliore e consente un'esperienza di registrazione certificati più deterministica. Usare ADFS RA per l'autenticazione basata su certificati con Windows Hello for business.
>
> Per i dispositivi con co-gestione, provare a trasferire il [carico di lavoro **criteri di accesso alle risorse** ](/configmgr/comanage/workloads#resource-access-policies) in Intune. Usare quindi i criteri di Intune per gestire questi certificati. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](/configmgr/comanage/how-to-switch-workloads).

Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/configmgr/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  

Configuration Manager si integra con Windows Hello for Business nei modi seguenti:  

- Controllare quali movimenti possono e non possono essere usati dagli utenti per accedere.  

- Archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](/configmgr/protect/deploy-use/introduction-to-certificate-profiles).  

- Creare e distribuire un profilo Windows Hello for business per controllarne le impostazioni nei dispositivi Windows 10 aggiunti a un dominio che eseguono il client di Configuration Manager. A partire dalla versione 1910, non è possibile usare l'autenticazione basata su certificati. Quando si usa l'autenticazione basata su chiavi non è necessario distribuire un profilo certificato.

## <a name="configure-a-profile"></a>Configurare un profilo  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **impostazioni di conformità**, **accesso risorse aziendali**e selezionare il nodo **profili di Windows Hello for business** .

1. Sulla barra multifunzione selezionare **Crea profilo Windows Hello for business** per avviare la creazione guidata profilo.

1. Nella pagina **generale** specificare un nome e una descrizione facoltativa per il profilo.

1. Nella pagina **piattaforme supportate** selezionare le versioni del sistema operativo a cui deve essere applicato questo profilo.

1. Nella pagina **Impostazioni** configurare le impostazioni seguenti:

    - **Configurare Windows Hello for business**: specificare se questo profilo Abilita, Disabilita o non configura Hello for business.

    - **Usa un modulo TPM (Trusted Platform Module)** : Un TPM (Trusted Platform Module) fornisce un livello aggiuntivo di sicurezza dei dati. Scegliere uno dei valori seguenti:  

      - **Richiesto**: Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.  

      - **Preferito**: I dispositivi provano a usare prima un modulo TPM. Se non è disponibile, possono usare la crittografia software.

    - **Metodo di autenticazione**: impostare questa opzione su **non configurato** o **basato su chiave**.

        > [!NOTE]
        > A partire dalla versione 1910, l'autenticazione basata su certificati con le impostazioni di Windows Hello for business in Configuration Manager non è supportata.

    - **Configurare la lunghezza minima del pin**: se si desidera richiedere una lunghezza minima per il PIN dell'utente, abilitare questa opzione e specificare un valore. Se abilitata, il valore predefinito è `4`.

    - **Configurare la lunghezza massima del pin**: se si desidera richiedere una lunghezza massima per il PIN dell'utente, abilitare questa opzione e specificare un valore. Quando è abilitata, il valore predefinito è `127`.

    - **Richiedi scadenza PIN (giorni)** : Specifica il numero di giorni prima che l'utente debba modificare il PIN del dispositivo.

    - **Impedisci riutilizzo dei PIN precedenti**: non consentire agli utenti di usare pin usati in precedenza.

    - **Richiedi lettere maiuscole nel PIN**: specifica se gli utenti devono includere lettere maiuscole nel PIN di Windows Hello for Business. Scegliere tra:  

      - **Consentito**: gli utenti possono usare caratteri maiuscoli nel PIN, ma non è obbligatorio.

      - **Richiesto**: gli utenti devono includere almeno un carattere maiuscolo nel PIN.  

      - **Non consentito**: gli utenti non possono usare caratteri maiuscoli nel PIN.  

    - **Richiedi lettere minuscole nel PIN**: specifica se gli utenti devono includere lettere minuscole nel PIN di Windows Hello for Business. Scegliere tra:  

      - **Consentito**: gli utenti possono usare caratteri minuscoli nel PIN, ma non è obbligatorio.

      - **Richiesto**: gli utenti devono includere almeno un carattere minuscolo nel PIN.  

      - **Non consentito**: gli utenti possono usare caratteri minuscoli nel PIN.  

    - **Configurare i caratteri speciali**: Specifica l'uso di caratteri speciali nel PIN. Scegliere tra:  

        > [!NOTE]
        > I caratteri speciali includono il seguente set:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Consentito**: gli utenti possono usare caratteri speciali nel PIN, ma non è obbligatorio.  

      - **Richiesto**: gli utenti devono includere almeno un carattere speciale nel PIN.  

      - **Non consentito**: gli utenti non possono usare caratteri speciali nel PIN. Questo comportamento è anche se l'impostazione **non è configurata**.  

    - **Configurare l'uso delle cifre nel pin**: specifica l'uso dei numeri nel pin. Scegliere tra:

      - **Consentito**: gli utenti possono usare numeri nel pin, ma non è necessario.  

      - **Obbligatorio**: gli utenti devono includere almeno un numero nel pin.  

      - **Non consentito**: gli utenti non possono usare numeri nel pin.

    - **Abilitare i movimenti biometrici**: usare l'autenticazione biometrica, ad esempio il riconoscimento facciale o l'impronta digitale. Queste modalità rappresentano un'alternativa a un PIN per Windows Hello for business. Gli utenti devono comunque configurare un PIN in caso di errore dell'autenticazione biometrica.  

      Se impostato su **Sì**, Windows Hello for Business consente l'autenticazione biometrica. Se impostato su **No**, Windows Hello for Business impedisce l'autenticazione biometrica per tutti i tipi di account.  

    - **Usa anti-spoofing avanzato**: configura l'anti-spoofing avanzato nei dispositivi che lo supportano. Se impostato su **Sì**, Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per le caratteristiche del viso, se supportata.  

    - **Usa l'accesso tramite telefono**: configura l'autenticazione a due fattori con un telefono cellulare.

1. Completare la procedura guidata.

Lo screenshot seguente è un esempio di impostazioni del profilo di Windows Hello for business:  

![Creazione guidata dei criteri di Windows Hello for Business, con l'elenco delle impostazioni disponibili](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Configurare le autorizzazioni

1. In qualità di amministratore di dominio o di credenziali equivalenti, accedere a una workstation amministrativa sicura con la seguente funzionalità facoltativa installata: strumenti di amministrazione remota del server: Active Directory Domain Services e Lightweight Directory Services.

1. Aprire la console **Utenti e computer di Active Directory**.

1. Selezionare il dominio, andare al menu **azione** e selezionare **Proprietà**.

1. Passare alla scheda **sicurezza** e selezionare **Avanzate**.

    > [!TIP]
    > Se la scheda **sicurezza** non è visualizzata, chiudere la finestra Proprietà. Passare al menu **Visualizza** e selezionare **funzionalità avanzate**.

1. Selezionare **Aggiungi**.

1. Scegliere **selezionare un'entità** e immettere `Key Admins`.

1. Dall'elenco **Si applica a** scegliere **Oggetti Utente discendenti**.

1. Nella parte inferiore della pagina selezionare **Clear All (Cancella tutto**).

1. Nella sezione **Proprietà** selezionare **Leggi msDS-KeyCredentialLink**.

1. Selezionare **OK** per salvare le modifiche e chiudere tutte le finestre.

## <a name="next-steps"></a>Passaggi successivi

[Profili certificato](/configmgr/protect/deploy-use/introduction-to-certificate-profiles)
