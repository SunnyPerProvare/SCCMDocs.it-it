---
title: Strumento Content Library Transfer
titleSuffix: Configuration Manager
description: Usare lo strumento Content Library Transfer per trasferire il contenuto da un'unità disco a un'altra in un punto di distribuzione di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5331443febeaf7f25cc5f37557abeed407e85ec3
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826068"
---
# <a name="content-library-transfer-tool"></a>Strumento Content Library Transfer

*Si applica a: Configuration Manager (Current Branch)*

Lo strumento Content Library Transfer è uno degli [strumenti di Configuration Manager](/sccm/core/support/tools). Trasferisce il contenuto da un'unità disco a un'altra. Lo strumento è progettato per l'esecuzione nei sistemi del sito del punto di distribuzione. Supporta i punti di distribuzione con il percorso condiviso con un sito o con i sistemi del sito remoto.  

Lo strumento è utile per lo scenario in cui l'unità disco che ospita la raccolta contenuto è piena. Prima di tutto aggiungere o identificare un altro disco rigido con spazio sufficiente per ospitare la raccolta contenuto. Usare quindi **ContentLibraryTransfer.exe** per trasferire il contenuto dal precedente disco rigido pieno alla nuova unità vuota.
 
Al termine del trasferimento, il contenuto è accessibile ai computer client dalla nuova posizione.



## <a name="usage"></a>Utilizzo 

Eseguire **ContentLibraryTransfer.exe** come utente con autorizzazioni amministrative per il punto di distribuzione. 

#### <a name="syntax"></a>Sintassi 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Esempio
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitazioni

- Eseguire lo strumento in locale nel punto di distribuzione. Non è possibile eseguirlo da un computer remoto.  

- Usarlo solo quando i client non accedono attivamente al punto di distribuzione. Se si esegue lo strumento mentre i client accedono al contenuto, la raccolta contenuto nell'unità di destinazione potrebbe avere dati incompleti. Il trasferimento dei dati potrebbe non riuscire del tutto, rendendo inutilizzabile una raccolta contenuto.  

- Non distribuire il contenuto al punto di distribuzione quando si esegue lo strumento. Se si esegue lo strumento mentre è in corso la scrittura del contenuto nel punto di distribuzione, la raccolta contenuto nell'unità di destinazione potrebbe avere dati incompleti. Il trasferimento dei dati potrebbe non riuscire del tutto, rendendo inutilizzabile una raccolta contenuto.



## <a name="see-also"></a>Vedere anche

- [Concetti di base sulla gestione dei contenuti](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Raccolta contenuto](/sccm/core/plan-design/hierarchy/the-content-library)
