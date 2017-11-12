---
title: Usare limiti del sito e gruppi di limiti
titleSuffix: Configuration Manager
description: Usare i limiti e i gruppi di limiti per definire percorsi di rete e sistemi del sito accessibili per i dispositivi gestiti.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5980b33cef6e7711e09c3199150bf60008d1a73b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definire i limiti del sito e i gruppi di limiti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I limiti per System Center Configuration Manager definiscono i percorsi di rete nella intranet che possono contenere i dispositivi da gestire. I gruppi di limiti sono gruppi logici di limiti che è possibile configurare.

 Una gerarchia può includere qualsiasi numero di gruppi di limiti e ogni gruppo di limiti può contenere qualsiasi combinazione dei tipi di limite seguenti:  

-   Subnet IP  
-   Nome del sito Active Directory  
-   Prefisso IPv6  
-   Intervallo indirizzi IP  

I client nella intranet valutano il relativo percorso di rete corrente e quindi usano tali informazioni per identificare i gruppi di limiti a cui appartengono.  

 I client usano i gruppi di limiti per:  
-   **Trovare un sito assegnato:** i gruppi di limiti consentono ai client di trovare un sito primario per l'assegnazione client (assegnazione automatica del sito).  
-   **Trovare specifici ruoli del sistema del sito che possono usare:** quando si associa un gruppo di limiti a specifici ruoli del sistema del sito, il gruppo di limiti fornisce ai client l'elenco di sistemi del sito da usare durante la specifica del percorso del contenuto e come punti di gestione preferiti.  

I client in Internet o configurati come client solo per Internet non usano le informazioni relative ai limiti. Questi client non possono usare l'assegnazione automatica del sito e, se il punto di distribuzione è configurato per consentire le connessioni client da Internet, scaricano sempre il contenuto da qualsiasi punto di distribuzione del sito assegnato.  

**Per iniziare:**
- Come prima operazione, [definire i percorsi di rete come limiti](/sccm/core/servers/deploy/configure/boundaries).
- Continuare quindi [configurando gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups) per associare i client presenti in tali limiti ai server del sistema del sito che possono usare.



##  <a name="BKMK_BoundaryBestPractices"></a> Procedure consigliate per i limiti e i gruppi di limiti  

-   **Usare una combinazione del numero minimo di limiti che soddisfano le esigenze:**  
   In passato era consigliabile preferire alcuni tipi di limiti rispetto ad altri. Con le modifiche apportate per migliorare le prestazioni, è ora consigliabile usare il tipo o i tipi di limiti più adatti all'ambiente in uso e il numero più basso possibile di limiti, per semplificare le attività di gestione.      

-   **Evitare la sovrapposizione dei limiti per l'assegnazione automatica del sito:**  
     Anche se ogni gruppo di limiti supporta sia le configurazioni di assegnazione del sito che quelle per il percorso del contenuto, è consigliabile creare un set separato di gruppi di limiti da usare solo per l'assegnazione del sito. Significato: verificare che ogni limite in un gruppo di limiti non sia membro di un altro gruppo di limiti con un'assegnazione del sito diversa. Motivo:  

    -   Un singolo limite può essere incluso in più gruppi di limiti  

    -   Ogni gruppo di limiti può essere associato a un sito primario diverso per l'assegnazione del sito  

    -   Un client in un limite membro di due gruppi di limiti con assegnazioni del sito diverse selezionerà in modo casuale il sito a cui aggiungersi, che potrebbe non corrispondere a quello a cui si intende aggiungere il client.  Questa configurazione è definita a limiti sovrapposti.  

     La sovrapposizione dei limiti non è un problema per il percorso del contenuto e spesso è la configurazione desiderata che fornisce ai client risorse aggiuntive o percorsi del contenuto che possono usare.  
