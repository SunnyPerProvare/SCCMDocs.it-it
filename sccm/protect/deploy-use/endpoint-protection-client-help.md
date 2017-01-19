---
title: Guida del client di Endpoint Protection | Microsoft Docs
description: "Informazioni sulle funzionalità e i miglioramenti in Endpoint Protection che consentono una migliore protezione del computer da minacce esterne."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
caps.latest.revision: 6
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 870aa9766c995a5c8858b9a8c9a5537cd5f82840


---
# <a name="endpoint-protection-client-help"></a>Guida del client Endpoint Protection

*Si applica a: System Center Configuration Manager (Current Branch)*


Questa versione di Endpoint Protection include le funzionalità seguenti per proteggere meglio il computer da eventuali minacce:  

-   **Integrazione con Windows Firewall.** Il programma di installazione di Endpoint Protection consente di attivare o disattivare Windows Firewall.  

-   **Sistema di ispezione di rete.** Con questa funzionalità è possibile migliorare la protezione in tempo reale controllando il traffico di rete per bloccare tempestivamente lo sfruttamento di vulnerabilità note basate sulla rete.  

-   **Motore di protezione.** Il motore aggiornato offre funzionalità avanzate di rilevamento e pulizia che garantiscono prestazioni migliori.  

 Queste funzionalità sono descritte più dettagliatamente nelle sezioni seguenti.  

## <a name="windows-firewall-integration"></a>Integrazione con Windows Firewall  
 Windows Firewall può impedire ai pirati informatici o a software dannoso di ottenere accesso al computer tramite Internet o una rete. Al momento dell'installazione di Endpoint Protection, l'installazione guidata verifica ora che Windows Firewall sia attivo. Se Windows Firewall è stato disattivato intenzionalmente, deselezionare l'apposita casella di controllo per evitare di riattivarlo. È possibile modificare le impostazioni di Windows Firewall in qualsiasi momento mediante le impostazioni di Sistema e sicurezza nel Pannello di controllo.  

## <a name="network-inspection-system"></a>Sistema di ispezione di rete  
 Sempre più spesso i pirati informatici sferrano attacchi in rete sfruttando vulnerabilità note prima che i produttori di software riescano a sviluppare e distribuire gli aggiornamenti di sicurezza. Gli studi relativi alle vulnerabilità mostrano che occorre almeno un mese dal momento della segnalazione iniziale dell'attacco prima che un aggiornamento di sicurezza adeguato venga sviluppato, testato e rilasciato. Questa lacuna nella protezione lascia molti computer vulnerabili ad attacchi e sfruttamento delle vulnerabilità per un periodo di tempo considerevole. Il sistema di ispezione di rete interagisce con la protezione in tempo reale per proteggere meglio il computer dagli attacchi in rete riducendo notevolmente l'intervallo di tempo che intercorre tra la divulgazione delle vulnerabilità e la distribuzione dell'aggiornamento da alcune settimane ad alcune ore.  

## <a name="award-winning-protection-engine"></a>Pluripremiato motore di protezione  
 Parte integrante di Endpoint Protection, il pluripremiato motore di protezione viene aggiornato regolarmente. Il motore è stato sviluppato da un team di ricercatori antimalware del Microsoft Malware Protection Center, il cui compito è fornire risposte alle ultime minacce malware 24 ore al giorno.  

### <a name="see-also"></a>Vedere anche  
 [Domande frequenti relative al client di Endpoint Protection](endpoint-protection-client-faq.md)   

 [Troubleshooting Windows Defender or Endpoint Protection client](troubleshoot-endpoint-client.md) (Risoluzione dei problemi di Windows Defender o del client di Endpoint Protection)



<!--HONumber=Dec16_HO3-->


