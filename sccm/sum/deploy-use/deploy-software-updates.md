---
title: Distribuire gli aggiornamenti software | Microsoft Docs
description: Scegliere gli aggiornamenti software nella console di Configuration Manager per avviare manualmente il processo di distribuzione o distribuire automaticamente gli aggiornamenti.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMDeploy"></a> Distribuire gli aggiornamenti software  

*Si applica a: System Center Configuration Manager (Current Branch)*

La fase di distribuzione degli aggiornamenti software è il processo di distribuzione degli aggiornamenti software. Indipendentemente da come vengono distribuiti gli aggiornamenti software, gli aggiornamenti sono in genere aggiunti a un gruppo di aggiornamento software, gli aggiornamenti software vengono scaricati nei punti di distribuzione e il gruppo di aggiornamento viene distribuito ai client. Quando viene creata la distribuzione, i criteri di aggiornamento software vengono inviati ai computer client, i file di contenuto dell'aggiornamento software vengono scaricati da un punto di distribuzione nella cache locale dei computer client e gli aggiornamenti software sono quindi disponibili per l'installazione nel client. I client su Internet scaricano il contenuto da Microsoft Update.  

> [!NOTE]  
>  È possibile configurare un client nella Intranet in modo che scarichi gli aggiornamenti software da Microsoft Update se un punto di distribuzione non è disponibile.  

> [!NOTE]  
>  A differenza di altri tipi di distribuzione gli aggiornamenti software vengono tutti scaricati nella cache del client, indipendentemente dall'impostazione della dimensione massima della cache sul client. Per altre informazioni sull'impostazione della cache client, vedere [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Se si configura una distribuzione degli aggiornamenti software necessaria, gli aggiornamenti software vengono installati automaticamente alla scadenza programmata. In alternativa, l'utente del computer client può pianificare o avviare l'installazione dell'aggiornamento software prima della scadenza. Dopo il tentativo di installazione, i computer client inviano messaggi di stato al server del sito per segnalare se l'installazione dell'aggiornamento software è stata eseguita correttamente. Per altre informazioni sulle distribuzioni degli aggiornamenti software, vedere [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Esistono due scenari principali per la distribuzione di aggiornamenti software: la distribuzione manuale e la distribuzione automatica. In genere, si effettuerà inizialmente la distribuzione manuale degli aggiornamenti software per creare una linea di base per i computer client e quindi si gestiranno gli aggiornamenti software sui client usando la distribuzione automatica.  

## <a name="BKMK_ManualDeployment"></a> Distribuire manualmente gli aggiornamenti software
È possibile scegliere gli aggiornamenti software nella console di Configuration Manager per avviare manualmente il processo di distribuzione. In genere si utilizzerà questo metodo di distribuzione per mantenere aggiornati i computer client con gli aggiornamenti software richiesti prima di creare regole di distribuzione automatica che gestiranno le distribuzioni degli aggiornamenti software in corso a cadenza mensile e per distribuire i requisiti di aggiornamento software fuori banda. Il seguente elenco descrive il flusso di lavoro generale per la distribuzione manuale degli aggiornamenti software:  

1. Filtrare gli aggiornamenti software che usano requisiti specifici. Ad esempio, è possibile fornire criteri per il recupero di tutti gli aggiornamenti software critici o della sicurezza necessari su più di 50 computer client.  
2. Creare un gruppo di aggiornamenti software che contenga gli aggiornamenti software.  
3. Scaricare il contenuto per gli aggiornamenti software nel gruppo di aggiornamenti software.  
4. Distribuire manualmente il gruppo di aggiornamenti software.

Per informazioni dettagliate, vedere [Distribuire manualmente gli aggiornamenti software](manually-deploy-software-updates.md).

## <a name="automatically-deploy-software-updates"></a>Distribuire automaticamente gli aggiornamenti software
La distribuzione automatica degli aggiornamenti software viene configurata con una regola di distribuzione automatica. Si tratta di un metodo comune di distribuzione per aggiornamenti software mensili ("Patch Tuesday") e per la gestione degli aggiornamenti delle definizioni. Quando si esegue la regola, gli aggiornamenti software vengono rimossi dal gruppo di aggiornamenti software (se si usa un gruppo di aggiornamento esistente), gli aggiornamenti software che soddisfano un criterio specificato (ad esempio, tutti gli aggiornamenti software della sicurezza rilasciati il mese precedente) vengono aggiunti a un gruppo di aggiornamenti software, i file di contenuto per gli aggiornamenti software vengono scaricati e copiati nei punti di distribuzione e gli aggiornamenti software vengono distribuiti nei computer client nella raccolta di destinazione. L'elenco seguente descrive il flusso di lavoro generale per la distribuzione automatica degli aggiornamenti software:  

1.  Creare una regola di distribuzione automatica che specifica le impostazioni di distribuzione.
2.  Gli aggiornamenti software vengono aggiunti a un gruppo di aggiornamenti software.  
3.  Il gruppo di aggiornamenti software viene distribuito ai computer client nella raccolta di destinazione, se specificato.  

È necessario determinare la strategia di distribuzione da usare nel proprio ambiente. Ad esempio, è possibile creare la regola di distribuzione automatica e trovare una raccolta di destinazione dei client di prova. Dopo aver verificato che gli aggiornamenti software siano installati nel gruppo di prova, è possibile aggiungere una nuova distribuzione alla regola o modificare la raccolta nella distribuzione esistente in una raccolta di destinazione che include un set di client più ampio. Gli oggetti di aggiornamento software creati dalle regole di distribuzione automatica sono interattivi.  

-   Gli aggiornamenti software distribuiti usando una regola di distribuzione automatica vengono distribuiti automaticamente nei nuovi client aggiunti alla raccolta di destinazione.  
-   I nuovi aggiornamenti software aggiunti a un gruppo di aggiornamenti software vengono distribuiti automaticamente ai client nella raccolta di destinazione.  
-   È possibile abilitare o disabilitare le distribuzioni in qualsiasi momento per la regola di distribuzione automatica.  

Dopo aver creato una regola di distribuzione automatica, è possibile aggiungere altre distribuzioni alla regola. Ciò consente di gestire la complessità della distribuzione di aggiornamenti diversi a raccolte differenti. Ogni nuova distribuzione include l'intera gamma dell'esperienza di monitoraggio di funzionalità e distribuzione. Ogni nuova distribuzione aggiunta:  

-   Utilizza lo stesso gruppo e lo stesso pacchetto di aggiornamento creato alla prima esecuzione di ADR  
-   Può specificare una raccolta diversa  
-   Supporta proprietà di distribuzione univoca tra cui:  
   -   Ora attivazione  
   -   Scadenza  
   -   Mostra o nascondi l'esperienza dell'utente finale  
   -   Avvisi separati per questa distribuzione  

Per informazioni dettagliate, vedere [Automatically deploy software updates](automatically-deploy-software-updates.md) (Distribuire automaticamente gli aggiornamenti software)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
