---
title: Creare applicazioni Windows Phone | Documentazione Microsoft
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Windows Phone.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 866113ff-efd0-40d2-ac3a-2edd49732a24
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 557888d1f1f899e3198c430bbe5ccdd44178f824
ms.openlocfilehash: 5cd1ba42afd13e98565d24d1ec8a3ee209e8532c


---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Creare applicazioni Windows Phone con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di System Center Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni per i dispositivi Windows Phone è necessario tenere presente quanto segue.  

## <a name="general-considerations"></a>Considerazioni generali  
 Configuration Manager supporta la distribuzione dei tipi di file app seguenti:  

|Tipo di dispositivo|Tipi di file supportati|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|  

 Sono supportate le azioni di distribuzione seguenti:  

|Tipo di dispositivo|Azioni supportate|  
|-----------------|-----------------------|  
|Windows Phone 8 e Windows Phone 8.1|disponibile, richiesto, disinstalla|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Passaggi per distribuire l'app più recente del portale aziendale di Windows Phone con sostituzione  
 Nella tabella seguente vengono forniti i passaggi, i dettagli e ulteriori informazioni per la creazione e distribuzione dell'app del portale aziendale più recente di Windows Phone 8.  

|Passaggio|Altre informazioni|  
|----------|----------------------|  
|**Passaggio 1:** ottenere l'app più recente del portale aziendale.|Scaricare l' [App Portale aziendale di Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Passaggio 2:** firmare l'app del portale aziendale con il certificato Symantec.|Per informazioni sulla procedura di firma dell'app Portale aziendale, vedere [Configurare la gestione di dispositivi ibridi Windows Phone e Windows 10 con System Center Configuration Manager e Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Passaggio 3:** creare una nuova applicazione con la versione più recente dell'app del portale aziendale e specificare una relazione di sostituzione.|Per altre informazioni, vedere le indicazioni su [come creare applicazioni](../../apps/deploy-use/create-applications.md) e [come rivedere e sostituire le applicazioni](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Passaggio 4:** aggiungere l'applicazione alla Sottoscrizione guidata di Microsoft Intune.|Per altre informazioni, vedere [Configurare la gestione di dispositivi ibridi Windows Phone e Windows 10 con System Center Configuration Manager e Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Passaggio 5:** eliminare la distribuzione che viene creata automaticamente quando si aggiunge l'app Portale aziendale alla Sottoscrizione guidata di Microsoft Intune.|La sottoscrizione di Microsoft Intune ha creato una distribuzione automatica di questa app e la distribuzione non supporterà la sostituzione.|  
|**Passaggio 6:** creare una nuova distribuzione dell'applicazione. Nella pagina **Impostazioni distribuzione** della **Distribuzione guidata del software** selezionare **Aggiorna automaticamente tutte le versioni sostituite di questa applicazione**.|Creare una nuova distribuzione con sostituzione usando l'applicazione creata con la relazione di sostituzione.|  
|**Passaggio 7 (facoltativo):** per impostazione predefinita, le app di sostituzione vengono installate nei dispositivi dopo 7 giorni. Per distribuire prima l'app del portale aziendale ai dispositivi registrati in precedenza, modificare l'impostazione **Pianificare nuova valutazione per le distribuzioni** impostandola su un valore inferiore.<br /><br /> Se viene impostato su un valore inferiore rispetto a quello predefinito, questo valore può influire negativamente sulle prestazioni della rete e dei computer client.|Nessuna informazione aggiuntiva.|  



<!--HONumber=Dec16_HO3-->


