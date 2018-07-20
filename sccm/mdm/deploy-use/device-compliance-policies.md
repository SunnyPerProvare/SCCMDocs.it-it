---
title: Criteri di conformità dei dispositivi
titleSuffix: Configuration Manager
description: Informazioni su come gestire i criteri di conformità in Configuration Manager per rendere i dispositivi conformi ai criteri di accesso condizionale.
ms.date: 07/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c27c945b384a9769d008667f124d414275a3c11
ms.sourcegitcommit: e54e9d4a735e72b84095e0017c5bec50af480207
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/14/2018
ms.locfileid: "39039591"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Criteri di conformità del dispositivo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I criteri di conformità in Configuration Manager definiscono le regole e le impostazioni che un dispositivo deve soddisfare per essere considerato conforme ai criteri di accesso condizionale. È anche possibile usare tali criteri per monitorare e correggere i problemi di conformità con i dispositivi, indipendentemente dall'accesso condizionale.  


> [!IMPORTANT]  
>  Questo articolo descrive i criteri di conformità per i dispositivi gestiti da Microsoft Intune. I criteri di conformità per i dispostivi gestiti dal client di Configuration Manager sono descritti in [Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 Queste regole includono requisiti come:  

-   PIN e password per accedere a un dispositivo  

-   Crittografia dei dati memorizzati sul dispositivo  

-   Se il dispositivo è jailbroken o rooted  

-   Se la posta elettronica nel dispositivo viene gestita da un criterio Intune o se il dispositivo è segnalato come non integro dal servizio di attestazione dell'integrità del dispositivo Windows.  

-   App che non possono essere installate nel dispositivo.  


 I criteri di conformità vengono distribuiti alle raccolte dell'utente. Quando un criterio di conformità viene distribuito a un utente, la conformità viene controllata su tutti i dispositivi dell’utente.  



## <a name="supported-device-types"></a>Tipi di dispositivi supportati

 Nella tabella seguente sono elencati i tipi di dispositivi supportati dai criteri di conformità e il modo in cui le impostazioni di non conformità vengono gestite quando i criteri vengono usati con i criteri di accesso condizionale.  

|Regola|Windows 8.1 e versioni successive|Windows Phone 8.1 e versioni successive|iOS 6.0 e versioni successive|Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configurazione di PIN o password**|Corretto|Corretto|Corretto|In quarantena|  
|**Crittografia dispositivo**|N/D|Corretto|Corretto (impostando il PIN)|In quarantena<br>(Android for Work sempre crittografato)|  
|**Dispositivo jailbroken o rooted**|N/D|N/D|In quarantena (non è un'impostazione)|In quarantena (non è un'impostazione)|  
|**Profilo di posta elettronica**|N/D|N/D|In quarantena|N/D|  
|**Versione minima del sistema operativo**|In quarantena|In quarantena|In quarantena|In quarantena|  
|**Versione massima del sistema operativo**|In quarantena|In quarantena|In quarantena|In quarantena|  
|**Attestazione dell'integrità dei dispositivi (aggiornamento 1602)**|L'impostazione non è applicabile a Windows 8.1<br /><br /> Windows 10 e Windows 10 Mobile vengono messi in quarantena.|N/D|N/D|N/D|  
|**App che non possono essere installate**|N/D|N/D|In quarantena|In quarantena|

 **Corretto** = la conformità viene forzata dal sistema operativo del dispositivo, ad esempio, l'utente è obbligato a impostare un PIN. Non riguarda i casi in cui l'impostazione non è conforme.  

 **In quarantena** = la conformità non viene forzata dal sistema operativo del dispositivo, ad esempio, l'utente di dispositivi Android non è obbligato a crittografare il dispositivo. In questo caso:  

-   Il dispositivo viene bloccato se i criteri di accesso condizionale sono destinati all'utente.  

-   Il portale aziendale o il portale Web informa l'utente di eventuali problemi di conformità.  



## <a name="devices-without-any-assigned-compliance-policy"></a>Dispositivi senza criteri di conformità assegnati
<!--2520152--> A partire da luglio 2018, è necessario configurare i dispositivi specificando se devono essere considerati conformi o non conformi nel caso in cui non abbiano criteri di conformità assegnati. Per impostazione predefinita, i dispositivi senza criteri di conformità assegnati vengono considerati conformi. Usare la procedura seguente per modificare questa impostazione nel portale di Azure:

1. Accedere a [Intune nel portale di Azure](https://aka.ms/intuneportal).  

2. Selezionare **Conformità del dispositivo**, quindi selezionare **Impostazioni dei criteri di conformità** nel gruppo Installazione.  

3. Per l'impostazione **Contrassegna i dispositivi senza criteri di conformità assegnati come**, selezionare una delle opzioni seguenti:  

     - **Conforme** (impostazione predefinita): i dispositivi senza criteri di conformità assegnati vengono considerati conformi. Se l'accesso condizionale è abilitato, questi dispositivi possono accedere alle risorse interne.  

     - **Non conforme**: i dispositivi senza criteri di conformità assegnati vengono considerati non conformi. Se l'accesso condizionale è abilitato, questi dispositivi vengono bloccati dalle risorse interne, in base alle condizioni nei criteri di accesso condizionale.  

4. Fare clic su Salva.  

Per ogni piattaforma, è consigliabile distribuire almeno un criterio di conformità a tutti gli utenti nell'ambiente. Impostare l'opzione **Non conforme** per garantire la sicurezza delle risorse interne. Per altre informazioni, vedere il post di blog [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) (Miglioramenti apportati alla sicurezza nel servizio Intune).



## <a name="next-steps"></a>Passaggi successivi  
[Create and deploy a device compliance policy](/sccm/mdm/deploy-use/create-compliance-policy) (Creare e distribuire criteri di conformità del dispositivo)

### <a name="see-also"></a>Vedere anche  
 [Gestire l'accesso ai servizi in Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)