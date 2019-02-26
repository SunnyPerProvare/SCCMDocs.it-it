---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755434"
---
Usare le definizioni seguenti per distinguere tra pilota e di produzione:  

- **Pilota**: Un subset dei dispositivi che si desidera convalidare prima di distribuire un set più ampio. Utilizzare Desktop Analitica per contrassegnare i dispositivi di proprietà univoci per il gruppo pilota. Dispositivi in una distribuzione pilota sono pronti per eseguire l'aggiornamento quando nessun asset siano bloccate. Un asset di blocco è contrassegnato come *critici* e *Impossibile* per eseguire l'aggiornamento.  

- **Production**: Tutti gli altri dispositivi registrati in Analitica Desktop che non sono in una distribuzione pilota. I dispositivi di produzione sono pronti per l'aggiornamento quando ingaggio sono tutte le risorse. Desktop Analitica conclude automaticamente tutte le risorse non critici.  

