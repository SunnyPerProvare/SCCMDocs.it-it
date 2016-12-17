---
title: Installare un sito usando il supporto di base della versione 1606 | System Center Configuration Manager
description: Informazioni sull'uso del supporto di base della versione 1606 per installare o aggiornare siti per System Center Configuration Manager.
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e97fbcdc21022e98b4cbdb198273dfe544a561f
ms.openlocfilehash: 3df46a00f2208ffa687c8c99ce610266e206eef0


---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Eseguire installazioni e aggiornamenti con il supporto di base della versione 1606 per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

Usare questo argomento per informazioni sull'esecuzione dell'installazione di Configuration Manager quando si usa il supporto di base della versione 1606 da Microsoft System Center 2016 o System Center Configuration Manager (Current Branch e Long-Term Servicing Branch 1606). È possibile usare questo supporto per installare un nuovo sito o per eseguire l'aggiornamento da System Center Configuration Manager 2012 con Service Pack 2 o da System Center Configuration Manager 2012 R2 con Service Pack 1. Durante l'installazione, è possibile scegliere di installare Current Branch o Long-Term Servicing Branch (LTSB).

Quando si usa il supporto di base della versione 1606, il sito che si installa o a cui si esegue l'aggiornamento è:
- **Un sito Current Branch** equivalente a un sito installato in precedenza con il supporto di base della versione 1511 e quindi aggiornato alla versione 1606 con l'hotfix rollup 1606 (KB3186654).
-   **Un sito LTSB** equivalente al sito Current Branch che esegue la versione 1606 con l'hotfix rollup 1606 (KB3186654). Il supporto di base include già l'hotfix rollup.  Tuttavia, LTSB non supporta tutte le funzionalità e tutte le caratteristiche disponibili con Current Branch, come descritto in dettaglio in [Introduzione a Long-Term Servicing Branch di System Center Configuration Manager](introduction-to-the-ltsb.md).

Se non si ha familiarità con i diversi rami di System Center Configuration Manager, vedere [Which branch of Configuration Manager should I use](which-branch-should-i-use.md) (Scelta del ramo di Configuration Manager da usare).


## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Modifiche all'installazione con il supporto di base della versione 1606
Il supporto di base della versione 1606 introduce nel programma di installazione per Configuration Manager le modifiche seguenti.

### <a name="branch-and-edition"></a>Ramo ed edizione
Quando si esegue il programma di installazione, viene ora visualizzata una pagina di gestione licenze in cui è possibile selezionare il ramo di Configuration Manager da installare. È possibile scegliere di installare con licenza Current Branch o LTSB oppure è possibile scegliere una copia di valutazione di Current Branch come installazione senza licenza.

