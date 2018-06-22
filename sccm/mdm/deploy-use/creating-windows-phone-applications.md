---
title: Creare applicazioni Windows Phone
titleSuffix: Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i dispositivi Windows Phone.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c755db47c9d3acb9c858ecb5bed14bb36055663b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347230"
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Creare applicazioni Windows Phone con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di System Center Configuration Manager contiene uno o più tipi di distribuzione che comprendono le informazioni e i file di installazione necessari per distribuire software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

 È possibile creare applicazioni usando due metodi:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere [Avviare la Creazione guidata applicazione](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). Inoltre, quando si creano e si distribuiscono applicazioni per i dispositivi Windows Phone, tenere presenti le considerazioni seguenti.  

## <a name="general-considerations"></a>Considerazioni generali  
 Configuration Manager supporta la distribuzione dei tipi di file app seguenti:  

|Tipo di dispositivo|Tipi di file supportati|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 Sono supportate le azioni di distribuzione seguenti:  

|Tipo di dispositivo|Azioni supportate|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 e Windows 10 Mobile|Disponibile, Richiesto, Disinstalla|  

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
