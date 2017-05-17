---
title: Aggiungere aggiornamenti a un gruppo di aggiornamento - Configuration Manager | Microsoft Docs
description: Aggiungere gli aggiornamenti software a un gruppo di aggiornamento software dell&quot;ambiente, manualmente o automaticamente.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
ms.translationtype: Human Translation
ms.sourcegitcommit: 4e44e2b8f6baf020c3b7742bafd607082ffacaa4
ms.openlocfilehash: 02e30ba48f3564fa8a31f21793c145054e02e002
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---

# <a name="add-software-updates-to-an-update-group"></a>Aggiungere gli aggiornamenti software a un gruppo di aggiornamento  

*Si applica a: System Center Configuration Manager (Current Branch)*

 I gruppi di aggiornamento software forniscono un metodo efficace per organizzare gli aggiornamenti software nel relativo ambiente. È possibile aggiungere manualmente aggiornamenti software a un gruppo di aggiornamenti software oppure farlo automaticamente usando un'ADR. È anche possibile distribuire manualmente un gruppo di aggiornamenti software oppure farlo automaticamente usando un'ADR. Dopo aver distribuito un gruppo di aggiornamento software, è possibile aggiungere nuovi aggiornamenti software al gruppo e Configuration Manager li distribuirà automaticamente. Usare le procedure seguenti per aggiungere gli aggiornamenti software a un gruppo di aggiornamento software nuovo o esistente.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Per aggiungere gli aggiornamenti software a un nuovo gruppo di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software, espandere **Aggiornamenti software**, quindi fare clic su **Tutti gli aggiornamenti software**.  

3.  Selezionare gli aggiornamenti software che devono essere aggiunti al nuovo gruppo di aggiornamento software.  

4.  Nella scheda **Home** , nel gruppo **Aggiorna** , fare clic su **Crea gruppo di aggiornamento software**.  

5.  Specificare il nome per il gruppo di aggiornamento software e fornire una descrizione facoltativa. Usare un nome e una descrizione che forniscano informazioni sufficienti per determinare il tipo di aggiornamenti software che si trovano nel gruppo di aggiornamento software. Per continuare, fare clic su **Crea**.  

6.  Fare clic su **Gruppi di aggiornamenti software** per visualizzare il nuovo gruppo di aggiornamento software.  

7.  Selezionare il gruppo di aggiornamento software, quindi nella scheda **Home** , nel gruppo **Aggiorna** , fare clic su **Mostra membri** per visualizzare un elenco degli aggiornamenti software inclusi nel gruppo.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Per aggiungere gli aggiornamenti software a un gruppo di aggiornamento software esistente  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software, espandere **Aggiornamenti software**, quindi fare clic su **Tutti gli aggiornamenti software**.  

3.  Selezionare gli aggiornamenti software che si desidera aggiungere al nuovo gruppo di aggiornamento software.  

    > [!NOTE]  
    >  Nel nodo **Tutti gli aggiornamenti software**, per impostazione predefinita Configuration Manager visualizza solo gli aggiornamenti software con classificazione **Errore critico** e **Sicurezza** e che sono stati rilasciati negli ultimi 30 giorni.  

4.  Nella scheda **Home** del gruppo **Aggiorna** , fare clic su **Modifica appartenenza**.  

5.  Selezionare il gruppo di aggiornamento software in cui si desidera aggiungere gli aggiornamenti software.  

6.  Fare clic sul nodo **Gruppi di aggiornamenti software** per visualizzare il gruppo di aggiornamento software.  

7.  Selezionare il gruppo di aggiornamento software, quindi nella scheda **Home** del gruppo **Aggiorna** , fare clic su **Mostra membri** per visualizzare un elenco degli aggiornamenti software inclusi nel gruppo.  

