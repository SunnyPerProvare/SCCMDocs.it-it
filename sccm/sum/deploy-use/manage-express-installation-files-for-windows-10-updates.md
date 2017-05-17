---
title: Gestire i file di installazione rapida per gli aggiornamenti di Windows 10 | Microsoft Docs
description: "Configuration Manager supporta l&quot;installazione rapida dei file per Windows 10, garantendo download più contenuti e tempi di installazione più rapidi per i client."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.translationtype: Human Translation
ms.sourcegitcommit: d7b13f3dea5a3ae413ca6b8150ec24e1632a4d4d
ms.openlocfilehash: fcdcbcde61402b47871d51deba32d23867a78370
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---

## <a name="manage-express-installation-files-for-windows-10-updates"></a>Gestire i file di installazione rapida per gli aggiornamenti di Windows 10
A partire dalla versione 1702, Configuration Manager supporta i file di installazione rapida per gli aggiornamenti di Windows 10. Se si usa una versione supportata di Windows 10, è possibile usare le impostazioni di Configuration Manager per scaricare solo le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Senza i file di installazione rapida, Configuration Manager scarica ogni mese l'aggiornamento cumulativo completo di Windows 10, inclusi tutti gli aggiornamenti dei mesi precedenti. Grazie ai file di installazione rapida sono possibili download più brevi e tempi di installazione più rapidi per i client.

> [!IMPORTANT]
> Anche se le impostazioni per il supporto dei file di installazione rapida sono disponibili in Configuration Manager versione 1702, il supporto per il sistema operativo client è disponibile in Windows 10 versione 1607 con un aggiornamento dell'agente Windows Update. Questo aggiornamento è incluso negli aggiornamenti rilasciati in data 11 aprile 2017 (Patch Tuesday). Per altre informazioni su questi aggiornamenti, vedere l'[articolo del supporto tecnico 4015217](http://support.microsoft.com/kb/4015217). Gli aggiornamenti futuri sfrutteranno i file di installazione rapida per download di dimensioni più contenute. Windows 10 versione 1607 senza l'aggiornamento e le versioni precedenti di Windows non supportano i file di installazione rapida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Per abilitare il download dei file di installazione rapida per gli aggiornamenti di Windows 10 nel server
Per avviare la sincronizzazione dei metadati per i file di installazione rapida di Windows 10 è necessario abilitarla nelle proprietà del punto di aggiornamento software.
1.    Nella console di Configuration Manager passare a **Amministrazione** > **Configurazione del sito** > **Siti**.
2.    Selezionare il sito di amministrazione centrale o il sito primario autonomo.
3.    Nel gruppo **Impostazioni** della scheda **Home** fare clic su **Configura componenti sito**, quindi fare clic su **Punto di aggiornamento software**. Nella scheda **File di aggiornamento** selezionare **Download full files for all approved updates and express installation files for Windows 10** (Download di file completi per tutti gli aggiornamenti approvati e i file di installazione rapida per Windows 10).

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Per abilitare il supporto del download e dell'installazione di file di installazione rapida per i client
Per abilitare il supporto dei file di installazione rapida per i client, è necessario abilitare i file di installazione rapida nei client nella sezione Aggiornamenti rapidi delle impostazioni del client. Questa operazione crea un nuovo listener HTTP che attende le richieste di download dei file di installazione rapida sulla porta specificata. Dopo aver distribuito le impostazioni client per abilitare questa funzionalità nel client, la funzionalità tenterà di scaricare le differenze tra l'aggiornamento cumulativo di Windows 10 del mese corrente e l'aggiornamento cumulativo del mese precedente. Nei client deve essere in esecuzione una versione di Windows 10 che supporti i file di installazione rapida.
1.    Abilitare il supporto per i file di installazione rapida nelle proprietà del componente del punto di aggiornamento software (procedura precedente).
2.    Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client**.
3.    Selezionare le impostazioni client appropriate e quindi nella scheda **Home** fare clic su **Proprietà**.
4.    Selezionare la pagina **Aggiornamenti software**, selezionare **Sì** nell'impostazione **Abilita l'installazione di aggiornamenti rapidi nei client** e configurare la porta usata dal listener HTTP nel client per l'impostazione **Porta usata per scaricare contenuto per gli aggiornamenti rapidi**.

