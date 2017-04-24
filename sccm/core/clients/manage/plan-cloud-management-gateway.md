---
title: Pianificare il gateway di gestione cloud | Microsoft Docs
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: c61769cc97c320452c9ee27a924cb01480e6f33d
ms.lasthandoff: 03/27/2017

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Pianificare il gateway di gestione cloud in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, il gateway di gestione cloud consente di gestire i client di Configuration Manager su Internet in modo semplice. Il servizio gateway di gestione cloud viene distribuito in Microsoft Azure e richiede una sottoscrizione di Azure. Si connette all'infrastruttura di Configuration Manager locale usando un nuovo ruolo chiamato punto di connessione del gateway di gestione cloud. Dopo che sarà stato completamente distribuito e configurato, i client potranno accedere ai ruoli del sistema del sito di Configuration Manager locale indipendentemente dal fatto che siano connessi alla rete privata interna o su Internet.

Usare la console di Configuration Manager per distribuire il servizio in Azure, aggiungere il ruolo punto di connessione del gateway di gestione cloud e configurare i ruoli del sistema del sito per consentire il traffico del gateway di gestione cloud. Il gateway di gestione cloud supporta attualmente solo i ruoli punto di gestione e punto di aggiornamento software.

Per autenticare i computer e crittografare le comunicazioni tra i diversi livelli di servizio sono necessari certificati client e certificati Secure Socket Layer (SSL). I computer client ricevono in genere un certificato client mediante l'imposizione dei criteri di gruppo. Per crittografare il traffico tra i client e il server di sistema del sito che ospita i ruoli, è necessario creare un certificato SSL personalizzato mediante un'autorità di certificazione. È anche necessario configurare un certificato di gestione in Azure che consente a Configuration Manager di distribuire il servizio gateway di gestione cloud.

## <a name="requirements-for-cloud-management-gateway"></a>Requisiti per il gateway di gestione cloud

-   Computer client e server di sistema del sito che eseguono il punto di connessione del gateway di gestione cloud.

-   Certificati SSL personalizzati dell'autorità di certificazione interna, necessari per crittografare le comunicazioni dai computer client e autenticare l'identità del servizio gateway di gestione cloud.

-   Sottoscrizione di Azure per i servizi cloud.

-   Certificato di gestione di Azure, utilizzato per l'autenticazione di Configuration Manager con Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Specifiche per il gateway di gestione cloud

- Ogni istanza del gateway di gestione cloud supporta 4.000 client.
- È consigliabile creare almeno due istanze del gateway di gestione cloud per aumentare la disponibilità.
- Il gateway di gestione cloud supporta solo i ruoli punto di gestione e punto di aggiornamento software.
-   Le funzionalità seguenti in Configuration Manager non sono attualmente supportate dal gateway di gestione cloud:

    -   Distribuzione client
    -   Assegnazione automatica al sito
    -   Criteri utente
    -   Catalogo applicazioni, incluse le richieste di approvazione software
    -   Distribuzione completa del sistema operativo
    -   Console di Configuration Manager
    -   Strumenti remoti
    -   Sito Web di Reporting
    -   Riattivazione LAN
    -   Client Mac, Linux e UNIX
    -   Azure Resource Manager
    -   Peer cache
    -   Gestione dei dispositivi mobili (MDM) locale

## <a name="cost-of-cloud-management-gateway"></a>Costo del gateway di gestione cloud

>[!IMPORTANT]
>Le informazioni sui costi specificate di seguito sono puramente stime. Altre variabili di ambiente possono influire sul costo complessivo dell'uso del gateway di gestione cloud.

Il gateway di gestione cloud usa le funzionalità di Microsoft Azure seguenti, che vengono addebitate all'account di sottoscrizione di Azure:

-   Macchina virtuale

    -   Per il gateway di gestione cloud è attualmente necessaria una macchina virtuale Standard\_A2. Quando si crea il servizio, è possibile selezionare il numero di macchine virtuali necessarie per supportare il servizio. Uno è il valore predefinito.

    -   Per una stima, supporre che una sola macchina virtuale Azure Standard\_A2 possa supportare circa 2000 client simultanei basati su Internet .

    -   Vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/en-us/pricing/calculator/) per determinare i costi potenziali.

      >[!NOTE]
      >I costi delle macchine virtuali variano a seconda dell'area.

-   Trasferimento dati in uscita

    -   Il flusso dati non compreso nel servizio viene addebitato. Vedere i [dettagli sui prezzi per la larghezza di banda di Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) per determinare i costi potenziali.

    -   Per una stima, supporre circa 100 MB per client/mese per client basati su Internet che eseguono l'aggiornamento dei criteri ogni ora.

    >[!NOTE]
    > Se vengono eseguite altre azioni supportate tramite il gateway di gestione cloud, ad esempio la distribuzione di aggiornamenti software o di applicazioni, il trasferimento dei dati in uscita da Azure aumenta.

-   Archivio del contenuto

    -   I client basati su Internet che sono gestiti con il gateway di gestione cloud ottengono contenuto di aggiornamento software da Windows Update senza nessun addebito.

    -   Altri contenuti necessari, ad esempio le applicazioni, devono essere distribuiti in un punto di distribuzione basato sul cloud. Il gateway di gestione cloud supporta attualmente solo il punto di distribuzione cloud per l'invio di contenuto a client.

    - Per altri dettagli, vedere il costo di utilizzo di una [distribuzione basata sul cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).

## <a name="next-steps"></a>Passaggi successivi

[Configurare il gateway di gestione cloud](setup-cloud-management-gateway.md)

