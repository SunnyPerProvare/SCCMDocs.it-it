---
title: Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune
titleSuffix: Configuration Manager
description: Informazioni su come eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida a Intune in Azure.
author: aczechowski
manager: dougeby
ms.date: 09/12/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 4e2471b06c1767bcf914000d626bb22b6ee2bd6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
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