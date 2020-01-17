---
title: Codici di non conformità
titleSuffix: Configuration Manager
description: Riferimento tecnico per i codici possibili di un client Configuration Manager non conforme ai criteri di BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e8b94a66cce2a6e8b4c5cc14e23ce8b8cdd655c
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75818979"
---
# <a name="non-compliance-codes"></a>Codici di non conformità

*Si applica a: Configuration Manager (Current Branch)*

<!--3601034-->

WMI sul client fornisce i codici non di conformità seguenti. Vengono inoltre descritti i motivi per cui un determinato dispositivo segnala come non conforme.

Sono disponibili diversi metodi per la visualizzazione di WMI. Ad esempio, usare il seguente comando di PowerShell:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Se il dispositivo è conforme, questo comando non restituisce alcun valore.
>
> È anche possibile controllare l'attributo `Compliant` di questa classe, che è `1` se il dispositivo è conforme.

|Codice di non conformità|Motivo della mancata conformità|
|--- |--- |
|0|Livello di codifica non AES 256.|
|1|Per i criteri di BitLocker è necessario crittografare il volume, ma non lo è.|
|2|Per i criteri di BitLocker è necessario che il volume *non* sia crittografato, ma è.|
|3|I criteri di BitLocker richiedono che questo volume usi una protezione TPM, ma non lo è.|
|4|I criteri di BitLocker richiedono che questo volume usi una protezione TPM e PIN, ma non lo è.|
|5|I criteri di BitLocker non consentono ai computer non TPM di creare report conformi.|
|6|Il volume ha una protezione TPM, ma il TPM non è visibile.|
|7|I criteri di BitLocker richiedono che questo volume usi una protezione con password, ma non ne ha uno.|
|8|I criteri di BitLocker richiedono che questo volume *non* usi una protezione con password, ma ne includa uno.|
|9|I criteri di BitLocker richiedono che questo volume usi una protezione di sblocco automatico, ma non ne è presente uno.|
|10|I criteri di BitLocker richiedono che questo volume *non* usi una protezione di sblocco automatico, ma ne includa uno.|
|11|BitLocker rileva un conflitto di criteri che impedisce la segnalazione del volume come conforme.|
|12|Un volume di sistema è necessario per crittografare il volume del sistema operativo, ma non è presente.|
|13|La protezione viene sospesa per il volume.|
|14|La protezione sblocco automatico non è sicura a meno che il volume del sistema operativo non sia crittografato.|
|15|Il criterio richiede un livello di crittografia minimo è XTS-AES-128 bit, il livello di crittografia effettivo è più vulnerabile.|
|16|Il criterio richiede un livello di crittografia minimo è XTS-AES-256 bit, il livello di crittografia effettivo è più vulnerabile.|
