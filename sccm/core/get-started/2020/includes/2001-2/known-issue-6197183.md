---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: bc4f8e172481af267548a4453748a46120e25fde
ms.sourcegitcommit: 36920d640a322ed44e34fb5bbc5027c66633bd72
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/04/2020
ms.locfileid: "76978716"
---
### <a name="ki_coll"></a> Non è possibile creare o modificare alcune raccolte

<!--6197183-->
In questa versione del ramo Technical Preview non è possibile creare una nuova raccolta. Non è inoltre possibile modificare le proprietà di una raccolta di utenti esistente.

Per risolvere questo problema, usare i cmdlet di PowerShell di Configuration Manager per creare nuove raccolte e modificare le raccolte di utenti esistenti. Di seguito sono riportati alcuni dei cmdlet disponibili per la gestione delle raccolte:

- [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)
