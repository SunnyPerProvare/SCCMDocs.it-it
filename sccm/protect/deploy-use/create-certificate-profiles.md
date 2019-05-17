---
title: Come creare profili certificato SCEP
titleSuffix: Configuration Manager
description: Informazioni su come usare i profili certificato per eseguire il provisioning dei certificati necessari ai dispositivi gestiti in System Center Configuration Manager.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 600b786bbb2f718868c5d08c722621682582f4e1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500654"
---
# <a name="create-certificate-profiles"></a>Creare i profili certificato

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i profili certificato in Configuration Manager (SCCM) per effettuare il provisioning dei certificati necessari ai dispositivi gestiti per accedere alle risorse aziendali. Prima di creare i profili certificato, configurare l'infrastruttura di certificazione come descritto in [Set up certificate infrastructure for System Center Configuration Manager](certificate-infrastructure.md) (Configurare l'infrastruttura di certificazione per System Center Configuration Manager).  

Questo argomento descrive come creare profili certificato SCEP e radice attendibile. Se si vuole creare profili certificato PFX, vedere [Creare profili certificato PFX](../../protect/deploy-use/create-pfx-certificate-profiles.md) .

Per creare un profilo certificato:

1.  Avviare la Creazione guidata profilo certificato.
1.  Fornire informazioni generali sul certificato.
1.  Configurare un certificato dell'autorità di certificazione (CA) attendibile.  
1.  Configurare le informazioni sul certificato SCEP (solo per i certificati SCEP).  
1.  Specificare le piattaforme supportate per il profilo certificato.


## <a name="start-the-create-certificate-profile-wizard"></a>Avviare la Creazione guidata profilo certificato  

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili certificati**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo certificato**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Fornire informazioni generali sul profilo certificato  

Nella pagina **Generale** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

-   **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

-   **Descrizione**: digitare una descrizione che offra una panoramica del profilo certificato e altre informazioni rilevanti per facilitarne l'identificazione nella console di System Center Configuration Manager. È possibile usare un massimo di 256 caratteri.  

-   **Specificare il tipo di profilo del certificato che si desidera creare**: scegliere uno tipi di profilo certificato seguenti:  

-   **Certificato CA attendibile**: selezionare questo tipo di profilo certificato se si vuole distribuire un certificato CA radice attendibile o un certificato CA intermedio per formare una catena di certificati attendibili quando l'utente o il dispositivo deve autenticare un altro dispositivo. Ad esempio, il dispositivo può essere un server RADIUS (Remote Authentication Dial-In User Service) o un server di rete privata virtuale (VPN). È anche necessario configurare un profilo certificato CA attendibile prima di creare un profilo certificato SCEP. In questo caso, il certificato CA attendibile deve essere un certificato radice trusted per la CA che rilascerà il certificato per l'utente o il dispositivo.  

-   **Impostazioni di Simple Certificate Enrollment Protocol (SCEP)**: selezionare questo tipo di profilo certificato se si desidera richiedere un certificato per un utente o un dispositivo utilizzando il Simple Certificate Enrollment Protocol e il servizio del ruolo del servizio Registrazione dispositivi di rete.

-   **Scambio informazioni personali - Impostazioni PKCS #12 (PFX) - Importa**: selezionare questa opzione per importare un certificato PFX. Per altre informazioni sulla creazione del certificato PFX, vedere [Importare profili certificato PFX](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md).

-   **Personal Information Exchange - Impostazioni PKCS #12 (PFX) - Crea**: selezionare questa opzione per elaborare i certificati PFX usando un'autorità di certificazione. Per altre informazioni sulla creazione del certificato PFX, vedere [Creare profili certificato PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md).


## <a name="configure-a-trusted-ca-certificate"></a>Configurare un certificato CA attendibile  

> [!IMPORTANT]  
>  Prima di creare un profilo certificato SCEP è necessario configurare almeno un profilo certificato CA attendibile.    
>  
>  Se si modifica uno di questi valori dopo aver distribuito il certificato, viene richiesto un nuovo certificato:
>  -  Provider di archiviazione chiavi
>  -  Nome modello di certificato
>  -  Tipo di certificato
>  -  Formato del nome soggetto
>  -  Nome alternativo soggetto
>  -  Periodo di validità del certificato
>  -  Utilizzo chiavi
>  -  Dimensione chiavi
>  -  Utilizzo chiavi avanzato
>  -  Certificato CA radice

