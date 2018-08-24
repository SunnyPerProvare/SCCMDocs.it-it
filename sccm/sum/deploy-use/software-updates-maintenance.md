---
title: Manutenzione degli aggiornamenti software
titleSuffix: Configuration Manager
description: Per gestire gli aggiornamenti in Configuration Manager, è possibile pianificare l'attività di pulizia di WSUS oppure eseguirla manualmente.
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a44643870234a08169db1d55cc834e4ca5fcbb5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385491"
---
# <a name="software-updates-maintenance"></a>Manutenzione degli aggiornamenti software

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile pianificare ed eseguire attività di pulizia WSUS nella console di Configuration Manager, dalle proprietà del componente del punto di aggiornamento software. Quando si sceglie di eseguire l'attività di pulizia WSUS, questa verrà eseguita dopo la successiva sincronizzazione degli aggiornamenti software.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Per pianificare ed eseguire il processo di pulizia WSUS 
Pianificare il processo di pulizia WSUS seguendo questa procedura:   

1.  Nella console di Configuration Manager passare a **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**. 
2. Selezionare il sito al livello superiore della gerarchia di Configuration Manager. 

3.  Fare clic su **Configura componenti del sito** nel gruppo **Impostazioni** , quindi fare clic su **Punto di aggiornamento software** per aprire Proprietà del componente del punto di aggiornamento software.  

4. Esaminare **Comportamento di sostituzione**. Se necessario, modificare il comportamento. 
![Screenshot di Comportamento di sostituzione](media/sccm-supersedence-behavior.PNG)

5.  Fare clic sulla scheda **Regole di sostituzione** e selezionare **Eseguire pulizia guidata WSUS**. Nella versione 1806, l'opzione è stata rinominata **Esegui la pulizia WSUS dopo la sincronizzazione**. 
 
6. Fare clic su **OK**. Se si esegue la versione 1806, fare clic su **Chiudi**.

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportamento del processo di pulizia WSUS nella versione 1802 e precedenti
Nelle versioni precedenti a Configuration Manager versione 1806, l'opzione della pulizia WSUS esegue questo elemento: 
- Opzione **Aggiornamenti scaduti** della pulizia guidata WSUS solo nel server WSUS del sito principale. 
![Screenshot della pulizia WSUS degli aggiornamenti scaduti](media/wsus-cleanup-expired.PNG)

-  Ogni sette giorni viene eseguita una pulizia degli elementi di configurazione degli aggiornamenti software nel database di Configuration Manager e vengono così rimossi gli aggiornamenti non necessari dalla console. 
   - Questa pulizia non rimuoverà dalla console di Configuration Manager gli aggiornamenti scaduti attualmente distribuiti. 

È comunque necessario eseguire operazioni di manutenzione aggiuntive sul database WSUS principale e su tutti gli altri database WSUS nell'ambiente. Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager). 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportamento del processo di pulizia WSUS a partire dalla versione 1806
A partire dalla versione 1806, l'opzione della pulizia WSUS viene eseguita dopo ogni sincronizzazione per questi elementi: <!--1357898 -->
- Opzione **Aggiornamenti scaduti** per i server WSUS nei siti CAS e primari.
    - I server WSUS per i server secondari non eseguono la pulizia WSUS per gli aggiornamenti scaduti. 
- Configuration Manager crea un elenco degli aggiornamenti sostituiti dal proprio database. L'elenco è basato sul comportamento di sostituzione nelle proprietà del componente del punto di aggiornamento software. 
    - Gli elementi di configurazione degli aggiornamenti che soddisfano i criteri del comportamento di sostituzione vengono impostati come scaduti nella console di Configuration Manager.
    - Gli aggiornamenti vengono rifiutati in WSUS per i siti CAS e primari, ma non per i siti secondari.
- Ogni sette giorni viene eseguita una pulizia degli elementi di configurazione degli aggiornamenti software nel database di Configuration Manager e vengono così rimossi gli aggiornamenti non necessari dalla console. 
    - Questa pulizia non rimuoverà dalla console di Configuration Manager gli aggiornamenti scaduti attualmente distribuiti. 

> [!NOTE]
> I mesi di attesa prima della scadenza di un aggiornamento sostituito sono basati sulla data di creazione dell'aggiornamento sostitutivo. Se per questa impostazione si usano 2 mesi, ad esempio, gli aggiornamenti che sono stati sostituiti verranno rifiutati in WSUS e impostati come scaduti in Configuration Manager quando l'aggiornamento sostitutivo risale a 2 mesi prima. 

Nei database WSUS dei siti secondari, tutte le operazioni di manutenzione di WSUS devono essere eseguite manualmente. Nei siti CAS e primari non vengono eseguite le opzioni di **Pulizia server Windows Server Update Services** seguenti:

- Aggiornamenti e revisioni dell'aggiornamento non utilizzati
- Computer non in contatto con il server
- File di aggiornamento non necessari

 Per altre informazioni e istruzioni, vedere il post di blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/) (Guida completa alla manutenzione con Microsoft WSUS e i punti di aggiornamento software di Configuration Manager). 

## <a name="updates-cleanup-log-entries"></a>Voci di log per la pulizia degli aggiornamenti
 
È possibile verificare la pulizia esaminando le voci seguenti in wsyncmgr.log: 
  - Il rifiuto degli aggiornamenti sostituiti in WSUS è completato quando è presente la voce di log `Cleanup processed <number> total updates and declined <number>`
  - È in corso l'avvio della pulizia WSUS quando è presente la voce `Calling WSUS Cleanup.`
  - La pulizia WSUS per gli aggiornamenti scaduti è completata quando è presente la voce `Successfully completed WSUS Cleanup.`
  - La pulizia degli elementi di configurazione degli aggiornamenti scaduti di Configuration Manager è stata avviata quando è presente la voce `Deleting old expired updates...`
  - La pulizia degli elementi di configurazione degli aggiornamenti scaduti di Configuration Manager è completata quando è presente la voce `Deleted <number> expired updates total`
