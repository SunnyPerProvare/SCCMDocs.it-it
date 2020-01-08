---
title: profili VPN
titleSuffix: Configuration Manager
description: Informazioni sui profili VPN nei dispositivi mobili in Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee8e7b3dd4130712eebb82caa4e6519b78991a3d
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520984"
---
# <a name="vpn-profiles-on-mobile-devices-in-configuration-manager"></a>Profili VPN nei dispositivi mobili in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare profili VPN in Configuration Manager per distribuire impostazioni VPN agli utenti dei dispositivi mobili nell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse sulla rete aziendale.  

Ad esempio, si supponga di voler configurare tutti i dispositivi iOS in modo che si connettano a una condivisione file nella rete aziendale. Creare un profilo VPN con le impostazioni di connessione necessarie. In seguito distribuire il profilo a tutti gli utenti con dispositivi iOS. Gli utenti visualizzano la connessione VPN nell'elenco delle reti disponibili e possono connettersi a tale rete con la massima facilità.  

Quando si crea un profilo VPN, è possibile includere una vasta gamma di impostazioni di protezione. È ad esempio possibile specificare certificati per la convalida del server e l'autenticazione del client impostati usando i profili di certificato di Configuration Manager. Per altre informazioni, vedere i [profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profili VPN usando Configuration Manager insieme a Intune

Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e Windows 8.1, tali dispositivi devono essere registrati in Microsoft Intune. Anche i dispositivi su altre piattaforme possono essere registrati in Intune. Per informazioni su come eseguire la registrazione, vedere [Registrare dispositivi mobili con Microsoft Intune](/intune/device-enrollment). 

La tabella seguente mostra il tipo di connessione supportato per ogni piattaforma del dispositivo:  

|Tipo di connessione|iOS e MacOS X|Android|Windows 8,1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
|---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
|Cisco AnyConnect|Sì<sup>1</sup>|sì|No|No|No|No|No|
|Cisco (IPSec)|Solo iOS|No|No|No|No|No|No|  
|Pulse Secure|sì|sì|sì|No|sì|sì|sì|  
|F5 Edge Client|sì|sì|sì|No|sì|sì|sì|  
|Dell SonicWALL Mobile Connect|sì|sì|sì|No|sì|sì|sì|  
|VPN mobile Check Point|sì|sì|sì|No|sì|sì|sì|  
|Microsoft SSL (SSTP)|No|No|sì|sì|sì|No|No|  
|Microsoft Automatico|No|No|sì|sì|sì|No|sì|  
|IKEv2|Sì (criteri personalizzati iOS 9 e versioni successive)|No|sì|sì|sì|sì|sì|  
|PPTP|sì|No|sì|sì|sì|No|sì|  
|L2TP|sì|No|sì|sì|sì|No|Sì (URI OMA)|  

<sup>1</sup> a partire dalla versione 1802, l'utilizzo del tipo di connessione Cisco AnyConnect varia.<!--1357393-->  
- Usare l'opzione **Cisco Legacy AnyConnect** per i profili VPN nelle versioni seguenti:
  - iOS con Cisco AnyConnect versione 4.0.5 o versioni precedenti
  - macOS con tutte le versioni di Cisco AnyConnect
