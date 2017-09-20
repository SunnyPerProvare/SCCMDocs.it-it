---
title: Creare ed eseguire script con Configuration Manager | Microsoft Docs
description: Creare ed eseguire script in dispositivi client con Configuration Manager.
ms.custom: na
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: e6b29cd85504742e8638a55db2f6c4ecc8ab3e55
ms.sourcegitcommit: 5ca89204716750eaaceb01bba40b35b85c7122ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/18/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creare ed eseguire script di PowerShell dalla console di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In Configuration Manager, oltre a usare pacchetti e programmi per la distribuzione di script, è possibile usare le funzionalità che seguono per eseguire le azioni seguenti:

- Importare gli script di PowerShell in Configuration Manager
- Modificare gli script dalla console di Configuration Manager (solo per script non firmati)
- Contrassegnare gli script come Approvato o Rifiutato per migliorare la sicurezza
- Eseguire gli script nelle raccolte di PC client Windows e nei PC Windows gestiti in locale. Gli script non vengono distribuiti ma eseguiti quasi immediatamente nei dispositivi client.
- Esaminare i risultati restituiti dallo script nella console di Configuration Manager.

>[!TIP]
>In questa versione di Configuration Manager, gli script sono in una versione non definitiva. Per abilitare gli script, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Prerequisiti

Per eseguire script PowerShell, nel client deve essere in esecuzione PowerShell versione 3.0 o successiva. Se tuttavia lo script eseguito contiene funzionalità di una versione successiva di PowerShell, il client in cui viene eseguito lo script deve avere in esecuzione tale versione.

Per eseguire gli script, i client Configuration Manager devono avere in esecuzione il client della versione 1706 o successiva.

Per usare gli script, l'utente deve essere membro del ruolo di sicurezza appropriato di Configuration Manager.

- Per importare e creare script: l'account deve avere autorizzazioni di **creazione** per **script SMS** nel ruolo di sicurezza **Amministratore completo**.
- Per approvare o rifiutare script: l'account deve avere autorizzazioni di **approvazione** per **script SMS** nel ruolo di sicurezza **Amministratore completo**.
- Per eseguire script: l'account deve avere autorizzazioni di** esecuzione script** per **Raccolte** nel ruolo di sicurezza **Gestione impostazioni di conformità**.

Per altre informazioni sui ruoli di sicurezza di Configuration Manager, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](/sccm/core/understand/fundamentals-of-role-based-administration).

Per impostazione predefinita, gli utenti non possono approvare uno script da loro stessi creato. Poiché gli script sono potenti e versatili e possono essere distribuiti in più dispositivi, è possibile separare i ruoli tra la persona che crea lo script e la persona che lo approva. Questi ruoli garantiscono un livello aggiuntivo di sicurezza, impedendo l'esecuzione di uno script senza supervisione. Per semplificare le attività di test, è possibile disattivare questa approvazione secondaria.

## <a name="allow-users-to-approve-their-own-scripts"></a>Consentire agli utenti di approvare i propri script

1. Nella console di Configuration Manager fare clic su **Amministrazione**.
2. Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.
3. Nell'elenco dei siti selezionare il sito e quindi scegliere la scheda **Home** nel gruppo **Siti** e fare clic su **Impostazioni gerarchia**.
4. Nella scheda **Generale** della finestra di dialogo **Proprietà delle impostazioni di gerarchia** deselezionare la casella di controllo **Do not allow script authors to approve their own scripts** (Non consentire agli autori di script di approvare i propri script).

## <a name="import-and-edit-a-script"></a>Importare e modificare uno script

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea gruppo**.
4. Nella pagina **Script** della procedura guidata **Crea script** configurare le impostazioni seguenti:
    - In **Nome script** inserire il nome dello script. Anche se è possibile creare più script con lo stesso nome, l'uso di nomi duplicati rende più difficile individuare lo script necessario nella console di Configuration Manager.
    - **Lingua script**: attualmente sono supportati solo script di PowerShell.
    - **Importa**: importare uno script di PowerShell nella console. Lo script viene visualizzato nel campo **Script**.
    - **Cancella**: rimuove lo script corrente dal campo Script.
    - **Script**: visualizza lo script attualmente importato. È possibile modificare lo script in questo campo in base alle esigenze.
5. Completare la procedura guidata. Il nuovo script viene visualizzato nell'elenco **Script** con stato **In attesa di approvazione **. Prima di poter eseguire questo script nei dispositivi client, è necessario approvarlo.

### <a name="script-examples"></a>Esempi di script

Di seguito sono riportati alcuni esempi che illustrano gli script che è possibile usare con questa funzionalità.

#### <a name="create-a-folder"></a>Crea una cartella

*New-Item "c:\scripts" -type folder name*


#### <a name="create-a-file"></a>Creare un file

*New-Item c:\scripts\new_file.txt -type file name*


## <a name="approve-or-deny-a-script"></a>Approvare o rifiutare uno script

Prima di eseguire uno script, deve essere approvato. Per approvare uno script:

1. Nella console di Configuration Manager fare clic su **Raccolta software**.
2. Nell'area di lavoro **Raccolta software** fare clic su **Script**.
3. Nell'elenco **Script** scegliere lo script che si desidera approvare o rifiutare e quindi scegliere la scheda **Home** nel gruppo **Script**, quindi fare clic su **Approve/Deny** (Approva/Rifiuta).
4. Nella finestra di dialogo **Approva o rifiuta script** scegliere **Approva** o **Rifiuta** e, facoltativamente, immettere un commento sulla decisione. Se si rifiuta uno script, questo non può essere eseguito sui dispositivi client.
5. Completare la procedura guidata. Nell'elenco **Script** la colonna **Stato dell'approvazione** cambia a seconda dell'azione eseguita.

## <a name="run-a-script"></a>Esegui uno script
Dopo che uno script è stato approvato, può essere eseguito su una raccolta a scelta dell'utente.

1. Nella console di Configuration Manager fare clic su **Asset e conformità**.
2. Nell'area di lavoro Asset e conformità fare clic su **Raccolte dispositivi**.
3. Nell'elenco **Raccolte dispositivi** fare clic sulla raccolta di dispositivi in cui si desidera eseguire lo script.
4. Nella scheda **Home** nel gruppo **Tutti i sistemi** fare clic su **Esegui script**.
5. Nella pagina **Script** della procedura guidata **Esegui Script** scegliere uno script dall'elenco. Vengono visualizzati solo gli script approvati.
6. Fare clic su **Avanti** e completare la procedura guidata.

>[!IMPORTANT]
>All'esecuzione dello script viene assegnato un periodo di un'ora. Se lo script non viene eseguito in questo periodo di tempo, ad esempio se il PC è spento, è necessario eseguirlo nuovamente.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver eseguito uno script sui dispositivi client, è possibile usare questa procedura per monitorare la riuscita dell'operazione.

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.
2. Nell'area di lavoro **Monitoraggio** fare clic su **Stato script**.
3. Nell'elenco **Stato script** sono visualizzati i risultati per ogni script eseguito nei dispositivi client. Un codice di uscita dello script uguale a **0** indica in genere che lo script è stato eseguito correttamente.
