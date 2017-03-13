---
title: "Abilitare una regola di protezione del dispositivo nei criteri di conformità | System Center Configuration Manager"
description: "Abilitare una regola di protezione dalle minacce nei criteri di conformità del dispositivo."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>Creare una regola di protezione dalle minacce per il dispositivo Lookout

*Si applica a: System Center Configuration Manager (Current Branch)*

## <a name="before-you-begin"></a>Prima di iniziare

Intune con Lookout Mobile Threat Protection offre la possibilità di rilevare le minacce per i dispositivi mobili ed eseguire una valutazione dei rischi sul dispositivo. In Configuration Manager è possibile creare una regola dei criteri di conformità che includa la valutazione dei rischi per determinare se il dispositivo è conforme. È quindi possibile usare i criteri di accesso condizionale per consentire o bloccare l'accesso a Exchange, SharePoint e ad altri servizi sulla base della conformità del dispositivo.

Per consentire a Lookout Mobile Threat Protection di influenzare i criteri di conformità del dispositivo, tenere presente quanto segue:

-   Nei criteri di conformità deve essere abilitata la regola **Protezione dalle minacce per il dispositivo**.

-   Lo stato della pagina **Stato di Lookout** della **console di amministrazione di Intune** deve essere **Attivo**. Per altri dettagli e istruzioni su come attivare l'integrazione di Lookout, vedere l'argomento [Enable Lookout MTP connection in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune) (Abilitare la connessione MTP Lookout in Intune).

Prima di creare la regola di protezione dalle minacce nei criteri di conformità, è consigliabile eseguire le operazioni seguenti:

1.  [Configurare la sottoscrizione con la protezione dalle minacce per il dispositivo Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Abilitare la connessione a Lookout in Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Configurare l'app Lookout for Work](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>La regola di conformità viene applicata solo dopo aver completo la configurazione.

## <a name="to-create-a-device-threat-protection-rule"></a>Per creare una regola di protezione dalle minacce

Come parte della configurazione di Lookout Mobile Threat Protection, nella [console di Lookout](https://aad.lookout.com) è necessario creare un criterio che classifichi le minacce secondo i livelli Alto, Medio e Basso. Nei criteri di conformità di Intune il livello di minaccia verrà usato per impostare il livello di minaccia massimo consentito.

Per creare una regola di protezione dalle minacce per il dispositivo Lookout:

1.  Nella console di Configuration Manager selezionare l'area di lavoro **Asset e conformità**.

2.  In **Asset e conformità** espandere **Criteri di conformità**.

3.  Fare clic con il pulsante destro del mouse su **Criteri di conformità** e selezionare **Crea criteri di conformità**.

4.  Immettere il nome dei criteri di conformità e selezionare **Regole di conformità per i dispositivi gestiti senza il client di Configuration Manager**.

5.  Selezionare le piattaforme del sistema operativo per le quali sarà eseguito il provisioning con i criteri di conformità, ad esempio Android 4.1 e versioni successive e/o iOS 8 e versioni successive.

6.  Nella pagina **Regole** fare clic su **Nuova** per specificare le regole per un dispositivo conforme.

7.  Nella pagina **Aggiungi regola** definire una nuova regola con le informazioni seguenti:
    1.  Condizione: livello di rischio massimo per la protezione dalle minacce per il dispositivo.
    
    2.  Valore: il valore può essere uno dei seguenti:
        1.  **Nessuno (protetto)**: questa è l'impostazione più sicura e indica che il dispositivo non può avere alcuna minaccia. Se viene rilevato un qualsiasi livello di minaccia, il dispositivo viene valutato come non conforme.
        2.  **Basso**: il dispositivo viene valutato come conforme se sono presenti solo minacce di livello Basso. Se sono presenti minacce di livello più alto, lo stato del dispositivo passa a Non conforme.
        3.  **Medio**: il dispositivo viene valutato come conforme se le minacce individuate sono di livello Basso o Medio. Se vengono rilevate minacce di livello più alto, il dispositivo viene considerato non conforme.
        4.  **Alto**: questa opzione è la meno sicura. L'opzione consente praticamente tutti i livelli di minaccia e può essere utile se si usa la soluzione soltanto per la creazione di report.

>[!IMPORTANT]
>Se si creano criteri di accesso condizionale per Office 365 e altri servizi, viene presa in considerazione la valutazione di conformità sopra descritta e ai dispositivi non conformi viene bloccato l'accesso alle risorse dell'azienda fino a quando la minaccia non viene risolta.
