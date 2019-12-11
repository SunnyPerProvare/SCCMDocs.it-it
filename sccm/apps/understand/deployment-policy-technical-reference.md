---
title: Riferimento tecnico per i criteri di distribuzione delle applicazioni
titleSuffix: Configuration Manager
description: Riferimento tecnico per la risoluzione dei problemi relativi ai criteri di distribuzione delle applicazioni per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b56a2b5b7ce6e1352bce6323aba0b5f918a2feb0
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74823331"
---
# <a name="application-deployment-policy"></a>Criteri di distribuzione delle applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

## <a name="policy-creation"></a>Creazione dei criteri

Quando si distribuisce un'applicazione, viene creata un'istanza di [SMS_ApplicationAssignment](/sccm/develop/reference/apps/sms_applicationassignment-server-wmi-class) classe che rappresenta l'assegnazione di un'applicazione a una raccolta. Questa attività può essere rilevata in **Smsprov. log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

Nel database di Configuration Manager queste informazioni vengono archiviate nella tabella `CI_CIAssignments`, in cui `AssignmentType` 2 rappresenta la distribuzione di un'applicazione. Quando viene creata l'assegnazione, il componente Monitoraggio database SMS rileva una modifica nella tabella quindi invia una notifica al gestore della replica degli oggetti per elaborare i criteri di assegnazione CI (CIA). Componente Gestione replica oggetti crea quindi i criteri per l'assegnazione dell'applicazione nel database archiviato nella tabella `Policy` nel database e l'ID criterio è basato sull'ID univoco dell'applicazione. Questa attività può essere rilevata in **objreplmgr. log** facendo riferimento all'ID univoco di assegnazione, che può essere ottenuto dalla query SQL a cui si fa riferimento nella sezione [prima di iniziare](/sccm/apps/understand/app-deployment-technical-reference#before-you-begin) .

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

I criteri per l'assegnazione dell'applicazione possono essere visualizzati nel database usando una query SQL simile alla seguente.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Destinazione dei criteri

Dopo la generazione del criterio, il componente provider di criteri assegna questo criterio alle risorse nella raccolta di destinazione della distribuzione dell'applicazione. Le informazioni sulla destinazione dei criteri vengono archiviate nella tabella `ResPolicyMap` del database. È possibile usare il PADBID restituito dalla query precedente per tenere traccia dell'attività in **policypv. log**. Tuttavia, la PADBID registrata nel log potrebbe non corrispondere sempre al PADBID restituito dalla query precedente se vengono elaborati più criteri simultaneamente.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap` tabella non contiene informazioni di destinazione per le applicazioni distribuite come **disponibili** per le raccolte di utenti. Software Center esegue una query su un elenco di queste applicazioni dal punto di gestione e le informazioni di destinazione dei criteri per queste applicazioni vengono generate in modo dinamico quando un utente richiede un'applicazione da software Center.

## <a name="next-steps"></a>Passaggi successivi

- [Distribuzione di applicazioni a raccolte di dispositivi](/sccm/apps/understand/device-deployment-technical-reference)
- [Distribuzione di applicazioni a raccolte di utenti](/sccm/apps/understand/user-deployment-technical-reference)
