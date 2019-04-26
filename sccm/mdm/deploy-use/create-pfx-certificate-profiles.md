---
title: Creare profili certificato PFX usando un'autorità di certificazione
titleSuffix: Configuration Manager
description: Informazioni su come usare i file PFX in System Center Configuration Manager per generare i certificati specifici dell'utente che supportano lo scambio di dati crittografati.
ms.date: 11/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bbe52a282db016077cb96144938a0d443955f6c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62224670"
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Come creare profili certificato PFX usando un'autorità di certificazione

*Si applica a: System Center Configuration Manager (Current Branch)*

Viene illustrato come creare un profilo certificato che usa un'autorità di certificazione per le credenziali.

L'argomento [Introduzione ai profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md) contiene informazioni generali sulla creazione e la configurazione dei profili certificato ed evidenzia alcune informazioni specifiche sui profili certificato relative ai certificati PFX.

## <a name="pfx-certificate-profiles"></a>Profili certificato PFX
System Center Configuration Manager consente di creare un profilo certificato PFX usando le credenziali rilasciate da un'autorità di certificazione.  A partire dalla versione 1706, è possibile scegliere Microsoft o Entrust come autorità di certificazione.  I file PFX (Personal Information Exchange), quando vengono distribuiti nei dispositivi utente, generano certificati specifici dell'utente per supportare lo scambio di dati crittografato.

Per importare le credenziali dai file dei certificati esistenti, vedere [How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/import-pfx-certificate-profiles.md) (Come creare profili certificato PFX importando i dettagli dei certificati).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creare e distribuire un profilo certificato PFX (Personal Information Exchange)  

### <a name="get-started"></a>Introduzione

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  
2.  Nell'area di lavoro **Asset e conformità** scegliere **Impostazioni di conformità** &gt; **Accesso risorse aziendali** &gt; **Profili certificati**.  

3.  Nella scheda **Home** del gruppo **Crea** scegliere **Crea profilo certificato**.

4.  Nella pagina **Generale** della **Creazione guidata profilo certificato** specificare le informazioni seguenti:  

    -   **Nome**: Immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    -   **Descrizione**: digitare una descrizione che offra una panoramica del profilo certificato e altre informazioni rilevanti per facilitarne l'identificazione nella console di System Center Configuration Manager. È possibile usare un massimo di 256 caratteri.  

    -   In **Specificare il tipo di profilo certificato che si desidera creare** scegliere **Personal Information Exchange -- Impostazioni di PKCS #12 (PFX) -- Crea** e quindi scegliere l'autorità di certificazione dall'elenco a discesa.  A partire dalla versione 1706, è possibile scegliere **Microsoft** o **Entrust**.

### <a name="select-supported-platforms"></a>Selezionare le piattaforme supportate

La pagina Piattaforme supportate identifica i sistemi operativi e i dispositivi supportati dal profilo certificato.  

I profili certificato possono supportare più sistemi operativi e dispositivi, ma determinate combinazioni di sistema operativo o dispositivo possono richiedere impostazioni diverse.  In questi casi, è meglio creare profili separati per ogni set univoco di impostazioni.  

A partire dalla versione 1710, sono disponibili le opzioni seguenti:

- Windows 10
    - Tutti i dispositivi Windows 10 (64 bit)
    - Tutti i dispositivi Windows 10 (32 bit)
    - Tutti i dispositivi Windows 10 (ARM64)
    - Tutti i dispositivi Windows 10 Holographic Enterprise e versioni successive
    - Tutti i dispositivi Windows 10 Holographic e versioni successive
    - Tutti i dispositivi Windows 10 Team e versioni successive
    - Tutti i dispositivi Windows 10 Mobile e versioni successive
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> I dispositivi MacOS/OSX non sono attualmente supportati.  

Quando non vengono selezionate altre opzioni, la casella di controllo **Seleziona tutto** seleziona tutte le opzioni disponibili.  Quando viene selezionata una o più opzioni, **Seleziona tutto** cancella le selezioni esistenti. 

1.  Selezionare uno o più piattaforme supportate dal profilo certificato.

1.  Scegliere **Avanti** per continuare.  


### <a name="configure-certification-authorities"></a>Configurare le autorità di certificazione

È possibile scegliere il punto di registrazione certificati per elaborare i certificati PFX.  

1.  Nell'elenco **Sito primario** scegliere il server contenente il ruolo Punto di registrazione certificati per l'autorità di certificazione.
1.  Nell'elenco **Autorità di certificazione** scegliere l'autorità di certificazione pertinente inserendo un segno di spunta nella colonna sinistra.
1.  Quando si è pronti per continuare, scegliere **Avanti**.

