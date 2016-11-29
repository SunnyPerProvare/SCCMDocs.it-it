---
title: Creare elementi di configurazione figlio| System Center Configuration Manager
description: Creare elementi di configurazione figlio in System Center Configuration Manager.Come creare elementi di configurazione figlio in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 977821799dc7323b03bc8c27c59473cd90f70e2a


---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Come creare elementi di configurazione figlio in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli elementi di configurazione figlio in System Center Configuration Manager sono copie di elementi di configurazione che mantengono una relazione con l'elemento di configurazione originale e che quindi ereditano la configurazione originale dall'elemento di configurazione padre.  

Quando si visualizzano le proprietà di un elemento di configurazione figlio nella console di Configuration Manager, non è possibile modificare le impostazioni e gli oggetti ereditati con i relativi criteri di convalida. Tuttavia, è possibile aggiungere e quindi modificare criteri di convalida aggiuntivi per l'elemento di configurazione figlio, al quale è anche possibile aggiungere nuovi oggetti e impostazioni.
Lo scopo della creazione e della modifica di un elemento di configurazione figlio è di solito quello di ottimizzare l'elemento di configurazione originale per soddisfare i requisiti aziendali.  

> [!NOTE]  
>  È possibile creare elementi di configurazione figlio solo da elementi di configurazione del tipo **Windows desktop o server (personalizzato)**.  

## <a name="to-create-a-child-configuration-item"></a>Per creare un elemento di configurazione figlio  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Elementi di configurazione**.  

3.  Nell'elenco **Elementi di configurazione** selezionare l'elemento di configurazione per il quale si vuole creare un elemento di configurazione figlio e quindi nel gruppo **Elemento di configurazione** della scheda **Home** fare clic su **Crea elemento di configurazione figlio**.  

4.  Nella pagina **Generale** della **Creazione guidata dell'elemento di configurazione figlio**è possibile scegliere la revisione specifica dell'elemento di configurazione padre da usare per creare l'elemento figlio. Gli altri passaggi di questa procedura guidata sono identici a quelli eseguiti per creare un elemento di configurazione standard. Per altre informazioni, vedere [Come creare elementi di configurazione personalizzati per computer desktop e server Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Completare la procedura guidata. Il nuovo elemento di configurazione figlio verrà visualizzato nell'elenco **Elementi di configurazione** .  



<!--HONumber=Nov16_HO1-->

