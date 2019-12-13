---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62231898"
---
Usare le definizioni seguenti per distinguere tra pilota e produzione:  

- **Pilota**: un subset di dispositivi da convalidare prima di procedere alla distribuzione in un set più ampio. Usare Desktop Analytics per contrassegnare i dispositivi come univoci per il set pilota. I dispositivi nel set pilota sono pronti per l'aggiornamento quando non sono presenti asset bloccanti. Un asset bloccante è contrassegnato come *critico* e *non idoneo* per l'aggiornamento.  

- **Production**: tutti gli altri dispositivi registrati in Desktop Analytics che non sono inclusi nel set pilota. I dispositivi di produzione sono pronti per l'aggiornamento quando tutti gli asset sono approvati. Desktop Analytics approva automaticamente tutti gli asset non critici.  

