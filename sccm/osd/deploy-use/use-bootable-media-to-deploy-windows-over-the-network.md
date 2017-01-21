---
title: Usare i supporti di avvio per distribuire Windows in rete | Microsoft Docs
description: Le distribuzioni dei supporti di avvio in System Center Configuration Manager consentono di distribuire il sistema operativo all&quot;avvio del computer di destinazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usare i supporti di avvio per distribuire Windows in rete con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le distribuzioni dei supporti di avvio in System Center Configuration Manager consentono di distribuire il sistema operativo all'avvio del computer di destinazione. All'avvio del computer di destinazione, viene recuperata la sequenza di attività, l'immagine del sistema operativo e qualsiasi altro contenuto richiesto dalla rete. Poiché tale contenuto non è incluso nel supporto, è possibile aggiornare il contenuto senza dover ricreare il supporto.  

 È possibile distribuire i sistemi operativi in rete usando il multicast negli scenari di distribuzione del sistema operativo seguenti:  

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md)  

 Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi fare riferimento alle sezioni seguenti per usare i supporti di avvio per distribuire il sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
 Quando si usa un supporto di avvio per avviare il processo di distribuzione del sistema operativo, è necessario configurare la distribuzione per rendere disponibile il sistema operativo per il supporto. È possibile eseguire questa configurazione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione.  Per l'impostazione **Rendi disponibile per** , configurare uno degli elementi seguenti:  

-   **Client di Configuration Manager, supporti e PXE**  

-   **Solo supporti e PXE**  

-   **Solo supporti e PXE (nascosto)**  

## <a name="create-the-bootable-media"></a>Creare il supporto di avvio  
 È possibile specificare se il supporto di avvio è un'unità flash USB o un set di CD/DVD. Il computer in cui verrà avviato il supporto deve supportare l'opzione scelta come unità di avvio. Per altre informazioni, vedere [Creare supporti di avvio](create-bootable-media.md).  

##  <a name="a-namebkmkdeploya-install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Installare il sistema operativo da supporti di avvio  
 Inserire il supporto di avvio in un'unità di avvio del computer e quindi accendere il sistema per installare il sistema operativo.  



<!--HONumber=Dec16_HO3-->


