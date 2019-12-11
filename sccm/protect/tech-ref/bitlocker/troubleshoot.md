---
title: Risolvere i problemi relativi a BitLocker
titleSuffix: Configuration Manager
description: Informazioni su come risolvere i problemi relativi alla gestione di BitLocker in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bd379017be114a9599f9519b3cb56ee0c3f22470
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662319"
---
# <a name="troubleshoot-bitlocker"></a>Risolvere i problemi relativi a BitLocker

*Si applica a: Configuration Manager (Current Branch)*

Utilizzare le informazioni contenute in questo articolo per risolvere i problemi relativi alla gestione di BitLocker in Configuration Manager.

## <a name="server-error-in-self-service"></a>Errore del server in self-service

Quando si tenta di aprire il portale self-service (`https://webserver.contoso.com/SelfService`) per la prima volta, viene visualizzato il messaggio di errore seguente:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Per risolvere questo problema, assicurarsi di aver installato il [prerequisito](/configmgr/protect/plan-design/bitlocker-management#prerequisites) per **Microsoft ASP.NET MVC 4,0** sul server Web.

## <a name="see-also"></a>Vedere anche

Per ulteriori informazioni sull'utilizzo dei registri eventi di BitLocker, vedere [log eventi di BitLocker](/configmgr/protect/tech-ref/bitlocker/about-event-logs).

Per un elenco degli errori noti e delle possibili cause per le voci del registro eventi, vedere gli articoli seguenti:

- [Registri eventi del client](/configmgr/protect/tech-ref/bitlocker/client-event-logs)
- [Registri eventi del server](/configmgr/protect/tech-ref/bitlocker/server-event-logs)

Per comprendere il motivo per cui i client inviano report non conformi ai criteri di gestione di BitLocker, vedere [codici non di conformità](/configmgr/protect/tech-ref/bitlocker/non-compliance-codes).