- Usare l'opzione **Cisco AnyConnect** per i profili VPN nelle versioni seguenti:
  - iOS con Cisco AnyConnect versione 4.0.7 o versione successiva

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x e versioni successive per iOS è una funzionalità introdotta per la prima volta nella versione 1802 come [versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dall'[aggiornamento 4163547](https://support.microsoft.com/help/4163547) per la versione 1802, questa funzionalità non è più in versione non definitiva.  

  
> [!Note]  
> F5 Access 3.0 o versione successiva per iOS non è supportato per i profili VPN in una soluzione MDM ibrida. Questo prodotto è detto anche F5 Access 2018. Se è necessario creare profili VPN per questo client VPN, usare una versione autonoma di Intune. Le versioni future di iOS, inclusa la versione 12, non supporteranno F5 Access versione 2.1 o versioni precedenti. Per altre informazioni, vedere il [blog del team di supporto di Microsoft Intune](https://aka.ms/iOS12_and_VPN).


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funzionalità VPN di Windows 10 disponibili quando si usa Configuration Manager con Intune  

Le opzioni seguenti sono disponibili per tutti i tipi di connessione in Windows 10:

- **Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**: la connessione VPN non viene usata quando il dispositivo è connesso alla rete Wi-Fi aziendale. Immettere il nome di rete attendibile usato per determinare se il dispositivo è connesso alla rete aziendale.  

- **Network traffic rules** (Regole del traffico di rete): impostare i protocolli, la porta locale, la porta remota e gli intervalli di indirizzi per l'abilitazione della connessione VPN.  

  > [!Note]  
  > Se non si crea una regola del traffico di rete, verranno abilitati tutti i protocolli, le porte e gli intervalli di indirizzi. Dopo la creazione di una regola, vengono usati dalla connessione VPN solo i protocolli, le porte e gli intervalli di indirizzi specificati in tale regola o nelle regole aggiuntive.  

- **Route**: route che usano la connessione VPN. La creazione di più di 60 route può causare errori dei criteri.  

- **Server DNS**: server DNS usati dalla connessione VPN una volta stabilita la connessione.  

- **Apps that automatically connect to the VPN** (App che si connettono automaticamente alla VPN): è possibile aggiungere app o importare elenchi di app che usano automaticamente la connessione VPN. Il tipo di app determina l'identificatore dell'app. Per un'app desktop, specificare il percorso file dell'app. Per un'app universale, specificare il nome della famiglia di pacchetti (PFN). Per sapere come individuare il nome PFN per un'app, vedere la sezione relativa al [reperimento di un nome di famiglia di pacchetti per la VPN per app](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md).  

  > [!IMPORTANT]  
  > Proteggere tutti gli elenchi di app associate che vengono compilati per l'uso nella configurazione della VPN per app. Se l'elenco viene modificato da un utente non autorizzato e viene importato nell'elenco di app della VPN per app, si autorizza potenzialmente l'accesso alla VPN da parte di applicazioni che non devono potervi accedere. Un modo per proteggere gli elenchi di app consiste nell'usare un elenco di controllo di accesso (ACL).  



## <a name="create-vpn-profiles"></a>Creare profili VPN


1. Nella console di Configuration Manager nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, espandere **Accesso risorse aziendali** e selezionare **Profilo VPN**. 

2. Fare clic su **Crea profilo VPN** nella barra multifunzione.  

3. Nella pagina **Generale** specificare un **Nome** e selezionare il **Tipo di profilo VPN**.   
    > [!NOTE]  
    > Il nome di un profilo VPN che usa le funzionalità VPN di Windows 10 non può essere in formato Unicode né contenere caratteri speciali.


4. Se la pagina **Piattaforme supportate** è disponibile, selezionare le versioni del sistema operativo per il tipo di profilo VPN specificato in precedenza. Scegliere **Seleziona tutto** per installare il profilo VPN in tutte le versioni dei sistemi operativi disponibili.  

5. Configurare la connessione VPN nella pagina **Connessione**. Per altre informazioni su queste opzioni, vedere il passaggio della pagina Connessione in [Creare un profilo VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6. Nella pagina **Metodo di autenticazione** specificare le informazioni seguenti:  

   - **Metodo di autenticazione**: selezionare il metodo di autenticazione usato dalla connessione VPN. I metodi disponibili variano a seconda del tipo di connessione come illustrato in questa tabella.  

     |Metodo di autenticazione|Tipi di &nbsp;connessione&nbsp; supportati|  
     |---------------------------|--------------------------------|  
     |**Certificati**<br /><br /> **Note:**<ul><li>Se il certificato client esegue l'autenticazione in un server RADIUS, ad esempio un server dei criteri di rete, impostare il nome alternativo del soggetto nel certificato sul nome dell'entità utente.</li><li>Per le distribuzioni Android, selezionare l'identificatore EKU e il valore hash di identificazione personale dell'autorità di certificazione. In caso contrario, gli utenti devono selezionare il certificato appropriato manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN mobile Check Point</li></ul>|  
     |**Nome utente e password**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN mobile Check Point</li></ul>|  
     |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
     |**Microsoft PEAP (Protected EAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Password protetta Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Smart card o altro certificato**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**RSA SecurID** (solo iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Usa certificati computer**|<ul><li>IKEv2</li></ul>|  

      A seconda delle opzioni selezionate, potrebbe essere necessario specificare altre informazioni, ad esempio:  

     - **Memorizza le credenziali utente a ogni accesso**: le credenziali utente vengono memorizzate in modo che gli utenti non debbano immetterle ogni volta che si connettono.  

     - **Selezionare un certificato client per l'autenticazione client**: selezionare il [certificato SCEP](create-pfx-certificate-profiles.md) creato in precedenza che viene usato per autenticare la connessione VPN.   

       > [!NOTE]  
       > Per i dispositivi iOS, il profilo SCEP selezionato viene incorporato nel profilo VPN. Per altre piattaforme, viene aggiunta una regola di applicabilità per garantire che il profilo VPN non venga installato se il certificato non è presente o non è conforme.  
       >   
       > Se il certificato SCEP specificato non è conforme o non è stato distribuito, il profilo VPN non viene installato nel dispositivo.
       >  
       > I dispositivi che eseguono iOS supportano solo RSA SecurID e MSCHAP v2 per il metodo di autenticazione quando il tipo di connessione è PPTP. Per evitare la segnalazione di errori, distribuire un profilo VPN PPTP distinto nei dispositivi che eseguono iOS.   

     - **Accesso condizionale**  
       - Scegliere **Abilita l'accesso condizionale per questa connessione VPN** per garantire che prima della connessione i dispositivi che si connettono alla rete VPN siano stati sottoposti a test di conformità all'accesso condizionale. Per altre informazioni, vedere [Criteri di conformità del dispositivo in System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  

       - Scegliere **Abilita l'accesso Single Sign-On (SSO) con il certificato alternativo** per scegliere un certificato diverso dal certificato di autenticazione VPN per la conformità del dispositivo. Se si sceglie questa opzione, specificare **EKU** (elenco delimitato da virgole) e **Hash dell'emittente** per ottenere il certificato corretto che il client VPN deve individuare.  

       - Per **Windows Information Protection**, specificare l'identità aziendale gestita dall'organizzazione, che corrisponde in genere al dominio primario dell'organizzazione, ad esempio *contoso.com*. È possibile specificare più domini di proprietà dell'organizzazione separandoli con il carattere "|". Ad esempio, *contoso.com|newcontoso.com*. Per altre informazioni, vedere [creare e distribuire un criterio di protezione delle app di Windows Information Protection con Intune](/intune/windows-information-protection-policy-create).   

       ![Pagina Metodo di autenticazione, creazione guidata profilo VPN](media/vpn-conditional-access.png)

       Quando la versione del client Windows lo supporta, è disponibile l'opzione **Configura** per il metodo di autenticazione. Questa opzione consente di aprire la finestra di dialogo delle proprietà di Windows per configurare il metodo di autenticazione. Se l'opzione **Configura** è disabilitata, usare modi diversi per configurare le proprietà del metodo di autenticazione.  

7. Nella pagina **Impostazioni proxy** della **Creazione guidata profilo VPN** selezionare la casella **Configura impostazioni proxy per questo profilo VPN** se la connessione VPN in uso utilizza un server proxy. Quindi, specificare le informazioni relative al server proxy. Per altre informazioni, vedere la documentazione di Windows Server.  

   > [!NOTE]  
   > Nei computer Windows 8.1 il profilo VPN non visualizzerà le informazioni sul proxy finché l'utente non si connette alla rete VPN usando tale computer.  


8. Configurare altre impostazioni DNS, se necessario.  

9. Completa la procedura guidata. Il nuovo profilo VPN viene visualizzato nel nodo **Profilo VPN** dell'area di lavoro **Asset e conformità**.  



## <a name="next-steps"></a>Passaggi successivi  
Per altre informazioni sulla distribuzione dei profili VPN, vedere [Distribuire profili Wi-Fi, VPN, di posta elettronica e di certificato](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Usare gli articoli seguenti per pianificare, configurare, usare e gestire i profili VPN:  

- [Prerequisiti per i profili VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

- [Sicurezza e privacy per i profili VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
