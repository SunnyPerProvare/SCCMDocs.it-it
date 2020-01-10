---
title: Riferimento tecnico per la distribuzione di app agli utenti
titleSuffix: Configuration Manager
description: Risoluzione dei problemi relativi alle distribuzioni di applicazioni ai riferimenti tecnici degli utenti per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ef441f8fe85f8d88b71eca13455e0cba5271994
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75817228"
---
# <a name="application-deployment-policy-for-users"></a>Criteri di distribuzione delle applicazioni per gli utenti

*Si applica a: Configuration Manager (Current Branch)*

Quando un'applicazione viene distribuita in una raccolta di utenti, i criteri per la distribuzione vengono creati solo per le distribuzioni richieste. Per le distribuzioni disponibili, i criteri vengono creati quando l'utente tenta di installare l'applicazione da software Center. In questo articolo viene illustrato il processo di distribuzione per le distribuzioni richieste e disponibili.

> [!TIP]
> Tutte le informazioni necessarie per esaminare i log del client possono essere ottenute eseguendo la query SQL a cui viene fatto riferimento nella sezione [prima di iniziare](/sccm/apps/understand/app-deployment-technical-reference#before-you-begin) .

## <a name="required-deployments"></a>Distribuzioni richieste

Il criterio per una distribuzione dell'applicazione richiesta a una raccolta di utenti è destinato a tutti gli utenti nella raccolta al momento della creazione della distribuzione. L'elaborazione sul lato client per queste distribuzioni è simile a una distribuzione richiesta a una raccolta di dispositivi. L'attivazione della distribuzione viene eseguita al momento specificato e l'imposizione si verifica al momento della scadenza definita. Per altre informazioni, vedere [distribuzione di applicazioni a raccolte di dispositivi](/sccm/apps/understand/device-deployment-technical-reference).

## <a name="available-deployments"></a>Distribuzioni disponibili

Le applicazioni distribuite in una raccolta di utenti come disponibili si comportano in modo diverso. Questa modifica del comportamento consente all'amministratore di rendere le applicazioni disponibili agli utenti senza causare conflitti di risorse per i criteri. Quando un utente avvia Software Center, un elenco di applicazioni disponibili per l'utente viene sottoposto a query dal punto di gestione in tempo reale. Questa richiesta viene effettuata al `CMUserService_WindowsAuth` directory virtuale nel punto di gestione e può essere visualizzata nel **SCClient_ [username]. log** nel client.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Quando il punto di gestione riceve questa richiesta, esegue una query sull'elenco di applicazioni disponibili per l'utente eseguendo `usp_GetApplicationPropertyValuesFiltered` stored procedure. Questa attività può essere rilevata in **UserService. log** nel punto di gestione.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Software Center riceve l'elenco e visualizza le applicazioni che l'utente può installare. Quando l'utente fa clic sull'applicazione, viene eseguita una query sulle informazioni aggiuntive sull'applicazione dal punto di gestione, che implica l'esecuzione di stored procedure, ad esempio usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence usp_ GetDeploymentTypeForAnApp e così via.

La distribuzione viene attivata quando l'utente seleziona l'applicazione e fa clic sul pulsante **Installa** e viene creato un processo dell'agente DCM per la valutazione dell'applicazione. Se l'applicazione è applicabile, viene creato un altro processo dell'agente DCM per scaricare e applicare l'applicazione. Questa attività può essere rilevata in **DCMAgent. log** nel client.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui componenti client di distribuzione delle applicazioni](/sccm/apps/understand/client-components-technical-reference)
