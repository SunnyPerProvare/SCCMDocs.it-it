---
title: "Creare supporti per sequenza di attività con System Center Configuration Manager | Microsoft Docs"
description: "È possibile creare supporti per sequenza di attività, ad esempio un CD, per distribuire un sistema operativo in un computer di destinazione nell'ambiente di Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: bd5448d70c2d465347de840cb197d4c33075c90a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Creare supporti per sequenza di attività con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare dei supporti per acquisire un'immagine del sistema operativo da un computer di riferimento o per distribuire un sistema operativo in un computer di destinazione presente nell'ambiente di System Center Configuration Manager. Il supporto creato può essere un set di CD/DVD o un'unità flash USB.  

 In genere, il supporto viene usato per distribuire sistemi operativi nei computer di destinazione che non hanno una connessione di rete o la cui connessione di rete al sito di Configuration Manager ha una larghezza di banda bassa. Tuttavia, il supporto di distribuzione viene usati anche per avviare la distribuzione del sistema operativo al di fuori di un sistema operativo Windows esistente. Questo secondo utilizzo del supporto di distribuzione risulta importante quando nel computer di destinazione non è presente alcun sistema operativo, quando il sistema operativo si trova in uno stato non eseguibile o quando l'utente amministratore desidera ripartire il disco rigido nel computer di destinazione.  

 I supporti di distribuzione includono supporti di avvio, supporti autonomi e supporti pre-installati. Il contenuto dei supporti di distribuzione varia a seconda del tipo di supporto usato. Ad esempio, i supporti autonomi includono la sequenza di attività che distribuisce il sistema operativo mentre altri tipi di supporti recuperano le sequenza di attività dal punto di gestione.  

> [!IMPORTANT]  
>  Per creare un supporto per sequenza di attività è necessario essere un amministratore del computer da cui si esegue la console di Configuration Manager. Se non si è un amministratore, verranno richieste le credenziali di amministratore quando si avvia la Creazione guidata del supporto per la sequenza di attività.  

##  <a name="BKMK_PlanCaptureMedia"></a> Supporto di acquisizione per immagini del sistema operativo  
 Il supporto di acquisizione consente di acquisire un'immagine del sistema operativo da un computer di riferimento. Il supporto di acquisizione contiene l'immagine di avvio che avvia il computer di riferimento e la sequenza di attività che acquisisce l'immagine del sistema operativo. Per altre informazioni sulla creazione di supporti di acquisizione, vedere [Creare supporti di acquisizione con System Center Configuration Manager](create-capture-media.md).  

##  <a name="BKMK_PlanBootableMedia"></a> Distribuzioni del sistema operativo con supporti di avvio  
 Il supporto di avvio contiene solo l'immagine di avvio, i [comandi di preavvio opzionali](../understand/prestart-commands-for-task-sequence-media.md) con i relativi file obbligatori e i file binari di Configuration Manager. All'avvio del computer di destinazione, si connette alla rete e recupera la sequenza di attività, l'immagine del sistema operativo e tutti gli altri contenuti richiesti dalla rete. Poiché la sequenza di attività non è presente sul supporto, è possibile modificare la sequenza di attività o il contenuto senza dover ricreare il supporto.  

> [!IMPORTANT]  
>  I pacchetti nei supporti di avvio non sono crittografati. L'utente amministratore deve adottare misure di protezione appropriate, ad esempio l'aggiunta di una password al supporto, per garantire che il contenuto del pacchetto sia protetto da utenti non autorizzati.  

 Per informazioni su come creare il supporto di avvio, vedere [Creare supporti di avvio](create-bootable-media.md).  

##  <a name="BKMK_PlanPrestagedMedia"></a> Distribuzioni del sistema operativo con supporti pre-installati  
 Il supporto pre-installato consente di pre-installare un supporto di avvio e un'immagine del sistema operativo in un disco rigido prima del processo di provisioning. Il supporto preinstallato è un file WIM (Windows Imaging Format) che può essere installato in un computer bare metal dal produttore o in un centro di gestione temporanea aziendale non connesso all'ambiente di Configuration Manager.  

 Il supporto pre-installato contiene l'immagine di avvio usata per avviare il computer di destinazione e l'immagine del sistema operativo applicata al computer di destinazione. È anche possibile specificare applicazioni, pacchetti e pacchetti driver da includere come parte del supporto pre-installato. La sequenza di attività che distribuisce il sistema operativo non è inclusa nel supporto. Quando si distribuisce una sequenza di attività che usa un supporto pre-installato, il client verifica prima di tutto la presenza di contenuto valido nella cache della sequenza di attività locale. Se non è possibile trovare il contenuto o se il contenuto è stato modificato, il client scarica il contenuto dal punto di distribuzione.  

 Il supporto pre-installato viene applicato al disco rigido di un nuovo computer prima che il computer venga inviato all'utente finale. Quando viene avviato per la prima volta dopo l'applicazione del supporto pre-installato, il computer avvia Windows PE e si connette a un punto di gestione per individuare la sequenza di attività che completa il processo di distribuzione del sistema operativo.  

> [!IMPORTANT]  
>  I pacchetti nei supporti pre-installati non sono crittografati. L'utente amministratore deve adottare misure di protezione appropriate, ad esempio l'aggiunta di una password al supporto, per garantire che il contenuto del pacchetto sia protetto da utenti non autorizzati.  

 Per informazioni su come creare i supporti pre-installati, vedere [Creare supporti pre-installati](create-prestaged-media.md).  

##  <a name="BKMK_PlanStandaloneMedia"></a> Distribuzioni del sistema operativo con supporti autonomi  
 Il supporto autonomo contiene tutti gli elementi necessari per distribuire il sistema operativo. Tra questi anche la sequenza di attività e gli altri contenuti necessari. Poiché tutti gli elementi necessari per distribuire il sistema operativo si trovano nel supporto autonomo, lo spazio sul disco richiesto per il supporto autonomo è notevolmente superiore allo spazio su disco richiesto per altri tipi di supporti.  

 Per informazioni sulla creazione dei supporti autonomi, vedere [Creare supporti autonomi](create-stand-alone-media.md).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Considerazioni sui supporti quando si usano sistemi del sito configurati per HTTPS  
 Quando il punto il gestione e il punto di distribuzione sono configurati per usare la comunicazione HTTPS, è necessario creare un supporto di avvio e un supporto pre-installato in un sito primario e non nel sito di amministrazione centrale. Inoltre, tenere presente quanto segue per stabilire se sia necessario configurare il supporto come dinamico o basato su sito:  

-   Per configurare il supporto come dinamico, tutti i siti primari devono disporre dell'autorità di certificazione radice del sito da cui è stato creato il supporto. È possibile importare la CA radice in tutti i siti primari della gerarchia.  

-   Quando i siti primari presenti nella gerarchia di Configuration Manager usano CA radice diverse è necessario usare un supporto basato su sito in ognuno di essi.  
