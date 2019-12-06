---
title: Modalità di provisioning
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di provisioning del client durante la sequenza di attività di Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f0e5a313bb5afd0501f0d6027d42b5a51a7e8946
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "69631946"
---
# <a name="provisioning-mode"></a>Modalità di provisioning

*Si applica a: System Center Configuration Manager (Current Branch)*

Durante una sequenza di attività di distribuzione del sistema operativo, Configuration Manager imposta i client in modalità di provisioning. Una sequenza di attività di distribuzione del sistema operativo include un aggiornamento sul posto a Windows 10. In questo stato, il client non elabora criteri del sito. Questo comportamento consente l'esecuzione della sequenza di attività senza il rischio di esecuzione di altre distribuzioni nel client. Quando la sequenza di attività viene completata,con esito positivo o errore gestito, il client esce dalla modalità di provisioning.

Se la sequenza di attività ha esito negativo in modo imprevisto, il client può rimanere in modalità di provisioning, ad esempio se il dispositivo si riavvia nel corso dell'elaborazione della sequenza di attività e non è in grado di riprendere l'elaborazione. I client in questo stato devono essere identificati e ripristinati manualmente da un amministratore.


## <a name="manually-remove-provisioning-mode"></a>Rimuovere manualmente la modalità di provisioning

Se un client viene lasciato in modalità di provisioning, utilizzare questo processo manuale per riportare il client alla modalità di funzionamento normale.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Una delle varie modifiche che esegue questo metodo WMI è l'impostazione di un valore del registro, anche se la semplice modifica del valore del registro non comporta l'uscita completa dalla modalità di provisioning. Se si modifica manualmente il registro, il client può presentare comportamenti imprevisti.  


## <a name="client-provisioning-mode-timeout"></a>Timeout della modalità di provisioning dei client

A partire dalla versione 1902, la sequenza di attività imposta un timestamp quando il client passa in modalità di provisioning. Un client in modalità di provisioning controlla ogni 60 minuti il tempo trascorso dall'impostazione del timestamp. Se è rimasto in modalità di provisioning per più di 48 ore, il client esce automaticamente da tale modalità e riavvia il processo.

48 ore è il valore predefinito del timeout della modalità di provisioning. È possibile regolare questo timer per un dispositivo impostando il valore **ProvisioningMaxMinutes** nella chiave del Registro di sistema seguente: `HKLM\Software\Microsoft\CCM\CcmExec`. Se questo valore non esiste o è pari a `0`, il client usa il valore predefinito di 48 ore.

Il timestamp **ProvisioningEnabledTime** si trova nella chiave del registro di sistema seguente: `HKLM\Software\Microsoft\CCM\CcmExec`. Il timestamp ha un valore dell'ultima volta in cui il computer è entrato in modalità di provisioning. Il formato è Epoch (timestamp Unix) ed è in formato UTC.

Questo timestamp viene anche reimpostato sull'ora corrente quando si posiziona manualmente il computer in modalità di provisioning usando il comando seguente:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Diagrammi di flusso del processo

Questi diagrammi mostrano il flusso del processo per la sequenza di attività e il client.

### <a name="task-sequence"></a>Sequenza di attività

Il diagramma seguente mostra come la sequenza di attività imposta la modalità di provisioning:

![Diagramma di flusso dell'impostazione della modalità di provisioning tramite la sequenza di attività](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Monitoraggio e aggiornamento client

Il diagramma seguente mostra come il client esce dalla modalità di provisioning:

![Diagramma di flusso di uscita dalla modalità di provisioning del client](media/3197824-client-flow.png)


## <a name="see-also"></a>Vedere anche

[Imposta Windows e ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)

[Aggiorna sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)
