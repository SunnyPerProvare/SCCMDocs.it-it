---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: d874997f26c9fcb690733d4eac9b6b4f1df8f752
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75805763"
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
