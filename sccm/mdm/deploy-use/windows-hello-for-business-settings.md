---
title: Impostazioni di Windows Hello for Business
titleSuffix: Configuration Manager
description: Informazioni su come integrare Windows Hello for Business con Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e177eb752becbe020e41b914694e86e3926ca32
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519685"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager-hybrid"></a>Impostazioni di Windows Hello for business in Configuration Manager (ibrido)

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager consente l'integrazione con Windows Hello for Business (in precedenza Microsoft Passport per Windows), che rappresenta un metodo di accesso alternativo per i dispositivi Windows 10. Hello for Business usa Active Directory o un account di Azure Active Directory per sostituire una password, una smart card o una smart card virtuale. Hello for Business consente di eseguire l'accesso usando un **movimento dell'utente** anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo esterno come un lettore di impronte digitali.  

> [!Important]  
> Da dicembre 2017 le impostazioni di Windows Hello for Business in Configuration Manager sono una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). La distribuzione di Active Directory Federation Services Registration Authority (ADFS RA) di Windows Server 2016 è più semplice, offre un'esperienza utente migliore e consente un'esperienza di registrazione certificati più deterministica. Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).  


Configuration Manager si integra con Windows Hello per le aziende in due modi:  

- È possibile usare Configuration Manager per controllare i movimenti che gli utenti possono utilizzare o meno per l'accesso.  

- È possibile archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](create-pfx-certificate-profiles.md).  

- È possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 che eseguono il client di Configuration Manager. Questa configurazione è descritta in [Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10](/sccm/protect/deploy-use/windows-hello-for-business-settings#configure-permissions). Quando si usa Configuration Manager con Intune (ibrido), è possibile configurare queste impostazioni nei dispositivi Windows 10 e Windows 10 Mobile, ma non su dispositivi appartenenti a un dominio che eseguono il client di Configuration Manager.   

Per informazioni generali sulla configurazione delle impostazioni di Windows Hello for business, vedere [le impostazioni di Windows Hello for business in Configuration Manager](/sccm/protect/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurare le impostazioni di Windows Hello per le aziende (ibrido)  

1. Nella console di Configuration Manager fare clic su **Amministrazione** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

2. Nell'elenco selezionare la sottoscrizione a Microsoft Intune e quindi nel gruppo **Sottoscrizione** della scheda **Home** fare clic su **Configura piattaforme** > **Windows (MDM)** .  

3. Nella scheda **Windows Hello for Business** della finestra di dialogo **Sottoscrizione a Microsoft Intune - Proprietà** scegliere tra i valori seguenti, che avranno effetto sui tutti i dispositivi Windows 10 e Windows 10 Mobile registrati:  

   - **Disabilita Windows Hello for Business per i dispositivi registrati** o **Abilita Windows Hello for Business per i dispositivi registrati** - Abilita o disabilita l'uso di Windows Hello for Business in tutti i dispositivi Windows 10 e Windows 10 Mobile registrati.  

   - **Usa un modulo TPM (Trusted Platform Module)** : un chip TPM (Trusted Platform Module) offre un livello aggiuntivo di sicurezza dei dati. Scegliere uno dei valori seguenti:  

     -   **Obbligatorio** (impostazione predefinita) - Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.  

     -   **Preferito**: i dispositivi provano a usare prima un modulo TPM. Se questo non è disponibile, possono usare la crittografia software.  

   - **Richiedi lunghezza minima del PIN** - Specificare il numero minimo di caratteri necessari per il PIN di Windows Hello for Business. È necessario usare almeno 4 caratteri (il valore predefinito è 6 caratteri).  

   - **Richiedi lunghezza massima del PIN** - Specificare il numero massimo di caratteri consentiti per il PIN di Windows Hello for Business. È possibile usare fino a 127 caratteri.  

   - **Richiedi lettere minuscole nel PIN** - Specifica se è necessario usare lettere minuscole nel PIN di Windows Hello for Business. Scegliere tra:  

     -   **Consentito** - Gli utenti possono usare caratteri minuscoli nel PIN.  

     -   **Obbligatorio** - Gli utenti devono includere almeno un carattere minuscolo nel PIN.  

     -   **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri minuscoli nel PIN.  

   - **Richiedi lettere maiuscole nel PIN** - Specifica se è necessario usare lettere maiuscole nel PIN di Windows Hello for Business. Scegliere tra:  

     -   **Consentito** - Gli utenti possono usare caratteri maiuscoli nel PIN.  

     -   **Obbligatorio** - Gli utenti devono includere almeno un carattere maiuscolo nel PIN.  

     -   **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri maiuscoli nel PIN.  

   - **Richiedi caratteri speciali** - Specifica l'uso di caratteri speciali nel PIN. Scegliere tra:  

     - **Consentito** - Gli utenti possono usare caratteri speciali nel PIN.  

     - **Obbligatorio** - Gli utenti devono includere almeno un carattere speciale nel PIN.  

     - **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri speciali nel PIN (questo è anche il comportamento se l'impostazione non è configurata).  

       I caratteri speciali includono: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~** .  

   - **Richiedi scadenza PIN (giorni)** - Specifica il numero di giorni prima che sia necessario modificare il PIN del dispositivo. L'impostazione predefinita è 41 giorni.  

   - **Impedisci riutilizzo dei PIN precedenti** - Usare questa impostazione per limitare il riutilizzo dei PIN usati in precedenza. L'impostazione predefinita impedisce il riutilizzo degli ultimi 5 PIN usati.  

   - **Abilita movimenti biometrici** - Abilita l'autenticazione biometrica, ad esempio il riconoscimento facciale o delle impronte digitali, come alternativa a un PIN di Windows Hello for Business. Gli utenti devono comunque configurare un PIN aziendale in caso di errore dell'autenticazione biometrica.  

      Se impostato su **Abilitato**, Windows Hello for Business consente l'autenticazione biometrica.  Se impostato su **Disabilitato**, Windows Hello for Business impedisce l'autenticazione biometrica (per tutti i tipi di account).  

   - **Usa anti-spoofing avanzato, se disponibile** - Configura l'uso della funzionalità avanzata di anti-spoofing nei dispositivi che la supportano.  

      Se impostato su **Abilitato**, Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per le caratteristiche del viso, se supportata.  

   - **Usare Passport remoto** - Se questa opzione è impostata su **Abilitato**, gli utenti possono usare Hello for Business come dispositivo portatile complementare per l'autenticazione del computer desktop. Il computer desktop deve essere aggiunto ad Azure Active Directory e il dispositivo complementare deve essere configurato con un PIN di Windows Hello for Business.  

4. Al termine, fare clic su **OK**.  



## <a name="see-also"></a>Vedere anche  

[Proteggere i dati e l'infrastruttura del sito](/sccm/protect/understand/protect-data-and-site-infrastructure)

[Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)  
