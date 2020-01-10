---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 5735d2662bd04293e083f52ed19d371da6b8a212
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75791647"
---
Usare le definizioni seguenti per distinguere tra pilota e produzione:  

- **Pilota**: un subset di dispositivi da convalidare prima di procedere alla distribuzione in un set più ampio. Usare Desktop Analytics per contrassegnare i dispositivi come univoci per il set pilota. I dispositivi nel set pilota sono pronti per l'aggiornamento quando non sono presenti asset bloccanti. Un asset bloccante è contrassegnato come *critico* e *non idoneo* per l'aggiornamento.  

- **Production**: tutti gli altri dispositivi registrati in Desktop Analytics che non sono inclusi nel set pilota. I dispositivi di produzione sono pronti per l'aggiornamento quando tutti gli asset sono approvati. Desktop Analytics approva automaticamente tutti gli asset non critici.  

