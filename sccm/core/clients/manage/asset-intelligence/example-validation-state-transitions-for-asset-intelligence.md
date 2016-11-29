---
title: Transizioni di esempio dello stato di convalida per Asset Intelligence | System Center Configuration Manager
description: Vedere le transizioni di esempio dello stato di convalida per Asset Intelligence in System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 72b6c4273c2e9f82b8b30501ad44a1e7985e6d86


---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>Transizioni dello stato di convalida di esempio per Asset Intelligence in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli stati di convalida di Asset Intelligence in System Center Configuration Manager non sono statici e possono essere modificati da operazioni di amministrazione eseguite per modificare i dati archiviati nel catalogo di Asset Intelligence. In questo argomento vengono descritti esempi relativi alle possibili transizioni dello stato di convalida.

##  <a name="a-namebkmkuncategorizediscategorizeda-uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a> L'elemento del catalogo senza categoria viene categorizzato dall'utente amministratore  

|**Transizione di stato**|**Descrizione della transizione di stato**|  
|--------------------------|--------------------------------------|  
|**Senza categoria**|Un titolo di software di inventario che non è stato categorizzato in precedenza da System Center Online o che l'utente amministratore ha inserito nel catalogo di Asset Intelligence.|  
|**Senza categoria** a **utentedefinito**|L'elemento senza categoria viene categorizzato dall'utente amministratore.|  

##  <a name="a-namebkmkcategorizedisrecategorizeda-categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> L'elemento del catalogo categorizzato viene categorizzato di nuovo dall'utente amministratore  

|**Transizione di stato**|**Descrizione della transizione di stato**|  
|--------------------------|--------------------------------------|  
|**Convalidato**|L'elemento del catalogo è stato definito dai ricercatori di System Center Online ed è presente nel catalogo di Asset Intelligence.|  
|**Convalidaa** a **Definito da utente**|L'elemento del catalogo convalidato viene categorizzato di nuovo dall'utente amministratore.|  

> [!NOTE]  
>  Dato che le informazioni di categorizzazione ottenute da System Center Online vengono archiviate nel database e non possono essere eliminate, l'utente amministratore può ripristinare la categorizzazione di System Center Online in un secondo momento.  

##  <a name="a-namebkmkuserdefinedisrecategorizeda-user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a> L'elemento del catalogo definito dall'utente è categorizzato di nuovo da System Center Online  

|**Transizione di stato**|**Descrizione della transizione di stato**|  
|--------------------------|--------------------------------------|  
|**Senza categoria**|Nel catalogo di Asset Intelligence viene inserito un titolo software di inventario non categorizzato in precedenza da System Center Online o dall'utente amministratore.|  
|**Definito da utente**|L'elemento senza categoria viene categorizzato dall'utente amministratore.|  
|**Definia da utente** a **Aggiornabile**|Un elemento di catalogo definito dall'utente è stato categorizzato in modo diverso da System Center Online durante i successivi aggiornamenti in blocco del catalogo di Asset Intelligence.<br /><br /> L'utente amministratore può usare la finestra di dialogo **Risoluzione conflitti dettagli software** per decidere se usare le nuove informazioni di categorizzazione o il precedente valore definito dall'utente.|  
|**Aggiornabile** a **Convalidato**|L'utente amministratore usa la finestra di dialogo **Risoluzione conflitti dettagli software** per usare le nuove informazioni di categorizzazione ricevute da System Center Online durante il precedente aggiornamento del catalogo.|  
|Oppure||  
|**Aggiornabile** a **Definito da utente**|L'utente amministratore usa la finestra di dialogo **Risoluzione conflitti dettagli software** per usare il precedente valore definito dall'utente.|  

> [!NOTE]  
>  Dato che le informazioni di categorizzazione ottenute da System Center Online vengono archiviate nel database e non possono essere eliminate, l'utente amministratore può ripristinare la categorizzazione di System Center Online in un secondo momento.  

##  <a name="a-namebkmkuncategorizedissubmitteda-uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a> L'elemento del catalogo senza categoria viene inviato a System Center Online per la categorizzazione  

|**Transizione di stato**|**Descrizione della transizione di stato**|  
|--------------------------|--------------------------------------|  
|**Senza categoria**|Nel database di Asset Intelligence viene inserito un titolo di software di inventario non categorizzato in precedenza da System Center Online o dall'utente amministratore.|  
|**Senza categoria** a **In sospeso**|L'elemento senza categoria viene inviato a System Center Online per la categorizzazione dall'utente amministratore|  
|**In sospeso** a **Convalidato**|L'elemento è categorizzato da System Center Online. L'utente amministratore importa l'elemento nel catalogo di Asset Intelligence tramite un aggiornamento in blocco del catalogo oppure una sincronizzazione del catalogo di Asset Intelligence. Entrambe le operazioni sono disponibili mediante il ruolo del sistema del sito del punto di sincronizzazione di Asset Intelligence.|  

##  <a name="a-namebkmkuserdefinedissubmitteda-user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a> L'elemento del catalogo definito dall'utente viene inviato a System Center Online per la categorizzazione  

|**Transizione di stato**|**Descrizione della transizione di stato**|  
|--------------------------|--------------------------------------|  
|**Senza categoria**|Nel database di Asset Intelligence viene inserito un titolo di software di inventario non categorizzato in precedenza da un utente amministratore o da System Center Online.|  
|**Definito da utente**|L'elemento senza categoria è stato categorizzato.|  
|**Definia da utente** a **In sospeso**|L'elemento definito dall'utente viene inviato a System Center Online per la categorizzazione.|  
|**In sospeso** a **Aggiornabile**|Un elemento di catalogo definito dall'utente è stato categorizzato in modo diverso da System Center Online durante una categorizzazione del catalogo successiva. È possibile usare l'azione **Risolvi conflitto** per decidere se usare le nuove informazioni di categorizzazione o il valore definito dall'utente precedente. Per altre informazioni sulla risoluzione dei conflitti, vedere [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Risolvere i conflitti con dettagli software)|  
|**Aggiornabile** a **Convalidato**|Usare l'azione **Risolvi conflitto** e selezionare le nuove informazioni di categorizzazione ricevute da System Center Online durante l'aggiornamento del catalogo precedente. Per altre informazioni sulla risoluzione dei conflitti, vedere [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Risolvere i conflitti con dettagli software)|  
|Oppure||  
|**Aggiornabile** a **Definito da utente**|Usare l'azione **Risolvi conflitto** e selezionare l'opzione per usare il valore definito dall'utente precedente. Per altre informazioni sulla risoluzione dei conflitti, vedere [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Risolvere i conflitti con dettagli software)|  

> [!NOTE]  
>  Dato che le informazioni di categorizzazione ottenute da System Center Online vengono archiviate nel database e non possono essere eliminate, è possibile ripristinare la categorizzazione di System Center Online in un secondo momento.  



<!--HONumber=Nov16_HO1-->


