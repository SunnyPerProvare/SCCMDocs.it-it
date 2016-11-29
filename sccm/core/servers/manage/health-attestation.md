---
title: "Attestazione dell'integrità | System Center Configuration Manager"
description: "Informazioni sulla funzionalità di Attestazione dell'integrità del dispositivo visibile nella console di Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7f3c95983f28d58bd0503570df9dc3b229059e82


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Attestazione dell'integrità per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con System Center Configuration Manager (Current Branch) versione 1602, gli amministratori possono visualizzare lo stato di [Attestazione dell'integrità del dispositivo di Windows 10 ](https://technet.microsoft.com/library/mt592023.aspx) nella console di Configuration Manager.  Questa funzionalità è disponibile per i PC e le risorse locali gestite da Configuration Manager e i dispositivi mobili gestiti con Microsoft Intune. Gli amministratori possono specificare se la creazione di report avviene tramite cloud o infrastruttura locale. In questo modo i PC client senza accesso a Internet possono abilitare e monitorare i dispositivi usando l'attestazione dell'integrità. L'attestazione dell'integrità dei dispositivi consente all'amministratore di assicurare che nei computer client siano abilitate le seguenti configurazioni attendibili di BIOS, TPM e software di avvio:  

-   Antimalware ad esecuzione anticipata: l'antimalware ad esecuzione anticipata (ELAM) protegge il computer all'avvio e prima dell'inizializzazione dei driver di terze parti. [Come attivare la funzionalità ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  

-   BitLocker: Crittografia unità BitLocker di Windows è un software che consente di crittografare tutti i dati archiviati nel volume del sistema operativo Windows.  [Come attivare BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  

-   Avvio protetto: Avvio protetto è uno standard di sicurezza sviluppato dai membri del settore IT per garantire che i computer vengano avviati usando solo software considerato attendibile dal relativo produttore. [Altre informazioni su Avvio protetto](https://technet.microsoft.com/library/hh824987.aspx)  

-   Integrità del codice: Integrità del codice è una funzionalità che migliora la sicurezza del sistema operativo convalidando l'integrità di un driver o di un file di sistema ogni volta che viene caricato nella memoria. [Altre informazioni su Integrità del codice](https://technet.microsoft.com/library/dd348642.aspx)  



##  <a name="device-health-attestation"></a>Attestazione dell'integrità dei dispositivi  
 L'attestazione dell'integrità del dispositivo di Configuration Manager visualizza quanto segue:  

-   **Stato dell'attestazione dell'integrità** : mostra la quota di dispositivi nello stato conforme, non conforme, errore e sconosciuto  

-   **Dispositivi che generano report di attestazione dell'integrità** : mostra la percentuale dei dispositivi che segnalano lo stato di attestazione dell'integrità  

-   **Dispositivi non conformi per tipo di client** : mostra la quota di dispositivi mobili e computer che non sono conformi  

-   **Impostazioni principali per l'attestazione dell'integrità mancante** : mostra il numero di dispositivi in cui manca l'impostazione per l'attestazione dell'integrità, elencati per impostazione  

 **Requisiti:**  

-   Dispositivi client che eseguono Win10  

-   Windows Server 2016 Technical Preview 5 con [Attestazione dell'integrità del dispositivo abilitata](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)

-    TPM 2 abilitato  

-   Sbloccare la comunicazione tra l'agente client di Configuration Manager e il servizio di Attestazione dell'integrità has.spserv.microsoft.com (port 443)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Come abilitare la comunicazione del servizio di Attestazione dell'integrità nei computer client di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Panoramica** > **Impostazioni client**.  Selezionare la scheda delle impostazioni di **Agente computer** .  

2.  Nella finestra di dialogo **Impostazioni predefinite** selezionare **Agente computer** e quindi scorrere fino a **Abilita le comunicazioni con il servizio di attestazione dell'integrità**  

3.  Impostare l'opzione **Abilita le comunicazioni con il servizio di attestazione dell'integrità** su **Sì**e quindi fare clic su **OK**.  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Come abilitare la comunicazione del servizio di attestazione dell'integrità locale nei computer client di Configuration Manager


1. Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Impostazioni client**e quindi impostare **Usare il servizio di attestazione dell'integrità locale** su **Sì**.


2. Specificare l' **URL del servizio di attestazione dell'integrità locale**e quindi fare clic su **OK**.

## <a name="how-to-view-health-attestation"></a>Come visualizzare Attestazione dell'integrità  


1.  Per visualizzare l'attestazione dell'integrità del dispositivo, nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** , fare clic sul nodo **Sicurezza** e quindi su **Attestazione dell'integrità**.  

2.  Viene visualizzato Attestazione dell'integrità dei dispositivi.  

 Lo stato di Attestazione dell'integrità del dispositivo client può essere usato per definire le regole per l'accesso condizionale nei criteri di conformità per i dispositivi gestiti da Configuration Manager con Microsoft Intune. Per maggiori dettagli, vedere [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  



<!--HONumber=Nov16_HO1-->

