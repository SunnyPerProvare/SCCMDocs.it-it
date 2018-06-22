---
title: Associare gli utenti a un computer di destinazione
titleSuffix: Configuration Manager
description: Configurare System Center Configuration Manager per associare gli utenti ai computer di destinazione quando si distribuiscono sistemi operativi.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a4065b0e6774160efb6be22fe2ec8268c60d6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347587"
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Associare gli utenti a un computer di destinazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si utilizza System Center Configuration Manager per la distribuzione del sistema operativo, è possibile associare gli utenti al computer di destinazione in cui viene distribuito il sistema operativo. Questa configurazione include i seguenti punti:  

-   Che un singolo utente sia l'utente primario del computer di destinazione.  

-   Che più utenti siano gli utenti primari del computer di destinazione.  

 L'affinità utente dispositivo supporta la gestione incentrata sull'utente durante la distribuzione delle applicazioni. Quando si associa un utente al computer di destinazione in cui viene installato un sistema operativo, successivamente è possibile distribuire le applicazioni all'utente associato e le applicazioni verranno installate automaticamente nel computer di destinazione. Tuttavia, nonostante sia possibile configurare il supporto per l'affinità utente dispositivo durante la distribuzione dei sistemi operativi, non è possibile utilizzare l'affinità utente dispositivo per la distribuzione dei sistemi operativi.  

 Per altre informazioni sull'affinità utente dispositivo, vedere l'argomento [Link users and devices with user device affinity in System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) (Collegare utenti e dispositivi con l'affinità utente dispositivo in System Center Configuration Manager).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Come specificare un utente durante la distribuzione dei sistemi operativi  
 Nella seguente tabella sono elencate le azioni che consentono di integrare l'affinità utente dispositivo nelle distribuzioni del sistema operativo. È possibile integrare l'affinità utente-dispositivo nelle distribuzioni PXE, nelle distribuzioni dei supporti di avvio e nelle distribuzioni dei supporti pre-installati.  

|Action|Altre informazioni|  
|------------|----------------------|  
|Creare una sequenza attività che includa la variabile **SMSTSAssignUsersMode**|Aggiungere la variabile **SMSTSAssignUsersMode** all'inizio della sequenza di attività usando il passaggio della sequenza di attività  [Set Task Sequence Variable](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) . Questa variabile specifica la modalità di gestione delle informazioni utente da parte della sequenza attività.<br /><br /> Impostare la variabile su uno dei seguenti valori:<br /><br /> <br /><br /> **Automatica**: la sequenza attività crea automaticamente una relazione tra l'utente e il computer di destinazione, quindi distribuisce il sistema operativo.<br /><br /> **In sospeso**: la sequenza attività crea una relazione tra l'utente e il computer di destinazione, ma attende l'approvazione dell'utente amministratore prima di distribuire il sistema operativo.<br /><br /> **Disattivata**: la sequenza attività non associa un utente al computer di destinazione e continua a distribuire il sistema operativo.<br /><br /> <br /><br /> È inoltre possibile impostare la variabile su un computer o una raccolta. Per altre informazioni sulle variabili predefinite, vedere [Task sequence built-in variables](../../osd/understand/task-sequence-built-in-variables.md) (Variabili predefinite della sequenza di attività).|  
|Creare un comando di preavvio che raccoglie le informazioni utente|Il comando di preavvio può essere uno script di Visual Basic (VB) con una casella di input oppure un'applicazione HTML (HTA) che convalida i dati utente immessi.<br /><br /> Il comando di preavvio deve impostare la variabile **SMSTSUdaUsers** utilizzata durante l'esecuzione della sequenza attività. Questa variabile può essere impostata su un computer, una raccolta o una variabile della sequenza attività. Quando si aggiungono più utenti, usare il seguente formato: *dominio\utente1, dominio\utente2, dominio\utente3*.|  
|Configurare la modalità di associazione dell'utente al computer di destinazione utilizzata da punti di distribuzione e supporti|Quando la [configurazione di un punto di distribuzione prevede l'accettazione delle richieste di avvio PXE](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) e quando si creano [supporti di avvio](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) o [supporti pre-installati](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) usando la Creazione guidata del supporto per la sequenza di attività, è possibile specificare la modalità di supporto dell'associazione degli utenti al computer di destinazione in cui viene distribuito il sistema operativo da parte del punto di distribuzione o del supporto.<br /><br /> La configurazione del supporto per l'affinità utente dispositivo non dispone di un metodo integrato per la convalida dell'identità utente. Questo elemento può essere importante quando un tecnico che esegue il provisioning del computer immette le informazioni per conto dell'utente. Oltre a impostare la modalità di gestione delle informazioni utente da parte della sequenza di attività, la configurazione di queste opzioni nel punto di distribuzione e nel supporto consente di limitare le distribuzioni avviate da un avvio PXE o da un tipo di supporto specifico.|  
