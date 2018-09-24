---
title: Eseguire la migrazione di risorse dalla soluzione MDM ibrida alla versione autonoma di Intune
titleSuffix: Configuration Manager
description: Informazioni su come eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida a Intune in Azure.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 09ea3340d8474c69e6e346fc68120b8849159374
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111043"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune

*Si applica a: System Center Configuration Manager (Current Branch)*    

Questo articolo illustra la migrazione dalla soluzione MDM ibrida a un'esperienza solo cloud tramite Intune in Azure. 

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


Avviare la migrazione alla versione autonoma di Intune usando un approccio in più fasi. Con questo approccio, si testa un piccolo subset di utenti e dispositivi mentre la maggior parte degli utenti e dei dispositivi è ancora gestita con la soluzione MDM ibrida. Dopo aver verificato la funzionalità di Intune, avviare la migrazione di altre risorse a Intune.    

Per altre informazioni, vedere gli articoli seguenti:    
  
1.  [Importare i dati di Configuration Manager in Microsoft Intune](migrate-import-data.md)   

    Strumento Intune Data Importer:  

    - Raccoglie i dati relativi agli oggetti selezionati dalla gerarchia di Configuration Manager  

    - Fornisce dettagli sugli oggetti che è possibile selezionare per l'importazione   

    - Fornisce informazioni sui motivi per cui non è possibile importare alcuni oggetti  

    - Consente di importare gli oggetti selezionati nel tenant di Microsoft Intune  

    Questo passaggio è facoltativo. Può consentire di risparmiare tempo automatizzando il processo di ricreazione degli oggetti da Configuration Manager a Intune.  

2.  [Preparare Intune per la migrazione degli utenti](migrate-prepare-intune.md)    

    - Convalidare gli oggetti importati da Configuration Manager  

    - Creare nuovi oggetti  

    - Creare gruppi di Azure AD e assegnare gli oggetti a questi gruppi  

    - Installare i connettori NDES ed Exchange  

    Quando si completano i passaggi e si avvia la migrazione alla versione autonoma di Intune, l'operazione dovrebbe essere trasparente per gli utenti.   

3.  [Modificare l'autorità MDM per utenti specifici (autorità MDM mista)](migrate-mixed-authority.md)    

    Configurare un'autorità MDM mista nello stesso tenant. Selezionare alcuni utenti da gestire in Intune e continuare a gestire tutti gli altri dispositivi con la soluzione MDM ibrida. Verificare che Intune funzioni nei dispositivi per un piccolo subset di utenti prima di iniziare la migrazione di altri utenti.   

4.  [Modificare l'autorità MDM scegliendo la versione autonoma di Intune](change-mdm-authority.md)     

    Modificare l'autorità MDM a livello di tenant da Configuration Manager a Intune. Verrà eseguita la migrazione alla versione autonoma di Intune di tutti gli utenti e i dispositivi rimanenti. Dopo avere testato accuratamente la funzionalità di Intune nel passaggio precedente e aver eseguito la migrazione di tutti gli utenti o della maggior parte di essi, modificare l'autorità MDM a livello di tenant.



## <a name="request-assistance"></a>Richiedere assistenza
<!--Intune bug 2339232--> Per richiedere assistenza al programma Microsoft FastTrack, iniziare da [FastTrack per Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Fare clic su "Accedi" e immettere l'ID dell'organizzazione.  

2. Passare al dashboard e seguire i prompt per accedere al modulo **Request for Assistance** (Richiesta di assistenza).    

3. Microsoft esamina la richiesta e la indirizza al team appropriato a seconda delle esigenze specifiche e dell'idoneità.  

In questo dashboard si trovano anche procedure consigliate, strumenti e risorse degli esperti di FastTrack che consentono di sfruttare al meglio l'esperienza con Microsoft Cloud.