1. Nella pagina **Certificato CA attendibile** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

   -   **File certificato**: fare clic su **Importa** e selezionare il percorso al file del certificato che si desidera utilizzare.  

   -   **Archivio di destinazione**: per i dispositivi che dispongono di più archivi di certificati, selezionare dove archiviare il certificato. Per i dispositivi con un solo archivio, questa impostazione viene ignorata.  

2. Usare il valore **Identificazione personale certificato** per accertarsi di aver importato il certificato corretto.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Configurare le informazioni sul certificato SCEP (solo per i certificati SCEP)  

1. Nella pagina **Server SCEP** della Creazione guidata profilo certificato specificare gli URL per i server NDES che emetteranno i certificati tramite SCEP. È possibile scegliere di assegnare automaticamente un URL NDES in base alla configurazione del server del sistema del sito del punto di registrazione certificati o aggiungere manualmente gli URL.  

2. Completare la pagina **Registrazione SCEP** della Creazione guidata profilo certificato.

   -  **Tentativi**: specificare il numero di tentativi di richiesta certificato inviati automaticamente dal dispositivo al server che esegue il servizio Registrazione dispositivi di rete. Questa impostazione supporta lo scenario in cui un CA manager deve approvare una richiesta di certificato prima di essere accettata. Questa impostazione viene in genere usata per gli ambienti ad alta protezione o se si dispone di una CA emittente autonoma invece di una CA globale (enterprise). È anche possibile usare questa impostazione a scopo di test, in modo da poter ispezionare le opzioni di richiesta certificato prima che la richiesta certificato venga elaborata dalla CA emittente. Usare questa impostazione con l'opzione **Intervallo tra tentativi (minuti)** .  

   -   **Intervallo tra tentativi (minuti)**: specificare l'intervallo in minuti tra ogni tentativo di registrazione quando si utilizza l'approvazione del responsabile CA prima che la richiesta certificato venga elaborata dalla CA emittente. Se si usa l'approvazione responsabile a scopo di test, potrebbe essere necessario specificare un valore basso in modo da non dover attendere troppo tempo prima di un nuovo tentativo di richiesta certificato dopo che questa è stata approvata. Tuttavia, se si usa l'approvazione responsabile in una rete di produzione, potrebbe essere necessario specificare un valore più elevato per fornire all'amministratore della CA il tempo sufficiente per verificare e approvare o negare le approvazioni in sospeso.  

   -   **Soglia rinnovo (%)**: specificare la percentuale di durata residua del certificato prima che il dispositivo richieda il rinnovo del certificato.  

   -   **Provider di archiviazione chiavi (KSP)**: specificare dove verrà archiviata la chiave per il certificato. Scegliere tra uno dei seguenti valori:  

   -   **Installa in TPM (Trusted Platform Module) se presente**: installa la chiave nel modulo TPM. Se il TPM non è presente, la chiave verrà installata nel provider di archiviazione per la chiave software.  

   -   **Installa in TPM (Trusted Platform Module) in caso di errore**: installa la chiave nel modulo TPM. Se il modulo TPM non è presente, l'installazione non riuscirà.  

   -   **Install to Windows Hello for Business otherwise fail** (Installa in Windows Hello per le aziende oppure genera errore): questa opzione è disponibile per i dispositivi Windows 10 Desktop e Mobile. Registra la chiave in **Windows Hello per aziende**, come descritto in [Impostazioni di Windows Hello per le aziende in System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md). Questa opzione consente inoltre di **richiedere l'autenticazione a più fattori** durante la registrazione dei dispositivi prima di rilasciare certificati per i dispositivi. Per altre informazioni, vedere [Proteggere i dispositivi Windows con l'autenticazione a più fattori](https://technet.microsoft.com/library/dn889751.aspx) .

   > [!NOTE]  
   > 
   > Quando un utente crea un PIN di Windows Hello per le aziende, Windows invia una notifica per la quale Configuration Manager è in ascolto. Ciò consente a Configuration Manager di venire rapidamente a conoscenza di quali utenti hanno creato un PIN di Windows Hello. Configuration Manager può quindi anche rilasciare nuovi certificati a tali utenti se Windows Hello viene usato come provider di archiviazione chiavi in un profilo di certificato.  

   -   **Installa nel provider di archiviazione chiavi software**: installa la chiave nel provider di archiviazione per la chiave software.  

   -   **Dispositivi per registrazione certificato**: se il profilo certificato viene distribuito in una raccolta utenti, scegliere se consentire la registrazione certificato solo sul dispositivo primario dell'utente o su tutti i dispositivi in cui l'utente esegue l'accesso. Se il profilo certificato viene distribuito in una raccolta dispositivi, scegliere se consentire la registrazione certificato solo per l'utente primario del dispositivo o per tutti gli utenti che accedono al dispositivo.  

3. Nella pagina **Proprietà certificato** della Creazione guidata profilo certificato specificare le informazioni seguenti:  

   -   **Nome modello certificato**: fare clic su **Sfoglia** per selezionare il nome di un modello del certificato configurato per essere utilizzato dal servizio Registrazione dispositivi di rete e che è stato aggiunto a una CA emittente. Per selezionare modelli di certificato, l'account utente usato per eseguire la console di System Center Configuration Manager deve disporre di autorizzazioni in lettura al modello di certificato. In alternativa, se non è possibile usare **Sfoglia**, digitare il nome del modello certificato.  

   > [!IMPORTANT]
   >   
   >  Se il nome del modello di certificato contiene caratteri non ASCII (ad esempio, i caratteri dell'alfabeto cinese), il certificato non verrà distribuito. Per garantire la distribuzione del certificato, è necessario creare in primo luogo una copia del modello del certificato nella CA e rinominare la copia usando caratteri ASCII.  

   Tenere presente quanto segue, a seconda del fatto che si selezioni il percorso al modello di certificato o si digiti il nome del certificato:  

   -   Se si seleziona il percorso per scegliere il nome del modello di certificato, alcuni campi nella pagina vengono popolati automaticamente dal modello del certificato. In alcuni casi, non è possibile modificare questi valori, a meno che non si scelga un modello di certificato diverso.  

   -   Se si digita il nome del modello del certificato, assicurarsi che il nome corrisponda esattamente a uno dei modelli del certificato elencati nel registro di sistema del servizio che esegue il servizio Registrazione dispositivi di rete. Accertarsi di specificare il nome del modello del certificato e non il nome visualizzato del modello del certificato.  

   Per trovare i nomi dei modelli di certificato, individuare la seguente chiave: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP. I modelli di certificato verranno visualizzati come i valori per **EncryptionTemplate**, **GeneralPurposeTemplate**e **SignatureTemplate**. Per impostazione predefinita, il valore per i tre modelli di certificato è **IPSECIntermediateOffline**, che è associato al nome visualizzato del modello **IPSec (Offline request)**.  

   > [!WARNING]  
   > 
   >  Poiché System Center Configuration Manager non è in grado di verificare i contenuti del modello di certificato quando si digita il nome del modello del certificato anziché eseguire una ricerca, potrebbe essere possibile selezionare opzioni che non sono supportate dal modello di certificato e che causano la mancata esecuzione della richiesta certificato. In questo caso, verrà visualizzato un messaggio di errore per w3wp.exe nel file CPR.log per segnalare che il nome modello in CSR e la richiesta di verifica non corrispondono.  
   >   
   >  Quando si digita il nome del modello di certificato specificato per il valore **GeneralPurposeTemplate** , è necessario selezionare le opzioni **Crittografia chiave** e **Firma digitale** per il profilo certificato. Tuttavia, se si desidera abilitare solo l'opzione **Crittografia chiave** in questo profilo certificato, specificare il nome modello del certificato per la chiave **EncryptionTemplate** . Analogamente, se si desidera abilitare solo l'opzione **Forma digitale** in questo profilo certificato, specificare il nome modello del certificato per la chiave **SignatureTemplate** .  

   -   **Tipo di certificato**: selezionare se il certificato verrà distribuito a un dispositivo o un utente.  
   -   **Formato nome soggetto**: dall'elenco, selezionare in che modo System Center Configuration Manager crei automaticamente il nome soggetto nella richiesta certificato. Se il certificato è per un utente, è anche possibile includere l'indirizzo di posta elettronica dell'utente nel nome del soggetto. 
    
   > [!NOTE]  
   > 
   > La selezione di **Codice IMEI**  o di **Numero di serie** consente di distinguere i diversi dispositivi appartenenti allo stesso utente. Tali dispositivi, ad esempio, potrebbero condividere il nome comune, ma non il codice IMEI o il numero di serie. Se il dispositivo non ha un codice IMEI o un numero di serie, il certificato viene emesso con il nome comune.

   -   **Nome alternativo oggetto**: specificare in che modo System Center Configuration Manager crea automaticamente i valori per il nome alternativo oggetto (SAN) nella richiesta certificato. Ad esempio, se si seleziona un tipo di certificato utente, è possibile includere il nome dell'entità utente (UPN) nel nome alternativo oggetto.  Se il certificato client verrà usato per eseguire l'autenticazione in un server dei criteri di rete, è necessario impostare il nome alternativo oggetto sul nome dell'entità utente.  

   > [!NOTE]  
   >  - I dispositivi iOS supportano formati del nome soggetto e nomi alternativi oggetto limitati nei certificati SCEP. Se si specifica un formato non supportato, i certificati non verranno registrati su dispositivi iOS. Quando si configura un profilo certificato SCEP da distribuire nei dispositivi iOS, usare il **Nome comune** per il **Formato del nome soggetto**e **Nome DNS**, **Indirizzo di posta elettronica** o **UPN** per il **Nome alternativo oggetto**.  

   -   **Periodo di validità del certificato**: se il comando certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE è stato eseguito nella CA emittente, che consente un periodo di validità personalizzato, è possibile specificare la quantità di tempo rimanente prima della scadenza del certificato. Per altre informazioni sui profili certificato, vedere [Certificate infrastructure in System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md) (Infrastruttura di certificazione in System Center Configuration Manager).  

   È possibile specificare un valore inferiore, ma non superiore rispetto al periodo di validità nel modello di certificato indicato. Ad esempio, se il periodo di validità del certificato nel modello di certificato è di due anni, è possibile specificare un valore di un anno ma non un valore di cinque anni. Inoltre, il valore deve essere inferiore rispetto al periodo di validità rimanente del certificato della CA emittente.  

   -   **Utilizzo chiave**: specificare le opzioni di utilizzo della chiave per il certificato. È possibile scegliere una delle opzioni seguenti:  

       -   **Crittografia chiave**: consentire lo scambio di chiavi solo quando la chiave viene crittografata.  

       -   **Firma digitale**: consentire lo scambio di chiavi soltanto se una firma digitale consente di proteggere la chiave.  

   Se è stato selezionato un modello di certificato usando **Sfoglia**, potrebbe non essere possibile modificare queste impostazioni senza selezionare un modello di certificato diverso.  

   Il modello di certificato selezionato deve essere configurato con una o entrambe le due opzioni di utilizzo della chiave sopra riportate. In caso contrario, verrà visualizzato il messaggio **Utilizzo chiave in CSR e richiesta di verifica non corrispondono** nel file di registro del punto di registrazione certificati, **Reg.cert**.  


- **Dimensione chiave (bits)**: selezionare la dimensione della chiave in bit.  

- **Utilizzo chiave esteso**: fare clic su **Seleziona** per aggiungere valori per lo scopo designato del certificato. Nella maggior parte dei casi il certificato richiederà l' **Autenticazione Client** in modo che l'utente o il dispositivo possa eseguire l'autenticazione a un server. È comunque possibile aggiungere altri utilizzi di chiavi secondo necessità.  


- **Algoritmo hash**: selezionare uno dei tipi di algoritmo hash disponibili da utilizzare con il certificato. Selezionare il livello di sicurezza più avanzato supportato dai dispositivi che verranno connessi.  

  > [!NOTE]  
  > 
  >  **SHA-2** supporta SHA-256, SHA-384 e SHA-512. **SHA-1** supporta solo SHA-3.  

- **Certificato CA radice**: fare clic su **Seleziona** per scegliere un profilo del certificato CA radice precedentemente configurato e distribuito all'utente o al dispositivo. Questo certificato CA deve essere il certificato radice per l'autorità di certificazione che rilascerà il certificato che si sta configurando in questo profilo certificato.  

  > [!IMPORTANT]  
  >  Se si specifica un certificato CA radice non distribuito all'utente o al dispositivo, System Center Configuration Manager non avvierà la richiesta certificato in fase di configurazione in questo profilo certificato.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Specificare le piattaforme supportate per il profilo certificato  

1. Nella pagina **Piattaforme supportate** della Creazione guidata profilo certificato, selezionare i sistemi operativi in cui si desidera installare il profilo certificato. In alternativa, fare clic su **Seleziona tutto** per installare il profilo certificato su tutti i sistemi operativi disponibili.
2. Rivedere le impostazioni nella pagina **Riepilogo** della procedura guidata e scegliere **Fine**. 
 
 
Il nuovo profilo certificato viene visualizzato nel nodo **Profili certificato** nell'area di lavoro **Asset e conformità** e può essere distribuito agli utenti o ai dispositivi come descritto in [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md)(Come distribuire profili in System Center Configuration Manager).  
