---
title: "Aggiornare i dispositivi Windows a una versione più recente | System Center Configuration Manager"
description: "Aggiornare automaticamente i dispositivi che eseguono Windows 10 Desktop, Windows 10 Mobile, o Windows 10 Holographic all'edizione più recente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7ee088f6da266742e7836499a7f0e072bf446a62


---

# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Aggiornare i dispositivi Windows con i criteri di aggiornamento edizione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I **criteri di aggiornamento edizione** di System Center Configuration Manager consentono di aggiornare automaticamente i dispositivi che eseguono una delle versioni seguenti di Windows 10 a un'edizione più recente:

- Windows 10 Desktop
- Windows 10 Mobile
- Windows 10 Holographic

Sono supportati i percorsi di aggiornamento seguenti:
- Da Windows 10 Pro a Windows 10 Enterprise
- Da Windows 10 Home a Windows 10 Education
- Da Windows 10 Mobile a Windows 10 Mobile Enterprise
- Da Windows 10 Holographic Pro a Windows 10 Holographic Enterprise

È necessario che i dispositivi siano registrati in Microsoft Intune. Questa funzionalità non è attualmente compatibile con PC che eseguono il software client di Configuration Manager o con PC che sono gestiti da un software MDM locale.

## <a name="before-you-start"></a>Prima di iniziare  
 Prima di iniziare l'aggiornamento dei dispositivi alla versione più recente, è necessario uno degli elementi seguenti:  

-   Un codice Product Key valido per installare la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri (per sistemi operativi desktop)  

-   Un file di licenza da Microsoft che contiene le informazioni sulle licenze per installare la nuova versione di Windows in tutti i dispositivi a cui sono destinati i criteri (per Windows 10 Mobile e Windows 10 Holographic).

- Per creare e distribuire questo tipo di criteri, è necessario aver assegnato il ruolo di sicurezza **amministratore completo** di Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurare i criteri di aggiornamento edizione  

1.  Nella console di Configuration Manager fare clic su **Assets e conformità** > **Impostazioni di conformità** > **Aggiornamento edizione di Windows 10**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea criteri aggiornamento edizione**.  

4.  Fare clic su **Crea criterio**.  

5.  Nella pagina **Generale** della **Creazione guidata criteri aggiornamento edizione**specificare le informazioni seguenti:  

    -   **Nome** - Immettere un nome per i criteri di aggiornamento edizione.  

    -   **Descrizione** (facoltativo) - Immettere facoltativamente una descrizione per i criteri che consenta di identificarli nella console di Intune.  

    -   **SKU per aggiornare il dispositivo a** - Nell'elenco a discesa selezionare la versione di Windows 10 Desktop, Windows 10 Holographic o Windows 10 Mobile a cui aggiornare i dispositivi specificati.  

    -   **Informazioni di licenza** - Selezionare una delle opzioni seguenti:  

        -   **Codice Product Key** - Immettere un codice Product Key di Windows 10 valido che verrà usato per seguire l'aggiornamento dei dispositivi specificati che eseguono sistemi operativi Windows 10 Desktop.  

            > [!NOTE]  
            >  Dopo aver creato criteri che contengono un codice Product Key, non è possibile modificare il codice Product Key in un secondo momento, perché il codice viene nascosto per motivi di sicurezza. Per modificare il codice Product Key, è necessario immettere nuovamente l'intero codice.  

        -   **File di licenza** - Fare clic su **Sfoglia** per selezionare un file di licenza valido in formato XML che verrà usato per aggiornare i dispositivi specificati che eseguono sistemi operativi Windows 10 Holographic e Windows 10 Mobile.  

6.  Completare la procedura guidata.  

 I nuovi criteri verranno visualizzati nel nodo **Aggiornamento edizione Windows 10** dell'area di lavoro **Asset e conformità** .  

## <a name="deploy-the-edition-upgrade-policy"></a>Distribuire i criteri di aggiornamento edizione  

1.  Nella console di Configuration Manager fare clic su **Assets e conformità** > **Impostazioni di conformità** > **Aggiornamento edizione di Windows 10**.  

3.  Selezionare i criteri di aggiornamento edizione Windows 10 da distribuire e quindi nel gruppo **Distribuzione** della scheda **Home** fare clic su **Distribuisci**.  

4.  Nella finestra di dialogo **Distribuisci aggiornamento edizione Windows 10** scegliere la raccolta di utenti o dispositivi a cui distribuire i criteri e la pianificazione per la valutazione dei criteri, quindi fare clic su **OK**.  

 È possibile monitorare la distribuzione appena creata dal nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** .  

 Quando i criteri raggiungono un PC Windows specificato, il PC verrà riavviato entro due ore per applicare l'aggiornamento. Informare tutti gli utenti interessati dalla distribuzione dei criteri o pianificare la distribuzione dei criteri in ore non lavorative.



<!--HONumber=Nov16_HO1-->


