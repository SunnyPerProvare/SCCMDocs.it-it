---
title: Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune
titleSuffix: Configuration Manager
description: Informazioni su come eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida a Intune in Azure.
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/17/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune

*Si applica a: System Center Configuration Manager (Current Branch)*    

Fare riferimento a questo articolo per informazioni sulla migrazione dalla soluzione MDM ibrida (Intune integrato con Configuration Manager) a un'esperienza solo cloud con Intune in Azure. Se non si è certi di voler eseguire questa operazione, vedere [Scegliere tra Microsoft Intune autonomo e la gestione di dispositivi mobili ibridi con System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

È possibile avviare la migrazione alla versione autonoma di Intune usando un approccio per fasi che consente di testare un piccolo subset di utenti e dispositivi, lasciando che la maggior parte degli utenti e dei dispositivi continui a essere gestita con la soluzione MDM ibrida. Dopo aver verificato la funzionalità di Intune, è quindi possibile avviare la migrazione di altri utenti a Intune.    

Gli argomenti seguenti illustrano i passaggi per la migrazione degli utenti alla versione autonoma di Intune usando un approccio per fasi.    
  
1.  [Importare i dati di Configuration Manager in Microsoft Intune](migrate-import-data.md)   
    Lo strumento di importazione dati di Intune raccoglie i dati relativi agli oggetti selezionati dalla gerarchia di Configuration Manager, fornisce informazioni dettagliate sugli oggetti che è possibile selezionare per l'importazione e informazioni sui motivi per cui non è possibile importare alcuni oggetti e consente di importare gli oggetti selezionati nel tenant di Microsoft Intune. Questo passaggio è facoltativo, ma può consentire di risparmiare molto tempo automatizzando il processo di ricreazione degli oggetti da Configuration Manager a Intune. 
2.  [Preparare Intune per la migrazione degli utenti](migrate-prepare-intune.md)    
    Convalidare gli oggetti importati da Configuration Manager, creare nuovi oggetti, creare gruppi di AAD e assegnare oggetti a tali gruppi, installare il connettore del servizio Registrazione dispositivi di rete (NDES), Exchange Connector e così via. Quando si completano i passaggi e si avvia la migrazione alla versione autonoma di Intune, l'operazione dovrebbe essere trasparente per gli utenti.  
3.  [Modificare l'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md)    
    Configurare un'autorità MDM mista nello stesso tenant selezionando alcuni utenti da gestire in Intune, mentre tutti gli altri dispositivi continuano a essere gestiti con la soluzione MDM ibrida (Intune integrato con Configuration Manager). È possibile verificare che Intune funzioni come previsto nei dispositivi per un piccolo subset di utenti prima di iniziare la migrazione di altri utenti. 
4.  [Modificare l'autorità MDM scegliendo la versione autonoma di Intune](change-mdm-authority.md)     
    Modificare l'autorità MDM a livello di tenant da Configuration Manager a Intune. Verrà eseguita la migrazione alla versione autonoma di Intune di tutti gli utenti e i dispositivi rimanenti. Modificare l'autorità MDM a livello di tenant dopo avere testato accuratamente la funzionalità di Intune nel passaggio precedente e aver eseguito la migrazione di tutti gli utenti o della maggior parte di essi.

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->