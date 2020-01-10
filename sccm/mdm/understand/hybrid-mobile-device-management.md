---
title: Soluzione MDM ibrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Informazioni sulla gestione di dispositivi mobili (MDM) ibrida con Configuration Manager e Microsoft Intune.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aaa1a6e3914c590a7575562fb5e6a29e31043c16
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826408"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Soluzione MDM ibrida con Configuration Manager e Intune

*Si applica a: Configuration Manager (Current Branch)*

> [!WARNING]
> L'offerta di servizio MDM ibrido è stata ritirata a partire dal 1° settembre 2019. Tutti i dispositivi MDM ibridi rimanenti non riceveranno i criteri, le app o gli aggiornamenti della sicurezza.

## <a name="remove-hybrid-mdm"></a>Rimuovi MDM ibrida

Se il sito di Configuration Manager dispone di una sottoscrizione Microsoft Intune, è necessario rimuoverlo.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**. Espandere **Servizi cloud** e selezionare il nodo **Sottoscrizione a Microsoft Intune**. Eliminare la sottoscrizione di Intune esistente.

1. Nella **procedura guidata rimuovi Microsoft Intune sottoscrizione**selezionare l'opzione per **rimuovere Microsoft Intune sottoscrizione da Configuration Manager**, quindi fare clic su **Avanti**.

1. completare la procedura guidata.

## <a name="deprecation-announcement"></a>Annuncio di deprecazione

La nota seguente è l'annuncio originale di deprecazione:

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). A partire dalla versione 1902 del servizio Intune, prevista per la fine di febbraio 2019, i nuovi clienti non possono creare una nuova connessione ibrida.
> <!--Intune feature 2683117-->  
> Dopo il lancio in Azure oltre un anno fa, sono state aggiunte a Intune centinaia di nuove funzionalità del servizio leader di settore e richieste dai clienti. Il servizio offre ora molte più funzionalità di quelle offerte nella gestione di dispositivi mobili (MDM) ibrida. Intune in Azure offre un'esperienza amministrativa più integrata e semplificata per le esigenze di mobilità aziendale.
>
> La maggior parte dei clienti sceglie di conseguenza Intune in Azure piuttosto che la soluzione MDM ibrida. Sempre meno clienti usano la soluzione MDM ibrida, mentre il numero di quelli che passano al cloud è in continuo aumento. L'1 settembre 2019, Microsoft ritirerà quindi l'offerta di servizio MDM ibrido. Pianificare la [migrazione a Intune in Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) per la gestione dei dispositivi mobili.
>
> Questa modifica non incide su Configuration Manager locale o sulla [co-gestione per i dispositivi Windows 10](/sccm/comanage/overview). Se non si è certi di usare la soluzione MDM ibrida, passare all'area di lavoro **Amministrazione** della console di Configuration Manager, espandere **Servizi Cloud** e fare clic su **Sottoscrizioni a Microsoft Intune**. Se è configurata una sottoscrizione di Microsoft Intune, il tenant è configurato per la soluzione MDM ibrida.
>
> **Quali sono le conseguenze di questa modifica?**
>
> - Microsoft supporterà l'utilizzo di MDM ibrido per il prossimo anno. La funzionalità continuerà a ricevere le principali correzioni di bug. Microsoft supporterà le funzionalità esistenti nelle nuove versioni del sistema operativo, ad esempio la registrazione in iOS 12. Non saranno disponibili nuove funzionalità per la soluzione MDM ibrida.  
>
> - Se si esegue la migrazione a Intune in Azure prima della fine dell'offerta MDM ibrida, non ci sarà alcun impatto sugli utenti finali.  
>
> - L'1 settembre 2019, i dispositivi MDM ibridi rimanenti non riceveranno più criteri, app o aggiornamenti della sicurezza.  
>
> - Le licenze rimangono invariate. Le licenze di Intune in Azure sono incluse con la soluzione MDM ibrida.  
>
> - La funzionalità MDM locale in Configuration Manager non è deprecata. A partire da Configuration Manager versione 1810, è possibile usare MDM locale senza una connessione a Intune. Per altre informazioni, vedere la pagina relativa a [una connessione Intune non è più necessaria per le nuove distribuzioni MDM locali](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm).
>
> - La funzionalità di accesso condizionale locale di Configuration Manager è anche deprecata con MDM ibrida. Se si usa l'accesso condizionale nei dispositivi gestiti con il client di Configuration Manager, assicurarsi che siano protetti prima della migrazione.
>     1. Configurare i criteri di accesso condizionale in Azure
>     2. Configurare i criteri di conformità nel portale di Intune
>     3. Terminare la migrazione ibrida e impostare l'autorità MDM su Intune
>     4. Abilitare la co-gestione
>     5. Spostare il carico di lavoro di co-gestione dei criteri di conformità in Intune
>
>     Per altre informazioni, vedere [accesso condizionale con la co-gestione](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access).
>
> **Operazioni di preparazione alla modifica**
>
> - Iniziare a pianificare la migrazione della soluzione MDM dalla console di ConfigMgr ad Azure. Molti clienti, incluso Microsoft IT, hanno completato questo processo. Per altre informazioni, vedere questo [case study di Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Esaminare gli strumenti e la documentazione seguenti per semplificare il processo di transizione dalla soluzione MDM ibrida a Intune in Azure:  
>   - [Importare i dati di Configuration Manager in Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>   - [Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
>
> - Contattare il Partner of Record o il partner di FastTrack per assistenza. [FastTrack per Microsoft 365](https://aka.ms/hybrid_fasttrack) può agevolare la migrazione dalla soluzione MDM ibrida a Intune in Azure.
>
> Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://aka.ms/hybrid_notification).

<!--

With the hybrid mobile device management (MDM) feature of Configuration Manager, manage iOS, Windows, and Android devices. All management tasks are handled from the Configuration Manager console where you perform the rest of your management tasks seamlessly integrated with Microsoft Intune's online service over the internet. Use Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned devices to access company data. 

This article assumes that you use Configuration Manager to manage computers. It also assumes that you're interested in extending the Configuration Manager console with Intune to manage mobile devices. 



## Capabilities

Hybrid MDM supports the following management capabilities on devices:

-   Retire and wipe devices  

-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication  

-   Deploy line-of-business (LOB) apps to devices  

-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play  

-   Collect hardware inventory  

-   Collect software inventory by using built-in reports  



## Hybrid MDM enrollment

To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed.

- **"Bring your own device" (BYOD)**: Users enroll their personal phones, tablets, or PCs  

- **Corporate-owned device (COD)**: Enable management scenarios like remote wipe, shared devices, or user affinity for a device  

- If you use [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

-->

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle funzionalità supportate per la gestione dei dispositivi MDM, vedere gli articoli seguenti:

- [Che cos'è Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [Che cos'è MDM locale?](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)
- [Gestione di dispositivi con Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)
