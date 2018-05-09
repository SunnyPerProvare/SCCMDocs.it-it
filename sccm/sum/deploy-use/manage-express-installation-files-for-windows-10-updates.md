---
title: Gestire i file di installazione rapida per gli aggiornamenti di Windows 10
titleSuffix: Configuration Manager
description: Configuration Manager supporta l'installazione rapida dei file per Windows 10, garantendo download più contenuti e tempi di installazione più rapidi per i client.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/24/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4ca7a6c37137e266d719b76532b4131a6c43d4de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gestire i file di installazione rapida per gli aggiornamenti di Windows 10
A partire dalla versione 1702, Configuration Manager supporta i file di installazione rapida per gli aggiornamenti di Windows 10. Se si usa una versione supportata di Windows 10, è possibile usare le impostazioni client di Configuration Manager per configurare il client in modo da scaricare solo le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento del mese precedente. Senza i file di installazione rapida, i client di Configuration Manager scaricano ogni mese l'aggiornamento cumulativo completo di Windows 10, inclusi tutti gli aggiornamenti dei mesi precedenti. Grazie ai file di installazione rapida sono possibili download più brevi e tempi di installazione più rapidi per i client.

> [!IMPORTANT]
> Anche se le impostazioni per il supporto dei file di installazione rapida sono disponibili in Configuration Manager versione 1702, il supporto per il sistema operativo client è disponibile in Windows 10 versione 1607 con un aggiornamento dell'agente Windows Update. Questo aggiornamento è incluso negli aggiornamenti rilasciati in data 11 aprile 2017 (Patch Tuesday). Per altre informazioni su questi aggiornamenti, vedere l'[articolo del supporto tecnico 4015217](http://support.microsoft.com/kb/4015217). Gli aggiornamenti futuri sfrutteranno i file di installazione rapida per download di dimensioni più contenute. Windows 10 versione 1607 senza l'aggiornamento e le versioni precedenti di Windows non supportano i file di installazione rapida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>Per abilitare il download dei file di installazione rapida per gli aggiornamenti di Windows 10
Per avviare la sincronizzazione dei metadati per i file di installazione rapida di Windows 10 è necessario abilitarla nelle proprietà del punto di aggiornamento software.
1.  Nella console di Configuration Manager passare a **Amministrazione** > **Configurazione del sito** > **Siti**.
2.  Selezionare il sito di amministrazione centrale o il sito primario autonomo.
3.  Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**. Nella scheda **File di aggiornamento** selezionare **Scarica i file completi per tutti gli aggiornamenti approvati e i file dell'installazione rapida per Windows 10**.

> [!NOTE]    
> Non è possibile configurare il componente del punto di aggiornamento software in modo da scaricare solo gli aggiornamenti rapidi.  Il download dei file dell'installazione rapida andrà ad aggiungersi a quello dei file completi, aumentando pertanto la quantità di contenuto distribuito e archiviato nei punti di distribuzione.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Per abilitare il supporto del download e dell'installazione di file di installazione rapida per i client
Per abilitare il supporto dei file di installazione rapida per i client, è necessario abilitare i file di installazione rapida nella sezione Aggiornamenti software delle impostazioni del client. Questa operazione crea un nuovo listener HTTP che attende le richieste di download dei file di installazione rapida sulla porta specificata.

> [!NOTE]    
> Si tratta di una porta locale usata dai client per restare in ascolto delle richieste da Ottimizzazione recapito o dal Servizio trasferimento intelligente in background (BITS) per scaricare il contenuto rapido dal punto di distribuzione. Non è necessario aprire la porta nel firewall perché tutto il traffico è nel computer locale.

Dopo aver distribuito le impostazioni client per abilitare questa funzionalità nel client, la funzionalità tenterà di scaricare le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Nei client deve essere in esecuzione una versione di Windows 10 che supporti i file di installazione rapida.
1.  Abilitare il supporto per i file di installazione rapida nelle proprietà del componente del punto di aggiornamento software (procedura precedente).
2.  Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client**.
3.  Selezionare le impostazioni client appropriate e quindi nella scheda **Home** fare clic su **Proprietà**.
4.  Selezionare la pagina **Aggiornamenti software** , selezionare **Sì** nell'impostazione **Abilita l'installazione di aggiornamenti rapidi nei client** e configurare la porta usata dal listener HTTP nel client per l'impostazione **Porta usata per scaricare contenuto per gli aggiornamenti rapidi**.
