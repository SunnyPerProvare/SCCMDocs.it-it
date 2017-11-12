---
title: "Abilitare una regola di protezione per i dispositivi nei criteri di conformità"
titleSuffix: Configuration Manager
description: "Abilitare una regola di protezione dalle minacce nei criteri di conformità del dispositivo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
caps.latest.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: d74360ce800f030e85e2b87defc1de3376c6aee5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Abilitare una regola di protezione dalle minacce per i dispositivi mobili nei criteri di conformità

*Si applica a: System Center Configuration Manager (Current Branch)*

Intune con Lookout Mobile Threat Protection offre la possibilità di rilevare le minacce per i dispositivi mobili ed eseguire una valutazione dei rischi sul dispositivo. In Configuration Manager è possibile creare una regola nei criteri di conformità che includa la valutazione dei rischi per determinare se il dispositivo è conforme. È quindi possibile usare i criteri di accesso condizionale per consentire o bloccare l'accesso a Exchange, SharePoint e ad altri servizi sulla base della conformità del dispositivo.

Per consentire a Lookout Mobile Threat Protection di influenzare i criteri di conformità del dispositivo, tenere presente quanto segue:

* Nei criteri di conformità deve essere abilitata la regola **Protezione dalle minacce per il dispositivo**.

* Lo stato della pagina **Stato di Lookout** della **console di amministrazione di Intune** deve essere **Attivo**. Per altri dettagli e istruzioni su come attivare l'integrazione di Lookout, vedere l'argomento [Enable Lookout MTP connection in Intune](enable-lookout-connection-in-intune.md) (Abilitare la connessione MTP Lookout in Intune).


Prima di creare la regola Protezione dalle minacce per il dispositivo nei criteri di conformità, è consigliabile [configurare la sottoscrizione a Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md), [abilitare la connessione a Lookout in Intune](enable-lookout-connection-in-intune.md) e [configurare l'app Lookout for Work](configure-and-deploy-lookout-for-work-apps.md). La regola di conformità viene applicata solo dopo il completamento della configurazione.

Per abilitare la regola Protezione dalle minacce per il dispositivo, è possibile usare un criterio di conformità esistente o crearne uno nuovo.

Come parte della configurazione di Lookout Mobile Threat Protection, nella [console di Lookout](https://aad.lookout.com) è necessario creare un criterio che classifichi le minacce secondo i livelli Alto, Medio e Basso. Nei criteri di conformità di Intune questi livelli verranno usati per impostare il livello di minaccia massimo consentito.

Nella pagina **Regole** della Creazione guidata criterio di conformità definire una nuova regola con le informazioni seguenti:
  * Condizione: livello di rischio massimo per la protezione dalle minacce per il dispositivo.
  * Valore: il valore può essere uno dei seguenti:
    * **Nessuno (protetto)**: questa è l'impostazione più sicura e indica che il dispositivo non può avere alcuna minaccia. Se viene individuato un qualsiasi livello di minaccia, il dispositivo viene valutato come non conforme.
    * **Basso**: il dispositivo viene valutato come conforme se sono presenti solo minacce di livello Basso. Se sono presenti minacce di livello più alto, lo stato del dispositivo passa a Non conforme.
    * **Medio**: il dispositivo viene valutato come conforme se le minacce individuate sono di livello Basso o Medio. Se vengono rilevate minacce di livello più alto, il dispositivo viene considerato non conforme.
    * **Alto**: questa opzione è la meno sicura. L'opzione consente praticamente tutti i livelli di minaccia e può essere utile se si usa la soluzione soltanto per la creazione di report.

Se si creano criteri di accesso condizionale per Office 365 e altri servizi, viene presa in considerazione la valutazione di conformità sopra descritta e ai dispositivi non conformi viene bloccato l'accesso alle risorse dell'azienda fino a quando la minaccia non viene risolta.

Lo stato di Protezione dalle minacce per il dispositivo viene visualizzato nel nodo **Sicurezza** dell'area di lavoro **Monitoraggio**.
Viene visualizzato un grafico con un riepilogo dello stato con i diversi livelli di minaccia. È possibile fare clic sulle diverse sezioni del grafico per visualizzare informazioni aggiuntive, ad esempio il numero di dispositivi indicati come non conformi dalla piattaforma e gli eventuali errori segnalati.
È anche possibile visualizzare lo stato dei singoli dispositivi nell'area di lavoro **Asset e conformità**, in **Dispositivi**.  Per visualizzare lo stato, è possibile aggiungere le colonne **Protezione dalle minacce per il dispositivo** e **Livello di minaccia del dispositivo**.  Queste colonne non vengono visualizzate per impostazione predefinita.
