---
title: Configurazione del risparmio energia
titleSuffix: Configuration Manager
description: Configurare il risparmio energia in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ceb8c07c111818136db7c3815eee58cc87ae75c8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333485"
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configurazione del risparmio energia in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter usare il risparmio energia in System Center Configuration Manager, è necessario eseguire i passaggi di configurazione seguenti.  

## <a name="enable-and-configure-power-management-client-settings"></a>Abilitare e configurare le impostazioni client di risparmio energia.  
 Questa procedura consente di configurare le impostazioni client predefinite per il risparmio energia e di applicarle a tutti i computer nella gerarchia. Per applicare queste impostazioni solo ad alcuni computer, creare un'impostazione client di dispositivo personalizzata e assegnarla a una raccolta contenente i computer in cui si vuole usare la funzionalità di risparmio energia. Per altre informazioni su come creare impostazioni dispositivo personalizzate, vedere [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Per abilitare le impostazioni client di risparmio energia  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Impostazioni client**.  

3.  Fare clic su **Impostazioni client predefinite**.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Impostazioni client predefinite** fare clic su **Risparmio energia**.  

6.  Configurare il valore seguente per le impostazioni client di risparmio energia:  

    -   **Consentire il risparmio energia dei dispositivi** : dall'elenco a discesa selezionare **Vero** per abilitare la funzionalità di risparmio energia.  

7.  Configurare le impostazioni client necessarie. Per un elenco di impostazioni client di risparmio energia che è possibile configurare, vedere la sezione [Risparmio energia](../../../../core/clients/deploy/about-client-settings.md#power-management) nell'argomento [Informazioni sulle impostazioni client in Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Impostazioni client predefinite** .  

 I computer client verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero criteri per un singolo client, vedere [Come gestire i client in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Escludere computer dal risparmio energia  
 È possibile evitare che raccolte di computer specifiche ricevano impostazioni di risparmio energia. Se un computer è membro di una raccolta esclusa dalle impostazioni di risparmio energia, a questo computer le impostazioni di risparmio energia non vengono applicate, neanche se il computer è membro di un'altra raccolta che applica impostazioni di risparmio energia.  

 È necessario escludere i computer dall'attivazione della funzione di risparmio energia nei casi seguenti:  

-   Un requisito aziendale impone che i computer siano sempre attivi.  

-   È stata creata una raccolta di controllo di computer alla quale non si vogliono applicare impostazioni di risparmio energia.  

-   Alcuni computer non sono in grado di applicare impostazioni di risparmio energia.  

-   Si vogliono escludere dalla funzionalità di risparmio energia i computer che eseguono Windows Server.  

> [!NOTE]  
>  Se l'opzione **Consentire agli utenti di escludere il dispositivo utilizzato dal risparmio energia** è configurata nelle impostazioni client, gli utenti possono escludere i propri computer dall'applicazione del risparmio energia tramite Software Center.  

 Per individuare i computer esclusi dal risparmio energia, eseguire il report **Computer esclusi**. Per altre informazioni su questo report vedere [Computer esclusi](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) nell'argomento [Come monitorare e pianificare il risparmio energia in Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Le impostazioni di risparmio energia applicate a computer che eseguono Windows XP o Windows Server 2003 non vengono ripristinate sui valori originali, neanche se si escludono i computer dalla funzionalità di risparmio energia. Nelle versioni successive di Windows, l'esclusione di un computer dal risparmio energia causa il ripristino sui valori originali di tutte le impostazioni di risparmio energia. Non è possibile ripristinare i valori originali per singole impostazioni di risparmio energia.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Per escludere una raccolta di computer dal risparmio energia  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Nell'elenco **Raccolte dispositivi** selezionare la raccolta che si vuole escludere dal risparmio energia e quindi nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà**.  

4.  Nella scheda **Risparmio energia** della finestra di dialogo **Proprietà** *<Nome raccolta\>* selezionare **Non applicare mai le impostazioni di risparmio energia ai computer di questa raccolta**.  

5.  Fare clic su **OK** per chiudere la finestra di dialogo ***Proprietà* *<Nome raccolta\>* e salvare le impostazioni.  
