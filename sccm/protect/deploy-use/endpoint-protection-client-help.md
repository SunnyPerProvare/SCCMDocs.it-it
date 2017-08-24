---
title: Guida del client di Endpoint Protection | Microsoft Docs
description: "Informazioni sulle funzionalità e i miglioramenti in Endpoint Protection che consentono una migliore protezione del computer da minacce esterne."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
caps.latest.revision: "6"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 212c73fcb947c3b56da6055bf47fe078301ad90d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-help"></a>Guida del client Endpoint Protection

*Si applica a: System Center Configuration Manager (Current Branch)*


Questa versione di Windows Defender o Endpoint Protection include le funzionalità seguenti per la protezione del computer da eventuali minacce:  

-   **Integrazione con Windows Firewall.** Il programma di installazione di Endpoint Protection consente di attivare o disattivare Windows Firewall.  
-   **Sistema di ispezione di rete.** Con questa funzionalità è possibile migliorare la protezione in tempo reale controllando il traffico di rete per bloccare tempestivamente lo sfruttamento di vulnerabilità note basate sulla rete.  
-   **Motore di protezione.** La protezione in tempo reale consente di trovare il malware e impedirne l'installazione o l'esecuzione nel PC. Il motore aggiornato offre funzionalità avanzate di rilevamento e pulizia che garantiscono prestazioni migliori.  

Windows Defender è incluso nel sistema operativo Windows 10.  Nelle versioni precedenti di Windows, l'amministratore può fornire Windows Defender o Endpoint Protection tramite software di gestione.

È anche disponibile un elenco di [domande frequenti su Windows Defender e su Endpoint Protection](endpoint-protection-client-faq.md). Per informazioni sulla risoluzione dei problemi, vedere [Risoluzione dei problemi di Windows Defender o del client Endpoint Protection](troubleshoot-endpoint-client.md). Per un elenco delle nuove funzionalità, vedere [Novità di Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integrazione con Windows Firewall  
 Windows Firewall può impedire ai pirati informatici o a software dannoso di ottenere accesso al computer tramite Internet o una rete. Al momento dell'installazione di Endpoint Protection, l'installazione guidata verifica ora che Windows Firewall sia attivo. Se Windows Firewall è stato disattivato intenzionalmente, deselezionare l'apposita casella di controllo per evitare di riattivarlo. È possibile modificare le impostazioni di Windows Firewall in qualsiasi momento mediante le impostazioni di Sistema e sicurezza nel Pannello di controllo.  

## <a name="network-inspection-system"></a>Sistema di ispezione di rete  
 Sempre più spesso i pirati informatici sferrano attacchi in rete sfruttando vulnerabilità note prima che i produttori di software riescano a sviluppare e distribuire gli aggiornamenti di sicurezza. Gli studi relativi alle vulnerabilità mostrano che occorre almeno un mese dal momento della segnalazione iniziale dell'attacco prima che un aggiornamento di sicurezza adeguato venga sviluppato, testato e rilasciato. Questa lacuna nella protezione lascia molti computer vulnerabili ad attacchi e sfruttamento delle vulnerabilità per un periodo di tempo considerevole. Il sistema di ispezione di rete interagisce con la protezione in tempo reale per proteggere meglio il computer dagli attacchi in rete riducendo notevolmente l'intervallo di tempo che intercorre tra la divulgazione delle vulnerabilità e la distribuzione dell'aggiornamento da alcune settimane ad alcune ore.  

## <a name="award-winning-protection-engine"></a>Pluripremiato motore di protezione  
 Parte integrante di Windows Defender o Endpoint Protection, il pluripremiato motore di protezione viene aggiornato regolarmente. Il motore è stato sviluppato da un team di ricercatori antimalware del Microsoft Malware Protection Center, il cui compito è fornire risposte alle ultime minacce malware 24 ore al giorno.  

## <a name="windows-defender-settings"></a>Impostazioni di Windows Defender
Le impostazioni di Windows Defender consentono di abilitare le impostazioni per proteggere il PC da software dannoso. L'amministratore può gestire alcune impostazioni di Windows Defender per l'utente. È possibile gestire altre opzioni tramite le impostazioni di Windows Defender. Si consiglia di abilitare le impostazioni di Windows Defender per proteggere il PC e i dati.

Per visualizzare le impostazioni di Windows Defender, cercare `Windows Defender` nel PC. Aprire **Windows Defender** e selezionare **Impostazioni**. Le impostazioni di Windows Defender includono:
- **Protezione in tempo reale** - La protezione in tempo reale consente di trovare il malware e impedirne l'installazione o l'esecuzione nel PC.
- **Protezione basata su cloud** - Windows Defender invia informazioni a Microsoft sulle potenziali minacce per la sicurezza.
- **Invio automatico di file di esempio** - Consentire a Windows Defender di inviare esempi di file sospetti a Microsoft per contribuire a migliorare il rilevamento del malware.
- **Esclusioni** - È possibile esclude file, cartelle, estensioni di file o processi specifici dalla scansione di Windows Defender.
- **Notifiche avanzate** - Abilita le notifiche per ricevere informazioni sull'integrità del PC. Anche se **Disattivato** si riceveranno le notifiche di importanza critica.
- **Windows Defender Offline** - È possibile eseguire Windows Defender Offline per individuare e rimuovere il software dannoso. Questa scansione include il riavvio del PC e richiede circa 15 minuti.

### <a name="see-also"></a>Vedere anche  
 [Domande frequenti relative al client Endpoint Protection](endpoint-protection-client-faq.md)   
 [Troubleshooting Windows Defender or Endpoint Protection client](troubleshoot-endpoint-client.md) (Risoluzione dei problemi di Windows Defender o del client di Endpoint Protection)