Per altre informazioni, vedere [Infrastruttura di certificazione](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Configurare le impostazioni del certificato per l'autorità di certificazione Microsoft

Per configurare le impostazioni del certificato quando si usa Microsoft come autorità di certificazione:

1.  Nell'elenco a discesa **Nome del modello di certificato** scegliere il modello di certificato.

1.  Abilitare la casella di controllo **Utilizzo del certificato** per usare il profilo certificato per la firma o la crittografia S/MIME.

    Quando si seleziona questa opzione mentre si usa Microsoft come autorità di certificazione, tutti i certificati PFX associati all'utente di destinazione vengono distribuiti in tutti i dispositivi registrati dall'utente.  Quando questa casella di controllo viene deselezionata, ogni dispositivo riceve un certificato univoco.  

1.  Impostare **Formato nome soggetto** su **Nome comune** o su **Nome distinto completo**.  In caso di dubbi su quale usare, contattare l'amministratore dell'autorità di certificazione.

1.  Per **Nome alternativo del soggetto**, abilitare **Indirizzo di posta elettronica** e **Nome dell'entità utente (UPN)** in modo appropriato per l'autorità di certificazione.

1.  **Soglia di rinnovo** determina quando i certificati vengono automaticamente rinnovati, in base alla percentuale di tempo rimanente prima della scadenza.

1.  Impostare **Periodo di validità del certificato** sulla durata del certificato.  Per specificare il periodo, impostare un numero (1-100) e un periodo (anni, mesi o giorni).

1.  **Pubblicazione di Active Directory** viene abilitata quando il punto di registrazione certificati specifica le credenziali di Active Directory.  Abilitare l'opzione per pubblicare il profilo certificato in Active Directory.

1.  Se è stata selezionata una o più piattaforme Windows 10 quando si sono specificate le piattaforme supportate:

    1.  Impostare **Archivio certificati Windows** su **Utente**.  L'opzione **Computer locale** non distribuisce i certificati e non è consigliabile.
    1.  Selezionare **Provider di archiviazione chiavi** da una delle opzioni seguenti:

        - **Installa in TPM (Trusted Platform Module) se presente**  
        - **Installa in TPM (Trusted Platform Module) in caso di errore** 
        - **Installa in Windows Hello for Business oppure genera errore** 
        - **Installa nel provider di archiviazione chiavi software** 

1.  Al termine, scegliere **Avanti** o **Riepilogo**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Configurare le impostazioni del certificato per l'autorità di certificazione Entrust

Per configurare le impostazioni del certificato quando si usa Entrust come autorità di certificazione:

1.  Nell'elenco a discesa **Configurazione dell'ID digitale** scegliere il profilo di configurazione.  Le opzioni di configurazione dell'ID digitale vengono create dall'amministratore di Entrust.

1.  Se selezionato, **Utilizzo del certificato** usa il profilo certificato per la firma o la crittografia S/MIME.

    Quando si usa Entrust come autorità di certificazione, tutti i certificati PFX associati all'utente di destinazione vengono distribuiti in tutti i dispositivi registrati dall'utente.    Quando questa opzione *non* viene selezionata, ogni dispositivo riceve un certificato univoco.  Il comportamento è diverso a seconda dell'autorità di certificazione. Per altre informazioni, vedere la sezione corrispondente.

1.  Usare il pulsante **Formatta** per eseguire il mapping dei token **Formato nome soggetto** di Entrust ai campi ConfigMgr.  

    La finestra di dialogo **Certificate Name Formatting** (Formattazione del nome del certificato) elenca le variabili di configurazione dell'ID digitale di Entrust.  Per ogni variabile di Entrust, scegliere la variabile LDAP appropriata nell'elenco a discesa associato.

1.  Usare il pulsante **Formatta** per eseguire il mapping dei token **Nome alternativo del soggetto** di Entrust alle variabili LDAP supportate.  

    La finestra di dialogo **Certificate Name Formatting** (Formattazione del nome del certificato) elenca le variabili di configurazione dell'ID digitale di Entrust.  Per ogni variabile di Entrust, scegliere la variabile LDAP appropriata nell'elenco a discesa associato.

1.  **Soglia di rinnovo** determina quando i certificati vengono automaticamente rinnovati, in base alla percentuale di tempo rimanente prima della scadenza.

1.  Impostare **Periodo di validità del certificato** sulla durata del certificato.  Per specificare il periodo, impostare un numero (1-100) e un periodo (anni, mesi o giorni).

1.  **Pubblicazione di Active Directory** viene abilitata quando il punto di registrazione certificati specifica le credenziali di Active Directory.  Abilitare l'opzione per pubblicare il profilo certificato in Active Directory.

1.  Se è stata selezionata una o più piattaforme Windows 10 quando si sono specificate le piattaforme supportate:

    1.  Impostare **Archivio certificati Windows** su **Utente**.  L'opzione **Computer locale** non distribuisce i certificati e non è consigliabile.
    1.  Selezionare **Provider di archiviazione chiavi** da una delle opzioni seguenti:

        - **Installa in TPM (Trusted Platform Module) se presente**  
        - **Installa in TPM (Trusted Platform Module) in caso di errore** 
        - **Installa in Windows Hello for Business oppure genera errore** 
        - **Installa nel provider di archiviazione chiavi software** 

1.  Al termine, scegliere **Avanti** o **Riepilogo**.


### <a name="finish-up"></a>Terminare

1.  Nella pagina Riepilogo esaminare gli elementi selezionati e verificare le scelte.

1.  Quando si è pronti, scegliere **Avanti** per creare il profilo.  

1.  Il profilo certificato contenente il file PFX è ora disponibile nell'area di lavoro **Profili certificato** . 

1.  Per distribuire il profilo:

    1. Aprire l'area di lavoro **Asset e conformità**.
    1. Scegliere **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profili certificato**
    1. Fare clic con il pulsante destro del mouse sul profilo certificato desiderato e quindi scegliere **Distribuisci**. 


## <a name="see-also"></a>Vedere anche
La sezione [Creare un nuovo profilo di certificato](../../protect/deploy-use/create-certificate-profiles.md) illustra la Creazione guidata profilo certificato.

[How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/import-pfx-certificate-profiles.md) (Come creare i profili certificato PFX importando i dettagli dei certificati)

[Distribuire profili certificato Wi-Fi, VPN e posta elettronica](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) illustra come distribuire i profili dei certificati.
