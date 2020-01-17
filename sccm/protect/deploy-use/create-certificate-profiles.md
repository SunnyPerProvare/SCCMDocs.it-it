---
title: Creare profili certificato SCEP
titleSuffix: Configuration Manager
description: Informazioni su come usare i profili certificato per effettuare il provisioning dei dispositivi gestiti con i certificati necessari.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fe0be3f57f5842405f614b7227a534f27b39b115
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75820577"
---
# <a name="create-certificate-profiles"></a>Creare i profili certificato

*Si applica a: Configuration Manager (Current Branch)*

Usare i profili certificato in Configuration Manager per effettuare il provisioning dei certificati necessari ai dispositivi gestiti per accedere alle risorse aziendali. Prima di creare i profili certificato, configurare l'infrastruttura di certificazione come descritto in [Configurare l'infrastruttura di certificazione per System Center Configuration Manager](/configmgr/protect/deploy-use/certificate-infrastructure).  

> [!TIP]
> Per i dispositivi con co-gestione, provare a trasferire il [carico di lavoro **criteri di accesso alle risorse** ](/configmgr/comanage/workloads#resource-access-policies) in Intune. Usare quindi i criteri di Intune per gestire questi certificati. Per altre informazioni, vedere [Come trasferire i carichi di lavoro](/configmgr/comanage/how-to-switch-workloads).

Questo articolo descrive come creare profili certificato radice attendibile e Simple Certificate Enrollment Protocol (SCEP). Se si vuole creare profili certificato PFX, vedere [Creare profili certificato PFX](/configmgr/mdm/deploy-use/create-pfx-certificate-profiles) .

Per creare un profilo certificato:

1. Avviare la Creazione guidata profilo certificato.
1. Fornire informazioni generali sul certificato.
1. Configurare un certificato dell'autorità di certificazione (CA) attendibile.  
1. Configurare le informazioni sul certificato SCEP.  
1. Specificare le piattaforme supportate per il profilo certificato.

## <a name="start-the-wizard"></a>Avviare la procedura guidata  

Per avviare la Creazione guidata profilo certificato:

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**, espandere **Impostazioni di conformità**, espandere **Accesso risorse aziendali** e quindi selezionare il nodo **Profili certificati**.  

1. Nella scheda **Home** della barra multifunzione selezionare **Crea profilo certificato** nel gruppo **Crea**.  

## <a name="general"></a>Generale

Nella pagina **Generale** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

- **Nome**: Immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

- **Descrizione**: specificare una descrizione che fornisca una panoramica del profilo certificato. Includere anche altre informazioni rilevanti per facilitarne l'identificazione nella console di Configuration Manager. È possibile usare un massimo di 256 caratteri.  

- Specificare il tipo di profilo certificato che si vuole creare:

  - **Certificato CA attendibile**: Selezionare questo tipo di profilo certificato se si vuole distribuire un certificato CA radice attendibile o un certificato CA intermedio per formare una catena di certificati quando l'utente o il dispositivo deve autenticare un altro dispositivo. Ad esempio, il dispositivo può essere un server RADIUS (Remote Authentication Dial-In User Service) o un server di rete privata virtuale (VPN).
  
    Configurare anche un profilo certificato CA attendibile prima di creare un profilo certificato SCEP. In questo caso, il certificato CA attendibile deve essere per la CA che rilascia il certificato all'utente o al dispositivo.  

  - **Impostazioni di Simple Certificate Enrollment Protocol (SCEP)** : Selezionare questo tipo per richiedere un certificato per un utente o un dispositivo con il protocollo SCEP (Simple Certificate Enrollment Protocol) e il servizio del ruolo del servizio Registrazione dispositivi di rete (NDES).

  - **Scambio informazioni personali -- Impostazioni PKCS #12 (PFX) -- Importa**: Selezionare questa opzione per importare un certificato PFX. Per altre informazioni, vedere [Importare profili certificato PFX](/configmgr/mdm/deploy-use/import-pfx-certificate-profiles).

  - **Scambio informazioni personali -- Impostazioni PKCS #12 (PFX) -- Crea**: Selezionare questa opzione per elaborare i certificati PFX usando un'autorità di certificazione. Per altre informazioni, vedere [Creare profili certificato PFX](/configmgr/mdm/deploy-use/create-pfx-certificate-profiles).

## <a name="trusted-ca-certificate"></a>Certificato CA attendibile  

> [!IMPORTANT]  
> Prima di creare un profilo certificato SCEP è necessario configurare almeno un profilo certificato CA attendibile.
>
> Se si modifica uno di questi valori dopo aver distribuito il certificato, viene richiesto un nuovo certificato:
>
> - Provider di archiviazione chiavi
> - Nome modello di certificato
> - Tipo di certificato
> - Formato del nome soggetto
> - Nome alternativo soggetto
> - Periodo di validità del certificato
> - Utilizzo chiavi
> - Dimensione chiavi
> - Utilizzo chiavi avanzato
> - Certificato CA radice

1. Nella pagina **Certificato CA attendibile** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

    - **File di certificato**: selezionare **Importa**, quindi passare al file del certificato.  

    - **Archivio di destinazione**: per i dispositivi con più archivi certificati consente di selezionare il percorso in cui archiviare il certificato. Per i dispositivi con un solo archivio, questa impostazione viene ignorata.  

2. Usare il valore **Identificazione personale certificato** per accertarsi di aver importato il certificato corretto.  

## <a name="scep-certificates"></a>Certificati SCEP

### <a name="1-scep-servers"></a>1. Server SCEP

Nella pagina **Server SCEP** della Creazione guidata profilo certificato specificare gli URL per i server NDES che emetteranno i certificati tramite SCEP. È possibile assegnare automaticamente un URL NDES in base alla configurazione del punto di registrazione certificati o aggiungere manualmente gli URL.  

### <a name="2-scep-enrollment"></a>2. Registrazione SCEP

Completare la pagina **Registrazione SCEP** della Creazione guidata profilo certificato.

- **Tentativi**: specificare il numero di volte in cui il dispositivo ritenta automaticamente la richiesta di certificato al server registrazione dispositivi. Questa impostazione supporta lo scenario in cui un CA Manager deve approvare una richiesta di certificato prima dell'accettazione. Questa impostazione viene in genere usata per gli ambienti ad alta protezione o se si dispone di una CA emittente autonoma invece di una CA globale (enterprise). È anche possibile usare questa impostazione a scopo di test, in modo da poter ispezionare le opzioni di richiesta certificato prima che la richiesta certificato venga elaborata dalla CA emittente. Usare questa impostazione con l'opzione **Intervallo tra tentativi (minuti)** .  

- **Intervallo tra tentativi (minuti)** : Specificare l'intervallo in minuti tra ogni tentativo di registrazione quando si usa l'approvazione del responsabile CA prima che la richiesta di certificato venga elaborata dalla CA emittente. Se si usa l'approvazione del responsabile a scopo di test, specificare un valore basso. Non è quindi necessario attendere molto tempo prima che il dispositivo ritenti la richiesta di certificato dopo l'approvazione della richiesta.

    Se si utilizza l'approvazione del responsabile in una rete di produzione, specificare un valore più elevato. Questo comportamento consente all'amministratore della CA un tempo sufficiente per approvare o negare le approvazioni in sospeso.  

- **Soglia di rinnovo (%)** : specificare la percentuale di durata residua del certificato prima che il dispositivo richieda il rinnovo del certificato.  

- **Provider di archiviazione chiavi (KSP)** : Specificare dove viene archiviata la chiave per il certificato. Scegliere tra uno dei seguenti valori:  

  - **Installa in TPM (Trusted Platform Module) se presente**: Installa la chiave in TPM. Se il TPM non è presente, la chiave viene installata nel provider di archiviazione per la chiave software.  

  - **Installa in TPM (Trusted Platform Module) in caso di errore**: Installa la chiave nel TPM. Se il modulo TPM non è presente, l'installazione non riesce.  

  - **Installa in Windows Hello for Business oppure genera errore**: Questa opzione è disponibile per i dispositivi Windows 10. Consente di archiviare il certificato nell'archivio Windows Hello for business, che è protetto da autenticazione a più fattori. Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Questa opzione non supporta l'accesso con smart card per l'utilizzo chiavi avanzato nella pagina Proprietà certificato.

  - **Installa nel provider di archiviazione chiavi software**: Installa la chiave nel provider di archiviazione per la chiave software.  

- **Dispositivi per la registrazione del certificato**: se il profilo certificato viene distribuito in una raccolta utenti, consentire la registrazione dei certificati solo sul dispositivo primario dell'utente o su qualsiasi dispositivo a cui l'utente accede.

    Se il profilo certificato viene distribuito in una raccolta dispositivi, consentire la registrazione dei certificati solo per l'utente primario del dispositivo o per tutti gli utenti che eseguono l'accesso al dispositivo.  

### <a name="3-certificate-properties"></a>3. Proprietà certificato

Nella pagina **Proprietà certificato** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

- **Nome modello di certificato**: selezionare il nome di un modello di certificato configurato in registrazione dispositivi e aggiunto a una CA emittente. Per accedere correttamente ai modelli di certificato, l'account utente deve disporre dell'autorizzazione di **lettura** per il modello di certificato. Se non è possibile **cercare** il certificato, digitarne il nome.  

  > [!IMPORTANT]
  > Se il nome del modello di certificato contiene caratteri non ASCII, il certificato non viene distribuito. Un esempio di questi caratteri è riportato nell'alfabeto cinese. Per assicurarsi che il certificato venga distribuito, creare prima di tutto una copia del modello di certificato nell'autorità di certificazione. Rinominare quindi la copia usando caratteri ASCII.  

  - Se si *esplora* il percorso per selezionare il nome del modello di certificato, alcuni campi nella pagina vengono popolati automaticamente dal modello del certificato. In alcuni casi, non è possibile modificare questi valori, a meno che non si scelga un modello di certificato diverso.  

  - Se si *digita* il nome del modello di certificato, assicurarsi che il nome corrisponda esattamente a uno dei modelli di certificato. Deve corrispondere ai nomi elencati nel registro di sistema del server registrazione dispositivi. Accertarsi di specificare il nome del modello del certificato e non il nome visualizzato del modello del certificato.  

    Per trovare i nomi dei modelli di certificato, individuare la chiave del Registro di sistema seguente: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP`. I modelli di certificato vengono elencati come i valori per **EncryptionTemplate**, **GeneralPurposeTemplate**e **SignatureTemplate**. Per impostazione predefinita, il valore per i tre modelli di certificato è **IPSECIntermediateOffline**, che è associato al nome visualizzato del modello **IPSec (Offline request)** .  

    > [!WARNING]  
    > Quando si digita il nome del modello di certificato, Configuration Manager possibile verificare il contenuto del modello di certificato. Potrebbe essere possibile selezionare le opzioni non supportate dal modello di certificato, che potrebbe generare una richiesta di certificato non riuscita. In presenza di questo comportamento, verrà visualizzato un messaggio di errore per w3wp.exe nel file CPR.log per segnalare che il nome modello in CSR e la richiesta di verifica non corrispondono.  
    >
    > Quando si digita il nome del modello di certificato specificato per il valore **GeneralPurposeTemplate**, selezionare le opzioni **Crittografia chiave** e **Firma digitale** per il profilo certificato. Se si vuole abilitare solo l'opzione **Crittografia chiave** in questo profilo certificato, specificare il nome del modello di certificato per la chiave **EncryptionTemplate**. Analogamente, se si desidera abilitare solo l'opzione **Forma digitale** in questo profilo certificato, specificare il nome modello del certificato per la chiave **SignatureTemplate** .  

- **Tipo di certificato**: selezionare se il certificato verrà distribuito a un dispositivo o a un utente.  

- **Formato nome soggetto**: Selezionare in che modo Configuration Manager crea automaticamente il nome del soggetto nella richiesta di certificato. Se il certificato è per un utente, è anche possibile includere l'indirizzo di posta elettronica dell'utente nel nome del soggetto.

    > [!NOTE]  
    > Se si seleziona **Codice IMEI**  o **Numero di serie**, è possibile distinguere i diversi dispositivi appartenenti allo stesso utente. Tali dispositivi, ad esempio, potrebbero condividere il nome comune, ma non il codice IMEI o il numero di serie. Se il dispositivo non ha un codice IMEI o un numero di serie, il certificato viene emesso con il nome comune.

- **Nome alternativo soggetto**: Specificare in che modo Configuration Manager crea automaticamente i valori per il nome alternativo oggetto (SAN) nella richiesta certificato. Ad esempio, se si seleziona un tipo di certificato utente, è possibile includere il nome dell'entità utente (UPN) nel nome alternativo oggetto. Se il certificato client verrà usato per eseguire l'autenticazione in un server dei criteri di rete, impostare il nome alternativo oggetto sul nome dell'entità utente.  

- **Periodo di validità del certificato**: se si imposta un periodo di validità personalizzato sulla CA emittente, specificare la quantità di tempo rimanente prima della scadenza del certificato.

    > [!TIP]
    > Impostare un periodo di validità personalizzato con la seguente riga di comando: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Per altre informazioni su questo comando, vedere [infrastruttura di certificazione](/configmgr/protect/deploy-use/certificate-infrastructure).  

    È possibile specificare un valore inferiore, ma non superiore rispetto al periodo di validità nel modello di certificato indicato. Ad esempio, se il periodo di validità del certificato nel modello di certificato è di due anni, è possibile specificare un valore di un anno ma non un valore di cinque anni. Inoltre, il valore deve essere inferiore rispetto al periodo di validità rimanente del certificato della CA emittente.  

- **Utilizzo chiavi**: specificare le opzioni di uso delle chiavi per il certificato. È possibile scegliere una delle opzioni seguenti:  

  - **Crittografia chiave**: consentire lo scambio di chiavi solo quando la chiave è crittografata.  

  - **Firma digitale**: consentire lo scambio di chiavi solo se viene usata una firma digitale per proteggere la chiave.  

  Se è stato visualizzato un modello di certificato, non è possibile modificare queste impostazioni, a meno che non si selezioni un modello di certificato diverso.  

  Configurare il modello di certificato selezionato con una o entrambe le due opzioni di utilizzo della chiave sopra riportate. In caso contrario, verrà visualizzato il messaggio seguente nel file di registro del punto di registrazione certificati **Crp.log**: **Utilizzo chiave in CSR e richiesta di verifica non corrispondono**  

- **Dimensioni chiave (bit)** : Selezionare le dimensioni della chiave in bit.  

- **Utilizzo chiavi avanzato**: aggiungere valori per lo scopo designato del certificato. Nella maggior parte dei casi il certificato richiede l'**Autenticazione Client** in modo che l'utente o il dispositivo possa eseguire l'autenticazione a un server. È possibile aggiungere altri utilizzi di chiavi secondo necessità.  

- **Algoritmo hash**: selezionare uno dei tipi di algoritmo hash disponibili da usare con questo certificato. Selezionare il livello di sicurezza più avanzato supportato dai dispositivi che verranno connessi.  

  > [!NOTE]  
  > **SHA-2** supporta SHA-256, SHA-384 e SHA-512. **SHA-1** supporta solo SHA-3.  

- **Certificato CA radice**: Scegliere un profilo del certificato della CA radice già configurato e distribuito all'utente o al dispositivo. Questo certificato CA deve essere il certificato radice per l'autorità di certificazione che rilascerà il certificato che si sta configurando in questo profilo certificato.  

  > [!IMPORTANT]  
  > Se si specifica un certificato CA radice non distribuito all'utente o al dispositivo, Configuration Manager non avvierà la richiesta di certificato in fase di configurazione in questo profilo certificato.  

## <a name="supported-platforms"></a>Piattaforme supportate  

Nella pagina **Piattaforme supportate** della Creazione guidata profilo certificato, selezionare le versioni del sistema operativo in cui si vuole installare il profilo certificato. Scegliere **Seleziona tutto** per installare il profilo certificato in tutti i sistemi operativi disponibili.

## <a name="next-steps"></a>Passaggi successivi

Il nuovo profilo certificato viene visualizzato nel nodo **profili certificato** nell'area di lavoro **asset e conformità** . È possibile eseguire la distribuzione a utenti o dispositivi. Per altre informazioni vedere [Come distribuire i profili](/configmgr/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).
