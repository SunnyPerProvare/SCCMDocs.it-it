---
title: 'Come creare profili VPN '
titleSuffix: Configuration Manager
description: Di seguito viene illustrato come si creano i profili VPN in System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2969a0df23f7e8b74708a4aee03c3ea7f689a99
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Come creare profili VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I tipi di connessione disponibili per le diverse piattaforme dei dispositivi sono descritti in [Profili VPN in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per informazioni sulla distribuzione delle app, vedere [Distribuire le applicazioni con System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Creare un profilo VPN   

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profili VPN**.  

2.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea profilo VPN**.  


3.  Completare la pagina **Generale**. Tenere presente quanto segue:  

    - Selezionare il valore appropriato in **Piattaforma**.

       - Se si seleziona la piattaforma Windows 8.1, è possibile selezionare **Importa un profilo VPN esistente da un file** per importare informazioni su un profilo VPN esportate in un file XML.

    - Nel nome del profilo VPN non usare i caratteri \\/:*?&lt;>&#124;, né lo spazio. Questi caratteri non sono supportati dal profilo VPN di Windows Server.  


4.  Nella pagina **Connessione** specificare:  

    -   **Tipo di connessione**: scegliere il tipo di connessione VPN. È possibile scegliere tra i tipi di connessione nella tabella seguente.  

    -   **Elenco server**: aggiungere un nuovo server da usare per la connessione VPN. In base al tipo di connessione è possibile aggiungere uno o più server VPN e specificare il server predefinito.  

        > [!NOTE]  
        >  I dispositivi che eseguono iOS non supportano l'utilizzo di più server VPN. Se si configurano più server VPN e si distribuisce il profilo VPN a un dispositivo iOS, verrà usato solo il server predefinito.  

     Questa tabella specifica le opzioni per i tipi di connessione. Per altre informazioni, vedere la documentazione del server VPN.

| &nbsp;&nbsp;Opzione&nbsp;&nbsp; | Altre informazioni | &nbsp;&nbsp;Tipo&nbsp;di connessione&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Area di autenticazione**     |L'area di autenticazione da usare. Un'area di autenticazione è un raggruppamento di risorse di autenticazione usate dal tipo di connessione Pulse Secure.|Pulse Secure|    
|**Ruolo**        |Il ruolo utente che ha accesso a questa connessione. |Pulse Secure|  
|**Gruppo o dominio di accesso** |Il nome del gruppo di accesso o del dominio a cui connettersi.|Dell SonicWALL Mobile Connect|  
|**Impronta digitale**  |Una stringa, ad esempio "Codice impronta digitale Contoso", che verrà usata per verificare l'attendibilità del server VPN.<br /><br /> Un'impronta digitale può essere:<br /><br /> - Inviata al client in modo da informarlo che può considerare attendibile un server che presenta la stessa impronta digitale durante la connessione.<br /><br /> - Se il dispositivo non ha ancora l'impronta digitale, richiederà all'utente di considerare attendibile il server VPN usato per la connessione durante la visualizzazione dell'impronta digitale (l'utente verifica manualmente l'impronta digitale e sceglie **Attendibilità** per connettersi).|VPN mobile Check Point|  
|**Invia tutto il traffico di rete tramite la connessione VPN** |Se questa opzione non è selezionata, è possibile specificare route aggiuntive per la connessione (per i tipi di connessione **Microsoft SSL (SSTP)**, **Microsoft Automatico**, **IKEv2**, **PPTP** e **L2TP** ), caratteristica nota come split o tunneling VPN.<br /><br /> Solo le connessioni alla rete aziendale vengono inviate tramite un tunnel VPN. Il tunneling VPN non viene usato quando si esegue la connessione alle risorse su Internet. |All|  
|**Suffisso DNS specifico della connessione** |Il suffisso DNS (Domain Name System) specifico per la connessione.|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**  |La connessione VPN non verrà usata quando il dispositivo è connesso alla rete Wi-Fi aziendale.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi domestica**  |La connessione VPN non verrà usata quando il dispositivo è connesso a una rete Wi-Fi domestica.|All|  
|**VPN per app (iOS 7 e versioni successive, Mac OS X 10.9 e versioni successive)** |Associare questa connessione VPN a un'app iOS in modo da aprire la connessione quando si esegue l'app. È possibile associare il profilo VPN a un'app quando viene distribuito.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
|**XML personalizzato (opzionale)** |Specificare i comandi XML personalizzati che consentono di configurare la connessione VPN.<br /><br /> Esempi:<br /><br /> Per **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> Per **VPN Checkpoint Mobile**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Per **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> Per **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Per altre informazioni su come scrivere comandi XML personalizzati, fare riferimento alla documentazione della VPN fornita dai singoli produttori.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

> [!NOTE]  
>  Per informazioni specifiche per la creazione di profili VPN per i dispositivi mobili, vedere [Creare profili VPN](../../mdm/deploy-use/create-vpn-profiles.md).  

Completare la procedura guidata. Il nuovo profilo VPN viene visualizzato nel nodo **Profili VPN** dell'area di lavoro **Asset e conformità** .

### <a name="next-steps"></a>Passaggi successivi

- Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per informazioni sulla distribuzione delle app, vedere [Distribuire le applicazioni con System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Distribuire il profilo VPN seguendo la procedura descritta in [Come distribuire profili VPN in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  