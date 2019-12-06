---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 10/04/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7d24b4032f893cfbbb347a1d0a37090f308c365
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "71975520"
---
### <a name="ki_hinv"></a> Report sull'inventario hardware

<!--5468413-->
Se si tenta di eseguire un report che si basa sull'inventario hardware, viene restituito un errore. Un report di BitLocker restituisce ad esempio un errore simile al messaggio seguente:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

È anche possibile che venga visualizzato l'errore seguente nel file **dataldr.log**:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Potrebbero essere interessati anche i dashboard della console che si basano sull'inventario hardware.

Questo problema è dovuto a una modifica dello schema del database nelle tabelle specifiche sull'inventario hardware.

#### <a name="workaround"></a>Soluzione alternativa

La soluzione alternativa consiste nell'eliminare l'attributo preesistente dal database. Il componente del sito del caricatore dati può quindi creare un nuovo attributo. Eseguire lo script SQL seguente nel server di database del sito per correggere lo schema della tabella:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
