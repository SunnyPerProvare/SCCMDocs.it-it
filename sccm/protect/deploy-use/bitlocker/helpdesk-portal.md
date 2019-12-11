---
title: Sito Web di amministrazione e monitoraggio BitLocker
titleSuffix: Configuration Manager
description: Come utilizzare il sito Web di Administration and Monitoring di BitLocker (portale helpdesk) in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f6ec7cc76066fa4e2cb9ce8bcabe6e4f5b0dfd6
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662629"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Sito Web di amministrazione e monitoraggio BitLocker

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

Il sito Web di Administration and Monitoring di BitLocker è un'interfaccia amministrativa per Crittografia unità BitLocker. Viene anche indicato come portale di help desk. Usare questo sito Web per esaminare i report, ripristinare le unità degli utenti e gestire i TPMs del dispositivo.

[![screenshot del sito Web predefinito di Administration and Monitoring di BitLocker](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Prima di poterlo usare, installare questo componente in un server Web. Per ulteriori informazioni, vedere la pagina relativa alla [configurazione di report e portali BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites).

Accedere al sito Web di Administration and Monitoring tramite l'URL seguente: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> È possibile visualizzare il **report controllo ripristino** nel sito Web di Administration and Monitoring. Aggiungere altri report di Gestione BitLocker al punto di Reporting Services. Per altre informazioni, vedere [visualizzare i report di BitLocker](/configmgr/protect/deploy-use/bitlocker/view-reports).

## <a name="groups"></a>Gruppi

Per accedere ad aree specifiche del sito Web di Administration and Monitoring, è necessario che l'account utente sia in uno dei gruppi seguenti. Creare questi gruppi in Active Directory usando il nome desiderato. Quando si installa il sito Web, è necessario specificare questi nomi di gruppo. Per ulteriori informazioni, vedere la pagina relativa alla [configurazione di report e portali BitLocker](/configmgr/protect/deploy-use/bitlocker/setup-websites).

|Gruppo|Descrizione|
|--- |--- |
|Amministratori help desk BitLocker|Fornisce l'accesso a tutte le aree del sito Web di amministrazione e monitoraggio. Quando si consente a un utente di ripristinare le unità, immettere solo la chiave di ripristino e non il dominio e il nome utente. Se un utente è membro sia di questo gruppo che del gruppo di utenti help desk di BitLocker, le autorizzazioni del gruppo di amministratori sostituiscono le autorizzazioni del gruppo utenti.|
|Utenti help desk di BitLocker|Fornisce l'accesso alle aree **Manage TPM** (Gestisci TPM) e **Drive Recovery** (Ripristino unità) nel sito Web di amministrazione e monitoraggio. Quando si usa una delle due aree, è necessario compilare tutti i campi, inclusi il dominio e il nome dell'account dell'utente. Se un utente è membro sia di questo gruppo che del gruppo help desk Admins di BitLocker, le autorizzazioni del gruppo amministratori sostituiscono le autorizzazioni del gruppo di utenti.|
|Utenti report di BitLocker|Fornisce l'accesso all'area **Reports** nel sito Web di amministrazione e monitoraggio.|

## <a name="manage-tpm"></a>Manage TPM (Gestisci TPM)

Se un utente immette un PIN errato per un numero eccessivo di volte, è possibile che blocchi il TPM. Il numero di volte in cui un utente può immettere un PIN errato prima del blocco del TPM varia in base al produttore. Dall'area **Gestisci TPM** del sito Web di Administration and Monitoring, accedere al sistema dati centralizzato di recupero chiavi.

Per ulteriori informazioni sulla proprietà del TPM, vedere [Configure mbam to escrow the TPM and Store OwnerAuth passwords](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> A partire da Windows 10, versione 1607, Windows non mantiene la password del proprietario del TPM durante il provisioning del TPM.

1. Accedere al sito Web di Administration and Monitoring nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **Gestisci TPM** .

    ![Pagina Gestisci TPM del sito Web di Administration and Monitoring di BitLocker](media/bitlocker-admin-manage-tpm.png)

1. Immettere il nome di dominio completo e il nome del computer.

1. Se necessario, immettere il dominio e il nome utente dell'utente per recuperare il file di password del proprietario del TPM.

1. Scegliere una delle opzioni seguenti per il **motivo della richiesta del file di password del proprietario del TPM**:

    - Reset PIN lockout (Reimposta blocco PIN)
    - Turn on TPM (Attiva TPM)
    - Turn off TPM (Disattiva TPM)
    - (Change TPM password) Modifica password TPM
    - Clear TPM (Cancella TPM)
    - Altro

    Dopo aver **inviato** il modulo, il sito Web restituisce una delle risposte seguenti:

    - Se non riesce a trovare un file di password del proprietario del TPM corrispondente, viene restituito un messaggio di errore.

    - Verrà restituito il file di password del proprietario del TPM per il computer interessato

    Dopo aver recuperato il file di password del proprietario del TPM, il sito Web Visualizza la password del proprietario.

1. Per salvare la password in un file, selezionare **Salva**.

1. Nell'area **Gestisci TPM** selezionare l'opzione **Reimposta blocco TPM** e fornire il file di password del proprietario del TPM.

    Il blocco del TPM viene reimpostato. BitLocker ripristina l'accesso dell'utente al dispositivo.

    > [!IMPORTANT]
    > Non condividere il valore hash TPM o il file di password del proprietario del TPM.

## <a name="drive-recovery"></a>Drive recovery (Ripristino unità)

### <a name="bkmk_recovery"></a> Ripristinare un'unità in modalità di ripristino

Le unità entrano in modalità di ripristino negli scenari seguenti:

- L'utente perde o dimentica il PIN o la password
- Il TPM (Trusted Module Platform) rileva le modifiche apportate al BIOS o ai file di avvio del computer

Per ottenere una password di ripristino, usare l'area **Drive recovery** (Ripristino unità) del sito Web di amministrazione e monitoraggio.

> [!IMPORTANT]
> Le password di ripristino scadono dopo un singolo uso. Nelle unità del sistema operativo e nelle unità dati fisse, viene applicata automaticamente la regola monouso. Nelle unità rimovibili si applica quando si rimuove e si inserisce nuovamente l'unità.

1. Accedere al sito Web di Administration and Monitoring nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **ripristino unità** .

    ![Pagina Ripristino driver del sito Web di Administration and Monitoring di BitLocker](media/bitlocker-admin-drive-recovery.png)

1. Se necessario, immettere il dominio e il nome utente dell'utente per visualizzare le informazioni di ripristino.

1. Per visualizzare un elenco di possibili chiavi di ripristino corrispondenti, immettere le prime otto cifre dell'ID della chiave di ripristino. Per ottenere la chiave di ripristino esatta, immettere l'intero ID della chiave di ripristino.

1. Scegliere una delle seguenti opzioni come **motivo per lo sblocco dell'unità**:

    - Operating system boot order changed (Ordine di avvio del sistema operativo modificato)
    - BIOS changed (BIOS modificato)
    - File del sistema operativo modificati
    - Lost startup key (Chiave di avvio persa)
    - Lost PIN (PIN perso)
    - TPM reset (Reimpostazione TPM)
    - Lost passphrase (Passphrase persa)
    - Lost smartcard (Smart card persa)
    - Altro

    Dopo aver **inviato** il modulo, il sito Web restituisce una delle risposte seguenti:

    - Se l'utente ha più password di ripristino corrispondenti, vengono restituite più corrispondenze possibili.

    - La password di ripristino e il relativo pacchetto per l'utente interessato.

        > [!NOTE]
        > Se si ripristina un'unità danneggiata, l'opzione del pacchetto di ripristino fornisce a BitLocker le informazioni critiche necessarie per il ripristino dell'unità.

    - Se non riesce a trovare una password di ripristino corrispondente, viene restituito un messaggio di errore.

    Una volta recuperata la password di ripristino e il pacchetto di ripristino, il sito Web Visualizza la password di ripristino.

1. Per copiare la password, selezionare **copia chiave**. Per salvare la password di ripristino in un file, selezionare **Salva**.

Per sbloccare l'unità, immettere la password di ripristino o usare il pacchetto di ripristino.

### <a name="bkmk_moved"></a> Ripristinare un'unità spostata

Quando si sposta un'unità in un nuovo computer, poiché il TPM è diverso, BitLocker non accetta il PIN precedente. Per ripristinare l'unità spostata, ottenere l'ID chiave di ripristino per recuperare la password di ripristino.

Per ripristinare un'unità spostata, usare l'area **Drive recovery** (Ripristino unità) del sito Web di amministrazione e monitoraggio.

1. Nel computer con l'unità spostata, avviare il computer in modalità ambiente ripristino Windows (WinRE).

1. In WinRE, BitLocker considera l'unità del sistema operativo spostata come un'unità dati fissa. BitLocker Visualizza l'ID della password di ripristino dell'unità e richiede la password di ripristino.

    > [!NOTE]
    > In alcune situazioni, durante il processo di avvio selezionare **ho dimenticato il pin** se l'opzione è disponibile. Quindi, passare alla modalità di ripristino per visualizzare l'ID della chiave di ripristino.

1. Utilizzare l'ID chiave di ripristino per ottenere la password di ripristino dal sito Web di Administration and Monitoring. Per altre informazioni, vedere [ripristinare un'unità in modalità di ripristino](#bkmk_recovery).

Se l'unità spostata è stata configurata per l'utilizzo di un chip TPM nel computer originale, completare i passaggi seguenti. In caso contrario, il processo di ripristino è terminato.

1. Dopo aver sbloccato l'unità, avviare il computer in modalità WinRE. Aprire un prompt dei comandi in WinRE e usare il comando `manage-bde` per decrittografare l'unità. Questo strumento costituisce l'unico modo per rimuovere la protezione **TPM più PIN** senza il chip TPM originale. Per altre informazioni su questo comando, vedere [Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Al termine, avviare normalmente il computer. Configuration Manager imporrà i criteri di BitLocker per crittografare l'unità con il TPM più PIN del nuovo computer.

### <a name="bkmk_corrupted"></a> Ripristinare un'unità danneggiata

Utilizzare l'ID chiave di ripristino per ottenere un pacchetto di chiavi di ripristino dal sito Web di Administration and Monitoring. Per altre informazioni, vedere [ripristinare un'unità in modalità di ripristino](#bkmk_recovery).

1. Salvare il **pacchetto della chiave di ripristino** nel computer, quindi copiarlo nel computer con l'unità danneggiata.

1. Aprire un prompt dei comandi come amministratore e digitare il comando seguente:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Sostituire i valori seguenti:

    - `<corrupted drive>`: la lettera di unità dell'unità danneggiata, ad esempio `D:`
    - `<fixed drive>`: la lettera di unità di un'unità disco rigido disponibile di dimensioni simili o maggiori rispetto all'unità danneggiata. BitLocker consente di ripristinare e spostare i dati sull'unità danneggiata nell'unità specificata. Tutti i dati in questa unità vengono sovrascritti.
    - `<key package>`: il percorso del pacchetto di chiavi di ripristino
    - `<recovery password>`: la password di ripristino associata

    Ad esempio:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Per altre informazioni su questo comando, vedere [Repair-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Report

Il sito Web di Administration and Monitoring include il **report controllo ripristino**. Altri report sono disponibili dal punto di Configuration Manager Reporting Services. Per altre informazioni, vedere [visualizzare i report di BitLocker](/configmgr/protect/deploy-use/bitlocker/view-reports).

1. Accedere al sito Web di Administration and Monitoring nel Web browser, ad esempio `https://webserver.contoso.com/HelpDesk`.

1. Nel riquadro sinistro selezionare l'area **report** .

1. Nella barra dei menu superiore selezionare il **report controllo ripristino**.

Per ulteriori informazioni su questo report, vedere [report controllo ripristino](/configmgr/protect/deploy-use/bitlocker/view-reports#bkmk-audit)

> [!TIP]
> Per salvare i risultati del report, selezionare **Esporta** sulla barra dei menu **report** .