Per altre informazioni, vedere [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Scadenza di Software Assurance
Durante l'installazione, è possibile immettere la **data di scadenza di Software Assurance**. Questo è un valore facoltativo, che è possibile specificare come utile promemoria.

> [!NOTE]
> Microsoft non convalida la data di scadenza immessa e non userà tale data per la convalida della licenza.  È possibile invece usarla come promemoria della data di scadenza. Configuration Manager infatti verifica periodicamente online la disponibilità di nuovi aggiornamenti software. Per usufruire di questi aggiornamenti aggiuntivi è necessario che lo stato della licenza di Software Assurance sia regolare.    

- È possibile specificare il valore nella pagina **Codice Product Key** dell'installazione guidata quando si esegue il programma di installazione dal supporto di base di System Center Configuration Manager versione 1606
- È anche possibile specificare la data nella scheda **Gestione licenze** di **Proprietà delle impostazioni di gerarchia** nella console di Configuration Manager

Per altre informazioni, vedere *Contratti Software Assurance* in [Licenze e rami per System Center Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configurazioni aggiuntive pre-aggiornamento
Prima di avviare un aggiornamento di System Center Configuration Manager 2012 a LTSB, è necessario eseguire la procedura aggiuntiva seguente nell'ambito dell'elenco di controllo pre-aggiornamento.  
Disinstallare i ruoli del sistema del sito non supportati da LTSB:
- Punto di sincronizzazione di Asset Intelligence
- Connettore Microsoft Intune
- Punti di distribuzione basati su cloud

Per altre informazioni, vedere [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) (Eseguire l'aggiornamento a System Center Configuration Manager).


### <a name="new-scripted-install-options"></a>Nuove opzioni di installazione tramite script
Il supporto di base della versione 1606 supporta una nuova chiave di file di script di installazione automatica per le installazioni tramite script di un nuovo sito di livello superiore. Ciò vale per l'installazione di un nuovo sito primario autonomo o per l'aggiunta di un sito di amministrazione centrale nell'ambito di uno scenario di espansione del sito.

Quando si usa uno script automatico per installare un ramo con licenza, è necessario aggiungere la sezione, i nomi delle chiavi e valori seguenti nella sezione Opzioni dello script. Non è necessario usare questi valori allo script per l'installazione di una copia di valutazione Current Branch.  

 **SABranchOptions**
-   **Nome chiave: SSActive**
  - Valori: 0 o 1  
  - Dettagli: 0 installa una copia di valutazione senza licenza di Current Branch, 1 installa una versione con licenza.   

- **CurrentBranch**
  - Valori: 0 o 1  
  - Dettagli: 0 installa Long-Term Servicing Branch, 1 installa Current Branch.  

Ad esempio, per installare una versione con licenza di Current Branch si usa:

  **Nome chiave: SABranchOptions**
   -    **SSActive = 1**
   - **CurrentBranch = 1**
 

> [!IMPORTANT]  
> **SABranchOptions** funziona solo con il programma di installazione del supporto di base. Non è applicabile quando si esegue il programma di installazione dalla cartella CD.Latest di un sito installato in precedenza tramite il supporto di base della versione 1606.
>
> **SABranchOptions** non si applica agli aggiornamenti tramite script da System Center Configuration Manager 2012 e installa sempre Current Branch.

Per altre informazioni, vedere [Use a command line to install System Center Configuration Manager sites](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites) (Installare siti di System Center Configuration Manager dalla riga di comando).


## <a name="install-a-new-site"></a>Installare un nuovo sito
Quando si usa il supporto di base della versione 1606 per installare un nuovo sito di uno dei due rami, usare le procedure di pianificazione, preparazione e installazione del sito documentate nell'argomento [Installare i siti di System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites), con l'aggiunta delle considerazioni seguenti per l'installazione:

- Durante l'installazione è necessario scegliere il ramo di Configuration Manager che si vuole installare specificando i dettagli del contratto Software Assurance.
-   Nuove opzioni di installazione tramite script

## <a name="expand-a-stand-alone-primary-site"></a>Espandere un sito primario autonomo
È possibile espandere un sito primario autonomo in cui è in esecuzione LTSB.  Il processo non è diverso rispetto a quello usato per un sito di Current Branch, con un'avvertenza:

- Quando si installa il nuovo sito di amministrazione centrale è necessario usare il programma di installazione dal supporto originale usato per installare il sito di LTSB. L'esecuzione del programma di installazione dalla cartella CD.Latest non è supportata per questo scenario.

Per altre informazioni sull'espansione di un sito, vedere *Expand a stand-alone primary site*(Espandere un sito primario autonomo) in [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)(Usare l'installazione guidata per installare i siti).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Eseguire l'aggiornamento da System Center Configuration Manager 2012
Quando si esegue l'aggiornamento da System Center Configuration Manager 2012 usare le attività di pianificazione e preparazione del sito e le procedure documentate nell'argomento [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) (Eseguire l'aggiornamento a System Center Configuration Manager), ma con le modifiche seguenti:

**Aggiornamento a Current Branch:**
- Durante l'installazione è necessario scegliere Current Branch, specificando i dettagli del contratto Software Assurance
-   Nuove opzioni di installazione tramite script

**Aggiornamento a LTSB:**  
- Passaggi aggiuntivi da seguire nell'elenco di controllo pre-aggiornamento
- Durante l'installazione è necessario scegliere LTSB, specificando i dettagli del contratto Software Assurance
- È possibile solo aggiornare un sito che esegue System Center Configuration Manager 2012 con Service Pack 2 o System Center Configuration Manager 2012 R2 con Service Pack 1

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Percorsi di aggiornamento sul posto per il supporto di base della versione 1606
È possibile usare il supporto di base della versione 1606 per aggiornare a una versione con licenza di System Center Configuration Manager i prodotti seguenti:
- System Center Configuration Manager 2012 con Service Pack 2
- System Center Configuration Manager 2012 R2 con Service Pack 1

È anche possibile usare questo supporto per aggiornare una versione di valutazione senza licenza di Current Branch a una versione con licenza completa di Current Branch.

Questo supporto non supporta l'aggiornamento di:
- Altre versioni di System Center Configuration Manager 2012
- Configuration Manager 2007 o versioni precedenti
- Installazione di una versione finale candidata di System Center Configuration Manager

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Informazioni sulla cartella CD.Latest e su LTSB
Di seguito sono riportate alcune avvertenze all'uso del supporto che Configuration Manager crea nella cartella CD.Latest nel server del sito. Queste avvertenze si applicano a siti che eseguono LTSB. Il supporto nella cartella CD.Latest è supportato per:
- Ripristino del sito
- Manutenzione del sito
- Installazione di siti primari figlio aggiuntivi

Il supporto nella cartella CD.Latest non è supportato per:  
- Installazione di un sito di amministrazione centrale nell'ambito di uno scenario di espansione del sito.

Per altre informazioni, vedere [la cartella CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Backup, ripristino e manutenzione del sito per LTSB
Per eseguire il backup e il ripristino o eseguire la manutenzione di un sito che esegue LTSB, seguire le linee guida e le procedure in [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery) (Backup e ripristino per System Center Configuration Manager).  

Usare il programma di installazione di Configuration Manager della cartella CD.Latest del backup del sito LTSB.



<!--HONumber=Nov16_HO1-->

