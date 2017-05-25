---
title: Installare Updates Publisher | Microsoft Docs
description: Installare System Center Updates Publisher nell&quot;ambiente in uso
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 996766d0bd9ab2a3acb1970414f0ae511d97fbff
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="install-updates-publisher"></a>Installare Updates Publisher

*Si applica a: System Center Updates Publisher*

Usare le informazioni riportate in questo argomento per ottenere, installare e configurare Updates Publisher per l'ambiente in uso.


## <a name="prerequisites-and-limitations"></a>Prerequisiti e limiti
Le sezioni seguenti riportano requisiti dettagliati per l'installazione e l'uso di Updates Publisher, nonché informazioni sulle limitazioni o i problemi noti.

### <a name="operating-systems"></a>Sistemi operativi
Installare ed eseguire Updates Publisher su edizioni a 64 bit dei sistemi operativi seguenti. Non sono presenti requisiti riguardanti aggiornamenti cumulativi minimi o Service Pack.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Prerequisiti
Di seguito sono riportati i requisiti per il computer che esegue Updates Publisher.

-   **Sistema operativo a 64 bit**: il sistema in cui viene installato Updates Publisher deve eseguire un sistema operativo a 64 bit.
-   **WSUS 4.0 o versione successiva**:
    -   per soddisfare questo requisito, in Windows Server installare la console di amministrazione predefinita.
    -   Per Windows 10 e Windows 8.1, installare [Strumenti di amministrazione remota del server per sistemi operativi Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Questo consente di installare il supporto necessario per l'uso di Updates Publisher (*API e cmdlet PowerShell* e *Console di gestione interfaccia utente*).
-   **Autorizzazioni**:
    -   Installazione: Amministratore locale
    -   Maggior parte delle operazioni: utente locale
    -   Per la pubblicazione o per operazioni che coinvolgono WSUS: membro del gruppo WSUS Administrators nel server WSUS.

### <a name="supported-languages"></a>Lingue supportate
Updates Publisher è disponibile solo in lingua inglese, ma può gestire aggiornamenti per altre lingue. Il supporto per le lingue dipende dall'attività, ad esempio pubblicazione, creazione o modifica di aggiornamenti.

Durante l'esportazione o la pubblicazione di aggiornamenti, Updates Publisher consente di visualizzare il titolo e la descrizione dell'aggiornamento software in base alle impostazioni locali del computer in cui è installato.

Si supponga, ad esempio, di creare un aggiornamento software con un titolo in inglese e spagnolo.

-   Se si crea l'aggiornamento in un computer con impostazioni locali configurate per l'inglese, per impostazione predefinita il titolo e la descrizione verranno visualizzati in inglese.
-   Se in un secondo tempo l'aggiornamento viene esportato o pubblicato in un computer con impostazioni locali configurate per lo spagnolo, in tale computer il titolo e la descrizione verranno visualizzati in spagnolo.

### <a name="publishing"></a>Pubblicazione
Quando si pubblica un aggiornamento software, è possibile specificare la lingua del relativo file binario. È anche possibile specificare che il file binario è indipendente dalla lingua. Sono supportate le lingue seguenti:

-   Arabo
-   Cinese (Hong Kong R.A.S)
-   Cinese (tradizionale)
-   Cinese (semplificato)
-   Ceco
-   Danese
-   Olandese
-   Inglese
-   Finlandese
-   Francese
-   Tedesco
-   Greco
-   Ebraico
-   Ungherese
-   Italiano
-   Giapponese
-   Coreano
-   Norvegese
-   Polacco
-   Portoghese
-   Portoghese (Brasile)
-   Russo
-   Spagnolo
-   Svedese
-   Turco

### <a name="software-update-titles-and-descriptions"></a>Descrizioni e titoli degli aggiornamenti software
Per i titoli e le descrizioni degli aggiornamenti software sono supportate le lingue seguenti.

-   Cinese (tradizionale)
-   Cinese (semplificato)
-   Inglese
-   Francese
-   Tedesco
-   Italiano
-   Giapponese
-   Coreano
-   Portoghese (Brasile)
-   Russo
-   Spagnolo



## <a name="install-updates-publisher"></a>Installare Updates Publisher
Per installare System Center Updates Publisher, scaricare il file **UpdatesPubliser.msi** dall'[Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=847967).

Per installare Updates Publisher, eseguire il file **UpdatesPublisher.msi** in un computer che soddisfa i *prerequisiti*. Il programma di installazione crea la cartella *&lt;percorso&gt;\Programmi\Microsoft\UpdatesPublisher* in cui sono presenti i file necessari per l'esecuzione di Updates Publisher.

Poiché questa cartella contiene tutti i file necessari per l'uso di Updates Publisher, è possibile copiarla con il relativo contenuto in un nuovo percorso o computer e quindi usare Updates Publisher da tale posizione. Per eseguire Updates Publisher, è tuttavia necessario che la nuova posizione o computer soddisfi i prerequisiti.

Dopo aver completato l'installazione, eseguire il file **UpdatesPublisher.exe** dalla cartella *UpdatesPublisher* per avviare Updates Publisher.

## <a name="next-steps"></a>Passaggi successivi
 Dopo aver completato l'installazione, è consigliabile [configurare le opzioni](/tools/updates-publisher-options) per Updates Publisher. Per poter usare alcune funzionalità di Updates Publisher, è prima necessario configurare determinate opzioni.

 Se, tuttavia, si vogliono usare le impostazioni predefinite e non si pianifica la distribuzione di aggiornamenti in un server di aggiornamento o in dispositivi gestiti, è possibile passare direttamente alla [gestione dei cataloghi di aggiornamenti software](/tools/updates-publisher-catalogs) o alla [creazione di aggiornamenti software](/tools/create-updates-with-updates-publisher) e creare cataloghi di aggiornamento personalizzati.
